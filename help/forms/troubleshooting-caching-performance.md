---
title: Hur felsöker vi cachningsrelaterade problem för AEM Forms as a Cloud Service?
description: Felsöka problem med cachelagring för AEM Forms as a Cloud Service.
contentOwner: khsingh
feature: Adaptive Forms, Troubleshooting
role: User
exl-id: eae44a6f-25b4-46e9-b38b-5cec57b6772c
source-git-commit: 527c9944929c28a0ef7f3e617ef6185bfed0d536
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 0%

---

# Cacheprestanda {#caching-performance}

Följande problem kan uppstå när du konfigurerar eller använder Adaptiv Forms-cache i en Cloud Service-miljö:

## En del anpassningsbara Forms som innehåller bilder eller videor ogiltigförklaras inte automatiskt från Dispatcher-cachen {#images-videos-not-invalidated}

Du kan välja och lägga till bilder eller videoklipp från en filläsare i ett anpassat formulär. När dessa bilder redigeras i Resursredigeraren blir den cachelagrade versionen av ett adaptivt formulär som innehåller sådana bilder inte ogiltig. Det adaptiva formuläret fortsätter att visa äldre bilder.

För att lösa problemet måste du efter att ha publicerat bilder och video uttryckligen avpublicera och publicera den adaptiva Forms som refererar till dessa resurser.

## En del anpassningsbara Forms som innehåller innehållsfragment eller Experience Fragments ogiltigförklaras inte automatiskt från Dispatcher-cachen {#content-fragments-experience-fragments-not-invalidated}

Du kan lägga till ett innehålls- eller upplevelsefragment i ett anpassat formulär. När dessa fragment redigeras och publiceras separat blir den cachelagrade versionen av ett adaptivt formulär som innehåller sådana fragment inte ogiltig. Det adaptiva formuläret fortsätter att visa äldre fragment.

För att lösa problemet måste du efter publicering av uppdaterat innehållsfragment eller Experience Fragment uttryckligen avpublicera och publicera den adaptiva Forms som använder dessa resurser.

## Endast första instansen av Adaptive Forms cachelagras {#only-first-instance-cached}

När URL:en för det adaptiva formuläret inte innehåller någon lokaliseringsinformation och alternativet Använd webbläsarens språkområde i konfigurationshanteraren är aktiverat, skickas en lokaliserad version av det adaptiva formuläret och en instans av det adaptiva formuläret, baserat på den första begäran (webbläsarens språkområde begärs), cachelagras och skickas till alla efterföljande användare.

Utför följande steg för att lösa problemet:

1. Öppna ditt Experience Manager-projekt.
1. Öppna `dispatcher/scr/conf.d/rewrites/rewrite.rules` för redigering.
1. Öppna `conf.d/httpd-dispatcher.conf` eller någon annan konfigurationsfil som är konfigurerad att läsas in vid körning.
1. Lägg till följande kod i filen och spara den. Det är en exempelkod som ändrar den så att den passar din miljö.

```shellscript
    # Handle actual URL convention (just pass through)
    RewriteRule "^/content/forms/af/(.*)[.](.*).html$" "/content/forms/af/$1.$2.html" [PT]
    
    # Handle selector-based redirection based on browser language
    <VirtualHost *:80>
            # Handle actual URL convention (just pass through)
    RewriteRule "^/content/forms/af/(.*)[.](.*).html$" "/content/forms/af/$1.$2.html" [PT]

    # Handle selector based redirection basded on browser language
    # The Rewrite Condition is looking for the Accept-Language header and if found takes the first two characters which most likely are the desired language selector.
    RewriteCond %{HTTP:Accept-Language} ^(..).*$ [NC]
    RewriteRule "^/content/forms/af/(.*).html$" "/content/forms/af/$1.%1.html" [R]
    RewriteRule "^/content/forms/af/(.*).html$" "/content/forms/af/$1.%1.html" [R]
```

## CDN-cachning slutar fungera efter 300 sekunder {#cdn-caching-stops-working-after-300-seconds}

CDN-cachning slutar fungera efter 300 sekunder och alla begäranden om cachning i CDN omdirigeras till Dispatcher.

Lös problemet genom att ange sidhuvudet 0:

1. Skapa en fil på `src\conf.d\available_vhosts`

1. Lägg till följande i filen för att ange sidhuvudet

   ```shellscript
       <IfModule mod_headers.c>
               Header add X-Vhost "publish"
               Header set age 0
       </IfModule>
   ```

1. Spara och stäng filen.
1. Ändra den mjuka länken för `src\conf.d\enabled_vhosts\default.vhost` för att peka på en ny fil.

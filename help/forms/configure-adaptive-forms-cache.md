---
title: Vad är cacheminne för anpassningsbara formulär? och hur man cache-lagrar ett AEM anpassat formulär?
description: Anpassningsbart Forms-cacheminne är utformat för adaptiva Forms och dokument med målet att minska den tid som krävs för att återge ett adaptivt formulär eller dokument.
uuid: ba8f79fd-d8dc-4863-bc0d-7c642c45505c
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 9fa6f761-58ca-4cd0-8992-b9337dc1a279
source-git-commit: 5e02cf36112ce29cd3ebfd772623654328598bf2
workflow-type: tm+mt
source-wordcount: '919'
ht-degree: 0%

---


# Konfigurera anpassad Forms-cache {#configure-adaptive-forms-cache}

Ett cacheminne är en mekanism som förkortar dataåtkomsttider, minskar latensen och förbättrar I/O-hastigheter (input/output). I adaptiv Forms-cache lagras endast HTML-innehåll och JSON-struktur i ett adaptivt formulär utan att några förfyllda data sparas. Det minskar tiden som krävs för att återge ett adaptivt formulär på klienten. Det är särskilt utformat för Adaptiv Forms.

## Konfigurera anpassad Forms-cache vid författare och publiceringsinstanser {#configure-adaptive-forms-caching-at-author-and-publish-instances}

1. Gå AEM webbkonsolens konfigurationshanterare på `https://[server]:[port]/system/console/configMgr`.
1. Klicka på **[!UICONTROL Adaptive Form and Interactive Communication Web Channel Configuration]** om du vill redigera dess konfigurationsvärden.
1. I dialogrutan [!UICONTROL edit configuration values] anger du det maximala antalet formulär, eller dokument som en instans av AEM [!DNL Forms Server] kan cachelagra i fältet **[!UICONTROL Number of Adaptive Forms]**. Standardvärdet är 100.

   >[!NOTE]
   >
   >Om du vill inaktivera cachen anger du värdet **0** i fältet Antal adaptiva Forms. Cacheminnet återställs och alla formulär och dokument tas bort från cacheminnet när du inaktiverar eller ändrar cachekonfigurationen.

   ![Dialogrutan Konfiguration för adaptiv Forms-cache](assets/cache-configuration-edit.png)

1. Klicka på **[!UICONTROL Save]** för att spara konfigurationen.

Miljön är konfigurerad att använda cacheanpassad Forms och relaterade resurser.


## (Valfritt) Konfigurera cacheminne för adaptiva formulär på Dispatcher {#configure-the-cache}

Du kan också konfigurera Adaptiv formulärcache-lagring på Dispatcher för ytterligare prestandaförbättringar.

### Krav {#pre-requisites}

* Aktivera alternativet [sammanfogning eller förifyllning av data på klienten](prepopulate-adaptive-form-fields.md#prefill-at-client). Det hjälper till att sammanfoga unika data för varje instans av ett förfyllt formulär.
* [Aktivera en rensningsagent för varje publiceringsinstans](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/page-invalidate.html?lang=en#invalidating-dispatcher-cache-from-a-publishing-instance). Det ger bättre cachningsprestanda för Adaptive Forms. Standardwebbadressen för rensningsagenter är `http://[server]:[port]]/etc/replication/agents.publish/flush.html`.

### Att tänka på vid cachelagring av Adaptiv Forms på en Dispatcher {#considerations}

* När du använder det adaptiva Forms-cacheminnet använder du AEM [!DNL Dispatcher] för att cachelagra klientbibliotek (CSS och JavaScript) i ett adaptivt formulär.
* När du utvecklar anpassade komponenter ska du på den server som används för utveckling inaktivera den adaptiva Forms-cachen.
* URL:er utan tillägg cachelagras inte. URL:er med mönstret `/content/forms/[folder-structure]/[form-name].html` cachelagras till exempel, och cachelagring ignorerar URL:er med mönstret `/content/dam/formsanddocument/[folder-name]/<form-name>/jcr:content`. Använd URL:er med tillägg för att utnyttja fördelarna med cachning.
* Överväganden för lokaliserade adaptiva Forms:
   * Använd URL-formatet `http://host:port/content/forms/af/<afName>.<locale>.html` för att begära en lokaliserad version av ett adaptivt formulär i stället för `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`
   * Inaktivera användning av webbläsarens språkområde <!-- [Disable using browser locale](supporting-new-language-localization.md#how-localization-of-adaptive-form-works) --> för URL:er med formatet `http://host:port/content/forms/af/<adaptivefName>.html`.
   * När du använder URL-formatet `http://host:port/content/forms/af/<adaptivefName>.html`, och **[!UICONTROL Use Browser Locale]** i konfigurationshanteraren är inaktiverat, används den icke-lokaliserade versionen av det adaptiva formuläret. Det icke-lokaliserade språket är det språk som används vid utvecklingen av det adaptiva formuläret. Det språk som är konfigurerat för webbläsaren (webbläsarens språkområde) beaktas inte och en icke-lokaliserad version av det anpassade formuläret används.
   * När du använder URL-formatet `http://host:port/content/forms/af/<adaptivefName>.html`, och **[!UICONTROL Use Browser Locale]** i konfigurationshanteraren är aktiverat, visas en lokaliserad version av det adaptiva formuläret, om en sådan finns. Språket i det lokaliserade adaptiva formuläret baseras på det språk som är konfigurerat för webbläsaren (webbläsarens språkområde). Det kan leda till [cachelagring av endast den första instansen av ett adaptivt formulär]. Information om hur du förhindrar att problemet inträffar på din instans finns i [felsökning](#only-first-insatnce-of-adptive-forms-is-cached).

### Aktivera cachelagring på Dispatcher

Följ stegen nedan för att aktivera och konfigurera cachelagring av Adaptiv Forms i Dispatcher:

1. Öppna följande URL för varje publiceringsinstans i miljön och konfigurera replikeringsagenten:
   `http://[server]:[port]]/etc/replication/agents.publish/flush.html`

1. [Lägg till följande i din dispatcher.vilken fil som helst](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#automatically-invalidating-cached-files):

   ```JSON
      /invalidate
      {
      /0000
      {
      /glob "*"
      /type "deny"
      }
      /0001
      {
      # Consider all HTML files stale after an activation.
      /glob "*.html"
      /type "allow"
      }
      /0002
      {
      # Exclude htmls present in AF directories
      /glob "/content/forms/**/*.html"
      /type "deny"
      }
   ```

   När du lägger till ovanstående:

   * Ett anpassat formulär finns kvar i cachen tills en uppdaterad version av formuläret inte publiceras.

   * När en nyare version av en resurs som refereras i ett adaptivt formulär publiceras blir den adaptiva formen automatiskt ogiltig. Det finns några undantag för automatisk ogiltigförklaring av refererade resurser. Du hittar mer information om undantag i avsnittet [felsökning](#troubleshooting).
1. [Lägg till nedanstående regeldispatcher.vilken eller vilken anpassad regelfil som helst](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#specifying-the-documents-to-cache). URL:er som inte stöder cachelagring utesluts. Interaktiv kommunikation.

   ```JSON
      /0000 {
            /glob "*"
            /type "allow"
      }
      ## Don't cache csrf login tokens
      /0001 {
            /glob "/libs/granite/csrf/token.json"
            /type "deny"
      }
      ## Don't cache IC - print channel
      /0002 {
            /glob "/content/forms/**/channels/print.html"
            /type "deny"
      }
      ## Don't cache IC - web channel
      /0003 {
            /glob "/content/forms/**/channels/web.html"
            /type "deny"
      }
   ```

1. [Lägg till följande parametrar i listan över ignorerade URL-parametrar](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#ignoring-url-parameters):

   ```JSON
      /ignoreUrlParams {
      /0001 { /glob "*" /type "deny" }
      # added for AEM forms specific use cases.
      /0003 { /glob "dataRef" /type "allow" }
      }
   ```

Din AEM är konfigurerad att cachelagra Adaptiv Forms. Den cachelagrar alla typer av adaptiva Forms. Om du behöver kontrollera användaråtkomstbehörighet för en sida innan du levererar den cachelagrade sidan läser du [cachelagra skyddat innehåll](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/permissions-cache.html).

## Felsökning {#troubleshooting}

### En del anpassningsbara Forms som innehåller bilder eller videor ogiltigförklaras inte automatiskt från Dispatcher cache {#videos-or-images-not-auto-invalidated}

#### Problem {#issue1}

När du markerar och lägger till bilder eller videoklipp via en filläsare i ett adaptivt formulär, och de redigeras i Assets redigerare, blir sådana resurser inte automatiskt ogiltiga från Dispatcher-cachen.

#### Lösning {#Solution1}

När du har publicerat bilder och video avpublicerar och publicerar du den adaptiva Forms som refererar till dessa resurser.

### En del anpassningsbara Forms som innehåller innehållsfragment eller upplevelsefragment ogiltigförklaras inte automatiskt från Dispatcher cache {#content-or-experience-fragment-not-auto-invalidated}

#### Problem {#issue2}

När du lägger till ett innehållsfragment eller en Experience Fragment i ett adaptivt formulär och dessa resurser redigeras och publiceras oberoende av varandra, blir Adaptiv Forms som innehåller sådana resurser inte automatiskt ogiltiga från Dispatcher cache.

#### Lösning {#Solution2}

När du har publicerat ett uppdaterat innehållsfragment eller Experience Fragment kan du uttryckligen avpublicera och publicera det adaptiva Forms som använder dessa resurser.

### Endast den första instansen av ett adaptivt formulär cachelagras{#only-first-insatnce-of-adptive-forms-is-cached}

#### Problem {#issue3}

När URL:en för det adaptiva formuläret inte har någon lokaliseringsinformation och **[!UICONTROL Use Browser Locale]** i konfigurationshanteraren är aktiverad. En lokaliserad version av det adaptiva formuläret levereras och endast den första instansen av det adaptiva formuläret cachelagras och skickas till alla efterföljande användare.

#### Lösning {#Solution3}

1. Öppna conf.d/httpd-dispatcher.conf eller någon annan konfigurationsfil som är konfigurerad att läsas in under körning.

1. Lägg till följande kod i filen och spara den. Det är en exempelkod som ändrar den så att den passar din miljö.

```XML
   <VirtualHost *:80>
        # Set log level high during development / debugging and then turn it down to whatever is appropriate
    LogLevel rewrite:trace6
        # Start Rewrite Engine
    RewriteEngine On
        # Handle actual URL convention (just pass through)
        RewriteRule "^/content/forms/af/(.*)[.](.*).html$" "/content/forms/af/$1.$2.html" [PT]
 
        # Handle selector based redirection basded on browser language
        # The Rewrite Cond(ition) is looking for the Accept-Lanague header and if found takes the first two characters which most likely is the desired language selector.
        RewriteCond %{HTTP:Accept-Language} ^(..).*$ [NC]
        RewriteRule "^/content/forms/af/(.*).html$" "/content/forms/af/$1.%1.html" [R]
   </VirtualHost>
```



>[!MORELIKETHIS]
>
>* [Felsöka cachningsrelaterade problem för AEM Forms as a Cloud Service](/help/forms/troubleshooting-caching-performance.md)
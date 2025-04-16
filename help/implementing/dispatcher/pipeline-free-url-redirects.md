---
title: Pipeline-fria URL-omdirigeringar
description: Lär dig hur du deklarerar 301- eller 302-omdirigeringar utan åtkomst till Git- eller Cloud Manager-pipelines.
feature: Dispatcher
role: Admin
exl-id: dacb1eda-79e0-4e76-926a-92b33bc784de
source-git-commit: 7a543c8fe63166ef34999f23ce9b05de8e8b0e9f
workflow-type: tm+mt
source-wordcount: '781'
ht-degree: 0%

---

# Pipeline-fria URL-omdirigeringar {#pipeline-free-redirects}

Av olika anledningar skriver organisationer om URL:er på ett sätt som orsakar en 301-omdirigering (eller 302), vilket innebär att webbläsaren omdirigeras till en annan sida.

Scenarier:

* En borttagen HTML-sida, så användaren tas till en ersättningssida (ibland hemsidan) i stället för att se ett `404 Page Not Found`-fel.
* En ny HTML-sida.
* SEO-optimering.

AEM as a Cloud Service erbjuder [flera strategier](https://experienceleague.adobe.com/en/docs/experience-manager-learn/foundation/administration/url-redirection) för att implementera omdirigeringar på serversidan, men den strategi som beskrivs i den här artikeln, omdirigeringar utan pipeline, är ett bra val när:

* De som underhåller omdirigeringarna är företagsanvändare som inte har den behörighet som krävs för att genomföra filändringar i källkontrollen eller möjligheten att utföra en konfigurationspipeline på Cloud Manager webbnivå.
* Antalet omdirigeringar varierar från några till tiotusentals.
* Du vill ha alternativet för ett användargränssnitt, antingen skapat som ett anpassat projekt eller med hjälp av [ACS Commons Redirect Map Manager](https://adobe-consulting-services.github.io/acs-aem-commons/features/redirect-map-manager/index.html) eller [ACS Commons Redirect Manager](https://adobe-consulting-services.github.io/acs-aem-commons/features/redirect-manager/subpages/rewritemap.html).

Kärnan i den här funktionen är möjligheten för AEM Apache/Dispatcher att läsa in (eller ladda om) en eller flera omskrivningsfiler som har placerats på en viss plats i publiceringsdatabasen (så att de kan hämtas från AEM publicering). Det är viktigt att nämna att hur filerna kommer in ligger utanför den här funktionens omfång, men du kan tänka dig någon av följande metoder:

* Inmatning av omskrivningskartan som en resurs i författarens användargränssnitt och publicering.
* Installerar [ACS Commons Redirect Map Manager](https://adobe-consulting-services.github.io/acs-aem-commons/features/redirect-map-manager/index.html) ([minst version 6.7.0 eller senare](https://github.com/Adobe-Consulting-Services/acs-aem-commons/releases)), som innehåller ett användargränssnitt för att hantera URL-mappningar och kan även publicera mappningsfilen för omskrivning.
* Installerar [ACS Commons Redirect Manager](https://adobe-consulting-services.github.io/acs-aem-commons/features/redirect-manager/subpages/rewritemap.html) ([minst version 6.10.0 eller senare](https://github.com/Adobe-Consulting-Services/acs-aem-commons/releases)), som även innehåller ett användargränssnitt för att hantera URL-mappningar och kan även publicera mappningsfilen för omskrivning.
* Full flexibilitet genom att skriva ett anpassat program. Till exempel ett användargränssnitt eller kommandoradsgränssnitt för att hantera URL-mappningar eller ett formulär för att överföra en omskrivningskarta, som sedan använder AEM API:er för att publicera omskrivningskartan.

>[!NOTE]
> Den här funktionen kräver AEM version **18311 eller senare**.

>[!NOTE]
> Funktionens användning av Redirect Map Manager kräver ACS Commons version **6.7.0 eller senare** medan användningen av Redirect Manager kräver version **6.10.0 eller senare**.

En detaljerad implementeringsguide steg för steg finns i självstudiekursen [Implementera URL-omdirigeringar utan pipeline](https://experienceleague.adobe.com/en/docs/experience-manager-learn/foundation/administration/implementing-pipeline-free-url-redirects).

## Mappen för omskrivning {#rewrite-map}

Omskrivningskartan läses in på nytt (om den ändras) av Apache HTTP-servern var 300:e sekund som standard (värdet är konfigurerbart). Filformatet bör följa det vanliga textnyckelvärdesschemat RewriteMap som beskrivs i [Apache-dokumentationen](https://httpd.apache.org/docs/2.4/rewrite/rewritemap.html#txt).

En fil med namnet `managed-rewrite-maps.yaml` ska skapas för att ange platsen för mappningsfilen för omskrivning och den måste distribueras en gång med Cloud Manager fullständiga stackpipeline eller webbskiktspipeline. Filen måste skapas i mappen [src/opt-in](https://github.com/adobe/aem-project-archetype/tree/develop/src/main/archetype/dispatcher.cloud/src/opt-in) i din dispatcher-konfiguration. Se till att du använder filstrukturen i det [flexibla läget](/help/implementing/dispatcher/validation-debug.md#flexible-mode-file-structure).

Du kan konfigurera den med följande mönster:

```
maps:
- name: my.map
  path: <path-in-publish-repository>/redirectmap.txt
```

Om du t.ex. har valt en metod för att montera omskrivningskartan är att importera den i AEM som en resurs med namnet `mysite-redirectmap.txt` och sedan publicera den, kan du ange en mapp under `/content/dam`:

```
maps:
- name: my.map
  path: /content/dam/redirectmaps/mysite-redirectmap.txt
```

I en Apache-konfigurationsfil som `rewrites/rewrite.rules` eller `<yourfile>.vhost` måste du sedan konfigurera den mappningsfil som namnegenskapen refererar till (`my.map` i exemplet ovan). När mappningsfilen har lästs in sparas den i det lokala lagringsutrymmet för dispatchern på **fast** plats `/tmp/rewrites/`.

Direktivet `RewriteMap` ska ange att data lagras i ett DBM-filformat (Database Manager) med formatet `sdbm` (simple DBM), och den fullständiga filsökvägen härleds från lagringsplatsens prefix och namnegenskapen.

Resten av konfigurationen beror på formatet för `redirectmap.txt`. Det enklaste formatet som visas i exemplet nedan är en till en mappning mellan den ursprungliga URL:en och den mappade url:en:

```
# RewriteMap from managed rewrite maps
RewriteMap map.foo dbm=sdbm:/tmp/rewrites/my.map
RewriteCond ${map.foo:$1} !=""
RewriteRule ^(.*)$ ${map.foo:$1|/} [L,R=301]
```

## Överväganden {#considerations}

Tänk på följande:

* När du läser in en omskrivningskarta startar Apache som standard utan att vänta på att de fullständiga mappningsfilerna ska läsas in, vilket kan leda till tillfälliga inkonsekvenser tills de fullständiga mappningarna läses in. Den här inställningen kan ändras så att Apache väntar på att det fullständiga kartinnehållet ska läsas in, men det tar längre tid för Apache att starta. Om du vill ändra detta så att Apache väntar lägger du till `wait:true` i filen `managed-rewrite-maps.yaml`.
* Om du vill ändra frekvensen mellan inläsningar lägger du till `ttl: <integer>` i filen `managed-rewrite-maps.yaml`. Till exempel: `ttl: 120`.
* Apache har en längdgräns på 1 024 för RewriteMap-enstaka poster.

## Självstudiekurser {#tutorials}

1. [Implementerar URL-omdirigeringar som är fria från pipeline](https://experienceleague.adobe.com/en/docs/experience-manager-learn/foundation/administration/implementing-pipeline-free-url-redirects)
1. [URL-omdirigeringar](https://experienceleague.adobe.com/en/docs/experience-manager-learn/foundation/administration/url-redirection)

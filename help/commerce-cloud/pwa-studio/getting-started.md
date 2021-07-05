---
title: Komma igång med AEM för PWA Studio
description: Lär dig hur du driftsätter ett AEM headless Content and Commerce-projekt med PWA Studio.
topics: Commerce
feature: Commerce Integration Framework
thumbnail: 37843.jpg
source-git-commit: 2d5207733a0ad5d88a321826727eb02440765faf
workflow-type: tm+mt
source-wordcount: '769'
ht-degree: 0%

---


# Komma igång med AEM för PWA Studio {#getting-started-pwa}

PWA Studio är integrerat med Adobe Commerce via GraphQL med obegränsade möjligheter att skapa innovativa och engagerande butiker och andra digitala upplevelser.

Innehållsfragment är innehållsdelar med en fördefinierad struktur som gör att de kan användas utan rubriker med GraphQL som API i olika format (t.ex. JSON, Markdown) och oberoende rendering. Innehållsfragment innehåller alla datatyper och fält som krävs för GraphQL för att säkerställa att programmet bara begär det som är tillgängligt och får det som förväntas. Den flexibilitet de ger i form av hur de är upplagda gör dem perfekta att använda på flera platser och i flera kanaler.

Det är enkelt att utforma den struktur du behöver med Modellredigeraren för innehållsfragment i Adobe Experience Manager. Den största utmaningen att integrera Adobe Experience Manager Content Fragments (eller andra data) med ditt PWA Studio-program är att hämta data från flera GraphQL-slutpunkter. Detta beror på att PWA Studio fungerar med en enda Adobe Commerce GraphQL-slutpunkt.

## Arkitektur {#architecture}

![PWA headless Architecture](/help/commerce-cloud/assets/PWA-Studio_Architecture.png)

## Konfigurera PWA Studio {#setup-pwa}

Följ dokumentationen för Adobe Commerce [PWA Studio](https://magento.github.io/pwa-studio/tutorials/) för att konfigurera din PWA Studio-app.

Om du vill ansluta PWA Studio till GraphQL-slutpunkten för AEM kan du använda [AEM-tillägget för PWA Studio](https://github.com/adobe/aem-pwa-studio-extensions).

1. Checka ut databasen

1. I ditt PWA Studio-program lägger du till tillägget som ett utvecklingsberoende.

   ```javascript
   yarn add --dev file:{path-to-extension}/extension
   ```

1. Lägg till Apollo Link-omslutningen i ditt PWA Studio-program. Gör följande ändringar i pwa-root/src/index.js:

   ```javascript
     import { linkWrapper } from '@adobe/pwa-studio-aem-cfm-blog-extension';
   
   // ...
   
   <Adapter apiBase={apiBase} apollo={{ link: linkWrapper(apolloLink) }} store={store}>
   ```

   Mer information om anpassning av Apollo-klienten finns i [linkWrapper.js](https://github.com/adobe/aem-pwa-studio-extensions/blob/master/aem-cfm-blog-extension/extension/src/linkWrapper.js).

1. Om du vill utöka navigeringskomponenten med ett blogginlägg lägger du till följande tillägg i pwa-root/local-intercept.js:

   ```javascript
   const addBlogToNavigation = require('@adobe/pwa-studio-aem-cfm-blog-extension/src/addBlogToNavigation');
   
   function localIntercept(targets) {
       addBlogToNavigation(targets);
   }    
   ```

   Mer information om anpassning av navigeringskomponenten finns i [addBlogToNavigation.js](https://github.com/adobe/aem-pwa-studio-extensions/blob/master/aem-cfm-blog-extension/extension/src/addBlogToNavigation.js) och i [Extensibility Framework](https://magento.github.io/pwa-studio/pwa-buildpack/extensibility-framework/)-dokumentationen för PWA Studio.

1. Apollo-klienten förväntar sig AEM GraphQL-slutpunkt vid <https://pwa-studio/endpoint.js>. Om du vill mappa slutpunkten till den här platsen måste du anpassa UPWARD-konfigurationen för ditt PWA Studio-program:
a. Lägg till variabeln AEM_CFM_GRAPHQL i pwa-root/.env och anpassa den så att den pekar på AEM Content Fragments GraphQL-slutpunkt.

   Exempel: AEM_CFM_GRAPHQL=<http://localhost:4503/content/graphql/global>

   b. Lägg till en proxymatchare i UPWARD-konfigurationen. Ett exempel på en UPWARD-konfiguration kan se ut så här:

```json
   response:
     resolver: conditional
     when:
       - matches: request.url.pathname
         pattern: ^/endpoint.json(/|$)
         use: aemProxy
     default: veniaResponse

   aemProxy:
     resolver: proxy
     target: env.AEM_CFM_GRAPHQL
     ignoreSSLErrors: true

   status: response.status
   headers: response.headers
   body: response.body
```

## AEM {#setup-aem}

Följ AEM Content Fragments dokumentation för att konfigurera en GraphQL-slutpunkt för ditt AEM. I ditt AEM lägger du till följande konfigurationer så att PWA Studio-programmet kan komma åt GraphQL-slutpunkten:

* Resursdelningspolicy för korsursprung för Adobe (com.adobe.granite.cors.impl.CORSPolicyImpl)

   Ställ in den tillåtna origin-egenskapen på det fullständiga värdnamnet för ditt PWA-program.

   Exempel:  <https://pwa-studio-test-vflyn.local.pwadev:9366>

* Apache Sling Referrer-filter (org.apache.sling.security.impl.ReferrerFilter.cfg.json)

   Ställ in egenskapen allow.hosts på värdnamnet för ditt PWA-program.

   Exempel: pwa-studio-test-vflyn.local.pwadev

Du hittar fullständiga exempel på båda konfigurationerna här: <https://github.com/adobe/aem-pwa-studio-extensions/tree/master/aem-cfm-blog-extension/aem/config/src/main/content/jcr_root/apps/blog-demo/config>.

För att visa GraphQL-slutpunkten förberedde vi några innehållsfragmentmodeller och data via ett innehållspaket. Dessa fungerar bra tillsammans med React Components som medföljer PWA Studio.

## Användning {#how-to-use}

Det här tillägget är ett exempel på implementering av hur du ansluter ett PWA Studio-program med AEM för att hämta och återge innehåll via GraphQL.

Beroende på ditt sätt att arbeta vill du skapa egna modeller för innehållsfragment som resulterar i ett anpassat GraphQL-schema som sedan kan användas av dina egna React-komponenter.

Produktionsinställningarna kan variera i olika aspekter.

* Du kan ha en enda federerad GraphQL-slutpunkt som kombinerar AEM- och Magento GraphQL-data i stället för att anpassa Apollo-klienten.
* Ditt PWA Studio-program kan använda AEM GraphQL-slutpunkts-URL direkt, utan en proxy med UPWARD. Proxyservern kan också flyttas till ett annat lager (t.ex. CDN).
* Vilken metod som passar bäst för dig beror också i hög grad på hur du levererar PWA Studio till slutanvändaren.

Det här tillägget innehåller två exempel.

### Blogg {#blog}

Visa blogginlägg baserat på vissa Content Fragment-modeller. Dessutom innehåller det exempel på hur du konfigurerar Apollo-klienten så att den fungerar med AEM GraphQL-slutpunkt och hur du utökar navigeringskomponenten i PWA Studio. Mer information finns i [GitHub](https://github.com/adobe/aem-pwa-studio-extensions/tree/master/aem-cfm-blog-extension).

### PDP-berikning {#pdp-enrichment}

Gör det möjligt för marknadsförare att enkelt utöka PDP:er med ytterligare innehåll som hanteras som innehållsfragment.  Mer information finns i [GitHub](https://github.com/adobe/aem-pwa-studio-extensions/tree/master/aem-cif-product-page-extension).

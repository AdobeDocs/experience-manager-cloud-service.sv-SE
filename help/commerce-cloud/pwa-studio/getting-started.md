---
title: Komma igång med AEM för PWA Studio
description: Lär dig hur du driftsätter ett AEM headless Content and Commerce-projekt med PWA Studio.
topics: Commerce
feature: Commerce Integration Framework
thumbnail: 37843.jpg
exl-id: a7c187ba-885e-45bf-a538-3c235b09a0f1
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 0%

---

# Komma igång med AEM för PWA Studio {#getting-started-pwa}

PWA Studio kan integreras smidigt med Adobe Commerce via GraphQL, vilket ger obegränsade möjligheter att skapa innovativa och engagerande butiker och andra digitala upplevelser.

Innehållsfragment är innehållsdelar med en fördefinierad struktur som gör att de kan konsumeras utan rubriker med GraphQL som API i olika format (till exempel JSON, Markdown) och oberoende rendering. Innehållsfragmenten innehåller alla datatyper och fält som krävs för att GraphQL ska vara säker på att ditt program bara begär det som är tillgängligt och får det som förväntas. Den flexibilitet de ger i form av hur de är upplagda gör dem perfekta att använda på flera platser och i flera kanaler.

Det är enkelt att utforma den struktur du behöver med Modellredigeraren för innehållsfragment i Adobe Experience Manager. Den största utmaningen att integrera Adobe Experience Manager Content Fragments (eller andra data) med ditt PWA Studio-program är att hämta data från flera GraphQL-slutpunkter. Det beror på att PWA Studio fungerar med en enda Adobe Commerce GraphQL-slutpunkt.

## Arkitektur {#architecture}

![PWA headless Architecture](/help/commerce-cloud/assets/PWA-Studio_Architecture.png)

## Konfigurera PWA Studio {#setup-pwa}

Följ Adobe Commerce [PWA Studio dokumentation](https://developer.adobe.com/commerce/pwa-studio/tutorials/) för att konfigurera din PWA Studio-app.

Om du vill ansluta PWA Studio till GraphQL AEM kan du använda kommandot [AEM för PWA Studio](https://github.com/adobe/aem-pwa-studio-extensions).

1. Checka ut databasen

1. I ditt PWA Studio-program lägger du till tillägget som ett utvecklingsberoende.

   ```javascript
   yarn add --dev file:{path-to-extension}/extension
   ```

1. Lägg till Apollo Link-omslutningen i PWA Studio. Gör följande ändringar i pwa-root/src/index.js:

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

   Mer information om anpassning av navigeringskomponenten finns i [addBlogToNavigation.js](https://github.com/adobe/aem-pwa-studio-extensions/blob/master/aem-cfm-blog-extension/extension/src/addBlogToNavigation.js) och i [Extensibility Framework](https://developer.adobe.com/commerce/pwa-studio/guides/general-concepts/extensibility/) Dokumentation för PWA Studio.

1. Apollo-klienten förväntar sig den AEM GraphQL-slutpunkten vid `<https://pwa-studio/endpoint.js>`. Om du vill mappa slutpunkten till den här platsen anpassar du UPWARD-konfigurationen för ditt PWA Studio-program: a. Lägg till variabeln AEM_CFM_GRAPHQL till pwa-root/.env och anpassa den så att den pekar på GraphQL-slutpunkten för AEM innehållsfragment.

   Exempel: `AEM_CFM_GRAPHQL=<http://localhost:4503/content/graphql/global>`

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

  Exempel:  `<https://pwa-studio-test-vflyn.local.pwadev:9366>`

* Apache Sling Referrer-filter (org.apache.sling.security.impl.ReferrerFilter.cfg.json)

  Ställ in egenskapen allow.hosts på värdnamnet för ditt PWA-program.

  Exempel: `pwa-studio-test-vflyn.local.pwadev`

Du hittar fullständiga exempel på båda konfigurationerna här: <https://github.com/adobe/aem-pwa-studio-extensions/tree/master/aem-cfm-blog-extension/aem/config/src/main/content/jcr_root/apps/blog-demo/config>.

För att visa GraphQL-slutpunkten har vi förberett några innehållsfragmentmodeller och data via ett innehållspaket. Dessa fungerar bra tillsammans med React Components som medföljer PWA Studio.

## Användning {#how-to-use}

Det här tillägget är ett exempel på implementering av hur du ansluter ett PWA Studio-program med AEM för att hämta och återge innehåll via GraphQL.

Beroende på ditt sätt att arbeta vill du skapa egna modeller för innehållsfragment som resulterar i ett anpassat GraphQL-schema som sedan kan användas av dina egna React-komponenter.

Produktionsinställningarna kan variera i olika aspekter.

* Du kan ha en enda federerad GraphQL-slutpunkt som kombinerar AEM- och Adobe Commerce GraphQL-data i stället för att anpassa Apollo-klienten.
* Ditt PWA Studio-program kan använda AEM GraphQL-slutpunkts-URL direkt, utan någon proxy med UPWARD. Proxyservern kan också flyttas till ett annat lager (till exempel CDN).
* Vilken metod som passar bäst för dig beror också i hög grad på hur du levererar PWA Studio till slutanvändaren.

Det här tillägget innehåller två exempel.

### Blogg {#blog}

Visa blogginlägg baserat på vissa innehållsfragmentmodeller. Dessutom innehåller det exempel på hur du konfigurerar Apollo-klienten så att den fungerar med AEM GraphQL-slutpunkt och hur du utökar navigeringskomponenten i PWA Studio. Se [GitHub](https://github.com/adobe/aem-pwa-studio-extensions/tree/master/aem-cfm-blog-extension) för mer information.

### PDP-berikning {#pdp-enrichment}

Gör det möjligt för marknadsförare att enkelt utöka PDP:er med ytterligare innehåll som hanteras som innehållsfragment.  Se [GitHub](https://github.com/adobe/aem-pwa-studio-extensions/tree/master/aem-cif-product-page-extension) för mer information.

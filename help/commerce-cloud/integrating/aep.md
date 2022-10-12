---
title: AEM-CIF-komponenter och integrering med Adobe Experience Platform
description: Lär dig hur du skickar händelsedata för butiker från en AEM produktsida till Experience Platform med CIF-anslutningsprogrammet Experience Platform.
sub-product: Commerce
version: Cloud Service
activity: setup
feature: Commerce Integration Framework
topic: Commerce
role: Architect, Developer
level: Beginner
kt: 10834
thumbnail: 346811.jpeg
source-git-commit: 2ebe9ddccd0b657b8aaeaf005c0ecb5b16079dee
workflow-type: tm+mt
source-wordcount: '2010'
ht-degree: 0%

---


# AEM-CIF-komponenter och integrering med Adobe Experience Platform {#aem-cif-aep-integration}

The [Commerce Integration Framework (CIF)](https://github.com/adobe/aem-core-cif-components) grundkomponenterna ger smidig integration med [Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-overview.html?lang=en) att vidarebefordra butikshändelser och deras data från interaktioner på klientsidan, som __lägg till i kundvagn__.

The [AEM CIF-kärnkomponenter](https://github.com/adobe/aem-core-cif-components) project innehåller ett JavaScript-bibliotek som kallas [Adobe Experience Platform Connector for Adobe Commerce](https://github.com/adobe/aem-core-cif-components/tree/master/extensions/experience-platform-connector) för att samla in händelsedata från din Commerce Store. Dessa händelsedata skickas till Experience Platform där de används i andra Adobe Experience Cloud-produkter, som Adobe Analytics och Adobe Target, för att skapa en helhetsprofil som täcker en kundresa. Genom att ansluta Commerce-data till andra produkter i Adobe Experience Cloud kan ni utföra uppgifter som att analysera användarbeteende på er webbplats, utföra AB-tester och skapa personaliserade kampanjer.

Läs mer om [Experience Platform datainsamling](https://experienceleague.adobe.com/docs/experience-platform/collection/home.html) en serie teknologier som gör att ni kan samla in kundupplevelsedata från källor på kundsidan.

## Skicka `addToCart` händelsedata till Experience Platform {#send-addtocart-to-aep}

Följande steg visar hur du skickar `addToCart` händelsedata från AEM produktsidor till Experience Platform med CIF - Experience Platform Connector. Med webbläsartillägget Adobe Experience Platform Debugger kan du testa och granska skickade data.

![Granska händelsedata för addToCart i Adobe Experience Platform Debugger](../assets/aep-integration/EventData-AEM-AEP.png)

## Förutsättningar {#prerequisites}

Du måste använda en lokal utvecklingsmiljö för att slutföra den här demon. Detta inkluderar en instans av AEM som körs och som är konfigurerad och ansluten till en Adobe Commerce-instans. Granska kraven och stegen för [konfigurera lokal utveckling med AEM as a Cloud Service SDK](../develop.md).

Du måste även ha tillgång till [Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-ui/ui-guide.html) och behörigheter för att skapa schema, datauppsättning och datastreams för datainsamling. Mer information finns i [Behörighetshantering](https://experienceleague.adobe.com/docs/experience-platform/collection/permissions.html).

## as a Cloud Service inställningar för AEM {#aem-setup}

Att ha en fungerande __AEM Commerce as a Cloud Service__ lokal miljö med nödvändig kod och konfiguration, utför följande steg.

### Lokal installation

Följ [Lokal installation](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/content-and-commerce/storefront/developing/develop.html?#local-setup) steg för att ha en fungerande AEM as a Cloud Service Commerce-miljö.

### Projektinställningar

Följ [AEM Project Archetype](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/content-and-commerce/storefront/developing/develop.html?#project) steg för att skapa ett helt nytt AEM Commerce-projekt (CIF).

>[!TIP]
>
>I följande exempel heter AEM Commerce-projektet: `My Demo Storefront`Du kan dock välja ett eget projektnamn.

![AEM](../assets/aep-integration/aem-project-with-commerce.png)


Skapa och distribuera det nya AEM Commerce-projektet till det lokala AEM SDK:t genom att köra följande kommando från projektets rotkatalog.

```bash
$ mvn clean install -PautoInstallSinglePackage
```

Lokalt distribuerad `My Demo StoreFront` e-handelswebbplatsen med standardkod och standardinnehåll ser ut så här:

![Standardwebbplats för AEM](../assets/aep-integration/demo-aem-storefront.png)

### Installera anslutningsberoenden för Premiere och CIF-AEP

Om du vill samla in och skicka händelsedata från kategori- och produktsidorna på den här AEM Commerce-webbplatsen måste du installera nyckeln `npm` i `ui.frontend` modulen i AEM Commerce-projektet.

Navigera till `ui.frontend` och installera de nödvändiga paketen genom att köra följande kommandon från kommandoraden.

```bash
npm i --save lodash.get@^4.4.2 lodash.set@^4.3.2
npm i --save apollo-cache-persist@^0.1.1
npm i --save redux-thunk@~2.3.0
npm i --save @adobe/apollo-link-mutation-queue@~1.1.0
npm i --save @magento/peregrine@~12.5.0
npm i --save @adobe/aem-core-cif-react-components --force
npm i --save-dev @magento/babel-preset-peregrine@~1.2.1
npm i --save @adobe/aem-core-cif-experience-platform-connector --force
```

>[!IMPORTANT]
>
>The `--force` argument krävs ibland som [PWA Studio](https://developer.adobe.com/commerce/pwa-studio/) är begränsat med peer-beroenden som stöds. Vanligtvis bör detta inte orsaka några problem.


### Konfigurera Maven för användning `--force` argument

Som en del av byggprocessen i Maven har npm-installationen gjorts rent (med `npm ci`) aktiveras. Detta kräver även `--force` argument.

Navigera till projektets POM-rotfil `pom.xml` och hitta `<id>npm ci</id>` körningsblock. Uppdatera blocket så att det ser ut så här:

```xml
<execution>
    <id>npm ci</id>
    <goals>
    <goal>npm</goal>
    </goals>
    <configuration>
    <arguments>ci --force</arguments>
    </configuration>
</execution>
```

### Ändra konfigurationsformat för Label

Växla från standard `.babelrc` filrelativt konfigurationsfilformat till `babel.config.js` format. Detta är ett projektövergripande konfigurationsformat som gör att plugin-program och förinställningar kan användas i `node_module` med större kontroll.

1. Navigera till `ui.frontend` och ta bort befintlig `.babelrc` -fil.

1. Skapa en `babel.config.js` som använder `peregrine` förinställning.

   ```javascript
   const peregrine = require('@magento/babel-preset-peregrine');
   
   module.exports = (api, opts = {}) => {
       const config = {
           ...peregrine(api, opts),
           sourceType: 'unambiguous'
       } 
   
       config.plugins = config.plugins.filter(plugin => plugin !== 'react-refresh/babel');
   
       return config;
   }
   ```

### Konfigurera webbpaket för användning av babel

Så här transplanterar du JavaScript-filer med hjälp av en babel-inläsare (`babel-loader`) och webbpaket måste du ändra `webpack.common.js` -fil.

Navigera till `ui.frontend` och uppdatera `webpack.common.js` filen så att följande regel finns i `module` egenskapsvärde:

```javascript
{
    test: /\.jsx?$/,
    exclude: /node_modules\/(?!@magento\/)/,
    loader: 'babel-loader'
}
```

### Konfigurera Apollo-klient

The [Apollo Client](https://www.apollographql.com/docs/react/) används för att hantera både lokala data och fjärrdata med GraphQL. Resultatet av GraphQL-frågor lagras också i en lokal, normaliserad cache i minnet.

För [`InMemoryCache`](https://www.apollographql.com/docs/react/caching/cache-configuration/) för att arbeta effektivt behöver du en `possibleTypes.js` -fil. Information om hur du skapar den här filen finns i [Generera möjliga typer automatiskt](https://www.apollographql.com/docs/react/data/fragments/#generating-possibletypes-automatically). Se även [PWA Studio referensimplementering](https://github.com/magento/pwa-studio/blob/1977f38305ff6c0e2b23a9da7beb0b2f69758bed/packages/pwa-buildpack/lib/Utilities/graphQL.js#L106-L120) och ett exempel på en [`possibleTypes.js`](../assets/aep-integration/possibleTypes.js) -fil.


1. Navigera till `ui.frontend` och spara filen som `./src/main/possibleTypes.js`

1. Uppdatera `webpack.common.js` fil `DefinePlugin` för att ersätta de statiska variabler som krävs under byggtiden.

   ```javascript
   const { DefinePlugin } = require('webpack');
   const { POSSIBLE_TYPES } = require('./src/main/possibleTypes');
   
   ...
   
   plugins: [
       ...
       new DefinePlugin({
           'process.env.USE_STORE_CODE_IN_URL': false,
           POSSIBLE_TYPES
       })
   ]
   ```

### Initiera kärnkomponenterna Peregrine och CIF

Om du vill initiera de React-baserade Premiere- och CIF-kärnkomponenterna skapar du den konfiguration och de JavaScript-filer som krävs.

1. Navigera till `ui.frontend` och skapa följande mapp: `src/main/webpack/components/commerce/App`

1. Skapa en `config.js` fil med följande innehåll:

   ```javascript
   // get and parse the CIF store configuration from the <head>
   const storeConfigEl = document.querySelector('meta[name="store-config"]');
   const storeConfig = storeConfigEl ? JSON.parse(storeConfigEl.content) : {};
   
   // the following global variables are needed for some of the peregrine features
   window.STORE_VIEW_CODE = storeConfig.storeView || 'default';
   window.AVAILABLE_STORE_VIEWS = [
       {
           code: window.STORE_VIEW_CODE,
           base_currency_code: 'USD',
           default_display_currency_code: 'USD',
           id: 1,
           locale: 'en',
           secure_base_media_url: '',
           store_name: 'My Demo StoreFront'
       }
   ];
   window.STORE_NAME = window.STORE_VIEW_CODE;
   window.DEFAULT_COUNTRY_CODE = 'en';
   
   export default {
       storeView: window.STORE_VIEW_CODE,
       graphqlEndpoint: storeConfig.graphqlEndpoint,
       // Can be GET or POST. When selecting GET, this applies to cache-able GraphQL query requests only.
       // Mutations will always be executed as POST requests.
       graphqlMethod: storeConfig.graphqlMethod,
       headers: storeConfig.headers,
   
       mountingPoints: {
           // TODO: define the application specific mount points as they may be used by <Portal> and <PortalPlacer>
       },
       pagePaths: {
           // TODO: define the application specific paths/urls as they may be used by the components
           baseUrl: storeConfig.storeRootUrl
       },
       eventsCollector: {
           // Enable the Experience Platform Connector and define the org and datastream to use
           aep: {
               orgId: // TODO: add your orgId
               datastreamId: // TODO: add your datastreamId
           }
       }
   };
   ```

   >[!IMPORTANT]
   >
   >Även om du redan är bekant med [`config.js`](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.frontend/src/main/components/App/config.js) fil från __AEM - CIF Venia Project__ måste du göra några ändringar i den här filen. Börja med att granska __ATT__ kommentarer. Sedan, i `eventsCollector` -egenskap, hitta `eventsCollector > aed` -objektet och uppdatera `orgId` och `datastreamId` till rätt värden. [Läs mer](./aep.md#add-aep-values-to-aem).

1. Skapa en `App.js` med följande innehåll. Den här filen liknar en vanlig React-startpunktsfil och innehåller React- och anpassade kopplingar samt React Context-användning som underlättar integreringen mellan Experience Platform.

   ```javascript
   import config from './config';
   
   import React, { useEffect } from 'react';
   import ReactDOM from 'react-dom';
   import { IntlProvider } from 'react-intl';
   import { BrowserRouter as Router } from 'react-router-dom';
   import { combineReducers, createStore } from 'redux';
   import { Provider as ReduxProvider } from 'react-redux';
   import { createHttpLink, ApolloProvider } from '@apollo/client';
   import { ConfigContextProvider, useCustomUrlEvent, useReferrerEvent, usePageEvent, useDataLayerEvents, useAddToCartEvent } from '@adobe/aem-core-cif-react-components';
   import { EventCollectorContextProvider, useEventCollectorContext } from '@adobe/aem-core-cif-experience-platform-connector';
   import { useAdapter } from '@magento/peregrine/lib/talons/Adapter/useAdapter';
   import { customFetchToShrinkQuery } from '@magento/peregrine/lib/Apollo/links';
   import { BrowserPersistence } from '@magento/peregrine/lib/util';
   import { default as PeregrineContextProvider } from '@magento/peregrine/lib/PeregrineContextProvider';
   import { enhancer, reducers } from '@magento/peregrine/lib/store';
   
   const storage = new BrowserPersistence();
   const store = createStore(combineReducers(reducers), enhancer);
   
   storage.setItem('store_view_code', config.storeView);
   
   const App = () => {
       const [{ sdk: mse }] = useEventCollectorContext();
   
       // trigger page-level events
       useCustomUrlEvent({ mse });
       useReferrerEvent({ mse });
       usePageEvent({ mse });
       // listen for add-to-cart events and enable forwarding to the magento storefront events sdk
       useAddToCartEvent(({ mse }));
       // enable CIF specific event forwarding to the Adobe Client Data Layer
       useDataLayerEvents();
   
       useEffect(() => {
           // implement a proper marketing opt-in, for demo purpose we hard-set the consent cookie
           if (document.cookie.indexOf('mg_dnt') < 0) {
               document.cookie += '; mg_dnt=track';
           }
       }, []);
   
       // TODO: use the App to create Portals and PortalPlaceholders to mount the CIF / Peregrine components to the server side rendered markup
       return <></>;
   };
   
   const AppContext = ({ children }) => {
       const { storeView, graphqlEndpoint, graphqlMethod = 'POST', headers = {}, eventsCollector } = config;
       const { apolloProps } = useAdapter({
           apiUrl: new URL(graphqlEndpoint, window.location.origin).toString(),
           configureLinks: (links, apiBase) =>
               // reconfigure the HTTP link to use the configured graphqlEndpoint, graphqlMethod and storeView header
   
               links.set('HTTP', createHttpLink({
                   fetch: customFetchToShrinkQuery,
                   useGETForQueries: graphqlMethod !== 'POST',
                   uri: apiBase,
                   headers: { ...headers, 'Store': storeView }
               }))
       });
   
       return (
           <ApolloProvider {...apolloProps}>
               <IntlProvider locale='en' messages={{}}>
                   <ConfigContextProvider config={config}>
                       <ReduxProvider store={store}>
                           <PeregrineContextProvider>
                               <EventCollectorContextProvider {...eventsCollector}>
                                   {children}
                               </EventCollectorContextProvider>
                           </PeregrineContextProvider>
                       </ReduxProvider>
                   </ConfigContextProvider>
               </IntlProvider>
           </ApolloProvider>
       );
   };
   
   window.onload = async () => {
       const root = document.createElement('div');
       document.body.appendChild(root);
   
       ReactDOM.render(
           <Router>
               <AppContext>
                   <App />
               </AppContext>
           </Router>,
           root
       );
   };
   ```

   The `EventCollectorContext` exporterar React-kontexten som:

   - läser in biblioteket commerce-events-sdk och commerce-events-collector,
   - initierar dem med en viss konfiguration för Experience Platform och/eller ACDS
   - prenumererar på alla händelser från Premiere och vidarebefordrar dem till SDK:n

   Du kan granska implementeringsinformationen för `EventCollectorContext` [här](https://github.com/adobe/aem-core-cif-components/blob/3d4e44d81fff2f398fd2376d24f7b7019f20b31b/extensions/experience-platform-connector/src/events-collector/EventCollectorContext.js).

### Bygg och distribuera det uppdaterade AEM projektet

För att se till att ovanstående paket-installation, kod- och konfigurationsändringar är korrekta återskapar och distribuerar du det uppdaterade AEM Commerce-projektet med följande Maven-kommando: `$ mvn clean install -PautoInstallSinglePackage`.

## Inställningar för Experience Platform {#aep-setup}

Så här tar du emot och lagrar händelsedata från AEM Commerce-sidor, t.ex. kategori och produkt:

>[!AVAILABILITY]
>
>Se till att du är en del av rätt __Produktprofiler__ under __Adobe Experience Platform__ och __Adobe Experience Platform Data Collection__. Om det behövs kan du samarbeta med systemadministratören för att skapa, uppdatera eller tilldela __Produktprofiler__ under [Admin Console](https://adminconsole.adobe.com/).

### Skapa schema med fältgrupp i Commerce

Om du vill definiera strukturen för e-handelshändelsedata måste du skapa ett XDM-schema (Experience Data Model). Ett schema är en uppsättning regler som representerar och validerar datastrukturen och dataformatet.

1. Navigera till __Adobe Experience Platform__ startsida för produkten. Till exempel, <https://experience.adobe.com/#/@YOUR-ORG-NAME/sname:prod/platform/home>.

1. Leta reda på __Scheman__ i det vänstra navigeringsavsnittet klickar du på __Skapa schema__ i det övre högra avsnittet och väljer __XDM ExperienceEvent__.

   ![Skapa schema för AEP](../assets/aep-integration/AEP-Schema-EventSchema-1.png)

1. Namnge schemat med __Schemaegenskaper > Visningsnamn__ fält och lägg till fältgrupper med  __Disposition > Fältgrupper > Lägg till__ -knappen.

   ![AEP-schemadefinition](../assets/aep-integration/AEP-Schema-Definition.png)

1. I __Lägg till fältgrupper__ dialogruta, söka efter `Commerce`väljer du __Handelsinformation__ och klicka __Lägg till fältgrupper__.

   ![AEP-schemadefinition](../assets/aep-integration/AEP-Schema-Field-Group.png)


>[!TIP]
>
>Se [Grunderna för schemakomposition](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html) för mer information.

### Skapa datauppsättning

Om du vill lagra händelsedata måste du skapa en datauppsättning som överensstämmer med schemadefinitionen. En datauppsättning är en lagrings- och hanteringskonstruktion för en datamängd, vanligtvis en tabell, som innehåller ett schema (kolumner) och fält (rader).

1. Navigera till __Adobe Experience Platform__ startsida för produkten. Till exempel, <https://experience.adobe.com/#/@YOUR-ORG-NAME/sname:prod/platform/home>.

1. Leta reda på __Datauppsättningar__ i det vänstra navigeringsavsnittet och klicka på __Skapa datauppsättning__ i det övre högra avsnittet.

   ![AEP Skapa datauppsättningar](../assets/aep-integration/AEP-Datasets-Create.png)

1. På den nya sidan väljer du __Skapa datauppsättning från schema__ kort.

   ![Alternativ för att skapa dataschema i AEP](../assets/aep-integration/AEP-Datasets-Schema-Option.png)

- På den nya sidan __sök och markera__ schemat som du skapade i föregående steg och klicka på __Nästa__ -knappen.

   ![AEP Skapa datauppsättningar Välj schema](../assets/aep-integration/AEP-Datasets-Select-Schema.png)

1. Namnge datauppsättningen med __Konfigurera datauppsättning > Namn__ och klicka på __Slutför__ -knappen.

   ![Namn på AEP Skapa datauppsättningar](../assets/aep-integration/AEP-Datasets-Name.png)

>[!TIP]
>
>Se [Översikt över datauppsättningar](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/overview.html) för mer information.


### Skapa dataström

Följ de här stegen för att skapa ett datastream i Experience Platform.

1. Navigera till __Adobe Experience Platform__ startsida för produkten. Till exempel, <https://experience.adobe.com/#/@YOUR-ORG-NAME/sname:prod/platform/home>.

1. Leta reda på __Datastreams__ i det vänstra navigeringsavsnittet och klicka på __Ny datastream__ i det övre högra avsnittet.

   ![AEP Skapa datastreams](../assets/aep-integration/AEP-Datastream-Create.png)

1. Namnge ditt datastream med __Namn__ obligatoriskt fält. Under __Händelseschema__ markerar du det nyligen skapade schemat och klickar på __Spara__.

   ![AEP Definiera datastreams](../assets/aep-integration/AEP-Datastream-Define.png)

1. Öppna den nya dataströmmen och klicka på __Lägg till tjänst__.

   ![AEP-datastreams Add Service](../assets/aep-integration/AEP-Datastream-Add-Service.png)

1. Under __Tjänst__ välj __Adobe Experience Platform__ alternativ. Under __Händelsedatauppsättning__ markerar du datauppsättningsnamnet från föregående steg och klickar på __Spara__.

   ![AEP-datastreams Lägg till serviceinformation](../assets/aep-integration/AEP-Datastream-Add-Service-Define.png)

>[!TIP]
>
>Se [Översikt över datastream](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/overview.html) för mer information.

## Lägg till datastream-värde i AEM Commerce-konfiguration {#add-aep-values-to-aem}

När du är klar med konfigurationen ovan för Experience Platform bör du ha `datastreamId` i den vänstra listen i dataströmmens detaljer och `orgId` i det övre högra hörnet av __Profilbild > Kontoinformation > Användarinformation__ modal.

![AEP-datastreams-ID](../assets/aep-integration/AEP-Datastream-ID.png)

1. I AEM Commerce-projekt `ui.frontend` modul, uppdatera `config.js` -filen och `eventsCollector > aep` objektegenskaper.

1. Bygg och distribuera det uppdaterade AEM Commerce-projektet


## Utlösare `addToCart` händelse och verifiera datainsamling {#event-trigger-verify}

Ovanstående steg avslutar installationen av AEM Commerce och Experience Platform. Nu kan du aktivera en `addToCart` händelse och verifiera datainsamling med Experience Platform-felsökaren och datauppsättningen __Mätvärden och diagram__ i produktgränssnittet.

Om du vill utlösa händelsen kan du använda AEM författare eller publiceringstjänsten från din lokala konfiguration. I det här exemplet använder du AEM författare genom att logga in på ditt konto.

1. På sidan Platser väljer du __My Demo StoreFront > us > en__ sida och klicka __Redigera__ i det övre åtgärdsfältet.

1. Klicka på i det övre åtgärdsfältet __Visa som publicerad__ klickar du sedan på valfri kategori i butikens navigering.

1. Klicka på ett valfritt produktkort i __Produktsida__ väljer __färg, storlek__ för att aktivera __Lägg i kundvagnen__ -knappen.


1. Öppna __Adobe Experience Platform Debugger__ tillägg från webbläsarens tilläggspanel och välj __Experience Platform Wed SDK__ till vänster.

   ![AEP Debugger](../assets/aep-integration/AEP-Debugger.png)


1. Återgå till __Produktsida__ och klicka __Lägg i kundvagnen__ -knappen. Detta skickar data till Experience Platform. The __Adobe Experience Platform Debugger__ tillägget visar händelseinformation.

   ![AEP Debugger Add-To-Cart Event-Data](../assets/aep-integration/AEP-Debugger-AddToCart-EventData.png)



1. I användargränssnittet för Experience Platform går du till __Datamängder > My Demo StoreFront__, under __Datauppsättningsaktivitet__ -fliken. Om __Mätvärden och diagram__ växlingsknappen är aktiverad visas händelsedatatillstånd.

   ![Datauppsättningsstatistik för Experience Platform](../assets/aep-integration/AEP-Dataset-AddToCart-EventData.png)



## Implementeringsinformation {#implementation-details}

The [CIF Experience Platform Connector](https://github.com/adobe/aem-core-cif-components/tree/master/extensions/experience-platform-connector) är byggd ovanpå [Experience Platform Connector for Adobe Commerce](https://marketplace.magento.com/magento-experience-platform-connector.html), som ingår i [PWA Studio](https://developer.adobe.com/commerce/pwa-studio/) projekt.

Med PWA Studio-projektet kan du skapa Progressive Web Application (PWA) butiker med Adobe Commerce eller Magento Open Source. Projektet innehåller också ett komponentbibliotek som kallas [Peregrin](https://developer.adobe.com/commerce/pwa-studio/api/peregrine/) för att lägga till logik i visuella komponenter. The [Bibliotek för pärmar](https://developer.adobe.com/commerce/pwa-studio/api/peregrine/) innehåller även anpassade React-kopplingar som används av [Experience Platform Connector](https://github.com/adobe/aem-core-cif-components/tree/master/extensions/experience-platform-connector) för smidig integrering med Experience Platform.


## Händelser som stöds {#supported-events}

Från och med nu stöds följande händelser:

- addToCart
- pageView
- customUrl
- referrerUrl

## Ytterligare resurser {#additional-resources}

Mer information finns i följande resurser:

- [PWA Studio](https://developer.adobe.com/commerce/pwa-studio/)
- [Experience Platform-anslutning - översikt](https://experienceleague.adobe.com/docs/commerce-merchant-services/experience-platform-connector/overview.html)
- [Adobe Experience Platform - översikt](https://experienceleague.adobe.com/docs/experience-platform/landing/home.html)


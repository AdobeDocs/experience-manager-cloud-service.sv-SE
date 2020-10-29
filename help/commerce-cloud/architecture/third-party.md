---
title: AEM och tredjeparts Commerce Integration med Commerce Integration Framework
description: Företag kan behöva ytterligare e-handelslösningar från tredje part för att göra sin butik tillgänglig. Commerce Integration Framework (CIF) kan användas i sådana integreringsscenarier för att ansluta en tredjepartslösning för e-handel till Adobe Experience Manager med hjälp av I/O Runtime.
thumbnail: cif-third-party-architecture.jpg
translation-type: tm+mt
source-git-commit: 72d98c21a3c02b98bd2474843b36f499e8d75a03
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 0%

---


# AEM och tredjeparts Commerce Integration med Commerce Integration Framework {#aem-third-party}

Företag kan behöva ytterligare e-handelslösningar från tredje part för att göra sin butik tillgänglig. Commerce Integration Framework (CIF) kan användas i sådana integreringsscenarier där en tredjepartslösning för e-handel även måste integreras med AEM, utöver Magento. CIF innehåller element som t.ex. en acceleratorreferenslager, AEM CIF Core Components och redigeringsverktyg som fungerar med Magento som standard. För att integrera AEM och en e-handelslösning från tredje part och återanvända dessa CIF-element krävs ytterligare utveckling.

## Arkitektur {#architecture}

Den övergripande arkitekturen är följande:

![Översikt över arkitekturen AEM andra än Magento/tredje part](/help/commerce-cloud/assets/AEM_nonMagento_Architecture.JPG)

Den största skillnaden mellan integrationsarkitekturen för AEM - Magento och AEM - tredjepartshandeln är tillägget av ett integrerings- och dataomvandlingslager, vilket visas i bilden ovan. Integreringslagret måste ligga på Adobe I/O Runtime-plattformen, som är Adobe serverless. Du kan läsa mer om Adobe I/O Runtime [här](https://www.adobe.io/apis/experienceplatform/runtime.html).

Syftet med det här integreringslagret är att mappa API:er från andra företag än Magento eller en tredje part mot API:er från Adobe Commerce (Magento GraphQL API:er). Med den här mappningen kan [AEM CIF Core Components](https://github.com/adobe/aem-core-cif-components) och CIF-redigeringsverktygen hämta data från andra lösningar än Magento. Med den här metoden inkapslar integreringslagret integreringslogiken och skapar en separat oro mellan AEM och tredjepartslösningen. Detta gör att CIF-elementen kan användas på ett agnostiskt sätt med olika tredjepartslösningar. Fördelarna med att använda CIF-element i ditt projekt har beskrivits i [introduktionen](/help/commerce-cloud/overview.md).

## Utveckla en integrering {#develop-integration}

För att hjälpa dig att komma igång med att skapa det integreringslager som krävs för att integrera en lösning från andra företag än Magento/tredje part med AEM har vi skapat en [referensimplementering](https://github.com/adobe/commerce-cif-graphql-integration-reference) som demonstrerar detta. Den här referensen kan användas som utgångspunkt i ditt projekt.

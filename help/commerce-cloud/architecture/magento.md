---
title: Integrering av AEM och Magento med Commerce Integration Framework
description: AEM och Magento integreras smidigt med Commerce Integration Framework (CIF). Med CIF kan AEM få åtkomst till en Magento-instans och kommunicera med Magento via GraphQL. AEM Authors kan också använda produkt- och kategoriväljare och produktkonsolen för att bläddra bland produkt- och kategoridata som hämtats on demand från Magento. Dessutom erbjuder CIF en färdig butik som kan snabba upp affärsprojekt.
thumbnail: aem-magento-architecture.jpg
translation-type: tm+mt
source-git-commit: 0f2b7176b44bb79bdcd1cecf6debf05bd652a1a1
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 0%

---


# Integrering av AEM och Magento med Commerce Integration Framework {#aem-magento-framework}

AEM och Magento integreras smidigt med Commerce Integration Framework (CIF). Med CIF kan AEM få åtkomst till en Magento-instans och kommunicera med Magento via GraphQL. AEM Authors kan också använda produkt- och kategoriväljare och produktkonsolen för att bläddra bland produkt- och kategoridata som hämtats on demand från Magento. Dessutom erbjuder CIF en färdig butik som kan snabba upp affärsprojekt.

>[!NOTE]
>
>GraphQL används för närvarande i två (separata) scenarier i Adobe Experience Manager (AEM) som en Cloud Service:
>
>* AEM Commerce använder data från en e-handelsplattform via GraphQL.
>* [AEM Content Fragments fungerar tillsammans med det AEM GraphQL-API:t (en anpassad implementering som baseras på standard GraphQL) för att leverera strukturerat innehåll som kan användas i dina program](/help/assets/content-fragments/graphql-api-content-fragments.md).


## Arkitekturöversikt {#overview}

Den övergripande arkitekturen är följande:

![CIF-arkitekturöversikt](../assets/AEM_Magento_Architecture.JPG)

CIF bygger på GraphQL-stöd. Huvudkommunikationskanalen mellan AEM och Magento är Magento [API:t för GraphQL](https://devdocs.magento.com/guides/v2.4/graphql/). Det finns olika sätt att konfigurera kommunikationen mellan AEM som en Cloud Service och Magento. Mer information finns på [Komma igång](../getting-started.md)-sidan.

Inom CIF finns stöd för kommunikationsmönster på serversidan och klientsidan.
API-anrop på serversidan implementeras med den generiska [GraphQL-klienten](https://github.com/adobe/commerce-cif-graphql-client) i kombination med en [uppsättning genererade datamodeller](https://github.com/adobe/commerce-cif-magento-graphql) för Magento GraphQL-schemat. Dessutom kan alla GraphQL-frågor eller mutationer i GQL-format användas.

För klientkomponenterna, som byggs med [React](https://reactjs.org/), används [Apollo Client](https://www.apollographql.com/docs/react/).

## AEM CIF Core Component Architecture {#cif-core-components}

![AEM CIF Core Component Architecture](../assets/cif-component-architecture.jpg)

[AEM CIF Core ](https://github.com/adobe/aem-core-cif-components) Components följer mycket liknande designmönster och bästa praxis som  [AEM WCM Core Components](https://github.com/adobe/aem-core-wcm-components).

Affärslogik och backend-kommunikation med Magento för AEM CIF Core Components implementeras i Sling Models. Om det är nödvändigt att anpassa den här logiken för att uppfylla projektspecifika krav kan delegeringsmönstret för segmentmodeller användas.

>[!TIP]
>
>Sidan [Anpassa AEM CIF Core Components](../customizing/customize-cif-components.md) innehåller ett detaljerat exempel och bästa praxis för att anpassa CIF Core Components.

I projekt kan AEM CIF Core Components och anpassade projektkomponenter enkelt hämta den konfigurerade klienten för en Magento-butik som är kopplad till en AEM sida via Sling Context-Aware-konfiguration.

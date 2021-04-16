---
title: Integrering av AEM och Adobe Commerce (Magento) med Commerce Integration Framework
description: AEM och Adobe Commerce (Magento) integreras smidigt med Commerce Integration Framework (CIF). Med CIF kan AEM få åtkomst till en Magento-instans och kommunicera med Magento via GraphQL. AEM Authors kan också använda produkt- och kategoriväljare och produktkonsolen för att bläddra bland produkt- och kategoridata som hämtats on demand från Magento. Dessutom erbjuder CIF en färdig butik som kan snabba upp affärsprojekt.
thumbnail: aem-magento-architecture.jpg
exl-id: 1cdfda88-a728-432f-b24a-f81347572bcf
translation-type: tm+mt
source-git-commit: a4e53fdcb33eab8afabcb13d651155cd247bda1f
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 0%

---

# Integrering av AEM och Adobe Commerce (Magento) med Commerce Integration Framework {#aem-magento-framework}

Handeln Experience Manager och Adobe (Magento) är sömlöst integrerad med Commerce Integration Framework (CIF). CIF gör det möjligt för AEM att komma åt och kommunicera direkt med den aktuella instansen med Adobe Commerce [GraphQL API:er](https://devdocs.magento.com/guides/v2.4/graphql/).

>[!NOTE]
>
>GraphQL används för närvarande i två (separata) scenarier i Adobe Experience Manager (AEM) som en Cloud Service:
>
>* Detta scenario, där CIF kommunicerar med e-handel via GraphQL.
>* [AEM Content Fragments fungerar tillsammans med det AEM GraphQL-API:t (en anpassad implementering som baseras på standard GraphQL) för att leverera strukturerat innehåll som kan användas i dina program](/help/assets/content-fragments/graphql-api-content-fragments.md).


## Arkitekturöversikt {#overview}

Den övergripande arkitekturen är följande:

![CIF-arkitekturöversikt](../assets/AEM_Magento_Architecture.png)

Inom CIF finns stöd för kommunikationsmönster på serversidan och klientsidan.
API:anrop på serversidan implementeras med den generiska [GraphQL-klienten](https://github.com/adobe/commerce-cif-graphql-client) i kombination med en [uppsättning genererade datamodeller](https://github.com/adobe/commerce-cif-magento-graphql) för GraphQL-schemat Commerce. Dessutom kan alla GraphQL-frågor eller mutationer i GQL-format användas.

För klientkomponenterna, som byggs med [React](https://reactjs.org/), används [Apollo Client](https://www.apollographql.com/docs/react/).

## AEM CIF Core Component Architecture {#cif-core-components}

![AEM CIF Core Component Architecture](../assets/cif-component-architecture.jpg)

[AEM CIF Core ](https://github.com/adobe/aem-core-cif-components) Components följer mycket liknande designmönster och bästa praxis som  [AEM WCM Core Components](https://github.com/adobe/aem-core-wcm-components).

Affärslogik och backend-kommunikation med Adobe Commerce för AEM CIF Core Components implementeras i Sling Models. Om det är nödvändigt att anpassa den här logiken för att uppfylla projektspecifika krav kan delegeringsmönstret för segmenteringsmodeller användas.

>[!TIP]
>
>Sidan [Anpassa AEM CIF Core Components](../customizing/customize-cif-components.md) innehåller ett detaljerat exempel och bästa praxis för att anpassa CIF Core Components.

I projekt kan AEM CIF Core Components och anpassade projektkomponenter enkelt hämta den konfigurerade klienten för en Adobe Commerce-butik som är kopplad till en AEM sida via Sling Context-Aware-konfiguration.

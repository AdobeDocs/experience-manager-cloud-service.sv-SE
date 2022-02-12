---
title: AEM och Adobe Commerce Integration med Commerce Integration Framework
description: AEM och Adobe Commerce integreras smidigt med Commerce Integration Framework (CIF). Med CIF kan AEM få åtkomst till en Adobe Commerce-instans och kommunicera med Adobe Commerce via GraphQL. AEM Authors kan också använda produkt- och kategoriväljare och produktkonsolen för att bläddra bland produkt- och kategoridata som hämtas on demand från Adobe Commerce. Dessutom erbjuder CIF en färdig butik som kan snabba upp affärsprojekt.
thumbnail: aem-magento-architecture.jpg
exl-id: 110ceef5-2c35-4b81-8e89-26929c0da91b,1cdfda88-a728-432f-b24a-f81347572bcf
source-git-commit: e304b49b44cf871f3c47120fad7899407c573234
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 0%

---

# AEM och Adobe Commerce Integration Using Commerce Integration Framework {#aem-framework}

Experience Manager och Adobe Commerce integreras smidigt med Commerce Integration Framework (CIF). CIF gör det möjligt för AEM att komma åt och kommunicera direkt med handelsinstansen med hjälp av Adobe Commerce [GraphQL API:er](https://devdocs.magento.com/guides/v2.4/graphql/).

>[!NOTE]
>
> Lägsta GraphQL API-version som stöds är 2.3.5. Vissa funktioner stöds endast i nyare versioner eller bara i Adobe Commerce.

>[!NOTE]
>
>GraphQL används för närvarande i två (separata) scenarier i Adobe Experience Manager (AEM) as a Cloud Service:
>
>* Detta scenario, där CIF kommunicerar med e-handel via GraphQL.
>* [AEM Content Fragments fungerar tillsammans med det AEM GraphQL-API:t (en anpassad implementering som bygger på standard GraphQL) för att leverera strukturerat innehåll som kan användas i dina program](/help/headless/graphql-api/content-fragments.md).


## Arkitektur - översikt {#overview}

Den övergripande arkitekturen är följande:

![CIF-arkitekturöversikt](../assets/AEM_Magento_Architecture.png)

Inom CIF finns stöd för kommunikationsmönster på serversidan och klientsidan.
API-anrop på serversidan implementeras med hjälp av de inbyggda, generiska [GraphQL-klient](https://github.com/adobe/commerce-cif-graphql-client) i kombination med en [uppsättning genererade datamodeller](https://github.com/adobe/commerce-cif-magento-graphql) för Commerce GraphQL-schemat. Dessutom kan alla GraphQL-frågor eller mutationer i GQL-format användas.

För komponenterna på klientsidan, som byggs med [Reagera](https://reactjs.org/), [Apollo Client](https://www.apollographql.com/docs/react/) används.

## AEM CIF Core Component Architecture {#cif-core-components}

![AEM CIF Core Component Architecture](../assets/cif-component-architecture.jpg)

[AEM CIF-kärnkomponenter](https://github.com/adobe/aem-core-cif-components) följer mycket liknande designmönster och bästa praxis som [AEM WCM-kärnkomponenter](https://github.com/adobe/aem-core-wcm-components).

Affärslogik och backend-kommunikation med Adobe Commerce för AEM CIF Core Components implementeras i Sling Models. Om det är nödvändigt att anpassa den här logiken för att uppfylla projektspecifika krav kan delegeringsmönstret för segmenteringsmodeller användas.

>[!TIP]
>
>The [Anpassa AEM CIF-kärnkomponenter](../customizing/customize-cif-components.md) sidan innehåller ett detaljerat exempel och bästa praxis för anpassning av CIF-kärnkomponenter.

I projekt kan AEM CIF Core Components och anpassade projektkomponenter enkelt hämta den konfigurerade klienten för en Adobe Commerce-butik som är kopplad till en AEM sida via Sling Context-Aware-konfiguration.

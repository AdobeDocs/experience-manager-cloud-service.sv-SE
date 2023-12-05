---
title: AEM och Adobe Commerce Integration med Commerce integration framework
description: AEM och Adobe Commerce är helintegrerade med Commerce integrationa frameworken (CIF). Med CIF kan AEM få åtkomst till en Adobe Commerce-instans och kommunicera med Adobe Commerce via GraphQL. AEM kan också använda produkt- och kategoriväljare och produktkonsolen för att bläddra bland produkt- och kategoridata som hämtas on demand från Adobe Commerce. Dessutom har CIF en färdig butik som kan snabba upp affärsprojekt.
thumbnail: aem-magento-architecture.jpg
exl-id: 110ceef5-2c35-4b81-8e89-26929c0da91b
source-git-commit: 6d63328ca17a00e0369c57714409f3f448cb311f
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 0%

---

# AEM och Adobe Commerce Integration Using Commerce integration framework {#aem-framework}

Experience Manager och Adobe Commerce är helintegrerade med Commerce integrationa frameworken (CIF). CIF gör att AEM kan komma åt och kommunicera direkt med handelsinstansen med Adobe Commerce [GraphQL API:er](https://devdocs.magento.com/guides/v2.4/graphql/).

>[!NOTE]
>
> Den lägsta GraphQL API-version som stöds är 2.3.5. Vissa funktioner stöds endast i nyare versioner eller bara i Adobe Commerce.

>[!NOTE]
>
>GraphQL används för närvarande i två (separata) scenarier i Adobe Experience Manager (AEM) as a Cloud Service:
>
>* Detta scenario, där CIF kommunicerar med e-handel via GraphQL.
>* [AEM Content Fragments fungerar tillsammans med det AEM GraphQL-API:t (en anpassad implementering som baseras på GraphQL) för att leverera strukturerat innehåll som kan användas i dina program](/help/headless/graphql-api/content-fragments.md).

## Arkitektur - översikt {#overview}

Den övergripande arkitekturen är följande:

![Översikt över CIF](../assets/AEM_Magento_Architecture.png)

Inom CIF finns stöd för kommunikationsmönster på serversidan och klientsidan.
API-anrop på serversidan implementeras med hjälp av de inbyggda, generiska [GraphQL-klient](https://github.com/adobe/commerce-cif-graphql-client) i kombination med en [uppsättning genererade datamodeller](https://github.com/adobe/commerce-cif-magento-graphql) för e-handelsschemat i GraphQL. Alla GraphQL-frågor och mutationer i GQL-format kan också användas.

För komponenterna på klientsidan, som byggs med [Reagera](https://reactjs.org/), [Apollo Client](https://www.apollographql.com/docs/react/) används.

## AEM CIF Core Component Architecture {#cif-core-components}

![AEM CIF Core Component Architecture](../assets/cif-component-architecture.jpg)

[AEM CIF-kärnkomponenter](https://github.com/adobe/aem-core-cif-components) följer mycket liknande designmönster och bästa praxis som [AEM WCM-kärnkomponenter](https://github.com/adobe/aem-core-wcm-components).

Affärslogik och serverdelskommunikation med Adobe Commerce för de AEM kärnkomponenterna implementeras i Sling Models. Om det är nödvändigt att anpassa den här logiken för att uppfylla projektspecifika krav kan delegeringsmönstret för segmenteringsmodeller användas.

>[!TIP]
>
>The [Anpassa AEM CIF kärnkomponenter](../customizing/customize-cif-components.md) sidan innehåller ett detaljerat exempel och bästa praxis för anpassning CIF kärnkomponenter.

I projekt kan AEM kärnkomponenter och anpassade projektkomponenter enkelt hämta den konfigurerade klienten för en Adobe Commerce-butik som är kopplad till en AEM sida via Sling Context-Aware-konfiguration.

## Sök {#search}

CIF har en färdig [Sökkärnkomponent](https://www.aemcomponents.dev/content/core-components-examples/library/commerce/search.html) som är en renderad sökupplevelse på serversidan baserad på [Commerce GraphQL API](https://developer.adobe.com/commerce/webapi/graphql/). Commerce-kunder har möjlighet att använda [Live Search](https://experienceleague.adobe.com/docs/commerce-merchant-services/live-search/guide-overview.html?lang=en) i stället. Följ detta [link](/help/commerce-cloud/integrating/live-search-plp.md) om du vill veta mer om CIF - Live Search-integrering.


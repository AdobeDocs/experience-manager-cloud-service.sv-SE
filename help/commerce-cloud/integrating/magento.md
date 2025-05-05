---
title: AEM och Adobe Commerce Integration med Commerce integration framework
description: AEM och Adobe Commerce är helintegrerade med Commerce integrationa frameworken (CIF). Med CIF kan AEM få åtkomst till en Adobe Commerce-instans och kommunicera med Adobe Commerce via GraphQL. AEM kan också använda produkt- och kategoriväljare och produktkonsolen för att bläddra bland produkt- och kategoridata som hämtas on demand från Adobe Commerce. Dessutom har CIF en färdig butik som kan snabba upp affärsprojekt.
thumbnail: aem-magento-architecture.jpg
exl-id: 110ceef5-2c35-4b81-8e89-26929c0da91b
feature: Commerce Integration Framework
role: Admin
source-git-commit: 0e328d013f3c5b9b965010e4e410b6fda2de042e
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 0%

---

# AEM och Adobe Commerce Integration Using Commerce integration framework {#aem-framework}

Experience Manager och Adobe Commerce är helintegrerade med Commerce integrationa frameworken (CIF). CIF gör att AEM kan komma åt och kommunicera direkt med e-handelsinstansen med Adobe Commerce [GraphQL API:er](https://devdocs.magento.com/guides/v2.4/graphql/).

>[!NOTE]
>
> Den lägsta GraphQL API-version som stöds är 2.3.5. Vissa funktioner stöds endast i nyare versioner eller bara i Adobe Commerce.

>[!NOTE]
>
>GraphQL används för närvarande i två (separata) scenarier i Adobe Experience Manager (AEM) as a Cloud Service:
>
>* Detta scenario, där CIF kommunicerar med e-handel via GraphQL.
>* [AEM Innehållsfragment fungerar tillsammans med det AEM GraphQL-API:t (en anpassad implementering som baseras på standard-GraphQL) för att leverera strukturerat innehåll som ska användas i dina program](/help/headless/graphql-api/content-fragments.md).

## Arkitektur - översikt {#overview}

Den övergripande arkitekturen är följande:

![CIF Översikt över arkitekturen](../assets/AEM_Magento_Architecture.png)

Inom CIF finns stöd för kommunikationsmönster på serversidan och klientsidan.
API-anrop på serversidan implementeras med den inbyggda, generiska [GraphQL-klienten](https://github.com/adobe/commerce-cif-graphql-client) i kombination med en [uppsättning genererade datamodeller](https://github.com/adobe/commerce-cif-magento-graphql) för Commerce GraphQL-schemat. Alla GraphQL-frågor och mutationer i GQL-format kan också användas.

För komponenter på klientsidan, som har skapats med [React](https://reactjs.org/), används [Apollo-klienten](https://www.apollographql.com/docs/react/).

## AEM CIF Core Component Architecture {#cif-core-components}

![AEM CIF Core Component Architecture](../assets/cif-component-architecture.jpg)

[AEM CIF kärnkomponenter](https://github.com/adobe/aem-core-cif-components) följer mycket liknande designmönster och metodtips som [AEM WCM-kärnkomponenter](https://github.com/adobe/aem-core-wcm-components).

Affärslogik och serverdelskommunikation med Adobe Commerce för de AEM kärnkomponenterna implementeras i Sling Models. Om det är nödvändigt att anpassa den här logiken för att uppfylla projektspecifika krav kan delegeringsmönstret för segmenteringsmodeller användas.

>[!TIP]
>
>Sidan [Anpassa AEM ](../customizing/customize-cif-components.md) CIF kärnkomponenter innehåller ett detaljerat exempel och bästa praxis för hur du anpassar CIF kärnkomponenter.

I projekt kan AEM kärnkomponenter och anpassade projektkomponenter enkelt hämta den konfigurerade klienten för en Adobe Commerce-butik som är kopplad till en AEM sida via Sling Context-Aware-konfiguration.

## Sök {#search}

CIF tillhandahåller en [sökkärnkomponent](https://www.aemcomponents.dev/content/core-components-examples/library/commerce/search.html) som är en renderad sökupplevelse på serversidan som baseras på [Commerce GraphQL API](https://developer.adobe.com/commerce/webapi/graphql/). Commerce-kunder kan använda [Live Search](https://experienceleague.adobe.com/docs/commerce-merchant-services/live-search/guide-overview.html?lang=sv-SE) i stället. Följ den här [länken](/help/commerce-cloud/integrating/live-search-plp.md) om du vill veta mer om CIF - Live Search-integrering.


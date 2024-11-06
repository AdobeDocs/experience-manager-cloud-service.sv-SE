---
title: AEM REST OpenAPI for Content Fragment Delivery
description: Läs mer om AEM REST OpenAPI for Content Fragment Delivery
feature: Headless, Content Fragments, Edge Delivery Services
role: Admin, Developer
source-git-commit: d98aa9d206486022d465ca19c8888088562d56c3
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 0%

---


# AEM REST OpenAPI for Content Fragment Delivery {#aem-rest-openapi-for-content-fragment-delivery}

>[!IMPORTANT]
>
>Detta API är tillgängligt via Early Adobe Program.
>
>Kontrollera [Versionsinformation](/help/release-notes/release-notes-cloud/release-notes-current.md) om du vill se status och hur du tillämpar den om du är intresserad.

I Adobe Experience Manager (AEM) as a Cloud Service AEM REST OpenAPI for Content Fragment Delivery:

* är ett HTTP REST API på [AEM Edge Delivery Services](/help/edge/overview.md), utformat för att leverera strukturerat innehåll från innehållsfragment i JSON-format
* erbjuder en modern CDN-integrering som tillåter att aktivt innehåll ogiltigförklaras
* fokuserar på innehållsleverans (prestanda, skalbarhet, CDN-integrering, optimerad JSON-kontroll och utdata)
* inkluderar möjlighet att hydratisera JSON för refererade fragment och resurser

Detta API:

* är efterträdare till [Stöd för innehållsfragment i AEM Assets HTTP API](/help/assets/content-fragments/assets-api-content-fragments.md)

* kompletterar [Content Fragments och Content Fragment Models OpenAPI:er](/help/headless/content-fragment-openapis.md), som gör att du kan hantera innehålls- och Content Fragment Models (CRUD)

* är ett HTTP REST-alternativ till [AEM GraphQL-API som används med innehållsfragment](/help/headless/graphql-api/content-fragments.md)

Fullständig dokumentation finns i [AEM Sites API-scheman - Content Fragments Delivery API (2024.07-experimentell)](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/sites/delivery/).

>[!NOTE]
>
>Se [AEM API:er för leverans och hantering av strukturerat innehåll](/help/headless/apis-headless-and-content-fragments.md) för en översikt över de olika tillgängliga API:erna och en jämförelse av några av de berörda begreppen.

## Cachning {#caching}

AEM kan integreras med AEM CDN snabbt. Det innebär att JSON-svar som hanteras på publiceringsnivån cachelagras på snabbnivå.

Svaren cachelagras sedan baserat på fördefinierade cache-huvuden (kan inte konfigureras):

* Svaren cachelagras i 5 minuter i webbläsarens/klientens cache
   * `max-age`=`300`
* Svaren cachelagras i 1 timme i CDN-cachen
   * `s-maxage`=`3600`
* Inaktuellt innehåll kan hanteras samtidigt som nya begäranden valideras i upp till en timme
   * `stale-while-revalidate`=`3600`
* Inaktuellt innehåll kan hanteras av misstag i upp till 1 dag
   * `stale-on-error`=`86400`

AEM innehåller även en aktiv CDN-cacheogiltigförklaring. Det innebär att när innehåll uppdateras, eller publiceras, blir motsvarande JSON OpenAPI-svar automatiskt ogiltiga, via en begäran om mjuk tömning till Fast. Detta gör att du kan se ändringar som återspeglas i JSON-utdata innan den faktiska CDN-cacheåldern (`s-maxage`) nås.
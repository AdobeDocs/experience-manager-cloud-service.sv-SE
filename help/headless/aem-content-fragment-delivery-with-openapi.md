---
title: AEM Content Fragment Delivery with OpenAPI
description: Läs mer om AEM Content Fragment Delivery med OpenAPI
feature: Headless, Content Fragments, Edge Delivery Services
role: Admin, Developer
exl-id: b298db37-1033-4849-bc12-7db29fb77777
source-git-commit: 163964a7183996226b14f3c803afa4c5bd58f848
workflow-type: tm+mt
source-wordcount: '475'
ht-degree: 0%

---

# AEM Content Fragment Delivery with OpenAPI {#aem-content-fragment-delivery-with-openapi}

I Adobe Experience Manager (AEM) as a Cloud Service, AEM OpenAPI for Content Fragment Delivery:

* är ett OpenAPI som är optimerat för direktleverans av AEM Content Fragments i JSON-format.
* erbjuder en modern CDN-integrering som tillåter att aktivt innehåll ogiltigförklaras
* fokuserar på innehållsleverans (prestanda, skalbarhet, CDN-integrering, optimerad JSON-kontroll och utdata)
* inkluderar möjlighet att hydratisera JSON för refererade fragment och resurser

Detta API:

* är efterträdare till [Stöd för innehållsfragment i AEM Assets HTTP API](/help/assets/content-fragments/assets-api-content-fragments.md)

* kompletterar [Content Fragments och Content Fragment Models OpenAPI:er](/help/headless/content-fragment-openapis.md), som gör att du kan hantera innehålls- och Content Fragment Models (CRUD)

* är ett HTTP REST-alternativ till [AEM GraphQL-API för användning med innehållsfragment](/help/headless/graphql-api/content-fragments.md)

Fullständig dokumentation finns i [AEM Content Fragment Delivery with OpenAPI](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/contentfragments/delivery/).

>[!NOTE]
>
>Se [AEM API:er för leverans och hantering av strukturerat innehåll](/help/headless/apis-headless-and-content-fragments.md) för en översikt över de olika tillgängliga API:erna och en jämförelse av några av de koncept som ingår.

>[!IMPORTANT]
>
>Om du vill aktivera Content Fragment Delivery med OpenAPI i AEM as a Cloud Service måste du kontrollera att det inte redan är aktiverat och sedan skicka en Adobe Support-biljett med titeln **Enable Content Fragment Delivery with OpenAPI** och ange:
>
>* Cloud Service program- och miljö-ID:n
>* information om det användningsfall du vill lösa med Content Fragment Delivery OpenAPI
>* information om alla dina kontakter som Adobe ska svara på och hålla dig informerad om begäran och projektet (om det behövs)

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

Content Fragment Delivery med OpenAPI har stöd för aktiv CDN-cacheogiltigförklaring. Det innebär att när innehåll uppdateras, eller publiceras, blir motsvarande JSON OpenAPI-svar automatiskt ogiltiga, via en begäran om mjuk tömning till Fast. Detta gör att du kan se ändringar som återspeglas i JSON-utdata innan den faktiska CDN-cacheåldern (`s-maxage`) nås.

## Tillgänglighet {#availability}

Content Fragment Delivery with OpenAPI är tillgängligt på nivåerna Förhandsgranska och Publicera. OpenAPI innehåller innehållsfragment i JSON-format, både för förhandsgranskning och direktleverans.

Förhandsgranska Content Fragment Delivery with OpenAPI:

* publicera till Förhandsgranska
* aktivera åtkomst till förhandsgranskning med IP tillåtelselista
* hämta URL:en för förhandsgranskning

## CORS {#cors}

[CORS tillåtna ursprung](/help/headless/deployment/cross-origin-resource-sharing.md) definierar de ursprung som kan anropa API:t.

CORS tillåtna ursprung som definieras på dispatcherkonfigurationssidan, speciellt för GraphQL, beaktas inte av detta API.

<!-- 
## API Rate Limits {#api-rate-limits}
-->

<!-- 
## Limitations {#limitations}
-->

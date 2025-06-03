---
title: AEM API:er för strukturerad innehållsleverans och hantering av innehållsfragment
description: Läs mer om API:erna för strukturerad innehållsleverans och hantering av innehållsfragment
feature: Headless, Content Fragments, Edge Delivery Services
role: Admin, Developer
exl-id: 95aecd30-566a-42a9-b97a-7efe45fd389c
source-git-commit: 243adc6f6428cea23c04ca788bd8ad0bda7e4501
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 0%

---

# AEM API:er för leverans och hantering av strukturerat innehåll {#aem-apis-structured-content-delivery-and-management}

Adobe Experience Manager (AEM) as a Cloud Service erbjuder flera API:er för både leverans av strukturerat innehåll från Content Fragments och Content Fragment Management. Mer information om specifika API:er finns på de enskilda sidorna.

* [AEM Content Fragment Delivery with OpenAPI](/help/headless/aem-content-fragment-delivery-with-openapi.md)
   * Detta API skapar JSON-svar för att leverera strukturerat innehåll från innehållsfragment i AEM.
   * En bana till ett innehållsfragment används som slutpunkt.
   * Detta API är REST-baserat.
   * Det är optimerat för innehållsleverans, inklusive CDN-integrering.
* [AEM GraphQL API for Content Fragment delivery](/help/headless/graphql-api/content-fragments.md)
   * Detta API är schemabaserat. API-scheman representeras av Content Fragment Models, som definierar innehållsstrukturen.
   * Detta API är GraphQL-baserat.
* [Content Fragments och Content Fragment Models OpenAPIs](/help/headless/content-fragment-openapis.md)
   * Dessa API:er är avsedda för strukturerad innehållshantering.
   * GET-operatorer är inte optimerade för innehållsleverans.
   * Detta API är REST-baserat.

>[!NOTE]
>
>[Stöd för innehållsfragment i Assets HTTP API](/help/assets/content-fragments/assets-api-content-fragments.md) är nu [inaktuellt](/help/release-notes/deprecated-removed-features.md). Den har ersatts av [Content Fragment Delivery med OpenAPI](/help/headless/aem-content-fragment-delivery-with-openapi.md) tillsammans med [Content Fragments och Content Fragment Models Management OpenAPI:er](/help/headless/content-fragment-openapis.md).

## REST vs GraphQL {#rest-vs-graphql}

Det API som används är ett beslut för utvecklarna - AEM stöder båda.

Många jämförelser finns tillgängliga online, men några av de viktigaste fördelarna med REST är:

* Enkelt

   * Utvecklare är (ofta) bekanta med HTTP och REST. Enligt [Postman State of the APIs report](https://www.postman.com/state-of-api/) använder en hög andel utvecklare REST.

   * Med enkelhet kommer kännedomen. Med REST finns det inga organisatoriska frågor om vem som äger frågorna och vem som äger appen, medan dessa frågor kan uppstå med GraphQL.

   * Med välbekant (vanligtvis) får du tillgång till ett brett användarforum och en bred verktygslandskap. Inte en inneboende nackdel för GraphQL, utan sannolikt en bredare och djupare REST.

   * Den enklare metoden kan också göra säkerhetsimplementeringen enklare. Med REST sker filtreringen för att avgöra vilket innehåll som ska återges i klientprogrammet. Med GraphQL sker detta i en schemabaserad fråga mellan klient och server.

* Flexibilitet

   * Med REST kan utvecklaren `GET` alla resurser. Med GraphQL begränsas de till resurser som definierats i ett schema.

* Cachning

   * JSON-svar på REST `GET`-begäranden är i sig tillgängliga. GraphQL `POST`-begäranden är inte tillgängliga om de inte har gjorts. Det kan till exempel gälla AEM Persisted Queries som är lagrade på servern och begärda med REST-liknande `GET`-begäranden.

Några fördelar med GraphQL:

* Effektiv leverans av innehåll

   * Fokus

      * Med GraphQL kan klientapplikationer begära exakt det innehåll de behöver för återgivning - och inte längre. Den här metoden förhindrar överleverans av innehåll, med överbelastad innehållsladdning och onödig bandbreddskonsumtion.

   * Enskild slutpunkt

      * I REST är varje API-begäran en slutpunkt, men i GraphQL finns det bara en gemensam slutpunkt, och olika innehållsförfrågningar uttrycks som frågor med den gemensamma slutpunkten.

* Snabba prototyper

   * Med GraphQL är detta en enstegsprocess som sammanförts i GraphQL-frågan och som kan underlätta framtagning av prototyper. REST å andra sidan är en tvåstegsprocess:

      1. Hämta innehåll med API.
      2. I JSON-svaret avgör du vad som ska användas för återgivning i klientprogrammet.

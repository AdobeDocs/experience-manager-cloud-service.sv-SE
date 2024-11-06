---
title: AEM-API:er för strukturerad innehållsleverans och hantering av innehållsfragment
description: Läs mer om API:erna för strukturerad innehållsleverans och hantering av innehållsfragment
feature: Headless, Content Fragments, Edge Delivery Services
role: Admin, Developer
source-git-commit: 21599676916068f3529976410a93951b02f750b0
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 0%

---


# AEM-API:er för leverans och hantering av strukturerat innehåll {#aem-apis-structured-content-delivery-and-management}

Adobe Experience Manager (AEM) as a Cloud Service erbjuder flera API:er för både leverans av strukturerat innehåll från Content Fragments och Content Fragment Management. Mer information om specifika API:er finns på de enskilda sidorna.

* [AEM REST OpenAPI för leverans av innehållsfragment](/help/headless/aem-rest-openapi-content-fragment-delivery.md)
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
* [Stöd för innehållsfragment i AEM Assets HTTP API](/help/assets/content-fragments/assets-api-content-fragments.md)
   * Ursprungligt API för JSON-utdata för strukturerad innehållsleverans i AEM.
      * Även om det är robust och bevisat levererar detta API inte *fullständigt hydrerade* JSON-utdata. Referenser genereras bara som sökvägar, vilket kräver sekundära API-begäranden för att hämta ytterligare innehåll.
   * Assets HTTP API kan också användas för att hantera innehållsfragment och modeller för innehållsfragment (CRUD).
   * Detta API är REST-baserat.
   * Stöd för innehållsfragment i Assets HTTP API kommer att bli inaktuellt i framtiden eftersom det genomförs av Edge Delivery Servicens JSON REST API. Tidsskalan har inte fastställts än.

<!--
## JSON vs HTML {#json-vs-HTML}

The content delivery format used is driven by frontend implementation. Unstructured content/HTML for full-stack implementations, structured content/JSON for headless implementations, or a combination of both in hybrid implementations. 

Key considerations include:

* Definition
  * JSON (JavaScript Object Notation) - used to represent, access and process structured data. 
  * HTML (HyperText Markup Language) - a markup language of tags and elements in a hierarchical structure.
* Primary Purpose
  * JSON is often used for transferring structure content between the server and client app.
  * HTML is the standard markup language for creating and rendering web pages in a browser.
-->

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

   * JSON-svar på REST `GET`-begäranden är i sig tillgängliga. GraphQL `POST`-begäranden är inte tillgängliga om de inte görs, till exempel genom att använda AEM beständiga frågor som är lagrade på servern och begärda med REST-liknande `GET`-begäranden.

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

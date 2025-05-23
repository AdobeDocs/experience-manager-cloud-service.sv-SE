---
title: Så här uppdaterar du innehåll via AEM API:er
description: I den här delen av AEM Headless Developer Journey lär du dig hur du använder de tillgängliga API:erna för att komma åt och uppdatera innehållet i dina innehållsfragment.
exl-id: 84120856-fd1d-40f7-8df4-73d4cdfcc43b
solution: Experience Manager
feature: Headless, Content Fragments, GraphQL API
role: Admin, Architect, Developer
source-git-commit: d9db32110e1e0aaa5bdc20bd6b4bff6da6a3a3a3
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 0%

---

# Så här uppdaterar du innehåll via AEM API:er {#update-your-content}

I den här delen av [AEM Headless Developer Journey](overview.md) kan du lära dig hur du använder de tillgängliga API:erna för att komma åt och uppdatera innehållet i dina innehållsfragment.

## Story hittills {#story-so-far}

I det tidigare dokumentet om AEM resa [Så här kommer du åt ditt innehåll via AEM Delivery API:er](access-your-content.md)  och du bör nu:

* Lär dig mer om GraphQL.
* Förstå hur AEM GraphQL API fungerar.
* Förstå några praktiska exempelfrågor.

Den här artikeln bygger på dessa grundläggande funktioner så att du förstår hur du uppdaterar det befintliga headless-innehållet i AEM via de tillgängliga API:erna.

## Syfte {#objective}

* **Målgrupp**: Avancerat
* **Mål**: Lär dig mer om de API:er som är tillgängliga för att komma åt och uppdatera innehållet i dina innehållsfragment.

## AEM API:er för användning med innehållsfragment {#aem-apis-for-use-with-content-fragments}

Adobe Experience Manager (AEM) as a Cloud Service erbjuder flera API:er för både leverans av strukturerat innehåll från Content Fragments och Content Fragment Management. Mer information om specifika API:er finns på de enskilda sidorna.

* AEM Content Fragment Delivery with OpenAPI
   * Detta API skapar JSON-svar för att leverera strukturerat innehåll från innehållsfragment i AEM.
   * En bana till ett innehållsfragment används som slutpunkt.
   * Detta API är REST-baserat.
   * Det är optimerat för innehållsleverans, inklusive CDN-integrering.
* AEM GraphQL API for Content Fragment delivery
   * Detta API är schemabaserat. API-scheman representeras av Content Fragment Models, som definierar innehållsstrukturen.
   * Detta API är GraphQL-baserat.
* Content Fragments och Content Fragment Models OpenAPIs
   * Dessa API:er är avsedda för strukturerad innehållshantering.
   * GET-operatorer är inte optimerade för innehållsleverans.
   * Detta API är REST-baserat.
* Stöd för innehållsfragment i AEM Assets HTTP API
   * Ursprungligt API för JSON-utdata för strukturerad innehållsleverans i AEM.
      * Även om det är robust och bevisat levererar detta API inte *fullständigt hydrerade* JSON-utdata. Referenser genereras bara som sökvägar, vilket kräver sekundära API-begäranden för att hämta ytterligare innehåll.
   * Assets HTTP API kan också användas för att hantera innehållsfragment och modeller för innehållsfragment (CRUD).
   * Detta API är REST-baserat.
   * Stöd för innehållsfragment i Assets HTTP API kommer att bli inaktuellt i framtiden eftersom det följs av Edge Delivery Services JSON REST API. Tidsskalan har inte fastställts än.

## What&#39;s Next {#whats-next}

Nu när du är klar med den här delen av AEM Headless Developer Journey bör du:

* Förstå tillgängliga API:er för AEM.
* Förstå hur innehållsfragment stöds i dessa API:er.

Du bör fortsätta din resa utan AEM genom att nästa gång granska dokumentet [Placera allt tillsammans - Din app och ditt innehåll i AEM Headless](put-it-all-together.md) där du lär dig grunderna och verktygen i AEM-arkitekturen som du behöver för att sätta ihop dina program.

## Ytterligare resurser {#additional-resources}

* [Adobe Experience Manager as a Cloud Service API:er](https://developer.adobe.com/experience-cloud/experience-manager-apis/)
* [AEM API:er för leverans och hantering av strukturerat innehåll](/help/headless/apis-headless-and-content-fragments.md)
* [AEM Content Fragment Delivery with OpenAPI](/help/headless/aem-content-fragment-delivery-with-openapi.md)
* [AEM GraphQL API for Content Fragment delivery](/help/headless/graphql-api/content-fragments.md)
* [Content Fragments och Content Fragment Models OpenAPIs](/help/headless/content-fragment-openapis.md)
* [Stöd för innehållsfragment i AEM Assets HTTP API](/help/assets/content-fragments/assets-api-content-fragments.md)
* [Arbeta med innehållsfragment](/help/sites-cloud/administering/content-fragments/overview.md)
* [AEM Core Components](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=sv-SE)
* [CORS/AEM förklarar](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/cors-security-article-understand.html)
* [Video - Utveckla för CORS med AEM](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/cors-security-technical-video-develop.html)
* [Introduktion till AEM som Headless CMS](/help/headless/introduction.md)
* [AEM Developer Portal](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=sv-SE)
* [Självstudiekurser för Headless i AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=sv-SE)

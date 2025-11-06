---
title: Så här uppdaterar du innehåll via AEM API:er
description: I den här delen av AEM Headless Developer Journey lär du dig hur du använder de tillgängliga API:erna för att komma åt och uppdatera innehållet i dina innehållsfragment.
exl-id: 84120856-fd1d-40f7-8df4-73d4cdfcc43b
solution: Experience Manager
feature: Headless, Content Fragments, GraphQL API
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '503'
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

>[!NOTE]
>
>[Stöd för innehållsfragment i Assets HTTP API](/help/assets/content-fragments/assets-api-content-fragments.md) är nu [inaktuellt](/help/release-notes/deprecated-removed-features.md). Den har ersatts av [Content Fragment Delivery med OpenAPI](/help/headless/aem-content-fragment-delivery-with-openapi.md) tillsammans med [Content Fragments och Content Fragment Models Management OpenAPI:er](/help/headless/content-fragment-openapis.md).

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
* [CORS/AEM förklarar](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html?lang=sv-SE)
* [Video - Utveckla för CORS med AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/develop-for-cross-origin-resource-sharing.html?lang=sv-SE)
* [Introduktion till AEM som Headless CMS](/help/headless/introduction.md)
* [AEM Developer Portal](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=sv-SE)
* [Självstudiekurser för Headless i AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=sv-SE)

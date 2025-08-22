---
title: Använda innehållsfragment med Adobe Journey Optimizer
description: Läs om hur Content Fragments kan integreras och användas med Adobe Journey Optimizer.
feature: Content Fragments
role: User, Developer, Architect
solution: Experience Manager Sites
exl-id: 4090ee41-80f1-4389-8961-e4af891f01ff
source-git-commit: 0fd7b2633488ceb14d34b1978a91a3a830d8762a
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 2%

---

# Innehållsfragment med Adobe Journey Optimizer {#content-fragments-with-journey-optimizer}

[Adobe Journey Optimizer](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/get-started/get-started) hjälper er att leverera sammankopplade, kontextuella och personaliserade upplevelser till era kunder. Genom att integrera Adobe Experience Manager (AEM) as a Cloud Service med Adobe Journey Optimizer (AJO) kan du återanvända AEM-innehåll i dina inkommande AJO-kanaler och i dina utgående AJO-kanaler, inklusive webb, SMS, e-post och andra.

Du kan till exempel:

* införliva dina [AEM Content Fragments](/help/sites-cloud/administering/content-fragments/overview.md) i ditt [Journey Optimizer e-postinnehåll](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/channels/email/email-landing-page)
* förgranska AJO direkt från AEM

Kopplingen mellan Content Fragments och AJO förenklar processen att komma åt och utnyttja AEM-innehåll, vilket gör det möjligt att skapa personaliserade och dynamiska kampanjer och resor.

Mer information finns i AJO-dokumentationen:

* [Använda innehållsfragment i AJO](https://experienceleague.adobe.com/docs/journey-optimizer/using/integrations/aem-fragments.html?lang=sv-SE#integrations)
* [Integrering av AJO-erbjudanden med innehållsfragment](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/decisioning/offer-decisioning/managing-offers-in-the-offer-library/configure-offers/add-representations#urls)

## Dispatcher Configuration {#dispatcher-configuration}

Om du vill att AJO ska kunna komma åt AEM Content Fragments via [API:t för hantering av innehållsfragment](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/) måste du konfigurera Dispatcher:

* I `dispatcher/src/conf.dispatcher.d/filters/filters.any`:

* Lägg till:

  ```xml
  # Allow Content Fragments API requests, required for integration with AJO 
  /200 {/type "allow" /url "/adobe/sites/cf/*" }
  ```

## Ytterligare information {#further-information}

Mer information finns i:

* Tillägget [Externa referenser från AJO](/help/sites-cloud/administering/content-fragments/extension-content-fragment-ajo-external-references.md)

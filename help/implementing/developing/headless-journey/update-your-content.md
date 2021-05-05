---
title: Så här uppdaterar du innehåll via AEM Assets API:er
description: I den här delen av den AEM Headless Developer Journey kan du lära dig hur du använder REST API för att komma åt och uppdatera innehållet i dina innehållsfragment.
hide: true
hidefromtoc: true
index: false
exl-id: 8d133b78-ca36-4c3b-815d-392d41841b5c
translation-type: tm+mt
source-git-commit: 3d5ea8df4cefdb8c2bebe26333002a4680fa9fd4
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 1%

---

# Så här uppdaterar du ditt innehåll via AEM Assets API:er {#update-your-content}

>[!CAUTION]
>
>ARBETE PÅGÅR - Dokumentet skapas för närvarande och ska inte tolkas som fullständigt eller slutgiltigt och inte heller användas i tillverkningssyfte.

I den här delen av [AEM Headless Developer Journey](overview.md) lär du dig hur du använder REST API för att komma åt och uppdatera innehållet i dina innehållsfragment.

## Berättelsen hittills {#story-so-far}

I det föregående dokumentet på den AEM resan [Hur du får åtkomst till ditt innehåll via AEM Delivery APIs](access-your-content.md) lärde du dig att få åtkomst till ditt headless-innehåll i AEM via AEM GraphQL API och du bör nu:

* Lär dig mer om GraphQL.
* Förstå hur AEM GraphQL API fungerar.
* Förstå några praktiska exempelfrågor.

Den här artikeln bygger på dessa grundläggande funktioner så att du förstår hur du uppdaterar det befintliga headless-innehållet i AEM via REST API.

## Mål {#objective}

* **Målgrupp**: Avancerat
* **Mål**: Lär dig hur du använder REST API för att komma åt och uppdatera innehållet i dina innehållsfragment:
   * Introducera AEM Assets HTTP API.
   * Presentera och diskutera stöd för innehållsfragment i API:t.
   * Visa information om API:t.
   * Titta på exempelkoden för att se hur saker och ting fungerar i praktiken.

## What&#39;s Next {#whats-next}

Nu när du är klar med den här delen av AEM Headless Developer Journey ska du:

* Förstå AEM Assets HTTP API.
* Förstå hur innehållsfragment stöds i detta API.
* Upplev exempelkod och veta hur API:t fungerar i praktiken.

Du bör fortsätta din AEM resa utan att behöva besöka dokumentet nästa gång [Placera allt tillsammans - Din app och ditt innehåll i AEM Headless](put-it-all-together.md) där du får lära dig hur du tar ditt AEM Headless-projekt och förbereder det för publicering.

## Ytterligare resurser {#additional-resources}

* [HTTP API för Assets](/help/assets/mac-api-assets.md)
* [Innehållsfragment REST API](/help/assets/content-fragments/assets-api-content-fragments.md)

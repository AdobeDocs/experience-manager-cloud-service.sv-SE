---
title: Introduktion till Assets as a Cloud Service
description: Nyheter i Assets som Cloud Service.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 26833f59f21efa4de33969b7ae2e782fe5db8a14
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 3%

---


# Nu kommer Assets as a Cloud Service {#assets-cloud-service-introduction}

<!-- Need review information from gklebus -->

Adobe Experience Manager Assets som Cloud Service är en molnbaserad, PaaS-lösning som gör att företag inte bara kan utföra sina Digital Asset Management- och Dynamic Media-åtgärder snabbt och effektivt, utan även använda nästa generations smarta funktioner, som AI/ML, inifrån ett system som alltid är tillgängligt och alltid håller på att lära sig.

Samtidig inmatning av många resurser eller komplexa resurser är en resurskrävande uppgift för en AEM Author-instans. Den primära instansen förbrukar mycket processorkraft, minne och I/O-resurser när resurser läggs till, bearbetas eller till och med migreras. Sådana prestandaproblem påverkar redigering och surfning hos slutanvändarna.

Företag behöver stöd för en mängd olika filformat och innehållsupplösningar för användning på flera enheter, i olika geografiska områden och på flera språk. Resurshanterings- och lagringskrav kräver resurser och funktioner som kan överbelasta en traditionell lösning. Ibland ger inte tekniska begränsningar av behandlingen av tillgångar de resultat man önskar och i andra fall är kostnaden för lagring ett hinder för vinstmarginalerna.

Börja med att förstå [fördelarna med ett molnbaserat erbjudande](#solution-benefits). Se de betydande [förändringarna av AEM som en Cloud Service](/help/release-notes/aem-cloud-changes.md) som också påverkade Experience Manager Assets och följde upp de betydande [förändringarna av Assets](/help/assets/assets-cloud-changes.md).

Läs vidare för att få [information om de nya Assets-funktionerna](#whats-new-assets) och de [kända problemen](/help/release-notes/known-issues.md). Se en lista över [borttagna eller borttagna funktioner](/help/release-notes/deprecated-removed-features.md) för att ta reda på vad som tas bort i den här versionen och se den här [listan över kommande funktioner](/help/release-notes/known-issues.md#upcoming-assets-capabilities) för att ta reda på vad som kommer inom kort. Slutligen, förstå AEM termer med hjälp av den här [ordlistan](/help/overview/terminology.md).

## Lösningsfördelar {#solution-benefits}

Nedan beskrivs de viktigaste fördelarna med Assets som Cloud Service. Mer information finns i [översikt över Experience Manager som en Cloud Service](/help/overview/introduction.md).

* **Modern Cloud Service för bearbetning** av resurser: De nya mikrotjänsterna är en molnbaserad, skalbar, tillförlitlig och problemfri tjänst för bearbetning av resurser.
* **Mycket skalbar**: Elastisk skalbarhet för alla typer av driftsättningar. Praktiskt taget obegränsade resurser som finns tillgängliga on-demand, vid behov. Sparar kostnaden för överdesign jämfört med ett traditionellt system.
* **Senaste programvara**: Alltid aktuell och alltid uppdaterad. Alla användare har bara den senaste programvaran med alla korrigeringar, funktioner, säkerhet och felkorrigeringar tillgängliga. Utvecklare och integratörer arbetar med den senaste uppsättningen API:er utan problem med stöd för flera versioner.
* **Alltid online**: Noll driftavbrott (0dt) tack vare instansen som distribuerats i ett kluster med säkerhetskopior och redundans. Uppgraderingar är också 0dt.
* **Konstantövervakning**: Övervakningen av systemet är automatiserade och inbyggda kontroller och utlösare som hjälper till att upprätthålla prestanda, tillgänglighet och övergripande tillförlitlighet.
* **Smidig driftsättning**: AEM i molnåtgärderna är helt automatiserade och kräver ingen manuell åtgärd. För automatiserad driftsättning automatiserar komponenten Cloud Manager (CM) byggandet av driftsättningsbara Docker-bilder som innehåller din anpassade kod.

## Nya Assets-funktioner {#whats-new-assets}

De viktiga nya funktionerna är:

* [Asset-mikrotjänster](/help/assets/asset-microservices-overview.md)
* [Metoder för överföring av resurser](/help/assets/add-assets.md)

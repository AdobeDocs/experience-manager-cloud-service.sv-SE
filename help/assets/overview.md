---
title: Adobe Digital Asset Management (DAM) med AEM
description: Lär dig hur du använder och administrerar Adobe Digital Asset Management (DAM) med Experience Manager Assets as a Cloud Service.
contentOwner: AK
feature: Asset Management
role: User, Leader, Architect
exl-id: 4437f214-d058-4975-8b8f-869a12c8103b
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 2%

---


# Vi presenterar Assets som [!DNL Cloud Service] för Digital Asset Management i AEM {#assets-cloud-service-introduction}

<!-- Need review information from gklebus -->

Adobe Experience Manager Assets som [!DNL Cloud Service] erbjuder en molnbaserad, PaaS-lösning för företag att inte bara utföra sina Digital Asset Management- och Dynamic Media-åtgärder snabbt och effektivt, utan även använda nästa generations smarta funktioner, som AI/ML, inifrån ett system som alltid är aktuellt, alltid tillgängligt och alltid håller på att lära sig.

Samtidig inmatning av många resurser eller komplexa resurser är en resurskrävande uppgift för en Experience Manager Author-instans. Den primära instansen kräver stora CPU-, minnes- och I/O-resurser när resurser läggs till, bearbetas eller till och med migreras. Sådana prestandaproblem påverkar redigering och surfning hos slutanvändarna.

Företag behöver stöd för en mängd olika filformat och innehållsupplösningar för användning på flera enheter, i olika geografiska områden och på flera språk. Resurshanterings- och lagringskrav kräver resurser och funktioner som kan överbelasta en traditionell lösning. Ibland ger inte tekniska begränsningar av behandlingen av tillgångar de resultat man önskar och i andra fall är kostnaden för lagring ett hinder för vinstmarginalerna.

Börja med att förstå [fördelarna med ett molnbaserat erbjudande](#solution-benefits) för hantering av digitala resurser. Kolla in de [ändringarna av Experience Manager som en [!DNL Cloud Service]](/help/release-notes/aem-cloud-changes.md) som också påverkar Experience Manager Assets och följ upp de [ändringarna av Assets](/help/assets/assets-cloud-changes.md) som är anmärkningsvärda.

Läs vidare om du vill veta [mer om de nya Assets-funktionerna](#whats-new-assets) och [kända problem](/help/release-notes/maintenance/latest.md). Se en lista över [borttagna eller borttagna funktioner](/help/release-notes/deprecated-removed-features.md) om du vill veta vad som har tagits bort i den här versionen. Lär dig slutligen Experience Manager-villkoren med hjälp av den här [ordlistan](/help/overview/terminology.md).

## Lösningsfördelar {#solution-benefits}

Följande är de viktigaste fördelarna med Assets som [!DNL Cloud Service] för Digital Asset Management. Mer information finns i [översikt över Experience Manager som en [!DNL Cloud Service]](/help/overview/introduction.md).

* **Moderna molntjänster för bearbetning av resurser**: De nya mikrotjänsterna är en molnbaserad, skalbar, tillförlitlig och problemfri tjänst för bearbetning av resurser.
* **Mycket skalbar**: Elastisk skalbarhet för alla typer av distributioner. Praktiskt taget obegränsade resurser som finns tillgängliga on-demand, vid behov. Sparar kostnaden för överdesign jämfört med ett traditionellt system.
* **Senaste programvara**: Alltid aktuell och alltid uppdaterad. Alla användare har bara den senaste programvaran med alla korrigeringar, funktioner, säkerhet och felkorrigeringar tillgängliga. Utvecklare och integratörer arbetar med den senaste uppsättningen API:er utan problem med stöd för flera versioner.
* **Alltid online**: Nollställ driftavbrott (0dt) tack vare instansen som distribuerats i ett kluster med säkerhetskopieringar och redundans. Uppgraderingar är också 0dt.
* **Konstantövervakning**: Övervakningen av systemet är automatiserad och inbyggd kontroll och utlösare som hjälper till att upprätthålla prestanda, tillgänglighet och övergripande tillförlitlighet.
* **Problemfria distributioner**: Experience Manager i molnåtgärderna är helt automatiserade och kräver ingen manuell åtgärd. För automatiserad driftsättning automatiserar Cloud Manager-komponenten (CM) byggandet av driftsättningsbara Docker-bilder som innehåller din anpassade kod.

## Tillgängliga personbaserade upplevelser för hantering av digitala resurser {#persona-based-experiences}

Adobe erbjuder robusta DAM-lösningar (Digital Asset Management) så att ni får ut mesta möjliga av era digitala resurser. Adobe Experience Manager Assets har två separata upplevelser som använder samma molntjänstdatabas:

* **Administratörsvy**: Det befintliga användargränssnittet i Assets as a Cloud Service. Använd administrationsvyn för alla avancerade funktioner för hantering av digitala resurser, inklusive integreringar, arbetsflöden, innehållsautomatisering, publicering med mera.

* **Assets View**: Adobe lättviktiga resurshantering för att lagra, hantera, identifiera och använda digitala resurser. Effektivt användargränssnitt med viktiga funktioner för hantering av digitala resurser. Utformad för enklare DAM-användare med fokus på överföring, metadatahantering, sökning, hämtning och delning.

Användare som har åtkomst till administrationsvyn har även åtkomst till vyn Assets. Assets View har ett förenklat användargränssnitt som gör det enkelt att hantera, upptäcka och distribuera digitala resurser. Ett stort antal användare från olika funktioner, inklusive kreatörer, marknadsförare och branschgrupper, kan samarbeta om resurser och få tillgång till rätt, godkänt material när och var de behöver det. Många tillfälliga DAM-användare föredrar Assets-vyn eftersom den bara innehåller en delmängd av funktioner. Upplevelsen riktar sig till kreatörer, skrivskyddade mediekonsumenter och användare med mindre vikt-DAM.

DAM-bibliotek, utvecklare och superanvändare kan fortsätta att använda administrationsvyn eller växla mellan användargränssnitten efter behov. Du kan välja den upplevelse som fungerar bäst för din roll.

![add-tags](assets/newui-overview.svg)

Mer information om hur du kommer åt vyn Assets och vissa av de förenklingar som den erbjuder via administratörsvyn finns i [Introduktion till vyn Assets](/help/assets/assets-view-introduction.md).

## Integrering med dokumentbaserad redigering för Edge Delivery Services {#integrate-doc-authoring-edge-and-assets}

Med Edge Delivery kan ni skapa snabba, engagerande webbplatser där författarna snabbt kan uppdatera och publicera innehåll och nya webbplatser snabbt kan lanseras.

Integrera AEM Assets med dokumentbaserad redigering för Edge Delivery Services för att göra det möjligt för webbplatsförfattare att använda bilder som finns i AEM Assets-arkiv när de skriver dokument i Microsoft Word eller Google Docs. Mer information finns i [Integrera AEM Assets med dokumentbaserad redigering](/help/edge/using.md#integrate-assets-edge).

## Integrering med Adobe Journey Optimizer {#integration-with-ajo}

[Adobe Journey Optimizer](https://business.adobe.com/products/journey-optimizer/adobe-journey-optimizer.html) förenklar kundens resehantering genom att tillhandahålla flerkanalskampanjer med smarta beslut och insikter. När du utformar meddelanden med Journey Optimizer kan du komma åt Assets as a Cloud Service-databasen direkt från Journey Optimizer-gränssnittet. Användare får åtkomst till resurser via det inbäddade användargränssnittet i Experience Manager Assets. Mer information finns i [Skapa och hantera resurser med Experience Manager Assets](https://experienceleague.adobe.com/docs/journey-optimizer/using/content-management/assets-images/assets.html?lang=sv-SE).

## Nya Assets-funktioner {#whats-new-assets}

De viktiga nya funktionerna är:

* [Asset-mikrotjänster](/help/assets/asset-microservices-overview.md)
* [Metoder för överföring av resurser](/help/assets/add-assets.md)

**Se även**

* [Översätt Assets](translate-assets.md)
* [ASSETS HTTP API](mac-api-assets.md)
* [Filformat som stöds av Assets](file-format-support.md)
* [Sök resurser](search-assets.md)
* [Anslutna resurser](use-assets-across-connected-assets-instances.md)
* [Resursrapporter](asset-reports.md)
* [Metadata-scheman](metadata-schemas.md)
* [Hämta resurser](download-assets-from-aem.md)
* [Hantera metadata](manage-metadata.md)
* [Sök efter ansikten](search-facets.md)
* [Hantera samlingar](manage-collections.md)
* [Import av massmetadata](metadata-import-export.md)
* [Publicera Assets till AEM och Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)

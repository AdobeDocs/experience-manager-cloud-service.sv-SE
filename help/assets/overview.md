---
title: Introduktion till Assets som [!DNL Cloud Service]
description: Nyheter i Assets som [!DNL Cloud Service].
contentOwner: AG
feature: Asset Management
role: User,Leader,Architect
exl-id: 4437f214-d058-4975-8b8f-869a12c8103b
source-git-commit: 5a7938d5e52388516f8b66bbcf8ffdee332a51a3
workflow-type: tm+mt
source-wordcount: '740'
ht-degree: 1%

---

# Introduktion av resurser som [!DNL Cloud Service] {#assets-cloud-service-introduction}

<!-- Need review information from gklebus -->

Adobe Experience Manager Assets som [!DNL Cloud Service] erbjuder en molnbaserad, PaaS-lösning som gör att företag inte bara kan utföra sin digitala resurshantering och Dynamic Media-åtgärder snabbt och effektivt, utan även använda nästa generations smarta funktioner, som AI/ML, inifrån ett system som alltid är aktuellt, alltid tillgängligt och alltid är inlärningsbart.

Samtidig förtäring av många resurser eller komplexa resurser är en resurskrävande uppgift för en författarinstans i Experience Manager. Den primära instansen förbrukar mycket processorkraft, minne och I/O-resurser när resurser läggs till, bearbetas eller till och med migreras. Sådana prestandaproblem påverkar redigering och surfning hos slutanvändarna.

Företag behöver stöd för en mängd olika filformat och innehållsupplösningar för användning på flera enheter, i olika geografiska områden och på flera språk. Resurshanterings- och lagringskrav kräver resurser och funktioner som kan överbelasta en traditionell lösning. Ibland ger inte tekniska begränsningar av behandlingen av tillgångar de resultat man önskar och i andra fall är kostnaden för lagring ett hinder för vinstmarginalerna.

Börja med att förstå [fördelarna med ett molnbaserat erbjudande](#solution-benefits). Se vad som står på notable [ändringar av Experience Manager som [!DNL Cloud Service]](/help/release-notes/aem-cloud-changes.md) som också påverkade Experience Manager Assets och som följde upp [ändringar i tillgångar](/help/assets/assets-cloud-changes.md).

Läs vidare för att lära dig mer om [information om de nya Assets-funktionerna](#whats-new-assets) och [kända problem](/help/release-notes/maintenance/latest.md). Se en lista med [borttagna eller inaktuella funktioner](/help/release-notes/deprecated-removed-features.md) om du vill veta vad som tas bort i den här versionen. Slutligen, förstå Experience Manager villkoren med hjälp av detta [ordlista](/help/overview/terminology.md).

## Lösningsfördelar {#solution-benefits}

Nedan beskrivs de viktigaste fördelarna med Assets som [!DNL Cloud Service]. Mer information finns på [översikt över Experience Manager som [!DNL Cloud Service]](/help/overview/introduction.md).

* **Moderna molntjänster för bearbetning av resurser**: De nya mikrotjänsterna är en molnbaserad, skalbar, tillförlitlig och problemfri tjänst för bearbetning av resurser.
* **Mycket skalbar**: Elastisk skalbarhet för alla typer av driftsättningar. Praktiskt taget obegränsade resurser som finns tillgängliga on-demand, vid behov. Sparar kostnaden för överdesign jämfört med ett traditionellt system.
* **Senaste programvara**: Alltid aktuell och alltid uppdaterad. Alla användare har bara den senaste programvaran med alla korrigeringar, funktioner, säkerhet och felkorrigeringar tillgängliga. Utvecklare och integratörer arbetar med den senaste uppsättningen API:er utan problem med stöd för flera versioner.
* **Alltid online**: Noll driftavbrott (0dt) tack vare instansen som distribuerats i ett kluster med säkerhetskopior och redundans. Uppgraderingar är också 0dt.
* **Konstantövervakning**: Övervakningen av systemet är automatiserade och inbyggda kontroller och utlösare som hjälper till att upprätthålla prestanda, tillgänglighet och övergripande tillförlitlighet.
* **Smidig driftsättning**: Experience Manager i molnfunktionerna är helt automatiserade och kräver ingen manuell åtgärd. För automatiserad driftsättning automatiserar komponenten Cloud Manager (CM) byggandet av driftsättningsbara Docker-bilder som innehåller din anpassade kod.

## Tillgängliga personbaserade upplevelser {#persona-based-experiences}

Adobe erbjuder robusta DAM-lösningar (Digital Asset Management) så att ni får ut mesta möjliga av era digitala resurser. Adobe Experience Manager Assets har två separata upplevelser som använder samma Cloud Services:

* **Administratörsvy**: Det befintliga as a Cloud Service användargränssnittet för Assets. Använd administrationsvyn för alla avancerade funktioner för resurshantering, inklusive integreringar, arbetsflöden, innehållsautomatisering, publicering med mera.

* **Resursvy**: Adobe lätthanterlig resurshantering för att lagra, hantera, identifiera och använda digitala resurser. Effektivt användargränssnitt med funktioner för resurshantering. Utformad för enklare DAM-användare med fokus på överföring, metadatahantering, sökning, hämtning och delning.

Användare som har åtkomst till administrationsvyn kan även komma åt resursvyn. Resursvyn har ett förenklat användargränssnitt som gör det enkelt att hantera, identifiera och distribuera digitala resurser. Ett stort antal användare från olika funktioner, inklusive kreatörer, marknadsförare och branschgrupper, kan samarbeta om resurser och få tillgång till rätt, godkänt material när och var de behöver det. Många tillfälliga DAM-användare föredrar resursvyn eftersom den bara innehåller en delmängd av funktioner. Upplevelsen riktar sig till kreatörer, skrivskyddade mediekonsumenter och användare med mindre vikt-DAM.

DAM-bibliotek, utvecklare och superanvändare kan fortsätta att använda administrationsvyn eller växla mellan användargränssnitten efter behov. Du kan välja den upplevelse som fungerar bäst för din roll.

![add-tags](assets/newui-overview.svg)

Mer information om hur du kommer åt resursvyn och vissa av de förenklingar som den erbjuder via administratörsvyn finns i [Introduktion till resursvyn](/help/assets/assets-view-introduction.md).

## Nya Assets-funktioner {#whats-new-assets}

De viktiga nya funktionerna är:

* [Asset-mikrotjänster](/help/assets/asset-microservices-overview.md)
* [Metoder för överföring av resurser](/help/assets/add-assets.md)

**Se även**

* [Översätt resurser](translate-assets.md)
* [HTTP API för Assets](mac-api-assets.md)
* [Resurser som stöds i filformat](file-format-support.md)
* [Söka efter resurser](search-assets.md)
* [Anslutna resurser](use-assets-across-connected-assets-instances.md)
* [Materialrapporter](asset-reports.md)
* [Metadata-scheman](metadata-schemas.md)
* [Hämta resurser](download-assets-from-aem.md)
* [Hantera metadata](manage-metadata.md)
* [Söka efter fasetter](search-facets.md)
* [Hantera samlingar](manage-collections.md)
* [Import av massmetadata](metadata-import-export.md)

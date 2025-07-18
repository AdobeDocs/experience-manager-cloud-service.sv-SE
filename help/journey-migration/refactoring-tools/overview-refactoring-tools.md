---
title: Omfaktoriseringsverktyg - översikt
description: Kom igång med AEM Refactoring Tools
exl-id: b8137e01-87e8-4298-b0cc-b376330cb730
source-git-commit: 879f4f3476ee369554188d6e3b7973d32454ed4b
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 0%

---

<!-- Alexandru: temporarily commeting this out, since it breaks validation

>[!CONTEXTUALHELP]
>id="aemcloud_rs_overview"
>title="Overview"
>abstract="Refactoring Tools is a solution developed by Adobe to help refactor existing AEM projects for compatibility with AEM as a Cloud Service. The tools are executed via Cloud Acceleration Manager (CAM) and automate key modernization tasks."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html?lang=sv-SE" text="Guidelines and Best Practices"

-->

# Omfaktoriseringsverktyg - översikt {#refactoring-tools-overview}

**Omfaktoriseringsverktygen** effektiviserar processen att uppdatera befintliga AEM-projekt så att de blir kompatibla med **AEM as a Cloud Service (AEMaaCS)**. De här verktygen automatiserar vanliga omfaktoriserings- och moderniseringsuppgifter och är integrerade med **Cloud Acceleration Manager** för en smidig upplevelse.

Omfaktoriseringsverktygen fanns tidigare bara som CLI-verktyg och har nu ett enhetligt gränssnitt med funktioner som automatiserad inspektion, konfigurationsgenerering och jobbkörning, vilket minskar de manuella kostnaderna och förbättrar synligheten.

## Inspektionsarbetsflöde {#inspection-workflow}

**Inspektionsarbetsflödet** förenklar förberedelseprocessen för att köra omfaktoriseringsverktyg.

### Viktiga funktioner:

* **Automatisk utlösare** - Om du överför ett projekt startas undersökningen automatiskt.
* **Konfigurationsgenerering** - Verktygen undersöker den överförda källkoden och genererar de nödvändiga konfigurationerna.
* **Belastningsöverföring** - Dessa konfigurationer skickas direkt till de valda verktygen för körning.

## Tillgängliga omfaktoriseringsverktyg

### Databasmodernisering {#repo-modernizer}

**Databasmodernisering** omstrukturerar ditt AEM-projekts databaslayout och innehåll så att det överensstämmer med AEMaaCS-standarder och bästa praxis. Det ersätter det gamla uppdateringsverktyget för databaser med förbättrad automatisering och exakthet.

### Kodtransformator {#code-transformer}

**Kodtransformatorn** använder intelligent mönsterigenkänning och AI-driven analys för att identifiera och uppdatera kodsegment som är inkompatibla med AEMaaCS. Det här verktyget förenklar migreringen och minskar antalet manuella kodändringar.

## Fas i arbetsflöde för omfaktorisering {#phases-in-refactoring-tools}

Omfaktoriseringsverktygen följer en strukturerad tvåstegsprocess:

### Fas 1: Överför din Source-kod

* Ladda upp källkoden (i ZIP-format) med CAM-gränssnittet.
* När projektet har överförts aktiveras **inspektionsarbetsflödet** automatiskt för att analysera projektet och förbereda det för verktygskörning.

>[!NOTE]
>Under inspektionen är det inte tillåtet att överföra ett annat projekt.

### Fas 2: Utlösa ett omfaktoriseringsjobb

Efter en lyckad undersökning kan du köra ett eller flera omfaktoriseringsverktyg:

* **Kör databasmodernisering** - Kör databasmodernisering.
* **Kör kodtransformator** - Kör kodtransformering baserat på undersökningsutdata.
* **Kör alla verktyg tillsammans** - Kör alla tillgängliga verktyg i en enda åtgärd.

>[!NOTE]
>Omfaktoriseringsjobb kan bara startas efter att källkoden har överförts och inspekterats.

>[!NOTE]
>Användare kan utlösa flera omfaktoriseringsjobb parallellt, men varje jobb utförs separat.

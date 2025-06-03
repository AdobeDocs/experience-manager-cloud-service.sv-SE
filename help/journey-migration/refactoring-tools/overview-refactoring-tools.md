---
title: Komma igång med omfaktoriseringsverktyg
description: Kom igång med AEM Refactoring Tools
exl-id: c0cecf65-f419-484b-9d55-3cbd561e8dcd
source-git-commit: fa65b489d54d5333811145a1875a8f6fc89317bc
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 0%

---


>[!CONTEXTUALHELP]
>id="aemcloud_rs_overview"
>title="Ökning"
>abstract="Refactoring Tools är en lösning som utvecklats av Adobe för att hjälpa till att omfaktorisera befintliga AEM-projekt för kompatibilitet med AEM as a Cloud Service. Verktygen körs via Cloud Acceleration Manager (CAM) och automatiserar viktiga moderniseringsuppgifter."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html?lang=sv-SE" text="Riktlinjer och bästa praxis"

# Komma igång med omfaktoriseringsverktyg {#getting-started-refactoring-tools}

**Omfaktoriseringsverktygen** effektiviserar processen att uppdatera befintliga AEM-projekt så att de blir kompatibla med **AEM as a Cloud Service (AEMaaCS)**. De här verktygen automatiserar vanliga omfaktoriserings- och moderniseringsuppgifter och är integrerade med **Cloud Acceleration Manager** för en smidig upplevelse.

Omfaktoriseringsverktygen fanns tidigare bara som CLI-verktyg och har nu ett enhetligt gränssnitt med funktioner som automatiserad inspektion, konfigurationsgenerering och jobbkörning, vilket minskar de manuella kostnaderna och förbättrar synligheten.

&#x200B;---

## Inspektionsarbetsflöde {#inspection-workflow}

**Inspektionsarbetsflödet** förenklar förberedelseprocessen för att köra omfaktoriseringsverktyg.

### Viktiga funktioner:

* **Automatisk utlösare** - Om du överför ett projekt startas undersökningen automatiskt.
* **Konfigurationsgenerering** - Verktygen undersöker den överförda källkoden och genererar de nödvändiga konfigurationerna.
* **Belastningsöverföring** - Dessa konfigurationer skickas direkt till de valda verktygen för körning.

&#x200B;---

## Tillgängliga omfaktoriseringsverktyg

### Databasmodernisering {#repo-modernizer}

**Databasmodernisering** omstrukturerar ditt AEM-projekts databaslayout och innehåll så att det överensstämmer med AEMaaCS-standarder och bästa praxis. Det ersätter det gamla uppdateringsverktyget för databaser med förbättrad automatisering och exakthet.

### Kodtransformator {#code-transformer}

**Kodtransformatorn** använder intelligent mönsterigenkänning och AI-driven analys för att identifiera och uppdatera kodsegment som är inkompatibla med AEMaaCS. Det här verktyget förenklar migreringen och minskar antalet manuella kodändringar.

&#x200B;---

## Fas i arbetsflöde för omfaktorisering {#phases-in-refactoring-tools}

Omfaktoriseringsverktygen följer en strukturerad tvåstegsprocess:

### Fas 1: Överför din Source-kod

* Ladda upp källkoden (i ZIP-format) med CAM-gränssnittet.
* När projektet har överförts aktiveras **inspektionsarbetsflödet** automatiskt för att analysera projektet och förbereda det för verktygskörning.

>[!NOTE]
>Under inspektionen är det inte tillåtet att överföra ett annat projekt.

&#x200B;---

### Fas 2: Utlösa ett omfaktoriseringsjobb

Efter en lyckad undersökning kan du köra ett eller flera omfaktoriseringsverktyg:

* **Kör databasmodernisering** - Kör databasmodernisering.
* **Kör kodtransformator** - Kör kodtransformering baserat på undersökningsutdata.
* **Kör alla verktyg tillsammans** - Kör alla tillgängliga verktyg i en enda åtgärd.

>[!NOTE]
>Omfaktoriseringsjobb kan bara startas efter att källkoden har överförts och inspekterats.

>[!NOTE]
>Användare kan utlösa flera omfaktoriseringsjobb parallellt, men varje jobb utförs separat.

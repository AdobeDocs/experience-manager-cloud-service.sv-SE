---
title: Versionsinformation om 2020.9.0-utgåvan av [!DNL Adobe Experience Manager] as a Cloud Service.
description: '"[!DNL Adobe Experience Manager] as a Cloud Service Release Notes for 2020.9.0."'
exl-id: 2332512f-8c52-4569-a006-faa36a7670a1
source-git-commit: bc4da79735ffa99f8c66240bfbfd7fcd69d8bc13
workflow-type: tm+mt
source-wordcount: '722'
ht-degree: 1%

---

# Versionsinformation för [!DNL Adobe Experience Manager] as a Cloud Service 2020.9.0 {#release-notes}

I följande avsnitt beskrivs den allmänna versionsinformationen för [!DNL Experience Manager] as a Cloud Service 2020.9.0.

## Releasedatum {#release-date}

Releasedatum för [!DNL Adobe Experience Manager] as a Cloud Service 2020.9.0 är 24 september 2020.

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

### Nyheter i [!DNL Sites] {#what-is-new-sites}

* Redigeraren för Single Page Application (SPA) JavaScript SDK [är nu öppen källkod.](/help/implementing/developing/hybrid/reference-materials.md)

## [!DNL Adobe Experience Manager Assets] as a Cloud Service {#assets}

### Nyheter i [!DNL Assets] {#what-is-new-assets}

* Vattenstämplingsbildfiler stöds för återgivningar som genereras med objektmikrotjänster. Den kan konfigureras som en bearbetningsprofil och använder en PNG-fil som vattenstämpel. Se [vattenstämpla dina resurser](/help/assets/watermark-assets.md).

* Förbättringar i [!DNL Dynamic Media]

   * Selektiv publicering - nu kan ett marknadsföringsteam få tillgång till [!DNL Dynamic Media] smarta beskärningsbilder och dynamiska återgivningar som synkroniseras med [!DNL Dynamic Media] så att de kan skapa marknadsföringsmaterial, utan att behöva publicera materialet på [!DNL Dynamic Media] för global leverans. [!DNL Experience Manager] och [!DNL Dynamic Media] publiceringen är fristående och kan ske separat för att uppnå detta. Se [selektiv publicering](/help/assets/dynamic-media/selective-publishing.md).
   * Administratörer kan nu återställa [!DNL Dynamic Media] Cloud Servicens lösenord som tas emot vid etablering. Återställningen kan göras i [!DNL Experience Manager] utan att behöva använda [!DNL Dynamic Media Classic] datorprogram.

* Mer information om följande förbättringar finns i [nyheter i Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/whats-new.html).

   * Förbättrad förhandsgranskning av PDF med integrering av Adobe Document Cloud View SDK.
   * Ladda ned med ett klick.
   * Nya administrationskonfigurationer för nedladdningen.

<!--
### Bugs Fixed {#bugs-fixed-assets}

TBD: list of Assets aaCS bugs that are fixed.
-->

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Vad är nytt? {#what-is-new-commerce}

* Frisläppta CIF-kärnkomponenter v1.3.0. Se [CIF-kärnkomponenter](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.3.0) för mer information.

* Nu finns funktioner för förhandsgranskning med produkt-/kategorimallar för produkt- och kategorimallar. På så sätt kan företagsanvändare/marknadsförare i AEM visa produkt-/kategorimallarna med riktiga data.

* Sidan Egenskaper har lagts till i produkter och kategorier så att företagsanvändare kan visa information som är kopplad till produkt-SKU/kategori-ID.

* Sorteringsfunktionen har lagts till i produktkonsolen för att tillåta sortering av produkter/kategorier efter namn eller prisattribut.

* Funktioner för produktsökning har lagts till i produktkonsolen.

### Felkorrigeringar {#bug-fixes-commerce}

* Commerce Cloud-konfigurationer respekterar inte arv. Detta har åtgärdats för att säkerställa att konfigurationen ärver värden.

## Cloud Manager {#cloud-manager}

### Releasedatum {#release-date-cm}

Releasedatum för [!UICONTROL Cloud Manager] Version 2020.9.0 är 3 september 2020.

### Nyheter {#what-is-new-cloud-manager}

* Innehållsgranskning har omdöpts till Experience Audit.
* Byggprocessen har delats upp i tre separata Maven-kommandon.
* Om Git-databasen inte kan klonas görs ett nytt försök upp till tre gånger.

### Felkorrigeringar {#bug-fixes-cm}

* Fliken Innehållsgranskning visade felaktigt bas-URL:en med författardomänen i stället för publiceringsdomänen.

## Cloud Readiness Analyzer {#cloud-readiness-analyzer}

Följ det här avsnittet för att lära dig mer om nyheter och uppdateringar för Cloud Readiness Analyzer version 1.1.0.

### Vad är nytt? {#what-is-new-cra}

* Cloud Readiness Analyzer (CRA) har en startstatuskonsol som visar en explicit **Generera rapport** för användaren att klicka för att köra CRA.

* CRA-gränssnittet visar förloppet medan det körs. Här visas objekt som analyseras och upptäckter som hittas under körningen.

* CRA-rapporten innehåller en sammanfattning och antalet fynd i tabellformat, ordnade efter typ av fynd och prioritetsnivå. Om du klickar på numret på sökningen rullas resultatet automatiskt till den plats där sökningen finns i rapporten.

### Felkorrigeringar {#cra-bug-fixes}

* I vissa fall uppdaterades inte CRA-rapporten efter en uppdatering. Detta har åtgärdats i den här versionen.

## Content Transfer Tool {#content-transfer-tool}

Följ det här avsnittet för att lära dig mer om nyheter och uppdateringar för Content Transfer Tool Release v1.1.10.

### Vad är nytt? {#what-is-new-ctt}

* Innehållsöverföringsverktyget (CTT) stöder Azure Blob Store-datalagret.

* CTT-användargränssnittet har en funktion för automatisk inläsning som laddar om översiktssidan var 30:e sekund.

* Knapp tillagd i CTT-användargränssnittet för hämtning *Åtkomsttoken* enkelt.

* Beskrivande valideringsmeddelande har lagts till för *URL* och *Migreringsuppsättningsnamn*.

## Verktyg för omstrukturering av kod {#code-refactoring}

Följ det här avsnittet för att lära dig mer om nyheter och uppdateringar för verktygen för kodkorrigering.

### Vad är nytt? {#what-is-new-refactoring}

* AIO-CLI-plugin-programmet har stöd för Repository Modernizer och gör att användare kan köra verktyget med plugin-programmet.

   Se [Git-resurs: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration) för mer information.

* Verktyget Databasmodernisering kan användas för att strukturera om befintliga projektpaket till paket som är kompatibla med den projektstruktur som har definierats för AEM as a Cloud Service.

   Se [Git-resurs: Databasmodernisering](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) för mer information.

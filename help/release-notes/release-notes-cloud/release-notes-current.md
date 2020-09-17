---
title: Versionsinformation för 2020.9.0-utgåvan [!DNL Adobe Experience Manager] av en Cloud Service.
description: '[!DNL Adobe Experience Manager] som Cloud Service versionsinformation för 2020.9.0.'
translation-type: tm+mt
source-git-commit: 9bb087cb0570a1f3bbffb989a9399d3274f9c5e1
workflow-type: tm+mt
source-wordcount: '389'
ht-degree: 1%

---


# Versionsinformation för [!DNL Adobe Experience Manager] som Cloud Service 2020.9.0 {#release-notes}

I följande avsnitt beskrivs den allmänna versionsinformationen för Experience Manager som Cloud Service 2020.7.0.

## [!DNL Adobe Experience Manager Sites] som en Cloud Service {#sites}

### What is new in [!DNL Sites] {#what-is-new-sites}

* SPA-redigeraren (Single Page Application) JavaScript SDK [är nu öppen källkod.](/help/implementing/developing/spa/reference-materials.md)

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### What&#39;s New {#what-is-new-commerce}

* Frisläppta CIF-kärnkomponenter v1.3.0. Mer information finns i [CIF Core Components](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.3.0) .

* Nu finns funktioner för förhandsgranskning med produkt-/kategorimallar för produkt- och kategorimallar. På så sätt kan företagsanvändare/marknadsförare i AEM visa produkt-/kategorimallarna med riktiga data.

* Sidan Egenskaper har lagts till i produkter och kategorier så att företagsanvändare kan visa information som är kopplad till produktens SKU/kategori-ID.

* Sorteringsfunktionen har lagts till i produktkonsolen för att tillåta sortering av produkter/kategorier efter namn eller prisattribut.

* Funktioner för produktsökning har lagts till i produktkonsolen.

### Bug Fixes {#bug-fixes-commerce}

* Commerce Cloud-konfigurationer respekterar inte arv. Detta har åtgärdats för att säkerställa att konfigurationen ärver värden.

## Cloud Manager {#cloud-manager}

### Releasedatum {#release-date-cm}

Releasedatum för [!UICONTROL Cloud Manager] version 2020.9.0 är 3 september 2020.

### What&#39;s New {#what-is-new-cloud-manager}

* Innehållsgranskning har omdöpts till Experience Audit.
* Byggprocessen har delats upp i tre separata Maven-kommandon.
* Om Git-databasen inte kan klonas görs ett nytt försök upp till tre gånger.

### Bug Fixes {#bug-fixes-cm}

* Fliken Innehållsgranskning visade felaktigt bas-URL:en med författardomänen i stället för publiceringsdomänen.

## Cloud Readiness Analyzer {#cloud-readiness-analyzer}

Följ det här avsnittet för att lära dig mer om nyheter och uppdateringar för Cloud Readiness Analyzer version 1.1.0.

### What&#39;s New {#what-is-new-cra}

* Cloud Readiness Analyzer (CRA) har en startstatuskonsol som visar en explicit **Generate Report** -knapp som användaren kan klicka på för att köra CRA.

* CRA-gränssnittet visar förloppet medan det körs. Här visas objekt som analyseras och upptäckter som hittas under körningen.

* CRA-rapporten innehåller en sammanfattning och antalet fynd i tabellformat ordnade efter typ av fynd och prioritetsnivå. Om du klickar på numret på sökningen rullas resultatet automatiskt till den plats där sökningen finns i rapporten.

### Bug Fixes {#cra-bug-fixes}

* I vissa fall uppdaterades inte CRA-rapporten efter en uppdatering. Detta har åtgärdats i den här versionen.


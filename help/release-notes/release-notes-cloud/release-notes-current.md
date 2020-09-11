---
title: Versionsinformation för 2020.9.0-utgåvan [!DNL Adobe Experience Manager] av en Cloud Service.
description: '[!DNL Adobe Experience Manager] som Cloud Service versionsinformation för 2020.9.0.'
translation-type: tm+mt
source-git-commit: cca8aff3ada327252bfabd2207e7aa86fdf00033
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---


# Versionsinformation för [!DNL Adobe Experience Manager] som Cloud Service 2020.9.0 {#release-notes}

I följande avsnitt beskrivs den allmänna versionsinformationen för Experience Manager som Cloud Service 2020.9.0.

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

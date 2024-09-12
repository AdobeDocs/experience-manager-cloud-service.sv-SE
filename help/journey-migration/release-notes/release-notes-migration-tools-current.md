---
title: Versionsinformation för migreringsverktyg i AEM as a Cloud Service version 2024.09
description: Versionsinformation om migreringsverktyg i AEM as a Cloud Service version 2024.09.0
feature: Release Information
exl-id: 52709511-eab2-47a7-8bea-1b707cd568a1
role: Admin
source-git-commit: 0c16f264826a46907afc33c91a021e7696f5b7a8
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 3%

---

# Versionsinformation om migreringsverktyg i AEM as a Cloud Service version 2024.09.0 {#release-notes}

Den här sidan innehåller versionsinformation för migreringsverktyg i AEM as a Cloud Service 2024.09.0.

## Verktyget Innehållsöverföring {#ctt-release}

### Releasedatum {#release-date-ctt}

Releasedatum för Content Transfer Tool v3.0.20 är 28 augusti 2024.

### Nyheter {#what-is-new-ctt}

* Användare kommer inte längre att vara intresserade av den här versionen och därför har den valfria funktionen för användarmappning tagits bort.
* En OSGI-konfigurationsalternativ har lagts till för att inaktivera eller aktivera migrering av principer vid extrahering och förtäring (standardinställningen är att aktivera den)

### Felkorrigeringar {#bug-fixes-ctt}

* CTT har förbättrats för att förhindra ett fel när en hemlig nyckel i azcopy-konfigurationen tas bort
* CTT hanterar nu felen på ett smidigt sätt när AzCopy-loggar kopieras i valideringsfasen
* Ändra loggkatalogen för azcopy som skapades under extraheringsprocessen

## Best Practices Analyzer {#bpa-release}

### Releasedatum {#release-date-bpa}

Releasedatum för Best Practices Analyzer v2.1.52 är 4 september 2024

### Nyheter {#what-is-new-bpa}

* Ett nytt mönster introducerades för att identifiera JCR-baserad händelse i AEM

### Felkorrigeringar {#bug-fixes-bpa}

* Felaktiga positiva korrigeringar
* Förbättrad tillförlitlighet för hantering av omdirigerade svar från dispatchern
* Korrigerad utebliven rapportering av NCC-sökning för alla språk under /apps/wcm/core/resources/languages/
* lade till en kontroll för att upptäcka om en nods multiegenskap saknar värden


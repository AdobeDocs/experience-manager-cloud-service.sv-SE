---
title: Versionsinformation för migreringsverktyg i AEM as a Cloud Service version 2023.07.0
description: Versionsinformation för migreringsverktyg i AEM as a Cloud Service version 2022.07.0
feature: Release Information
exl-id: 2f787321-f156-480d-bbe8-1a6d04f110c5
source-git-commit: 1f01408223a661c0149d959b1901293dc91ed7ee
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 1%

---

# Versionsinformation för migreringsverktyg i AEM as a Cloud Service version 2023.07.0 {#release-notes}

Den här sidan innehåller versionsinformation för migreringsverktyg i AEM as a Cloud Service 2022.07.0.

## Best Practices Analyzer {#bpa-release}

### Releasedatum {#release-date-bpa}

Releasedatum för Best Practices Analyzer v2.1.42 är 6 juli 2023.

### Nyheter {#what-is-new-bpa}

* I den här versionen av Best Practices Analyzer har flera metodmönster lagts till. Bland dessa finns:
   * Identifiera konfiguration av minsta underhållsaktivitet
   * Identifiera långvariga/tunga frågor
   * Identifiera ett stort antal författararbetsflöden i körnings- eller inkörningstillstånd
   * Identifierar konfigurationen för SLing-jobb för OSGI Apache
   * Identifiera anpassade Guava-caches

### Felkorrigeringar {#bug-fixes-bpa}

* BPA har förbättrats för att förhindra fel vid generering av minnesrapporter för rapporter med ett stort antal resultat.
* BPA har förbättrats för att upptäcka escape-tecken i sökvägar för att förhindra misslyckade innehållsöverföringar när innehåll migreras till AEM as a Cloud Service.

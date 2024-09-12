---
title: Versionsinformation om migreringsverktyg i AEM as a Cloud Service version 2024.05.0
description: Versionsinformation om migreringsverktyg i AEM as a Cloud Service version 2024.05.0
feature: Release Information
role: Admin
exl-id: f50a74fa-ad7d-4837-b0a1-9945c32af02f
source-git-commit: 3b2ed44b438fe8587a9b9603ddfacc41111fb903
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 2%

---

# Versionsinformation om migreringsverktyg i AEM as a Cloud Service version 2024.05.0 {#release-notes}

På den här sidan finns versionsinformation för migreringsverktyg i AEM as a Cloud Service 2024.05.0.

## Best Practices Analyzer {#bpa-release}

### Releasedatum {#release-date-bpa}

Releasedatum för Best Practices Analyzer v2.1.50 är maj 2024.

### Nyheter {#what-is-new-bpa}

* Best Practices Analyzer (BPA) stöder nu automatisk överföring av BPA-genererade rapporter direkt till Cloud Acceleration Manager (CAM). Användarna behöver inte längre hämta rapporten manuellt och överföra den till CAM. Mer information finns i [Använda analysverktyg för bästa praxis](/help/journey-migration/best-practices-analyzer/using-best-practices-analyzer.md)

### Felkorrigeringar {#bug-fixes-bpa}

* Best Practices Analyzer identifierar nu alla noder som är större än 16 MB
* Race-tillstånd som orsakar sporadiska förekomster av NCC-fynd har åtgärdats.

## Cloud Acceleration Manager {#cam-release}

### Nyheter {#what-is-new-cam}

* Cloud Acceleration Manager (CAM) har nu stöd för automatisk överföring av BPA-genererade rapporter direkt till CAM. Mer information finns i [Readiness Phase i Cloud Acceleration Manager - Using Best Practices Analysis Card](/help/journey-migration/cloud-acceleration-manager/using-cam/cam-readiness-phase.md#best-practices-analysis)

* Cloud Acceleration Manager ger nu en uppskattning av hur lång tid ett intag kan ta, med hänsyn till faktorer som nodantal, datalagringsstorlek osv. Läs mer med [Inkluderar innehåll i Cloud Servicen](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md)

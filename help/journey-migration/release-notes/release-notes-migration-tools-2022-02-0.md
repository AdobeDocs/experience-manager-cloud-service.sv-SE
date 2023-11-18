---
title: Versionsinformation för migreringsverktyg i AEM as a Cloud Service version 2022.2.0
description: Versionsinformation för migreringsverktyg i AEM as a Cloud Service version 2022.2.0
feature: Release Information
exl-id: b1cd871d-c71e-4902-a97e-2c859f6a4da4
source-git-commit: 6bb7b2d056d501d83cf227adb239f7f40f87d0ce
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 2%

---

# Versionsinformation för migreringsverktyg i AEM as a Cloud Service version 2022.2.0 {#release-notes}

Den här sidan innehåller versionsinformation för migreringsverktyg i AEM as a Cloud Service 202.2.0.

## Best Practices Analyzer {#bpa-release}

### Releasedatum {#release-date-bpa}

Releasedatum för Best Practices Analyzer v2.1.24 är 1 februari 2022.

### Nyheter {#what-is-new-bpa}

* Möjlighet att identifiera och rapportera antalet resurser med och utan smarta taggar.
* Möjlighet att identifiera och rapportera vilken version av Core Component som används.
* Möjlighet att identifiera och rapportera om typen av källnivå (författare eller publicering) där BPA utfördes.

### Felkorrigeringar {#bug-fixes-bpa}

* Logiken för BPA-storleksändring gjordes snabbare och effektivare.
* I vissa scenarier ökade inte BPA antalet analyserade när det kördes. Den här har åtgärdats.

## Content Transfer Tool {#ctt-release}

### Releasedatum {#release-date-ctt}

Releasedatum för Content Transfer Tool v1.8.6 är 3 februari 2022.

### Nyheter {#what-is-new-ctt}

* Innehållsvalidering - Användarna kan på ett tillförlitligt sätt avgöra om allt innehåll som extraherats av verktyget Innehållsöverföring har importerats till målinstansen. Om du vill använda den här funktionen aktiverar du den i `System Console` i AEM. Se [Verifierar innehållsöverföringar - Komma igång](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/validating-content-transfers.html?lang=en#getting-started) för mer information.

### Felkorrigeringar {#bug-fixes-ctt}

* Vissa användare mappades inte eftersom användarmappningen var skiftlägeskänslig. Den här har åtgärdats. Användarmappning är inte längre skiftlägeskänslig.

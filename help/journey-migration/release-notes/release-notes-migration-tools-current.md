---
title: Versionsinformation för migreringsverktyg i AEM as a Cloud Service version 2023.03.0
description: Versionsinformation för migreringsverktyg i AEM as a Cloud Service version 2022.03.0
feature: Release Information
exl-id: 2f787321-f156-480d-bbe8-1a6d04f110c5
source-git-commit: 5815dacd2806cc7886aa0c7c5c9fd329306b3e1b
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 1%

---

# Versionsinformation för migreringsverktyg i AEM as a Cloud Service version 2023.03.0 {#release-notes}

Den här sidan innehåller versionsinformation för migreringsverktyg i AEM as a Cloud Service 2022.03.0.

## Best Practices Analyzer {#bpa-release}

### Releasedatum {#release-date-bpa}

Releasedatum för Best Practices Analyzer v2.1.40 är 3 mars 2023.

### Nyheter {#what-is-new-bpa}

* BPA kan nu identifiera och rapportera om noder som är i konflikt - noder med samma `jcr:uuid`. Sådana upptäckter flaggas som kritiska eftersom det kan leda till innehållsproblem när innehåll flyttas till AEM as a Cloud Service.
* BPA kan nu identifiera och rapportera om användningen av händelseavlyssnare. Vi rekommenderar att du justerar den här typen av händelsehanteringsmekanism till snedningsjobb när du går till AEM as a Cloud Service.

### Felkorrigeringar {#bug-fixes-bpa}

* BPA rapporterade falsk positiv information om `grouprendercondition`. Den här har åtgärdats.
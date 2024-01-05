---
title: Versionsinformation för migreringsverktyg i AEM as a Cloud Service version 2023.03.0
description: Versionsinformation för migreringsverktyg i AEM as a Cloud Service version 2023.03.0
feature: Release Information
exl-id: cdc57cca-e10a-4b0d-b803-910ccc9350a6
source-git-commit: ecf4c06fd290d250c14386b3135250633b26c910
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 1%

---

# Versionsinformation för migreringsverktyg i AEM as a Cloud Service version 2023.03.0 {#release-notes}

Den här sidan innehåller versionsinformation för migreringsverktyg i AEM as a Cloud Service 2023.03.0.

## Best Practices Analyzer {#bpa-release}

### Releasedatum {#release-date-bpa}

Releasedatum för Best Practices Analyzer v2.1.40 är 3 mars 2023.

### Nyheter {#what-is-new-bpa}

* BPA kan nu identifiera och rapportera om noder som är i konflikt - noder med samma `jcr:uuid`. Sådana upptäckter flaggas som kritiska eftersom det kan leda till innehållsproblem när innehåll flyttas till AEM as a Cloud Service.
* BPA kan nu identifiera och rapportera om användningen av händelseavlyssnare. Vi rekommenderar att du justerar den här typen av händelsehanteringsmekanism till snedningsjobb när du går till AEM as a Cloud Service.

### Felkorrigeringar {#bug-fixes-bpa}

* BPA rapporterade falsk positiv information om `grouprendercondition`. Den här har åtgärdats.

## Verktyget Innehållsöverföring {#ctt-release}

### Releasedatum {#release-date-ctt}

Releasedatum för Content Transfer Tool v 2.0.16 är 8 mars 2023.

### Nyheter {#what-is-new-ctt}

* Användarmappningen har effektiviserats och integrerats i innehållsextraheringssteget. Ingen konfiguration behövs, och som standard görs användarmappningen automatiskt när användaren startar innehållsextraheringen. Användaren har möjlighet att inaktivera användarmappning vid behov. Läs mer [här.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/user-mapping-and-migration.html#user-mapping-detail)
* Förkopieringssteget med [AzCopy](https://learn.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) har integrerats med verktyget Innehållsöverföring för att avsevärt snabba upp extraheringen. Precopy konfigureras och installeras automatiskt när den här versionen av CTT installeras. När extraheringen initieras körs som standard precopy automatiskt för migreringsuppsättningar som är större än 200 GB. Användaren har möjlighet att inaktivera det vid behov. Läs mer [här.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/handling-large-content-repositories.html)
* CTT kan nu användas på Windows-servrar.

### Felkorrigeringar {#bug-fixes-ctt}

* Flera felkorrigeringar som förbättrar innehållsextraheringens flexibilitet.

---
title: Versionsinformation om migreringsverktyg i AEM as a Cloud Service version 2022.9.0
description: Versionsinformation om migreringsverktyg i AEM as a Cloud Service version 2022.9.0
feature: Release Information
exl-id: 581370ba-e3e8-487e-af83-a1eacbda2763
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 1%

---

# Versionsinformation om migreringsverktyg i AEM as a Cloud Service version 2022.9.0 {#release-notes}

Den här sidan innehåller versionsinformation för migreringsverktyg i AEM as a Cloud Service 2022.9.0.

## Best Practices Analyzer {#bpa-release}

### Releasedatum {#release-date-bpa}

Releasedatum för Best Practices Analyzer v2.1.34 är 12 september 2022.

### Nyheter {#what-is-new-bpa}

* BPA kan nu identifiera och rapportera om kunden har lagt till en anpassad loggningskonfiguration. AEM as a Cloud Service stöder inte anpassade loggfiler. Alla loggfiler måste skickas till `error.log`
* BPA kan nu rapportera de olika binära MIME-typerna som finns i kundens databas och antalet som är kopplade till dem.

### Felkorrigeringar {#bug-fixes-bpa}

* BPA-gränssnittet hade återgivningsproblem när ett stort antal resultat visades under ett enda mönster. Den här har åtgärdats.
* BPA rapporterade felaktigt vissa upptäckter som icke-kompatibla ändringar med kritisk allvarlighetsgrad. Den här har åtgärdats.

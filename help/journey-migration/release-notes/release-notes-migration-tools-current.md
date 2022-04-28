---
title: Versionsinformation för migreringsverktyg i AEM as a Cloud Service version 2022.4.0
description: Versionsinformation för migreringsverktyg i AEM as a Cloud Service version 2022.4.0
feature: Release Information
source-git-commit: 87e3291b4a72c24fc6cf8df488df305f1a078ea5
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---

# Versionsinformation för migreringsverktyg i AEM as a Cloud Service version 2022.4.0 {#release-notes}

Den här sidan innehåller versionsinformation för migreringsverktyg i AEM as a Cloud Service 2022.4.0.

## Best Practices Analyzer {#bpa-release}

### Releasedatum {#release-date-bpa}

Releasedatum för Best Practices Analyzer v2.1.28 är 22 april 2022.

### Nyheter {#what-is-new-bpa}

* Möjlighet att upptäcka och rapportera om användning av tillgångshanterarens API:er som inte stöds. Det finns fyra API:er som inte längre stöds i AEM as a Cloud Service. Kunderna bör se till att de inte längre använder dessa API:er och bör använda den nya metoden för överföring av resurser.

* Möjlighet att upptäcka användning av mallar för innehållsfragment. Mallar för innehållsfragment stöds inte längre för att skapa nya innehållsfragment på AEM as a Cloud Service. Kunderna måste skapa innehållsfragmentmodeller för att ersätta innehållets fragmentmallar.

* Möjlighet att identifiera resurser med fler än 100 underordnade under metadatanoden för resursen i databasen. Vi rekommenderar att du tar bort metadatanoder som inte behövs för att förbättra prestandan vid inläsning av mappar som består av sådana resurser.

* Möjlighet att identifiera och rapportera vilken typ av datalager som används.

* Mönstret har uppdaterats för AEM Form Portal.

### Felkorrigeringar {#bug-fixes-bpa}

* BPA rapporterade resultat för kärnkomponenter i stället för att bara rapportera om kundkomponenter. Den här har åtgärdats.
---
title: Versionsinformation för migreringsverktyg i AEM as a Cloud Service version 2022.3.0
description: Versionsinformation för migreringsverktyg i AEM as a Cloud Service version 2022.3.0
feature: Release Information
exl-id: ab43605d-d46e-43de-b71f-fab610609550
source-git-commit: 87e3291b4a72c24fc6cf8df488df305f1a078ea5
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 1%

---

# Versionsinformation för migreringsverktyg i AEM as a Cloud Service version 2022.3.0 {#release-notes}

Den här sidan innehåller versionsinformation för migreringsverktyg i AEM as a Cloud Service 2022.3.0.

## Best Practices Analyzer {#bpa-release}

### Releasedatum {#release-date-bpa}

Releasedatum för Best Practices Analyzer v2.1.26 är 16 mars 2022.

### Nyheter {#what-is-new-bpa}

* Möjlighet att upptäcka obearbetade resurser. Om obearbetade resurser upptäcks måste dessa resurser antingen ställas in på bearbetad eller tas bort från migreringsuppsättningen under innehållsöverföring för att undvika problem under innehållsimporten.
* Möjlighet att identifiera om innehållet har fler än 1000 ogiltiga URL:er. Det är inte bra att använda ett stort antal användar-URL:er eftersom en belastning läggs på Dispatcher- och Publish-servrar.
* Möjlighet att identifiera problem relaterade till indexdefinitioner för ekon och upptäcka inkompatibilitet med AEM as a Cloud Service.
* Möjlighet att upptäcka och rapportera om användningen av Externalizer-konfigurationer. I AEM as a Cloud Service externaliserarkonfigurationer anges av Cloud Manager, och därför måste befintliga Externalizer-konfigurationer omfaktoriseras för att bibehålla kompatibiliteten.

### Felkorrigeringar {#bug-fixes-bpa}

* I vissa scenarier gick det inte att köra BPA på grund av att FormsSelectiveFeaturesAnalysis genererade ett kontrollfel. Den här har åtgärdats.
* BPA rapporterade fynd relaterade till WRK-mönstret som MAJOR i stället för CRITICAL. Den här har åtgärdats.
* BPA rapporterade felaktigt resultat relaterade till OAK-indexdefinitioner i ui.apps som CRITICAL. Den här har åtgärdats.

## Content Transfer Tool {#ctt-release}

### Releasedatum {#release-date-ctt}

Releasedatum för Content Transfer Tool v1.9.0 är 28 februari 2022.

### Nyheter {#what-is-new-ctt}

* Kontrollera storleksordrar - Funktionen Kontrollera storlek för verktyget Innehållsöverföring hjälper till att minska misslyckade innehållsöverföringar.  Med funktionen Kontrollera storlek kan användarna 1) avgöra om de har tillräckligt med diskutrymme i `crx-quickstart` underkatalog före extrahering och 2) beräkna storleken på migreringsuppsättningen och kontrollera om den stöds. Om en av eller båda dessa kontroller överträds visas varningar i användargränssnittet för aktuell tid. Med den här skyddsguiden kan du undvika innehållsöverföringsfel och proaktivt diskutera migreringsalternativ med Adobe kundtjänst. Se [Bestämma migreringsuppsättningens storlek och diskutrymme](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=en#migration-set-size) för mer information.

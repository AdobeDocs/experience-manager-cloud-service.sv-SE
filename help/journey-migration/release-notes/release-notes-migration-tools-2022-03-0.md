---
title: Versionsinformation om migreringsverktyg i AEM as a Cloud Service version 2022.3.0
description: Versionsinformation om migreringsverktyg i AEM as a Cloud Service version 2022.3.0
feature: Release Information
exl-id: ab43605d-d46e-43de-b71f-fab610609550
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 1%

---

# Versionsinformation om migreringsverktyg i AEM as a Cloud Service version 2022.3.0 {#release-notes}

Den här sidan innehåller versionsinformation för migreringsverktyg i AEM as a Cloud Service 2022.3.0.

## Best Practices Analyzer {#bpa-release}

### Releasedatum {#release-date-bpa}

Releasedatum för Best Practices Analyzer v2.1.26 är 16 mars 2022.

### Nyheter {#what-is-new-bpa}

* Möjlighet att upptäcka obearbetade resurser. Om obearbetade resurser upptäcks måste dessa resurser antingen ställas in på att bearbetas eller tas bort från migreringsuppsättningen under innehållsöverföring för att undvika problem under innehållsimporten.
* Möjlighet att identifiera om innehållet har fler än 1000 ogiltiga URL:er. Det är inte bra att använda ett stort antal användar-URL:er eftersom det belastar Dispatcher- och Publish-servrar.
* Möjlighet att identifiera problem relaterade till Oak indexdefinitioner och upptäcka inkompatibilitet med AEM as a Cloud Service.
* Möjlighet att upptäcka och rapportera om användningen av Externalizer-konfigurationer. I AEM as a Cloud Service Externalizer ställs konfigurationerna in av Cloud Manager. Därför måste befintliga Externalizer-konfigurationer omfaktoriseras för att bibehålla kompatibiliteten.

### Felkorrigeringar {#bug-fixes-bpa}

* I vissa scenarier gick det inte att köra BPA på grund av att FormsSelectiveFeaturesAnalysis genererade ett kontrollfel.
* BPA rapporterade fynd relaterade till WRK-mönstret som MAJOR i stället för CRITICAL.
* BPA rapporterade felaktigt resultat relaterade till Oak indexdefinitioner i ui.apps som CRITICAL.

## Verktyget Innehållsöverföring {#ctt-release}

### Releasedatum {#release-date-ctt}

Releasedatum för Content Transfer Tool v1.9.0 är 28 februari 2022.

### Nyheter {#what-is-new-ctt}

* Kontrollera storleksordrar - Funktionen Kontrollera storlek för verktyget Innehållsöverföring hjälper till att minska misslyckade innehållsöverföringar. Med funktionen Kontrollera storlek kan användare avgöra om de har tillräckligt med diskutrymme i underkatalogen `crx-quickstart` innan extraheringen. De kan också beräkna storleken på migreringsuppsättningen och kontrollera om den stöds. Om en eller båda dessa kontroller överträds visas varningar i CTT-användargränssnittet. Med den här skyddsguiden kan du undvika innehållsöverföringsfel och proaktivt diskutera migreringsalternativ med Adobe kundtjänst. Mer information finns i [Bestämma migreringsuppsättningens storlek och diskutrymme](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html#migration-set-size).

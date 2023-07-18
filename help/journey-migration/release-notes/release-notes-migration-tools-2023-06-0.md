---
title: Versionsinformation för migreringsverktyg i AEM as a Cloud Service version 2023.06.0
description: Versionsinformation för migreringsverktyg i AEM as a Cloud Service version 2022.06.0
feature: Release Information
source-git-commit: 88227693b7dfc3cbd30751718dc85e55ee67bb96
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 2%

---

# Versionsinformation för migreringsverktyg i AEM as a Cloud Service version 2023.06.0 {#release-notes}

Den här sidan innehåller versionsinformation för migreringsverktyg i AEM as a Cloud Service 2022.06.0.

## Content Transfer Tool {#ctt-release}

### Releasedatum {#release-date-ctt}

Releasedatum för Content Transfer Tool v 2.0.20 är 8 juni 2023.

### Nyheter {#what-is-new-ctt}

* Ett nytt migreringsverktyg - Content Transformer (CT) har integrerats med Content Transfer Tool (CTT) i den här versionen. Innehållstransformeraren kan automatiskt identifiera och åtgärda innehållsrelaterade problem som rapporterats av [Best Practices Analyzer (BPA)](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en) innan du migrerar innehåll från den aktuella AEM-implementeringen (lokal eller Managed Services) till AEM as a Cloud Service.
Fördelarna med Content Transformer är:
   * Felsäker: ett paket skapas av innehållstreraren varje gång den gör ändringar i databasen för att åtgärda problem. Om det behövs kan du återgå till det tidigare läget genom att installera paketet.
   * Lättanvänt: Content Transformer har integrerats med Content Transfer Tool och har ett enkelt, intuitivt användargränssnitt.
   * Sparar tid: När du har ett stort antal innehållsproblem som faller under en mönsterkategori kan du lösa alla med bara ett par klick med hjälp av Innehållsomvandlaren, vilket minskar tiden och komplexiteten vid migrering avsevärt.

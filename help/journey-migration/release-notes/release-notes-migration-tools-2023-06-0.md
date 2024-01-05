---
title: Versionsinformation för migreringsverktyg i AEM as a Cloud Service version 2023.06.0
description: Versionsinformation för migreringsverktyg i AEM as a Cloud Service version 2023.06.0
feature: Release Information
exl-id: 021b7472-d1e4-4ef6-a040-c612fed8d3c3
source-git-commit: a77e5dc4273736b969e9a4a62fcac75664495ee6
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---

# Versionsinformation för migreringsverktyg i AEM as a Cloud Service version 2023.06.0 {#release-notes}

Den här sidan innehåller versionsinformation för migreringsverktyg i AEM as a Cloud Service 2023.06.0.

## Verktyget Innehållsöverföring {#ctt-release}

### Releasedatum {#release-date-ctt}

Releasedatum för Content Transfer Tool v 2.0.20 är 8 juni 2023.

### Nyheter {#what-is-new-ctt}

* Ett nytt migreringsverktyg - Content Transformer (CT) har integrerats med Content Transfer Tool (CTT) i den här versionen. Innehållstransformeraren kan automatiskt identifiera och åtgärda innehållsrelaterade problem som rapporterats av [Best Practices Analyzer (BPA)](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html) innan du migrerar innehåll från den aktuella AEM-implementeringen (lokal eller Managed Services) till AEM as a Cloud Service.
Fördelarna med Content Transformer är:
   * Felsäker: ett paket skapas av innehållstreraren varje gång det ändras i databasen för att åtgärda problem. Om det behövs kan du återgå till det tidigare läget genom att installera paketet.
   * Lättanvänt: Content Transformer har integrerats med Content Transfer Tool och har ett enkelt, intuitivt användargränssnitt.
   * Sparar tid: när du har ett stort antal innehållsproblem som faller under en mönsterkategori kan du lösa dem alla med flera klick med hjälp av Innehållsomvandlaren, vilket minskar tiden och komplexiteten vid migrering avsevärt.

---
title: Dynamic Media begränsningar
description: 'Lär dig mer om de effektivaste strategierna och de tvingande gränserna när du skapar en bilduppsättning eller en snurruppsättning, eller överför en PDF. Läs också om webbläsarkombinationer och operativsystemkombinationer som inte stöds för Dynamic Media Viewer. '
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/Dynamic-Media-Classic
geptopics: SG_SCENESEVENONDEMAND_PK/categories/ecatalogs
feature: Dynamic Media Classic,Asset Management,Viewers,Image Sets,Spin Sets,eCatalog
role: User
source-git-commit: 42298e0ff7d977a32c87e61e9e1f4b02a846f2c0
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 3%

---

# Dynamic Media-begränsningar

I följande avsnitt beskrivs begränsningar i Dynamic Media.

Det här avsnittet innehåller följande avsnitt:

* Dynamic Media bästa praxis och tvingande begränsningar för tillgångstyper

<!-- * Unsupported web browser and operating system combinations for Dynamic Media Viewers -->

## Dynamic Media bästa praxis och tvingande begränsningar för tillgångstyper

När du skapar en snurra uppsättning eller en bilduppsättning, eller överför PDF för sidextrahering, rekommenderar Adobe följande metodtips och tillämpar följande begränsningar:

| Resurs - begränsningstyp | Bästa praxis | Implementerad gräns | Ändringar av begränsningen 31 december 2022 |
| --- | --- | --- | --- |
| **Bild** - Antal smarta beskärningar per bild | 5 | 100 |  |
| **Bilduppsättning** - Antal dubblettresurser per uppsättning | Inga dubbletter | 100 | 20 |
| **Bilduppsättning** - Maximalt antal bilder per uppsättning | 5-10 bilder per uppsättning | 1000 |
| **Snurra uppsättning** - Maximalt antal rader/kolumner per 2D-uppsättning | 12-18 bilder per uppsättning | 1000 |
| **PDF** - Maximalt antal sidor för PDF som ska användas för extrahering |  | 5000 (för nya överföringar) | 100 |

<!-- See also [Dynamic Media limitations](/help/assets/limitations.md). -->

<!-- ## Unsupported web browser and operating system combinations for Dynamic Media Viewers

Dynamic Media Viewers do not support following combinations of web browser and operating system.

* Internet Explorer 11 + Windows 7
* Internet Explorer 11 + Windows 8.1
* Internet Explorer 11 + Windows Phone 8.1
* Internet Explorer 11 + Windows Phone 8.1 Update
* Safari 6 + iOS 6.0.1
* Safari 7 + iOS 7.1
* Safari 7 + macOS X 10.9 Mavericks
* Safari 8 + iOS 8.4
* Safari 8 + macOS X 10.10 Yosemite -->
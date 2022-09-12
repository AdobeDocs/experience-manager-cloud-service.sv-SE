---
title: Dynamic Media begränsningar
description: Lär dig mer om de effektivaste strategierna och de tvingande gränserna när du skapar en bilduppsättning eller en snurruppsättning, eller överför en PDF. Läs också om webbläsarkombinationer och operativsystemkombinationer som inte stöds för Dynamic Media Viewer.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/Dynamic-Media-Classic
geptopics: SG_SCENESEVENONDEMAND_PK/categories/ecatalogs
feature: Dynamic Media Classic,Asset Management,Viewers,Image Sets,Spin Sets,eCatalog
role: User
exl-id: fb63e2d4-2c8c-48dd-a0dc-fdfbbfb57b30
source-git-commit: 479349d2dad841a782519de3302993ea2a9f5162
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 4%

---

# Dynamic Media-begränsningar

I följande avsnitt beskrivs begränsningar i Dynamic Media.

Det här avsnittet innehåller följande avsnitt:

* [Dynamic Media bästa praxis och tvingande begränsningar för tillgångstyper](#best-practice-enforced-limits)
* [Webbläsare- och operativsystemskombinationer som inte stöds för Dynamic Media Viewer](#unsupported-browser-os)

## Dynamic Media bästa praxis och tvingande begränsningar för tillgångstyper {#best-practice-enforced-limits}

När du skapar en snurra uppsättning eller en bilduppsättning, eller överför PDF för sidextrahering, rekommenderar Adobe följande metodtips och tillämpar följande begränsningar:

| Resurs - begränsningstyp | Bästa praxis | Begränsning har införts | Ändring till begränsning den 31 december 2022 |
| --- | --- | --- | --- |
| **Bild** - Antal smarta beskärningar per bild | 5 | 100 | 20 |
| **Alla uppsättningar** - Antal dubblettresurser per uppsättning | Inga dubbletter | 20 | Ej relevant |
| **Alla uppsättningar** - Maximalt antal resurser per uppsättning | 5-10 bilder per uppsättning | 1000 | Ej relevant |
| **Snurra uppsättning** - Maximalt antal rader/kolumner per 2D-uppsättning | 12-18 bilder per uppsättning | 1000 | Ej relevant |
| **PDF** - Maximalt antal sidor för PDF som ska användas för extrahering |  | 5000 (för nya överföringar) | 100 (för alla PDF) |

<!-- See also [Dynamic Media limitations](/help/assets/limitations.md). -->

## Webbläsare- och operativsystemskombinationer som inte stöds för Dynamic Media Viewer {#unsupported-browser-os}

Dynamic Media Viewer stöder inte följande kombinationer av webbläsare och operativsystem.

* Internet Explorer 11 + Windows 7
* Internet Explorer 11 + Windows 8.1
* Internet Explorer 11 + Windows Phone 8.1
* Internet Explorer 11 + Windows Phone 8.1 - uppdatering
* Safari 6 + iOS 6.0.1
* Safari 7 + iOS 7.1
* Safari 7 + OS X 10.9 Mavericks
* Safari 8 + iOS 8.4
* Safari 8 + OS X 10.10 Yosemite

## Stöd för TLS 1.0 och 1.1 upphör {#tls}

<!-- CQDOC-19433 -->

Från och med 30 september 2022 upphör stödet för Dynamic Media-visningsprogram för Adobe att

* TLS (Transport Layer Security) 1.0 och 1.1
* Följande svaga lärare i TLS 1.2:
   * `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384`
   * `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA`
   * `TLS_RSA_WITH_AES_256_GCM_SHA384`
   * `TLS_RSA_WITH_AES_256_CBC_SHA256`
   * `TLS_RSA_WITH_AES_256_CBC_SHA`
   * `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256`
   * `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA`
   * `TLS_RSA_WITH_AES_128_GCM_SHA256`
   * `TLS_RSA_WITH_AES_128_CBC_SHA256`
   * `TLS_RSA_WITH_AES_128_CBC_SHA`
   * `TLS_RSA_WITH_CAMELLIA_256_CBC_SHA`
   * `TLS_RSA_WITH_CAMELLIA_128_CBC_SHA`
   * `TLS_ECDHE_RSA_WITH_3DES_EDE_CBC_SHA`
   * `TLS_RSA_WITH_SDES_EDE_CBC_SHA`


---
title: Dynamic Media begränsningar
description: Lär dig mer om de effektivaste strategierna och de tvingande gränserna när du skapar en bilduppsättning eller en snurruppsättning, eller överför en PDF. Läs också om webbläsarkombinationer och operativsystemkombinationer som inte stöds för Dynamic Media.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/Dynamic-Media-Classic
geptopics: SG_SCENESEVENONDEMAND_PK/categories/ecatalogs
feature: Dynamic Media Classic,Asset Management,Image Sets,Spin Sets,eCatalog
role: User
exl-id: fb63e2d4-2c8c-48dd-a0dc-fdfbbfb57b30
source-git-commit: 284b46066a3cd64351c9915eb6a12875517a0c3d
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 5%

---

# Dynamic Media-begränsningar

I följande avsnitt beskrivs begränsningar i Dynamic Media.

Det här avsnittet innehåller följande avsnitt:

* [Dynamic Media bästa praxis och tvingande begränsningar för tillgångstyper](#best-practice-enforced-limits)
* [Webbläsare och operativsystem som inte stöds för Dynamic Media](#unsupported-browser-os)

## Dynamic Media bästa praxis och tvingande begränsningar för tillgångstyper {#best-practice-enforced-limits}

När du skapar en snurra uppsättning eller en bilduppsättning, eller överför PDF för sidextrahering, rekommenderar Adobe följande metodtips och tillämpar följande begränsningar:

| Resurs - begränsningstyp | Bästa praxis | Begränsning har införts | Ändring till begränsning den 31 december 2022 |
| --- | --- | --- | --- |
| **Bild** - Antal smarta beskärningar per bild | 5 | 100 | Ej relevant |
| **Alla uppsättningar** - Antal dubblettresurser per uppsättning | Inga dubbletter | 20 | Ej relevant |
| **Alla uppsättningar** - Maximalt antal resurser per uppsättning | 5-10 bilder per uppsättning | 1000 | Ej relevant |
| **Snurra uppsättning** - Maximalt antal rader/kolumner per 2D-uppsättning | 12-18 bilder per uppsättning | 1000 | Ej relevant |
| **PDF** - Maximalt antal sidor för PDF som ska användas för extrahering |  | 5000 (för nya överföringar) | 100 (för alla PDF) |

<!-- See also [Dynamic Media limitations](/help/assets/limitations.md). -->

## Webbläsare och operativsystem som inte stöds för Dynamic Media {#unsupported-browser-os}

Dynamic Media stöder inte följande kombinationer av webbläsare och operativsystem.

* Internet Explorer 11 + Windows 7
* Internet Explorer 11 + Windows 8.1
* Internet Explorer 11 + Windows Phone 8.1
* Internet Explorer 11 + Windows Phone 8.1 - uppdatering
* Safari 6 + iOS 6.0.1
* Safari 7 + iOS 7.1
* Safari 7 + OS X 10.9 Mavericks
* Safari 8 + iOS 8.4
* Safari 8 + OS X 10.10 Yosemite

<!-- ## End of support for TLS 1.0 and 1.1 {#tls}

CQDOC-19433 (original ticket)
and CQDOC-19792 (removed as per this ticket December 5, 2022)

Effective September 30, 2022, Adobe Dynamic Media will end support for the following:

* TLS (Transport Layer Security) 1.0 and 1.1
* The following weak ciphers in TLS 1.2:
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
  * `TLS_RSA_WITH_SDES_EDE_CBC_SHA` -->


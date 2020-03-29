---
title: Filformat och MIME-typer som stöds av Experience Manager Assets som en molntjänst
description: Filformat och MIME-typer som stöds av Experience Manager Assets som en molntjänst.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 68b2214a4c8941365120bdef670e89b4c9058966

---


# Assets supported file formats {#supported-file-formats}

Adobe Experience Manager som molntjänst har stöd för grundläggande innehållshanteringsfunktioner - lagring, hantering av metadata online, versionshantering, överföring och hämtning och så vidare - för alla binära filer, oavsett format. Adobe Experience Manager Assets har stöd för ett stort antal filformat och varje produktfunktion har ett varierat stöd för olika format.

Dessutom har Experience Manager Assets utökat stöd för att generera förhandsgranskningar och återgivningar och extrahera metadata och text för fulltextindexering. Detta utökade stöd tillhandahålls med hjälp av [tillgångsmikrotjänster](asset-microservices-configure-and-use.md).

Följande förklaring beskriver supportnivån.

| Supportnivå | Beskrivning |
| ------------------------------------------------------------ | --------------------------- |
| ✓ | Stöds |
| * | Se anmärkningarna nedanför tabellen |
| - | Ej relevant |

## Konvertering av tillgångar med hjälp av mikrotjänster {#asset-microservices-supported-formats}

Högdagrarna är följande:

* Viktiga [Adobe-filformat](#adobe-formats) som skapats av program och tjänster från Adobe, bland annat Adobe Photoshop, InDesign, Illustrator, XD, Dimension och Acrobat / PDF.
* Viktiga [bildfilformat](#image-formats).
* [Camera Raw-filformat](#camera-raw-formats) för en mängd olika kameror, inklusive Canon, Nikon, Fujifilm, Olympus och andra tillverkare (med Adobe Camera Raw som bas).
* Vanliga [dokumentformat](#document-formats), inklusive [Microsoft Office](#microsoft-office-formats) (Word, Excel, PowerPoint) och [Open Document](#opendocument-formats) -format.
* Ett stort antal [video](#video-formats)- och [ljud](#audio-formats)-format.

Kolumnerna i följande tabeller innehåller följande information:

| Kolumn | Beskrivning |
| ------------ | --------------------------------------------------------------- |
| Format | Filformat (filtillägg) för objektets ursprungliga binära fil |
| GIF | GIF-format för återgivningsgenerering |
| JPEG | JPEG-format för återgivningsgenerering |
| PNG | PNG-format för återgivningsgenerering |
| XMP | Extrahering av metadata från den ursprungliga binärfilen |
| TXT | Extrahering av text från dokument för indexering |
| Bredd/höjd | Stöd för att definiera bredden och höjden på en återgivning (pixlar) |

### Adobe-format {#adobe-formats}

| Filformat | GIF | JPEG | PNG | TXT | XMP | Bredd/höjd |
| ----------- | --- | ---- | --- | --- | --- | ------------ |
| AI | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| COLLAGE | - | - | - | - | ✓ | - |
| DN | ✓ | ✓ | ✓ |  | ✓ | ✓ |
| IDÉER | - | - | - | - | ✓ | - |
| INDD | ✓ | ✓ | ✓ | - | ✓ | ✓* |
| INDT | - | - | - | - | ✓ | - |
| PDF | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| PROTO | - | - | - | - | ✓ | - |
| PSB | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| PSD | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| XD | ✓ | ✓ | ✓ | - | ✓ | ✓ |

\* För INDD (InDesign-filer) bestäms återgivningens storlek av den förhandsgranskning som är inbäddad i INDD-filen. Konfigurera inställningarna i InDesign (**[!UICONTROL Inställningar > Filhantering > Spara alltid förhandsvisningsbilder med dokument, förhandsvisningsstorlek]**) för att bädda in större återgivning.

### Bildformat {#image-formats}

| Filformat | GIF | JPEG | PNG | XMP | Bredd/höjd |
| ----------- | --- | ---- | --- | --- | ------------ |
| BMP | ✓ | ✓ | ✓ | - | ✓ |
| EPS | - | - | - | ✓ | - |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ |
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ |
| SVG | - | - | - | ✓ | - |
| TIFF | ✓ | ✓ | ✓ | ✓ | ✓ |

### Camera RAW-format {#camera-raw-formats}

| Filformat | GIF | JPEG | PNG | XMP | Bredd/höjd |
| ----------- | --- | ---- | --- | --- | ------------ |
| 3FR | ✓ | ✓ | ✓ | ✓ | ✓ |
| ARW | ✓ | ✓ | ✓ | ✓ | ✓ |
| CR2 | ✓ | ✓ | ✓ | ✓ | ✓ |
| CR3 | ✓ | ✓ | ✓ | ✓ | ✓ |
| CRW | ✓ | ✓ | ✓ | ✓ | ✓ |
| DCR | ✓ | ✓ | ✓ | ✓ | ✓ |
| DNG | ✓ | ✓ | ✓ | ✓ | ✓ |
| ERF | ✓ | ✓ | ✓ | ✓ | ✓ |
| FFF | ✓ | ✓ | ✓ | ✓ | ✓ |
| GPR | ✓ | ✓ | ✓ | ✓ | ✓ |
| IIQ | ✓ | ✓ | ✓ | ✓ | ✓ |
| KDC | ✓ | ✓ | ✓ | ✓ | ✓ |
| MEF | ✓ | ✓ | ✓ | ✓ | ✓ |
| MFW | ✓ | ✓ | ✓ | ✓ | ✓ |
| MOS | ✓ | ✓ | ✓ | ✓ | ✓ |
| MRW | ✓ | ✓ | ✓ | ✓ | ✓ |
| NEF | ✓ | ✓ | ✓ | ✓ | ✓ |
| NRW | ✓ | ✓ | ✓ | ✓ | ✓ |
| ORF | ✓ | ✓ | ✓ | ✓ | ✓ |
| PEF | ✓ | ✓ | ✓ | ✓ | ✓ |
| RAF | ✓ | ✓ | ✓ | ✓ | ✓ |
| RAW | ✓ | ✓ | ✓ | ✓ | ✓ |
| RW2 | ✓ | ✓ | ✓ | ✓ | ✓ |
| RWL | ✓ | ✓ | ✓ | ✓ | ✓ |
| SRF | ✓ | ✓ | ✓ | ✓ | ✓ |
| SRW | ✓ | ✓ | ✓ | ✓ | ✓ |
| X3F | ✓ | ✓ | ✓ | ✓ | ✓ |

### Dokumentformat {#document-formats}

| Filformat | TXT | XMP |
| ----------- | --- | --- |
| EPUB | ✓ | - |
| HTML | ✓ | - |
| PS | - | ✓ |
| RTF | ✓ | - |
| TEXT | ✓ | - |
| XML | ✓ | - |

### Microsoft Office-format {#microsoft-office-formats}

| Filformat | GIF | JPEG | PNG | TEXT | Bredd/höjd |
| ----------- | --- | ---- | --- | ---- | ------------ |
| DOCX | ✓ | ✓ | ✓ | ✓ | ✓ |
| PPTX | ✓ | ✓ | ✓ | ✓ | ✓ |
| XLSX | ✓ | ✓ | ✓ | ✓ | ✓ |

### OpenDocument-format {#opendocument-formats}

| Filformat | GIF | JPEG | PNG | TEXT | Höjd |
| ----------- | --- | ---- | --- | ---- | ------ |
| ODF | ✓ | ✓ | ✓ | ✓ | ✓ |
| OFG | ✓ | ✓ | ✓ | ✓ | ✓ |
| ODM | ✓ | ✓ | ✓ | ✓ | ✓ |
| ODP | ✓ | ✓ | ✓ | ✓ | ✓ |
| ODS | ✓ | ✓ | ✓ | ✓ | ✓ |
| ODT | ✓ | ✓ | ✓ | ✓ | ✓ |

### Videoformat {#video-formats}

| Filformat | GIF | JPEG | PNG | XMP | Bredd/höjd |
| ----------- | --- | ---- | --- | --- | ------------ |
| 3G2 | - | - | - | ✓ | - |
| 3GP | - | - | - | ✓ | - |
| AVI | ✓ | ✓ | ✓ | ✓ | ✓ |
| DIVX | ✓ | ✓ | ✓ |  | ✓ |
| F4V | ✓ | ✓ | ✓ | ✓ | ✓ |
| FLV | ✓ | ✓ | ✓ | ✓ | ✓ |
| M2T | ✓ | ✓ | ✓ | - | ✓ |
| M2TS | ✓ | ✓ | ✓ | - | ✓ |
| M2V | ✓ | ✓ | ✓ | - | ✓ |
| M4V | ✓ | ✓ | ✓ | ✓ | ✓ |
| MKV | ✓ | ✓ | ✓ | - | ✓ |
| MOV | ✓ | ✓ | ✓ | ✓ | ✓ |
| MP4 | ✓ | ✓ | ✓ | ✓ | ✓ |
| MPEG | ✓ | ✓ | ✓ | ✓ | ✓ |
| MPG | ✓ | ✓ | ✓ | ✓ | ✓ |
| MTS | ✓ | ✓ | ✓ | - | ✓ |
| OGV | ✓ | ✓ | ✓ | - | ✓ |
| QT | ✓ | ✓ | ✓ | - | ✓ |
| R3D | ✓ | ✓ | ✓ | - | ✓ |
| SWF | ✓ | ✓ | ✓ | - | ✓ |
| WEBM | ✓ | ✓ | ✓ | - | ✓ |
| WMV | ✓ | ✓ | ✓ | ✓ | ✓ |

### Ljudformat {#audio-formats}

Resurser som molntjänst ger XMP-stöd för följande ljudformat: AIF, ASF, M4A, MP3, WAV och WMA.

## Dokumentformat som stöds {#doc-formats}

Dokumentformat som stöds för filhanteringsfunktioner är följande.

| Filformat | Lagring | Metadatahantering | [Anslutna resurser](use-assets-across-connected-assets-instances.md) |
|---|---|---|---|
| DOC | ✓ | ✓ | ✓ |
| DOCX | ✓ | ✓ | ✓ |
| ODT | ✓ | ✓ | ✓ |
| PDF | ✓ | ✓ | ✓ |
| HTML | ✓ | ✓ | ✓ |
| RTF | ✓ | ✓ | ✓ |
| TXT | ✓ | ✓ | ✓ |
| XLS | ✓ | ✓ | ✓ |
| XLSX | ✓ | ✓ | ✓ |
| PPT | ✓ | ✓ | ✓ |
| PPTX | ✓ | ✓ | ✓ |

>[!MORELIKETHIS]
>
>* [Behandling av tillgångar med hjälp av mikrotjänster](asset-microservices-overview.md)


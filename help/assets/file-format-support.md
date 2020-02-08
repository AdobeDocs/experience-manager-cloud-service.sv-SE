---
title: Filformat och MIME-typer som stöds av Experience Manager Assets som en molntjänst
description: Filformat och MIME-typer som stöds av Experience Manager Assets som en molntjänst.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 776b089a322cc4f86fdcb9ddf1c3cc207fc85d39

---


# Resurser som stöds i filformat {#supported-file-formats}

Adobe Experience Manager som molntjänst har stöd för grundläggande innehållshanteringsfunktioner - lagring, hantering av metadata online, versionshantering, överföring och hämtning och så vidare - för alla binära filer, oavsett format. Dessutom har programmet utökat stöd för de vanligaste filformaten, som bild, Adobe-material, dokument och video, för att generera förhandsgranskningar och återgivningar samt extrahera metadata och text för fulltextindexering. Detta utökade stöd tillhandahålls med hjälp av [tillgångsmikrotjänster](asset-microservices-configure-and-use.md).

En del högdagrar med utökat stöd för filformat är:

* Viktiga [Adobe-filformat](#adobe-formats) som skapats av program och tjänster från Adobe, bland annat Adobe Photoshop, InDesign, Illustrator, XD, Dimension och Acrobat / PDF.
* Viktiga [bildfilformat](#image-formats)
* [Camera Raw-filformat](#camera-raw-formats) för en mängd olika kameror, bland annat Canon, Nikon, Fujifilm, Olympus och andra (från Adobe Camera Raw)
* Vanliga [dokumentformat](#document-formats), inklusive [Microsoft Office](#microsoft-office-formats) (Word, Excel, PowerPoint) och [Open Document](#opendocument-formats) -format
* Ett stort antal [video](#video-formats) - och [ljudformat](#audio-formats)

## Förklaring till detaljerad supportinformation {#legend-for-detailed-support-information}

Följande förklaring beskriver nivån på stödet för en funktion:

| Supportnivå | Beskrivning |
| ------------------------------------------------------------ | --------------------------- |
| ✓ | Stöds |
| * | Se anmärkningarna nedanför tabellen |
| - | Ej relevant |

Kolumnerna i supporttabellerna innehåller följande information:

| Kolumn | Beskrivning |
| ------------ | --------------------------------------------------------------- |
| Format | Filformat (filtillägg) för objektets ursprungliga binära fil |
| GIF | GIF-format för återgivningsgenerering |
| JPEG | JPEG-format för återgivningsgenerering |
| PNG | PNG-format för återgivningsgenerering |
| XMP | Extrahering av metadata från den ursprungliga binärfilen |
| TXT | Extrahering av text från dokument för indexering |
| Bredd/höjd | Stöd för att definiera bredden och höjden på en återgivning (pixlar) |

<!-- Adding this checkmark icon ✓ does not look good in table. The icon's shade and size has to be toned down for good readability and less clutter.
@gklebus: I suggest using a checkmark character, either U+2713 ✓ CHECK MARK or U+2714 ✔ HEAVY CHECK MARK
-->

## Adobe-format {#adobe-formats}

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

## Bildformat {#image-formats}

| Filformat | GIF | JPEG | PNG | XMP | Bredd/höjd |
| ----------- | --- | ---- | --- | --- | ------------ |
| BMP | ✓ | ✓ | ✓ | - | ✓ |
| EPS | - | - | - | ✓ | - |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ |
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ |
| SVG | - | - | - | ✓ | - |
| TIFF | ✓ | ✓ | ✓ | ✓ | ✓ |


## Camera RAW-format {#camera-raw-formats}

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

## Dokumentformat {#document-formats}

| Filformat | TXT | XMP |
| ----------- | --- | --- |
| EPUB | ✓ | - |
| HTML | ✓ | - |
| PS | - | ✓ |
| RTF | ✓ | - |
| TEXT | ✓ | - |
| XML | ✓ | - |

## Microsoft Office-format {#microsoft-office-formats}

| Filformat | GIF | JPEG | PNG | TEXT | Bredd/höjd |
| ----------- | --- | ---- | --- | ---- | ------------ |
| DOCX | ✓ | ✓ | ✓ | ✓ | ✓ |
| PPTX | ✓ | ✓ | ✓ | ✓ | ✓ |
| XLSX | ✓ | ✓ | ✓ | ✓ | ✓ |

## OpenDocument-format {#opendocument-formats}

| Filformat | GIF | JPEG | PNG | TEXT | Höjd |
| ----------- | --- | ---- | --- | ---- | ------ |
| ODF | ✓ | ✓ | ✓ | ✓ | ✓ |
| OFG | ✓ | ✓ | ✓ | ✓ | ✓ |
| ODM | ✓ | ✓ | ✓ | ✓ | ✓ |
| ODP | ✓ | ✓ | ✓ | ✓ | ✓ |
| ODS | ✓ | ✓ | ✓ | ✓ | ✓ |
| ODT | ✓ | ✓ | ✓ | ✓ | ✓ |

## Videoformat {#video-formats}

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

## Ljudformat {#audio-formats}

Resurser som molntjänst ger XMP-stöd för följande ljudformat: AIF, ASF, M4A, MP3, WAV och WMA.

<!-- TBD: Some items from https://helpx.adobe.com/experience-manager/6-5/assets/using/assets-formats.html#SupportedinputvideoformatsforDynamicMediatranscoding may be applicable.

Bring more parity with https://helpx.adobe.com/experience-manager/6-5/assets/using/assets-formats.html#SupportedMIMEtypes.
https://helpx.adobe.com/experience-manager/6-5/assets/using/assets-formats.html#Supportedmultimediaformats
-->

>[!MORELIKETHIS]
>
>* [Behandling av tillgångar med hjälp av mikrotjänster](asset-microservices-overview.md)


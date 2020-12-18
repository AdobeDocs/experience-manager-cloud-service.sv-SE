---
title: Filformat och MIME-typer som stöds
description: Filformat och MIME-typer som stöds av [!DNL Experience Manager Assets] som a [!DNL Cloud Service].
contentOwner: AG
translation-type: tm+mt
source-git-commit: 744f63306187b991a11acee2071b9266d11e1a21
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 6%

---


# [!DNL Assets] filformat som stöds  {#supported-file-formats}

[!DNL Adobe Experience Manager] som en  [!DNL Cloud Service] lösning med stöd för grundläggande innehållshanteringsfunktioner - lagring, hantering av metadata online, versionshantering, överföring och hämtning med mera - för alla binära filer, oavsett filformat. [!DNL Adobe Experience Manager Assets] har stöd för ett stort antal filformat och alla funktioner har olika stöd för olika format.

[!DNL Experience Manager Assets] har dessutom utökat stöd för att generera förhandsgranskningar och återgivningar och extrahera metadata och text för fulltextindexering. Detta utökade stöd tillhandahålls med [asset microservices](asset-microservices-configure-and-use.md).

Några av de viktigaste funktionerna för tillgångskonvertering med hjälp av mikrotjänster:

* Nyckelformat [Adobe](#adobe-formats) som skapats av Adobe program och tjänster, inklusive [!DNL Adobe Photoshop], [!DNL Adobe InDesign], [!DNL Adobe Illustrator], [!DNL Adobe XD], [!DNL Adobe Dimension] och [!DNL Adobe Acrobat] eller PDF.
* Nyckel [filformat för bildåtergivning](#image-formats).
* [Camera Raw filformat ](#camera-raw-formats) för ett stort antal kameror, inklusive Canon, Nikon, Fujifilm, Olympus och andra tillverkare (med Adobe Camera Raw i botten).
* Vanliga [dokumentformat](#document-formats), inklusive Microsoft Office- och Open Document-format.
* Ett stort antal [video](#video-formats)- och [ljud](#audio-formats)-format.

Följande förklaring beskriver supportnivån.

| Supportnivå | Beskrivning |
| ------------- | --------------------------- |
| ✓ | Stöds |
| * | Se anmärkningarna nedanför tabellen |
| - | Ej relevant |

## Adobe-format {#adobe-formats}

| Filformat | Generering av miniatyrbilder | Extrahering av fulltext | Extrahering av metadata | Bredd/höjd |
| ----------- | -------------------- | ------------------- | ------------------- | ------------ |
| AI | ✓ | - | ✓ | ✓ |
| COLLAGE | - | - | ✓ | - |
| DN | ✓ | - | ✓ | ✓ |
| IDÉER | - | - | ✓ | - |
| INDD | ✓ | - | ✓ | ✓ * |
| INDT | - | - | ✓ | - |
| PDF | ✓ | ✓ | ✓ | ✓ |
| PROTO | - | - | ✓ | - |
| PSB | ✓ | - | ✓ | ✓ |
| PSD | ✓ | - | ✓ | ✓ |
| XD | ✓ | - | ✓ | ✓ |

\* För [!DNL Adobe InDesign]-filer (INDD) bestäms återgivningens storlek av den förhandsgranskning som är inbäddad i INDD-filen. Konfigurera inställningarna i [!DNL InDesign] (**[!UICONTROL Preferences > File Handling > Always Save Preview Images with Documents, Preview Size]**) för att bädda in större återgivning.

## Bildformat {#image-formats}

| Filformat | Generering av miniatyrbilder | Extrahering av metadata | Bredd/höjd | Beskär |
| ----------- | -------------------- | ------------------- | ------------ | -------- |
| BMP | ✓ | - | ✓ | ✓ |
| EPS | - | ✓ | - | - |
| GIF | ✓ | ✓ | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ |
| PNG | ✓ | ✓ | ✓ | ✓ |
| TIFF | ✓ | ✓ | ✓ | - |
| SVG | ✓ | - | ✓ | ✓ |
| SGI | ✓ | ✓ | ✓ | ✓ |
| RGB | ✓ | ✓ | ✓ | ✓ |
| RGBA | ✓ | ✓ | ✓ | ✓ |

## Bildformat i [!DNL Dynamic Media] {#image-support-dynamic-media}

| Format | Överför (indataformat) | Skapa bildförinställning (utdataformat) | Förhandsgranska dynamisk återgivning | Leverera dynamisk återgivning | Hämta dynamisk återgivning |
| ------- | --------------------- | ----------------------------------- | ------------------------- | ------------------------- | -------------------------- |
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ |
| TIFF | ✓ | ✓ | ✓ | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ |
| BMP | ✓ | - | - | - | - |
| PSD   ‡ | ✓ | - | - | - | - |
| EPS | ✓ | ✓ | ✓ | ✓ | ✓ |
| PICT | ✓ | - | - | - | - |

‡ Den sammanfogade bilden extraheras från PSD-filen. Det är en bild som genereras av [!DNL Adobe Photoshop] och inkluderas i PSD-filen. Beroende på inställningarna kan den sammanfogade bilden vara den faktiska bilden eller inte.

Följande undertyper av rasterbildfilformat som inte stöds i [!DNL Dynamic Media]:

* PNG-filer som har en IDAT-segmentstorlek som är större än 100 MB.
* PSB-filer.
* PSD-filer med en annan färgrymd än CMYK, RGB, Gråskala eller Bitmapp stöds inte. Färgrymderna DuoTone, Lab och Indexed stöds inte.
* PSD-filer med ett bitdjup som är större än 16.
* TIFF-filer som har flyttalsdata.
* TIFF-filer med Lab-färgrymd.

## 3D-format {#support-3d-formats}

Följande lista över 3D-format stöds.

Se även [Arbeta med 3D-resurser i Dynamic Media.](/help/assets/dynamic-media/assets-3d.md)

| Format | Lagring | Versionshantering | Arbetsflöde | Publicering | Åtkomstkontroll | Förhandsvisning av miniatyrbilder | Förhandsgranska 3D | Leverans till Dynamic Media |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| DN | ✓ | ✓ | ✓ | - | ✓ | ✓ | - | - |
| gLB | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| gLTF | ✓ | ✓ | ✓ | - | ✓ | - | ✓ | - |
| OBJ | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| STL | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| USDz | ✓ | ✓ | ✓ | ✓ | ✓ | - | - | ✓ |

## [!DNL Camera RAW] format  {#camera-raw-formats}

| Filformat | Generering av miniatyrbilder | Extrahering av metadata | Bredd/höjd |
| ----------- | -------------------- | ------------------- | ------------ |
| 3FR | ✓ | ✓ | ✓ |
| ARW | ✓ | ✓ | ✓ |
| CR2 | ✓ | ✓ | ✓ |
| CR3 | ✓ | ✓ | ✓ |
| CRW | ✓ | ✓ | ✓ |
| DCR | ✓ | ✓ | ✓ |
| DNG | ✓ | ✓ | ✓ |
| ERF | ✓ | ✓ | ✓ |
| FFF | ✓ | ✓ | ✓ |
| GPR | ✓ | ✓ | ✓ |
| IIQ | ✓ | ✓ | ✓ |
| KDC | ✓ | ✓ | ✓ |
| MEF | ✓ | ✓ | ✓ |
| MFW | ✓ | ✓ | ✓ |
| MOS | ✓ | ✓ | ✓ |
| MRW | ✓ | ✓ | ✓ |
| NEF | ✓ | ✓ | ✓ |
| NRW | ✓ | ✓ | ✓ |
| ORF | ✓ | ✓ | ✓ |
| PEF | ✓ | ✓ | ✓ |
| RAF | ✓ | ✓ | ✓ |
| RAW | ✓ | ✓ | ✓ |
| RW2 | ✓ | ✓ | ✓ |
| RWL | ✓ | ✓ | ✓ |
| SRF | ✓ | ✓ | ✓ |
| SRW | ✓ | ✓ | ✓ |
| X3F | ✓ | ✓ | ✓ |

## Dokumentformat {#document-formats}

Följande dokumentformat stöds för filhanteringsfunktioner.

| Filformat | Generering av miniatyrbilder | Extrahering av fulltext | Bredd/höjd | Metadatahantering | [Anslutna resurser](use-assets-across-connected-assets-instances.md) |
| ----------- | -------------------- | ------------------- | ------------ | ------------------- | ---------------- |
| PDF | ✓ | ✓ | ✓ | ✓ | ✓ |
| DOCX | ✓ | ✓ | ✓ | ✓ | ✓ |
| DOC | - | - | - | ✓ | ✓ |
| PPTX | ✓ | ✓ | ✓ | ✓ | ✓ |
| PPT | - | - | - | ✓ | ✓ |
| XLSX | ✓ | ✓ | ✓ | ✓ | ✓ |
| XLS | - | - | - | ✓ | ✓ |
| ODF | ✓ | ✓ | ✓ | - | - |
| OFG | ✓ | ✓ | ✓ | - | - |
| ODM | ✓ | ✓ | ✓ | - | - |
| ODP | ✓ | ✓ | ✓ | - | - |
| ODS | ✓ | ✓ | ✓ | - | - |
| ODT | ✓ | ✓ | ✓ | ✓ | ✓ |
| EPUB | - | ✓ | - | - | - |
| HTML | - | ✓ | - | ✓ | ✓ |
| PS | - | - | ✓ | - | - |
| RTF | - | ✓ | - | ✓ | ✓ |
| TXT | - | ✓ | - | ✓ | ✓ |
| XML | - | ✓ | - | - | - |

## Dokumentformat i [!DNL Dynamic Media] {#document-support-dynamic-media}

| Format | Överför (indataformat) | Skapa bildförinställning (utdataformat) | Förhandsgranska dynamisk återgivning | Leverera dynamisk återgivning | Hämta dynamisk återgivning |
| ------ | --------------------- | ----------------------------------- | ------------------------- | ------------------------- | -------------------------- |
| AI | ✓ | - | - | - | - |
| PDF | ✓ | ✓ | ✓ | ✓ | ✓ |
| INDD | ✓ | - | - | - | - |

## Videoformat {#video-formats}

| Filformat | Generering av miniatyrbilder | Extrahering av metadata | Bredd/höjd |
| ----------- | -------------------- | ------------------- | ------------ |
| 3G2 | - | ✓ | - |
| 3GP | - | ✓ | - |
| AVI | ✓ | ✓ | ✓ |
| DIVX | ✓ | - | ✓ |
| F4V | ✓ | ✓ | ✓ |
| FLV | ✓ | ✓ | ✓ |
| M2T | ✓ | - | ✓ |
| M2TS | ✓ | - | ✓ |
| M2V | ✓ | - | ✓ |
| M4V | ✓ | ✓ | ✓ |
| MKV | ✓ | - | ✓ |
| MOV | ✓ | ✓ | ✓ |
| MP4 | ✓ | ✓ | ✓ |
| MPEG | ✓ | ✓ | ✓ |
| MPG | ✓ | ✓ | ✓ |
| MTS | ✓ | - | ✓ |
| OGV | ✓ | - | ✓ |
| QT | ✓ | - | ✓ |
| R3D | - | ✓ | ✓ |
| SWF | ✓ | - | ✓ |
| WebM | ✓ | - | ✓ |
| WMV | ✓ | ✓ | ✓ |

## Videoformat i [!DNL Dynamic Media] för omkodning {#video-dynamic-media-transcoding}

| Videofiltillägg | Behållare | Rekommenderade videokodekar | Videokodekar som inte stöds |
|------------------------|--------------------|--------|-------|
| MP4 | MPEG-4 | H264/AVC (alla profiler) | - |
| MOV, QT | Apple QuickTime | H264/AVC, Apple ProRes422 &amp; HQ, Sony XDCAM, Sony DVCAM, HDV, Panasonic DVCPro, Apple DV (DV25), Apple PhotoJPEG, Sorenson, Avid DNxHD, Avid AVR | Apple Intermediate, Apple Animation |
| FLV, F4V | Adobe Flash | H264/AVC, Flix VP6, H263, Sorenson | SWF (vektoranimeringsfiler) |
| WMV | Windows Media 9 | WMV3 (v9), WMV2 (v8), WMV1 (v7), GoToMeeting (G2M2, G2M3, G2M4) | Microsoft-skärm (MSS2), Microsoft Photo Story (WVP2) |
| MPG, VOB, M2V, MP2 | MPEG-2 | MPEG-2 | - |
| M4V | Apple iTunes | H264/AVC | - |
| AVI | A/V-sammanflätning | XVID, DIVX, HDV, MiniDV (DV25), Techsmith Camtasia, Huffyuv, Fraps, Panasonic DVCPro | Indeo3 (IV30), MJPEG, Microsoft Video 1 (MS-CRAM) |
| WebM | WebM | Google VP8 | - |
| OGV, OGG | Ogg | Theora, VP3, Dirac | - |
| MXF | MXF | Sony XDCAM, MPEG-2, MPEG-4, Panasonic DVCPro | - |
| MTS | AVCHD | H264/AVC | - |
| MKV | Matroska | H264/AVC | - |
| R3D, RM | Red Raw-video | MJPEG 2000 | - |
| RAM, RM | RealVideo | Stöds inte | Real G2 (RV20), Real 8 (RV30), Real 10 (RV40) |
| FLAC | Inbyggd Flash | Kostnadsfri förlustfri ljudkodek | - |
| MJ2 | Motion JPEG 2000 | Motion JPEG 2000-kodek | - |

## Ljudformat {#audio-formats}

[!DNL Assets] som en  [!DNL Cloud Service] funktion för XMP metadataextraheringsstöd för ljudformaten AIF, ASF, M4A, MP3, WAV och WMA.

## Tips och begränsningar {#limitations-and-tips}

* För närvarande är filstorleksgränsen för metadataextrahering ungefär 10 GB. När mycket stora resurser överförs misslyckas ibland metadataextraheringen.

>[!MORELIKETHIS]
>
>* [Behandling av tillgångar med hjälp av mikrotjänster](asset-microservices-overview.md)


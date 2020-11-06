---
title: Filformat och MIME-typer som stöds
description: Filformat och MIME-typer som stöds av Experience Manager Assets som Cloud Service.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 2df737ae0601774f4a9d1dce470125f596fab467
workflow-type: tm+mt
source-wordcount: '801'
ht-degree: 5%

---


# Assets supported file formats {#supported-file-formats}

Adobe Experience Manager som Cloud Service har stöd för grundläggande innehållshanteringsfunktioner - lagring, hantering av metadata online, versionshantering, överföring och hämtning och så vidare - för alla binära filer, oavsett format. Adobe Experience Manager Assets har stöd för en mängd olika filformat och alla funktioner har olika stöd för olika format.

Dessutom har Experience Manager Assets utökat stöd för att generera förhandsgranskningar och återgivningar och extrahera metadata och text för fulltextindexering. Detta utökade stöd tillhandahålls med hjälp av [tillgångsmikrotjänster](asset-microservices-configure-and-use.md).

Några av de viktigaste funktionerna för tillgångskonvertering med hjälp av mikrotjänster:

* Filformaten [för](#adobe-formats) Adobe som skapats av program och tjänster från Adobe, t.ex. Adobe Photoshop, Adobe InDesign, Adobe Illustrator, Adobe XD, Adobe Dimension och Adobe Acrobat eller PDF.
* Viktiga [bildfilformat](#image-formats).
* [Camera Raw filformat](#camera-raw-formats) för ett stort antal kameror, inklusive Canon, Nikon, Fujifilm, Olympus och andra tillverkare (med Adobe Camera Raw i botten).
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
| DN | ✓ |  | ✓ | ✓ |
| IDÉER | - | - | ✓ | - |
| INDD | ✓ | - | ✓ | ✓ * |
| INDT | - | - | ✓ | - |
| PDF | ✓ | ✓ | ✓ | ✓ |
| PROTO | - | - | ✓ | - |
| PSB | ✓ | - | ✓ | ✓ |
| PSD | ✓ | - | ✓ | ✓ |
| XD | ✓ | - | ✓ | ✓ |

\* För [!DNL Adobe InDesign] filer (INDD) bestäms återgivningens storlek av den förhandsgranskning som är inbäddad i INDD-filen. Konfigurera inställningarna i [!DNL InDesign] (**[!UICONTROL Preferences > File Handling > Always Save Preview Images with Documents, Preview Size]**) för att bädda in större återgivning.

## Bildformat {#image-formats}

| Filformat | Generering av miniatyrbilder | Extrahering av metadata | Bredd/höjd | Beskär |
| ----------- | -------------------- | ------------------- | ------------ | -------- |
| BMP | ✓ | - | ✓ | ✓ |
| EPS | - | ✓ | - | - |
| GIF | ✓ | ✓ | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ |
| PNG | ✓ | ✓ | ✓ | ✓ |
| TIFF | ✓ | ✓ | ✓ | - |

## Bildformat i [!DNL Dynamic Media] {#image-support-dynamic-media}

| Format | Överför (indataformat) | Skapa bildförinställning (utdataformat) | Förhandsgranska dynamisk återgivning | Leverera dynamisk återgivning | Hämta dynamisk återgivning |
| ------- | --------------------- | ----------------------------------- | ------------------------- | ------------------------- | -------------------------- |
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ |
| TIFF | ✓ | ✓ | ✓ | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ |
| BMP | ✓ | - | - | - | - |
| PSD ‡ | ✓ | - | - | - | - |
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

| Format | Lagring | Versionshantering | Arbetsflöde | Publicering | Åtkomstkontroll | Förhandsvisning av miniatyrbilder | Förhandsgranska 3D | Dynamisk medieleverans |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| DN | ✓ | ✓ | ✓ |  | ✓ | ✓ |  |  |
| gLB | ✓ | ✓ | ✓ | ✓ | ✓ |  | ✓ | ✓ |
| gLTF | ✓ | ✓ | ✓ |  | ✓ |  | ✓ |  |
| OBJ | ✓ | ✓ | ✓ | ✓ | ✓ |  | ✓ | ✓ |
| STL | ✓ | ✓ | ✓ | ✓ | ✓ |  | ✓ | ✓ |
| USDz | ✓ | ✓ | ✓ | ✓ | ✓ |  |  | ✓ |

## [!DNL Camera RAW] format {#camera-raw-formats}

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
| DIVX | ✓ |  | ✓ |
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
| R3D | ✓ | - | ✓ |
| SWF | ✓ | - | ✓ |
| WEBM | ✓ | - | ✓ |
| WMV | ✓ | ✓ | ✓ |

## Videoformat i [!DNL Dynamic Media] för omkodning {#video-dynamic-media-transcoding}

| Videofiltillägg | Behållare | Rekommenderade videokodekar | Videokodekar som inte stöds |
|------------------------|--------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------|
| MP4 | MPEG-4 | H264/AVC (alla profiler) |  |
| MOV, QT | Apple QuickTime | H264/AVC, Apple ProRes422 &amp; HQ, Sony XDCAM, Sony DVCAM, HDV, Panasonic DVCPro, Apple DV (DV25), Apple PhotoJPEG, Sorenson, Avid DNxHD, Avid AVR | Apple Intermediate, Apple Animation |
| FLV, F4V | Adobe Flash | H264/AVC, Flix VP6, H263, Sorenson | SWF (vektoranimeringsfiler) |
| WMV | Windows Media 9 | WMV3 (v9), WMV2 (v8), WMV1 (v7), GoToMeeting (G2M2, G2M3, G2M4) | Microsoft-skärm (MSS2), Microsoft Photo Story (WVP2) |
| MPG, VOB, M2V, MP2 | MPEG-2 | MPEG-2 |  |
| M4V | Apple iTunes | H264/AVC |  |
| AVI | A/V-sammanflätning | XVID, DIVX, HDV, MiniDV (DV25), Techsmith Camtasia, Huffyuv, Fraps, Panasonic DVCPro | Indeo3 (IV30), MJPEG, Microsoft Video 1 (MS-CRAM) |
| WebM | WebM | Google VP8 |  |
| OGV, OGG | Ogg | Theora, VP3, Dirac |  |
| MXF | MXF | Sony XDCAM, MPEG-2, MPEG-4, Panasonic DVCPro |  |
| MTS | AVCHD | H264/AVC |  |
| MKV | Matroska | H264/AVC |  |
| R3D, RM | Red Raw-video | MJPEG 2000 |  |
| RAM, RM | RealVideo | Stöds inte | Real G2 (RV20), Real 8 (RV30), Real 10 (RV40) |
| FLAC | Inbyggd Flash | Kostnadsfri förlustfri ljudkodek |  |
| MJ2 | Motion JPEG 2000 | Motion JPEG 2000-kodek |  |

## Ljudformat {#audio-formats}

Assets as a Cloud Service provides XMP metadata extraction support for AIF, ASF, M4A, MP3, WAV, and WMA audio formats.

>[!MORELIKETHIS]
>
>* [Behandling av tillgångar med hjälp av mikrotjänster](asset-microservices-overview.md)


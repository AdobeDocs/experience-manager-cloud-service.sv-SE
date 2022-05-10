---
title: Filformat och MIME-typer som stöds
description: Filformat och MIME-typer som stöds av [!DNL Experience Manager Assets] som [!DNL Cloud Service].
contentOwner: AG
feature: Asset Management,Renditions
role: User,Admin
exl-id: e848aa77-7829-4adc-8b88-0279791a4525
source-git-commit: 77cba988368c07438835148d08f1e8cc6e469b7b
workflow-type: tm+mt
source-wordcount: '984'
ht-degree: 4%

---

# [!DNL Assets] filformat som stöds {#supported-file-formats}

[!DNL Adobe Experience Manager] som [!DNL Cloud Service] har stöd för grundläggande funktioner för innehållshantering - lagring, hantering av metadata online, versionshantering, överföring och hämtning med mera - för alla binära filer, oavsett format. [!DNL Adobe Experience Manager Assets] har stöd för ett stort antal filformat och alla funktioner har olika stöd för olika format.

Dessutom [!DNL Experience Manager Assets] har utökat stöd för att generera förhandsgranskningar och återgivningar och för att extrahera metadata och text för fulltextindexering. Den här utökade supporten tillhandahålls med [tillgångsmikrotjänster](asset-microservices-configure-and-use.md).

Några av de viktigaste funktionerna för resurskonvertering är följande:

* Nyckel [Adobe-filformat](#adobe-formats) som producerats av Adobe program och tjänster, inklusive [!DNL Adobe Photoshop], [!DNL Adobe InDesign], [!DNL Adobe Illustrator], [!DNL Adobe XD], [!DNL Adobe Dimension]och [!DNL Adobe Acrobat] eller PDF.
* Nyckel [bildfilformat](#image-formats).
* [Camera Raw filformat](#camera-raw-formats) för ett stort antal kameror, inklusive Canon, Nikon, Fujifilm, Olympus och andra tillverkare (med Adobe Camera Raw som bas).
* Vanliga [dokumentformat](#document-formats), inklusive Microsoft Office och Open Document-format.
* Ett stort antal [video](#video-formats)- och [ljud](#audio-formats)-format.

I följande förklaring beskrivs stödnivån för varje format.

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

\* för [!DNL Adobe InDesign] filer (INDD) bestäms storleken på återgivningen av den förhandsgranskning som är inbäddad i INDD-filen. Konfigurera inställningarna i [!DNL InDesign] (**[!UICONTROL Preferences > File Handling > Always Save Preview Images with Documents, Preview Size]**) för att bädda in större återgivning.

## Bildformat {#image-formats}

| Filformat | Generering av miniatyrbilder | Extrahering av metadata | Bredd/höjd | Beskär |
| ----------- | -------------------- | ------------------- | ------------ | -------- |
| BMP | ✓ | - | ✓ | ✓ |
| EPS | ✓ | ✓ | - | - |
| GIF | ✓ | ✓ | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ |
| PNG | ✓ | ✓ | ✓ | ✓ |
| RGB | ✓ | ✓ | ✓ | ✓ |
| RGBA | ✓ | ✓ | ✓ | ✓ |
| SGI | ✓ | ✓ | ✓ | ✓ |
| SVG | ✓ | - | ✓ | ✓ |
| TIFF | ✓ | ✓ | ✓ | - |

## 3D-format {#support-3d-formats}

Följande 3D-format stöds.

Se även [Arbeta med 3D-resurser i Dynamic Media](/help/assets/dynamic-media/assets-3d.md).

| Format | Lagring | Versionshantering | Arbetsflöde | Publicering | Åtkomstkontroll | Förhandsvisning av miniatyrbilder | Förhandsgranska 3D | Leverans till Dynamic Media |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| DN | ✓ | ✓ | ✓ | - | ✓ | ✓ | - | - |
| gLB | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| gLTF | ✓ | ✓ | ✓ | - | ✓ | - | ✓ | - |
| OBJ | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| STL | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| USDz | ✓ | ✓ | ✓ | ✓ | ✓ | - | - | ✓ |

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
| DOC | - | - | - | ✓ | ✓ |
| DOCX | ✓ | ✓ | ✓ | ✓ | ✓ |
| ePub | - | ✓ | - | - | - |
| HTML | - | ✓ | - | ✓ | ✓ |
| ODF | ✓ | ✓ | ✓ | - | - |
| ODM | ✓ | ✓ | ✓ | - | - |
| ODP | ✓ | ✓ | ✓ | - | - |
| ODS | ✓ | ✓ | ✓ | - | - |
| ODT | ✓ | ✓ | ✓ | ✓ | ✓ |
| OFG | ✓ | ✓ | ✓ | - | - |
| PDF | ✓ | ✓ | ✓ | ✓ | ✓ |
| PPT | - | - | - | ✓ | ✓ |
| PPTX | ✓ | ✓ | ✓ | ✓ | ✓ |
| PS | - | - | ✓ | - | - |
| RTF | - | ✓ | - | ✓ | ✓ |
| TXT | ✓ | ✓ | - | ✓ | ✓ |
| XLS | - | - | - | ✓ | ✓ |
| XLSX | ✓ | ✓ | ✓ | ✓ | ✓ |
| XML | - | ✓ | - | - | - |

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
| MXF | ✓ | - | ✓ |
| OGV | ✓ | - | ✓ |
| QT | ✓ | - | ✓ |
| R3D | - | ✓ | ✓ |
| SWF | ✓ | - | ✓ |
| WebM | ✓ | - | ✓ |
| WMV | ✓ | ✓ | ✓ |

## Ljudformat {#audio-formats}

[!DNL Assets] som [!DNL Cloud Service] har stöd för XMP metadataextrahering för ljudformaten AIF, ASF, M4A, MP3, WAV och WMA.

## Indataformat som stöds för ljud- och videotranskription {#audio-video-transcription-formats}

* FLV (med H.264- och AAC-kodekar) (.flv)
* MXF (.mxf)
* MPEG2-PS, MPEG2-TS, 3GP (.ts, .ps, .3gp, .3gpp, .mpg)
* Windows Media Video (WMV)/ASF (.wmv, .asf)
* AVI (okomprimerad 8 bitar/10 bitar) (.avi)
* MP4 (.mp4, .m4a, .m4v)
* Microsoft Digital Video Recording (DVR-MS) (.dvr-ms)
* Matroska/WebM (.mkv)
* WAVE/WAV (.wav)
* QuickTime (.mov)

## Tips och begränsningar {#limitations-and-tips}

* För närvarande är filstorleksgränsen för metadataextrahering ungefär 15 GB. När mycket stora resurser överförs misslyckas ibland metadataextraheringen.

## Dynamic Media - Videoformat som stöds för transkodning {#video-dynamic-media-transcoding}

| Videofiltillägg | Behållare | Rekommenderade videokodekar | Videokodekar som inte stöds |
| --- | --- | --- | --- |
| AVI | A/V-sammanflätning | XVID, DIVX, HDV, MiniDV (DV25), Techsmith Camtasia, Huffyuv, Fraps, Panasonic DVCPro | Indeo3 (IV30), MJPEG, Microsoft Video 1 (MS-CRAM) |
| FLV, F4V | Adobe Flash | H264/AVC, Flix VP6, H263, Sorenson | SWF (vektoranimeringsfiler) |
| M4V | Apple iTunes | H264/AVC | - |
| MKV | Matroska | H264/AVC | - |
| MOV, QT | Apple QuickTime | H264/AVC, Apple ProRes422 &amp; HQ, Sony XDCAM, Sony DVCAM, HDV, Panasonic DVCPro, Apple DV (DV25), Apple PhotoJPEG, Sorenson, Avid DNxHD, Avid AVR | Apple Intermediate, Apple Animation |
| MP4 | MPEG-4 | H264/AVC (alla profiler) | - |
| MPG, VOB, M2V, MP2 | MPEG-2 | MPEG-2 | - |
| MXF ‡ | MXF | Sony XDCAM, MPEG-2, MPEG-4, Panasonic DVCPro | - |
| OGV, OGG | Ogg | Theora, VP3, Dirac | - |
| WebM | WebM | Google VP8 | - |
| WMV | Windows Media 9 | WMV3 (v9), WMV2 (v8), WMV1 (v7), GoToMeeting (G2M2, G2M3, G2M4) | Microsoft Screen (MSS2), Microsoft Photo Story (WVP2) |

‡ Det här videoformatet stöds ännu inte för interaktiva videoklipp i Dynamic Media eller för användning med anteckningar i Experience Manager Assets.

## Dynamic Media - dokumentformat som stöds {#document-support-dynamic-media}

| Format | Överför (indataformat) | Skapa bildförinställning (utdataformat) | Förhandsgranska dynamisk återgivning | Leverera dynamisk återgivning | Hämta dynamisk återgivning |
| ------ | --------------------- | ----------------------------------- | ------------------------- | ------------------------- | -------------------------- |
| AI | ✓ | - | - | - | - |
| INDD | ✓ | - | - | - | - |
| PDF (se anm. nedan) | ✓ | ✓ | ✓ | ✓ | ✓ |

>[!NOTE]
>
>För säker PDF stöds bara överföring.

## Dynamic Media - Rasterbildformat som stöds {#image-support-dynamic-media}

| Format | Överför (indataformat) | Skapa bildförinställning (utdataformat) | Förhandsgranska dynamisk återgivning | Leverera dynamisk återgivning | Hämta dynamisk återgivning | Ange typer som stöder det här formatet |
| ------- | --------------------- | ----------------------------------- | ------------------------- | ------------------------- | -------------------------- | ---------------------------------- |
| BMP | ✓ | - | - | - | - | [Bild](/help/assets/dynamic-media/image-sets.md), [Blandade media](/help/assets/dynamic-media/mixed-media-sets.md)och [Snurra](/help/assets/dynamic-media/spin-sets.md) |
| EPS | ✓ | ✓ | ✓ | ✓ | ✓ | - |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ | - |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ | [Bild](/help/assets/dynamic-media/image-sets.md), [Blandade media](/help/assets/dynamic-media/mixed-media-sets.md)och [Snurra](/help/assets/dynamic-media/spin-sets.md) |
| PICT | ✓ | - | - | - | - | - |
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ | [Bild](/help/assets/dynamic-media/image-sets.md), [Blandade media](/help/assets/dynamic-media/mixed-media-sets.md)och [Snurra](/help/assets/dynamic-media/spin-sets.md) |
| PSD ‡ | ✓ | - | - | - | - | - |
| TIFF | ✓ | ✓ | ✓ | ✓ | ✓ | [Bild](/help/assets/dynamic-media/image-sets.md), [Blandade media](/help/assets/dynamic-media/mixed-media-sets.md)och [Snurra](/help/assets/dynamic-media/spin-sets.md) |

‡ Den sammanfogade bilden extraheras från filen PSD. Det är en bild som genereras av [!DNL Adobe Photoshop] och ingår i filen PSD. Beroende på inställningarna kan den sammanfogade bilden vara den faktiska bilden eller inte.

## Dynamic Media - Rasterbildformat som inte stöds {#unsupported-raster-image-formats-dm}

Följande undertyper av rasterbildfilformat som är *not* stöds i [!DNL Dynamic Media]:

* PNG-filer som har en IDAT-segmentstorlek som är större än 100 MB.
* PSB-filer.
* PSD-filer med en annan färgmodell än CMYK, RGB, Gråskala eller Bitmapp stöds inte. Färgrymderna DuoTone, Lab och Indexed stöds inte.
* PSD-filer med ett bitdjup som är större än 16.
* TIFF-filer med flyttalsdata.
* TIFF-filer med Lab-färgrymd.

## Dynamic Media - 3D-filformat som stöds {#support-3d-formats-dynamic-media}

Se även [Stöd för 3D-format](/help/assets/file-format-support.md#support-3d-formats)

| 3D-filtillägg | Filformat | MIME-typ | Anteckningar |
|---|---|---|---|
| GLB | Binär GL-överföring | model/gltf-binary | Materialen och texturerna inkluderas som en enda resurs. |
| OBJ | WaveFront 3D-objektfil | application/x-tgif |  |
| STL | Stereolitografi | application/vnd.ms-pki.stl |  |
| USDZ | Zip-arkiv för universell scenbeskrivning | model/vnd.usdz+zip | *Stöd endast för förtäring. ingen visning eller interaktion är tillgänglig.* USDZ är ett tillverkarspecifikt 3D-format som kan visas direkt av Safari eller iOS. |

>[!MORELIKETHIS]
>
>* [Behandling av tillgångar med hjälp av mikrotjänster](asset-microservices-overview.md)
>* [Filformat som stöds för smart taggning av textbaserade resurser](/help/assets/smart-tags.md#smart-tags-supported-file-formats)


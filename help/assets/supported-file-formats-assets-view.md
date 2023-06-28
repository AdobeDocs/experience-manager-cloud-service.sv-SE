---
title: Filformat som stöds
description: Filformat som stöds för olika användningsområden för [!DNL Assets view]
role: User,Leader,Admin,Architect,Developer
contentOwner: AG
exl-id: bc44e98d-446e-41ff-b5b4-9dc324834630
source-git-commit: 6cb30ffda6c0de04e5cb3d01341b59c9ee75b335
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 1%

---

# Filformat stöds i [!DNL Assets view] {#file-format-support}

[!DNL Assets view] har stöd för ett stort antal filformat och alla funktioner har olika stöd för olika filtyper.

* ![ikon för bildfiltyp](assets/image-icon.svg) Bilder: JPG, PNG, GIF, TIFF med flera
* ![creative cloudType, ikon](assets/creative-cloud-files.svg) Creative Cloud-filer: PSD, AI och INDD
* ![ikon för kameratyp](assets/camera-icon.svg) Camera Raw filer: CR2/CR3, NEF, SRW/SRF med flera
* ![ikon för dokumentfiltyp](assets/document-icon.svg) Dokument: DOCX, PDF, PPTX och XLSX
* ![ikon för videofiltyp](assets/video-icon.svg) Videor: MP4

[!DNL Assets view] har stöd för alla binära filformat med grundläggande tjänster, som lagring, överföring, kopiering, flyttning, borttagning och tillägg av metadata.

[!DNL Assets view] har också stöd för Camera RAW-filer från ett stort antal ledande kameratillverkare, bland annat Canon (CR2/CR3), Nikon (NEF), Sony (SRW/SRF), Fujifilm (RAF), Olympus (ORF) och andra, som drivs av Adobe Camera Raw.

De olika filtyperna har olika typer av stöd för användningsfall och funktioner, vilket beskrivs nedan. Använd teckenförklaringen för att förstå supportnivån.

| Supportnivå | Beskrivning |
|-------------------|-------------------------|
| ✓ | Stöds |
| ✓ ‡ | Stöds villkorligt |
| − | Ej tillämpligt |

## Lägga till, överföra och visa resurser {#support-to-upload-view}

<!-- TBD: For AEM, AI files require the PDF option to be selected when saving the AI file.
-->

| Tillgångstyp | [Bläddra](/help/assets/navigate-assets-view.md) | Kopiera | [Överför](/help/assets/add-delete-assets-view.md) | Skapa | [Ta bort](/help/assets/add-delete-assets-view.md#delete-assets) | Detaljer | Zooma bilden | [Senast visade](/help/assets/navigate-assets-view.md) |
|-------------------|----------|----------|----------|----------|----------|-------------------|------------|-----------------|
| Rasterbilder | ✓ | ✓ | ✓ | − | ✓ | ✓ | ✓ | ✓ |
| RAW-filer | ✓ | ✓ | ✓ | − | ✓ | ✓ | ✓ | ✓ |
| Mappar | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | − | − |
| MP4-videor | ✓ | ✓ | ✓ | − | ✓ | ✓ ‡ | − | ✓ |
| PDF | ✓ | ✓ | ✓ | − | ✓ | ✓ | − | ✓ |
| PSD, AI och INDD | ✓ | ✓ | ✓ | − | ✓ | ✓ ‡ | − | ✓ |
| Andra binära filer | ✓ | ✓ | ✓ | − | ✓ | ✓ | − | ✓ |

<!-- Hiding CC Libraries (considered beta) as per PM feedback.
| CC Libraries  | &#10003; | &minus;  | &#10003; | &#10003; | &#10003; | &#10003; | &minus;    | &minus;         |
-->

## Söka efter, använda och redigera resurser {#support-to-search-use-edit}

| Tillgångstyp | [Hämta](/help/assets/manage-organize-assets-view.md#download) | Dra och släpp | [Bildredigerare](/help/assets/edit-images-assets-view.md) | [Sökning](/help/assets/search-assets-view.md) | [Smarta taggar](/help/assets/metadata-assets-view.md#tags) | [Byt namn](/help/assets/manage-organize-assets-view.md) | [Versioner](/help/assets/manage-organize-assets-view.md#versions-of-assets) |
|---------------|----------|---------------|--------------|----------|------------|----------|----------|
| Rasterbilder | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| RAW-filer | ✓ | ✓ | − | ✓ | ✓ | ✓ | ✓ | ✓ |
| Mappar | ✓ | ✓ | − | ✓ | − | ✓ | ✓ |
| Videor | ✓ | ✓ | − | ✓ | ✓ | ✓ | ✓ |
| CC Libraries | − | − | − | − | − | ✓ | ✓ |
| PDF | ✓ | ✓ | − | ✓ | ✓ | ✓ | ✓ |
| PSD | ✓ | ✓ | − | ✓ | ✓ | ✓ | ✓ |
| AI och INDD | ✓ | ✓ | − | ✓ | − | ✓ | ✓ |
| Andra binära filer | ✓ | ✓ | − | ✓ | − | ✓ | ✓ |


## Granska resurser och samarbeta {#support-to-review-collaborate}

| Tillgångstyp | Anteckna | Kommentar | Skapa uppgifter och granska |
|---------------|----------|----------|-------------------------|
| Rasterbilder | ✓ | ✓ | ✓ |
| RAW-filer | ✓ | ✓ | ✓ |
| Mappar | − | − | − |
| Videor | − | ✓ | ✓ |
| CC Libraries | − | − | − |
| PDF | − | ✓ | ✓ |
| PSD, AI och INDD | − | ✓ | ✓ |
| Andra binära filer | − | ✓ | ✓ |
| DOC | − | ✓ | ✓ |
| DOCX | − | ✓ | ✓ |
| PPT | − | ✓ | ✓ |
| PPTX | − | ✓ | ✓ |
| XLS | − | ✓ | ✓ |
| XLSX | − | ✓ | ✓ |
| TXT | − | ✓ | ✓ |
| RTF | − | ✓ | ✓ |

## Andra resurshanteringsåtgärder {#support-to-manage-assets}

| Tillgångstyp | [Metadata](/help/assets/metadata-assets-view.md) | [Återgivningar](/help/assets/add-delete-assets-view.md#renditions) | [Papperskorgen](/help/assets/add-delete-assets-view.md#delete-assets) | Kopiera | Flytta |
|---------------|-------------------|------------|----------|----------|----------|
| Rasterbilder | ✓ | ✓ | ✓ | ✓ | ✓ |
| RAW-filer | ✓ | ✓ | ✓ | ✓ | ✓ |
| Mappar | ✓ | − | ✓ | ✓ | ✓ |
| Videor | ✓ | − | ✓ | ✓ | ✓ |
| CC Libraries | ✓ | − | − | − | − |
| PDF | ✓ | − | ✓ | ✓ | ✓ |
| PSD, AI och INDD | ✓ | − | ✓ | ✓ | ✓ |
| Andra binära filer | ✓ | − | ✓ | ✓ | ✓ |

Användare av [!DNL Adobe Asset Link] kan överföra och checka in (överföra en ny version) filer till [!DNL Assets view] databas från den databas som stöds [!DNL Adobe Creative Cloud] datorprogram.

<!-- TBD: Saving the template table separately for later use.
| Asset type    | Features |
|---------------|----------|
| Raster images |          |
| Folders       |          |
| Videos        |          |
| CC Libraries  |          |
| PDF files     |          |
| PSD           |          |
| AI            |          |
| INDD          |          |

>[!MORELIKETHIS]
>
>* []()
-->

## Nästa steg {#next-steps}

* Ge produktfeedback med [!UICONTROL Feedback] alternativ som finns i användargränssnittet i resursvyn

* Ge feedback på dokumentationen med [!UICONTROL Edit this page] ![redigera sidan](assets/do-not-localize/edit-page.png) eller [!UICONTROL Log an issue] ![skapa ett GitHub-problem](assets/do-not-localize/github-issue.png) som finns till höger

* Kontakt [Kundtjänst](https://experienceleague.adobe.com/?support-solution=General#support)

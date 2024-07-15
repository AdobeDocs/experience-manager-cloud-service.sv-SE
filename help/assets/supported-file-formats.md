---
title: Filformat som stöds
description: Filformat som stöds för olika användningsområden för  [!DNL Assets View]
role: User,Leader,Admin,Architect,Developer
contentOwner: AG
exl-id: bc44e98d-446e-41ff-b5b4-9dc324834630
source-git-commit: b4b397a09960f507df1daa0cf6f5dc49d6b286c6
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 0%

---

# Filformat stöds i [!DNL Assets View] {#file-format-support}

[!DNL Assets View] har stöd för ett stort antal filformat och alla funktioner har olika stöd för olika filtyper.

* ![ikon för bildfiltyp](assets/image-icon.svg) Bilder: JPG, PNG, GIF, TIFF och andra
* ![creative cloudType, ikon](assets/creative-cloud-files.svg) Creative Cloud filer: PSD, AI och INDD
* ![kameratypsikon](assets/camera-icon.svg) Camera Raw filer: CR2/CR3, NEF, SRW/SRF med flera
* ![ikon för dokumentfiltyp](assets/document-icon.svg) Dokument: DOCX, PDF, PPTX och XLSX
* ![ikon för videofiltyp](assets/video-icon.svg) Videoklipp: MP4

[!DNL Assets View] har stöd för alla binära filformat med grundläggande tjänster, som lagring, överföring, kopiering, flyttning, borttagning och tillägg av metadata.

[!DNL Assets View] har också stöd för Camera RAW-filer från ett stort antal ledande kameratillverkare, bland annat Canon (CR2/CR3), Nikon (NEF), Sony (SRW/SRF), Fujifilm (RAF), Olympus (ORF) och andra, som drivs av Adobe Camera Raw.

De olika filtyperna har olika typer av stöd för användningsfall och funktioner, vilket beskrivs nedan. Använd teckenförklaringen för att förstå supportnivån.

| Supportnivå | Beskrivning |
|-------------------|-------------------------|
| ✓ | Stöds |
| ✓ ‡ | Stöds villkorligt |
| - | Ej tillämpligt |

## Lägga till, överföra och visa resurser {#support-to-upload-view}

<!-- TBD: For AEM, AI files require the PDF option to be selected when saving the AI file.
-->

| Tillgångstyp | [Bläddra](/help/assets/navigate-view.md) | Kopiera | [Överför](/help/assets/add-delete.md) | Skapa | [Ta bort](/help/assets/add-delete.md#delete-assets) | Information | Zooma bilden | [Senast visade](/help/assets/navigate-view.md) |
|-------------------|----------|----------|----------|----------|----------|-------------------|------------|-----------------|
| Rasterbilder | ✓ | ✓ | ✓ | - | ✓ | ✓ | ✓ | ✓ |
| RAW-filer | ✓ | ✓ | ✓ | - | ✓ | ✓ | ✓ | ✓ |
| Mappar | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | - | - |
| MP4-videor | ✓ | ✓ | ✓ | - | ✓ | ✓ ‡ | - | ✓ |
| PDF | ✓ | ✓ | ✓ | - | ✓ | ✓ | - | ✓ |
| PSD, AI och INDD | ✓ | ✓ | ✓ | - | ✓ | ✓ ‡ | - | ✓ |
| Andra binära filer | ✓ | ✓ | ✓ | - | ✓ | ✓ | - | ✓ |

<!-- Hiding CC Libraries (considered beta) as per PM feedback.
| CC Libraries  | &#10003; | &minus;  | &#10003; | &#10003; | &#10003; | &#10003; | &minus;    | &minus;         |
-->

## Söka efter, använda och redigera resurser {#support-to-search-use-edit}

| Tillgångstyp | [Hämta](/help/assets/manage-organize.md#download) | Dra och släpp | [Bildredigeraren](/help/assets/edit-images.md) | [Sökning](/help/assets/search.md) | [Smarta taggar](/help/assets/metadata.md#tags) | [Byt namn](/help/assets/manage-organize.md) | [Versioner](/help/assets/manage-organize.md#versions-of-assets) |
|---------------|----------|---------------|--------------|----------|------------|----------|----------|
| Rasterbilder | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| RAW-filer | ✓ | ✓ | - | ✓ | ✓ | ✓ | ✓ | ✓ |
| Mappar | ✓ | ✓ | - | ✓ | - | ✓ | ✓ |
| Videor | ✓ | ✓ | - | ✓ | ✓ | ✓ | ✓ |
| CC Libraries | - | - | - | - | - | ✓ | ✓ |
| PDF | ✓ | ✓ | - | ✓ | ✓ | ✓ | ✓ |
| PSD | ✓ | ✓ | - | ✓ | ✓ | ✓ | ✓ |
| AI och INDD | ✓ | ✓ | - | ✓ | - | ✓ | ✓ |
| Andra binära filer | ✓ | ✓ | - | ✓ | - | ✓ | ✓ |


## Granska resurser och samarbeta {#support-to-review-collaborate}

| Tillgångstyp | Anteckna | Kommentar | Skapa uppgifter och granska |
|---------------|----------|----------|-------------------------|
| Rasterbilder | ✓ | ✓ | ✓ |
| RAW-filer | ✓ | ✓ | ✓ |
| Mappar | - | - | - |
| Videor | - | ✓ | ✓ |
| CC Libraries | - | - | - |
| PDF | - | ✓ | ✓ |
| PSD, AI och INDD | - | ✓ | ✓ |
| Andra binära filer | - | ✓ | ✓ |
| DOC | - | ✓ | ✓ |
| DOCX | - | ✓ | ✓ |
| PPT | - | ✓ | ✓ |
| PPTX | - | ✓ | ✓ |
| XLS | - | ✓ | ✓ |
| XSX | - | ✓ | ✓ |
| TXT | - | ✓ | ✓ |
| RTF | - | ✓ | ✓ |

## Andra resurshanteringsåtgärder {#support-to-manage-assets}

| Tillgångstyp | [Metadata](/help/assets/metadata.md) | [Återgivningar](/help/assets/add-delete.md#renditions) | [Papperskorgen](/help/assets/add-delete.md#delete-assets) | Kopiera | Flytta |
|---------------|-------------------|------------|----------|----------|----------|
| Rasterbilder | ✓ | ✓ | ✓ | ✓ | ✓ |
| RAW-filer | ✓ | ✓ | ✓ | ✓ | ✓ |
| Mappar | ✓ | - | ✓ | ✓ | ✓ |
| Videor | ✓ | - | ✓ | ✓ | ✓ |
| CC Libraries | ✓ | - | - | - | - |
| PDF | ✓ | - | ✓ | ✓ | ✓ |
| PSD, AI och INDD | ✓ | - | ✓ | ✓ | ✓ |
| Andra binära filer | ✓ | - | ✓ | ✓ | ✓ |

Användare av [!DNL Adobe Asset Link] kan överföra och checka in (överföra en ny version) filer till databasen [!DNL Assets View] från de [!DNL Adobe Creative Cloud] skrivbordsprogram som stöds.

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

* Ge produktfeedback med alternativet [!UICONTROL Feedback] som finns i användargränssnittet i Assets View

* Ge feedback om dokumentationen med [!UICONTROL Edit this page] ![redigera sidan](assets/do-not-localize/edit-page.png) eller [!UICONTROL Log an issue] ![skapa ett GitHub-problem](assets/do-not-localize/github-issue.png) som är tillgängligt på den högra sidopanelen

* Kontakta [kundtjänst](https://experienceleague.adobe.com/?support-solution=General#support)

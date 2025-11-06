---
title: Filformat som stöds
description: Filformat som stöds för olika användningsområden för  [!DNL Assets view]
role: User, Leader, Admin, Developer
contentOwner: AG
exl-id: 5936ace2-318e-4888-9ad4-23e6f6bfb857
feature: Asset Management, Publishing, Collaboration, Asset Processing
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 0%

---

# Filformat stöds i [!DNL Assets view] {#file-format-support}

[!DNL Assets view] har stöd för ett stort antal filformat och alla funktioner har olika stöd för olika filtyper.

* ![ikon för bildfiltyp](assets/image-icon.svg) Bilder: JPG, PNG, GIF, TIFF med flera
* ![ikon för kreativ molntyp](assets/creative-cloud-files.svg) Creative Cloud-filer: PSD, PSB, AI och INDD
* ![kameratypsikon](assets/camera-icon.svg) Camera Raw-filer: CR2/CR3, NEF, SRW/SRF med flera
* ![ikon för dokumentfiltyp](assets/document-icon.svg) Dokument: DOCX, PDF, PPTX och XLSX
* ![ikon för videofiltyp](assets/video-icon.svg) Videoklipp: MP4

[!DNL Assets view] har stöd för alla binära filformat med grundläggande tjänster, som lagring, överföring, kopiering, flyttning, borttagning och tillägg av metadata.

[!DNL Assets view] har också stöd för Camera RAW-filer från ett stort antal ledande kameratillverkare, bland annat Canon (CR2/CR3), Nikon (NEF), Sony (SRW/SRF), Fujifilm (RAF), Olympus (ORF) och andra, som drivs av Adobe Camera Raw.

De olika filtyperna har olika typer av stöd för användningsfall och funktioner, vilket beskrivs nedan. Använd teckenförklaringen för att förstå supportnivån.

| Supportnivå | Beskrivning |
|-------------------|-------------------------|
| ✓ | Stöds |
| ✓ ‡ | Stöds villkorligt |
| - | Ej tillämpligt |

## Lägga till, överföra och visa resurser {#support-to-upload-view}

<!-- TBD: For AEM, AI files require the PDF option to be selected when saving the AI file.
-->

| Tillgångstyp | [Bläddra](/help/assets/navigate-assets-view.md) | Kopiera | [Överför](/help/assets/add-delete-assets-view.md) | Skapa | [Ta bort](/help/assets/add-delete-assets-view.md#delete-assets) | Information | Zooma bilden | [Senast visade](/help/assets/navigate-assets-view.md) |
|-------------------|----------|----------|----------|----------|----------|-------------------|------------|-----------------|
| Rasterbilder | ✓ | ✓ | ✓ | - | ✓ | ✓ | ✓ | ✓ |
| RAW-filer | ✓ | ✓ | ✓ | - | ✓ | ✓ | ✓ | ✓ |
| Mappar | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | - | - |
| MP4-videor | ✓ | ✓ | ✓ | - | ✓ | ✓ ‡ | - | ✓ |
| PDF | ✓ | ✓ | ✓ | - | ✓ | ✓ | - | ✓ |
| PSD, PSB, AI och INDD | ✓ | ✓ | ✓ | - | ✓ | ✓ ‡ | - | ✓ |
| Andra binära filer | ✓ | ✓ | ✓ | - | ✓ | ✓ | - | ✓ |

<!-- Hiding CC Libraries (considered beta) as per PM feedback.
| CC Libraries  | &#10003; | &minus;  | &#10003; | &#10003; | &#10003; | &#10003; | &minus;    | &minus;         |
-->

## Söka efter, använda och redigera resurser {#support-to-search-use-edit}

| Tillgångstyp | [Hämta](/help/assets/manage-organize-assets-view.md#download) | Dra och släpp | [Bildredigeraren](/help/assets/edit-images-assets-view.md) | [Sökning](/help/assets/search-assets-view.md) | [Smarta taggar](/help/assets/metadata-assets-view.md#tags) | [Byt namn](/help/assets/manage-organize-assets-view.md) | [Versioner](/help/assets/manage-organize-assets-view.md#versions-of-assets) |
|---------------|----------|---------------|--------------|----------|------------|----------|----------|
| Rasterbilder | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| RAW-filer | ✓ | ✓ | - | ✓ | ✓ | ✓ | ✓ | ✓ |
| Mappar | ✓ | ✓ | - | ✓ | - | ✓ | ✓ |
| Videor | ✓ | ✓ | - | ✓ | ✓ | ✓ | ✓ |
| CC Libraries | - | - | - | - | - | ✓ | ✓ |
| PDF | ✓ | ✓ | - | ✓ | ✓ | ✓ | ✓ |
| PSD och PSB | ✓ | ✓ | - | ✓ | ✓ | ✓ | ✓ |
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
| PSD, PSB, AI och INDD | - | ✓ | ✓ |
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

| Tillgångstyp | [Metadata](/help/assets/metadata-assets-view.md) | [Återgivningar](/help/assets/add-delete-assets-view.md#renditions) | [Papperskorgen](/help/assets/add-delete-assets-view.md#delete-assets) | Kopiera | Flytta |
|---------------|-------------------|------------|----------|----------|----------|
| Rasterbilder | ✓ | ✓ | ✓ | ✓ | ✓ |
| RAW-filer | ✓ | ✓ | ✓ | ✓ | ✓ |
| Mappar | ✓ | - | ✓ | ✓ | ✓ |
| Videor | ✓ | - | ✓ | ✓ | ✓ |
| CC Libraries | ✓ | - | - | - | - |
| PDF | ✓ | - | ✓ | ✓ | ✓ |
| AI och INDD | ✓ | - | ✓ | ✓ | ✓ |
| PSD och PSB | ✓ | ✓ | ✓ | ✓ | ✓ |
| Andra binära filer | ✓ | - | ✓ | ✓ | ✓ |

Användare av [!DNL Adobe Asset Link] kan överföra och checka in (överföra en ny version) filer till databasen [!DNL Assets view] från de [!DNL Adobe Creative Cloud] skrivbordsprogram som stöds.

<!-- TBD: Saving the template table separately for later use.
| Asset type    | Features |
|---------------|----------|
| Raster images |          |
| Folders       |          |
| Videos        |          |
| CC Libraries  |          |
| PDF files     |          |
| PSD, PSB           |          |
| AI            |          |
| INDD          |          |

>[!MORELIKETHIS]
>
>* []()
-->

## Nästa steg {#next-steps}

* Ge produktfeedback med alternativet [!UICONTROL Feedback] som finns i användargränssnittet i Assets-vyn

* Ge feedback om dokumentationen med [!UICONTROL Edit this page] ![redigera sidan](assets/do-not-localize/edit-page.png) eller [!UICONTROL Log an issue] ![skapa ett GitHub-problem](assets/do-not-localize/github-issue.png) som är tillgängligt på den högra sidopanelen

* Kontakta [kundtjänst](https://experienceleague.adobe.com/sv?support-solution=General#support)

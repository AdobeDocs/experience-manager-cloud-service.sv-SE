---
title: Hantera rapporter i Assets-vyn
description: Använd uppgifterna i rapportavsnittet i Assets-vyn för att utvärdera produkt- och funktionsanvändning och få insikter om viktiga framgångsmått.
exl-id: 26d0289e-445a-4b8e-a5a1-b02beedbc3f1
feature: Asset Insights, Asset Reports
role: User, Admin, Developer
source-git-commit: e3fd0fe2ee5bad2863812ede2a294dd63864f3e2
workflow-type: tm+mt
source-wordcount: '800'
ht-degree: 1%

---

# Hantera rapporter {#manage-reports}

| [Sök efter bästa praxis](/help/assets/search-best-practices.md) | [Metadata - bästa praxis](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [Dynamic Media med OpenAPI-funktioner](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets-dokumentation för utvecklare](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

Med tillgångsrapportering kan administratörer se vilka aktiviteter Adobe Experience Manager Assets View-miljön har. Dessa data ger användbar information om hur användarna interagerar med innehållet och produkten. Alla användare har tillgång till Insikter-kontrollpanelen och de som har tilldelats administratörens produktprofil kan skapa användardefinierade rapporter.

## Åtkomstrapporter {#access-reports}

Alla användare som har tilldelats produktprofilen för Assets-vyadministratörer kan komma åt Insikter-instrumentpanelen eller skapa användardefinierade rapporter i Assets-vyn.

Navigera till **[!UICONTROL Reports]** under **[!UICONTROL Settings]** för att få åtkomst till rapporter.

![Rapporter](assets/reports.png)
<!--
In the **[!UICONTROL Reports]** screen, various components are shown in the tabular format which includes the following:

* **Title**: Title of the report
* **Type**: Determines whether the report is uploaded or downloaded to the repository
* **Description**: Provide details of the report that was given during uploading/downloading the report
* **Status**: Determines whether the report is completed, under progress, or deleted.
* **Author**: Provides email of the author who has uploaded/downloaded the report.
* **Created**: Gives information of the date when the report was generated.
-->

## Visa insikter {#view-live-statistics}

I Assets-vyn kan du visa realtidsdata för din Assets-visningsmiljö med Insikter-kontrollpanelen. Du kan visa händelsemått i realtid under de senaste 30 dagarna eller under de senaste 12 månaderna.

<!--![Toolbar options when you select an asset](assets/assets-essentials-live-statistics.png)-->

Klicka på **[!UICONTROL Insights]** i den vänstra navigeringsrutan för att visa följande automatiskt genererade diagram:

* **Hämtningar**: Antalet resurser som hämtats från Assets-visningsmiljön under de senaste 30 dagarna eller 12 månaderna representeras av ett linjediagram.
  ![insights-downloads](/help/assets/assets/insights-downloads2341.svg)

* **Överföringar**: Antalet resurser som har överförts till visningsmiljön i Assets under de senaste 30 dagarna eller 12 månaderna representeras av ett linjediagram.
  ![insights-uploads](/help/assets/assets/insights-uplods2.svg)
  <!--* **Asset Count by Size**: The division of count of assets based on their range of various sizes from 0 MB to 100 GB.-->

* **Lagringsanvändning**: Lagringsanvändningen (i byte) för visningsmiljön i Assets representeras av ett stapeldiagram.
  ![insights-uploads](/help/assets/assets/insights-storage-usage1.svg)
  <!--* **Delivery**: The graph depicts the count of assets as the delivery dates.-->

<!--* **Asset Count by Asset Type**: Represents count of various MIME types of the available assets. For example, application/zip, image/png, video/mp4, application/postscripte.-->

* **Vanliga sökningar**: Visa de mest sökta söktermerna tillsammans med det antal gånger som de sökts igenom i Assets-visningsmiljön under de senaste 30 dagarna eller 12 månaderna, representerade i ett tabellformat.
  ![insights-uploads](/help/assets/assets/insights-top-search.svg)
  <!--
   ![Insights](assets/insights1.png)
   ![Insights](assets/insights2.png)
   -->

## Skapa en nedladdningsrapport {#create-download-report}

Så här skapar du en hämtningsrapport:

1. Navigera till **[!UICONTROL Settings]** > **[!UICONTROL Reports]** och klicka på **[!UICONTROL Create Report]**.

1. Ange rapporttypen **[!UICONTROL Download]** på fliken [!UICONTROL Configuration].

1. Ange en rubrik och en valfri beskrivning för rapporten.

1. Välj mappsökvägen, som omfattar de resurser som rapporten ska köras på, med hjälp av fältet **[!UICONTROL Select Folder Path]**.

1. Välj datumintervall för rapporten.

   >[!NOTE]
   >
   > I Assets-vyn konverteras alla lokala tidszoner till UTC (Coordinated Universal Time).

1. På fliken [!UICONTROL Columns] markerar du de kolumnnamn som du vill visa i rapporten.

1. Klicka på **[!UICONTROL Create]**.

   ![Hämta rapport](assets/download-reports-config.png)

I följande tabell förklaras användningen av alla kolumner som du kan lägga till i rapporten:

<table>
    <tbody>
     <tr>
      <th><strong>Kolumnnamn</strong></th>
      <th><strong>Beskrivning</strong></th>
     </tr>
     <tr>
      <td>Titel</td>
      <td>Namnet på resursen.</td>
     </tr>
     <tr>
      <td>Bana</td>
      <td>Mappsökvägen där resursen är tillgänglig i Assets-vyn.</td>
     </tr>
     <tr>
      <td>MIME-typ</td>
      <td>MIME-typen för resursen.</td>
     </tr>
     <tr>
      <td>Storlek</td>
      <td>Resursens storlek i byte.</td>
     </tr>
     <tr>
      <td>Hämtat av</td>
      <td>E-post-ID för den användare som hämtade resursen.</td>
     </tr>
     <tr>
      <td>Hämtningsdatum</td>
      <td>Datumet då hämtningsåtgärden för resursen utförs.</td>
     </tr>
     <tr>
      <td>Författare</td>
      <td>Resursens författare.</td>
     </tr>
     <tr>
      <td>Skapad den</td>
      <td>Det datum då resursen överförs till Assets-vyn.</td>
     </tr>
     <tr>
      <td>Ändringsdatum</td>
      <td>Datumet då tillgången senast ändrades.</td>
     </tr>
     <tr>
      <td>Utgånget</td>
      <td>Tillgångens förfallostatus.</td>
     </tr>
     <tr>
      <td>Hämtat efter användarnamn</td>
      <td>Namnet på den användare som hämtade resursen.</td>
     </tr>           
    </tbody>
   </table>

## Skapa en överföringsrapport {#create-upload-report}

Så här skapar du en överföringsrapport:

1. Navigera till **[!UICONTROL Settings]** > **[!UICONTROL Reports]** och klicka på **[!UICONTROL Create Report]**.

1. Ange rapporttypen **[!UICONTROL Upload]** på fliken [!UICONTROL Configuration].

1. Ange en rubrik och en valfri beskrivning för rapporten.

1. Välj mappsökvägen, som omfattar de resurser som rapporten ska köras på, med hjälp av fältet **[!UICONTROL Select Folder Path]**.

1. Välj datumintervall för rapporten.

1. På fliken [!UICONTROL Columns] markerar du de kolumnnamn som du vill visa i rapporten.

1. Klicka på **[!UICONTROL Create]**.

   ![Överför rapport](assets/upload-reports-config.png)

I följande tabell förklaras användningen av alla kolumner som du kan lägga till i rapporten:

<table>
    <tbody>
     <tr>
      <th><strong>Kolumnnamn</strong></th>
      <th><strong>Beskrivning</strong></th>
     </tr>
     <tr>
      <td>Titel</td>
      <td>Namnet på resursen.</td>
     </tr>
     <tr>
      <td>Bana</td>
      <td>Mappsökvägen där resursen är tillgänglig i Assets-vyn.</td>
     </tr>
     <tr>
      <td>MIME-typ</td>
      <td>MIME-typen för resursen.</td>
     </tr>
     <tr>
      <td>Storlek</td>
      <td>Resursens storlek.</td>
     </tr>
     <tr>
      <td>Författare</td>
      <td>Resursens författare.</td>
     </tr>
     <tr>
      <td>Skapad den</td>
      <td>Det datum då resursen överförs till Assets-vyn.</td>
     </tr>
     <tr>
      <td>Ändringsdatum</td>
      <td>Datumet då tillgången senast ändrades.</td>
     </tr>
     <tr>
      <td>Utgånget</td>
      <td>Tillgångens förfallostatus.</td>
     </tr>              
    </tbody>
   </table>

## Visa befintliga rapporter {#view-report-list}

När du har [skapat rapporten](#create-download-report) kan du visa listan över befintliga rapporter och välja att hämta dem i ett CSV-format eller ta bort dem.

Navigera till **[!UICONTROL Settings]** > **[!UICONTROL Reports]** om du vill visa listan med rapporter.

För varje rapport kan du visa rapportrubrik, rapporttyp, beskrivning som anges när rapporten skapas, rapportens status, e-post-ID för den som skapade rapporten och rapportens skapandedatum.

`Completed `-status för rapporten visar att rapporten är klar för hämtning.

![Lista över rapporter](assets/list-of-reports.png)


## Hämta en CSV-rapport {#download-csv-report}

Så här hämtar du en rapport i CSV-format:

1. Navigera till **[!UICONTROL Settings]** > **[!UICONTROL Reports]**.

1. Välj en rapport och klicka på **[!UICONTROL Download CSV]**.

Den valda rapporten hämtas i CSV-format. Kolumnerna som visas i CSV-rapporten beror på vilka kolumner du markerar när du [skapar rapporten](#create-download-report).

## Ta bort en rapport {#delete-report}

Ta bort en rapport:

1. Navigera till **[!UICONTROL Settings]** > **[!UICONTROL Reports]**.

1. Välj en rapport och klicka på **[!UICONTROL Delete]**.

1. Bekräfta genom att klicka på **[!UICONTROL Delete]** igen.

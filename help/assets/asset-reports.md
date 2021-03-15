---
title: Rapporter om användning och delning
description: Rapporterar om dina resurser i [!DNL Adobe Experience Manager Assets] som hjälper dig att förstå användningen, aktiviteten och delningen av dina digitala resurser.
contentOwner: AG
translation-type: tm+mt
source-git-commit: dc6823d9a0dabcc4fe1537073d90ca53da205556
workflow-type: tm+mt
source-wordcount: '820'
ht-degree: 6%

---


# Materialrapporter {#asset-reports}

Med tillgångsrapportering kan du utvärdera verktyget för din [!DNL Adobe Experience Manager Assets]-distribution. Med [!DNL Assets] kan du generera olika rapporter för dina digitala resurser. Rapporterna innehåller användbar information om hur ditt system används, hur användarna interagerar med resurser och vilka resurser som delas med <!-- downloaded and -->.

Använd informationen i rapporterna för att ta fram nyckeltal för att mäta hur [!DNL Assets] används i ert företag och av era kunder.

I [!DNL Assets]-rapporteringsramverket används [!DNL Sling]-jobb för att asynkront bearbeta rapportbegäranden på ett ordnat sätt. Den kan skalas för stora databaser. Asynkron rapportbearbetning ökar effektiviteten och hastigheten med vilken rapporter genereras.

Rapporthanteringsgränssnittet är intuitivt och innehåller detaljerade alternativ och kontroller för att komma åt arkiverade rapporter och visa rapportkörningsstatus (lyckad, misslyckad och köad).

När en rapport skapas meddelas du via <!-- through an email (optional) and --> ett inkorgsmeddelande. Du kan visa, hämta eller ta bort en rapport från rapportlistsidan, där alla tidigare genererade rapporter visas.

## Generera rapporter {#generate-reports}

[!DNL Experience Manager Assets] genererar följande standardrapporter:

* Överför
* Förfaller
* Ändring
* Publicera
* [!DNL Brand Portal] publicera
* Diskanvändning
* Filer
* Länkdelning

<!-- Removed download report.
* Upload
* Download
* Expiration
* Modification
* Publish
* [!DNL Brand Portal] publish
* Disk Usage
* Files
* Link Share
-->

[!DNL Adobe Experience Manager] administratörer kan enkelt generera och anpassa dessa rapporter för din implementering. Administratören kan följa de här stegen för att skapa en rapport:

1. I [!DNL Experience Manager]-gränssnittet klickar du på **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Reports]**.

   ![Verktygssida för att navigera bland resurser - rapport](assets/navigation.png)

1. På sidan [!UICONTROL Asset Reports] klickar du på **[!UICONTROL Create]** i verktygsfältet.
1. Välj den rapport du vill skapa på sidan **[!UICONTROL Create Report]** och klicka på **[!UICONTROL Next]**.

   ![Välj rapporttyp](assets/choose_report.png)

1. Konfigurera rapportinformation som titel, beskrivning, miniatyrbild och mappsökväg i CRX-databasen där rapporten lagras. Som standard är mappsökvägen `/content/dam`. Du kan ange en annan sökväg.

   ![Sida för att lägga till rapportinformation](assets/report_configuration.png)

   Välj datumintervall för rapporten. Du kan välja att generera rapporten nu eller vid ett framtida datum och tid.

   >[!NOTE]
   >
   >Om du väljer att schemalägga rapporten senare måste du ange datum och tid i fälten Datum och Tid. Om du inte anger något värde behandlas det som en rapport som ska genereras omedelbart.

   Konfigurationsfälten kan variera beroende på vilken typ av rapport du skapar. Rapporten **[!UICONTROL Disk Usage]** innehåller till exempel alternativ för att inkludera resursåtergivningar när du beräknar det diskutrymme som används av resurserna. Du kan välja att inkludera eller exkludera resurser i undermappar för beräkning av diskanvändning.

   >[!NOTE]
   >
   >Rapporten **[!UICONTROL Disk Usage]** innehåller inga fält för datumintervall eftersom den endast visar hur mycket diskutrymme som används.

   ![Sidan Information om rapporten Diskanvändning](assets/disk_usage_configuration.png)

   När du skapar **[!UICONTROL Files]**-rapporten kan du inkludera/exkludera undermappar. Du kan dock inte inkludera resursåtergivningar för den här rapporten.

   ![Detaljsida för rapporten Filer](assets/files_report.png)

   I rapporten **[!UICONTROL Link Share]** visas URL:er till resurser som delas med externa användare inifrån [!DNL Assets]. <!-- It includes email ids of the user who shared the assets, emails ids of users with which the assets are shared, share date, and expiration date for the link. --> Det går inte att anpassa kolumnerna.

   **[!UICONTROL Link Share]**-rapporten innehåller inga alternativ för undermappar och återgivningar eftersom den bara publicerar de delade URL:er som visas under `/var/dam/share`.

   ![Detaljsida för länkdelningsrapport](assets/link_share.png)

1. Klicka på **[!UICONTROL Next]** i verktygsfältet.

1. På sidan **[!UICONTROL Configure Columns]** är vissa kolumner markerade för att visas i rapporten som standard. Du kan markera fler kolumner. Avbryt valet av en kolumn för att utesluta den i rapporten.

   ![Markera eller avbryta markering av rapportkolumner](assets/configure_columns.png)

   Om du vill visa ett anpassat kolumnnamn eller en egenskapssökväg konfigurerar du egenskaperna för resursens binärfil under noden `jcr:content` i CRX. Du kan också lägga till den via egenskapssökvägsväljaren.

   ![Markera eller avbryta markering av rapportkolumner](assets/custom_columns.png)

1. Klicka på **[!UICONTROL Create]** i verktygsfältet. Ett meddelande meddelar att rapportgenereringen har initierats.
1. På sidan [!UICONTROL Asset Reports] baseras rapportgenereringsstatusen på rapportjobbets aktuella tillstånd, till exempel [!UICONTROL Success], [!UICONTROL Failed], [!UICONTROL Queued] eller [!UICONTROL Scheduled]. Samma status visas i inkorgen för meddelanden.Om du vill visa rapportsidan klickar du på rapportlänken. Du kan också markera rapporten och klicka på **[!UICONTROL View]** i verktygsfältet.

   ![En genererad rapport](assets/report_page.png)

   Klicka på **[!UICONTROL Download]** i verktygsfältet för att hämta rapporten i CSV-format.

## Lägg till anpassade kolumner i rapporter {#add-custom-columns}

Du kan lägga till anpassade kolumner i följande rapporter om du vill visa mer data för dina anpassade krav:

<!-- Remove download report.
* Upload
* Download
* Expiration
* Modification
* Publish
* [!DNL Brand Portal] publish
* Files
-->

* Överför
* Hämta
* Förfaller
* Ändring
* Publicera
* [!DNL Brand Portal] publicera
* Filer

Följ de här stegen för att lägga till anpassade kolumner i de här rapporterna:

1. I [!DNL Manager interface] klickar du på **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Reports]**.
1. På sidan [!UICONTROL Asset Reports] klickar du på **[!UICONTROL Create]** i verktygsfältet.

1. Välj den rapport du vill skapa på sidan **[!UICONTROL Create Report]**. Klicka på **[!UICONTROL Next]**.

1. Konfigurera rapportinformationen, t.ex. titel, beskrivning, miniatyrbild, mappsökväg och datumintervall. Klicka på **[!UICONTROL Next]**.

1. Välj tillämplig information i listan **[!UICONTROL Default Columns]**. Om du vill visa en anpassad kolumn anger du namnet på kolumnen under **[!UICONTROL Custom Columns]**.

   ![Ange namn för anpassad rapportkolumn](assets/custom_columns-1.png)

1. Lägg till egenskapssökvägen under noden `jcr:content` i CRXDE med egenskapssökvägsväljaren. Du kan också skriva sökvägen i fältet för egenskapssökväg.

   ![Mappa egenskapssökvägen från banor i jcr:content](assets/property_picker.png)

   Om du vill lägga till fler anpassade kolumner klickar du på **[!UICONTROL Add]** och upprepar stegen ovan.

1. Klicka på **[!UICONTROL Create]** i verktygsfältet. Ett meddelande meddelar att rapportgenereringen har initierats.

<!-- TBD: How to configure purge now? Is it using OSGi configurations?

## Configure purging service {#configure-purging-service}

To remove reports that you no longer require, configure the DAM Report Purge service from the web console to purge existing reports based on their quantity and age.

1. Access the web console (configuration manager) from `https://[aem_server]:[port]/system/console/configMgr`.
1. Open the **[!UICONTROL DAM Report Purge Service]** configuration.
1. Specify the frequency (time interval) for the purging service in the `scheduler.expression.name` field. You can also configure the age and the quantity threshold for reports.
1. Save the changes.
-->

## Felsökningsinformation {#tips-troubleshoot}

* Om [!UICONTROL Disk Usage Report] inte genererar och om du använder [!DNL Dynamic Media] måste du se till att alla resurser fortsätter korrekt. Du löser problemet genom att bearbeta resurserna på nytt och generera rapporten igen.

<!-- These notes were present in generate report section above. Removing commented text from in between the instructions to preserve the numbering of the ordered list.

TBD: How do enable this in CS now? Is it done using some OSGi config now?
   >[!NOTE]
   >
   >Before you can generate an **[!UICONTROL Asset Downloaded]** report, ensure that the Asset Download service is enabled. From the web console (`https://[aem_server]:[port]/system/console/configMgr`), open the **[!UICONTROL Day CQ DAM Event Recorder]** configuration, and select the **[!UICONTROL Asset Downloaded (DOWNLOADED)]** option in Event Types if not already selected.
-->

<!-- Removed download report.
   >[!NOTE]
   >
   >By default, the Content Fragments and link shares are included in the asset [!UICONTROL Download] report. Select the appropriate option to create a report of link shares or to exclude Content Fragments from the download report.

   >[!NOTE]
   >
   >The [!UICONTROL Download] report displays details of only those assets which are downloaded after selecting individually or are downloaded using Quick Action. However, it does not include the details of the assets that are inside a downloaded folder.
-->

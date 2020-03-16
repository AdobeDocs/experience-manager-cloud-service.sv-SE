---
title: Materialrapporter
description: I den här artikeln beskrivs olika rapporter om resurser i AEM Resurser och hur du skapar rapporter.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 6998ee5f3c1c1563427e8739998effe0eba867fc

---


# Asset Reports {#asset-reports}

Resursrapportering är ett viktigt verktyg för att utvärdera hur användbart Adobe Experience Manager Assets-distributionen är. Med AEM Assets kan ni generera en mängd olika rapporter om era digitala resurser. Rapporterna innehåller användbar information om hur ditt system används, hur användarna interagerar med resurser och vilka resurser som hämtas och delas.

Använd informationen i rapporterna för att ta fram nyckeltal för att mäta hur AEM Assets används i ert företag och av era kunder.

AEM Assets-rapporteringsramverket utnyttjar Sling-jobb för att asynkront bearbeta rapportbegäranden på ett ordnat sätt. Den kan skalas för stora databaser. Asynkron rapportbearbetning ökar effektiviteten och hastigheten med vilken rapporter genereras.

Rapporthanteringsgränssnittet är intuitivt och innehåller detaljerade alternativ och kontroller för att komma åt arkiverade rapporter och visa rapportkörningsstatus (lyckad, misslyckad och köad).

När en rapport genereras meddelas du via <!-- through an email (optional) and --> ett inkorgsmeddelande. Du kan visa, hämta eller ta bort en rapport från rapportlistsidan, där alla tidigare genererade rapporter visas.

## Generera rapporter {#generate-reports}

AEM Assets genererar följande standardrapporter:

* Överför
* Hämta
* Förfaller
* Ändring
* Publicera
* Publicera varumärkesportalen
* Diskanvändning
* Filer
* Länkdelning

AEM-administratörer kan enkelt generera och anpassa dessa rapporter för implementeringen. Administratören kan följa de här stegen för att skapa en rapport:

1. Tryck/klicka på AEM-logotypen och gå till **[!UICONTROL Verktyg]** > **[!UICONTROL Resurser]** > **[!UICONTROL Rapporter]**.

   ![navigering](assets/navigation.png)

1. Tryck/klicka på **[!UICONTROL Skapa]** i verktygsfältet på sidan Resursrapporter.
1. Välj den rapport du vill skapa på sidan **[!UICONTROL Skapa rapport]** och tryck/klicka på **[!UICONTROL Nästa]**.

   ![choose_report](assets/choose_report.png)

   >[!NOTE]
   >
   >Before you can generate an **[!UICONTROL Asset Downloaded]** report, ensure that the Asset Download service is enabled. Öppna konfigurationen`https://[aem_server]:[port]/system/console/configMgr`Day CQ DAM Event Recorder **[!UICONTROL i webbkonsolen (]** ) och välj alternativet **[!UICONTROL Asset Downloaded (DOWNLOADED)]** i Händelsetyper om det inte redan är valt.

   >[!NOTE]
   >
   >Som standard inkluderas innehållsfragment och länkdelningar i rapporten Hämtade resurser. Välj lämpligt alternativ för att skapa en rapport över länkdelningar eller för att utesluta innehållsfragment från hämtningsrapporten.

1. Konfigurera rapportinformation som titel, beskrivning, miniatyrbild och mappsökväg i CRX-databasen där rapporten lagras. Som standard är mappsökvägen */content/dam*. Du kan ange en annan sökväg.

   ![report_configuration](assets/report_configuration.png)

   Välj datumintervall för rapporten.

   Du kan välja att generera rapporten nu eller vid ett framtida datum och tid.

   >[!NOTE]
   >
   >Om du väljer att schemalägga rapporten vid ett senare datum måste du ange datum och tid i fältet Datum och tid. Om du inte anger något värde behandlas det som en rapport som ska genereras omedelbart.

   Konfigurationsfälten kan variera beroende på vilken typ av rapport du skapar.

   Rapporten **[!UICONTROL Diskanvändning]** innehåller till exempel alternativ för att inkludera resursåtergivningar när du beräknar det diskutrymme som används av resurserna. Du kan välja att inkludera eller exkludera resurser i undermappar för beräkning av diskanvändning.

   >[!NOTE]
   >
   >The **[!UICONTROL Disk Usage]** report does not include date range fields because it indicates current disk space usage only.

   ![disk_usage_configuration](assets/disk_usage_configuration.png)

   När du skapar rapporten **[!UICONTROL Filer]** kan du inkludera/exkludera undermappar. Du kan dock inte inkludera resursåtergivningar för den här rapporten.

   ![files_report](assets/files_report.png)

   The **[!UICONTROL Link Share]** report displays URLs to assets that are shared with external users from within AEM Assets. <!-- It includes email ids of the user who shared the assets, emails ids of users with which the assets are shared, share date, and expiration date for the link. --> Det går inte att anpassa kolumnerna.

   The **[!UICONTROL Link Share]** report, does not include options for subfolders and renditions because it merely publishes the shared URLs that appear under */var/dam/share*.

   ![link_share](assets/link_share.png)

1. Tryck/klicka på **[!UICONTROL Nästa]** i verktygsfältet.

1. På sidan **[!UICONTROL Konfigurera kolumner]** är vissa kolumner markerade för att visas i rapporten som standard. Du kan markera ytterligare kolumner. Avmarkera en markerad kolumn om du vill utesluta den i rapporten.

   ![configure_columns](assets/configure_columns.png)

   Om du vill visa ett anpassat kolumnnamn eller en egenskapssökväg konfigurerar du egenskaperna för resursens binärfil under noden jcr:content i CRX. Du kan också lägga till den via egenskapssökvägsväljaren.

   ![custom_columns](assets/custom_columns.png)

1. Tryck/klicka på **[!UICONTROL Skapa]** i verktygsfältet. Ett meddelande meddelar att rapportgenereringen har initierats.
1. På sidan Resursrapporter baseras rapportgenereringsstatusen på rapportjobbets aktuella tillstånd, till exempel Slutfört, Misslyckades, Köat eller Schemalagt. Samma status visas i inkorgen för meddelanden.

   Om du vill visa rapportsidan trycker/klickar du på rapportlänken. Du kan också markera rapporten och trycka/klicka på ikonen Visa i verktygsfältet.

   ![report_page](assets/report_page.png)

   Tryck/klicka på ikonen Hämta i verktygsfältet för att hämta rapporten i CSV-format.

## Lägg till anpassade kolumner {#add-custom-columns}

Du kan lägga till anpassade kolumner i följande rapporter om du vill visa mer data för dina anpassade krav:

* Överför
* Hämta
* Förfaller
* Ändring
* Publicera
* Publicera varumärkesportalen
* Filer

1. Tryck/klicka på AEM-logotypen och gå till **[!UICONTROL Verktyg]** > **[!UICONTROL Resurser]** > **[!UICONTROL Rapporter]**.
1. Tryck/klicka på **[!UICONTROL Skapa]** i verktygsfältet på sidan Resursrapporter.

1. Välj den rapport du vill skapa på sidan **[!UICONTROL Skapa rapport]** och tryck/klicka på **[!UICONTROL Nästa]**.
1. Konfigurera rapportinformation som titel, beskrivning, miniatyrbild, mappsökväg, datumintervall och så vidare.

1. To display a custom column, specify the name of the column in under **[!UICONTROL Custom Columns]**.

   ![custom_columns-1](assets/custom_columns-1.png)

1. Lägg till egenskapssökvägen under `jcr:content` noden i CRXDE med egenskapssökvägsväljaren.

   ![property_picker](assets/property_picker.png)

   Du kan också skriva sökvägen i fältet för egenskapssökväg.

   ![property_path](assets/property_path.png)

   Om du vill lägga till fler anpassade kolumner trycker/klickar du på **[!UICONTROL Lägg till]** och upprepar steg 5 och 6.

1. Tryck/klicka på **[!UICONTROL Skapa]** i verktygsfältet. Ett meddelande meddelar att rapportgenereringen har initierats.

## Konfigurera rensningstjänst {#configure-purging-service}

Om du vill ta bort rapporter som du inte längre behöver konfigurerar du tjänsten DAM Report Renge från webbkonsolen så att befintliga rapporter rensas baserat på antal och ålder.

1. Gå till webbkonsolen (konfigurationshanteraren) från `https://[aem_server]:[port]/system/console/configMgr`.
1. Öppna konfigurationen för **[!UICONTROL DAM-rapportrensningstjänsten]** .
1. Ange frekvens (tidsintervall) för rensningstjänsten i `scheduler.expression.name` fältet. Du kan också konfigurera åldern och tröskelvärdet för antal rapporter.
1. Spara ändringarna.

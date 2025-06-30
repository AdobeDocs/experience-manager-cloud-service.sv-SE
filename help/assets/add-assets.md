---
title: Lägg till dina digitala resurser i  [!DNL Adobe Experience Manager].
description: Lägg till dina digitala resurser i [!DNL Adobe Experience Manager] som en [!DNL Cloud Service].
feature: Asset Ingestion, Asset Management, Asset Processing, Upload
role: User, Admin
exl-id: 0e624245-f52e-4082-be21-13cc29869b64
source-git-commit: 9c1104f449dc2ec625926925ef8c95976f1faf3d
workflow-type: tm+mt
source-wordcount: '3071'
ht-degree: 0%

---

# Lägg till digitala resurser i [!DNL Adobe Experience Manager] som en [!DNL Cloud Service] [!DNL Assets] {#add-assets-to-experience-manager}

[!DNL Adobe Experience Manager Assets] accepterar många typer av digitala resurser från många källor. Den lagrar binärfiler och skapade renderingar, kan hantera resurser med olika arbetsflöden och [!DNL Adobe Sensei]-tjänster, vilket möjliggör distribution via många kanaler över många ytor.

[!DNL Adobe Experience Manager] förbättrar det binära innehållet i de överförda digitala filerna med omfattande metadata, smarta taggar, återgivningar och andra DAM-tjänster (Digital Asset Management). Du kan överföra olika typer av filer, till exempel bilder, dokument och råbildsfiler, från den lokala mappen eller en nätverksenhet till [!DNL Experience Manager Assets].

Förutom den vanligaste webbläsaröverföringen finns det andra metoder för att lägga till resurser i databasen [!DNL Experience Manager]. De här andra metoderna omfattar skrivbordsklienter, som Adobe Asset Link eller [!DNL Experience Manager]-datorprogrammet, överförings- och förtäringsskript som kunder skulle skapa samt automatiserade ingångsintegreringar som lagts till som [!DNL Experience Manager] -tillägg.

Du kan överföra och hantera binära filer i [!DNL Experience Manager], men de vanligaste filformaten har stöd för ytterligare tjänster, som metadataextrahering eller generering av förhandsgranskning/återgivning. Mer information finns i [filformat som stöds](file-format-support.md).

Du kan också välja att utföra ytterligare bearbetning av de överförda resurserna. Flera resursbearbetningsprofiler kan konfigureras för mappen, till vilken resurser överförs, för att lägga till specifika metadata, återgivningar eller bildbehandlingstjänster. Se [bearbeta resurser vid överföring](#process-when-uploaded).

[!DNL Assets] tillhandahåller följande överföringsmetoder. Adobe rekommenderar att du förstår hur du använder ett överföringsalternativ innan du använder det.

| Överföringsmetod | När ska du använda? | Primär persona |
|---------------------|----------------|-----------------|
| [Assets Console-användargränssnitt](#upload-assets) | Tillfällig uppladdning, enkel nedladdning och dragning, uppladdning av sökare. Använd inte för att överföra många resurser. | Alla användare |
| [Överför API](#upload-using-apis) | För dynamiska beslut under överföring. | Developer |
| [[!DNL Experience Manager] skrivbordsapp](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html) | Intag av resurser med låg volym, men inte för migrering. | Administratör, marknadsförare |
| [[!DNL Adobe Asset Link]](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html) | Användbar när kreatörer och marknadsförare arbetar med resurser från de [!DNL Creative Cloud]-skrivbordsappar som stöds. | Creative, Marketer |
| [Massinklistring av resurser](#asset-bulk-ingestor) | Rekommenderas för storskalig migrering och ibland även för bulkimport. Endast för datalager som stöds. | Administratör, utvecklare |

## Överför resurser {#upload-assets}

<!-- #ENGCHECK do we support pausing? I couldn't get pause to show with 1.5GB upload.... If not, this should be removed#

   You can pause the uploading of large assets (greater than 500 MB) and resume it later from the same page. Select the **[!UICONTROL Pause]** icon beside progress bar that appears when an upload starts.

   The size above which an asset is considered a large asset is configurable. For example, you can configure the system to consider assets above 1000 MB (instead of 500 MB) as large assets. In this case, **[!UICONTROL Pause]** appears on the progress bar when assets of size greater than 1000 MB are uploaded.

   The [!UICONTROL Pause] option does not show if a file greater than 1000 MB is uploaded with a file less than 1000 MB. However, if you cancel the less than 1000 MB file upload, the **[!UICONTROL Pause]** option appears.

   To modify the size limit, configure the `chunkUploadMinFileSize` property of the `fileupload` node in the CRX repository.

   When you click the **[!UICONTROL Pause]** icon, it toggles to a **[!UICONTROL Play]** icon. To resume uploading, click **[!UICONTROL Play]** option.
-->

<!-- #ENGCHECK do we support pausing? I couldn't get pause to show with 1.5GB upload.... If not, this should be removed#
   The ability to resume uploading is especially helpful in low-bandwidth scenarios and network glitches, where it takes a long time to upload a large asset. You can pause the upload operation and continue later when the situation improves. When you resume, uploading starts from the point where you paused it.
-->

<!-- #ENGCHECK assuming this is not relevant? remove after confirming#
   During the upload operation, [!DNL Experience Manager] saves the portions of the asset being uploaded as chunks of data in the CRX repository. When the upload completes, [!DNL Experience Manager] consolidates these chunks into a single block of data in the repository.

   To configure the cleanup task for the unfinished chunk upload jobs, go to `https://[aem_server]:[port]/system/console/configMgr/org.apache.sling.servlets.post.impl.helper.ChunkCleanUpTask`.
-->

Om du vill överföra en fil (eller flera filer) kan du antingen markera dem på skrivbordet och dra användargränssnittet (webbläsaren) till målmappen. Du kan också starta en överföring från användargränssnittet.

>[!IMPORTANT]
>
>Assets som du överför till Experience Manager och som har ett filnamn som är längre än 100 tecken får ett kortare namn när de används i Dynamic Media.
>
>De första 100 tecknen i filnamnet används som de är. Alla återstående tecken ersätts med en alfanumerisk sträng. Den här namnbytesmetoden ger ett unikt namn när resursen används i Dynamic Media. Den är också avsedd att rymma den maximala längden för filnamn som tillåts i Dynamic Media.


1. Navigera till den plats där du vill lägga till digitala resurser i användargränssnittet [!DNL Assets].
1. Gör något av följande om du vill överföra resurserna:

   * Klicka på **[!UICONTROL Create]** > **[!UICONTROL Files]** i verktygsfältet. Du kan byta namn på filen i den dialogruta som visas om det behövs.
   * I en webbläsare som stöder HTML5 drar du resurserna direkt i användargränssnittet för [!DNL Assets]. Dialogrutan för att byta namn på filen visas inte.

   ![create_menu](assets/create_menu.png)

   Om du vill markera flera filer väljer du `Ctrl` eller `Command`-tangenten och markerar resurserna i dialogrutan för filväljaren. När du använder en iPad kan du bara markera en fil i taget.

1. Om du vill avbryta en pågående överföring klickar du på Stäng (`X`) bredvid förloppsindikatorn. När du avbryter överföringen tar [!DNL Assets] bort den delvis överförda delen av resursen.
Om du avbryter en överföring innan filerna har överförts, avbryter [!DNL Assets] överföringen av den aktuella filen och uppdaterar innehållet. Filer som redan har överförts tas dock inte bort.

1. I dialogrutan för överföringsförlopp i [!DNL Assets] visas antalet överförda filer och de filer som inte kunde överföras.
Dessutom visar användargränssnittet [!DNL Assets] den senaste resursen som du överför eller den mapp som du skapade först.

>[!NOTE]
>
>Mer information om hur du överför kapslade mapphierarkier finns i [Massöverföring av resurser](#bulk-upload).

<!-- #ENGCHECK I'm assuming this is no longer relevant.... If yes, this should be removed#

### Serial uploads {#serialuploads}

Uploading numerous assets in bulk consumes significant I/O resources, which may adversely impact the performance of [!DNL Assets]. In particular, if you have a slow internet connection, the time to upload drastically increases due to a spike in disk I/O. Moreover, your web browser may introduce additional restrictions to the number of POST requests [!DNL Assets] can handle for concurrent asset uploads. As a result, the upload operation fails or terminate prematurely. In other words, [!DNL Assets] may miss some files while ingesting a bunch of files or altogether fail to ingest any file.

To overcome this situation, [!DNL Assets] ingests one asset at a time (serial upload) during a bulk upload operation, instead of the concurrently ingesting all the assets.

Serial uploading of assets is enabled by default. To disable the feature and allow concurrent uploading, overlay the `fileupload` node in CRX-DE and set the value of the `parallelUploads` property to `true`.

### Streamed uploads {#streamed-uploads}

If you upload many assets to [!DNL Experience Manager], the I/O requests to server increase drastically, which reduces the upload efficiency and can even cause some upload task to time out. [!DNL Assets] supports streamed uploading of assets. Streamed uploading reduces the disk I/O during the upload operation by avoiding asset storage in a temporary folder on the server before copying it to the repository. Instead, the data is transferred directly to the repository. This way, the time to upload large assets and the possibility of timeouts is reduced. Streamed upload is enabled by default in [!DNL Assets].

>[!NOTE]
>
>Streaming upload is disabled for [!DNL Experience Manager] running on JEE server with servlet-api version lower than 3.1.
-->

### Hantera överföringar för befintliga resurser {#handling-upload-existing-file}

Du kan överföra en resurs med samma sökväg (samma namn och samma plats) som en befintlig resurs. En varningsdialogruta med följande alternativ visas:

* Ersätt befintlig resurs: Om du ersätter en befintlig resurs tas metadata för resursen och eventuella tidigare ändringar (till exempel anteckningar och beskärning) som du har gjort för den befintliga resursen bort.

  >[!NOTE]
  >
  >Alternativet att ersätta resurser är inte tillgängligt om resursen är låst eller utcheckad.

* Skapa en annan version: En ny version av den befintliga resursen skapas i databasen. Du kan visa de två versionerna i [!UICONTROL Timeline] och återställa den tidigare versionen om det behövs.
* Behåll båda: Om du väljer att behålla båda resurserna får den nya resursen ett nytt namn.

Om du vill behålla den duplicerade resursen i [!DNL Assets] klickar du på **[!UICONTROL Keep]**. Klicka på **[!UICONTROL Delete]** om du vill ta bort den duplicerade resursen som du överförde.

### Hantering av filnamn och förbjudna tecken {#filename-handling}

[!DNL Experience Manager Assets] förhindrar att du överför resurser med förbjudna tecken i filnamn. Om du försöker överföra en resurs med filnamn som innehåller ett otillåtet tecken eller fler, visar [!DNL Assets] ett varningsmeddelande och stoppar överföringen tills du tar bort dessa tecken eller överför med ett tillåtet namn.

I dialogrutan [!UICONTROL Upload Assets] kan du ange långa namn för de filer som du överför, så att den passar din organisations specifika filnamnskonventioner. Följande (blankstegsavgränsad lista med) tecken stöds inte:

* Ogiltiga tecken för resursnamn: `* / : [ \\ ] | # % { } ? &`
* Ogiltiga tecken för resursmappens namn: `* / : [ \\ ] | # % { } ? \" . ^ ; + & \t`

## Överför resurser gruppvis {#bulk-upload}

Inspelaren av gruppresurser kan hantera många resurser effektivt. Men ett storskaligt intag är inte bara en stor fildump eller en tillfällig migrering. För att ett storskaligt intag ska bli ett meningsfullt projekt som passar ert företag och är effektivt, måste ni planera migreringen och strukturera resursorganisationen. Alla förslag skiljer sig åt, i stället för att generalisera, vilket spelar en avgörande roll för den nya databassammansättningen och affärsbehoven. Nedan följer några övergripande förslag på hur du kan planera och utföra ett massintagande:

* Kuratresurser: Ta bort resurser som inte behövs i DAM. Överväg att ta bort oanvända, föråldrade eller duplicerade resurser. Sådan hushållning minskar överförda data och insamlade resurser, vilket leder till snabbare frågor.
* Ordna resurser: Överväg att ordna innehållet i någon logisk ordning, t.ex. efter filstorlek, filformat, skiftläge eller prioritet. I allmänhet kräver stora komplexa filer mer bearbetning. Du kan också överväga att importera stora filer separat med filstorleksfiltreringsalternativet (som beskrivs nedan).
* Större frågor: Överväg att dela upp ditt intag i flera massintagningsprojekt. q gör att du kan se innehållet snabbare och uppdatera ditt intag efter behov. Du kan t.ex. importera bearbetningsintensiva resurser under icke-toppade timmar eller gradvis i flera segment. Du kan emellertid importera mindre och enklare resurser som inte kräver mycket bearbetning på en gång.

Om du vill överföra fler filer använder du någon av följande metoder. Se även [användningsexempel och metoder](#upload-methods-comparison)

* [API:er för överföring av resurser](developer-reference-material-apis.md#asset-upload): Använd ett anpassat överföringsskript eller verktyg som använder API:er för att lägga till ytterligare hantering av resurser (till exempel översätt metadata eller byt namn på filer), om det behövs.
* [[!DNL Experience Manager] skrivbordsapp](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html): Användbart för kreatörer och marknadsförare som överför resurser från det lokala filsystemet. Använd den för att överföra kapslade mappar som är tillgängliga lokalt.
* [Verktyget Massintag](#asset-bulk-ingestor): Används för konsumtion av stora mängder resurser, antingen då och då eller när [!DNL Experience Manager] distribueras.

### Verktyget Importera flera resurser {#asset-bulk-ingestor}

Verktyget tillhandahålls endast administratörsgruppen som kan användas för storskalig förtäring av resurser från Azure- eller S3-datalager. Se en video som visar hur konfigurationen och intagandet fungerar.

>[!VIDEO](https://video.tv.adobe.com/v/329680/?quality=12&learn=on)

Följande bild visar de olika faserna när du importerar resurser till Experience Manager från ett datalager:

![Verktyget Massinmatning](assets/bulk-ingestion.png)

**Förutsättningar**

Ett externt lagringskonto eller en bucket från Azure eller AWS krävs för att använda den här funktionen.

>[!NOTE]
>
>Skapa lagringskontobehållaren eller lagringskassetten som privat och acceptera anslutningar endast från auktoriserade begäranden. Ytterligare begränsningar för inkommande nätverksanslutningar stöds dock inte.

>[!NOTE]
>
>Externa lagringskonton kan ha andra fil-/mappnamnsregler än verktyget för massimport. Se [Hantera filnamn vid bulkimport](#filename-handling-bulkimport) om du vill ha mer information om ej tillåtna/escape-namn.


### Konfigurera verktyget Massimport {#configure-bulk-ingestor-tool}

Så här konfigurerar du verktyget för massimport:

1. Navigera till **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Bulk Import]**. Välj alternativet **[!UICONTROL Create]**.

1. Ange en rubrik för bulkimportkonfigurationen i fältet **[!UICONTROL Title]**.

1. Välj datakälltyp i listrutan **[!UICONTROL Import Source]**.

1. Ange värdena för att skapa en anslutning till datakällan. Om du till exempel väljer **Azure Blob Storage** som datakälla anger du värdena för Azure-lagringskontot, Azure-blobbehållaren och Azure-åtkomstnyckeln.

1. Välj önskat autentiseringsläge i listrutan. **Azure Access Key** ger fullständig åtkomst till Azure-lagringskontot, medan **Azure SAS-token** tillåter administratören att begränsa möjligheterna för token med hjälp av behörigheter och förfalloprinciper.

1. Ange namnet på rotmappen som innehåller resurser i datakällan i fältet **[!UICONTROL Source Folder]**.

1. (Valfritt) Ange den minsta filstorleken för resurser i MB för att inkludera dem i inmatningsprocessen i fältet **[!UICONTROL Filter by Min Size]**.

1. (Valfritt) Ange den maximala filstorleken för resurser i MB som ska inkluderas i inmatningsprocessen i fältet **[!UICONTROL Filter by Max Size]**.

1. (Valfritt) Ange en kommaavgränsad lista med MIME-typer som ska uteslutas från intaget i fältet **[!UICONTROL Exclude MIME Types]**. Exempel: `image/jpeg, image/.*, video/mp4`. Se [alla filformat som stöds](/help/assets/file-format-support.md).

1. Ange en kommaavgränsad lista med MIME-typer som ska tas med från inmatningen i fältet **[!UICONTROL Include MIME Types]**. Se [alla filformat som stöds](/help/assets/file-format-support.md).

1. Välj alternativet **[!UICONTROL Delete source file after import]** om du vill ta bort originalfilerna från källdatalagret efter att filerna har importerats till [!DNL Experience Manager].

1. Välj **[!UICONTROL Import Mode]**. Välj **Hoppa över**, **Ersätt** eller **Skapa version**. Hoppa över är standardläget och i det här läget hoppar användaren över att importera en resurs om den redan finns. Se innebörden av [Ersätt och skapa versionsalternativ](#handling-upload-existing-file).

1. Om du vill definiera en plats i DAM där resurser ska importeras med fältet **[!UICONTROL Assets Target Folder]** anger du en sökväg. Exempel: `/content/dam/imported_assets`.

1. (Valfritt) Ange den metadatafil som ska importeras i CSV-format i fältet **[!UICONTROL Metadata File]**. Ange CSV-filen på blobbplatsen för källan och referera till sökvägen när verktyget för massimport konfigureras. CSV-filformatet som det här fältet refererar till är samma som CSV-filformatet när du [importerar och exporterar resursmetadata satsvis](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/metadata-import-export.html). Om du väljer alternativet **Ta bort källfil efter import** kan du filtrera CSV-filer antingen med fälten **Uteslut** eller **Inkludera MIME-typ** eller **Filtrera efter sökväg/fil**. Du kan använda ett reguljärt uttryck för att filtrera CSV-filer i dessa fält.

1. Klicka på **[!UICONTROL Save]** för att spara konfigurationen.

### Hantera konfigurationen för verktyget Massimport {#manage-bulk-import-configuration}

När du har skapat konfigurationen för verktyget Massimport kan du utföra uppgifter för att utvärdera konfigurationen innan du gruppimporterar resurser till din Experience Manager-instans. Om du vill visa de tillgängliga alternativen för att hantera konfigurationen av verktyget för massimport väljer du den konfiguration som är tillgänglig på **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Bulk Import]**.

### Redigera konfigurationen {#edit-configuration}

Om du vill redigera konfigurationsinformationen markerar du konfigurationen och klickar sedan på **[!UICONTROL Edit]**. Du kan inte redigera titeln för konfigurationen och importdatakällan när du utför redigeringsåtgärden.

### Ta bort konfigurationen {#delete-configuration}

Markera konfigurationen och klicka på **[!UICONTROL Delete]** för att ta bort konfigurationen för massimport.

### Validera anslutningen till datakällan {#validate-connection}

Om du vill validera anslutningen till datakällan markerar du konfigurationen och klickar sedan på **[!UICONTROL check]**. Om anslutningen lyckas visas följande meddelande i Experience Manager:

![Meddelande om slutförd gruppimport](assets/bulk-import-success-message.png)

### Anropa en testkörning för massimportjobbet {#invoke-test-run-bulk-import}

Markera konfigurationen och klicka på **[!UICONTROL Dry Run]** för att starta en testkörning för massimportjobbet. Experience Manager visar följande information om massimportjobbet:

![Resultat för torr körning](assets/dry-assets-result.png)

### Hantera filnamn vid bulkimport {#filename-handling-bulkimport}

När du importerar resurser eller mappar i grupp importerar [!DNL Experience Manager Assets] hela strukturen för det som finns i importkällan. [!DNL Experience Manager] följer de inbyggda reglerna för specialtecken i resurs- och mappnamnen, och därför måste dessa filnamn saneras. För både mappnamn och resursnamn ändras inte den rubrik som definieras av användaren och lagras i `jcr:title`.

Under bulkimporten letar [!DNL Experience Manager] efter de befintliga mapparna för att undvika att importera resurserna och mapparna igen, och verifierar även rensningsreglerna som tillämpas i den överordnade mappen där importen sker. Om saneringsreglerna tillämpas i den överordnade mappen, tillämpas samma regler på importkällan. För ny import används följande saneringsregler för att hantera filnamnen på resurser och mappar.

**Otillåtna namn vid bulkimport**

Följande tecken tillåts inte i fil- och mappnamn:

* Tecken för kontroll och privat användning (0x00 till 0x1F, \u0081, \uE000)
* Fil- eller mappnamn som slutar med en punkt (.)

Filer eller mappar med namn som matchar dessa villkor hoppas över under importprocessen och markeras som misslyckade.

**Hantera resursnamn i bulkimport**

JCR-namnet och sökvägen saneras med API:t `JcrUtil.escapeIllegalJcrChars` för filnamn för resurser.

* Unicode-tecken ändras inte
* Ersätt specialtecknen med deras URL Escape-kod, till exempel uppdateras `new%asset.png` till `new%25asset.png`:

  ```
                  URL escape code   
  
  "               %22
  %               %25
  '               %27
  *               %2A
  /               %2F
  :               %3A
  [               %5B
  \n              %0A
  \r              %0D
  \t              %09
  ]               %5D
  |               %7C
  ```

**Hantera mappnamn vid bulkimport**

För mappfilnamn sanpassas JCR-namnet och sökvägen med API:t `DamUtil.getSanitizedFolderName`.

* Versaler konverteras till gemener
* Unicode-tecken ändras inte
* Ersätt specialtecknen med bindestreck (&#39;-&#39;). `new folder` uppdateras till `new-folder`:

  ```
  "                           
  #                         
  %                           
  &                          
  *                           
  +                          
  .                           
  :                           
  ;                          
  ?                          
  [                           
  ]                           
  ^                         
  {                         
  }                         
  |                           
  /         It is used for split folder in cloud storage and is pre-handled, no conversion here.
  \         Not allowed in Azure, allowed in AWS.
  \t
  space     It is the space character.
  ```

<!-- 
[!DNL Experience Manager Assets] manages the forbidden characters in the filenames while you upload assets or folders. [!DNL Experience Manager] updates only the node names in the DAM repository. However, the `title` of the asset or folder remains unchanged.

Following are the file naming conventions that are applied while uploading assets or folders in [!DNL Experience Manager Assets]:

| Characters &Dagger; | When occurring in file names | When occurring in folder names | Example |
|---|---|---|---|
| `. / : [ ] | *` | Replaced with `-` (hyphen). | Replaced with `-` (hyphen). A `.` (dot) in the filename extension is retained as is. | Replaced with `-` (hyphen). | `myimage.jpg` remains as is and `my.image.jpg` changes to `my-image.jpg`. |
| `% ; # , + ? ^ { } "` and whitespaces | Whitespaces are retained | Replaced with `-` (hyphen). | `My Folder.` changes to `my-folder-`. |
| `# % { } ? & .` | Replaced with `-` (hyphen). | NA. | `#My New File.` changes to `-My New File-`. |
| Uppercase characters | Casing is retained as is. | Changed to lowercase characters. | `My New Folder` changes to `my-new-folder`. |
| Lppercase characters | Casing is retained as is. | Casing is retained as is. | NA. |

&Dagger; The list of characters is a whitespace-separated list.
-->

#### Schemalägg en engångs- eller återkommande massimport {#schedule-bulk-import}

Så här schemalägger du en enstaka eller återkommande bulkimport:

1. Skapa en bulkimportkonfiguration.
1. Markera konfigurationen och välj **[!UICONTROL Schedule]** i verktygsfältet.
1. Ställ in ett engångsintag eller schemalägg ett timschema, ett dagligt eller ett veckoschema. Klicka på **[!UICONTROL Submit]**.

   ![Schemalägg massinläsarjobb](assets/bulk-ingest-schedule1.png)


#### Visa Assets målmapp {#view-assets-target-folder}

Om du vill visa Assets-målplatsen där resurserna importeras efter att du har kört massimportjobbet, markerar du konfigurationen och klickar sedan på **[!UICONTROL View Assets]**.

#### Kör verktyget Massimport {#run-bulk-import-tool}

När [du har konfigurerat verktyget för massimport](#configure-bulk-ingestor-tool) och [har hanterat konfigurationen av verktyget för massimport](#manage-bulk-import-configuration) kan du köra konfigurationsjobbet för att starta massintagningen av resurser.

Om du vill starta processen för massimport går du till **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Bulk Import]**, markerar [konfigurationen för massimport](#configure-bulk-ingestor-tool) och klickar sedan på **[!UICONTROL Run]**. Bekräfta genom att klicka på **[!UICONTROL Run]** igen.

Experience Manager uppdaterar statusen för jobbet till **Bearbetning** och till **Slutförd** när jobbet har slutförts. Klicka på **Visa Assets** om du vill visa de importerade resurserna i Experience Manager.

När jobbet pågår kan du även välja konfigurationen och klicka på **Stopp** för att stoppa massinläsningsprocessen. Klicka på **Kör** igen för att återuppta processen. Du kan också klicka på **Torr körning** om du vill veta mer om de resurser som fortfarande väntar på import.

#### Hantera jobb efter körning {#manage-jobs-after-execution}

Med Experience Manager kan du se historiken för massimportjobben. Jobbhistoriken omfattar jobbstatus, jobbskapare, loggar och annan information, t.ex. startdatum och starttid, datum och tid för att skapa samt slutdatum och sluttid.

Om du vill komma åt jobbhistoriken för en konfiguration markerar du konfigurationen och klickar på **[!UICONTROL Job History]**. Välj ett jobb och klicka på **Öppna**.

![Schemalägg massinläsarjobb](assets/job-history-bulk-import.png)

Experience Manager visar jobbhistoriken. På historiksidan för massimportjobb kan du även klicka på **Ta bort** för att ta bort jobbet för konfigurationen för massimport.


## Överför resurser med skrivbordsklienter {#upload-assets-desktop-clients}

Förutom webbläsargränssnittet stöder [!DNL Experience Manager] andra klienter på skrivbordet. De ger också en uppladdningsupplevelse utan att du behöver gå till webbläsaren.

* [[!DNL Adobe Asset Link]](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html) ger åtkomst till resurser från [!DNL Experience Manager] i skrivbordsprogrammen Adobe Photoshop, Adobe Illustrator och Adobe InDesign. Du kan överföra det öppna dokumentet till [!DNL Experience Manager] direkt från Adobe Asset Link-användargränssnittet från dessa skrivbordsprogram.
* [[!DNL Experience Manager] skrivbordsappen](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html) gör det enklare att arbeta med resurser på skrivbordet, oberoende av filtyp eller vilket program som hanterar dem. Det är användbart att överföra filer i kapslade mapphierarkier från det lokala filsystemet, eftersom webbläsaröverföring bara stöder överföring av platta fillistor.

## Bearbeta resurser när de överförs {#process-when-uploaded}

Om du vill utföra ytterligare bearbetning på de överförda resurserna kan du använda bearbetningsprofiler på överförda mappar. Profilerna är tillgängliga på sidan **[!UICONTROL Properties]** i en mapp i [!DNL Assets]. En digital resurs utan ett tillägg eller med ett felaktigt tillägg bearbetas inte som du vill. När du till exempel överför sådana resurser händer ingenting eller så kan en felaktig bearbetningsprofil gälla för resursen. Användarna kan fortfarande lagra de binära filerna i DAM.

![Egenskaper för en resursmapp med alternativ för att lägga till en bearbetningsprofil](assets/assets-folder-properties.png)

Följande flikar är tillgängliga:

* Med [metadataprofiler](metadata-profiles.md) kan du använda standardmetadataegenskaper för resurser som överförs till den mappen.
* Med [Bearbetningsprofiler](asset-microservices-configure-and-use.md) kan du generera fler återgivningar än vad som är möjligt som standard.

Om [!DNL Dynamic Media] är aktiverat i din distribution är följande flikar tillgängliga:

* Med [[!DNL Dynamic Media] bildprofiler](dynamic-media/image-profiles.md) kan du använda en särskild beskärningskonfiguration (**[!UICONTROL Smart Cropping]** och pixelbeskärning) och skärpekonfiguration för de överförda resurserna.
* Med [[!DNL Dynamic Media] videoprofiler](dynamic-media/video-profiles.md) kan du använda särskilda videokodningsprofiler (upplösning, format, parametrar).

>[!NOTE]
>
>[!DNL Dynamic Media] beskärning och andra åtgärder för resurser är icke-förstörande, vilket innebär att åtgärderna inte ändrar det överförda originalet. I stället innehåller det parametrar som ska beskäras eller omformas när resurserna levereras.

För mappar som har en tilldelad bearbetningsprofil visas profilnamnet på miniatyrbilden i kortvyn. I listvyn visas profilnamnet i kolumnen **[!UICONTROL Processing Profile]**.

## Överför eller importera resurser med API:er {#upload-using-apis}

Teknisk information om överförings-API:er och protokoll samt länkar till SDK och exempelklienter med öppen källkod finns i avsnittet [Överför resurser](developer-reference-material-apis.md#asset-upload) i utvecklarreferensen.

## Tips, metodtips och begränsningar {#tips-limitations}

* Direkt binär överföring är en ny metod för att överföra resurser. Det stöds som standard av produktfunktioner och klienter, som [!DNL Experience Manager]-användargränssnittet, [!DNL Adobe Asset Link] och [!DNL Experience Manager]-datorprogrammet. All anpassad kod som anpassas eller utökas av kundens tekniska team måste använda de nya API:erna och protokollen för överföring.

* Adobe rekommenderar att du lägger till högst 1 000 resurser i varje mapp i [!DNL Experience Manager Assets]. Om du försöker göra det kan du få ett varningsmeddelande med texten &quot;This directory contains 1000+ items. Överföringar och nya mappar kan fördröjas.&quot; Du kan fortfarande lägga till fler resurser i en mapp, men det kan uppstå prestandaproblem, till exempel långsammare navigering i sådana mappar.

* När du väljer **[!UICONTROL Replace]** i dialogrutan [!UICONTROL Name Conflict] genereras resurs-ID om för den nya resursen. Detta ID skiljer sig från ID:t för föregående resurs. Om [Assets Insights](/help/assets/assets-insights.md) är aktiverat för att spåra visningar eller klickningar med [!DNL Adobe Analytics] blir det återskapade resurs-ID:t ogiltigt för de data som hämtats för resursen på [!DNL Analytics].

* En del överföringsmetoder hindrar dig inte från att överföra resurser med [förbjudna tecken](#filename-handling) i filnamnen. Tecknen ersätts med symbolen `-`.

* När du överför resurser med webbläsaren stöds endast platta fillistor och inte kapslade mapphierarkier. Om du vill överföra alla resurser i en kapslad mapp bör du överväga att använda [skrivbordsappen](#upload-assets-desktop-clients).

* Vid massimport importeras hela mappstrukturen som den finns i datakällan. Endast de mappar som inte är tomma skapas i [!DNL Experience Manager].


<!-- TBD: Link to file name handling in DA docs when it is documented. 
-->

**Se även**

* [Översätt Assets](translate-assets.md)
* [ASSETS HTTP API](mac-api-assets.md)
* [Filformat som stöds av Assets](file-format-support.md)
* [Sök resurser](search-assets.md)
* [Anslutna resurser](use-assets-across-connected-assets-instances.md)
* [Resursrapporter](asset-reports.md)
* [Metadata-scheman](metadata-schemas.md)
* [Hämta resurser](download-assets-from-aem.md)
* [Hantera metadata](manage-metadata.md)
* [Sök efter ansikten](search-facets.md)
* [Hantera samlingar](manage-collections.md)
* [Import av massmetadata](metadata-import-export.md)
* [Publicera Assets till AEM och Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)

>[!MORELIKETHIS]
>
>* [[!DNL Adobe Experience Manager] skrivbordsapp](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html)
>* [Om [!DNL Adobe Asset Link]](https://www.adobe.com/creativecloud/business/enterprise/adobe-asset-link.html)
>* [[!DNL Adobe Asset Link] dokumentation](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html)
>* [Teknisk referens för överföring av resurser](developer-reference-material-apis.md#asset-upload)

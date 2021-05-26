---
title: Lägg till dina digitala resurser i [!DNL Adobe Experience Manager].
description: Lägg till dina digitala resurser i [!DNL Adobe Experience Manager] som en [!DNL Cloud Service].
feature: Resurshantering,Överför
role: Business Practitioner,Administrator
exl-id: 0e624245-f52e-4082-be21-13cc29869b64
source-git-commit: 2e00b62efa07488fbdba723d283b9b76b53f6d34
workflow-type: tm+mt
source-wordcount: '2006'
ht-degree: 0%

---

# Lägg till digitala resurser i [!DNL Adobe Experience Manager] som en [!DNL Cloud Service] [!DNL Assets] {#add-assets-to-experience-manager}

[!DNL Adobe Experience Manager Assets] kan hantera många typer av digitala resurser från många olika källor. Det lagrar binärfiler och skapade renderingar, kan hantera resurser med ett antal olika arbetsflöden och [!DNL Adobe Sensei]-tjänster, möjliggör distribution via många kanaler över många ytor.

[!DNL Adobe Experience Manager] berikar det binära innehållet i de överförda digitala filerna med omfattande metadata, smarta taggar, renderingar och andra DAM-tjänster (Digital Asset Management). Du kan överföra olika typer av filer, till exempel bilder, dokument och råbildsfiler, från den lokala mappen eller en nätverksenhet till [!DNL Experience Manager Assets].

Förutom den vanligaste webbläsaröverföringen finns det andra metoder att lägga till resurser i [!DNL Experience Manager]-databasen, bland annat skrivbordsklienter, som Adobe Asset Link eller [!DNL Experience Manager]-skrivbordsapp, överförings- och förtäringsskript som kunder skulle skapa samt automatiserade importfunktioner som lagts till som [!DNL Experience Manager]-tillägg.

Du kan överföra och hantera binära filer i [!DNL Experience Manager], men de vanligaste filformaten har stöd för ytterligare tjänster, som metadataextrahering eller generering av förhandsgranskning/återgivning. Mer information finns i [filformat](file-format-support.md) som stöds.

Du kan också välja att utföra ytterligare bearbetning av de överförda resurserna. Ett antal resursbearbetningsprofiler kan konfigureras för mappen, till vilken resurserna överförs, för att lägga till specifika metadata, återgivningar eller bildbehandlingstjänster. Se [bearbeta resurser när de överförs](#process-when-uploaded).

[!DNL Assets] innehåller följande överföringsmetoder. Adobe rekommenderar att du förstår hur du använder ett överföringsalternativ innan du använder det.

| Överföringsmetod | När ska du använda? | Primär persona |
|---------------------|----------------|-----------------|
| [Användargränssnittet i Resurskonsolen](#upload-assets) | Tillfällig uppladdning, enkel nedladdning och dragning, uppladdning av sökare. Använd inte för att överföra ett stort antal resurser. | Alla användare |
| [Överför API](#upload-using-apis) | För dynamiska beslut under överföring. | Developer |
| [[!DNL Experience Manager] datorprogram](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html) | Intag av resurser med låg volym, men inte för migrering. | Administratör, marknadsförare |
| [[!DNL Adobe Asset Link]](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/adobe-asset-link.ug.html) | Användbar när kreatörer och marknadsförare arbetar med resurser från de [!DNL Creative Cloud]-skrivbordsappar som stöds. | Kreativ, Marketer |
| [Massinhämtning av resurser](#asset-bulk-ingestor) | Rekommenderas för storskalig migrering och ibland även för bulkimport. Endast för datalager som stöds. | Administratör, utvecklare |

## Överför resurser {#upload-assets}

<!-- #ENGCHECK do we support pausing? I couldn't get pause to show with 1.5GB upload.... If not, this should be removed#

   You can pause the uploading of large assets (greater than 500 MB) and resume it later from the same page. Tap the **[!UICONTROL Pause]** icon beside progress bar that appears when an upload starts.

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

1. Navigera till den plats där du vill lägga till digitala resurser i [!DNL Assets]-användargränssnittet.
1. Gör något av följande om du vill överföra resurserna:

   * Klicka på **[!UICONTROL Create]** > **[!UICONTROL Files]** i verktygsfältet. Du kan byta namn på filen i den dialogruta som visas om det behövs.
   * I en webbläsare som stöder HTML5 drar du resurserna direkt i [!DNL Assets]-användargränssnittet. Dialogrutan för att byta namn på filen visas inte.

   ![create_menu](assets/create_menu.png)

   Om du vill markera flera filer väljer du `Ctrl` eller `Command`-tangenten och markerar resurserna i dialogrutan för filväljaren. När du använder en iPad kan du bara markera en fil i taget.

1. Om du vill avbryta en pågående överföring klickar du på Stäng (`X`) bredvid förloppsindikatorn. När du avbryter överföringsåtgärden tar [!DNL Assets] bort den delvis överförda delen av resursen.
Om du avbryter en överföring innan filerna överförs slutar [!DNL Assets] att överföra den aktuella filen och uppdaterar innehållet. Filer som redan har överförts tas dock inte bort.

1. Dialogrutan för överföringsförlopp i [!DNL Assets] visar antalet överförda filer och de filer som inte kunde överföras.
Dessutom visar [!DNL Assets]-användargränssnittet den senaste resursen som du överför eller den mapp som du skapade först.

>[!NOTE]
>
>Information om hur du överför kapslade mapphierarkier finns i [massöverföring av resurser](#bulk-upload).

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

### Hantera överföringar när resursen redan finns {#handling-upload-existing-file}

Du kan överföra en resurs med samma sökväg (samma namn och plats) som en befintlig resurs. En varningsdialogruta med följande alternativ visas:

* Ersätt befintlig resurs: Om du ersätter en befintlig resurs tas metadata för resursen och eventuella tidigare ändringar (till exempel anteckningar, beskärning och så vidare) som du har gjort för den befintliga resursen bort.
* Skapa en ny version: En ny version av den befintliga resursen skapas i databasen. Du kan visa de två versionerna i [!UICONTROL Timeline] och återgå till den tidigare versionen om det behövs.
* Behåll båda: Om du väljer att behålla båda resurserna får den nya resursen ett nytt namn.

Om du vill behålla den duplicerade resursen i [!DNL Assets] klickar du på **[!UICONTROL Keep]**. Klicka på **[!UICONTROL Delete]** om du vill ta bort den duplicerade resursen som du överförde.

### Hantering av filnamn och förbjudna tecken {#filename-handling}

[!DNL Experience Manager Assets] försöker förhindra att du överför resurser med de förbjudna tecknen i filnamnen. Om du försöker överföra en resurs med ett filnamn som innehåller ett eller flera otillåtna tecken visar [!DNL Assets] ett varningsmeddelande och stoppar överföringen tills du tar bort dessa tecken eller överför med ett tillåtet namn.

Om du vill anpassa namngivningskonventionerna för din organisation kan du i [!UICONTROL Upload Assets]-dialogrutan ange långa namn för de filer som du överför. Följande (blankstegsavgränsad lista med) tecken stöds inte:

* ogiltiga tecken för objektfilnamnet `* / : [ \\ ] | # % { } ? &`
* ogiltiga tecken för resursmappens namn `* / : [ \\ ] | # % { } ? \" . ^ ; + & \t`

## Överför resurser gruppvis {#bulk-upload}

Inspelaren av massresurser kan hantera mycket stora mängder resurser effektivt. Men ett storskaligt intag är inte bara en stor fildump eller en tillfällig migrering. För att ett storskaligt intag ska bli ett meningsfullt projekt som passar ert företag och är effektivt, måste ni planera migreringen och strukturera resursorganisationen. Alla förslag skiljer sig åt, i stället för att generalisera, vilket spelar en avgörande roll för den nya databassammansättningen och affärsbehoven. Nedan följer några övergripande förslag på hur du kan planera och utföra ett massintagande:

* Kuratresurser: Ta bort resurser som inte behövs i DAM. Överväg att ta bort oanvända, föråldrade eller duplicerade resurser. Detta minskar antalet överförda data och insamlade resurser, vilket leder till snabbare frågor.
* Ordna resurser: Överväg att ordna innehållet i någon logisk ordning, t.ex. efter filstorlek, filformat, skiftläge eller prioritet. I allmänhet kräver stora komplexa filer mer bearbetning. Du kan också överväga att importera stora filer separat med hjälp av filstorleksfiltreringsalternativet (som beskrivs nedan).
* Större frågor: Överväg att dela upp ditt intag i flera massintagningsprojekt. Detta gör att du kan se innehållet snabbare och uppdatera ditt intag efter behov. Du kan t.ex. importera bearbetningsintensiva resurser under icke-toppade timmar eller gradvis i flera segment. Du kan emellertid importera mindre och enklare resurser som inte kräver mycket bearbetning på en gång.

Om du vill överföra fler filer använder du någon av följande metoder. Se även [användningsexempel och metoder](#upload-methods-comparison)

* [API:er](developer-reference-material-apis.md#asset-upload) för överföring av resurser: Använd ett anpassat överföringsskript eller verktyg som använder API:er för att lägga till ytterligare hantering av resurser (t.ex. översätta metadata eller byta namn på filer), om det behövs.
* [[!DNL Experience Manager] datorprogram](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html): Användbart för kreatörer och marknadsförare som överför resurser från det lokala filsystemet. Använd den för att överföra kapslade mappar som är tillgängliga lokalt.
* [Verktyget](#asset-bulk-ingestor) Massintag: Används för konsumtion av stora mängder resurser, antingen vid enstaka tillfällen eller vid första driftsättningen  [!DNL Experience Manager].

### Verktyget Massinhämtning {#asset-bulk-ingestor}

Verktyget tillhandahålls bara till administratörsgruppen som kan användas för storskalig förtäring av resurser från Azure- eller S3-datalager. Se en video som visar hur konfigurationen och intagandet fungerar.

>[!VIDEO](https://video.tv.adobe.com/v/329680/?quality=12&learn=on)

Så här konfigurerar du verktyget:

1. Navigera till **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Bulk Import]**. Välj alternativet **[!UICONTROL Create]**.

![Konfiguration av bulkimporterare](assets/bulk-import-config.png)

1. På sidan [!UICONTROL bulk import configuration] anger du önskade värden.

   * [!UICONTROL Title]: En beskrivande titel.
   * [!UICONTROL Import Source]: Välj lämplig datakälla.
   * [!UICONTROL Filter by Min Size]: Ange den minsta filstorleken för resurser i MB.
   * [!UICONTROL Filter by Max Size]: Ange maximal filstorlek för resurser i MB.
   * [!UICONTROL Exclude Mime Types]: Kommaavgränsad lista med MIME-typer som ska uteslutas från intaget. Till exempel, `image/jpeg, image/.*, video/mp4`.
   * [!UICONTROL Include Mime Types]: Kommaavgränsad lista med MIME-typer som ska ingå i intaget. Se [alla filformat som stöds](/help/assets/file-format-support.md).
   * [!UICONTROL Import Mode]: Välj Hoppa över, Ersätt eller Skapa version. Hoppa över är standardläget och i det här läget hoppar användaren över att importera en resurs om den redan finns. Se innebörden i [Ersätt och skapa versionsalternativ](#handling-upload-existing-file).
   * [!UICONTROL Assets Target Folder]: Importera mapp i DAM där resurser ska importeras. Till exempel, `/content/dam/imported_assets`

1. Du kan ta bort, ändra, köra och göra mer med dina inmatningskonfigurationer. När du väljer en import av flera lager är följande alternativ tillgängliga i verktygsfältet.

   * [!UICONTROL Edit]: Redigera den valda konfigurationen.
   * [!UICONTROL Delete]: Ta bort den valda konfigurationen.
   * [!UICONTROL Check]: Validera anslutningen till datalagret.
   * [!UICONTROL Dry Run]: Anropa en testkörning av massintagning.
   * [!UICONTROL Run]: Kör den valda konfigurationen.
   * [!UICONTROL Stop]: Avsluta en aktiv konfiguration.
   * [!UICONTROL Schedule]: Ställ in engångs- eller återkommande schema för att importera resurser.
   * [!UICONTROL Job Status]: Visa konfigurationsstatus när den används i ett pågående importjobb eller används för ett slutfört jobb.
   * [!UICONTROL Job History]: Tidigare instanser av jobbet.
   * [!UICONTROL View Assets]: Visa målmappen om den finns.

   ![Alternativ i verktygsfältet för inmatningskonfigurationer](assets/bulk-ingest-toolbar-options.png)

Så här schemalägger du en engångsimport eller en återkommande bulkimport:

1. Skapa en bulkimportkonfiguration.
1. Markera konfigurationen och välj **[!UICONTROL Schedule]** i verktygsfältet.
1. Ställ in ett engångsintag eller schemalägg ett timschema, ett dagligt eller ett veckoschema. Klicka på **[!UICONTROL Submit]**.

   ![Schemalägg massinmatningsjobb](assets/bulk-ingest-schedule1.png)

## Överför resurser med skrivbordsklienter {#upload-assets-desktop-clients}

Förutom webbläsarens användargränssnitt har [!DNL Experience Manager] stöd för andra klienter på skrivbordet. De ger också en uppladdningsupplevelse utan att du behöver gå till webbläsaren.

* [[!DNL Adobe Asset Link]](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html) ger åtkomst till material från  [!DNL Experience Manager] Adobe Photoshop, Adobe Illustrator och Adobe InDesign. Du kan överföra det öppna dokumentet till [!DNL Experience Manager] direkt från användargränssnittet Adobe Asset Link från dessa skrivbordsprogram.
* [[!DNL Experience Manager] datorprogram ](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html) gör det enklare att arbeta med resurser på datorn, oberoende av filtyp eller vilket ursprungsprogram som hanterar dem. Det är särskilt användbart att överföra filer i kapslade mapphierarkier från det lokala filsystemet, eftersom webbläsaröverföring bara stöder överföring av platta fillistor.

## Bearbeta resurser när {#process-when-uploaded} överförs

För att kunna utföra ytterligare bearbetning av de överförda resurserna kan du använda bearbetningsprofiler på överförda mappar. Profilerna är tillgängliga på sidan **[!UICONTROL Properties]** i en mapp i [!DNL Assets]. En digital resurs utan ett tillägg eller med ett felaktigt tillägg bearbetas inte som du vill. När du till exempel överför sådana resurser händer ingenting eller så kan en felaktig bearbetningsprofil gälla för resursen. Användarna kan fortfarande lagra de binära filerna i DAM.

![Egenskaper för en resursmapp med alternativ för att lägga till en bearbetningsprofil](assets/assets-folder-properties.png)

Följande flikar är tillgängliga:

* [Med ](metadata-profiles.md) metadataprofiler kan du använda standardmetadataegenskaper för resurser som överförs till den mappen.
* [Genom att bearbeta ](asset-microservices-configure-and-use.md) profiler kan du generera fler återgivningar än vad som är möjligt som standard.

Om [!DNL Dynamic Media] är aktiverat i din distribution är dessutom följande flikar tillgängliga:

* [[!DNL Dynamic Media] Med ](dynamic-media/image-profiles.md) bildprofiler kan du tillämpa en särskild beskärningskonfiguration (**[!UICONTROL Smart Cropping]** och pixelbeskärning) och skärpekonfiguration på de överförda resurserna.
* [[!DNL Dynamic Media] Med ](dynamic-media/video-profiles.md) videoprofiler kan du använda särskilda videokodningsprofiler (upplösning, format, parametrar).

>[!NOTE]
>
>[!DNL Dynamic Media] Beskärning och andra åtgärder för resurser är icke-förstörande, vilket innebär att åtgärderna inte ändrar det överförda originalet. I stället innehåller det parametrar som ska beskäras eller omformas när resurserna levereras.

För mappar som har en tilldelad bearbetningsprofil visas profilnamnet på miniatyrbilden i kortvyn. I listvyn visas profilnamnet i kolumnen **[!UICONTROL Processing Profile]**.

## Överför eller importera resurser med API:er {#upload-using-apis}

Teknisk information om överförings-API:erna och -protokollet samt länkar till öppen källkod-SDK och exempelklienter finns i [avsnittet för överföring av resurser](developer-reference-material-apis.md#asset-upload) i utvecklarreferensen.

## Tips, metodtips och begränsningar {#tips-limitations}

* Direkt binär överföring är en ny metod för att överföra resurser. Det stöds som standard av produktfunktioner och klienter, som [!DNL Experience Manager] användargränssnitt, [!DNL Adobe Asset Link] och [!DNL Experience Manager]-skrivbordsprogram. All anpassad kod som anpassas eller utökas av kundens tekniska team måste använda de nya API:erna och protokollen för överföring.

* Adobe rekommenderar att du lägger till högst 1 000 resurser i varje mapp i [!DNL Experience Manager Assets]. Du kan lägga till fler resurser i en mapp, men det kan hända att du får prestandaproblem, till exempel långsammare navigering i sådana mappar.

* När du väljer **[!UICONTROL Replace]** i dialogrutan [!UICONTROL Name Conflict] genereras resurs-ID om för den nya resursen. Detta ID skiljer sig från ID:t för föregående resurs. Om [Resursinsikter](/help/assets/assets-insights.md) är aktiverat för att spåra visningar eller klickningar med [!DNL Adobe Analytics] blir det återskapade resurs-ID:t ogiltigt för de data som hämtats för resursen på [!DNL Analytics].

* Vissa överföringsmetoder hindrar dig inte från att överföra resurser med [förbjudna tecken](#filename-handling) i filnamnen. Tecknen ersätts med symbolen `-`.

* När du överför resurser med webbläsaren stöds endast platta fillistor och inte kapslade mapphierarkier. Om du vill överföra alla resurser i en kapslad mapp bör du använda [skrivbordsapp](#upload-assets-desktop-clients).

<!-- TBD: Link to file name handling in DA docs when it is documented. 
-->

>[!MORELIKETHIS]
>
>* [[!DNL Adobe Experience Manager] datorprogram](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html)
>* [Om [!DNL Adobe Asset Link]](https://www.adobe.com/creativecloud/business/enterprise/adobe-asset-link.html)
>* [[!DNL Adobe Asset Link] dokumentation](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html)
>* [Teknisk referens för överföring av tillgångar](developer-reference-material-apis.md#asset-upload)


---
title: Hantera videomaterial
description: Överför, förhandsgranska, kommentera och publicera videomaterial i  [!DNL Adobe Experience Manager].
contentOwner: AG
feature: Asset Management, Publishing, Collaboration, Video
role: User
exl-id: 91edce4a-dfa0-4eca-aba7-d41ac907b81e
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '4643'
ht-degree: 5%

---

# Hantera videomaterial {#manage-video-assets}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/managing-video-assets.html?lang=sv-SE) |
| AEM as a Cloud Service | Den här artikeln |

Videoformatet är en viktig del av ett företags digitala resurser. [!DNL Adobe Experience Manager] erbjuder mogna erbjudanden och funktioner för att hantera hela livscykeln för dina videoresurser efter att de har skapats.

Lär dig hur du hanterar och redigerar videoresurserna i [!DNL Adobe Experience Manager Assets]. Videokodning och omkodning, till exempel FFmpeg-omkodning, är möjlig med Bearbeta profiler och med integrering med [!DNL Dynamic Media]. Utan licensen för [!DNL Dynamic Media] tillhandahåller [!DNL Experience Manager] grundläggande stöd för videor, till exempel omkodning med hjälp av MPEG, extrahering av förhandsvisningsminiatyrer för de filformat som stöds och förhandsgranskning i användargränssnittet för format som stöds för direktuppspelning i webbläsaren.

## Överföra och förhandsgranska videomaterial {#upload-and-preview-video-assets}

Du kan överföra och förhandsgranska videoresurser i ett format som stöds till [!DNL Experience Manager Assets].
<!-- It generates previews for video assets with the extension MP4. -->

### Ladda upp videomaterial

Så här överför du en videoresurs:

1. I mappen eller undermapparna för digitala resurser går du till den plats där du behöver lägga till resursen.
1. Klicka på **[!UICONTROL Create]** i verktygsfältet och välj **[!UICONTROL Files]**. <br>Du kan också dra en fil till användargränssnittet.
Läs mer om att [överföra resurser](manage-digital-assets.md#uploading-assets) i [!DNL Experience Manager Assets].

<!-- 1. To preview a video in the card view, click the **[!UICONTROL Play]** ![play option](assets/do-not-localize/play.png) option on the video asset. You can pause or play video in the card view only. The [!UICONTROL Play] and [!UICONTROL Pause] options are not available in the list view.
1. To preview the video in the asset details page, select **[!UICONTROL Edit]** on the card. The video plays in the native video player of the browser. You can play, pause, control the volume, and zoom the video to full screen. -->

### Förhandsgranska videomaterial

Du kan förhandsgranska videoklipp i återgivningar som stöds i användargränssnittet för [!DNL Assets]. Så här förhandsgranskar du en videoresurs:

1. Överför en videoresurs i ett format som stöds till [!DNL Experience Manager Assets]. Läs mer om de [videoformat som stöds](file-format-support.md#video-formats). <br>När videoresursen har överförts bearbetas den och en förhandsvisningsåtergivning genereras.
1. Klicka på resursen och välj ![informationsalternativet](assets/do-not-localize/details_icon.svg) **[!UICONTROL Details]** i det övre verktygsfältet. Videoresursen öppnas i videovisningsprogrammet.
1. Klicka på ikonen ![uppspelningsalternativ](assets/do-not-localize/play.png) på videominiatyrbilden. <br>Du kan spela upp, pausa, styra volymen och zooma videon till helskärm.

För befintliga videoresurser i [!DNL Experience Manager Assets] måste du **[!UICONTROL Reprocess]** resurserna i [!DNL Experience Manager] för att aktivera funktionen för förhandsgranskning av video. Lär dig hur du [bearbetar om digitala resurser](reprocessing.md) i [!DNL Experience Manager].

### Begränsningar för förhandsgranskning av video

* MXF-filer visar inte videoförhandsvisningar trots att återgivningen genereras.
* WebM-filer genererar inte förhandsvisningsåtergivningar eftersom de kan spelas upp i webbläsare.

## Publicera videomaterial {#publish-video-assets}

Efter publiceringen kan du inkludera videomaterialet på en webbsida som en URL eller bädda in resurserna direkt. Mer information finns i [publicera [!DNL Dynamic Media] resurser](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

## Publicera videor på YouTube {#publishing-videos-to-youtube}

Du kan publicera videoresurser som hanteras i Experience Manager Assets direkt till en YouTube-kanal som du tidigare har skapat.

Om du vill publicera videoresurser på YouTube taggar du videoresurser i Experience Manager Assets med taggar. Du kopplar dessa taggar till en YouTube-kanal. Om videoresursens tagg matchar taggen för en YouTube-kanal publiceras videon till YouTube. Publicera till YouTube sker tillsammans med en normal publicering av videon så länge en associerad tagg används.

YouTube gör sin egen kodning. Den ursprungliga videofilen som överfördes till Experience Manager publiceras till YouTube i stället för den videoåtergivning som Dynamic Medias kodning har skapat. Även om det inte krävs för att bearbeta videofilmer med Dynamic Media, förväntas de göra det om en visningsförinställning behövs för uppspelning.

När du åsidosätter videobearbetningsprofilen och publicerar direkt till YouTube innebär det helt enkelt att videomaterialet i Experience Manager Asset inte får någon miniatyrbild som kan visas. Det innebär också att videoklipp som inte är kodade inte fungerar med någon av resurstyperna för dynamiska media.

När du publicerar videomaterial till YouTube-servrar utför du följande uppgifter för att säkerställa säker server-till-server-verifiering med YouTube:

1. [Konfigurera inställningar för Google Cloud](#configuring-google-cloud-settings)
1. [Create a YouTube channel](#creating-a-youtube-channel)
1. [Lägga till taggar för publicering](#adding-tags-for-publishing)
1. [Konfigurera YouTube i Experience Manager](#setting-up-youtube-in-aem)
1. [(Valfritt) Automatisera inställningen av YouTube standardegenskaper för överförda videofilmer](#optional-automating-the-setting-of-default-youtube-properties-for-your-uploaded-videos)
1. [Publicera videor i din YouTube-kanal](#publishing-videos-to-your-youtube-channel)
1. [(Valfritt) Verifiera den publicerade videon på YouTube](/help/assets/dynamic-media/video.md#optional-verifying-the-published-video-on-youtube)
1. [Länka YouTube URL:er till ditt webbprogram](#linking-youtube-urls-to-your-web-application)

Du kan även [avpublicera videoklipp för att ta bort dem från YouTube](#unpublishing-videos-to-remove-them-from-youtube).

### Konfigurera inställningar för Google Cloud {#configuring-google-cloud-settings}

Du behöver ett Google-konto för att kunna publicera till YouTube. Om du har ett GMAIL-konto har du redan ett Google-konto. Om du inte har något Google-konto kan du enkelt skapa ett. Du behöver kontot eftersom du behöver inloggningsuppgifter för att publicera videoresurser på YouTube. <!-- hidden March 3 2022 If you have an account already created, then skip this task and proceed directly to [Create a YouTube channel](#creating-a-youtube-channel). -->

Kontot som används med Google Cloud och Google-kontot som används för YouTube behöver inte vara samma.

Google ändrar regelbundet användargränssnittet. Stegen för att publicera videofilmer till YouTube kan därför variera något från vad som beskrivs nedan. Denna caveat gäller även YouTube när du försöker kontrollera om videoklipp har överförts till det.

>[!NOTE]
>
>Följande steg var korrekta vid skrivandet. Google uppdaterar dock regelbundet sina webbsidor i molnet utan föregående meddelande. Därför kan vissa konfigurationsalternativ namnges något annorlunda i Google användargränssnitt jämfört med det namn som används i stegen.

**Så här konfigurerar du Google Cloud-inställningar:**

1. Skapa ett Google-konto.

   Om du redan har ett Google-konto kan du gå vidare till nästa steg.

1. Gå till [https://cloud.google.com/](https://cloud.google.com/).
1. På sidan **[!UICONTROL Google Cloud]**, nära det övre högra hörnet, väljer du **[!UICONTROL Console]**.

   Om det behövs använder **[!UICONTROL Sign in]** dina Google-kontouppgifter för att se alternativet **[!UICONTROL Console]**.

1. På sidan **[!UICONTROL Dashboard]**, till höger om **[!UICONTROL Google Cloud Platform]**, väljer du listrutan **[!UICONTROL Project]** för att öppna dialogrutan **[!UICONTROL Select a project]**.
1. Välj **[!UICONTROL New Project]** i dialogrutan **[!UICONTROL Select a project]**.
1. Skriv namnet på det nya projektet i fältet **[!UICONTROL Project name]** i dialogrutan **[!UICONTROL New Project]**.

   Ditt projekt-ID baseras på ditt projektnamn. Välj därför projektnamnet noggrant. Det går inte att ändra det efter att det har skapats. Du måste även ange samma projekt-ID igen när du konfigurerar YouTube i Experience Manager senare. Skriv därför ned den.

1. Välj **[!UICONTROL Create]**.

1. Gör något av följande:

   * Välj **[!UICONTROL Explore and enable APIs]** på ditt projekts Dashboard på **[!UICONTROL Getting Started]**-kortet.
   * Välj **[!UICONTROL Go to APIs overview]** på ditt projekts Dashboard på **[!UICONTROL APIs]**-kortet.

1. Välj **[!UICONTROL ENABLE APIS AND SERVICES]** i mitten av sidan **[!UICONTROL APIs & Services]**.<!-- NEXT STEP BELOW IS STEP 10 -->
1. På sidan **[!UICONTROL API Library]**, till vänster, under **[!UICONTROL Category]**, väljer du **[!UICONTROL YouTube]**. Välj **[!UICONTROL YouTube]** till höger på sidan.
1. Välj **[!UICONTROL YouTube Data API v3]** på sidan **[!UICONTROL YouTube]**.
1. Välj **[!UICONTROL MANAGE]** på sidan **[!UICONTROL YouTube Data API v3]**.

   ![6_5_googleaccount-apis-manage](/help/assets/dynamic-media/assets/6_5_googleaccount-apis-manage.png)

1. Om du vill använda API:t måste du ha autentiseringsuppgifter. Om det behövs väljer du **[!UICONTROL Credentials]** till vänster på sidan **[!UICONTROL APIs & Services]**.
1. På sidan **[!UICONTROL Credentials]**, nära överkanten, väljer du **[!UICONTROL CREATE CREDENTIALS]** och sedan **[!UICONTROL OAuth client ID]**.
1. På sidan **[!UICONTROL Create OAuth client ID]** väljer du **[!UICONTROL Web application]** i listrutan **[!UICONTROL Application type]**.

   ![6_5_googleaccount-apis-applicationtype](/help/assets/dynamic-media/assets/6_5_googleaccount-apis-applicationtype.png)

1. Gör något av följande:

   * I fältet **[!UICONTROL Name]** anger du ett unikt namn för din OAuth 2.0-klient.
   * Använd det standardnamn som Google redan har angett i fältet **[!UICONTROL Name]**.

1. Välj **[!UICONTROL ADD URI]** under rubriken **[!UICONTROL Authorized JavaScript origins]**.

   ![6_5_googleaccount-apis-namepermissions](/help/assets/dynamic-media/assets/6_5_googleaccount-apis-nameauthorizations.png)

1. Ange följande sökväg i textfältet **[!UICONTROL URIs]**, ersätt din egen domän och portnummer i sökvägen och tryck sedan på **[!UICONTROL Enter]** för att lägga till sökvägen i listan:

   `https://<servername.domain>:<port_number>`

   Exempel: `https://1a2b3c.mycompany.com:4321`

   >[!NOTE]
   >
   >URI-sökvägsexemplet ovan är hypotetiskt och endast i förklaringssyfte.

1. Välj ADD URI under rubriken **[!UICONTROL Authorized redirect URIs]**.
1. Ange följande sökväg i textfältet **[!UICONTROL URIs]**, ersätt din egen domän och portnummer i sökvägen och tryck sedan på **[!UICONTROL Enter]** för att lägga till sökvägen i listan:

   `https://<servername.domain>:<port_number>/etc/cloudservices/youtube.youtubecredentialcallback.json`

   Exempel: `https://1a2b3c.mycompany.com:4321/etc/cloudservices/youtube.youtubecredentialcallback.json`

   >[!NOTE]
   >
   >URI-sökvägsexemplet ovan är hypotetiskt och endast i förklaringssyfte.

1. Välj **[!UICONTROL Create]** längst ned på sidan **[!UICONTROL Create OAuth client ID]**.
1. Gör följande i dialogrutan **[!UICONTROL OAuth client created]**:

   * (Valfritt) Kopiera värdena i fälten **[!UICONTROL Your Client ID]** och **[!UICONTROL Your Client Secret]** och spara.
   * Välj **[!UICONTROL DOWNLOAD JSON]** och spara sedan JSON-filen.

   Du behöver den här hämtade JSON-filen när du konfigurerar YouTube i Adobe Experience Manager senare.

   ![6_5_googleaccount-apis-authclientcreated](/help/assets/dynamic-media/assets/6_5_googleaccount-apis-oauthclientcreated.png)

1. Välj **[!UICONTROL OK]** i dialogrutan **[!UICONTROL OAuth client created]**.
1. Logga ut från ditt Google-konto. Skapa nu en YouTube-kanal.

### Create a YouTube channel {#creating-a-youtube-channel}

Du måste ha en eller flera kanaler för att kunna publicera videofilmer på YouTube. Om du redan har skapat en YouTube-kanal kan du hoppa över den här uppgiften och gå till [Lägg till taggar för publicering](/help/assets/dynamic-media/video.md#adding-tags-for-publishing).

>[!CAUTION]
>
>Kontrollera att du redan har konfigurerat en eller flera kanaler i YouTube *innan* du lägger till kanaler under YouTube-inställningar i Experience Manager (se [Konfigurera YouTube i Experience Manager](#setting-up-youtube-in-aem) nedan). Om du inte gör kanalinställningarna får du ingen varning om att det inte finns några befintliga kanaler. Google-verifiering sker dock fortfarande när du lägger till en kanal, men det finns inget alternativ för att välja vilken kanal videon ska skickas till.

**Så här skapar du en YouTube-kanal:**

1. Gå till [https://www.youtube.com](https://www.youtube.com/) och logga in med autentiseringsuppgifterna för ditt Google-konto.
1. I det övre högra hörnet av YouTube-sidan markerar du din profilbild (den kan också visas som en bokstav i en enfärgad cirkel) och väljer sedan **[!UICONTROL YouTube settings]** (den runda kugghjulsikonen).
1. Välj **[!UICONTROL See all my channels or create a channel]** på sidan Översikt under rubriken Ytterligare funktioner.
1. Välj **[!UICONTROL Create a new channel]** på sidan Kanaler.
1. På sidan Varumärkeskonto anger du ett företagsnamn eller ett annat kanalnamn som du väljer där du vill publicera videoresurserna i fältet Namn på varumärkeskonto och väljer sedan **[!UICONTROL Create]**.

   Kom ihåg namnet som du anger här. Du måste ange det igen när du måste konfigurera YouTube i Experience Manager.

1. (Valfritt) Lägg till fler kanaler om det behövs.

   Nu lägger du till taggar för publicering.

### Lägga till taggar för publicering {#adding-tags-for-publishing}

Experience Manager kopplar taggar till en eller flera YouTube-kanaler för att publicera dem till dina videofilmer på YouTube. Mer information om hur du lägger till taggar för publicering finns i [Administrera taggar](/help/sites-cloud/authoring/sites-console/tags.md).

Om du tänker använda standardtaggarna i Experience Manager kan du hoppa över den här uppgiften och gå till [Konfigurera YouTube i Experience Manager](#setting-up-youtube-in-aem).

>[!NOTE]
>
>När Cloud Service har konfigurerats krävs ingen annan konfiguration för att aktivera YouTube Publish-replikeringsagenten. Orsaken är att den aktiverades när Cloud Service-konfigurationen sparades.

<!-- ### Enabling the YouTube Publish replication agent {#enabling-the-youtube-publish-replication-agent}

After you enable the YouTube Publish replication agent, if you want to test the connection to the Google Cloud account, select **[!UICONTROL Test Connection]**. A browser tab displays the connection results. If you have added YouTube Channels, then a listing of those is displayed as part of the test.

1. In the upper-left corner of Experience Manager, select the Experience Manager logo, then in the left rail, navigate to **[!UICONTROL Tools]** > **[!UICONTROL Deployment]** > **[!UICONTROL Replication]** > **[!UICONTROL Agents on Author]**.
1. On the Agents of Author page, select **[!UICONTROL YouTube Publish (youtube)]**.
1. On the toolbar, to the right of Settings, select **[!UICONTROL Edit]**.
1. Select the **[!UICONTROL Enabled]** checkbox to turn on the replication agent.
1. Select **[!UICONTROL OK]**. -->

### Konfigurera YouTube i Experience Manager {#setting-up-youtube-in-aem}

Från och med Experience Manager 6.4 introducerades en ny pekgränssnittsmetod för att konfigurera YouTube-publicering i Experience Manager. Baserat på den installerade instansen av Experience Manager som du använder gör du något av följande:

* Information om hur du konfigurerar YouTube i Experience Manager före 6.4 finns i [Konfigurera YouTube i Experience Manager före 6.4](/help/assets/dynamic-media/video.md#setting-up-youtube-in-aem-before).
* Information om hur du konfigurerar YouTube i Experience Manager 6.4 eller senare finns i [Konfigurera YouTube i Experience Manager 6.4 och senare](#setting-up-youtube-in-aem-and-later).

#### Konfigurera YouTube i Experience Manager 6.4 och senare {#setting-up-youtube-in-aem-and-later}

1. Se till att du loggar in på din instans av Dynamic Media som administratör.
1. I det övre vänstra hörnet av Experience Manager väljer du Experience Manager logotyp och navigerar sedan till **[!UICONTROL Tools]**(hammikon) > **[!UICONTROL Cloud Services]** > **[!UICONTROL YouTube Publishing Configuration]** i den vänstra listen.
1. Välj **[!UICONTROL global]** (markera inte det).

1. Välj **[!UICONTROL Create]** i det övre högra hörnet på den globala sidan.
1. På sidan Skapa YouTube-konfiguration anger du Googles projekt-ID under Inställningar för Google Cloud-plattform i fältet **[!UICONTROL Application Name]**.

   Du angav projekt-ID:t när du konfigurerade Google Cloud-inställningarna tidigare.
Lämna sidan Skapa YouTube-konfiguration öppen. Du kommer tillbaka till den om en stund.

   ![6_5_youtubepublish-createUtubeConfiguration](/help/assets/dynamic-media/assets/6_5_youtubepublish-createyoutubeconfiguration.png)

1. Öppna JSON-filen som du hämtade och sparade tidigare i aktiviteten [Konfigurera Google Cloud-inställningar](/help/assets/dynamic-media/video.md#configuring-google-cloud-settings) med en vanlig textredigerare.
1. Markera och kopiera hela JSON-texten.
1. Återgå till dialogrutan YouTube-kontoinställningar Klistra in JSON-texten i fältet **[!UICONTROL JSON Config]**.
1. Välj **[!UICONTROL Save]** i sidans övre högra hörn.

   Konfigurera nu YouTube-kanaler i Experience Manager.

1. Välj **[!UICONTROL Add Channel]**.
1. I fältet Kanalnamn anger du namnet på kanalen som du skapade i aktiviteten **[!UICONTROL Adding one or more channels to YouTube]** tidigare.

   Om du vill kan du lägga till en beskrivning.

1. Välj **[!UICONTROL Add]**.
1. YouTube/Google-verifiering visas. Om du inte redan är inloggad på Google Cloud-kontot hoppar du över det här steget.

   * Ange det användarnamn och lösenord för Google som är kopplat till Google projekt-ID och JSON-texten ovan.
   * Beroende på hur många kanaler ditt konto har visas två eller flera objekt. Välj en kanal. Markera inte e-postadressen, den är inte en kanal.
   * På nästa sida väljer du **[!UICONTROL Accept]** för att tillåta åtkomst till den här kanalen.

1. Välj **[!UICONTROL Allow]**.

   Konfigurera taggar för publicering.

1. **[!UICONTROL Setting up tags for publishing]** - På sidan Molntjänster > YouTube väljer du pennikonen för att redigera listan med taggar som du vill använda.
1. Om du vill visa en lista med tillgängliga taggar i Experience Manager väljer du listruteikonen (cirkumflex upp och ned).
1. Om du vill lägga till dem markerar du en eller flera taggar.

   Om du vill ta bort en tagg som du har lagt till markerar du den och väljer **[!UICONTROL X]**.

1. När du är klar med att lägga till de taggar du vill ha väljer du **[!UICONTROL Save]**.

   Nu kan du publicera videor i din YouTube-kanal.

#### Konfigurera YouTube i Experience Manager före 6.4 {#setting-up-youtube-in-aem-before}

1. Se till att du loggar in på din instans av Dynamic Media som administratör.

1. I det övre vänstra hörnet av Experience Manager väljer du Experience Manager logotyp och navigerar sedan till **[!UICONTROL Tools]** (hammarikon) > **[!UICONTROL Deployment]** > **[!UICONTROL Cloud Services]** i den vänstra listen.
1. Välj **[!UICONTROL Configure now]** under Tredjepartstjänster, under YouTube.
1. I dialogrutan Skapa konfiguration anger du en rubrik (obligatoriskt) och ett namn (valfritt) i respektive fält.
1. Välj **[!UICONTROL Create]**.
1. I dialogrutan YouTube-kontoinställningar anger du Googles projekt-ID i fältet **[!UICONTROL Application Name]**.

   Du angav projekt-ID:t när du [konfigurerade Google Cloud-inställningarna](/help/assets/dynamic-media/video.md#configuring-google-cloud-settings) tidigare.
Lämna dialogrutan YouTube Kontoinställning öppen. Du kommer tillbaka till den om en stund.

1. Använd en vanlig textredigerare för att öppna JSON-filen som du hämtade och sparade tidigare i uppgiften Konfigurera inställningar för Google Cloud.
1. Markera och kopiera hela JSON-texten.
1. Återgå till dialogrutan YouTube-kontoinställningar Klistra in JSON-texten i fältet **[!UICONTROL JSON Config]**.
1. Välj **[!UICONTROL OK]**.

   Konfigurera nu YouTube-kanaler i Experience Manager.

1. Till höger om **[!UICONTROL Available Channels]** väljer du **+** (plusteckenikon).
1. I dialogrutan YouTube-kanalinställningar, i fältet Titel, anger du namnet på kanalen som du skapade i uppgiften **[!UICONTROL Adding one or more channels to YouTube]** tidigare.

   Om du vill kan du lägga till en beskrivning.

1. Välj **[!UICONTROL OK]**.
1. YouTube/Google-verifiering visas. Om du inte redan är inloggad på Google Cloud-kontot hoppar du över det här steget.

   * Ange det användarnamn och lösenord för Google som är kopplat till Google projekt-ID och JSON-texten ovan.
   * Beroende på hur många kanaler ditt konto har visas två eller flera objekt. Välj en kanal. Markera inte e-postadressen, den är inte en kanal.
   * På nästa sida väljer du **[!UICONTROL Accept]** för att tillåta åtkomst till den här kanalen.

1. Välj **[!UICONTROL Allow]**.

   Konfigurera taggar för publicering.

1. **[!UICONTROL Setting up tags for publishing]** - På sidan Molntjänster > YouTube väljer du pennikonen för att redigera listan med taggar som du vill använda.
1. Om du vill visa en lista med tillgängliga taggar i Experience Manager väljer du listruteikonen (cirkumflex upp och ned).
1. Om du vill lägga till dem markerar du en eller flera taggar.

   Om du vill ta bort en tagg som du har lagt till markerar du den och väljer **X**.

1. När du är klar med att lägga till de taggar du vill ha väljer du **[!UICONTROL OK]**.

   Nu kan du publicera videor i din YouTube-kanal.

### (Valfritt) Automatisera inställningen av YouTube standardegenskaper för överförda videofilmer {#optional-automating-the-setting-of-default-youtube-properties-for-your-uploaded-videos}

Du kan även automatisera inställningen av YouTube-egenskaper när du överför videoklipp. Skapa en metadatabearbetningsprofil i Experience Manager.

Om du vill skapa en profil för metadatabearbetning kopierar du först värden från fälten **[!UICONTROL Field Label]**, **[!UICONTROL Map to property]** och **[!UICONTROL Choices]**, som alla finns i metadatascheman för video. Sedan skapar du en YouTube-metadatabearbetningsprofil för video genom att lägga till dessa värden.

**Så här automatiserar du inställningen av YouTube standardegenskaper för dina överförda videofilmer:**

1. I det övre vänstra hörnet av Experience Manager väljer du Experience Manager logotyp och navigerar sedan till **[!UICONTROL Tools]** (hammarikon) > **[!UICONTROL Assets]** > **[!UICONTROL Metadata Schemas]** i den vänstra listen.
1. Välj **[!UICONTROL default]**. (Lägg inte till en bockmarkering i markeringsrutan till vänster om &quot;standard&quot;.)
1. Markera rutan till vänster om **[!UICONTROL video]** på sidan **[!UICONTROL default]** och välj sedan **[!UICONTROL Edit]**.
1. Välj fliken **[!UICONTROL Advanced]** på sidan Redigerare för metadatamodeller.
1. Välj **[!UICONTROL YouTube Category]** under rubriken YouTube Publishing.
1. Till höger på sidan, under fliken **[!UICONTROL Settings]**, gör du följande:

   * Markera och kopiera värdet i textfältet **[!UICONTROL Map to property]**.
Klistra in det kopierade värdet i textredigeraren. Du kommer att behöva det här värdet senare när du skapar din metadatabearbetningsprofil. Låt textredigeraren vara öppen.

   * Under **[!UICONTROL Choices]** markerar och kopierar du standardvärdet som du vill använda (till exempel Folk &amp; bloggar eller Vetenskap och teknik).
Klistra in det kopierade värdet i textredigeraren. Du kommer att behöva det här värdet senare när du skapar din metadatabearbetningsprofil. Låt textredigeraren vara öppen.

1. Välj **[!UICONTROL YouTube Privacy]** under rubriken YouTube Publishing.
1. Till höger på sidan, under fliken **[!UICONTROL Settings]**, gör du följande:

   * Markera och kopiera värdet i textfältet **[!UICONTROL Map to property]**.
Klistra in det kopierade värdet i textredigeraren. Du kommer att behöva det här värdet senare när du skapar din metadatabearbetningsprofil. Låt textredigeraren vara öppen.

   * Under **[!UICONTROL Choices]** markerar och kopierar du standardvärdet som du vill använda. Observera att alternativen grupperas i par om två. Det undre fältet i paret är standardvärdet som du vill kopiera, till exempel public, unlisted eller private.
Klistra in det kopierade värdet i textredigeraren. Du kommer att behöva det här värdet senare när du skapar din metadatabearbetningsprofil. Låt textredigeraren vara öppen.

1. Välj **[!UICONTROL Cancel]** i det övre högra hörnet på sidan för redigeringsprogram för metadatamatchning.
1. I det övre vänstra hörnet av Experience Manager väljer du Experience Manager logotyp och sedan väljer du **[!UICONTROL Tools]** (hammikon) > **[!UICONTROL Assets]** > **[!UICONTROL Metadata Profiles]** i den vänstra listen.

1. Välj **[!UICONTROL Create]** på sidan Metadataprofiler, i det övre högra hörnet på sidan.
1. I dialogrutan Lägg till metadataprofil anger du namnet `YouTube Video` i textfältet **[!UICONTROL Profile title]** och väljer sedan **[!UICONTROL Create]**.
1. Välj fliken **[!UICONTROL Advance]** på sidan för metadataprofilredigeraren.
1. Lägg till de kopierade YouTube Publishing-värdena i profilen genom att göra följande:

   * Välj fliken **[!UICONTROL Build Form]** till höger på sidan.
   * (Valfritt) Dra komponenten **[!UICONTROL Section Header]** till vänster och släpp den i formulärområdet.
   * (Valfritt) Markera **[!UICONTROL Field Label]** om du vill markera komponenten.
   * (Valfritt) Skriv `YouTube Publishing` till höger på sidan under fliken Inställningar i textfältet Fältetikett.
   * Välj fliken **[!UICONTROL Build Form]** och dra sedan komponenten **[!UICONTROL Multi Value Text]** och släpp den under rubriken **[!UICONTROL YouTube Publishing]** som du skapade.

   * Markera komponenten genom att välja **[!UICONTROL Field Label]**.
   * Till höger på sidan, under fliken Inställningar, klistrar du in de YouTube Publishing-värden (Field Label-värde och Map to property-värde) som du kopierade tidigare i deras respektive fält i formuläret. Klistra in alternativvärdet i fältet Standardvärde.

1. Lägg till de kopierade sekretessvärdena för YouTube till profilen genom att göra följande:

   * Välj fliken **[!UICONTROL Build Form]** till höger på sidan.
   * (Valfritt) Dra komponenten **[!UICONTROL Section Header]** till vänster och släpp den i formulärområdet.
   * (Valfritt) Markera **[!UICONTROL Field Label]** om du vill markera komponenten.
   * (Valfritt) Skriv `YouTube Privacy` till höger på sidan under fliken Inställningar i textfältet Fältetikett.
   * Välj fliken **[!UICONTROL Build Form]**, dra sedan komponenten **[!UICONTROL Multi Value Text]** och släpp den under rubriken **[!UICONTROL YouTube Privacy]** som du skapade.

   * Markera komponenten genom att välja **[!UICONTROL Field Label]**.
   * Till höger på sidan, under fliken Inställningar, klistrar du in de YouTube Publishing-värden (Field Label-värde och Map to property-värde) som du kopierade tidigare i deras respektive fält i formuläret. Klistra in alternativvärdet i fältet Standardvärde.

1. Välj **[!UICONTROL Save]** i sidans övre högra hörn.
1. Använd metadataprofilen för YouTube Publishing på de mappar där du ska överföra videoklipp. Du måste ha angett både Metadataprofil och Videoprofil.

   Se [Metadataprofiler](/help/assets/metadata-profiles.md) och [Videoprofiler](/help/assets/dynamic-media/video-profiles.md).

### Publicera videor i din YouTube-kanal {#publishing-videos-to-your-youtube-channel}

Nu kopplar du taggarna som du lade till tidigare till videoresurser. På så sätt får Experience Manager veta vilka mediefiler som ska publiceras i din YouTube-kanal.

>[!NOTE]
>
>Publicera direkt publicerar inte automatiskt till YouTube. När Dynamic Media har konfigurerats finns det två publiceringsalternativ att välja mellan, **[!UICONTROL Immediately]** och **[!UICONTROL Upon Activation]**.
>
>**[!UICONTROL Publish Immediately]** betyder att den överförda resursen, efter att den har synkroniserats med IPS-versionen, automatiskt publiceras till leveranssystemet. Det gäller Dynamic Media, men inte YouTube. Om du vill publicera till YouTube måste du publicera via Experience Manager Author.

>[!NOTE]
>
>Experience Manager använder arbetsflödet **[!UICONTROL Publish to YouTube]** för att publicera innehåll från YouTube, vilket gör att du kan övervaka förloppet och visa felinformation.
>
>Se [Övervaka videokodning och YouTube publiceringsförlopp](#monitoring-video-encoding-and-youtube-publishing-progress).
>
>Mer detaljerad förloppsinformation finns i YouTube-loggen som replikeras. Tänk dock på att sådan övervakning kräver administratörsåtkomst.

**Så här publicerar du videofilmer i din YouTube-kanal:**

1. I Experience Manager navigerar du till en videoresurs som du vill publicera i din YouTube-kanal.
1. Välj videoresurs (den adaptiva videouppsättningen).
1. Välj **[!UICONTROL Properties]** i verktygsfältet.
1. Välj **[!UICONTROL Open Selection Dialog]** till höger om fältet Taggar på fliken Grundläggande under rubriken Metadata.
1. På sidan Välj taggar navigerar du till de taggar du vill använda och markerar sedan en eller flera taggar.

   Kom ihåg att taggarna måste kopplas till YouTube-kanalen.

1. Välj **[!UICONTROL Select]** i det övre högra hörnet på sidan.
1. Välj **[!UICONTROL Save and Close]** i det övre högra hörnet på videons egenskapssida.
1. Välj **[!UICONTROL Quick Publish]** i verktygsfältet.

   Se även [Använd publikationshantering med Experience Manager Sites](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/page-authoring/publication-management-feature-video-use.html?lang=sv-SE#page-authoring).

   Du kan även verifiera den publicerade videon på din YouTube-kanal.

### (Valfritt) Verifiera den publicerade videon på YouTube {#optional-verifying-the-published-video-on-youtube}

Du kan också övervaka förloppet för din YouTube-publicering (eller avpublicering).

Se [Övervaka videokodning och YouTube publiceringsförlopp](#monitoring-video-encoding-and-youtube-publishing-progress).

Publiceringstiderna kan variera avsevärt beroende på olika faktorer, bland annat formatet för den primära källvideon, filstorleken och överföringstrafiken. Publiceringsprocessen kan ta från några minuter till flera timmar. Högre upplösningsformat återges dessutom mycket långsammare. 720p och 1080p tar till exempel längre tid att visa än 480p.

Efter åtta timmar, om du fortfarande ser ett statusmeddelande som säger **[!UICONTROL Uploaded (processing, please wait)]**, kan du försöka ta bort videon från webbplatsen och överföra den igen.

### Länka YouTube URL:er till ditt webbprogram {#linking-youtube-urls-to-your-web-application}

Du kan hämta en YouTube URL-sträng som genereras av Dynamic Media när du har publicerat videon. När du kopierar YouTube-URL:en markeras den i Urklipp så att du kan klistra in den på sidor på webbplatsen eller i programmet.

>[!NOTE]
>
>YouTube-URL:en kan inte kopieras förrän du har publicerat videoresursen till YouTube.

Så här länkar du YouTube URL:er till ditt webbprogram:

1. Navigera till den *YouTube-publicerade*-videoresurs vars URL du vill kopiera och markera den.

   Kom ihåg att YouTube URL:er endast är tillgängliga för kopiering av *efter* att du först *har publicerat* videomaterialet till YouTube.

1. Välj **[!UICONTROL Properties]** i verktygsfältet.
1. Välj fliken **[!UICONTROL Advanced]**.
1. Under rubriken YouTube Publishing (Publicering), i YouTube URL List, markerar och kopierar du URL-texten till webbläsaren för att förhandsgranska resursen eller lägga till den på webbinnehållssidan.

### Avpublicera videofilmer så att du kan ta bort dem från YouTube {#unpublishing-videos-to-remove-them-from-youtube}

När du avpublicerar en videoresurs i Experience Manager tas videon bort från YouTube.

>[!CAUTION]
>
>Om du tar bort en video direkt från YouTube är Experience Manager inte medveten om det och fortsätter att uppföra sig som om videon fortfarande publicerats till YouTube. Avpublicera alltid en videoresurs från YouTube via Experience Manager.

>[!NOTE]
>
>Experience Manager använder arbetsflödet **[!UICONTROL Unpublish from YouTube]** för att ta bort innehåll från YouTube, vilket gör att du kan övervaka förloppet och visa felinformation.
>
>Se [Övervaka videokodning och YouTube publiceringsförlopp](#monitoring-video-encoding-and-youtube-publishing-progress).

**Så här avpublicerar du videoklipp för att ta bort dem från YouTube:**

1. Navigera till de videoresurser som du vill avpublicera från din YouTube-kanal.
1. Välj en eller flera publicerade videoresurser i ett resursurvalsläge.
1. Välj **[!UICONTROL Manage Publication]** i verktygsfältet. Om det behövs väljer du ikonen med tre punkter (`. . .`) i verktygsfältet för att se **[!UICONTROL Manage Publication]**.
1. Välj **[!UICONTROL Unpublish]** på sidan Hantera publikation.
1. Välj **[!UICONTROL Next]** i det övre högra hörnet på sidan.
1. Välj **[!UICONTROL Unpublish]** i det övre högra hörnet på sidan.

## Övervaka videokodning och YouTube publiceringsförlopp {#monitoring-video-encoding-and-youtube-publishing-progress}

När du överför en ny video till en mapp där videokodning används eller publicerar videon till YouTube, ska du övervaka hur videokodningen/YouTube-publiceringen fortskrider (eller misslyckas). Det faktiska publiceringsförloppet för YouTube är endast tillgängligt via loggarna. Oavsett om det misslyckas eller lyckas visas det på andra sätt som beskrivs i följande procedur. Dessutom får du e-postmeddelanden när en YouTube-publiceringsarbetsgång eller videokodning har slutförts eller avbrutits.

### Övervaka förlopp {#monitoring-progress}

Du kan övervaka förloppet, inklusive misslyckad kodning/YouTube-publicering.

1. Visa videokodningsförloppet i resursmappen:

   * I kortvyn visas videokodningsförloppet för resursen i procent. Om ett fel uppstår visas även den här informationen på resursen.

   ![chlimage_1-429](/help/assets/dynamic-media/assets/chlimage_1-429.png)

   * I listvyn visas videokodningsförloppet i kolumnen **[!UICONTROL Processing Status]**. Om ett fel uppstår visas det här meddelandet i samma kolumn.

   ![chlimage_1-430](/help/assets/dynamic-media/assets/chlimage_1-430.png)

   Den här kolumnen visas inte som standard. Om du vill aktivera kolumnen väljer du **[!UICONTROL View Settings]** i listrutan Vyer, lägger till kolumnen **[!UICONTROL Processing Status]** och väljer **[!UICONTROL Update]**.

   ![chlimage_1-431](/help/assets/dynamic-media/assets/chlimage_1-431.png)

1. Visa förloppet i tillgångsinformationen. När du väljer en resurs öppnar du listrutan och väljer **[!UICONTROL Timeline]**. Om du vill begränsa det till arbetsflödesaktiviteter som kodning eller YouTube-publicering väljer du **[!UICONTROL Workflows]**.

   ![chlimage_1-432](/help/assets/dynamic-media/assets/chlimage_1-432.png)

   All arbetsflödesinformation, till exempel kodning, visas på tidslinjen. För YouTube-publicering innehåller tidslinjen för arbetsflödet även namnet på YouTube-kanalen och YouTube video-URL:en. Dessutom visas felmeddelanden på tidslinjen i arbetsflödet när publiceringen är klar.

   >[!NOTE]
   >
   >Det kan ta lång tid innan fel-/felmeddelanden slutligen spelas in på grund av flera arbetsflödeskonfigurationer på **[!UICONTROL retries]**, **[!UICONTROL retry delay]** och **[!UICONTROL timeout]** från [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr), till exempel:
   >
   >* Konfiguration av Apache Sling-jobbkö
   >* Extern processhanterare för Adobe Granite-arbetsflöde
   >* Timeoutkö för Granite-arbetsflöde
   >
   >Du kan justera egenskaperna **[!UICONTROL retries]**, **[!UICONTROL retry delay]** och **[!UICONTROL timeout]** i dessa konfigurationer.

1. Information om pågående arbetsflöden finns i Arbetsflödesinstanser som är tillgängliga i **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Instances]**.

   >[!NOTE]
   >
   >Du behöver administratörsbehörighet för att komma åt menyn **[!UICONTROL Tools]**.

   ![chlimage_1-433](/help/assets/dynamic-media/assets/chlimage_1-433.png)

   Markera instansen och välj **[!UICONTROL Open History]**.

   ![chlimage_1-434](/help/assets/dynamic-media/assets/chlimage_1-434.png)

   I området Arbetsflödesinstanser kan du även göra uppehåll i, avsluta eller byta namn på arbetsflöden. Mer information finns i [Administrera arbetsflöden](/help/sites-cloud/authoring/workflows/overview.md).

1. Information om misslyckade jobb finns i Arbetsflödesfel i **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Failures]**. I listan **[!UICONTROL Workflow Failure]** visas alla misslyckade arbetsflödesaktiviteter.

   >[!NOTE]
   >
   >Du behöver administratörsbehörighet för att komma åt menyn **[!UICONTROL Tools]**.

   ![chlimage_1-435](/help/assets/dynamic-media/assets/chlimage_1-435.png)

   >[!NOTE]
   >
   >Det kan ta lång tid innan felmeddelandet slutligen spelas in på grund av flera arbetsflödeskonfigurationer på **[!UICONTROL retries]**, **[!UICONTROL retry delay]** och **[!UICONTROL timeout]** från [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr), till exempel:
   >
   >* Konfiguration av Apache Sling-jobbkö
   >* Extern processhanterare för Adobe Granite-arbetsflöde
   >* Timeoutkö för Granite-arbetsflöde
   >
   >Du kan justera egenskaperna **[!UICONTROL retries]**, **[!UICONTROL retry delay]** och **[!UICONTROL timeout]** i dessa konfigurationer.

1. Information om slutförda arbetsflöden finns i Arbetsflödesarkiv som är tillgängligt från **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Archive]**. **[!UICONTROL Workflow Archive]** visar alla slutförda arbetsflödesaktiviteter.

   >[!NOTE]
   >
   >Du behöver administratörsbehörighet för att komma åt menyn **[!UICONTROL Tools]**.

   ![chlimage_1-436](/help/assets/dynamic-media/assets/chlimage_1-436.png)

1. Du får e-postmeddelanden om avbrutna eller misslyckade arbetsflödesjobb. Dessa e-postmeddelanden kan konfigureras av en administratör. Se [Konfigurera e-postmeddelanden](#configuring-e-mail-notifications).

<!-- EMAIL NOT AVAILABLE IN SKYLINE

#### Configuring e-mail notifications {#configuring-e-mail-notifications}

>[!NOTE]
>
>You may need administrative rights to access the **[!UICONTROL Tools]** menu.

How you configure notification depends on whether you want notifications for YouTube publishing jobs.

* For encoding jobs, you can access the configuration page for all Experience Manager workflow email notifications at **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]** and by searching for **[!UICONTROL Day CQ Workflow Email Notification Service]**. You can select or clear the check boxes for **[!UICONTROL Notify on Abort]** or **[!UICONTROL Notify on Complete]** accordingly.

For YouTube publishing jobs, do the following:

1. In Experience Manager, navigate to **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**.
1. On the Workflow Models page, select **[!UICONTROL Publish to YouTube]**, then select **[!UICONTROL Edit]** on the toolbar.
1. Near the upper-right corner of the Publish to YouTube workflow page, select **[!UICONTROL Edit]**.
1. Hover the mouse pointer on the YouTube Upload component, then select once to display the inline toolbar.

   ![6_5_publishtoyoutubeworkflow](assets/6_5_publishtoyoutubeworkflow.png)

1. On the inline toolbar, select the Configuration icon (wrench). Select the **[!UICONTROL Arguments]** tab.

   ![6_5_publishtoyoutubeworkflow-configurationicon](assets/6_5_publishtoyoutubeworkflow-configurationicon.png)

1. In the YouTube Upload Process - Step Properties dialog box, select the **[!UICONTROL Arguments]** tab.

   ![6_5_publishtoyoutubeworkflow-arguments-tab](assets/6_5_publishtoyoutubeworkflow-arguments-tab.png)

1. You can select or clear the following check boxes:

    * Publish Start
    * Publish Failure
    * Publish Completion - includes information on channels and URLs

   Clearing a check box means that you will not receive the specified email notification from the YouTube Publish workflow.

   >[!NOTE]
   >
   >These emails are specific to YouTube and are in addition to the generic workflow email notifications. As a result, you may receive two sets of email notification - the generic notification available in the **[!UICONTROL Day CQ Workflow Email Notification Service]** and one specific to YouTube depending on your configuration settings.

1. When you are finished, near the upper-right corner of the dialog box, select the **[!UICONTROL Done]** icon (check mark).
1. On the Publish to YouTube workflow page, near the upper-right corner, select **[!UICONTROL Sync]**.

-->

## Omkoda med Bearbetningsprofil {#transcode-video}

[!DNL Experience Manager] som [!DNL Cloud Service] gör att du kan utföra grundläggande omkodning av MP4-videofiler med Bearbeta profiler. Med den här funktionen kan du inte bara överföra utan även förhandsgranska och skala en MP4-videofil.

![Skapa bearbetningsprofil för videoomkodning i [!DNL Experience Manager]](assets/video-processing-profile-for-mp4.png)

*Figur: En bearbetningsprofil för videoomkodning i [!DNL Experience Manager].*

Om du bara anger bredd eller enbart höjd och lämnar det andra fältet tomt behåller återgivningarna proportionerna. H.264-videokodeken finns tillgänglig för transkodning.

Om du vill bearbeta resurser med en bearbetningsprofil lägger du till en profil i en mapp. Se [Bearbeta resurser med bearbetningsprofiler](/help/assets/asset-microservices-configure-and-use.md#use-profiles).

## Kommentera videomaterial {#annotate-video-assets}

Du kan lägga till anteckningar i videoresurser. När du kommenterar videoklipp pausas spelaren så att du kan anteckna i en bildruta. Mer information finns i [hantera videomaterial](manage-video-assets.md).

>[!NOTE]
>
>MXF-videoformatet stöds ännu inte med videoresursanteckningar.

1. I konsolen [!DNL Assets] väljer du **[!UICONTROL Edit]** på resurskortet för att visa sidan med resursinformation.
1. Om du vill spela upp videon klickar du på **[!UICONTROL Preview]**.
1. Klicka på **[!UICONTROL Annotate]** om du vill kommentera videon. En anteckning läggs till vid en viss tidpunkt (bildruta) i videon. När du gör anteckningar kan du rita på arbetsytan och ta med en kommentar med ritningen. Kommentarerna sparas automatiskt. Klicka på **[!UICONTROL Close]** om du vill avsluta anteckningsguiden.
1. Gå till en viss punkt i videon, ange tiden i sekunder i **textfältet** och klicka på **Hoppa**. Om du till exempel vill hoppa över de första 20 sekunderna av videon anger du 20 i textfältet.
1. Klicka på en anteckning om du vill visa den i tidslinjen. Klicka på **[!UICONTROL Delete]** om du vill ta bort anteckningen från tidslinjen.

## Bästa praxis och begränsningar {#tips-limitations}

* Utan [!DNL Dynamic Media]-licens kan du bara bearbeta MP4-filer med bearbetningsprofiler.
* När MP4-filer kodas om med Bearbeta profiler gäller följande riktlinjer och begränsningar:

   * Apple ProRes-filer kan endast kodas om till en maximal upplösning på 1080p.
   * Om källfilen har en bithastighet på >200 Mbit/s kan du bara omkoda till en maximal upplösning på 1080p.
   * Om källbildrutefrekvensen är >=60 fps blir den maximala storleken på källfilen som du kan använda:

      * 400 MB för 4K-omkodning.
      * 800 MB för 1080p-omkodning.
      * 8 GB för 720p-omkodning.

   * Maximal filstorlek som du kan omkoda till en upplösning på 4 000 v/min är 2,55 GB MP4-fil med en upplösning på 4 000, en bithastighet på 12 Mbit/s och 23 fps.

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
>* [Videodokumentation för dynamiska media](/help/assets/dynamic-media/video.md).
>* [Mer information om användning, typer och konfiguration av bearbetningsprofiler](/help/assets/asset-microservices-configure-and-use.md).

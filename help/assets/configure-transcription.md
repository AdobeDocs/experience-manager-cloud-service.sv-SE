---
title: Konfigurera transkriberingstjänsten
description: Adobe Experience Manager Assets är konfigurerat med  [!DNL Azure Media Services] som automatiskt genererar textutskrift av det talade språket i en ljud- eller videofil som stöds i WebVTT-format (Vtt).
products: SG_EXPERIENCEMANAGER/ASSETS and Experience Manager as a Cloud Service
sub-product: assets
content-type: reference
contentOwner: Vishabh Gupta
topic-tags: Configuration
feature: Asset Management, Configuration
role: Admin
exl-id: e96c8d68-74a6-4d61-82dc-20e619338d4b
source-git-commit: 02ad83eb9fa9ed3bf06cf7fe0ef10fd9577f66a9
workflow-type: tm+mt
source-wordcount: '1606'
ht-degree: 0%

---

# Konfigurera transkription i [!DNL Experience Manager Assets] {#configure-transcription-service}

Transkription är processen att översätta ljudet från en ljud- eller videofil till text (tal till text) med hjälp av taligenkänningstekniken.
[!DNL Adobe Experience Manager Assets] har konfigurerats med [!DNL Azure Media Services] som automatiskt genererar textutskrift av det talade språket i en ljud- eller videofil som stöds i WebVTT-format (.vtt). När en ljud- eller videoresurs bearbetas i [!DNL Experience Manager Assets] genererar transkriberingstjänsten automatiskt texttranskriberingen av ljud- eller videoresursen och lagrar den på samma plats i Assets-databasen där den ursprungliga resursen finns. Med transkriberingstjänsten [!DNL Experience Manager Assets] kan marknadsförarna effektivt hantera sitt ljud- och videoinnehåll med ökad identifiering av textinnehållet och öka avkastningen på dessa resurser genom stöd för hjälpmedel och lokalisering.

Transskript är textversioner av talat innehåll. Ett exempel är en film som du ser på alla OTT-plattformar, som ofta innehåller bildtexter som hjälper till med tillgänglighet eller som konsumerar innehållet på andra språk. Eller alla ljud- och videofiler som används i marknadsförings-, utbildnings- eller underhållningssyfte. De här upplevelserna börjar med en transkription som sedan formateras eller översätts på lämpligt sätt. Att transkribera ljud eller video är en tidskrävande och felbenägen process när den utförs manuellt. Det är också en utmaning att skala den manuella processen, med tanke på det ständigt ökande behovet av ljud- och videoinnehåll. [!DNL Experience Manager Assets] använder Azure:s AI-baserade transkription som tillåter storskalig bearbetning av ljud- och videoresurserna och genererar texttranskriberingarna (.vtt-filer) tillsammans med tidsstämpelsinformationen. Tillsammans med Assets stöds även transkriberingsfunktionen i Dynamic Media.

transkriberingsfunktionen är tillgänglig utan kostnad i [!DNL Experience Manager Assets]. Administratörerna kräver dock användarens Azure-autentiseringsuppgifter för att konfigurera transkriberingstjänsten i [!DNL Experience Manager Assets]. Du kan också [hämta autentiseringsuppgifterna för utvärderingsversionen](https://azure.microsoft.com/en-us/pricing/details/media-services/) direkt från Microsoft® för att få en upplevelse av ljud- eller videotranskriberingsfunktionen i Assets.

## Krav för transkribering {#prerequisites}

1. En [!DNL Experience Manager Assets as a Cloud Service]-instans som körs.
1. Följande Azure-autentiseringsuppgifter krävs för konfiguration i [!DNL Experience Manager Assets]:

   * Klient-ID (API-nyckel)
   * Klienthemlig nyckel
   * Klientslutpunkt (domän)
   * Mediekonto
   * Resursgrupp
   * Prenumerations-ID

   Se [Azure-dokumentation](https://docs.microsoft.com/en-us/azure/media-services/latest/access-api-howto?tabs=portal) för att få autentiseringsuppgifter för åtkomst till Azure Media Services API.

1. Kontrollera att Azure-kontot har tillräcklig kredit för att behandla nya begäranden.

## Konfigurera transkription i [!DNL Experience Manager Assets] {#configure-transcription}

Följande konfigurationer krävs för att aktivera transkriberingsfunktionen i [!DNL Experience Manager Assets]:

1. [Konfigurera Azure Media Services](#configure-azure-media-service)
1. [Konfigurera Bearbetningsprofil för ljud-/videotranskription](#configure-processing-profile-for-transcription)


### Konfigurera Azure Media Services {#configure-azure-media-services}

[!DNL Experience Manager Assets] använder [!DNL Azure Media Services] som automatiskt genererar textutskrifter av det talade språket i en [ljud- eller videofil som stöds](#supported-file-formats-for-transcription) i WebVTT-formatet (.vtt). Administratörerna kan konfigurera [!DNL Azure Media Services] i [!DNL Experience Manager Assets] med hjälp av Azure-autentiseringsuppgifterna. [transkriberingskraven](#transcription-prerequisites) listar de [!DNL Azure]-autentiseringsuppgifter som krävs för konfigurationen. Om du inte har [!DNL Azure]-konto och autentiseringsuppgifter kan du läsa [dokumentationen för Azure Media Services](https://azure.microsoft.com/en-us/pricing/details/media-services/) för att hämta autentiseringsuppgifter för utvärderingsversionen.

![configure-transcription-service](assets/configure-transcription-service.png)

Gå till **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Azure Media Services Configuration]**. Välj en mapp (plats) i den vänstra listen och klicka på knappen [!UICONTROL Create] för att konfigurera anslutningen till ditt [!DNL Azure]-konto. Den här mappen är den plats där din [!DNL Azure]-molnkonfiguration lagras i Experience Manager Assets. Ange inloggningsuppgifterna för [!DNL Azure] och klicka på **[!UICONTROL Save & Close]**.

### Konfigurera bearbetningsprofil för transkription {#configure-processing-profile}

När [!DNL Azure Media Services] har konfigurerats i Experience Manager Assets är nästa steg att skapa en resursbearbetningsprofil för att generera en AI-baserad transkription av ljud- och videoresurserna. Den AI-baserade bearbetningsprofilen genererar transkriberingar av det [ljud- eller videomaterial ](#supported-file-formats-for-transcription) som stöds som en rendering i Experience Manager Assets och lagrar transkriberingen (.vtt-filen) i samma mapp som den ursprungliga resursen finns i. Det är därför enklare för användarna att söka efter och hitta resursen och dess utskrivna återgivning.

Gå till **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Processing Profiles]** och klicka på knappen **[!UICONTROL Create]** för att skapa en AI-baserad bearbetningsprofil för generering av transkription av dina ljud- och videofiler. Som standard visas bara tre flikar på sidan Bearbetningsprofil (Bild, Video och Anpassad). En **[!UICONTROL Content AI]**-flik visas emellertid om du har konfigurerat [!DNL Azure Media Services] i [!DNL Experience Manager Assets]-instansen. Verifiera dina [!DNL Azure]-inloggningsuppgifter om du inte ser fliken **[!UICONTROL Content AI]** när du skapar en bearbetningsprofil.

Klicka på knappen **[!UICONTROL Add New]** på fliken **[!UICONTROL Content AI]** för att konfigurera transkriberingen. Här kan du inkludera och exkludera filformat (MIME-typer) för att generera transkript genom att välja filtyper i listrutan. I följande bild inkluderas alla ljud- och videofiler som stöds och textfilerna exkluderas.

Aktivera växlingsknappen **[!UICONTROL Create VTT transcript in same directory]** för att skapa och lagra den krypterade återgivningen (.vtt-fil) i samma mapp som den ursprungliga resursen finns i. De andra återgivningarna genereras också av standardarbetsflödet för DAM-resurshantering oavsett den här inställningen.

![configure-transcription-service](assets/configure-transcription-profile.png)

I följande bild visas en anpassad videoprofil som har skapats i Experience Manager Assets.

![configure-transcription-service](assets/video-processing-profile.png)

Videoprofilen innehåller även följande anpassade konfigurationer. Mer information om hur du skapar en anpassad bearbetningsprofil finns i [Bearbetningsprofildokumentation](/help/assets/asset-microservices-configure-and-use.md).

![configure-transcription-service](assets/video-processing-profile2.png)

Låt oss nu konfigurera transkriberingen i den här videoprofilen. Navigera till fliken **[!UICONTROL Content AI]** och klicka på knappen **[!UICONTROL Add New]**. Inkludera alla ljud- och videofiler och exkludera bild- och programfilerna. Aktivera växlingsknappen **[!UICONTROL Create VTT transcript in same directory]** och spara konfigurationen.

![configure-transcription-service](assets/video-processing-profile1.png)

När bearbetningsprofilen har konfigurerats för transkription av ljud- och videofiler kan du använda den här bearbetningsprofilen för mappar på något av följande sätt:

* Välj en bearbetningsprofildefinition i **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Processing Profiles]** och använd åtgärden **[!UICONTROL Apply Profile to Folders]**. I innehållsläsaren kan du navigera till en viss mapp, välja en mapp och bekräfta programmet för profilen.
* Markera en mapp i Assets användargränssnitt och klicka på åtgärden **[!UICONTROL Properties]** för att öppna mappegenskaper. Klicka på fliken **[!UICONTROL Asset Processing]** och välj lämplig bearbetningsprofil för mappen i listan **[!UICONTROL Processing Profile]**. Klicka på **[!UICONTROL Save & Close]** om du vill spara ändringarna.

  ![configure-transcription-service](assets/video-processing-profile3.png)

* Användare kan välja mappar eller specifika resurser i Assets användargränssnitt för att tillämpa en bearbetningsprofil och sedan välja alternativet **[!UICONTROL Reprocess Assets]** bland de tillgängliga alternativen överst.

>[!TIP]
>Endast en bearbetningsprofil kan användas för en mapp.
>
>När en bearbetningsprofil har tillämpats på en mapp bearbetas alla nya resurser som har överförts (eller uppdaterats) i den här mappen eller någon av dess undermappar med hjälp av den extra bearbetningsprofilen som har konfigurerats. Den här bearbetningen är utöver standardprofilen.

>[!NOTE]
>
>En bearbetningsprofil som tillämpas på en mapp fungerar för hela trädet, men kan åsidosättas om en annan profil tillämpas på en undermapp.
>
>När resurser överförs till en mapp kommunicerar Experience Manager med mappens egenskaper för att identifiera bearbetningsprofilen. Om ingen används kontrolleras en överordnad mapp i hierarkin för att en bearbetningsprofil ska användas.


## Generera transkriberingar av ljud- eller videomaterial {#generate-transcription}

När du bearbetar en videoresurs genererar den [AI-baserade bearbetningsprofilen](#configure-processing-profile-for-transcription) automatiskt utskriften (.vtt-fil) som en återgivning tillsammans med den ursprungliga resursen i samma mapp.

![configure-transcription-service](assets/transcript1.png)

Du kan också se den transkriberade återgivningen genom att gå till återgivningarna av den ursprungliga videoresursen. Om du vill komma åt panelen **[!UICONTROL Renditions]** markerar du den ursprungliga videoresursen och öppnar den vänstra listen. Du kan se att den krypterade återgivningen (.vtt-fil) är synlig under huvudet **[!UICONTROL TRANSCRIPTVTT]**.

![configure-transcription-service](assets/transcript.png)

Du kan hämta transkriberingen (.vtt-textfilen) direkt från mappen som en separat resursåtergivning, eller från panelen **[!UICONTROL Renditions]** för den ursprungliga resursen genom att hämta alla återgivningar av resursen.

För närvarande stöder inte Experience Manager förhandsgranskning av eller redigering av VTT-filer i sin helhet. Du kan dock hämta transkriberingen och använda valfri textredigerare för att redigera eller verifiera transkriberingen. I transkriften visas det talade språket som en text vid den angivna tidsstämpeln i videon med transkriberingens konfidensgrad (precision).

![configure-transcription-service](assets/transcript-text.png)

## Använda transkription i Dynamic Media {#using-transcription-in-dynamic-media}

Om du har [konfigurerat Dynamic Media](/help/assets/dynamic-media/config-dm.md) i din Experience Manager Assets-instans kan du publicera resursen (ljud- eller videofilen) och dess transkript (.vtt-fil) till Dynamic Media. På så sätt publiceras den ursprungliga resursen (ljud- eller videofilen) och dess transkriberade återgivning (.vtt-filen) till Dynamic Media i samma mapp. Dynamic Media-administratören kan [aktivera CC Closed Caption](/help/assets/dynamic-media/video.md#adding-captions-to-video) för ljud- eller videofilen med hjälp av transkriptrenderingen (.vtt-filen).

Se även:

* [Videosjälvstudiekurs om hur du lägger till CC-undertexter i Dynamic Media-video](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-overview-feature-video-use.html#add-cc-closed-captioning-to-dynamic-media-video)
* [Publish Dynamic Media-videor till YouTube](/help/assets/dynamic-media/video.md#publishing-videos-to-youtube)

I följande bild återspeglar webbadressen bildtextdelen som refererar till utskriften (.vtt-filen). Videon visar det talade språket (transkriberad text) som **[!UICONTROL Closed Caption]** vid den angivna tidsstämpeln i videon. Användaren kan aktivera eller inaktivera bildtexten med knappen **[!UICONTROL CC]**.

![configure-transcription-service](assets/transcript-example.png)

## Filformat som stöds för transkription {#supported-file-format}

Följande ljud- och videofilformat stöds för transkription:

| Ljud-/videoformat som stöds | Tillägg |
|----|----|
| FLV (med H.264- och AAC-kodekar) | (.flv) |
| MXF | (.mxf) |
| MPEG2-PS, MPEG2-TS, 3GP | (.ts, .ps, .3gp, .3gpp, .mpg) |
| Windows Media Video (WMV)/ASF | (.wmv, .asf) |
| AVI (okomprimerad 8 bitar/10 bitar) | (.avi) |
| MP4 | (.mp4, .m4a, .m4v) |
| Microsoft® Digital Video Recording (DVR-MS) | (.dvr-ms) |
| Matroska/WebM | (.mkv) |
| WAVE/WAV | (.wav) |
| QuickTime | (.mov) |


>[!NOTE]
>
>Resurser (ljud- eller videofiler) av programtyp stöds inte för transkription.

## Kända begränsningar {#known-limitations}

* transkriberingsfunktionen stöds för videoklipp med en varaktighet på upp till 10 minuter.
* Videotiteln får innehålla högst 80 tecken.
* Filstorleken är upp till 15 GB.
* Den maximala bearbetningstiden som stöds är 60 minuter.
* I ett betalt [!DNL Azure]-konto kan du överföra upp till 50 filmer per minut. I ett testversionskonto kan du dock överföra upp till fem filmer per minut.

## Felsökningstips {#troubleshooting}

Logga in på ditt [!DNL Azure Media Services]-konto med samma autentiseringsuppgifter (som du har använt för konfigurationen) för att verifiera status för begäran. Kontakta support för [!DNL Azure] om din begäran inte kan bearbetas.

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
* [Publish Assets till AEM och Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)

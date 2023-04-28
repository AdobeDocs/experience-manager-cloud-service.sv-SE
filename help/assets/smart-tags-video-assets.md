---
title: Smarta taggar för videomaterial
description: Experience Manager lägger automatiskt till kontextuella och beskrivande smarta taggar i videoklipp med [!DNL Adobe Sensei].
feature: Smart Tags,Tagging
role: Admin,User
exl-id: b59043c5-5df3-49a7-b4fc-da34c03649d7
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '1172'
ht-degree: 1%

---

# Smarta taggar för videomaterial {#video-smart-tags}

Det växande behovet av nytt innehåll kräver mindre manuella insatser för att leverera övertygande digitala upplevelser på nolltid. [!DNL Adobe Experience Manager] som [!DNL Cloud Service] har stöd för automatisk taggning av videomaterial med hjälp av artificiell intelligens. Det kan vara tidskrävande att tagga videoklipp manuellt. Men [!DNL Adobe Sensei] den kraftfulla videomaterifieringen använder artificiella intelligensmodeller för att analysera videomaterial och lägga till taggar i videomaterialet. På så sätt minskar tiden för DAM-användare att leverera avancerade upplevelser till sina kunder. Adobe maskininlärningstjänst genererar två uppsättningar taggar för en video. En uppsättning motsvarar objekt, scener och attribut i videon. den andra uppsättningen avser åtgärder som att dricka, köra och jogga.

Videotaggning är aktiverad som standard i [!DNL Adobe Experience Manager] som [!DNL Cloud Service]. Du kan dock [avanmäl dig från smart taggning av video](#opt-out-video-smart-tagging) på en mapp. Videor taggas automatiskt när du överför nya videoklipp eller bearbetar om befintliga. [!DNL Experience Manager] skapar också miniatyrbilder och extraherar metadata för videofilerna. De smarta taggarna visas i fallande ordning efter deras [konfidensgrad](#confidence-score-video-tag) i tillgången [!UICONTROL Properties].

## Smart taggning av videoklipp vid överföring {#smart-tag-assets-on-ingestion}

När du [ladda upp videomaterial](add-assets.md#upload-assets) till [!DNL Adobe Experience Manager] som [!DNL Cloud Service], bearbetas videoklippen. När bearbetningen är klar går du till [!UICONTROL Basic] tillgångsflik [!UICONTROL Properties] sida. Smarta taggar läggs automatiskt till i videon under [!UICONTROL Smart Tags]. Resursmikrotjänster utnyttjar [!DNL Adobe Sensei] för att skapa dessa smarta taggar.

![Smarta taggar läggs till i videoklipp och visas på fliken Grundläggande i resursegenskaper](assets/smart-tags-added-to-videos.png)

De använda smarta taggarna sorteras i fallande ordning efter [konfidensgrad](#confidence-score-video-tag), kombinerat för object- och action-taggar, inom [!UICONTROL Smart Tags].

>[!IMPORTANT]
>
>Du rekommenderas att granska dessa automatiskt genererade taggar för att säkerställa att de överensstämmer med ditt varumärke och dess värden.

## Smart taggning av befintliga videor i DAM {#smart-tag-existing-videos}

De befintliga videomaterialet i DAM är inte automatiskt smarta taggade. Du måste [!UICONTROL Reprocess Assets] manuellt för att generera smarta taggar för dem.

Följ de här stegen för att smart tagga videoresurser eller mappar (inklusive undermappar) med resurser som redan finns i resurskatalogen:

1. Välj [!DNL Adobe Experience Manager] logotypen och välj sedan resurser från [!UICONTROL Navigation] sida.

1. Välj [!UICONTROL Files] för att visa gränssnittet Resurser.

1. Navigera till mappen som du vill använda smarta taggar på.

1. Markera hela mappen eller specifika videoresurser.

1. Välj ![Ikon för att bearbeta resurser](assets/do-not-localize/reprocess-assets-icon.png) [!UICONTROL Reprocess Assets] -ikonen och välj [!UICONTROL Full Process] alternativ.

<!-- TBD: Limit size -->

![Bearbeta om resurser för att lägga till taggar i videoklipp i en befintlig DAM-databas](assets/reprocess.gif)

När processen är klar går du till [!UICONTROL Properties] sida med videoresurser i mappen. De automatiskt tillagda taggarna visas i [!UICONTROL Smart Tags] avsnitt i [!UICONTROL Basic] -fliken. De använda smarta taggarna sorteras i fallande ordning efter [konfidensgrad](#confidence-score-video-tag).

## Sök efter taggade videofilmer {#search-smart-tagged-videos}

Om du vill söka efter videoresurserna baserat på de automatiskt genererade smarta taggarna använder du [Omnisearch](search-assets.md#search-assets-in-aem):

1. Välj sökikonen ![sökningsikon](assets/do-not-localize/search_icon.png) för att visa Omnissearch-fältet.

1. Ange en tagg, i Omnissearch-fältet, som du inte uttryckligen har lagt till i en video.

1. Sök baserat på taggen.

Sökresultaten visar videoresurserna baserat på den tagg du har angett.

Sökresultaten är en kombination av videomaterial med sökbara nyckelord i metadata och videomaterialet som är smarta taggade med de sökbara nyckelorden. Sökresultaten som matchar alla söktermer i metadatafält visas först, följt av sökresultaten som matchar någon av söktermerna i de smarta taggarna. Mer information finns i [Förstå [!DNL Experience Manager] sökresultat med smarta taggar](smart-tags.md#understand-search).

## Moderera smarta taggar för video {#moderate-video-smart-tags}

[!DNL Adobe Experience Manager] använder du för att strukturera de smarta taggarna till:

* ta bort felaktiga taggar som tilldelats era varumärkesvideor.

* förfina taggbaserade sökningar efter videoklipp genom att se till att videon visas i sökresultaten för de mest relevanta taggarna. Det eliminerar därför risken för att videoklipp som inte är relaterade visas i sökresultaten.

* tilldelar en högre rankning till en tagg för att öka dess relevans med avseende på en video. Om du befordrar en tagg för en video ökar risken för att videon visas i sökresultaten när en sökning utförs baserat på den taggen.

Mer information om hur du modererar smarta taggar för resurser finns i [Hantera smarta taggar](smart-tags.md#manage-smart-tags-and-searches).

![Moderera smarta taggar för video](assets/manage-video-smart-tags.png)

>[!NOTE]
>
>Alla taggar som modereras enligt stegen i [Hantera smarta taggar](smart-tags.md#manage-smart-tags-and-searches) sparas inte vid ombearbetning av tillgången. Den ursprungliga uppsättningen taggar visas igen.

## Avanmäl dig från smart taggning av video {#opt-out-video-smart-tagging}

När den automatiska taggningen av videor körs parallellt med andra bearbetningsuppgifter som att skapa miniatyrbilder och extrahera metadata kan det vara tidskrävande. Om du vill påskynda resursbearbetningen kan du välja bort smart taggning för video vid överföring på mappnivå.

Så här avanmäler du dig från automatisk generering av smarta videotaggar för resurser som överförts till en viss mapp:

1. Öppna [!UICONTROL Asset Processing] flik i mapp [!UICONTROL Properties].

1. I [!UICONTROL Smart Tags for Videos] meny, [!UICONTROL Inherited] som standard är det här alternativet markerat och den smarta taggen för video är aktiverad.

   När [!UICONTROL Inherited] om du väljer det här alternativet visas den ärvda mappsökvägen tillsammans med informationen om den är inställd på [!UICONTROL Enable] eller [!UICONTROL Disable].

   ![Inaktivera smart taggning för video](assets/disable-video-tagging.png)

1. Välj [!UICONTROL Disable] om du vill avanmäla smart taggning av videoklipp som överförts till mappen.

>[!IMPORTANT]
>
>Om du har valt att inte längre tagga videoklipp i en mapp vid överföringen och vill tagga videoklippen smart efter överföringen kan du **[!UICONTROL Enable Smart Tags for Videos]** från [!UICONTROL Asset Processing] mappens flik [!UICONTROL Properties] och använda [[!UICONTROL Reprocess Asset] option](#smart-tag-existing-videos) om du vill lägga till smarta taggar i videon.

## Konfidenspoäng {#confidence-score-video-tag}

[!DNL Adobe Experience Manager] använder ett lägsta konfidensintervall för smarta taggar för objekt och åtgärder för att undvika att ha för många taggar för varje videoresurs, vilket gör indexeringen långsammare. Sökresultaten för dina resurser rangordnas baserat på konfidensintervallet, vilket i allmänhet förbättrar sökresultaten utöver vad en inspektion av de tilldelade taggarna för en videoresurs antyder. Felaktiga taggar har ofta låga konfidensvärden, så de visas sällan överst i listan Smarta taggar för resurser.

Standardtröskelvärdet för åtgärdstaggar och objekttaggar i [!DNL Adobe Experience Manager] är 0,7 (ska vara ett värde mellan 0 och 1). Om vissa videoresurser inte är taggade med en viss tagg betyder det att algoritmen är mindre än 70 % säker i de förväntade taggarna. Standardtröskelvärdet kanske inte alltid är optimalt för alla användare. Du kan därför ändra konfidensvärdet i OSGI-konfigurationen.

Lägga till OSGI-konfiguration med konfidensgrad i projektet som distribueras till [!DNL Adobe Experience Manager] som [!DNL Cloud Service] via [!DNL Cloud Manager]:

* I [!DNL Adobe Experience Manager] projekt (`ui.config` sedan Archetype 24, eller tidigare `ui.apps`) `config.author` OSGi-konfiguration, inkludera en konfigurationsfil med namnet `com.adobe.cq.assetcompute.impl.senseisdk.SenseiSdkImpl.cfg.json` med följande innehåll:

```json
{
  "minVideoActionConfidenceScore":0.5,
  "minVideoObjectConfidenceScore":0.5,
}
```

>[!NOTE]
>
>Manuella taggar tilldelas en konfidensgrad på 100 % (maximal konfidensgrad). Om det finns videomaterial med manuella taggar som matchar sökfrågan visas de därför före smarta taggar som matchar sökfrågan.

## Begränsningar {#video-smart-tagging-limitations}

* Du kan inte utbilda tjänsten som tillämpar smarta taggar på videoklipp med hjälp av specifika videoklipp. Fungerar som standard [!DNL Adobe Sensei] inställningar.

* Taggningsförloppet visas inte.

* Endast videoklipp som är mindre än 300 MB i filstorlek taggas automatiskt. The [!DNL Adobe Sensei] hoppar över videofiler som är större.

* Endast videoklipp i de filformat och kodekar som stöds som omnämns i [Smarta taggar](/help/assets/smart-tags.md#smart-tags-supported-file-formats) är taggade.

**Se även**

* [Översätt resurser](translate-assets.md)
* [HTTP API för Assets](mac-api-assets.md)
* [Resurser som stöds i filformat](file-format-support.md)
* [Söka efter resurser](search-assets.md)
* [Anslutna resurser](use-assets-across-connected-assets-instances.md)
* [Materialrapporter](asset-reports.md)
* [Metadata-scheman](metadata-schemas.md)
* [Hämta resurser](download-assets-from-aem.md)
* [Hantera metadata](manage-metadata.md)
* [Söka efter fasetter](search-facets.md)
* [Hantera samlingar](manage-collections.md)
* [Import av massmetadata](metadata-import-export.md)

>[!MORELIKETHIS]
>
>* [Hantera smarta taggar och resurssökningar](smart-tags.md#manage-smart-tags-and-searches)
>* [Utbilda tjänsten Smart Tag och tagga dina bilder](smart-tags.md)


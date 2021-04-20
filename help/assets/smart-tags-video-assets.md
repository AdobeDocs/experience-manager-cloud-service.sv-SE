---
title: Smarta taggar för videomaterial
description: Experience Manager lägger automatiskt till kontextuella och beskrivande smarta taggar i videoklipp med  [!DNL Adobe Sensei].
feature: Smart Tags,Tagging
role: Administrator,Business Practitioner
translation-type: tm+mt
source-git-commit: 8093f6cec446223af58515fd8c91afa5940f9402
workflow-type: tm+mt
source-wordcount: '1148'
ht-degree: 0%

---


# Smart tagga dina videoresurser {#video-smart-tags}

Det växande behovet av nytt innehåll kräver mindre manuella insatser för att leverera övertygande digitala upplevelser på nolltid. [!DNL Adobe Experience Manager] som ett  [!DNL Cloud Service] stöd för automatisk taggning av videomaterial med hjälp av artificiell intelligens. Det kan vara tidskrävande att tagga videoklipp manuellt. Med funktionen [!DNL Adobe Sensei] för smart taggning av video används artificiell intelligens för att analysera videoinnehåll och lägga till taggar i videoresurserna. På så sätt minskar tiden för DAM-användare att leverera avancerade upplevelser till sina kunder. Adobe maskininlärningstjänst genererar två uppsättningar taggar för en video. En uppsättning motsvarar objekt, scener och attribut i videon. den andra uppsättningen avser åtgärder som att dricka, köra och jogga.

Videotaggning är som standard aktiverad i [!DNL Adobe Experience Manager] som [!DNL Cloud Service]. Du kan dock [välja bort smart taggning för video](#opt-out-video-smart-tagging) i en mapp. Videor taggas automatiskt när du överför nya videoklipp eller bearbetar om befintliga. [!DNL Experience Manager] skapar också miniatyrbilder och extraherar metadata för videofilerna. De smarta taggarna visas i fallande ordning efter [konfidensintervallet](#confidence-score-video-tag) i resursen [!UICONTROL Properties].

## Smart taggning av videoklipp vid överföring {#smart-tag-assets-on-ingestion}

När du [överför videoresurser](add-assets.md#upload-assets) till [!DNL Adobe Experience Manager] som en [!DNL Cloud Service] bearbetas videoklippen. När bearbetningen är klar går du till fliken [!UICONTROL Basic] på sidan [!UICONTROL Properties] för resursen. Smarta taggar läggs automatiskt till i videon under [!UICONTROL Smart Tags]. Resursmikrotjänsterna använder [!DNL Adobe Sensei] för att skapa dessa smarta taggar.

![Smarta taggar läggs till i videoklipp och visas på fliken Grundläggande i resursegenskaper](assets/smart-tags-added-to-videos.png)

De använda smarta taggarna sorteras i fallande ordning i [konfidensintervallet](#confidence-score-video-tag), kombinerat för object- och action-taggar, inom [!UICONTROL Smart Tags].

>[!IMPORTANT]
>
>Du rekommenderas att granska dessa automatiskt genererade taggar för att säkerställa att de överensstämmer med ditt varumärke och dess värden.

## Smart taggning av befintliga videoklipp i DAM {#smart-tag-existing-videos}

De befintliga videomaterialet i DAM är inte automatiskt smarta taggade. Du måste [!UICONTROL Reprocess Assets] manuellt om du vill generera smarta taggar för dem.

Följ de här stegen för att smart tagga videoresurser eller mappar (inklusive undermappar) med resurser som redan finns i resurskatalogen:

1. Välj logotypen [!DNL Adobe Experience Manager] och välj sedan resurser på sidan [!UICONTROL Navigation].

1. Välj [!UICONTROL Files] för att visa gränssnittet Resurser.

1. Navigera till mappen som du vill använda smarta taggar på.

1. Markera hela mappen eller specifika videoresurser.

1. Välj ikonen ![Bearbeta resurser](assets/do-not-localize/reprocess-assets-icon.png) [!UICONTROL Reprocess Assets] och välj alternativet [!UICONTROL Full Process].

<!-- TBD: Limit size -->

![Bearbeta om resurser för att lägga till taggar i videoklipp i en befintlig DAM-databas](assets/reprocess.gif)

När processen är klar navigerar du till [!UICONTROL Properties]-sidan för alla videoresurser i mappen. De automatiskt tillagda taggarna visas i avsnittet [!UICONTROL Smart Tags] på fliken [!UICONTROL Basic]. De använda smarta taggarna sorteras i fallande ordning efter [konfidensgrad](#confidence-score-video-tag).

## Sök efter taggade videofilmer {#search-smart-tagged-videos}

Om du vill söka efter videoresurser baserat på de automatiskt genererade smarta taggarna använder du [Omnissearch](search-assets.md#search-assets-in-aem):

1. Välj sökikonen ![sökikonen](assets/do-not-localize/search_icon.png) för att visa Omnissearch-fältet.

1. Ange en tagg, i Omnissearch-fältet, som du inte uttryckligen har lagt till i en video.

1. Sök baserat på taggen.

Sökresultaten visar videoresurserna baserat på den tagg du har angett.

Sökresultaten är en kombination av videomaterial med sökbara nyckelord i metadata och videomaterialet som är smarta taggade med de sökbara nyckelorden. Sökresultaten som matchar alla söktermer i metadatafält visas först, följt av sökresultaten som matchar någon av söktermerna i de smarta taggarna. Mer information finns i [Förstå [!DNL Experience Manager] sökresultat med smarta taggar](smart-tags.md#understandsearch).

## Moderera smarta taggar för video {#moderate-video-smart-tags}

[!DNL Adobe Experience Manager] använder du för att strukturera de smarta taggarna till:

* ta bort felaktiga taggar som tilldelats era varumärkesvideor.

* förfina taggbaserade sökningar efter videoklipp genom att se till att videon visas i sökresultaten för de mest relevanta taggarna. Det eliminerar därför risken för att videoklipp som inte är relaterade visas i sökresultaten.

* tilldelar en högre rankning till en tagg för att öka dess relevans med avseende på en video. Om du befordrar en tagg för en video ökar risken för att videon visas i sökresultaten när en sökning utförs baserat på den taggen.

Mer information om hur du modererar smarta taggar för resurser finns i [Hantera smarta taggar](smart-tags.md#manage-smart-tags-and-searches).

![Moderera smarta taggar för video](assets/manage-video-smart-tags.png)

>[!NOTE]
>
>Eventuella taggar som modereras med stegen i [Hantera smarta taggar](smart-tags.md#manage-smart-tags-and-searches) sparas inte när resursen bearbetas om. Den ursprungliga uppsättningen taggar visas igen.

## Välj bort smarta taggar för video {#opt-out-video-smart-tagging}

När den automatiska taggningen av videor körs parallellt med andra bearbetningsuppgifter som att skapa miniatyrbilder och extrahera metadata kan det vara tidskrävande. Om du vill påskynda resursbearbetningen kan du välja bort smart taggning för video vid överföring på mappnivå.

Så här avanmäler du dig från automatisk generering av smarta videotaggar för resurser som överförts till en viss mapp:

1. Öppna fliken [!UICONTROL Asset Processing] i mappen [!UICONTROL Properties].

1. I [!UICONTROL Smart Tags for Videos]-menyn är alternativet [!UICONTROL Inherited] markerat som standard och smart tagg för video är aktiverat.

   När alternativet [!UICONTROL Inherited] är markerat visas även den ärvda mappsökvägen tillsammans med information om den är inställd på [!UICONTROL Enable] eller [!UICONTROL Disable].

   ![Inaktivera smart taggning för video](assets/disable-video-tagging.png)

1. Välj [!UICONTROL Disable] om du vill avanmäla dig från smart taggning för videofilmer som överförts till mappen.

>[!IMPORTANT]
>
>Om du har valt att inte längre tagga videoklipp i en mapp vid överföringen och vill tagga videoklippen med smarta taggar efter överföringen kan du lägga till smarta taggar med **[!UICONTROL Enable Smart Tags for Videos]** från fliken [!UICONTROL Asset Processing] i mappen [!UICONTROL Properties] och [[!UICONTROL Reprocess Asset]-alternativet](#smart-tag-existing-videos) för att lägga till smarta taggar i videon.

## Konfidenspoäng {#confidence-score-video-tag}

[!DNL Adobe Experience Manager] använder ett lägsta konfidensintervall för smarta taggar för objekt och åtgärder för att undvika att ha för många taggar för varje videoresurs, vilket gör indexeringen långsammare. Sökresultaten för dina resurser rangordnas baserat på konfidensintervallet, vilket i allmänhet förbättrar sökresultaten utöver vad en inspektion av de tilldelade taggarna för en videoresurs antyder. Felaktiga taggar har ofta låga konfidensvärden, så de visas sällan överst i listan Smarta taggar för resurser.

Standardtröskelvärdet för action- och object-taggar i [!DNL Adobe Experience Manager] är 0,7 (bör vara ett värde mellan 0 och 1). Om vissa videoresurser inte är taggade med en viss tagg betyder det att algoritmen är mindre än 70 % säker i de förväntade taggarna. Standardtröskelvärdet kanske inte alltid är optimalt för alla användare. Du kan därför ändra konfidensvärdet i OSGI-konfigurationen.

Så här lägger du till OSGI-konfigurationen med konfidensintervallet i projektet som distribuerats till [!DNL Adobe Experience Manager] som en [!DNL Cloud Service] till [!DNL Cloud Manager]:

* I [!DNL Adobe Experience Manager]-projektet (`ui.config` sedan Archetype 24, eller tidigare `ui.apps`) och `config.author` OSGi-konfigurationen, inkluderar du en konfigurationsfil med namnet `com.adobe.cq.assetcompute.impl.senseisdk.SenseiSdkImpl.cfg.json` med följande innehåll:

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

* Du kan inte utbilda tjänsten som tillämpar smarta taggar på videoklipp med hjälp av specifika videoklipp. Det fungerar med standardinställningarna för [!DNL Adobe Sensei].

* Taggningsförloppet visas inte.

* Endast videoklipp som är mindre än 300 MB i filstorlek taggas automatiskt. Tjänsten [!DNL Adobe Sensei] hoppar över videofiler som är större.

* Endast videoklipp i de filformat och kodekar som stöds och som omnämns i [Smarta taggar](/help/assets/smart-tags.md#smart-tags-supported-file-formats) är taggade.

>[!MORELIKETHIS]
>
>* [Hantera smarta taggar och resurssökningar](smart-tags.md#manage-smart-tags-and-searches)
>* [Utbilda tjänsten Smart Tag och tagga dina bilder](smart-tags.md)


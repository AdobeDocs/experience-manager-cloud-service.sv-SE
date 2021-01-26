---
title: Hantera videoresurser
description: Överför, förhandsgranska, kommentera och publicera videomaterial i [!DNL Adobe Experience Manager].
contentOwner: AG
translation-type: tm+mt
source-git-commit: deab2183447e64e8a98f3072ceab2ef2216c4528
workflow-type: tm+mt
source-wordcount: '608'
ht-degree: 6%

---


# Hantera videoresurser {#manage-video-assets}

Videoformatet är en viktig del av ett företags digitala resurser. [!DNL Adobe Experience Manager] erbjuder mogna erbjudanden och funktioner för att hantera hela livscykeln för videomaterialet när de har skapats.

Lär dig hur du hanterar och redigerar videoresurserna i [!DNL Adobe Experience Manager Assets]. Videokodning och omkodning, till exempel FFmpeg-omkodning, är möjlig med Bearbeta profiler och [!DNL Dynamic Media]-integrering. Utan [!DNL Dynamic Media]-licens ger [!DNL Experience Manager] grundläggande stöd för videoklipp, till exempel omkodning med FFmpeg, extrahering av förhandsvisningsminiatyrer för de filformat som stöds samt förhandsgranskning i användargränssnittet för format som stöds för direktuppspelning i webbläsaren.

## Överför och förhandsgranska videomaterial {#upload-and-preview-video-assets}

[!DNL Adobe Experience Manager Assets] skapar förhandsvisningar för videoresurser med filnamnstillägget MP4. Du kan förhandsgranska återgivningarna i [!DNL Assets]-användargränssnittet.

1. Navigera till den plats där du vill lägga till digitala resurser i mappen eller undermapparna för digitala resurser.
1. Om du vill överföra resursen klickar du på **[!UICONTROL Create]** i verktygsfältet och väljer **[!UICONTROL Files]**. Du kan också dra en fil till användargränssnittet. Mer information finns i [överföra resurser](manage-digital-assets.md#uploading-assets).
1. Om du vill förhandsgranska en video i kortvyn klickar du på **[!UICONTROL Play]** ![uppspelningsalternativet](assets/do-not-localize/play.png) för videoresursen. Du kan bara pausa eller spela upp video i kortvyn. Alternativen [!UICONTROL Play] och [!UICONTROL Pause] är inte tillgängliga i listvyn.
1. Om du vill förhandsgranska videon på sidan med resursinformation väljer du **[!UICONTROL Edit]** på kortet. Videon spelas upp i webbläsarens inbyggda videospelare. Du kan spela upp, pausa, styra volymen och zooma videon till helskärm.

## Publicera videoresurser {#publish-video-assets}

Efter publiceringen kan du inkludera videomaterialet på en webbsida som en URL eller bädda in resurserna direkt. Mer information finns i [publicera [!DNL Dynamic Media] resurser](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

## Omkoda med Bearbetningsprofil {#transcode-video}

[!DNL Experience Manager] som  [!DNL Cloud Service] gör att du kan utföra grundläggande omkodning av MP4-videofiler med Bearbeta profiler. Med den här funktionen kan du inte bara överföra utan även förhandsgranska och skala en MP4-videofil.

![Skapa bearbetningsprofil för videoomkodning i  [!DNL Experience Manager]](assets/video-processing-profile-for-mp4.png)

*Bild: En bearbetningsprofil för videoomkodning i  [!DNL Experience Manager].*

Om du bara anger bredd eller enbart höjd och lämnar det andra fältet tomt behåller återgivningarna proportionerna. H.264-videokodeken finns tillgänglig för transkodning.

Om du vill bearbeta resurser med en bearbetningsprofil lägger du till en profil i en mapp. Se [använd bearbetningsprofiler för att bearbeta resurser](/help/assets/asset-microservices-configure-and-use.md#use-profiles).

## Kommentera videoresurser {#annotate-video-assets}

1. På [!DNL Assets]-konsolen väljer du **[!UICONTROL Edit]** på resurskortet för att visa sidan med resursinformation.
1. Om du vill spela upp videon klickar du på **[!UICONTROL Preview]**.
1. Klicka på **[!UICONTROL Annotate]** om du vill kommentera videon. En anteckning läggs till vid en viss tidpunkt (bildruta) i videon. När du gör anteckningar kan du rita på arbetsytan och ta med en kommentar med ritningen. Kommentarerna sparas automatiskt. Om du vill avsluta anteckningsguiden klickar du på **[!UICONTROL Close]**.
1. Gå till en viss punkt i videon, ange tiden i sekunder i **textfältet** och klicka på **Hoppa**. Om du till exempel vill hoppa över de första 20 sekunderna av videon anger du 20 i textfältet.
1. Klicka på en anteckning om du vill visa den i tidslinjen. Om du vill ta bort anteckningen från tidslinjen klickar du på **[!UICONTROL Delete]**.

## God praxis och begränsningar {#tips-limitations}

* Utan [!DNL Dynamic Media]-licens kan du bara bearbeta MP4-filer med bearbetningsprofiler.
* När MP4-filer kodas om med Bearbeta profiler gäller följande riktlinjer och begränsningar:

   * Apple ProRes-filer kan bara koda om till en maximal upplösning på 1080p.
   * Om källfilen har en bithastighet på >200 Mbit/s kan du bara omkoda till en maximal upplösning på 1080p.
   * Om källbildrutefrekvensen är >=60 fps blir den maximala storleken på källfilen som du kan använda:

      * 400 MB för 4K-omkodning.
      * 800 MB för 1080p-omkodning.
      * 8 GB för 720p-omkodning.
   * Maximal filstorlek som du kan omkoda till en upplösning på 4 000 v/min är 2,55 GB MP4-fil med en upplösning på 4 000, en bithastighet på 12 Mbit/s och 23 fps.


>[!MORELIKETHIS]
>
>* [Dynamic Media videodokumentation](/help/assets/dynamic-media/video.md).
>* [Lär dig mer om användning, typer och konfiguration av bearbetningsprofiler](/help/assets/asset-microservices-configure-and-use.md).


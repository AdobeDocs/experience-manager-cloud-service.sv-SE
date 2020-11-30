---
title: Hantera videoresurser
description: Överför, förhandsgranska, kommentera och publicera videomaterial i [!DNL Adobe Experience Manager].
contentOwner: AG
translation-type: tm+mt
source-git-commit: 8b1cc8af67c6d12d7e222e12ac4ff77e32ec7e0e
workflow-type: tm+mt
source-wordcount: '528'
ht-degree: 7%

---


# Hantera videoresurser {#manage-video-assets}

Videoformatet är en viktig del av ett företags digitala resurser. [!DNL Adobe Experience Manager] erbjuder mogna erbjudanden och funktioner för att hantera hela livscykeln för videomaterialet när de har skapats.

Lär dig hur du hanterar och redigerar videoresurserna i [!DNL Adobe Experience Manager Assets]. Videokodning och omkodning, till exempel FFmpeg-omkodning, är möjlig med Bearbeta profiler och genom [!DNL Dynamic Media] integrering. Utan [!DNL Dynamic Media] licens [!DNL Experience Manager] ger grundläggande stöd för videor, till exempel omkodning med hjälp av MPEG, extrahering av förhandsvisningsminiatyrer för de filformat som stöds samt förhandsgranskning i användargränssnittet för format som stöds för direktuppspelning i webbläsaren.

## Överföra och förhandsgranska videomaterial {#upload-and-preview-video-assets}

[!DNL Adobe Experience Manager Assets] skapar förhandsvisningar för videoresurser med filnamnstillägget MP4. Du kan förhandsgranska återgivningarna i [!DNL Assets] användargränssnittet.

1. Navigera till den plats där du vill lägga till digitala resurser i mappen eller undermapparna för digitala resurser.
1. Om du vill överföra resursen klickar du **[!UICONTROL Create]** i verktygsfältet och väljer **[!UICONTROL Files]**. Du kan också dra en fil till användargränssnittet. Mer information finns i [Överför resurser](manage-digital-assets.md#uploading-assets) .
1. Om du vill förhandsgranska en video i kortvyn klickar du på alternativet **[!UICONTROL Play]** för ![](assets/do-not-localize/play.png) uppspelning på videoresursen. Du kan bara pausa eller spela upp video i kortvyn. Alternativen [!UICONTROL Play] och [!UICONTROL Pause] är inte tillgängliga i listvyn.
1. Om du vill förhandsgranska videon på sidan med resursinformation väljer du **[!UICONTROL Edit]** på kortet. Videon spelas upp i webbläsarens inbyggda videospelare. Du kan spela upp, pausa, styra volymen och zooma videon till helskärm.

## Publicera videomaterial {#publish-video-assets}

Efter publiceringen kan du inkludera videomaterialet på en webbsida som en URL eller bädda in resurserna direkt. Mer information finns i [Publicera dynamiska medieresurser](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

## Omkoda med Bearbetningsprofil {#transcode-video}

[!DNL Experience Manager] som Cloud Service kan du utföra grundläggande omkodning av MP4-videofiler med Bearbeta profiler. Med den här funktionen kan du inte bara överföra utan även förhandsgranska och skala en MP4-videofil.

![Skapa bearbetningsprofil för videoomkodning i Experience Manager](assets/video-processing-profile-for-mp4.png)

*Bild: En bearbetningsprofil för videoomkodning i [!DNL Experience Manager].*

Om du bara anger bredd eller enbart höjd och lämnar det andra fältet tomt behåller återgivningarna proportionerna. För närvarande är bara h264-kodek tillgänglig för omkodning.

Om du vill bearbeta resurser med en bearbetningsprofil lägger du till en profil i en mapp. Se [Använda bearbetningsprofiler för att bearbeta resurser](/help/assets/asset-microservices-configure-and-use.md#use-profiles).

## Kommentera videomaterial {#annotate-video-assets}

1. I [!DNL Assets] konsolen väljer du **[!UICONTROL Edit]** på resurskortet för att visa sidan med resursinformation.
1. Om du vill spela upp videon klickar du på **[!UICONTROL Preview]**.
1. Om du vill kommentera videon klickar du på **[!UICONTROL Annotate]**. En anteckning läggs till vid en viss tidpunkt (bildruta) i videon. När du gör anteckningar kan du rita på arbetsytan och ta med en kommentar med ritningen. Kommentarerna sparas automatiskt. Om du vill avsluta anteckningsguiden klickar du på **[!UICONTROL Close]**.
1. Gå till en viss punkt i videon, ange tiden i sekunder i **textfältet** och klicka på **Hoppa**. Om du till exempel vill hoppa över de första 20 sekunderna av videon anger du 20 i textfältet.
1. Klicka på en anteckning om du vill visa den i tidslinjen. Om du vill ta bort anteckningen från tidslinjen klickar du på **[!UICONTROL Delete]**.

## God praxis och begränsningar {#tips-limitations}

* Utan Dynamic Media-licens kan du bara bearbeta MP4-filer med bearbetningsprofiler.
* För grundläggande omkodning med

>[!MORELIKETHIS]
>
>* [Videodokumentation](/help/assets/dynamic-media/video.md)för Dynamic Media.
>* [Lär dig mer om användning, typer och konfiguration av bearbetningsprofiler](/help/assets/asset-microservices-configure-and-use.md).


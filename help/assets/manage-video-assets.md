---
title: Hantera videomaterial
description: Lär dig hur du överför, förhandsgranskar, kommenterar och publicerar videomaterial.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff

---


# Hantera videomaterial {#manage-video-assets}

Lär dig hur du hanterar och redigerar videoresurser i Adobe Experience Manager (AEM) Assets. <!-- Also, if you are licensed to use Dynamic Media, see the [Dynamic Media video documentation](/help/assets/dynamic-media/video.md). -->

## Överföra och förhandsgranska videomaterial {#upload-and-preview-video-assets}

Adobe Experience Manager Assets genererar förhandsgranskningar för videoresurser med tillägget MP4. Om formatet för resursen inte är MP4 installerar du FFMPEG-paketet för att generera en förhandsvisning. FFMPEG skapar videoåtergivningar av typen OGG och MP4. Du kan förhandsgranska dessa återgivningar i användargränssnittet för AEM Resurser.

1. Navigera till den plats där du vill lägga till digitala resurser i mappen eller undermapparna Digital Assets.
1. Om du vill överföra resursen klickar du på eller trycker på **[!UICONTROL Skapa]** i verktygsfältet och väljer sedan **[!UICONTROL Filer]**. Du kan också släppa det direkt i resursområdet. Mer information om överföring finns i [Överföra resurser](manage-digital-assets.md#uploading-assets) .
1. Om du vill förhandsgranska en video i kortvyn trycker du på **[!UICONTROL uppspelningsknappen]** på videoresursen. Du kan bara pausa eller spela upp video i kortvyn. Knapparna [!UICONTROL Spela] upp och [!UICONTROL Paus] är inte tillgängliga i listvyn.
1. Om du vill förhandsgranska videon på sidan med resursinformation klickar eller trycker du på ikonen **[!UICONTROL Redigera]** på kortet. Videon spelas upp i webbläsarens inbyggda videospelare. Du kan spela upp, pausa, styra volymen och zooma videon till helskärm.

## Konfiguration för att överföra resurser som är större än 2 GB {#configuration-to-upload-assets-that-are-larger-than-gb}

Som standard kan du inte överföra resurser som är större än 2 GB på grund av en begränsad filstorlek med Experience Manager Assets. Du kan dock skriva över den här gränsen genom att gå till CRXDE Lite och skapa en nod under `/apps` katalogen. Noden måste ha samma nodnamn, katalogstruktur och jämförbara nodegenskaper i ordningen.

Förutom Experience Manager Assets-konfigurationen kan du ändra följande konfigurationer för att överföra stora resurser:

* Öka tokens förfallotid. <!-- See [!UICONTROL Adobe Granite CSRF Servlet] in Web Console at `https://[aem_server]:[port]/system/console/configMgr`. For more information, see [CSRF protection](/help/sites-developing/csrf-protection.md). -->
* Öka `receiveTimeout` i Dispatcher-konfigurationen. Mer information finns i [Experience Manager Dispatcher-konfiguration](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#renders-options).

>[!NOTE]
>
>Användargränssnittet i AEM Classic har ingen begränsning för filstorlek på 2 GB. Slutgiltigt arbetsflöde för stor video stöds inte heller helt.

Utför följande steg i `/apps` katalogen för att konfigurera en större filstorleksgräns.

1. I AEM trycker du på **[!UICONTROL Verktyg]** > **[!UICONTROL Allmänt]** > **[!UICONTROL CRXDE Lite]**.
1. Navigera till CRXDE Lite `/libs/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`. Tryck på `>>` ikonen om du vill visa katalogfönstret.
1. Tryck på **[!UICONTROL Overlay Node]** i verktygsfältet. Du kan också välja **[!UICONTROL Överläggsnod]** på snabbmenyn.
1. I dialogrutan **[!UICONTROL Overlay Node]** (Överläggningsnod) trycker du på **[!UICONTROL OK]**.
1. Uppdatera webbläsaren. Överläggsnoden `/jcr_root/apps/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload` är markerad.
1. På fliken **[!UICONTROL Egenskaper]** anger du ett värde i byte för att öka storleksgränsen till önskad storlek. Om du till exempel vill öka storleksgränsen till 30 GB anger du `{sizeLimit : "32212254720"}` ett värde.

1. Tryck på **[!UICONTROL Spara alla]** i verktygsfältet.
1. I AEM trycker du på **[!UICONTROL Verktyg]** > **[!UICONTROL Åtgärder]** > **[!UICONTROL Webbkonsol]**.
1. På sidan Adobe Experience Manager Web Console Bundles, under kolumnen Namn i tabellen, letar du upp och trycker på **[!UICONTROL Adobe Granite Workflow External Process Job Handler]**.
1. På sidan Extern processhanterare för Adobe Granite-arbetsflöde anger du sekunder för fälten **[!UICONTROL Standardtimeout]** och **[!UICONTROL Maximal timeout]** till `18000` (fem timmar).
1. Tryck på **[!UICONTROL Spara]**.
1. I AEM trycker du på **[!UICONTROL Verktyg]** > **[!UICONTROL Arbetsflöde]** > **[!UICONTROL Modeller]**.
1. På sidan Arbetsflödesmodeller väljer du **[!UICONTROL Dynamic Media Encode Video]** och sedan trycker du på **[!UICONTROL Edit]**.
1. Dubbeltryck på **[!UICONTROL komponenten Dynamic Media Video Service Process]** på arbetsflödessidan.
1. Expandera [!UICONTROL Avancerade inställningar] under fliken **[!UICONTROL Allmänt]** i dialogrutan **Stegegenskaper**.
1. I fältet **[!UICONTROL Timeout]** anger du värdet `18000`och trycker sedan på **[!UICONTROL OK]** för att återgå till arbetsflödessidan för **[!UICONTROL Dynamic Media Encode Video]** .
1. Långt upp på sidan, under rubriken Dynamic Media Encode Video, trycker du på **[!UICONTROL Save]**.

## Publicera videomaterial {#publish-video-assets}

När videomaterialet har publicerats kan du inkludera det på en webbsida via en URL eller genom att bädda in det på en webbsida. Se [Publicera resurser](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

## Kommentera videomaterial {#annotate-video-assets}

1. I resurskonsolen klickar eller trycker du på ikonen [!UICONTROL Redigera] på resurskortet för att visa sidan med resursinformation.
1. Om du vill spela upp videon klickar eller trycker du på ikonen [!UICONTROL Förhandsgranska] .
1. Om du vill kommentera videon klickar du på knappen **[!UICONTROL Anteckna]** . En anteckning läggs till vid den särskilda tidspunkten (bildrutan) i videon. När du gör anteckningar kan du rita på arbetsytan och ta med en kommentar med ritningen. Kommentarerna sparas automatiskt. Om du vill avsluta anteckningsguiden klickar du på **[!UICONTROL Stäng]**.
1. Gå till en viss punkt i videon, ange tiden i sekunder i **textfältet** och klicka på **Hoppa**. Om du till exempel vill hoppa över de första 10 sekunderna av video anger du 20 i textfältet.
1. Klicka på en anteckning om du vill visa den i tidslinjen. Om du vill ta bort anteckningen från tidslinjen klickar du på **[!UICONTROL Ta bort]**.

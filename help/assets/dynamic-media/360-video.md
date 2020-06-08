---
title: 360/VR-video
description: Lär dig hur du arbetar med 360- och VR-video (Virtual Reality) i Dynamic Media.
translation-type: tm+mt
source-git-commit: 6224d193adfb87bd9b080f48937e0af1f03386d6
workflow-type: tm+mt
source-wordcount: '953'
ht-degree: 0%

---


# 360/VR Video {#vr-video}

360-gradersvyer spelar in en vy i alla riktningar samtidigt. De filmas med en omdirigerad kamera eller en samling kameror. Vid uppspelning på en platt skärm har användaren kontroll över betraktningsvinkeln. uppspelning på mobila enheter utnyttjar vanligtvis de inbyggda gyroskopiska kontrollerna.

Dynamic Media har inbyggt stöd för leverans av 360 videomaterial. Som standard krävs ingen ytterligare konfiguration för visning eller uppspelning. Du levererar 360-video med standardvideotillägg som .mp4, .mkv och .mov. Den vanligaste kodeken är H.264.

I det här avsnittet beskrivs hur du arbetar med 360/VR Video Viewer för att återge ekvirektangulär video för en engagerande tittarupplevelse av ett rum, en egenskap, plats, landskap, medicinska procedurer och så vidare.

Spatial audio stöds för närvarande inte. om ljudet blandas i stereo ändras inte balansen (L/R) när kunden ändrar kamerans visningsvinkel.

Se [Använda Dynamic Media 360-videor och en anpassad videominiatyr med AEM Assets](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/dynamic-media/dynamic-media-360-video-custom-thumbnail-feature-video-use.html).

Se även [Hantera visningsförinställningar](/help/assets/dynamic-media/managing-viewer-presets.md).

## 360 Video in action {#video-in-action}

Tryck på [Space Station 360](http://mobiletest.scene7.com/s7viewers/html5/Video360Viewer.html?asset=Viewers/space_station_360-AVS) för att öppna ett webbläsarfönster och titta på en 360-gradersvideo. Under videouppspelningen drar du muspekaren till en ny plats för att ändra visningsvinkeln.

![360 Videoexempel](assets/6_5_360videoiss_simplified.png)*Videobildruta från Space Station 360*

## 360/VR Video och Adobe Premiere Pro {#vr-video-and-adobe-premiere-pro}

Du kan använda Adobe Premier Pro för att visa och redigera 360/VR-film. Du kan till exempel placera logotyper och text på rätt sätt i en scen och använda effekter och övergångar som är särskilt utformade för ekvirektangulära medier.

Se [Redigera 360/VR-video](https://helpx.adobe.com/premiere-pro/how-to/edit-360-vr-video.html).

## Överföra resurser som ska användas med 360-videovisningsprogrammet {#uploading-assets-for-use-with-the-video-viewer}

360 videomaterial som överförs till AEM kallas **Multimedia** på en Assets-sida, ungefär som vanliga videomaterial.

![6_5_360video-selectopreview](assets/6_5_360video-selecttopreview.png)*En överförd 360-videoresurs som visas i kortvyn. Resursen är märkt som Multimedia.*

**Så här överför du resurser som ska användas med 360-videovisningsprogrammet:**

1. Skapade en mapp som är dedikerad till ditt 360-videomaterial.
1. [Använd en adaptiv videoprofil på mappen](/help/assets/dynamic-media/video-profiles.md#applying-a-video-profile-to-folders).

   Om du återger 360-videoinnehåll ställs högre krav på källvideoupplösning och för kodad återgivningsupplösning än standardvideoinnehåll som inte är 360.

   Du kan använda den färdiga adaptiva videoprofilen som redan finns i Dynamic Media. Tänk dock på att det ger betydligt lägre 360-videokvalitet än vad du skulle få för icke-360-video som är kodad med samma inställningar som återges med ett icke-360-videovisningsprogram. Om 360-video med hög kvalitet krävs gör du därför följande:

   * Helst bör ditt ursprungliga 360-videoinnehåll ha någon av följande upplösningar:

      * 1080p - 1920 x 1080, känd som Full HD eller FHD upplösning eller
      * 2160p - 3840 x 2160, känd som 4K-, UHD- eller Ultra HD-upplösning. Den här mycket stora skärmupplösningen finns oftast på tv-apparater och datorskärmar. Upplösningen 2160p kallas ofta för&quot;4K&quot; eftersom bredden är nästan 4 000 pixlar. Med andra ord har den fyra gånger så många pixlar som 1080p.
   * [Skapa en anpassad adaptiv videoprofil](/help/assets/dynamic-media/video-profiles.md#creating-a-video-encoding-profile-for-adaptive-streaming) med renderingar av högre kvalitet. Du kan till exempel skapa en adaptiv videoprofil som innehåller följande tre inställningar:

      * width=auto; height=720; bithastighet=2 500 kbit/s
      * width=auto; height=1080; bithastighet=5000 kbit/s
      * width=auto; height=1440; bithastighet=6600 kbit/s
   * Bearbeta 360-videoinnehåll i en mapp som är exklusivt dedikerad till 360-videoresurser.
   Tänk på att detta tillvägagångssätt också kommer att ställa större krav på slutanvändarens nätverk och CPU.

1. [Överför videon till mappen](/help/assets/manage-video-assets.md#upload-and-preview-video-assets).

<!--

## Overriding the default aspect ratio of 360 videos  {#overriding-the-default-aspect-ratio-of-videos}

For an uploaded asset to qualify as a 360 video that you intend to use with the 360 Video viewer, the asset must have an aspect ratio of 2.

By default, AEM detects video as "360" if its aspect ratio (width/height) is 2.0. If you are an Administrator, you can override the default aspect ratio setting of 2 by setting the optional `s7video360AR` property in CRXDE Lite at the following:

* `/conf/global/settings/cloudconfigs/dmscene7/jcr:content`

  * **Property type**: Double
  * **Value**: floating-point aspect ratio, default 2.0.

After you set this property, it takes effect immediately on both existing videos and newly uploaded videos.

The aspect ratio applies to 360 video assets for the asset details page and the [Video 360 Media WCM component](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md#dynamic-media-components).

Start by uploading 360 Videos.

-->

## Förhandsgranska 360-video {#previewing-video}

Du kan använda Förhandsgranska för att se hur 360-videon ser ut för kunderna och kontrollera att den beter sig som förväntat.

Se även [Redigera visningsförinställningar](/help/assets/dynamic-media/managing-viewer-presets.md#editing-viewer-presets).

När du är nöjd med 360-videon kan du publicera den.

See [Embedding the Video or Image Viewer on a Web Page](/help/assets/dynamic-media/embed-code.md).
See [Linking URLs to your web application](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md). Observera att den URL-baserade länkningsmetoden inte är möjlig om ditt interaktiva innehåll har länkar till relativa URL:er, särskilt länkar till AEM Sites-sidor.
See [Adding Dynamic Media Assets to pages.](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)

**Så här förhandsgranskar du 360-videoklipp**

1. Navigera **[!UICONTROL Assets]** till en befintlig 360-video som du har skapat. Tryck på 360-videoresursen för att öppna den i förhandsgranskningsläge.

   ![6_5_360video-selecttopreview-1](assets/6_5_360video-selecttopreview-1.png)

   Tryck på 360-videoresursen för att förhandsgranska videon.

1. Tryck på listrutan på förhandsvisningssidan, i det övre vänstra hörnet av sidan, och välj sedan **[!UICONTROL Viewers]**.

   ![6_5_360video-preview-viewers](assets/6_5_360video-preview-viewers.png)

   Tryck på **[!UICONTROL Video360_social]** i visningslistan och gör sedan något av följande:

   * Dra muspekaren över videon om du vill ändra visningsvinkeln för den statiska scenen.
   * Tryck på videoknappen för att börja spela upp videon **[!UICONTROL Play]** . När videon spelas upp drar du muspekaren över videon för att ändra visningsvinkeln.
   ![6_5_360video-preview-video360-](assets/6_5_360video-preview-video360-social.png)*socialA 360 video, skärmdump.*

   * Tryck på i visningslistan **[!UICONTROL Video360VR]**.

      VR-video (Virtual Reality) är engagerande videomaterial som nås via virtuella verklighetshuvuden. Precis som med vanliga videor skapar du VR-videor i början när en video spelas in eller spelas in med 360-graderskameror.
   ![6_5_360video-preview-video360vr](assets/6_5_360video-preview-video360vr.png)
   *En 360 VR-videobildskärm.*

1. Tryck på i det övre högra hörnet på förhandsvisningssidan **[!UICONTROL Close]**.

## Publicera 360-video {#publishing-video}

Du måste publicera 360-videon för att kunna använda den. När du publicerar en 360-video aktiveras URL:en och Bädda in kod. Dessutom publiceras 360-videon i Dynamic Media Cloud, som är integrerat med ett CDN för skalbar och prestandaoptimerad leverans.

Mer information om hur du publicerar 360-video finns i [Publicera dynamiska medieresurser](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md) .
See also [Embedding the Video or Image Viewer on a Web Page](/help/assets/dynamic-media/embed-code.md).
See also [Linking URLs to your web application](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md). Observera att den URL-baserade länkningsmetoden inte är möjlig om ditt interaktiva innehåll har länkar till relativa URL:er, särskilt länkar till AEM Sites-sidor.
See also [Adding Dynamic Media Assets to pages.](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)

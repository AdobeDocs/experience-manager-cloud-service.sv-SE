---
title: 360/VR-video
description: Lär dig hur du arbetar med 360- och VR-video (Virtual Reality) i Dynamic Media.
translation-type: tm+mt
source-git-commit: 5ff144ffd43501d04d8295d3726fe2368e9b4389
workflow-type: tm+mt
source-wordcount: '932'
ht-degree: 0%

---


# 360/VR-video {#vr-video}

360-gradersvyer spelar in en vy i alla riktningar samtidigt. De filmas med en omdirigerad kamera eller en samling kameror. Vid uppspelning på en platt skärm har användaren kontroll över betraktningsvinkeln. de inbyggda gyroskopiska kontrollerna används vanligtvis vid uppspelning på mobila enheter.

Dynamic Media har inbyggt stöd för leverans av 360 videomaterial. Som standard krävs ingen ytterligare konfiguration för visning eller uppspelning. Du levererar 360-video med standardvideotillägg som .mp4, .mkv och .mov. Den vanligaste kodeken är H.264.

Du kan använda 360/VR-visningsprogrammet för att återge ekvirektangulär video. Resultatet blir en engagerande tittarupplevelse av ett rum, en fastighet, en plats, ett landskap, ett medicinskt förfarande och så vidare.

Spatial audio stöds för närvarande inte. om ljudet blandas i stereo ändras inte balansen (L/R) när kunden ändrar kamerans visningsvinkel.

Se [Använda Dynamic Media 360-videoklipp och miniatyrbild för anpassad video med AEM Assets](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-360-video-custom-thumbnail-feature-video-use.html#dynamic-media).

Se även [Hantera visningsförinställningar](/help/assets/dynamic-media/managing-viewer-presets.md).

## 360 Video in action {#video-in-action}

Tryck på [Space Station 360](http://mobiletest.scene7.com/s7viewers/html5/Video360Viewer.html?asset=Viewers/space_station_360-AVS) för att öppna ett webbläsarfönster och titta på en 360-gradersvideo. Under videouppspelningen drar du pekaren till en ny plats för att ändra visningsvinkeln.

![360-](assets/6_5_360videoiss_simplified.png)
*videoexempelVideobildruta från Space Station 360*

## 360/VR Video och Adobe Premiere Pro {#vr-video-and-adobe-premiere-pro}

Du kan använda Adobe Premier Pro för att visa och redigera 360/VR-filmer. Du kan till exempel placera logotyper och text på rätt sätt i en scen och använda effekter och övergångar som är särskilt utformade för ekvirektangulära medier.

Se [Redigera 360/VR-video](https://helpx.adobe.com/premiere-pro/how-to/edit-360-vr-video.html).

## Överför resurser som ska användas med 360-videovisningsprogrammet {#uploading-assets-for-use-with-the-video-viewer}

360 videomaterial som överförs till Experience Manager namnges som **Multimedia** på en tillgångssida, på liknande sätt som vanliga videomaterial.

![6_5_360video-](assets/6_5_360video-selecttopreview.png)
*selectPreviewEn överförd 360-videoresurs som visas i kortvyn. Resursen är märkt som Multimedia.*

**Så här överför du resurser som ska användas med 360-videovisningsprogrammet:**

1. Skapade en mapp som är dedikerad till ditt 360-videomaterial.
1. [Använd en adaptiv videoprofil på mappen](/help/assets/dynamic-media/video-profiles.md#applying-a-video-profile-to-folders).

   Om du återger 360-videoinnehåll ställs högre krav på källvideoupplösning och för kodad återgivningsupplösning än standardvideoinnehåll som inte är 360.

   Du kan använda den färdiga adaptiva videoprofilen som redan finns i Dynamic Media. Det ger dock betydligt lägre 360-videokvalitet än vad du skulle få för icke-360-video som är kodad med samma inställningar som återges med ett icke-360-videovisningsprogram. Om 360-video med hög kvalitet krävs gör du därför följande:

   * Helst har ditt ursprungliga 360-videoinnehåll någon av följande upplösningar:

      * 1080p - 1920 x 1080, känd som Full HD eller FHD upplösning eller
      * 2160p - 3840 x 2160, känd som 4K-, UHD- eller Ultra HD-upplösning. Den här stora skärmupplösningen finns oftast på tv-apparater och datorskärmar. Upplösningen 2160p kallas ofta för&quot;4K&quot; eftersom bredden är nästan 4 000 pixlar. Med andra ord har den fyra gånger så många pixlar som 1080p.
   * [Skapa en anpassad adaptiv ](/help/assets/dynamic-media/video-profiles.md#creating-a-video-encoding-profile-for-adaptive-streaming) videoprofil med renderingar av högre kvalitet. Du kan till exempel skapa en adaptiv videoprofil som innehåller följande tre inställningar:

      * Width=auto; Höjd=720; Bithastighet=2 500 kbit/s
      * Width=auto; Höjd=1080; Bithastighet=5000 kbit/s
      * Width=auto; Höjd=1440; Bithastighet=6600 kbit/s
   * Bearbeta 360-videoinnehåll i en mapp som är exklusivt dedikerad till 360-videoresurser.

   Detta tillvägagångssätt ställer större krav på slutanvändarens nätverk och processor.

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

Se [Bädda in video- eller bildvisningsprogrammet på en webbsida](/help/assets/dynamic-media/embed-code.md).
Se [Länka URL:er till ditt webbprogram](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md). Den URL-baserade länkningsmetoden är inte möjlig om det interaktiva innehållet har länkar till relativa URL-adresser, särskilt länkar till Experience Manager-sidor.
Se [Lägga till Dynamic Media Assets på sidor.](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)

**Så här förhandsgranskar du 360-videoklipp**

1. I **[!UICONTROL Assets]** navigerar du till en befintlig 360-video som du har skapat. Tryck på resursen 360 Video för att öppna den i förhandsgranskningsläge.

   ![6_5_360video-selecttopreview-1](assets/6_5_360video-selecttopreview-1.png)

   Om du vill förhandsgranska videon trycker du på 360-videoresursen.

1. Tryck på listrutan på förhandsgranskningssidan i det övre vänstra hörnet av sidan och välj **[!UICONTROL Viewers]**.

   ![6_5_360video-preview-viewers](assets/6_5_360video-preview-viewers.png)

   Tryck på **[!UICONTROL Video360_social]** i visningslistan och gör sedan något av följande:

   * Om du vill ändra visningsvinkeln för den statiska scenen drar du pekaren över videon.
   * Tryck på videoknappen **[!UICONTROL Play]** för att påbörja uppspelningen. När videon spelas upp drar du pekaren över videon för att ändra visningsvinkeln.

   ![6_5_360video-preview-video360-](assets/6_5_360video-preview-video360-social.png)*socialA 360 video, skärmdump.*

   * Tryck på **[!UICONTROL Video360VR]** i visningslistan.

      VR-video (Virtual Reality) är engagerande videomaterial som nås via virtuella verklighetshuvuden. Precis som med vanliga videor skapar du VR-videor i början när en video spelas in eller spelas in med 360-graderskameror.
   ![6_5_360video-preview-video360vr](assets/6_5_360video-preview-video360vr.png)
   *En 360 VR-videobildskärm.*

1. Tryck på **[!UICONTROL Close]** uppe till höger på förhandsgranskningssidan.

## Publicerar 360-video {#publishing-video}

Om du vill använda 360-video måste du publicera den. När du publicerar en 360-video aktiveras URL:en och Bädda in kod. Dessutom publiceras 360-videon i Dynamic Media-molnet, som är integrerat med ett CDN för skalbar leverans och leverans med höga prestanda.

Mer information om hur du publicerar 360-video finns i [Publicera Dynamic Media Assets](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).
Se även [Bädda in video- eller bildvisningsprogrammet på en webbsida](/help/assets/dynamic-media/embed-code.md).
Se även [Länka URL:er till ditt webbprogram](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md). Den URL-baserade länkningsmetoden är inte möjlig om det interaktiva innehållet har länkar till relativa URL-adresser, särskilt länkar till Experience Manager-sidor.
Se även [Lägga till Dynamic Media Assets på sidor.](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)

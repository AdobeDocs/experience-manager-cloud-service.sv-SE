---
title: Hantera förinställningar för visningsprogram
description: Lär dig hur du skapar och hanterar visningsförinställningar i Dynamic Media.
feature: Viewer Presets,Viewers
role: User
exl-id: da2e1a10-f54b-440e-b70c-f04ad4caeac1
source-git-commit: 1b9864c4532d15068b6edbd187a78a0ee0fdcfb4
workflow-type: tm+mt
source-wordcount: '4084'
ht-degree: 8%

---

# Hantera förinställningar för visningsprogram{#managing-viewer-presets}

En visningsförinställning är en samling inställningar som bestämmer hur användare visar mediefiler på datorskärmar och mobila enheter. Om du är administratör kan du skapa visningsförinställningar. Inställningarna är tillgängliga för en array med visningskonfigurationsalternativ. Du kan till exempel ändra visningsprogrammets visningsstorlek eller zoombeteende.

<!-- OBSOLETE SDK withdrawn from public view. Available internally only at `http://staging.scene7.com/s7sdk/3.8/docs/jsdoc/symbols/_s7sdk.html` 

For instructions on creating and customizing your own HTML5 viewer presets, see the *Adobe Scene7 HTML5 Viewer SDK*. The SDK is available on the IS publish server embedded in the SDK itself. Each library version has its own SDK documentation included.

Path: `<scene7_domain>/s7sdk/<library_version>/docs/jsdocs/index.html`.
For example, 3.5 SDK: [https://s7d1.scene7.com/s7sdk/3.5/docs/jsdoc/index.html](https://s7d1.scene7.com/s7sdk/3.5/docs/jsdoc/index.html)

-->

Se även [Referenshandbok för Dynamic Media Viewer](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources.html).

I det här avsnittet beskrivs hur du skapar, redigerar och hanterar visningsprogramförinställningar. Du kan använda en visningsförinställning för en resurs när du vill förhandsgranska den. Se [Använd förinställningar för visningsprogram](#applying-a-viewer-preset-to-an-asset).

>[!NOTE]
>
>Redigera alla *fördefinierade färdiga förinställningar för visningsprogram* är inte ett scenario som stöds. Om du försöker redigera en visningsförinställning som inte är klar uppmanas du att spara visningsförinställningen med ett nytt namn.

## Tangentbordstillgänglighet för tittare {#keyboard-accessibility-for-viewers}

Alla färdiga visningsprogram har stöd för tangentbordstillgänglighet.

Se även [Tangentbordstillgänglighet och -navigering](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/c-keyboard-accessibility.html).

## Hantera förinställningar för visningsprogram {#managing-viewer-presets-1}

Du kan lägga till, redigera, ta bort, publicera, avpublicera och förhandsgranska visningsförinställningar i Adobe Experience Manager genom att gå till **[!UICONTROL Tools]** (hammarikon) > **[!UICONTROL Assets]>[!UICONTROL Viewer Presets]**.

![6_5_tools-assets-viewerpresets](assets/6_5_tools-assets-viewerpresets.png)

>[!NOTE]
>
>Som standard visas 15 visningsförinställningar när du väljer visningsprogram i detaljvyn för en resurs. Du kan öka den här gränsen. Se [Öka antalet visningsförinställningar som visas](#increasing-the-number-of-viewer-presets-that-display).

### Stöd för visningsprogram för responsiva webbsidor {#viewer-support-for-responsive-designed-web-pages}

Olika webbsidor har olika behov. Ibland kanske du vill ha en webbsida som innehåller en länk som öppnar visningsprogrammet för HTML 5 i ett separat webbläsarfönster. I andra fall måste du bädda in HTML5-visningsprogrammet direkt på värdsidan. I det senare fallet har webbsidan en statisk layout. Eller så är den&quot;responsiv&quot; och visas på olika enheter eller för olika webbläsarfönsterstorlekar. För att tillgodose dessa behov har alla fördefinierade, färdiga HTML5-visningsprogram som medföljer Dynamic Media stöd för både statiska webbsidor och responsiva webbsidor.

Se [Responsiv statisk bildbibliotek](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/responsive-static-image-library/c-about-responsive-static-image-library.html#about-responsive-image-library) i *Hjälp om Dynamic Media Image Serving and Rendering API* om du vill ha mer information om hur du bäddar in responsiva visningsprogram på dina webbsidor.

>[!NOTE]
>
>Publicera alla färdiga visningsprogram innan du använder dem för första gången.
>Se [Publicera förinställningar för visningsprogram](#publishing-viewer-presets).

### Systemkompatibilitet för visningsförinställningar  {#viewer-preset-system-compatibility}

Alla färdiga visningsförinställningar som medföljer Dynamic Media är helt kompatibla med följande system:

* Stationära datorer
* Apple iPhone
* Apple iPad
* Android™ Smartphone
* Android™ Tablet PC

<!-- OUTDATED 2/25/22 * For video, extra support for MP4 playback is provided for [BlackBerry®](https://developer.blackberry.com/devzone/develop/supported_media/bb_media_support_at_a_glance.html#kba1328730952678) and [Windows® Phone](https://docs.microsoft.com/en-us/windows/uwp/audio-video-camera/supported-codecs). -->

### Multimedietyper för visningsförinställningar {#rich-media-types-for-viewer-presets}

Administratörer kan lägga till och anpassa följande typer av multimedia när de skapar visningsförinställningar.

<table>
 <tbody>
  <tr>
   <td><strong>Carousel Set</strong><br /> </td>
   <td><p>Aktiveringspunkter, bildscheman eller båda läggs till i en serie med två eller flera bilder. Kunden kan panorera bilderna åt vänster eller höger och sedan markera en hotspot på en bild för mer information eller för att köpa direkt från en webbplats landning, kategori eller hemsidor.</p> </td>
  </tr>
    <tr>
   <td><strong>Dimensionell</strong><br /> </td>
   <td><p>Visar 3D-scener där du kan vrida, panorera, zooma eller centrera om kameran.</p> </td>
  </tr>
  <tr>
   <td><strong>Utfällbar zoom</strong></td>
   <td><p>Visar en andra bild av det zoomade området bredvid originalbilden. Det finns inga kontroller att använda - användarna flyttar markeringen över det område de vill visa.</p> <p>När du fastställer den fullständiga bandbreddsanvändningen för det här visningsprogrammet bör du tänka på att både huvudbilden och den utfällbara bilden visas i visningsprogrammet. Huvudbildens storlek (scenens bredd och höjd) och zoomfaktorn bestämmer den utfällbara bildens storlek. Om du vill förhindra att den utfällbara filstorleken blir för stor ska du balansera dessa två värden: om du har en stor huvudbildstorlek, sänker du zoomfaktorn. (Utfällbar bredd och Utfällbar höjd bestämmer storleken på det utfällbara fönstret, men inte storleken på den utfällbara bild som visas i visningsprogrammet.)</p> <p>Om huvudbildens storlek till exempel är 350 x 350 pixlar, med zoomfaktorn 3, blir den utfällbara bilden 1 050 x 1 050 pixlar. Om huvudbildstorleken är 300 x 300 pixlar, med zoomfaktorn 4, är den utfällbara bilden 1 200 x 1 200 pixlar. Beroende på kvalitetsinställningen för JPEG (rekommenderade inställningar är mellan 80 och 90) kan du minska filstorleken avsevärt. Rekommenderade zoomningsfaktorer är 2,5 till 4, beroende på storleken på huvudbilden.</p> </td>
  </tr>
  <tr>
   <td><strong>Textbunden zoom</strong></td>
   <td>Visar en bild av det zoomade området i det ursprungliga visningsprogrammet. Det finns inga kontroller att använda. Användarna flyttar markeringen över det område de vill visa.</td>
  </tr>
  <tr>
   <td><strong>Bilduppsättning</strong></td>
   <td>I visningsprogrammet för bilduppsättningen kan användare visa olika vyer eller färgvariationer för ett objekt genom att välja en miniatyrbild. Det här visningsprogrammet har även zoomverktyg som gör att du kan granska bilder noggrant.</td>
  </tr>
  <tr>
   <td><strong>Interaktiv bild</strong></td>
   <td>Aktiveringspunkter läggs till i delar av en bild som en kund sedan kan välja för mer information eller för köp direkt från en webbplats landning, kategori eller hemsidor.</td>
  </tr>
  <tr>
   <td><strong>Interaktiv video</strong></td>
   <td>Miniatyrbilder läggs till i tidslinjesegment i en video som en kund sedan kan välja för mer information eller för att köpa direkt från en webbplats landning, kategori eller hemsidor.</td>
  </tr>
  <tr>
   <td><strong>Blandade media</strong></td>
   <td>Visar olika typer av media i ett och samma visningsprogram. Du kan inkludera snurruppsättningar, bilduppsättningar, bilder och videoklipp.</td>
  </tr>
  <tr>
   <td><strong>Panoramabild</strong></td>
   <td><p>Visningsprogrammen Panoramabild och PanoramicVR återger sfäriska panoramabilder så att användarna kan se dem i ett 360-gradersrum, på en plats eller i ett landskap.</p> <p>För att en överförd bild ska kvalificeras som ett sfäriskt panorama måste den ha antingen ett eller båda av följande:</p>
    <ul>
     <li>Proportionerna 2:1.</li>
     <li>Taggad med nyckelorden <code>equirectangular</code>, eller <code>spherical</code> och <code>panorama</code>, eller <code>spherical </code>och <code>panoramic</code>. Se <a href="/help/sites-cloud/authoring/features/tags.md">Använda taggar</a>.</li>
    </ul> <p>Både proportioner och nyckelordskriterier gäller för panoramaresurser för sidan med resursinformation och WCM-komponenten "Panoramic Media".</p></td>
  </tr>
    <tr>
   <td><strong>Video för smart beskärning</strong><br /> </td>
   <td><p>Använd det här visningsprogrammet för att automatiskt identifiera och beskära till fokalpunkten i alla videofilmer.</p> </td>
  </tr>
  <tr>
   <td><strong>Snurra uppsättning</strong></td>
   <td>Ger flera vyer av en bild så att användare kan vrida objektet för att undersöka olika sidor och vinklar.</td>
  </tr>
  <tr>
   <td><strong>360-video</strong></td>
   <td><p>Använd 360/VR Video Viewer för att återge ekvirektangulär video för en engagerande tittarupplevelse av ett rum, en egenskap, plats, landskap eller medicinskt förfarande.</p> <p>Vid uppspelning på en platt skärm har användaren kontroll över visningsvinkeln. För uppspelning på mobila enheter används de inbyggda gyroskopiska kontrollerna.</p> <p>Visningsprogrammet har inbyggt stöd för leverans av 360 videomaterial. Som standard krävs ingen ytterligare konfiguration för visning eller uppspelning. Du levererar 360-video med standardvideotillägg som .mp4, .mkv och .mov. Den vanligaste kodeken är H.264.</p> </td>
  </tr>
  <tr>
   <td><strong>Video</strong></td>
   <td><p>Spelar upp video med strömning med progressiv eller adaptiv bithastighet. Med adaptiv bithastighetsströmning utförs automatiskt enhets- och bandbreddsidentifiering för att leverera rätt kvalitetsvideo i rätt format.</p> </td>
  </tr>
  <tr>
   <td><strong>Lodrät zoomning</strong></td>
   <td><p>Med Lodrät zoomning kan du maximera visningen av produktbilder och ge användarna bästa möjliga återgivning av en produkt. Den lodräta placeringen av färgrutor gör följande:</p>
    <ul>
     <li>Ser till att färgrutorna"ligger över vikningen".<br/> Med vågräta färgrutor, beroende på användarens skärmstorlek, visas inte färgrutorna förrän användaren rullade nedåt på sidan. Genom att placera färgrutorna lodrätt i visningsprogrammet ser du till att de visas oavsett användarens skärmstorlek.</li>
     <li>Maximerar storleken på huvudbilden.<br /> Med vågräta färgrutor måste du reservera utrymme på sidan för att se till att de är synliga. Den här placeringen minskade storleken på huvudbilden. Om du har en lodrät färgrutelayout behöver du dock inte tilldela det här utrymmet. Därför kan du maximera huvudbildstorleken.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Zoomning</strong></td>
   <td>Låter användarna zooma in i området genom att markera det. Användare kan välja kontroller för att zooma in, zooma ut och återställa bilden till standardstorleken.</td>
  </tr>
 </tbody>
</table>

### Lista med färdiga visningsförinställningar {#list-of-out-of-the-box-viewer-presets}

I följande tabell visas alla fördefinierade färdiga visningsförinställningar som medföljer Dynamic Media.

Se även [Live Demos](https://landing.adobe.com/en/na/dynamic-media/ctir-2755/live-demos.html).

Information om vilka webbläsare och operativsystemversioner som stöds för visningsprogram finns i Viewer Release Notes.

Se&quot;Viewer release notes&quot; i innehållsförteckningen i [Referenshandbok för visningsprogram](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources.html).

>[!NOTE]
>
>Alla färdiga visningsförinställningar i Dynamic Media aktiveras (på), men du måste publicera dem.
>Se [Publicera förinställningar för visningsprogram](#publishing-viewer-presets).
>
>Alla nya visningsprogramförinställningar som du skapar och lägger till måste vara aktiverade *och *publicerade.
>Se [Aktivera eller inaktivera visningsprogramförinställningar](#activating-or-deactivating-viewer-presets) och [Förinställningar för publiceringsvisningsprogram](#publishing-viewer-presets).

<table>
 <tbody>
  <tr>
   <td><strong>Förinställningsrubrik för visningsprogram</strong></td>
   <td><strong>Typ</strong></td>
   <td><strong>CSS-filnamn</strong><br /> </td>
  </tr>
  <tr>
   <td>Carousel_Doted_dark</td>
   <td>Carousel_Set</td>
   <td><code>html5_carouselviewer_dotted_dark.css</code></td>
  </tr>
  <tr>
   <td>Carousel_Doted_light</td>
   <td>Carousel_Set</td>
   <td><code>html5_carouselviewer_dotted_light.css</code></td>
  </tr>
  <tr>
   <td>Carousel_Numeric_dark</td>
   <td>Carousel_Set</td>
   <td><code>html5_carouselviewer_numeric_dark.css</code></td>
  </tr>
  <tr>
   <td>Carousel_Numeric_light</td>
   <td>Carousel_Set</td>
   <td><code>html5_carouselviewer_numeric_light.css</code></td>
  </tr>
  <tr>
   <td>Utfällbar</td>
   <td>Flyout_Zoom</td>
   <td><code>html5_flyoutviewer.css</code></td>
  </tr>
  <tr>
   <td>ImageSet_dark</td>
   <td>Bilduppsättning</td>
   <td><code>html5_zoomviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>ImageSet_light</td>
   <td>Bilduppsättning</td>
   <td><code>html5_zoomviewer_light.css</code></td>
  </tr>
  <tr>
   <td>InlineMixedMedia_dark</td>
   <td>Mixed_Media</td>
   <td><code>html5_inlinemixedmediaviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>InlineMixedMedia_light</td>
   <td>Mixed_Media</td>
   <td><code>html5_inlinemixedmediaviewer_light.css</code></td>
  </tr>
  <tr>
   <td>InlineZoom</td>
   <td>Flyout_Zoom</td>
   <td><code>html5_inlinezoomviewer.css</code></td>
  </tr>
  <tr>
   <td>MixedMedia_dark</td>
   <td>Mixed_Media</td>
   <td><code>html5_mixedmediaviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>MixedMedia_light</td>
   <td>Mixed_Media</td>
   <td><code>html5_mixedmediaviewer_light.css</code></td>
  </tr>
  <tr>
   <td>Panoramabild</td>
   <td>Panorama_bild</td>
   <td><code>html5_panoramicimage.css</code></td>
  </tr>
  <tr>
   <td>PanoramabildVR</td>
   <td>Panorama_bild</td>
   <td><code>html5_panoramicimage.css</code></td>
  </tr>
  <tr>
   <td>Shoppable_Banner</td>
   <td>Interactive_image</td>
   <td><code>html5_interactiveimage.css</code></td>
  </tr>
  <tr>
   <td>Shoppable_Video_dark</td>
   <td>Interactive_Video</td>
   <td><code>html5_interactivevideoviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>Shoppable_Video_light</td>
   <td>Interactive_Video</td>
   <td><code>html5_interactivevideovewer_light.css</code></td>
  </tr>
  <tr>
   <td>SpinSet_dark</td>
   <td>Spin_mängd</td>
   <td><code>html5_spinviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>SpinSet_light</td>
   <td>Spin_mängd</td>
   <td><code>html5_spinviewer_light.css</code></td>
  </tr>
  <tr>
   <td><p>Video</p> <p>(Inkluderar stöd för undertextning)</p> </td>
   <td>Video</td>
   <td><code>html5_videoviewer.css</code></td>
  </tr>
  <tr>
   <td><p>Video360_social</p> <p>(Innehåller grundläggande videouppspelningskontroller, videoåtergivning görs i stereoläge, manuell vykontroll är inaktiverad men gyroskopisk kontroll är aktiverad och inga sociala mediefunktioner är aktiverade)</p> </td>
   <td>Video_360</td>
   <td><code>html5_video360viewersocial.css</code></td>
  </tr>
  <tr>
   <td><p>Video360VR</p> <p>(Utformad för slutanvändare som använder virtuella verklighetsglasögon. Innehåller grundläggande videouppspelningskontroller och funktioner för sociala medier)</p> </td>
   <td>Video_360</td>
   <td><code>html5_video360viewer.css</code></td>
  </tr>
  <tr>
   <td><p>Video_social</p> <p>(Inkluderar stöd för undertexter och sociala medier)</p> </td>
   <td>Video</td>
   <td><code>html5_videoviewersocial.css</code></td>
  </tr>
  <tr>
   <td>Zoom_dark<br /> </td>
   <td>Zoomning<br /> </td>
   <td><code>html5_basiczoomviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>Zoom_light<br /> </td>
   <td>Zoomning</td>
   <td><code>html5_basiczoomviewer_light.css</code></td>
  </tr>
  <tr>
   <td>ZoomVertical_dark<br /> </td>
   <td>Lodrät_zoom</td>
   <td><code>html5_zoomverticalviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>ZoomVertical_light</td>
   <td>Lodrät_zoom</td>
   <td><code>html5_zoomverticalviewer_light.css</code></td>
  </tr>
 </tbody>
</table>

### Rörelsematris för mobilvisningsprogram som stöds {#supported-mobile-viewers-gestures-matrix}

Följande tabell visar vilka mobilvisningsgester som stöds på enheter med iOS, Android™ 2.x och Android™ 3.x.

<table>
 <tbody>
  <tr>
   <td><strong>Gesture</strong></td>
   <td><strong>Utfällbar zoom</strong></td>
   <td><strong>Zoomning</strong></td>
   <td><strong>Snurra</strong></td>
  </tr>
  <tr>
   <td><p><strong>Dra</strong></p> </td>
   <td><p>Panoreringar</p> </td>
   <td><p>Panoreringar</p> </td>
   <td><p>Panoreringar</p> </td>
  </tr>
  <tr>
   <td><p><strong>Tryck på</strong></p> </td>
   <td><p>Visar utfällbart fönster</p> </td>
   <td><p>Visar eller döljer användargränssnittet</p> </td>
   <td><p>Visar eller döljer användargränssnittet</p> </td>
  </tr>
  <tr>
   <td><p><strong>Dubbelknacka</strong></p> </td>
   <td><p>Gäller inte</p> </td>
   <td><p>Zoomar in eller återställer</p> </td>
   <td><p>Zoomar in eller återställer</p> </td>
  </tr>
  <tr>
   <td><p><strong>Knipning öppen</strong></p> </td>
   <td><p>Gäller inte</p> </td>
   <td><p>Zoomar in (endast iOS och Android™ 3x)</p> </td>
   <td><p>Zoomar in (endast iOS och Android™ 3x)</p> </td>
  </tr>
  <tr>
   <td><p><strong>Knipning - stäng</strong></p> </td>
   <td><p>Gäller inte</p> </td>
   <td><p>Zoomar ut (endast iOS och Android™ 3x)</p> </td>
   <td><p>Zoomar ut (endast iOS och Android™ 3x)</p> </td>
  </tr>
  <tr>
   <td><p><strong>Svep</strong></p> </td>
   <td><p>Rullningslist</p> </td>
   <td><p>Rulla bilder</p> </td>
   <td><p>Spins</p> </td>
  </tr>
  <tr>
   <td><p><strong>Snurra</strong></p> </td>
   <td><p>Rullningslist</p> </td>
   <td><p>Rulla bilder</p> </td>
   <td><p>Spins</p> </td>
  </tr>
 </tbody>
</table>

## Öka antalet visningsförinställningar som visas {#increasing-the-number-of-viewer-presets-that-display}

Experience Manager visar en mängd olika förinställningar för visningsprogram när resurser från **[!UICONTROL Detail View]** > **[!UICONTROL Viewers]**. Du kan öka eller minska antalet visningsprogram som visas.

**Så här ökar du antalet visningsförinställningar som visas:**

1. Navigera till CRXDE Lite ([https://localhost:4502/crx/de](https://localhost:4502/crx/de)).
1. Navigera till noden med visningsförinställningar på `/libs/dam/gui/coral/content/commons/sidepanels/viewerpresets/viewerpresetslist`

   ![chlimage_1-221](/help/assets/dynamic-media/assets/chlimage_1-221.png)

1. I egenskapen **[!UICONTROL limit]** ändrar du **[!UICONTROL Value]**, som är inställt på 15 som standard, till önskat tal.
1. Navigera till datakällan för visningsförinställningen på `/libs/dam/gui/coral/content/commons/sidepanels/viewerpresets/viewerpresetslist/datasource`

   ![chlimage_1-222](/help/assets/dynamic-media/assets/chlimage_1-222.png)

1. I egenskapen limit ändrar du talet till önskat tal, till exempel `{empty requestPathInfo.selectors[1] ? "20" : requestPathInfo.selectors[1]}`
1. Välj **[!UICONTROL Save All]**.

## Skapa förinställningar för visningsprogram {#creating-a-new-viewer-preset}

Genom att skapa visningsförinställningar kan du använda olika inställningar för att visa och interagera med resurser. Du behöver dock inte skapa visningsförinställningar. Om du vill kan du använda de förinställda visningsprogrammen som redan finns i Experience Manager Assets.

Om du väljer att skapa en visningsförinställning aktiveras visningsprogrammets läge automatiskt när du har sparat den (inställt på **[!UICONTROL On]**) på sidan Förinställningar för visningsprogram. Det här läget innebär att det är synligt i Dynamic Media-komponenten och i Interactive Media-komponenten och när du förhandsgranskar en bild eller video.

Vissa visningsprogramförinställningar har exklusiva inställningar som kan påverka visningsprogrammets användning och allmänna beteende. Beroende på vilken visningsförinställning du skapar bör du tänka på dessa speciella saker.

Se [Specialöverväganden när du skapar en interaktiv visningsförinställning](#special-considerations-for-creating-an-interactive-viewer-preset).

Se [Specialöverväganden när du skapar en Carousel Banner Viewer-förinställning](#special-considerations-for-creating-a-carousel-banner-viewer-preset).

**Så här skapar du förinställningar för visningsprogram:**

1. I det övre vänstra hörnet av Experience Manager väljer du logotypen för Experience Manager och går sedan till vänster **[!UICONTROL Tools]** (hammarikon) > **[!UICONTROL Assets]** > **[!UICONTROL Viewer Presets]**.

   ![6_5_viewerpresets](assets/6_5_viewerpresets.png)

1. På sidan Förinställningar för visningsprogram väljer du **[!UICONTROL Create]**.
1. I **[!UICONTROL New Viewer Preset]** i **[!UICONTROL Preset Name]** anger du namnet på den nya förinställningen. Välj ett namn noggrant - de går inte att redigera efter att du har markerat **[!UICONTROL Create]**.

   När du sparar förinställningen senare i de här stegen visas namnet på sidan Förinställningar för visningsprogram under kolumnrubriken Förinställningstitel.

1. I listrutan Multimedietyp väljer du den typ av visningsförinställning som du vill skapa och sedan väljer du den i det övre högra hörnet på sidan **[!UICONTROL Create]**.

   Se [Multimedietyper för visningsförinställningar](#rich-media-types-for-viewer-presets).

1. På sidan Redigerare för visningsförinställning väljer du **[!UICONTROL Appearance]** -fliken.
1. Gör något av följande:

   * I **[!UICONTROL Selected Type]** väljer du en komponent vars visuella design du vill anpassa. Du kan också markera ett visuellt element i visningsprogrammet och välja det för konfiguration.

      Med den visuella redigeraren kan du se vilken effekt en viss egenskap har på ett format. Ange eller justera valfri egenskap för att omedelbart se vilken effekt den har på visningsprogrammet med exemplet till vänster om redigeraren.

      CSS-formategenskaperna för varje typ av visningsförinställning beskrivs i&quot;Anpassa *`<viewer name>`* Hjälpavsnittet för visningsprogrammet i [Referenshandbok för visningsprogram](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources.html). Om du till exempel skapar en visningsförinställning av typen `Mixed_Media`, se [Anpassa visningsprogrammet för blandade media](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/mixed-media/customing-mixed-media/c-html5-mixedmedia-viewer-customizingviewer.html) för en lista och en beskrivning av varje egenskap.

   * Om du har definierat formatinställningar i en separat CSS-fil kan du överföra CSS-filen till Experience Manager Assets. Om du vill hitta den överförda CSS-filen och associera den med visningsförinställningen väljer du **[!UICONTROL Import CSS]** nedanför **[!UICONTROL Selected Type]** nedrullningsbar meny (om det behövs kan du rulla den visuella redigeraren uppåt för att se den).

      När du importerar en CSS-fil kontrollerar den visuella redigeraren om rätt visningsmarkörer används i CSS. Om du till exempel skapar ett zoomvisningsprogram måste alla CSS-regler som du importerar definieras med hjälp av visningsprogrammets klassnamn `.s7mixedmediaviewer` definieras för ett överordnat visningsprogramelement.

      Du kan importera godtycklig, handgjord CSS så länge den definierar CSS-markörerna för ett visst visningsprogram. (CSS-markörer beskrivs i&quot;Anpassning&quot; *&lt;viewer name=&quot;&quot;>* Hjälpavsnittet för visningsprogrammet i [Referenshandbok för visningsprogram](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources.html). Om du till exempel vill läsa om CSS-markörer för Zoomvisningsprogrammet läser du [Anpassa Zoom Viewer](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/zoom/customizing-zoom/c-html5-20-zoom-viewer-customizingviewer.html).) Det är dock möjligt att den visuella redigeraren inte förstår vissa CSS-värden. I sådana fall försöker den visuella redigeraren åsidosätta felen så att CSS fortfarande fungerar.
   >[!NOTE]
   >
   >Om du föredrar att redigera CSS direkt i dess Raw-format väljer du **[!UICONTROL Show/Hide CSS]** nedanför listrutan Markerad typ (om det behövs rullar du den visuella redigeraren uppåt för att se den).
   >När du ändrar en egenskap direkt i CSS kan du, precis som den visuella redigeraren, omedelbart se vilken effekt den har på visningsprogramexemplet. Och samma egenskap uppdateras automatiskt samtidigt i den visuella redigeraren. Därför kan du använda CSS-redigeraren raw eller den visuella redigeraren, eller använda båda för båda.

   >[!NOTE]
   >
   >För knappbilder väljer du 2x-bilden och överför högupplösta bilder. När du arbetar med interaktiva bilder och köpbara banners kan du även välja bland olika färdiga hotspot-knappar.

1. (Valfritt) I början av sidan Redigera visningsförinställning väljer du **[!UICONTROL Desktop]**, **[!UICONTROL Tablet]**, eller **[!UICONTROL Phone]** för att unikt definiera visuella format för olika enhets- och skärmtyper.
1. På sidan Redigerare för visningsförinställning väljer du **[!UICONTROL Behavior]** -fliken. Du kan också markera ett visuellt element i visningsprogrammet och välja det för konfiguration.
1. Välj en komponent vars beteenden du vill ändra i listrutan **[!UICONTROL Selected Type]**.

   Många komponenter i den visuella redigeraren har en detaljerad beskrivning. Dessa beskrivningar visas i blå rutor när du expanderar en komponent för att visa dess associerade parametrar.

   Vissa typer av visningsprogram har komponenter som gör att du kan ange bildserverkommandon i ett **[!UICONTROL IS Command]**-textfält. En lista med kommandon som du kan använda finns i [API-referenshandboken för bildservrar](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/c-is-home.html).

   >[!NOTE]
   >
   >**Om du använder en pekenhet, till exempel en telefon eller surfplatta...**
   >
   >
   >När du har skrivit ett värde i textfältet kan du markera någon annanstans i användargränssnittet för att skicka ändringen och stänga det virtuella tangentbordet. Om du väljer **[!UICONTROL Enter]**, utförs ingen åtgärd.

1. I sidans övre högra hörn väljer du **[!UICONTROL Save]**.
1. Publicera din nya visningsförinställning. Du måste publicera förinställningen innan du kan använda den på webbplatsen.

   Se [Förinställningar för publiceringsvisningsprogram](#publishing-viewer-presets).

### Specialöverväganden när du skapar en interaktiv visningsförinställning {#special-considerations-for-creating-an-interactive-viewer-preset}

**Om Visningslägen för miniatyrbilder på panelen:**

När du skapar eller redigerar en förinställning för Interactive Video Viewer kan du välja vilken visningsinställning som ska användas. Det här valet görs när du markerar `InteractiveSwatches` från **[!UICONTROL Selected Component]** nedrullningsbar meny under **[!UICONTROL Behavior]** -fliken. Det visningsläge du väljer påverkar hur och när miniatyrbilder visas när videon spelas upp. Du kan välja antingen ett `segment`-visningsläge (standard) eller ett `continuous`-visningsläge.

<table>
 <tbody>
  <tr>
   <td><strong>Visningsläge</strong></td>
   <td><strong>Beskrivning</strong></td>
  </tr>
  <tr>
   <td>Segment</td>
   <td><p><code>Segment </code>är standardvisningsläget för förinställningarna för interaktiv video i visningsprogrammet <code>Shoppable_Video_light</code> och <code>Shoppable_Video_dark</code> och alla förinställningar för Interactive Video Viewer som du själv skapar.</p> <p>I det här läget kan du anta att det finns färre miniatyrer tilldelade till ett videosegment än antalet synliga fläckar på visningspanelen. I sådana fall är miniatyrbilder från nästa eller föregående delsegment <i>not </i>dras in för att fylla i tomma fläckar på panelen. Det innebär att det bevarar visningen av färgrutor som har tilldelats ett visst videosegment.</p> </td>
  </tr>
  <tr>
   <td>Kontinuerlig</td>
   <td><p>I <code>continuous </code>i visningsläget, anta att antalet miniatyrbilder i ett segment är mindre än antalet som visas på panelen. I så fall visas miniatyrbilder automatiskt från nästa segment, eller det föregående segmentet, där den sista miniatyrbilden visas.</p> <p>The <a href="/help/assets/dynamic-media/interactive-videos.md">video i det här avsnittet</a> är ett exempel på <code>continuous </code>visningsläge.</p> </td>
  </tr>
 </tbody>
</table>

**Om beteendet för automatisk rullning i det interaktiva visningsprogrammet:**

Funktionen för automatisk rullning för miniatyrbilder i det interaktiva visningsprogrammet fungerar oberoende av det visningsläge du väljer.

När du skapar eller redigerar en visningsförinställning för interaktiv video öppnar du Autorullning på fliken Beteende. På fliken Beteende kan du gå till **[!UICONTROL Selected Components]** nedrullningsbar meny, välja **[!UICONTROL InteractiveSwatches]**. Kryssrutan Autorullning visas under textfältet IS-kommando.

Om du inaktiverar **[!UICONTROL Auto Scroll]** (avmarkerar kryssrutan) i visningsförinställningen visas bara den första miniatyrbilden för hela videolängden på panelen när användaren spelar upp videon. Användaren kan dock bläddra bland miniatyrbilderna manuellt med upp- och nedpilarna om så önskas.

När du aktiverar (markerar) **[!UICONTROL Auto Scroll]** i visningsförinställningen rullas miniatyrbilder som tilldelats ett videosegment in i vyn i början av ett segment under videouppspelningen. Det kan hända att vissa miniatyrer i ett segment visas dubbelt så länge som andra miniatyrer före eller efter dem. Det här beteendet beror på att antalet miniatyrbilder i ett segment är större än det antal som visas på panelen och inte är jämnt delbart.

Anta att du har ett 30-sekunders videosegment. Och det finns totalt nio miniatyrbilder som ska visas under 30 sekunder. Storleken på webbläsaren ändras så att det finns fyra synliga miniatyrpositioner på visningspanelen. Det 30 sekunder långa videotidssegmentet är uppdelat i tre delsegment. I följande tabell visas hur miniatyrbilder visas för ett givet tidsdelsegment:

| **Video subsegment** | **Delsegmenttid i sekunder** | **Miniatyrbilder som visas på panelen** |
|---|---|---|
| 1 | 0-10 | 1, 2, 3, 4 |
| 2 | 10-20 | 4, 5, 6, 7 |
| 3 | 20-30 | 6, 7, 8, 9 |

Delsegmentet Video 3 sträcker sig inte utanför de miniatyrbilder som är tilldelade till det. Lägg märke till att miniatyrbilderna 4, 6 och 7 visas dubbelt så långt på panelen som de andra miniatyrbilderna.

Följande logik används för hur många miniatyrbilder som visas på panelen baserat på antalet tillgängliga positioner:

* Antal delsegment = rund upp till nästa delsegment (antal miniatyrbilder/antal synliga platser på miniatyrbildspanelen, baserat på webbläsarfönstrets storlek).
I exemplet i tabellen ovan används 9 miniatyrbilder/4 kortplatser = 2,25; visningsprogrammets logik omger den med upp till tre undersegment.

* Antal miniatyrbilder = avrunda till nästa miniatyrbild (antal miniatyrbilder/antal undersegment).
Med exemplet i tabellen ovan används 9 miniatyrbilder/3 videodelsegment = 3 miniatyrbilder.

* Delsegmentets längd = den totala videons längd/antal undersegment.
Med hjälp av exemplet i tabellen ovan visas 30 sekunder/3 videodelsegment = 10 sekunder för varje videodelsegment.

#### Specialöverväganden när du skapar visningsförinställningar för Carousel Banner {#special-considerations-for-creating-a-carousel-banner-viewer-preset}

När du skapar visningsförinställningar för Carousel Banner kan du ändra format för aktiveringspunkter på följande sätt:

|  | **Beskrivning** | **Åtgärder** |
|---|---|---|
| **[!UICONTROL Hotspot Icon]** | Ändra ikonen som används för hotspot-områden | Om du vill ändra hotspot-ikonens bild går du till **[!UICONTROL Appearance]** flik, in **[!UICONTROL Selected Component]**, markera **[!UICONTROL ImageMapEffect]**. Under **[!UICONTROL Icon]** markerar du **[!UICONTROL Background]** och i fältet **[!UICONTROL Image]** navigerar du till den bakgrundsbild du vill ha. |

## Aktivera eller inaktivera visningsprogramförinställningar {#activating-or-deactivating-viewer-presets}

Vilka visningsprogramförinställningar som är tillgängliga i användargränssnittet beror på vilka som är aktiva i redigeringsläget. Som standard är en visningsförinställning&quot;På&quot; när du har skapat den. Om du stänger av förinställningen visas den inte i redigeringsläge. Om förinställningen publiceras publiceras den alltid oavsett om den är aktiverad eller inte. Inaktivera visningsförinställningar om listan blir för oskarp eller om du inte vill att en visningsförinställning ska vara tillgänglig för användning.

**Så här aktiverar eller inaktiverar du visningsförinställningar:**

1. I det övre vänstra hörnet av Experience Manager väljer du logotypen Experience Manager och sedan i den vänstra listen väljer du **[!UICONTROL Tools]** (hammarikon) > **[!UICONTROL Assets]** > **[!UICONTROL Viewer Presets]**.
1. På sidan Viewer Preset (Visningsförinställning), under **[!UICONTROL State]** markerar du alternativet för att aktivera eller inaktivera en visningsförinställning.

   De visningsprogramförinställningar som är aktiverade visas till höger, i en blå ruta. förinställningar för inaktiverat visningsprogram har växlingsknappen till vänster, i en ljusgrå ruta.

## Publicera förinställningar för visningsprogram {#publishing-viewer-presets}

När du aktiverar (eller aktiverar&quot;På&quot;) ett visningsförinställningsläge visas det i Dynamic Media-komponenten, i Interactive Media-komponenten och när du visar en mediefil.

Men *leverera* Om du har en resurs med en visningsförinställning måste visningsförinställningen också publiceras. Alla visningsförinställningar måste aktiveras *och* publiceras för att hämta URL eller inbäddningskod för en resurs. Aktivera och publicera alla färdiga visningsinställningar som medföljer Dynamic Media. Anpassade visningsförinställningar som du skapar och lägger till aktiveras automatiskt, men de måste också publiceras.

Se [Aktivera eller inaktivera visningsförinställningar](#activating-or-deactivating-viewer-presets).

Se även [Förhandsgranska resurser](/help/assets/dynamic-media/previewing-assets.md).

**Så här publicerar du förinställningar för visningsprogram:**

1. I det övre vänstra hörnet av Experience Manager väljer du logotypen Experience Manager och sedan i den vänstra listen väljer du **[!UICONTROL Tools]** (hammarikon) > **[!UICONTROL Assets]>[!UICONTROL Viewer Presets]**.
1. Välj en eller flera visningsförinställningar som du vill publicera.
1. I verktygsfältet väljer du **[!UICONTROL Publish]** ikon.

## Sortera visningsförinställningar {#sorting-viewer-presets}

1. I det övre vänstra hörnet av Experience Manager väljer du logotypen Experience Manager och sedan i den vänstra listen väljer du **[!UICONTROL Tools]** (hammarikon) > **[!UICONTROL Assets]>[!UICONTROL Viewer Presets]**.
1. Välj **[!UICONTROL Preset Title]**, **[!UICONTROL Type]**, **[!UICONTROL Published]**, eller **[!UICONTROL State]** för att sortera efter den kolumnrubriken. Välj till exempel **[!UICONTROL Type]**  om du vill sortera förinställningstyperna för visningsprogrammet i alfabetisk eller omvänd alfabetisk ordning.

## Redigera förinställningar för visningsprogram {#editing-viewer-presets}

Redigera alla *fördefinierade färdiga förinställningar för visningsprogram* är inte ett scenario som stöds. Om du redigerar en förinställning för ett visningsprogram som inte är installerat uppmanas du att spara den med ett nytt namn.

**Så här redigerar du förinställningar för visningsprogram:**

1. I det övre vänstra hörnet av Experience Manager väljer du logotypen Experience Manager och sedan i den vänstra listen väljer du **[!UICONTROL Tools]** (hammarikon) > **[!UICONTROL Asset]** > **[!UICONTROL Viewer Presets]**.
1. Markera en förinställning genom att markera rutan till vänster om visningsförinställningens titel.
1. I verktygsfältet väljer du **[!UICONTROL Edit]**.
1. På **[!UICONTROL Viewer Preset Editor]** gör du de ändringar du vill ha i visningsförinställningen med hjälp av alternativen på sidan **[!UICONTROL Appearance]** och **[!UICONTROL Behavior]** -tabbar.

   Från **[!UICONTROL Appearance]** -fliken, i det övre vänstra hörnet på sidan Redigerare för visningsförinställningar, väljer **[!UICONTROL Desktop]**, **[!UICONTROL Tablet]**, eller **[!UICONTROL Phone]** om du vill ändra resursens presentationsläge.

1. Gör något av följande i det övre högra hörnet på sidan:

   * Välj **[!UICONTROL Save]** om du vill spara ändringarna och gå tillbaka till sidan med visningsförinställningar.
   * Välj **[!UICONTROL Cancel]** för att ångra ändringar du gjort och återgå till sidan för visningsförinställningar.

## Ta bort anpassade förinställningar för visningsprogram {#deleting-custom-viewer-presets}

Du kan ta bort visningsförinställningar som du har skapat och lagt till i Dynamic Media.

**Så här tar du bort anpassade visningsprogramförinställningar:**

1. I det övre vänstra hörnet av Experience Manager väljer du logotypen Experience Manager och sedan i den vänstra listen väljer du **[!UICONTROL Tools]** (hammarikon) > **[!UICONTROL Assets]>[!UICONTROL Viewer Presets]**.
1. Markera en förinställningsrubrik på sidan Förinställningar för visningsprogram och välj sedan alternativet **[!UICONTROL Trash]** ikon.
1. Välj **[!UICONTROL Delete]**.

## Använda förinställningar för visningsprogram på en resurs {#applying-a-viewer-preset-to-an-asset}

Om du redan har publicerat både resursen och det valda visningsprogrammet visas knapparna **[!UICONTROL URL]** och **[!UICONTROL Embed]** när du har valt en visningsförinställning.

**Så här använder du en visningsförinställning för en resurs:**

1. Öppna resursen och i närheten av sidans övre vänstra hörn, välj den nedrullningsbara menyn och välj sedan **[!UICONTROL Viewers]**.

   >[!NOTE]
   >
   >Om du redan har publicerat både resursen och det valda visningsprogrammet visas knapparna **[!UICONTROL URL]** och **[!UICONTROL Embed]** när du har valt en visningsförinställning.

1. Om du vill använda den på resursen väljer du en visningsförinställning i den vänstra rutan.

   Du kan [kopiera URL:en som ska delas](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md) med andra användare.

## Leverera resurser med visningsförinställningar {#delivering-assets-with-viewer-presets}

Information om hur du hämtar URL:er för visningsförinställningar finns i [Länka URL:er till webbprogrammet](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md). Se även [Bädda in Video Viewer på en webbsida](/help/assets/dynamic-media/embed-code.md).

Om du använder Experience Manager som WCM-fil kan du lägga till resurser med visningsförinställningarna direkt på sidan. Se [Lägga till Dynamic Media-resurser på sidor](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md).

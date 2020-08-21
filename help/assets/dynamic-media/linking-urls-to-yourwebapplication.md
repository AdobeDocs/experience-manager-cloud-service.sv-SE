---
title: Länka URL till ett webbprogram
description: Länka URL:er till webbprogrammet i dynamiska medier
translation-type: tm+mt
source-git-commit: c240f9aa465b019fa77cc471f865db1f4ab45532
workflow-type: tm+mt
source-wordcount: '1207'
ht-degree: 10%

---


# Länka URL till ett webbprogram {#linking-urls-to-your-web-application}

Dina webbplatser och tillämpningar har åtkomst till Dynamic Media-tjänster via URL-samtal. När du har publicerat en resurs aktiverar Dynamic Media en URL-sträng som refererar till resursen. Du kan klistra in dessa URL:er i en webbläsare för testning.

Du länkar bara till URL:er om du *inte* använder AEM som WCM-fil. Länkning/inbäddning används när du vill leverera en videospelare som ett popup-fönster eller modalt fönster. Om du använder AEM som WCM-fil lägger [du till resurserna direkt på sidan.](adding-dynamic-media-assets-to-pages.md)

Om du vill placera dessa URL-strängar på dina webbsidor och i dina program kopierar du dem från Dynamic Media.

>[!NOTE]
>
>URL-strängar är bara tillgängliga för dynamiska återgivningar av resurser. De är för närvarande inte tillgängliga för statiska resurser som finns i DAM och inte för den dynamiska medieservern. URL-knappen visas inte för återgivningar som är statiska.

See also [Embedding the Video or Image Viewer on a Web Page](embed-code.md).

Se även [Länka YouTube-URL:er till ditt webbprogram](video.md).

See also [Delivering Optimized Images for a Responsive Site](responsive-site.md).

Se även [Överföra resurser](/help/assets/manage-digital-assets.md#uploading-assets).

## Hämta en URL för en resurs {#obtaining-a-url-for-an-asset}

Du kan hämta en URL-sträng som genereras av en bildförinställning eller en visningsförinställning. När du har kopierat URL:en markeras den i Urklipp så att du kan klistra in den på sidorna på webbplatsen eller i programmet.

>[!NOTE]
>
>URL:en är inte tillgänglig för kopiering förrän du har publicerat den valda resursen. Dessutom måste du även publicera visningsförinställningen eller bildförinställningen.
>
>Se [Publicera resurser](publishing-dynamicmedia-assets.md).
>
>Se [Publicera förinställningar](managing-viewer-presets.md#publishing-viewer-presets)för visningsprogram.
>
>Se [Publicera bildförinställningar](managing-image-presets.md#publishing-image-presets).

Du kan hämta en URL-sträng på flera olika sätt. Stegen nedan visar dock bara en metod som du kan använda.

**Så här hämtar du en URL för en resurs**

1. Navigera till den *publicerade* resurs vars URL-adress för bildförinställning eller URL-adress för visningsförinställning som du vill kopiera och tryck på resursen för att öppna den.

   Kom ihåg att URL:er endast går att kopiera *efter* att du har *publicerat* resurserna. Dessutom måste visningsförinställningen eller bildförinställningen också publiceras.

   Se [Publicera resurser](publishing-dynamicmedia-assets.md).

   Se [Publicera förinställningar](managing-viewer-presets.md#publishing-viewer-presets)för visningsprogram.

   Se [Publicera bildförinställningar](managing-image-presets.md#publishing-image-presets).

1. Gör något av följande beroende på vilken resurs du valt:

   * Om du har valt en bild trycker du på **[!UICONTROL Renditions]**.

      Tryck på ett förinställningsnamn under rubriken för att visa återgivningen i den högra bildrutan. **[!UICONTROL Dynamic]** Du kan behöva bläddra i listan Återgivningar för att se den dynamiska rubriken.

      Tryck på längst ned i den vänstra listen **[!UICONTROL URL]**.

      ![chlimage_1-270](assets/chlimage_1-270.png)

   * Om du har valt en snurruppsättning, en bilduppsättning, en Carousel-uppsättning eller en video trycker du på **[!UICONTROL Viewers]**.

      Tryck på ett namn på en visningsförinställning i den vänstra listen. En förhandsgranskning av uppsättningen eller videon öppnas på en separat sida.

      I den vänstra listen, längst ned, tryck **[!UICONTROL URL]**.

      ![chlimage_1-271](assets/chlimage_1-271.png)

1. Markera och kopiera texten till webbläsaren för att förhandsgranska resursen eller lägga till den på webbinnehållssidan.

   Tryck på **[!UICONTROL X]** eller tryck på **[!UICONTROL Close]** för att stänga URL-fönstret.

## Hämta en URL för en statisk resurs {#obtaining-a-url-for-a-static-asset}

Dynamic Media har stöd för leverans av statiska resurser, som är ytterligare resurser utöver bara bilder och video. Statiska medieformat som stöds för leverans är bland annat följande:

* 3D-filer
* Animerad GIF
* Ljudfiler
* CSS
* JavaScript (när ditt företag är konfigurerat med sin egen domän)
* PDF
* SVG
* XML
* ZIP

**Hämta en URL för en statisk resurs**

1. Navigera till den *publicerade *statiska resurs vars URL du vill kopiera och öppna den genom att trycka på resursen.

   Remember that URLs are only available to copy *after* you have first *published* the static asset.

   Se [Publicera resurser](publishing-dynamicmedia-assets.md).

1. Använd någon av följande metoder för att hämta URL:en för den publicerade statiska resursen:

   * `The URL of the published static is the following:`

      * `https://*<server_name>*/is/content/*<company_name>*/*<static_asset_filename>*.*<extension>*`

         Till exempel, `https://aem.com/is/content/adobe/image.gif`.
   * Tryck **[!UICONTROL Asset > Dynamic Renditions]** och tryck sedan på en dynamisk återgivning av den statiska resursen och kopiera URL:en.

      Ändra den kopierade URL-adressen som ska användas `is/content` i sökvägen i stället för `is/image/`.


## Hämta en video-URL för en publicerad videoåtergivning {#obtaining-a-video-url-for-a-published-video-rendition}

1. Navigera AEM till **[!UICONTROL Tools > Deployment > Cloud > Cloud Services]**.
1. På sidan **[!UICONTROL Cloud Services]** bläddrar du nedåt till rubriken **[!UICONTROL Dynamic Media Cloud Services]** och trycker sedan på **[!UICONTROL Show Configurations]**.
1. Under **[!UICONTROL Available Configurations]** trycker du på namnet på den konfiguration du vill använda.

1. På **[!UICONTROL Dynamic Media Cloud Settings]** sidan, under **[!UICONTROL Video Service URL]**, kopierar du ned hela URL-sökvägen. Du behöver den kopierade URL-sökvägen senare i stegen.

   URL-sökvägen kan till exempel se ut ungefär så här:

   `https://s7athens.macromedia.com:9090/DMGateway/`

   (Banan ovan är endast avsedd som illustration. det är inte den faktiska sökvägen som du kopierar.)

1. Under **[!UICONTROL Registration ID]** kopierar du det kundnamn som finns i den sista delen av ID:t.

   Om registrerings-ID:t till exempel är `87654321|MyCompany`det blir kundens namn `MyCompany`.

1. I närheten av det övre vänstra hörnet på sidan trycker du **[!UICONTROL Cloud Services]** och sedan på ikonen AEM och navigerar till **[!UICONTROL General > CRXDE Lite]**.
1. Kopiera ned hela videouppdateringssökvägen från JCR-filen (Java Content Repository).

   Videons återgivningssökväg kan till exempel se ut ungefär så här:

   `/_renditions_/0bd/0bd28743-a616-4fe6-92aa-6eae7c2112f/avs/Momentum_1080-0x720-2600k.mp4`

   (Banan ovan är endast avsedd som illustration. det är inte den faktiska sökvägen som du kopierar.)

1. Ordna den kopierade informationen i följande ordning för att skapa en fullständig URL-sökväg:

   `<Video_Service_URL>/public/<Customer_name_from_Registration_ID>/<Video_rendition_path>`

   Om du till exempel använder exempelsökvägarna och exempelkundnamnet från stegen ovan, visas den fullständiga sökvägen enligt följande:

   `https://s7athens.macromedia.com:9090/DMGateway/public/MyCompany/_renditions_/0bd/0bd28743-a616-4fe6-92aa-6eae7c2112ff/avs/Momentum_1080-0x720-2600k.mp4`

   Det här är den fullständiga video-URL:en för en publicerad videoåtergivning.

## Hämta en video-URL för adaptiv direktuppspelning (HLS) {#obtaining-a-video-url-for-adaptive-streaming-hls}

1. Navigera AEM till **[!UICONTROL Tools > Deployment > Cloud > Cloud Services]**.
1. På sidan **[!UICONTROL Cloud Services]** bläddrar du nedåt till rubriken **[!UICONTROL Dynamic Media Cloud Services]** och trycker sedan på **[!UICONTROL Show Configurations]**.
1. Under **[!UICONTROL Available Configurations]** trycker du på namnet på den konfiguration du vill använda.
1. Gör följande på **[!UICONTROL Dynamic Media Cloud Services Settings]** sidan:

   * Under **[!UICONTROL Video Service URL]** kopierar du hela URL-sökvägen. Du behöver den kopierade URL-sökvägen senare i dessa steg. URL-sökvägen kan till exempel se ut ungefär så här:

   `https://gateway-na.assetsadobe.com/DMGateway/`

   (Banan ovan är endast avsedd som illustration. det är inte den faktiska sökvägen som du kopierar.)

   * Under **[!UICONTROL Registration ID]** kopierar du det kundnamn som finns i den sista delen av ID:t. Du behöver det kopierade kundnamnet längre fram i de här stegen.

      Om registrerings-ID:t till exempel är `87654321|demoCo`det kundnamn du kopierar blir `demoCo`.


1. Kopiera respektive protokollväljare baserat på vilket videoleveransprotokoll du använder. Du behöver den kopierade protokollväljaren senare i dessa steg.

   <table>
    <tbody>
      <tr>
      <td><strong>Videoleveransprotokoll som du använder</strong></td>
      <td><strong>Protokollväljare som ska användas</strong></td>
      </tr>
      <tr>
      <td><p>HTTP</p> <p>Om du använder HTTP (osäker videoleverans) måste du ändra <code>https</code> till URL-värdet <code>http</code> för den videotjänst du kopierade tidigare.</p> </td>
      <td><code>public/</code></td>
      </tr>
      <tr>
      <td>HTTPS</td>
      <td><code>public-ssl/</code></td>
      </tr>
    </tbody>
   </table>

1. Kopiera den fullständiga sökvägen till videomaterialet i AEM, som bearbetats av Dynamic Media. Du behöver den här kopierade sökvägen för videoresurser senare i dessa steg.

   Till exempel:

   `/content/dam/marketing/MyVideo.mp4`

1. Kombinera alla delar du kopierat tidigare och skapa en sträng i följande ordning:

   &lt; `video service URL`>&lt; `protocol selector`>&lt; `customer name`>&lt; `video asset path`>

   Om du till exempel använder den kopierade informationen från exemplen i de här stegen ser strängen ut så här:

   `https://gateway-na.assetsadobe.com/DMGateway/public-ssl/demoCo/content/dam/marketing/MyVideo.mp4`

1. Fyll i URL:en genom `.m3u8` att lägga till i slutet av strängen. Om du t.ex. lägger `.m3u8` till strängen från föregående steg ser den fullständiga URL-sökvägen ut så här:

   `https://gateway-na.assetsadobe.com/DMGateway/public-ssl/demoCo/content/dam/marketing/MyVideo.mp4.m3u8`

## Använda HTTP/2 för att leverera dina dynamiska medieresurser {#using-http-to-deliver-your-dynamic-media-assets}

HTTP/2 är det nya, uppdaterade webbprotokollet som förbättrar kommunikationen mellan webbläsare och servrar. Det ger snabbare överföring av information och minskar mängden processorkraft som behövs. Dynamic Media-material kan nu levereras via HTTP/2 vilket ger bättre respons och laddningstider.

Se [HTTP2 Delivery of Content](http2faq.md) för fullständig information om hur du kommer igång med HTTP/2 med ditt Dynamic Media-konto.

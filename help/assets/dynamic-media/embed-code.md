---
title: Bädda in Dynamic Media Video eller Image Viewer på en webbsida
description: Lär dig bädda in Dynamic Media-video eller -bilder på en webbsida
translation-type: tm+mt
source-git-commit: 7dae5c0ed82687415719cd2d72f98028cf0a8e64
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 21%

---


# Bädda in Dynamic Media Video, Image Viewer eller Dimensional Viewer på en webbsida {#embedding-the-video-or-image-viewer-on-a-web-page}

Använd funktionen **[!UICONTROL Embed Code]** när du vill spela upp videon eller visa en resurs som är inbäddad på en webbsida. Du kopierar inbäddningskoden till Urklipp så att du kan klistra in den på webbsidorna. Det är inte tillåtet att redigera koden i dialogrutan **[!UICONTROL Embed Code]**.

Du bäddar bara in URL:er om du _inte_ använder AEM som WCM-fil. Om du använder AEM som WCM-fil lägger [du till resurserna direkt på sidan.](adding-dynamic-media-assets-to-pages.md)

See [Linking URLs to your Web Application.](linking-urls-to-yourwebapplication.md)

See [Delivering Optimized Images for a Responsive Site.](responsive-site.md)

>[!NOTE]
>
>Inbäddningskoden kan inte kopieras förrän du har publicerat den valda resursen. Dessutom måste du även publicera visningsförinställningen eller bildförinställningen.
>
>Se [Publicera resurser](publishing-dynamicmedia-assets.md).
>
>Se [Publicera förinställningar](managing-viewer-presets.md#publishing-viewer-presets)för visningsprogram.
>
>Se [Publicera bildförinställningar](managing-image-presets.md#publishing-image-presets).

**Bädda in Dynamic Media Video eller Image Viewer på en webbsida**

1. Navigera till den *publicerade* video- eller bildresurs vars inbäddningskod du vill kopiera.

   Kom ihåg att inbäddningskoden endast går att kopiera *efter* att du har *publicerat* resurserna. Dessutom måste visningsförinställningen eller bildförinställningen också publiceras.

   Se [Publicera resurser.](publishing-dynamicmedia-assets.md)

   Se [Publicera förinställningar](managing-viewer-presets.md#publishing-viewer-presets)för visningsprogram.

   Se [Publicera bildförinställningar](managing-image-presets.md#publishing-image-presets).

1. Markera listrutan i den vänstra listen och tryck sedan på **[!UICONTROL Viewers]**.
1. Tryck på ett namn på en visningsförinställning i den vänstra listen. Visningsförinställningen används på resursen.
1. Tryck på **[!UICONTROL Embed]**.
1. Kopiera hela koden till Urklipp i **[!UICONTROL Embed Code]** dialogrutan och tryck sedan på **[!UICONTROL Close]**.
1. Klistra in inbäddningskoden på dina webbsidor.

## Använda HTTP/2 för att leverera dina dynamiska medieresurser {#using-http-to-deliver-your-dynamic-media-assets}

HTTP/2 är det nya, uppdaterade webbprotokollet som förbättrar kommunikationen mellan webbläsare och servrar. Det ger snabbare överföring av information och minskar mängden processorkraft som behövs. Dynamic Media-material kan nu levereras via HTTP/2 vilket ger bättre respons och laddningstider.

Se [HTTP2 Delivery of Content](http2faq.md) för fullständig information om hur du kommer igång med HTTP/2 med ditt Dynamic Media-konto.

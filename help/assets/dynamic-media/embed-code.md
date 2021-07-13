---
title: Bädda in Dynamic Media Video eller Image Viewer på en webbsida
description: Lär dig bädda in Dynamic Media video- eller bildresurser på en webbsida.
feature: Resurshantering
role: User
exl-id: 76335781-e39f-4aae-967f-5af8634d8f61
source-git-commit: 6933f053e11320d8201922723879983084c52209
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 21%

---

# Bädda in Dynamic Media Video-, Image Viewer- eller Dimensional-visningsprogram på en webbsida {#embedding-the-video-or-image-viewer-on-a-web-page}

Använd funktionen **[!UICONTROL Embed Code]** när du vill spela upp videon eller visa en resurs som är inbäddad på en webbsida. Du kopierar inbäddningskoden till Urklipp så att du kan klistra in den på webbsidorna. Det är inte tillåtet att redigera koden i dialogrutan **[!UICONTROL Embed Code]**.

Du bäddar bara in URL:er om du är _inte_ och använder Adobe Experience Manager som WCM. Om du använder Experience Manager som WCM-fil [lägger du till resurserna direkt på sidan](adding-dynamic-media-assets-to-pages.md).

Se [Länka URL:er till ditt webbprogram](linking-urls-to-yourwebapplication.md).

Se [Leverera optimerade bilder för en responsiv plats](responsive-site.md).

>[!NOTE]
>
>Inbäddningskoden kan inte kopieras förrän du har publicerat den valda resursen. Dessutom måste du även publicera visningsförinställningen eller bildförinställningen.
>
>Se [Publicera resurser](publishing-dynamicmedia-assets.md).
>
>Se [Publicera förinställningar för visningsprogram](managing-viewer-presets.md#publishing-viewer-presets).
>
>Se [Publicera bildförinställningar](managing-image-presets.md#publishing-image-presets).

**Så här bäddar du in Dynamic Media Video eller Image Viewer på en webbsida:**

1. Navigera till den *publicerade* video- eller bildresurs vars inbäddningskod du vill kopiera.

   Kom ihåg att inbäddningskoden endast går att kopiera *efter* att du har *publicerat* resurserna. Dessutom måste visningsförinställningen eller bildförinställningen också publiceras.

   Se [Publicera resurser](publishing-dynamicmedia-assets.md).

   Se [Publicera förinställningar för visningsprogram](managing-viewer-presets.md#publishing-viewer-presets).

   Se [Publicera bildförinställningar](managing-image-presets.md#publishing-image-presets).

1. Markera listrutan till vänster och välj **[!UICONTROL Viewers]**.
1. Välj ett namn på visningsförinställningen i den vänstra listen. Visningsförinställningen används på resursen.
1. Välj **[!UICONTROL Embed]**.
1. Kopiera hela koden till Urklipp i dialogrutan **[!UICONTROL Embed Code]** och välj sedan **[!UICONTROL Close]**.
1. Klistra in inbäddningskoden på dina webbsidor.

## Använd HTTP/2 för att leverera dina Dynamic Media-resurser {#using-http-to-deliver-your-dynamic-media-assets}

HTTP/2 är det nya, uppdaterade webbprotokollet som förbättrar kommunikationen mellan webbläsare och servrar. Det ger snabbare överföring av information och minskar mängden processorkraft som behövs. Dynamic Media-material kan nu levereras via HTTP/2 vilket ger bättre respons och laddningstider.

Se [HTTP2 Delivery of Content](http2faq.md) för fullständig information om hur du kommer igång med HTTP/2 med ditt Dynamic Media-konto.

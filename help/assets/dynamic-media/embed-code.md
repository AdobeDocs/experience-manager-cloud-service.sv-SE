---
title: Bädda in Dynamic Media Video eller Image Viewer på en webbsida
description: Lär dig bädda in Dynamic Media-video eller bildresurser på en webbsida.
contentOwner: Rick Brough
feature: Asset Management
role: User
exl-id: 76335781-e39f-4aae-967f-5af8634d8f61
source-git-commit: c82f84fe99d8a196adebe504fef78ed8f0b747a9
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 18%

---

# Bädda in Dynamic Media Video, Image Viewer eller Dimensional Viewer på en webbsida {#embedding-the-video-or-image-viewer-on-a-web-page}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime och Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM Assets-integrering med Edge Delivery Services</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>UI-utökningsbarhet</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Aktivera Dynamic Media Prime och Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>Sök efter bästa praxis</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>Metadata - bästa praxis</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Content Hub</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>Dynamiska media med OpenAPI-funktioner</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>AEM Assets-dokumentation för utvecklare</b></a>
        </td>
    </tr>
</table>

Använd funktionen **[!UICONTROL Embed Code]** när du vill spela upp videon eller visa en resurs som är inbäddad på en webbsida. Du kopierar inbäddningskoden till Urklipp så att du kan klistra in den på webbsidorna. Det är inte tillåtet att redigera koden i dialogrutan **[!UICONTROL Embed Code]**.

Du bäddar bara in URL:er om du _inte_ använder Adobe Experience Manager som WCM-fil. Om du använder Experience Manager som WCM-fil [lägger du till resurserna direkt på sidan](adding-dynamic-media-assets-to-pages.md).

Se [Länka URL:er till ditt webbprogram](linking-urls-to-yourwebapplication.md).

Se [Leverera optimerade bilder för en responsiv webbplats](responsive-site.md).

>[!NOTE]
>
>Inbäddningskoden kan inte kopieras förrän du har publicerat den valda resursen. Dessutom måste du även publicera visningsförinställningen eller bildförinställningen.
>
>Se [Publicera Assets](publishing-dynamicmedia-assets.md).
>
>Se [Publicera visningsförinställningar](managing-viewer-presets.md#publishing-viewer-presets).
>
>Se [Publicera bildförinställningar](managing-image-presets.md#publishing-image-presets).

**Så här bäddar du in Dynamic Media Video eller Image Viewer på en webbsida:**

1. Navigera till den *publicerade* videon eller bildresurs vars inbäddningskod du vill kopiera.

   Kom ihåg att inbäddningskoden endast går att kopiera *efter* att du har *publicerat* resurserna. Dessutom måste visningsförinställningen eller bildförinställningen också publiceras.

   Se [Publicera Assets](publishing-dynamicmedia-assets.md).

   Se [Publicera visningsförinställningar](managing-viewer-presets.md#publishing-viewer-presets).

   Se [Publicera bildförinställningar](managing-image-presets.md#publishing-image-presets).

1. Markera listrutan till vänster och välj **[!UICONTROL Viewers]**.
1. Välj ett namn på visningsförinställningen i den vänstra listen. Visningsförinställningen används på resursen.
1. Välj **[!UICONTROL Embed]**.
1. I dialogrutan **[!UICONTROL Embed Code]** kopierar du hela koden till Urklipp och väljer sedan **[!UICONTROL Close]**.
1. Klistra in inbäddningskoden på dina webbsidor.

## Använd HTTP/2 för att leverera dina dynamiska medieresurser {#using-http-to-deliver-your-dynamic-media-assets}

HTTP/2 är det nya, uppdaterade webbprotokollet som förbättrar kommunikationen mellan webbläsare och servrar. Det ger snabbare överföring av information och minskar mängden processorkraft som behövs. Dynamic Media-material kan nu levereras via HTTP/2 vilket ger bättre respons och laddningstider.

Mer information om hur du kommer igång med HTTP/2 med ditt Dynamic Media-konto finns i [HTTP2 Delivery of Content](http2faq.md).

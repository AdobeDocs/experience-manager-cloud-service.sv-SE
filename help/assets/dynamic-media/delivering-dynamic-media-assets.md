---
title: Deliver Dynamic Media Assets
description: Lär dig leverera Dynamic Media-material.
feature: Asset Management
role: User
exl-id: 4557b561-b3c4-4d6f-8044-2069bda41613
source-git-commit: 6933f053e11320d8201922723879983084c52209
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 0%

---

# Deliver Dynamic Media Assets{#delivering-dynamic-media-assets}

How you can deliver your Dynamic Media assets - both video and images - depends on how your website is implemented.

Med Dynamic Media har du flera alternativ:

* If your website is hosted on Adobe Experience Manager, then you want to add the Dynamic Media assets directly to your page.
* Om webbplatsen inte ligger på Experience Manager kan du välja något av följande:

   * Embedding your video or image on your website.
   * Länka URL:er till webbprogrammet. Använd länkning när du vill leverera en videospelare som ett popup-fönster eller modalt fönster.
   * Om din webbplats är responsiv kan du [leverera optimerade bilder](/help/assets/dynamic-media/responsive-site.md).

>[!NOTE]
>
>Smart bildbehandling fungerar med befintliga bildförinställningar. Den använder intelligens under de sista millisekunderna för att ytterligare minska bildfilens storlek baserat på webbläsarens eller nätverkets anslutningshastighet. Se [Smart bildbehandling](/help/assets/dynamic-media/imaging-faq.md) för mer information.

For more information, see the following topics:

* [Lägg till Dynamic Media Assets på webbsidor](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)
* [Bädda in video- eller bildvisningsprogrammet på en webbsida](/help/assets/dynamic-media/embed-code.md)
* [Aktivera hotlink-skydd i Dynamic Media](/help/assets/dynamic-media/hotlink-protection.md)
* [Länka URL:er till ditt webbprogram](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md)
* [Leverera optimerade bilder för en responsiv webbplats](/help/assets/dynamic-media/responsive-site.md)
* [HTTP2-leverans av innehåll](/help/assets/dynamic-media/http2faq.md)
* [Invalidera CDN-cachen med Dynamic Media](/help/assets/dynamic-media/invalidate-cdn-cache-dynamic-media.md)
* [Invalidate the CDN cache by way of Dynamic Media Classic](/help/assets/dynamic-media/invalidate-cdn-cache-dm-classic.md)
* [Use Rulesets to Transform URLs](/help/assets/dynamic-media/using-rulesets-to-transform-urls.md)

## HTTP/2 delivery of Dynamic Media assets {#http-delivery-of-dynamic-media-assets}

Experience Manager now supports the delivery of all Dynamic Media content (images and video) over HTTP/2. That is, a published URL or embed code for the image or video is available to be integrated with any application that accepts a hosted asset. Den publicerade resursen levereras sedan via HTTP/2-protokollet. Den här leveransmetoden förbättrar kommunikationen mellan webbläsare och servrar, vilket ger bättre respons och laddningstider för alla dina Dynamic Media-resurser.

Mer information finns på [HTTP/2 - Vanliga frågor och svar om innehållsleverans](/help/assets/dynamic-media/http2faq.md).

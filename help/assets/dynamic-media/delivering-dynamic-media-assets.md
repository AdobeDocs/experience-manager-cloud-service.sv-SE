---
title: Leverera Dynamic Media Assets
description: Lär dig hur du levererar Dynamic Media-resurser till dina webbsidor via inbäddad video och bilder, eller länkar URL:er till ditt webbprogram.
contentOwner: Rick Brough
feature: Asset Management
role: User
exl-id: 4557b561-b3c4-4d6f-8044-2069bda41613
source-git-commit: 0e452bd94d75609ecc3c20ab6b56ded968ed0a70
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---

# Leverera Dynamic Media Assets{#delivering-dynamic-media-assets}

Hur du kan leverera dina Dynamic Media-resurser - både video och bilder - beror på hur webbplatsen implementeras.

Med Dynamic Media har du flera alternativ:

* Om webbplatsen finns på Adobe Experience Manager vill du lägga till Dynamic Media-resurserna direkt på sidan.
* Om din webbplats inte finns på Experience Manager kan du välja något av följande:

   * Bädda in videon eller bilden på webbplatsen.
   * Länka URL:er till webbprogrammet. Använd länkning när du vill leverera en videospelare som ett popup-fönster eller modalt fönster.
   * Om din webbplats är responsiv kan du [leverera optimerade bilder](/help/assets/dynamic-media/responsive-site.md).

>[!NOTE]
>
>Smart bildbehandling fungerar med befintliga bildförinställningar. Den använder intelligens under de sista millisekunderna i leveransen för att ytterligare minska bildfilens storlek baserat på webbläsarens eller nätverkets anslutningshastighet. Mer information finns i [Smart bildbehandling](/help/assets/dynamic-media/imaging-faq.md).

Mer information finns i följande avsnitt:

* [Lägg till Dynamic Media Assets på webbsidor](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)
* [Bädda in video- eller bildvisningsprogrammet på en webbsida](/help/assets/dynamic-media/embed-code.md)
* [Aktivera hotlink-skydd i Dynamic Media](/help/assets/dynamic-media/hotlink-protection.md)
* [Länka URL:er till ditt webbprogram](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md)
* [Leverera optimerade bilder för en responsiv webbplats](/help/assets/dynamic-media/responsive-site.md)
* [HTTP2-leverans av innehåll](/help/assets/dynamic-media/http2faq.md)
* [Invalidera CDN-cachen med Dynamic Media](/help/assets/dynamic-media/invalidate-cdn-cache-dynamic-media.md)
* [Invalidera CDN-cachen med Dynamic Media Classic](/help/assets/dynamic-media/invalidate-cdn-cache-dm-classic.md)
* [Använd regeluppsättningar för att omforma URL:er](/help/assets/dynamic-media/using-rulesets-to-transform-urls.md)

## HTTP/2-leverans av Dynamic Media-resurser {#http-delivery-of-dynamic-media-assets}

Experience Manager stöder nu leverans av allt Dynamic Media-innehåll (bilder och video) via HTTP/2. Det betyder att en publicerad URL eller inbäddningskod för bilden eller videon är tillgänglig för integrering med alla program som accepterar en värdbaserad resurs. Den publicerade resursen levereras sedan via HTTP/2-protokollet. Den här leveransmetoden förbättrar sättet som webbläsare och servrar kommunicerar på, vilket ger bättre respons och laddningstider för alla era Dynamic Media-resurser.

Mer information finns i [HTTP/2 Delivery of Content Frequently Asked Questions](/help/assets/dynamic-media/http2faq.md).

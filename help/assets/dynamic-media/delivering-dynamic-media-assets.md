---
title: Leverera dynamiska medieresurser
description: Lär dig leverera dynamiska medieresurser
translation-type: tm+mt
source-git-commit: 218afb360ec3a13f2f4562a703ca3184083fa7f6

---


# Delivering Dynamic Media Assets{#delivering-dynamic-media-assets}

Hur du kan leverera dynamiska medieresurser - både video och bilder - beror på hur webbplatsen implementeras.

Med Dynamic Media har du flera alternativ:

* Om din webbplats ligger hos AEM vill du lägga till de dynamiska medieresurserna direkt på sidan.
* Om din webbplats inte finns på AEM kan du välja något av följande:

   * Bädda in videon eller bilden på webbplatsen.
   * Länka URL:er till webbprogrammet. Använd länkning när du vill leverera en videospelare som ett popup-fönster eller modalt fönster.
   * Om webbplatsen är responsiv kan du [leverera optimerade bilder.](/help/assets/dynamic-media/responsive-site.md)

>[!NOTE]
>
>Smart bildbehandling fungerar med befintliga bildförinställningar och använder intelligens under de sista millisekunderna i leveransen för att ytterligare minska bildfilens storlek baserat på webbläsarens eller nätverkets anslutningshastighet. Mer information finns i [Smart](/help/assets/dynamic-media/imaging-faq.md) Imaging.

Mer information finns i följande avsnitt:

* [Lägga till dynamiska medieresurser på webbsidor](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)
* [Bädda in video- eller bildvisningsprogrammet på en webbsida](/help/assets/dynamic-media/embed-code.md)
* [Aktivera hotlink-skydd i Dynamic Media](/help/assets/dynamic-media/hotlink-protection.md)
* [Länka URL:er till ditt webbprogram](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md)
* [Leverera optimerade bilder för en responsiv webbplats](/help/assets/dynamic-media/responsive-site.md)
* [HTTP2-leverans av innehåll](/help/assets/dynamic-media/http2faq.md)
* [Upphäva CDN-cachelagrat innehåll](/help/assets/dynamic-media/invalidate-cdn-cached-content.md)
* [Använda regeluppsättningar för att omforma URL:er](/help/assets/dynamic-media/using-rulesets-to-transform-urls.md)

## HTTP/2-leverans av Dynamic Media-resurser {#http-delivery-of-dynamic-media-assets}

AEM har nu stöd för leverans av allt dynamiskt medieinnehåll (bilder och video) via HTTP/2. Det betyder att en publicerad URL eller inbäddningskod för bilden eller videon är tillgänglig för integrering med alla program som accepterar en värdbaserad resurs. Den publicerade resursen levereras sedan via HTTP/2-protokollet. Den här leveransmetoden förbättrar sättet som webbläsare och servrar kommunicerar på, vilket ger bättre respons och laddningstider för alla dynamiska medieresurser.

Mer information finns i [HTTP/2 Delivery of Content Frequently Asked Questions](/help/assets/dynamic-media/http2faq.md) .

---
title: Leverera Dynamic Media Assets
description: Lär dig leverera Dynamic Media-material.
feature: Resurshantering
role: Business Practitioner
exl-id: 4557b561-b3c4-4d6f-8044-2069bda41613
translation-type: tm+mt
source-git-commit: e94289bccc09ceed89a2f8b926817507eaa19968
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 1%

---

# Leverera Dynamic Media Assets{#delivering-dynamic-media-assets}

Hur du kan leverera dina Dynamic Media-resurser - både video och bilder - beror på hur webbplatsen implementeras.

Med Dynamic Media har du flera alternativ:

* Om du har AEM som värd för webbplatsen vill du lägga till Dynamic Media-resurserna direkt på sidan.
* Om webbplatsen inte finns AEM kan du välja mellan följande:

   * Bädda in videon eller bilden på webbplatsen.
   * Länka URL:er till webbprogrammet. Använd länkning när du vill leverera en videospelare som ett popup-fönster eller modalt fönster.
   * Om webbplatsen är responsiv kan du [leverera optimerade bilder](/help/assets/dynamic-media/responsive-site.md).

>[!NOTE]
>
>Smart bildbehandling fungerar med befintliga bildförinställningar. Den använder intelligens under de sista millisekunderna i leveransen för att ytterligare minska bildfilens storlek baserat på webbläsarens eller nätverkets anslutningshastighet. Mer information finns i [Smart bildbehandling](/help/assets/dynamic-media/imaging-faq.md).

Mer information finns i följande avsnitt:

* [Lägga till Dynamic Media-resurser på webbsidor](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)
* [Bädda in video- eller bildvisningsprogrammet på en webbsida](/help/assets/dynamic-media/embed-code.md)
* [Aktivera hotlink-skydd i Dynamic Media](/help/assets/dynamic-media/hotlink-protection.md)
* [Länka URL:er till ditt webbprogram](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md)
* [Leverera optimerade bilder för en responsiv webbplats](/help/assets/dynamic-media/responsive-site.md)
* [HTTP2-leverans av innehåll](/help/assets/dynamic-media/http2faq.md)
* [CDN-cachen har inte verifierats via Dynamic Media](/help/assets/dynamic-media/invalidate-cdn-cache-dynamic-media.md)
* [CDN-cachen har inte verifierats med Dynamic Media Classic](/help/assets/dynamic-media/invalidate-cdn-cache-dm-classic.md)
* [Använda regeluppsättningar för att omforma URL:er](/help/assets/dynamic-media/using-rulesets-to-transform-urls.md)

## HTTP/2-leverans av Dynamic Media-resurser {#http-delivery-of-dynamic-media-assets}

AEM har nu stöd för leverans av allt Dynamic Media-innehåll (bilder och video) via HTTP/2. Det betyder att en publicerad URL eller inbäddningskod för bilden eller videon är tillgänglig för integrering med alla program som accepterar en värdbaserad resurs. Den publicerade resursen levereras sedan via HTTP/2-protokollet. Den här leveransmetoden förbättrar kommunikationen mellan webbläsare och servrar, vilket ger bättre respons och laddningstider för alla dina Dynamic Media-resurser.

Mer information finns i [HTTP/2 Delivery of Content Frequently Asked Questions](/help/assets/dynamic-media/http2faq.md).

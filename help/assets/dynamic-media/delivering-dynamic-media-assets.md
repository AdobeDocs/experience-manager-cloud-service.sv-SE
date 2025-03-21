---
title: Leverera Dynamic Media Assets
description: Lär dig hur du levererar Dynamic Media-resurser till dina webbsidor via inbäddad video och bilder, eller länkar URL:er till ditt webbprogram.
contentOwner: Rick Brough
feature: Asset Management
role: User
exl-id: 4557b561-b3c4-4d6f-8044-2069bda41613
source-git-commit: c82f84fe99d8a196adebe504fef78ed8f0b747a9
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 0%

---

# Leverera Dynamic Media Assets{#delivering-dynamic-media-assets}

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

Hur ni kan leverera ert mediematerial i Dynamic Media - både video och bilder - beror på hur er webbplats implementeras.

Med Dynamic Media har du flera alternativ:

* Om din webbplats ligger hos Adobe Experience Manager vill du lägga till resurserna för dynamiska media direkt på din sida.
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
* [Gör CDN-cachen ogiltig via Dynamic Media](/help/assets/dynamic-media/invalidate-cdn-cache-dynamic-media.md)
* [Invalidera CDN-cachen med Dynamic Media Classic](/help/assets/dynamic-media/invalidate-cdn-cache-dm-classic.md)
* [Använd regeluppsättningar för att omforma URL:er](/help/assets/dynamic-media/using-rulesets-to-transform-urls.md)

## HTTP/2-leverans av Dynamic Media-resurser {#http-delivery-of-dynamic-media-assets}

Experience Manager stöder nu leverans av allt dynamiskt medieinnehåll (bilder och video) via HTTP/2. Det betyder att en publicerad URL eller inbäddningskod för bilden eller videon är tillgänglig för integrering med alla program som accepterar en värdbaserad resurs. Den publicerade resursen levereras sedan via HTTP/2-protokollet. Den här leveransmetoden förbättrar sättet som webbläsare och servrar kommunicerar på, vilket ger bättre respons och laddningstider för alla dynamiska medieresurser.

Mer information finns i [HTTP/2 Delivery of Content Frequently Asked Questions](/help/assets/dynamic-media/http2faq.md).

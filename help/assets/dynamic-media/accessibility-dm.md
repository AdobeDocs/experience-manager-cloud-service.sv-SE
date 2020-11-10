---
title: Tillgänglighet i [!DNL Dynamic Media]
description: Lär dig hur du arbetar med 3D-resurser i Dynamic Media
contentOwner: Rick Brough
topic-tags: introduction
content-type: reference
translation-type: tm+mt
source-git-commit: 7af8ddda4aee093b22147db9be9f65cd0c131c04
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 0%

---


# Tillgänglighet i dynamiska media {#working-with-three-d-assets-dm}

Dynamic Media har stöd för tangentbordskontroll och hjälpfunktioner som JAWS och NVDA-skärmläsare i hela användargränssnittet.



## Stöd för tangentbordstillgänglighet i Dynamic Media

Tangentbordslinjer som stöds av enskilda element i användargränssnittet är i de flesta fall enkla att upptäcka. Tangentbordskontrollen i Dynamic Media handlar om följande:

* Möjlighet att använda `Tab` - och `Shift+Tab` tangenttryckningar för att navigera mellan interaktiva element på sidan.
Användning av `Tab` flyttar indatafokus till nästa element i användargränssnittet i tabbordningen. med `Shift+Tab` får indatafokus tillbaka till föregående element i användargränssnittet.
Fokusförflyttningen följer det naturliga elementet i användargränssnittet på skärmen och flyttas från vänster till höger och sedan uppifrån och ned.
* Möjlighet att använda tangenten `Spacebar` och `Enter` för att aktivera standardelement i användargränssnittet, som knappar, listrutor o.s.v.
* Möjlighet att se fokus på tangentbordet på det aktiva elementet. Det element i användargränssnittet som har indatafokus kan få en visuell fokusindikation som en kantlinje som återges runt elementet i användargränssnittet.
* Möjlighet att använda vissa anpassade tangenttryckningar för att interagera med komplexa gränssnittselement, till exempel piltangenter i Aktiv punkt-redigeraren. I redigeraren för bildbeskärning/smart beskärning kan du använda piltangenterna för att beskära bildrutestorleken, placera om bilden eller båda.

Eftersom Dynamic Media är ett plugin-program till AEM Assets är det mesta av tangentbordskontrollbeteendet precis som i AEM Assets. Knappen i Dynamic Media har till exempel samma fokus som i AEM Assets och reagerar på `Cancel` `Spacebar` tangenten som i AEM Assets. Se [Kortkommandon i Resurser](/help/assets/accessibility.md#keyboard-shortcuts). Undantag från detta är redigeraren för aktiveringspunkter och redigerarna Bildbeskärning/Smart beskärning.

<!-- Keyboarding is the same because Dynamic Media is using the same UI library (Coral 3 (AEM 6.5) or Coral Spectrum (in Skyline)) as entire AEM Assets.  -->

I Hotspot-redigeraren kan du använda piltangenterna för att styra positionen för en aktiveringspunkt. Se [Carousel Banners](/help/assets/dynamic-media/carousel-banners.md##adding-hotspots-or-image-maps-to-an-image-banner) eller [Interactive Images](/help/assets/dynamic-media/interactive-images.md#adding-hotspots-to-an-image-banner)

Använd piltangenterna för att beskära bildrutestorleken i redigeraren för bildbeskärning/smart beskärning, eller flytta om bilden eller båda. Se [Redigera smart beskärning eller smarta färgrutor för en enskild bild](/help/assets/dynamic-media/image-profiles.md#editing-the-smart-crop-or-smart-swatch-of-a-single-image)

<!-- I think we should definitely mention this in the DM-specific area of documentation for keyboard support. -->

<!-- I would not get into much of details of specific keyboard support logic of these editors. One of the reasons - chances are that accessibility support will receive Phase2-like attention, with more holistic approach. -->

## Stöd för tangentbordstillgänglighet för Dynamic Media-visningsprogram {#keyboard-accessibility-for-dm-viewers}

Alla komponenter för dynamiska medievisningsprogram som är färdiga att användas stöder tangentbordstillgänglighet för dina kunder.

Se [Tangentbordstillgänglighet och -navigering](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/c-keyboard-accessibility.html) i referenshandboken för Dynamic Media Viewer.

## Stöd för hjälpfunktioner för Dynamic Media-visningsprogram {#assistive-technology=support-for-dm-viewers}

Alla visningsprogramkomponenter i Dynamic Media har stöd för rollerna ARIA (Accessible Rich Internet Applications) och attribut för att förbättra integrationen med hjälpmedelstekniker som skärmläsare.

Läs hjälpavsnittet om **stöd** för hjälpfunktioner i avsnittet om anpassning av visningsprogram i referenshandboken för Dynamic Media Viewer. Se till exempel [Teknikstöd](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/r-html5-video-viewer-20-assistive.html) för Video Viewer eller [Teknikstöd](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-assistive.html?lang=en#viewers-for-aem-assets-only) för Interactive Image Viewer.

>[!MORELIKETHIS]
>
>* [Tillgänglighet för Adobe-lösningar](https://www.adobe.com/accessibility.html)
>* [Tillgänglighet i Experience Manager Assets](/help/assets/dynamic-media/accessibility-dm.md)


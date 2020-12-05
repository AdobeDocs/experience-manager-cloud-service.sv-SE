---
title: Hjälpmedel i [!DNL Dynamic Media]
description: Läs mer om tillgänglighet i Dynamic Media och Dynamic Media Viewer
contentOwner: Rick Brough
topic-tags: introduction
content-type: reference
translation-type: tm+mt
source-git-commit: d87710badeeb0518a2e51b8abc3974fa77914515
workflow-type: tm+mt
source-wordcount: '621'
ht-degree: 0%

---


# Hjälpmedel i dynamiska media {#working-with-three-d-assets-dm}

Dynamic Media har stöd för tangentbordskontroll och hjälpfunktioner som JAWS och NVDA-skärmläsare i hela användargränssnittet.

## Stöd för tangentbordstillgänglighet i Dynamic Media

Eftersom Dynamic Media är ett plugin-program till Experience Manager Assets är det mesta av tangentbordskontrollbeteendet precis som i Experience Manager Assets. Knappen `Cancel` i Dynamic Media har till exempel samma fokus som i Experience Manager Assets och reagerar på `Spacebar`-tangenten som i Experience Manager Assets. Se [Kortkommandon i Resurser](/help/assets/accessibility.md#keyboard-shortcuts).

Tangentbordslinjer som stöds av enskilda element i användargränssnittet i Dynamic Media är i de flesta fall enkla att upptäcka. Tangentbordskontrollen i Dynamic Media handlar om följande:

* Möjlighet att använda `Tab` och `Shift+Tab`-tangenttryckningar för att navigera mellan interaktiva element på sidan.
Om du använder `Tab` flyttas indatafokus till nästa element i användargränssnittet i tabbordningen; om du använder `Shift+Tab` får indatafokus tillbaka till det föregående elementet i användargränssnittet.
Fokusförflyttningen följer det naturliga elementet i användargränssnittet på skärmen och flyttas från vänster till höger och sedan uppifrån och ned. Om ett fält innehåller ett fel kan du dessutom trycka på `Tab` för att flytta fokus till det.
* Möjlighet att använda tangenterna `Spacebar` och `Enter` för att aktivera standardelement i användargränssnittet, som knappar, listrutor och så vidare.
* Möjlighet att se fokus på tangentbordet på det aktiva elementet. Det element i användargränssnittet som har indatafokus kan få en visuell fokusindikation som en kantlinje som återges runt elementet i användargränssnittet.
* I Hotspot-redigeraren kan du använda vissa anpassade tangenttryckningar, till exempel piltangenter, för att interagera med komplexa element i användargränssnittet för att flytta hotspot-områden.
* I den interaktiva videoredigeraren kan du använda `Spacebar` för att markera en bild och lägga till den i ett segment. Dessutom kan du använda `Backspace`-tangenten för att ta bort det markerade objektet från fliken **[!UICONTROL Content]**. Om du trycker på `Tab`-funktioner efter behov för att navigera mellan interaktiva element på sidan.
* I redigeraren för bildbeskärning/smart beskärning kan du göra följande:
   * Använd piltangenterna för att beskära bildrutestorleken, flytta om bilden eller båda.
   * Det första `Tab`-steget markerar hela bildramen. Du kan sedan använda piltangenterna på tangentbordet för att placera bildrutan igen.
   * De följande fyra `Tab` stoppen är ramens fyra hörn. När fokus placeras i ett ramhörn markeras hörnet. Återigen kan du använda piltangenterna på tangentbordet för att flytta det fokuserade hörnet.
Se [Redigera den smarta beskärningen eller den smarta färgrutan för en enskild bild](/help/assets/dynamic-media/image-profiles.md#editing-the-smart-crop-or-smart-swatch-of-a-single-image)

<!-- Keyboarding is the same because Dynamic Media is using the same UI library (Coral 3 (AEM 6.5) or Coral Spectrum (in Skyline)) as entire AEM Assets.  -->

<!-- In the Hotspot editor, Dynamic Media lets you use arrow keys to control the position of a hot spot. See [Carousel Banners](/help/assets/dynamic-media/carousel-banners.md##adding-hotspots-or-image-maps-to-an-image-banner) or [Interactive Images](/help/assets/dynamic-media/interactive-images.md#adding-hotspots-to-an-image-banner)  -->

<!-- I think we should definitely mention this in the DM-specific area of documentation for keyboard support. -->

<!-- I would not get into much of details of specific keyboard support logic of these editors. One of the reasons - chances are that accessibility support will receive Phase2-like attention, with more holistic approach. -->

## Stöd för hjälpfunktioner i Dynamic Media {#assistive-technology=support-for-dm}

Elementen i användargränssnittet i Dynamic Media fungerar med hjälpmedelstekniker som skärmläsare. Det känner till exempel igen landmärken på en sida när du navigerar mellan landmärken med kortkommandot `D` eller regioner med kortkommandot `R`. Rubriken visas också med en berättarröst när du navigerar med rubrikens kortkommando `H`.

## Stöd för tangentbordstillgänglighet i Dynamic Media-visningsprogram {#keyboard-accessibility-for-dm-viewers}

Alla komponenter för dynamiska medievisningsprogram som är färdiga att användas stöder tangentbordstillgänglighet för dina kunder.

Se [Tangentbordstillgänglighet och -navigering](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/c-keyboard-accessibility.html) i referenshandboken för dynamiska medievyer.

## Stöd för hjälpfunktioner i Dynamic Media-visningsprogram {#assistive-technology=support-for-dm-viewers}

Alla komponenter i Dynamic Media Viewer stöder rollerna och attributen ARIA (Accessible Rich Internet Applications) för att förbättra integrationen med hjälpmedelstekniker som skärmläsare.
Se hjälpavsnittet **Stöd för hjälpteknik** i alla hjälpavsnitt som rör anpassning av visningsprogram i referenshandboken för Dynamic Media Viewer. Se till exempel [Stöd för hjälpfunktioner](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/r-html5-video-viewer-20-assistive.html) för Video Viewer eller [Stöd för hjälpfunktioner](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-assistive.html?lang=en#viewers-for-aem-assets-only) för Interactive Image Viewer.

>[!MORELIKETHIS]
>
>* [Tillgänglighet för Adobe-lösningar](https://www.adobe.com/accessibility.html)
>* [Tillgänglighet i Experience Manager Assets](/help/assets/dynamic-media/accessibility-dm.md)


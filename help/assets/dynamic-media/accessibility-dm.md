---
title: Tillgänglighet i Dynamic Media
description: Lär dig hur du arbetar med video i Dynamic Media, till exempel de bästa sätten att koda videofilmer, publicera videofilmer i YouTube och visa videorapporter. Lär dig även hur du lägger till undertexter, bildtexter eller kapitelmarkörer i videoklipp.
contentOwner: Rick Brough
topic-tags: introduction
content-type: reference
feature: Accessibility
role: Admin,User
exl-id: f8d2dcbf-f61a-4b27-a3fc-406e3662adcb
source-git-commit: 6ad46350906c3b8a36a8e361714fa5fffdbf8e82
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 0%

---

# Tillgänglighet i Dynamic Media {#accessibility-in-dm}

{{work-with-dynamic-media}}

Dynamic Media har stöd för tangentbordskontroll och hjälpmedelstekniker, som JAWS och NVDA-skärmläsare, i hela användargränssnittet.

## Stöd för tangentbordstillgänglighet i Dynamic Media {#keyboard-support-in-dm}

Eftersom Dynamic Media är ett plugin-program till [!DNL Experience Manager Assets] är det mesta av tangentbordskontrollbeteendet detsamma som i [!DNL Experience Manager Assets]. Knappen `Cancel` i Dynamic Media har till exempel samma fokus som i [!DNL Experience Manager Assets]. Den reagerar även på tangenten `Spacebar` som i [!DNL Experience Manager Assets]. Se [kortkommandon i Assets](/help/assets/accessibility.md#keyboard-shortcuts).

Tangenttryckningar som stöds av enskilda element i användargränssnittet i Dynamic Media är i de flesta fall enkla att hitta. Keyboard control in Dynamic Media is about the following:

* Möjlighet att använda `Tab`- och `Shift+Tab`-tangenttryckningar för att navigera mellan interaktiva element på sidan.
Om du använder `Tab` flyttas indatafokus till nästa element i användargränssnittet i tabbordningen. Om du använder `Shift+Tab` flyttas indatafokus tillbaka till det föregående elementet i användargränssnittet.
Fokusförflyttningen följer det naturliga elementet i användargränssnittet på skärmen och flyttas från vänster till höger och sedan uppifrån och ned. Om något fält dessutom innehåller ett fel kan du trycka på `Tab` för att flytta fokus till det.
* Möjlighet att använda tangenten `Spacebar` och `Enter` för att aktivera standardelement i användargränssnittet, till exempel knappar och nedrullningsbara listor.
* Möjlighet att se fokus på tangentbordet på det aktiva elementet. Det element i användargränssnittet som har indatafokus fick en visuell fokusindikation som en kantlinje som renderades runt elementet i användargränssnittet.
* I Hotspot-redigeraren kan du använda vissa anpassade tangenttryckningar, till exempel piltangenter, för att interagera med komplexa element i användargränssnittet för att flytta hotspot-områden.
* I den interaktiva videoredigeraren kan du använda `Spacebar` för att markera en bild och lägga till den i ett segment. Du kan dessutom använda tangenten `Backspace` för att ta bort det markerade objektet från fliken **[!UICONTROL Content]**. Tryck också på `Tab` för att navigera mellan interaktiva element på sidan.
* I redigeraren för bildbeskärning/smart beskärning kan du göra följande:
   * Använd piltangenterna för att beskära bildrutestorleken, flytta bilden eller båda.
   * Det första `Tab` steget markerar hela bildramen. Du kan sedan använda piltangenterna på tangentbordet för att flytta ramen.
   * De följande fyra `Tab` stoppen är ramens fyra hörn. När fokus placeras på ett ramhörn markeras hörnet. Återigen kan du använda piltangenterna på tangentbordet för att flytta det fokuserade hörnet.
Se [Redigera den smarta beskärningen eller den smarta färgrutan för en enskild bild](/help/assets/dynamic-media/image-profiles.md#editing-the-smart-crop-or-smart-swatch-of-a-single-image)

<!-- Keyboarding is the same because Dynamic Media is using the same UI library (Coral 3 (Experience Manager 6.5) or Coral Spectrum (in Skyline)) as entire Experience Manager Assets.  -->

<!-- In the Hotspot editor, Dynamic Media lets you use arrow keys to control the position of a hot spot. See [Carousel Banners](/help/assets/dynamic-media/carousel-banners.md#adding-hotspots-or-image-maps-to-an-image-banner) or [Interactive Images](/help/assets/dynamic-media/interactive-images.md#adding-hotspots-to-an-image-banner)  -->

<!-- I think we should definitely mention this in the DM-specific area of documentation for keyboard support. -->

<!-- I would not get into much of details of specific keyboard support logic of these editors. One of the reasons - chances are that accessibility support will receive Phase2-like attention, with more holistic approach. -->

## Stöd för hjälpfunktioner i Dynamic Media {#assistive-technology=support-for-dm}

Dynamic Media gränssnittselement fungerar med hjälpmedelstekniker som skärmläsare. Det känner till exempel igen landmärken på en sida när du navigerar mellan landmärken med kortkommandot `D` eller regioner med kortkommandot `R`. Rubriken visas också med en berättarröst när du navigerar med rubrikkortkommandot `H`.

## Stöd för tangentbordstillgänglighet i Dynamic Media-visningsprogram {#keyboard-accessibility-for-dm-viewers}

Alla färdiga Dynamic Media-visningsprogram har stöd för tangentbordstillgänglighet för dina kunder.

Se [Tangentbordstillgänglighet och navigering](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/c-keyboard-accessibility.html) i referenshandboken för Dynamic Media-visningsprogram.

## Stöd för hjälpfunktioner i Dynamic Media-visningsprogram {#assistive-technology=support-for-dm-viewers}

Alla Dynamic Media-visningsprogramkomponenter har stöd för ARIA-roller (Accessible Rich Internet Applications) och -attribut för att förbättra integrationen med hjälpmedelstekniker som skärmläsare.
Läs hjälpavsnittet **Stöd för hjälpfunktioner** i avsnittet om anpassning av visningsprogram i referenshandboken för Dynamic Media Viewer. Se till exempel [Teknikstöd](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/r-html5-video-viewer-20-assistive.html) för Video Viewer eller [Teknikstöd](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-assistive.html#viewers-for-aem-assets-only) för Interactive Image Viewer.

## Stöd för undertexter i [!DNL Dynamic Media] {#closed-caption-support}

Dynamic Media stöder leverans av videor och adaptiva videouppsättningar med undertexter. Bildtexterna måste visas ovanpå videoinnehållet.

Se [Video i Dynamic Media - Lägg till undertexter i videon](/help/assets/dynamic-media/video.md#adding-captions-to-video).


>[!MORELIKETHIS]
>
>* [Tillgänglighet för Adobe-lösningar](https://www.adobe.com/accessibility.html)
>* [Hjälpmedel i Experience Manager Assets](/help/assets/dynamic-media/accessibility-dm.md)

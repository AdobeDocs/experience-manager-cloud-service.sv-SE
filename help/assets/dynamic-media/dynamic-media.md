---
title: Arbeta med Dynamic Media
description: Lär dig hur du använder Dynamic Media för att leverera mediefiler för webben, mobiler och sociala medier.
translation-type: tm+mt
source-git-commit: a8eb6a88b889facca8518c05a80051fc17dd0617
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 7%

---


# Arbeta med Dynamic Media {#working-with-dynamic-media}

[Dynamic ](https://www.adobe.com/solutions/web-experience-management/dynamic-media.html) Media hjälper er att leverera visuella marknadsförings- och marknadsföringsresurser on demand, som automatiskt skalas för konsumtion på webben, mobilsajter och sociala medier. Med en uppsättning primära källresurser genererar och levererar Dynamic Media flera varianter av multimedieinnehåll i realtid via sitt globala, skalbara, prestandaoptimerade nätverk.

Dynamic Media visar interaktivt material, som zoomning, 360-graders rotation och video. Dynamic Media införlivar smidigt arbetsflödena i Adobe Experience Manager Digital Asset Management (Assets) för att förenkla och effektivisera hanteringen av digitala kampanjer.

<!-- >[!NOTE]
>
>A Community article is available on [Working with Adobe Experience Manager and Dynamic Media](https://helpx.adobe.com/experience-manager/using/aem_dynamic_media.html). -->

## Vad du kan göra med Dynamic Media {#what-you-can-do-with-dynamic-media}

Med Dynamic Media kan du hantera dina resurser innan du publicerar dem. Hur du arbetar med resurser i allmänhet beskrivs i detalj i [Arbeta med digitala resurser](/help/assets/manage-digital-assets.md). Allmänna ämnen är bland annat att ladda upp, ladda ned, redigera och publicera material. visa och redigera egenskaper och söka efter resurser.

Dynamic Media har följande funktioner:

* [Karusellbanner](carousel-banners.md)
* [Bilduppsättningar](image-sets.md)
* [Interaktiva bilder](interactive-images.md)
* [Interaktiva videoklipp](interactive-videos.md)
* [Blandade medieuppsättningar](mixed-media-sets.md)
* [Panoramabilder](panoramic-images.md)

* [Snurrande uppsättningar](spin-sets.md)
* [Video](video.md)
* [Leverera Dynamic Media Assets](delivering-dynamic-media-assets.md)
* [Hantera resurser](managing-assets.md)
* [Använda snabbvyer för att skapa anpassade popup-fönster](custom-pop-ups.md)

Se även [Konfigurera Dynamic Media](administering-dynamic-media.md).

<!-- 

OBSOLETE UNTIL INTEGRATING SCENE7 TOPIC GETS A MAJOR UPDATE
>[!NOTE]
>
>To understand the differences between using Dynamic Media and integrating Dynamic Media Classic with AEM, see [Dynamic Media Classic integration versus Dynamic Media](/help/sites-cloud/administering/integrating-scene7.md#aem-scene-integration-versus-dynamic-media).

-->

## Dynamic Media aktiverat jämfört med Dynamic Media inaktiverat {#dynamic-media-on-versus-dynamic-media-off}

Du kan se om Dynamic Media är aktiverat (aktiverat) enligt följande:

* Dynamiska återgivningar är tillgängliga när du hämtar eller förhandsgranskar resurser.
* Bilduppsättningar, snurruppsättningar, blandade medieuppsättningar är tillgängliga.
* PTIFF-återgivningar skapas.

När du klickar på en bildresurs ser resursen annorlunda ut med Dynamic Media aktiverat. Dynamic Media använder on demand-visningsprogrammen för HTML5.

### Dynamiska renderingar {#dynamic-renditions}

Dynamiska renderingar som bild- och visningsförinställningar (under **[!UICONTROL Dynamic]**) är tillgängliga när Dynamic Media är aktiverat.

![chlimage_1-358](assets/chlimage_1-358.png)

### Bilduppsättningar, snurruppsättningar, blandade medieuppsättningar {#image-sets-spins-sets-mixed-media-sets}

Uppsättningar med bilder, snurra och blandade medieuppsättningar är tillgängliga om Dynamic Media är aktiverat.

![chlimage_1-359](assets/chlimage_1-359.png)

### PTIFF-återgivningar {#ptiff-renditions}

Dynamic Media-aktiverade resurser innehåller `pyramid.tiffs`.

![chlimage_1-360](assets/chlimage_1-360.png)

### Resursvyer ändras {#asset-views-change}

När Dynamic Media är aktiverat kan du zooma in och ut genom att klicka på knapparna `+` och `-`. Du kan också klicka/trycka för att zooma in i ett visst område. Med Återställ återgår du till den ursprungliga versionen och du kan göra bilden i helskärmsläge genom att klicka på de diagonala pilarna. Dynamic Media-aktiverad ser ut så här:

![chlimage_1-361](assets/chlimage_1-361.png)

Med Dynamic Media inaktiverat kan du zooma in och ut och återställa till den ursprungliga storleken:

![chlimage_1-362](assets/chlimage_1-362.png)

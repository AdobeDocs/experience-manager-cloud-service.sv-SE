---
title: Arbeta med Dynamic Media
description: Läs mer om vad Dynamic Media är och hur ni kan använda Dynamic Media för att leverera material för webben, mobiler och sociala medier.
contentOwner: Rick Brough
feature: Dynamic Media,Asset Management
role: Admin,User
exl-id: 3ec3cb85-88ce-4277-a45c-30e52c75ed42
source-git-commit: bc422429d4a57bbbf89b7af2283b537a1f516ab5
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 1%

---

# Arbeta med Dynamic Media {#working-with-dynamic-media}

[Dynamic Media](https://business.adobe.com/products/experience-manager/assets/dynamic-media.html) hjälper till att leverera visuella marknadsförings- och marknadsföringsresurser on demand, som automatiskt skalas för konsumtion på webben, mobiler och sociala medier. Med hjälp av en uppsättning primära källresurser genererar och levererar Dynamic Media flera varianter av multimediematerial i realtid via sitt globala, skalbara, prestandaoptimerade nätverk.

Dynamic Media levererar interaktiva visningsupplevelser som zoomning, 360-gradersrotation och video. Dynamic Media införlivar arbetsflödena i Adobe Experience Manager Digital Asset Management (Assets) för att förenkla och effektivisera hanteringen av digitala kampanjer.

<!-- 
>[!NOTE]
>
>A Community article is available on [Working with Adobe Experience Manager and Dynamic Media](https://helpx.adobe.com/experience-manager/using/aem_dynamic_media.html). 
-->

## Vad är Dynamic Media?

Dynamic Media i Adobe Experience Manager (AEM) as a Cloud Service är en kraftfull lösning som hjälper dig att hantera, leverera och optimera mediematerial som bilder och videor för olika digitala plattformar. Det omvandlar statiska medier till dynamiska, engagerande upplevelser genom att tillåta realtidsändringar, som storleksändring, beskärning och kvalitetsjustering baserat på användarens enhet eller skärmstorlek. Med Dynamic Media anpassar sig materialet automatiskt för att ge den bästa visuella upplevelsen, oavsett om användarna arbetar på en dator, mobil eller surfplatta.

En stor fördel med Dynamic Media är möjligheten att effektivisera mediehanteringen. Du behöver inte skapa flera versioner av bilder eller videor - Dynamic Media hanterar allt genom att leverera det format som passar bäst för varje situation. E-handelsföretag kan till exempel dra nytta av 360-graders produktvisningar eller zoombara bilder för att skapa interaktiva upplevelser, medan innehållsintensiva webbplatser kan säkerställa snabb, högkvalitativ videoströmning. Detta ger snabbare laddningstider och mer engagerande användarupplevelser, vilket i slutänden leder till bättre kundnöjdhet och bättre konverteringsgrader.

Dynamic Media kan integreras smidigt med ditt DAM-system (Digital Asset Management) i AEM, vilket ger en gemensam plattform för att lagra, ordna och driftsätta medierna. Detta centraliserade tillvägagångssätt förenklar samarbetet mellan team och ger realtidsinsikter om resursprestanda. Oavsett om ni fokuserar på att leverera engagerande bilder eller förbättra mediadriven användarinteraktion hjälper Dynamic Media er att optimera ert innehåll för alla kanaler, vilket gör det till ett oumbärligt verktyg för företag som vill höja sin digitala närvaro.

## Vad du kan göra med Dynamic Media {#what-you-can-do-with-dynamic-media}

Med Dynamic Media kan du hantera dina resurser innan du publicerar dem. Hur du arbetar med resurser i allmänhet beskrivs i detalj i [Arbeta med Digital Assets](/help/assets/manage-digital-assets.md). Allmänna ämnen är bland annat att ladda upp, ladda ned, redigera och publicera resurser, visa och redigera egenskaper och söka efter resurser.

Funktioner som bara är dynamiska media inkluderar följande:

* [Carousel Banners](carousel-banners.md)
* [Bilduppsättningar](image-sets.md)
* [Interaktiva bilder](interactive-images.md)
* [Interaktiva videoklipp](interactive-videos.md)
* [Blandade medieuppsättningar](mixed-media-sets.md)
* [Panorambilder](panoramic-images.md)
* [Snurra uppsättningar](spin-sets.md)
* [Video](video.md)
* [Leverera Dynamic Media Assets](delivering-dynamic-media-assets.md)
* [Hantera Assets](managing-assets.md)
* [Använda snabbvyer för att skapa anpassade popup-fönster](custom-pop-ups.md)

Se även [Konfigurera dynamiska media](administering-dynamic-media.md).

<!-- 

OBSOLETE UNTIL INTEGRATING SCENE7 TOPIC GETS A MAJOR UPDATE
>[!NOTE]
>
>To understand the differences between using Dynamic Media and integrating Dynamic Media Classic with AEM, see [Dynamic Media Classic integration versus Dynamic Media](/help/sites-cloud/administering/integrating-scene7.md#aem-scene-integration-versus-dynamic-media).

-->

## Dynamiska media aktiverat jämfört med Dynamic Media inaktiverat {#dynamic-media-on-versus-dynamic-media-off}

Du kan se om Dynamic Media är aktiverat (aktiverat) av följande egenskaper:

* Dynamiska återgivningar är tillgängliga när du hämtar eller förhandsgranskar resurser.
* Bilduppsättningar, snurruppsättningar, blandade medieuppsättningar är tillgängliga.
* PTIFF-återgivningar skapas.

När du klickar på en bildresurs ser resursen annorlunda ut med Dynamic Media aktiverat. Dynamic Media använder on-demand-visningsprogrammen från HTML5.

### Dynamiska renderingar {#dynamic-renditions}

Dynamiska återgivningar som bild- och visningsförinställningar (under **[!UICONTROL Dynamic]**) är tillgängliga när Dynamic Media är aktiverat.

![chlimage_1-358](assets/chlimage_1-358.png)

### Dynamiska medieuppsättningar, snurruppsättningar, blandade medieuppsättningar {#image-sets-spins-sets-mixed-media-sets}

Bilduppsättningar, snurruppsättningar och blandade medieuppsättningar är tillgängliga om Dynamic Media är aktiverat.

![chlimage_1-359](assets/chlimage_1-359.png)

### PTIFF-renderingar aktiverade för dynamiska media {#ptiff-renditions}

Dynamiska mediaaktiverade resurser innehåller `pyramid.tiffs`.

![chlimage_1-360](assets/chlimage_1-360.png)

### Vyerna för dynamiska medieresurser ändras {#asset-views-change}

När Dynamic Media är aktiverat kan du zooma in och ut genom att klicka på knapparna `+` och `-`. Du kan också välja att zooma in i ett visst område. Med Återställ återgår du till den ursprungliga versionen och du kan göra bilden i helskärmsläge genom att klicka på de diagonala pilarna. Dynamiska media som är aktiverat ser ut så här:

![chlimage_1-361](assets/chlimage_1-361.png)

När Dynamic Media är inaktiverat kan du zooma in och ut och återgå till den ursprungliga storleken:

![chlimage_1-362](assets/chlimage_1-362.png)

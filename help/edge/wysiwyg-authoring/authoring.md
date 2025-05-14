---
title: WYSIWYG Content Authoring for Edge Delivery Services
description: Lär dig hur innehållsutveckling fungerar med Edge Delivery Services och hur du skapar AEM-innehåll med Edge Delivery Services.
feature: Edge Delivery Services
exl-id: 963ff71a-8176-4d9d-8240-dc429405d139
role: User
index: false
hide: true
hidefromtoc: true
source-git-commit: e57610e4c5e498ddfdbaa0ba39c9197ecfb5d177
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 0%

---


# WYSIWYG Content Authoring for Edge Delivery Services {#authoring-edge}

Med Edge Delivery Services är det enkelt, snabbt och flexibelt att skapa. Det finns två alternativ för att skapa innehåll för Edge Delivery Services:

* [Universell redigerare](#universal-editor) - Ett modernt användargränssnitt för det du-se-is-what-you-get (WYSIWYG) för att skapa innehåll i AEM
* [Dokumentbaserad redigering](#document-based) - t.ex. Microsoft Word eller Google Docs

## Redigering i Universal Editor {#universal-editor}

När du använder Edge Delivery Services med AEM as a Cloud Service är det mest grundläggande att förstå att det innehåll du skapar bevaras i AEM as a Cloud Service.

![Så här fungerar WYSIWYG Authoring med Edge Delivery Services](assets/how-aem-edge-works.png)

1. [AEM Sites-miljön](/help/sites-cloud/authoring/quick-start.md) används för innehållshantering som att skapa nya sidor, upplevelsefragment, innehållsfragment osv.
   * Alla funktioner i AEM är tillgängliga, t.ex. arbetsflöden, MSM, översättning, startprogram.
1. [Den universella redigeraren](/help/sites-cloud/authoring/universal-editor/authoring.md) används för att skapa innehåll som hanteras i AEM.
   * Universal Editor har ett nytt och modernt gränssnitt för framtagning av material.
   * AEM återger HTML men innehåller skript, format, ikoner och andra resurser från Edge Delivery Services.
   * Även om Universell redigerare används sparas alla ändringar i AEM.
   * Den universella redigeraren fungerar ännu inte som den ska i AEM Page Editor och vissa AEM-funktioner kanske inte är tillgängliga i den universella redigeraren.
1. Innehåll som du skapar med den universella redigeraren och behåller för AEM publiceras till Edge Delivery Services.
   * Innehållet lagras i AEM.
   * AEM återger semantiska HTML som behövs för intag.
   * Innehåll publiceras till Edge Delivery Services.
1. [Edge Delivery Services](/help/edge/developer/keeping-it-100.md) säkerställer 100 % Lighthuse-poäng.

Block är grundläggande komponenter i en sida som levereras av Edge Delivery Services. Man kan välja mellan standardblock som Adobe tillhandahåller som standard eller block som utvecklarna anpassat för ditt projekt.

Universal Editor är ett modernt och intuitivt GUI som du kan använda för att skapa innehåll genom att lägga till och ordna block.

![Lägga till och ordna block i den universella redigeraren](assets/blocks.png)

Information om blocken kan sedan konfigureras på egenskapspanelen.

![Konfigurerar blockegenskaper](assets/block-properties.png)

Mer information om hur du redigerar med den universella redigeraren finns i dokumentet [Skapa innehåll med den universella redigeraren](/help/sites-cloud/authoring/universal-editor/authoring.md).

Läs [Utvecklarhandboken Komma igång för WYSIWYG-redigering med Edge Delivery Services](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md) om du vill veta hur du startar ett eget projekt som du kan skapa med AEM och Edge Delivery Services.

## Ytterligare redigeringsmetoder  {#authoring-methods}

WYSIWYG är ett kraftfullt och intuitivt verktyg för skribenter. Det finns dock många olika användningsområden, och därför erbjuder AEM ytterligare redigeringslösningar.

Läs dokumentet [Edge Delivery Services Overview](/help/edge/overview.md#authoring-method) om du vill veta mer om de redigeringslösningar som AEM erbjuder, inklusive dokumentbaserad redigering och headless.

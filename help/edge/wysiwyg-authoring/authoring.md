---
title: Skapa innehåll för Edge Delivery Services
description: Lär dig hur innehållsredigering fungerar med Edge Delivery Services och hur du redigerar AEM innehåll med Edge Delivery Services.
feature: Edge Delivery Services
exl-id: 963ff71a-8176-4d9d-8240-dc429405d139
role: User
source-git-commit: 7ad9a959592f1e8cebbcad9a67d280d5b2119866
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 0%

---


# Skapa innehåll för Edge Delivery Services {#authoring-edge}

Med Edge Delivery Services är det enkelt, snabbt och flexibelt att skapa. Du kan skapa innehåll för Edge Delivery Services på två sätt:

* [Universell redigerare](#universal-editor) - Ett modernt WYSIWYG-gränssnitt för att skapa innehåll i AEM
* [Dokumentbaserad redigering](#document-based) - t.ex. Microsoft Word eller Google Docs

## Redigering i Universal Editor {#universal-editor}

När du använder Edge Delivery Services med AEM as a Cloud Service är det viktigaste att förstå att det innehåll du skapar bevaras i AEM as a Cloud Service.

![Så här fungerar WYSIWYG-redigering med Edge Delivery Services](assets/how-aem-edge-works.png)

1. [WYSIWYG-redigeringsmiljön](/help/sites-cloud/authoring/quick-start.md) används för innehållshantering som att skapa nya sidor, upplevelsefragment, innehållsfragment osv.
   * Alla funktioner i AEM är tillgängliga, t.ex. arbetsflöden, MSM, översättning, startprogram.
1. [Den universella redigeraren](/help/sites-cloud/authoring/universal-editor/authoring.md) används för att skapa innehåll som hanteras i AEM.
   * Universal Editor har ett nytt och modernt gränssnitt för framtagning av material.
   * För redigering återges HTML i AEM men skript, format, ikoner och andra resurser från Edge Delivery Services tas med.
   * Även om Universell redigerare används sparas alla ändringar i AEM.
   * Den universella redigeraren fungerar ännu inte som den AEM sidredigeraren och en del AEM funktioner kanske inte är tillgängliga i den universella redigeraren.
1. Innehåll som du redigerar med den universella redigeraren och som bevaras för AEM publiceras till Edge Delivery Services.
   * Innehållet sparas i AEM.
   * AEM återger semantiskt HTML som behövs för intag.
   * Innehåll publiceras till Edge Delivery Services.
1. [Edge Delivery Services](/help/edge/developer/keeping-it-100.md) säkerställer 100 % Lighthhade-poäng.

Block är grundläggande komponenter i en sida som levereras av Edge Delivery Services. Författare kan välja bland standardblock som tillhandahålls som standard av Adobe eller block som anpassas för ditt projekt av utvecklarna.

Universal Editor är ett modernt och intuitivt GUI som du kan använda för att skapa innehåll genom att dra och släppa block.

![Dra och släppa block i den universella redigeraren](assets/blocks.png)

Information om blocken kan sedan konfigureras i egenskapsfältet.

![Konfigurerar blockegenskaper](assets/block-properties.png)

Mer information om hur du redigerar med den universella redigeraren finns i dokumentet [Skapa innehåll med den universella redigeraren.](/help/sites-cloud/authoring/universal-editor/authoring.md)

Läs [Utvecklarhandboken Komma igång för WYSIWYG-redigering med Edge Delivery Services](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md) om du vill veta hur du startar ett eget projekt som du kan skapa med AEM och Edge Delivery Services.

## Dokumentbaserad redigering  {#document-based}

När du använder dokumentbaserad redigering kan du arbeta med olika källor som Microsoft Word- och Google Docs-dokument. Dokument från dessa källor blir sidor på din webbplats. Rubriker, listor, bilder, teckensnittselement och videor kan alla överföras från den ursprungliga källan till webbplatsen. Du kan lägga till metadata för SEO-syften eller använda block för att arbeta med strukturerat innehåll och lägga till funktioner.

Mer information om dokumentbaserad redigering finns i [det här dokumentet i dokumentationen för Edge Delivery Services.](/help/edge/docs/authoring.md)


---
title: Skapa innehåll för Edge Delivery Services
description: Lär dig hur innehållsredigering fungerar med Edge Delivery Services och hur du redigerar AEM innehåll med Edge Delivery Services.
feature: Edge Delivery Services
source-git-commit: f6e1c5de57ee0297abdf6b03faf550a266dfac32
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 0%

---


# Skapa innehåll för Edge Delivery Services {#authoring-edge}

Med Edge Delivery Services är det enkelt, snabbt och flexibelt att skapa. Du kan skapa innehåll för Edge Delivery Services på två sätt:

* [Dokumentbaserad redigering](#document-based) - t.ex. Microsoft Word eller Google Docs
* [Universal Editor](#universal-editor) - Ett modernt användargränssnitt för att skapa innehåll i AEM

## Dokumentbaserad redigering {#document-based}

Vid dokumentbaserad redigering kan du arbeta med olika källor som Microsoft Word och Google Docs. Dokument från dessa källor blir sidor på din webbplats. Rubriker, listor, bilder, teckensnittselement och videor kan alla överföras från den ursprungliga källan till webbplatsen. Du kan lägga till metadata för SEO-syften eller använda block för att arbeta med strukturerat innehåll och lägga till funktioner.

Mer information om dokumentbaserad redigering finns i [det här dokumentet i dokumentationen för Edge Delivery Services.](https://www.aem.live/docs/authoring)

## Redigering i Universal Editor {#universal-editor}

När du använder Edge Delivery Services med AEM as a Cloud Service är det mest grundläggande att förstå att det innehåll du skapar bevaras i AEM as a Cloud Service.

![Hur AEM fungerar med Edge Delivery Services](assets/how-aem-edge-works.png)

1. [AEM redigeringsmiljö](/help/sites-cloud/authoring/getting-started/quick-start.md) används för innehållshantering som att skapa nya sidor, upplevelsefragment, innehållsfragment osv.
   * Alla funktioner i AEM är tillgängliga, t.ex. arbetsflöden, MSM, översättning, startprogram.
1. [Universell redigerare](/help/implementing/universal-editor/authoring.md) används för att skapa innehåll som hanteras i AEM.
   * Universal Editor har ett nytt och modernt gränssnitt för framtagning av material.
   * För redigering återges HTML i AEM men skript, format, ikoner och andra resurser från Edge Delivery Services tas med.
   * Även om Universell redigerare används sparas alla ändringar i AEM.
   * Den universella redigeraren fungerar ännu inte som den AEM sidredigeraren och en del AEM funktioner kanske inte är tillgängliga i den universella redigeraren.
1. Innehåll som du redigerar med den universella redigeraren och som bevaras för AEM publiceras till Edge Delivery Services.
   * Innehållet sparas i AEM.
   * AEM återger semantiskt HTML som behövs för intag.
   * Innehåll publiceras till Edge Delivery Services.
1. [Edge Delivery Services](https://www.aem.live/home) säkerställa 100 % Lighhade-poäng.

Block är grundläggande komponenter i en sida som levereras av Edge Delivery Services. Författare kan välja bland standardblock som tillhandahålls som standard av Adobe eller block som anpassas för ditt projekt av utvecklarna.

Universal Editor är ett modernt och intuitivt GUI som du kan använda för att skapa innehåll genom att dra och släppa block.

![Dra och släppa block i den universella redigeraren](assets/blocks.png)

Information om blocken kan sedan konfigureras i egenskapsfältet.

![Konfigurera blockegenskaper](assets/block-properties.png)

Mer information om hur du redigerar i Universal Editor finns i dokumentet [Skapa innehåll med den universella redigeraren.](/help/implementing/universal-editor/authoring.md)

## Så här kommer du igång {#how-to-get-started}

Kontakta din Adobe-representant för att få tillgång till den här funktionen.

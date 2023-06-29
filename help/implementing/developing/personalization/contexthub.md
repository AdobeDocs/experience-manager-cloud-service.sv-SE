---
title: ContextHub
description: ContextHub är ett ramverk för att lagra, ändra och presentera kontextdata
exl-id: 604477c6-d96a-441f-b5fc-5def93832478
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 0%

---

# ContextHub {#contexthub}

ContextHub är ett ramverk för att lagra, ändra och presentera kontextdata. Den viktigaste funktionen är möjligheten att [visa kontextdata samtidigt som man simulerar och växlar mellan olika personligheter](/help/sites-cloud/authoring/personalization/contexthub.md).

Med ContextHub kan du:

* [Presentera, visa, växla mellan personligheter och simulera användarupplevelsen](#presentation) när sidor skapas med kontextdata.
* [Behåll kontextdata](#persistence) på webbplatsen som en datalagerrepresentation.
* [Hantera segment](#segmentation) för den markerade kontexten.

Med JavaScript API:t på klientsidan kan du komma åt data för att anpassa innehåll.

## Presentation {#presentation}

The [ContextHub-verktygsfältet](/help/sites-cloud/authoring/personalization/contexthub.md) gör det möjligt för marknadsförare och författare att se och ändra butiksdata för att simulera användarupplevelsen när de skapar sidor. Verktygsfältet består av grupper med UI-moduler som ger åtkomst till [ContextHub-butiker,](#persistence) som innehåller ContextHub-data på klienten.

Varje ContextHub-gränssnittsmodul är en instans av en fördefinierad modultyp:

* ContextHub innehåller flera [exempelmodultyper](sample-modules.md).
* Använd AEM konsoler för att [lägg till gränssnittsmoduler](configuring-contexthub.md#adding-a-ui-module)och till [gruppera dem i gränssnittslägen](configuring-contexthub.md#adding-a-ui-mode).
* Utvecklare kan [skapa anpassade modultyper](extending-contexthub.md#creating-contexthub-ui-module-types).

Utvecklare måste [lägg till ContextHub-komponenten på sidan](configuring-contexthub.md).

## Persistence {#persistence}

ContextHub lagrar kontextdata på klienten. Med ContextHub JavaScript API kan du komma åt butiker för att skapa, uppdatera och ta bort data efter behov. Därför representerar ContextHub ett datalager på dina sidor.

Varje ContextHub-butik är en instans av en fördefinierad lagringstyp:

* ContextHub innehåller flera [exempelarkivtyper](sample-stores.md).
* Använd AEM konsoler för att [skapa butiker](configuring-contexthub.md#creating-a-contexthub-store).
* Utvecklare kan [skapa anpassade butikstyper](extending-contexthub.md#creating-custom-store-candidates).
* Utvecklare kan [åtkomstarkivdata](adding-contexthub.md#interacting-with-contexthub-stores) genom JavaScript.

## Segmentering {#segmentation}

ContextHub innehåller en segmenteringsmotor som hanterar segment och fastställer vilka segment som matchas för den aktuella kontexten. Flera segment är definierade. Du kan använda JavaScript-API:t för att [identifiera matchade segment](adding-contexthub.md#determining-resolved-contexthub-segments).

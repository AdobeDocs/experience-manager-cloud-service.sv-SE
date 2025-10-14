---
title: ContextHub
description: ContextHub är ett ramverk för att lagra, ändra och presentera kontextdata
exl-id: 604477c6-d96a-441f-b5fc-5def93832478
feature: Developing, Personalization
role: Admin, Architect, Developer
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 0%

---

# ContextHub {#contexthub}

ContextHub är ett ramverk för att lagra, ändra och presentera kontextdata. Dess primära funktion är att erbjuda möjligheten att [visa kontextdata samtidigt som man simulerar och växlar mellan olika profiler &#x200B;](/help/sites-cloud/authoring/personalization/contexthub.md).

Med ContextHub kan du:

* [Presentera, visa, växla mellan olika profiler och simulera användarupplevelsen](#presentation) när du redigerar sidor med hjälp av kontextdata.
* [Behåll kontextdata](#persistence) på webbplatsen som en datalagerrepresentation.
* [Hantera segment](#segmentation) för den valda kontexten.

Med JavaScript-API:t på klientsidan kan du komma åt data för att anpassa innehåll.

## Presentation {#presentation}

Verktygsfältet [ContextHub](/help/sites-cloud/authoring/personalization/contexthub.md) gör att marknadsförare och författare kan se och ändra lagringsdata för att simulera användarupplevelsen när de skapar sidor. Verktygsfältet består av grupper med gränssnittsmoduler som ger åtkomst till [ContextHub-butiker](#persistence), som innehåller ContextHub-data på klienten.

Varje ContextHub-gränssnittsmodul är en instans av en fördefinierad modultyp:

* ContextHub innehåller flera [exempelmodultyper](sample-modules.md).
* Använd AEM konsoler för att [lägga till gränssnittsmoduler](configuring-contexthub.md#adding-a-ui-module) och för att [gruppera dem i gränssnittslägen](configuring-contexthub.md#adding-a-ui-mode).
* Utvecklare kan [skapa anpassade modultyper](extending-contexthub.md#creating-contexthub-ui-module-types).

Utvecklare måste [lägga till ContextHub-komponenten på sidan](configuring-contexthub.md).

## Persistence {#persistence}

ContextHub lagrar kontextdata på klienten. Med ContextHub JavaScript API kan du komma åt butiker för att skapa, uppdatera och ta bort data efter behov. Därför representerar ContextHub ett datalager på dina sidor.

Varje ContextHub-butik är en instans av en fördefinierad lagringstyp:

* ContextHub innehåller flera [typer av exempelarkiv](sample-stores.md).
* Använd AEM för att [skapa butiker](configuring-contexthub.md#creating-a-contexthub-store).
* Utvecklare kan [skapa anpassade butikstyper](extending-contexthub.md#creating-custom-store-candidates).
* Utvecklare kan [komma åt lagringsdata](adding-contexthub.md#interacting-with-contexthub-stores) via JavaScript.

## Segmentering {#segmentation}

ContextHub innehåller en segmenteringsmotor som hanterar segment och fastställer vilka segment som matchas för den aktuella kontexten. Flera segment är definierade. Du kan använda JavaScript API för att [identifiera lösta segment](adding-contexthub.md#determining-resolved-contexthub-segments).

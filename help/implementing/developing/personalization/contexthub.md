---
title: ContextHub
description: ContextHub är ett ramverk för att lagra, ändra och presentera kontextdata
translation-type: tm+mt
source-git-commit: b8bc27b51eefcfcfa1c23407a4ac0e7ff068081e
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 0%

---


# ContextHub {#contexthub}

ContextHub är ett ramverk för att lagra, ändra och presentera kontextdata. Den primära funktionen är möjligheten att [visa kontextdata samtidigt som man simulerar och växlar mellan olika profiler.](/help/sites-cloud/authoring/personalization/contexthub.md)

Med ContextHub kan du:

* [Presentera, visa, växla mellan personligheter och simulera användarupplevelser ](#presentation) när du redigerar sidor med hjälp av kontextdata.
* [Bevara kontextdata ](#persistence) på webbplatsen som en datalagerrepresentation.
* [Hantera ](#segmentation) segment för den valda kontexten.

Javascript-API:t på klientsidan gör att du kan komma åt data för att anpassa innehåll.

## Presentation {#presentation}

Med verktygsfältet [ContextHub](/help/sites-cloud/authoring/personalization/contexthub.md) kan marknadsförare och författare visa och ändra lagringsdata för att simulera användarupplevelsen när de skapar sidor. Verktygsfältet består av grupper med UI-moduler som ger åtkomst till [ContextHub-arkiv,](#persistence) som innehåller ContextHub-data på klienten.

Varje ContextHub-gränssnittsmodul är en instans av en fördefinierad modultyp:

* ContextHub innehåller flera [exempelmodultyper](sample-modules.md).
* Använd AEM konsoler för att [lägga till gränssnittsmoduler](configuring-contexthub.md#adding-a-ui-module) och för att [gruppera dem i gränssnittslägen](configuring-contexthub.md#adding-a-ui-mode).
* Utvecklare kan [skapa anpassade modultyper](extending-contexthub.md#creating-contexthub-ui-module-types).

Utvecklare måste [lägga till ContextHub-komponenten på sidan](configuring-contexthub.md).

## Persistence {#persistence}

ContextHub lagrar kontextdata på klienten. Med ContextHub Javascript API kan du komma åt arkiv för att skapa, uppdatera och ta bort data efter behov. Därför representerar ContextHub ett datalager på dina sidor.

Varje ContextHub-butik är en instans av en fördefinierad lagringstyp:

* ContextHub innehåller flera [typer av exempelarkiv](sample-stores.md).
* Använd AEM konsoler för att [skapa butiker](configuring-contexthub.md#creating-a-contexthub-store).
* Utvecklare kan [skapa anpassade butikstyper](extending-contexthub.md#creating-custom-store-candidates).
* Utvecklare kan [komma åt butiksdata](adding-contexthub.md#interacting-with-contexthub-stores) via Javascript.

## Segmentering {#segmentation}

ContextHub innehåller en segmenteringsmotor som hanterar segment och fastställer vilka segment som matchas för den aktuella kontexten. Flera segment är definierade. Du kan använda Javascript-API:t för att [identifiera lösta segment](adding-contexthub.md#determining-resolved-contexthub-segments).

---
title: Skapande och publicering av begrepp
description: Lär dig mer om redigering i AEM, med hjälp av redigerings-, förhandsgransknings- och publiceringsmiljöer.
exl-id: ee9e4952-e075-4398-b31f-d7886153efff
source-git-commit: bbd845079cb688dc3e62e2cf6b1a63c49a92f6b4
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 0%

---


# Skapande och publicering av begrepp {#authoring-publishing}

För en innehållsförfattare kan en AEM as a Cloud Service installation betraktas som tre primära lager på den mest grundläggande nivån

* Författarnivå
* Förhandsgranskningsnivå
* Publiceringsnivå

Dessa nivåer interagerar så att ni kan göra innehåll tillgängligt på er webbplats så att era besökare kan komma åt det. Det grundläggande arbetsflödet är:

1. Innehållsförfattare skapar sitt innehåll med hjälp av författarnivån.
1. Innehållsförfattare gör sitt innehåll tillgängligt för granskare att förhandsgranska med förhandsgranskningsnivån.
1. När innehållet är klart för allmänheten publicerar författarna innehållet med publiceringsnivån.

Innehåll kan vara av många olika typer, bland annat sidor, resurser och publikationer. Om författaren så önskar kan du hoppa över förhandsgranskning av innehåll.

![Diagram över författare, utgivare och avsändare](assets/author-publish.jpg)

Mer information om den tekniska arkitekturen för AEM as a Cloud Service finns i dokumentet [En introduktion till arkitekturen i Adobe Experience Manager as a Cloud Service.](/help/overview/architecture.md)

{{edge-delivery-authoring}}

## Skapa innehåll {#author-environment}

Redigeringsmiljön i redigeringsskiktet ger ett lättanvänt grafiskt användargränssnitt för att skapa innehåll. Det kräver att författaren loggar in med ett konto som tilldelats rätt åtkomstbehörighet.

Beroende på hur din instans och dina personliga åtkomsträttigheter är konfigurerade kan du utföra många åtgärder på ditt innehåll, bland annat:

* Generera nytt innehåll eller redigera befintligt innehåll på en sida
* Använda fördefinierade mallar för att skapa innehållssidor
* Skapa, redigera och hantera dina resurser och samlingar
* Flytta, kopiera och ta bort innehållssidor och resurser.
* Publicera (eller avpublicera) sidor och resurser.

Det finns även administrativa uppgifter som hjälper dig att hantera ditt innehåll:

* Arbetsflöden som styr hur ändringar hanteras, t.ex. framtvingar en granskning före publicering
* Projekt som koordinerar enskilda uppgifter

AEM administreras också från författarmiljön.

Se dokumentet [Quick Start Guide to Authoring](/help/sites-cloud/authoring/quick-start.md) för en översikt över redigeringsprocessen.

## Förhandsgranska innehåll {#previewing-content}

AEM erbjuder också en förhandsgranskningstjänst som gör att utvecklare och innehållsförfattare kan förhandsgranska en webbplats slutliga upplevelse innan den når publiceringsmiljön och är tillgänglig för allmänheten.

Se dokumentet [Förhandsgranska innehåll](/help/sites-cloud/authoring/sites-console/previewing-content.md) för mer information.

## Publiceringsmiljö {#publish-environment}

När det är klart publiceras webbplatsens innehåll i publiceringsmiljön på publiceringsnivån. Här blir webbplatsens sidor tillgängliga för den avsedda publiken i enlighet med innehållsmallens utseende och känsla.

Se dokumentet [Publicera sidor](/help/sites-cloud/authoring/sites-console/publishing-pages.md) för mer information om publicering och avpublicering av sidor.

## Dispatcher {#dispatcher}

Om du vill optimera prestanda för besökare på webbplatsen kan du **[Dispatcher](/help/implementing/dispatcher/overview.md)** implementerar belastningsutjämning och cachelagring för både publicerings- och förhandsgranskningsnivåer.

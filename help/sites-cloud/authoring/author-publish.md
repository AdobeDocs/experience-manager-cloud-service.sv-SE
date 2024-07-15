---
title: Skapande och publicering av begrepp
description: Lär dig mer om redigering i AEM, med hjälp av redigerings-, förhandsgransknings- och publiceringsmiljöer.
exl-id: ee9e4952-e075-4398-b31f-d7886153efff
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 0%

---


# Skapande och publicering av begrepp {#authoring-publishing}

En AEM as a Cloud Service-installation kan ses som tre primära lager på den mest grundläggande nivån

* Författarnivå
* Förhandsgranskningsnivå
* Publish Tier

Dessa nivåer interagerar så att ni kan göra innehåll tillgängligt på er webbplats så att era besökare kan komma åt det. Det grundläggande arbetsflödet är:

1. Innehållsförfattare skapar sitt innehåll med hjälp av författarnivån.
1. Innehållsförfattare gör sitt innehåll tillgängligt för granskare att förhandsgranska med förhandsgranskningsnivån.
1. När innehållet är klart för allmänheten publicerar författarna innehållet med publiceringsnivån.

Innehåll kan vara av många olika typer, bland annat sidor, resurser och publikationer. Om författaren så önskar kan du hoppa över förhandsgranskning av innehåll.

![Diagram över författare, utgivare och avsändare](assets/author-publish.jpg)

Mer information om AEM as a Cloud Service tekniska arkitektur finns i dokumentet [En introduktion till Adobe Experience Manager as a Cloud Service arkitektur.](/help/overview/architecture.md)

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

I dokumentet [Snabbstartsguide till redigering](/help/sites-cloud/authoring/quick-start.md) finns en översikt över redigeringsprocessen.

## Förhandsgranska innehåll {#previewing-content}

AEM erbjuder också en förhandsgranskningstjänst som gör att utvecklare och innehållsförfattare kan förhandsgranska en webbplats slutliga upplevelse innan den når publiceringsmiljön och är tillgänglig för allmänheten.

Mer information finns i dokumentet [Förhandsgranska innehåll](/help/sites-cloud/authoring/sites-console/previewing-content.md).

## Publish Environment {#publish-environment}

När det är klart publiceras webbplatsens innehåll i publiceringsmiljön på publiceringsnivån. Här blir webbplatsens sidor tillgängliga för den avsedda publiken i enlighet med innehållsmallens utseende och känsla.

Mer information om publicering och avpublicering av sidor finns i dokumentet [Publicera sidor](/help/sites-cloud/authoring/sites-console/publishing-pages.md).

## Dispatcher {#dispatcher}

**[Dispatcher](/help/implementing/dispatcher/overview.md)** implementerar belastningsutjämning och cachning för både publicerings- och förhandsgranskningsnivåer för att optimera prestanda för besökare på din webbplats.

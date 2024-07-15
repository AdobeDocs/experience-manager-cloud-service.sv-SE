---
title: Authoring Concepts
description: Lär dig mer om redigering i AEM, med hjälp av redigerings-, förhandsgransknings- och publiceringsmiljöer.
exl-id: ee9e4952-e075-4398-b31f-d7886153efff
source-git-commit: 0ad9f349c997c35862e4f571b4741ed4c0c947e2
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 0%

---


# Authoring Concepts {#authoring-concepts}

En AEM består vanligtvis av minst två miljöer:

* Författare
* Publish

Dessa miljöer interagerar så att ni kan göra innehållet tillgängligt på er webbplats så att besökarna kan komma åt det.

I redigeringsmiljön finns mekanismer för att skapa, uppdatera och granska innehållet innan det publiceras:

* En författare skapar och granskar innehållet. Innehåll kan vara av många olika typer, bland annat sidor, resurser och publikationer.
* Det här innehållet kommer vid något tillfälle att publiceras på din webbplats.

![Diagram över författare, utgivare och avsändare](/help/sites-cloud/authoring/assets/author-publish.png)

I redigeringsmiljön är AEM funktionalitet tillgänglig genom AEM redigeringsgränssnitt. I publiceringsmiljön utformar du hela det gränssnitt som är tillgängligt för användarna.

{{edge-delivery-authoring}}

## Författarmiljö {#author-environment}

Författaren arbetar i det som kallas **författarmiljön**. I den här miljön finns ett användarvänligt gränssnitt (grafiskt användargränssnitt (GUI eller UI)) för att skapa innehållet. Det kräver att författaren loggar in med ett konto som tilldelats rätt åtkomstbehörighet.

>[!NOTE]
>
>Ditt konto behöver rätt behörighet för att skapa, redigera och publicera innehåll.

Beroende på hur din instans och dina personliga åtkomsträttigheter är konfigurerade kan du utföra många åtgärder på ditt innehåll, bland annat:

* Generera nytt innehåll eller redigera befintligt innehåll på en sida
* Använda fördefinierade mallar för att skapa innehållssidor
* Skapa, redigera och hantera dina resurser och samlingar
* Flytta, kopiera och ta bort innehållssidor och resurser.
* Publicera (eller avpublicera) sidor och resurser.

Det finns även administrativa uppgifter som hjälper dig att hantera ditt innehåll:

* Arbetsflöden som styr hur ändringar hanteras, t.ex. framtvingar en granskning före publicering
* Projekt som koordinerar enskilda uppgifter

>[!NOTE]
>
>AEM administreras också från författarmiljön.

## Förhandsgranska innehåll {#previewing-content}

AEM erbjuder även en förhandsvisningstjänst för webbplatser som gör att utvecklare och innehållsförfattare kan förhandsgranska webbplatsens slutliga upplevelse innan den når publiceringsmiljön och är tillgänglig för allmänheten.

Mer information finns i [Förhandsgranska innehåll](/help/sites-cloud/authoring/fundamentals/previewing-content.md).

## Publish Environment {#publish-environment}

När det är klart publiceras webbplatsens innehåll i **publiceringsmiljön**. Här blir webbplatsens sidor tillgängliga för den avsedda publiken i enlighet med det gränssnitt som har utformats.

Mer information om att publicera och avpublicera sidor finns i dokumentet [Publicera sidor](/help/sites-cloud/authoring/fundamentals/publishing-pages.md).

## Dispatcher {#dispatcher}

**[Dispatcher](/help/implementing/dispatcher/overview.md)** implementerar belastningsutjämning och cachning för att optimera prestanda för besökare på din webbplats.

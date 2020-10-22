---
title: Redigeringsbegrepp
description: Begrepp att skapa i AEM
translation-type: tm+mt
source-git-commit: 92434d0dc29ac5fe1b395a2d34c8e48e2fdb7c97
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 1%

---


# Redigeringsbegrepp {#authoring-concepts}

En AEM består vanligtvis av minst två miljöer:

* Författare
* Publicera

Dessa interagerar så att ni kan göra innehåll tillgängligt på er webbplats så att besökarna kan komma åt det.

I redigeringsmiljön finns mekanismer för att skapa, uppdatera och granska innehållet innan det publiceras:

* En författare skapar och granskar innehållet. Innehåll kan vara av många olika typer, t.ex. sidor, resurser, publikationer m.m.
* Det här innehållet kommer vid något tillfälle att publiceras på din webbplats.

![Diagram över författare, utgivare och avsändare](/help/sites-cloud/authoring/assets/author-publish.png)

I redigeringsmiljön är AEM funktionalitet tillgänglig via AEM. För publiceringsmiljön utformar du hela det gränssnitt som är tillgängligt för användarna.

## Författarmiljö {#author-environment}

Författaren arbetar i det som kallas **författarmiljö**. Detta ger ett användarvänligt gränssnitt (grafiskt användargränssnitt (GUI eller UI)) för att skapa innehållet. Det kräver att författaren loggar in med ett konto som har tilldelats rätt åtkomstbehörighet.

>[!NOTE]
>
>Ditt konto behöver rätt behörighet för att skapa, redigera eller publicera innehåll.

Beroende på hur din instans och dina personliga åtkomsträttigheter är konfigurerade kan du utföra många åtgärder på ditt innehåll, bland annat:

* Generera nytt innehåll eller redigera befintligt innehåll på en sida
* Använda fördefinierade mallar för att skapa nya innehållssidor
* Skapa, redigera och hantera dina resurser och samlingar
* Flytta, kopiera och ta bort innehållssidor, resurser osv.
* Publicera (eller ta bort publicering) sidor, resurser osv.

Det finns dessutom administrativa uppgifter som hjälper dig att hantera ditt innehåll:

* Arbetsflöden som styr hur ändringar hanteras, t.ex. framtvingar en granskning före publicering
* Projekt som koordinerar enskilda uppgifter

>[!NOTE]
>
>AEM administreras också från författarmiljön.

## Publiceringsmiljö {#publish-environment}

När det är klart publiceras webbplatsens innehåll i **publiceringsmiljön**. Här blir webbplatsens sidor tillgängliga för den avsedda publiken i enlighet med det gränssnitt som har utformats.

Mer information om att publicera och avpublicera sidor finns i dokumentet [Publicera sidor.](/help/sites-cloud/authoring/fundamentals/publishing-pages.md)

## Dispatcher {#dispatcher}

För att optimera prestanda för besökare på webbplatsen **[implementerar dispatchern](/help/implementing/dispatcher/overview.md)** belastningsfördelning och cachning.

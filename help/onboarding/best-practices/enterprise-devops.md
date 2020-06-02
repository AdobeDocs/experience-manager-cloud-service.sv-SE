---
title: Enterprise DevOps
description: Läs om de processer, metoder och den kommunikation som krävs för att underlätta driftsättningen och samarbetet.
translation-type: tm+mt
source-git-commit: 5fe4eb9f9cad4ad2f1d259ebb5fa0302ea5c515f
workflow-type: tm+mt
source-wordcount: '1001'
ht-degree: 0%

---


# Enterprise DevOps{#enterprise-devops}

DevOps omfattar de processer, metoder och den kommunikation som krävs för att

* Underlätta driftsättningen av programvaran i olika miljöer.
* Förenkla samarbetet mellan utvecklings-, testnings- och driftsättningsteamen.

DevOps vill undvika problem som:

* Manuella fel.
* Glömda element; till exempel filer, konfigurationsinformation.
* Avvikelser. till exempel mellan en utvecklares lokala miljö och andra miljöer.

## Miljöer {#environments}

Adobe Experience Manager (AEM) som en molntjänst består vanligtvis av flera miljöer som används för olika syften på olika nivåer:

* [Utveckling](#development)
* [Kvalitetssäkring](#quality-assurance)
* [Mellanlagring](#staging)
* [Produktion](#production-author-and-publish)

>[!NOTE]
>
>Produktionsmiljön måste ha minst en författare och en publiceringsmiljö.
>
>Vi rekommenderar att alla andra miljöer även består av en författare och en publiceringsmiljö som speglar produktionsmiljön och möjliggör tidig testning.

### Utveckling {#development}

Utvecklarna ansvarar för att utveckla och anpassa det föreslagna projektet (oavsett om det är en webbplats, mobilappar, DAM-implementering osv.) med alla funktioner som krävs. De:

* utveckla och anpassa de nödvändiga delarna, till exempel mallar, komponenter, arbetsflöden, program
* förverkliga designen
* utveckla de tjänster och skript som krävs för att implementera de funktioner som krävs

Konfigurationen av [utvecklingsmiljön](/help/implementing/developing/introduction/development-guidelines.md) kan vara beroende av olika faktorer, men består vanligtvis av:

* Ett integrerat utvecklingssystem med versionskontroll som ger en integrerad kodbas. Detta används för att sammanfoga och konsolidera kod från de enskilda utvecklingsmiljöer som används av varje utvecklare.
* En personlig miljö för varje utvecklare, bor vanligtvis på sin lokala dator. Koden synkroniseras med versionskontrollsystemet vid lämpliga intervall

Beroende på hur stort ditt system är kan utvecklingsmiljön ha både författare och publiceringsinstanser.

### Kvalitetssäkring {#quality-assurance}

Den här miljön används av kvalitetssäkringsteamet för att på ett heltäckande sätt testa ditt nya system. både design och funktion. Den bör ha både utvecklings- och publiceringsmiljöer med lämpligt innehåll och tillhandahålla alla tjänster som behövs för att möjliggöra en komplett serie tester.

### Mellanlagring {#staging}

Mellanlagringsmiljön bör vara en spegling av produktionsmiljön - konfiguration, kod och innehåll:

* Den används för att testa de skript som används för att implementera den faktiska distributionen.
* Den kan användas för sluttester (design, funktionalitet och gränssnitt) innan den distribueras till produktionsmiljöerna.
* Även om det inte alltid är möjligt att ha samma staging-miljö som produktionsmiljön bör det vara så nära som möjligt att aktivera prestanda- och lasttestning.

### Produktion - Skapa och publicera {#production-author-and-publish}

Produktionsmiljön består av de miljöer som behövs för att [skapa och publicera](/help/sites-cloud/authoring/getting-started/concepts.md) implementeringen.

En produktionsmiljö består av minst en författarinstans och en publiceringsinstans:

* En [redigeringsinstans](#author) för indata av innehåll.
* En [publiceringsinstans](#publish) för innehåll som är tillgängligt för besökare/användare.

Beroende på projektets omfattning består den ofta av flera författare och/eller publiceringsinstanser. På en lägre nivå kan databasen även grupperas i flera instanser.

#### Författare {#author}

Författarinstanser ligger vanligtvis bakom den interna brandväggen. I den här miljön kommer du, och dina kollegor, att utföra redigeringsuppgifter som:

* administrera hela systemet
* infoga ditt innehåll
* konfigurera layout och design för ditt innehåll
* aktivera ditt innehåll i publiceringsmiljön

Innehåll som aktiverades paketeras och placeras i redigeringsmiljöns replikeringskö. Replikeringsprocessen överför sedan innehållet till publiceringsmiljön.

För att återreplikera data som genererats i en publiceringsmiljö tillbaka till redigeringsmiljön kommer en replikeringslyssnare i redigeringsmiljön att undersöka publiceringsmiljön och hämta sådant innehåll från publiceringsmiljöns utkorg för omvänd replikering.

#### Publicera {#publish}

En publiceringsmiljö finns vanligtvis i DMZ (Demilitarized Zone). Det är i den här miljön som besökare kommer att få tillgång till ditt innehåll (t.ex. via en webbplats eller i form av en mobilapp) och interagera med det. vara offentligt, eller i intranätet. En publiceringsmiljö:

* innehåller innehåll som replikerats från redigeringsmiljön
* gör det innehållet tillgängligt för besökarna
* lagrar användardata som genererats av besökarna, t.ex. kommentarer eller andra inskickade formulär
* kan konfigureras för att lägga till sådana användardata i en utkorg, för återreplikering tillbaka till författarmiljön

I publiceringsmiljön genereras ditt innehåll dynamiskt i realtid och innehållet kan anpassas för varje enskild användare.

## Kodförflyttning {#code-movement}

Kod ska alltid spridas nedifrån och upp:

* koden utvecklas först lokalt och sedan i integrerade utvecklingsmiljöer
* följt av grundlig testning av QA-miljön
* testas sedan på nytt i testmiljöer
* endast bör koden distribueras till produktionsmiljöerna

Koden (t.ex. anpassade webbprogramfunktioner och designmallar) överförs vanligtvis genom att paket exporteras och importeras mellan olika innehållsdatabaser. Om det behövs kan den här replikeringen konfigureras som en automatisk process.

AEM som ett Cloud Service-projekt utlöser ofta koddistribution:

* Automatiskt: för överföring till utvecklings- och QA-miljöer.
* Manuellt: driftsättning till stagnings- och produktionsmiljöerna sker på ett mer kontrollerat sätt, ofta manuellt, automatisering är dock möjlig vid behov.

![Kodförflyttning](assets/code-movement.png)

## Innehållsförflyttning {#content-movement}

Innehåll som skapas för produktion ska **alltid** redigeras på författarinstansen.

Innehåll bör inte följa kod från lägre miljöer till högre, eftersom det inte är bra att låta skribenter skapa innehåll på lokala datorer eller lägre miljöer, och att sedan flytta innehållet till produktionsmiljön är en god vana och troligen orsaka fel och inkonsekvenser.

Produktionsinnehållet bör flyttas från produktionsmiljön till testmiljön för att säkerställa att testmiljön är effektiv och korrekt.

>[!NOTE]
>
>Detta innebär inte att mellanlagringsinnehåll måste synkroniseras kontinuerligt med produktionen, att regelbundna uppdateringar är tillräckliga, men framför allt innan en ny kodupprepning testas. Innehåll i kvalitetssäkring och utvecklingsmiljöer behöver inte uppdateras lika ofta, utan bara vara en bra representation av produktionsinnehållet.

Innehåll kan överföras:

* Mellan olika miljöer - genom att exportera och importera paket.
* Mellan olika instanser - genom direkt replikering (AEM som molntjänstreplikering) av innehållet (med HTTP- eller HTTPS-anslutning).

![Innehållsförflyttning](assets/content-movement.png)
---
title: Enterprise DevOps
description: Läs om de processer, metoder och den kommunikation som krävs för att underlätta driftsättningen och samarbetet.
exl-id: c8da1fd7-fe3e-4c7b-8fe7-1f7faf02769c
source-git-commit: 1a4c5e618adaef99d82a00e1118d1a0f8536fc14
workflow-type: tm+mt
source-wordcount: '1009'
ht-degree: 46%

---

# Enterprise DevOps{#enterprise-devops}

DevOps omfattar processer, metoder och kommunikation som krävs för att

* Underlätta driftsättningen av programvaran i olika miljöer.
* Förenkla samarbetet mellan utvecklings-, testnings- och driftsättningsteamen.

DevOps vill undvika problem som:

* Manuella fel.
* Glömda element: till exempel filer och konfigurationsinformation.
* Avvikelser: till exempel mellan en utvecklares lokala miljö och andra miljöer.

## Miljö {#environments}

Adobe Experience Manager (AEM) as a Cloud Service består vanligtvis av flera miljöer som används för olika syften på olika nivåer:

* [Utveckling](#development)
* [Kvalitetssäkring](#quality-assurance)
* [Mellanlagring](#staging)
* [Produktion](#production-author-and-publish)

>[!NOTE]
>
>Produktionsmiljön måste ha minst en författar- och en publiceringsmiljö.
>
>Vi rekommenderar att alla andra miljöer också består av en författar- och en publiceringsmiljö som speglar produktionsmiljön och möjliggör tidig testning.

### Utveckling {#development}

Utvecklarna ansvarar för att utveckla och anpassa det föreslagna projektet (oavsett om det är en webbplats, mobilappar, DAM-implementering och så vidare) med alla funktioner som krävs. De ska:

* utveckla och anpassa de nödvändiga delarna, till exempel mallar, komponenter, arbetsflöden och program
* förverkliga designen
* utveckla nödvändiga tjänster och skript så att ni kan implementera de funktioner som krävs

Konfigurationen av [utveckling](/help/implementing/developing/introduction/development-guidelines.md) miljön kan vara beroende av olika faktorer, men vanligtvis består den av:

* Ett integrerat utvecklingssystem med versionskontroll som ger en integrerad kodbas. Den här integrerade kodbasen används för att sammanfoga kod från de enskilda utvecklingsmiljöer som används av varje utvecklare.
* En personlig miljö för varje utvecklare, vilken vanligtvis finns på hens lokala dator. Koden synkroniseras med versionskontrollsystemet med lämpliga intervall

Beroende på hur omfattande ditt system är kan utvecklingsmiljön ha både författar- och publiceringsinstanser.

### Kvalitetssäkring {#quality-assurance}

Den här miljön används av kvalitetssäkringsteamet för att på ett heltäckande sätt testa ditt nya system – både design och funktion. Den bör ha både författar- och publiceringsmiljöer med lämpligt innehåll och tillhandahålla alla tjänster som behövs för att möjliggöra en komplett serie tester.

### Mellanlagring {#staging}

Mellanlagringsmiljön bör vara en spegling av produktionsmiljön - konfiguration, kod och innehåll:

* Den används för att testa de skript som används för att implementera den faktiska driftsättningen.
* Den kan användas för sluttester (design, funktionalitet och gränssnitt) innan den distribueras till produktionsmiljöerna.
* Även om det inte alltid är möjligt att ha samma mellanlagringsmiljö som produktionsmiljön bör den vara så lik som möjligt för att möjliggöra prestanda- och lasttestning.

### Produktion - Skapa och publicera {#production-author-and-publish}

Produktionsmiljön består av miljöer som [skapa och publicera](/help/sites-cloud/authoring/author-publish.md) implementeringen.

En produktionsmiljö består av minst en författarinstans och en publiceringsinstans:

* En [författarinstans](#author) för inmatning av innehåll.
* En [publiceringsinstans](#publish) för innehåll som är tillgängligt för besökare/användare.

Beroende på projektets omfattning består den ofta av flera författare, utgivare eller både och. På en lägre nivå kan databasen även grupperas i flera instanser.

#### Författare {#author}

Vanligtvis ligger författarinstanser bakom den interna brandväggen. Den interna brandväggen är den miljö där du, och dina kollegor, utför redigeringsuppgifter som följande:

* administrera hela systemet
* mata in innehåll
* konfigurera layout och design för innehållet
* aktivera innehållet i Publish-miljön

Innehåll som aktiverats paketeras och placeras i författarmiljöns replikeringskö. Replikeringsprocessen överför sedan innehållet till publiceringsmiljön.

Om du vill återreplikera data som genererats i en publiceringsmiljö till författarmiljön avsöker en replikeringslyssnare i redigeringsmiljön publiceringsmiljön och hämtar sådant innehåll från publiceringsmiljöns utkorg för omvänd replikering.

#### Publicera {#publish}

Normalt finns en publiceringsmiljö i DMZ (Demilitarized Zone). I den här miljön får besökarna tillgång till ditt innehåll (t.ex. via en webbplats eller i form av ett mobilprogram) och kan interagera med det, oavsett om det är offentligt eller i intranätet. En publiceringsmiljö:

* innehåller innehåll som replikerats från författarmiljön
* gör innehållet tillgängligt för besökare
* lagrar användardata som genererats av besökarna, t.ex. kommentarer eller andra inskickade formulär
* kan konfigureras för att lägga till sådana användardata i en utkorg, för återreplikering tillbaka till författarmiljön

I publiceringsmiljön genereras ditt innehåll dynamiskt i realtid och innehållet kan anpassas för varje enskild användare.

## Kodförflyttning {#code-movement}

Sprid alltid kod nedifrån och upp:

* koden utvecklas först lokalt och sedan i integrerade utvecklingsmiljöer
* följt av grundlig testning av QA-miljöer
* testas sedan på nytt i mellanlagringsmiljöer
* endast därefter får koden driftsättas till produktionsmiljöerna

Vanligtvis överförs koden (till exempel anpassade webbprogramfunktioner och designmallar) genom att paket exporteras och importeras mellan olika innehållsdatabaser. Om det behövs kan den här replikeringen konfigureras som en automatisk process.

Projekt på AEM as a Cloud Service utlöser ofta koddistribution:

* Automatiskt: för överföring till utvecklings- och QA-miljöer.
* Manuellt: distributioner till staging- och produktionsmiljöerna görs på ett mer kontrollerat sätt, ofta manuellt, men det går att automatisera vid behov.

![Kodförflyttning](assets/code-movement.png)

## Innehållsförflyttning {#content-movement}

Innehåll som skapas för produktion ska **alltid** författas inom författarinstansen.

Innehåll bör inte följa kod som flyttas från lägre miljöer till högre. Det är alltså inte bra att låta skribenter skapa innehåll på lokala datorer eller i lägre miljöer och sedan flytta det till produktionsmiljön. Orsaken är att den kan orsaka fel och inkonsekvenser.

Produktionsinnehållet bör flyttas från produktionsmiljön till mellanlagringsmiljön för att säkerställa att mellanlagringsmiljön är effektiv och korrekt.

>[!NOTE]
>
>Den här metoden innebär inte att mellanlagringsinnehållet måste synkroniseras kontinuerligt med produktionen. Det räcker med regelbundna uppdateringar, men framför allt innan du testar en ny kodupprepning. Innehåll i QA- och utvecklingsmiljöer behöver inte uppdateras lika ofta. Det måste bara vara en bra representation av produktionsinnehållet.

Innehåll kan överföras:

* Mellan olika miljöer – genom exporter och importer av paket.
* Mellan olika instanser - genom direkt replikering (AEM as a Cloud Service replikering) av innehållet (med en HTTP- eller HTTPS-anslutning).

![Innehållsförflyttning](assets/content-movement.png)

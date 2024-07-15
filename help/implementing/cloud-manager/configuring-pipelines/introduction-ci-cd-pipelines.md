---
title: CI/CD-rör
description: Lär dig mer om Cloud Manager pipelines för CI/CD och hur de kan användas för att driftsätta koden effektivt.
index: true
exl-id: 40d6778f-65e0-4612-bbe3-ece02905709b
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '1418'
ht-degree: 0%

---


# Cloud Manager CI/CD Pipelines {#intro-cicd}

Lär dig mer om Cloud Manager pipelines för CI/CD och hur de kan användas för att driftsätta koden effektivt.

## Introduktion {#introduction}

En CI/CD-pipeline i Cloud Manager är ett sätt att skapa kod från en källdatabas och distribuera den till en miljö. En pipeline kan utlösas av en händelse, till exempel en pull-begäran från en källkodsdatabas (d.v.s. en kodändring), eller enligt ett regelbundet schema för att matcha en releasecedence.

Om du vill konfigurera en pipeline måste du:

* Definiera utlösaren som ska starta pipelinen.
* Definiera parametrarna som styr produktionsdistributionen.
* Konfigurera prestandatestparametrarna.

Cloud Manager har två typer av rörledningar:

* [Produktionsförlopp](#prod-pipeline)
* [Icke-produktionsförlopp](#non-prod-pipeline)

![Olika typer av pipelines](/help/implementing/cloud-manager/assets/configure-pipeline/ci-cd-config1.png)

## Produktionsförlopp {#prod-pipeline}

En produktionspipeline är en konstruerad pipeline som innehåller en serie samordnade steg för att distribuera källkod för produktionsanvändning. Stegen är att först bygga, paketera, testa, validera och driftsätta i alla miljöer. Därför kan en produktionspipeline bara läggas till när en uppsättning produktions- och stagningsmiljöer har skapats.

>[!TIP]
>
>Mer information finns i [Konfigurera en produktionspipeline](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md).

## Icke-produktionsförlopp {#non-prod-pipeline}

En icke-produktionspipeline används främst för att köra kodkvalitetssökningar eller för att distribuera källkod till en utvecklingsmiljö.

>[!TIP]
>
>Mer information finns i [Konfigurera en icke-produktionspipeline](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md).

## Kodkällor {#code-sources}

Förutom produktion och icke-produktion kan rörledningar differentieras efter vilken typ av kod de använder.

* **[Kompletta stackförgreningar](#full-stack-pipeline)** - Distribuera kodsbyggen bakåt- och framifrån som innehåller en eller flera AEM serverprogram tillsammans med HTTPD/Dispatcher-konfigurationer samtidigt
* **[Konfigurera pipelines](#config-deployment-pipeline)** - Konfigurera och distribuera trafikfilterregler, inklusive WAF-regler, inom några minuter
* **[Front-End Pipelines](#front-end)** - Distribuera front-end-kodsbyggen som innehåller ett eller flera gränssnittsprogram på klientsidan
* **[Konfigurationsrör för webbnivå](#web-tier-config-pipelines)** - Distribuerar HTTPD/Dispatcher-konfigurationer

Dessa beskrivs senare i detalj i det här dokumentet.

### Förstå CI-CD-pipeline i Cloud Manager {#understand-pipelines}

I följande tabell sammanfattas de rörledningar som är tillgängliga i Cloud Manager och deras användning.

| Typ av pipeline | Driftsättnings- eller kodkvalitet | Source Code | Syfte | Anteckningar |
|--- |--- |--- |---|---|
| Produktion eller icke-produktion | Distribution | Fullhög | Distribuerar samtidigt kodbyggen för baksidan och framsidan tillsammans med HTTPD/Dispatcher-konfigurationer | När slutkoden måste distribueras samtidigt med AEM serverkod.<br>När pipelines för frontendpipelines eller webbnivåkonfigurationer ännu inte har använts. |
| Produktion eller icke-produktion | Distribution | Front-End | Distribuerar frontkodbygge som innehåller ett eller flera gränssnittsprogram på klientsidan | Stöder flera samtidiga pipelines<br>mycket snabbare än fullstacksdistributioner |
| Produktion eller icke-produktion | Distribution | Webbnivåkonfiguration | Distribuerar HTTPD/Dispatcher-konfigurationer | Distribuerar på några minuter |
| Produktion eller icke-produktion | Distribution | Konfig | Distribuerar trafikfiltreringsregler | Distribuerar på några minuter |
| Icke-produktion | Kodkvalitet | Fullhög | Kör kodkvalitetsgenomsökningar på kod i full stack utan distribution | Stöd för flera rörledningar |
| Icke-produktion | Kodkvalitet | Front-End | Kör kodkvalitetsgenomsökningar på slutkod utan distribution | Stöd för flera rörledningar |
| Icke-produktion | Kodkvalitet | Webbnivåkonfiguration | Kör kodkvalitetsgenomsökningar på dispatcherkonfigurationer utan distribution | Stöd för flera rörledningar |
| Icke-produktion | Kodkvalitet | Konfig | Distribuerar trafikfiltreringsregler |  |

I följande diagram visas Cloud Manager pipeline-konfigurationer med traditionella, enskilda front-end-databaser eller oberoende front-end-databaskonfigurationer.

![Cloud Manager pipeline-konfigurationer](/help/implementing/cloud-manager/assets/configure-pipeline/cm-setup.png)

## Pipelines i fullhög {#full-stack-pipeline}

I rörledningar i fullhög distribueras back-end-kod, front-end-kod och webbskiktskonfigurationer till AEM runtime-modulen samtidigt.

* Back-End-kod - oföränderligt innehåll som Java-kod, OSGi-konfigurationer, återanvisning och ändringsbart innehåll
* Front-End-kod - användargränssnittsresurser som JavaScript, CSS, teckensnitt
* Webbnivåkonfiguration - HTTPD/Dispatcher-konfigurationer

Pipelinen i full hög representerar en rörledning som gör allt på en gång, samtidigt som användarna får möjlighet att exklusivt distribuera sin slutkod eller Dispatcher-konfigurationer via pipeline i frontend-led respektive webbskiktskonfigurationen.

Framåtslutningskod för paket (JavaScript/CSS) i full stapel som [AEM klientbibliotek](/help/implementing/developing/introduction/clientlibs.md).

I pipelines med fullständig stapel kan webbnivåkonfigurationer distribueras om en [pipeline för webbnivåkonfiguration](#web-tier-config-pipelines) inte har konfigurerats.

Följande begränsningar gäller.

* En användare måste vara inloggad med rollen **Distributionshanterare** för att kunna konfigurera eller köra pipelines.
* Det kan bara finnas en pipeline i full hög per miljö.

Observera dessutom hur pipelinen för hela stacken fungerar om du väljer att introducera en [konfigurationspipeline för webbskikt.](#web-tier-config-pipelines)

* Om det finns en motsvarande konfigurationspipeline för webbskiktet ignoreras Dispatcher-konfigurationen i en fullständigt stackpipeline för en miljö.
* Om motsvarande konfigurationsflöde för webbskiktet för miljön inte finns kan användaren konfigurera pipelinen för helhög som innehåller eller ignorerar Dispatcher-konfigurationen.

Fullspaltig rörledning kan vara pipelines med kodkvalitet eller driftsättning.

### Konfigurera rörledningar i helhög {#configure-full-stack}

Om du vill veta mer om hur du konfigurerar rörledningar i full hög läser du i följande dokument:

* [Lägga till en produktionspipeline](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#full-stack-code)
* [Lägga till en icke-produktionspipeline](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#full-stack-code)

## Konfigurera rörledningar {#config-deployment-pipeline}

Med ett konfigurationsflöde kan du konfigurera och distribuera trafikfilterregler, inklusive WAF-regler, inom några minuter.

Se [Trafikfilterregler inklusive WAF-regler](/help/security/traffic-filter-rules-including-waf.md) om du vill veta mer om hur du hanterar konfigurationerna i din databas så att de distribueras på rätt sätt.

### Konfigurera konfigurationsförlopp {#configure-config-deployment}

Mer information om hur du konfigurerar pipelines finns i följande dokument:

* [Lägga till en produktionspipeline](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#targeted-deployment)
* [Lägga till en icke-produktionspipeline](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#targeted-deployment)

## Front-End Pipelines {#front-end}

Front-end-kod är kod som används som statiska filer. Den är skild från gränssnittskod som hanteras av AEM och kan innehålla webbplatsteman, kunddefinierade SPA, SPA och andra lösningar.

Med rörledningar kan era team effektivisera design- och utvecklingsprocessen genom att möjliggöra snabbare driftsättning av frontkodasynkron backend-utveckling. Detta dedikerade tillvägagångssätt distribuerar JavaScript och CSS till AEM distributionslager som ett tema, vilket resulterar i en ny temaversion som kan refereras från sidor som levereras av AEM.

>[!NOTE]
>
>En användare med rollen **Distributionshanteraren** kan skapa och köra flera frontendpipelines samtidigt.
>
>Det finns dock en högsta gräns på 300 rörledningar per program (för alla typer).

Frontrörledningar kan vara pipelines med kodkvalitet eller distributionsrörledningar.

### Innan du konfigurerar frontmatriser {#before-start}

Innan du konfigurerar rörledningar för frontend bör du gå igenom [AEM snabbregistreringsresan](/help/journey-sites/quick-site/overview.md) för att få en komplett guide med hjälp av det lättanvända AEM snabbplatsverktyget. Den här resan hjälper er att effektivisera utvecklingen på frontend och göra det möjligt att snabbt anpassa webbplatsen utan kunskaper om AEM.

### Konfigurera en frontpipeline {#configure-front-end}

Om du vill veta mer om hur du konfigurerar rörledningar för frontservrar kan du läsa följande:

* [Lägga till en produktionspipeline](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#adding-production-pipeline)
* [Lägga till en icke-produktionspipeline](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#adding-non-production-pipeline)

### Developing Sites with the Front-End Pipeline {#developing-with-front-end-pipeline}

Med rörledningar kan utvecklarna bli mer självständiga och utvecklingsprocessen kan accelereras.

Se [Utveckla platser med frontdelspipeline](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md) för hur den här processen fungerar tillsammans med vissa överväganden som du bör vara medveten om för att få ut mesta möjliga av processen.

## Konfigurationsrör för webbnivå {#web-tier-config-pipelines}

Med konfigurationspipelines på webbnivå kan du exklusiv distribution av HTTPD/Dispatcher-konfiguration till AEM genom att koppla loss den från andra kodändringar. Det är en smidig pipeline som ger användare som bara vill distribuera ändringar i dispatcherkonfigurationen, ett accelererat sätt att göra det på bara några minuter.

>[!TIP]
>
>Med konfigurationspipelinjer för webbnivå kan du välja mellan att lagra webbkonfigurationen på samma källplats som för hela stackpipelinen eller på en annan plats, beroende på vilken struktur som passar ditt projekt bäst.

Följande begränsningar gäller.

* Du måste vara i AEM version `2021.12.6151.20211217T120950Z` eller senare för att kunna använda konfigurationspipelines på webbnivå.
* Du måste [anmäla dig till det flexibla läget för dispatcherverktygen](/help/implementing/dispatcher/disp-overview.md#validation-debug) om du vill använda konfigurationspipelines på webbnivå.
* En användare måste vara inloggad med rollen **Distributionshanterare** för att kunna konfigurera eller köra pipelines.
* Det kan bara finnas en konfigurationspipeline för webbskikt per miljö.
* Användaren kan inte konfigurera en konfigurationspipeline för ett webbskikt när motsvarande pipeline för en hel hög körs.
* Webbnivåstrukturen måste följa strukturen för det flexibla läget, enligt definitionen i dokumentet [Dispatcher i molnet](/help/implementing/dispatcher/disp-overview.md#validation-debug).

Tänk dessutom på hur den [fullständiga stackpipelinen](#full-stack-pipeline) fungerar när du introducerar en webbskiktspipeline.

* Om en konfigurationspipeline för ett webbskikt inte har konfigurerats för en miljö, kan användaren göra ett val när han/hon konfigurerar sin motsvarande pipeline för hela stacken för att inkludera eller ignorera Dispatcher-konfigurationen under körning och distribution.
* När en konfigurationspipeline för ett webbskikt har konfigurerats för en miljö, ignorerar dess motsvarande pipeline för hela stacken (om det finns en sådan) dispatcherkonfigurationen under körning och distribution.
* När en konfigurationspipeline för ett webbskikt har tagits bort återställs dess motsvarande pipeline för hela stacken för att distribuera Dispatcher-konfigurationer under körningen.

Rörledningar för webbnivåkonfiguration kan vara av typen kodkvalitet eller distribution.

### Konfigurerar webbnivåpipeline {#configure-web-tier}

Mer information om hur du konfigurerar rörledningar på webbnivå finns i följande dokument:

* [Lägga till en produktionspipeline](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#targeted-deployment)
* [Lägga till en icke-produktionspipeline](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#targeted-deployment)

## Videoöversikt över pipeline-typer {#video}

I den här korta videon får du en snabb översikt över pipelinetyper.

>[!VIDEO](https://video.tv.adobe.com/v/342363)

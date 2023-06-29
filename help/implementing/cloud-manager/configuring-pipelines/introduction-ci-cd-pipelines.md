---
title: CI/CD-rör
description: Lär dig mer om Cloud Managers pipelines för CI/CD och hur de kan användas för att driftsätta koden på ett effektivt sätt.
index: true
exl-id: 40d6778f-65e0-4612-bbe3-ece02905709b
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '1339'
ht-degree: 0%

---


# Cloud Manager CI/CD Pipelines {#intro-cicd}

Lär dig mer om Cloud Managers pipelines för CI/CD och hur de kan användas för att driftsätta koden på ett effektivt sätt.

## Introduktion {#introduction}

En CI/CD-pipeline i Cloud Manager är en mekanism som bygger kod från en källdatabas och distribuerar den till en miljö. En pipeline kan utlösas av en händelse, till exempel en pull-begäran från en källkodsdatabas (d.v.s. en kodändring), eller enligt ett regelbundet schema för att matcha en releasecedence.

Om du vill konfigurera en pipeline måste du:

* Definiera utlösaren som ska starta pipelinen.
* Definiera parametrarna som styr produktionsdistributionen.
* Konfigurera prestandatestparametrarna.

Det finns två typer av pipelines i Cloud Manager:

* [Produktionsförlopp](#prod-pipeline)
* [Icke-produktionsförlopp](#non-prod-pipeline)

![Typer av rörledningar](/help/implementing/cloud-manager/assets/configure-pipeline/ci-cd-config1.png)

## Videoöversikt {#video}

I den här korta videon får du en snabb översikt över pipelinetyper.

>[!VIDEO](https://video.tv.adobe.com/v/342363)

## Produktionsförlopp {#prod-pipeline}

En produktionspipeline är en konstruerad pipeline som innehåller en serie samordnade steg för att distribuera källkod för produktionsanvändning. Stegen är att först bygga, paketera, testa, validera och driftsätta i alla miljöer. Därför kan en produktionspipeline bara läggas till när en uppsättning produktions- och stagningsmiljöer har skapats.

>[!TIP]
>
>Se [Konfigurera en produktionspipeline](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) för mer information.

## Icke-produktionsförlopp {#non-prod-pipeline}

En icke-produktionspipeline används främst för att köra kodkvalitetssökningar eller för att distribuera källkod till en utvecklingsmiljö.

>[!TIP]
>
>Se [Konfigurera en icke-produktionspipeline](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md) för mer information.

## Kodkällor {#code-sources}

Förutom produktion och icke-produktion kan rörledningar differentieras efter vilken typ av kod de använder.

* **[Kompletta stackrör](#full-stack-pipeline)** - Driftsätt samtidigt kodbyggen i bakände och framände som innehåller en eller flera AEM serverprogram tillsammans med HTTPD/Dispatcher-konfigurationer
* **[Front-End Pipelines](#front-end)** - Distribuera kodsbyggen som innehåller ett eller flera gränssnittsprogram på klientsidan
* **[Konfigurationsrör för webbnivå](#web-tier-config-pipelines)** - Distribuerar konfigurationer för HTTPD/Dispatcher

Dessa beskrivs senare i detalj i det här dokumentet.

### Förstå CI-CD-pipeline i Cloud Manager {#understand-pipelines}

I följande tabell sammanfattas alla rörledningar som är tillgängliga i Cloud Manager och deras användning.

| Typ av pipeline | Driftsättnings- eller kodkvalitet | Källkod | Syfte | Anteckningar |
|--- |--- |--- |---|---|
| Produktion eller icke-produktion | Distribution | Full-Stack | Distribuerar samtidigt kodbyggen i bakände och framände tillsammans med konfigurationer för HTTPD/Dispatcher | När slutkoden måste distribueras samtidigt med AEM serverkod.<br>När rörledningar i frontendsystemet eller konfigurationsledningar i webbskiktet ännu inte har antagits. |
| Produktion eller icke-produktion | Distribution | Front-End | Distribuerar frontkodbygge som innehåller ett eller flera gränssnittsprogram på klientsidan | Stöd för flera samtidiga rörledningar<br>Mycket snabbare än driftsättningar i fullstacksformat |
| Produktion eller icke-produktion | Distribution | Webbnivåkonfiguration | Distribuerar konfigurationer för HTTPD/Dispatcher | Distribuerar på några minuter |
| Icke-produktion | Kodkvalitet | Full-Stack | Kör kodkvalitetsgenomsökningar på kod i full stack utan distribution | Stöd för flera rörledningar |
| Icke-produktion | Kodkvalitet | Front-End | Kör kodkvalitetsgenomsökningar på slutkod utan distribution | Stöd för flera rörledningar |
| Icke-produktion | Kodkvalitet | Webbnivåkonfiguration | Kör kodkvalitetsgenomsökningar på dispatcherkonfigurationer utan distribution | Stöd för flera rörledningar |

I följande diagram visas Cloud Managers pipeline-konfigurationer med traditionella, enskilda databaser eller oberoende databasinställningar för front-end.

![pipelinekonfigurationer för Cloud Manager](/help/implementing/cloud-manager/assets/configure-pipeline/cm-setup.png)

## Pipelines i fullhög {#full-stack-pipeline}

I rörledningar i fullhög distribueras back-end-kod, front-end-kod och webbskiktskonfigurationer till AEM runtime-modulen samtidigt.

* Back-End-kod - oföränderligt innehåll som Java-kod, OSGi-konfigurationer, återanvisning och ändringsbart innehåll
* Front-End-kod - programgränssnittsresurser som JavaScript, CSS, teckensnitt
* Webbnivåkonfiguration - HTTPD/Dispatcher-konfigurationer

Pipelinen i full hög representerar en rörledning som gör allt på en gång, samtidigt som användarna får möjlighet att exklusivt distribuera sin frontkodkonfiguration eller Dispatcher-konfigurationer via frontendpipelines respektive webbskiktskonfigurationspipelines.

Kompletta rörledningar paketerar slutkod (JavaScript/CSS) som [AEM klientbibliotek](/help/implementing/developing/introduction/clientlibs.md).

I rörledningar med hel hög kan webbnivåkonfigurationer distribueras om en [pipeline för konfiguration av webbnivå](#web-tier-config-pipelines) har inte konfigurerats.

Följande begränsningar gäller.

* En användare måste vara inloggad med **Distributionshanteraren** roll för att konfigurera eller köra rörledningar.
* Det kan bara finnas en pipeline i full hög per miljö.

Du bör dessutom vara medveten om hur rörledningen i en hel hög fungerar om du väljer att introducera en [konfigurationsflöde för webbnivå.](#web-tier-config-pipelines)

* I en helgrupps-pipeline för en miljö ignoreras Dispatcher-konfigurationen om motsvarande konfigurationsflöde för webbnivån finns.
* Om motsvarande konfigurationsflöde för webbskiktet för miljön inte finns kan användaren konfigurera pipelinen för hela stacken som innehåller eller ignorerar Dispatcher-konfigurationen.

Fullspaltig rörledning kan vara pipelines med kodkvalitet eller driftsättning.

## Front-End Pipelines {#front-end}

Front-end-kod är kod som används som statiska filer. Den är skild från gränssnittskod som hanteras av AEM och kan innehålla webbplatsteman, kunddefinierade SPA, SPA och andra lösningar.

Med rörledningar kan era team effektivisera design- och utvecklingsprocessen genom att möjliggöra snabbare driftsättning av frontkodasynkron backend-utveckling. Detta dedikerade tillvägagångssätt distribuerar JavaScript och CSS till AEM distributionslager som ett tema, vilket resulterar i en ny temaversion som kan refereras från sidor som levereras av AEM.

>[!IMPORTANT]
>
>Du måste ha AEM version `2021.10.5933.20211012T154732Z ` eller senare när AEM Sites är aktiverat för att använda rörledningar för frontservrar.

>[!NOTE]
>
>En användare med **Distributionshanteraren** kan skapa och köra flera rörledningar samtidigt.
>
>Det finns dock en högsta gräns på 300 rörledningar per program (för alla typer).

Frontrörledningar kan vara pipelines med kodkvalitet eller distributionsrörledningar.

### Innan du konfigurerar frontmatriser {#before-start}

Läs mer i [AEM för att skapa webbplatser snabbt](/help/journey-sites/quick-site/overview.md) för att få en komplett guide genom det lättanvända AEM för att skapa webbplatser. Den här resan hjälper er att effektivisera utvecklingen på frontend och göra det möjligt att snabbt anpassa webbplatsen utan kunskaper om AEM.

### Konfigurera en frontpipeline {#configure-front-end}

Om du vill veta mer om hur du konfigurerar rörledningar för frontservrar kan du läsa följande:

* [Lägga till en produktionspipeline](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#adding-production-pipeline)
* [Lägga till en icke-produktionspipeline](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#adding-non-production-pipeline)

### Developing Sites with the Front-End Pipeline {#developing-with-front-end-pipeline}

Med rörledningar kan utvecklarna bli mer självständiga och utvecklingsprocessen kan accelereras.

Se [Developing Sites with the Front-End Pipeline](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md) om hur den här processen fungerar tillsammans med vissa överväganden för att vara medveten om att utnyttja hela potentialen i den här processen.

### Konfigurera rörledningar i helhög {#configure-full-stack}

Om du vill veta mer om hur du konfigurerar rörledningar i full hög läser du i följande dokument:

* [Lägga till en produktionspipeline](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#adding-production-pipeline)
* [Lägga till en icke-produktionspipeline](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#adding-non-production-pipeline)


## Konfigurationsrör för webbnivå {#web-tier-config-pipelines}

Med konfigurationspipelines på webbnivå kan du exklusiv distribution av HTTPD/Dispatcher-konfiguration till AEM genom att koppla loss den från andra kodändringar. Det är en smidig pipeline som ger användare som bara vill distribuera ändringar i dispatcherkonfigurationen, ett accelererat sätt att göra det på bara några minuter.

>[!TIP]
>
>Med konfigurationspipelinjer för webbnivå kan du välja mellan att lagra webbkonfigurationen på samma källplats som för hela stackpipelinen eller på en annan plats, beroende på vilken struktur som passar ditt projekt bäst.

Följande begränsningar gäller.

* Du måste ha AEM version `2021.12.6151.20211217T120950Z` eller nyare för att använda konfigurationströrningar på webbnivå.
* Du måste [välja det flexibla läget för dispatcherverktygen](/help/implementing/dispatcher/disp-overview.md#validation-debug) om du vill använda konfigurationströrningar på webbnivå.
* En användare måste vara inloggad med **Distributionshanteraren** roll för att konfigurera eller köra rörledningar.
* Det kan bara finnas en konfigurationspipeline för webbskikt per miljö.
* Användaren kan inte konfigurera en konfigurationspipeline för ett webbskikt när motsvarande pipeline för en hel hög körs.
* Webbnivåstrukturen måste följa strukturen för det flexibla läget, enligt definitionen i dokumentet [Dispatcher i molnet](/help/implementing/dispatcher/disp-overview.md#validation-debug).

Var dessutom medveten om hur [fullständigt stackflöde](#full-stack-pipeline) fungerar när du introducerar ett webbskiktsflöde.

* Om en konfigurationspipeline för ett webbskikt inte har konfigurerats för en miljö, kan användaren göra ett val när han/hon konfigurerar sin motsvarande pipeline för hela stacken för att inkludera eller ignorera Dispatcher-konfigurationen under körning och distribution.
* När en konfigurationspipeline för ett webbskikt har konfigurerats för en miljö, ignorerar dess motsvarande pipeline för hela stacken (om det finns en sådan) dispatcherkonfigurationen under körning och distribution.
* När en konfigurationspipeline för ett webbskikt har tagits bort återställs dess motsvarande pipeline för hela stacken för att distribuera Dispatcher-konfigurationer under körningen.

Rörledningar för webbnivåkonfiguration kan vara av typen kodkvalitet eller distribution.

### Konfigurera konfigurationsförlopp för webbnivå {#configure-web-tier-config-pipelines}

Mer information om hur du konfigurerar pipelines för webbnivåkonfiguration finns i följande dokument:

* [Lägga till en produktionspipeline](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#adding-production-pipeline)
* [Lägga till en icke-produktionspipeline](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#adding-non-production-pipeline)

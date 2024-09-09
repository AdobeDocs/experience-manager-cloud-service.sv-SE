---
title: CI/CD-rör
description: Lär dig mer om Cloud Manager pipelines för CI/CD och hur de kan användas för att distribuera koden effektivt.
index: true
exl-id: 40d6778f-65e0-4612-bbe3-ece02905709b
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 5d6d3374f2dd95728b2d3ed0cf6fab4092f73568
workflow-type: tm+mt
source-wordcount: '1482'
ht-degree: 0%

---


# Cloud Manager CI/CD Pipelines {#intro-cicd}

Lär dig mer om Cloud Manager pipelines för CI/CD (Continuous Integration/Continuous Delivery) och hur de kan användas för att distribuera koden effektivt.

## Introduktion {#introduction}

En CI/CD-pipeline i Cloud Manager är ett sätt att skapa kod från en källdatabas och distribuera den till en miljö. En händelse utlöser en pipeline, till exempel en pull-begäran från en källkodsdatabas som Git (d.v.s. en kodändring). Den kan också aktiveras enligt ett regelbundet schema för att matcha en release-cadence.

Så här konfigurerar du en pipeline:

* Definiera utlösaren som startar pipelinen.
* Definiera parametrarna som styr produktionsdistributionen.
* Konfigurera prestandatestparametrarna.

Cloud Manager har två typer av rörledningar:

* [Produktionspipelinjer](#prod-pipeline)
* [Icke-produktionsrörledningar](#non-prod-pipeline)

![Olika typer av pipelines](/help/implementing/cloud-manager/assets/configure-pipeline/ci-cd-config1.png)

## Produktionspipelinjer {#prod-pipeline}

En produktionspipeline är en konstruerad pipeline som innehåller en serie samordnade steg för att distribuera källkod för produktionsanvändning. Stegen är att först bygga, paketera, testa, validera och driftsätta i alla miljöer. Därför kan en produktionspipeline bara läggas till när en uppsättning produktions- och stagningsmiljöer har skapats.

>[!TIP]
>
>Se [Konfigurera en produktionspipeline](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md).

## Icke-produktionsrörledningar {#non-prod-pipeline}

En icke-produktionspipeline används främst för att köra kodkvalitetssökningar eller för att distribuera källkod till en utvecklingsmiljö.

>[!TIP]
>
>Se [Konfigurera en icke-produktionspipeline](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md).

## Kodkällor {#code-sources}

Rörledningar kan också skilja sig åt beroende på vilken typ av kod de distribuerar, förutom i produktions- och icke-produktionsmiljöer.

* **[Fullspaltig rörledning](#full-stack-pipeline)** - Distribuera samtidigt kodbyggen i bakände och i framände som innehåller ett eller flera AEM serverprogram tillsammans med HTTPD/Dispatcher-konfigurationer.
* **[Konfigurera pipelines](#config-deployment-pipeline)** - Du kan snabbt distribuera konfigurationer för funktioner som vidarebefordran av loggar och tömningsrelaterade underhållsaktiviteter. Det innehåller även olika CDN-konfigurationer (Content Delivery Network), till exempel trafikfilterregler, inklusive WAF-regler (Web Application Firewall). Dessutom kan du hantera begäran- och svarsomvandlingar, ursprungsväljare, klientomdirigeringar, felsidor, CDN-nycklar, rensnings-API-nycklar och grundläggande autentisering. Mer information finns i [Använd konfigurationspipelines](/help/operations/config-pipeline.md).
* **[Framtidspipelines](#front-end)** - Distribuera frontkodsbyggen som innehåller ett eller flera klientprogram.
* **[Dirigeringspipelines för webbskiktskonfiguration](#web-tier-config-pipelines)** - Distribuerar HTTPD/Dispatcher-konfigurationer.

Dessa pipelinetyper beskrivs närmare i det här dokumentet senare.

### Förstå pipelines för CI-CD i Cloud Manager {#understand-pipelines}

I följande tabell sammanfattas de rörledningar som är tillgängliga i Cloud Manager och deras användning.

| Typ av pipeline | Driftsättnings- eller kodkvalitet | Source code | Syfte | Anteckningar |
| --- | --- | --- | --- | ---|
| Produktion eller icke-produktion | Distribution | Fullhög | Distribuerar samtidigt kodbyggen för baksidan och framsidan tillsammans med HTTPD/Dispatcher-konfigurationer | Används när serverkod måste distribueras samtidigt med AEM kod. Används när rörledningar i frontendänden eller konfigurationsledningar i webbskiktet ännu inte har antagits. |
| Produktion eller icke-produktion | Distribution | Front-end | Distribuerar frontkodbygge som innehåller ett eller flera gränssnittsprogram på klientsidan | Stöder flera samtidiga frontendledningar<br>mycket snabbare än fullstacksdistributioner. |
| Produktion eller icke-produktion | Distribution | Webbnivåkonfiguration | Distribuerar HTTPD/Dispatcher-konfigurationer | Distribuerar på några minuter |
| Produktion eller icke-produktion | Distribution | Konfig | Distribuerar [konfiguration för ett antal funktioner ](/help/operations/config-pipeline.md) som är relaterade till CDN, vidarebefordring av loggar och tömningsunderhåll | Distribuerar på några minuter |
| Icke-produktion | Kodkvalitet | Hel hög | Kör kodkvalitetsgenomsökningar på kod i full stack utan distribution | Stöd för flera rörledningar |
| Icke-produktion | Kodkvalitet | Front-end | Kör kodkvalitetsgenomsökningar på slutkod utan distribution | Stöd för flera rörledningar |
| Icke-produktion | Kodkvalitet | Webbnivåkonfiguration | Kör kodkvalitetsgenomsökningar på Dispatcher-konfigurationer utan distribution | Stöd för flera rörledningar |

I följande diagram visas Cloud Manager pipeline-konfigurationer med traditionella, enskilda front-end-databaser eller oberoende front-end-databaskonfigurationer.

![Cloud Manager pipeline-konfigurationer](/help/implementing/cloud-manager/assets/configure-pipeline/cm-setup.png)

## Rörledningar i fullhög {#full-stack-pipeline}

I rörledningar i fullhög distribueras back-end-kod, front-end-kod och webbskiktskonfigurationer till AEM samtidigt.

* Back-End-kod - oföränderligt innehåll som Java-kod, OSGi-konfigurationer, återanvisning och ändringsbart innehåll
* Front-End-kod - användargränssnittsresurser som JavaScript, CSS, teckensnitt
* Webbnivåkonfiguration - HTTPD/Dispatcher-konfigurationer

Pipelinen i full hög representerar en rörledning i &#39;uber&#39;. Den hanterar allt samtidigt, samtidigt som användarna kan driftsätta sin klientkod eller Dispatcher-konfigurationer separat. Distributionen sker via pipeline i frontend-läge respektive via konfigurationspipelines på webbnivå.

Framåtslutningskod för paket (JavaScript/CSS) i full stapel som [AEM klientbibliotek](/help/implementing/developing/introduction/clientlibs.md).

I pipelines med fullständig stapel kan webbnivåkonfigurationer distribueras om en [pipeline för webbnivåkonfiguration](#web-tier-config-pipelines) inte har konfigurerats.

Följande begränsningar gäller.

* En användare måste vara inloggad med rollen **Distributionshanterare** för att kunna konfigurera eller köra pipelines.
* Det kan bara finnas en pipeline i full hög per miljö.

Tänk dessutom på hur pipelinen i en hel hög fungerar om du väljer att introducera en [konfigurationspipeline för webbskikt](#web-tier-config-pipelines).

* I helstacksflödet för en miljö ignoreras Dispatcher-konfigurationen om motsvarande konfigurationsflöde för webbnivån finns.
* Om motsvarande konfigurationsflöde för webbskiktet för miljön inte finns kan användaren konfigurera pipelinen för helhög som innehåller eller ignorerar Dispatcher-konfigurationen.

Fullspaltig rörledning kan vara pipelines med kodkvalitet eller driftsättning.

### Konfigurera rörledningar i full hög {#configure-full-stack}

Se [Lägga till en produktionspipeline](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#full-stack-code).
Se [Lägg till en icke-produktionspipeline](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#full-stack-code).

## Konfigurera rörledningar {#config-deployment-pipeline}

Med hjälp av ett konfigurationsflöde kan du snabbt distribuera inställningar för vidarebefordran av loggfiler, rensningsrelaterade underhållsåtgärder och olika CDN-konfigurationer, inklusive trafikfilterregler (som WAF-regler (Web Application Firewall)). Dessutom kan du hantera begäran- och svarsomvandlingar, ursprungsväljare, klientomdirigeringar, felsidor, kundhanterade CDN-nycklar, rensnings-API-nycklar och grundläggande autentisering.

Se [Använd konfigurationspipelines](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) för en utförlig lista över funktioner som stöds och för att lära dig hur du hanterar konfigurationerna i din databas så att de distribueras på rätt sätt.

### Konfigurera konfigurationsförlopp {#configure-config-deployment}

Se [Lägga till en produktionspipeline](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#targeted-deployment).
Se [Lägg till en icke-produktionspipeline](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#targeted-deployment).

## Förloppsledningar {#front-end}

Front-end-kod är kod som används som statiska filer. Den är skild från gränssnittskod som hanteras av AEM och kan innehålla webbplatsteman, kunddefinierade SPA, SPA och andra lösningar.

Med rörledningar kan era team effektivisera design- och utvecklingsprocessen genom att möjliggöra snabbare driftsättning av frontkodslayout, asynkron backend-utveckling. Detta dedikerade tillvägagångssätt distribuerar JavaScript och CSS till AEM distributionslager som ett tema, vilket resulterar i en ny temaversion, som kan refereras från sidor som levereras av AEM.

>[!NOTE]
>
>En användare med rollen **Distributionshanteraren** kan skapa och köra flera frontendpipelines samtidigt.
>
>Det finns dock en högsta gräns på 300 rörledningar per program (för alla typer).

Frontrörledningar kan vara pipelines med kodkvalitet eller distributionsrörledningar.

### Innan du konfigurerar frontendpipelines {#before-start}

Innan du konfigurerar rörledningar för frontend bör du gå igenom [AEM snabbregistreringsresan](/help/journey-sites/quick-site/overview.md) för att få en komplett guide med hjälp av det lättanvända AEM snabbplatsverktyget. Med den här resan kan du effektivisera utvecklingen på frontend och snabbt anpassa webbplatsen utan kunskaper om AEM.

### Konfigurera en frontendpipeline {#configure-front-end}

Se [Lägga till en produktionspipeline](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#adding-production-pipeline).
Se [Lägg till en icke-produktionspipeline](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#adding-non-production-pipeline).

### Utveckla webbplatser med den integrerade pipeline som behövs {#developing-with-front-end-pipeline}

Med rörledningar kan utvecklarna bli mer självständiga och utvecklingsprocessen kan accelereras.

Se [Utveckla webbplatser med frontendpipeline](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md) för hur den här processen fungerar tillsammans med en del överväganden som du bör vara medveten om för att få ut mesta möjliga av den här processen.

## Konfigurationspipelines på webbnivå {#web-tier-config-pipelines}

Med konfigurationspipelines på webbnivå kan du exklusiv distribution av HTTPD/Dispatcher-konfiguration till AEM, vilket frigör den från andra kodändringar. Det är en smidig pipeline som ger användare som bara vill driftsätta konfigurationsändringar från Dispatcher, ett snabbare sätt att göra det på bara några minuter.

>[!TIP]
>
>Med konfigurationspipelines på webbnivå kan du lagra webbkonfigurationen på samma eller en annan källplats som den fullständiga stackpipeline, beroende på vad som passar din projektstruktur bäst.

Följande begränsningar gäller.

* Var på AEM version `2021.12.6151.20211217T120950Z` eller senare för att använda konfigurationspipelines på webbnivå.
* [Anmäl dig till det flexibla läget för Dispatcher-verktygen](/help/implementing/dispatcher/disp-overview.md#validation-debug) om du vill använda konfigurationspipelines på webbnivå.
* En användare måste vara inloggad med rollen **Distributionshanterare** för att kunna konfigurera eller köra pipelines.
* Det kan bara finnas en konfigurationspipeline för webbskikt per miljö.
* Användaren kan inte konfigurera en konfigurationspipeline för ett webbskikt när motsvarande pipeline för en hel hög körs.
* Webbnivåstrukturen måste följa strukturen för det flexibla läget, enligt definitionen i dokumentet [Dispatcher i molnet](/help/implementing/dispatcher/disp-overview.md#validation-debug).

Tänk dessutom på hur den [fullständiga stackpipelinen](#full-stack-pipeline) fungerar när du introducerar en webbskiktspipeline.

* Om en konfigurationspipeline för ett webbskikt inte är inställd för en miljö kan användaren välja att ta med eller ignorera Dispatcher-konfigurationen när pipeline för hela stacken konfigureras. Det här valet görs under körning och distribution.
* När en konfigurationspipeline för ett webbskikt har konfigurerats för en miljö, ignorerar dess motsvarande pipeline för hela stacken (om det finns en sådan) Dispatcher-konfigurationen under körning och distribution.
* När en konfigurationspipeline för ett webbskikt har tagits bort återställs dess motsvarande pipeline för hela stacken för att distribuera Dispatcher-konfigurationer under körningen.

Rörledningar för webbnivåkonfiguration kan vara av typen `Code quality` eller `Deployment`.

### Konfigurera rörledningar för webbnivå {#configure-web-tier}

Se [Lägga till en produktionspipeline](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#targeted-deployment).
Se [Lägg till en icke-produktionspipeline](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#targeted-deployment).

## Videoöversikt över pipeline-typer {#video}

Om du vill få en snabb översikt över olika pipeline-typer kan du titta på följande video (2 minuter, 26 sekunder).

>[!VIDEO](https://video.tv.adobe.com/v/342363)

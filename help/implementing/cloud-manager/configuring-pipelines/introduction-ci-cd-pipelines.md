---
title: CI-CD-rör
description: Följ den här sidan för att lära dig mer om Cloud Manager CI-CD-förgreningar
index: false
source-git-commit: 71e4a9932ef89ebf263ebbc0300bf2c938fa50f5
workflow-type: tm+mt
source-wordcount: '935'
ht-degree: 0%

---


# Cloud Manager CI-CD-pipeline {#intro-cicd}

## Introduktion {#introduction}

En CI/CD-pipeline i Cloud Manager kan utlösas av någon typ av händelse, till exempel en pull-begäran från en källkodsdatabas, d.v.s. en kodändring eller någon typ av regelbundet schema som matchar en releasedatans.

>[!NOTE]
>Om du vill konfigurera din pipeline måste du:
>* definiera den utlösare som ska starta pipelinen
>* definiera parametrarna som styr produktionsdistributionen
>* konfigurera parametrar för prestandatestning


I Cloud Manager finns det två typer av pipelines:

* [Produktionspipeline](#prod-pipeline)
* [Icke-produktionsförlopp](#non-prod-pipeline)

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/ci-cd-config.png)


## Produktionspipeline {#prod-pipeline}

En produktionspipeline är en konstruerad pipeline som innehåller en serie samordnade steg för att ta källkod hela vägen in i produktionen. Stegen omfattar att först bygga, paketera, testa, validera och distribuera till alla scenmiljöer. Det behöver väl inte sägas att en produktionspipeline bara kan läggas till när en produktions- och scenmiljöuppsättning skapas.

Se [Konfigurera en produktionspipeline](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) för mer information.


## Icke-produktionsförlopp {#non-prod-pipeline}

En icke-produktionspipeline syftar till att köra kodkvalitetssökningar eller att distribuera källkod i en utvecklingsmiljö.

Se [Konfigurera en icke-produktionspipeline](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md) för mer information.

## Förstå CI-CD-pipeline i Cloud Manager {#understand-pipelines}

I följande tabell sammanfattas alla pipelines i Cloud Manager tillsammans med deras användning.

| Typ av pipeline | Driftsättnings- eller kodkvalitet | Källkod | När ska användas | När eller varför ska jag använda? |
|--- |--- |--- |---|---|---|
| Produktion eller icke-produktion | Distribution | Front End | Snabba driftsättningstider.<br>Flera frontledningar kan konfigureras och köras samtidigt per miljö.<br>Front End-pipeline-bygget spolar ut ur bygget till ett lagringsutrymme. När en HTML-sida hanteras kan den referera till statiska Frontend Code-filer som hanteras av CDN med detta lagringsutrymme som ursprung. | För exklusiv driftsättning av klientslutkod som innehåller ett eller flera användargränssnittsprogram. Front end-kod är kod som används som statisk fil. Den är skild från den gränssnittskod som AEM använder. Här ingår webbplatsteman, kunddefinierade SPA, Firefoly SPA och andra lösningar.<br>Måste vara i AEM version `2021.10.5933.20211012T154732Z` |
| Produktion eller icke-produktion | Distribution | Hel hög | När frontledningarna ännu inte har anammats.<br>I de fall där Front End-koden måste distribueras exakt samtidigt som AEM Server-koden. | Distribuera AEM Server-kod (oföränderligt innehåll, Java-kod, OSGi-konfigurationer, HTTPD/dispatcher-konfiguration, återanvisning, ändringsbart innehåll, teckensnitt) som innehåller ett eller flera AEM serverprogram samtidigt. |
| Icke-produktion | Kodkvalitet | Front End | För att Cloud Manager ska kunna utvärdera din programutveckling och kodkvalitet utan att behöva göra någon distribution.<br>Flera rörledningar kan konfigureras och köras. | Kör kodkvalitetsgenomsökningar på slutkoden. |
| Icke-produktion | Kodkvalitet | Hel hög | För att Cloud Manager ska kunna utvärdera din programutveckling och kodkvalitet utan att behöva göra någon distribution.<br>Flera rörledningar kan konfigureras och köras. | Kör kodkvalitetssökning på den fullständiga stackkoden. |

I följande diagram visas molnhanterarens pipeline-konfigurationer med traditionella, enskilda front end-databaser eller oberoende front end-databaskonfigurationer:

![](/help/implementing/cloud-manager/assets/configure-pipeline/cm-setup.png)

## Front End Pipelines för Cloud Manager {#front-end}

Front End-pipelines hjälper era team att effektivisera design- och utvecklingsprocessen genom att aktivera snabbredigerade front end-pipelines för implementering av front end-kod. Denna differentierade pipeline distribuerar JavaScript och CSS till AEM distributionslager som ett tema, vilket resulterar i en ny temaversion som kan refereras från sidor som levereras från AEM. Front end-kod är kod som används som statisk fil. Den är skild från den gränssnittskod som AEM använder. Här ingår webbplatsteman, kunddefinierade SPA, Firefoly SPA och andra lösningar.

>[!NOTE]
>En användare som är inloggad som rollen Distributionshanterare kan skapa och köra flera frontendpipelines samtidigt. Det finns dock en högsta gräns på 300 rörledningar per program (för alla typer).

Dessa kan vara av typen frontslutskodens kvalitet eller frontslutets distributionsrör.

### Innan du konfigurerar frontmatriser {#before-start}

Innan du börjar konfigurera frontend-pipelines ska du läsa AEM Quick Site Creation Journey för ett komplett arbetsflöde med det lättanvända AEM Quick Site Creation-verktyget. På den här dokumentationswebbplatsen kan du effektivisera utvecklingen av AEM och snabbt anpassa webbplatsen utan AEM kunskaper om bakomliggande funktioner.

### Konfigurera en frontpipeline {#configure-front-end}

Mer information om hur du konfigurerar frontendpipeline finns i:

* [Lägga till en produktionspipeline](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#adding-production-pipeline)
* [Lägga till en icke-produktionspipeline](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#adding-non-production-pipeline)

## Kompletta stackrör {#full-stack-pipeline}

Med en fullständig stackpipeline kan användaren välja att distribuera back-end-, front-end- och HTTPD/dispatcher-konfiguration samtidigt.  Den distribuerar kod och innehåll till AEM, inklusive klientkod (JavaScript/CSS) som paketerats som AEM klientbibliotek. Den kan distribuera webbnivåkonfiguration om en webbnivåpipeline inte har konfigurerats. Detta representerar rörledningen&quot;uber&quot;, samtidigt som användarna får möjlighet att exklusivt distribuera sin Front End-kod eller dispatcherkonfiguration via Front End-pipeline respektive Web Tier Config-pipeline.

Följande begränsningar gäller:

1. En användare måste vara inloggad som Deployment Manager för att kunna konfigurera eller köra pipelines.

1. Det kan bara finnas en fullständig stackpipeline per miljö.

1. Användaren kan konfigurera pipelinen Full stack för en miljö så att den ignorerar eller inte ignorerar dispatcherkonfigurationen, om motsvarande pipeline för Web Tier Config för miljön inte finns.

1. Komplett stapel-pipeline för en miljö ignorerar dispatcherkonfigurationen om motsvarande Web Tier Config-pipeline för miljön finns.

De kan vara av typen Full Stack - Kodkvalitet eller Full Stack - Deployment.

### Konfigurera en hel stackpipeline {#configure-full-stack}

Mer information om hur du konfigurerar en hel stackpipeline finns i:

* [Lägga till en produktionspipeline](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#adding-production-pipeline))
* [Lägga till en icke-produktionspipeline](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#adding-non-production-pipeline)
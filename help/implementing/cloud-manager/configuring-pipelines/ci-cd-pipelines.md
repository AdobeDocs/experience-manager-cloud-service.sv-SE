---
title: CI-CD-rör
description: CI-CD-rör
index: false
source-git-commit: e51b995aebb053f38cb99879be70e23447f543c0
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 0%

---


# Cloud Manager CI-CD-pipeline {#intro-cicd}

I Cloud Manager finns det två typer av pipeline:

* **Produktionspipeline**
* **Icke-produktionsförlopp**

## Produktionspipeline {#prod-pipeline}

En produktionspipeline är en konstruerad pipeline som innehåller en serie samordnade steg för att ta källkod hela vägen in i produktionen. Stegen omfattar att först bygga, paketera, testa, validera och distribuera till alla scenmiljöer. Det behöver väl inte sägas att en produktionspipeline bara kan läggas till när en produktions- och scenmiljöuppsättning skapas.

>[!NOTE]
>Mer information finns i Konfigurera produktionspipeline.


## Icke-produktionsförlopp {#non-prod-pipeline}

En icke-produktionspipeline syftar till att köra kodkvalitetssökningar eller att distribuera källkod i en utvecklingsmiljö.

>[!NOTE]
>Mer information finns i Icke-produktion och Endast kodkvalitet i pipeline.

Driftsättnings- och kodkvaliteten som stöds i produktions- och icke-produktionsflödet i Cloud Manager är indelad i två olika typer:

* Front End
* Hel hög

I följande tabell sammanfattas rörledningarna:


>[!NOTE]
>En CI/CD-pipeline i Cloud Manager utlöses av en händelse, till exempel en pull-begäran från en källkodsdatabas som det vill säga en kodändring, eller ett regelbundet schema som matchar en releasefedans.
>
>Om du vill konfigurera din pipeline måste du:
>* definiera den utlösare som ska starta pipelinen
>* definiera parametrarna som styr produktionsdistributionen
>* konfigurera parametrar för prestandatestning
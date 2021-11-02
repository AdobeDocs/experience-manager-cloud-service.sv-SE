---
title: CI-CD-rör
description: CI-CD-rör
index: false
source-git-commit: 1887cc7374ece840b2dcca4482924b14c4793567
workflow-type: tm+mt
source-wordcount: '185'
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


I Cloud Manager finns det två typer av pipeline:

* [Produktionspipeline](#prod-pipeline)
* [Icke-produktionsförlopp](#non-prod-pipeline)

## Produktionspipeline {#prod-pipeline}

En produktionspipeline är en konstruerad pipeline som innehåller en serie samordnade steg för att ta källkod hela vägen in i produktionen. Stegen omfattar att först bygga, paketera, testa, validera och distribuera till alla scenmiljöer. Det behöver väl inte sägas att en produktionspipeline bara kan läggas till när en produktions- och scenmiljöuppsättning skapas.

Mer information finns i Konfigurera produktionspipeline.


## Icke-produktionsförlopp {#non-prod-pipeline}

En icke-produktionspipeline syftar till att köra kodkvalitetssökningar eller att distribuera källkod i en utvecklingsmiljö.

Mer information finns i Icke-produktion och Endast kodkvalitet i pipeline.

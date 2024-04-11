---
title: Använda Edge Delivery Services med befintliga AEM
description: Lär dig utnyttja fördelarna med Edge Delivery Services i dina befintliga AEM projekt
feature: Edge Delivery Services
exl-id: f54aac3a-1d0c-4be0-9aa6-616217e0e458
source-git-commit: 11f721b4a617c99e30329d7196f42d7b48067f1b
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 0%

---


# Använda Edge Delivery Services med befintliga AEM {#existing-projects}

Du behöver inte vänta på ett nytt AEM projekt för att kunna dra nytta av Edge Delivery Services. Edge Delivery Services kan integreras i ditt befintliga AEM så att du kan utnyttja prestandavinster direkt.

## Begränsningar för AEM sidredigeraren {#page-editor}

Innan Edge Delivery Services skapades redigerades innehåll som hanterades i AEM med AEM Page Editor. Om ditt projekt började innan Edge Delivery Services introducerades är det nästan säkert att du använder sidredigeraren.

AEM sidredigeraren fungerar bara med [AEM](/help/implementing/developing/components/overview.md) som [Kärnkomponenter.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) De här komponenterna är inte kompatibla med Edge Delivery Services. På grund av detta krävs två faser för att införa Edge Delivery Services i ett befintligt AEM:

* [Phase 1 - Replace Front End](#replace-front-end)
* [Fas 2 - Byt till Universal Editor](#switch-ue)

## Phase 1 - Replace Front End {#replace-front-end}

I fas ett kan du fortsätta att använda din befintliga AEM platsstruktur, komponenter och redigeringsverktyg. Webbplatsåtergivningen byggs om med hjälp av block med JavaScript och CSS, och den levereras via Edge Delivery Services.

Se [Byggavsnitt](/help/edge/developer/block-collection.md) av dokumentationen till Edge Delivery Servicens för mer information om block och hur du utvecklar för Edge Delivery-tjänster.

En konverterare i App Builder krävs för att konvertera den AEM renderade HTML-utdata och skicka den till Edge Delivery Services.

![Innehållskonverteraren i publiceringsflödet](assets/content-converter.png)

Fas två slutför processen genom att eliminera den tekniska överlappningen: AEM kärnkomponenter med HTML och Java på AEM Author, JS-baserade block på Edge Delivery och en nodeJS-baserad konverterare.

## Fas 2 - Byt till Universal Editor {#switch-ue}

I den här fasen ersätts AEM Page Editor med Universal Editor. Eftersom den universella redigeraren kan arbeta direkt med block behövs inte längre AEM Core Components and converter.


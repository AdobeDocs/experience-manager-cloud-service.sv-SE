---
title: Publicera innehåll för Edge Delivery Services
description: Lär dig hur innehållspublicering fungerar med Edge Delivery Services och hur du publicerar AEM innehåll med Edge Delivery Services.
feature: Edge Delivery Services
exl-id: 32fbb144-9175-47a9-bb5a-ca15f3fcd2d8
source-git-commit: 58d85886ef04b548c09e3ef9308fe596dd3eda38
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---

# Publicera innehåll för Edge Delivery Services {#publishing-edge}

Med Edge Delivery Services är det smidigt att publicera innehåll oavsett innehållskälla:

* Dokumentbaserat innehåll - se [Publiceringsavsnitt](/help/edge/docs/authoring.md) av Edge Delivery Servicens dokumentation.
* AEM - Se informationen nedan.

## Publiceringsflöde från AEM {#publishing-flow}

När du använder den universella redigeraren för att skapa AEM innehåll är det bara att klicka på **Publicera** i Universal Editor. Se dokumentet [Publicera innehåll med den universella redigeraren.](/help/sites-cloud/authoring/universal-editor/publishing.md)

Informationsflödet vid publicering är följande. När författaren börjar publicera är det här ett automatiskt flöde som illustreras här i informationssyfte.

>[!NOTE]
>
>Upp till 5 000 sökvägar som publiceras från redigeringsgränssnittet eller arbetsflöden tillåts per dag. Integrationer som skapar arbetsbelastningar för masspublicering stöds inte.

![Informationsflödet vid publicering från AEM till Edge Delivery Services](assets/publishing-flow.png)

1. Innehållsförfattaren publicerar AEM i Universell redigerare.
1. En publiceringshändelse skickas till Adobe Pipeline-kön.
1. Edge Delivery Publish Service skickar relevanta händelser till Edge Delivery Admin API.
1. Edge Delivery pulls and ingests semantic HTML från AEM Author.
1. AEM uppdateras med publiceringsstatus.

## Så här kommer du igång {#how-to-get-started}

Kontakta din Adobe-representant för att få tillgång till den här funktionen.

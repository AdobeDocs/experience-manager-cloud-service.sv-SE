---
title: Publicera innehåll för Edge Delivery Services
description: Lär dig hur innehållspublicering fungerar med Edge Delivery Services och hur du publicerar AEM innehåll med Edge Delivery Services.
feature: Edge Delivery Services
exl-id: 32fbb144-9175-47a9-bb5a-ca15f3fcd2d8
source-git-commit: 3ee1ba83518c3d4fba59b0c98b31e5c63a2eb6ab
workflow-type: tm+mt
source-wordcount: '295'
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
1. En publiceringshändelse skickas till Adobe pipeline-kön.
1. Edge Delivery Servicens publiceringstjänst vidarebefordrar de relevanta händelserna till Edge Delivery Servicens admin-API.
1. Edge Delivery pulls and ingests semantic HTML från AEM författare.
1. AEM uppdateras med publiceringsstatus.

>[!NOTE]
>
>Som standard är Edge Delivery Servicens administratörs-API inte skyddat och kan användas för att publicera eller avpublicera dokument utan autentisering. För att konfigurera autentisering för admin-API:t enligt [Konfigurerar autentisering för författare](https://www.aem.live/docs/authentication-setup-authoring), måste projektet etableras med en API_KEY som ger åtkomst till publiceringstjänsten. [Kontakta Adobe-teamet på Slack](/help/edge/docs/slack.md) för vägledning.

## Så här kommer du igång {#how-to-get-started}

Kontakta din Adobe-representant för att få tillgång till den här funktionen.

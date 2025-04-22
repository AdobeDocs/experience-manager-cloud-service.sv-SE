---
title: Publicera innehåll för Edge Delivery Services
description: Lär dig hur innehållspublicering fungerar med Edge Delivery Services och hur du publicerar AEM-innehåll med Edge Delivery Services.
feature: Edge Delivery Services
exl-id: 32fbb144-9175-47a9-bb5a-ca15f3fcd2d8
role: User
index: false
hide: true
hidefromtoc: true
source-git-commit: 17c14a78c2cfa262e25c6196fa73c6c4b17e200a
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---


# Publicera innehåll för Edge Delivery Services {#publishing-edge}

Med Edge Delivery Services är det smidigt att publicera innehåll oavsett innehållskälla:

* Dokumentbaserat innehåll - se [avsnittet Publicera](/help/edge/docs/authoring.md) i Edge Delivery Services-dokumentationen.
* AEM content - Please see the details below.

## Publiceringsflöde från AEM {#publishing-flow}

När du använder den universella redigeraren för att skapa AEM-innehåll är publiceringen bara ett klick på knappen **Publicera** i den universella redigeraren. Se dokumentet [Publishing Content with the Universal Editor](/help/sites-cloud/authoring/universal-editor/publishing.md).

Informationsflödet vid publicering är följande. När författaren börjar publicera är det här ett automatiskt flöde som illustreras här i informationssyfte.

>[!NOTE]
>
>Upp till 5 000 sökvägar som publiceras från redigeringsgränssnittet eller arbetsflöden tillåts per dag. Integrationer som skapar arbetsbelastningar för masspublicering stöds inte. Om ditt projekt kräver högre kapacitet föreslår du det för [VIP-programmet](https://www.aem.live/vip/intake).

![Informationsflödet vid publicering från AEM till Edge Delivery Services](assets/publishing-flow.png)

1. Innehållsförfattaren publicerar AEM-innehåll i den universella redigeraren.
1. En publiceringshändelse skickas till Adobe pipeline-kö.
1. Edge Delivery Services publiceringstjänst vidarebefordrar de relevanta händelserna till Edge Delivery Services admin API.
1. Edge Delivery tar fram semantiska HTML från AEM författare.
1. AEM uppdateras med publiceringsstatus.

>[!NOTE]
>
>Som standard är Edge Delivery Services admin-API inte skyddat och kan användas för att publicera eller avpublicera dokument utan autentisering. Om du vill konfigurera autentisering för admin-API:t enligt [Konfigurera autentisering för författare](https://www.aem.live/docs/authentication-setup-authoring) måste projektet etableras med en API_KEY som ger åtkomst till publiceringstjänsten. [Kontakta Adobe-teamet på Slack](/help/edge/docs/slack.md) om du behöver hjälp.


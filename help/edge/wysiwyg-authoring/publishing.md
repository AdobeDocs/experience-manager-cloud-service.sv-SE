---
title: Publicera innehåll för Edge Delivery Services
description: Lär dig hur innehållspublicering fungerar med Edge Delivery Services och hur du publicerar AEM innehåll med Edge Delivery Services.
feature: Edge Delivery Services
exl-id: 32fbb144-9175-47a9-bb5a-ca15f3fcd2d8
role: User
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---


# Publicera innehåll för Edge Delivery Services {#publishing-edge}

Med Edge Delivery Services är det smidigt att publicera innehåll oavsett innehållskälla:

* Dokumentbaserat innehåll - se [Publish-avsnittet](/help/edge/docs/authoring.md) i dokumentationen för Edge Delivery Services.
* AEM - Se informationen nedan.

## Publiceringsflöde från AEM {#publishing-flow}

När du använder den universella redigeraren för att redigera AEM innehåll är publiceringen bara att klicka på knappen **Publish** i den universella redigeraren. Se dokumentet [Publishing Content with the Universal Editor](/help/sites-cloud/authoring/universal-editor/publishing.md).

Informationsflödet vid publicering är följande. När författaren börjar publicera är det här ett automatiskt flöde som illustreras här i informationssyfte.

>[!NOTE]
>
>Upp till 5 000 sökvägar som publiceras från redigeringsgränssnittet eller arbetsflöden tillåts per dag. Integrationer som skapar arbetsbelastningar för masspublicering stöds inte. Om ditt projekt kräver högre kapacitet föreslår du det för [VIP-programmet](https://www.aem.live/vip/intake).

![Informationsflödet vid publicering från AEM till Edge Delivery Services](assets/publishing-flow.png)

1. Innehållsförfattaren publicerar AEM i Universell redigerare.
1. En publiceringshändelse skickas till Adobe pipeline-kön.
1. Edge Delivery Servicens publiceringstjänst vidarebefordrar de relevanta händelserna till Edge Delivery Servicens admin-API.
1. Edge Delivery drar och importerar semantiskt HTML från AEM författare.
1. AEM uppdateras med publiceringsstatus.

>[!NOTE]
>
>Som standard är Edge Delivery Servicens administratörs-API inte skyddat och kan användas för att publicera eller avpublicera dokument utan autentisering. Om du vill konfigurera autentisering för admin-API:t enligt [Konfigurera autentisering för författare](https://www.aem.live/docs/authentication-setup-authoring) måste projektet etableras med en API_KEY som ger åtkomst till publiceringstjänsten. [Kontakta Adobe-teamet på Slack](/help/edge/docs/slack.md) om du vill ha hjälp.


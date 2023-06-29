---
title: Förhandsgranska innehåll
description: Lär dig hur du använder AEM förhandsvisningstjänst för att förhandsgranska innehåll innan du publicerar.
exl-id: 6b4b57f6-2e66-4c83-94d9-bc1e0daab0f3
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 0%

---


# Förhandsgranska innehåll {#previewing-content}

AEM erbjuder en tjänst för förhandsgranskning av webbplatser som gör att utvecklare och innehållsförfattare kan förhandsgranska webbplatsens slutresultat innan den når publiceringsmiljön och blir tillgänglig för allmänheten.

Det gör det lättare att förhandsgranska sidor som annars inte skulle vara synliga i redigeringsmiljön, som sidövergångar och annat innehåll på publiceringssidan.

Mer information om förhandsvisningsmiljöerna finns i [Hantera miljöer](/help/implementing/cloud-manager/manage-environments.md#access-preview-service).

## Publicera innehåll för förhandsgranskning {#publishing-content-to-preview}

Du kan publicera innehåll till förhandsgranskningstjänsten med **Hanterad publikation** Gränssnitt.

1. På webbplatskonsolen markerar du den eller de sidor du vill skicka för förhandsgranskning och klickar på **Hantera publikation** knapp
1. I följande guide väljer du **Förhandsgranska** som mål

   ![hanterad publikation](/help/sites-cloud/authoring/assets/previewmanagedpublication.png)

1. Klicka **Nästa** och sedan **Publicera** för att bekräfta.

1. I en dialogruta visas URL:er för att komma åt innehållet i förhandsvisningsmiljön.


Du kan även använda de URL-adresser som visas i guiden för att visa förhandsgranskningsinnehållet, men du kan också lägga till `preview-` till publicerings-URL:en för produktionsinstansen.

```
https://preview-p<programID>-e>environmentID>.adobeaemcloud.com/<pathtopage>.html
```

Se dokumentet [Hantera miljöer](/help/implementing/cloud-manager/manage-environments.md) om du vill ha mer information om hur du hämtar URL:er för dina miljöer.

Innehåll kan också publiceras för förhandsgranskning med en [arbetsflöde för publicera innehållsträd](/help/operations/replication.md#publish-content-tree-workflow) med `agentId` parametern inställd på `preview` eller genom att använda [replikerings-API](/help/operations/replication.md#replication-api) med `AgentFilter` konfigurerad för förhandsgranskning.

## Avpublicera innehåll från förhandsgranskning {#unpublishing-content-from-preview}

Avpublicera innehåll från **Förhandsgranska** miljön är i stort sett samma process som [avpublicera sidor](/help/sites-cloud/authoring/fundamentals/publishing-pages.md#unpublishing-pages) från **Publicera** miljö.

Den enda skillnaden är att du kan välja **Mål** att **Förhandsgranska**.

## Ytterligare information {#further-information}

Se även:

* [Konfigurera OSGi-inställningar för förhandsgranskningsnivån](/help/implementing/preview-tier/preview-tier-configuring-osgi.md#configuring-osgi-settings-for-the-preview-tier)

* [Förhandsvisa felsökning med Developer Console](/help/implementing/preview-tier/preview-tier-configuring-osgi.md#debugging-preview-using-the-developer-console)
---
title: Förhandsgranska innehåll
description: Lär dig hur du använder AEM förhandsvisningstjänst för att förhandsgranska innehåll innan du publicerar.
exl-id: 6b4b57f6-2e66-4c83-94d9-bc1e0daab0f3
source-git-commit: a9a2362903e8eec25393e2ceb307814e1a21f142
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 0%

---


# Förhandsgranska innehåll {#previewing-content}

AEM erbjuder en tjänst för förhandsgranskning av webbplatser som gör att utvecklare och innehållsförfattare kan förhandsgranska webbplatsens slutresultat innan den når publiceringsmiljön och blir tillgänglig för allmänheten.

Det gör det lättare att förhandsgranska sidor som annars inte skulle vara synliga i redigeringsmiljön, som sidövergångar och annat innehåll på publiceringssidan.

>[!NOTE]
>
>Eftersom innehållet är *publicerat* i förhandsvisningsmiljön är det tillgängligt via URL (så behöver inte åtkomst till AEM).

Mer information om förhandsvisningsmiljöerna finns i [Hantera miljöer](/help/implementing/cloud-manager/manage-environments.md#access-preview-service).

## Publicera innehåll för förhandsgranskning {#publishing-content-to-preview}

Du kan publicera innehåll till förhandsgranskningstjänsten med användargränssnittet för **Hanterad publikation**.

1. I webbplatskonsolen markerar du den eller de sidor som du vill skicka för förhandsgranskning och klickar på knappen **Hantera publikation** .
1. Välj **Förhandsgranska** som mål i följande guide.

   ![hanterad publikation](/help/sites-cloud/authoring/assets/previewmanagedpublication.png)

1. Klicka på **Nästa** och sedan på **Publish** för att bekräfta.

1. I en dialogruta visas URL:er för att komma åt innehållet i förhandsvisningsmiljön.

   >[!NOTE]
   >
   >Eftersom innehållet är *publicerat* i förhandsvisningsmiljön är det tillgängligt via URL (så behöver inte åtkomst till AEM).

Du kan också använda de URL:er som visas i guiden för att visa förhandsgranskningsinnehållet, men du kan också lägga till `preview-` i publicerings-URL:en för produktionsinstansen.

```
https://preview-p<programID>-e>environmentID>.adobeaemcloud.com/<pathtopage>.html
```

Mer information om hur du hämtar URL:er för dina miljöer finns i dokumentet [Hantera miljöer](/help/implementing/cloud-manager/manage-environments.md).

Innehåll kan också publiceras för förhandsgranskning med ett [publiceringsinnehållsträdsarbetsflöde](/help/operations/replication.md#publish-content-tree-workflow) med parametern `agentId` inställd på `preview` eller med [replikerings-API](/help/operations/replication.md#replication-api) med en `AgentFilter` konfigurerad för förhandsgranskning.

## Avpublicera innehåll från förhandsgranskning {#unpublishing-content-from-preview}

Att avpublicera innehåll från din **förhandsvisningsmiljö** är i princip samma process som [att avpublicera sidor](/help/sites-cloud/authoring/fundamentals/publishing-pages.md#unpublishing-pages) från **Publish** -miljön.

Den enda skillnaden är att du kan välja **destination** som **förhandsvisning**.

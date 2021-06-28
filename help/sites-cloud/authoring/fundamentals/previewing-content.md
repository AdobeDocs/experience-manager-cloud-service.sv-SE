---
title: Förhandsgranska innehåll
description: Lär dig hur du använder AEM Preview Service för att förhandsgranska innehåll innan du publicerar.
exl-id: 6b4b57f6-2e66-4c83-94d9-bc1e0daab0f3
source-git-commit: c30470b321a4fba8c8de9becb62c518faff05498
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---

# Förhandsgranska innehåll {#previewing-content}

>[!NOTE]
>
>Förhandsgranskningsfunktionen ingår i version 2021.5.0 och kommer att lanseras gradvis under de kommande veckorna.

AEM har en Site Preview Service som är avsedd att låta utvecklare och skribenter förhandsgranska en webbplats innan den når publiceringsmiljön och är tillgänglig för allmänheten.

Det underlättar förhandsgranskning av sidupplevelser som annars inte skulle vara synliga i redigeringsmiljön, som sidövergångar och annat innehåll på publiceringssidan.

## Publicera innehåll för förhandsgranskning {#publishing-content-to-preview}

Du kan publicera innehåll till förhandsgranskningstjänsten med hjälp av gränssnittet för hanterade publikationer på följande sätt:

1. Markera den eller de sidor du vill skicka för förhandsgranskning i webbplatskonsolen och klicka på knappen **Hantera publikation**
1. I följande guide väljer du **Förhandsgranska** som mål

   ![hanterad publikation](/help/sites-cloud/authoring/assets/previewmanagedpublication.png)

1. Klicka på **Nästa** och **Publicera** för att bekräfta.

1. I en dialogruta visas URL:er för att komma åt innehållet i förhandsvisningsmiljön.

   Du kan också lägga till **förhandsgranskning** till publicerings-URL:en för produktionsinstansen om du vill visa förhandsvisningsinnehållet.

   URL:en ska utformas så här:

   ```
   https://preview-p[programID]-e[environmentID].adobeaemcloud.com/pathtopage.html
   ```

Mer information om hur du hämtar URL:er för dina miljöer finns i [Hantera dina miljöer](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/manage-your-environment.html?lang=en).

Innehåll kan också publiceras för förhandsgranskning med hjälp av ett [Publicera innehållsträdsarbetsflöde](/help/operations/replication.md#publish-content-tree-workflow) med parametern agentId inställd på förhandsgranskning eller med hjälp av [replikerings-API](/help/operations/replication.md#replication-api) med ett AgentFilter konfigurerat för förhandsgranskning.

## Konfigurera OSGi-inställningar för förhandsgranskningsnivån {#configuring-osgi-settings-for-the-preview-tier}

OSGI-egenskapsvärdena för förhandsgranskningsskiktet ärvs från publiceringsskiktet, men värdena för förhandsgranskningsskiktet kan särskiljas från publiceringsskiktet med hjälp av miljöspecifika värden som anger tjänstparametern med värdet &quot;preview&quot;. Ta exemplet nedan på en OSGI-egenskap som bestämmer URL:en för en integreringsslutpunkt:

```
[
{
"name":"INTEGRATION_URL",
"type":"string",
"value":"http://s2.integrationvendor.com",
"service": "preview"
}
]
```

Mer information finns i [det här avsnittet](/help/implementing/deploying/configuring-osgi.md#author-vs-publish-configuration) i OSGi-konfigurationsdokumentationen.

## Förhandsvisa felsökning med Developer Console {#debugging-preview-using-the-developer-console}

Följ de här stegen för att felsöka förhandsvisningsnivån med hjälp av utvecklarkonsolen:

* I [Developer Console](/help/implementing/developing/introduction/development-guidelines.md#aem-as-a-cloud-service-development-tools) väljer du antingen **— All Preview —** eller en produktionsmiljö som innehåller **prev** i namnet
* Generera relevant information för förhandsvisningsinstansen
Mer information om hur du hämtar URL:er för dina miljöer finns i [Hantera dina miljöer](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/manage-your-environment.html?lang=en).

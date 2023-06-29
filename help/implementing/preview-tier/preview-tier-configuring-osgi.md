---
title: Konfigurera OSGi-inställningar för förhandsgranskningsnivån
description: Lär dig hur du konfigurerar AEM förhandsvisningstjänst för att förhandsgranska innehåll innan du publicerar.
exl-id: 1200bb17-8a3c-4e41-85f4-ed2334b61f69
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---

# Konfigurera OSGi-inställningar för förhandsgranskningsnivån {#configure-osgi-preview-tier}

AEM erbjuder en förhandsvisningstjänst för webbplatser som gör att utvecklare och innehållsförfattare kan förhandsgranska webbplatsens slutliga upplevelse innan den når publiceringsmiljön och är tillgänglig för allmänheten.

Det underlättar förhandsgranskning av en rad upplevelser som annars inte skulle vara synliga från författarmiljön. Exempel: sidövergångar, upplevelsefragment och annat innehåll på publiceringssidan.

OSGi-egenskapsvärdena för förhandsvisningsskiktet ärvs från publiceringsskiktet. Värdena för förhandsvisningsskiktet kan dock skilja sig från publiceringsskiktet genom att ställa in `service` parameter till värdet `preview`.

>[!NOTE]
>
>Mer information om förhandsvisningsmiljöerna finns i [Hantera miljöer](/help/implementing/cloud-manager/manage-environments.md#access-preview-service).

## Konfigurera OSGi-inställningarna för förhandsgranskningsnivån {#configuring-osgi-settings-for-the-preview-tier}

Följande exempel på en OSGi-egenskap avgör URL:en för en integreringsslutpunkt.

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

Följ de här stegen för att felsöka förhandsvisningsnivån med hjälp av Developer Console:

* I [Developer Console](/help/implementing/developing/introduction/development-guidelines.md#aem-as-a-cloud-service-development-tools), välj antingen **— All Preview —** eller en produktionsmiljö som innehåller **föregående** i namnet
* Generera relevant information för förhandsvisningsinstansen Se [Hantera miljöer](/help/implementing/cloud-manager/manage-environments.md) om du vill ha mer information om hur du hämtar URL:er för dina miljöer.

---
title: Integrera med Git
description: Integrera med Git - Cloud Services
translation-type: tm+mt
source-git-commit: 23349f3350631f61f80b54b69104e5a19841272f
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 2%

---


# Integrera Git med Adobe Cloud Manager {#git-integration}

Adobe Cloud Manager levereras med en enda Git-databas som används för att distribuera kod med Cloud Managers CI/CD-pipelines. Kunderna kan använda Cloud Managers Git-databas direkt. Kunderna kan också integrera en lokal eller **kundhanterad** Git-databas med Cloud Manager.

## Git-integrering - översikt {#git-integration-overview}

>[!VIDEO](https://video.tv.adobe.com/v/28710/)

I den här videoserien utforskas flera användningsexempel när det gäller att integrera en kundhanterad Git-databas med Cloud Manager, bland annat:

* [Inledande synkronisering](#initial-sync)
* [Grundläggande förgreningsstrategi](#branching-strategy)
* [Funktionsutveckling](#feature-development)
* [Produktionsdistribution](#production-deployment)
* [Synkroniserar versionstaggar](#sync-tags)

Videoserien bygger på grundläggande kunskaper i Git och källkodshantering. Se [ytterligare resurser nedan](#additional-resources) för mer information om Git.

>[!NOTE]
>
>Stegen och namnkonventioner som beskrivs i den här videoserien är några av de bästa sätten att arbeta med en kundhanterad Git-databas och Cloud Manager. Konventioner och arbetsflöden som skildras förväntas anpassas för enskilda utvecklingsteam.

## Inledande synkronisering {#initial-sync}

Första steget för synkronisering av en kundhanterad Git-databas med Cloud Managers Git-databas.

>[!VIDEO](https://video.tv.adobe.com/v/28711/?quality=12)

## Grundläggande förgreningsstrategi {#branching-strategy}

Följ videon nedan för att lära dig de grundläggande förgreningsstrategierna.

>[!VIDEO](https://video.tv.adobe.com/v/28712/?quality=12)

## Funktionsutveckling {#feature-development}

Använd en funktionsgren för att isolera kodändringar i en kundhanterad Git-databas och synkronisera med Cloud Managers Git-databas för att använda en icke-produktionsprocess för kodkvalitets- och valideringstestning.

>[!VIDEO](https://video.tv.adobe.com/v/28723/?quality=12)

## Produktionsdistribution {#production-deployment}

Förbered kod för en produktionsrelease i en kundhanterad Git-databas och synkronisera med Cloud Managers Git-databas för att distribuera till scen- och produktionsmiljöer.

>[!VIDEO](https://video.tv.adobe.com/v/28724/?quality=12)

## Synkroniserar versionstaggar {#sync-tags}

Synkronisera versionstaggar från en Cloud Manager Git-databas till en kundhanterad Git-databas för att ge dig en bild av vilken kod som har distribuerats till scen- och produktionsmiljöer.

>[!VIDEO](https://video.tv.adobe.com/v/28725/?quality=12)

## Ytterligare resurser {#additional-resources}

* [GitHub-resurser](https://try.github.io)
* [Atlassian Git Tutorials](https://www.atlassian.com/git/tutorials/what-is-version-control)
* [Git Cheat Sheet](https://education.github.com/git-cheat-sheet-education.pdf)
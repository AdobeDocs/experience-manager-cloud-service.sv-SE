---
title: Använd Git med Cloud Manager
description: Lär dig hur du använder Cloud Manager Git-databaser och hur du integrerar din egen kundhanterade Git-databas med Cloud Manager.
exl-id: 57e71b8a-4546-4d7f-825c-a1637d08e608
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 80206fc1396896fe45e2c959c78a0bf30eba71c5
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# Använd Git med Cloud Manager {#git-integration}

Adobe Cloud Manager levereras med en enda Git-databas som används för att distribuera kod med Cloud Manager CI/CD-pipelines.

Du kan använda Cloud Manager Git-databas direkt, men du har också möjlighet att integrera en kundhanterad Git-databas med Cloud Manager.

## Översikt över Git-integrering {#git-integration-overview}

I den här videoserien utforskas flera användningsfall när en kundhanterad Git-databas integreras med Cloud Manager, bland annat:

* [Inledande synkronisering](#initial-sync)
* [Grundläggande förgreningsstrategi](#branching-strategy)
* [Funktionsutveckling](#feature-development)
* [Produktionsdistribution](#production-deployment)
* [Synkroniserar versionstaggar](#sync-tags)

Videoserien bygger på grundläggande kunskaper i Git och källkodshantering. Mer information om Git finns i [ytterligare resurser nedan](#additional-resources).

>[!VIDEO](https://video.tv.adobe.com/v/28710/)

Stegen och namnkonventioner som beskrivs i den här videoserien är några av de bästa sätten att arbeta med en kundhanterad Git-databas i Cloud Manager. Konventionerna och arbetsflödena som återges förväntas vara anpassade för enskilda användningsområden.

## Inledande synkronisering {#initial-sync}

I den här videon lär du dig de första stegen för att synkronisera en kundhanterad Git-databas med Cloud Manager Git-databas.

>[!VIDEO](https://video.tv.adobe.com/v/28711/?quality=12)

## Grundläggande förgreningsstrategi {#branching-strategy}

I den här videon lär du dig grundläggande förgrenade strategier.

>[!VIDEO](https://video.tv.adobe.com/v/28712/?quality=12)

## Utveckling av funktionsgrenar {#feature-development}

Använd en funktionsgren för att isolera kodändringar i en kundhanterad Git-databas och synkronisera med Cloud Manager Git-databas för att använda en icke-produktionsprocess för kodkvalitets- och valideringstestning.

>[!VIDEO](https://video.tv.adobe.com/v/28723/?quality=12)

## Produktionsdistribution {#production-deployment}

Förbered kod för en produktionsrelease i en kundhanterad Git-databas och synkronisera med Cloud Manager Git-databas för att distribuera till scen- och produktionsmiljöer.

>[!VIDEO](https://video.tv.adobe.com/v/28724/?quality=12)

## Synkronisera versionstaggar {#sync-tags}

Synkronisera versionstaggar från en Cloud Manager Git-databas i en kundhanterad Git-databas för att se vilken kod som har distribuerats till testnings- och produktionsmiljöer.

>[!VIDEO](https://video.tv.adobe.com/v/28725/?quality=12)

## Ytterligare resurser {#additional-resources}

* [GitHub-resurser](https://docs.github.com/en/get-started/getting-started-with-git/set-up-git)
* [Atlassisk Git Tutorials](https://www.atlassian.com/git/tutorials/what-is-version-control)
* [Git Cheat Sheet](https://education.github.com/git-cheat-sheet-education.pdf)

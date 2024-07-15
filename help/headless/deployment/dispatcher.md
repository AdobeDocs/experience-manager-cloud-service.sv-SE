---
title: Dispatcher slutpunktskonfiguration med AEM Headless
description: Dispatcher är ett cachnings- och säkerhetslager framför Adobe Experience Manager Publish-miljöer. Flera konfigurationer används för att öppna GraphQL-slutpunkter till headless-program.
feature: Headless, Dispatcher, GraphQL API
exl-id: 78a20021-910f-4cf0-87bf-6e2223994f76
role: Admin, Developer
source-git-commit: bdf3e0896eee1b3aa6edfc481011f50407835014
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 0%

---


# Dispatcher - slutpunktskonfiguration med AEM Headless

[Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html) är ett cachnings- och säkerhetslager framför Adobe Experience Manager Publish-miljöer. Flera konfigurationer ingår som standard för att öppna GraphQL-slutpunkter för headless-program.

>[!NOTE]
>
>Detaljerad dokumentation om Dispatcher finns i [Dispatcher Guide](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html).

Som en del i ett AEM Project ingår en Dispatcher-modul som innehåller konfigurationer för Dispatcher. Nyligen genererade projekt från [AEM Project Archetype](https://github.com/adobe/aem-project-archetype) inkluderar automatiskt [filter](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?#defining-a-filter) som aktiverar GraphQL-slutpunkter.

## GraphQL Endpoints

Som en del av standardfiltren öppnas [GraphQL-slutpunkter](/help/headless/graphql-api/graphql-endpoint.md) med följande regel:

```
/0060 { /type "allow" /method '(POST|OPTIONS)' /url "/content/_cq_graphql/*/endpoint.json" }
```

Jokertecknet `*` öppnar flera slutpunkter på AEM. En fråga om att använda en GraphQL-slutpunkt görs med `POST` och svaret är **inte** cachelagrat.

## GraphQL Beständiga frågor

Begäran om beständiga frågor görs mot en annan slutpunkt. Som en del av standardfilterkonfigurationen öppnas URL:en för [beständiga frågor](/help/headless/graphql-api/persisted-queries.md) med följande regel:

```
/0061 { /type "allow" /method '(GET|POST|OPTIONS)' /url "/graphql/execute.json*" }
```

Beständiga frågor kan begäras med `GET` genom att svaret cachelagras på Dispatcher- och CDN-nivå. Mer information om cachelagring och cacheogiltigförklaring finns [här](/help/implementing/dispatcher/caching.md).

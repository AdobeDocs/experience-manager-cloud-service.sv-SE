---
title: Dispatcher-konfiguration med AEM Headless
description: Dispatcher är ett cachnings- och säkerhetslager framför Adobe Experience Manager Publish-miljöer. Flera konfigurationer används för att öppna GraphQL-slutpunkter till headless-program.
feature: Dispatcher, GraphQL API
exl-id: 78a20021-910f-4cf0-87bf-6e2223994f76
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---

# Dispatcher-konfiguration med AEM Headless

The [Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html) är ett cachnings- och säkerhetslager framför Adobe Experience Manager Publish-miljöer. Flera konfigurationer ingår som standard för att öppna GraphQL-slutpunkter för headless-program.

>[!NOTE]
>
>Detaljerad dokumentation om Dispatcher finns i [Dispatcher Guide](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html)

Som en del av ett AEM-projekt inkluderas en dispatchermodul som innehåller konfigurationer för dispatchern. Nyligen genererade projekt från [AEM Project Archetype](https://github.com/adobe/aem-project-archetype) innehåller [filter](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?#defining-a-filter) som möjliggör slutpunkter från GraphQL.

## GraphQL-slutpunkt(er)

Som en del av standardfiltren [GraphQL slutpunkter](/help/headless/graphql-api/graphql-endpoint.md) öppnas med följande regel:

```
/0060 { /type "allow" /method '(POST|OPTIONS)' /url "/content/_cq_graphql/*/endpoint.json" }
```

The `*` jokertecken öppnar flera slutpunkter på AEM. Fråga med en GraphQL-slutpunkt görs med `POST` och svaret **not** cachelagras.

## GraphQL Beständiga frågor

Begäran om beständiga frågor görs mot en annan slutpunkt. Som en del av standardfilterkonfigurationen, URL:en för [Beständiga frågor](/help/headless/graphql-api/persisted-queries.md) öppnas med följande regel:

```
/0061 { /type "allow" /method '(GET|POST|OPTIONS)' /url "/graphql/execute.json*" }
```

Beständiga frågor kan begäras med `GET`, vilket cachelagrar svaret på Dispatcher- och CDN-nivå. Mer information om cachelagring och ogiltigförklaring av cache finns [här](/help/implementing/dispatcher/caching.md).

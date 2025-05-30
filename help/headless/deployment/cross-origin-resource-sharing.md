---
title: Cross-Origin Resource Sharing (CORS)-konfiguration med AEM Headless
description: Adobe Experience Manager Cross-Origin Resource Sharing (CORS) gör att webbapplikationer utan gränssnitt kan ringa AEM på klientsidan. En CORS-konfiguration krävs för att aktivera åtkomst till GraphQL-slutpunkten.
feature: Headless, GraphQL API
exl-id: 426be9f9-f44a-4744-ac08-e64bb97308a0
solution: Experience Manager
role: Admin, Developer
source-git-commit: bdf3e0896eee1b3aa6edfc481011f50407835014
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 0%

---

# CORS-konfiguration (Cross-Origin Resource Sharing)

>[!CAUTION]
>
>Om [cachelagring i Dispatcher har aktiverats](/help/headless/deployment/dispatcher-caching.md) behövs inte CORS-filtret, så det här avsnittet kan ignoreras.

>[!NOTE]
>
>En detaljerad översikt över CORS-resursdelningsprincipen i AEM finns i [Förstå korsdomänsresursdelning (CORS)](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html?lang=sv-SE#understand-cross-origin-resource-sharing-(cors)).

För att få åtkomst till GraphQL-slutpunkten måste en CORS-princip konfigureras och läggas till i ett AEM som [distribueras till AEM via Cloud Manager](/help/implementing/cloud-manager/deploy-code.md). Detta görs genom att en lämplig OSGi CORS-konfigurationsfil läggs till för de önskade slutpunkterna. Flera CORS-konfigurationer kan skapas och distribueras till olika miljöer. Exempel finns i [WKND-referenswebbplatsen](https://github.com/adobe/aem-guides-wknd/tree/master/ui.config/src/main/content/jcr_root/apps/wknd/osgiconfig)

CORS-konfigurationen måste ange den betrodda webbplatsens ursprung `alloworigin` eller `alloworiginregexp` som åtkomst måste beviljas för.

Konfigurationsfilen måste ha följande namn: `com.adobe.granite.cors.impl.CORSPolicyImpl~appname-graphql.cfg.json` där `appname` speglar namnet på ditt program.

Om du till exempel vill ge åtkomst till GraphQL-slutpunkten `/content/cq:graphql/wknd/endpoint` och den beständiga frågeslutpunkten för `https://my.domain` kan du använda:

```json
{
  "supportscredentials":false,
  "supportedmethods":[
    "GET",
    "HEAD",
    "POST"
  ],
  "exposedheaders":[
    ""
  ],
  "alloworigin":[
    "https://my.domain"
  ],
  "maxage:Integer":1800,
  "alloworiginregexp":[
    ""
  ],
  "supportedheaders":[
    "Origin",
    "Accept",
    "X-Requested-With",
    "Content-Type",
    "Access-Control-Request-Method",
    "Access-Control-Request-Headers"
  ],
  "allowedpaths":[
    "/content/cq:graphql/wknd/endpoint.json",
    "/graphql/execute.json/.*"
  ]
}
```

Om du har konfigurerat en huvudsökväg för slutpunkten kan du även använda den i `allowedpaths`.

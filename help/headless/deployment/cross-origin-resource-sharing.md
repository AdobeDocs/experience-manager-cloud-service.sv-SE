---
title: Cross-Origin Resource Sharing (CORS)-konfiguration med AEM Headless
description: Adobe Experience Manager Cross-Origin Resource Sharing (CORS) gör att webbapplikationer utan gränssnitt kan ringa AEM på klientsidan. En CORS-konfiguration krävs för att aktivera åtkomst till GraphQL-slutpunkten.
feature: GraphQL API
source-git-commit: 0cc131209f497241949f8da6e8144dfcaffe7e6e
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---


# CORS-konfiguration (Cross-Origin Resource Sharing)

>[!NOTE]
>
>En detaljerad översikt över CORS resursdelningsprincip i AEM finns på [CORS (Cross-Origin Resource Sharing)](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html#understand-cross-origin-resource-sharing-(cors)).

För att komma åt GraphQL-slutpunkten måste en CORS-princip konfigureras och läggas till i ett AEM projekt som [distribueras till AEM via Cloud Manager](/help/implementing/cloud-manager/deploy-code.md). Detta görs genom att en lämplig OSGi CORS-konfigurationsfil läggs till för de önskade slutpunkterna. Flera CORS-konfigurationer kan skapas och distribueras till olika miljöer. Exempel finns i [WKND-referensplats](https://github.com/adobe/aem-guides-wknd/tree/master/ui.config/src/main/content/jcr_root/apps/wknd/osgiconfig)

CORS-konfigurationen måste ange en betrodd webbplatsens ursprung `alloworigin` eller `alloworiginregexp` för vilka tillträde måste beviljas.

Konfigurationsfilen måste ha följande namn: `com.adobe.granite.cors.impl.CORSPolicyImpl~appname-graphql.cfg.json` där `appname` återspeglar programmets namn.

Om du till exempel vill ge åtkomst till GraphQL-slutpunkten `/content/cq:graphql/wknd/endpoint` och beständiga frågeslutpunkter för `https://my.domain` du kan använda:

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

Om du har konfigurerat en hjälpsökväg för slutpunkten kan du även använda den i `allowedpaths`.



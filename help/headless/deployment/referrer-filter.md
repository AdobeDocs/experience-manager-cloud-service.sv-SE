---
title: Referensfilterkonfiguration med AEM Headless
description: Adobe Experience Manager referensfilter ger åtkomst från tredjepartsvärdar. En OSGi-konfiguration för referensfiltret krävs för att aktivera åtkomst till GraphQL-slutpunkten för headless-program.
feature: GraphQL API
source-git-commit: 0cc131209f497241949f8da6e8144dfcaffe7e6e
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 0%

---


# Referensfilter {#referrer-filter}

Adobe Experience Manager referensfilter ger åtkomst från tredjepartsvärdar. En OSGi-konfiguration för referensfiltret krävs för att aktivera åtkomst till GraphQL-slutpunkten för headless-program.

Detta gör du genom att lägga till en lämplig OSGi-konfiguration för referensfiltret som:

* anger ett betrott värdnamn för en webbplats, antingen `allow.hosts` eller `allow.hosts.regexp`,
* ger åtkomst till det här värdnamnet.

Namnet på filen måste vara `org.apache.sling.security.impl.ReferrerFilter.cfg.json`.

Om du till exempel vill ge åtkomst för begäranden med referenten `my.domain` du kan:

```xml
{
    "allow.empty":false,
    "allow.hosts":[
      "my.domain"
    ],
    "allow.hosts.regexp":[
      ""
    ],
    "filter.methods":[
      "POST",
      "PUT",
      "DELETE",
      "COPY",
      "MOVE"
    ],
    "exclude.agents.regexp":[
      ""
    ]
}
```

>[!CAUTION]
>
>Det är kundens ansvar att
>
>* endast ge åtkomst till betrodda domäner
>* se till att ingen känslig information exponeras
>* inte använda jokertecken [*] syntax, Detta inaktiverar både autentiserad åtkomst till GraphQL-slutpunkten och exponerar den även för hela världen.


>[!CAUTION]
>
>Alla GraphQL [scheman](#schema-generation) (härleds från Content Fragment Models som har **Aktiverad**) går att läsa via GraphQL-slutpunkten.
>
>Detta innebär att ni måste se till att inga känsliga uppgifter finns tillgängliga, eftersom de skulle kunna läckas på detta sätt. Detta inkluderar till exempel information som kan finnas som fältnamn i modelldefinitionen.

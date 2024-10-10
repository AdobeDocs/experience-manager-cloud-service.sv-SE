---
title: Refererarfilterkonfiguration med AEM Headless
description: Adobe Experience Manager referensfilter ger åtkomst från tredjepartsvärdar. En OSGi-konfiguration för referensfiltret krävs för att aktivera åtkomst till GraphQL-slutpunkten för headless-program.
feature: Headless, GraphQL API
exl-id: e2e3d2dc-b839-4811-b5d1-38ed8ec2cc87
solution: Experience Manager
role: Admin, Developer
source-git-commit: 3096436f8057833419249d51cb6c15e6c28e9e13
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---

# Referensfilter {#referrer-filter}

Adobe Experience Manager referensfilter ger åtkomst från tredjepartsvärdar.

En OSGi-konfiguration för referensfiltret behövs för att aktivera åtkomst till GraphQL-slutpunkten för headless-program via HTTP-POST. När du använder AEM Headless Persisted Queries som öppnar AEM via HTTP-GET behövs ingen konfiguration av referensfiltret.

>[!WARNING]
> AEM referensfilter är inte en OSGi-konfigurationsfabrik, vilket innebär att endast en konfiguration är aktiv i en AEM. Undvik när det är möjligt att lägga till anpassade inställningar för referensfilter, eftersom detta skriver över AEM egna konfigurationer och kan störa produktfunktionerna.

Detta gör du genom att lägga till en lämplig OSGi-konfiguration för referensfiltret som:

* anger ett betrott värdnamn för en webbplats, antingen `allow.hosts` eller `allow.hosts.regexp`,
* ger åtkomst till det här värdnamnet.

Namnet på filen måste vara `org.apache.sling.security.impl.ReferrerFilter.cfg.json`.

## Exempelkonfiguration {#example-configuration}

Om du till exempel vill bevilja åtkomst för begäranden med referenten `my.domain` kan du:

>[!CAUTION]
>
>Detta är ett grundläggande exempel som kan skriva över standardkonfigurationen. Du måste se till att produktuppdateringar alltid tillämpas på alla anpassningar.

```xml
{
    "allow.empty": false,
    "allow.hosts": [
      "my.domain"
    ],
    "allow.hosts.regexp": [
      ""
    ],
    "filter.methods": [
      "POST",
      "PUT",
      "DELETE",
      "COPY",
      "MOVE"
    ],
    "exclude.agents.regexp": [
      ""
    ]
}
```

## Datasäkerhet {#data-security}

>[!CAUTION]
>
>Det är fortfarande ditt ansvar att till fullo ta itu med följande punkter.

För att dina data ska förbli säkra måste du se till att:

* åtkomst är **endast** beviljad till betrodda domäner

* jokertecknets [`*`]-syntax i **används inte**. Detta inaktiverar både autentiserad åtkomst till GraphQL-slutpunkten och utsätter den även för hela världen

* känslig information **aldrig** exponeras; varken direkt eller indirekt:

   * Alla [GraphQL-scheman](/help/headless/graphql-api/content-fragments.md#schema-generation) är till exempel:

      * härledd från modeller för innehållsfragment som har **aktiverats**

     **och**

      * går att läsa via GraphQL-slutpunkten

     Det innebär att information som finns som fältnamn i modelldefinitionen kan bli tillgänglig.

Du måste se till att inga känsliga data finns tillgängliga på något sätt, så sådana detaljer måste noggrant övervägas.

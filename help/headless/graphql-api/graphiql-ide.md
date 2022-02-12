---
title: Använda GraphiQL IDE i AEM
description: Lär dig hur du använder GraphiQL IDE i Adobe Experience Manager.
feature: Content Fragments,GraphQL API
source-git-commit: c4490690edb1ec0e2a6b8cca724fe9c290650bc8
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 3%

---


# Använda GraphiQL IDE {#graphiql-ide}

En implementering av standarden [GraphiQL](https://graphql.org/learn/serving-over-http/#graphiql) IDE kan användas med AEM GraphQL. Det här kan [installerade med AEM](#installing-graphiql-ide).

>[!NOTE]
>
>GraphiQL är bundet till den globala slutpunkten (och fungerar inte med andra slutpunkter för specifika platskonfigurationer).

Med GraphiQL-verktyget kan du direkt mata in, testa och felsöka frågor. GraphiQL ger också enkel åtkomst till dokumentationen vilket gör det enkelt att ta reda på vilka metoder som finns tillgängliga.

Till exempel:

* `http://localhost:4502/content/graphiql.html`

Detta innehåller funktioner som syntaxmarkering, automatisk komplettering, autoförslag, samt historik och onlinedokumentation:

![GraphiQL-gränssnitt](assets/cfm-graphiql-interface.png "GraphiQL-gränssnitt")

## Installera AEM GraphiQL IDE {#installing-graphiql-ide}

GraphiQL IDE är ett utvecklingsverktyg och behövs bara i miljöer på låg nivå, t.ex. en utvecklingsmiljö eller lokal instans. Det ingår därför inte i AEM utan ingår som ett separat paket som kan installeras på ad hoc-basis.

1. Navigera till **[Programdistributionsportal](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)** > **AEM as a Cloud Service**.
1. Sök efter &quot;GraphiQL&quot; (se till att inkludera **i** in **GraphiQL**.
1. Ladda ned den senaste **Innehållspaket för GraphiQL v.x.x.x**
1. Från **AEM** gå till **verktyg** > **Distribution** > **Paket**.
1. Klicka **Överför paket** och välj det paket som laddats ned i föregående steg. Klicka **Installera** för att installera paketet.


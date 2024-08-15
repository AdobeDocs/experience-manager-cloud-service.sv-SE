---
title: Autentisering för fjärrfrågor AEM GraphQL-frågor om innehållsfragment
description: Förstå den autentisering som krävs för fjärrfrågor till Adobe Experience Manager GraphQL för att säkra din headless-leverans av innehåll.
feature: Headless, Content Fragments,GraphQL API
exl-id: dfeae661-06a1-4001-af24-b52ae12d625f
role: Admin, Developer
source-git-commit: 6719e0bcaa175081faa8ddf6803314bc478099d7
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---

# Autentisering för fjärrfrågor AEM GraphQL-frågor om innehållsfragment {#authentication-for-remote-aem-graphql-queries-on-content-fragments}

Ett primärt användningsfall för [Adobe Experience Manager as a Cloud Service (AEM) GraphQL API for Content Fragment Delivery](/help/headless/graphql-api/content-fragments.md) är att ta emot fjärrfrågor från tredjepartsprogram eller -tjänster. Dessa fjärrfrågor kan kräva autentiserad API-åtkomst för säker leverans av headless-innehåll.

>[!NOTE]
>
>För testning och utveckling kan du även komma åt det AEM GraphQL-API:t direkt via [GraphiQL-gränssnittet](/help/headless/graphql-api/graphiql-ide.md).

För autentisering måste tredjepartstjänsten [hämta en åtkomsttoken](#retrieving-access-token) som sedan kan [användas i GraphQL-begäran](#use-access-token-in-graphql-request).

## Hämtar en åtkomsttoken {#retrieving-access-token}

Mer information finns i [Generera åtkomsttoken för API:er på serversidan](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md).

## Använda åtkomsttoken i en GraphQL-begäran {#use-access-token-in-graphql-request}

För att en tredjepartstjänst ska kunna ansluta till en AEM måste den ha en *åtkomsttoken*. Tjänsten måste sedan lägga till denna token i huvudet `Authorization` på POSTENS begäran.

Ett GraphQL Authorization Header:

```xml
Authorization: Bearer <access_token>
```

## Behörighetskrav {#permission-requirements}

Alla begäranden som görs med åtkomsttoken görs *av användarkontot som genererade token*.

Det här användarkontot innebär att du måste kontrollera att kontot har de behörigheter som krävs för att köra GraphQL-frågor.

Du kan kontrollera dessa behörigheter med GraphiQL på den lokala instansen. Mer information finns i [Behörighetsaspekter för headless-innehåll](/help/headless/security/permissions.md).

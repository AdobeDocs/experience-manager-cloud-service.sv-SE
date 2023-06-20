---
title: Autentisering för fjärrfrågor AEM GraphQL-frågor om innehållsfragment
description: Förstå den autentisering som krävs för AEM GraphQL-frågor på fjärrbasis för att skydda din headless-innehållsleverans.
feature: Content Fragments,GraphQL API
exl-id: dfeae661-06a1-4001-af24-b52ae12d625f
source-git-commit: bceec9ea6858b1c4c042ecd96f13ae5cac1bbee5
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---

# Autentisering för fjärrfrågor AEM GraphQL-frågor om innehållsfragment {#authentication-for-remote-aem-graphql-queries-on-content-fragments}

Ett primärt användningsexempel för [Adobe Experience Manager as a Cloud Service (AEM) GraphQL API for Content Fragment Delivery](/help/headless/graphql-api/content-fragments.md) tar emot fjärrfrågor från program eller tjänster från tredje part. Dessa fjärrfrågor kan kräva autentiserad API-åtkomst för säker leverans av headless-innehåll.

>[!NOTE]
>
>För testning och utveckling kan du även komma åt AEM GraphQL API direkt via [GraphiQL-gränssnitt](/help/headless/graphql-api/graphiql-ide.md) gränssnitt.

För autentisering måste tredjepartstjänsten [hämta en åtkomsttoken](#retrieving-access-token)som sedan kan [som används i GraphQL Request](#use-access-token-in-graphql-request).

## Hämtar en åtkomsttoken {#retrieving-access-token}

Se [Genererar åtkomsttoken för API:er på serversidan](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md) för fullständig information.

## Använda åtkomsttoken i en GraphQL-begäran {#use-access-token-in-graphql-request}

För att en tredjepartstjänst ska kunna ansluta till en AEM instans måste den ha en *Åtkomsttoken*. Tjänsten måste sedan lägga till denna token i `Authorization` sidhuvud på POSTEN.

Ett GraphQL Authorization Header:

```xml
Authorization: Bearer <access_token>
```

## Behörighetskrav {#permission-requirements}

Alla förfrågningar som görs med åtkomsttoken kommer faktiskt att göras *av användarkontot som genererade token*.

Det innebär att du måste kontrollera att kontot har de behörigheter som krävs för att köra GraphQL-frågor.

Du kan kontrollera detta med GraphiQL på den lokala instansen. Mer information om [behörigheter finns här](/help/headless/security/permissions.md).

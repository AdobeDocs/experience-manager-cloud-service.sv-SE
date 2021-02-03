---
title: Autentisering för AEM GraphQL-frågor om innehållsfragment
description: Lär dig mer om den autentisering som krävs för GraphQL-frågor i AEM.
translation-type: tm+mt
source-git-commit: 42ca0c70f7018a6e3c9be68ef13adefafc987864
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---


# Autentisering för AEM GraphQL-frågor för innehållsfragment {#authentication-for-remote-aem-graphql-queries-on-content-fragments}

Ett primärt användningsexempel för [Adobe Experience Manager som en Cloud Service (AEM) GraphQL API för Content Fragment Delivery](/help/assets/content-fragments/graphql-api-content-fragments.md) är att ta emot fjärrfrågor från tredjepartsprogram eller -tjänster.  Dessa fjärrfrågor kan kräva autentiserad API-åtkomst.

>[!NOTE]
>
>För testning och utveckling kan du även komma åt AEM GraphQL API direkt via gränssnittet [GraphiQL](/help/assets/content-fragments/graphql-api-content-fragments.md#graphiql-interface).

För autentisering måste tredjepartstjänsten använda en [åtkomsttoken](#access-token), som sedan kan användas [i GraphQL-begäran](#use-access-token-in-graphql-request).

## Hämtar en åtkomsttoken {#retrieving-access-token}

Mer information finns i [Generera åtkomsttoken för API:er på serversidan](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md).

## Använda åtkomsttoken i en GraphQL-begäran {#use-access-token-in-graphql-request}

För att en tredjepartstjänst ska kunna ansluta till en AEM måste den ha en *åtkomsttoken*. Tjänsten måste sedan lägga till denna token i rubriken `Authorization` på begäran om POST.

Ett GraphQL Authorization Header:

```xml
Authorization: Bearer <access_token>
```

## Behörighetskrav {#permission-requirements}

Alla förfrågningar som görs med åtkomsttoken kommer faktiskt att göras *av användarkontot som genererade token*.

Det innebär att du måste kontrollera att kontot har de behörigheter som krävs för att köra GraphQL-frågor.

Du kan kontrollera detta med GraphiQL på den lokala instansen.

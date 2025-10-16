---
title: Skapa en API-begäran - Headless-konfiguration
description: Lär dig hur du använder GraphQL API för headless-leverans av Content Fragment-innehåll och AEM Assets REST API för hantering av innehållsfragment.
exl-id: 2b72f222-2ba5-4a21-86e4-40c763679c32
feature: Headless, Content Fragments,GraphQL API
role: Admin, Developer
source-git-commit: 38a4bf89e099432163163e90e08aa0f47407724f
workflow-type: tm+mt
source-wordcount: '417'
ht-degree: 0%

---

# Skapa en API-begäran - Headless-konfiguration {#accessing-delivering-content-fragments}

Lär dig hur du använder GraphQL API för headless-leverans av Content Fragment-innehåll och AEM Assets REST API för hantering av innehållsfragment.

## Vad är GraphQL och Assets REST API:er? {#what-are-the-apis}

[Nu när du har skapat några innehållsfragment](create-content-fragment.md) kan du använda AEM API:er för att leverera dem utan problem.

* [Med GraphQL-API:t](/help/headless/graphql-api/content-fragments.md) kan du skapa begäranden om åtkomst till och leverans av innehållsfragment. API:t erbjuder den mest robusta uppsättningen funktioner för att fråga efter och konsumera innehåll i innehållsfragment.
   * Om du vill använda API:t [definierar och aktiverar du slutpunkter i AEM](/help/headless/graphql-api/graphql-endpoint.md), och om det behövs [GraphiQL-gränssnittet som är installerat](/help/headless/graphql-api/graphiql-ide.md).
* Ett urval av [AEM-API:er för leverans och hantering av strukturerat innehåll](/help/headless/apis-headless-and-content-fragments.md) är tillgängliga för användning med innehållsfragment.

Resten av guiden fokuserar på GraphQL åtkomst och leverans av innehållsfragment.

## Aktivera GraphQL Endpoint {#enable-graphql-endpoint}

Innan GraphQL API:er kan användas måste en GraphQL-slutpunkt skapas.

Mer information finns i [Hantera GraphQL-slutpunkter i AEM](/help/headless/graphql-api/graphql-endpoint.md).

## Fråga innehåll med GraphQL med GraphiQL

Informationsarkitekterna skapar frågor om sina kanalslutpunkter för att leverera innehåll. Ta hänsyn till dessa frågor endast en gång per slutpunkt, per modell. För att komma igång-guiden behöver du bara skapa en.

GraphiQL är en IDE som ingår i din AEM-miljö. Den är tillgänglig/synlig när du har [konfigurerat slutpunkterna](#enable-graphql-endpoint).

Mer information finns i [Använda GraphiQL IDE](/help/headless/graphql-api/graphiql-ide.md).

GraphQL möjliggör strukturerade frågor som inte bara kan rikta sig till specifika datauppsättningar eller enskilda dataobjekt, utan även kan leverera specifika element i objekten, kapslade resultat, har stöd för frågevariabler och mycket annat.

GraphQL kan undvika iterativa API-förfrågningar och överleverans, och tillåter istället massleverans av exakt det som behövs för återgivning som svar på en enda API-fråga. Den resulterande JSON kan användas för att leverera data till andra webbplatser eller appar.

## Nästa steg {#next-steps}

Så ja! Nu har du en grundläggande förståelse för headless content management i AEM. Det finns många fler resurser där du kan fördjupa dig för att få en heltäckande bild av de funktioner som finns.

* **[Innehållsfragment](/help/sites-cloud/administering/content-fragments/managing.md)** - Mer information om hur du skapar och hanterar innehållsfragment
* **[Stöd för innehållsfragment i AEM Assets HTTP API](/help/assets/content-fragments/assets-api-content-fragments.md)** - Mer information om hur du får åtkomst till AEM-innehåll direkt via HTTP API, via CRUD-åtgärder (Skapa, Läs, Uppdatera, Ta bort)
* **[GraphQL API](/help/headless/graphql-api/content-fragments.md)** - Mer information om hur du skickar innehållsfragment utan problem

>[!NOTE]
>
>OpenAPI:erna [Content Fragment och Content Fragment Model](/help/headless/content-fragment-openapis.md) är också tillgängliga.

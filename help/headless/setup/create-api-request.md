---
title: Skapa en API-begäran - Headless-konfiguration
description: Lär dig hur du använder GraphQL API för headless-leverans av Content Fragment-innehåll och AEM Assets REST API för att hantera innehållsfragment.
exl-id: 2b72f222-2ba5-4a21-86e4-40c763679c32
feature: Headless, Content Fragments,GraphQL API
role: Admin, Developer
source-git-commit: bdf3e0896eee1b3aa6edfc481011f50407835014
workflow-type: tm+mt
source-wordcount: '674'
ht-degree: 0%

---

# Skapa en API-begäran - Headless-konfiguration {#accessing-delivering-content-fragments}

Lär dig hur du använder GraphQL API för headless-leverans av Content Fragment-innehåll och AEM Assets REST API för att hantera innehållsfragment.

## Vad är GraphQL och Assets REST API:er? {#what-are-the-apis}

[Nu när du har skapat några innehållsfragment ](create-content-fragment.md) kan du använda AEM API:er för att leverera dem utan problem.

* [Med GraphQL-API:t](/help/headless/graphql-api/content-fragments.md) kan du skapa begäranden om åtkomst till och leverans av innehållsfragment. API:t erbjuder den mest robusta uppsättningen funktioner för att fråga efter och konsumera innehåll i innehållsfragment.
   * Om du vill använda API:t [definierar och aktiverar du slutpunkter i AEM](/help/headless/graphql-api/graphql-endpoint.md) och om det behövs [GraphiQL-gränssnittet som är installerat](/help/headless/graphql-api/graphiql-ide.md).
* [Med Assets REST API](/help/assets/content-fragments/assets-api-content-fragments.md) kan du skapa och ändra innehållsfragment (och andra resurser).

>[!NOTE]
>
>OpenAPI:erna [Content Fragment och Content Fragment Model](/help/headless/content-fragment-openapis.md) är också tillgängliga.

Resten av guiden fokuserar på GraphQL åtkomst och leverans av innehållsfragment.

## Aktivera GraphQL Endpoint {#enable-graphql-endpoint}

Innan GraphQL API:er kan användas måste en GraphQL-slutpunkt skapas.

1. Navigera till **Verktyg**, **Allmänt** och välj sedan **GraphQL**.
1. Välj **Skapa**.
1. Dialogrutan **Skapa ny GraphQL-slutpunkt** öppnas. Här kan du ange:
   * **Namn**: slutpunktens namn. Du kan ange valfri text.
   * **Använd GraphQL-schema från**: använd listrutan för att välja den konfiguration som krävs.
1. Bekräfta med **Skapa**.
1. I konsolen visas en **sökväg** baserat på konfigurationen som skapades tidigare. Den här sökvägen används för att köra GraphQL-frågor.

   ```
   /content/cq:graphql/<configuration-name>/endpoint
   ```

Mer information om att aktivera [GraphQL-slutpunkter finns här](/help/headless/graphql-api/graphql-endpoint.md).

## Fråga innehåll med GraphQL med GraphiQL

Informationsarkitekterna skapar frågor om sina kanalslutpunkter för att leverera innehåll. Ta hänsyn till dessa frågor endast en gång per slutpunkt, per modell. För att komma igång-guiden behöver du bara skapa en.

GraphiQL är en IDE som ingår i AEM. Den är tillgänglig/synlig när du [har konfigurerat slutpunkterna](#enable-graphql-endpoint).

1. Logga in i AEM as a Cloud Service och öppna GraphiQL-gränssnittet:

   Du kan öppna frågeredigeraren från:

   * **Verktyg** > **Allmänt** > **GraphQL Query Editor**
   * direkt, till exempel `http://localhost:4502/aem/graphiql.html`

1. GraphiQL IDE är en frågeredigerare i webbläsaren för GraphQL. Du kan använda den för att skapa frågor för att hämta innehållsfragment och leverera dem i headlessläge som JSON.
   * I den nedrullningsbara menyn längst upp till höger kan du välja slutpunkten.
   * I en panel längst till vänster visas de beständiga frågorna (om de är tillgängliga)
   * På panelen i mitten till vänster kan du skapa din fråga.
   * Resultaten visas på panelen i det mittersta högra hörnet.
   * Frågeredigeraren har funktioner för kodkomplettering och snabbtangenter för att enkelt köra frågan.

   ![GraphiQL-redigerare](../assets/graphiql.png)

1. Om du utgår ifrån att den modell du skapade anropades med fälten `firstName`, `lastName` och `position` kan du skapa en enkel fråga för att hämta innehållet i innehållsfragmentet.`person`

   ```text
   query 
   {
     personList {
       items {
         _path
         firstName
         lastName
         position
       }
     }
   }
   ```

1. Skriv frågan i den vänstra panelen.
   ![GraphiQL-fråga](../assets/graphiql-query.png)

1. Klicka på knappen **Kör fråga** eller använd snabbtangenten `Ctrl-Enter` så visas resultatet som JSON i den högra panelen.
   ![GraphiQL-resultat](../assets/graphiql-results.png)

1. Klicka på länken **Dokument** i det övre högra hörnet på sidan om du vill visa sammanhangsberoende dokumentation så att du kan skapa frågor som anpassar sig efter dina egna modeller.
   ![GraphiQL-dokumentation](../assets/graphiql-documentation.png)

GraphQL möjliggör strukturerade frågor som inte bara kan rikta sig till specifika datauppsättningar eller enskilda dataobjekt, utan även kan leverera specifika element i objekten, kapslade resultat, har stöd för frågevariabler och mycket annat.

GraphQL kan undvika iterativa API-förfrågningar och överleverans, och tillåter istället massleverans av exakt det som behövs för återgivning som svar på en enda API-fråga. Den resulterande JSON kan användas för att leverera data till andra webbplatser eller appar.

## Nästa steg {#next-steps}

Så ja! Ni har nu en grundläggande förståelse för innehållshantering utan problem i AEM. Det finns många fler resurser där du kan fördjupa dig för att få en heltäckande bild av de funktioner som finns.

* **[Innehållsfragment](/help/sites-cloud/administering/content-fragments/managing.md)** - Mer information om hur du skapar och hanterar innehållsfragment
* **[Stöd för innehållsfragment i AEM Assets HTTP API](/help/assets/content-fragments/assets-api-content-fragments.md)** - Mer information om hur du får åtkomst till AEM direkt via HTTP API, via CRUD-åtgärder (Create, Read, Update, Delete)
* **[GraphQL API](/help/headless/graphql-api/content-fragments.md)** - Mer information om hur du skickar innehållsfragment utan problem

>[!NOTE]
>
>OpenAPI:erna [Content Fragment och Content Fragment Model](/help/headless/content-fragment-openapis.md) är också tillgängliga.

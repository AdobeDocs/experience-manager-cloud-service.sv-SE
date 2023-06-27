---
title: Skapa en API-begäran - Headless-konfiguration
description: Lär dig hur du använder GraphQL API för headless-leverans av Content Fragment-innehåll och AEM Assets REST API för att hantera innehållsfragment.
exl-id: 2b72f222-2ba5-4a21-86e4-40c763679c32
source-git-commit: d361ddc9a50a543cd1d5f260c09920c5a9d6d675
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 0%

---

# Skapa en API-begäran - Headless-konfiguration {#accessing-delivering-content-fragments}

Lär dig hur du använder GraphQL API för headless-leverans av Content Fragment-innehåll och AEM Assets REST API för att hantera innehållsfragment.

## Vad är GraphQL och Assets REST API:er? {#what-are-the-apis}

[Nu när du har skapat några innehållsfragment,](create-content-fragment.md) kan du använda AEM-API:er för att leverera dem utan problem.

* [GraphQL API](/help/headless/graphql-api/content-fragments.md) Med kan du skapa förfrågningar om åtkomst och leverans av innehållsfragment. API:t erbjuder den mest robusta uppsättningen funktioner för att fråga efter och konsumera innehåll i innehållsfragment.
   * Om du vill använda API:t [definiera och aktivera slutpunkter i AEM](/help/headless/graphql-api/graphql-endpoint.md)och, om det behövs, [GraphiQL-gränssnittet är installerat](/help/headless/graphql-api/graphiql-ide.md).
* [Resursens REST API](/help/assets/content-fragments/assets-api-content-fragments.md) I kan du skapa och ändra innehållsfragment (och andra resurser).

Resten av guiden fokuserar på GraphQL åtkomst och leverans av innehållsfragment.

## Aktivera GraphQL Endpoint {#enable-graphql-endpoint}

Innan GraphQL API:er kan användas måste en GraphQL-slutpunkt skapas.

1. Navigera till **verktyg**, **Allmänt** väljer **GraphQL**.
1. Välj **Skapa**.
1. The **Skapa ny GraphQL-slutpunkt** öppnas. Här kan du ange:
   * **Namn**: Slutpunktens namn. du kan skriva vilken text som helst.
   * **Använd GraphQL-schema från**: Använd listrutan för att välja önskad konfiguration.
1. Bekräfta med **Skapa**.
1. I konsolen **Bana** visas baserat på konfigurationen som skapades tidigare. Den här sökvägen används för att köra GraphQL-frågor.

   ```
   /content/cq:graphql/<configuration-name>/endpoint
   ```

Mer information om aktivering [GraphQL-slutpunkter finns här](/help/headless/graphql-api/graphql-endpoint.md).

## Fråga innehåll med GraphQL med GraphiQL

Informationsarkitekterna skapar frågor om sina kanalslutpunkter för att leverera innehåll. Ta hänsyn till dessa frågor endast en gång per slutpunkt, per modell. För att komma igång-guiden behöver du bara skapa en.

GraphiQL är en integrerad utvecklingsmiljö som ingår i AEM. den är tillgänglig/synlig efter att du har [konfigurera dina slutpunkter](#enable-graphql-endpoint).

1. Logga in AEM as a Cloud Service och gå till GraphiQL-gränssnittet:

   Du kan öppna frågeredigeraren från:

   * **verktyg** -> **Allmänt** -> **GraphQL Query Editor**
   * direkt, till exempel `http://localhost:4502/aem/graphiql.html`

1. GraphiQL IDE är en frågeredigerare i webbläsaren för GraphQL. Du kan använda den för att skapa frågor för att hämta innehållsfragment och leverera dem i headlessläge som JSON.
   * I den nedrullningsbara listrutan högst upp till höger kan du välja slutpunkten.
   * I en panel längst till vänster visas de beständiga frågorna (om de är tillgängliga)
   * På panelen i mitten till vänster kan du skapa din fråga.
   * Resultaten visas på panelen i det mittersta högra hörnet.
   * Frågeredigeraren har funktioner för kodkomplettering och snabbtangenter för att enkelt köra frågan.

   ![GraphiQL editor](../assets/graphiql.png)

1. Anta att modellen du skapade anropades `person` med fält `firstName`, `lastName`och `position`kan du skapa en enkel fråga som hämtar innehållet i innehållsfragmentet.

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

1. Klicka på **Kör fråga** eller använder `Ctrl-Enter` snabbtangenten och resultatet visas som JSON i den högra panelen.
   ![GraphiQL-resultat](../assets/graphiql-results.png)

1. Klicka på i det övre högra hörnet på sidan **Dokument** om du vill visa sammanhangsberoende dokumentation så att du kan skapa frågor som anpassar sig efter dina egna modeller.
   ![GraphiQL-dokumentation](../assets/graphiql-documentation.png)

GraphQL möjliggör strukturerade frågor som inte bara kan rikta sig till specifika datauppsättningar eller enskilda dataobjekt, utan även kan leverera specifika element i objekten, kapslade resultat, har stöd för frågevariabler och mycket annat.

GraphQL kan undvika iterativa API-förfrågningar och överleverans, och tillåter istället massleverans av exakt det som behövs för återgivning som svar på en enda API-fråga. Den resulterande JSON kan användas för att leverera data till andra webbplatser eller appar.

## Nästa steg {#next-steps}

Så ja! Ni har nu en grundläggande förståelse för innehållshantering utan problem i AEM. Det finns många fler resurser där du kan fördjupa dig för att få en heltäckande bild av de funktioner som finns.

* **[Innehållsfragment](/help/sites-cloud/administering/content-fragments/content-fragments.md)** - Mer information om hur du skapar och hanterar innehållsfragment
* **[Stöd för innehållsfragment i AEM Assets HTTP API](/help/assets/content-fragments/assets-api-content-fragments.md)** - Mer information om hur du får åtkomst till AEM direkt via HTTP API, via CRUD-åtgärder (Create, Read, Update, Delete)
* **[GraphQL API](/help/headless/graphql-api/content-fragments.md)** - Mer information om hur du levererar innehållsfragment utan problem

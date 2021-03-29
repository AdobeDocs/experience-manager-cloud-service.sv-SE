---
title: Komma åt och leverera innehållsfragment Headless Quick Start Guide
description: Lär dig hur du använder AEM Assets REST API för att hantera innehållsfragment och GraphQL API för headless-leverans av Content Fragment-innehåll.
translation-type: tm+mt
source-git-commit: e7ca6dc841ba777384be74021a27d523d530a956
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 0%

---


# Komma åt och leverera innehållsfragment Headless Quick Start Guide {#accessing-delivering-content-fragments}

Lär dig hur du använder AEM Assets REST API för att hantera innehållsfragment och GraphQL API för headless-leverans av Content Fragment-innehåll.

## Vad är GraphQL och Assets REST API:er? {#what-are-the-apis}

[Nu när du har skapat några innehållsfragment kan ](create-content-fragment.md) du använda AEM-API:er för att leverera dem direkt.

* [Med GraphQL ](/help/assets/content-fragments/graphql-api-content-fragments.md) API:t kan du skapa begäranden om åtkomst till och leverans av innehållsfragment.
* [Med Resurser REST ](/help/assets/content-fragments/assets-api-content-fragments.md) API kan du skapa och ändra innehållsfragment (och andra resurser).

Resten av guiden fokuserar på GraphQL-åtkomst och leverans av innehållsfragment.

## Leverera ett innehållsfragment med GraphQL {#how-to-deliver-a-content-fragment}

Informationsarkitekterna måste utforma frågor för sina kanalslutpunkter för att kunna leverera innehåll. Dessa frågor behöver i allmänhet bara övervägas en gång per slutpunkt och modell. I den här guiden behöver vi bara skapa en.

<!-- Not in the UI yet - will need updating when it is -->
<!--
1. Log into AEM as a Cloud Service and from the main menu select **Tools -&gt; Assets -&gt; GraphQL** 
   * Alternatively open the page directly at `https://<host>:<port>/content/graphiql.html`.
-->

1. Logga in AEM som Cloud Service och öppna GraphiQL-gränssnittet:
   * Till exempel: `https://<host>:<port>/content/graphiql.html`.

1. GraphiQL är en frågeredigerare i webbläsaren för GraphQL. Du kan använda den för att skapa frågor för att hämta innehållsfragment och leverera dem i headlessskick som JSON.
   * I den vänstra panelen kan du skapa din fråga.
   * Resultatet visas på den högra panelen.
   * Frågeredigeraren har funktioner för kodkomplettering och snabbtangenter för att enkelt köra frågan.
      ![GraphiQL editor](../assets/graphiql.png)

1. Om vi utgår ifrån att modellen vi skapade hette `person` med fälten `firstName`, `lastName` och `position`, kan vi skapa en enkel fråga för att hämta innehållet i innehållsfragmentet.

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

1. Klicka på länken **Dokument** längst upp till höger på sidan om du vill visa sammanhangsberoende dokumentation som hjälper dig att skapa frågor som anpassar sig till dina egna modeller.
   ![GraphiQL-dokumentation](../assets/graphiql-documentation.png)

GraphQL möjliggör strukturerade frågor som inte bara kan ha specifika datauppsättningar eller enskilda dataobjekt som mål, utan också kan leverera specifika element i objekten, kapslade resultat, har stöd för frågevariabler och mycket annat.

GraphQL kan undvika både iterativa API-begäranden och överleverans, och i stället möjliggör massleverans av exakt det som behövs för återgivning som svar på en enda API-fråga. Den resulterande JSON kan användas för att leverera data till andra webbplatser eller appar.

## Nästa steg {#next-steps}

Så ja! Ni har nu en grundläggande förståelse för innehållshantering utan problem i AEM. Det finns förstås många fler resurser där du kan fördjupa dig i en heltäckande bild av de funktioner som finns.

* **Konfigurationsläsaren**  - Mer information om AEM konfigurationsläsare
* **[Innehållsfragment](/help/assets/content-fragments/content-fragments.md)**  - Mer information om hur du skapar och hanterar innehållsfragment
* **[Stöd för innehållsfragment i AEM Assets HTTP API](/help/assets/content-fragments/assets-api-content-fragments.md)**  - Mer information om hur du får åtkomst till AEM direkt via HTTP API, via CRUD-åtgärder (Create, Read, Update, Delete)
* **[GraphQL API](/help/assets/content-fragments/graphql-api-content-fragments.md)**  - Mer information om hur du skickar innehållsfragment utan problem

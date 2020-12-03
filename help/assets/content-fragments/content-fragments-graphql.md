---
title: Headless Content Delivery using Content Fragments with GraphQL
description: Lär dig hur du använder innehållsfragment i Adobe Experience Manager (AEM) som en Cloud Service med GraphQL för leverans av Headless-innehåll.
translation-type: tm+mt
source-git-commit: 1e9596fb12a38f5c4c6e15d7c33af86e59e76083
workflow-type: tm+mt
source-wordcount: '860'
ht-degree: 0%

---


# Headless Content Delivery using Content Fragments with GraphQL {#headless-content-delivery-using-content-fragments-with-graphQL}

>[!CAUTION]
>
>AEM GraphQL API, för Content Fragment Delivery, släpps i början av 2021.
>
>Den relaterade dokumentationen är redan tillgänglig för förhandsgranskning.

Med Adobe Experience Manager (AEM) som Cloud Service kan du använda innehållsfragment tillsammans med det AEM GraphQL-API:t (en anpassad implementering baserad på standard GraphQL) för att leverera strukturerat innehåll som ska användas i dina program.

## Headless CMS {#headless-cms}

Ett CMS-system (Headless Content Management System) är:

* &quot;*Ett headless content management-system, eller headless CMS, är ett CMS-system (content management system) som byggs från grunden som en innehållsdatabas som gör innehåll tillgängligt via ett API för visning på valfri enhet.*

   *Termen&quot;headless&quot; kommer från begreppet&quot;head&quot; (den främre delen, dvs. webbplatsen) av&quot;body&quot; (den bakre delen, dvs. innehållsdatabasen).*&quot;

   Se [Wikipedia](https://en.wikipedia.org/wiki/Headless_content_management_system).

När det gäller utveckling av innehållsfragment i AEM innebär detta att:

* Du kan använda Innehållsfragment för att skapa innehåll som inte primärt är avsett att publiceras direkt (1:1) på formaterade sidor.

* Innehållet i dina innehållsfragment kommer att struktureras på ett förutbestämt sätt, enligt modellerna för innehållsfragment. Detta förenklar åtkomsten för dina program, som kommer att bearbeta innehållet ytterligare.

>[!NOTE]
>
>Se [Headless och AEM](/help/implementing/developing/headless/introduction.md) för en introduktion till Headless Development för AEM Sites som Cloud Service.

## GraphQL - en översikt {#graphql-overview}

GraphQL är:

* &quot;*..ett frågespråk för API:er och en körningsmiljö för att utföra dessa frågor med dina befintliga data. GraphQL ger en komplett och lättförståelig beskrivning av data i ditt API, ger kunderna möjlighet att fråga efter exakt vad de behöver och inget mer, gör det enklare att utveckla API:er över tid och möjliggör kraftfulla utvecklingsverktyg.*&quot;.

   Se [GraphQL.org](https://graphql.org)

* &quot;*..en öppen specifikation för ett flexibelt API-lager. Flytta GraphQL över dina befintliga bakgrunder för att skapa produkter snabbare än någonsin....*&quot;.

   Se [Utforska GraphQL](https://www.graphql.com). &quot;*Explore GraphQL hanteras av Apollo-teamet. Vårt mål är att ge utvecklare och tekniska ledare över hela världen alla verktyg de behöver för att förstå och implementera GraphQL.*&quot;.

Med [AEM GraphQL API](#aem-graphql-api) kan du utföra (komplexa) frågor på dina [innehållsfragment](/help/assets/content-fragments/content-fragments.md); där varje fråga följer en viss modelltyp. Det returnerade innehållet kan sedan användas av dina program.

### GraphQL-terminologi {#graphql-terminology}

GraphQL använder följande:

* **[Frågor](https://graphql.org/learn/queries/)**

* **[Scheman och typer](https://graphql.org/learn/schema/)**  - GraphQL visar de typer och åtgärder som tillåts för GraphQL för AEM implementering.

* **[Fält](https://graphql.org/learn/queries/#fields)**

* **GraphQL-slutpunkt**  - den sökväg i AEM som svarar på GraphQL-frågor och ger åtkomst till GraphQL-scheman.

Mer information finns i [(GraphQL.org) Introduktion till GraphQL](https://graphql.org/learn/), inklusive [Best Practices](https://graphql.org/learn/best-practices/).

### GraphQL-frågetyper {#graphql-query-types}

Med GraphQL kan du utföra frågor för antingen:

* **En post**

* **[Förteckning över poster](https://graphql.org/learn/schema/#lists-and-non-null)**

## AEM GraphQL API {#aem-graphql-api}

För [Adobe Experience som Cloud Experience har en anpassad implementering av standard-GraphQL API](/help/assets/content-fragments/graphql-api-content-fragments.md) implementerats.

Implementeringen av AEM GraphQL API baseras på Java-biblioteken [GraphQL](https://graphql.org/code/#java).

## Innehållsfragment för användning med AEM GraphQL API {#content-fragments-use-with-aem-graphql-api}

[Content ](#content-fragments) Fragmentscan kan användas som bas för GraphQL för AEM frågor som:

* Med dem kan du utforma, skapa, strukturera och publicera sidoberoende innehåll.
* [Modeller för innehållsfragment](#content-fragments-models) tillhandahåller den struktur som krävs med hjälp av definierade datatyper.
* Du kan använda [fragmentreferensen](#fragment-references) när du definierar en modell för att definiera ytterligare lager i strukturen.

![Innehållsfragment för användning med ](assets/cfm-nested-01.png "GraphQLContent Fragments för GraphQL")

### Innehållsfragment {#content-fragments}

Innehållsfragment:

* Innehåller strukturerat innehåll.

* De baseras på en [modell för innehållsfragment](#content-fragments-models), som fördefinierar strukturen för det resulterande fragmentet.

### Modeller för innehållsfragment {#content-fragments-models}

Dessa [modeller för innehållsfragment](/help/assets/content-fragments/content-fragments-models.md):

* Ange de datatyper och fält som krävs för GraphQL. De ser till att programmet bara begär det som är möjligt och får det som förväntas.

* Datatypen **[Fragmentreferenser](#fragment-references)** kan användas i din modell för att referera till ett annat innehållsfragment, vilket innebär att ytterligare strukturnivåer införs.

### Fragmentreferenser {#fragment-references}

**[Fragmentreferens](/help/assets/content-fragments/content-fragments-models.md#fragment-reference-nested-fragments)**:

* Är av särskilt intresse tillsammans med GraphQL.

* Är en specifik datatyp som kan användas när en innehållsfragmentmodell definieras.

* Refererar till ett annat fragment, beroende på en viss innehållsfragmentmodell.

* Gör att du kan hämta strukturerade data.

   * När det definieras som en **multifeed** kan flera delfragment refereras (hämtas) av det primära fragmentet.

### JSON Preview {#json-preview}

Om du vill ha hjälp med att utforma och utveckla Content Fragment-lägen kan du förhandsgranska [JSON-utdata](/help/assets/content-fragments/content-fragments-json-preview.md).

## Lära sig att använda GraphQL med AEM - exempelinnehåll och frågor {#learn-graphql-with-aem-sample-content-queries}

Se [Lära dig använda GraphQL med AEM - Sample Content and Queries](/help/assets/content-fragments/content-fragments-graphql-samples.md) för en introduktion till att använda det AEM GraphQL API:t.

## Självstudiekurs - Komma igång med AEM Headless och GraphQL

Söker du en praktisk självstudiekurs? Ta en titt på [Komma igång med AEM Headless och GraphQL](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html) heltäckande självstudiekurs som visar hur du bygger upp och visar innehåll med AEM GraphQL API:er och som används av en extern app i ett headless CMS-scenario.
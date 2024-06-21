---
title: Headless Content Delivery using Content Fragments with GraphQL (Assets - Content Fragments)
description: Lär dig de grundläggande begreppen för att implementera ett AEM Headless CMS med hjälp av Content Fragments med GraphQL för leverans av headless-innehåll.
feature: Content Fragments
exl-id: 4a3b030d-ed59-4920-bf94-e00a45f85b51
role: User
solution: Experience Manager Sites
source-git-commit: f66ea281e6abc373e9704e14c97b77d82c55323b
workflow-type: tm+mt
source-wordcount: '719'
ht-degree: 0%

---

# Headless Content Delivery using Content Fragments with GraphQL {#headless-content-delivery-using-content-fragments-with-graphQL}

Med Content Fragments och GraphQL API kan du använda Adobe Experience Manager (AEM) as a Cloud Service som Headless Content Management System (CMS).

Detta uppnås med hjälp av innehållsfragment och det AEM GraphQL-API:t (en anpassad implementering som baseras på GraphQL-standard) för att enkelt kunna leverera strukturerat innehåll som ska användas i dina program. Möjligheten att anpassa en enda API-fråga gör att du kan hämta och leverera det specifika innehåll som du vill ha/behöver återge (som svar på en enskild API-fråga).

>[!NOTE]
>
>Se även:
>
>* [Vad är Headless?](/help/headless/what-is-headless.md) för en introduktion till Headless-koncept och -terminologi.
>
>* [Headless och AEM](/help/headless/introduction.md) för en introduktion till Headless Development för AEM Sites as a Cloud Service.

>[!NOTE]
>
>GraphQL används för närvarande i två (separata) scenarier i Adobe Experience Manager (AEM) as a Cloud Service:
>
>* [AEM Commerce använder data från en e-handelsplattform via GraphQL](/help/commerce-cloud/integrating/magento.md).
>* [AEM Content Fragments fungerar tillsammans med det AEM GraphQL-API:t (en anpassad implementering som baseras på GraphQL) för att leverera strukturerat innehåll som kan användas i dina program](/help/headless/graphql-api/content-fragments.md).

## Headless CMS {#headless-cms}

Ett Headless Content Management System (CMS) är ett innehållshanteringssystem som bara fungerar i bakgrunden och som utformats och byggts explicit som ett innehållsarkiv som gör innehåll tillgängligt via ett API för visning på alla enheter.

När det gäller utveckling av innehållsfragment i AEM innebär detta att:

* Du kan använda Innehållsfragment för att skapa innehåll som inte primärt är avsett att publiceras direkt (1:1) på formaterade sidor.

* Innehållet i dina innehållsfragment är strukturerat på ett förutbestämt sätt, enligt modellerna för innehållsfragment. Detta förenklar åtkomsten för dina program, som kommer att bearbeta innehållet ytterligare.

## GraphQL - en översikt {#graphql-overview}

GraphQL är:

* &quot;*...ett frågespråk för API:er och en körningsmiljö för att utföra dessa frågor med dina befintliga data.*&quot;.

  Se [GraphQL.org](https://graphql.org)

The [AEM GRAPHQL API](#aem-graphql-api) gör att du kan utföra (komplexa) frågor på [Innehållsfragment](/help/assets/content-fragments/content-fragments.md); där varje fråga följer en viss modelltyp. Det returnerade innehållet kan sedan användas av dina program.

## AEM GRAPHQL API {#aem-graphql-api}

För Adobe Experience som Cloud Experience har en anpassad implementering av GraphQL-standardprogrammeringsgränssnittet utvecklats. Se [AEM GraphQL API för användning med innehållsfragment](/help/headless/graphql-api/content-fragments.md) för mer information.

Den AEM API-implementeringen i GraphQL baseras på [GraphQL Java-bibliotek](https://graphql.org/code/#java).

## Innehållsfragment för användning med AEM GraphQL API {#content-fragments-use-with-aem-graphql-api}

[Innehållsfragment](#content-fragments) kan användas som bas för GraphQL AEM frågor som:

* Med dem kan du utforma, skapa, strukturera och publicera sidoberoende innehåll.
* The [Modeller för innehållsfragment](#content-fragments-models) tillhandahålla den struktur som krävs med hjälp av definierade datatyper.
* The [Fragmentreferens](#fragment-references), som är tillgängligt när du definierar en modell, kan användas för att definiera ytterligare lager av strukturen.

![Content Fragments for use with GraphQL](assets/cfm-nested-01.png "Content Fragments for use with GraphQL")

### Innehållsfragment {#content-fragments}

Innehållsfragment:

* Innehåller strukturerat innehåll.

* De är baserade på en [Content Fragment Model](#content-fragments-models), som fördefinierar strukturen för det resulterande fragmentet.

### Modeller för innehållsfragment {#content-fragments-models}

Dessa [Modeller för innehållsfragment](/help/assets/content-fragments/content-fragments-models.md):

* Används för att generera [Scheman](https://graphql.org/learn/schema/), en gång **Aktiverad**.

* Ange de datatyper och fält som krävs för GraphQL. De ser till att programmet bara begär det som är möjligt och får det som förväntas.

* Datatypen **[Fragmentreferenser](#fragment-references)** kan användas i din modell för att referera till ett annat innehållsfragment, och därför införs ytterligare strukturnivåer.

### Fragmentreferenser {#fragment-references}

The **[Fragmentreferens](/help/assets/content-fragments/content-fragments-models.md#fragment-reference-nested-fragments)**:

* Är av särskilt intresse tillsammans med GraphQL.

* Är en specifik datatyp som kan användas när en innehållsfragmentmodell definieras.

* Refererar till ett annat fragment, beroende på en viss innehållsfragmentmodell.

* Gör att du kan hämta strukturerade data.

   * Vid definition som **multifeed**, kan flera delfragment refereras (hämtas) av det primära fragmentet.

### JSON Preview {#json-preview}

Om du vill ha hjälp med att utforma och utveckla dina modeller för innehållsfragment kan du förhandsgranska [JSON-utdata](/help/assets/content-fragments/content-fragments-json-preview.md).

## Lära sig använda GraphQL med AEM - exempelinnehåll och frågor {#learn-graphql-with-aem-sample-content-queries}

Se [Lära sig använda GraphQL med AEM - exempelinnehåll och frågor](/help/headless/graphql-api/sample-queries.md) om du vill få en introduktion till hur du använder AEM GraphQL API.

## Självstudiekurs - Komma igång med AEM Headless och GraphQL

Söker du en praktisk självstudiekurs? Checka ut [Komma igång med AEM Headless och GraphQL](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html) en komplett självstudiekurs som visar hur man bygger upp och exponerar innehåll med hjälp av AEM GraphQL API:er och som används av en extern app, i ett headless CMS-scenario.

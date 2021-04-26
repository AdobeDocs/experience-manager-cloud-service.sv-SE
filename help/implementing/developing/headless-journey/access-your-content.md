---
title: Få åtkomst till ditt innehåll via AEM-API:er
description: I den här delen av AEM Headless Developer Journey kan du lära dig hur du använder GraphQL-frågor för att komma åt innehållet i innehållsfragment.
hide: true
hidefromtoc: true
index: false
translation-type: tm+mt
source-git-commit: d17583399b6792583e3e210005b62d360b91d05a
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 2%

---


# Så här kommer du åt ditt innehåll via AEM Delivery API:er {#access-your-content}

>[!CAUTION]
>
>ARBETE PÅGÅR - Dokumentet skapas för närvarande och ska inte tolkas som fullständigt eller slutgiltigt och inte heller användas i tillverkningssyfte.

I den här delen av [AEM Headless Developer Journey](#overview.md) lär du dig hur du använder GraphQL-frågor för att komma åt innehållet i dina innehållsfragment.

## Berättelsen hittills {#story-so-far}

I det föregående dokumentet från den AEM resan, [How to Model Your Content](model-your-content.md), lärde du dig grunderna i datamodellering i AEM och du bör nu:

* Förstå viktiga planeringsöverväganden när du utformar ditt innehåll.
* Förstå stegen för att implementera headless beroende på vilka krav ni har på integreringsnivån.
* Konfigurera de verktyg och AEM som behövs.
* Lär dig de bästa sätten att göra den enkla resan smidig, hålla innehållsgenereringen effektiv och se till att innehållet levereras snabbt.

Den här artikeln bygger på dessa grundläggande funktioner så att du förstår hur du får tillgång till ditt befintliga headless-innehåll i AEM via API.

* **Målgrupp**: Nybörjare
* **Mål**: Lär dig hur du kommer åt innehållet i dina innehållsfragment med AEM GraphQL-frågor:
   * Introducera GraphQL.
   * Introducera AEM GraphQL API.
   * Ta en titt på detaljerna i AEM GraphQL API.
   * Titta på några exempelfrågor för att se hur saker och ting fungerar i praktiken.

Med Adobe Experience Manager (AEM) som Cloud Service kan du använda innehållsfragment tillsammans med det AEM GraphQL-API:t för att leverera strukturerat innehåll som ska användas i dina program. Möjligheten att anpassa en enda API-fråga gör att du kan hämta och leverera det specifika innehåll som du vill ha/behöver återge (som svar på en enskild API-fråga).

>[!NOTE]
>AEM GraphQL API är en anpassad implementering som baseras på standard GraphQL.

## GraphQL - en introduktion {#graphql-introduction}

GraphQL är:

* &quot;*..ett frågespråk för API:er och en körningsmiljö för att utföra dessa frågor med dina befintliga data.*&quot;.

   Se *GraphQL*.

### GraphQL - typer {#graphql-types}

### GraphQL - scheman {#graphql-schemas}

### GraphQL - frågor {#graphql-queries}

## AEM och GraphQL {#aem-graphql}

GraphQL används på olika platser i AEM:

* Handel
   * Platshållare
* Innehållsfragment
   * Ett anpassat API har utvecklats för det här användningsfallet.
   * Det här är AEM GraphQL API.

## AEM GraphQL API {#aem-graphql-api}

För Adobe Experience som Cloud Experience har en anpassad implementering av standard-API:t GraphQL utvecklats.

Med AEM GraphQL API kan du utföra (komplexa) frågor på dina innehållsfragment; där varje fråga följer en viss modelltyp. Det returnerade innehållet kan sedan användas av dina program.

>[!NOTE]
>
>Implementeringen AEM GraphQL API baseras på GraphQL Java-biblioteken.

### AEM GraphQL API och innehållsfragment {#aem-graphql-content-fragments}

## Innehållsfragment för användning med AEM GraphQL API {#content-fragments-use-with-aem-graphql-api}

Innehållsfragment kan användas som bas för GraphQL för AEM frågor som:

* Med dem kan du utforma, skapa, strukturera och publicera sidoberoende innehåll.
* Modellerna för innehållsfragment tillhandahåller den struktur som krävs med hjälp av definierade datatyper.
* Fragmentreferensen, som är tillgänglig när du definierar en modell, kan användas för att definiera ytterligare lager med struktur.

### Innehållsfragment {#content-fragments}

Innehållsfragment:

* Innehåller strukturerat innehåll.

* De baseras på en Content Fragment Model, som i förväg definierar strukturen för det resulterande fragmentet.

### Modeller för innehållsfragment {#content-fragments-models}

Dessa modeller för innehållsfragment:

* Används för att generera scheman en gång **Aktiverat**.

* Ange de datatyper och fält som krävs för GraphQL. De ser till att programmet bara begär det som är möjligt och får det som förväntas.

* Datatypen **Fragmentreferenser** kan användas i din modell för att referera till ett annat innehållsfragment, vilket innebär att ytterligare strukturnivåer införs.

### Fragmentreferenser {#fragment-references}

**Fragmentreferens**:

* Är av särskilt intresse tillsammans med GraphQL.

* Är en specifik datatyp som kan användas när en innehållsfragmentmodell definieras.

* Refererar till ett annat fragment, beroende på en viss innehållsfragmentmodell.

* Gör att du kan hämta strukturerade data.

   * När det definieras som en **multifeed** kan flera delfragment refereras (hämtas) av det primära fragmentet.

### JSON Preview {#json-preview}

Om du vill ha hjälp med att designa och utveckla dina modeller för innehållsfragment kan du förhandsgranska [JSON-utdata](/help/assets/content-fragments/content-fragments-json-preview.md).

## What&#39;s Next {#whats-next}

[Lär dig hur du använder REST API för att komma åt och uppdatera innehållet i dina innehållsfragment](/help/implementing/developing/headless-journey/update-your-content.md).

## Ytterligare resurser {#additional-resources}

* [Getting Started with AEM Headless](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html)  - En kort videoserie med en översikt över hur du använder AEM headless-funktioner som datamodellering och GraphQL
* [GraphQL.org](https://graphql.org)
   * [Scheman](https://graphql.org/learn/schema/)
   * [GraphQL Java-bibliotek](https://graphql.org/code/#java)
* [AEM GraphQL API för användning med innehållsfragment](/help/assets/content-fragments/graphql-api-content-fragments.md)
   * [Att lära sig använda GraphQL med AEM - exempelinnehåll och frågor](/help/assets/content-fragments/content-fragments-graphql-samples.md)
   * [Autentisering för AEM GraphQL-frågor om innehållsfragment](/help/assets/content-fragments/graphql-authentication-content-fragments.md)
* [Arbeta med innehållsfragment](/help/assets/content-fragments/content-fragments.md)
   * [Modeller för innehållsfragment](/help/assets/content-fragments/content-fragments-models.md)
   * [JSON-utdata](/help/assets/content-fragments/content-fragments-json-preview.md)

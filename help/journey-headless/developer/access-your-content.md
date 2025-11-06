---
title: Så här kommer du åt ditt innehåll via AEM Delivery APIs
description: I den här delen av AEM Headless Developer Journey kan du lära dig hur du använder GraphQL-frågor för att komma åt ditt innehåll i Content Fragments.
exl-id: 1adecc69-5f92-4007-8a2a-65bf1e960645
solution: Experience Manager
feature: Headless, Content Fragments,GraphQL API
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1320'
ht-degree: 0%

---

# Så här kommer du åt ditt innehåll via AEM Delivery APIs {#access-your-content}

I den här delen av [AEM Headless Developer Journey](overview.md) kan du lära dig hur du använder GraphQL-frågor för att komma åt innehållet i dina innehållsfragment och skicka det till din app (headless delivery).

## Story hittills {#story-so-far}

I det tidigare dokumentet om AEM rubrikfria resa [Så här modellerar du ditt innehåll](model-your-content.md) lärde du dig grunderna i innehållsmodellering i AEM, så du bör nu förstå hur du modellerar innehållsstrukturen och sedan inse att strukturen med AEM Content Fragment Models och Content Fragments:

* Identifiera koncept och terminologi i samband med innehållsmodellering.
* Förstå varför innehållsmodellering behövs för leverans av Headless-innehåll.
* Förstå hur ni kan förverkliga den här strukturen med AEM Content Fragment Models (och skapa innehåll med Content Fragments).
* Förstå hur du modellerar innehåll, principer med grundläggande exempel.

Den här artikeln bygger på dessa grundläggande funktioner så att du kan förstå hur du får tillgång till ditt befintliga headless-innehåll i AEM med AEM GraphQL API.

* **Målgrupp**: Nybörjare
* **Mål**: Lär dig hur du kommer åt innehållet i dina innehållsfragment med hjälp av AEM GraphQL-frågor:
   * Nu kommer GraphQL och AEM GraphQL API.
   * Läs mer om AEM GraphQL API.
   * Titta på några exempelfrågor för att se hur saker och ting fungerar i praktiken.

## Så du vill komma åt ditt innehåll? {#so-youd-like-to-access-your-content}

Så.. du har fått allt det här innehållet, är strukturerat (i innehållsfragment) och bara väntar på att mata din nya app. Frågan är - hur man får dit den?

Vad du behöver är ett sätt att rikta specifikt innehåll, välja vad du behöver och returnera det till appen för vidare bearbetning.

Med Adobe Experience Manager (AEM) as a Cloud Service kan du selektivt komma åt dina innehållsfragment med hjälp av AEM GraphQL-API:t och endast returnera det innehåll du behöver. Det innebär att du kan leverera strukturerat innehåll utan extra kostnad och använda det i dina program.

>[!NOTE]
>
>AEM GraphQL API är en anpassad implementering som baseras på GraphQL standard-API-specifikationen.

## GraphQL - en introduktion {#graphql-introduction}

GraphQL är en öppen källkodsspecifikation som innehåller:

* ett frågespråk där du kan välja specifikt innehåll från strukturerade objekt.
* en körningsmiljö där du kan utföra dessa frågor med ditt strukturerade innehåll.

GraphQL är ett starkt typbestämt API. Det innebär att *allt*-innehåll måste vara tydligt strukturerat och organiserat efter typ, så att GraphQL *förstår* vad som ska användas och hur. Datafälten definieras i GraphQL-scheman, som definierar strukturen för innehållsobjekten.

GraphQL slutpunkter innehåller sedan de sökvägar som svarar på GraphQL-frågorna.

Allt detta innebär att appen kan välja rätt, tillförlitligt och effektivt innehåll - precis det du behöver när du använder AEM.

>[!NOTE]
>
>Se *GraphQL*.org och *GraphQL*.com.

<!--
## AEM and GraphQL {#aem-graphql}

GraphQL is used in various locations in AEM; for example:

* Content Fragments
  * A customized API has been developed for this use-case (Headless Delivery to your app).
    * This is the AEM GraphQL API.
* Commerce
  * AEM Commerce consumes data from a Commerce platform via GraphQL.
  * There are GraphQL integrations between AEM and various third-party commerce solutions, used with the extension hooks provided by the CIF Core Components.
    * This does not use the AEM GraphQL API.

>[!NOTE]
>
>This step of the Headless Journey is only concerned with the AEM GraphQL API and Content Fragments.
-->

## AEM GRAPHQL API {#aem-graphql-api}

AEM GraphQL API är en anpassad version som baseras på GraphQL API-standardspecifikationen som är särskilt konfigurerad för att du ska kunna utföra (komplexa) frågor på dina innehållsfragment.

Innehållsfragment används eftersom innehållet är strukturerat enligt modeller för innehållsfragment. Detta uppfyller GraphQL grundläggande krav.

* En innehållsfragmentmodell består av ett eller flera fält.
   * Varje fält definieras enligt en datatyp.
* Content Fragment Models används för att generera motsvarande AEM GraphQL-scheman.

För att få åtkomst till GraphQL för AEM (och innehållet) används en slutpunkt för att ange åtkomstsökvägen.

Innehållet som returneras via AEM GraphQL API kan sedan användas av dina program.

För att du ska få hjälp med direktinmatning och testfrågor finns en implementering av standardgränssnittet GraphiQL som också kan användas med AEM GraphQL (som kan installeras med AEM). Den innehåller funktioner som syntaxmarkering, automatisk komplettering, automatisk föreslå, samt historik och onlinedokumentation.

>[!NOTE]
>
>API-implementeringen för AEM GraphQL baseras på GraphQL Java-bibliotek.

<!--
### Use Cases for Author and Publish Environments {#use-cases-author-publish-environments}

The use cases for the AEM GraphQL API can depend on the type of AEM as a Cloud Service environment:

* Publish environment; used to: 
  * Query content for JS application (standard use-case)

* Author environment; used to: 
  * Query content for "content management purposes":
    * GraphQL in AEM as a Cloud Service is currently a read-only API.
    * The REST API can be used for CR(u)D operations.
-->

## Innehållsfragment för användning med AEM GraphQL API {#content-fragments-use-with-aem-graphql-api}

Innehållsfragment kan användas som bas för scheman och frågor för GraphQL för AEM som:

* Med dem kan du utforma, skapa, strukturera och publicera sidoberoende innehåll som kan levereras utan problem.
* De baseras på en Content Fragment Model, som fördefinierar strukturen för det resulterande fragmentet med hjälp av ett urval datatyper.
* Ytterligare strukturlager kan uppnås med datatypen Fragmentreferens, som är tillgänglig när du definierar en modell.

### Modeller för innehållsfragment {#content-fragments-models}

Dessa modeller för innehållsfragment:

* Används för att generera scheman när **Enabled** har aktiverats.
* Ange de datatyper och fält som krävs för GraphQL. De ser till att programmet bara begär det som är möjligt och får det som förväntas.
* Datatypen **Fragmentreferenser** kan användas i modellen för att referera till ett annat innehållsfragment, vilket innebär att ytterligare strukturnivåer införs.

### Fragmentreferenser {#fragment-references}

**Fragmentreferens** och **UUID för fragmentreferens**:

* Är specifika datatyper tillgängliga när du definierar en innehållsfragmentmodell.
* Refererar till ett annat fragment, beroende på en viss innehållsfragmentmodell.
* Gör att du kan skapa och sedan hämta strukturerade data.

   * När det definieras som en **multifeed** kan flera delfragment refereras (hämtas) av det primära fragmentet.

## Använda AEM GraphQL API {#actually-using-aem-graphiql}

### Inledande konfiguration {#initial-setup}

Innan du börjar med frågor om ditt innehåll måste du:

* Aktivera slutpunkten
   * Använd Verktyg > Allmänt > GraphQL
   * [Aktivera din GraphQL-slutpunkt](/help/headless/graphql-api/graphql-endpoint.md)
      * Detta aktiverar även GraphiQL IDE.

### Exempelstruktur {#sample-structure}

Om du vill använda AEM GraphQL API i en fråga kan vi använda de två mycket grundläggande modellstrukturerna för innehållsfragment:

* Företag
   * Namn - text
   * CEO (Person) - Fragmentreferens
   * Anställda (personer) - fragmentreferens(er)
* Person
   * Namn - text
   * Förnamn - text

Som du ser refererar fälten CEO och Employees till Personfragmenten.

Fragmentmodellerna används:

* när du skapar innehåll i Content Fragment Editor
* för att generera de GraphQL-scheman som du ska fråga efter

### Var ska du testa dina frågor? {#where-to-test-your-queries}

Frågorna kan anges i GraphiQL-gränssnittet. Du kan öppna frågeredigeraren från:

* **Verktyg** > **Allmänt** > **GraphQL Query Editor**
* direkt, till exempel `http://localhost:4502/aem/graphiql.html`

![Gränssnittet GraphiQL](assets/graphiql-interface.png "Gränssnittet GraphiQL")

### Komma igång med frågor {#getting-Started-with-queries}

En enkel fråga är att returnera namnet på alla poster i företagsschemat. Här begär du en lista med alla företagsnamn:

```xml
query {
  companyList {
    items {
      name
    }
  }
}
```

En något mer komplex fråga är att markera alla personer som inte har namnet&quot;Jobs&quot;. Detta filtrerar alla personer för alla som inte har namnet Jobs. Detta uppnås med operatorn EQUALS_NOT (det finns många fler):

```xml
query {
  personList(filter: {
    name: {
      _expressions: [
        {
          value: "Jobs"
          _operator: EQUALS_NOT
        }
      ]
    }
  }) {
    items {
      name
      firstName
    }
  }
}
```

Du kan också skapa mer komplexa frågor. Du kan till exempel söka efter alla företag som har minst en anställd med namnet &quot;Smith&quot;. Den här frågan visar filtrering för alla personer med namnet &quot;Smith&quot;, vilket returnerar information från de kapslade fragmenten:

```xml
query {
  companyList(filter: {
    employees: {
      _match: {
        name: {
          _expressions: [
            {
              value: "Smith"
            }
          ]
        }
      }
    }
  }) {
    items {
      name
      ceo {
        name
        firstName
      }
      employees {
        name
        firstName
      }
    }
  }
}
```

Mer information om hur du använder API:t för AEM GraphQL, tillsammans med hur du konfigurerar de nödvändiga elementen, finns i:

* Lära sig använda GraphQL med AEM
* Strukturen för exempelinnehållsfragment
* Lära sig använda GraphQL med AEM - exempelinnehåll och frågor

## What&#39;s Next {#whats-next}

Nu när du har lärt dig att komma åt och fråga efter rubriklöst innehåll med AEM GraphQL API kan du nu [lära dig hur du använder REST API för att komma åt och uppdatera innehållet i dina innehållsfragment](update-your-content.md).

## Ytterligare resurser {#additional-resources}

* [Adobe Experience Manager as a Cloud Service API:er](https://developer.adobe.com/experience-cloud/experience-manager-apis/)
* [GraphQL.org](https://graphql.org)
   * [Scheman](https://graphql.org/learn/schema/)
   * [Variabler](https://graphql.org/learn/queries/#variables)
   * [GraphQL Java-bibliotek](https://graphql.org/code/#java)
* [GraphiQL](https://graphql.org/learn/serving-over-http/#graphiql)
* [Lära sig använda GraphQL med AEM](/help/headless/graphql-api/content-fragments.md)
   * [Aktivera din GraphQL-slutpunkt](/help/headless/graphql-api/graphql-endpoint.md)
   * [Installera AEM GraphiQL-gränssnittet](/help/headless/graphql-api/graphiql-ide.md)
* [Strukturen för exempelinnehållsfragment](/help/headless/graphql-api/sample-queries.md#content-fragment-structure-graphql)
* [Lära sig använda GraphQL med AEM - exempelinnehåll och frågor](/help/headless/graphql-api/sample-queries.md)
   * [Exempelfråga - Ett enskilt specifikt stadsfragment](/help/headless/graphql-api/sample-queries.md#sample-single-specific-city-fragment)
   * [Exempelfråga för metadata - Ange metadata för utmärkelserna med namnet GB](/help/headless/graphql-api/sample-queries.md#sample-metadata-awards-gb)
   * [Exempelfråga - Alla städer med en namngiven variant](/help/headless/graphql-api/sample-queries.md#sample-cities-named-variation)
* [Aktivera funktionen för innehållsfragment i konfigurationsläsaren](/help/sites-cloud/administering/content-fragments/setup.md#enable-content-fragment-functionality-configuration-browser)
* [Arbeta med innehållsfragment](/help/sites-cloud/administering/content-fragments/overview.md)
   * [Modeller för innehållsfragment](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md)
   * [JSON-utdata](/help/assets/content-fragments/content-fragments-json-preview.md)
* [Förstå korsursprunglig resursdelning (CORS)](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html#understand-cross-origin-resource-sharing-(cors))
* [GraphQL Persisted Queries - aktivera cachelagring i Dispatcher](/help/headless/deployment/dispatcher-caching.md)
* [Genererar åtkomsttoken för API:er på serversidan](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md)
* [Komma igång med AEM Headless](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html) - En kort videosjälvstudiekurs med en översikt över hur du använder AEM headless-funktioner, inklusive innehållsmodellering och GraphQL.

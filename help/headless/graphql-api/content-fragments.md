---
title: AEM GraphQL API för användning med innehållsfragment
description: Lär dig hur du använder innehållsfragment i Adobe Experience Manager (AEM) as a Cloud Service med AEM GraphQL API för leverans av headless-innehåll.
feature: Content Fragments,GraphQL API
exl-id: bdd60e7b-4ab9-4aa5-add9-01c1847f37f6
source-git-commit: e43feb24adad7ef16dd92f59ed1f37638febd631
workflow-type: tm+mt
source-wordcount: '2569'
ht-degree: 0%

---


# AEM GraphQL API för användning med innehållsfragment {#graphql-api-for-use-with-content-fragments}

Lär dig hur du använder innehållsfragment i Adobe Experience Manager (AEM) as a Cloud Service med AEM GraphQL API för leverans av headless-innehåll.

AEM as a Cloud Service GraphQL API som används med innehållsfragment är till stor del baserat på standard-API:t GraphQL med öppen källkod.

Genom att använda GraphQL API i AEM kan du effektivt leverera innehållsfragment till JavaScript-klienter i headless CMS-implementeringar:

* Undvika iterativa API-begäranden som REST,
* se till att leveransen begränsas till de specifika kraven,
* Det går att skicka exakt det som behövs för återgivningen som svar på en enda API-fråga.

>[!NOTE]
>
>GraphQL används för närvarande i två (separata) scenarier i Adobe Experience Manager (AEM) as a Cloud Service:
>
>* [AEM Commerce använder data från en handelsplattform via GraphQL](/help/commerce-cloud/integrating/magento.md).
>* AEM Content Fragments fungerar tillsammans med det AEM GraphQL-API:t (en anpassad implementering som baseras på standard GraphQL) för att leverera strukturerat innehåll som kan användas i dina program.


## GraphQL API {#graphql-api}

GraphQL är:

* &quot;*...ett frågespråk för API:er och en körningsmiljö för att utföra dessa frågor med dina befintliga data. GraphQL ger en fullständig och begriplig beskrivning av data i API:t, ger kunderna möjlighet att fråga efter exakt vad de behöver och inget mer, gör det enklare att utveckla API:er över tid och möjliggör kraftfulla utvecklingsverktyg.*&quot;.

   Se [GraphQL.org](https://graphql.org)

* &quot;*...en öppen specifikation för ett flexibelt API-lager. Flytta GraphQL över dina befintliga bakgrunder för att skapa produkter snabbare än någonsin....*&quot;.

   Se [Utforska GraphQL](https://www.graphql.com).

* *&quot;...ett datameddelande och en specifikation som utvecklats internt av Facebook 2012 innan de blev offentligt tillgängliga 2015. Det är ett alternativ till REST-baserade arkitekturer i syfte att öka utvecklarnas produktivitet och minimera mängden data som överförs. GraphQL används i produktion av hundratals organisationer av alla storlekar...&quot;*

   Se [GraphQL Foundation](https://foundation.graphql.org/).

<!--
"*Explore GraphQL is maintained by the Apollo team. Our goal is to give developers and technical leaders around the world all of the tools they need to understand and adopt GraphQL.*". 
-->

Mer information om GraphQL API finns i följande avsnitt (bland många andra resurser):

* At [graphql.org](https://graphql.org):

   * [Introduktion till GraphQL](https://graphql.org/learn)

   * [GraphQL-specifikationen](https://spec.graphql.org/)

* At [graphql.com](https://graphql.com):

   * [Stödlinjer](https://www.graphql.com/guides/)

   * [Tutorials](https://www.graphql.com/tutorials/)

   * [Fallstudier](https://www.graphql.com/case-studies/)

GraphQL för AEM är baserad på standardbiblioteket GraphQL Java Library. Se:

* [graphQL.org - Java](https://graphql.org/code/#java)

* [GraphQL Java vid GitHub](https://github.com/graphql-java)

### GraphQL Terminologi {#graphql-terminology}

GraphQL använder följande:

* **[Frågor](https://graphql.org/learn/queries/)**

* **[Scheman och typer](https://graphql.org/learn/schema/)**:

   * Scheman genereras av AEM baserat på modeller för innehållsfragment.
   * GraphQL visar de typer och åtgärder som tillåts för GraphQL för AEM implementering med dina scheman.

* **[Fält](https://graphql.org/learn/queries/#fields)**

* **[GraphQL-slutpunkt](graphql-endpoint.md)**
   * Den sökväg i AEM som svarar på GraphQL-frågor och ger åtkomst till GraphQL-scheman.

   * Se [Aktivera GraphQL-slutpunkten](graphql-endpoint.md) för mer information.

Se [(GraphQL.org) Introduktion till GraphQL](https://graphql.org/learn/) för utförlig information, inklusive [Bästa praxis](https://graphql.org/learn/best-practices/).

### GraphQL-frågetyper {#graphql-query-types}

Med GraphQL kan du utföra frågor för att returnera:

* A **enkel inmatning**

* A **[lista över poster](https://graphql.org/learn/schema/#lists-and-non-null)**

Du kan också utföra:

* [Beständiga frågor, som är cachelagrade](/help/headless/graphql-api/persisted-queries.md)

### GraphiQL IDE {#graphiql-ide}

Du kan testa och felsöka GraphQL-frågor med [GraphiQL IDE](/help/headless/graphql-api/graphiql-ide.md).

## Användningsexempel för skribent- och publiceringsmiljöer {#use-cases-author-publish-environments}

Användningsexemplen kan bero på vilken typ av AEM as a Cloud Service miljö det är:

* Publiceringsmiljö. används för att:
   * Frågedata för JS-program (standardfall)

* Författarmiljö; används för att:
   * Fråga efter data för&quot;innehållshanteringssyften&quot;:
      * GraphQL i AEM as a Cloud Service är för närvarande ett skrivskyddat API.
      * REST API kan användas för CR(u)D-åtgärder.

## Behörigheter {#permission}

Behörigheterna är de som krävs för åtkomst av resurser.

## Schemagenerering {#schema-generation}

GraphQL är ett starkt typbestämt API, vilket innebär att data måste vara tydligt strukturerade och ordnade efter typ.

GraphQL-specifikationen innehåller en serie riktlinjer för hur du skapar ett robust API för att förhöra data i en viss instans. För att göra detta måste en kund hämta [Schema](#schema-generation), som innehåller alla typer som behövs för en fråga.

För innehållsfragment baseras GraphQL-scheman (struktur och typer) på **Aktiverad** [Modeller för innehållsfragment](/help/assets/content-fragments/content-fragments-models.md) och deras datatyper.

>[!CAUTION]
>
>Alla GraphQL-scheman (härledda från Content Fragment Models som har **Aktiverad**) går att läsa via GraphQL-slutpunkten.
>
>Detta innebär att ni måste se till att inga känsliga uppgifter finns tillgängliga, eftersom de skulle kunna läckas på detta sätt. Detta inkluderar till exempel information som kan finnas som fältnamn i modelldefinitionen.

Om en användare till exempel har skapat en innehållsfragmentmodell som kallas `Article`AEM genererar objektet `article` som är av en typ `ArticleModel`. Fälten i den här typen motsvarar fälten och datatyperna som definieras i modellen.

1. En innehållsfragmentmodell:

   ![Content Fragment Model for use with GraphQL](assets/cfm-graphqlapi-01.png "Content Fragment Model for use with GraphQL")

1. Motsvarande GraphQL-schema (utdata från automatisk GraphiQL-dokumentation):
   ![GraphQL-schema baserat på innehållsfragmentmodell](assets/cfm-graphqlapi-02.png "GraphQL-schema baserat på innehållsfragmentmodell")

   Detta visar att den genererade typen `ArticleModel` innehåller flera [fält](#fields).

   * Tre av dem har kontrollerats av användaren: `author`, `main` och `referencearticle`.

   * De andra fälten lades till automatiskt av AEM och representerar användbara metoder för att tillhandahålla information om ett visst innehållsfragment. i det här exemplet `_path`, `_metadata`, `_variations`. Dessa [hjälpfält](#helper-fields) markeras med föregående `_` för att skilja mellan vad som har definierats av användaren och vad som har genererats automatiskt.

1. När en användare har skapat ett innehållsfragment baserat på artikelmodellen kan det sedan förfrågas via GraphQL. Mer information finns i [Exempelfrågor](/help/headless/graphql-api/sample-queries.md#graphql-sample-queries) (baserat på [sampla innehållsfragmentstruktur för användning med GraphQL](/help/headless/graphql-api/sample-queries.md#content-fragment-structure-graphql)).

Schemat är flexibelt i GraphQL för AEM. Det innebär att den genereras automatiskt varje gång en innehållsfragmentmodell skapas, uppdateras eller tas bort. Cacheminnen för dataschemat uppdateras också när du uppdaterar en innehållsfragmentmodell.

Tjänsten Sites GraphQL lyssnar (i bakgrunden) efter ändringar som gjorts i en innehållsfragmentmodell. När uppdateringar upptäcks återskapas endast den delen av schemat. Denna optimering sparar tid och ger stabilitet.

Om du till exempel:

1. Installera ett paket som innehåller `Content-Fragment-Model-1` och `Content-Fragment-Model-2`:

   1. GraphQL-typer för `Model-1` och `Model-2` kommer att genereras.

1. Ändra sedan `Content-Fragment-Model-2`:

   1. Endast `Model-2` GraphQL-typen uppdateras.

   1. med beaktande av följande: `Model-1` kommer att förbli desamma.

>[!NOTE]
>
>Detta är viktigt att observera om du vill göra satsvisa uppdateringar på modeller för innehållsfragment via REST-API:t, eller på annat sätt.

Schemat hanteras via samma slutpunkt som GraphQL-frågorna, där klienthanteraren anger att schemat anropas med tillägget `GQLschema`. Du kan till exempel utföra en enkel `GET` begäran på `/content/cq:graphql/global/endpoint.GQLschema` resulterar i utdata från schemat med innehållstypen: `text/x-graphql-schema;charset=iso-8859-1`.

### Schemagenerering - opublicerade modeller {#schema-generation-unpublished-models}

När innehållsfragment är kapslade kan det hända att en överordnad Content Fragment Model publiceras, men ingen refererad modell gör det.

>[!NOTE]
>
>Gränssnittet AEM förhindrar detta, men om publiceringen görs programmatiskt eller med innehållspaket kan det ske.

När detta inträffar genererar AEM en *ofullständig* Schema för den överordnade innehållsfragmentmodellen. Det innebär att fragmentreferensen, som är beroende av den opublicerade modellen, tas bort från schemat.

## fält {#fields}

Inom schemat finns det enskilda fält av två baskategorier:

* Fält som du genererar.

   Ett urval av [Fälttyper](#field-types) används för att skapa fält baserat på hur du konfigurerar innehållsfragmentmodellen. Fältnamnen hämtas från **Egenskapsnamn** fält för **Datatyp**.

   * Det finns också **Återge som** Egenskaper som ska beaktas, eftersom användare kan konfigurera vissa datatyper. t.ex. som en enda rad eller som ett multifält.

* GraphQL för AEM genererar även ett antal [hjälpfält](#helper-fields).

   Dessa används för att identifiera ett innehållsfragment eller för att få mer information om ett innehållsfragment.

### Fälttyper {#field-types}

GraphQL för AEM stöder en lista med typer. Alla Content Fragment Model-datatyper som stöds och motsvarande GraphQL-typer visas:

| Content Fragment Model - datatyp | GraphQL-typ | Beskrivning |
|--- |--- |--- |
| Enkelradig text | String, [Sträng] |  Används för enkla strängar som författarnamn, platsnamn osv. |
| Flerradstext | Sträng |  Används för att skriva ut text, t.ex. brödtexten i en artikel |
| Siffra |  Float, [Float] | Används för att visa flyttal och reguljära tal |
| Boolesk |  Boolesk |  Används för att visa kryssrutor → enkla sant/falskt-satser |
| Datum och tid | Kalender |  Används för att visa datum och tid i ett ISO 8086-format. Beroende på vilken typ som valts finns det tre olika varianter att använda i AEM GraphQL: `onlyDate`, `onlyTime`, `dateTime` |
| Uppräkning |  Sträng |  Används för att visa ett alternativ från en lista med alternativ som definieras när modellen skapas |
|  Taggar |  [Sträng] |  Används för att visa en lista över strängar som representerar taggar som används i AEM |
| Innehållsreferens |  Sträng |  Används för att visa sökvägen till en annan resurs i AEM |
| Fragmentreferens |  *En modelltyp* |  Används för att referera till ett annat innehållsfragment av en viss modelltyp, som definieras när modellen skapades |

### Hjälpfält {#helper-fields}

Förutom datatyperna för användargenererade fält genererar GraphQL för AEM även ett antal *hjälpare* fält för att hjälpa till att identifiera ett innehållsfragment eller för att ge ytterligare information om ett innehållsfragment.

#### Bana {#path}

Sökvägsfältet används som en identifierare i GraphQL. Den representerar sökvägen till Content Fragment-resursen i AEM. Vi har valt detta som identifierare för ett innehållsfragment eftersom det:

* är unikt inom AEM,
* kan enkelt hämtas.

I följande kod visas sökvägarna för alla innehållsfragment som har skapats baserat på modellen för innehållsfragment `Person`.

```xml
{
  personList {
    items {
      _path
    }
  }
}
```

Om du vill hämta ett enstaka innehållsfragment av en viss typ måste du också bestämma sökvägen först. till exempel:

```xml
{
  personByPath(_path: "/content/dam/path/to/fragment/john-doe") {
    item {
      _path
      firstName
      name
    }
  }
}
```

Se [Exempelfråga - Ett enskilt specifikt stadsfragment](/help/headless/graphql-api/sample-queries.md#sample-single-specific-city-fragment).

#### Metadata {#metadata}

Via GraphQL visar AEM även metadata för ett innehållsfragment. Metadata är den information som beskriver ett innehållsfragment, till exempel titeln på ett innehållsfragment, miniatyrsökvägen, beskrivningen av ett innehållsfragment och datumet då det skapades, bland annat.

Eftersom metadata genereras via Schemaredigeraren och därför inte har någon särskild struktur, har `TypedMetaData` GraphQL-typen implementerades för att visa metadata för ett innehållsfragment. `TypedMetaData` visar informationen som grupperats med följande skalära typer:

| Fält |
|--- |
| `stringMetadata:[StringMetadata]!` |
| `stringArrayMetadata:[StringArrayMetadata]!` |
| `intMetadata:[IntMetadata]!` |
| `intArrayMetadata:[IntArrayMetadata]!` |
| `floatMetadata:[FloatMetadata]!` |
| `floatArrayMetadata:[FloatArrayMetadata]!` |
| `booleanMetadata:[BooleanMetadata]!` |
| `booleanArrayMetadata:[booleanArrayMetadata]!`  |
| `calendarMetadata:[CalendarMetadata]!` |
| `calendarArrayMetadata:[CalendarArrayMetadata]!` |

Varje skalär typ representerar antingen ett namn/värde-par eller en array med namn/värde-par, där värdet för det paret är av den typ som det grupperades i.

Om du till exempel vill hämta titeln för ett innehållsfragment vet vi att den här egenskapen är en String-egenskap, så vi frågar efter alla strängmetadata:

Så här frågar du efter metadata:

```xml
{
  personByPath(_path: "/content/dam/path/to/fragment/john-doe") {
    item {
      _path
      _metadata {
        stringMetadata {
          name
          value
        }
      }
    }
  }
}
```

Du kan visa alla metadata för GraphQL-typer om du visar det genererade GraphQL-schemat. Alla modelltyper har samma `TypedMetaData`.

>[!NOTE]
>
>**Skillnad mellan normala metadata och arraymetadata**
>Kom ihåg att `StringMetadata` och `StringArrayMetadata` båda hänvisar till vad som lagras i databasen, inte till hur du hämtar dem.
>
>Genom att anropa `stringMetadata` får du en array med alla metadata som lagras i databasen som `String` och om du ringer `stringArrayMetadata` får du en array med alla metadata som lagras i databasen som `String[]`.

Se [Exempelfråga för metadata - Ange metadata för utmärkelserna med namnet GB](/help/headless/graphql-api/sample-queries.md#sample-metadata-awards-gb).

#### Variationer {#variations}

The `_variations` -fältet har implementerats för att förenkla frågor om variationer som ett innehållsfragment har. Till exempel:

```xml
{
  personByPath(_path: "/content/dam/path/to/fragment/john-doe") {
    item {
      _variations
    }
  }
}
```

Se [Exempelfråga - Alla städer med en namngiven variant](/help/headless/graphql-api/sample-queries.md#sample-cities-named-variation).

<!--
## Security Considerations {#security-considerations}
-->

## GraphQL-variabler {#graphql-variables}

GraphQL tillåter att variabler placeras i frågan. Mer information finns i [GraphQL-dokumentation för variabler](https://graphql.org/learn/queries/#variables).

Om du till exempel vill hämta alla innehållsfragment av typen `Article` som har en viss variant kan du ange variabeln `variation` i GraphiQL.

![GraphQL-variabler](assets/cfm-graphqlapi-03.png "GraphQL-variabler")

```xml
### query
query GetArticlesByVariation($variation: String!) {
    articleList(variation: $variation) {
        items {
            _path
            author
        }
    }
}
 
### in query variables
{
    "variation": "Introduction"
}
```

## GraphQL-direktiv {#graphql-directives}

I GraphQL finns det en möjlighet att ändra frågan baserat på variabler, så kallade GraphQL-direktiv.

Du kan till exempel inkludera `adventurePrice` fält i en fråga för alla `AdventureModels`, baserat på en variabel `includePrice`.

![GraphQL-direktiv](assets/cfm-graphqlapi-04.png "GraphQL-direktiv")

```xml
### query
query GetAdventureByType($includePrice: Boolean!) {
  adventureList {
    items {
      adventureTitle
      adventurePrice @include(if: $includePrice)
    }
  }
}
 
### in query variables
{
    "includePrice": true
}
```

## Filtrering {#filtering}

Du kan också använda filtrering i GraphQL-frågor för att returnera specifika data.

Vid filtrering används en syntax som baseras på logiska operatorer och uttryck.

Följande (grundläggande) fråga filtrerar till exempel alla personer som har namnet `Jobs` eller `Smith`:

```xml
query {
  personList(filter: {
    name: {
      _logOp: OR
      _expressions: [
        {
          value: "Jobs"
        },
        {
          value: "Smith"
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

Ytterligare exempel finns i:

* information om [GraphQL för AEM tillägg](#graphql-extensions)

* [Exempelfrågor med detta exempelinnehåll och -struktur](/help/headless/graphql-api/sample-queries.md#graphql-sample-queries-sample-content-fragment-structure)

   * Och [Exempelinnehåll och struktur](/help/headless/graphql-api/sample-queries.md#content-fragment-structure-graphql) förberedda för användning i provfrågor

* [Exempelfrågor baserade på WKND-projektet](/help/headless/graphql-api/sample-queries.md#sample-queries-using-wknd-project)

## GraphQL för AEM - Sammanfattning av tillägg {#graphql-extensions}

Den grundläggande åtgärden för frågor med GraphQL för AEM följer standarden GraphQL-specifikation. För GraphQL-frågor med AEM finns det några tillägg:

* Om du behöver ett enda resultat:
   * använda modellnamnet, eg stad

* Om du förväntar dig en resultatlista:
   * add `List` till modellnamnet, till exempel  `cityList`
   * Se [Exempelfråga - All information om alla städer](#sample-all-information-all-cities)

* Om du vill använda ett logiskt OR:
   * use ` _logOp: OR`
   * Se [Exempelfråga - Alla personer som har namnet &quot;Jobs&quot; eller &quot;Smith&quot;](#sample-all-persons-jobs-smith)

* Logiskt AND finns också, men är (ofta) implicit

* Du kan fråga efter fältnamn som motsvarar fälten i innehållsfragmentmodellen
   * Se [Exempelfråga - Fullständig information om företagets VD och anställda](#sample-full-details-company-ceos-employees)

* Förutom fälten från modellen finns det vissa systemgenererade fält (föregås av understreck):

   * För innehåll:

      * `_locale` : för att avslöja språket, baserat på Language Manager
         * Se [Exempelfråga för flera innehållsfragment för en viss språkinställning](#sample-wknd-multiple-fragments-given-locale)
      * `_metadata` : för att visa metadata för ditt fragment
         * Se [Exempelfråga för metadata - Ange metadata för utmärkelserna med namnet GB](#sample-metadata-awards-gb)
      * `_model` : tillåt frågor för en innehållsfragmentmodell (sökväg och rubrik)
         * Se [Exempelfråga för en innehållsfragmentmodell från en modell](#sample-wknd-content-fragment-model-from-model)
      * `_path` : sökvägen till ditt innehållsfragment i databasen
         * Se [Exempelfråga - Ett enskilt specifikt stadsfragment](#sample-single-specific-city-fragment)
      * `_reference` : avslöja referenser, inkludera textbundna referenser i RTF-redigeraren
         * Se [Exempelfråga för flera innehållsfragment med förhämtade referenser](#sample-wknd-multiple-fragments-prefetched-references)
      * `_variation` : för att visa specifika variationer i ditt innehållsfragment
         * Se [Exempelfråga - Alla städer med en namngiven variant](#sample-cities-named-variation)
   * Och åtgärder:

      * `_operator` : tillämpa särskilda operatörer, `EQUALS`, `EQUALS_NOT`, `GREATER_EQUAL`, `LOWER`, `CONTAINS`, `STARTS_WITH`
         * Se [Exempelfråga - Alla personer som inte har namnet &quot;Jobs&quot;](#sample-all-persons-not-jobs)
         * Se [Exempelfråga - Alla annonser där `_path` börjar med ett visst prefix](#sample-wknd-all-adventures-cycling-path-filter)
      * `_apply` : tillämpa särskilda villkor, till exempel  `AT_LEAST_ONCE`
         * Se [Exempelfråga - Filtrera en array med ett objekt som måste förekomma minst en gång](#sample-array-item-occur-at-least-once)
      * `_ignoreCase` : för att ignorera skiftläget vid fråga
         * Se [Exempelfråga - Alla städer med SAN i namnet, oavsett fall](#sample-all-cities-san-ignore-case)









* Det finns stöd för unionstyper för GraphQL:

   * use `... on`
      * Se [Exempelfråga för ett innehållsfragment för en viss modell med en innehållsreferens](#sample-wknd-fragment-specific-model-content-reference)

* Reservation vid fråga om kapslade fragment:

   * Om en viss variant inte finns i ett kapslat fragment, kommer **Överordnad** variationen skulle returneras.

## Fråga GraphQL-slutpunkten från en extern webbplats {#query-graphql-endpoint-from-external-website}

Om du vill komma åt GraphQL-slutpunkten från en extern webbplats måste du konfigurera:

* [CORS-filter](/help/headless/deployment/cross-origin-resource-sharing.md)
* [Referensfilter](/help/headless/deployment/referrer-filter.md)

## Autentisering {#authentication}

Se [Autentisering för AEM GraphQL-frågor om innehållsfragment](/help/headless/security/authentication.md).

<!-- to be addressed later -->

<!--
## Sorting {#sorting}
-->

<!-- to be addressed later -->

<!--
## Paging {#paging}
-->

## Vanliga frågor {#faqs}

Frågor som har uppstått:

1. **Q**: &quot;*Hur skiljer sig GraphQL API för AEM från Query Builder API?*&quot;

   * **A**: &quot;*AEM GraphQL API ger total kontroll över JSON-utdata och är en branschstandard för att fråga efter innehåll.
AEM planerar att investera i det AEM GraphQL-API:t.*&quot;

## Självstudiekurs - Komma igång med AEM Headless och GraphQL {#tutorial}

Söker du en praktisk självstudiekurs? Checka ut [Komma igång med AEM Headless och GraphQL](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html) en komplett självstudiekurs som visar hur du bygger upp och exponerar innehåll med AEM GraphQL API:er och som används av en extern app i ett headless CMS-scenario.

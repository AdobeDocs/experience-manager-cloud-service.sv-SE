---
title: AEM GraphQL API för användning med innehållsfragment
description: Lär dig hur du använder innehållsfragment i Adobe Experience Manager (AEM) as a Cloud Service med AEM GraphQL API för leverans av headless-innehåll.
feature: Content Fragments,GraphQL API
exl-id: bdd60e7b-4ab9-4aa5-add9-01c1847f37f6
source-git-commit: 17b0604cb192a375c3097255812c89caa8580d5b
workflow-type: tm+mt
source-wordcount: '4173'
ht-degree: 0%

---


# AEM GraphQL API för användning med innehållsfragment {#graphql-api-for-use-with-content-fragments}

Lär dig hur du använder innehållsfragment i Adobe Experience Manager (AEM) as a Cloud Service med AEM GraphQL API för leverans av headless-innehåll.

AEM as a Cloud Service GraphQL-API som används med innehållsfragment är till stor del baserat på GraphQL-API:t med öppen källkod.

Genom att använda GraphQL API i AEM kan du effektivt leverera innehållsfragment till JavaScript-klienter i headless CMS-implementeringar:

* Undvika iterativa API-begäranden som REST,
* se till att leveransen begränsas till de specifika kraven,
* Det går att skicka exakt det som behövs för återgivningen som svar på en enda API-fråga.

>[!NOTE]
>
>GraphQL används för närvarande i två (separata) scenarier i Adobe Experience Manager (AEM) as a Cloud Service:
>
>* [AEM Commerce använder data från en Commerce-plattform via GraphQL](/help/commerce-cloud/integrating/magento.md).
>* AEM Content Fragments fungerar tillsammans med det AEM GraphQL-API:t (en anpassad implementering som baseras på standard-GraphQL) för att leverera strukturerat innehåll som kan användas i dina program.


## GraphQL API {#graphql-api}

GraphQL är:

* &quot;*...ett frågespråk för API:er och en körningsmiljö för att utföra dessa frågor med dina befintliga data. GraphQL ger en fullständig och begriplig beskrivning av data i API:t, ger kunderna möjlighet att fråga efter exakt vad de behöver och ingenting mer, gör det enklare att utveckla API:er över tid och möjliggör kraftfulla utvecklingsverktyg.*&quot;.

   Se [GraphQL.org](https://graphql.org)

* &quot;*...en öppen specifikation för ett flexibelt API-lager. Placera GraphQL över era befintliga bakgrunder för att skapa produkter snabbare än någonsin ....*&quot;.

   Se [Utforska GraphQL](https://www.graphql.com).

* *&quot;...ett datameddelande och en specifikation som utvecklats internt av Facebook 2012 innan de blev offentligt tillgängliga 2015. Det är ett alternativ till REST-baserade arkitekturer i syfte att öka utvecklarnas produktivitet och minimera mängden data som överförs. GraphQL används i produktionen av hundratals organisationer av alla storlekar..&quot;*

   Se [GraphQL Foundation](https://foundation.graphql.org/).

<!--
"*Explore GraphQL is maintained by the Apollo team. Our goal is to give developers and technical leaders around the world all of the tools they need to understand and adopt GraphQL.*". 
-->

Mer information om GraphQL API finns i följande avsnitt (bland annat på engelska):

* At [graphql.org](https://graphql.org):

   * [Introduktion till GraphQL](https://graphql.org/learn)

   * [GraphQL-specifikationen](https://spec.graphql.org/)

* At [graphql.com](https://graphql.com):

   * [Stödlinjer](https://www.graphql.com/guides/)

   * [Självstudiekurser](https://www.graphql.com/tutorials/)

   * [Fallstudier](https://www.graphql.com/case-studies/)

Implementeringen av GraphQL för AEM baseras på GraphQL Java Library. Se:

* [graphQL.org - Java](https://graphql.org/code/#java)

* [GraphQL Java på GitHub](https://github.com/graphql-java)

### GraphQL Terminologi {#graphql-terminology}

GraphQL använder följande:

* **[Frågor](https://graphql.org/learn/queries/)**

* **[Scheman och typer](https://graphql.org/learn/schema/)**:

   * Scheman genereras av AEM baserat på modeller för innehållsfragment.
   * Med hjälp av dina scheman kan GraphQL presentera de typer och åtgärder som är tillåtna för implementeringen av GraphQL AEM.

* **[Fält](https://graphql.org/learn/queries/#fields)**

* **[GraphQL Endpoint](graphql-endpoint.md)**
   * Sökvägen i AEM som svarar på GraphQL-frågor och ger åtkomst till GraphQL-scheman.

   * Se [Aktivera din GraphQL-slutpunkt](graphql-endpoint.md) för mer information.

Se [(GraphQL.org) Introduktion till GraphQL](https://graphql.org/learn/) för utförlig information, inklusive [Bästa praxis](https://graphql.org/learn/best-practices/).

### GraphQL Query Types {#graphql-query-types}

Med GraphQL kan du utföra frågor för att returnera:

* A **enkel inmatning**

* A **[lista över poster](https://graphql.org/learn/schema/#lists-and-non-null)**

AEM innehåller funktioner för att konvertera frågor (båda typerna) till [Beständiga frågor som kan cachas](/help/headless/graphql-api/persisted-queries.md) av Dispatcher och CDN.

### GraphQL Query Best Practices (Dispatcher and CDN) {#graphql-query-best-practices}

The [Beständiga frågor](/help/headless/graphql-api/persisted-queries.md) är den rekommenderade metod som ska användas för publiceringsinstanser som:

* de cachelagras
* de hanteras centralt av AEM as a Cloud Service

>[!NOTE]
>
>Vanligtvis finns det ingen dispatcher/CDN på författaren, så det är ingen fördel att använda beständiga frågor där. förutom att testa dem.

GraphQL-frågor som använder förfrågningar om POST rekommenderas inte eftersom de inte cachelagras, så i en standardinstans är Dispatcher konfigurerad att blockera sådana frågor.

Även om GraphQL har stöd för GET-förfrågningar kan dessa få träffgränser (till exempel längden på URL:en) som kan undvikas med beständiga frågor.

>[!NOTE]
>
>Om du vill tillåta direkta och/eller POST frågor i Dispatcher kan du be systemadministratören att:
>
>* Skapa en [Cloud Manager-miljövariabel](/help/implementing/cloud-manager/environment-variables.md) anropad `ENABLE_GRAPHQL_ENDPOINT`
>* med värdet `true`


>[!NOTE]
>
>Möjligheten att utföra direkta frågor kan vara föråldrad vid något tillfälle i framtiden.

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

GraphQL-frågor körs med tillstånd från den AEM användaren av den underliggande begäran. Om användaren inte har läsåtkomst till vissa fragment (som lagras som resurser) blir de inte en del av resultatuppsättningen.

Dessutom måste användaren ha åtkomst till en GraphQL-slutpunkt för att kunna köra GraphQL-frågor.

## Schemagenerering {#schema-generation}

GraphQL är ett starkt typbestämt API, vilket innebär att data måste vara tydligt strukturerade och ordnade efter typ.

GraphQL-specifikationen innehåller en serie riktlinjer för hur du skapar ett robust API för att förhöra data i en viss instans. För att göra detta måste en kund hämta [Schema](#schema-generation), som innehåller alla typer som behövs för en fråga.

För innehållsfragment baseras GraphQL-scheman (struktur och typer) på **Aktiverad** [Modeller för innehållsfragment](/help/sites-cloud/administering/content-fragments/content-fragments-models.md) och deras datatyper.

>[!CAUTION]
>
>Alla GraphQL-scheman (härledda från Content Fragment Models som har **Aktiverad**) går att läsa via GraphQL-slutpunkten.
>
>Detta innebär att ni måste se till att inga känsliga uppgifter finns tillgängliga, eftersom de skulle kunna läckas på detta sätt. Detta inkluderar till exempel information som kan finnas som fältnamn i modelldefinitionen.

Om en användare till exempel har skapat en innehållsfragmentmodell som kallas `Article`AEM sedan generera en GraphQL-typ `ArticleModel`. Fälten i den här typen motsvarar fälten och datatyperna som definieras i modellen. Dessutom skapas vissa startpunkter för frågor som arbetar med den här typen, till exempel `articleByPath` eller `articleList`.

1. En innehållsfragmentmodell:

   ![Content Fragment Model for use with GraphQL](assets/cfm-graphqlapi-01.png "Content Fragment Model for use with GraphQL")

1. Motsvarande GraphQL-schema (utdata från den automatiska dokumentationen för GraphiQL):
   ![GraphQL-schema baserat på innehållsfragmentmodell](assets/cfm-graphqlapi-02.png "GraphQL-schema baserat på innehållsfragmentmodell")

   Detta visar att den genererade typen `ArticleModel` innehåller flera [fält](#fields).

   * Tre av dem har kontrollerats av användaren: `author`, `main` och `referencearticle`.

   * De andra fälten lades till automatiskt av AEM och representerar användbara metoder för att tillhandahålla information om ett visst innehållsfragment. i det här exemplet [hjälpfält](#helper-fields)) `_path`, `_metadata`, `_variations`.

1. När en användare har skapat ett innehållsfragment baserat på artikelmodellen kan det sedan förhöras via GraphQL. Mer information finns i [Exempelfrågor](/help/headless/graphql-api/sample-queries.md#graphql-sample-queries) (baserat på [exempelstruktur för innehållsfragment för användning med GraphQL](/help/headless/graphql-api/sample-queries.md#content-fragment-structure-graphql)).

I GraphQL for AEM är schemat flexibelt. Det innebär att den genereras automatiskt varje gång en innehållsfragmentmodell skapas, uppdateras eller tas bort. Cacheminnen för dataschemat uppdateras också när du uppdaterar en innehållsfragmentmodell.

<!-- move the following to a separate "in depth" page -->

Cacheminnen för dataschemat uppdateras också när du uppdaterar en innehållsfragmentmodell.

Tjänsten Sites GraphQL avlyssnar (i bakgrunden) alla ändringar som görs i en innehållsfragmentmodell. När uppdateringar upptäcks återskapas endast den delen av schemat. Denna optimering sparar tid och ger stabilitet.

Om du till exempel:

1. Installera ett paket som innehåller `Content-Fragment-Model-1` och `Content-Fragment-Model-2`:

   1. GraphQL-typer för `Model-1` och `Model-2` kommer att genereras.

1. Ändra sedan `Content-Fragment-Model-2`:

   1. Endast `Model-2` GraphQL Type kommer att uppdateras.

   1. med beaktande av följande: `Model-1` kommer att förbli desamma.

>[!NOTE]
>
>Detta är viktigt att observera om du vill göra satsvisa uppdateringar på modeller för innehållsfragment via REST-API:t, eller på annat sätt.

Schemat hanteras via samma slutpunkt som GraphQL-frågorna, där klienthanteraren hanterar det faktum att schemat anropas med tillägget `GQLschema`. Du kan till exempel utföra en enkel `GET` begäran på `/content/cq:graphql/global/endpoint.GQLschema` resulterar i utdata från schemat med innehållstypen: `text/x-graphql-schema;charset=iso-8859-1`.

<!-- move through to here to a separate "in depth" page -->

### Schemagenerering - opublicerade modeller {#schema-generation-unpublished-models}

När innehållsfragment är kapslade kan det hända att en överordnad Content Fragment Model publiceras, men ingen refererad modell gör det.

>[!NOTE]
>
>Gränssnittet AEM förhindrar detta, men om publiceringen görs programmatiskt eller med innehållspaket kan det ske.

När detta inträffar genererar AEM en *ofullständig* Schema för den överordnade innehållsfragmentmodellen. Det innebär att fragmentreferensen, som är beroende av den opublicerade modellen, tas bort från schemat.

## fält {#fields}

Inom schemat finns det enskilda fält av två baskategorier:

* Fält som du genererar.

   Ett urval av [Datatyper](#Data-types) används för att skapa fält baserat på hur du konfigurerar innehållsfragmentmodellen. Fältnamnen hämtas från **Egenskapsnamn** fält för **Datatyp** -fliken.

   * Det finns också **Återge som** inställning som ska beaktas, eftersom användare kan konfigurera vissa datatyper. Ett textfält med en rad kan till exempel konfigureras att innehålla flera textrader genom att välja `multifield` i listrutan.

* GraphQL for AEM genererar också ett antal [hjälpfält](#helper-fields).

### Datatyper {#data-types}

GraphQL för AEM har stöd för en lista med typer. Alla Content Fragment Model-datatyper som stöds och motsvarande GraphQL-typer visas:

| Content Fragment Model - datatyp | GraphQL Type | Beskrivning |
|--- |--- |--- |
| Enkelradig text | String, [Sträng] | Används för enkla strängar som författarnamn, platsnamn osv. |
| Flerradstext | String, [Sträng] | Används för att skriva ut text, t.ex. brödtexten i en artikel |
| Siffra | Float, [Float] | Används för att visa flyttal och reguljära tal |
| Boolesk | Boolesk | Används för att visa kryssrutor → enkla sant/falskt-satser |
| Datum och tid | Kalender | Används för att visa datum och tid i ett ISO 8601-format. Beroende på vilken typ som valts finns det tre aromer som kan användas i AEM GraphQL: `onlyDate`, `onlyTime`, `dateTime` |
| Uppräkning | Sträng | Används för att visa ett alternativ från en lista med alternativ som definieras när modellen skapas |
| Taggar | [Sträng] | Används för att visa en lista över strängar som representerar taggar som används i AEM |
| Innehållsreferens | String, [Sträng] | Används för att visa sökvägen till en annan resurs i AEM |
| Fragmentreferens | *En modelltyp* | Används för att referera till ett annat innehållsfragment av en viss modelltyp, som definieras när modellen skapades |

### Hjälpfält {#helper-fields}

Förutom datatyperna för användargenererade fält genererar GraphQL för AEM även ett antal *hjälpare* fält för att hjälpa till att identifiera ett innehållsfragment eller för att ge ytterligare information om ett innehållsfragment.

Dessa [hjälpfält](#helper-fields) markeras med föregående `_` för att skilja mellan vad som har definierats av användaren och vad som har genererats automatiskt.

#### Bana {#path}

Sökvägsfältet används som en identifierare i AEM GraphQL. Den representerar sökvägen till Content Fragment-resursen i AEM. Vi har valt detta som identifierare för ett innehållsfragment eftersom det:

* är unikt inom AEM,
* kan enkelt hämtas.

I följande kod visas sökvägarna för alla innehållsfragment som har skapats baserat på modellen för innehållsfragment `Author`, enligt självstudiekursen för WKND.

```graphql
{
  authorList {
    items {
      _path
    }
  }
}
```

Om du vill hämta ett enstaka innehållsfragment av en viss typ måste du också bestämma sökvägen först. Till exempel:

```graphql
{
  authorByPath(_path: "/content/dam/wknd-shared/en/contributors/sofia-sj-berg") {
    item {
      _path
      firstName
      lastName
    }
  }
}
```

Se [Exempelfråga - Ett enskilt specifikt stadsfragment](/help/headless/graphql-api/sample-queries.md#sample-single-specific-city-fragment).

#### Metadata {#metadata}

Via GraphQL visar AEM också metadata för ett innehållsfragment. Metadata är den information som beskriver ett innehållsfragment, till exempel titeln på ett innehållsfragment, miniatyrsökvägen, beskrivningen av ett innehållsfragment och datumet då det skapades, bland annat.

Eftersom metadata genereras via Schemaredigeraren och därför inte har någon särskild struktur, har `TypedMetaData` GraphQL-typ implementerades för att visa metadata för ett innehållsfragment. `TypedMetaData` visar informationen som grupperats med följande skalära typer:

| Fält |
|--- |
| `stringMetadata:[StringMetadata]!` |
| `stringArrayMetadata:[StringArrayMetadata]!` |
| `intMetadata:[IntMetadata]!` |
| `intArrayMetadata:[IntArrayMetadata]!` |
| `floatMetadata:[FloatMetadata]!` |
| `floatArrayMetadata:[FloatArrayMetadata]!` |
| `booleanMetadata:[BooleanMetadata]!` |
| `booleanArrayMetadata:[booleanArrayMetadata]!` |
| `calendarMetadata:[CalendarMetadata]!` |
| `calendarArrayMetadata:[CalendarArrayMetadata]!` |

Varje skalär typ representerar antingen ett namn/värde-par eller en array med namn/värde-par, där värdet för det paret är av den typ som det grupperades i.

Om du till exempel vill hämta titeln för ett innehållsfragment vet vi att den här egenskapen är en String-egenskap, så vi frågar efter alla strängmetadata:

Så här frågar du efter metadata:

```graphql
{
  authorByPath(_path: "/content/dam/wknd-shared/en/contributors/sofia-sj-berg") {
    item {
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

```graphql
{
  authorByPath(_path: "/content/dam/wknd-shared/en/contributors/ian-provo") {
    item {
      _variations
    }
  }
}
```

>[!NOTE]
>
>Observera att `_variations` fältet innehåller inte `master` variation, som tekniskt sett originaldata (refereras som *Överordnad* i användargränssnittet) inte betraktas som en explicit variation.

Se [Exempelfråga - Alla städer med en namngiven variant](/help/headless/graphql-api/sample-queries.md#sample-cities-named-variation).

>[!NOTE]
>
>Om den angivna varianten inte finns för ett innehållsfragment returneras originaldata (som också kallas för den överordnad variationen) som standard (fallback).

<!--
## Security Considerations {#security-considerations}
-->

## GraphQL Variables {#graphql-variables}

GraphQL tillåter att variabler placeras i frågan. Mer information finns i [GraphQL-dokumentation för variabler](https://graphql.org/learn/queries/#variables).

Om du till exempel vill hämta alla innehållsfragment av typen `Author` i en viss variant (om den är tillgänglig) kan du ange argumentet `variation` i GraphiQL.

![GraphQL Variables](assets/cfm-graphqlapi-03.png "GraphQL Variables")

**Fråga**:

```graphql
query($variation: String!) {
  authorList(variation: $variation) {
    items {
      _variation
      lastName
      firstName
    }
  }
}
```

**Frågevariabler**:

```json
{
  "variation": "another"
}
```

Frågan returnerar den fullständiga listan med författare. Författare utan `another` återgår till originaldata (`_variation` kommer att rapportera `master` i detta fall).

Om du vill begränsa listan till författare som anger den angivna varianten (och hoppa över författare som skulle återgå till originaldata) måste du använda en [filter](#filtering):

```graphql
query($variation: String!) {
  authorList(variation: $variation, filter: {
    _variation: {
      _expressions: {
        value: $variation
      }
    }
  }) {
    items {
      _variation
      lastName
      firstName
    }
  }
}
```

## GraphQL-direktiv {#graphql-directives}

I GraphQL finns en möjlighet att ändra frågan baserat på variabler, så kallade GraphQL-direktiv.

Du kan till exempel inkludera `adventurePrice` fält i en fråga för alla `AdventureModels`, baserat på en variabel `includePrice`.

![GraphQL-direktiv](assets/cfm-graphqlapi-04.png "GraphQL-direktiv")

**Fråga**:

```graphql
query GetAdventureByType($includePrice: Boolean!) {
  adventureList {
    items {
      title
      price @include(if: $includePrice)
    }
  }
}
```

**Frågevariabler**:

```json
{
    "includePrice": true
}
```

## Filtrering {#filtering}

Du kan också använda filtrering i dina GraphQL-frågor för att returnera specifika data.

Vid filtrering används en syntax som baseras på logiska operatorer och uttryck.

Den mest atomiska delen är ett enstaka uttryck som kan tillämpas på innehållet i ett visst fält. Innehållet i fältet jämförs med ett givet konstantvärde.

Ta t ex följande uttryck

```graphql
{
  value: "some text"
  _op: EQUALS
}
```

skulle jämföra innehållet i fältet med värdet `some text` och lyckas om innehållet är lika med värdet. Annars misslyckas uttrycket.

Följande operatorer kan användas för att jämföra fält med ett visst värde:

| Operator | Typ(er) | Uttrycket lyckas om ... |
|--- |--- |--- |
| `EQUALS` | `String`, `ID`, `Boolean` | ... värdet är exakt detsamma som fältets innehåll |
| `EQUALS_NOT` | `String`, `ID` | ... värdet är *not* samma som fältets innehåll |
| `CONTAINS` | `String` | ... innehållet i fältet innehåller värdet (`{ value: "mas", _op: CONTAINS }` matchar `Christmas`, `Xmas`, `master`, ...) |
| `CONTAINS_NOT` | `String` | ... fältets innehåll *not* innehåller värdet |
| `STARTS_WITH` | `ID` | ... ID:t börjar med ett visst värde (`{ value: "/content/dam/", _op: STARTS_WITH` matchar `/content/dam/path/to/fragment`, men inte `/namespace/content/dam/something` |
| `EQUAL` | `Int`, `Float` | ... värdet är exakt detsamma som fältets innehåll |
| `UNEQUAL` | `Int`, `Float` | ... värdet är *not* samma som fältets innehåll |
| `GREATER` | `Int`, `Float` | ... innehållet i fältet är större än värdet |
| `GREATER_EQUAL` | `Int`, `Float` | ... innehållet i fältet är större än eller lika med värdet |
| `LOWER` | `Int`, `Float` | ... innehållet i fältet är lägre än värdet |
| `LOWER_EQUAL` | `Int`, `Float` | ... innehållet i fältet är mindre än eller lika med värdet |
| `AT` | `Calendar`, `Date`, `Time` | ... innehållet i fältet är exakt detsamma som värdet (inklusive tidszonsinställning) |
| `NOT_AT` | `Calendar`, `Date`, `Time` | ... innehållet i fältet är *not* samma som värdet |
| `BEFORE` | `Calendar`, `Date`, `Time` | ... den tidpunkt som anges av värdet är före den tidpunkt som anges av fältets innehåll |
| `AT_OR_BEFORE` | `Calendar`, `Date`, `Time` | ... den tidpunkt som anges av värdet är före eller vid samma tidpunkt som anges av fältets innehåll |
| `AFTER` | `Calendar`, `Date`, `Time` | ... den tidpunkt som anges av värdet är efter den tidpunkt som anges av fältets innehåll |
| `AT_OR_AFTER` | `Calendar`, `Date`, `Time` | ... den tidpunkt som anges av värdet är efter eller vid samma tidpunkt som anges av fältets innehåll |

I vissa typer kan du även ange ytterligare alternativ som ändrar hur ett uttryck utvärderas:

| Alternativ | Typ(er) | Beskrivning |
|--- |--- |--- |
| `_ignoreCase` | `String` | Ignorerar skiftläget för en sträng, t.ex. värdet `time` matchar `TIME`, `time`, `tImE`, ... |
| `_sensitiveness` | `Float` | Tillåter en viss marginal för `float` värden som ska anses vara desamma (för att kringgå tekniska begränsningar på grund av den interna representationen av `float` Värden. bör undvikas eftersom detta alternativ kan ha en negativ inverkan på prestandan |

Uttryck kan kombineras till en uppsättning med hjälp av en logisk operator (`_logOp`):

* `OR` - uttrycksuppsättningen lyckas om minst ett uttryck lyckas
* `AND` - uttrycksuppsättningen lyckas om alla uttryck lyckas (standard)

Varje fält kan filtreras med en egen uppsättning uttryck. Uttrycksuppsättningarna för alla fält som omnämns i filterargumentet kombineras till slut av den egna logiska operatorn.

En filterdefinition (skickas som `filter` argument till en fråga) innehåller:

* En underdefinition för varje fält (fältet kan nås via sitt namn, t.ex. finns det en `lastName` i filtret för `lastName` i fältet Data (fälttyp)
* Varje underdefinition innehåller `_expressions` -array som innehåller uttrycksuppsättningen och `_logOp` fält som definierar den logiska operatorn ska uttrycken kombineras med
* Varje uttryck definieras av värdet (`value` fält) och operatorn (`_operator` fält) innehållet i ett fält ska jämföras med

Observera att du kan utesluta `_logOp` om du vill kombinera objekt med `AND` och `_operator` om du vill kontrollera likhet, eftersom det här är standardvärdena.

I följande exempel visas en fullständig fråga som filtrerar alla personer som har en `lastName` av `Provo` eller innehåller `sjö`, oberoende av omständigheterna:

```graphql
{
  authorList(filter: {
    lastname: {
      _logOp: OR
      _expressions: [
        {
          value: "sjö",
          _operator: CONTAINS,
          _ignoreCase: true
        },
        {
          value: "Provo"
        }
      ]
    }
  }) {
    items {
      lastName
      firstName
    }
  }
}
```

Du kan även filtrera efter kapslade fält, men det rekommenderas inte eftersom det kan leda till prestandaproblem.

Ytterligare exempel finns i:

* information om [GraphQL för AEM tillägg](#graphql-extensions)

* [Exempelfrågor med detta exempelinnehåll och -struktur](/help/headless/graphql-api/sample-queries.md#graphql-sample-queries-sample-content-fragment-structure)

   * Och [Exempelinnehåll och struktur](/help/headless/graphql-api/sample-queries.md#content-fragment-structure-graphql) förberedda för användning i provfrågor

* [Exempelfrågor baserade på WKND-projektet](/help/headless/graphql-api/sample-queries.md#sample-queries-using-wknd-project)

## Sortering {#sorting}

Med den här funktionen kan du sortera frågeresultaten efter ett angivet fält.

Sorteringskriterierna:

* är en kommaavgränsad lista med värden som representerar fältsökvägen
   * det första fältet i listan definierar den primära sorteringsordningen, det andra fältet används om två värden för det primära sorteringsvillkoret är lika, det tredje om de första två kriterierna är lika, osv.
   * punktnotation, t.ex. field1.subfield.subfield osv.
* med valfri orderriktning
   * ASC (stigande) eller DESC (fallande). som standard används ASC
   * Riktningen kan anges per fält. det innebär att du kan sortera ett fält i stigande ordning och ett annat i fallande ordning (name, firstName DESC)

Till exempel:

```graphql
query {
  authorList(sort: "lastName, firstName") {
    items {
      firstName
      lastName
    }
  }
}
```

Och dessutom:

```graphql
{
  authorList(sort: "lastName DESC, firstName DESC") {
    items {
        lastName
        firstName
    }
  }
}
```

<!-- to be included? -->

Du kan även sortera ett fält i ett kapslat fragment med formatet `nestedFragmentname.fieldname`.

>[!NOTE]
>
>Detta kan ha en negativ inverkan på prestandan.

Till exempel:

```graphql
query {
  articleList(sort: "authorFragment.lastName")  {
    items {
      title
      authorFragment {
        firstName
        lastName
        birthDay
      }
      slug
    }
  }
}
```

## Sidindelning {#paging}

Med den här funktionen kan du utföra sidindelning på frågetyper som returnerar en lista. Det finns två metoder:

* `offset` och `limit` i en `List` fråga
* `first` och `after` i en `Paginated` fråga

### Listfråga - förskjutning och begränsning {#list-offset-limit}

I en `...List`fråga som du kan använda `offset` och `limit` om du vill returnera en viss delmängd av resultaten:

* `offset`: Anger den första datauppsättningen som ska returneras
* `limit`: Anger det maximala antalet datauppsättningar som ska returneras

Om du till exempel vill visa en resultatsida som innehåller upp till fem artiklar, med början från den femte artikeln från *complete* resultatlista:

```graphql
query {
   articleList(offset: 5, limit: 5) {
    items {
      authorFragment {
        lastName
        firstName
      }
    }
  }
}
```

<!-- When available link to BP and replace "JCR query level" with a more neutral term. -->

<!-- When available link to BP and replace "JCR query result set" with a more neutral term. -->

>[!NOTE]
>
>* Sidindelning kräver en stabil sorteringsordning för att fungera korrekt i flera frågor som begär olika sidor i samma resultatuppsättning. Som standard används databassökvägen för varje objekt i resultatuppsättningen för att säkerställa att ordningen alltid är densamma. Om en annan sorteringsordning används, och om sorteringen inte kan göras på JCR-frågenivå, kommer det att få en negativ prestandapåverkan eftersom hela resultatuppsättningen måste läsas in i minnet innan sidorna kan bestämmas.
>
>* Ju högre förskjutning, desto längre tid tar det att hoppa över objekten från den fullständiga JCR-frågeresultatuppsättningen. En alternativ lösning för stora resultatuppsättningar är att använda den numrerade frågan med `first` och `after` -metod.


### Sidnumrerad fråga - första och efter {#paginated-first-after}

The `...Paginated` frågetypen återanvänder de flesta `...List` frågetypsfunktioner (filtrering, sortering), men i stället för att använda `offset`/`limit` argument, använder `first`/`after` argument som definieras av [GraphQL Cursor Connections Specification](https://relay.dev/graphql/connections.htm). Du hittar en mindre formell introduktion i [GraphQL introduktion](https://graphql.org/learn/pagination/#pagination-and-edges).

* `first`: The `n` de första objekten som ska returneras.
Standardvärdet är `50`.
Max antal är `100`.
* `after`: Den markör som bestämmer början på den begärda sidan. Observera att det objekt som markören representerar inte ingår i resultatuppsättningen. markören för ett objekt bestäms av `cursor` fält för `edges` struktur.

Du kan till exempel skriva ut en resultatsida som innehåller upp till fem äventyr, med början från det angivna markörobjektet i *complete* resultatlista:

```graphql
query {
    adventurePaginated(first: 5, after: "ODg1MmMyMmEtZTAzMy00MTNjLThiMzMtZGQyMzY5ZTNjN2M1") {
        edges {
          cursor
          node {
            title
          }
        }
        pageInfo {
          endCursor
          hasNextPage
        }
    }
}
```

<!-- When available link to BP -->
<!-- Due to internal technical constraints, performance will degrade if sorting and filtering is applied on nested fields. Therefore it is recommended to use filter/sort fields stored at root level. For more information, see the [Best Practices document](link). -->

>[!NOTE]
>
>* Som standard för sidindelning använder du UUID för databasnoden som representerar fragmentet för att säkerställa att resultatordningen alltid är densamma. När `sort` används UUID implicit för att säkerställa en unik sortering, även för två objekt med identiska sorteringsnycklar.
>
>* På grund av interna tekniska begränsningar försämras prestanda om sortering och filtrering tillämpas på kapslade fält. Därför bör du använda filter-/sorteringsfält som lagras på rotnivå. Detta är också det rekommenderade sättet om du vill fråga stora sidnumrerade resultatuppsättningar.


## GraphQL for AEM - i korthet {#graphql-extensions}

Den grundläggande funktionen för frågor med GraphQL för AEM följer GraphQL standardspecifikation. För GraphQL-frågor med AEM finns det några tillägg:

* Om du förväntar dig en resultatlista:
   * add `List` till modellnamnet, till exempel  `cityList`
   * Se [Exempelfråga - All information om alla städer](/help/headless/graphql-api/sample-queries.md#sample-all-information-all-cities)

   Då kan du:

   * [Sortera resultaten](#sorting)

      * `ASC` : stigande
      * `DESC` : fallande
   * Returnera en resultatsida med antingen:

      * [En listfråga med förskjutning och begränsning](#list-offset-limit)
      * [En sidnumrerad fråga med första och efter](#paginated-first-after)
   * Se [Exempelfråga - All information om alla städer](/help/headless/graphql-api/sample-queries.md#sample-all-information-all-cities)



* Om du behöver ett enda resultat:
   * använda modellnamnet, eg stad

* Om du förväntar dig en resultatlista:
   * add `List` till modellnamnet, till exempel  `cityList`
   * Se [Exempelfråga - All information om alla städer](/help/headless/graphql-api/sample-queries.md#sample-all-information-all-cities)

* Om du vill använda ett logiskt OR:
   * use ` _logOp: OR`
   * Se [Exempelfråga - Alla personer som har namnet &quot;Jobs&quot; eller &quot;Smith&quot;](/help/headless/graphql-api/sample-queries.md#sample-all-persons-jobs-smith)

* Logiskt AND finns också, men är (ofta) implicit

* Du kan fråga efter fältnamn som motsvarar fälten i innehållsfragmentmodellen
   * Se [Exempelfråga - Fullständig information om företagets VD och anställda](/help/headless/graphql-api/sample-queries.md#sample-full-details-company-ceos-employees)

* Förutom fälten från modellen finns det vissa systemgenererade fält (föregås av understreck):

   * För innehåll:

      * `_locale` : för att avslöja språket, baserat på Language Manager
         * Se [Exempelfråga för flera innehållsfragment för en viss språkinställning](/help/headless/graphql-api/sample-queries.md#sample-wknd-multiple-fragments-given-locale)
      * `_metadata` : för att visa metadata för ditt fragment
         * Se [Exempelfråga för metadata - Ange metadata för utmärkelserna med namnet GB](/help/headless/graphql-api/sample-queries.md#sample-metadata-awards-gb)
      * `_model` : tillåt frågor för en innehållsfragmentmodell (sökväg och rubrik)
         * Se [Exempelfråga för en innehållsfragmentmodell från en modell](/help/headless/graphql-api/sample-queries.md#sample-wknd-content-fragment-model-from-model)
      * `_path` : sökvägen till ditt innehållsfragment i databasen
         * Se [Exempelfråga - Ett enskilt specifikt stadsfragment](/help/headless/graphql-api/sample-queries.md#sample-single-specific-city-fragment)
      * `_reference` : avslöja referenser, inkludera textbundna referenser i RTF-redigeraren
         * Se [Exempelfråga för flera innehållsfragment med förhämtade referenser](/help/headless/graphql-api/sample-queries.md#sample-wknd-multiple-fragments-prefetched-references)
      * `_variation` : för att visa specifika variationer i ditt innehållsfragment

         >[!NOTE]
         >
         >Om den angivna varianten inte finns för ett innehållsfragment returneras den överordnad varianten som ett (fallback) standardvärde.

         * Se [Exempelfråga - Alla städer med en namngiven variant](#sample-cities-named-variation)
   * Och åtgärder:

      * `_operator` : tillämpa särskilda operatörer, `EQUALS`, `EQUALS_NOT`, `GREATER_EQUAL`, `LOWER`, `CONTAINS`, `STARTS_WITH`
         * Se [Exempelfråga - Alla personer som inte har namnet &quot;Jobs&quot;](/help/headless/graphql-api/sample-queries.md#sample-all-persons-not-jobs)
         * Se [Exempelfråga - Alla annonser där `_path` börjar med ett visst prefix](/help/headless/graphql-api/sample-queries.md#sample-wknd-all-adventures-cycling-path-filter)
      * `_apply` : tillämpa särskilda villkor, till exempel  `AT_LEAST_ONCE`
         * Se [Exempelfråga - Filtrera en array med ett objekt som måste förekomma minst en gång](/help/headless/graphql-api/sample-queries.md#sample-array-item-occur-at-least-once)
      * `_ignoreCase` : för att ignorera skiftläget vid fråga
         * Se [Exempelfråga - Alla städer med SAN i namnet, oavsett fall](/help/headless/graphql-api/sample-queries.md#sample-all-cities-san-ignore-case)









* GraphQL-unionstyper stöds:

   * use `... on`
      * Se [Exempelfråga för ett innehållsfragment för en viss modell med en innehållsreferens](/help/headless/graphql-api/sample-queries.md#sample-wknd-fragment-specific-model-content-reference)

* Reservation vid fråga om kapslade fragment:

   * Om en viss variant inte finns i ett kapslat fragment, kommer **Överordnad** variationen skulle returneras.

## Fråga GraphQL-slutpunkten från en extern webbplats {#query-graphql-endpoint-from-external-website}

Om du vill komma åt GraphQL-slutpunkten från en extern webbplats måste du konfigurera:

* [CORS-filter](/help/headless/deployment/cross-origin-resource-sharing.md)
* [Referensfilter](/help/headless/deployment/referrer-filter.md)

## Autentisering {#authentication}

Se [Autentisering för fjärrfrågor AEM GraphQL-frågor om innehållsfragment](/help/headless/security/authentication.md).

## Vanliga frågor {#faqs}

Frågor som har uppstått:

1. **Q**: &quot;*Hur skiljer sig GraphQL API för AEM från Query Builder API?*&quot;

   * **A**: &quot;*AEM GraphQL API ger total kontroll över JSON-utdata och är en branschstandard för att fråga efter innehåll.
AEM planerar att investera i det AEM GraphQL API:t.*&quot;

## Självstudiekurs - Komma igång med AEM Headless och GraphQL {#tutorial}

Söker du en praktisk självstudiekurs? Checka ut [Komma igång med AEM Headless och GraphQL](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html) en komplett självstudiekurs som visar hur man bygger upp och exponerar innehåll med AEM GraphQL API:er och som används av en extern app, i ett headless CMS-scenario.

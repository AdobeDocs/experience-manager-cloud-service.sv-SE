---
title: AEM GraphQL API för användning med innehållsfragment
description: Lär dig hur du använder innehållsfragment i Adobe Experience Manager (AEM) as a Cloud Service med AEM GraphQL API för leverans av headless-innehåll.
feature: Headless, Content Fragments,GraphQL API
exl-id: bdd60e7b-4ab9-4aa5-add9-01c1847f37f6
role: Admin, Developer
source-git-commit: 3789904b4aa1ffa4a039e6b84af64f03f06a3206
workflow-type: tm+mt
source-wordcount: '6021'
ht-degree: 0%

---


# AEM GraphQL API för användning med innehållsfragment {#graphql-api-for-use-with-content-fragments}

>[!IMPORTANT]
>
>Olika funktioner i GraphQL API för användning med innehållsfragment är tillgängliga via Tidiga Adobe-program.
>
>Kontrollera [Versionsinformation](/help/release-notes/release-notes-cloud/release-notes-current.md) om du vill se status och hur du tillämpar den om du är intresserad.

Lär dig hur du använder innehållsfragment i Adobe Experience Manager (AEM) as a Cloud Service med AEM GraphQL API för leverans av headless-innehåll.

AEM as a Cloud Service GraphQL API som används med innehållsfragment är till stor del baserat på GraphQL-API:t med öppen källkod.

Med GraphQL API i AEM kan du effektivt leverera innehållsfragment till JavaScript-klienter i headless CMS-implementeringar:

* Undvika iterativa API-begäranden som REST,
* se till att leveransen begränsas till de specifika kraven,
* Det går att skicka exakt det som behövs för återgivningen som svar på en enda API-fråga.

>[!NOTE]
>
>GraphQL används för närvarande i två (separata) scenarier i Adobe Experience Manager (AEM) as a Cloud Service:
>
>* [AEM Commerce förbrukar data från en Commerce-plattform via GraphQL](/help/commerce-cloud/integrating/magento.md).
>* AEM Content Fragments fungerar tillsammans med AEM GraphQL API (en anpassad implementering som baseras på standard-GraphQL) för att leverera strukturerat innehåll som kan användas i dina program.

>[!NOTE]
>
>Se [AEM API:er för leverans och hantering av strukturerat innehåll](/help/headless/apis-headless-and-content-fragments.md) för en översikt över de olika tillgängliga API:erna och en jämförelse av några av de koncept som ingår.

>[!NOTE]
>
>Den senaste informationen om Experience Manager API:er finns även på [Adobe Experience Manager as a Cloud Service API:er](https://developer.adobe.com/experience-cloud/experience-manager-apis/).

## GRAPHQL API {#graphql-api}

GraphQL är:

* &quot;*...ett frågespråk för API:er och en körningsmiljö för att utföra dessa frågor med dina befintliga data. GraphQL ger en fullständig och begriplig beskrivning av data i ditt API, ger kunderna möjlighet att fråga efter exakt vad de behöver och ingenting mer, gör det enklare att utveckla API:er över tid och aktiverar kraftfulla utvecklingsverktyg.*&quot;.

  Se [GraphQL.org](https://graphql.org)

* &quot;*... en öppen specifikation för ett flexibelt API-lager. Placera GraphQL över era befintliga backend-enheter för att skapa produkter snabbare än någonsin ...*&quot;.

  Se [Utforska GraphQL](https://www.graphql.com).

* *&quot;... ett datamfrågespråk och en specifikation utvecklades internt av Facebook 2012 innan Facebook öppnades offentligt 2015. Det är ett alternativ till REST-baserade arkitekturer i syfte att öka utvecklarnas produktivitet och minimera mängden data som överförs. GraphQL används i produktion av hundratals organisationer av alla storlekar..&quot;*

  Se [GraphQL Foundation](https://foundation.graphql.org/).

<!--
"*Explore GraphQL is maintained by the Apollo team. Our goal is to give developers and technical leaders around the world the tools they need to understand and adopt GraphQL.*". 
-->

Mer information om GraphQL API finns i följande avsnitt (bland annat på engelska):

* Vid [graphql.org](https://graphql.org):

   * [Introduktion till GraphQL](https://graphql.org/learn)

   * [GraphQL-specifikationen](https://spec.graphql.org/)

* På [graphql.com](https://graphql.com):

   * [Stödlinjer](https://www.graphql.com/guides/)

   * [Självstudiekurser](https://www.graphql.com/tutorials/)

   * [Fallstudier](https://www.graphql.com/case-studies/)

Implementeringen av GraphQL för AEM baseras på GraphQL Java Library. Se:

* [graphQL.org - Java](https://graphql.org/code/#java)

* [GraphQL Java vid GitHub](https://github.com/graphql-java)

### GraphQL Terminologi {#graphql-terminology}

GraphQL använder följande:

* **[Frågor](https://graphql.org/learn/queries/)**

* **[Scheman och typer](https://graphql.org/learn/schema/)**:

   * Scheman genereras av AEM baserat på modeller för innehållsfragment.
   * Med hjälp av dina scheman kan GraphQL presentera de typer och åtgärder som är tillåtna för implementeringen av GraphQL för AEM.

* **[Fält](https://graphql.org/learn/queries/#fields)**

* **[GraphQL-slutpunkt](graphql-endpoint.md)**
   * Sökvägen i AEM som svarar på GraphQL-frågor och ger åtkomst till GraphQL-scheman.

   * Mer information finns i [Aktivera GraphQL-slutpunkten](graphql-endpoint.md).

Se [(GraphQL.org) Introduktion till GraphQL](https://graphql.org/learn/) för utförlig information, inklusive [Bästa praxis](https://graphql.org/learn/best-practices/).

### GraphQL Query Types {#graphql-query-types}

Med GraphQL kan du utföra frågor för att returnera:

* En **enkel post**

* En **[lista med poster](https://graphql.org/learn/schema/#lists-and-non-null)**

AEM innehåller funktioner för att konvertera frågor (båda typerna) till [beständiga frågor, som kan cachas](/help/headless/graphql-api/persisted-queries.md) av Dispatcher och CDN.

### GraphQL Query Best Practices (Dispatcher och CDN) {#graphql-query-best-practices}

[Beständiga frågor](/help/headless/graphql-api/persisted-queries.md) är den metod som rekommenderas för publiceringsinstanser som:

* de är cachelagrade
* hanteras de centralt av AEM as a Cloud Service

>[!NOTE]
>
>Vanligtvis finns det ingen dispatcher/CDN på författaren, så det är ingen fördel att använda beständiga frågor där, förutom att testa dem.

GraphQL-frågor som använder POST-begäranden rekommenderas inte eftersom de inte cachelagras, så i en standardinstans är Dispatcher konfigurerat att blockera sådana frågor.

GraphQL stöder även GET-förfrågningar, men dessa kan få träffgränser (till exempel längden på URL:en) som kan undvikas med hjälp av beständiga frågor.

Mer information finns i [Aktivera cachelagring av beständiga frågor](/help/headless/deployment/dispatcher-caching.md).

>[!NOTE]
>
>Om du vill tillåta direkta och/eller POST-frågor i Dispatcher kan du be systemadministratören att:
>
>* Skapa en [Cloud Manager-miljövariabel ](/help/implementing/cloud-manager/environment-variables.md) med namnet `ENABLE_GRAPHQL_ENDPOINT`
>* med värdet `true`

>[!NOTE]
>
>Möjligheten att utföra direkta frågor kan vara föråldrad vid något tillfälle i framtiden.

### GraphiQL IDE {#graphiql-ide}

Du kan testa och felsöka GraphQL-frågor med [GraphiQL IDE](/help/headless/graphql-api/graphiql-ide.md).

## Använd exempel för författare, förhandsgranskning och publicering {#use-cases-author-preview-publish}

Användningsexemplen kan bero på vilken typ av AEM as a Cloud Service-miljö det är:

* Publiceringsmiljö; används för att:
   * Frågedata för JS-program (standardfall)

* Förhandsgranskningsmiljö; används för att:
   * Förhandsgranska frågor innan de distribueras i publiceringsmiljön
      * Frågedata för JS-program (standardfall)

* Författarmiljö, används för att:
   * Fråga efter data för&quot;innehållshanteringssyften&quot;:
      * GraphQL i AEM as a Cloud Service är för närvarande ett skrivskyddat API.
      * REST API kan användas för CR(u)D-åtgärder.

## Behörigheter {#permission}

Behörigheterna är de som krävs för åtkomst till Assets.

GraphQL-frågor körs med tillstånd från AEM-användaren av den underliggande begäran. Om användaren inte har läsåtkomst till vissa fragment (som lagras som Assets) blir de inte en del av resultatuppsättningen.

Användaren måste också ha tillgång till en GraphQL-slutpunkt för att kunna köra GraphQL-frågor.

## Schemagenerering {#schema-generation}

GraphQL är ett högtypat API, vilket innebär att data måste vara tydligt strukturerade och ordnade efter typ.

GraphQL-specifikationen innehåller en serie riktlinjer för hur du skapar ett robust API för att förhöra data i en viss instans. För att kunna göra detta måste en klient hämta [Schema](#schema-generation), som innehåller alla typer som krävs för en fråga.

För innehållsfragment baseras GraphQL-scheman (struktur och typer) på **Enabled** [Content Fragment Models](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md) och deras datatyper.

>[!CAUTION]
>
>Alla GraphQL-scheman (härledda från modeller för innehållsfragment som har **aktiverats**) kan läsas via GraphQL slutpunkt.
>
>Det innebär att du måste se till att inga känsliga data är tillgängliga, eftersom de kan läcka på det här sättet. Detta inkluderar till exempel information som kan finnas som fältnamn i modelldefinitionen.

Om en användare till exempel har skapat en innehållsfragmentmodell med namnet `Article`, genererar AEM en GraphQL-typ `ArticleModel`. Fälten i den här typen motsvarar fälten och datatyperna som definieras i modellen. Dessutom skapas några startpunkter för frågor som arbetar med den här typen, till exempel `articleByPath` eller `articleList`.

1. En innehållsfragmentmodell:

   ![Content Fragment Model for use with GraphQL](assets/cfm-graphqlapi-01.png "Content Fragment Model for use with GraphQL")

1. Motsvarande GraphQL-schema (utdata från den automatiska dokumentationen för GraphiQL):
   ![GraphQL-schema baserat på innehållsfragmentmodell](assets/cfm-graphqlapi-02.png "GraphQL-schema baserat på innehållsfragmentmodell")

   Detta visar att den genererade typen `ArticleModel` innehåller flera [fält](#fields).

   * Tre av dem har kontrollerats av användaren: `author`, `main` och `referencearticle`.

   * De andra fälten lades till automatiskt av AEM och representerar användbara metoder för att tillhandahålla information om ett visst innehållsfragment, i det här exemplet ([hjälpfälten](#helper-fields)) `_path`, `_metadata`, `_variations`.

1. När en användare har skapat ett innehållsfragment baserat på artikelmodellen kan det sedan förhöras via GraphQL. Se till exempel [Exempelfrågor](/help/headless/graphql-api/sample-queries.md#graphql-sample-queries) (baserat på en [innehållsfragmentstruktur som används med GraphQL](/help/headless/graphql-api/sample-queries.md#content-fragment-structure-graphql)).

I GraphQL for AEM är schemat flexibelt. Det innebär att den genereras automatiskt varje gång en innehållsfragmentmodell skapas, uppdateras eller tas bort. Cacheminnen för dataschemat uppdateras också när du uppdaterar en innehållsfragmentmodell.

<!-- move the following to a separate "in depth" page -->

Cacheminnen för dataschemat uppdateras också när du uppdaterar en innehållsfragmentmodell.

Tjänsten Sites GraphQL avlyssnar (i bakgrunden) alla ändringar som görs i en innehållsfragmentmodell. När uppdateringar upptäcks återskapas endast den delen av schemat. Denna optimering sparar tid och ger stabilitet.

Om du till exempel:

1. Installera ett paket som innehåller `Content-Fragment-Model-1` och `Content-Fragment-Model-2`:

   1. GraphQL-typer för `Model-1` och `Model-2` genereras.

1. Ändra sedan `Content-Fragment-Model-2`:

   1. Endast GraphQL-typen `Model-2` kommer att uppdateras.

   1. `Model-1` kommer att förbli densamma.

>[!NOTE]
>
>Detta är viktigt att observera om du vill göra satsvisa uppdateringar på modeller för innehållsfragment via REST-API:t, eller på annat sätt.

Schemat hanteras via samma slutpunkt som GraphQL-frågorna, där klienthanteraren hanterar det faktum att schemat anropas med tillägget `GQLschema`. Om du till exempel utför en enkel `GET`-begäran på `/content/cq:graphql/global/endpoint.GQLschema` resulterar det i utdata från schemat med innehållstypen `text/x-graphql-schema;charset=iso-8859-1`.

<!-- move through to here to a separate "in depth" page -->

### Schemagenerering - opublicerade modeller {#schema-generation-unpublished-models}

När innehållsfragment är kapslade kan det hända att en överordnad Content Fragment Model publiceras, men ingen refererad modell gör det.

>[!NOTE]
>
>AEM gränssnitt förhindrar detta, men om publiceringen görs programmatiskt eller med innehållspaket kan det ske.

När detta inträffar genererar AEM ett *ofullständigt*-schema för den överordnade innehållsfragmentmodellen. Det innebär att fragmentreferensen, som är beroende av den opublicerade modellen, tas bort från schemat.

## Fält {#fields}

Inom schemat finns det enskilda fält av två baskategorier:

* Fält som du genererar.

  Ett urval av [datatyper](#Data-types) används för att skapa fält baserat på hur du konfigurerar innehållsfragmentmodellen. Fältnamnen hämtas från fältet **Egenskapsnamn** på fliken **Datatyp**.

   * Det finns också en inställning för **Återge som** som ska beaktas, eftersom användare kan konfigurera vissa datatyper. Ett textfält med en rad kan till exempel konfigureras att innehålla flera enkelradstexter genom att välja `multifield` i listrutan.

* GraphQL för AEM genererar även flera [hjälpfält](#helper-fields).

### Datatyper {#data-types}

GraphQL för AEM har stöd för en lista med typer. Alla Content Fragment Model-datatyper som stöds och motsvarande GraphQL-typer visas:

| Content Fragment Model - datatyp | GraphQL Type | Beskrivning |
|--- |--- |--- |
| Enkelradig text | `String`, `[String]` | Används för enkla strängar som författarnamn, platsnamn och så vidare. |
| Flerradstext | `String`, `[String]` | Används för att skriva ut text, t.ex. brödtexten i en artikel |
| Nummer | `Float`, `[Float]` | Används för att visa flyttal och reguljära tal |
| Boolean | `Boolean` | Används för att visa kryssrutor → enkla sant/falskt-satser |
| Datum och tid | `Calendar` | Används för att visa datum och tid i ett ISO 8601-format. Beroende på vilken typ som valts finns det tre olika varianter att använda i AEM GraphQL: `onlyDate`, `onlyTime`, `dateTime` |
| Uppräkning | `String` | Används för att visa ett alternativ från en lista med alternativ som definieras när modellen skapas |
| Taggar | `[String]` | Används för att visa en lista över strängar som representerar taggar som används i AEM |
| Innehållsreferens | `String`, `[String]` | Används för att visa sökvägen till en annan resurs i AEM |
| Innehållsreferens (UUID) | `String`, `[String]` | Används för att visa sökvägen, som representeras av ett UUID mot en annan resurs i AEM |
| Fragmentreferens |  *En modelltyp* <br><br>Ett fält: `Model` - Modelltyp, refererad direkt <br><br>Multifält, med en refererad typ: `[Model]` - Array av typen `Model`, refererad direkt från matris <br><br>Multifält, med flera refererade typer: `[AllFragmentModels]` - Array med alla modelltyper, refererad från matris med unionstyp |  Används för att referera till en eller flera innehållsfragment av vissa modelltyper, som definieras när modellen skapades |
| Fragmentreferens (UUID) |  *En modelltyp* <br><br>Ett fält: `Model` - Modelltyp, refererad direkt <br><br>Multifält, med en refererad typ: `[Model]` - Array av typen `Model`, refererad direkt från matris <br><br>Multifält, med flera refererade typer: `[AllFragmentModels]` - Array med alla modelltyper, refererad från matris med unionstyp |  Används för att referera till en eller flera innehållsfragment av vissa modelltyper, som definieras när modellen skapades |

{style="table-layout:auto"}

### Hjälpfält {#helper-fields}

Förutom datatyperna för användargenererade fält genererar GraphQL för AEM även flera *hjälpfält* som hjälper till att identifiera ett innehållsfragment eller att tillhandahålla ytterligare information om ett innehållsfragment.

Dessa [hjälpfält](#helper-fields) är markerade med en `_` som föregår vad som har definierats av användaren och vad som har genererats automatiskt.

#### Bana {#path}

Sökvägsfältet används som en identifierare i AEM GraphQL. Den representerar sökvägen till Content Fragment-resursen i AEM-databasen. Vi har valt detta som identifierare för ett innehållsfragment eftersom det:

* är unikt inom AEM,
* kan enkelt hämtas.

I följande kod visas sökvägarna för alla innehållsfragment som har skapats baserat på innehållsfragmentmodellen `Author`, som tillhandahålls av WKND-självstudien.

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

#### ID (UUID) {#id-uuid}

ID-fältet används också som identifierare i AEM GraphQL. Den representerar sökvägen till Content Fragment-resursen i AEM-databasen, men i stället för att innehålla den faktiska sökvägen finns det ett UUID som representerar resursen. Vi har valt detta som identifierare för ett innehållsfragment eftersom det:

* är unikt inom AEM,
* kan enkelt hämtas,
* ändras inte när resursen flyttas.

UUID för ett innehållsfragment och för ett refererat innehållsfragment, eller resurs, kan returneras via JSON-egenskapen `_id`.

```graphql
{
  articleList {
    items {
        _id
        _path
    }
  }
}
```

#### Metadata {#metadata}

Via GraphQL visar AEM även metadata för ett innehållsfragment. Metadata är den information som beskriver ett innehållsfragment, till exempel titeln på ett innehållsfragment, miniatyrsökvägen, beskrivningen av ett innehållsfragment och datumet då det skapades, bland annat.

Eftersom metadata genereras via Schemaredigeraren och därför inte har någon specifik struktur, implementerades GraphQL-typen `TypedMetaData` för att visa metadata för ett innehållsfragment. `TypedMetaData` visar information grupperad efter följande skalärtyper:

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
>Tänk på att både `StringMetadata` och `StringArrayMetadata` refererar till det som lagras i databasen, inte till hur du hämtar det.
>
>Om du till exempel anropar fältet `stringMetadata` får du en array med alla metadata som lagrats i databasen som `String` , och om du anropar `stringArrayMetadata` får du en array med alla metadata som lagrats i databasen som `String[]`.

Se [Exempelfråga för metadata - Visa en lista över metadata för utdelade med namnet GB](/help/headless/graphql-api/sample-queries.md#sample-metadata-awards-gb).

#### Variationer {#variations}

Fältet `_variations` har implementerats för att förenkla frågor om variationer som ett innehållsfragment har. Till exempel:

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
>Fältet `_variations` innehåller inte någon `master`-variant, eftersom originaldata (som refereras till som *Master* i användargränssnittet) inte betraktas som en explicit variant.

Se [Exempelfråga - Alla städer med en namngiven variant](/help/headless/graphql-api/sample-queries.md#sample-cities-named-variation).

>[!NOTE]
>
>Om den angivna variationen inte finns för ett innehållsfragment returneras originaldata (kallas även huvudvariant) som ett (reservformat) standardvärde.

<!--
## Security Considerations {#security-considerations}
-->

## GraphQL Variables {#graphql-variables}

GraphQL tillåter att variabler placeras i frågan. Mer information finns i [GraphQL-dokumentation för variabler](https://graphql.org/learn/queries/#variables).

Om du till exempel vill hämta alla innehållsfragment av typen `Author` i en viss variant (om tillgängligt) kan du ange argumentet `variation` i GraphiQL.

![GraphQL-variabler](assets/cfm-graphqlapi-03.png "GraphQL-variabler")

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

Frågan returnerar den fullständiga listan med författare. Författare utan varianten `another` återgår till originaldata (`_variation` rapporterar `master` i det här fallet).

Använd ett [filter](#filtering) om du vill begränsa listan till författare som anger den angivna varianten (och hoppa över författare som skulle återgå till originaldata):

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

## GraphQL Direktiv {#graphql-directives}

I GraphQL finns en möjlighet att ändra frågan baserat på variabler, så kallade GraphQL-direktiv.

Där kan du till exempel inkludera fältet `adventurePrice` i en fråga för alla `AdventureModels`, baserat på variabeln `includePrice`.

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

Uttrycket

```graphql
{
  value: "some text"
  _op: EQUALS
}
```

skulle jämföra innehållet i fältet med värdet `some text` och lyckas om innehållet är lika med värdet. Annars kommer uttrycket att misslyckas.

Följande operatorer kan användas för att jämföra fält med ett visst värde:

| Operator | Typ(er) | Uttrycket lyckas om ... |
|--- |--- |--- |
| `EQUALS` | `String`, `ID`, `Boolean` | ... värdet är exakt detsamma som innehållet i fältet |
| `EQUALS_NOT` | `String`, `ID` | ... värdet är *inte* detsamma som innehållet i fältet |
| `CONTAINS` | `String` | ... innehållet i fältet innehåller värdet (`{ value: "mas", _op: CONTAINS }` matchar `Christmas`, `Xmas`, `master`, ...) |
| `CONTAINS_NOT` | `String` | ... innehållet i fältet innehåller *inte* värdet |
| `STARTS_WITH` | `ID` | ... ID:t börjar med ett visst värde (`{ value: "/content/dam/", _op: STARTS_WITH` matchar `/content/dam/path/to/fragment`, men inte `/namespace/content/dam/something`) |
| `EQUAL` | `Int`, `Float` | ... värdet är exakt detsamma som innehållet i fältet |
| `UNEQUAL` | `Int`, `Float` | ... värdet är *inte* detsamma som innehållet i fältet |
| `GREATER` | `Int`, `Float` | ... fältets innehåll är större än värdet |
| `GREATER_EQUAL` | `Int`, `Float` | ... fältets innehåll är större än eller lika med värdet |
| `LOWER` | `Int`, `Float` | ... fältets innehåll är lägre än värdet |
| `LOWER_EQUAL` | `Int`, `Float` | ... fältets innehåll är lägre än eller lika med värdet |
| `AT` | `Calendar`, `Date`, `Time` | ... fältets innehåll är exakt detsamma som värdet (inklusive tidszonsinställning) |
| `NOT_AT` | `Calendar`, `Date`, `Time` | ... innehållet i fältet är *inte* detsamma som värdet |
| `BEFORE` | `Calendar`, `Date`, `Time` | ... den tidpunkt som anges av värdet ligger före den tidpunkt som anges av fältets innehåll |
| `AT_OR_BEFORE` | `Calendar`, `Date`, `Time` | ... den tidpunkt som anges av värdet är före eller vid samma tidpunkt som anges av fältets innehåll |
| `AFTER` | `Calendar`, `Date`, `Time` | ... tidpunkten som anges av värdet är efter tidpunkten som anges av fältets innehåll |
| `AT_OR_AFTER` | `Calendar`, `Date`, `Time` | ... den tidpunkt som anges av värdet är efter eller vid samma tidpunkt som anges av fältets innehåll |

I vissa typer kan du även ange ytterligare alternativ som ändrar hur ett uttryck utvärderas:

| Alternativ | Typ(er) | Beskrivning |
|--- |--- |--- |
| `_ignoreCase` | `String` | Ignorerar skiftläget för en sträng, till exempel värdet `time` matchar `TIME`, `time`, `tImE`, ... |
| `_sensitiveness` | `Float` | Tillåter en viss marginal för `float`-värden att anses vara densamma (för att kringgå tekniska begränsningar på grund av den interna representationen av `float`-värden). Bör undvikas eftersom det här alternativet kan ha en negativ inverkan på prestandan |

Uttryck kan kombineras till en uppsättning med hjälp av en logisk operator (`_logOp`):

* `OR` - uttrycksuppsättningen lyckas om minst ett uttryck lyckas
* `AND` - uttrycksuppsättningen lyckas om alla uttryck lyckas (standard)

Varje fält kan filtreras med en egen uppsättning uttryck. Uttrycksuppsättningarna för alla fält som omnämns i filterargumentet kombineras till slut av den egna logiska operatorn.

En filterdefinition (skickas som `filter`-argument till en fråga) innehåller:

* En underdefinition för varje fält (fältet kan nås via sitt namn, till exempel finns det ett `lastName`-fält i filtret för fältet `lastName` i datatypen (fältet))
* Varje underdefinition innehåller arrayen `_expressions` som innehåller uttrycksuppsättningen och fältet `_logOp` som definierar den logiska operatorn som uttrycken ska kombineras med
* Varje uttryck definieras av värdet (`value` fält) och operatorn (`_operator` fält) ska innehållet i ett fält jämföras med

Du kan utelämna `_logOp` om du vill kombinera objekt med `AND` och `_operator` om du vill kontrollera om de är lika, eftersom det är standardvärdena.

I följande exempel visas en fullständig fråga som filtrerar alla personer som har `lastName` av `Provo` eller som innehåller `sjö`, oberoende av fallet:

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

* information om [GraphQL för AEM-tillägg](#graphql-extensions)

* [Exempelfrågor med detta exempelinnehåll och -struktur](/help/headless/graphql-api/sample-queries.md#graphql-sample-queries-sample-content-fragment-structure)

   * Och [Exempelinnehållet och strukturen](/help/headless/graphql-api/sample-queries.md#content-fragment-structure-graphql) har förberetts för användning i exempelfrågor

* [Exempelfrågor baserade på WKND-projektet](/help/headless/graphql-api/sample-queries.md#sample-queries-using-wknd-project)

## Sortering {#sorting}

>[!NOTE]
>
>Bästa prestanda får du om du [uppdaterar innehållsfragment för sidindelning och sortering i GraphQL Filtering](/help/headless/graphql-api/graphql-optimized-filtering-content-update.md).

Med den här funktionen kan du sortera frågeresultaten enligt ett angivet fält.

Sorteringskriterierna:

* är en kommaavgränsad lista med värden som representerar fältsökvägen
   * det första fältet i listan definierar den primära sorteringsordningen, det andra fältet används om två värden för det primära sorteringsvillkoret är lika, det tredje om de första två kriterierna är lika, och så vidare.
   * punktnotation, d.v.s. field1.subfield.subfield och så vidare..
* med valfri orderriktning
   * ASC (stigande) eller DESC (fallande); som standard används ASC
   * riktningen kan anges per fält, vilket betyder att du kan sortera ett fält i stigande ordning och ett annat i fallande ordning (namn, firstName DESC)

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

Du kan också sortera på ett fält i ett kapslat fragment med formatet `nestedFragmentname.fieldname`.

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

>[!NOTE]
>
>Bästa prestanda får du om du [uppdaterar innehållsfragment för sidindelning och sortering i GraphQL Filtering](/help/headless/graphql-api/graphql-optimized-filtering-content-update.md).

Med den här funktionen kan du utföra sidindelning på frågetyper som returnerar en lista. Det finns två metoder:

* `offset` och `limit` i en `List`-fråga
* `first` och `after` i en `Paginated`-fråga

### Listfråga - förskjutning och begränsning {#list-offset-limit}

I en `...List`fråga kan du använda `offset` och `limit` för att returnera en viss delmängd av resultaten:

* `offset`: Anger den första datauppsättningen som ska returneras
* `limit`: Anger maximalt antal datauppsättningar som ska returneras

Om du till exempel vill visa en resultatsida som innehåller upp till fem artiklar, med början från den femte artikeln i resultatlistan *complete* :

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
>* Sidindelning kräver en stabil sorteringsordning för att fungera korrekt i flera frågor som begär olika sidor i samma resultatuppsättning. Som standard används databassökvägen för varje objekt i resultatuppsättningen för att säkerställa att ordningen alltid är densamma. Om en annan sorteringsordning används, och om sorteringen inte kan göras på JCR-frågenivå, uppstår en negativ prestandapåverkan eftersom hela resultatuppsättningen måste läsas in i minnet innan sidorna kan bestämmas.
>
>* Ju högre förskjutning, desto längre tid tar det att hoppa över objekten från den fullständiga JCR-frågeresultatuppsättningen. En alternativ lösning för stora resultatuppsättningar är att använda den numrerade frågan med metoden `first` och `after`.

### Sidnumrerad fråga - första och efter {#paginated-first-after}

Frågetypen `...Paginated` återanvänder de flesta av `...List`-frågetypsfunktionerna (filtrering, sortering), men i stället för att använda `offset`/`limit`-argument använder den `first`/`after`-argumenten som definierats av [GraphQL Cursor Connections Specification](https://relay.dev/graphql/connections.htm). En mindre formell introduktion finns i [GraphQL-introduktionen](https://graphql.org/learn/pagination/#pagination-and-edges).

* `first`: De `n` första objekten som ska returneras.
Standardvärdet är `50`.
Det maximala antalet är `100`.
* `after`: Markören som bestämmer början på den begärda sidan. Observera att det objekt som markören representerar inte ingår i resultatmängden. Markören för ett objekt bestäms av fältet `cursor` i strukturen `edges`.

Du kan till exempel skriva ut en resultatsida som innehåller upp till fem äventyr, med början från markörobjektet i resultatlistan *complete* :

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
>* Som standard används UUID för databasnoden som representerar fragmentet för att säkerställa att resultatordningen alltid är densamma. När `sort` används används UUID implicit för att säkerställa en unik sortering, även för två objekt med identiska sorteringsnycklar.
>
>* På grund av interna tekniska begränsningar försämras prestanda om sortering och filtrering tillämpas på kapslade fält. Därför bör du använda filter-/sorteringsfält som lagras på rotnivå. Detta är också det rekommenderade sättet om du vill fråga efter stora sidnumrerade resultatuppsättningar.

## Webboptimerad bildleverans i GraphQL-frågor {#web-optimized-image-delivery-in-graphql-queries}

Med webboptimerad bildleverans kan du använda en Graphql-fråga för att:

* Begär en URL till en DAM-resursbild (refereras av en **innehållsreferens**)

* Skicka parametrar med frågan så att en viss återgivning av bilden genereras och returneras automatiskt

  >[!NOTE]
  >
  >Den angivna återgivningen lagras inte i AEM Assets. Återgivningen genereras och sparas i cache-minnet under en kort period.

* Returnera URL:en som en del av JSON-leveransen

Med AEM kan du

* Skicka [webboptimerad bildleverans](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/web-optimized-image-delivery.html) till GraphQL-frågor.

Det innebär att kommandona tillämpas under frågekörningen, på samma sätt som URL-parametrar på GET-begäranden för dessa bilder.

På så sätt kan du dynamiskt skapa bildåtergivningar för JSON-leverans, vilket innebär att du slipper skapa och lagra dessa återgivningar manuellt i databasen.

Lösningen i GraphQL innebär att man kan

* Begär en URL: använd `_dynamicUrl` på referensen `ImageRef`

* Skicka parametrar: lägg till `_assetTransform` i listhuvudet där dina filter definieras

>[!NOTE]
>
>En **innehållsreferens** kan användas för både DAM-resurser och Dynamic Media-resurser. När du hämtar rätt URL används olika parametrar:
>* `_dynamicUrl` : en DAM-resurs
>* `_dmS7Url` : en dynamisk mediaresurs
> 
>Om resursen som refereras är en DAM-resurs blir värdet för `_dmS7Url` `null`. Se [Leverans av dynamiska mediefiler via URL i GraphQL-frågor](#dynamic-media-asset-delivery-by-url).

### Omformningsbegärans struktur {#structure-transformation-request}

`AssetTransform` (`_assetTransform`) används för att göra URL-omvandlingsbegäranden.

Strukturen och syntaxen är:

* `format`: en uppräkning med alla format som stöds av dess tillägg: GIF, PNG, PNG8, JPG, PJPG, BJPG, WEBP, WEBPLL eller WEBPLY
* `seoName`: en sträng som används som filnamn i stället för nodnamnet
* `crop`: en bildruteunderstruktur, om bredd eller höjd utelämnas, används höjd eller bredd som samma värde
   * `xOrigin`: x-origo för bildrutan och är obligatoriskt
   * `yOrigin`: Bildrutans y-ursprung och är obligatoriskt
   * `width`: ramens bredd
   * `height`: bildrutans höjd
* `size`: en dimensionsunderstruktur, om bredd eller höjd utelämnas, används höjd eller bredd som samma värde
   * `width`: dimensionens bredd
   * `height`: dimensionens höjd
* `rotation`: en uppräkning av alla rotationer som stöds: R90, R180, R270
* `flip`: en uppräkning av HORIZONTAL, VERTICAL, HORIZONTAL_AND_VERTICAL
* `quality`: ett heltal mellan 1 och 100 som anger procentvärdet för bildkvaliteten
* `width`: ett heltal som definierar bredden på utdatabilden men ignoreras av Image Generator
* `preferWebp`: ett booleskt värde som anger om webben är att föredra (standardvärdet är false)

URL-omformningen är tillgänglig för alla frågetyper: efter sökväg, lista eller sidnumrerad.

### Webboptimerad bildleverans med fullständiga parametrar {#web-optimized-image-delivery-full-parameters}

Här följer ett exempel på en fråga med en fullständig uppsättning parametrar:

```graphql
{
  articleList(
    _assetTransform: {
      format:GIF
      seoName:"test"
      crop:{
        xOrigin:10
        yOrigin:20
        width:50
        height:45
      }
      size:{
        height:100
        width:200
      }
      rotation:R90
      flip:HORIZONTAL_AND_VERTICAL
      quality:55
      width:123
      preferWebp:true
    }
  ) {
    items {
      _path
      featuredImage {
        ... on ImageRef {
          _dynamicUrl
        }
      }
    }
  }
}
```

### Webboptimerad bildleverans med en enda frågevariabel {#web-optimized-image-delivery-single-query-variable}

I följande exempel visas användningen av en enda frågevariabel:

```graphql
query ($seoName: String!) {
  articleList(
    _assetTransform: {
      format:GIF
      seoName:$seoName
      crop:{
        xOrigin:10
        yOrigin:20
        width:50
        height:45
      }
      size:{
        height:100
        width:200
      }
      rotation:R90
      flip:HORIZONTAL_AND_VERTICAL
      quality:55
      width:123
      preferWebp:true
    }
  ) {
    items {
      _path
      featuredImage {
        ... on ImageRef {
          _dynamicUrl
        }
      }
    }
  }
}
```

### Webboptimerad bildleverans med flera frågevariabler {#web-optimized-image-delivery-multiple-query-variables}

I följande exempel visas hur flera frågevariabler används:

```graphql
query ($seoName: String!, $format: AssetTransformFormat!) {
  articleList(
    _assetTransform: {
      format:$format
      seoName:$seoName
      crop:{
        xOrigin:10
        yOrigin:20
        width:50
        height:45
      }
      size:{
        height:100
        width:200
      }
      rotation:R90
      flip:HORIZONTAL_AND_VERTICAL
      quality:55
      width:123
      preferWebp:true
    }
  ) {
    items {
      _path
      featuredImage {
        ... on ImageRef {
          _dynamicUrl
        }
      }
    }
  }
}
```

### Webboptimerad begäran om bildleverans via URL {#web-optimized-image-delivery-request-url}

Om du sparar frågan som en beständig fråga (till exempel med namnet `dynamic-url-x`) kan du [köra den beständiga frågan direkt](/help/headless/graphql-api/persisted-queries.md#execute-persisted-query).

Om du till exempel vill köra de tidigare exemplen direkt (sparade som beständiga frågor) använder du följande URL:er:

* [En parameter](#dynamic-image-delivery-single-specified-parameter); Persisted Query med namnet `dynamic-url-x`

   * `http://localhost:4502/graphql/execute.json/wknd-shared/dynamic-url-x;seoName=xxx`

     Svaret ser ut så här:

     ![Bildleverans med parametrar](assets/cfm-graphiql-sample-image-delivery.png "Bildleverans med parametrar")

* [Flera parametrar](#dynamic-image-delivery-multiple-specified-parameters); Beständig fråga med namnet `dynamic`

   * `http://localhost:4502/graphql/execute.json/wknd-shared/dynamic;seoName=billiboy;format=GIF;`

     >[!CAUTION]
     >
     >Den efterföljande `;` måste avslutas för att parameterlistan ska kunna avslutas korrekt.

### Begränsningar för webboptimerad bildleverans {#web-optimized-image-delivery-limitations}

Följande begränsningar finns:

* Modifierare som används för alla bilder i frågan (globala parametrar)

* Cachelagra rubriker

   * Ingen cachelagring av författare
   * Cachelagring vid publicering - max 10 minuters ålder (kan inte ändras av klienten)

## Dynamisk leverans av medieresurser via URL i GraphQL-frågor{#dynamic-media-asset-delivery-by-url}

Med GraphQL for AEM Content Fragments kan du begära en URL till en AEM Dynamic Media-resurs (Scene7) (som refereras av **Content Reference**).

Lösningen i GraphQL innebär att man kan

* använd `_dmS7Url` på referensen `ImageRef`
   * se [Exempelfråga för leverans av dynamiska medieresurser via URL - Bildreferens](#sample-query-dynamic-media-asset-delivery-by-url-imageref)
* använd `_dmS7Url` på flera referenser; `ImageRef`, `MultimediaRef` och `DocumentRef`
   * se [Exempelfråga för leverans av dynamiska medieresurser via URL - flera referenser](#sample-query-dynamic-media-asset-delivery-by-url-multiple-refs)

* använd `_dmS7Url` med funktionen SmartCrop

   * Egenskapen `_smartCrops` visar de Smart Crop-konfigurationer som är tillgängliga för en viss resurs

   * se [Exempelfråga för leverans av dynamiska medieresurser via URL - med smart beskärning](#sample-query-dynamic-media-asset-delivery-by-url-smart-crop)

>[!NOTE]
>
>Därför måste du ha en [dynamisk konfiguration för Media Cloud](/help/assets/dynamic-media/config-dm.md).
>
>Detta lägger till attributen `dam:scene7File` och `dam:scene7Domain` i resursens metadata när den skapas.

>[!NOTE]
>
>En **innehållsreferens** kan användas för både DAM-resurser och Dynamic Media-resurser. När du hämtar rätt URL används olika parametrar:
>
>* `_dmS7Url` : en dynamisk mediaresurs
>* `_dynamicUrl` : en DAM-resurs
> 
>Om resursen som refereras är en Dynamic Media-resurs blir värdet för `_dynamicURL` `null`. Se [webboptimerad bildleverans i GraphQL-frågor](#web-optimized-image-delivery-in-graphql-queries).

### Exempelfråga för leverans av Dynamic Media-resurser via URL - Bildreferens{#sample-query-dynamic-media-asset-delivery-by-url-imageref}

Här följer ett exempel på en fråga:
* för flera innehållsfragment av typen `team` och `person`, returnerar `ImageRef`

```graphql
query allTeams {
  teamList {
    items {
      _path
      title
      teamMembers {
        fullName
        profilePicture {
          __typename
          ... on ImageRef{
            _dmS7Url
            height
            width
          }
        }
      }
    }
  }
} 
```

### Exempelfråga för leverans av Dynamic Media-resurser via URL - Flera referenser{#sample-query-dynamic-media-asset-delivery-by-url-multiple-refs}

Här följer ett exempel på en fråga:
* för flera innehållsfragment av typen `team` och `person`, returnerar `ImageRef`, `MultimediaRef` och `DocumentRef`:

```graphql
query allTeams {
  teamList {
    items {
      _path
      title
      teamMembers {
        fullName
        profilePicture {
          __typename
          ... on ImageRef{
            _dmS7Url
            height
            width
          }
        }
       featureVideo {
          __typename
          ... on MultimediaRef{
            _dmS7Url
            size
          }
        }
      about-me {
          __typename
          ... on DocumentRef{
            _dmS7Url
            _path
          }
        }
      }
    }
  }
}
```

### Exempelfråga för leverans av dynamiska medieresurser via URL - med Smart Crop {#sample-query-dynamic-media-asset-delivery-by-url-smart-crop}

Här följer ett exempel på en fråga:

* för att visa de Smart Crop-konfigurationer som är tillgängliga för de begärda resurserna

```graphql
query allTeams {
  teamList {
    items {
      title
      teamMembers {
        profilePicture {
          ... on ImageRef {
            height
            width
            _dmS7Url
            _smartCrops {
              width
              height
              name
            }
          }
        }
      }
    }
  }
} 
```

## Stöd för dynamiska media för OpenAPI-resurser (Remote Assets) {#dynamic-media-for-openapi-asset-support}

Integreringen av [Fjärrresurser](/help/sites-cloud/administering/content-fragments/authoring.md#reference-remote-assets) gör att du kan referera till Assets, som inte är lokala för den aktuella AEM-instansen, från redigeraren för innehållsfragment. Det implementeras av stödet för OpenAPI-resurser i Content Fragment Editor och GraphQL JSON.

### Exempelfråga för Dynamic Media för OpenAPI-resurser (Remote Assets) {#sample-query-dynamic-media-for-openapi-asset-support}

Här följer ett exempel på en förfrågan:

* för att illustrera konceptet med att referera till fjärrresurser

  ```graphql
  {
    testModelList {
      items {
        remoteasset {
          ... on RemoteRef {
              repositoryId
                  assetId
          }
        }
        multiplecontent {
          ... on ImageRef {
            _path
            _authorUrl
            _publishUrl
          }
          ... on RemoteRef {
              repositoryId
              assetId
          }
        }
      }
      _references {
        ... on ImageRef {
            _path
            _authorUrl
            _publishUrl
          }
          ... on RemoteRef {
              repositoryId
              assetId
          }
      }
    }
  }
  ```

* svaret

  ```graphql
  {
    "data": {
      "testModelList": {
        "items": [
          {
            "remoteasset": {
              "repositoryId": "delivery-p123456-e123456.adobeaemcloud.com",
              "assetId": "urn:aaid:aem:1fb05fe4-c12b-4f85-b1ca-aa92cdbd6a62"
            },
            "multiplecontent": [
              {
                "repositoryId": "delivery-p123456-e123456.adobeaemcloud.com",
                "assetId": "urn:aaid:aem:1fb05fe4-c12b-4f85-b1ca-aa92cdbd6a62"
              },
              {
                "_path": "/content/dam/test-folder/test.jpg",
                "_authorUrl": "http://localhost:4502/content/dam/test-folder/test.jpg",
                "_publishUrl": "http://localhost:4503/content/dam/test-folder/test.jpg"
              }
            ]
          }
        ],
        "_references": [
          {
            "repositoryId": "delivery-p123456-e123456.adobeaemcloud.com",
            "assetId": "urn:aaid:aem:1fb05fe4-c12b-4f85-b1ca-aa92cdbd6a62"
          },
          {
            "_path": "/content/dam/test-folder/test.jpg",
            "_authorUrl": "http://localhost:4502/content/dam/test-folder/test.jpg",
            "_publishUrl": "http://localhost:4503/content/dam/test-folder/test.jpg"
          }
        ]
      }
    }
  }  
  ```

**Begränsningar**

De nuvarande begränsningarna är:

* GraphQL-leverans stöder endast `repositoryId` och `assetId` (andra metadata för resursen returneras inte)

  >[!NOTE]
  >
  >Den fullständiga URL:en måste sedan skapas på klientsidan, baserat på [API:t för resursleverans](https://adobe-aem-assets-delivery.redoc.ly/#operation/getAssetSeoFormat).

* Endast *Godkända* resurser är tillgängliga för referens från fjärrdatabaserna
* Om en resurs som refereras tas bort från fjärrdatabasen resulterar detta i en trasig referens för innehållsfragmentresurser.
* Alla tillgångsdatabaser som användaren har åtkomst till kommer att vara tillgängliga för val. Listan kan inte begränsas.
* Både AEM-instansen och fjärrresurslagringsplatsen måste ha samma version.
* Inga resursmetadata visas via [hanterings-API:t](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/) och [leverans-API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/sites/delivery/). Du måste använda API:t för tillgångsmetadata för att hämta information om objektets metadata.

## GraphQL for AEM - i korthet {#graphql-extensions}

Den grundläggande funktionen för frågor med GraphQL för AEM följer GraphQL standardspecifikation. Det finns några tillägg för GraphQL-frågor med AEM:

* Om du behöver ett enda resultat:
   * använd modellnamnet, till exempel ort

* Om du förväntar dig en resultatlista:
   * lägg till `List` i modellnamnet, till exempel `cityList`
   * Se [Exempelfråga - All information om alla städer](/help/headless/graphql-api/sample-queries.md#sample-all-information-all-cities)

  Då kan du:

   * [Sortera resultaten](#sorting)

      * `ASC`: stigande
      * `DESC` : fallande

   * Returnera en resultatsida med antingen:

      * [En listfråga med förskjutning och begränsning](#list-offset-limit)
      * [En sidnumrerad fråga med första och efter](#paginated-first-after)

   * Se [Exempelfråga - All information om alla städer](/help/headless/graphql-api/sample-queries.md#sample-all-information-all-cities)

* Filtret `includeVariations` ingår i frågetyperna `List` och `Paginated`.  Om du vill hämta variationer för innehållsfragment i frågeresultatet måste filtret `includeVariations` anges till `true`.

   * Se [Exempelfråga för flera innehållsfragment och deras variationer för en viss modell](/help/headless/graphql-api/sample-queries.md#sample-wknd-multiple-fragment-variations-given-model)

  >[!CAUTION]
  >Det går inte att använda filtret `includeVariations` och det systemgenererade fältet `_variation` tillsammans i samma frågedefinition.

* Om du vill använda ett logiskt OR:
   * använd ` _logOp: OR`
   * Se [Exempelfråga - Alla personer som har namnet &quot;Jobs&quot; eller &quot;Smith&quot;](/help/headless/graphql-api/sample-queries.md#sample-all-persons-jobs-smith)

* Logiskt AND finns också, men är (ofta) implicit

* Du kan fråga efter fältnamn som motsvarar fälten i innehållsfragmentmodellen
   * Se [Exempelfråga - fullständig information om ett företags VD och anställda](/help/headless/graphql-api/sample-queries.md#sample-full-details-company-ceos-employees)

* Förutom fälten från modellen finns det vissa systemgenererade fält (föregås av understreck):

   * För innehåll:

      * `_locale` : för att visa språket, baserat på Språkhanteraren
         * Se [Exempelfråga för flera innehållsfragment för en viss språkinställning](/help/headless/graphql-api/sample-queries.md#sample-wknd-multiple-fragments-given-locale)

      * `_metadata` : för att visa metadata för ditt fragment
         * Se [Exempelfråga för metadata - Lista metadata för utdelade med namnet GB](/help/headless/graphql-api/sample-queries.md#sample-metadata-awards-gb)

      * `_model` : tillåt att fråga efter en innehållsfragmentmodell (sökväg och rubrik)
         * Se [Exempelfråga för en innehållsfragmentmodell från en modell](/help/headless/graphql-api/sample-queries.md#sample-wknd-content-fragment-model-from-model)

      * `_path` : sökvägen till ditt innehållsfragment i databasen
         * Se [Exempelfråga - Ett enskilt specifikt stadsfragment](/help/headless/graphql-api/sample-queries.md#sample-single-specific-city-fragment)

      * `_id` : UUID för ditt innehållsfragment i databasen

         * Se [Exempelfråga för ett innehållsfragment av en specifik modell med UUID-referenser](/help/headless/graphql-api/sample-queries.md#sample-wknd-fragment-specific-model-uuid-references)
         * [Se Exempelfråga för innehållsfragment efter UUID-referens](/help/headless/graphql-api/sample-queries.md#sample-wknd-fragment-specific-model-uuid-reference)

      * `_reference` : om du vill visa referenser, inklusive textbundna referenser i RTF-redigeraren
         * Se [Exempelfråga för flera innehållsfragment med förhämtade referenser](/help/headless/graphql-api/sample-queries.md#sample-wknd-multiple-fragments-prefetched-references)

      * `_variation` : om du vill visa specifika variationer i ditt innehållsfragment

        >[!NOTE]
        >
        >Om den angivna variationen inte finns för ett innehållsfragment returneras huvudvarianten som ett (fallback) standardvärde.

        >[!CAUTION]
        >
        >Det systemgenererade fältet `_variation` kan inte användas tillsammans med filtret `includeVariations`.

         * Se [Exempelfråga - Alla städer med en namngiven variant](/help/headless/graphql-api/sample-queries.md#sample-cities-named-variation)

   * För bildleverans:

      * `_authorURL`: den fullständiga URL:en till bildresursen på AEM Author
      * `_publishURL`: den fullständiga URL:en till bildresursen i AEM Publish

      * För [webboptimerad bildleverans](#web-optimized-image-delivery-in-graphql-queries) (av DAM-resurser):

         * `_dynamicUrl`: Den fullständiga URL:en till den webboptimerade DAM-resursen på referensen `ImageRef`

           >[!NOTE]
           >
           >`_dynamicUrl` är den URL som ska användas för webboptimerade DAM-resurser och bör ersätta användningen av `_path`, `_authorUrl` och `_publishUrl` när det är möjligt.

         * `_assetTransform`: för att skicka parametrar i listhuvudet där dina filter definieras

         * Se:

            * [Exempelfråga för webboptimerad bildleverans med fullständiga parametrar](#web-optimized-image-delivery-full-parameters)

            * [Exempelfråga för webboptimerad bildleverans med en enda angiven parameter](#web-optimized-image-delivery-single-query-variable)

      * `_dmS7Url`: på referensen `ImageRef` för leverans av URL:en till en [Dynamic Media-resurs](#dynamic-media-asset-delivery-by-url)

         * Se [Exempelfråga för leverans av dynamiska mediefiler via URL - ImageRef](#sample-query-dynamic-media-asset-delivery-by-url-imageref)

         * Se [Exempelfråga för leverans av dynamiska mediefiler via URL - flera referenser](#sample-query-dynamic-media-asset-delivery-by-url-multiple-refs)

   * `_tags`: om du vill visa ID:n för innehållsfragment eller variationer som innehåller taggar, är detta en array med `cq:tags` identifierare.

      * Se [Exempelfråga - Namn på alla städer som taggats som stadbrytningar](/help/headless/graphql-api/sample-queries.md#sample-names-all-cities-tagged-city-breaks)
      * Se [Exempelfråga för innehållsfragmentvariationer för en given modell som har en specifik tagg bifogad](/help/headless/graphql-api/sample-queries.md#sample-wknd-fragment-variations-given-model-specific-tag)
      * Se [Exempelfråga med filtrering efter _tags-ID och exkludera variationer](/help/headless/graphql-api/sample-queries.md#sample-filtering-tag-not-variations)
      * Se [Exempelfråga med filtrering efter _tags-ID och inklusive variationer](/help/headless/graphql-api/sample-queries.md#sample-filtering-tag-with-variations)

     >[!NOTE]
     >
     >Taggar kan också efterfrågas genom att en lista med metadata för ett innehållsfragment visas.

   * Och åtgärder:

      * `_operator` : använd specifika operatorer; `EQUALS`, `EQUALS_NOT`, `GREATER_EQUAL`, `LOWER`, `CONTAINS`, `STARTS_WITH`
         * Se [Exempelfråga - Alla personer som inte har namnet Jobs](/help/headless/graphql-api/sample-queries.md#sample-all-persons-not-jobs)
         * Se [Exempelfråga - Alla annonser där `_path` börjar med ett visst prefix](/help/headless/graphql-api/sample-queries.md#sample-wknd-all-adventures-cycling-path-filter)

      * `_apply` : om du vill använda särskilda villkor, till exempel `AT_LEAST_ONCE`
         * Se [Exempelfråga - Filtrera en array med ett objekt som måste förekomma minst en gång](/help/headless/graphql-api/sample-queries.md#sample-array-item-occur-at-least-once)

      * `_ignoreCase` : om du vill ignorera skiftläget vid fråga
         * Se [Exempelfråga - Alla städer med SAN i namnet, oavsett fall](/help/headless/graphql-api/sample-queries.md#sample-all-cities-san-ignore-case)

* GraphQL-unionstyper stöds:

   * använd `... on`
      * Se [Exempelfråga för ett innehållsfragment av en viss modell med en innehållsreferens](/help/headless/graphql-api/sample-queries.md#sample-wknd-fragment-specific-model-content-reference)

* Reservation vid fråga om kapslade fragment:

   * Om en angiven variation inte finns i ett kapslat fragment returneras varianten **Master**.

## Fråga GraphQL-slutpunkten från en extern webbplats {#query-graphql-endpoint-from-external-website}

Om du vill komma åt GraphQL-slutpunkten från en extern webbplats måste du konfigurera:

* [CORS-filter](/help/headless/deployment/cross-origin-resource-sharing.md)
* [Referensfilter](/help/headless/deployment/referrer-filter.md)

## Autentisering {#authentication}

Se [Autentisering för AEM GraphQL-fjärrfrågor om innehållsfragment](/help/headless/security/authentication.md).

## Automatiserad testning {#automated-testing}

När du kör en distributionsprocess i AEM Cloud Manager körs automatiska tester under körningen.

För att få korrekta resultat bör din AEM as a Cloud Service **Stage** -miljö spegla din **Production** -miljö så nära som möjligt. Detta är särskilt viktigt för innehåll.

Du kan göra detta genom att använda AEM as a Cloud Service [innehållskopieringsverktyg](/help/implementing/developing/tools/content-copy.md) för att kopiera ditt produktionsinnehåll till scenmiljön.

## Begränsningar {#limitations}

För att skydda dig mot potentiella problem finns det standardbegränsningar för dina frågor:

* Frågan får inte innehålla fler än 1M (1024 * 1024) tecken
* Frågan får inte innehålla fler än 15000 token
* Frågan får inte innehålla fler än 200000 blankstegstoken

Du måste också vara medveten om:

* Ett fältkonfliktsfel returneras när din GraphQL-fråga innehåller fält med samma namn i två (eller flera) modeller och följande villkor uppfylls:

   * Så här:

      * Två (eller flera modeller) används som möjliga referenser, när de definieras som en tillåten **modelltyp** i Content Fragment-referensen.

     och:

      * Dessa två modeller har fält med ett gemensamt namn, vilket betyder att samma namn används i båda modellerna.

     och

      * Dessa fält har olika datatyper.

   * Till exempel:

      * När två (eller flera) fragment med olika modeller (till exempel `M1`, `M2`) används som möjliga referenser (innehållsreferens eller fragmentreferens) från ett annat fragment, till exempel `Fragment1` `MultiField/List`
      * Och dessa två fragment med olika modeller (`M1`, `M2`) har fält med samma namn, men olika typer.
Så här illustrerar du:
         * `M1.Title` som `Text`
         * `M2.Title` som `Text/MultiField`
      * Ett fältkonfliktsfel uppstår sedan om GraphQL-frågan innehåller fältet `Title`.

## Vanliga frågor {#faqs}

Frågor som har uppstått:

1. **Q**: *Hur skiljer sig GraphQL API för AEM från Query Builder API?*

   * **A**:
&quot;*AEM GraphQL API ger total kontroll över JSON-utdata och är en branschstandard för att fråga efter innehåll.
AEM planerar att investera i AEM GraphQL API.*&quot;

## Självstudiekurs - Komma igång med AEM Headless och GraphQL {#tutorial}

Söker du en praktisk självstudiekurs? Ta en titt på [Komma igång med AEM Headless och GraphQL](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html) - en komplett självstudiekurs som visar hur du bygger upp och exponerar innehåll med AEM GraphQL API:er och som används av en extern app i ett headless CMS-scenario.

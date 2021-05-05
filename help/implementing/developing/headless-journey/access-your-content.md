---
title: Få åtkomst till ditt innehåll via AEM-API:er
description: I den här delen av AEM Headless Developer Journey kan du lära dig hur du använder GraphQL-frågor för att komma åt innehållet i innehållsfragment.
hide: true
hidefromtoc: true
index: false
exl-id: 5ef557ff-e299-4910-bf8c-81c5154ea03f
translation-type: tm+mt
source-git-commit: 7b04ae2bfa75fe3d3af13271efe567a5fc401f49
workflow-type: tm+mt
source-wordcount: '4636'
ht-degree: 0%

---

# Så här kommer du åt ditt innehåll via AEM Delivery API:er {#access-your-content}

>[!CAUTION]
>
>ARBETE PÅGÅR - Dokumentet skapas för närvarande och ska inte tolkas som fullständigt eller slutgiltigt och inte heller användas i tillverkningssyfte.

I den här delen av [AEM Headless Developer Journey](overview.md) kan du lära dig hur du använder GraphQL-frågor för att komma åt innehållet i dina innehållsfragment.

## Berättelsen hittills {#story-so-far}

I det föregående dokumentet från den AEM resan, [How to Model Your Content](model-your-content.md), lärde du dig grunderna i datamodellering i AEM, så du bör nu förstå hur du modellerar innehållsstrukturen och sedan inse att strukturen med AEM Content Fragment Models och Content Fragments:

* Identifiera koncept och terminologi relaterade till [datamodellering](#data-modeling).
* Förstå [varför datamodellering krävs för leverans av Headless-innehåll](#data-modeling-for-aem-headless).
* Förstå [hur du realiserar den här strukturen med AEM Content Fragment Models](#create-structure-content-fragment-models) (och redigera innehåll med [Content Fragments](#use-content-to-author-content)).
* Förstå [hur du modellerar innehåll](#getting-started-examples); principer med grundläggande urval.

Den här artikeln bygger på dessa grundläggande funktioner så att du förstår hur du får tillgång till ditt befintliga headless-innehåll i AEM med hjälp av AEM GraphQL API.

* **Målgrupp**: Nybörjare
* **Mål**: Lär dig hur du kommer åt innehållet i dina innehållsfragment med AEM GraphQL-frågor:
   * Introducera GraphQL och AEM GraphQL API.
   * Ta en titt på detaljerna i AEM GraphQL API.
   * Titta på några exempelfrågor för att se hur saker och ting fungerar i praktiken.

## Så du vill komma åt dina data? {#so-youd-like-to-access-your-data}

Så..har du allt det här innehållet, har en struktur (i innehållsfragment) och väntar bara på att mata in din nya app. Frågan är hur man får dit den?

Vad du behöver är ett sätt att rikta specifikt innehåll, välja vad du behöver och returnera det till appen för vidare bearbetning.

Med Adobe Experience Manager (AEM) som Cloud Service kan du selektivt komma åt dina innehållsfragment med hjälp av det AEM GraphQL-API:t och returnera endast det innehåll du behöver. Det innebär att du kan leverera strukturerat innehåll utan extra kostnad och använda det i dina program.

>[!NOTE]
>
>AEM GraphQL API är en anpassad implementering som baseras på standard GraphQL.

## GraphQL - en introduktion {#graphql-introduction}

GraphQL är en öppen källkodsspecifikation som ger:

* ett frågespråk där du kan välja specifikt innehåll från strukturerade objekt.
* en körningsmiljö där du kan utföra dessa frågor med ditt strukturerade innehåll.

GraphQL är ett *starkt*-typat API. Det innebär att *allt*-innehåll måste vara tydligt strukturerat och organiserat efter typ, så att GraphQL *förstår* vad som ska användas och hur. Datafälten definieras i GraphQL-scheman, som definierar strukturen för innehållsobjekten.

GraphQL-slutpunkterna tillhandahåller sedan de sökvägar som svarar på GraphQL-frågor.

Allt detta innebär att appen kan välja de data den behöver korrekt, tillförlitligt och effektivt - precis vad du behöver när du använder AEM.

>[!NOTE]
>
>Se *GraphQL*.org och *GraphQL*.com.

## AEM och GraphQL {#aem-graphql}

GraphQL används på olika platser i AEM. till exempel:

* Handel
   * Det finns GraphQL-integreringar mellan AEM och olika e-handelslösningar från tredje part, som används med de utbyggnadskopplingar som tillhandahålls av CIF Core Components.
* Innehållsfragment
   * Ett anpassat API har utvecklats för det här användningsfallet.
   * Det här är AEM GraphQL API.

>[!NOTE]
>
>Det här steget i Headless Journey gäller endast AEM GraphQL API och innehållsfragment.

## AEM GraphQL API {#aem-graphql-api}

AEM GraphQL API är en anpassad version av standard-API:t GraphQL som är särskilt konfigurerad för att du ska kunna utföra (komplexa) frågor på dina innehållsfragment.

Innehållsfragment används eftersom innehållet är strukturerat enligt modeller för innehållsfragment. Detta uppfyller ett grundläggande krav i GraphQL.

* En innehållsfragmentmodell består av ett eller flera fält.
   * Varje fält definieras enligt en datatyp.
* Content Fragment Models används för att generera motsvarande AEM GraphQL-scheman.

För att komma åt GraphQL för AEM (och innehållet) används en slutpunkt för att ange åtkomstsökvägen.

Innehållet som returneras via AEM GraphQL API kan sedan användas av dina program.

>[!NOTE]
>
>Implementeringen AEM GraphQL API baseras på GraphQL Java-biblioteken.

### Användningsexempel för redigerings- och publiceringsmiljöer {#use-cases-author-publish-environments}

Användningsexemplen för AEM GraphQL API kan vara beroende av vilken typ av AEM som en Cloud Service:

* Publiceringsmiljö. används för att:
   * Frågedata för JS-program (standardfall)

* Författarmiljö; används för att:
   * Fråga efter data för&quot;innehållshanteringssyften&quot;:
      * GraphQL i AEM som en Cloud Service är för närvarande ett skrivskyddat API.
      * REST API kan användas för CR(u)D-åtgärder.

## Innehållsfragment för användning med AEM GraphQL API {#content-fragments-use-with-aem-graphql-api}

Innehållsfragment kan användas som bas för GraphQL för AEM scheman och frågor som:

* Med dem kan du utforma, skapa, strukturera och publicera sidoberoende innehåll.
* De baseras på en Content Fragment Model, som fördefinierar strukturen för det resulterande fragmentet med hjälp av definierade datatyper.
* Ytterligare strukturlager kan uppnås med datatypen Fragmentreferens, som är tillgänglig när du definierar en modell.

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

Om du vill ha hjälp med att utforma och utveckla dina modeller för innehållsfragment kan du förhandsgranska JSON-utdata i redigeraren för innehållsfragment.

## Generering av GraphQL-schema från innehållsfragment {#graphql-schema-generation-content-fragments}

GraphQL är ett starkt typbestämt API, vilket innebär att data måste vara tydligt strukturerade och ordnade efter typ. GraphQL-specifikationen innehåller en serie riktlinjer för hur du skapar ett robust API för att förhöra data i en viss instans. För att göra detta måste klienten hämta schemat, som innehåller alla typer som krävs för en fråga.

För innehållsfragment baseras GraphQL-scheman (struktur och typer) på **Enabled** Content Fragment Models och deras datatyper.

>[!CAUTION]
>
>Alla GraphQL-scheman (härledda från modeller för innehållsfragment som har **aktiverats**) kan läsas via GraphQL-slutpunkten.
>
>Detta innebär att ni måste se till att inga känsliga uppgifter finns tillgängliga, eftersom de skulle kunna läcka ut på detta sätt. Detta inkluderar till exempel information som kan finnas som fältnamn i modelldefinitionen.

Om en användare till exempel har skapat en innehållsfragmentmodell med namnet `Article`, genererar AEM objektet `article` som är av typen `ArticleModel`. Fälten i den här typen motsvarar fälten och datatyperna som definieras i modellen.

1. En innehållsfragmentmodell:

   ![Content Fragment Model for use with ](assets/graphqlapi-cfmodel.png "GraphQLContent Fragment Model for use with GraphQL")

1. Motsvarande GraphQL-schema (utdata från automatisk GraphiQL-dokumentation):
   ![GraphQL-schema baserat på Content Fragment ](assets/graphqlapi-cfm-schema.png "ModelGraphQL-schema baserat på Content Fragment Model")

   Detta visar att den genererade typen `ArticleModel` innehåller flera [fält](#fields).

   * Tre av dem har kontrollerats av användaren: `author`, `main` och `referencearticle`.

   * De andra fälten lades till automatiskt av AEM och representerar användbara metoder för att tillhandahålla information om ett visst innehållsfragment. i det här exemplet är `_path`, `_metadata`, `_variations`. Dessa [hjälpfält](#helper-fields) är markerade med en föregående `_` för att skilja mellan vad som har definierats av användaren och vad som har genererats automatiskt.

1. När en användare har skapat ett innehållsfragment baserat på artikelmodellen kan det sedan förfrågas via GraphQL. Se till exempel exempelfrågor.md#graphql-sample-queries (baserat på en innehållsfragmentstruktur som du kan använda med GraphQL.

Schemat är flexibelt i GraphQL för AEM. Det innebär att den genereras automatiskt varje gång en innehållsfragmentmodell skapas, uppdateras eller tas bort. Cacheminnen för dataschemat uppdateras också när du uppdaterar en innehållsfragmentmodell.

Tjänsten Sites GraphQL lyssnar (i bakgrunden) efter ändringar som gjorts i en innehållsfragmentmodell. När uppdateringar upptäcks återskapas endast den delen av schemat. Denna optimering sparar tid och ger stabilitet.

Om du till exempel:

1. Installera ett paket som innehåller `Content-Fragment-Model-1` och `Content-Fragment-Model-2`:

   1. GraphQL-typer för `Model-1` och `Model-2` genereras.

1. Ändra sedan `Content-Fragment-Model-2`:

   1. Endast GraphQL-typen `Model-2` uppdateras.

   1. `Model-1` kommer att vara detsamma.

>[!NOTE]
>
>Detta är viktigt att observera om du vill göra satsvisa uppdateringar på modeller för innehållsfragment via REST-API:t, eller på annat sätt.

Schemat hanteras via samma slutpunkt som GraphQL-frågorna, med klienten som hanterar det faktum att schemat anropas med tillägget `GQLschema`. Om du till exempel utför en enkel `GET`-begäran på `/content/cq:graphql/global/endpoint.GQLschema` resulterar det i utdata från schemat med innehållstypen: `text/x-graphql-schema;charset=iso-8859-1`.

### Schemagenerering - opublicerade modeller {#schema-generation-unpublished-models}

När innehållsfragment är kapslade kan det hända att en överordnad Content Fragment Model publiceras, men ingen refererad modell gör det.

>[!NOTE]
>
>Gränssnittet AEM förhindrar detta, men om publiceringen görs programmatiskt eller med innehållspaket kan det ske.

När detta inträffar genererar AEM ett *ofullständigt*-schema för den överordnade modellen för innehållsfragment. Det innebär att fragmentreferensen, som är beroende av den opublicerade modellen, tas bort från schemat.

## AEM GraphQL-slutpunkter {#aem-graphql-endpoints}

<!--
need details/examples
-->

En slutpunkt är den bana som används för att komma åt GraphQL för AEM. Med den här sökvägen kan du (eller din app):

* tillgång till GraphQL-scheman,
* skicka GraphQL-frågor,
* ta emot svar (på GraphQL-frågor).

AEM tillåter:

* En global slutpunkt - tillgänglig för användning på alla webbplatser.
* Klientslutpunkter - som du kan konfigurera, specifika för en angiven plats/ett visst projekt.

## Behörigheter {#permissions}

Behörigheterna är de som krävs för åtkomst av resurser.

## AEM GraphiQL-gränssnitt {#aem-graphiql-interface}

En implementering av standardgränssnittet GraphiQL är tillgänglig för användning med GraphQL för att hjälpa dig att direkt mata in och testa frågor. Detta kan installeras med AEM.

Den innehåller funktioner som syntaxmarkering, automatisk komplettering, automatisk föreslå, samt historik och onlinedokumentation.

![Gränssnittet GraphiQL ](assets/graphiql-interface.png "InterfaceGraphiQL")

<!--
new page?
-->

## Använda AEM GraphQL API {#using-aem-graphiql}

### Slutpunkter {#endpoints}

Databassökvägen för GraphQL för AEM globala slutpunkten är:

`/content/cq:graphql/global/endpoint`

För vilken ditt program kan använda följande sökväg i URL:en för begäran:

`/content/_cq_graphql/global/endpoint.json`

För en klientslutpunkt är sökvägarna jämförbara:

`/content/cq:graphql/your-tenant/endpoint`
`/content/_cq_graphql/your-tenant/endpoint.json`

Innan du använder måste alla slutpunkter vara aktiverade. Om du vill aktivera en slutpunkt, global eller tenant, för GraphQL för AEM måste du:

* Aktivera GraphQL-slutpunkten
* Publicera slutpunkten

>[!CAUTION]
>
>Med Content Fragment Editor kan ett innehållsfragment för en klientorganisation referera till ett innehållsfragment för en annan klientorganisation (via policyer).
>
>I så fall går det inte att hämta allt innehåll med en klientspecifik slutpunkt.
>
>Innehållsförfattaren bör kontrollera detta scenario; Det kan till exempel vara bra att överväga att placera delade modeller för innehållsfragment under den globala klienten.

### Aktivera GraphQL-slutpunkten {#enabling-graphql-endpoint}

Om du vill aktivera en GraphQL-slutpunkt måste du först ha en lämplig konfiguration i Configuration Browser.

>[!CAUTION]
>
>Om användningen av innehållsfragmentmodeller inte har aktiverats är alternativet **Skapa** inte tillgängligt.

Så här aktiverar du motsvarande slutpunkt:

1. Navigera till **Verktyg**, **Platser** och välj sedan **GraphQL**.
1. Välj **Skapa**.
1. Dialogrutan **Skapa ny GraphQL-slutpunkt** öppnas. Här kan du ange:
   * **Namn**: Slutpunktens namn. du kan skriva vilken text som helst.
   * **Använd GraphQL-schema från**: Använd listrutan för att välja önskad plats/önskat projekt.

   >[!NOTE]
   >
   >Följande varning visas i dialogrutan:
   >
   >* *GraphQL-slutpunkter kan medföra problem med datasäkerhet och prestanda om de inte hanteras varsamt. Kontrollera att du har angett rätt behörigheter när du har skapat en slutpunkt.*


1. Bekräfta med **Skapa**.
1. Dialogrutan **Nästa steg** innehåller en direktlänk till säkerhetskonsolen så att du kan kontrollera att den nyskapade slutpunkten har rätt behörigheter.

   >[!CAUTION]
   >
   >Slutpunkten är tillgänglig för alla. Detta kan - särskilt när det gäller publiceringsinstanser - utgöra ett säkerhetsproblem, eftersom GraphQL-frågor kan medföra en stor belastning på servern.
   >
   >Du kan ställa in åtkomstkontrollistor, som passar ditt användningsfall, på slutpunkten.

### Publicerar GraphQL-slutpunkten {#publishing-graphql-endpoint}

Markera den nya slutpunkten och **Publicera** för att göra den helt tillgänglig i alla miljöer.

>[!CAUTION]
>
>Slutpunkten är tillgänglig för alla.
>
>På publiceringsinstanser kan detta utgöra ett säkerhetsproblem, eftersom GraphQL-frågor kan medföra en stor belastning på servern.
>
>Du måste konfigurera åtkomstkontrollistor som passar ditt användningsfall på slutpunkten.

### Installera AEM GraphiQL-gränssnitt {#installing-graphiql-interface}

Användargränssnittet GraphiQL kan installeras på AEM med ett dedikerat paket: [Innehållspaketet GraphiQL v0.0.6 (2021.3)](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/aem-graphql/graphiql-0.0.6.zip).

### AEM GraphQL-scheman {#aem-graphql-schemas}

För att få tillgång till dina data måste du först välja önskad typ av innehållsfragmentmodell, som representeras av ett GraphQL-schema. AEM GraphQL-scheman är härledda från dina modeller för innehållsfragment - som kan användas i GraphQL-frågor.

<!--
Confirm is the schema city or CityModel? -->

Om du har en innehållsfragmentmodell med namnet `City` kommer det att finnas ett motsvarande schema med namnet `city`. Du kan använda följande fråga för att lista `name` för alla innehållsfragment som baseras på den här modellen.

```xml
query {
  cityList {
    items {
      name
    }
  }
}
```

Du kan använda följande fråga för att lista `name` och `description` för alla `types` för alla tillgängliga scheman:

```xml
{
  __schema {
    types {
      name
      description
    }
  }
}
```

### AEM GraphQL-fält {#aem-graphql-fields}

När du har valt det schema du behöver, vill du komma åt specifika data - som representeras av fält i schemat.

Inom schemat finns det enskilda fält av två baskategorier:

* Fält som du genererar.

   Ett urval av [fälttyper](#field-types) används för att skapa fält baserat på hur du konfigurerar innehållsfragmentmodellen. Fältnamnen hämtas från fältet **Egenskapsnamn** i **datatypen**.

   * Det finns också egenskapen **Återge som** som ska beaktas, eftersom användare kan konfigurera vissa datatyper; t.ex. som en enda rad eller som ett multifält.

* GraphQL för AEM genererar även ett antal hjälpfält.

   Dessa används för att identifiera ett innehållsfragment eller för att få mer information om ett innehållsfragment.

### Fälttyper {#field-types}

GraphQL för AEM stöder en lista med typer. Alla Content Fragment Model-datatyper som stöds och motsvarande GraphQL-typer visas:

| Content Fragment Model - datatyp | GraphQL-typ | Beskrivning |
|--- |--- |--- |
| Enkelradig text | Sträng, [Sträng] | Används för enkla strängar som författarnamn, platsnamn osv. |
| Flerradstext | Sträng | Används för att skriva ut text, t.ex. brödtexten i en artikel |
| Siffra | Float, [Float] | Används för att visa flyttal och reguljära tal |
| Boolesk | Boolesk | Används för att visa kryssrutor → enkla sant/falskt-satser |
| Datum och tid | Kalender | Används för att visa datum och tid i ett ISO 8086-format. Beroende på vilken typ som valts finns det tre olika varianter att använda i AEM GraphQL: `onlyDate`, `onlyTime`, `dateTime` |
| Uppräkning | Sträng | Används för att visa ett alternativ från en lista med alternativ som definieras när modellen skapas |
| Taggar | [Sträng] | Används för att visa en lista över strängar som representerar taggar som används i AEM |
| Innehållsreferens | Sträng | Används för att visa sökvägen till en annan resurs i AEM |
| Fragmentreferens | *En modelltyp* | Används för att referera till ett annat innehållsfragment av en viss modelltyp, som definieras när modellen skapades |

### Hjälpfält {#helper-fields}

Förutom datatyperna för användargenererade fält genererar GraphQL för AEM även ett antal *hjälpfält*-fält för att hjälpa till att identifiera ett innehållsfragment eller för att ge ytterligare information om ett innehållsfragment.

#### Sökväg {#path}

Sökvägsfältet används som en identifierare i GraphQL. Den representerar sökvägen till Content Fragment-resursen i AEM. Vi har valt detta som identifierare för ett innehållsfragment eftersom det:

* är unikt inom AEM,
* kan enkelt hämtas.

I följande kod visas sökvägarna för alla innehållsfragment som har skapats baserat på innehållsfragmentmodellen `Person`.

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

>[!NOTE]
>
>Se Exempelfråga - Ett enskilt specifikt stadsfragment.

#### Metadata {#metadata}

Via GraphQL visar AEM även metadata för ett innehållsfragment. Metadata är den information som beskriver ett innehållsfragment, till exempel titeln på ett innehållsfragment, miniatyrsökvägen, beskrivningen av ett innehållsfragment och datumet då det skapades, bland annat.

Eftersom metadata genereras via Schemaredigeraren och därför inte har någon specifik struktur, implementerades GraphQL-typen `TypedMetaData` för att visa metadata för ett innehållsfragment. `TypedMetaData` visar informationen som grupperats med följande skalära typer:

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
>Kom ihåg att både `StringMetadata` och `StringArrayMetadata` hänvisar till vad som lagras i databasen, inte till hur du hämtar dem.
>
>Om du till exempel anropar fältet `stringMetadata` får du en array med alla metadata som lagrats i databasen som `String`. Om du anropar `stringArrayMetadata` får du en array med alla metadata som lagrats i databasen som `String[]`.

>[!NOTE]
>
>Se Exempelfråga för metadata - Ange metadata för utmärkelser med namnet GB.

#### Variationer {#variations}

Fältet `_variations` har implementerats för att förenkla frågor om variationerna som ett innehållsfragment har. Till exempel:

```xml
{
  personByPath(_path: "/content/dam/path/to/fragment/john-doe") {
    item {
      _variations
    }
  }
}
```

>[!NOTE]
>
>Se Exempelfråga - Alla städer med en namngiven variant.

### AEM GraphQL-variabler {#aem-graphql-variables}

Variabler är användbara i alla typer av programmering, eller frågor, eftersom de gör att du kan lagra olika värden på en plats. För AEM GraphQL innebär detta att du, i stället för att behöva skriva en separat fråga för varje värde, kan skriva frågan för en variabel och variabelns värde kan ändras om det behövs.

GraphQL tillåter att variabler placeras i frågan.

>[!NOTE]
>
>Mer information finns i dokumentationen för GraphQL för variabler.

Om du till exempel vill hämta alla innehållsfragment av typen `Article` som har en viss variation, kan du ange variabeln `variation` i GraphiQL. Alla instanser hämtas i `GetArticlesByVariation` och skickas sedan för användning i `articleList`.

![Variabler för GraphQL ](assets/graphqlapi-variables.png "VariablesGraphQL")

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
    "variation": "uk"
}
```

### AEM GraphQL-direktiv {#aem-graphql-directives}

I GraphQL finns det en möjlighet att ändra frågan baserat på variabler, så kallade GraphQL-direktiv.

Där kan du till exempel inkludera fältet `adventurePrice` i en fråga för alla `AdventureModels`, baserat på variabeln `includePrice`.

!![GraphQL Directives](assets/graphqlapi-directl .png &quot;GraphQL directs&quot;)

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

### AEM GraphQL-filter {#aem-graphql-filters}

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

* information om GraphQL för AEM tillägg

* Exempelfrågor med detta exempelinnehåll och -struktur

### AEM GraphQL-tillägg {#aem-graphql-extensions}

Den grundläggande åtgärden för frågor med GraphQL för AEM följer standarden GraphQL-specifikation. För GraphQL-frågor med AEM finns det några tillägg:

* Om du behöver ett enda resultat:
   * använda modellnamnet, eg stad

* Om du förväntar dig en resultatlista:
   * lägg till `List` i modellnamnet; till exempel `cityList`
   * Se [Exempelfråga - All information om alla städer](#sample-all-information-all-cities)

* Om du vill använda ett logiskt OR:
   * use ` _logOp: OR`
   * Se [Exempelfråga - Alla personer som har namnet &quot;Jobs&quot; eller &quot;Smith&quot;](#sample-all-persons-jobs-smith)

* Logiskt AND finns också, men är (ofta) implicit

* Du kan fråga efter fältnamn som motsvarar fälten i innehållsfragmentmodellen
   * Se [Exempelfråga - Fullständig information om ett företags VD och anställda](#sample-full-details-company-ceos-employees)

* Förutom fälten från modellen finns det vissa systemgenererade fält (föregås av understreck):

   * För innehåll:

      * `_locale` : för att avslöja språket, baserat på Language Manager
         * Se [Exempelfråga för flera innehållsfragment för en viss språkinställning](#sample-wknd-multiple-fragments-given-locale)
      * `_metadata` : för att visa metadata för ditt fragment
         * Se [Exempelfråga för metadata - Lista metadata för utmärkelser med namnet GB](#sample-metadata-awards-gb)
      * `_model` : tillåt frågor för en innehållsfragmentmodell (sökväg och rubrik)
         * Se [Exempelfråga för en innehållsfragmentmodell från en modell](#sample-wknd-content-fragment-model-from-model)
      * `_path` : sökvägen till ditt innehållsfragment i databasen
         * Se [Exempelfråga - Ett enskilt specifikt stadsfragment](#sample-single-specific-city-fragment)
      * `_reference` : avslöja referenser, inkludera textbundna referenser i RTF-redigeraren
         * Se [Exempelfråga för flera innehållsfragment med förhämtade referenser](#sample-wknd-multiple-fragments-prefetched-references)
      * `_variation` : för att visa specifika variationer i ditt innehållsfragment
         * Se [Exempelfråga - Alla städer med en namngiven variant](#sample-cities-named-variation)
   * Och åtgärder:

      * `_operator` : tillämpa särskilda operatörer,  `EQUALS`,  `EQUALS_NOT`,  `GREATER_EQUAL`,  `LOWER`,  `CONTAINS`,  `STARTS_WITH`
         * Se [Exempelfråga - Alla personer som inte har namnet &quot;Jobs&quot;](#sample-all-persons-not-jobs)
         * Se [Exempelfråga - Alla annonser där `_path` börjar med ett visst prefix](#sample-wknd-all-adventures-cycling-path-filter)
      * `_apply` : tillämpa särskilda villkor, till exempel   `AT_LEAST_ONCE`
         * Se [Exempelfråga - Filtrera en array med ett objekt som måste finnas minst en gång](#sample-array-item-occur-at-least-once)
      * `_ignoreCase` : för att ignorera skiftläget vid fråga
         * Se [Exempelfråga - Alla städer med SAN i namnet, oavsett fall](#sample-all-cities-san-ignore-case)









* Det finns stöd för unionstyper för GraphQL:

   * använd `... on`
      * Se [Exempelfråga för ett innehållsfragment av en viss modell med en innehållsreferens](#sample-wknd-fragment-specific-model-content-reference)

### Beständiga frågor (cachelagring) {#persisted-queries-caching}

När en fråga har förberetts med en begäran om POST kan den köras med en GET-begäran som kan cachas av HTTP-cacher eller ett CDN.

Detta är nödvändigt eftersom POST-frågor vanligtvis inte cachelagras, och om GET med frågan används som parameter finns det en stor risk för att parametern blir för stor för HTTP-tjänster och mellanhänder.

Beständiga frågor måste alltid använda den slutpunkt som är relaterad till lämplig (klientorganisation) konfiguration. så att de kan använda antingen eller båda:

* Den globala konfigurationen och slutpunkten
Frågan har åtkomst till alla modeller för innehållsfragment.
* Specifika klientkonfigurationer och slutpunkter
Om du vill skapa en beständig fråga för en viss klientkonfiguration måste du ha en motsvarande klientspecifik slutpunkt (för att ge åtkomst till relaterade modeller för innehållsfragment).
Om du till exempel vill skapa en beständig fråga specifikt för WKND-klienten, måste en motsvarande WKND-specifik klientkonfiguration och en WKND-specifik slutpunkt skapas i förväg.

>[!NOTE]
>
>Mer information finns i Aktivera funktionen för innehållsfragment i Configuration Browser.
>
>**GraphQL Persistence Queries** måste aktiveras för rätt klientkonfiguration.

Om det till exempel finns en viss fråga med namnet `my-query` som använder modellen `my-model` från klientkonfigurationen `my-conf`:

* Du kan skapa en fråga med den `my-conf` specifika slutpunkten och sedan sparas frågan så här:
   `/conf/my-conf/settings/graphql/persistentQueries/my-query`
* Du kan skapa samma fråga med hjälp av `global`-slutpunkten, men sedan sparas frågan så här:
   `/conf/global/settings/graphql/persistentQueries/my-query`

>[!NOTE]
>
>Det här är två olika frågor - sparade under olika sökvägar.
>
>De råkar bara använda samma modell, men via olika slutpunkter.

Här följer de steg som krävs för att behålla en given fråga:

1. Förbered frågan genom att PUTing den till den nya slutpunkts-URL:en `/graphql/persist.json/<config>/<persisted-label>`.

   Skapa till exempel en beständig fråga:

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query" \
       -d \
   '{
     articleList {
       items{
           _path
           author
           main {
               json
           }
       }
     }
   }'
   ```

1. Kontrollera svaret nu.

   Kontrollera till exempel om åtgärden lyckades:

   ```xml
   {
     "action": "create",
     "configurationName": "wknd",
     "name": "plain-article-query",
     "shortPath": "/wknd/plain-article-query",
     "path": "/conf/wknd/settings/graphql/persistentQueries/plain-article-query"
   }
   ```

1. Du kan sedan spela upp den beständiga frågan igen genom att GETa URL:en `/graphql/execute.json/<shortPath>`.

   Använd till exempel den beständiga frågan:

   ```xml
   $ curl -X GET \
       http://localhost:4502/graphql/execute.json/wknd/plain-article-query
   ```

1. Uppdatera en beständig fråga genom POSTing till en redan befintlig frågesökväg.

   Använd till exempel den beständiga frågan:

   ```xml
   $ curl -X POST \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query" \
       -d \
   '{
     articleList {
       items{
           _path
           author
           main {
               json
           }
         referencearticle {
           _path
         }
       }
     }
   }'
   ```

1. Skapa en omsluten vanlig fråga.

   Till exempel:

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-wrapped" \
       -d \
   '{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }"}'
   ```

1. Skapa en omsluten oformaterad fråga med cachekontroll.

   Till exempel:

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-max-age" \
       -d \
   '{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }", "cache-control": { "max-age": 300 }}'
   ```

1. Skapa en beständig fråga med parametrar:

   Till exempel:

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-parameters" \
       -d \
   'query GetAsGraphqlModelTestByPath($apath: String!, $withReference: Boolean = true) {
     articleByPath(_path: $apath) {
       item {
         _path
           author
           main {
           plaintext
           }
           referencearticle @include(if: $withReference) {
           _path
           }
         }
       }
     }'
   ```

1. Kör en fråga med parametrar.

   Till exempel:

   ```xml
   $ curl -X POST \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters;apath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"
   
   $ curl -X GET \
       "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters;apath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"
   ```

1. Om du vill köra frågan vid publicering måste det relaterade beständiga trädet replikeras

   * Använda en POST för replikering:

      ```xml
      $curl -X POST   http://localhost:4502/bin/replicate.json \
        -H 'authorization: Basic YWRtaW46YWRtaW4=' \
        -F path=/conf/wknd/settings/graphql/persistentQueries/plain-article-query \
        -F cmd=activate
      ```

   * Använda ett paket:
      1. Skapa en ny paketdefinition.
      1. Inkludera konfigurationen (till exempel `/conf/wknd/settings/graphql/persistentQueries`).
      1. Bygg paketet.
      1. Replikera paketet.
   * Använda replikerings-/distributionsverktyget.
      1. Gå till distributionsverktyget.
      1. Välj trädaktivering för konfigurationen (till exempel `/conf/wknd/settings/graphql/persistentQueries`).
   * Använda ett arbetsflöde (via konfiguration för att starta arbetsflöde):
      1. Definiera en startregel för arbetsflöde för att köra en arbetsflödesmodell som skulle återge konfigurationen för olika händelser (till exempel skapa, ändra).



1. När frågekonfigurationen är publicerad gäller samma principer, bara med publiceringsslutpunkten.

   >[!NOTE]
   >
   >För anonym åtkomst förutsätter systemet att åtkomstkontrollistan tillåter &quot;alla&quot; att ha åtkomst till frågekonfigurationen.
   >
   >Om så inte är fallet kommer det inte att kunna köras.

   >[!NOTE]
   >
   >Alla semikolon (&quot;;&quot;) i URL:erna måste kodas.
   >
   >Som i begäran att köra en beständig fråga:
   >
   >
   ```xml
   >curl -X GET \ "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters%3bapath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"
   >```

### Frågar GraphQL-slutpunkten från en extern webbplats {#query-graphql-endpoint-from-external-website}

Om du vill komma åt GraphQL-slutpunkten från en extern webbplats måste du konfigurera:

* CORS-filter
* Referensfilter

#### CORS-filter {#cors-filter}

>[!NOTE]
>
>En detaljerad översikt över CORS-resursdelningsprincipen i AEM finns i Förstå korsdomänsresursdelning (CORS).

För att komma åt GraphQL-slutpunkten måste en CORS-princip konfigureras i kundens Git-databas. Detta görs genom att en lämplig OSGi CORS-konfigurationsfil läggs till för de önskade slutpunkterna.

Den här konfigurationen måste ange en betrodd webbplatsursprung `alloworigin` eller `alloworiginregexp` som åtkomst måste beviljas för.

Om du till exempel vill ge åtkomst till GraphQL-slutpunkten och den beständiga frågeslutpunkten för `https://my.domain` kan du använda:

```xml
{
  "supportscredentials":true,
  "supportedmethods":[
    "GET",
    "HEAD",
    "POST"
  ],
  "exposedheaders":[
    ""
  ],
  "alloworigin":[
    "https://my.domain"
  ],
  "maxage:Integer":1800,
  "alloworiginregexp":[
    ""
  ],
  "supportedheaders":[
    "Origin",
    "Accept",
    "X-Requested-With",
    "Content-Type",
    "Access-Control-Request-Method",
    "Access-Control-Request-Headers"
  ],
  "allowedpaths":[
    "/content/_cq_graphql/global/endpoint.json",
    "/graphql/execute.json/.*"
  ]
}
```

Om du har konfigurerat en huvudsökväg för slutpunkten kan du även använda den i `allowedpaths`.

#### Referensfilter {#referrer-filter}

Förutom CORS-konfigurationen måste ett referensfilter konfigureras så att åtkomst från tredjepartsvärdar tillåts.

Detta gör du genom att lägga till en lämplig konfigurationsfil för OSGi-referensfiltret som:

* anger ett betrott värdnamn för en webbplats, antingen `allow.hosts` eller `allow.hosts.regexp`,
* ger åtkomst till det här värdnamnet.

Om du till exempel vill bevilja åtkomst för begäranden med referenten `my.domain` kan du:

```xml
{
    "allow.empty":false,
    "allow.hosts":[
      "my.domain"
    ],
    "allow.hosts.regexp":[
      ""
    ],
    "filter.methods":[
      "POST",
      "PUT",
      "DELETE",
      "COPY",
      "MOVE"
    ],
    "exclude.agents.regexp":[
      ""
    ]
}
```

>[!CAUTION]
>
>Det är kundens ansvar att
>
>* endast ge åtkomst till betrodda domäner
>* se till att ingen känslig information exponeras
>* inte använda jokertecken [*] syntax; Detta inaktiverar både autentiserad åtkomst till GraphQL-slutpunkten och exponerar den även för hela världen.


>[!CAUTION]
>
>Alla GraphQL-scheman (härledda från modeller för innehållsfragment som har **aktiverats**) kan läsas via GraphQL-slutpunkten.
>
>Detta innebär att ni måste se till att inga känsliga uppgifter finns tillgängliga, eftersom de skulle kunna läcka ut på detta sätt. Detta inkluderar till exempel information som kan finnas som fältnamn i modelldefinitionen.

### AEM GraphQL-autentisering {#aem-graphql-authentication}

Ett primärt användningsexempel för Adobe Experience Manager som en Cloud Service (AEM) GraphQL API för Content Fragment Delivery är att ta emot fjärrfrågor från tredjepartsprogram eller -tjänster. Dessa fjärrfrågor kan kräva autentiserad API-åtkomst för att säkra headless-innehållsleverans.

>[!NOTE]
>
>För testning och utveckling kan du även komma åt AEM GraphQL API direkt via gränssnittet GraphiQL.

För autentisering måste tredjepartstjänsten använda en åtkomsttoken som sedan kan användas i GraphQL-begäran.

#### Hämtar en åtkomsttoken {#retrieving-access-token}

Mer information finns i Generera åtkomsttoken för API:er på serversidan.

#### Använda åtkomsttoken i en GraphQL-begäran {#use-access-token-in-graphql-request}

För att en tredjepartstjänst ska kunna ansluta till en AEM måste den ha en *åtkomsttoken*. Tjänsten måste sedan lägga till denna token i rubriken `Authorization` på begäran om POST.

Ett GraphQL Authorization Header:

```xml
Authorization: Bearer <access_token>
```

#### Behörighetskrav {#permission-requirements}

Alla förfrågningar som görs med åtkomsttoken kommer faktiskt att göras *av användarkontot som genererade token*.

Det innebär att du måste kontrollera att kontot har de behörigheter som krävs för att köra GraphQL-frågor.

Du kan kontrollera detta med GraphiQL på den lokala instansen.

## Exempel på AEM GraphQL-frågor {#samples-aem-graphql-queries}

Se Lär dig använda GraphQL med AEM - exempelinnehåll och frågor för ett omfattande urval av exempelfrågor.

<!--
## Code Samples for AEM GraphQL Queries {#code-samples-aem-graphql-queries}
-->

## What&#39;s Next {#whats-next}

Nu när du har lärt dig att komma åt och fråga efter rubriklöst innehåll med AEM GraphQL API kan du nu [lära dig hur du använder REST API för att komma åt och uppdatera innehållet i dina innehållsfragment](/help/implementing/developing/headless-journey/update-your-content.md).

## Ytterligare resurser {#additional-resources}

* [GraphQL.org](https://graphql.org)
   * [Scheman](https://graphql.org/learn/schema/)
   * [Variabler](https://graphql.org/learn/queries/#variables)
   * [GraphQL Java-bibliotek](https://graphql.org/code/#java)
* [GraphiQL](https://graphql.org/learn/serving-over-http/#graphiql)
* [Strukturen för exempelinnehållsfragment](/help/assets/content-fragments/content-fragments-graphql-samples.md#content-fragment-structure-graphql)
* [Att lära sig använda GraphQL med AEM - exempelinnehåll och frågor](/help/assets/content-fragments/content-fragments-graphql-samples.md)
   * [Exempelfråga - Ett enskilt specifikt stadsfragment](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-single-specific-city-fragment)
   * [Exempelfråga för metadata - Ange metadata för utmärkelserna med namnet GB](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-metadata-awards-gb)
   * [Exempelfråga - Alla städer med en namngiven variant](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-cities-named-variation)
* [Aktivera funktionen för innehållsfragment i konfigurationsläsaren](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser)
* [Arbeta med innehållsfragment](/help/assets/content-fragments/content-fragments.md)
   * [Modeller för innehållsfragment](/help/assets/content-fragments/content-fragments-models.md)
   * [JSON-utdata](/help/assets/content-fragments/content-fragments-json-preview.md)
* [CORS (Cross-Origin Resource Sharing)](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html?lang=en#understand-cross-origin-resource-sharing-(cors))
* [Genererar åtkomsttoken för API:er på serversidan](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md)
* [Getting Started with AEM Headless](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html)  - En kort videosjälvstudiekurs med en översikt över hur du använder AEM headless-funktioner, inklusive datamodellering och GraphQL.

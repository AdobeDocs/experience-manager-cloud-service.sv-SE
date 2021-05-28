---
title: AEM GraphQL API för användning med innehållsfragment
description: Lär dig hur du använder innehållsfragment i Adobe Experience Manager (AEM) som en Cloud Service med det AEM GraphQL-API:t för leverans av headless-innehåll.
feature: Innehållsfragment,GraphQL API
exl-id: bdd60e7b-4ab9-4aa5-add9-01c1847f37f6
source-git-commit: 8be8308c15ede115c21ccca8f91a13a23356d0b1
workflow-type: tm+mt
source-wordcount: '3935'
ht-degree: 0%

---


# AEM GraphQL API för användning med innehållsfragment {#graphql-api-for-use-with-content-fragments}

Lär dig hur du använder innehållsfragment i Adobe Experience Manager (AEM) som en Cloud Service med det AEM GraphQL-API:t för leverans av headless-innehåll.

AEM som ett Cloud Service GraphQL API som används med innehållsfragment är till stor del baserat på det öppna GraphQL API:t.

Genom att använda GraphQL API i AEM kan du effektivt leverera innehållsfragment till JavaScript-klienter i headless CMS-implementeringar:

* Undvika iterativa API-begäranden som REST,
* se till att leveransen begränsas till de specifika kraven,
* Det går att skicka exakt det som behövs för återgivningen som svar på en enda API-fråga.

>[!NOTE]
>
>GraphQL används för närvarande i två (separata) scenarier i Adobe Experience Manager (AEM) som en Cloud Service:
>
>* [AEM använder data från en handelsplattform via GraphQL](/help/commerce-cloud/integrating/magento.md).
>* AEM Content Fragments fungerar tillsammans med det AEM GraphQL-API:t (en anpassad implementering som baseras på standard GraphQL) för att leverera strukturerat innehåll som kan användas i dina program.


## GraphQL API {#graphql-api}

GraphQL är:

* &quot;*..ett frågespråk för API:er och en körningsmiljö för att utföra dessa frågor med dina befintliga data. GraphQL ger en komplett och lättförståelig beskrivning av data i ditt API, ger kunderna möjlighet att fråga efter exakt vad de behöver och inget mer, gör det enklare att utveckla API:er över tid och möjliggör kraftfulla utvecklingsverktyg.*&quot;.

   Se [GraphQL.org](https://graphql.org)

* &quot;*..en öppen specifikation för ett flexibelt API-lager. Flytta GraphQL över dina befintliga bakgrunder för att skapa produkter snabbare än någonsin....*&quot;.

   Se [Utforska GraphQL](https://www.graphql.com).

* *&quot;...ett datameddelande och en specifikation som utvecklats internt av Facebook 2012 innan de blev offentligt tillgängliga 2015. Det är ett alternativ till REST-baserade arkitekturer i syfte att öka utvecklarnas produktivitet och minimera mängden data som överförs. GraphQL används i produktion av hundratals organisationer av alla storlekar...&quot;*

   Se [GraphQL Foundation](https://foundation.graphql.org/).

<!--
"*Explore GraphQL is maintained by the Apollo team. Our goal is to give developers and technical leaders around the world all of the tools they need to understand and adopt GraphQL.*". 
-->

Mer information om GraphQL API finns i följande avsnitt (bland många andra resurser):

* Vid [graphql.org](https://graphql.org):

   * [Introduktion till GraphQL](https://graphql.org/learn)

   * [GraphQL-specifikationen](http://spec.graphql.org/)

* Vid [graphql.com](https://graphql.com):

   * [Stödlinjer](https://www.graphql.com/guides/)

   * [Tutorials](https://www.graphql.com/tutorials/)

   * [Fallstudier](https://www.graphql.com/case-studies/)

GraphQL för AEM är baserad på standardbiblioteket GraphQL Java Library. Se:

* [graphQL.org - Java](https://graphql.org/code/#java)

* [GraphQL Java vid GitHub](https://github.com/graphql-java)

### GraphQL-terminologi {#graphql-terminology}

GraphQL använder följande:

* **[Frågor](https://graphql.org/learn/queries/)**

* **[Scheman och typer](https://graphql.org/learn/schema/)**:

   * Scheman genereras av AEM baserat på modeller för innehållsfragment.
   * GraphQL visar de typer och åtgärder som tillåts för GraphQL för AEM implementering med dina scheman.

* **[Fält](https://graphql.org/learn/queries/#fields)**

* **[GraphQL-slutpunkt](#graphql-aem-endpoint)**
   * Den sökväg i AEM som svarar på GraphQL-frågor och ger åtkomst till GraphQL-scheman.

   * Mer information finns i [Aktivera GraphQL-slutpunkten](#enabling-graphql-endpoint).

Mer information finns i [(GraphQL.org) Introduktion till GraphQL](https://graphql.org/learn/), inklusive [Best Practices](https://graphql.org/learn/best-practices/).

### GraphQL-frågetyper {#graphql-query-types}

Med GraphQL kan du utföra frågor för att returnera:

* En **enkel post**

* En **[lista över poster](https://graphql.org/learn/schema/#lists-and-non-null)**

Du kan också utföra:

* [Beständiga frågor, som är cachelagrade](#persisted-queries-caching)

>[!NOTE]
>Du kan testa och felsöka GraphQL-frågor med [GraphiQL IDE](#graphiql-interface).

## The GraphQL for AEM Endpoint {#graphql-aem-endpoint}

Slutpunkten är den bana som används för att komma åt GraphQL för AEM. Med den här sökvägen kan du (eller din app):

* få tillgång till GraphQL-schemat,
* skicka GraphQL-frågor,
* ta emot svar (på GraphQL-frågor).

Det finns två typer av slutpunkter i AEM:

* Global
   * Tillgängligt för alla webbplatser.
   * Den här slutpunkten kan använda alla modeller för innehållsfragment från alla platskonfigurationer (definieras i [Konfigurationsläsaren](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser)).
   * Om det finns några modeller för innehållsfragment som ska delas mellan platskonfigurationer, ska dessa skapas under de globala platskonfigurationerna.
* Platskonfigurationer:
   * Motsvarar en platskonfiguration, enligt definitionen i [Configuration Browser](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser).
   * Specifikt för en angiven plats/ett angivet projekt.
   * En platskonfigurationsspecifik slutpunkt använder innehållsfragmentmodellerna från den specifika platskonfigurationen tillsammans med de från den globala platskonfigurationen.

>[!CAUTION]
>
>Innehållsfragmentsredigeraren kan tillåta att ett innehållsfragment av en platskonfiguration refererar till ett innehållsfragment av en annan platskonfiguration (via principer).
>
>I så fall går det inte att hämta allt innehåll med en platskonfigurationsspecifik slutpunkt.
>
>Innehållsförfattaren bör kontrollera detta scenario; Det kan till exempel vara bra att överväga att placera delade modeller för innehållsfragment under konfigurationen för globala platser.

Databassökvägen för GraphQL för AEM globala slutpunkten är:

`/content/cq:graphql/global/endpoint`

För vilken ditt program kan använda följande sökväg i URL:en för begäran:

`/content/_cq_graphql/global/endpoint.json`

Om du vill aktivera en slutpunkt för GraphQL för AEM måste du:

* [Aktivera GraphQL-slutpunkten](#enabling-graphql-endpoint)
* [Publicera din GraphQL-slutpunkt](#publishing-graphql-endpoint)

### Aktivera GraphQL-slutpunkten {#enabling-graphql-endpoint}

Om du vill aktivera en GraphQL-slutpunkt måste du först ha en lämplig konfiguration. Se [Innehållsfragment - Konfigurationsläsaren](/help/assets/content-fragments/content-fragments-configuration-browser.md).

>[!CAUTION]
>
>Om [användningen av innehållsfragmentmodeller inte har aktiverats](/help/assets/content-fragments/content-fragments-configuration-browser.md) är alternativet **Skapa** inte tillgängligt.

Så här aktiverar du motsvarande slutpunkt:

1. Navigera till **Verktyg**, **Resurser** och välj sedan **GraphQL**.
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

## GraphiQL-gränssnitt {#graphiql-interface}

En implementering av standardgränssnittet [GraphiQL](https://graphql.org/learn/serving-over-http/#graphiql) finns tillgänglig för användning med AEM GraphQL. Detta kan vara [installerat med AEM](#installing-graphiql-interface).

>[!NOTE]
>
>GraphiQL är bundet till den globala slutpunkten (och fungerar inte med andra slutpunkter för specifika platskonfigurationer).

Med det här gränssnittet kan du direkt mata in och testa frågor.

Till exempel:

* `http://localhost:4502/content/graphiql.html`

Detta innehåller funktioner som syntaxmarkering, automatisk komplettering, autoförslag, samt historik och onlinedokumentation:

![Gränssnittet GraphiQL ](assets/cfm-graphiql-interface.png "InterfaceGraphiQL")

### Installera AEM GraphiQL-gränssnitt {#installing-graphiql-interface}

Användargränssnittet GraphiQL kan installeras på AEM med ett dedikerat paket: [Innehållspaketet GraphiQL v0.0.6 (2021.3)](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/aem-graphql/graphiql-0.0.6.zip).

## Användningsexempel för redigerings- och publiceringsmiljöer {#use-cases-author-publish-environments}

Användningsexempel kan bero på vilken typ av AEM som en Cloud Service-miljö:

* Publiceringsmiljö. används för att:
   * Frågedata för JS-program (standardfall)

* Författarmiljö; används för att:
   * Fråga efter data för&quot;innehållshanteringssyften&quot;:
      * GraphQL i AEM som en Cloud Service är för närvarande ett skrivskyddat API.
      * REST API kan användas för CR(u)D-åtgärder.

## Behörigheter {#permission}

Behörigheterna är de som krävs för åtkomst av resurser.

## Schemagenerering {#schema-generation}

GraphQL är ett starkt typbestämt API, vilket innebär att data måste vara tydligt strukturerade och ordnade efter typ.

GraphQL-specifikationen innehåller en serie riktlinjer för hur du skapar ett robust API för att förhöra data i en viss instans. För att göra detta måste klienten hämta [schemat](#schema-generation), som innehåller alla typer som krävs för en fråga.

För innehållsfragment baseras GraphQL-scheman (struktur och typer) på **Enabled** [Content Fragment Models](/help/assets/content-fragments/content-fragments-models.md) och deras datatyper.

>[!CAUTION]
>
>Alla GraphQL-scheman (härledda från modeller för innehållsfragment som har **aktiverats**) kan läsas via GraphQL-slutpunkten.
>
>Detta innebär att ni måste se till att inga känsliga uppgifter finns tillgängliga, eftersom de skulle kunna läcka ut på detta sätt. Detta inkluderar till exempel information som kan finnas som fältnamn i modelldefinitionen.

Om en användare till exempel har skapat en innehållsfragmentmodell med namnet `Article`, genererar AEM objektet `article` som är av typen `ArticleModel`. Fälten i den här typen motsvarar fälten och datatyperna som definieras i modellen.

1. En innehållsfragmentmodell:

   ![Content Fragment Model for use with ](assets/cfm-graphqlapi-01.png "GraphQLContent Fragment Model for use with GraphQL")

1. Motsvarande GraphQL-schema (utdata från automatisk GraphiQL-dokumentation):
   ![GraphQL-schema baserat på Content Fragment ](assets/cfm-graphqlapi-02.png "ModelGraphQL-schema baserat på Content Fragment Model")

   Detta visar att den genererade typen `ArticleModel` innehåller flera [fält](#fields).

   * Tre av dem har kontrollerats av användaren: `author`, `main` och `referencearticle`.

   * De andra fälten lades till automatiskt av AEM och representerar användbara metoder för att tillhandahålla information om ett visst innehållsfragment. i det här exemplet är `_path`, `_metadata`, `_variations`. Dessa [hjälpfält](#helper-fields) är markerade med en föregående `_` för att skilja mellan vad som har definierats av användaren och vad som har genererats automatiskt.

1. När en användare har skapat ett innehållsfragment baserat på artikelmodellen kan det sedan förfrågas via GraphQL. Se till exempel [Exempelfrågor](/help/assets/content-fragments/content-fragments-graphql-samples.md#graphql-sample-queries) (baserat på en [innehållsfragmentstruktur för GraphQL](/help/assets/content-fragments/content-fragments-graphql-samples.md#content-fragment-structure-graphql)).

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

## fält {#fields}

Inom schemat finns det enskilda fält av två baskategorier:

* Fält som du genererar.

   Ett urval av [fälttyper](#field-types) används för att skapa fält baserat på hur du konfigurerar innehållsfragmentmodellen. Fältnamnen hämtas från fältet **Egenskapsnamn** i **datatypen**.

   * Det finns också egenskapen **Återge som** som ska beaktas, eftersom användare kan konfigurera vissa datatyper; t.ex. som en enda rad eller som ett multifält.

* GraphQL för AEM genererar även ett antal [hjälpfält](#helper-fields).

   Dessa används för att identifiera ett innehållsfragment eller för att få mer information om ett innehållsfragment.

### Fälttyper {#field-types}

GraphQL för AEM stöder en lista med typer. Alla Content Fragment Model-datatyper som stöds och motsvarande GraphQL-typer visas:

| Content Fragment Model - datatyp | GraphQL-typ | Beskrivning |
|--- |--- |--- |
| Enkelradig text | Sträng, [Sträng] |  Används för enkla strängar som författarnamn, platsnamn osv. |
| Flerradstext | Sträng |  Används för att skriva ut text, t.ex. brödtexten i en artikel |
| Siffra |  Float, [Float] | Används för att visa flyttal och reguljära tal |
| Boolesk |  Boolesk |  Används för att visa kryssrutor → enkla sant/falskt-satser |
| Datum och tid | Kalender |  Används för att visa datum och tid i ett ISO 8086-format. Beroende på vilken typ som valts finns det tre olika varianter att använda i AEM GraphQL: `onlyDate`, `onlyTime`, `dateTime` |
| Uppräkning |  Sträng |  Används för att visa ett alternativ från en lista med alternativ som definieras när modellen skapas |
|  Taggar |  [Sträng] |  Används för att visa en lista över strängar som representerar taggar som används i AEM |
| Innehållsreferens |  Sträng |  Används för att visa sökvägen till en annan resurs i AEM |
| Fragmentreferens |  *En modelltyp* |  Används för att referera till ett annat innehållsfragment av en viss modelltyp, som definieras när modellen skapades |

### Hjälpfält {#helper-fields}

Förutom datatyperna för användargenererade fält genererar GraphQL för AEM även ett antal *hjälpfält*-fält för att hjälpa till att identifiera ett innehållsfragment eller för att ge ytterligare information om ett innehållsfragment.

#### Bana {#path}

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

Se [Exempelfråga - Ett enskilt specifikt stadsfragment](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-single-specific-city-fragment).

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
>Kom ihåg att både `StringMetadata` och `StringArrayMetadata` hänvisar till vad som lagras i databasen, inte till hur du hämtar dem.
>
>Om du till exempel anropar fältet `stringMetadata` får du en array med alla metadata som lagrats i databasen som `String`. Om du anropar `stringArrayMetadata` får du en array med alla metadata som lagrats i databasen som `String[]`.

Se [Exempelfråga för metadata - Visa en lista över metadata för utmärkelser med namnet GB](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-metadata-awards-gb).

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

Se [Exempelfråga - Alla städer med en namngiven variant](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-cities-named-variation).

<!--
## Security Considerations {#security-considerations}
-->

## GraphQL-variabler {#graphql-variables}

GraphQL tillåter att variabler placeras i frågan. Mer information finns i [GraphQL-dokumentationen för variabler](https://graphql.org/learn/queries/#variables).

Om du till exempel vill hämta alla innehållsfragment av typen `Article` som har en viss variation, kan du ange variabeln `variation` i GraphiQL.

![Variabler för GraphQL ](assets/cfm-graphqlapi-03.png "VariablesGraphQL")

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

## GraphQL-direktiv {#graphql-directives}

I GraphQL finns det en möjlighet att ändra frågan baserat på variabler, så kallade GraphQL-direktiv.

Där kan du till exempel inkludera fältet `adventurePrice` i en fråga för alla `AdventureModels`, baserat på variabeln `includePrice`.

![GraphQL-](assets/cfm-graphqlapi-04.png "direktivGraphQL-direktiv")

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

* [Exempelfrågor med detta exempelinnehåll och -struktur](/help/assets/content-fragments/content-fragments-graphql-samples.md#graphql-sample-queries-sample-content-fragment-structure)

   * Och [exempelinnehållet och strukturen](/help/assets/content-fragments/content-fragments-graphql-samples.md#content-fragment-structure-graphql) har förberetts för användning i exempelfrågor

* [Exempelfrågor baserade på WKND-projektet](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-queries-using-wknd-project)

## GraphQL för AEM - Sammanfattning av tillägg {#graphql-extensions}

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

## Beständiga frågor (cachelagring) {#persisted-queries-caching}

När en fråga har förberetts med en begäran om POST kan den köras med en GET-begäran som kan cachas av HTTP-cacher eller ett CDN.

Detta är nödvändigt eftersom POST-frågor vanligtvis inte cachelagras, och om GET med frågan används som parameter finns det en stor risk för att parametern blir för stor för HTTP-tjänster och mellanhänder.

Beständiga frågor måste alltid använda den slutpunkt som är relaterad till [rätt platskonfiguration](#graphql-aem-endpoint); så att de kan använda antingen eller båda:

* Den globala konfigurationen och slutpunkten
Frågan har åtkomst till alla modeller för innehållsfragment.
* Specifika platskonfigurationer och slutpunkter
För att skapa en beständig fråga för en specifik platskonfiguration krävs en motsvarande platskonfigurationsspecifik slutpunkt (för att ge åtkomst till relaterade modeller för innehållsfragment).
Om du till exempel vill skapa en beständig fråga specifikt för WKND-platskonfigurationen, måste en motsvarande WKND-specifik platskonfiguration och en WKND-specifik slutpunkt skapas i förväg.

>[!NOTE]
>
>Mer information finns i [Aktivera funktionen för innehållsfragment i konfigurationsläsaren](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser).
>
>**GraphQL Persistence Queries** måste aktiveras för rätt platskonfiguration.

Om det till exempel finns en viss fråga med namnet `my-query`, som använder modellen `my-model` från platskonfigurationen `my-conf`:

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

## Frågar GraphQL-slutpunkten från en extern webbplats {#query-graphql-endpoint-from-external-website}

Om du vill komma åt GraphQL-slutpunkten från en extern webbplats måste du konfigurera:

* [CORS-filter](#cors-filter)
* [Referensfilter](#referrer-filter)

### CORS-filter {#cors-filter}

>[!NOTE]
>
>En detaljerad översikt över CORS resursdelningsprincip i AEM finns i [Förstå korsdomänsresursdelning (CORS)](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html?lang=en#understand-cross-origin-resource-sharing-(cors)).

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

### Referensfilter {#referrer-filter}

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
>Alla GraphQL [scheman](#schema-generation) (härledda från Content Fragment Models som har **Enabled**) kan läsas via GraphQL-slutpunkten.
>
>Detta innebär att ni måste se till att inga känsliga uppgifter finns tillgängliga, eftersom de skulle kunna läcka ut på detta sätt. Detta inkluderar till exempel information som kan finnas som fältnamn i modelldefinitionen.

## Autentisering {#authentication}

Se [Autentisering för AEM GraphQL-frågor om innehållsfragment](/help/assets/content-fragments/graphql-authentication-content-fragments.md).

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

1. **Fråga**: &quot;*Hur skiljer sig GraphQL API för AEM från Query Builder API?*&quot;

   * **S**: &quot;*AEM GraphQL API ger total kontroll över JSON-utdata och är en branschstandard för att fråga efter innehåll.
AEM planerar att investera i AEM GraphQL API.*&quot;

## Självstudiekurs - Komma igång med AEM Headless och GraphQL {#tutorial}

Söker du en praktisk självstudiekurs? Ta en titt på [Komma igång med AEM Headless och GraphQL](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html) heltäckande självstudiekurs som visar hur du bygger upp och visar innehåll med AEM GraphQL API:er och som används av en extern app i ett headless CMS-scenario.

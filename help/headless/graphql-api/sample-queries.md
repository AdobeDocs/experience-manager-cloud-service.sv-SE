---
title: Att lära sig använda GraphQL med AEM - exempelinnehåll och frågor
description: Lär dig använda GraphQL med AEM för att leverera innehåll utan problem genom att utforska exempelinnehåll och frågor.
feature: Content Fragments,GraphQL API
exl-id: b60fcf97-4736-4606-8b41-4051b8b0c8a7
source-git-commit: 6be7cc7678162c355c39bc3000716fdaf421884d
workflow-type: tm+mt
source-wordcount: '1430'
ht-degree: 2%

---

# Att lära sig använda GraphQL med AEM - exempelinnehåll och frågor {#learn-graphql-with-aem-sample-content-queries}

Lär dig använda GraphQL med AEM för att leverera innehåll utan problem genom att utforska exempelinnehåll och frågor.

>[!NOTE]
>
>Den här sidan ska läsas tillsammans med:
>
>* [Innehållsfragment](/help/sites-cloud/administering/content-fragments/content-fragments.md)
>* [Modeller för innehållsfragment](/help/sites-cloud/administering/content-fragments/content-fragments-models.md)
>* [AEM GraphQL API för användning med innehållsfragment](/help/headless/graphql-api/content-fragments.md)


Om du vill komma igång med GraphQL-frågor och hur de fungerar med AEM innehållsfragment kan du se några praktiska exempel.

Mer information finns i:

* A [exempel på struktur för innehållsfragment](#content-fragment-structure-graphql)

* Och några [sampla GraphQL-frågor](#graphql-sample-queries), baserat på fragmentstrukturen för exempelinnehåll (modeller för innehållsfragment och relaterade innehållsfragment).


## GraphQL - Exempelfrågor med strukturen för exempelinnehållsfragment {#graphql-sample-queries-sample-content-fragment-structure}

I de här exempelfrågorna finns illustrationer av hur du skapar frågor, tillsammans med exempelresultat.

>[!NOTE]
>
>Beroende på din instans kan du komma åt [GraphiQL-gränssnittet ingår i AEM GraphQL API](/help/headless/graphql-api/graphiql-ide.md) för att skicka och testa frågor.
>
>Du kan öppna frågeredigeraren från:
>
>* **verktyg** -> **Allmänt** -> **GraphQL Query Editor**
>* direkt, till exempel `http://localhost:4502/aem/graphiql.html`


>[!NOTE]
>
>Exempelfrågorna baseras på [Exempel på struktur för innehållsfragment som ska användas med GraphQL](#content-fragment-structure-graphql)

### Exempelfråga - Alla tillgängliga scheman och datatyper {#sample-all-schemes-datatypes}

Detta returnerar alla `types` för alla tillgängliga scheman.

**Exempelfråga**

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

**Provresultat**

```xml
{
  "data": {
    "__schema": {
      "types": [
        {
          "name": "AdventureModel",
          "description": null
        },
        {
          "name": "AdventureModelArrayFilter",
          "description": null
        },
        {
          "name": "AdventureModelFilter",
          "description": null
        },
        {
          "name": "AdventureModelResult",
          "description": null
        },
        {
          "name": "AdventureModelResults",
          "description": null
        },
        {
          "name": "AllFragmentModels",
          "description": null
        },
        {
          "name": "ArchiveRef",
          "description": null
        },
        {
          "name": "ArrayMode",
          "description": null
        },
        {
          "name": "ArticleModel",
          "description": null
        },

...more results...

        {
          "name": "__EnumValue",
          "description": null
        },
        {
          "name": "__Field",
          "description": null
        },
        {
          "name": "__InputValue",
          "description": null
        },
        {
          "name": "__Schema",
          "description": "A GraphQL Introspection defines the capabilities of a GraphQL server. It exposes all available types and directives on the server, the entry points for query, mutation, and subscription operations."
        },
        {
          "name": "__Type",
          "description": null
        },
        {
          "name": "__TypeKind",
          "description": "An enum describing what kind of type a given __Type is"
        }
      ]
    }
  }
}
```

### Exempelfråga - All information om alla städer {#sample-all-information-all-cities}

Om du vill hämta all information om alla städer kan du använda den grundläggande frågan:
**Exempelfråga**

```xml
{
  cityList {
    items
  }
}
```

När den körs utökas frågan automatiskt så att den omfattar alla fält:

```xml
{
  cityList {
    items {
      _path
      name
      country
      population
    }
  }
}
```

**Exempelresultat**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "_path": "/content/dam/sample-content-fragments/cities/basel",
          "name": "Basel",
          "country": "Switzerland",
          "population": 172258
        },
        {
          "_path": "/content/dam/sample-content-fragments/cities/berlin",
          "name": "Berlin",
          "country": "Germany",
          "population": 3669491
        },
        {
          "_path": "/content/dam/sample-content-fragments/cities/bucharest",
          "name": "Bucharest",
          "country": "Romania",
          "population": 1821000
        },
        {
          "_path": "/content/dam/sample-content-fragments/cities/san-francisco",
          "name": "San Francisco",
          "country": "USA",
          "population": 883306
        },
        {
          "_path": "/content/dam/sample-content-fragments/cities/san-jose",
          "name": "San Jose",
          "country": "USA",
          "population": 1026350
        },
        {
          "_path": "/content/dam/sample-content-fragments/cities/stuttgart",
          "name": "Stuttgart",
          "country": "Germany",
          "population": 634830
        },
        {
          "_path": "/content/dam/sample-content-fragments/cities/zurich",
          "name": "Zurich",
          "country": "Switzerland",
          "population": 415367
        }
      ]
    }
  }
}
```

### Exempelfråga - namn på alla städer {#sample-names-all-cities}

Det här är en enkel fråga som returnerar `name`av alla poster i `city`schema.

**Exempelfråga**

```xml
query {
  cityList {
    items {
      name
    }
  }
}
```

**Exempelresultat**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "name": "Basel"
        },
        {
          "name": "Berlin"
        },
        {
          "name": "Bucharest"
        },
        {
          "name": "San Francisco"
        },
        {
          "name": "San Jose"
        },
        {
          "name": "Stuttgart"
        },
        {
          "name": "Zurich"
        }
      ]
    }
  }
}
```

### Exempelfråga - Ett enskilt specifikt stadsfragment {#sample-single-specific-city-fragment}

Det här är en fråga som returnerar information om en enskild fragmentpost på en viss plats i databasen.

**Exempelfråga**

```xml
{
  cityByPath (_path: "/content/dam/sample-content-fragments/cities/berlin") {
    item {
      _path
      name
      country
      population
     categories
    }
  }
}
```

**Exempelresultat**

```xml
{
  "data": {
    "cityByPath": {
      "item": {
        "_path": "/content/dam/sample-content-fragments/cities/berlin",
        "name": "Berlin",
        "country": "Germany",
        "population": 3669491,
        "categories": [
          "city:capital",
          "city:emea"
        ]
      }
    }
  }
}
```

### Exempelfråga - Alla städer med en namngiven variant {#sample-cities-named-variation}

Om du skapar en ny variant som heter &quot;Berlin Center&quot; (`berlin_centre`), för `city` I Berlin kan du använda en fråga för att returnera information om variationen.

**Exempelfråga**

```xml
{
  cityList (variation: "berlin_center") {
    items {
      _path
      name
      country
      population
      categories
    }
  }
}
```

**Exempelresultat**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "_path": "/content/dam/sample-content-fragments/cities/berlin",
          "name": "Berlin",
          "country": "Germany",
          "population": 3669491,
          "categories": [
            "city:capital",
            "city:emea"
          ]
        }
      ]
    }
  }
}
```

### Exempelfråga - Fullständig information om företagets VD och anställda {#sample-full-details-company-ceos-employees}

Med hjälp av strukturen för kapslade fragment returnerar den här frågan alla detaljer för ett företags VD och alla dess anställda.

**Exempelfråga**

```xml
query {
  companyList {
    items {
      name
      ceo {
        _path
        name
        firstName
        awards {
        id
          title
        }
      }
      employees {
       name
        firstName
       awards {
         id
          title
        }
      }
    }
  }
}
```

**Exempelresultat**

```xml
{
  "data": {
    "companyList": {
      "items": [
        {
          "name": "Apple Inc.",
          "ceo": {
            "_path": "/content/dam/sample-content-fragments/persons/steve-jobs",
            "name": "Jobs",
            "firstName": "Steve",
            "awards": []
          },
          "employees": [
            {
              "name": "Marsh",
              "firstName": "Duke",
              "awards": []
            },
            {
              "name": "Caulfield",
              "firstName": "Max",
              "awards": [
                {
                  "id": "GB",
                  "title": "Gameblitz"
                }
              ]
            }
          ]
        },
        {
          "name": "Little Pony, Inc.",
          "ceo": {
            "_path": "/content/dam/sample-content-fragments/persons/adam-smith",
            "name": "Smith",
            "firstName": "Adam",
            "awards": []
          },
          "employees": [
            {
              "name": "Croft",
              "firstName": "Lara",
              "awards": [
                {
                  "id": "GS",
                  "title": "Gamestar"
                }
              ]
            },
            {
              "name": "Slade",
              "firstName": "Cutter",
              "awards": [
                {
                  "id": "GB",
                  "title": "Gameblitz"
                },
                {
                  "id": "GS",
                  "title": "Gamestar"
                }
              ]
            }
          ]
        },
        {
          "name": "NextStep Inc.",
          "ceo": {
            "_path": "/content/dam/sample-content-fragments/persons/steve-jobs",
            "name": "Jobs",
            "firstName": "Steve",
            "awards": []
          },
          "employees": [
            {
              "name": "Smith",
              "firstName": "Joe",
              "awards": []
            },
            {
              "name": "Lincoln",
              "firstName": "Abraham",
              "awards": []
            }
          ]
        }
      ]
    }
  }
}
```

### Exempelfråga - Alla personer som har namnet &quot;Jobs&quot; eller &quot;Smith&quot; {#sample-all-persons-jobs-smith}

Detta kommer att filtrera alla `persons` för alla som har ett namn `Jobs`eller `Smith`.

**Exempelfråga**

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

**Exempelresultat**

```xml
{
  "data": {
    "personList": {
      "items": [
        {
          "name": "Smith",
          "firstName": "Adam"
        },
        {
          "name": "Smith",
          "firstName": "Joe"
        },
        {
          "name": "Jobs",
          "firstName": "Steve"
        }
      ]
    }
  }
}
```

### Exempelfråga - Alla personer som inte har namnet &quot;Jobs&quot; {#sample-all-persons-not-jobs}

Detta kommer att filtrera alla `persons` för alla som har ett namn `Jobs`eller `Smith`.

**Exempelfråga**

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

**Exempelresultat**

```xml
{
  "data": {
    "personList": {
      "items": [
        {
          "name": "Lincoln",
          "firstName": "Abraham"
        },
        {
          "name": "Smith",
          "firstName": "Adam"
        },
        {
          "name": "Slade",
          "firstName": "Cutter"
        },
        {
          "name": "Marsh",
          "firstName": "Duke"
        },
        {
          "name": "Smith",
          "firstName": "Joe"
        },
        {
          "name": "Croft",
          "firstName": "Lara"
        },
        {
          "name": "Caulfield",
          "firstName": "Max"
        }
      ]
    }
  }
}
```

### Exempelfråga - Alla annonser vars `_path` börjar med ett visst prefix {#sample-wknd-all-adventures-cycling-path-filter}

Alla `adventures` där `_path` börjar med ett visst prefix (`/content/dam/wknd/en/adventures/cycling`).

**Exempelfråga**

```xml
query {
  adventureList(
    filter: {
      _path: {
        _expressions: [
        {
          value: "/content/dam/wknd/en/adventures/cycling"
         _operator: STARTS_WITH
        }]
       }
    })
    {
    items {
      _path
    }
  }
}
```

**Exempelresultat**

```xml
{
  "data": {
    "adventureList": {
      "items": [
        {
          "_path": "/content/dam/wknd/en/adventures/cycling-southern-utah/cycling-southern-utah"
        },
        {
          "_path": "/content/dam/wknd/en/adventures/cycling-tuscany/cycling-tuscany"
        }
      ]
    }
  }
}
```

### Exempelfråga - Alla städer i Tyskland eller Schweiz med en befolkning på mellan 400000 och 99999 {#sample-all-cities-d-ch-population}

Här filtreras en kombination av fält. An `AND` (implicit) används för att välja `population`omfång, medan `OR` (explicit) används för att välja önskade städer.

**Exempelfråga**

```xml
query {
  cityList(filter: {
    population: {
      _expressions: [
        {
          value: 400000
          _operator: GREATER_EQUAL
        }, {
          value: 1000000
          _operator: LOWER
        }
      ]
    },
    country: {
      _logOp: OR
      _expressions: [
        {
          value: "Germany"
        }, {
          value: "Switzerland"
        }
      ]
    }
  }) {
    items {
      name
      population
      country
    }
  }
}
```

**Exempelresultat**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "name": "Stuttgart",
          "population": 634830,
          "country": "Germany"
        },
        {
          "name": "Zurich",
          "population": 415367,
          "country": "Switzerland"
        }
      ]
    }
  }
}
```

### Exempelfråga - Alla städer med SAN i namnet, oavsett fall {#sample-all-cities-san-ignore-case}

Den här frågan frågar efter alla städer som har `SAN` i namnet, oavsett skiftläge.

**Exempelfråga**

```xml
query {
  cityList(filter: {
    name: {
      _expressions: [
        {
          value: "SAN"
          _operator: CONTAINS
          _ignoreCase: true
        }
      ]
    }
  }) {
    items {
      name
      population
      country
    }
  }
}
```

**Exempelresultat**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "name": "San Francisco",
          "population": 883306,
          "country": "USA"
        },
        {
          "name": "San Jose",
          "population": 1026350,
          "country": "USA"
        }
      ]
    }
  }
}
```

### Exempelfråga - Filtrera en array med ett objekt som måste förekomma minst en gång {#sample-array-item-occur-at-least-once}

Den här frågan filtrerar en array med ett objekt (`city:na`) som måste inträffa minst en gång.

**Exempelfråga**

```xml
query {
  cityList(filter: {
    categories: {
      _expressions: [
        {
          value: "city:na"
          _apply: AT_LEAST_ONCE
        }
      ]
    }
  }) {
    items {
      name
      population
      country
      categories
    }
  }
}
```

**Exempelresultat**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "name": "San Francisco",
          "population": 883306,
          "country": "USA",
          "categories": [
            "city:beach",
            "city:na"
          ]
        },
        {
          "name": "San Jose",
          "population": 1026350,
          "country": "USA",
          "categories": [
            "city:na"
          ]
        }
      ]
    }
  }
}
```

### Exempelfråga - Filtrera på ett exakt arrayvärde {#sample-array-exact-value}

Den här frågan filtrerar på ett exakt arrayvärde.

**Exempelfråga**

```xml
query {
  cityList(filter: {
    categories: {
      _expressions: [
        {
          values: [
            "city:beach",
            "city:na"
          ]
        }
      ]
    }
  }) {
    items {
      name
      population
      country
      categories
    }
  }
}
```

**Exempelresultat**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "name": "San Francisco",
          "population": 883306,
          "country": "USA",
          "categories": [
            "city:beach",
            "city:na"
          ]
        }
      ]
    }
  }
}
```

### Exempelfråga för kapslade innehållsfragment - Alla företag som har minst en anställd med namnet &quot;Smith&quot; {#sample-companies-employee-smith}

Den här frågan visar filtrering för alla `person` av `name` &quot;Smith&quot;, returnera information från två kapslade fragment - `company` och `employee`.

**Exempelfråga**

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

**Exempelresultat**

```xml
{
  "data": {
    "companyList": {
      "items": [
        {
          "name": "NextStep Inc.",
          "ceo": {
            "name": "Jobs",
            "firstName": "Steve"
          },
          "employees": [
            {
              "name": "Smith",
              "firstName": "Joe"
            },
            {
              "name": "Lincoln",
              "firstName": "Abraham"
            }
          ]
        }
      ]
    }
  }
}
```

### Exempelfråga för kapslade innehållsfragment - Alla företag där alla anställda har vunnit utmärkelsen&quot;Gamestar&quot; {#sample-all-companies-employee-gamestar-award}

Den här frågan visar filtrering över tre kapslade fragment - `company`, `employee`och `award`.

**Exempelfråga**

```xml
query {
  companyList(filter: {
    employees: {
      _apply: ALL
      _match: {
        awards: {
          _match: {
            id: {
              _expressions: [
                {
                  value: "GS"
                  _operator:EQUALS
                }
              ]
            }
          }
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
        awards {
          id
          title
        }
      }
    }
  }
}
```

**Exempelresultat**

```xml
{
  "data": {
    "companyList": {
      "items": [
        {
          "name": "Little Pony, Inc.",
          "ceo": {
            "name": "Smith",
            "firstName": "Adam"
          },
          "employees": [
            {
              "name": "Croft",
              "firstName": "Lara",
              "awards": [
                {
                  "id": "GS",
                  "title": "Gamestar"
                }
              ]
            },
            {
              "name": "Slade",
              "firstName": "Cutter",
              "awards": [
                {
                  "id": "GB",
                  "title": "Gameblitz"
                },
                {
                  "id": "GS",
                  "title": "Gamestar"
                }
              ]
            }
          ]
        }
      ]
    }
  }
}
```

### Exempelfråga för metadata - Ange metadata för utmärkelserna med namnet GB {#sample-metadata-awards-gb}

Den här frågan visar filtrering över tre kapslade fragment - `company`, `employee`och `award`.

**Exempelfråga**

```xml
query {
  awardList(filter: {
      id: {
        _expressions: [
          {
            value:"GB"
          }
        ]
    }
  }) {
    items {
      _metadata {
        stringMetadata {
          name,
          value
        }
      }
      id
      title
    }
  }
}
```

**Exempelresultat**

```xml
{
  "data": {
    "awardList": {
      "items": [
        {
          "_metadata": {
            "stringMetadata": [
              {
                "name": "title",
                "value": "Gameblitz Award"
              },
              {
                "name": "description",
                "value": ""
              }
            ]
          },
          "id": "GB",
          "title": "Gameblitz"
        }
      ]
    }
  }
}
```

## Exempelfrågor med WKND-projektet {#sample-queries-using-wknd-project}

Dessa exempelfrågor är baserade på WKND-projektet. Detta har:

* Content Fragment Models available under:
   `http://<hostname>:<port>/libs/dam/cfm/models/console/content/models.html/conf/wknd`

* Innehållsfragment (och annat innehåll) tillgängliga under:
   `http://<hostname>:<port>/assets.html/content/dam/wknd/en`

>[!NOTE]
>
>Eftersom resultaten kan bli omfattande återges de inte här.

### Exempelfråga för alla innehållsfragment i en viss modell med de angivna egenskaperna {#sample-wknd-all-model-properties}

Detta exempel på frågor intervjuar:

* för alla innehållsfragment av typen `article`
* med `path`och `author` egenskaper.

**Exempelfråga**

```xml
{
  articleList {
    items {
      _path
      author
    }
  }
}
```

### Exempelfråga för metadata {#sample-wknd-metadata}

Den här frågan förhör:

* för alla innehållsfragment av typen `adventure`
* metadata

**Exempelfråga**

```xml
{
  adventureList {
    items {
      _path,
      _metadata {
        stringMetadata {
          name,
          value
        }
        stringArrayMetadata {
          name,
          value
        }
        intMetadata {
          name,
          value
        }
        intArrayMetadata {
          name,
          value
        }
        floatMetadata {
          name,
          value
        }
        floatArrayMetadata {
          name,
          value
        }
        booleanMetadata {
          name,
          value
        }
        booleanArrayMetadata {
          name,
          value
        }
        calendarMetadata {
          name,
          value
        }
        calendarArrayMetadata {
          name,
          value
        }
      }
    }
  }
}
```

### Exempelfråga för ett enstaka innehållsfragment av en given modell {#sample-wknd-single-content-fragment-of-given-model}

Detta exempel på frågor intervjuar:

* för ett enda innehållsfragment av typen `article` vid en viss sökväg
   * där alla format:
      * HTML
      * Markdown
      * Oformaterad text
      * JSON

**Exempelfråga**

```xml
{
  articleByPath (_path: "/content/dam/wknd/en/magazine/alaska-adventure/alaskan-adventures") {
    item {
        _path
        author
        main {
          html
          markdown
          plaintext
          json
        }
    }
  }
}
```

### Exempelfråga för en innehållsfragmentmodell från en modell {#sample-wknd-content-fragment-model-from-model}

Detta exempel på frågor intervjuar:

* för ett enda innehållsfragment
   * information om den underliggande modellen för innehållsfragment

**Exempelfråga**

```xml
{
  adventureByPath(_path: "/content/dam/wknd/en/adventures/riverside-camping-australia/riverside-camping-australia") {
    item {
      _path
      adventureTitle
      _model {
        _path
        title
      }
    }
  }
}
```

### Exempelfråga för ett kapslat innehållsfragment - typ av en modell{#sample-wknd-nested-fragment-single-model}

Den här frågan förhör:

* för ett enda innehållsfragment av typen `article` vid en viss sökväg
   * i det, sökvägen och författaren till det refererade (kapslade) fragmentet

>[!NOTE]
>
>Fältet `referencearticle` har datatypen `fragment-reference`.

**Exempelfråga**

```xml
{
  articleByPath (_path: "/content/dam/wknd/en/magazine/skitouring/skitouring") {
    item {
        _path
        author
        referencearticle {
          _path
          author
      }
    }
  }
}
```

### Exempelfråga för ett kapslat innehållsfragment - flera modelltyper{#sample-wknd-nested-fragment-multiple-model}

Den här frågan förhör:

* för flera innehållsfragment av typen `bookmark`
   * med fragmentreferenser till andra fragment av de specifika modelltyperna `article` och `adventure`

>[!NOTE]
>
>Fältet `fragments` har datatypen `fragment-reference`, med modellerna `Article`, `Adventure` markerat.

```xml
{
  bookmarkList {
    items {
        fragments {
          ... on ArticleModel {
            _path
            author
          }
          ... on AdventureModel {
            _path
            adventureTitle
          }
        }
     }
  }
}
```

### Exempelfråga för ett innehållsfragment för en viss modell med innehållsreferenser{#sample-wknd-fragment-specific-model-content-reference}

Det finns två varianter av den här frågan:

1. Returnera alla innehållsreferenser.
1. Returnera de specifika innehållsreferenserna av typen `attachments`.

De här frågorna förhör:

* för flera innehållsfragment av typen `bookmark`
   * med Innehållsreferenser till andra fragment

#### Exempelfråga för flera innehållsfragment med förhämtade referenser {#sample-wknd-multiple-fragments-prefetched-references}

Följande fråga returnerar alla innehållsreferenser genom att använda `_references`:

```xml
{
  bookmarkList {
     _references {
         ... on ImageRef {
          _path
          type
          height
        }
        ... on MultimediaRef {
          _path
          type
          size
        }
        ... on DocumentRef {
          _path
          type
          author
        }
        ... on ArchiveRef {
          _path
          type
          format
        }
    }
    items {
        _path
    }
  }
}
```

#### Exempelfråga för flera innehållsfragment med bifogade filer {#sample-wknd-multiple-fragments-attachments}

Följande fråga returnerar alla `attachments` - ett specifikt fält (undergrupp) av typen `content-reference`:

>[!NOTE]
>
>Fältet `attachments` har datatypen `content-reference`, med olika formulär markerade.

```xml
{
  bookmarkList {
    items {
      attachments {
        ... on PageRef {
          _path
          type
        }
        ... on ImageRef {
          _path
          width
        }
        ... on MultimediaRef {
          _path
          size
        }
        ... on DocumentRef {
          _path
          author
        }
        ... on ArchiveRef {
          _path
          format
        }
      }
    }
  }
}
```

### Exempelfråga för ett enskilt innehållsfragment med intern referens för textredigering {#sample-wknd-single-fragment-rte-inline-reference}

Den här frågan förhör:

* för ett enda innehållsfragment av typen `bookmark` vid en viss sökväg
   * i det, textbundna RTE-referenser

>[!NOTE]
>
>De textbundna RTE-referenserna är hydratiserade i `_references`.

**Exempelfråga**

```xml
{
  bookmarkByPath(_path: "/content/dam/wknd/en/bookmarks/skitouring") {
    item {
      _path
      description {
        json
      }
    }
    _references {
      ... on ArticleModel {
        _path
      }
      ... on AdventureModel {
        _path
      }
      ... on ImageRef {
        _path
      }
      ... on MultimediaRef {
        _path
      }
      ... on DocumentRef {
        _path
      }
      ... on ArchiveRef {
        _path
      }
    }
  }
}
```

### Exempelfråga för en enstaka variant av innehållsfragment av en given modell {#sample-wknd-single-fragment-given-model}

Den här frågan förhör:

* för ett enda innehållsfragment av typen `article` vid en viss sökväg
   * inom detta, de uppgifter som avser variationen: `variation1`

**Exempelfråga**

```xml
{
  articleByPath (_path: "/content/dam/wknd/en/magazine/alaska-adventure/alaskan-adventures", variation: "variation1") {
    item {
      _path
      author
      main {
        html
        markdown
        plaintext
        json
      }
    }
  }
}
```

### Exempelfråga för en namngiven variant av flera innehållsfragment i en given modell {#sample-wknd-variation-multiple-fragment-given-model}

Den här frågan förhör:

* för innehållsfragment av typen `article` med en specifik variation: `variation1`

**Exempelfråga**

```xml
{
  articleList (variation: "variation1") {
    items {
      _path
      author
      main {
        html
        markdown
        plaintext
        json
      }
    }
  }
}
```

### Exempelfråga för flera innehållsfragment för en viss språkinställning {#sample-wknd-multiple-fragments-given-locale}

Den här frågan förhör:

* för innehållsfragment av typen `article` inom `fr` locale

**Exempelfråga**

```xml
{ 
  articleList (_locale: "fr") {
    items {
      _path
      author
      main {
        html
        markdown
        plaintext
        json
      }
    }
  }
}
```

## Exempel på struktur för innehållsfragment (används med GraphQL) {#content-fragment-structure-graphql}

Exempelfrågorna baseras på följande struktur som använder:

* en eller flera, [Exempel på modeller för innehållsfragment](#sample-content-fragment-models-schemas) - utgör grunden för GraphQL-scheman

* [Exempel på innehållsfragment](#sample-content-fragments) baserat på ovanstående modeller

### Exempel på modeller för innehållsfragment (scheman) {#sample-content-fragment-models-schemas}

För exempelfrågorna använder vi följande innehållsmodeller och deras inbördes relationer (referenser ->):

* [Företag](#model-company)
-> [Person](#model-person)
    -> [Utmärkelse](#model-award)

* [Ort](#model-city)

#### Företag {#model-company}

De grundläggande fälten som definierar företaget är:

| Fältnamn | Datatyp | Referens |
|--- |--- |--- |
| Företag | Enkelradig text |  |
| VD | Fragmentreferens (enkel) | [Person](#model-person) |
| Anställda | Fragmentreferens (multifält) | [Person](#model-person) |

#### Person {#model-person}

Fälten som definierar en person, som också kan vara en medarbetare:

| Fältnamn | Datatyp | Referens |
|--- |--- |--- |
| Namn | Enkelradig text |  |
| Förnamn | Enkelradig text |  |
| Utmärkelser | Fragmentreferens (multifält) | [Utmärkelse](#model-award) |

#### Utmärkelse {#model-award}

Fälten som definierar en utmärkelse är:

| Fältnamn | Datatyp | Referens |
|--- |--- |--- |
| Genväg/ID | Enkelradig text |  |
| Titel | Enkelradig text |  |

#### Ort {#model-city}

Fälten för att definiera en stad är:

| Fältnamn | Datatyp | Referens |
|--- |--- |--- |
| Namn | Enkelradig text |  |
| Land | Enkelradig text |  |
| Population | Siffra |  |
| Kategorier | Taggar |  |

### Exempel på innehållsfragment {#sample-content-fragments}

Följande fragment används för rätt modell.

#### Företag {#fragment-company}

| Företag | VD | Anställda |
|--- |--- |--- |
| Apple | Steve Jobs | Duke Marsh<br>Max. textfält |
|  Little Pony Inc. | Adam Smith | Lara Croft<br>Cutter Slade |
| NextStep Inc. | Steve Jobs | Joe Smith<br>Abe Lincoln |

#### Person {#fragment-person}

| Namn | Förnamn | Utmärkelser |
|--- |--- |--- |
| Lincoln |  Adobe |  |
| Smith | Adam |   |
| Slade |  Rensare |  Gameblitz<br>Gamestar |
| Marmor |  Duke |   |   |
|  Smith |  Joe |   |
| Beskär |  Lara | Gamestar |
| Caulfield |  Max |  Gameblitz |
|  Jobb |  Steve |   |

#### Utmärkelse {#fragment-award}

| Genväg/ID | Titel |
|--- |--- |
| GB | Gameblitz |
|  GS | Gamestar |
|  OSC | Oscar |

#### Ort {#fragment-city}

| Namn | Land | Population | Kategorier |
|--- |--- |--- |--- |
| Basel | Schweiz | 172258 | stad:emea |
| Berlin | Tyskland | 3669491 | stad:huvudstad<br>stad:emea |
| Bucharest | Rumänien | 1821000 |  stad:huvudstad<br>stad:emea |
| San Francisco |  USA |  883306 |  stad:strand<br>stad:na |
| San Jose |  USA |  102635 |  stad:na |
| Stuttgart |  Tyskland |  634830 |  stad:emea |
|  Zürich |  Schweiz |  415367 |  stad:huvudstad<br>stad:emea |

---
title: Lära sig använda GraphQL med AEM - exempelinnehåll och frågor
description: Lär dig använda GraphQL med AEM så att du kan leverera innehåll utan problem genom att utforska exempelinnehåll och frågor.
feature: Headless, Content Fragments,GraphQL API
exl-id: b60fcf97-4736-4606-8b41-4051b8b0c8a7
role: Admin, Developer
source-git-commit: fdfe0291ca190cfddf3bed363a8c2271a65593a1
workflow-type: tm+mt
source-wordcount: '1938'
ht-degree: 0%

---

# Lära sig använda GraphQL med AEM - exempelinnehåll och frågor {#learn-graphql-with-aem-sample-content-queries}

Lär dig använda GraphQL med AEM så att du kan leverera innehåll utan problem genom att utforska exempelinnehåll och frågor.

>[!NOTE]
>
>Läs den här sidan tillsammans med följande:
>
>* [Innehållsfragment](/help/sites-cloud/administering/content-fragments/overview.md)
>* [Modeller för innehållsfragment](/help/sites-cloud/administering/content-fragments/content-fragment-models.md)
>* [AEM GraphQL API för användning med innehållsfragment](/help/headless/graphql-api/content-fragments.md)

Om du vill komma igång med GraphQL-frågor och hur de fungerar med AEM Content Fragments kan det vara bra att se några praktiska exempel.

Mer information finns i:

* Ett [exempel på struktur för innehållsfragment](#content-fragment-structure-graphql)

* Och några [exempel på GraphQL-frågor](#graphql-sample-queries) som baseras på innehållsfragmentstrukturen (Content Fragment Models och relaterade innehållsfragment).

>[!CONTEXTUALHELP]
>id="aemcloud_headless_graphql_sample"
>title="Lära sig använda GraphQL med AEM - exempelinnehåll och frågor"
>abstract="Lär dig använda GraphQL med AEM för att leverera innehåll utan problem genom att utforska exempelinnehåll och frågor."

## GraphQL - Exempelfrågor med strukturen för exempelinnehållsfragment {#graphql-sample-queries-sample-content-fragment-structure}

I de här exempelfrågorna finns illustrationer av hur du skapar frågor, tillsammans med exempelresultat.

>[!NOTE]
>
>Beroende på din instans kan du få direkt åtkomst till [GraphiQL-gränssnittet som ingår i AEM GraphQL API](/help/headless/graphql-api/graphiql-ide.md) för att skicka och testa frågor.
>
>Du kan öppna frågeredigeraren från:
>
>* **Verktyg** > **Allmänt** > **GraphQL Query Editor**
>* direkt, till exempel `http://localhost:4502/aem/graphiql.html`

>[!NOTE]
>
>Exempelfrågorna är baserade på [strukturen för exempelinnehållsfragment som kan användas med GraphQL](#content-fragment-structure-graphql)

### Exempelfråga - Alla tillgängliga scheman och datatyper {#sample-all-schemes-datatypes}

Returnerar alla `types` för alla tillgängliga scheman.

**Exempelfråga**

```graphql
{
  __schema {
    types {
      name
      description
    }
  }
}
```

**Exempelresultat**

```json
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

Om du vill hämta all information om alla städer kan du använda följande grundläggande fråga:
**Exempelfråga**

```graphql
{
  cityList {
    items
  }
}
```

Vid körning utökas frågan automatiskt så att den omfattar alla fält:

```graphql
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

```json
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

En enkel fråga som returnerar `name` för alla poster i `city`schemat.

**Exempelfråga**

```graphql
query {
  cityList {
    items {
      name
    }
  }
}
```

**Exempelresultat**

```json
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

En fråga som returnerar information om en enskild fragmentpost på en viss plats i databasen.

**Exempelfråga**

```graphql
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

```json
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

Om du skapar en variant med namnet&quot;Berlin Center&quot; (`berlin_centre`) för `city` Berlin kan du använda en fråga för att returnera information om variationen.

**Exempelfråga**

```graphql
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

```json
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

### Exempelfråga - namn på alla städer som taggats som stadbrytningar {#sample-names-all-cities-tagged-city-breaks}

Om du:

* skapa olika taggar med namnet `Tourism` : `Business`, `City Break`, `Holiday`
* och tilldela dem till mallvarianten av olika `City` instanser

Sedan kan du använda en fråga för att returnera information om `name` och `tags` för alla poster som är taggade som City Breaks i `city`schemat.

**Exempelfråga**

```xml
query {
  cityList(
    includeVariations: true,
    filter: {_tags: {_expressions: [{value: "tourism:city-break", _operator: CONTAINS}]}}
  ){
    items {
      name,
      _tags
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
          "name": "Berlin",
          "_tags": [
            "tourism:city-break",
            "tourism:business"
          ]
        },
        {
          "name": "Zurich",
          "_tags": [
            "tourism:city-break",
            "tourism:business"
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

```graphql
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

```json
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

En fråga som filtrerar alla `persons` för alla som har namnet `Jobs` eller `Smith`.

**Exempelfråga**

```graphql
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

```json
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

En fråga som filtrerar alla `persons` för alla som har namnet `Jobs` eller `Smith`.

**Exempelfråga**

```graphql
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

```json
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

```graphql
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

```json
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

Här filtreras en kombination av fält. En `AND` (implicit) används för att markera `population`intervallet, medan en `OR` (explicit) används för att välja de önskade städerna.

**Exempelfråga**

```graphql
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

```json
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

```graphql
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

```json
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

Den här frågan filtrerar på en array med ett objekt (`city:na`) som måste förekomma minst en gång.

**Exempelfråga**

```graphql
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

```json
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

```graphql
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

```json
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

Den här frågan visar filtrering för `person` av `name` &quot;Smith&quot;, vilket returnerar information från två kapslade fragment - `company` och `employee`.

**Exempelfråga**

```graphql
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

```json
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

Den här frågan visar filtrering över tre kapslade fragment - `company`, `employee` och `award`.

**Exempelfråga**

```graphql
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

```json
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

Den här frågan visar filtrering över tre kapslade fragment - `company`, `employee` och `award`.

**Exempelfråga**

```graphql
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

```json
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

Dessa exempelfrågor är baserade på WKND-projektet. Den har följande:

* Content Fragment Models available under:
  `http://<hostname>:<port>/libs/dam/cfm/models/console/content/models.html/conf/wknd`

* Innehållsfragment (och annat innehåll) tillgängliga under:
  `http://<hostname>:<port>/assets.html/content/dam/wknd/en`
  `http://<hostname>:<port>/assets.html/content/dam/wknd-shared/en`

>[!NOTE]
>
>Eftersom resultaten kan bli omfattande återges de inte här.

### Exempelfråga för alla innehållsfragment i en viss modell med de angivna egenskaperna {#sample-wknd-all-model-properties}

Detta exempel på frågor intervjuar:

* för alla innehållsfragment av typen `article`
* med `_path` och egenskaperna för `authorFragment`.

**Exempelfråga**

```graphql
{
  articleList {
    items {
      _path
      authorFragment {
        _path
        firstName
        lastName
        birthDay
      }
    }
 }
}
```

### Exempelfråga för metadata {#sample-wknd-metadata}

Den här frågan förhör:

* för alla innehållsfragment av typen `adventure`
* metadata

**Exempelfråga**

```graphql
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

* för ett enstaka innehållsfragment av typen `article` vid en specifik sökväg
   * inom det fragmentet, alla innehållsformat:
      * HTML
      * Markering
      * Oformaterad text
      * JSON

**Exempelfråga**

```graphql
{
  articleByPath(_path: "/content/dam/wknd-shared/en/magazine/alaska-adventure/alaskan-adventures") {
    item {
        _path
        authorFragment {
          _path
          firstName
          lastName
          birthDay
        }
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

```graphql
{
  adventureByPath(_path: "/content/dam/wknd-shared/en/magazine/western-australia/western-australia-by-camper-van") {
    item {
      _path
      title
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

* för ett enstaka innehållsfragment av typen `article` vid en specifik sökväg
   * inom det fragmentet, sökvägen och författaren till det refererade (kapslade) fragmentet

>[!NOTE]
>
>Fältet `referencearticle` har datatypen `fragment-reference`.

**Exempelfråga**

```graphql
{
  adventureByPath(_path: "/content/dam/wknd-shared/en/magazine/western-australia/western-australia-by-camper-van") {
    item {
      _path
      title
      _model {
        _path
        title
      }
    }
  }
}
```

### Exempelfråga för ett kapslat innehållsfragment - flera modelltyper{#sample-wknd-nested-fragment-multiple-model}

#### En refererad modelltyp

Den här frågan förhör:

* för flera innehållsfragment av typen `bookmark`
   * med fragmentreferenser till andra fragment av den specifika modelltypen `Article`

>[!NOTE]
>
>Fältet `fragments` har datatypen `fragment-reference`, med modellen `Article` markerad. Frågan levererar `fragments` som en matris av `[Article]`.

```graphql
{
  bookmarkList {
    items {
        fragments {
          _path
          author
        }
     }
  }
}
```

#### Flera refererade modelltyper

Den här frågan förhör:

* för flera innehållsfragment av typen `bookmark`
   * med fragmentreferenser till andra fragment av de specifika modelltyperna `Article` och `Adventure`

>[!NOTE]
>
>Fältet `fragments` har datatypen `fragment-reference`, med modellerna `Article`, `Adventure` markerad. Frågan levererar `fragments` som en matris av `[AllFragmentModels]`, som är avrefererad med unionstypen.

```graphql
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
1. Returnerar de specifika innehållsreferenserna av typen `attachments`.

De här frågorna förhör:

* för flera innehållsfragment av typen `bookmark`
   * med Innehållsreferenser till andra fragment

#### Exempelfråga för flera innehållsfragment med förhämtade referenser {#sample-wknd-multiple-fragments-prefetched-references}

Följande fråga returnerar alla innehållsreferenser med hjälp av `_references`:

<!-- need replacement query -->

```graphql
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

<!-- need replacement query -->

```graphql
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

### Exempelfrågor för ett innehållsfragment för en viss modell med hjälp av UUID-referenser {#sample-wknd-fragment-specific-model-uuid-references}

De här frågorna förhör:

* UUID för ett innehållsfragment och för refererade innehållsfragment eller resurser
* resultatet returneras via JSON-egenskapen `_id`

#### Exempelfråga för ett innehållsfragment för en viss modell med hjälp av en UUID-referens {#sample-wknd-fragment-specific-model-using-a-uuid-reference}

Följande fråga returnerar alla innehållsreferenser med hjälp av `_id` och `_path`:

```graphql
{
  articleList {
    items {
        _id
        _path
        title
        featuredImage {
          ... on ImageRef {
            _id
            _path           
          }
        }
        authorFragment {
          firstName
          lastName
          profilePicture {
            ... on ImageRef {
              _id
              _path
            }
          }
        }
      }
  }
}
```

#### Exempelfråga för innehållsfragment efter UUID-referens {#sample-wknd-fragment-specific-model-by-uuid-reference}

Följande fråga returnerar alla innehållsreferenser som är relaterade till en specifik `_id`:

```graphql
{
  articleById(_id: "3ce2bf53-7436-4d3e-b19a-2793bc2ca63e") {
    item {
      _id
      _path
      title
      featuredImage {
        ... on ImageRef {
          _id
          _path
        }
      }
      authorFragment {
        firstName
        lastName
        profilePicture {
          ... on ImageRef {
            _id
            _path
          }
        }
      }
    }
  }
}
```

### Exempelfråga för ett enskilt innehållsfragment med intern referens för textredigering {#sample-wknd-single-fragment-rte-inline-reference}

Den här frågan förhör:

* för ett enstaka innehållsfragment av typen `bookmark` vid en specifik sökväg
   * i det, textbundna RTE-referenser

>[!NOTE]
>
>De textbundna RTE-referenserna är hydratiserade i `_references`.

<!-- need replacement query -->

**Exempelfråga**

```graphql
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

* för ett enstaka innehållsfragment av typen `author` vid en specifik sökväg
   * inom det fragmentet, data relaterade till variationen: `another`

**Exempelfråga**

```graphql
{
  authorByPath(_path: "/content/dam/wknd-shared/en/contributors/ian-provo", variation: "another") {
    item {
        _path
        _variation
        firstName
        lastName
        birthDay
    }
  }
}
```

### Exempelfråga för en namngiven variant av flera innehållsfragment i en given modell {#sample-wknd-variation-multiple-fragment-given-model}

Den här frågan förhör:

* för innehållsfragment av typen `author` med en specifik variant: `another`

>[!NOTE]
>
>Den här frågan visar återfall för innehållsfragment som inte har en [variant](/help/headless/graphql-api/content-fragments.md#variations) av det angivna namnet.

**Exempelfråga**

```graphql
{
  authorList(variation: "another") {
    items {
        _path
        _variation
        firstName
        lastName
        birthDay
    }
  }
}
```

### Exempelfråga för flera innehållsfragment, och deras variationer, för en given modell {#sample-wknd-multiple-fragment-variations-given-model}

Den här frågan förhör:

* för innehållsfragment av typen `article` och alla variationer

**Exempelfråga**

```xml
query {
  articleList(
    includeVariations: true  ){
    items {
      _variation
      _path
      _tags
      _metadata {
        stringArrayMetadata {
          name
          value
        }
      }
    }
  }
}
```

### Exempelfråga för innehållsfragmentvariationer för en viss modell som har en specifik tagg bifogad{#sample-wknd-fragment-variations-given-model-specific-tag}

Den här frågan förhör:

* för innehållsfragment av typen `article` med en eller flera variationer med taggen `WKND : Activity / Hiking`

**Exempelfråga**

```xml
{
  articleList(
    includeVariations: true,
    filter: {_tags: {_expressions: [{value: "wknd:activity/hiking", _operator: CONTAINS}]}}
  ){
    items {
      _variation
      _path
      _tags
      _metadata {
        stringArrayMetadata {
          name
          value
        }
      }
    }
  }
}
```

### Exempelfråga för flera innehållsfragment för en viss språkinställning {#sample-wknd-multiple-fragments-given-locale}

Den här frågan förhör:

* för innehållsfragment av typen `article` i språkinställningen `fr`

**Exempelfråga**

```graphql
{ 
  articleList(_locale: "fr") {
    items {
      _path
      authorFragment {
        _path
        firstName
        lastName
        birthDay
      }
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

### Samplingslistefråga med förskjutning och begränsning {#sample-list-offset-limit}

Den här frågan förhör:

* för sidan med resultat som innehåller upp till fem artiklar, från den femte artikeln i resultatlistan *complete*

**Exempelfråga**

```graphql
{
   articleList(offset: 5, limit: 5) {
    items {
      authorFragment {
        _path
        firstName
        lastName
        birthDay
      }
      _path
    }
  }
}
```

### Exempelsidnumreringsfråga som använder första och efter  {#sample-pagination-first-after}

Den här frågan förhör:

* för sidan med resultat som innehåller upp till fem äventyr, med början från markörobjektet i resultatlistan *complete*

**Exempelfråga**

```graphql
{
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

### Exempelfråga med filtrering efter _tagg-ID och utan variationer {#sample-filtering-tag-not-variations}

Den här frågan förhör:

* för innehållsfragment av typen `vehicle` med taggen `big-block`
* utom variationer

**Exempelfråga**

```graphql
query {
  vehicleList(
    filter: {
    _tags: {
      _expressions: [
        {
          value: "vehicles:big-block"
          _operator: CONTAINS
        }
      ]
    }
  }) {
    items {
      _variation
      _path
      type
      name
      model
      fuel
      _tags
    }
  }
} 
```

### Exempelfråga med filtrering efter _tagg-ID och inklusive variationer {#sample-filtering-tag-with-variations}

Den här frågan förhör:

* för innehållsfragment av typen `vehicle` med taggen `big-block`
* inklusive variationer

**Exempelfråga**

```graphql
{
  enginePaginated(after: "SjkKNmVkODFmMGQtNTQyYy00NmQ4LTljMzktMjhlNzQwZTY1YWI2Cmo5", first: 9 ,includeVariations:true, sort: "name",
    filter: {
    _tags: {
      _expressions: [
        {
          value: "vehicles:big-block"
          _operator: CONTAINS
        }
      ]
    }
  }) {
    edges{
    node {
        _variation
        _path
        name
        type
        size
        _tags
        _metadata {
          stringArrayMetadata {
            name
            value
          }
        }
    }
      cursor
    }
  }
} 
```

## Exempelfrågor för leverans av DAM och Dynamic Media Assets {#sample-queries-delivery-DAM-DM}

För webboptimerad bildleverans (av DAM-resurser):

* [Exempelfråga för webboptimerad bildleverans med fullständiga parametrar](/help/headless/graphql-api/content-fragments.md#web-optimized-image-delivery-full-parameters)

* [Exempelfråga för webboptimerad bildleverans med en enda angiven parameter](/help/headless/graphql-api/content-fragments.md#web-optimized-image-delivery-single-query-variable)

För leverans av URL:en till en Dynamic Media-resurs

* Se [Exempelfråga för leverans av dynamiska medieresurser via URL - Bildreferens](/help/headless/graphql-api/content-fragments.md#sample-query-dynamic-media-asset-delivery-by-url-imageref)

* Se [Exempelfråga för leverans av dynamiska mediefiler via URL - flera referenser](/help/headless/graphql-api/content-fragments.md#sample-query-dynamic-media-asset-delivery-by-url-multiple-refs)

För leverans av fjärrresurser som inte är lokala till den aktuella AEM-instansen från Content Fragment Editor.

* Se [Exempelfråga för Dynamic Media för OpenAPI-objektstöd (Remote Assets)](/help/headless/graphql-api/content-fragments.md#sample-query-dynamic-media-for-openapi-asset-support)

## Exempel på struktur för innehållsfragment (används med GraphQL) {#content-fragment-structure-graphql}

Exempelfrågorna baseras på följande struktur som använder:

* En eller flera [modeller för exempelinnehållsfragment](#sample-content-fragment-models-schemas) - utgör grunden för GraphQL-scheman

* [Exempelinnehållsfragment](#sample-content-fragments) baserat på modellerna ovan

### Exempel på modeller för innehållsfragment (scheman) {#sample-content-fragment-models-schemas}

För exempelfrågorna använder du följande innehållsmodeller och deras inbördes relationer (referenser ->):

* [Företag](#model-company)
-> [Person](#model-person)
    -> [Utmärkelse](#model-award)

* [Ort](#model-city)

#### Företag {#model-company}

De grundläggande fälten som definierar företaget är:

| Fältnamn | Datatyp | Referens |
|--- |--- |--- |
| Företagsnamn | Enkelradig text | |
| VD | Fragmentreferens (enkel) | [Person](#model-person) |
| Anställda | Fragmentreferens (multifält) | [Person](#model-person) |

#### Person {#model-person}

Fälten som definierar en person, som också kan vara en medarbetare:

| Fältnamn | Datatyp | Referens |
|--- |--- |--- |
| Namn | Enkelradig text | |
| Förnamn | Enkelradig text | |
| Utmärkelser | Fragmentreferens (multifält) | [Utmärkelse](#model-award) |

#### Utmärkelse {#model-award}

Fälten som definierar en utmärkelse är:

| Fältnamn | Datatyp | Referens |
|--- |--- |--- |
| Genväg/ID | Enkelradig text | |
| Titel | Enkelradig text | |

#### Ort {#model-city}

Fälten för att definiera en stad är:

| Fältnamn | Datatyp | Referens |
|--- |--- |--- |
| Namn | Enkelradig text | |
| Land | Enkelradig text | |
| Population | Nummer | |
| Kategorier | Taggar | |

### Exempel på innehållsfragment {#sample-content-fragments}

Följande fragment används för rätt modell.

#### Företag {#fragment-company}

| Företagsnamn | VD | Anställda |
|--- |--- |--- |
| Apple | Steve Jobs | Duke Marsh<br>Max Caulfield |
| Little Pony Inc. | Adam Smith | Lara Crop<br>Cutter Slade |
| NextStep Inc. | Steve Jobs | Joe Smith<br>Abe Lincoln |

#### Person {#fragment-person}

| Namn | Förnamn | Utmärkelser |
|--- |--- |--- |
| Lincoln | Adobe | |
| Smith | Adam | |
| Slade | Rensare | Gameblitz<br>Gamestar |
| Marmor | Duke | |
| Smith | Joe | |
| Beskär | Lara | Gamestar |
| Caulfield | Max | Gameblitz |
| Jobb | Steve | |

#### Utmärkelse {#fragment-award}

| Genväg/ID | Titel |
|--- |--- |
| GB | Gameblitz |
| GS | Gamestar |
| OSC | Oscar |

#### Ort {#fragment-city}

| Namn | Land | Population | Kategorier |
|--- |--- |--- |--- |
| Basel | Schweiz | 172258 | stad:emea |
| Berlin | Tyskland | 3669491 | stad:huvudstad<br>stad:emea |
| Bucharest | Rumänien | 1821000 | stad:huvudstad<br>stad:emea |
| San Francisco | USA | 883306 | city:beach<br>city:na |
| San Jose | USA | 102635 | stad:na |
| Stuttgart | Tyskland | 634830 | stad:emea |
| Zürich | Schweiz | 415367 | stad:huvudstad<br>stad:emea |

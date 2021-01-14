---
title: Att lära sig använda GraphQL med AEM - exempelinnehåll och frågor
description: Lär dig använda GraphQL med AEM - exempelinnehåll och frågor.
translation-type: tm+mt
source-git-commit: da8fcf1288482d406657876b5d4c00b413461b21
workflow-type: tm+mt
source-wordcount: '1298'
ht-degree: 2%

---


# Lära sig att använda GraphQL med AEM - exempelinnehåll och frågor {#learn-graphql-with-aem-sample-content-queries}

>[!CAUTION]
>
>AEM GraphQL API för leverans av innehållsfragment är tillgänglig på begäran.
>
>Kontakta [Adobe Support](https://experienceleague.adobe.com/?lang=en&amp;support-solution=General#support) om du vill aktivera API:t för din AEM som ett Cloud Service-program.

Om du vill komma igång med GraphQL-frågor och hur de fungerar med AEM innehållsfragment kan du se några praktiska exempel.

Mer information finns i:

* A [sample Content Fragment structure](#content-fragment-structure-graphql)

* Och några [exempel på GraphQL-frågor](#graphql-sample-queries), baserade på fragmentstrukturen för exempelinnehåll (modeller för innehållsfragment och relaterade innehållsfragment).

## GraphQL för AEM - Vissa tillägg {#graphql-some-extensions}

Den grundläggande åtgärden för frågor med GraphQL för AEM följer standarden GraphQL-specifikation. För GraphQL-frågor med AEM finns det några tillägg:

* Om du behöver ett enda resultat:
   * använda modellnamnet, eg stad

* Om du förväntar dig en resultatlista:
   * lägga till&quot;Lista&quot; i modellnamnet, till exempel `cityList`

* Om du vill använda ett logiskt OR:
   * använd _logOp: ELLER&quot;

* Logiskt AND finns också, men är (ofta) implicit

* Du kan fråga efter fältnamn som motsvarar fälten i innehållsfragmentmodellen

* Förutom fälten från modellen finns det vissa systemgenererade fält (föregås av understreck):

   * För innehåll:

      * `_locale` : för att avslöja språket, baserat på Language Manager

      * `_metadata` : för att visa metadata för ditt fragment

      * `_path` : sökvägen till ditt innehållsfragment i databasen

      * `_references` : avslöja referenser, inkludera textbundna referenser i RTF-redigeraren

      * `_variations` : för att visa specifika variationer i ditt innehållsfragment
   * Och åtgärder:

      * `_operator` : tillämpa särskilda operatörer,  `EQUALS`,  `EQUALS_NOT`,  `GREATER_EQUAL`,  `LOWER`,  `CONTAINS`,

      * `_apply` : tillämpa särskilda villkor, till exempel   `AT_LEAST_ONCE`

      * `_ignoreCase` : för att ignorera skiftläget vid fråga


* Det finns stöd för unionstyper för GraphQL:

   * use `...on`


## Ett exempel på struktur för innehållsfragment som används med GraphQL {#content-fragment-structure-graphql}

Vi behöver ett enkelt exempel:

* En eller flera [modeller för exempelinnehållsfragment](#sample-content-fragment-models-schemas) - utgör grunden för GraphQL-scheman

* [Exempelinnehåll ](#sample-content-fragments) fragmenterbaserat på ovanstående modeller

### Exempel på modeller för innehållsfragment (scheman) {#sample-content-fragment-models-schemas}

För exempelfrågorna använder vi följande innehållsmodeller och deras inbördes relationer (referenser ->):

* [Company](#model-company)
->  [Person](#model-person)
    ->  [Award](#model-award)

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

### Exempelinnehållsfragment {#sample-content-fragments}

Följande fragment används för rätt modell.

#### Företag {#fragment-company}

| Företag | VD | Anställda |
|--- |--- |--- |
| Apple | Steve Jobs | Duke Marsh<br>Max Caulfield |
|  Little Pony Inc. | Adam Smith | Lara Crop<br>Städerplatta |
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
| San Francisco |  USA |  883306 |  city:beach<br>city:na |
| San Jose |  USA |  102635 |  stad:na |
| Stuttgart |  Tyskland |  634830 |  stad:emea |
|  Zürich |  Schweiz |  415367 |  stad:huvudstad<br>stad:emea |

## GraphQL - Exempelfrågor med strukturen för exempelinnehållsfragment {#graphql-sample-queries-sample-content-fragment-structure}

Se exempelfrågorna för illustrationer av hur du skapar frågor tillsammans med exempelresultat.

>[!NOTE]
>
>Beroende på din instans kan du komma åt det [Graph *i* QL-gränssnitt som ingår i AEM GraphQL API](/help/assets/content-fragments/graphql-api-content-fragments.md#graphiql-interface) för att skicka och testa frågor.
>
>Till exempel: `http://localhost:4502/content/graphiql.html`

### Exempelfråga - Alla tillgängliga scheman och datatyper {#sample-all-schemes-datatypes}

Detta returnerar alla typer för alla tillgängliga scheman.

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

Detta är en enkel fråga som returnerar `name`alla poster i `city`schemat.

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

### Exempelfråga - Ett enkelt stadsfragment {#sample-single-city-fragment}

Det här är en fråga som returnerar information om ett enskilt fragment på en viss plats i databasen.

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

Om du skapar en ny variant med namnet&quot;Berlin Center&quot; (`berlin_centre`) för `city` Berlin kan du använda en fråga för att returnera information om variationen.

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

### Exempelfråga - Alla personer som har namnet &quot;Jobs&quot; eller &quot;Smith&quot; {#sample-all-persons-jobs-smith}

Detta filtrerar alla `persons` för alla som har namnet `Jobs`eller `Smith`.

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

Detta filtrerar alla `persons` för alla som har namnet `Jobs`eller `Smith`.

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

### Exempelfråga - Alla städer i Tyskland eller Schweiz med en befolkning mellan 400000 och 99999 {#sample-all-cities-d-ch-population}

Här filtreras en kombination av fält. Ett `AND`-värde (implicit) används för att välja `population`intervallet, medan ett `OR` (explicit) används för att välja önskade städer.

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

Den här frågan filtrerar en array med ett objekt (`city:na`) som måste förekomma minst en gång.

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

Den här frågan visar filtrering för `person` av `name` &quot;Smith&quot;, vilket returnerar information från två kapslade fragment - `company` och `employee`.

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

### Exempelfråga för kapslade innehållsfragment - Alla företag där alla anställda har vunnit utmärkelsen &quot;Gamestar&quot; {#sample-all-companies-employee-gamestar-award}

Den här frågan visar filtrering över tre kapslade fragment - `company`, `employee` och `award`.

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

### Exempelfråga för metadata - Ange metadata för utmärkelserna GB {#sample-metadata-awards-gb}

Den här frågan visar filtrering över tre kapslade fragment - `company`, `employee` och `award`.

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

Dessa exempelfrågor är baserade på WKND-projektet.

>[!NOTE]
>
>Eftersom resultaten kan bli omfattande återges de inte här.

### Exempelfråga för alla innehållsfragment i en viss modell med de angivna egenskaperna {#sample-wknd-all-model-properties}

Detta exempel på frågor intervjuar:

* för alla innehållsfragment av typen `article`
* med egenskaperna `path`och `author`.

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

* för ett enstaka innehållsfragment av en viss modell
* för alla innehållsformat:
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

### Exempelfråga för ett kapslat innehållsfragment - typ av en modell{#sample-wknd-nested-fragment-single-model}

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

### Exempelfråga för ett kapslat innehållsfragment - Flera modelltyper{#sample-wknd-nested-fragment-multiple-model}

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

### Exempelfråga för ett innehållsfragment för en viss modell med en innehållsreferens{#sample-wknd-fragment-specific-model-content-reference}

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

### Exempelfråga för flera innehållsfragment med förhämtade referenser {#sample-wknd-multiple-fragments-prefetched-references}

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
  }
}
```

### Exempelfråga för en enstaka variant av innehållsfragment av en given modell {#sample-wknd-single-fragment-given-model}

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

### Exempelfråga för flera innehållsfragment för en given språkinställning {#sample-wknd-multiple-fragments-given-locale}

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

### Exempelfråga för ett enskilt innehållsfragment med intern RTE-referens {#sample-wknd-single-fragment-rte-inline-reference}

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

### Exempelfråga för en namngiven variant av flera innehållsfragment i en given modell {#sample-wknd-variation-multiple-fragment-given-model}

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

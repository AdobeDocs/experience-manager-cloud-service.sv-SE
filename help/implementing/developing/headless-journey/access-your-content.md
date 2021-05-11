---
title: Få åtkomst till ditt innehåll via AEM-API:er
description: I den här delen av AEM Headless Developer Journey kan du lära dig hur du använder GraphQL-frågor för att komma åt innehållet i innehållsfragment.
hide: true
hidefromtoc: true
index: false
exl-id: 5ef557ff-e299-4910-bf8c-81c5154ea03f
translation-type: tm+mt
source-git-commit: c9b8e14a3beca11b6f81f2d5e5983d6fd801bf3f
workflow-type: tm+mt
source-wordcount: '846'
ht-degree: 1%

---

# Så här kommer du åt ditt innehåll via AEM Delivery API:er {#access-your-content}

>[!CAUTION]
>
>ARBETE PÅGÅR - Dokumentet skapas för närvarande och ska inte tolkas som fullständigt eller slutgiltigt och inte heller användas i tillverkningssyfte.

I den här delen av [AEM Headless Developer Journey](overview.md) kan du lära dig hur du använder GraphQL-frågor för att komma åt innehållet i dina innehållsfragment och skicka det till din app (headless delivery).

## Berättelsen hittills {#story-so-far}

I det föregående dokumentet från den AEM resan, [How to Model Your Content](model-your-content.md), lärde du dig grunderna i innehållsmodellering i AEM, så du bör nu förstå hur du modellerar innehållsstrukturen och sedan inse att strukturen med AEM Content Fragment Models och Content Fragments:

* Identifiera koncept och terminologi i samband med innehållsmodellering.
* Förstå varför innehållsmodellering behövs för leverans av Headless-innehåll.
* Förstå hur ni kan förverkliga den här strukturen med AEM Content Fragment Models (och skapa innehåll med Content Fragments).
* Förstå hur ni modellerar ert innehåll. principer med grundläggande urval.

Den här artikeln bygger på dessa grundläggande funktioner så att du förstår hur du får tillgång till ditt befintliga headless-innehåll i AEM med hjälp av AEM GraphQL API.

* **Målgrupp**: Nybörjare
* **Mål**: Lär dig hur du kommer åt innehållet i dina innehållsfragment med AEM GraphQL-frågor:
   * Introducera GraphQL och AEM GraphQL API.
   * Ta en titt på detaljerna i AEM GraphQL API.
   * Titta på några exempelfrågor för att se hur saker och ting fungerar i praktiken.

## Så du vill komma åt ditt innehåll? {#so-youd-like-to-access-your-content}

Så..har du allt det här innehållet, har en struktur (i innehållsfragment) och väntar bara på att mata in din nya app. Frågan är hur man får dit den?

Vad du behöver är ett sätt att rikta specifikt innehåll, välja vad du behöver och returnera det till appen för vidare bearbetning.

Med Adobe Experience Manager (AEM) som Cloud Service kan du selektivt komma åt dina innehållsfragment med hjälp av det AEM GraphQL-API:t och returnera endast det innehåll du behöver. Det innebär att du kan leverera strukturerat innehåll utan extra kostnad och använda det i dina program.

>[!NOTE]
>
>AEM GraphQL API är en anpassad implementering som baseras på standard-API-specifikationen GraphQL.

<!--
## GraphQL - An Introduction {#graphql-introduction}

GraphQL is an open-source specification that provides:

* a query language that enables you to select specific content from structured objects.
* a runtime to fulfill these queries with your structured content.

GraphQL is a *strongly* typed API. This means that *all* content must be clearly structured and organized by type, so that GraphQL *understands* what to access and how. The data fields are defined within GraphQL schemas, that define the structure of your content objects. 

GraphQL endpoints then provide the paths that respond to the GraphQL queries.

All this means that your app can accurately, reliably and efficiently select the content that it needs - just what you need when used with AEM.

>[!NOTE]
>
>See *GraphQL*.org and *GraphQL*.com.

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

## AEM GraphQL API {#aem-graphql-api}

The AEM GraphQL API is a customized version based on the standard GraphQL API specification, specially configured to allow you to perform (complex) queries on your Content Fragments.

Content Fragments are used, as the content is structured according to Content Fragment Models. This fulfills a basic requirement of GraphQL.

* A Content Fragment Model is built up of one, or more, fields. 
  * Each field is defined according to a Data Type.
* Content Fragment Models are used to generate the corresponding AEM GraphQL Schemas.

To actually access GraphQL for AEM (and the content) an endpoint is used to provide the access path. 

The content returned, via the AEM GraphQL API, can then be used by your applications. 

>[!NOTE]
>
>The AEM GraphQL API implementation is based on the GraphQL Java libraries.

### Use Cases for Author and Publish Environments {#use-cases-author-publish-environments}

The use cases for the AEM GraphQL API can depend on the type of AEM as a Cloud Service environment:

* Publish environment; used to: 
  * Query content for JS application (standard use-case)

* Author environment; used to: 
  * Query content for "content management purposes":
    * GraphQL in AEM as a Cloud Service is currently a read-only API.
    * The REST API can be used for CR(u)D operations.

## Content Fragments for use with the AEM GraphQL API {#content-fragments-use-with-aem-graphql-api}

Content Fragments can be used as a basis for GraphQL for AEM schemas and queries as:

* They enable you to design, create, curate and publish page-independent content.
* They are based on a Content Fragment Model, which pre-defines the structure for the resulting fragment by means of defined data types.
* Additional layers of structure can be achieved with the Fragment Reference data type, available when defining a model.
 
### Content Fragment Models {#content-fragments-models}

These Content Fragment Models:

* Are used to generate the Schemas, once **Enabled**.

* Provide the data types and fields required for GraphQL. They ensure that your application only requests what is possible, and receives what is expected.

* The data type **Fragment References** can be used in your model to reference another Content Fragment, and so introduce additional levels of structure.

### Fragment References {#fragment-references}

The **Fragment Reference**:

* Is a specific data type available when defining a Content Fragment Model.

* References another fragment, dependent on a specific Content Fragment Model.

* Allows you to create, and then retrieve, structured data.

  * When defined as a **multifeed**, multiple sub-fragments can be referenced (retrieved) by the prime fragment.

### JSON Preview {#json-preview}

To help with designing and developing your Content Fragment Models, you can preview JSON output in the Content Fragment Editor.

## GraphQL Schema Generation from Content Fragments {#graphql-schema-generation-content-fragments}

GraphQL is a strongly typed API, which means that content must be clearly structured and organized by type. The GraphQL specification provides a series of guidelines on how to create a robust API for interrogating content on a certain instance. To do this, a client needs to fetch the Schema, which contains all the types necessary for a query. 

For Content Fragments, the GraphQL schemas (structure and types) are based on **Enabled** Content Fragment Models and their data types.

>[!CAUTION]
>
>All the GraphQL schemas (derived from Content Fragment Models that have been **Enabled**) are readable through the GraphQL endpoint.
>
>This means that you need to ensure that no sensitive content is available, to ensure that no sensitive data is exposed via GraphQL endpoints; for example, this includes information that could be present as field names in the model definition.

For example, if a user created a Content Fragment Model called `Article`, then AEM generates the object `article` that is of a type `ArticleModel`. The fields within this type correspond to the fields and data types defined in the model.

1. A Content Fragment Model:

   ![Content Fragment Model for use with GraphQL](assets/graphqlapi-cfmodel.png "Content Fragment Model for use with GraphQL")

1. The corresponding GraphQL schema (output from GraphiQL automatic documentation):
   ![GraphQL Schema based on Content Fragment Model](assets/graphqlapi-cfm-schema.png "GraphQL Schema based on Content Fragment Model")

   This shows that the generated type `ArticleModel` contains several [fields](#fields). 
   
   * Three of them have been controlled by the user: `author`, `main` and `referencearticle`.

   * The other fields were added automatically by AEM, and represent helpful methods to provide information about a certain Content Fragment; in this example, `_path`, `_metadata`, `_variations`. These [helper fields](#helper-fields) are marked with a preceding `_` to distinguish between what has been defined by the user and what has been auto-generated.

1. After a user creates a Content Fragment based on the Article model, it can then be interrogated through GraphQL. For examples, see the Sample Queries.md#graphql-sample-queries) (based on a sample Content Fragment structure for use with GraphQL.

In GraphQL for AEM, the schema is flexible. This means that it is auto-generated each and every time a Content Fragment Model is created, updated or deleted. The data schema caches are also refreshed when you update a Content Fragment Model.

The Sites GraphQL service listens (in the background) for any modifications made to a Content Fragment Model. When updates are detected, only that part of the schema is regenerated. This optimization saves time and provides stability.

So for example, if you:

1. Install a package containing `Content-Fragment-Model-1` and `Content-Fragment-Model-2`:
 
   1. GraphQL types for `Model-1` and `Model-2` will be generated.

1. Then modify `Content-Fragment-Model-2`:

   1. Only the `Model-2` GraphQL type will get updated.

   1. Whereas `Model-1` will remain the same. 

>[!NOTE]
>
>This is important to note in case you want to do bulk updates on Content Fragment Models through the REST api, or otherwise.

The schema is served through the same endpoint as the GraphQL queries, with the client handling the fact that the schema is called with the extension `GQLschema`. For example, performing a simple `GET` request on `/content/cq:graphql/global/endpoint.GQLschema` will result in the output of the schema with the Content-type: `text/x-graphql-schema;charset=iso-8859-1`.

### Schema Generation - Unpublished Models {#schema-generation-unpublished-models}

When Content Fragments are nested it can happen that a parent Content Fragment Model is published, but a referenced model is not.

>[!NOTE]
>
>The AEM UI prevents this happening, but if publishing is made programmatically, or with content packages, it can occur.

When this happens, AEM generates an *incomplete* Schema for the parent Content Fragment Model. This means that the Fragment Reference, which is dependent on the unpublished model, is removed from the schema.

## AEM GraphQL Endpoints {#aem-graphql-endpoints}

An endpoint is the path used to access GraphQL for AEM. Using this path you (or your app) can:

* access the GraphQL schemas,
* send your GraphQL queries,
* receive the responses (to your GraphQL queries).

AEM allows for:

* A global endpoint - available for use by all sites.
* Endpoints for specific Sites configurations - that you can configure (in the Configuration Browser), specific to a specified site/project.

## Permissions {#permissions}

The permissions are those required for accessing Assets.

## The AEM GraphiQL Interface {#aem-graphiql-interface}

To help you directly input, and test queries, an implementation of the standard GraphiQL interface is available for use with AEM GraphQL. This can be installed with AEM.

>[!NOTE]
>
>GraphiQL is bound the global endpoint (and does not work with other endpoints for specific Sites configurations).

It provides features such as syntax-highlighting, auto-complete, auto-suggest, together with a history and online documentation.

![GraphiQL Interface](assets/graphiql-interface.png "GraphiQL Interface")
-->

## Använda faktiskt AEM GraphQL API {#actually-using-aem-graphiql}

### Inledande inställning {#initial-setup}

Innan du börjar med frågor om ditt innehåll måste du:

* Aktivera slutpunkten
   * Använd Verktyg -> Webbplatser -> GraphQL

* Installera GraphiQL (vid behov)
   * Installerat som ett dedikerat paket

### Exempelstruktur {#sample-structure}

Om du vill använda det AEM GraphQL-API:t i en fråga kan vi använda de två mycket grundläggande modellstrukturerna för innehållsfragment:

* Företag
   * Namn
   * VD (person)
   * Anställda (personer)
* Person
   * Namn
   * Förnamn

Som du ser refererar fälten CEO och Employees till Personfragmenten.

Fragmentmodellerna används:

* när du skapar innehåll i Content Fragment Editor
* för att generera de GraphQL-scheman som du ska fråga efter

### Testa dina frågor {#where-to-test-your-queries}

Frågorna kan anges i GraphiQL-gränssnittet, till exempel på:

* `http://localhost:4502/content/graphiql.html `

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

<!-- need code / curl / cli examples-->

Mer information om hur du använder API:t för AEM GraphQL tillsammans med de nödvändiga elementen finns i följande exempel:

* Lär dig använda GraphQL med AEM
* Strukturen för exempelinnehållsfragment
* Att lära sig använda GraphQL med AEM - exempelinnehåll och frågor

## What&#39;s Next {#whats-next}

Nu när du har lärt dig att komma åt och fråga efter rubriklöst innehåll med AEM GraphQL API kan du nu [lära dig hur du använder REST API för att komma åt och uppdatera innehållet i dina innehållsfragment](/help/implementing/developing/headless-journey/update-your-content.md).

## Ytterligare resurser {#additional-resources}

* [GraphQL.org](https://graphql.org)
   * [Scheman](https://graphql.org/learn/schema/)
   * [Variabler](https://graphql.org/learn/queries/#variables)
   * [GraphQL Java-bibliotek](https://graphql.org/code/#java)
* [GraphiQL](https://graphql.org/learn/serving-over-http/#graphiql)
* [Lär dig använda GraphQL med AEM](/help/assets/content-fragments/graphql-api-content-fragments.md)
   * [Aktivera GraphQL-slutpunkten](/help/assets/content-fragments/graphql-api-content-fragments.md#enabling-graphql-endpoint)
   * [Installera AEM GraphiQL-gränssnitt](/help/assets/content-fragments/graphql-api-content-fragments.md#installing-graphiql-interface)
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
* [Getting Started with AEM Headless](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html) - En kort videosjälvstudiekurs med en översikt över hur du använder AEM headless-funktioner, inklusive innehållsmodellering och GraphQL.

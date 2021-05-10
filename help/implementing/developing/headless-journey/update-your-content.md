---
title: Så här uppdaterar du innehåll via AEM Assets API:er
description: I den här delen av den AEM Headless Developer Journey kan du lära dig hur du använder REST API för att komma åt och uppdatera innehållet i dina innehållsfragment.
hide: true
hidefromtoc: true
index: false
exl-id: 8d133b78-ca36-4c3b-815d-392d41841b5c
translation-type: tm+mt
source-git-commit: 7732a291d070a5d93a6f490877b909e1331be1e2
workflow-type: tm+mt
source-wordcount: '1270'
ht-degree: 1%

---

# Så här uppdaterar du ditt innehåll via AEM Assets API:er {#update-your-content}

>[!CAUTION]
>
>ARBETE PÅGÅR - Dokumentet skapas för närvarande och ska inte tolkas som fullständigt eller slutgiltigt och inte heller användas i tillverkningssyfte.

I den här delen av [AEM Headless Developer Journey](overview.md) lär du dig hur du använder REST API för att komma åt och uppdatera innehållet i dina innehållsfragment.

## Berättelsen hittills {#story-so-far}

I det föregående dokumentet på den AEM resan [Hur du får åtkomst till ditt innehåll via AEM Delivery APIs](access-your-content.md) lärde du dig att få åtkomst till ditt headless-innehåll i AEM via AEM GraphQL API och du bör nu:

* Lär dig mer om GraphQL.
* Förstå hur AEM GraphQL API fungerar.
* Förstå några praktiska exempelfrågor.

Den här artikeln bygger på dessa grundläggande funktioner så att du förstår hur du uppdaterar det befintliga headless-innehållet i AEM via REST API.

## Mål {#objective}

* **Målgrupp**: Avancerat
* **Mål**: Lär dig hur du använder REST API för att komma åt och uppdatera innehållet i dina innehållsfragment:
   * Introducera AEM Assets HTTP API.
   * Presentera och diskutera stöd för innehållsfragment i API:t.
   * Visa information om API:t.

<!--
  * Look at sample code to see how things work in practice.
-->

## Varför behöver du Assets HTTP API för innehållsfragment {#why-http-api}

I det föregående steget i Headless Journey lärde du dig att använda API:t AEM GraphQL för att hämta ditt innehåll med hjälp av frågor.

Varför behövs en annan API?

Med Assets HTTP API kan du **läsa** ditt innehåll, men du kan även **skapa**, **uppdatera** och **ta bort** innehåll - åtgärder som inte är möjliga med GraphQL API.

Resursens REST API är tillgängligt för varje körklar installation av en nyligen använd Adobe Experience Manager som Cloud Service-version.

## HTTP API för Assets {#assets-http-api}

Resursens HTTP-API omfattar:

* Resurser REST API
* inklusive stöd för innehållsfragment

Den aktuella implementeringen av Assets HTTP API baseras på arkitekturformatet **REST** och gör att du kan komma åt innehåll (som lagras i AEM) via **CRUD**-åtgärder (Skapa, Läs, Uppdatera, Ta bort).

Med den här åtgärden kan du med API:t köra Adobe Experience Manager som en Cloud Service som ett headless CMS (Content Management System) genom att tillhandahålla Content Services till ett JavaScript-klientprogram. Eller något annat program som kan köra HTTP-begäranden och hantera JSON-svar. Exempelvis kräver Single Page-program (SPA), ramverksbaserade eller anpassade, innehåll som tillhandahålls via ett API, ofta i JSON-format.

<!--
>[!NOTE]
>
>It is not possible to customize JSON output from the Assets REST API. 

The Assets REST API:

* follows the HATEOAS principle
* implements the SIREN format

## Key Concepts {#key-concepts}

The Assets REST API offers REST-style access to assets stored within an AEM instance. 

It uses the `/api/assets` endpoint and requires the path of the asset to access it (without the leading `/content/dam`). 

* This means that to access the asset at:
  * `/content/dam/path/to/asset`
* You need to request:
  * `/api/assets/path/to/asset` 

For example, to access `/content/dam/wknd/en/adventures/cycling-tuscany`, request `/api/assets/wknd/en/adventures/cycling-tuscany.json` 

>[!NOTE]
>Access over:
>
>* `/api/assets` **does not** need the use of the `.model` selector.
>* `/content/path/to/page` **does** require the use of the `.model` selector.

The HTTP method determines the operation to be executed:

* **GET** - to retrieve a JSON representation of an asset or a folder
* **POST** - to create new assets or folders
* **PUT** - to update the properties of an asset or folder
* **DELETE** - to delete an asset or folder

>[!NOTE]
>
>The request body and/or URL parameters can be used to configure some of these operations; for example, define that a folder or an asset should be created by a **POST** request.

The exact format of supported requests is defined in the API Reference documentation. 

### Transactional Behavior {#transactional-behavior}

All requests are atomic.

This means that subsequent (`write`) requests cannot be combined into a single transaction that could succeed or fail as a single entity.

### Security {#security}

If the Assets REST API is used within an environment without specific authentication requirements, AEM's CORS filter needs to be configured correctly.

>[!NOTE]
>
>For further information see:
>
>* CORS/AEM explained
>* Video - Developing for CORS with AEM

In environments with specific authentication requirements, OAuth is recommended.

## Available Features {#available-features}

Content Fragments are a specific type of Asset, see Working with Content Fragments.

For further information about features available through the API see:

* The Assets REST API (Additional Resources) 
* Entity Types, where the features specific to each supported type (as relevant to Content Fragments) are explained 

### Paging {#paging}

The Assets REST API supports paging (for GET requests) via the URL parameters:

* `offset` - the number of the first (child) entity to retrieve
* `limit` - the maximum number of entities returned

The response will contain paging information as part of the `properties` section of the SIREN output. This `srn:paging` property contains the total number of (child) entities ( `total`), the offset and the limit ( `offset`, `limit`) as specified in the request.

>[!NOTE]
>
>Paging is typically applied on container entities (i.e. folders or assets with renditions), as it relates to the children of the requested entity.

#### Example: Paging {#example-paging}

`GET /api/assets.json?offset=2&limit=3`

```json
...
"properties": {
    ...
    "srn:paging": {
        "total": 7,
        "offset": 2,
        "limit": 3
    }
    ...
}
...
```

## Entity Types {#entity-types}

### Folders {#folders}

Folders act as containers for assets and other folders. They reflect the structure of the AEM content repository.

The Assets REST API exposes access to the properties of a folder; for example its name, title, etc. Assets are exposed as child entities of folders, and sub-folders.

>[!NOTE]
>
>Depending on the asset type of the child assets and folders the list of child entities may already contain the full set of properties that defines the respective child entity. Alternatively, only a reduced set of properties may be exposed for an entity in this list of child entities.

### Assets {#assets}

If an asset is requested, the response will return its metadata; such as title, name and other information as defined by the respective asset schema.

The binary data of an asset is exposed as a SIREN link of type `content`.

Assets can have multiple renditions. These are typically exposed as child entities, one exception being a thumbnail rendition, which is exposed as a link of type `thumbnail` ( `rel="thumbnail"`).
-->

## Resurser för HTTP API och innehållsfragment {#assets-http-api-content-fragments}

Innehållsfragment används för rubrikfri leverans och ett innehållsfragment är en särskild typ av resurs. De används för att komma åt strukturerade data, t.ex. texter, siffror och datum.

Eftersom det finns flera skillnader mellan *standardobjekt*-resurser (t.ex. bilder eller ljud) gäller vissa ytterligare regler för att hantera dem.

### Representation {#representation}

Innehållsfragment:

* Visa inga binära data.
* Finns helt i JSON-utdata (inom egenskapen `properties`).

* betraktas också som atomiska, dvs. elementen och variationerna exponeras som en del av fragmentets egenskaper jämfört med som länkar eller underordnade enheter. Detta ger effektiv åtkomst till nyttolasten för ett fragment.

### Innehållsmodeller och innehållsfragment {#content-models-and-content-fragments}

För närvarande visas inte modellerna som definierar strukturen för ett innehållsfragment via ett HTTP-API. Därför måste *konsumenten* känna till modellen för ett fragment (åtminstone ett minimum), även om den mesta informationen kan härledas från nyttolasten. som datatyper, osv. är en del av definitionen.

Om du vill skapa ett nytt innehållsfragment måste modellens (interna databas) sökväg anges.

### Associerat innehåll {#associated-content}

Associerat innehåll visas för närvarande inte.

## Använda Resurser REST API {#using-aem-assets-rest-api}

### Öppna {#access}

Resursens REST API använder slutpunkten `/api/assets` och kräver att resursens sökväg har åtkomst till den (utan inledande `/content/dam`).

* Det innebär att du kan få tillgång till resursen på:
   * `/content/dam/path/to/asset`
* Du måste begära:
   * `/api/assets/path/to/asset`

Om du till exempel vill komma åt `/content/dam/wknd/en/adventures/cycling-tuscany` begär du `/api/assets/wknd/en/adventures/cycling-tuscany.json`

>[!NOTE]
>Åtkomst över:
>
>* `/api/assets` **använder** inte  `.model` väljaren.
>* `/content/path/to/page` **kräver** att du använder  `.model` väljaren.


### Åtgärd {#operation}

HTTP-metoden avgör vilken åtgärd som ska utföras:

* **GET**  - för att hämta en JSON-representation av en resurs eller en mapp
* **POST**  - för att skapa nya resurser eller mappar
* **PUT** - för att uppdatera egenskaperna för en resurs eller mapp
* **DELETE** - för att ta bort en resurs eller mapp

>[!NOTE]
>
>Begärandetexten och/eller URL-parametrarna kan användas för att konfigurera vissa av dessa åtgärder. Ange till exempel att en mapp eller en resurs ska skapas med en **POST**-begäran.

Det exakta formatet för begäranden som stöds definieras i API-referensdokumentationen.

Användningen kan variera beroende på om du använder en AEM författare eller publiceringsmiljö, tillsammans med ditt specifika användningsexempel.

* Vi rekommenderar att skapandet binds till en författarinstans (och det finns för närvarande inget sätt att replikera ett fragment för publicering med denna API).
* Leverans är möjlig från båda, eftersom AEM endast skickar begärt innehåll i JSON-format.

   * Lagring och leverans från en AEM författarinstans bör räcka för program som ligger bakom brandväggen och mediabibliotek.

   * För direktwebbleverans rekommenderas en publiceringsinstans AEM.

>[!CAUTION]
>
>Dispatcher-konfigurationen på AEM molninstanser kan blockera åtkomsten till `/api`.

>[!NOTE]
>
>Mer information finns i API-referensen. Speciellt [Adobe Experience Manager Assets API - Content Fragments](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/assets-api-content-fragments/index.html).

### Läs/Leverera {#read-delivery}

Användning sker via:

`GET /{cfParentPath}/{cfName}.json`

Till exempel:

`http://<host>/api/assets/wknd/en/adventures/cycling-tuscany.json`

Svaret är serialiserat JSON med innehållet strukturerat som i innehållsfragmentet. Referenser levereras som referens-URL:er.

Det finns två typer av läsåtgärder:

* När du läser ett visst innehållsfragment efter sökväg, returneras JSON-representationen av innehållsfragmentet.
* Läsa en mapp med innehållsfragment efter sökväg: returnerar JSON-representationerna för alla innehållsfragment i mappen.

### Skapa {#create}

Användning sker via:

`POST /{cfParentPath}/{cfName}`

Brödtexten måste innehålla en JSON-representation av det innehållsfragment som ska skapas, inklusive allt ursprungligt innehåll som ska anges för elementen i innehållsfragmentet. Det är obligatoriskt att ange egenskapen `cq:model` och den måste peka på en giltig innehållsfragmentmodell. Om du inte gör det uppstår ett fel. Du måste också lägga till en rubrik `Content-Type` som är inställd på `application/json`.

### Uppdatera {#update}

Användning sker via

`PUT /{cfParentPath}/{cfName}`

Brödtexten måste innehålla en JSON-representation av vad som ska uppdateras för det angivna innehållsfragmentet.

Detta kan helt enkelt vara titeln eller beskrivningen av ett innehållsfragment, ett enskilt element eller alla elementvärden och/eller metadata.

### Ta bort {#delete}

Användning sker via:

`DELETE /{cfParentPath}/{cfName}`

Mer information om hur du använder AEM Assets REST API finns i:

* Adobe Experience Manager Assets HTTP API (ytterligare resurser)
* Stöd för innehållsfragment i AEM Assets HTTP API (ytterligare resurser)

## What&#39;s Next {#whats-next}

Nu när du är klar med den här delen av AEM Headless Developer Journey ska du:

* Förstå grunderna i AEM Assets HTTP API.
* Förstå hur innehållsfragment stöds i detta API.

<!--
* Have experience with sample code and know how the API works in practice.
-->

Du bör fortsätta din AEM resa utan att behöva besöka dokumentet nästa gång [Placera allt tillsammans - Din app och ditt innehåll i AEM Headless](put-it-all-together.md) där du får lära dig hur du tar ditt AEM Headless-projekt och förbereder det för publicering.

## Ytterligare resurser {#additional-resources}

* [REST](https://en.wikipedia.org/wiki/Representational_state_transfer)
* [HATEOAS-principen](https://en.wikipedia.org/wiki/HATEOAS)
* [SIREN-format](https://github.com/kevinswiber/siren)
* [HTTP API för Assets](/help/assets/mac-api-assets.md)
* [Innehållsfragment REST API](/help/assets/content-fragments/assets-api-content-fragments.md)
   * [API-referens](/help/assets/content-fragments/assets-api-content-fragments.md#api-reference)
* [Adobe Experience Manager Assets API - innehållsfragment](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/assets-api-content-fragments/index.html)
* [Arbeta med innehållsfragment](/help/assets/content-fragments/content-fragments.md)
* [AEM kärnkomponenter](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html)
* [CORS/AEM](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/cors-security-article-understand.html)
* [Video - Utveckla för CORS med AEM](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/cors-security-technical-video-develop.html)


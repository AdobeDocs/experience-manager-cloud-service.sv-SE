---
title: Så här uppdaterar du innehåll via AEM Assets API:er
description: I den här delen av den AEM Headless Developer Journey kan du lära dig hur du använder REST API för att komma åt och uppdatera innehållet i dina innehållsfragment.
exl-id: 84120856-fd1d-40f7-8df4-73d4cdfcc43b
source-git-commit: e2505c0fec1da8395930f131bfc55e1e2ce05881
workflow-type: tm+mt
source-wordcount: '1096'
ht-degree: 1%

---

# Så här uppdaterar du innehåll via AEM Assets API:er {#update-your-content}

I den här delen av [AEM Headless Developer Journey](overview.md) Lär dig hur du använder REST API för att komma åt och uppdatera innehållet i dina innehållsfragment.

## Story hittills {#story-so-far}

I det föregående dokumentet om den AEM resan utan headless [Få åtkomst till ditt innehåll via AEM-API:er](access-your-content.md) har du lärt dig hur du får tillgång till ditt headless-innehåll i AEM via det AEM GraphQL API:t, och du bör nu:

* Lär dig mer om GraphQL.
* Förstå hur AEM GraphQL API fungerar.
* Förstå några praktiska exempelfrågor.

Den här artikeln bygger på dessa grundläggande funktioner så att du förstår hur du uppdaterar det befintliga headless-innehållet i AEM via REST API.

## Syfte {#objective}

* **Målgrupp**: Avancerat
* **Syfte**: Lär dig hur du använder REST API för att komma åt och uppdatera innehållet i dina innehållsfragment:
   * Introducera AEM Assets HTTP API.
   * Presentera och diskutera stöd för innehållsfragment i API:t.
   * Visa information om API:t.

<!--
  * Look at sample code to see how things work in practice.
-->

## Varför behöver du Assets HTTP API för innehållsfragment {#why-http-api}

I det föregående steget i Headless Journey lärde du dig att använda AEM GraphQL API för att hämta ditt innehåll med hjälp av frågor.

Varför behövs en annan API?

Med Assets HTTP API kan du **Läs** innehållet, men det gör det också möjligt för dig **Skapa**, **Uppdatera** och **Ta bort** content - åtgärder som inte är möjliga med GraphQL API.

Resursens REST API är tillgängligt för varje körklar installation av en nyligen använd Adobe Experience Manager as a Cloud Service-version.

## HTTP API för Assets {#assets-http-api}

Resursens HTTP-API omfattar:

* Resurser REST API
* inklusive stöd för innehållsfragment

Den aktuella implementeringen av Assets HTTP API baseras på **REST** arkitektoniskt format så att du kan komma åt innehåll (lagrat i AEM) via **CRUD** (Skapa, läsa, uppdatera, ta bort).

Med dessa åtgärder kan du med API:t köra Adobe Experience Manager as a Cloud Service som ett headless CMS (Content Management System) genom att tillhandahålla Content Services till ett JavaScript-klientprogram. Eller något annat program som kan köra HTTP-begäranden och hantera JSON-svar. Exempelvis kräver Single Page-program (SPA), ramverksbaserade eller anpassade, innehåll som tillhandahålls via ett API, ofta i JSON-format.

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
>For more information, see:
>
>* CORS/AEM explained
>* Video - Developing for CORS with AEM

In environments with specific authentication requirements, OAuth is recommended.

## Available Features {#available-features}

Content Fragments are a specific type of Asset, see Working with Content Fragments.

For more information about features available through the API see:

* The Assets REST API (Additional Resources) 
* Entity Types, where the features specific to each supported type (as relevant to Content Fragments) are explained 

### Paging {#paging}

The Assets REST API supports paging (for GET requests) via the URL parameters:

* `offset` - the number of the first (child) entity to retrieve
* `limit` - the maximum number of entities returned

The response will contain paging information as part of the `properties` section of the SIREN output. This `srn:paging` property contains the total number of (child) entities ( `total`), the offset and the limit ( `offset`, `limit`) as specified in the request.

>[!NOTE]
>
>Paging is typically applied on container entities (that is, folders or assets with renditions), as it relates to the children of the requested entity.

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

<!--
As there are several differences to *standard* assets (such as images or audio), some additional rules apply to handling them.

### Representation {#representation}

Content fragments:

* Do not expose any binary data.
* Are completely contained in the JSON output (within the `properties` property).

* Are also considered atomic, that is, the elements and variations are exposed as part of the fragment's properties vs. as links or child entities. This allows for efficient access to the payload of a fragment.

### Content Models and Content Fragments {#content-models-and-content-fragments}

Currently the models that define the structure of a content fragment are not exposed through an HTTP API. Therefore the *consumer* needs to know about the model of a fragment (at least a minimum) - although most information can be inferred from the payload; as data types, etc. are part of the definition.

To create a content fragment, the (internal repository) path of the model has to be provided.

### Associated Content {#associated-content}

Associated content is currently not exposed.
-->

## Använda REST API för resurser {#using-aem-assets-rest-api}

### Åtkomst {#access}

Resursens REST API använder `/api/assets` slutpunkten och kräver att sökvägen till resursen har åtkomst till den (utan radavståndet) `/content/dam`).

* Det innebär att du kan få tillgång till resursen på
   * `/content/dam/path/to/asset`
* Du måste begära:
   * `/api/assets/path/to/asset`

Till exempel för att komma åt `/content/dam/wknd/en/adventures/cycling-tuscany`, begäran `/api/assets/wknd/en/adventures/cycling-tuscany.json`

>[!NOTE]
>Åtkomst över:
>
>* `/api/assets` **inte** behöver du använda `.model` väljare.
>* `/content/path/to/page` **gör** kräver att `.model` väljare.

### Åtgärd {#operation}

HTTP-metoden avgör vilken åtgärd som ska utföras:

* **GET** - för att hämta en JSON-representation av en resurs eller en mapp
* **POST** - för att skapa nya resurser eller mappar
* **PUT** - för att uppdatera egenskaperna för en resurs eller mapp
* **DELETE** - ta bort en resurs eller mapp

>[!NOTE]
>
>Parametrarna för begärandeinnehåll och/eller URL kan användas för att konfigurera vissa av dessa åtgärder. Du kan till exempel definiera att en mapp eller en resurs ska skapas av en **POST** begäran.

Det exakta formatet för begäranden som stöds definieras i API-referensdokumentationen.

Användningen kan variera beroende på om du använder en AEM författare eller publiceringsmiljö, tillsammans med ditt specifika användningsexempel.

* Vi rekommenderar starkt att skapandet är bundet till en författarinstans (och att det för närvarande inte finns något sätt att replikera ett fragment för publicering med detta API).
* Leverans är möjlig från båda, eftersom AEM endast skickar begärt innehåll i JSON-format.

   * Lagring och leverans från en AEM författarinstans bör räcka för program som ligger bakom brandväggen och mediabibliotek.

   * För live-webbleverans rekommenderas en publiceringsinstans AEM.

>[!CAUTION]
>
>Dispatcher-konfigurationen på AEM molninstanser kan blockera åtkomst till `/api`.

>[!NOTE]
>
>Mer information finns i API-referensen. Särskilt gäller följande: [Adobe Experience Manager Assets API - innehållsfragment](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/assets-api-content-fragments/index.html).

### Läsning/leverans {#read-delivery}

Användning sker via:

`GET /{cfParentPath}/{cfName}.json`

Till exempel:

`http://<host>/api/assets/wknd/en/adventures/cycling-tuscany.json`

Svaret är serialiserat JSON med innehållet strukturerat som i innehållsfragmentet. Referenser levereras som referens-URL:er.

Det finns två typer av läsåtgärder:

* När du läser ett visst innehållsfragment efter sökväg, returneras JSON-representationen av innehållsfragmentet.
* Läser en mapp med innehållsfragment efter sökväg: Detta returnerar JSON-representationerna för alla innehållsfragment i mappen.

### Skapa {#create}

Användning sker via:

`POST /{cfParentPath}/{cfName}`

Brödtexten måste innehålla en JSON-representation av det innehållsfragment som ska skapas, inklusive allt ursprungligt innehåll som ska anges för elementen i innehållsfragmentet. Det är obligatoriskt att ange `cq:model` och måste peka på en giltig innehållsfragmentmodell. Om du inte gör det kommer ett fel att uppstå. Du måste också lägga till en rubrik `Content-Type` som är inställd på `application/json`.

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

<!-- The "How to put it all together" page is not going to be published until the first public release of the Headless SDK. Temporarily commenting out the reference below. -->

<!--You should continue your AEM headless journey by next reviewing the document [How to Put It All Together - Your App and Your Content in AEM Headless](put-it-all-together.md) where you learn how to take your AEM Headless project and prepare it for going live.-->

Du bör fortsätta den AEM resan utan trassel genom att nästa gång du granskar dokumentet [Så här sätter du samman allt - din app och ditt innehåll i AEM utan rubriker](put-it-all-together.md) där du kommer att bekanta dig med grunderna och verktygen för AEM arkitektur som du behöver för att sätta ihop programmen.

## Ytterligare resurser {#additional-resources}

* [HTTP API för Assets](/help/assets/mac-api-assets.md)
* [Innehållsfragment REST API](/help/assets/content-fragments/assets-api-content-fragments.md)
   * [API-referens](/help/assets/content-fragments/assets-api-content-fragments.md#api-reference)
* [Adobe Experience Manager Assets API - innehållsfragment](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/assets-api-content-fragments/index.html)
* [Arbeta med innehållsfragment](/help/sites-cloud/administering/content-fragments/overview.md)
* [Grundläggande komponenter i AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html)
* [CORS/AEM](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/cors-security-article-understand.html)
* [Video - Utveckla för CORS med AEM](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/cors-security-technical-video-develop.html)
* [Introduktion till AEM som headless CMS](/help/headless/introduction.md)
* [AEM Developer Portal](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html)
* [Tutorials för Headless i AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html)

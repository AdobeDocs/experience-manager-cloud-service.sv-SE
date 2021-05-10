---
title: Så här uppdaterar du innehåll via AEM Assets API:er
description: I den här delen av den AEM Headless Developer Journey kan du lära dig hur du använder REST API för att komma åt och uppdatera innehållet i dina innehållsfragment.
hide: true
hidefromtoc: true
index: false
exl-id: 8d133b78-ca36-4c3b-815d-392d41841b5c
translation-type: tm+mt
source-git-commit: 787af0d4994bf1871c48aadab74d85bd7c3c94fb
workflow-type: tm+mt
source-wordcount: '1668'
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

[Resursens HTTP API](/help/assets/mac-api-assets.md) omfattar:

* Resurser REST API
* inklusive stöd för innehållsfragment

Den aktuella implementeringen av Assets HTTP API baseras på arkitekturstilen **REST**.

Med Assets REST API kan utvecklare av Adobe Experience Manager som Cloud Service komma åt innehåll (som lagras i AEM) direkt via HTTP-API:t via **CRUD**-åtgärder (Create, Read, Update, Delete).

Med den här åtgärden kan du med API:t köra Adobe Experience Manager som en Cloud Service som ett headless CMS (Content Management System) genom att tillhandahålla Content Services till ett JavaScript-klientprogram. Eller något annat program som kan köra HTTP-begäranden och hantera JSON-svar. Exempelvis kräver Single Page-program (SPA), ramverksbaserade eller anpassade, innehåll som tillhandahålls via ett API, ofta i JSON-format.

>[!NOTE]
>
>Det går inte att anpassa JSON-utdata från Assets REST API.

Resursens REST API:

* följer HATEOAS-principen
* implementerar SIREN-formatet

## Nyckelbegrepp {#key-concepts}

REST API:t ger REST-åtkomst till resurser som lagras i en AEM.

Slutpunkten `/api/assets` används och resursens sökväg krävs för att komma åt den (utan inledande `/content/dam`).

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


HTTP-metoden avgör vilken åtgärd som ska utföras:

* **GET**  - för att hämta en JSON-representation av en resurs eller en mapp
* **POST**  - för att skapa nya resurser eller mappar
* **PUT** - för att uppdatera egenskaperna för en resurs eller mapp
* **DELETE** - för att ta bort en resurs eller mapp

>[!NOTE]
>
>Begärandetexten och/eller URL-parametrarna kan användas för att konfigurera vissa av dessa åtgärder. Ange till exempel att en mapp eller en resurs ska skapas med en **POST**-begäran.

Det exakta formatet för begäranden som stöds definieras i API-referensdokumentationen.

### Transaktionsbeteende {#transactional-behavior}

Alla förfrågningar är atomiska.

Det innebär att efterföljande (`write`)-begäranden inte kan kombineras till en enda transaktion som kan lyckas eller misslyckas som en enskild enhet.

### Dokumentskydd {#security}

Om REST API:t för Resurser används i en miljö utan särskilda autentiseringskrav måste AEM CORS-filtret konfigureras korrekt.

>[!NOTE]
>
>Mer information finns i:
>
>* CORS/AEM
>* Video - Utveckla för CORS med AEM


I miljöer med specifika autentiseringskrav rekommenderas OAuth.

## Tillgängliga funktioner {#available-features}

Innehållsfragment är en specifik typ av resurs, se Arbeta med innehållsfragment.

Mer information om funktioner som är tillgängliga via API finns i:

* Resursens REST API (ytterligare resurser)
* Enhetstyper, där funktioner som är specifika för varje typ som stöds (som är relevant för innehållsfragment) förklaras

### Sidindelning {#paging}

Resursens REST API stöder sidindelning (för GET-begäranden) via URL-parametrarna:

* `offset` - numret på den första (underordnade) entiteten som ska hämtas
* `limit` - det maximala antalet returnerade enheter

Svaret kommer att innehålla växlingsinformation som en del av `properties`-avsnittet i SIREN-utdata. Den här `srn:paging`-egenskapen innehåller det totala antalet (underordnade) entiteter ( `total`), förskjutningen och gränsen ( `offset`, `limit`) som anges i begäran.

>[!NOTE]
>
>Sidindelning används vanligtvis för behållarentiteter (d.v.s. mappar eller resurser med återgivningar), eftersom det relaterar till den begärda entitetens underordnade.

#### Exempel: Sidindelning {#example-paging}

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

## Enhetstyper {#entity-types}

### Mappar {#folders}

Mappar fungerar som behållare för resurser och andra mappar. De återspeglar strukturen i AEM innehållsdatabas.

Resursens REST API ger åtkomst till en mapps egenskaper. till exempel namn, titel osv. Resurser visas som underordnade enheter till mappar och undermappar.

>[!NOTE]
>
>Beroende på resurstypen för de underordnade resurserna och mapparna kan listan med underordnade enheter redan innehålla den fullständiga uppsättningen egenskaper som definierar respektive underordnade enhet. Alternativt kan bara en reducerad uppsättning egenskaper visas för en enhet i den här listan över underordnade enheter.

### Assets {#assets}

Om en resurs begärs returneras dess metadata. som titel, namn och annan information som definieras av respektive resursschema.

Binära data för en resurs visas som en SIREN-länk av typen `content`.

Resurser kan ha flera renderingar. Dessa visas vanligtvis som underordnade enheter, ett undantag är en miniatyrrendering som visas som en länk av typen `thumbnail` ( `rel="thumbnail"`).

### Innehållsfragment {#content-fragments}

Ett innehållsfragment är en särskild typ av resurs. De kan användas för att komma åt strukturerade data, t.ex. texter, siffror och datum.

Eftersom det finns flera skillnader mellan *standardobjekt*-resurser (t.ex. bilder eller ljud) gäller vissa ytterligare regler för att hantera dem.

#### Representation {#representation}

Innehållsfragment:

* Visa inga binära data.
* Finns helt i JSON-utdata (inom egenskapen `properties`).

* betraktas också som atomiska, dvs. elementen och variationerna exponeras som en del av fragmentets egenskaper jämfört med som länkar eller underordnade enheter. Detta ger effektiv åtkomst till nyttolasten för ett fragment.

#### Innehållsmodeller och innehållsfragment {#content-models-and-content-fragments}

För närvarande visas inte modellerna som definierar strukturen för ett innehållsfragment via ett HTTP-API. Därför måste *konsumenten* känna till modellen för ett fragment (åtminstone ett minimum), även om den mesta informationen kan härledas från nyttolasten. som datatyper, osv. är en del av definitionen.

Om du vill skapa ett nytt innehållsfragment måste modellens (interna databas) sökväg anges.

#### Associerat innehåll {#associated-content}

Associerat innehåll visas för närvarande inte.

## Använda Resurser REST API {#using-aem-assets-rest-api}

Användningen kan variera beroende på om du använder en AEM författare eller publiceringsmiljö, tillsammans med ditt specifika användningsexempel.

* Vi rekommenderar att skapandet binds till en författarinstans ([och att det för närvarande inte finns något sätt att replikera ett fragment för publicering med denna API](/help/assets/content-fragments/assets-api-content-fragments.md#limitations)).
* Leverans är möjlig från båda, eftersom AEM endast skickar begärt innehåll i JSON-format.

   * Lagring och leverans från en AEM författarinstans bör räcka för program som ligger bakom brandväggen och mediabibliotek.

   * För direktwebbleverans rekommenderas en publiceringsinstans AEM.

>[!CAUTION]
>
>Dispatcher-konfigurationen på AEM molninstanser kan blockera åtkomsten till `/api`.

>[!NOTE]
>
>Mer information finns i [API-referens](/help/assets/content-fragments/assets-api-content-fragments.md#api-reference). Speciellt [Adobe Experience Manager Assets API - Content Fragments](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/assets-api-content-fragments/index.html).

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
* [Arbeta med innehållsfragment](/help/assets/content-fragments/content-fragments.md)
* [AEM kärnkomponenter](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html)
* [CORS/AEM](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/cors-security-article-understand.html)
* [Video - Utveckla för CORS med AEM](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/cors-security-technical-video-develop.html)


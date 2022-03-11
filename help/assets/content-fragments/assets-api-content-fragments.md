---
title: Stöd för Adobe Experience Manager as a Cloud Service Content Fragments i Assets HTTP API
description: Lär dig mer om stöd för innehållsfragment i Assets HTTP API, en viktig del AEM headless delivery feature.
feature: Content Fragments,Assets HTTP API
exl-id: d72cc0c0-0641-4fd6-9f87-745af5f2c232
source-git-commit: ad51218652d3e7fbe90abb1fc02cce7212394c21
workflow-type: tm+mt
source-wordcount: '1951'
ht-degree: 1%

---

# Stöd för Content Fragments i AEM Assets HTTP API {#content-fragments-support-in-aem-assets-http-api}

## Översikt {#overview}

Lär dig mer om stöd för innehållsfragment i Assets HTTP API, en viktig del AEM headless delivery feature.

>[!NOTE]
>
>The [Resurser för HTTP API](/help/assets/mac-api-assets.md) Innefattar:
>
>* Resurser REST API
>* inklusive stöd för innehållsfragment
>
>Den aktuella implementeringen av Assets HTTP API baseras på [REST](https://en.wikipedia.org/wiki/Representational_state_transfer) arkitekturstil.

The [Resurser REST API](/help/assets/mac-api-assets.md) ger utvecklare av Adobe Experience Manager as a Cloud Service tillgång till innehåll (som lagras i AEM) direkt via HTTP-API:t via CRUD-åtgärder (Create, Read, Update, Delete).

Med API kan du använda Adobe Experience Manager as a Cloud Service som headless CMS (Content Management System) genom att tillhandahålla Content Services till ett JavaScript-klientprogram. Eller något annat program som kan köra HTTP-begäranden och hantera JSON-svar.

Till exempel: [Single Page Applications (SPA)](/help/implementing/developing/hybrid/introduction.md), ramverksbaserade eller anpassade, kräver innehåll som tillhandahålls via HTTP API, ofta i JSON-format.

while [AEM kärnkomponenter](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) tillhandahåller ett mycket omfattande, flexibelt och anpassningsbart API som kan tillhandahålla de läsoperationer som krävs för detta, och vars JSON-utdata kan anpassas, kräver de AEM WCM-kunskaper (Web Content Management) för implementering eftersom de måste finnas på sidor som är baserade på dedikerade AEM-mallar. Det är inte varje SPA utvecklingsorganisation som har direkt tillgång till sådan kunskap.

Detta är när REST API:t för resurser kan användas. Med det kan utvecklare komma åt resurser (till exempel bilder och innehållsfragment) direkt, utan att först behöva bädda in dem på en sida, och leverera innehållet i serialiserat JSON-format.

>[!NOTE]
>
>Det går inte att anpassa JSON-utdata från Assets REST API.

Med Assets REST API kan utvecklare ändra innehåll genom att skapa nya, uppdatera eller ta bort befintliga resurser, innehållsfragment och mappar.

Resursens REST API:

* följer [HATEOAS-principen](https://en.wikipedia.org/wiki/HATEOAS)

* implementerar [SIREN-format](https://github.com/kevinswiber/siren)

## Förutsättningar {#prerequisites}

Resursens REST API är tillgängligt för varje körklar installation av en nyligen använd Adobe Experience Manager as a Cloud Service-version.

## Viktiga begrepp {#key-concepts}

Resurser REST API erbjuder [REST](https://en.wikipedia.org/wiki/Representational_state_transfer)-liknande åtkomst till resurser som lagras i en AEM.

Den använder `/api/assets` slutpunkten och kräver att sökvägen till resursen har åtkomst till den (utan radavståndet) `/content/dam`).

* Det innebär att du kan få tillgång till resursen på:
   * `/content/dam/path/to/asset`
* Du måste begära:
   * `/api/assets/path/to/asset`

Till exempel för att komma åt `/content/dam/wknd/en/adventures/cycling-tuscany`, begäran `/api/assets/wknd/en/adventures/cycling-tuscany.json`

>[!NOTE]
>Åtkomst över:
>
>* `/api/assets` **inte** behöver du använda `.model` väljare.
>* `/content/path/to/page` **gör** kräver att `.model` väljare.


HTTP-metoden avgör vilken åtgärd som ska utföras:

* **GET** - för att hämta en JSON-representation av en resurs eller en mapp
* **POST** - för att skapa nya resurser eller mappar
* **PUT** - för att uppdatera egenskaperna för en resurs eller mapp
* **DELETE** - ta bort en resurs eller mapp

>[!NOTE]
>
>Begärandetexten och/eller URL-parametrarna kan användas för att konfigurera vissa av dessa åtgärder. Definiera till exempel att en mapp eller en resurs ska skapas av en **POST** begäran.

Det exakta formatet för begäranden som stöds definieras i [API-referens](/help/assets/content-fragments/assets-api-content-fragments.md#api-reference) dokumentation.

### Transaktionsbeteende {#transactional-behavior}

Alla förfrågningar är atomiska.

Detta innebär att följande (`write`) kan inte kombineras till en enda transaktion som kan lyckas eller misslyckas som en enskild enhet.

### AEM (Resurser) REST API jämfört med AEM komponenter {#aem-assets-rest-api-versus-aem-components}

<table>
 <thead>
  <tr>
   <td>Proportioner</td>
   <td>Resurser REST API<br/> </td>
   <td>AEM<br/> (komponenter med Sling Models)</td>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td>Användningsfall som stöds</td>
   <td>Allmänt syfte.</td>
   <td><p>Optimerad för konsumtion i ett Single Page-program (SPA) eller i något annat (innehållsförbrukande) sammanhang.</p> <p>Kan även innehålla layoutinformation.</p> </td>
  </tr>
  <tr>
   <td>Åtgärder som stöds</td>
   <td><p>Skapa, läsa, uppdatera, ta bort.</p> <p>Med ytterligare åtgärder beroende på enhetstyp.</p> </td>
   <td>Skrivskyddad.</td>
  </tr>
  <tr>
   <td>Åtkomst</td>
   <td><p>Kan nås direkt.</p> <p>Använder <code>/api/assets </code>slutpunkt, mappad till <code>/content/dam</code> (i databasen).</p> 
   <p>En exempelsökväg skulle se ut så här: <code>/api/assets/wknd/en/adventures/cycling-tuscany.json</code></p>
   </td>
    <td><p>Måste refereras via en AEM på en AEM.</p> <p>Använder <code>.model</code> för att skapa JSON-representationen.</p> <p>En exempelsökväg skulle se ut så här:<br/> <code>/content/wknd/language-masters/en/adventures/cycling-tuscany.model.json</code></p> 
   </td>
  </tr>
  <tr>
   <td>Dokumentskydd</td>
   <td><p>Flera alternativ är möjliga.</p> <p>OAuth föreslås. kan konfigureras separat från standardinställningarna.</p> </td>
   <td>Använder AEM standardinställningar.</td>
  </tr>
  <tr>
   <td>Arkitektur</td>
   <td><p>Skrivåtkomst avser vanligtvis en författarinstans.</p> <p>Läsningen kan även dirigeras till en publiceringsinstans.</p> </td>
   <td>Eftersom det här arbetssättet är skrivskyddat används det vanligtvis för publiceringsinstanser.</td>
  </tr>
  <tr>
   <td>Utdata</td>
   <td>JSON-baserade SIREN-utdata: mycket, men kraftfullt. Tillåter navigering i innehållet.</td>
   <td>JSON-baserade egna produkter. som kan konfigureras med Sling Models. Att navigera i innehållsstrukturen är svårt att implementera (men inte nödvändigtvis omöjligt).</td>
  </tr>
 </tbody>
</table>

### Dokumentskydd {#security}

Om REST API:t för Resurser används i en miljö utan särskilda autentiseringskrav måste AEM CORS-filtret konfigureras korrekt.

>[!NOTE]
>
>Mer information finns i:
>
>* [CORS/AEM](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/cors-security-article-understand.html)
>* [Video - Utveckla för CORS med AEM](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/cors-security-technical-video-develop.html)
>


I miljöer med specifika autentiseringskrav rekommenderas OAuth.

## Tillgängliga funktioner {#available-features}

Innehållsfragment är en specifik typ av resurs, se [Arbeta med innehållsfragment](/help/assets/content-fragments/content-fragments.md).

Mer information om funktioner som är tillgängliga via API finns i:

* The [Resurser REST API](/help/assets/mac-api-assets.md)
* [Enhetstyper](/help/assets/content-fragments/assets-api-content-fragments.md#entity-types), där de funktioner som är specifika för varje typ som stöds (som är relevant för innehållsfragment) förklaras

### Sidindelning {#paging}

Resursens REST API stöder sidindelning (för GET-begäranden) via URL-parametrarna:

* `offset` - numret på den första (underordnade) entiteten som ska hämtas
* `limit` - det maximala antalet returnerade enheter

Svaret kommer att innehålla sidindelningsinformation som en del av `properties` i SIREN-utdata. Detta `srn:paging` egenskapen innehåller det totala antalet (underordnade) entiteter ( `total`), förskjutningen och gränsen ( `offset`, `limit`) enligt begäran.

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

Den binära informationen för en resurs visas som en SIREN-länk av typen `content`.

Resurser kan ha flera renderingar. Dessa visas vanligtvis som underordnade enheter, och ett undantag är en miniatyrrendering, som visas som en länk av typen `thumbnail` ( `rel="thumbnail"`).

### Innehållsfragment {#content-fragments}

A [innehållsfragment](/help/assets/content-fragments/content-fragments.md) är en särskild typ av tillgång. De kan användas för att komma åt strukturerade data, t.ex. texter, siffror och datum.

Som det finns flera skillnader mellan *standard* resurser (t.ex. bilder eller ljud), kan vissa andra regler gälla för att hantera dem.

#### Representation {#representation}

Innehållsfragment:

* Visa inga binära data.
* Finns helt i JSON-utdata (i `properties` egenskap).

* betraktas också som atomiska, dvs. elementen och variationerna exponeras som en del av fragmentets egenskaper jämfört med som länkar eller underordnade enheter. Detta ger effektiv åtkomst till nyttolasten för ett fragment.

#### Innehållsmodeller och innehållsfragment {#content-models-and-content-fragments}

För närvarande visas inte modellerna som definierar strukturen för ett innehållsfragment via ett HTTP-API. Därför *konsument* behöver känna till modellen för ett fragment (minst ett minimum), men den mesta informationen kan härledas från nyttolasten, som datatyper, osv. är en del av definitionen.

Om du vill skapa ett nytt innehållsfragment måste modellens (interna databas) sökväg anges.

#### Associerat innehåll {#associated-content}

Associerat innehåll visas för närvarande inte.

## Använda {#using}

Användningen kan variera beroende på om du använder en AEM författare eller publiceringsmiljö, tillsammans med ditt specifika användningsexempel.

* Vi rekommenderar starkt att skapandet är bundet till en författarinstans ([och det finns för närvarande inget sätt att replikera ett fragment som ska publiceras med detta API](/help/assets/content-fragments/assets-api-content-fragments.md#limitations)).
* Leverans är möjlig från båda, eftersom AEM endast skickar begärt innehåll i JSON-format.

   * Lagring och leverans från en AEM författarinstans bör räcka för program som ligger bakom brandväggen och mediabibliotek.

   * För direktwebbleverans rekommenderas en publiceringsinstans AEM.

>[!CAUTION]
>
>Dispatcher-konfigurationen på AEM molninstanser kan blockera åtkomst till `/api`.

>[!NOTE]
>
>Mer information finns i [API-referens](/help/assets/content-fragments/assets-api-content-fragments.md#api-reference). I synnerhet [Adobe Experience Manager Assets API - innehållsfragment](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/assets-api-content-fragments/index.html).

### Läsning/leverans {#read-delivery}

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

Brödtexten måste innehålla en JSON-representation av det innehållsfragment som ska skapas, inklusive allt ursprungligt innehåll som ska anges för elementen i innehållsfragmentet. Det är obligatoriskt att ange `cq:model` och måste peka på en giltig innehållsfragmentmodell. Om du inte gör det uppstår ett fel. Du måste också lägga till en rubrik `Content-Type` som är inställd på `application/json`.

### Uppdatera {#update}

Användning sker via

`PUT /{cfParentPath}/{cfName}`

Brödtexten måste innehålla en JSON-representation av vad som ska uppdateras för det angivna innehållsfragmentet.

Detta kan helt enkelt vara titeln eller beskrivningen av ett innehållsfragment, ett enskilt element eller alla elementvärden och/eller metadata.

### Ta bort {#delete}

Användning sker via:

`DELETE /{cfParentPath}/{cfName}`

## Begränsningar {#limitations}

Det finns några begränsningar:

* **Modeller för innehållsfragment stöds för närvarande inte**: kan inte läsas eller skapas. För att kunna skapa ett nytt, eller uppdatera ett befintligt, innehållsfragment, måste utvecklarna veta rätt sökväg till innehållsfragmentmodellen. För närvarande är det enda sättet att få en översikt över dessa genom administrationsgränssnittet.
* **Referenser ignoreras**. För närvarande finns det inga kontroller för om ett befintligt innehållsfragment refereras. Om du t.ex. tar bort ett innehållsfragment kan det leda till problem på en sida som innehåller en referens till det borttagna innehållsfragmentet.
* **JSON-datatyp** REST API-utdata för *JSON-datatyp* är för närvarande *strängbaserade utdata*.

## Statuskoder och felmeddelanden {#status-codes-and-error-messages}

Följande statuskoder kan visas under de relevanta omständigheterna:

* **200** (OK)

   Returneras när:

   * begära ett innehållsfragment via `GET`
   * uppdaterar ett innehållsfragment via `PUT`

* **201** (Skapad)

   Returneras när:

   * har skapat ett innehållsfragment via `POST`

* **404** (Hittades inte)

   Returneras när:

   * det begärda innehållsfragmentet inte finns

* **500** (Internt serverfel)

   >[!NOTE]
   >
   >Detta fel returneras:
   >
   >* när ett fel som inte kan identifieras med en viss kod har inträffat
   >* när den angivna nyttolasten inte var giltig


   I följande exempel visas vanliga scenarier när den här felstatusen returneras, tillsammans med felmeddelandet (monospace) som genereras:

   * Överordnad mapp finns inte (när ett innehållsfragment skapas via `POST`)
   * Ingen innehållsfragmentmodell har angetts (cq:model saknas), kan inte läsas (på grund av en ogiltig sökväg eller ett behörighetsproblem) eller så finns det ingen giltig fragmentmodell:

      * `No content fragment model specified`
      * `Cannot create a resource of given model '/foo/bar/qux'`
   * Det gick inte att skapa innehållsfragmentet (eventuellt ett behörighetsproblem):

      * `Could not create content fragment`
   * Titeln och/eller beskrivningen kunde inte uppdateras:

      * `Could not set value on content fragment`
   * Det gick inte att ange metadata:

      * `Could not set metadata on content fragment`
   * Innehållselementet kunde inte hittas eller kunde inte uppdateras

      * `Could not update content element`
      * `Could not update fragment data of element`

   De detaljerade felmeddelandena returneras vanligtvis på följande sätt:

   ```xml
   {
     "class": "core/response",
     "properties": {
       "path": "/api/assets/foo/bar/qux",
       "location": "/api/assets/foo/bar/qux.json",
       "parentLocation": "/api/assets/foo/bar.json",
       "status.code": 500,
       "status.message": "...{error message}.."
     }
   }
   ```

## API-referens {#api-reference}

Här finns detaljerade API-referenser:

* [Adobe Experience Manager Assets API - innehållsfragment](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/assets-api-content-fragments/index.html)

* [HTTP API för Assets](/help/assets/mac-api-assets.md)

   * [Tillgängliga funktioner](/help/assets/mac-api-assets.md#available-features)

## Ytterligare resurser {#additional-resources}

Mer information finns i:

* [Resurser för HTTP API-dokumentation](/help/assets/mac-api-assets.md)
* [AEM Gem-session: OAuth](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-oauth-server-functionality-in-aem.html)

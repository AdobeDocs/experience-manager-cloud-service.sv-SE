---
title: Stöd för Adobe Experience Manager as a Cloud Service Content Fragments i Assets HTTP API
description: Läs om stödet för innehållsfragment i Assets HTTP API, en viktig del av Adobe Experience Manager headless-leveransfunktion.
feature: Content Fragments, Assets HTTP API
exl-id: d72cc0c0-0641-4fd6-9f87-745af5f2c232
role: User, Admin
source-git-commit: 7386298ee83eef5693ce00077659bbc4a1a70d24
workflow-type: tm+mt
source-wordcount: '1829'
ht-degree: 0%

---

# Stöd för innehållsfragment i AEM Assets HTTP API {#content-fragments-support-in-aem-assets-http-api}

## Ökning {#overview}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/content/assets/extending/assets-api-content-fragments.html) |
| AEM as a Cloud Service | Den här artikeln |

Läs om stödet för innehållsfragment i Assets HTTP API, en viktig del av Adobe Experience Manager headless-leveransfunktion (AEM).

>[!NOTE]
>
>Se [AEM API:er för leverans och hantering av strukturerat innehåll](/help/headless/apis-headless-and-content-fragments.md) för en översikt över de olika tillgängliga API:erna och en jämförelse av några av de berörda begreppen.
>
>OpenAPI:erna [Content Fragment och Content Fragment Model](/help/headless/content-fragment-openapis.md) är också tillgängliga.

>[!NOTE]
>
>[Assets HTTP API](/help/assets/mac-api-assets.md) omfattar:
>
>* ASSETS REST API
>* inklusive stöd för innehållsfragment
>
>Den aktuella implementeringen av Assets HTTP API baseras på arkitekturstilen [REST](https://en.wikipedia.org/wiki/Representational_state_transfer).

>[!NOTE]
>
>Den senaste informationen om Experience Manager API:er finns även på [Adobe Experience Manager as a Cloud Service API:er](https://developer.adobe.com/experience-cloud/experience-manager-apis/).

Med [Assets REST API](/help/assets/mac-api-assets.md) kan utvecklare av Adobe Experience Manager as a Cloud Service komma åt innehåll (som lagras i AEM) direkt via HTTP-API:t via CRUD-åtgärder (Create, Read, Update, Delete).

Med API:t kan du använda Adobe Experience Manager as a Cloud Service som ett headless CMS (Content Management System) genom att tillhandahålla innehållstjänster till ett JavaScript front-end-program. Eller något annat program som kan köra HTTP-begäranden och hantera JSON-svar.

[Single Page-program (SPA)](/help/implementing/developing/hybrid/introduction.md), ramverksbaserade eller anpassade, kräver till exempel innehåll som tillhandahålls via HTTP API, ofta i JSON-format.

[AEM Core Components](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) har ett anpassningsbart API som kan hantera nödvändiga läsåtgärder i detta syfte, och vars JSON-utdata kan anpassas, men de kräver AEM WCM-kunskaper (Web Content Management) för implementering. Detta beror på att de måste finnas på sidor som är baserade på dedikerade AEM. Det är inte varje SPA utvecklingsorganisation som har direkt tillgång till sådan kunskap.

Detta är när Assets REST API kan användas. Med det kan utvecklare komma åt resurser (till exempel bilder och innehållsfragment) direkt, utan att först behöva bädda in dem på en sida, och leverera innehållet i serialiserat JSON-format.

>[!NOTE]
>
>Det går inte att anpassa JSON-utdata från Assets REST API.

Med Assets REST API kan utvecklare ändra innehåll genom att skapa nya, uppdatera eller ta bort befintliga resurser, innehållsfragment och mappar.

Assets REST API:

* följer [HATEOAS-principen](https://en.wikipedia.org/wiki/HATEOAS)

* implementerar formatet [SIREN](https://github.com/kevinswiber/siren)

## Förutsättningar {#prerequisites}

Assets REST API är tillgängligt för alla färdiga installationer av en nyligen använd Adobe Experience Manager as a Cloud Service-version.

## Viktiga begrepp {#key-concepts}

Assets REST API ger [REST](https://en.wikipedia.org/wiki/Representational_state_transfer)-åtkomst till resurser som lagras i en AEM.

Slutpunkten `/api/assets` används och resursens sökväg krävs för att komma åt den (utan radavståndet `/content/dam`).

* Det innebär att du kan få tillgång till resursen på
   * `/content/dam/path/to/asset`
* Begäran:
   * `/api/assets/path/to/asset`

Om du till exempel vill komma åt `/content/dam/wknd/en/adventures/cycling-tuscany` begär du `/api/assets/wknd/en/adventures/cycling-tuscany.json`

>[!NOTE]
>Åtkomst över:
>
>* `/api/assets` **behöver inte** använda väljaren `.model`.
>* `/content/path/to/page` **does** kräver att väljaren `.model` används.

HTTP-metoden avgör vilken åtgärd som ska utföras:

* **GET** - för att hämta en JSON-representation av en resurs eller en mapp
* **POST** - för att skapa resurser eller mappar
* **PUT** - för att uppdatera egenskaperna för en resurs eller mapp
* **DELETE** - om du vill ta bort en resurs eller mapp

>[!NOTE]
>
>Parametrarna för begärandeinnehåll och/eller URL kan användas för att konfigurera vissa av dessa åtgärder. Definiera till exempel att en mapp eller en resurs ska skapas av en **POST** -begäran.

Exakt format för begäranden som stöds definieras i [API Reference](/help/assets/content-fragments/assets-api-content-fragments.md#api-reference) -dokumentationen.

>[!NOTE]
>
>OpenAPI:erna [Content Fragment och Content Fragment Model](/help/headless/content-fragment-openapis.md) är också tillgängliga.

### Transaktionsbeteende {#transactional-behavior}

Alla förfrågningar är atomiska.

Detta innebär att efterföljande (`write`) begäranden inte kan kombineras till en enda transaktion som kan lyckas eller misslyckas som en enskild enhet.

### AEM (Assets) REST API jämfört med AEM {#aem-assets-rest-api-versus-aem-components}

<table>
 <thead>
  <tr>
   <td>Proportioner</td>
   <td>Assets REST API<br/> </td>
   <td>AEM komponent <br/> (komponenter som använder Sling Models)</td>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td>Användningsfall som stöds</td>
   <td>Allmänt syfte.</td>
   <td><p>Optimerad för konsumtion i ett Single Page-program (SPA) eller i något annat (innehållsförbrukande) sammanhang.</p> <p>Den kan också innehålla layoutinformation.</p> </td>
  </tr>
  <tr>
   <td>Åtgärder som stöds</td>
   <td><p>Skapa, läsa, uppdatera, ta bort.</p> <p>Med ytterligare åtgärder, beroende på enhetstyp.</p> </td>
   <td>Skrivskyddad.</td>
  </tr>
  <tr>
   <td>Åtkomst</td>
   <td><p>Den kan nås direkt.</p> <p>Använder <code>/api/assets </code>slutpunkten, mappad till <code>/content/dam</code> (i databasen).</p> 
   <p>En exempelsökväg skulle se ut så här: <code>/api/assets/wknd/en/adventures/cycling-tuscany.json</code></p>
   </td>
    <td><p>Det måste refereras via en AEM på en AEM.</p> <p>Använder väljaren <code>.model</code> för att skapa JSON-representationen.</p> <p>En exempelsökväg skulle se ut så här:<br/> <code>/content/wknd/language-masters/en/adventures/cycling-tuscany.model.json</code></p> 
   </td>
  </tr>
  <tr>
   <td>Dokumentskydd</td>
   <td><p>Flera alternativ är möjliga.</p> <p>OAuth föreslås; kan konfigureras separat från standardinställningen.</p> </td>
   <td>Använder AEM standardinställningar.</td>
  </tr>
  <tr>
   <td>Arkitektur</td>
   <td><p>Skrivåtkomst adresserar vanligtvis en Author-instans.</p> <p>Läsningen kan även dirigeras till en Publish-instans.</p> </td>
   <td>Eftersom den här metoden är skrivskyddad används den vanligtvis för Publish-instanser.</td>
  </tr>
  <tr>
   <td>Utdata</td>
   <td>JSON-baserade SIREN-utdata: utförlig, men kraftfull. Det gör det möjligt att navigera i innehållet.</td>
   <td>JSON-baserade egna utdata som kan konfigureras via Sling-modeller. Att navigera i innehållsstrukturen är svårt att implementera (men inte nödvändigtvis omöjligt).</td>
  </tr>
 </tbody>
</table>

### Dokumentskydd {#security}

Om Assets REST API används i en miljö utan särskilda autentiseringskrav måste AEM CORS-filter konfigureras korrekt.

>[!NOTE]
>
>Mer information finns i:
>
>* [CORS/AEM har förklarats](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html)
>* [Video - Utveckla för CORS med AEM (04:06)](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/develop-for-cross-origin-resource-sharing.html)
>

I miljöer med specifika autentiseringskrav rekommenderas OAuth.

## Tillgängliga funktioner {#available-features}

Innehållsfragment är en specifik typ av resurs, se [Arbeta med innehållsfragment](/help/assets/content-fragments/content-fragments.md).

Mer information om funktioner som är tillgängliga via API finns i:

* [Assets REST API](/help/assets/mac-api-assets.md)
* [Enhetstyper](/help/assets/content-fragments/assets-api-content-fragments.md#entity-types), där funktioner som är specifika för varje typ som stöds (som är relevant för innehållsfragment) förklaras

>[!NOTE]
>
>OpenAPI:erna [Content Fragment och Content Fragment Model](/help/headless/content-fragment-openapis.md) är också tillgängliga.

### Sidindelning {#paging}

Assets REST API har stöd för sidindelning (för GET-begäranden) via URL-parametrarna:

* `offset` - numret på den första (underordnade) entiteten som ska hämtas
* `limit` - det maximala antalet enheter som returneras

Svaret innehåller sidindelningsinformation som en del av avsnittet `properties` i SIREN-utdata. Den här `srn:paging`-egenskapen innehåller det totala antalet (underordnade) entiteter ( `total`), förskjutningen och gränsen ( `offset`, `limit`) som anges i begäran.

>[!NOTE]
>
>Sidindelning används vanligtvis för behållarentiteter (d.v.s. mappar eller resurser med återgivningar), eftersom den relaterar till den begärda entitetens underordnade.

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

Assets REST API ger åtkomst till egenskaperna för en mapp. Till exempel dess namn och titel. Assets visas som underordnade enheter till mappar och undermappar.

>[!NOTE]
>
>Beroende på resurstypen för de underordnade resurserna och mapparna kan listan med underordnade enheter redan innehålla den fullständiga uppsättningen egenskaper som definierar respektive underordnade enhet. Alternativt kan bara en reducerad uppsättning egenskaper visas för en enhet i den här listan över underordnade enheter.

### Assets {#assets}

Om en resurs begärs returnerar svaret dess metadata, t.ex. titel, namn och annan information som definieras i respektive resursschema.

Binära data för en resurs visas som en SIREN-länk av typen `content`.

Assets kan ha flera renderingar. Dessa visas vanligtvis som underordnade entiteter, ett undantag är en miniatyrrendering som visas som en länk av typen `thumbnail` ( `rel="thumbnail"`).

### Innehållsfragment {#content-fragments}

Ett [innehållsfragment](/help/assets/content-fragments/content-fragments.md) är en särskild typ av resurs. De kan användas för att komma åt strukturerade data, t.ex. texter, siffror och datum.

Eftersom det finns flera skillnader mellan *standardresurser* (till exempel bilder eller ljud) gäller vissa ytterligare regler för att hantera dem.

#### Representation {#representation}

Innehållsfragment:

* Visa inga binära data.
* Finns i JSON-utdata (inom egenskapen `properties`).

* De betraktas också som atomiska. Det innebär att elementen och variationerna visas som en del av fragmentets egenskaper jämfört med som länkar eller underordnade enheter. Detta ger effektiv åtkomst till nyttolasten för ett fragment.

#### Innehållsmodeller och innehållsfragment {#content-models-and-content-fragments}

För närvarande visas inte modellerna som definierar strukturen för ett innehållsfragment via ett HTTP-API. Därför måste *konsumenten* känna till modellen för ett fragment (minst ett minimum), även om den mesta informationen kan härledas från nyttolasten, eftersom datatyper och så vidare är en del av definitionen.

Om du vill skapa ett innehållsfragment måste modellens (interna databas) sökväg anges.

#### Associerat innehåll {#associated-content}

Associerat innehåll visas inte.

## Använda {#using}

Användningen kan variera beroende på om du använder en AEM Author eller Publish-miljö, tillsammans med ditt specifika användningsexempel.

* Vi rekommenderar att skapandet är bundet till en Author-instans ([) och att det för närvarande inte finns något sätt att replikera ett fragment för publicering med denna API](/help/assets/content-fragments/assets-api-content-fragments.md#limitations)).
* Leverans är möjlig från båda, eftersom AEM endast skickar begärt innehåll i JSON-format.

   * Lagring och leverans från en AEM Author-instans bör räcka för program bakom brandväggen, mediabibliotek.

   * För webbpublicering rekommenderas en AEM Publish-instans.

>[!CAUTION]
>
>Dispatcher-konfigurationen på AEM molninstanser kan blockera åtkomst till `/api`.

>[!NOTE]
>
>Se [API-referens](/help/assets/content-fragments/assets-api-content-fragments.md#api-reference). Särskilt [Adobe Experience Manager Assets API - innehållsfragment](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/assets-api-content-fragments/index.html).
>
>OpenAPI:erna [Content Fragment och Content Fragment Model](/help/headless/content-fragment-openapis.md) är också tillgängliga.

## Begränsningar {#limitations}

Det finns några begränsningar:

* **Modeller för innehållsfragment stöds för närvarande inte**: de kan inte läsas eller skapas. För att kunna skapa eller uppdatera ett befintligt innehållsfragment måste utvecklarna veta rätt sökväg till innehållsfragmentmodellen. För närvarande är det enda sättet att få en översikt över dessa genom administrationsgränssnittet.
* **Referenser ignoreras**. För närvarande finns det inga kontroller för om ett befintligt innehållsfragment refereras. Om du tar bort ett innehållsfragment kan det därför leda till problem på en sida som innehåller en referens till det borttagna innehållsfragmentet.
* **JSON-datatyp** REST API-utdata för *JSON-datatypen* är *strängbaserade utdata*.

## Statuskoder och felmeddelanden {#status-codes-and-error-messages}

Följande statuskoder kan ses under de relevanta omständigheterna:

* **200** (OK)

  Returneras när:

   * begär ett innehållsfragment via `GET`
   * uppdaterar ett innehållsfragment med hjälp av `PUT`

* **201** (skapad)

  Returneras när:

   * har skapat ett innehållsfragment genom `POST`

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

   * Den överordnade mappen finns inte (när du skapar ett innehållsfragment med hjälp av `POST`)
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

  De detaljerade felmeddelandena returneras på följande sätt:

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

* [Adobe Experience Manager Assets API - innehållsfragment](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/assets-api-content-fragments/index.html)

* [ASSETS HTTP API](/help/assets/mac-api-assets.md)

   * [Tillgängliga funktioner](/help/assets/mac-api-assets.md#available-features)

* OpenAPI:erna [Content Fragment och Content Fragment Model](/help/headless/content-fragment-openapis.md) är också tillgängliga.

## Ytterligare resurser {#additional-resources}

Mer information finns i:

* [Assets HTTP API-dokumentation](/help/assets/mac-api-assets.md)
* [AEM Gem-session: OAuth](https://experienceleague.adobe.com/docs/events/experience-manager-gems-recordings/gems2014/aem-oauth-server-functionality-in-aem.html)

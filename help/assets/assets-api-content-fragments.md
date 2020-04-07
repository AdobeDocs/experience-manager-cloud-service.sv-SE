---
title: Adobe Experience Manager som ett molntjänstinnehåll Stöd för innehållsfragment i Assets HTTP API
description: Lär dig mer om Adobe Experience Manager som stöd för molntjänstinnehållsfragment i Assets HTTP API.
translation-type: tm+mt
source-git-commit: 26833f59f21efa4de33969b7ae2e782fe5db8a14

---


# Stöd för innehållsfragment i AEM Assets HTTP API{#content-fragments-support-in-aem-assets-http-api}

## Översikt {#overview}

>[!NOTE]
>
>HTTP-API:t för [resurser](/help/assets/mac-api-assets.md) omfattar:
>
>* Resurser REST API
>* inklusive stöd för innehållsfragment
>
>
Den aktuella implementeringen av Assets HTTP API baseras på arkitekturformatet [REST](https://en.wikipedia.org/wiki/Representational_state_transfer) .

Med [Assets REST API](/help/assets/mac-api-assets.md) kan utvecklare av Adobe Experience Manager som en molntjänst få åtkomst till innehåll (som lagras i AEM) direkt via HTTP-API:t via CRUD-åtgärder (Skapa, Läs, Uppdatera, Ta bort).

Med API:t kan du använda Adobe Experience Manager som en molntjänst som ett headless CMS (Content Management System) genom att tillhandahålla innehållstjänster till ett JavaScript-klientprogram. Eller något annat program som kan köra HTTP-begäranden och hantera JSON-svar.

Exempelvis kräver Single Page Applications (SPA), ramverksbaserade eller anpassade, innehåll som tillhandahålls via HTTP API, ofta i JSON-format.

Även om [AEM Core Components](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html) är ett mycket omfattande, flexibelt och anpassningsbart API som kan användas för de nödvändiga läsåtgärderna, och vars JSON-utdata kan anpassas, behöver de AEM WCM-kunskaper (Web Content Management) för implementeringen eftersom de måste finnas på sidor som är baserade på dedikerade AEM-mallar. Alla SPA-utvecklingsorganisationer har inte direkt tillgång till sådan kunskap.

Detta är när REST API:t för resurser kan användas. Med det kan utvecklare komma åt resurser (till exempel bilder och innehållsfragment) direkt, utan att först behöva bädda in dem på en sida, och leverera innehållet i serialiserat JSON-format.

>[!NOTE]
>Det går inte att anpassa JSON-utdata från Assets REST API.

Med Assets REST API kan utvecklare ändra innehåll genom att skapa nya, uppdatera eller ta bort befintliga resurser, innehållsfragment och mappar.

Resursens REST API:

* följer [HATEOAS-principen](https://en.wikipedia.org/wiki/HATEOAS)

* implementerar [SIREN-formatet](https://github.com/kevinswiber/siren)

## Förutsättningar {#prerequisites}

Resursens REST API är tillgängligt för varje körklar installation av en nyligen använd Adobe Experience Manager som en molntjänstversion.

## Viktiga begrepp {#key-concepts}

Resursens REST API ger åtkomst i [REST](https://en.wikipedia.org/wiki/Representational_state_transfer)-stil till resurser som lagras i en AEM-instans.

Slutpunkten används och resursens sökväg måste vara `/api/assets` tillgänglig (utan radavstånd `/content/dam`).

* Det innebär att du kan få tillgång till resursen på:
   * `/content/dam/path/to/asset`
* Du måste begära:
   * `/api/assets/path/to/asset`

Till exempel för att få åtkomst `/content/dam/wknd/en/adventures/cycling-tuscany`och begära `/api/assets/wknd/en/adventures/cycling-tuscany.json`

>[!NOTE]
>Åtkomst över:
>* `/api/assets` behöver **inte** använda `.model` väljaren.
>* `/content/assets` kräver **** att `.model` väljaren används.


HTTP-metoden avgör vilken åtgärd som ska utföras:

* **GET** - för att hämta en JSON-representation av en resurs eller en mapp
* **POST** - för att skapa nya resurser eller mappar
* **PUT** - för att uppdatera egenskaperna för en resurs eller mapp
* **TA BORT** - för att ta bort en resurs eller mapp

>[!NOTE]
>
>Begärandetexten och/eller URL-parametrarna kan användas för att konfigurera vissa av dessa åtgärder. Ange till exempel att en mapp eller en resurs ska skapas av en **POST** -begäran.

<!--
The exact format of supported requests is defined in the [API Reference](/help/assets/assets-api-content-fragments.md#api-reference) documentation.
-->

### Transaktionsbeteende {#transactional-behavior}

Alla förfrågningar är atomiska.

Detta innebär att efterföljande (`write`) begäranden inte kan kombineras till en enda transaktion som kan lyckas eller misslyckas som en enskild enhet.

### AEM (Assets) REST API jämfört med AEM Components {#aem-assets-rest-api-versus-aem-components}

<table>
 <thead>
  <tr>
   <td>Proportioner</td>
   <td>Resurser REST API<br/> </td>
   <td>AEM-komponent<br/> (komponenter som använder Sling-modeller)</td>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td>Användningsfall som stöds</td>
   <td>Allmänt syfte.</td>
   <td><p>Optimerad för konsumtion i ett Single Page Application (SPA) eller i något annat (innehållsförbrukande) sammanhang.</p> <p>Kan även innehålla layoutinformation.</p> </td>
  </tr>
  <tr>
   <td>Åtgärder som stöds</td>
   <td><p>Skapa, läsa, uppdatera, ta bort.</p> <p>Med ytterligare åtgärder beroende på enhetstyp.</p> </td>
   <td>Skrivskyddad.</td>
  </tr>
  <tr>
   <td>Åtkomst</td>
   <td><p>Kan nås direkt.</p> <p>Använder <code>/api/assets </code>slutpunkten, mappad till <code>/content/dam</code> (i databasen).</p> 
   <p>En exempelsökväg skulle se ut så här: <code>/api/assets/wknd/en/adventures/cycling-tuscany.json</code></p>
   </td>
    <td><p>Måste refereras via en AEM-komponent på en AEM-sida.</p> <p>Använder väljaren <code>.model</code> för att skapa JSON-representationen.</p> <p>En exempelsökväg skulle se ut så här:<br/> <code>/content/wknd/language-masters/en/adventures/cycling-tuscany.model.json</code></p> 
   </td>
  </tr>
  <tr>
   <td>Dokumentskydd</td>
   <td><p>Flera alternativ är möjliga.</p> <p>OAuth föreslås. kan konfigureras separat från standardinställningarna.</p> </td>
   <td>Använder AEM:s standardinställning.</td>
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

Om REST API:t för resurser används i en miljö utan särskilda autentiseringskrav måste AEM:s CORS-filter konfigureras korrekt.

>[!NOTE]
>
>Mer information finns i:
>
>* [CORS/AEM - förklaring](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/cors-security-article-understand.html)
>* [Video - Developing for CORS with AEM](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/cors-security-technical-video-develop.html)
>



I miljöer med specifika autentiseringskrav rekommenderas OAuth.

## Tillgängliga funktioner {#available-features}

Innehållsfragment är en specifik typ av resurs, se [Arbeta med innehållsfragment](/help/assets/content-fragments/content-fragments.md).

Mer information om funktioner som är tillgängliga via API finns i:

* REST API för [resurser](/help/assets/mac-api-assets.md)
* [Enhetstyper](/help/assets/assets-api-content-fragments.md#entity-types), där funktioner som är specifika för varje typ som stöds (som är relevant för innehållsfragment) förklaras

### Sidindelning {#paging}

REST API:t för Resurser stöder sidindelning (för GET-begäranden) via URL-parametrarna:

* `offset` - numret på den första (underordnade) entiteten som ska hämtas
* `limit` - det maximala antalet returnerade enheter

Svaret kommer att innehålla sidindelningsinformation som en del av `properties` avsnittet i SIREN-utdata. Den här `srn:paging` egenskapen innehåller det totala antalet (underordnade) entiteter ( `total`), förskjutningen och gränsen ( `offset`, `limit`) som anges i begäran.

>[!NOTE]
>
>Sidindelning används vanligtvis för behållarentiteter (d.v.s. mappar eller resurser med återgivningar), eftersom det relaterar till den begärda entitetens underordnade.

#### Exempel: Sidindelning {#example-paging}

`GET /api/assets.json?offset=2&limit=3`

```
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

Mappar fungerar som behållare för resurser och andra mappar. De återspeglar strukturen i AEM-innehållsdatabasen.

Resursens REST API ger åtkomst till en mapps egenskaper. till exempel namn, titel osv. Resurser visas som underordnade enheter till mappar och undermappar.

>[!NOTE]
>
>Beroende på resurstypen för de underordnade resurserna och mapparna kan listan med underordnade enheter redan innehålla den fullständiga uppsättningen egenskaper som definierar respektive underordnade enhet. Alternativt kan bara en reducerad uppsättning egenskaper visas för en enhet i den här listan över underordnade enheter.

### Assets {#assets}

Om en resurs begärs returneras dess metadata. som titel, namn och annan information som definieras av respektive resursschema.

En tillgångs binära data visas som en SIREN-länk av typen `content` (kallas även `rel attribute`).

Resurser kan ha flera renderingar. Dessa visas vanligtvis som underordnade enheter, och ett undantag är en miniatyrrendering, som visas som en länk av typen `thumbnail` ( `rel="thumbnail"`).

### Innehållsfragment {#content-fragments}

Ett [innehållsfragment](/help/assets/content-fragments/content-fragments.md) är en särskild typ av resurs. De kan användas för att komma åt strukturerade data, t.ex. texter, siffror och datum.

Eftersom det finns flera skillnader mellan *standardresurser* (t.ex. bilder och ljud) gäller vissa ytterligare regler för att hantera dem.

#### Representation {#representation}

Innehållsfragment:

* Visa inga binära data.
* Finns helt i JSON-utdata (inom `properties` egenskapen).

* betraktas också som atomiska, dvs. elementen och variationerna exponeras som en del av fragmentets egenskaper jämfört med som länkar eller underordnade enheter. Detta ger effektiv åtkomst till nyttolasten för ett fragment.

#### Innehållsmodeller och innehållsfragment {#content-models-and-content-fragments}

För närvarande visas inte modellerna som definierar strukturen för ett innehållsfragment via ett HTTP-API. Därför måste *konsumenten* känna till fragmentmodellen (minst ett minimum), även om de flesta uppgifter kan härledas från nyttolasten. som datatyper, osv. är en del av definitionen.

Om du vill skapa ett nytt innehållsfragment måste modellens (interna databas) sökväg anges.

#### Associerat innehåll {#associated-content}

Associerat innehåll visas för närvarande inte.

## Använda {#using}

Användningssättet kan variera beroende på om du använder en AEM-författare eller publiceringsmiljö, tillsammans med ditt specifika användningsexempel.

* Skapandet är strikt bundet till en författarinstans ([och det finns för närvarande inget sätt att replikera ett fragment för publicering med denna API](/help/assets/assets-api-content-fragments.md#limitations)).
* Leverans är möjlig från båda, eftersom AEM endast skickar begärt innehåll i JSON-format.

   * Lagring och leverans från en AEM-författarinstans bör räcka för program bakom brandväggen, mediabibliotek.

   * För direktsänd webbleverans rekommenderas en AEM-publiceringsinstans.

>[!CAUTION]
>
>Dispatcher-konfigurationen på AEM-molninstanser kan blockera åtkomst till `/api`.

<!--
>[!NOTE]
>
>For further details, see the [API Reference](/help/assets/assets-api-content-fragments.md#api-reference). In particular, [Adobe Experience Manager Assets API - Content Fragments](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/assets-api-content-fragments/index.html). 
-->

### Läsning/leverans {#read-delivery}

Användning sker via:

`GET /{cfParentPath}/{cfName}.json`

Exempel:

`http://<host>/api/assets/wknd/en/adventures/cycling-tuscany.json`

Svaret är serialiserat JSON med innehållet strukturerat som i innehållsfragmentet. Referenser levereras som referens-URL:er.

Det finns två typer av läsåtgärder:

* När du läser ett visst innehållsfragment efter sökväg, returneras JSON-representationen av innehållsfragmentet.
* Läsa en mapp med innehållsfragment efter sökväg: returnerar JSON-representationerna för alla innehållsfragment i mappen.

### Skapa {#create}

Användning sker via:

`POST /{cfParentPath}/{cfName}`

Brödtexten måste innehålla en JSON-representation av det innehållsfragment som ska skapas, inklusive allt ursprungligt innehåll som ska anges för elementen i innehållsfragmentet. Det är obligatoriskt att ange `cq:model` egenskapen och den måste peka på en giltig innehållsfragmentmodell. Om du inte gör det uppstår ett fel. Du måste också lägga till en rubrik `Content-Type` som är inställd på `application/json`.

### Update {#update}

Användning sker via

`PUT /{cfParentPath}/{cfName}`

Brödtexten måste innehålla en JSON-representation av vad som ska uppdateras för det angivna innehållsfragmentet.

Detta kan helt enkelt vara titeln eller beskrivningen av ett innehållsfragment, ett enskilt element eller alla elementvärden och/eller metadata.

### Ta bort {#delete}

Användning sker via:

`DELETE /{cfParentPath}/{cfName}`

## Begränsningar {#limitations}

Det finns några begränsningar:

* **Variationer kan inte skrivas och uppdateras.** Om dessa variationer läggs till i en nyttolast (t.ex. för uppdateringar) kommer de att ignoreras. Variationen kommer dock att hanteras via leveransen ( `GET`).

* **Modeller för innehållsfragment stöds** inte för närvarande: kan inte läsas eller skapas. För att kunna skapa ett nytt, eller uppdatera ett befintligt, innehållsfragment, måste utvecklarna veta rätt sökväg till innehållsfragmentmodellen. För närvarande är det enda sättet att få en översikt över dessa genom administrationsgränssnittet.
* **Referenser ignoreras**. För närvarande finns det inga kontroller för om ett befintligt innehållsfragment refereras. Om du t.ex. tar bort ett innehållsfragment kan det leda till problem på en sida som innehåller en referens till det borttagna innehållsfragmentet.

## Statuskoder och felmeddelanden {#status-codes-and-error-messages}

Följande statuskoder kan ses under de relevanta omständigheterna:

1. 200 (OK)

   Returneras när:

   * begära ett innehållsfragment via `GET`

   * uppdaterar ett innehållsfragment via `PUT`

1. 201 (skapad)

   Returneras när:

   * har skapat ett innehållsfragment via `POST`

1. 404 (Hittades inte)

   Returneras när:

   * det begärda innehållsfragmentet inte finns

1. 500 (Internt serverfel)

   >[!NOTE]
   >
   >Detta fel returneras:
   >
   >    * när ett fel som inte kan identifieras med en viss kod har inträffat
   >    * när den angivna nyttolasten inte var giltig


   I följande exempel visas vanliga scenarier när den här felstatusen returneras, tillsammans med felmeddelandet (monospace) som genereras:

   * Den överordnade mappen finns inte (när du skapar ett innehållsfragment via `POST`)
   * Ingen innehållsfragmentmodell har angetts (cq:model saknas), kan inte läsas (på grund av en ogiltig sökväg eller ett behörighetsproblem) eller så finns det ingen giltig fragmentmodell/mall:

      * `No content fragment model specified`
      * `Cannot create a resource of given model '/foo/bar/qux'`
      * `Cannot adapt the resource '/foo/bar/qux' to a content fragment template`
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
<!--
* [Adobe Experience Manager Assets API - Content Fragments](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/assets-api-content-fragments/index.html)
-->

* [HTTP API för Assets](/help/assets/mac-api-assets.md)

   * [Tillgängliga funktioner](/help/assets/mac-api-assets.md#available-features)

## Additional Resources {#additional-resources}

Mer information finns i:

* [Resurser för HTTP API-dokumentation](/help/assets/mac-api-assets.md)
* [AEM Gem-session: OAuth](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-oauth-server-functionality-in-aem.html)


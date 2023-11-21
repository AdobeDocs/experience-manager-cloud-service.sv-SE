---
title: ContextHub JavaScript API-referens
description: ContextHub JavaScript API är tillgängligt för skript när ContextHub-komponenten har lagts till på sidan
exl-id: ec35bef5-610c-4e85-a43a-d4201b5eb03e
source-git-commit: 8ed477ec0c54bb0913562b9581e699c0bdc973ec
workflow-type: tm+mt
source-wordcount: '4613'
ht-degree: 0%

---

# ContextHub JavaScript API-referens {#contexthub-javascript-api-reference}

ContextHub JavaScript API är tillgängligt för skript när [ContextHub-komponenten har lagts till på sidan](adding-contexthub.md).

## ContextHub-konstanter {#contexthub-constants}

Konstantvärden som definieras av JavaScript-API:t för ContextHub.

### Händelsekonstanter {#event-constants}

I följande tabell visas namnen på händelser som inträffar för ContextHub Stores. Se även [ContextHub.Utils.Eventing](#contexthub-utils-eventing).

| Konstant | Beskrivning | Värde |
|---|---|---|
| `ContextHub.Constants.EVENT_NAMESPACE` | ContextHub&#39;s event namespace | `ch` |
| `ContextHub.Constants.EVENT_ALL_STORES_READY` | Anger att alla nödvändiga butiker är registrerade, initierade och klara att användas | `all-stores-ready` |
| `ContextHub.Constants.EVENT_STORES_PARTIALLY_READY` | Anger att inte alla butiker initierades inom en angiven tidsgräns | `stores-partially-ready` |
| `ContextHub.Constants.EVENT_STORE_REGISTERED` | Utlöses när en butik registreras | `store-registered` |
| `ContextHub.Constants.EVENT_STORE_READY` | Anger att butikerna är redo att arbeta. Den aktiveras omedelbart efter registreringen, förutom JSONP-arkiv, där den aktiveras när data hämtas). | `store-ready` |
| `ContextHub.Constants.EVENT_STORE_UPDATED` | Utlöses när en butik uppdaterar sin beständighet | `store-updated` |
| `ContextHub.Constants.PERSISTENCE_CONTAINER_NAME` | Namn på beständiga behållare | `ContextHubPersistence` |
| `ContextHub.Constants.SERVICE_RAW_RESPONSE_KEY` | Lagrar ett särskilt namn på en beständig nyckel där JSON-resultatet i Raw-format lagras | `/_/raw-response` |
| `ContextHub.Constants.SERVICE_RESPONSE_TIME_KEY` | Lagrar en specifik tidsstämpel som anger när JSON-data hämtades | `/_/response-time` |
| `ContextHub.Constants.SERVICE_LAST_URL_KEY` | Lagrar en specifik URL för JSON-tjänsten som användes under det senaste anropet | `/_/url` |
| `ContextHub.Constants.IS_CONTAINER_EXPANDED` | Anger om användargränssnittet för ContextHub är expanderat | `/_/container-expanded` |

### Konstanter för gränssnittshändelser {#ui-event-constants}

I följande tabell visas namnen på händelser som inträffar för användargränssnittet för ContextHub.

| **Konstant** | **Beskrivning** | **Värde** |
|---|---|---|
| `ContextHub.Constants.EVENT_UI_MODE_REGISTERED` | Utlöses när ett läge registreras | `ui-mode-registered` |
| `ContextHub.Constants.EVENT_UI_MODE_UNREGISTERED` | Utlöses när ett läge avregistreras | `ui-mode-unregistered` |
| `ContextHub.Constants.EVENT_UI_MODE_RENDERER_REGISTERED` | Utlöses när en lägesåtergivare registreras | `ui-mode-renderer-registered` |
| `ContextHub.Constants.EVENT_UI_MODE_RENDERER_UNREGISTERED` | Utlöses när en lägesåtergivare avregistreras | `ui-mode-renderer-unregistered` |
| `ContextHub.Constants.EVENT_UI_MODE_ADDED` | Utlöses när ett nytt läge läggs till | `ui-mode-added` |
| `ContextHub.Constants.EVENT_UI_MODE_REMOVED` | Utlöses när ett läge tas bort | `ui-mode-removed` |
| `ContextHub.Constants.EVENT_UI_MODE_SELECTED` | Utlöses när ett läge väljs av användaren | `ui-mode-selected` |
| `ContextHub.Constants.EVENT_UI_MODULE_REGISTERED` | Utlöses när en ny modul registreras | `ui-module-registered` |
| `ContextHub.Constants.EVENT_UI_MODULE_UNREGISTERED` | Utlöses när en modul avregistreras | `ui-module-unregistered` |
| `ContextHub.Constants.EVENT_UI_MODULE_RENDERER_REGISTERED` | Utlöses när en modulåtergivare registreras | `ui-module-renderer-registered` |
| `ContextHub.Constants.EVENT_UI_MODULE_RENDERER_UNREGISTERED` | Utlöses när en modulåtergivare avregistreras | `ui-module-renderer-unregistered` |
| `ContextHub.Constants.EVENT_UI_MODULE_ADDED` | Utlöses när en ny modul läggs till | `ui-module-added` |
| `ContextHub.Constants.EVENT_UI_MODULE_REMOVED` | Utlöses när en modul tas bort | `ui-module-removed` |
| `ContextHub.Constants.EVENT_UI_CONTAINER_ADDED` | Utlöses när gränssnittsbehållaren läggs till på sidan | `ui-container-added` |
| `ContextHub.Constants.EVENT_UI_CONTAINER_OPENED` | Utlöses när ContextHub-gränssnittet öppnas | `ui-container-opened` |
| `ContextHub.Constants.EVENT_UI_CONTAINER_CLOSED` | Utlöses när gränssnittet för ContextHub är komprimerat | `ui-container-closed` |
| `ContextHub.Constants.EVENT_UI_PROPERTY_MODIFIED` | Utlöses när en egenskap ändras | `ui-property-modified` |
| `ContextHub.Constants.EVENT_UI_RENDERED` | Utlöses varje gång ContextHub-gränssnittet återges (till exempel efter en egenskapsändring) | `ui-rendered` |
| `ContextHub.Constants.EVENT_UI_INITIALIZED` | Utlöses när gränssnittsbehållaren initieras | `ui-initialized` |
| `ContextHub.Constants.ACTIVE_UI_MODE` | Anger aktivt användargränssnittsläge | `/_/active-ui-mode` |

## ContextHub JavaScript API-referens {#contexthub-javascript-api-reference-2}

ContextHub-objektet ger åtkomst till alla arkiv.

### Funktioner (ContextHub) {#functions-contexthub}

#### getAllStores() {#getallstores}

Returnerar alla registrerade ContextHub-butiker.

Den här funktionen har inga parametrar.

##### Returnerar {#returns-}

Ett objekt som innehåller alla ContextHub-arkiv. Varje butik är ett objekt som använder samma namn som butiken.

##### Exempel {#example-}

I följande exempel hämtas alla butiker och sedan hämtas geopositioneringsarkivet:

```javascript
var allStores = ContextHub.getAllStores();
var geoloc = allStores.geolocation
```

#### getStore(name) {#getstore-name}

Hämtar en butik som ett JavaScript-objekt.

##### Parametrar {#parameters-}

* **`name`:** Namnet som butiken registrerades med.

##### Returnerar {#returns-getstore-name}

Ett objekt som representerar butiken.

##### Exempel {#example-getstore-name}

I följande exempel hämtas geopositioneringsarkivet:

```javascript
var geoloc = ContextHub.getStore("geolocation");
```

## ContextHub.SegmentEngine.Segment {#contexthub-segmentengine-segment}

Representerar ett ContextHub-segment. Använd `ContextHub.SegmentEngine.SegmentManager` för att få segment.

### Funktioner (ContextHub.ContextEngine.Segment) {#functions-contexthub-contextengine-segment}

#### getName() {#getname}

Returnerar segmentets namn som ett strängvärde.

#### getPath() {#getpath}

Returnerar databassökvägen för segmentdefinitionen som ett strängvärde.

## ContextHub.SegmentEngine.SegmentManager {#contexthub-segmentengine-segmentmanager}

Ger åtkomst till ContextHub-segment.

### Funktioner (ContextHub.SegmentEngine.SegmentManager) {#functions-contexthub-segmentengine-segmentmanager}

#### getResolvedSegments() {#getresolvedsegments}

Returnerar de segment som matchas i den aktuella kontexten. Den här funktionen har inga parametrar.

##### Returnerar {#returns-getresolvedsegments}

En array med `ContextHub.SegmentEngine.Segment` objekt.

## ContextHub.Store.Core {#contexthub-store-core}

Basklassen för ContextHub-butiker.

### Egenskaper (ContextHub.Store.Core) {#properties-contexthub-store-core}

#### eventera {#eventing}

A [`ContextHub.Utils.Eventing`](#contexthub-utils-eventing) -objekt. Använd det här objektet för bindningsfunktioner för att lagra händelser. Mer information om standardvärde och initiering finns i [`init(name,config)`](#init-name-config).

#### name {#name}

Butikens namn.

#### beständighet {#persistence}

A `ContextHub.Utils.Persistence` -objekt. Mer information om standardvärde och initiering finns i [`init(name,config)`](#init-name-config).

### Funktioner (ContextHub.Store.Core) {#functions-contexthub-store-core}

#### addAllItems(träd, alternativ) {#addallitems-tree-options}

Sammanfogar ett dataobjekt eller en array med lagringsdata. Varje nyckel/värde-par i objektet eller arrayen läggs till i arkivet (via `setItem` function):

* **Objekt:** Tangenter är egenskapsnamnen.
* **Array:** Tangenter är matrisindex.

Observera att värden kan vara objekt.

##### Parametrar {#parameters-addallitems}

* **`tree`:** (Objekt eller array) De data som ska läggas till i arkivet.
* **`options`:** (Object) Ett valfritt objekt med alternativ som skickas till funktionen setItem. Mer information finns i `options` parameter för [`setItem(key,value,options)`](#setitem-key-value-options).

##### Returnerar {#returns-addallitems}

A `boolean` värde:

* Värdet för `true` anger att dataobjektet har lagrats.
* Värdet för `false` anger att datalagret inte ändras.

#### addReference(key, anotherKey) {#addreference-key-anotherkey}

Skapar en referens från en tangent till en annan. En nyckel kan inte referera till sig själv.

##### Parametrar {#parameters-addreference}

* **`key`:** Nyckeln som refererar `anotherKey`.

* **`anotherkey`:** Nyckeln som refereras av `key`.

##### Returnerar {#returns-addreference}

A `boolean` värde:

* Värdet för `true` anger att referensen har lagts till.
* Värdet för `false` anger att ingen referens har lagts till.

#### announReadiness() {#announcereadiness}

Utlöser `ready` -händelse för den här butiken. Den här funktionen har inga parametrar och returnerar inget värde.

#### clear() {#clean}

Tar bort alla data från arkivet. Funktionen har inga parametrar och inget returvärde.

#### getItem(key) {#getitem-key}

Returnerar värdet som är associerat med en nyckel.

##### Parametrar {#parameters-getitem}

* **`key`:** (String) Nyckeln som värdet ska returneras för.

##### Returnerar {#returns-getitem}

Ett objekt som representerar värdet för nyckeln.

#### getKeys(includeInternals) {#getkeys-includeinternals}

Hämtar nycklarna från butiken. Du kan också hämta nycklar som används internt av ContextHub-ramverket.

##### Parametrar {#parameters-getkeys}

* **`includeInternals`:** Värdet för `true` innehåller internt använda nycklar i resultatet. Dessa tangenter börjar med understrecket (`_`). Standardvärdet är `false`.

##### Returnerar {#returns-getkeys}

En array med nyckelnamn ( `string` värden).

#### getReferences() {#getreferences}

Hämtar referenserna från butiken.

##### Returnerar {#returns-getreferences}

En array som använder refererande nycklar som index för refererade nycklar:

* Referensnycklar motsvarar `key` parametern för `addReference` funktion.
* Refererade nycklar motsvarar `anotherKey` parametern för `addReference` funktion.

#### getTree(includeInternals) {#gettree-includeinternals}

Hämtar dataträdet från butiken. Du kan också inkludera nyckel/värde-par som används internt av ContextHub-ramverket.

##### Parametrar {#parameters-gettree}

* `includeInternals:` Värdet för `true` innehåller nyckelvärdepar som används internt i resultatet. Nyckeln till dessa data börjar med understrecket (`_`). Standardvärdet är `false`.

##### Returnerar {#returns-gettree}

Ett objekt som representerar dataträdet. Nycklarna är objektets egenskapsnamn.

#### init(name, config) {#init-name-config}

Initierar butiken.

* Ställer in lagringsdata till ett tomt objekt.
* Ställer in butiksreferenserna till ett tomt objekt.
* The `eventChannel` är `data:<name>`, där `<name>` är butiksnamnet.
* The `storeDataKey` är `/store/<name>`, där `<name>` är butiksnamnet.

##### Parametrar {#parameters-init}

* **`name`:** Butikens namn.
* **`config`:** Ett objekt som innehåller konfigurationsegenskaper:
   * `eventDeferring`: Standardvärdet är 32.
   * `eventing`: [ContextHub.Utils.Eventing](#contexthub-utils-eventing) objekt för den här butiken. Standardvärdet är `ContextHub.eventing` objekt använder.
   * `persistence`: `ContextHub.Utils.Persistence` objekt för den här butiken. Standardvärdet är `ContextHub.persistence` -objekt.

#### isEventingPaused() {#iseventingpaused}

Avgör om händelser pausas för det här arkivet.

##### Returnerar {#returns-iseventingpaused}

Boolesk:

* `true`: Händelsen pausas så att inga händelser utlöses för det här arkivet.
* `false`: Händelser pausas inte så att händelser utlöses för det här arkivet.

#### pauseEventing() {#pauseeventing}

Pausar händelser för arkivet så att inga händelser utlöses. Den här funktionen kräver inga parametrar och returnerar inget värde.

#### removeItem(key, options) {#removeitem-key-options}

Tar bort ett nyckel/värde-par från arkivet.

När en tangent tas bort utlöser funktionen `data` -händelse. Händelsedata innehåller arkivnamnet, namnet på den nyckel som togs bort, det värde som togs bort, det nya värdet för nyckeln (null) och åtgärdstypen &quot;remove&quot;.

Du kan även förhindra att `data` -händelse.

##### Parametrar {#parameters-removeitem}

* **`key`:** (String) Namnet på nyckeln som ska tas bort.
* **`options`:** (Objekt) Ett objekt med alternativ. Följande objektegenskaper är giltiga:
   * silent: Ett värde på `true` förhindrar att `data` -händelse. Standardvärdet är `false`.

##### Returnerar {#returns-removeitem}

A `boolean` värde:

* Värdet för `true` anger att nyckel/värde-paret har tagits bort.
* Värdet för `false` anger att datalagret inte ändras eftersom nyckeln inte hittades i arkivet.

#### removeReference(key) {#removereference-key}

Tar bort en referens från arkivet.

##### Parametrar {#parameters-removereference}

* **`key`:** Nyckelreferensen som ska tas bort. Den här parametern motsvarar `key` parametern för `addReference` funktion.

##### Returnerar {#returns-removereference}

A `boolean` värde:

* Värdet för `true` anger att referensen har tagits bort.
* Värdet för `false` anger att nyckeln inte var giltig och att arkivet är oförändrat.

#### reset(keepRemainingData) {#reset-keepremainingdata}

Återställer de ursprungliga värdena för butikens beständiga data. Du kan också ta bort alla andra data från arkivet. Händelser pausas för det här arkivet när arkivet återställs. Den här funktionen returnerar inget värde.

Startvärden anges i `initialValues` egenskapen för det config-objekt som används för att instansiera lagringsobjektet.

##### Parametrar {#parameters-reset}

* **`keepRemainingData`**: (Boolean) Värdet true gör att icke-initiala data bevaras. Värdet false medför att alla data tas bort utom de ursprungliga värdena.

#### resolveReference(key, retry) {#resolvereference-key-retry}

Hämtar en refererad nyckel. Du kan också ange antalet iterationer som ska användas för att matcha den bästa matchningen.

##### Parametrar {#parameters-resolvereference}

* **`key`:** (String) Nyckeln som referensen ska matchas för. Detta `key` parametern motsvarar `key` parametern för `addReference` funktion.
* **`retry`:** (Number) Antalet iterationer som ska användas.

##### Returnerar {#returns-resolvereference}

A `string` värdet som representerar den refererade nyckeln. Om ingen referens är löst, är värdet för `key` parametern returneras.

#### resumeEventing() {#resumeeventing}

Återupptar händelser för den här butiken så att händelser utlöses. Den här funktionen definierar inga parametrar och returnerar inget värde.

#### setItem(key, value, options) {#setitem-key-value-options}

Lägger till ett nyckel/värde-par i butiken.

Utlöser `data` bara om värdet för nyckeln skiljer sig från värdet som för närvarande lagras för nyckeln. Du kan även förhindra att utlösaren av `data` -händelse.

Händelsedata innehåller butiksnamnet, nyckeln, det föregående värdet, det nya värdet och åtgärdstypen för `set`.

##### Parametrar {#parameters-setitem}

* **`key`:** (String) Namnet på nyckeln.
* **`options`:** (Objekt) Ett objekt med alternativ. Följande objektegenskaper är giltiga:
   * `silent`: Värdet för `true` förhindrar att `data` -händelse. Standardvärdet är `false`.
* **`value`:** (Objekt) Värdet som ska associeras med nyckeln.

##### Returnerar {#returns-setitem}

A `boolean` värde:

* Värdet för `true` anger att dataobjektet har lagrats.
* Värdet för `false` anger att datalagret inte ändras.

## ContextHub.Store.JSONPStore {#contexthub-store-jsonpstore}

Ett arkiv som innehåller JSON-data. Data hämtas från en extern JSONP-tjänst, eller eventuellt från en tjänst som returnerar JSON-data. Ange tjänstinformationen med [`init`](#init-name-config) när du skapar en instans av den här klassen.

Butiken använder beständighet i minnet (JavaScript-variabel). Lagringsdata är bara tillgängliga under sidans livstid.

ContextHub.Store.JSONPStore extends [ContextHub.Store.Core](#contexthub-store-core) och ärver funktionerna i den klassen.

### Funktioner (ContextHub.Store.JSONPStore) {#functions-contexthub-store-jsonpstore}

#### configureService(serviceConfig, override) {#configureservice-serviceconfig-override}

Konfigurerar informationen för anslutning till den JSONP-tjänst som det här objektet använder. Du kan antingen uppdatera eller ersätta den befintliga konfigurationen. Funktionen returnerar inget värde.

##### Parametrar {#parameters-configureservice}

* **`serviceConfig`:** Ett objekt som innehåller följande egenskaper:
   * `host`: (String) Servernamnet eller IP-adressen.
   * `jsonp`: (Boolean) Värdet true anger att tjänsten är en JSONP-tjänst, i annat fall false. När värdet är true är {callback: &quot;ContextHub.Callbacks.*Object.name*}-objektet läggs till i service.params-objektet.
   * `params`: (Object) URL-parametrar representeras som objektegenskaper. Parameternamn är egenskapsnamn och parametervärden är egenskapsvärden.
   * `path`: (String) Sökvägen till tjänsten.
   * `port`: (Number) Tjänstens portnummer.
   * `secure`: (String eller Boolean) Anger vilket protokoll som ska användas för tjänstens URL:
      * `auto`: //
      * `true`: https://
      * `false`: http://
* **åsidosätt:** (Boolean). Värdet för `true` gör att den befintliga tjänstkonfigurationen ersätts med egenskaperna för `serviceConfig`. Värdet för `false` gör att befintliga tjänstkonfigurationsegenskaper sammanfogas med egenskaperna för `serviceConfig`.

#### getRawResponse() {#getrawresponse}

Returnerar det obearbetade svar som har cachelagrats sedan det senaste anropet till JSONP-tjänsten. Funktionen kräver inga parametrar.

##### Returnerar {#returns-getrawresponse}

Ett objekt som representerar råsvaret.

#### getServiceDetails() {#getservicedetails}

Hämtar tjänstobjektet för det här ContextHub.Store.JSONPStore-objektet. Tjänsteobjektet innehåller den information som krävs för att skapa tjänst-URL:en.

##### Returnerar {#returns-getservicedetails}

Ett objekt med följande egenskaper:

* **`host`:** (String) Servernamnet eller IP-adressen.
* **`jsonp`:** (Boolean) Värdet true anger att tjänsten är en JSONP-tjänst, i annat fall false. När värdet är true är {callback: &quot;ContextHub.Callbacks.*Object.name*}-objektet läggs till i service.params-objektet.
* **`params`:** (Objekt) URL-parametrar representeras som objektegenskaper. Parameternamn är egenskapsnamn och parametervärden är egenskapsvärden.
* **`path`:** (String) Sökvägen till tjänsten.
* **`port`:** (Nummer) Tjänstens portnummer.
* **`secure`:** (Sträng eller Boolean) Anger vilket protokoll som ska användas för tjänstens URL:
   * `auto`: //
   * `true`: https://
   * `false`: http://

#### getServiceURL(resolve) {#getserviceurl-resolve}

Hämtar URL:en för JSONP-tjänsten.

##### Parametrar {#parameters-getserviceurl}

* **`resolve`:** (Boolean) Avgör om lösta parametrar ska tas med i URL:en. Värdet för `true` löser parametrar, och `false` inte.

##### Returnerar {#returns-getserviceurl}

A `string` värde som representerar tjänst-URL:en.

#### init(name, config) {#init-name-config-1}

initierar `ContextHub.Store.JSONPStore` -objekt.

##### Parametrar {#parameters-init-1}

* **`name`:** (String) Butikens namn.
* **`config`:** (Objekt) Ett objekt som innehåller egenskapen service. JSONPStore-objektet använder egenskaperna för `service` objekt för att skapa URL:en för JSONP-tjänsten:
   * `eventDeferring`: 32.
   * `eventing`: ContextHub.Utils.Eventing-objektet för det här arkivet. Standardvärdet är `ContextHub.eventing` -objekt.
   * `persistence`: ContextHub.Utils.Persistence-objektet för det här arkivet. Som standard används minnesbeständighet (JavaScript-objekt).
   * `service`: (Object)
      * `host`: (String) Servernamnet eller IP-adressen.
      * `jsonp`: (Boolean) Värdet true anger att tjänsten är en JSONP-tjänst, i annat fall false. När true är `{callback: "ContextHub.Callbacks.*Object.name*}`objekt läggs till i `service.params`.
      * `params`: (Object) URL-parametrar representeras som objektegenskaper. Parameternamn och värden är objektegenskapsnamnen och -värdena.
      * `path`: (String) Sökvägen till tjänsten.
      * `port`: (Number) Tjänstens portnummer.
      * `secure`: (String eller Boolean) Anger vilket protokoll som ska användas för tjänstens URL:
         * `auto`: //
         * `true`: https://
         * `false`: http://
      * `timeout`: (Number) Den väntetid i millisekunder som JSONP-tjänsten ska svara före timeout.
         * `ttl`: Den kortaste tiden i millisekunder som går mellan anrop till JSONP-tjänsten. (Se [queryService](#queryservice-reload) funktion).

#### queryService(reload) {#queryservice-reload}

Frågar fjärrtjänsten JSONP och cachelagrar svaret. Om tiden sedan föregående anrop till den här funktionen är mindre än värdet för `config.service.ttl`, anropas inte tjänsten och det cachelagrade svaret ändras inte. Du kan också tvinga tjänsten att anropas. The `config.service.ttl`egenskapen anges när anropet av [init](#init-name-config) funktion för att initiera arkivet.

Startar ready-händelsen när frågan är klar. Om JSONP-tjänstens URL inte är inställd händer ingenting.

##### Parametrar {#parameters-queryservice}

* **`reload`:** (Boolean) Värdet true tar bort det cachelagrade svaret och tvingar JSONP-tjänsten att anropas.

#### återställ {#reset}

Återställer de ursprungliga värdena för butikens beständiga data och anropar sedan JSONP-tjänsten. Du kan också ta bort alla andra data från arkivet. Händelser pausas för det här arkivet medan de ursprungliga värdena återställs. Den här funktionen returnerar inget värde.

Initialvärden anges i egenskapen initialValues för det config-objekt som används för att instansiera lagringsobjektet.

##### Parametrar {#parameters-reset-1}

* **`keepRemainingData`:** (Boolean) Värdet true gör att icke-initiala data bevaras. Värdet false medför att alla data tas bort utom de ursprungliga värdena.

#### resolveParameter(f) {#resolveparameter-f}

Matchar den angivna parametern.

## ContextHub.Store.PersistedJSONPStore {#contexthub-store-persistedjsonpstore}

`ContextHub.Store.PersistedJSONPStore` extends [ContextHub.Store.JSONPStore](#contexthub-store-jsonpstore) så den ärver alla funktioner i den klassen. Data som hämtas från JSONP-tjänsten sparas dock enligt konfigurationen för ContextHub-beständighet. (Se [Persistenslägen:](adding-contexthub.md#persistence-modes))

## ContextHub.Store.PersistedStore {#contexthub-store-persistedstore}

`ContextHub.Store.PersistedStore` extends [ContextHub.Store.Core](#contexthub-store-core) så den ärver alla funktioner i den klassen. Data i det här arkivet bevaras enligt konfigurationen för ContextHub-beständighet.

## ContextHub.Store.SessionStore {#contexthub-store-sessionstore}

`ContextHub.Store.SessionStore` extends [ContextHub.Store.Core](#contexthub-store-core) så den ärver alla funktioner i den klassen. Data i det här arkivet bevaras med hjälp av en minnesbeständig (JavaScript-objekt).

## ContextHub.UI {#contexthub-ui}

Hanterar gränssnittsmoduler och gränssnittsmodulrenderare.

### Funktioner (ContextHub.UI) {#functions-contexthub-ui}

#### registerRenderer(moduleType, renderer, dontRender) {#registerrenderer-moduletype-renderer-dontrender}

Registrerar en gränssnittsmodulrenderare med ContextHub. När återgivaren har registrerats kan den användas för att [skapa gränssnittsmoduler](configuring-contexthub.md#adding-a-ui-module). Använd den här funktionen när du är [utöka `ContextHub.UI.BaseModuleRenderer`](extending-contexthub.md#creating-contexthub-ui-module-types) för att skapa en anpassad renderare för användargränssnittsmodul.

##### Parametrar {#parameters-registerrenderer}

* **`moduleType`:** (String) Identifieraren för gränssnittsmodulens renderare. Om en renderare redan är registrerad med det angivna värdet avregistreras den befintliga renderaren innan den registreras.
* **`renderer`:** (String) Namnet på den klass som återger gränssnittsmodulen.
* **`dontRender`:** (Boolean) Ange som `true` för att förhindra att ContextHub-gränssnittet återges efter att återgivaren har registrerats. Standardvärdet är `false`.

##### Exempel {#example-registerrenderer}

I följande exempel registreras en renderare som `contexthub.browserinfo` modultyp.

```javascript
ContextHub.UI.registerRenderer('contexthub.browserinfo', new SurferinfoRenderer());
```

## ContextHub.Utils.Cookie {#contexthub-utils-cookie}

En verktygsklass för interaktion med cookies.

### Funktioner (ContextHub.Utils.Cookie) {#functions-contexthub-utils-cookie}

#### exists(key) {#exists-key}

Avgör om det finns en cookie.

##### Parametrar {#parameters-exists}

* **`key`:** A `String` som innehåller nyckeln till den cookie som du testar för.

##### Returnerar {#returns-exists}

A `boolean` värdet true anger att cookien finns.

##### Exempel {#example-exists}

```javascript
if (ContextHub.Utils.Cookie.exists("name")) {
   // conditionally-executed code
}
```

#### getAllItems(filter) {#getallitems-filter}

Returnerar alla cookies som har nycklar som matchar ett filter.

##### Parametrar {#parameters-getallitems}

* **`filter`:** (Valfritt) Kriterier för att matcha cookie-nycklar. Om du vill returnera alla cookies anger du inget värde. Följande typer stöds:
   * Sträng: Strängen jämförs med cookie-nyckeln.
   * Array: Varje objekt i arrayen är ett filter.
   * Ett RegExp-objekt: Objektets testfunktion används för att matcha cookie-nycklar.
   * En funktion: En funktion som testar en cookie-nyckel för en matchning. Funktionen måste ta cookie-nyckeln som en parameter och returnera true om testet bekräftar en matchning.

##### Returnerar {#returns-getallitems}

Ett objekt med cookies. Objektegenskaper är cookie-nycklar och nyckelvärden är cookie-värden.

##### Exempel {#example-getallitems}

```javascript
ContextHub.Utils.Cookie.getAllItems([/^cq-authoring/, /^cq-editor/])
```

#### getItem(key) {#getitem-key-1}

Returnerar ett cookie-värde.

##### Parametrar {#parameters-getitem-1}

* **`key`:** Nyckeln till den cookie som du vill ha värdet för.

##### Returnerar {#returns-getitem-1}

cookie-värdet, eller `null` om ingen cookie hittades för nyckeln.

##### Exempel {#example-getitem-1}

```javascript
ContextHub.Utils.Cookie.getItem("name");
```

#### getKeys(filter) {#getkeys-filter}

Returnerar en array med nycklarna för befintliga cookies som matchar ett filter.

##### Parametrar {#parameters-getkeys-1}

* **`filter`:** Kriterier för matchning av cookie-nycklar. Följande typer stöds:
   * Sträng: Strängen jämförs med cookie-nyckeln.
   * Array: Varje objekt i arrayen är ett filter.
   * Ett RegExp-objekt: Objektets testfunktion används för att matcha cookie-nycklar.
   * En funktion: En funktion som testar en cookie-nyckel för en matchning. Funktionen måste ta cookie-nyckeln som parameter och returnera `true` om testet bekräftar en matchning.

##### Returnerar {#returns-getkeys-1}

En array med strängar där varje sträng är nyckeln till en cookie som matchar filtret.

##### Exempel {#example-getkeys-1}

```javascript
ContextHub.Utils.Cookie.getKeys([/^cq-authoring/, /^cq-editor/])
```

#### removeItem(key, options) {#removeitem-key-options-1}

Tar bort en cookie. Om du vill ta bort cookien anges värdet till en tom sträng och förfallodatumet anges till dagen före det aktuella datumet.

##### Parametrar {#parameters-removeitem-1}

* **`key`:** A `String` värdet som representerar nyckeln till den cookie som ska tas bort.
* **`options`:** Ett objekt som innehåller egenskapsvärden för konfiguration av cookie-attributen. Se [`setItem`](#setitem-key-value-options) funktion för information. The `expires` -egenskapen har ingen effekt.

##### Returnerar {#returns-removeitem-1}

Den här funktionen returnerar inget värde.

##### Exempel {#example-removeitem-1}

```javascript
ContextHub.Utils.Cookie.vanish([/^cq-authoring/, 'cq-scrollpos']);
```

#### setItem(key, value, options) {#setitem-key-value-options-1}

Skapar en cookie med den angivna nyckeln och det angivna värdet och lägger till cookien i det aktuella dokumentet. Du kan också ange alternativ som konfigurerar attributen för cookien.

##### Parametrar {#parameters-setitem-1}

* **`key`:** En sträng som innehåller nyckeln till cookien.
* **`value`:** En sträng som innehåller cookie-värdet.
* **`options`:** (Valfritt) Ett objekt som innehåller någon av följande egenskaper som konfigurerar cookie-attributen:
   * `expires`: A `date` eller `number` värdet som anger när cookien förfaller. Ett datumvärde anger den absoluta förfallotiden. Ett tal (i dagar) anger förfallotiden till den aktuella tiden plus talet. Standardvärdet är `undefined`.
   * `secure`: A `boolean` värde som anger `Secure` cookie-attributet. Standardvärdet är `false`.
   * `path`: A `String` värde som ska användas som `Path` cookie-attributet. Standardvärdet är `undefined`.

##### Returnerar {#returns-setitem-1}

Cookien med det angivna värdet.

##### Exempel {#example-setitem-1}

```javascript
ContextHub.Utils.Cookie.setItem("name", "mycookie", {
    expires: 3,
    domain: 'localhost',
    path: '/some/directory',
    secure: true
});
```

#### vDanish(filter, options) {#vanish-filter-options}

Tar bort alla cookies som matchar ett visst filter. Cookies matchas med `getKeys` och tas bort med `removeItem` funktion.

##### Parametrar {#parameters-vanish}

* **`filter`:** The `filter` argument som ska användas i anropet till [`getKeys`](#getkeys-filter) funktion.
* **`options`:** The `options` argument som ska användas i anropet till [`removeItem`](#removeitem-key-options) funktion.

##### Returnerar {#returns-vanish}

Den här funktionen returnerar inget värde.

## ContextHub.Utils.Eventing {#contexthub-utils-eventing}

Gör att du kan binda och koppla upp funktioner till ContextHub-butikshändelser. Åtkomst `ContextHub.Utils.Eventing` objekt för en butik med [eventera](#eventing) butikens egenskap.

### Funktioner (ContextHub.Utils.Eventing) {#functions-contexthub-utils-eventing}

#### off(name, selector) {#off-name-selector}

Avbinder en funktion från en händelse.

##### Parametrar {#parameters-off}

* **`name`:** The [händelsens namn](#contexthub-utils-eventing) som du avbinder funktionen för.
* **`selector`:** Väljaren som identifierar bindningen. (Se `selector` -parametern för [`on`](#on-name-handler-selector-triggerforpastevents) och [`once`](#once-name-handler-selector-triggerforpastevents) funktioner).

##### Returnerar {#returns-off}

Den här funktionen returnerar inget värde.

#### on(name, handler, selector, triggerForPastEvents) {#on-name-handler-selector-triggerforpastevents}

Bindar en funktion till en händelse. Funktionen anropas varje gång händelsen inträffar. Funktionen kan också anropas för händelser som har inträffat tidigare, innan bindningen har upprättats.

##### Parametrar {#parameters-on}

* **`name`:** (String) [händelsens namn](#contexthub-utils-eventing) som du binder funktionen till.
* **`handler`:** (Funktion) Funktionen som ska bindas till händelsen.
* **`selector`:** (String) En unik identifierare för bindningen. Du behöver väljaren för att identifiera bindningen om du vill använda `off` funktionen för att ta bort bindningen.
* **`triggerForPastEvents`:** (Boolean) Anger om hanteraren ska köras för händelser som har inträffat tidigare. Värdet för `true` anropar hanteraren för tidigare händelser. Värdet för `false` anropar hanteraren för framtida händelser. Standardvärdet är `true`.

##### Returnerar {#returns-on}

När `triggerForPastEvents` argument `true`returnerar den här funktionen en `boolean` värde som anger om händelsen har inträffat tidigare:

* `true`: Händelsen inträffade tidigare och hanteraren anropas.
* `false`: Händelsen har inte inträffat tidigare.

If `triggerForPastEvents` är `false`returnerar den här funktionen inget värde.

##### Exempel {#example-on}

I följande exempel binds en funktion till händelsen data i geolocation-arkivet. Funktionen fyller i ett element på sidan med värdet för latituddataobjektet från butiken.

```html
<div class="location">
    <p>latitude: <span id="lat"></span></p>
</div>

<script>
    var geostore = ContextHub.getStore("geolocation");
    geostore.eventing.on(ContextHub.Constants.EVENT_DATA_UPDATE,getlat,"getlat");

    function getlat(){
       latitude = geostore.getItem("latitude");
       $("#lat").html(latitude);
    }
</script>
```

#### once(name, handler, selector, triggerForPastEvents) {#once-name-handler-selector-triggerforpastevents}

Bindar en funktion till en händelse. Funktionen anropas bara en gång för den första förekomsten av händelsen. Funktionen kan också anropas för den händelse som har inträffat tidigare, innan bindningen har upprättats.

##### Parametrar {#parameters-once}

* **`name`:** (String) [händelsens namn](#contexthub-utils-eventing) som du binder funktionen till.
* **`handler`:** (Funktion) Funktionen som ska bindas till händelsen.
* **`selector`:** (String) En unik identifierare för bindningen. Du behöver väljaren för att identifiera bindningen om du vill använda `off` funktionen för att ta bort bindningen.
* **`triggerForPastEvents`:** (Boolean) Anger om hanteraren ska köras för händelser som har inträffat tidigare. Värdet för `true` anropar hanteraren för tidigare händelser. Värdet för `false` anropar hanteraren för framtida händelser. Standardvärdet är `true`.

##### Returnerar {#returns-once}

När `triggerForPastEvents` argument `true`returnerar den här funktionen en `boolean` värde som anger om händelsen har inträffat tidigare:

* `true`: Händelsen inträffade tidigare och hanteraren anropas.
* `false`: Händelsen har inte inträffat tidigare.

If `triggerForPastEvents` är `false`returnerar den här funktionen inget värde.

## ContextHub.Utils.inheritance {#contexthub-utils-inheritance}

En verktygsklass som gör att ett objekt kan ärva egenskaper och metoder för ett annat objekt.

### Funktioner (ContextHub.Utils.arv) {#functions-contexthub-utils-inheritance}

#### inherit(child, parent) {#inherit-child-parent}

Gör att ett objekt ärver egenskaper och metoder för ett annat objekt.

##### Parametrar {#parameters-inherit}

* **`child`:** (Objekt) Det objekt som ärver.
* **`parent`:** (Object) Det objekt som definierar de egenskaper och metoder som ärvs.

## ContextHub.Utils.JSON {#contexthub-utils-json}

Tillhandahåller funktioner för att serialisera objekt till JSON-format och deserialisera JSON-strängar till objekt.

### Funktioner (ContextHub.Utils.JSON) {#functions-contexthub-utils-json}

#### parse(data) {#parse-data}

Tolkar ett strängvärde som JSON och konverterar det till ett javascript-objekt.

##### Parametrar {#parameters-parse}

* **`data`:** Ett strängvärde i JSON-format.

##### Returnerar {#returns-parse}

Ett JavaScript-objekt.

##### Exempel {#example-parse}

Koden:

```javascript
ContextHub.Utils.JSON.parse("{'city':'Basel','country':'Switzerland','population':'173330'}");
```

Returnerar följande objekt:

```javascript
Object {
   city: "Basel",
   country: "Switzerland",
   population: 173330
}
```

#### stringify(data) {#stringify-data}

Serialiserar JavaScript-värden och -objekt till strängvärden i JSON-format.

##### Parametrar {#parameters-stringify}

* **`data`:** Värdet eller objektet som ska serialiseras. Den här funktionen stöder värden för booleskt värde, matris, tal, sträng och datum.

##### Returnerar {#returns-stringify}

Det serialiserade strängvärdet. När `data` är ett R `egExp` returnerar funktionen ett tomt objekt. När `data` är en funktion, returnerar `undefined`.

##### Exempel {#example-stringify}

Följande kod:

```javascript
ContextHub.Utils.JSON.stringify({
   city: "Basel",
   country: "Switzerland",
   population: 173330
});
```

Returnerar:

```javascript
"{'city':'Basel','country':'Switzerland','population':'173330'}":
```

## ContextHub.Utils.JSON.tree {#contexthub-utils-json-tree}

Den här klassen underlättar manipuleringen av dataobjekt som ska lagras eller hämtas från ContextHub-arkiv.

### Funktioner (ContextHub.Utils.JSON.tree) {#functions-contexthub-utils-json-tree}

#### addAllItems() {#addallitems}

Skapar en kopia av ett dataobjekt och lägger till dataträdet från ett andra objekt. Funktionen returnerar kopian och ändrar inte något av de ursprungliga objekten. När dataträden för de två objekten innehåller identiska nycklar skriver värdet för det andra objektet över värdet för det första objektet.

##### Parametrar {#parameters-addallitems-1}

* **`tree`:** Det objekt som kopieras.
* **`secondTree`:** Det objekt som sammanfogas med kopian av `tree` -objekt.

##### Returnerar {#returns-addallitems-1}

Ett objekt som innehåller sammanfogade data.

#### cleanup() {#cleanup}

Skapar en kopia av ett objekt, söker efter och tar bort objekt i dataträdet som inte innehåller några värden, null-värden eller odefinierade värden och returnerar kopian.

##### Parametrar {#parameters-cleanup}

* **`tree`:** Det objekt som ska rensas.

##### Returnerar {#returns-cleanup}

En kopia av trädet som är städat.

#### getItem() {#getitem}

Hämtar värdet från ett objekt för nyckeln.

##### Parametrar {#parameters-getitem-2}

* **`tree`:** Dataobjektet.
* **`key`:** Nyckeln för värdet som du vill hämta.

##### Returnerar {#returns-getitem-2}

Värdet som motsvarar tangenten. När nyckeln har underordnade nycklar returnerar den här funktionen ett komplext objekt. När värdetypen för nyckeln är `undefined`, `null` returneras.

##### Exempel {#example-getitem-2}

Titta på följande JavaScript-objekt:

```javascript
myObject {
  user: {
    location: {
      city: "Basel",
        details: {
          population: 173330,
          elevation: 260
        }
      }
    }
  }
```

Följande exempelkod returnerar värdet `260`:

```javascript
ContextHub.Utils.JSON.tree.getItem(myObject, "/user/location/details/elevation");
```

Följande exempelkod hämtar värdet för en nyckel som har underordnade nycklar:

```javascript
ContextHub.Utils.JSON.tree.getItem(myObject, "/user");
```

Funktionen returnerar följande objekt:

```javascript
Object {
  location: {
    city: "Basel",
    details: {
      population: 173330,
      elevation: 260
    }
  }
}
```

#### getKeys() {#getkeys}

Hämtar alla nycklar från ett objekts dataträd. Om du vill kan du bara hämta nycklarna för de underordnade nycklarna för en viss nyckel. Du kan också ange en sorteringsordning för de hämtade nycklarna.

##### Parametrar {#parameters-getkeys-2}

* **`tree`:** Det objekt som nycklarna för dataträdet ska hämtas från.
* **`parent`:** (Valfritt) Nyckeln till ett objekt i dataträdet som du vill hämta nycklarna för de underordnade objekten för.
* **`order`:** (Valfritt) En funktion som bestämmer sorteringsordningen för de returnerade tangenterna. (Se [`Array.prototype.sort`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort) på Mozilla Developer Network.)

##### Returnerar {#returns-getkeys-2}

En array med nycklar.

##### Exempel {#example-getkeys-2}

Tänk på följande objekt:

```javascript
myObject {
  location: {
    weather: {
      temperature: "28C",
      humidity: "77%",
      precipitation: "10%",
      wind: "8km/h"
    },
    city: "Basel",
    country: "Switzerland",
    longitude: 7.5925727,
    latitude: 47.557421
  }
}
```

The `ContextHub.Utils.JSON.tree.getKeys(myObject);` skriptet returnerar följande array:

```javascript
["/location", "/location/city", "/location/country", "/location/latitude", "/location/longitude", "/location/weather", "/location/weather/humidity", "/location/weather/precipitation", "/location/weather/temperature", "/location/weather/wind"]
```

#### removeItem() {#removeitem}

Skapar en kopia av ett givet objekt, tar bort den angivna grenen från dataträdet och returnerar den ändrade kopian.

##### Parametrar {#parameters-removeitem-2}

* **`tree`:** Ett dataobjekt.
* **`key`:** Nyckeln som ska tas bort.

##### Returnerar {#returns-removeitem-2}

En kopia av det ursprungliga dataobjektet där tangenten har tagits bort.

##### Exempel {#example-removeitem-2}

Tänk på följande objekt:

```javascript
myObject {
  one: {
    foo: "bar",
    two: {
      three: {
        four: {
          five: 5,
          six: 6
        }
      }
    }
  }
}
```

Följande exempelskript tar bort grenen /en/två/tre/fyra från dataträdet:

```javascript
myObject = ContextHub.Utils.JSON.tree.removeItem(myObject, "/one/two/three/four");
```

Funktionen returnerar följande objekt:

```javascript
myObject {
  one: {
    foo: "bar"
  }
}
```

#### sanitizeKey(key) {#sanitizekey-key}

Ändrar strängvärden så att de kan användas som nycklar. Om du vill sanera en sträng utför den här funktionen följande åtgärder:

* Minskar flera efterföljande snedstreck till ett enda snedstreck.
* Tar bort mellanrum från början och slutet av strängen.
* Delar upp resultatet i en array med strängar som avgränsas av snedstreck.

Använd den resulterande arrayen för att skapa en användbar nyckel.

##### Parametrar {#parameters-sanitizekey}

* **`key`:** The `string` för att sanera.

##### Returnerar {#returns-sanitizekey}

En array med `string` värden där varje sträng är den del av `key` som avgränsades av snedstreck. representerar den sanerade nyckeln. Om den sanerade arrayen har längden noll returneras den här funktionen `null`.

##### Exempel {#example-sanitizekey}

Följande kod sanerar en sträng för att skapa arrayen `["this", "is", "a", "path"]`och sedan genererar nyckeln `"/this/is/a/path"` från matrisen:

```javascript
var key = " / this////is/a/path ";
ContextHub.Utils.JSON.tree.sanitizeKey(key)
"/" + ContextHub.Utils.JSON.tree.sanitizeKey(key).join("/");
```

#### setItem(tree, key, value) {#setitem-tree-key-value}

Lägger till ett nyckel/värde-par i dataträdet för en kopia av ett objekt. Mer information om dataträd finns i [Persistens.](contexthub.md#persistence)

##### Parametrar {#parameters-setitem-2}

* **`tree`:** Ett dataobjekt.
* **`key`:** Den tangent som ska kopplas till värdet som du lägger till. Nyckeln är sökvägen till objektet i dataträdet. Detta funktionsanrop `ContextHub.Utils.JSON.tree.sanitize` om du vill rensa nyckeln innan du lägger till den.
* **`value`:** Värdet som ska läggas till i dataträdet.

##### Returnerar {#returns-setitem-2}

En kopia av `tree` objekt som innehåller `key`/ `value` par.

##### Exempel {#example-setitem-2}

Tänk på följande JavaScript-kod:

```javascript
var myObject = {
     user: {
        location: {
           city: "Basel"
           }
        }
     };

var myKey = "/user/location/details";

var myValue = {
      population: 173330,
      elevation: 260
     };

myObject = ContextHub.Utils.JSON.tree.setItem(myObject, myKey, myValue);
```

## ContextHub.Utils.storeCandidates {#contexthub-utils-storecandidates}

Här kan du registrera butikskandidater och få registrerade butikskandidater.

### Funktioner (ContextHub.Utils.storeCandidates) {#functions-contexthub-utils-storecandidates}

#### getRegisteredCandidates(storeType) {#getregisteredcandidates-storetype}

Returnerar de butikstyper som är registrerade som butikskandidater. Hämta antingen registrerade anbudssökande för en viss butikstyp eller alla butikstyper.

##### Parametrar {#parameters-getregisteredcandidates}

* **`storeType`:** (String) Namnet på lagringstypen. Se `storeType` parametern för [`ContextHub.Utils.storeCandidates.registerStoreCandidate`](#contexthub-utils-storecandidates) funktion.

##### Returnerar {#returns-getregisteredcandidates}

Ett objekt av lagringstyper. Objektegenskaperna är lagringstypsnamnen och egenskapsvärdena är en array med registrerade lagringskandidater.

#### getStoreFromCandidates(storeType) {#getstorefromcandidates-storetype}

Returnerar en butikstyp från de registrerade anbudssökande. Om fler än en lagringstyp med samma namn är registrerad returnerar funktionen den lagringstyp som har högst prioritet.

##### Parametrar {#parameters-getstorefromcandidates}

* `storeType`: (String) Namnet på lagringskandidaten. Se `storeType` parametern för [`ContextHub.Utils.storeCandidates.registerStoreCandidate`](#registerstorecandidate-store-storetype-priority-applies) funktion.

##### Returnerar {#returns-getstorefromcandidates}

Ett objekt som representerar den registrerade butikskandidaten. Om den begärda lagringstypen inte har registrerats genereras ett fel.

#### getSupportedStoreTypes() {#getsupportedstoretypes}

Returnerar namnen på de butikstyper som är registrerade som butikskandidater. Den här funktionen kräver inga parametrar.

##### Returnerar {#returns-getsupportedstoretypes}

En array med strängvärden, där varje sträng är den storetype som en lagringskandidat registrerades med. Se `storeType` parametern för [`ContextHub.Utils.storeCandidates.registerStoreCandidate`](#contexthub-utils-storecandidates) funktion.

#### registerStoreCandidate(store, storeType, priority, apply) {#registerstorecandidate-store-storetype-priority-applies}

Registrerar ett lagringsobjekt som ett arkivkandidat med ett namn och en prioritet.

Prioriteten är ett tal som anger vikten av butiker med samma namn. När en butikskandidat registreras med samma namn som en redan registrerad butikskandidat, används den som har den högre prioriteten. När du registrerar en butikskandidater registreras butiken endast om prioriteten är högre än de registrerade butikskandidaterna med samma namn.

##### Parametrar {#parameters-registerstorecandidate}

* **`store`:** (Objekt) Det lagringsobjekt som ska registreras som lagringskandidater.
* **`storeType`:** (String) Namnet på lagringskandidaten. Detta värde krävs när en instans av lagringskandidaten skapas.
* **`priority`:** (Number) Prioriteten för butikskandidaten.
* **`applies`:** (Funktion) Funktionen som ska anropas som utvärderar butikens tillämplighet i den aktuella miljön. Funktionen måste returnera `true` om butiken är tillämplig, och `false` annars. Standardvärdet är en funktion som returnerar true: `function() {return true;}`

##### Exempel {#example-registerstorecandidate}

```javascript
ContextHub.Utils.storeCandidates.registerStoreCandidate(myStoreCandidate,
                                'contexthub.mystorecandiate', 0);
```

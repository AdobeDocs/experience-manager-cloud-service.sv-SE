---
title: ContextHub Javascript API-referens
description: ContextHub Javascript-API:t är tillgängligt för skript när ContextHub-komponenten har lagts till på sidan
translation-type: tm+mt
source-git-commit: e361f24b943eff68982a37ac0dc2597f92450026
workflow-type: tm+mt
source-wordcount: '4621'
ht-degree: 3%

---


# ContextHub Javascript API-referens {#contexthub-javascript-api-reference}

ContextHub Javascript-API:t är tillgängligt för dina skript när [ContextHub-komponenten har lagts till på sidan](configuring-contexthub.md#adding-contexthub-to-a-page-component).

## ContextHub-konstanter {#contexthub-constants}

Konstantvärden som definieras av ContextHub Javascript-API:t.

### Händelsekonstanter {#event-constants}

I följande tabell visas namnen på händelser som inträffar för ContextHub Stores. Se även [ContextHub.Utils.Eventing](contexthub-api.md#contexthub-utils-eventing).

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
| `ContextHub.Constants.EVENT_UI_RENDERED` | Utlöses varje gång ContextHub-gränssnittet återges (t.ex. efter en egenskapsändring) | `ui-rendered` |
| `ContextHub.Constants.EVENT_UI_INITIALIZED` | Utlöses när gränssnittsbehållaren initieras | `ui-initialized` |
| `ContextHub.Constants.ACTIVE_UI_MODE` | Anger aktivt användargränssnittsläge | `/_/active-ui-mode` |

## ContextHub Javascript API-referens {#contexthub-javascript-api-reference-2}

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

Representerar ett ContextHub-segment. Använd för `ContextHub.SegmentEngine.SegmentManager` att hämta segment.

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

Ett [`ContextHub.Utils.Eventing`](#contexthub-utils-eventing) objekt. Använd det här objektet för bindningsfunktioner för att lagra händelser. Mer information om standardvärde och initiering finns i [`init(name,config)`](#init-name-config).

#### name {#name}

Butikens namn.

#### beständighet {#persistence}

Ett `ContextHub.Utils.Persistence` objekt. Mer information om standardvärde och initiering finns i [`init(name,config)`](#init-name-config).

### Funktioner (ContextHub.Store.Core) {#functions-contexthub-store-core}

#### addAllItems(träd, alternativ) {#addallitems-tree-options}

Sammanfogar ett dataobjekt eller en array med lagringsdata. Varje nyckel/värde-par i objektet eller arrayen läggs till i arkivet (via `setItem` funktionen):

* **Objekt:** Tangenter är egenskapsnamnen.
* **Array:** Tangenter är matrisindex.

Observera att värden kan vara objekt.

##### Parametrar {#parameters-addallitems}

* **`tree`:** (Objekt eller array) De data som ska läggas till i arkivet.
* **`options`:** (Object) Ett valfritt objekt med alternativ som skickas till funktionen setItem. Mer information finns i parametern `options` för [`setItem(key,value,options)`](#setitem-key-value-options).

##### Returnerar {#returns-addallitems}

Ett `boolean` värde:

* Värdet `true` anger att dataobjektet har lagrats.
* Värdet `false` anger att datalagret inte ändras.

#### addReference(key, anotherKey) {#addreference-key-anotherkey}

Skapar en referens från en tangent till en annan. En nyckel kan inte referera till sig själv.

##### Parametrar {#parameters-addreference}

* **`key`:** Nyckeln som refererar `anotherKey`.

* **`anotherkey`:** Nyckeln som refereras av `key`.

##### Returnerar {#returns-addreference}

Ett `boolean` värde:

* Värdet `true` anger att referensen har lagts till.
* Värdet `false` anger att ingen referens har lagts till.

#### announReadiness() {#announcereadiness}

Startar `ready` händelsen för den här butiken. Den här funktionen har inga parametrar och returnerar inget värde.

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

* **`includeInternals`:** Värdet `true` inkluderar internt använda nycklar i resultatet. Dessa tangenter börjar med understrecket (`_`). Standardvärdet är `false`.

##### Returnerar {#returns-getkeys}

En array med nyckelnamn ( `string` värden).

#### getReferences() {#getreferences}

Hämtar referenserna från butiken.

##### Returnerar {#returns-getreferences}

En array som använder refererande nycklar som index för refererade nycklar:

* Referensnycklar motsvarar `key` parametern för `addReference` funktionen.
* Refererade nycklar motsvarar `anotherKey` funktionens parameter `addReference` .

#### getTree(includeInternals) {#gettree-includeinternals}

Hämtar dataträdet från butiken. Du kan också inkludera nyckel/värde-par som används internt av ContextHub-ramverket.

##### Parametrar {#parameters-gettree}

* `includeInternals:` Värdet `true` inkluderar nyckelvärdepar som används internt i resultatet. Nycklarna för dessa data börjar med understrecket (`_`). Standardvärdet är `false`.

##### Returnerar {#returns-gettree}

Ett objekt som representerar dataträdet. Nycklarna är objektets egenskapsnamn.

#### init(name, config) {#init-name-config}

Initierar butiken.

* Ställer in lagringsdata till ett tomt objekt.
* Ställer in butiksreferenserna till ett tomt objekt.
* Det `eventChannel` är `data:<name>`, där `<name>` är butiksnamnet.
* Det `storeDataKey` är `/store/<name>`, där `<name>` är butiksnamnet.

##### Parametrar {#parameters-init}

* **`name`:** Butikens namn.
* **`config`:** Ett objekt som innehåller konfigurationsegenskaper:
   * `eventDeferring`: Standardvärdet är 32.
   * `eventing`: Objektet [ContextHub.Utils.Eventing](#contexthub-utils-eventing) för det här arkivet. Standardvärdet är det objekt som `ContextHub.eventing` används.
   * `persistence`: Objektet `ContextHub.Utils.Persistence` för den här butiken. Standardvärdet är `ContextHub.persistence` objektet.

#### isEventingPaused() {#iseventingpaused}

Avgör om händelser pausas för det här arkivet.

##### Returnerar {#returns-iseventingpaused}

Ett booleskt värde:

* `true`: Händelsen pausas så att inga händelser aktiveras för den här butiken.
* `false`: Händelsen pausas inte så att händelser aktiveras för den här butiken.

#### pauseEventing() {#pauseeventing}

Pausar händelser för arkivet så att inga händelser utlöses. Den här funktionen kräver inga parametrar och returnerar inget värde.

#### removeItem(key, options) {#removeitem-key-options}

Tar bort ett nyckel/värde-par från arkivet.

När en tangent tas bort utlöser funktionen `data` händelsen. Händelsedata innehåller arkivnamnet, namnet på den nyckel som togs bort, det värde som togs bort, det nya värdet för nyckeln (null) och åtgärdstypen &quot;remove&quot;.

Du kan även förhindra att `data` händelsen utlöses.

##### Parametrar {#parameters-removeitem}

* **`key`:** (String) Namnet på nyckeln som ska tas bort.
* **`options`:** (Objekt) Ett objekt med alternativ. Följande objektegenskaper är giltiga:
   * tyst: Värdet `true` förhindrar att `data` händelsen utlöses. Standardvärdet är `false`.

##### Returnerar {#returns-removeitem}

Ett `boolean` värde:

* Värdet `true` anger att nyckel/värde-paret har tagits bort.
* Värdet `false` anger att datalagret inte ändras eftersom nyckeln inte hittades i arkivet.

#### removeReference(key) {#removereference-key}

Tar bort en referens från arkivet.

##### Parametrar {#parameters-removereference}

* **`key`:** Nyckelreferensen som ska tas bort. Den här parametern motsvarar parametern `key` för `addReference` funktionen.

##### Returnerar {#returns-removereference}

Ett `boolean` värde:

* Värdet `true` anger att referensen har tagits bort.
* Värdet `false` anger att nyckeln inte var giltig och att arkivet inte är det.

#### reset(keepRemainingData) {#reset-keepremainingdata}

Återställer de ursprungliga värdena för butikens beständiga data. Du kan också ta bort alla andra data från arkivet. Händelser pausas för det här arkivet när arkivet återställs. Den här funktionen returnerar inget värde.

Startvärden anges i egenskapen `initialValues` för det config-objekt som används för att instansiera lagringsobjektet.

##### Parametrar {#parameters-reset}

* **`keepRemainingData`**: (Boolean) Värdet true gör att icke-initiala data bevaras. Värdet false medför att alla data tas bort utom de ursprungliga värdena.

#### resolveReference(key, retry) {#resolvereference-key-retry}

Hämtar en refererad nyckel. Du kan också ange antalet iterationer som ska användas för att matcha den bästa matchningen.

##### Parametrar {#parameters-resolvereference}

* **`key`:** (String) Nyckeln som referensen ska matchas för. Den här `key` parametern motsvarar `key` funktionens `addReference` parameter.
* **`retry`:** (Number) Antalet iterationer som ska användas.

##### Returnerar {#returns-resolvereference}

Ett `string` värde som representerar den refererade nyckeln. Om ingen referens är löst returneras värdet för `key` parametern.

#### resumeEventing() {#resumeeventing}

Återupptar händelser för den här butiken så att händelser utlöses. Den här funktionen definierar inga parametrar och returnerar inget värde.

#### setItem(key, value, options) {#setitem-key-value-options}

Lägger till ett nyckel/värde-par i butiken.

Startar bara `data` händelsen om värdet för nyckeln skiljer sig från värdet som för närvarande lagras för nyckeln. Du kan också förhindra att `data` händelsen utlöses.

Händelsedata innehåller butiksnamnet, nyckeln, det föregående värdet, det nya värdet och åtgärdstypen för `set`.

##### Parametrar {#parameters-setitem}

* **`key`:** (String) Namnet på nyckeln.
* **`options`:** (Objekt) Ett objekt med alternativ. Följande objektegenskaper är giltiga:
   * `silent`: Värdet `true` förhindrar att `data` händelsen utlöses. Standardvärdet är `false`.
* **`value`:** (Objekt) Värdet som ska associeras med nyckeln.

##### Returnerar {#returns-setitem}

Ett `boolean` värde:

* Värdet `true` anger att dataobjektet har lagrats.
* Värdet `false` anger att datalagret inte ändras.

## ContextHub.Store.JSONPStore {#contexthub-store-jsonpstore}

Ett arkiv som innehåller JSON-data. Data hämtas från en extern JSONP-tjänst, eller eventuellt från en tjänst som returnerar JSON-data. Ange tjänstinformationen med hjälp av [`init`](#init-name-config) funktionen när du skapar en instans av den här klassen.

Butiken använder beständighet i minnet (Javascript-variabel). Lagringsdata är bara tillgängliga under sidans livstid.

ContextHub.Store.JSONPStore utökar [ContextHub.Store.Core](#contexthub-store-core) och ärver den klassens funktioner.

### Funktioner (ContextHub.Store.JSONPStore) {#functions-contexthub-store-jsonpstore}

#### configureService(serviceConfig, override) {#configureservice-serviceconfig-override}

Konfigurerar informationen för anslutning till den JSONP-tjänst som det här objektet använder. Du kan antingen uppdatera eller ersätta den befintliga konfigurationen. Funktionen returnerar inget värde.

##### Parametrar {#parameters-configureservice}

* **`serviceConfig`:** Ett objekt som innehåller följande egenskaper:
   * `host`: (String) Servernamnet eller IP-adressen.
   * `jsonp`: (Boolean) Värdet true anger att tjänsten är en JSONP-tjänst, i annat fall false. När true är {callback: &quot;ContextHub.Callbacks.*Object.name*}-objektet läggs till i service.params-objektet.
   * `params`: (Objekt) URL-parametrar representeras som objektegenskaper. Parameternamn är egenskapsnamn och parametervärden är egenskapsvärden.
   * `path`: (String) Sökvägen till tjänsten.
   * `port`: (Nummer) Tjänstens portnummer.
   * `secure`: (Sträng eller Boolean) Anger vilket protokoll som ska användas för tjänstens URL:
      * `auto`: //
      * `true`: https://
      * `false`: http://
* **åsidosätt:** (Boolean). Värdet på `true` gör att den befintliga tjänstkonfigurationen ersätts av egenskaperna för `serviceConfig`. Värdet på `false` sammanfogar de befintliga tjänstkonfigurationsegenskaperna med egenskaperna för `serviceConfig`.

#### getRawResponse() {#getrawresponse}

Returnerar det obearbetade svar som har cachelagrats sedan det senaste anropet till JSONP-tjänsten. Funktionen kräver inga parametrar.

##### Returnerar {#returns-getrawresponse}

Ett objekt som representerar råsvaret.

#### getServiceDetails() {#getservicedetails}

Hämtar tjänstobjektet för det här ContextHub.Store.JSONPStore-objektet. Tjänsteobjektet innehåller all information som krävs för att skapa tjänstens URL.

##### Returnerar {#returns-getservicedetails}

Ett objekt med följande egenskaper:

* **`host`:** (String) Servernamnet eller IP-adressen.
* **`jsonp`:** (Boolean) Värdet true anger att tjänsten är en JSONP-tjänst, i annat fall false. När true är {callback: &quot;ContextHub.Callbacks.*Object.name*}-objektet läggs till i service.params-objektet.
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

* **`resolve`:** (Boolean) Avgör om lösta parametrar ska tas med i URL:en. Värdet `true` löser parametrarna och `false` gör det inte.

##### Returnerar {#returns-getserviceurl}

Ett `string` värde som representerar tjänst-URL:en.

#### init(name, config) {#init-name-config-1}

initierar `ContextHub.Store.JSONPStore` objektet.

##### Parametrar {#parameters-init-1}

* **`name`:** (String) Butikens namn.
* **`config`:** (Objekt) Ett objekt som innehåller egenskapen service. Objektet JSONPStore använder egenskaperna för `service` objektet för att skapa URL:en för JSONP-tjänsten:
   * `eventDeferring`: 32.
   * `eventing`: Objektet ContextHub.Utils.Eventing för det här arkivet. Standardvärdet är `ContextHub.eventing` objektet.
   * `persistence`: ContextHub.Utils.Persistence-objektet för det här arkivet. Som standard används minnesbeständighet (Javascript-objekt).
   * `service`: (Objekt)
      * `host`: (String) Servernamnet eller IP-adressen.
      * `jsonp`: (Boolean) Värdet true anger att tjänsten är en JSONP-tjänst, i annat fall false. När true läggs `{callback: "ContextHub.Callbacks.*Object.name*}`objektet till `service.params`.
      * `params`: (Objekt) URL-parametrar representeras som objektegenskaper. Parameternamn och värden är objektegenskapsnamnen och -värdena.
      * `path`: (String) Sökvägen till tjänsten.
      * `port`: (Nummer) Tjänstens portnummer.
      * `secure`: (Sträng eller Boolean) Anger vilket protokoll som ska användas för tjänstens URL:
         * `auto`: //
         * `true`: https://
         * `false`: http://
      * `timeout`: (Nummer) Hur lång tid det tar att vänta på att JSONP-tjänsten ska svara före timeout, i millisekunder.
         * `ttl`: Den kortaste tiden i millisekunder som går mellan anrop till JSONP-tjänsten. (Se [funktionen queryService](#queryservice-reload) .)

#### queryService(reload) {#queryservice-reload}

Frågar fjärrtjänsten JSONP och cachelagrar svaret. Om tiden sedan det föregående anropet till den här funktionen är mindre än värdet för `config.service.ttl`anropas inte tjänsten och det cachelagrade svaret ändras inte. Du kan också tvinga tjänsten att anropas. Egenskapen `config.service.ttl`anges när funktionen [init](#init-name-config) anropas för att initiera arkivet.

Startar ready-händelsen när frågan är klar. Om JSONP-tjänstens URL inte är inställd händer ingenting.

##### Parametrar {#parameters-queryservice}

* **`reload`:** (Boolean) Värdet true tar bort det cachelagrade svaret och tvingar JSONP-tjänsten att anropas.

#### reset {#reset}

Återställer de ursprungliga värdena för butikens beständiga data och anropar sedan JSONP-tjänsten. Du kan också ta bort alla andra data från arkivet. Händelser pausas för det här arkivet medan de ursprungliga värdena återställs. Den här funktionen returnerar inget värde.

Initialvärden anges i egenskapen initialValues för det config-objekt som används för att instansiera lagringsobjektet.

##### Parametrar {#parameters-reset-1}

* **`keepRemainingData`:** (Boolean) Värdet true gör att icke-initiala data bevaras. Värdet false medför att alla data tas bort utom de ursprungliga värdena.

#### resolveParameter(f) {#resolveparameter-f}

Matchar den angivna parametern.

## ContextHub.Store.PersistedJSONPStore {#contexthub-store-persistedjsonpstore}

`ContextHub.Store.PersistedJSONPStore` utökar [ContextHub.Store.JSONPStore](#contexthub-store-jsonpstore) så att den ärver alla funktioner i den klassen. Data som hämtas från JSONP-tjänsten sparas dock enligt konfigurationen för ContextHub-beständighet. (Se [Persistenslägen:](configuring-contexthub.md#persistence-modes))

## ContextHub.Store.PersistedStore {#contexthub-store-persistedstore}

`ContextHub.Store.PersistedStore` utökar [ContextHub.Store.Core](#contexthub-store-core) så att den ärver alla funktioner i den klassen. Data i det här arkivet bevaras enligt konfigurationen för ContextHub-beständighet.

## ContextHub.Store.SessionStore {#contexthub-store-sessionstore}

`ContextHub.Store.SessionStore` utökar [ContextHub.Store.Core](#contexthub-store-core) så att den ärver alla funktioner i den klassen. Data i det här arkivet bevaras med beständighet i minnet (Javascript-objekt).

## ContextHub.UI {#contexthub-ui}

Hanterar gränssnittsmoduler och gränssnittsmodulrenderare.

### Funktioner (ContextHub.UI) {#functions-contexthub-ui}

#### registerRenderer(moduleType, renderer, dontRender) {#registerrenderer-moduletype-renderer-dontrender}

Registrerar en gränssnittsmodulrenderare med ContextHub. När återgivaren har registrerats kan den användas för att [skapa gränssnittsmoduler](configuring-contexthub.md#adding-a-ui-module). Använd den här funktionen när du [utökar `ContextHub.UI.BaseModuleRenderer`](extending-contexthub.md#creating-contexthub-ui-module-types) för att skapa en anpassad UI-modulrenderare.

##### Parametrar {#parameters-registerrenderer}

* **`moduleType`:** (String) Identifieraren för gränssnittsmodulens renderare. Om en renderare redan är registrerad med det angivna värdet avregistreras den befintliga renderaren innan den registreras.
* **`renderer`:** (String) Namnet på den klass som återger gränssnittsmodulen.
* **`dontRender`:** (Boolean) Ange detta för `true` att förhindra att ContextHub-gränssnittet återges efter att återgivaren har registrerats. Standardvärdet är `false`.

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

Värdet `boolean` true anger att cookien finns.

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

Värdet för cookie eller `null` om ingen cookie hittades för nyckeln.

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
   * En funktion: En funktion som testar en cookie-nyckel för en matchning. Funktionen måste ta cookie-nyckeln som en parameter och returnera `true` om testet bekräftar en matchning.

##### Returnerar {#returns-getkeys-1}

En array med strängar där varje sträng är nyckeln till en cookie som matchar filtret.

##### Exempel {#example-getkeys-1}

```javascript
ContextHub.Utils.Cookie.getKeys([/^cq-authoring/, /^cq-editor/])
```

#### removeItem(key, options) {#removeitem-key-options-1}

Tar bort en cookie. Om du vill ta bort cookien anges värdet till en tom sträng och förfallodatumet anges till dagen före det aktuella datumet.

##### Parametrar {#parameters-removeitem-1}

* **`key`:** Ett `String` värde som representerar nyckeln till den cookie som ska tas bort.
* **`options`:** Ett objekt som innehåller egenskapsvärden för konfiguration av cookie-attributen. Mer information finns i [`setItem`](#setitem-key-value-options) funktionen. Egenskapen har ingen effekt `expires` .

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
   * `expires`: Ett `date` - eller `number` -värde som anger när cookien upphör att gälla. Ett datumvärde anger den absoluta förfallotiden. Ett tal (i dagar) anger förfallotiden till den aktuella tiden plus talet. Standardvärdet är `undefined`.
   * `secure`: Ett `boolean` värde som anger `Secure` cookie-attributet. Standardvärdet är `false`.
   * `path`: Ett `String` värde som ska användas som `Path` attribut för cookien. Standardvärdet är `undefined`.

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

Tar bort alla cookies som matchar ett visst filter. Cookies matchas med funktionen och tas bort med `getKeys` funktionen `removeItem` .

##### Parametrar {#parameters-vanish}

* **`filter`:** Argumentet `filter` som ska användas i anropet till [`getKeys`](#getkeys-filter) funktionen.
* **`options`:** Argumentet `options` som ska användas i anropet till [`removeItem`](#removeitem-key-options) funktionen.

##### Returnerar {#returns-vanish}

Den här funktionen returnerar inget värde.

## ContextHub.Utils.Eventing {#contexthub-utils-eventing}

Gör att du kan binda och koppla upp funktioner till ContextHub-butikshändelser. Få åtkomst till `ContextHub.Utils.Eventing` objekt för en butik med hjälp av egenskapen [eventing](#eventing) i butiken.

### Funktioner (ContextHub.Utils.Eventing) {#functions-contexthub-utils-eventing}

#### off(name, selector) {#off-name-selector}

Avbinder en funktion från en händelse.

##### Parametrar {#parameters-off}

* **`name`:** Namnet [på händelsen](#contexthub-utils-eventing) som du tar bort bindningen till funktionen för.
* **`selector`:** Väljaren som identifierar bindningen. (Se parametern `selector` för [`on`](#on-name-handler-selector-triggerforpastevents) och [`once`](#once-name-handler-selector-triggerforpastevents) funktioner).

##### Returnerar {#returns-off}

Den här funktionen returnerar inget värde.

#### on(name, handler, selector, triggerForPastEvents) {#on-name-handler-selector-triggerforpastevents}

Bindar en funktion till en händelse. Funktionen anropas varje gång händelsen inträffar. Funktionen kan också anropas för händelser som har inträffat tidigare, innan bindningen har upprättats.

##### Parametrar {#parameters-on}

* **`name`:** (String) Namnet [på händelsen](#contexthub-utils-eventing) som du binder funktionen till.
* **`handler`:** (Funktion) Funktionen som ska bindas till händelsen.
* **`selector`:** (String) En unik identifierare för bindningen. Du behöver väljaren för att identifiera bindningen om du vill använda funktionen för att ta bort bindningen `off` .
* **`triggerForPastEvents`:** (Boolean) Anger om hanteraren ska köras för händelser som har inträffat tidigare. Ett värde på `true` anropar hanteraren för tidigare händelser. Ett värde på `false` anropar hanteraren för framtida händelser. Standardvärdet är `true`.

##### Returnerar {#returns-on}

När argumentet `triggerForPastEvents` är `true`returnerar funktionen ett `boolean` värde som anger om händelsen har inträffat tidigare:

* `true`: Händelsen inträffade tidigare och hanteraren anropas.
* `false`: Händelsen har inte inträffat tidigare.

Om `triggerForPastEvents` är `false`det returnerar funktionen inget värde.

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

* **`name`:** (String) Namnet [på händelsen](#contexthub-utils-eventing) som du binder funktionen till.
* **`handler`:** (Funktion) Funktionen som ska bindas till händelsen.
* **`selector`:** (String) En unik identifierare för bindningen. Du behöver väljaren för att identifiera bindningen om du vill använda funktionen för att ta bort bindningen `off` .
* **`triggerForPastEvents`:** (Boolean) Anger om hanteraren ska köras för händelser som har inträffat tidigare. Ett värde på `true` anropar hanteraren för tidigare händelser. Ett värde på `false` anropar hanteraren för framtida händelser. Standardvärdet är `true`.

##### Returnerar {#returns-once}

När argumentet `triggerForPastEvents` är `true`returnerar funktionen ett `boolean` värde som anger om händelsen har inträffat tidigare:

* `true`: Händelsen inträffade tidigare och hanteraren anropas.
* `false`: Händelsen har inte inträffat tidigare.

Om `triggerForPastEvents` är `false`det returnerar funktionen inget värde.

## ContextHub.Utils.arv {#contexthub-utils-inheritance}

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

Det serialiserade strängvärdet. När `data` är ett R- `egExp` värde returnerar den här funktionen ett tomt objekt. När `data` är en funktion returneras `undefined`.

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
* **`secondTree`:** Det objekt som sammanfogas med kopian av `tree` objektet.

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

Tänk på följande JavaScript-objekt:

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
* **`order`:** (Valfritt) En funktion som bestämmer sorteringsordningen för de returnerade tangenterna. (Se [`Array.prototype.sort`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort) i Mozilla Developer Network.)

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

Skriptet `ContextHub.Utils.JSON.tree.getKeys(myObject);` returnerar följande array:

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

* Minskar flera på varandra följande snedstreck till ett enda snedstreck.
* Tar bort mellanrum från början och slutet av strängen.
* Delar upp resultatet i en array med strängar som avgränsas av snedstreck.

Använd den resulterande arrayen för att skapa en användbar nyckel.

##### Parametrar {#parameters-sanitizekey}

* **`key`:** De `string` som ska saneras.

##### Returnerar {#returns-sanitizekey}

En array med `string` värden där varje sträng är den del av `key` som avgränsades av snedstreck. representerar den sanerade nyckeln. Om den sanerade arrayen har längden noll returneras den här funktionen `null`.

##### Exempel {#example-sanitizekey}

I följande kod saneras en sträng så att arrayen skapas `["this", "is", "a", "path"]`och sedan genereras nyckeln `"/this/is/a/path"` från arrayen:

```javascript
var key = " / this////is/a/path ";
ContextHub.Utils.JSON.tree.sanitizeKey(key)
"/" + ContextHub.Utils.JSON.tree.sanitizeKey(key).join("/");
```

#### setItem(tree, key, value) {#setitem-tree-key-value}

Lägger till ett nyckel/värde-par i dataträdet för en kopia av ett objekt. Mer information om dataträd finns i [Persistence.](contexthub.md#persistence)

##### Parametrar {#parameters-setitem-2}

* **`tree`:** Ett dataobjekt.
* **`key`:** Den tangent som ska kopplas till värdet som du lägger till. Nyckeln är sökvägen till objektet i dataträdet. Den här funktionen anropar `ContextHub.Utils.JSON.tree.sanitize` för att rensa nyckeln innan den läggs till.
* **`value`:** Värdet som ska läggas till i dataträdet.

##### Returnerar {#returns-setitem-2}

En kopia av `tree` objektet som innehåller `key`/ `value` -paret.

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

* **`storeType`:** (String) Namnet på lagringstypen. Se `storeType` funktionens parameter. [`ContextHub.Utils.storeCandidates.registerStoreCandidate`](#contexthub-utils-storecandidates)

##### Returnerar {#returns-getregisteredcandidates}

Ett objekt av lagringstyper. Objektegenskaperna är lagringstypsnamnen och egenskapsvärdena är en array med registrerade lagringskandidater.

#### getStoreFromCandidates(storeType) {#getstorefromcandidates-storetype}

Returnerar en butikstyp från de registrerade anbudssökandena. Om fler än en lagringstyp med samma namn är registrerad returnerar funktionen den lagringstyp som har högst prioritet.

##### Parametrar {#parameters-getstorefromcandidates}

* `storeType`: (String) Namnet på lagringskandidaten. Se `storeType` funktionens parameter. [`ContextHub.Utils.storeCandidates.registerStoreCandidate`](#registerstorecandidate-store-storetype-priority-applies)

##### Returnerar {#returns-getstorefromcandidates}

Ett objekt som representerar den registrerade butikskandidaten. Om den begärda lagringstypen inte har registrerats genereras ett fel.

#### getSupportedStoreTypes() {#getsupportedstoretypes}

Returnerar namnen på de butikstyper som är registrerade som butikskandidater. Den här funktionen kräver inga parametrar.

##### Returnerar {#returns-getsupportedstoretypes}

En array med strängvärden, där varje sträng är den storetype som en lagringskandidat registrerades med. Se `storeType` funktionens parameter. [`ContextHub.Utils.storeCandidates.registerStoreCandidate`](#contexthub-utils-storecandidates)

#### registerStoreCandidate(store, storeType, priority, apply) {#registerstorecandidate-store-storetype-priority-applies}

Registrerar ett lagringsobjekt som ett arkivkandidat med ett namn och en prioritet.

Prioriteten är ett tal som anger vikten av butiker med samma namn. När en butikskandidat registreras med samma namn som en redan registrerad butikskandidat, används den som har den högre prioriteten. När du registrerar en butikskandidater registreras butiken endast om prioriteten är högre än de registrerade butikskandidaterna med samma namn.

##### Parametrar {#parameters-registerstorecandidate}

* **`store`:** (Objekt) Det lagringsobjekt som ska registreras som lagringskandidater.
* **`storeType`:** (String) Namnet på lagringskandidaten. Det här värdet krävs när du skapar en instans av lagringskandidaten.
* **`priority`:** (Number) Prioriteten för butikskandidaten.
* **`applies`:** (Funktion) Funktionen som ska anropas som utvärderar butikens tillämplighet i den aktuella miljön. Funktionen måste returneras `true` om butiken är tillämplig, `false` annars. Standardvärdet är en funktion som returnerar true: `function() {return true;}`

##### Exempel {#example-registerstorecandidate}

```javascript
ContextHub.Utils.storeCandidates.registerStoreCandidate(myStoreCandidate,
                                'contexthub.mystorecandiate', 0);
```

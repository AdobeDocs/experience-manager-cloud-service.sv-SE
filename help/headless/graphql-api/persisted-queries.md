---
title: Beständiga GraphQL-frågor
description: Lär dig hur du bibehåller GraphQL-frågor i Adobe Experience Manager as a Cloud Service för att optimera prestandan. Beständiga frågor kan begäras av klientprogram med HTTP GET-metoden och svaret kan cachas i dispatcher- och CDN-lagren, vilket i slutänden förbättrar klientprogrammens prestanda.
feature: Content Fragments,GraphQL API
exl-id: 080c0838-8504-47a9-a2a2-d12eadfea4c0
source-git-commit: c3d7cd591bce282bb4d3b5b5d0ee2e22fd337a83
workflow-type: tm+mt
source-wordcount: '1687'
ht-degree: 1%

---

# Beständiga GraphQL-frågor {#persisted-queries-caching}

Beständiga frågor är GraphQL-frågor som skapas och lagras på den as a Cloud Service Adobe Experience Manager-servern (AEM). De kan begäras med en GET-begäran från klientprogram. Svaret på en GET-begäran kan cachas i skikten dispatcher och CDN, vilket i slutänden förbättrar prestanda för det begärande klientprogrammet. Detta skiljer sig från vanliga GraphQL-frågor, som körs med förfrågningar från POSTER där svaret inte enkelt kan cachas.

>[!NOTE]
>
>Beständiga frågor rekommenderas. Se [GraphQL Query Best Practices (Dispatcher)](/help/headless/graphql-api/content-fragments.md#graphql-query-best-practices) för mer information och den relaterade Dispatcher-konfigurationen.

The [GraphiQL IDE](/help/headless/graphql-api/graphiql-ide.md) finns i AEM för att du ska kunna utveckla, testa och behålla dina GraphQL-frågor innan [överföra till produktionsmiljön](#transfer-persisted-query-production). För ärenden som behöver anpassas (till exempel när [anpassa cachen](/help/headless/graphql-api/graphiql-ide.md#caching-persisted-queries)) kan du använda API:t, se exemplet med cURL i [Så här behåller du en GraphQL-fråga](#how-to-persist-query).

## Beständiga frågor och slutpunkter {#persisted-queries-and-endpoints}

Beständiga frågor måste alltid använda den slutpunkt som är relaterad till [lämplig platskonfiguration](graphql-endpoint.md); så att de kan använda antingen eller båda:

* Den globala konfigurationen och slutpunkten Frågan har åtkomst till alla modeller för innehållsfragment.
* Specifika platskonfigurationer och slutpunkter Om du vill skapa en beständig fråga för en specifik platskonfiguration måste du ha en motsvarande platskonfigurationsspecifik slutpunkt (för att ge åtkomst till relaterade modeller för innehållsfragment).
Om du till exempel vill skapa en beständig fråga specifikt för WKND-platskonfigurationen, måste en motsvarande WKND-specifik platskonfiguration och en WKND-specifik slutpunkt skapas i förväg.

>[!NOTE]
>
>Se [Aktivera funktionen för innehållsfragment i konfigurationsläsaren](/help/sites-cloud/administering/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser) för mer information.
>
>The **GraphQL Beständiga frågor** måste aktiveras för rätt platskonfiguration.

Om det till exempel finns en viss fråga som heter `my-query`, som använder en modell `my-model` från platskonfigurationen `my-conf`:

* Du kan skapa en fråga med `my-conf` en specifik slutpunkt, och därefter sparas frågan enligt följande:
   `/conf/my-conf/settings/graphql/persistentQueries/my-query`
* Du kan skapa samma fråga med `global` slutpunkten, men frågan sparas sedan enligt följande:
   `/conf/global/settings/graphql/persistentQueries/my-query`

>[!NOTE]
>
>Det här är två olika frågor - sparade under olika sökvägar.
>
>De råkar bara använda samma modell, men via olika slutpunkter.

## Så här behåller du en GraphQL-fråga {#how-to-persist-query}

Vi rekommenderar att du behåller frågor i en AEM redigeringsmiljö först och sedan [överför frågan](#transfer-persisted-query-production) till din produktion AEM publiceringsmiljö, som kan användas av program.

Det finns olika metoder för beständiga frågor, bland annat:

* GraphiQL IDE - se [Sparar beständiga frågor](/help/headless/graphql-api/graphiql-ide.md#saving-persisted-queries) (föredragen metod)
* cURL - se följande exempel
* Andra verktyg, inklusive [Postman](https://www.postman.com/)

GraphiQL IDE är **standard** metod för beständiga frågor. Bevara en given fråga med **cURL** kommandoradsverktyg:

1. Förbered frågan genom att PUTing den till den nya slutpunkts-URL:en `/graphql/persist.json/<config>/<persisted-label>`.

   Skapa till exempel en beständig fråga:

   ```shell
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query" \
       -d \
   '{
     articleList {
       items{
           _path
           author
           main {
               json
           }
       }
     }
   }'
   ```

1. Kontrollera svaret nu.

   Kontrollera till exempel om åtgärden lyckades:

   ```json
   {
     "action": "create",
     "configurationName": "wknd",
     "name": "plain-article-query",
     "shortPath": "/wknd/plain-article-query",
     "path": "/conf/wknd/settings/graphql/persistentQueries/plain-article-query"
   }
   ```

1. Du kan sedan begära den beständiga frågan genom att GETing the URL `/graphql/execute.json/<shortPath>`.

   Använd till exempel den beständiga frågan:

   ```shell
   $ curl -X GET \
       http://localhost:4502/graphql/execute.json/wknd/plain-article-query
   ```

1. Uppdatera en beständig fråga genom POSTing till en redan befintlig frågesökväg.

   Använd till exempel den beständiga frågan:

   ```shell
   $ curl -X POST \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query" \
       -d \
   '{
     articleList {
       items{
           _path
           author
           main {
               json
           }
         referencearticle {
           _path
         }
       }
     }
   }'
   ```

1. Skapa en omsluten vanlig fråga.

   Till exempel:

   ```shell
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-wrapped" \
       -d \
   '{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }"}'
   ```

1. Skapa en omsluten oformaterad fråga med cachekontroll.

   Till exempel:

   ```shell
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-max-age" \
       -d \
   '{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }", "cache-control": { "max-age": 300 }}'
   ```

1. Skapa en beständig fråga med parametrar:

   Till exempel:

   ```shell
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-parameters" \
       -d \
   'query GetAsGraphqlModelTestByPath($apath: String!, $withReference: Boolean = true) {
     articleByPath(_path: $apath) {
       item {
         _path
           author
           main {
           plaintext
           }
           referencearticle @include(if: $withReference) {
           _path
           }
         }
       }
     }'
   ```


## Så här kör du en fråga som är sparad {#execute-persisted-query}

Om du vill köra en fråga som är permanent skapar ett klientprogram en GET-begäran med följande syntax:

```
GET <AEM_HOST>/graphql/execute.json/<PERSISTENT_PATH>
```

Plats `PERSISTENT_PATH` är en förkortad sökväg där den beständiga frågan sparas.

1. Till exempel `wknd` är konfigurationsnamnet och `plain-article-query` är namnet på den beständiga frågan. Så här kör du frågan:

   ```shell
   $ curl -X GET \
       https://publish-p123-e456.adobeaemcloud.com/graphql/execute.json/wknd/plain-article-query
   ```

1. Kör en fråga med parametrar.

   >[!NOTE]
   >
   > Frågevariabler och -värden måste vara korrekta [kodad](#encoding-query-url) när en fråga som är sparad körs.

   Till exempel:

   ```xml
   $ curl -X GET \
       "https://publish-p123-e456.adobeaemcloud.com/graphql/execute.json/wknd/plain-article-query-parameters%3Bapath%3D%2Fcontent%2Fdam%2Fwknd%2Fen%2Fmagazine%2Falaska-adventure%2Falaskan-adventures%3BwithReference%3Dfalse
   ```

   Se använda [frågevariabler](#query-variables) för mer information.

## Använda frågevariabler {#query-variables}

Frågevariabler kan användas med beständiga frågor. Frågevariablerna läggs till i begäran med ett semikolon (`;`) med variabelnamnet och variabelvärdet. Flera variabler avgränsas med semikolon.

Mönstret ser ut så här:

```
<AEM_HOST>/graphql/execute.json/<PERSISTENT_QUERY_PATH>;variable1=value1;variable2=value2
```

Följande fråga innehåller till exempel en variabel `activity` om du vill filtrera en lista baserat på ett aktivitetsvärde:

```graphql
query getAdventuresByActivity($activity: String!) {
      adventureList (filter: {
        adventureActivity: {
          _expressions: [
            {
              value: $activity
            }
          ]
        }
      }){
        items {
          _path
        adventureTitle
        adventurePrice
        adventureTripLength
      }
    }
  }
```

Den här frågan kan sparas under en sökväg `wknd/adventures-by-activity`. Så här anropar du den beständiga frågan där `activity=Camping` begäran skulle se ut så här:

```
<AEM_HOST>/graphql/execute.json/wknd/adventures-by-activity%3Bactivity%3DCamping
```

Observera att `%3B` är UTF-8-kodning för `;` och `%3D` är kodningen för `=`. Frågevariablerna och eventuella specialtecken måste [korrekt kodad](#encoding-query-url) för den beständiga frågan som ska köras.

## Cachelagra beständiga frågor {#caching-persisted-queries}

Beständiga frågor rekommenderas eftersom de kan cachelagras på [Dispatcher](/help/headless/deployment/dispatcher.md) och CDN-lager (Content Delivery Network), vilket i slutänden förbättrar prestandan för det begärande klientprogrammet.

Som standard blir cachen ogiltig AEM baserat på en TTL-definition (Time To Live). Dessa TTL:er kan definieras med följande parametrar. Dessa parametrar kan nås på olika sätt, med variationer i namnen beroende på vilken mekanism som används:

| Cachetyp | [HTTP-huvud](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cache-Control)  | cURL  | OSGi-konfiguration  | Cloud Manager |
|--- |--- |--- |--- |--- |
| Webbläsare | `max-age` | `cache-control : max-age` | `cacheControlMaxAge` | `graphqlCacheControl` |
| CDN | `s-maxage` | `surrogate-control : max-age` | `surrogateControlMaxAge` | `graphqlSurrogateControl` | 60 |
| CDN | `stale-while-revalidate` | `surrogate-control : stale-while-revalidate ` | `surrogateControlStaleWhileRevalidate` | `graphqlStaleWhileRevalidate` |
| CDN | `stale-if-error` | `surrogate-control : stale-if-error` | `surrogateControlStaleIfError` | `graphqlStaleIfError` |

{style="table-layout:auto"}

### Författarinstanser {#author-instances}

För författarinstanser är standardvärdena:

* `max-age`  : 60
* `s-maxage` : 60
* `stale-while-revalidate` : 86400
* `stale-if-error` : 86400

De var:

* kan inte skrivas över:
   * med en OSGi-konfiguration
* kan skrivas över:
   * av en begäran som definierar inställningar för HTTP-huvudet med cURL, bör innehålla lämpliga inställningar för `cache-control` och/eller `surrogate-control`; finns i [Hantera cache på nivån för beständig fråga](#cache-persisted-query-level)
   * om du anger värden i **Sidhuvuden** dialogrutan [GraphiQL IDE](#http-cache-headers-graphiql-ide)

### Publicera instanser {#publish-instances}

Standardvärdena för publiceringsinstanser är:

* `max-age`  : 60
* `s-maxage` : 7200
* `stale-while-revalidate` : 86400
* `stale-if-error` : 86400

Dessa kan skrivas över:

* [från GraphQL IDE](#http-cache-headers-graphiql-ide)

* [på den beständiga frågenivån](#cache-persisted-query-level); detta innebär att skicka frågan till AEM med cURL i kommandoradsgränssnittet och att publicera den beständiga frågan.

* [med Cloud Manager-variabler](#cache-cloud-manager-variables)

* [med en OSGi-konfiguration](#cache-osgi-configration)

### Hantera rubriker för HTTP-cache i GraphiQL IDE {#http-cache-headers-graphiql-ide}

GraphiQL IDE - se [Sparar beständiga frågor](/help/headless/graphql-api/graphiql-ide.md#managing-cache)

### Hantera cache på nivån för beständig fråga {#cache-persisted-query-level}

Detta innebär att skicka frågan till AEM med cURL i kommandoradsgränssnittet.

Ett exempel på metoden PUT (skapa):

```bash
curl -u admin:admin -X PUT \
--url "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-max-age" \
--header "Content-Type: application/json" \
--data '{ "query": "{articleList { items { _path author } } }", "cache-control": { "max-age": 300 }, "surrogate-control": {"max-age":600, "stale-while-revalidate":1000, "stale-if-error":1000} }'
```

Ett exempel på metoden POST (update):

```bash
curl -u admin:admin -X POST \
--url "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-max-age" \
--header "Content-Type: application/json" \
--data '{ "query": "{articleList { items { _path author } } }", "cache-control": { "max-age": 300 }, "surrogate-control": {"max-age":600, "stale-while-revalidate":1000, "stale-if-error":1000} }'
```

The `cache-control` kan anges vid skapande (PUT) eller senare (till exempel via en POST-förfrågan). Cachekontrollen är valfri när du skapar den beständiga frågan, eftersom AEM kan ange standardvärdet. Se [Så här behåller du en GraphQL-fråga](#how-to-persist-query), för ett exempel på beständig fråga med cURL.

### Hantera cache med Cloud Manager-variabler {#cache-cloud-manager-variables}

[Miljövariabler för Cloud Manager](/help/implementing/cloud-manager/environment-variables.md) kan definieras med Cloud Manager för att definiera de värden som krävs:

| Namn | Värde | Tjänsten används | Typ |
|--- |--- |--- |--- |
| `graphqlStaleIfError` | 86400 | *efter behov* | *efter behov* |
| `graphqlSurrogateControl` | 600 | *efter behov* | *efter behov* |

{style="table-layout:auto"}

### Hantera cache med en OSGi-konfiguration {#cache-osgi-configration}

Om du vill hantera cachen globalt kan du [konfigurera OSGi-inställningarna](/help/implementing/deploying/configuring-osgi.md) för **Konfiguration av beständig frågetjänst**.

>[!NOTE]
>
>För cachekontroll är OSGi-konfigurationen endast lämplig för publiceringsinstanser. Konfigurationen finns på författarinstanser, men ignoreras.

>[!NOTE]
>
>The **Konfiguration av beständig frågetjänst** används också för [konfigurera frågesvarskoden](#configuring-query-response-code).

Standardkonfigurationen för OSGi för publiceringsinstanser:

* läser Cloud Manager-variabler om de är tillgängliga:

   | OSGi-konfigurationsegenskap | läser detta | Cloud Manager-variabel |
   |--- |--- |--- |
   | `cacheControlMaxAge` | läsningar | `graphqlCacheControl` |
   | `surrogateControlMaxAge` | läsningar | `graphqlSurrogateControl` |
   | `surrogateControlStaleWhileRevalidate` | läsningar | `graphqlStaleWhileRevalidate` |
   | `surrogateControlStaleIfError` | läsningar | `graphqlStaleIfError` |

   {style="table-layout:auto"}

* Om den inte är tillgänglig använder OSGi-konfigurationen [standardvärden för publiceringsinstanser](#publish-instances).

## Konfigurera frågesvarskoden {#configuring-query-response-code}

Som standard är `PersistedQueryServlet` skickar en `200` svar när den kör en fråga, oavsett det faktiska resultatet.

Du kan [konfigurera OSGi-inställningarna](/help/implementing/deploying/configuring-osgi.md) för **Konfiguration av beständig frågetjänst** för att kontrollera vilken statuskod som returneras av `/execute.json/persisted-query` slutpunkten, om det finns ett fel i den beständiga frågan.

>[!NOTE]
>
>The **Konfiguration av beständig frågetjänst** används också för [hantera cache](#cache-osgi-configration).

Fältet `Respond with application/graphql-response+json` (`responseContentTypeGraphQLResponseJson`) kan definieras enligt behov:

* `false` (standardvärde): Det spelar ingen roll om den beständiga frågan lyckas eller inte. The `/execute.json/persisted-query` returnerar statuskoden `200` och `Content-Type` returnerad rubrik `application/json`.

* `true`: Slutpunkten returnerar `400` eller `500` om det finns någon form av fel när den beständiga frågan körs. Även den returnerade `Content-Type` kommer att `application/graphql-response+json`.

   >[!NOTE]
   >
   >Mer information finns på https://graphql.github.io/graphql-over-http/draft/#sec-Status-Codes

## Kodning av fråge-URL för användning av ett program {#encoding-query-url}

Om det används av ett program används alla specialtecken som används för att skapa frågevariabler (t.ex. semikolon (`;`), likhetstecken (`=`), snedstreck `/`) måste konverteras till motsvarande UTF-8-kodning.

Till exempel:

```xml
curl -X GET \ "https://publish-p123-e456.adobeaemcloud.com/graphql/execute.json/wknd/adventure-by-path%3BadventurePath%3D%2Fcontent%2Fdam%2Fwknd%2Fen%2Fadventures%2Fbali-surf-camp%2Fbali-surf-camp"
```

URL:en kan delas upp i följande delar:

| URL-del | Beskrivning |
|----------| -------------|
| `/graphql/execute.json` | Beständig frågeslutpunkt |
| `/wknd/adventure-by-path` | Sökväg för beständig fråga |
| `%3B` | Kodning av `;` |
| `adventurePath` | Frågevariabel |
| `%3D` | Kodning av `=` |
| `%2F` | Kodning av `/` |
| `%2Fcontent%2Fdam...` | Kodad sökväg till innehållsfragmentet |

I vanlig text ser URI:n för begäran ut så här:

```plaintext
/graphql/execute.json/wknd/adventure-by-path;adventurePath=/content/dam/wknd/en/adventures/bali-surf-camp/bali-surf-camp
```

Om du vill använda en beständig fråga i en klientapp bör AEM headless Client SDK användas för [JavaScript](https://github.com/adobe/aem-headless-client-js), [Java](https://github.com/adobe/aem-headless-client-java), eller [NodeJS](https://github.com/adobe/aem-headless-client-nodejs). SDK för den Headless-klienten kodar automatiskt alla frågevariabler som behövs i begäran.

## Överför en beständig fråga till produktionsmiljön  {#transfer-persisted-query-production}

Beständiga frågor bör alltid skapas i en AEM Author-tjänst och sedan publiceras (replikeras) till en AEM Publish-tjänst. Vanligtvis skapas och testas beständiga frågor i miljöer som lokala miljöer och utvecklingsmiljöer. Det är sedan nödvändigt att befordra beständiga frågor till miljöer på högre nivå och i slutänden göra dem tillgängliga i en AEM Publish-produktionsmiljö så att klientapplikationerna kan använda dem.

### Paketera beständiga frågor

Beständiga frågor kan byggas in i [AEM](/help/implementing/developing/tools/package-manager.md). AEM paket kan sedan laddas ned och installeras i olika miljöer. AEM kan också replikeras från en AEM Author-miljö till AEM Publish-miljöer.

Så här skapar du ett paket:

1. Navigera till **verktyg** > **Distribution** > **Paket**.
1. Skapa ett nytt paket genom att trycka **Skapa paket**. Då öppnas en dialogruta där du kan definiera paketet.
1. I dialogrutan Paketdefinition, under **Allmänt** ange **Namn** som &quot;wknd-persistent-queries&quot;.
1. Ange ett versionsnummer som &quot;1.0&quot;.
1. Under **Filter** lägg till en ny **Filter**. Använd Sökväg för att välja `persistentQueries` under konfigurationen. Till exempel `wknd` konfiguration den fullständiga sökvägen kommer att `/conf/wknd/settings/graphql/persistentQueries`.
1. Tryck **Spara** för att spara den nya paketdefinitionen och stänga dialogrutan.
1. Tryck på **Bygge** i den nyligen skapade paketdefinitionen.

När paketet har byggts kan du:

* **Hämta** paketet och ladda upp det igen i en annan miljö.
* **Replikera** paketet genom att trycka **Mer** > **Replikera**. Paketet kommer att replikeras till den anslutna AEM-publiceringsmiljön.

<!--
1. Using replication/distribution tool:
   1. Go to the Distribution tool.
   1. Select tree activation for the configuration (for example, `/conf/wknd/settings/graphql/persistentQueries`).

* Using a workflow (via workflow launcher configuration):
  1. Define a workflow launcher rule for executing a workflow model that would replicate the configuration on different events (for example, create, modify, amongst others).
-->

---
title: Beständiga GraphQL-frågor
description: Lär dig hur du bibehåller GraphQL-frågor i Adobe Experience Manager as a Cloud Service för att optimera prestandan. Beständiga frågor kan begäras av klientprogram med HTTP GET-metoden och svaret kan cachas i dispatcher- och CDN-lagren, vilket i slutänden förbättrar klientprogrammens prestanda.
feature: Headless, Content Fragments,GraphQL API
exl-id: 080c0838-8504-47a9-a2a2-d12eadfea4c0
role: Admin, Developer
source-git-commit: 2e257634313d3097db770211fe635b348ffb36cf
workflow-type: tm+mt
source-wordcount: '1952'
ht-degree: 0%

---

# Beständiga GraphQL-frågor {#persisted-graphql-queries}

Beständiga frågor är GraphQL-frågor som skapas och lagras på Adobe Experience Manager (AEM) as a Cloud Service-servern. De kan begäras med en GET-begäran från klientprogram. Svaret på en GET-begäran kan cachelagras på dispatcher- och CDN-lagren, vilket i slutänden förbättrar prestanda för det begärande klientprogrammet. Detta skiljer sig från vanliga GraphQL-frågor, som körs med POST-begäranden där svaret inte enkelt kan cachas.

>[!NOTE]
>
>Beständiga frågor rekommenderas. Läs [GraphQL Query Best Practices (Dispatcher)](/help/headless/graphql-api/content-fragments.md#graphql-query-best-practices) om du vill ha mer information och relaterad Dispatcher-konfiguration.

[GraphiQL IDE](/help/headless/graphql-api/graphiql-ide.md) är tillgänglig i AEM så att du kan utveckla, testa och behålla dina GraphQL-frågor innan du [överför dem till produktionsmiljön](#transfer-persisted-query-production). Om du behöver anpassa (till exempel när du [anpassar cachen](/help/headless/graphql-api/graphiql-ide.md#caching-persisted-queries)) kan du använda API:t, se exemplet på cURL i [Så här gör du för att behålla en GraphQL-fråga](#how-to-persist-query).

## Beständiga frågor och slutpunkter {#persisted-queries-and-endpoints}

Beständiga frågor måste alltid använda den slutpunkt som är relaterad till [lämplig platskonfiguration](graphql-endpoint.md), så att de kan använda antingen eller båda:

* Den globala konfigurationen och slutpunkten
Frågan har åtkomst till alla modeller för innehållsfragment.
* Specifika platskonfigurationer och slutpunkter
För att skapa en beständig fråga för en specifik platskonfiguration krävs en motsvarande platskonfigurationsspecifik slutpunkt (för att ge åtkomst till relaterade modeller för innehållsfragment).
Om du till exempel vill skapa en beständig fråga specifikt för WKND-platskonfigurationen, måste en motsvarande WKND-specifik platskonfiguration och en WKND-specifik slutpunkt skapas i förväg.

>[!NOTE]
>
>Mer information finns i [Aktivera funktionen för innehållsfragment i konfigurationsläsaren](/help/sites-cloud/administering/content-fragments/setup.md#enable-content-fragment-functionality-configuration-browser).
>
>**GraphQL beständiga frågor** måste aktiveras för rätt platskonfiguration.

Om det till exempel finns en viss fråga med namnet `my-query` som använder modellen `my-model` från platskonfigurationen `my-conf`:

* Du kan skapa en fråga med den `my-conf` specifika slutpunkten och sedan sparas frågan så här:
  `/conf/my-conf/settings/graphql/persistentQueries/my-query`
* Du kan skapa samma fråga med `global`-slutpunkten, men sedan sparas frågan så här:
  `/conf/global/settings/graphql/persistentQueries/my-query`

>[!NOTE]
>
>Det här är två olika frågor - sparade under olika sökvägar.
>
>De råkar bara använda samma modell, men via olika slutpunkter.

## Så här behåller du en GraphQL-fråga {#how-to-persist-query}

Vi rekommenderar att du till att börja med behåller frågor i en AEM-redigeringsmiljö och sedan [överför frågan](#transfer-persisted-query-production) till din publiceringsmiljö i AEM där den kan användas av program.

Det finns olika metoder för beständiga frågor, bland annat:

* GraphiQL IDE - se [Spara beständiga frågor](/help/headless/graphql-api/graphiql-ide.md#saving-persisted-queries) (föredragen metod)
* cURL - se följande exempel
* Andra verktyg, inklusive [Postman](https://www.postman.com/)

GraphiQL IDE är den **föredragna** metoden för beständiga frågor. Så här behåller du en given fråga med kommandoradsverktyget **cURL**:

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

1. Du kan sedan begära den beständiga frågan genom att GETing anger URL:en `/graphql/execute.json/<shortPath>`.

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

För att köra en Persistent-fråga gör ett klientprogram en GET-begäran med följande syntax:

```
GET <AEM_HOST>/graphql/execute.json/<PERSISTENT_PATH>
```

Där `PERSISTENT_PATH` är en förkortad sökväg till den plats där den beständiga frågan sparas.

1. `wknd` är till exempel konfigurationsnamnet och `plain-article-query` är namnet på den beständiga frågan. Så här kör du frågan:

   ```shell
   $ curl -X GET \
       https://publish-p123-e456.adobeaemcloud.com/graphql/execute.json/wknd/plain-article-query
   ```

1. Kör en fråga med parametrar.

   >[!NOTE]
   >
   > Frågevariabler och -värden måste vara korrekt [kodade](#encoding-query-url) när en Persisted-fråga körs.

   Till exempel:

   ```xml
   $ curl -X GET \
       "https://publish-p123-e456.adobeaemcloud.com/graphql/execute.json/wknd/plain-article-query-parameters%3Bapath%3D%2Fcontent%2Fdam%2Fwknd%2Fen%2Fmagazine%2Falaska-adventure%2Falaskan-adventures%3BwithReference%3Dfalse
   ```

   Mer information finns i Använda [frågevariabler](#query-variables).

## Använda frågevariabler {#query-variables}

Frågevariabler kan användas med beständiga frågor. Frågevariablerna läggs till i begäran med prefixet semikolon (`;`) med variabelnamnet och variabelvärdet. Flera variabler avgränsas med semikolon.

Mönstret ser ut så här:

```
<AEM_HOST>/graphql/execute.json/<PERSISTENT_QUERY_PATH>;variable1=value1;variable2=value2
```

Följande fråga innehåller till exempel variabeln `activity` för att filtrera en lista baserat på ett aktivitetsvärde:

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

Den här frågan kan sparas under sökvägen `wknd/adventures-by-activity`. Så här anropar du den beständiga frågan där `activity=Camping` begäran skulle se ut:

```
<AEM_HOST>/graphql/execute.json/wknd/adventures-by-activity%3Bactivity%3DCamping
```

UTF-8-kodningen `%3B` är för `;` och `%3D` är kodningen för `=`. Frågevariablerna och eventuella specialtecken måste vara [kodade korrekt](#encoding-query-url) för att den beständiga frågan ska kunna köras.

### Använda frågevariabler - Bästa praxis {#query-variables-best-practices}

När du använder variabler i dina frågor finns det några metodtips som du bör följa:

* Kodning
Som en allmän metod bör du alltid koda alla specialtecken, till exempel `;`, `=`, `?`, `&`.

* Semikolon
Beständiga frågor som använder flera variabler (som avgränsas med semikolon) måste ha antingen:
   * semikolon kodade (`%3B`). Om URL:en kodas kommer även detta att uppnås
   * eller ett avslutande semikolon som lagts till i slutet av frågan

* `CACHE_GRAPHQL_PERSISTED_QUERIES`
När `CACHE_GRAPHQL_PERSISTED_QUERIES` är aktiverat för Dispatcher kodas parametrar som innehåller `/` - eller `\` -tecknen i deras värde två gånger på Dispatcher-nivå.
För att undvika denna situation:

   * Aktivera `DispatcherNoCanonURL` på Dispatcher.
Detta instruerar Dispatcher att vidarebefordra den ursprungliga URL:en till AEM, så att dubblerade kodningar förhindras.
Den här inställningen fungerar för närvarande bara på nivån `vhost`, så om du redan har Dispatcher-konfigurationer för att skriva om URL:er (t.ex. när du använder förkortade URL:er) kan du behöva en separat `vhost` för beständiga fråge-URL:er.

   * Skicka `/` eller `\` tecken utan kodning.

     När du anropar den beständiga fråge-URL:en måste du se till att alla `/`- eller `\`-tecken förblir okodade i värdet för beständiga frågevariabler.

     >[!NOTE]
     >
     >Det här alternativet rekommenderas bara när `DispatcherNoCanonURL`-lösningen inte kan implementeras av någon anledning.

* `CACHE_GRAPHQL_PERSISTED_QUERIES`

  När `CACHE_GRAPHQL_PERSISTED_QUERIES` är aktiverat för Dispatcher kan inte tecknet `;` användas i värdet för en variabel.

## Cachelagra beständiga frågor {#caching-persisted-queries}

Beständiga frågor rekommenderas eftersom de kan cachelagras på [Dispatcher](/help/headless/deployment/dispatcher.md) - och CDN-lagren (Content Delivery Network), vilket i slutänden förbättrar prestandan för det begärande klientprogrammet.

Som standard gör AEM cachen ogiltig baserat på en TTL-definition (Time To Live). Dessa TTL:er kan definieras med följande parametrar. Dessa parametrar kan nås på olika sätt, med variationer i namnen beroende på vilken mekanism som används:

| Cache-typ | [HTTP-huvud](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cache-Control)  | cURL  | OSGi-konfiguration  | Cloud Manager |
|--- |--- |--- |--- |--- |
| Webbläsare | `max-age` | `cache-control : max-age` | `cacheControlMaxAge` | `graphqlCacheControl` |
| CDN | `s-maxage` | `surrogate-control : max-age` | `surrogateControlMaxAge` | `graphqlSurrogateControl` \|60 |
| CDN | `stale-while-revalidate` | `surrogate-control : stale-while-revalidate ` | `surrogateControlStaleWhileRevalidate` | `graphqlStaleWhileRevalidate` |
| CDN | `stale-if-error` | `surrogate-control : stale-if-error` | `surrogateControlStaleIfError` | `graphqlStaleIfError` |

{style="table-layout:auto"}

### Författarinstanser {#author-instances}

För författarinstanser är standardvärdena:

* `max-age` : 60
* `s-maxage` : 60
* `stale-while-revalidate` : 86400
* `stale-if-error` : 86400

De var:

* kan inte skrivas över:
   * med en OSGi-konfiguration
* kan skrivas över:
   * av en begäran som definierar inställningar för HTTP-huvudet med cURL; den bör innehålla lämpliga inställningar för `cache-control` och/eller `surrogate-control`; se till exempel [Hantera cache på den beständiga frågenivån](#cache-persisted-query-level)
   * om du anger värden i dialogrutan **Headers** i [GraphiQL IDE](#http-cache-headers-graphiql-ide)

### Publicera förekomster {#publish-instances}

Standardvärdena för publiceringsinstanser är:

* `max-age` : 60
* `s-maxage` : 7200
* `stale-while-revalidate` : 86400
* `stale-if-error` : 86400

Dessa kan skrivas över:

* [från GraphQL IDE](#http-cache-headers-graphiql-ide)

* [&#x200B; på nivån för beständig fråga](#cache-persisted-query-level). Detta innebär att frågan skickas till AEM med cURL i kommandoradsgränssnittet och att den beständiga frågan publiceras.

* [med Cloud Manager-variabler](#cache-cloud-manager-variables)

* [med en OSGi-konfiguration](#cache-osgi-configration)

### Hantera rubriker för HTTP-cache i GraphiQL IDE {#http-cache-headers-graphiql-ide}

GraphiQL IDE - se [Spara beständiga frågor](/help/headless/graphql-api/graphiql-ide.md#managing-cache)

### Hantera cache på nivån för beständig fråga {#cache-persisted-query-level}

Detta innebär att skicka frågan till AEM med cURL i kommandoradsgränssnittet.

Ett exempel på PUT-metoden (skapa):

```bash
curl -u admin:admin -X PUT \
--url "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-max-age" \
--header "Content-Type: application/json" \
--data '{ "query": "{articleList { items { _path author } } }", "cache-control": { "max-age": 300 }, "surrogate-control": {"max-age":600, "stale-while-revalidate":1000, "stale-if-error":1000} }'
```

Ett exempel på POST-metoden (update):

```bash
curl -u admin:admin -X POST \
--url "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-max-age" \
--header "Content-Type: application/json" \
--data '{ "query": "{articleList { items { _path author } } }", "cache-control": { "max-age": 300 }, "surrogate-control": {"max-age":600, "stale-while-revalidate":1000, "stale-if-error":1000} }'
```

`cache-control` kan anges när den skapas (PUT) eller senare (till exempel via en POST-begäran). Cachekontrollen är valfri när du skapar den beständiga frågan, eftersom AEM kan ange standardvärdet. Se [Så här behåller du en GraphQL-fråga](#how-to-persist-query) om du vill se ett exempel på hur en fråga bevaras med cURL.

### Hantera cache med Cloud Manager-variabler {#cache-cloud-manager-variables}

[Cloud Manager miljövariabler](/help/implementing/cloud-manager/environment-variables.md) kan definieras med Cloud Manager för att definiera de värden som krävs:

| Namn | Värde | Tjänsten används | Typ |
|--- |--- |--- |--- |
| `graphqlStaleIfError` | 86400 | *efter behov* | *efter behov* |
| `graphqlSurrogateControl` | 600 | *efter behov* | *efter behov* |

{style="table-layout:auto"}

### Hantera cache med en OSGi-konfiguration {#cache-osgi-configration}

Om du vill hantera cacheminnet globalt kan du [konfigurera OSGi-inställningarna](/help/implementing/deploying/configuring-osgi.md) för **konfigurationen för den beständiga frågetjänsten**.

>[!NOTE]
>
>För cachekontroll är OSGi-konfigurationen endast lämplig för publiceringsinstanser. Konfigurationen finns på författarinstanser, men ignoreras.

>[!NOTE]
>
>**Konfiguration av den beständiga frågetjänsten** används även för [konfigurering av frågesvartekod](#configuring-query-response-code).

Standardkonfigurationen för OSGi för publiceringsinstanser:

* läser Cloud Manager-variablerna om sådana finns:

  | OSGi-konfigurationsegenskap | läser detta | Cloud Manager Variable |
  |--- |--- |--- |
  | `cacheControlMaxAge` | läsningar | `graphqlCacheControl` |
  | `surrogateControlMaxAge` | läsningar | `graphqlSurrogateControl` |
  | `surrogateControlStaleWhileRevalidate` | läsningar | `graphqlStaleWhileRevalidate` |
  | `surrogateControlStaleIfError` | läsningar | `graphqlStaleIfError` |

  {style="table-layout:auto"}

* Om det inte är tillgängligt använder OSGi-konfigurationen [standardvärdena för publiceringsinstanser](#publish-instances).

## Konfigurera frågesvarskoden {#configuring-query-response-code}

Som standard skickar `PersistedQueryServlet` ett `200`-svar när en fråga körs, oavsett det faktiska resultatet.

Du kan [konfigurera OSGi-inställningarna](/help/implementing/deploying/configuring-osgi.md) för **konfigurationen för den beständiga frågetjänsten** för att kontrollera om mer detaljerade statuskoder returneras av `/execute.json/persisted-query`-slutpunkten, om det finns ett fel i den beständiga frågan.

>[!NOTE]
>
>**Konfiguration av den beständiga frågetjänsten** används även för [hantering av cache](#cache-osgi-configration).

Fältet `Respond with application/graphql-response+json` (`responseContentTypeGraphQLResponseJson`) kan definieras enligt behov:

* `false` (standardvärde):
Det spelar ingen roll om den beständiga frågan lyckas eller inte. Det `Content-Type`-huvud som returnerades är `application/json` och `/execute.json/persisted-query` *always* returnerar statuskoden `200`.

* `true`:
Den returnerade `Content-Type` är `application/graphql-response+json` och slutpunkten returnerar lämplig svarskod när det finns någon form av fel när den beständiga frågan körs:

  | Code | Beskrivning |
  |--- |--- |
  | 200 | Slutfört svar |
  | 400 | Anger att det saknas rubriker eller ett problem med den beständiga frågesökvägen. Konfigurationsnamnet har till exempel inte angetts, suffixet har inte angetts och andra har inte angetts.<br>Se [Felsökning - GraphQL-slutpunkt har inte konfigurerats](/help/headless/graphql-api/persisted-queries-troubleshoot.md#missing-path-query-url). |
  | 404 | Det går inte att hitta den begärda resursen. Graphql-slutpunkten är till exempel inte tillgänglig på servern.<br>Se [Felsökning - Sökväg saknas i GraphQL beständiga fråge-URL](/help/headless/graphql-api/persisted-queries-troubleshoot.md#graphql-endpoint-not-configured). |
  | 500 | Internt serverfel. Exempel: valideringsfel, beständighetsfel med mera. |

  >[!NOTE]
  >
  >Se även https://graphql.github.io/graphql-over-http/draft/#sec-Status-Codes

## Kodning av fråge-URL för användning av ett program {#encoding-query-url}

Om du vill använda ett program måste alla specialtecken som används för att skapa frågevariabler (d.v.s. semikolon (`;`), likhetstecken (`=`), snedstreck `/`) konverteras till motsvarande UTF-8-kodning.

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

Om du vill använda en beständig fråga i en klientapp bör AEM Headless-klienten SDK användas för [JavaScript](https://github.com/adobe/aem-headless-client-js), [Java](https://github.com/adobe/aem-headless-client-java) eller [NodeJS](https://github.com/adobe/aem-headless-client-nodejs). Den Headless Client SDK kodar automatiskt alla frågevariabler som behövs i begäran.

## Överför en beständig fråga till produktionsmiljön  {#transfer-persisted-query-production}

Beständiga frågor ska alltid skapas i en AEM Author-tjänst och sedan publiceras (replikeras) i en AEM Publish-tjänst. Vanligtvis skapas och testas beständiga frågor i miljöer som lokala miljöer och utvecklingsmiljöer. Det är sedan nödvändigt att befordra beständiga frågor till miljöer på högre nivå och i slutänden göra dem tillgängliga i en produktionsmiljö i AEM Publish för att klientprogram ska kunna använda dem.

### Paketera beständiga frågor

Beständiga frågor kan byggas in i [AEM-paket](/help/implementing/developing/tools/package-manager.md). AEM Packages kan sedan laddas ned och installeras i olika miljöer. AEM-paket kan också replikeras från en AEM Author-miljö till AEM Publish-miljöer.

Skapa ett paket:

1. Navigera till **Verktyg** > **Distribution** > **Paket**.
1. Skapa ett nytt paket genom att trycka på **Skapa paket**. Då öppnas en dialogruta där du kan definiera paketet.
1. I dialogrutan Paketdefinition, under **Allmänt**, anger du ett **Namn** som &quot;wknd-persistent-queries&quot;.
1. Ange ett versionsnummer som &quot;1.0&quot;.
1. Lägg till ett nytt **Filter** under **Filter**. Använd Sökväg till Finder för att välja mappen `persistentQueries` under konfigurationen. Den fullständiga sökvägen för konfigurationen `wknd` är till exempel `/conf/wknd/settings/graphql/persistentQueries`.
1. Välj **Spara** om du vill spara den nya paketdefinitionen och stänga dialogrutan.
1. Välj knappen **Skapa** i den skapade paketdefinitionen.

När paketet har byggts kan du:

* **Hämta** paketet och överföra det igen till en annan miljö.
* **Replikera** paketet genom att trycka på **Mer** > **Replikera**. Paketet kommer att replikeras till den anslutna AEM Publish-miljön.

<!--
1. Using replication/distribution tool:
   1. Go to the Distribution tool.
   1. Select tree activation for the configuration (for example, `/conf/wknd/settings/graphql/persistentQueries`).

* Using a workflow (via workflow launcher configuration):
  1. Define a workflow launcher rule for executing a workflow model that would replicate the configuration on different events (for example, create, modify, amongst others).
-->

---
title: Beständiga GraphQL-frågor
description: Lär dig hur du bibehåller GraphQL-frågor i Adobe Experience Manager för att optimera prestanda. Beständiga frågor kan begäras av klientprogram med HTTP GET-metoden och svaret kan cachas i dispatcher- och CDN-lagren, vilket i slutänden förbättrar klientprogrammens prestanda.
feature: Content Fragments,GraphQL API
exl-id: 080c0838-8504-47a9-a2a2-d12eadfea4c0
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '644'
ht-degree: 1%

---

# Beständiga GraphQL-frågor {#persisted-queries-caching}

Beständiga frågor är GraphQL-frågor som skapas och lagras på AEM. Standard GraphQL-frågor körs med POST-förfrågningar och svaret kan inte enkelt cachelagras. Beständiga frågor kan begäras med en GET-begäran från klientprogram. Svaret på en GET-begäran kan cachas i skikten dispatcher och CDN, vilket i slutänden förbättrar prestanda för det begärande klientprogrammet.

Beständiga frågor måste alltid använda den slutpunkt som är relaterad till [lämplig platskonfiguration](graphql-endpoint.md); så att de kan använda antingen eller båda:

* Den globala konfigurationen och slutpunkten Frågan har åtkomst till alla modeller för innehållsfragment.
* Specifika platskonfigurationer och slutpunkter Om du vill skapa en beständig fråga för en specifik platskonfiguration måste du ha en motsvarande platskonfigurationsspecifik slutpunkt (för att ge åtkomst till relaterade modeller för innehållsfragment).
Om du till exempel vill skapa en beständig fråga specifikt för WKND-platskonfigurationen, måste en motsvarande WKND-specifik platskonfiguration och en WKND-specifik slutpunkt skapas i förväg.

>[!NOTE]
>
>Se [Aktivera funktionen för innehållsfragment i konfigurationsläsaren](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser) för mer information.
>
>The **frågor om GraphQL-beständighet** måste aktiveras för rätt platskonfiguration.

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

## Bevara en GraphQL-fråga

Vi rekommenderar att du behåller frågor i en AEM redigeringsmiljö först och sedan [publicera frågan](#publish-persisted-query) till en AEM publiceringsmiljö. verktyg som [Postman](https://www.postman.com/) eller kommandoradsverktyg som [kurva](https://curl.se/) kan användas.

Här följer de steg som krävs för att behålla en given fråga med **kurva** kommandoradsverktyg:

1. Förbered frågan genom att PUTing den till den nya slutpunkts-URL:en `/graphql/persist.json/<config>/<persisted-label>`.

   Skapa till exempel en beständig fråga:

   ```xml
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

   ```xml
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

   ```xml
   $ curl -X GET \
       http://localhost:4502/graphql/execute.json/wknd/plain-article-query
   ```

1. Uppdatera en beständig fråga genom POSTing till en redan befintlig frågesökväg.

   Använd till exempel den beständiga frågan:

   ```xml
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

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-wrapped" \
       -d \
   '{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }"}'
   ```

1. Skapa en omsluten oformaterad fråga med cachekontroll.

   Till exempel:

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-max-age" \
       -d \
   '{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }", "cache-control": { "max-age": 300 }}'
   ```

1. Skapa en beständig fråga med parametrar:

   Till exempel:

   ```xml
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

1. Kör en fråga med parametrar.

   Till exempel:

   ```xml
   $ curl -X POST \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters;apath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"
   
   $ curl -X GET \
       "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters;apath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"
   ```

## Publicera en beständig fråga {#publish-persisted-query}

Beständiga frågor kan publiceras i en AEM-publiceringsmiljö där de kan begäras av klientprogram. Om du vill använda en beständig fråga vid publicering måste det relaterade beständiga trädet replikeras.

Det finns flera sätt att publicera en beständig fråga:

* **Använda en POST för replikering**:

   ```xml
   $ curl -X POST   http://localhost:4502/bin/replicate.json \
   -H 'authorization: Basic YWRtaW46YWRtaW4=' \
   -F path=/conf/wknd/settings/graphql/persistentQueries/plain-article-query \
   -F cmd=activate
   ```

* **Använda ett paket**:
   1. Skapa en ny paketdefinition.
   1. Inkludera konfigurationen (till exempel `/conf/wknd/settings/graphql/persistentQueries`).
   1. Bygg paketet.
   1. Replikera paketet.

* **Använda replikerings-/distributionsverktyg**:
   1. Gå till distributionsverktyget.
   1. Välj trädaktivering för konfigurationen (till exempel `/conf/wknd/settings/graphql/persistentQueries`).

* **Använda ett arbetsflöde (via konfiguration för att starta arbetsflöde)**:
   1. Definiera en startregel för arbetsflöde för att köra en arbetsflödesmodell som skulle återge konfigurationen för olika händelser (till exempel skapa, ändra).

När frågekonfigurationen publiceras gäller samma autentiseringsprinciper, bara med publiceringsslutpunkten.

>[!NOTE]
>
>För anonym åtkomst förutsätter systemet att åtkomstkontrollistan tillåter &quot;alla&quot; att ha åtkomst till frågekonfigurationen.
>
>Om så inte är fallet kommer det inte att kunna köras.

>[!NOTE]
>
>Alla semikolon (&quot;;&quot;) i URL:erna måste kodas.
>
>Som i begäran att köra en beständig fråga:
>
>
```xml
>curl -X GET \ "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters%3bapath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"
>```

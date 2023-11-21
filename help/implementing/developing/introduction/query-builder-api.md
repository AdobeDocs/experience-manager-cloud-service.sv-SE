---
title: Query Builder API
description: Funktionerna i Asset Share Query Builder visas via Java&trade; API och REST API.
exl-id: d5f22422-c9da-4c9d-b81c-ffa5ea7cdc87
source-git-commit: 8ed477ec0c54bb0913562b9581e699c0bdc973ec
workflow-type: tm+mt
source-wordcount: '2008'
ht-degree: 0%

---

# Query Builder API {#query-builder-api}

Med Query Builder kan du enkelt hämta innehåll från AEM. Funktionerna visas via ett Java™-API och ett REST-API. I det här dokumentet beskrivs dessa API:er.

Frågeverktyget på serversidan ([`QueryBuilder`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/QueryBuilder.html)) kan hantera en frågebeskrivning, skapa och köra en XPath-fråga, eventuellt filtrera resultatuppsättningen och även extrahera ansikten, om så önskas.

Frågebeskrivningen är helt enkelt en uppsättning predikat ([`Predicate`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/Predicate.html)). Exempel är ett fulltextpredikat, som motsvarar `jcr:contains()` i XPath.

För varje predikattyp finns det en utvärderingskomponent ([`PredicateEvaluator`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/eval/PredicateEvaluator.html)) som kan hantera det specifika predikatet för XPath, filtrering och facet-extrahering. Det är enkelt att skapa anpassade utvärderare, som kopplas in via OSGi-komponentkörningen.

REST API ger åtkomst till samma funktioner via HTTP med svar som skickas i JSON.

>[!NOTE]
>
>QueryBuilder-API:t byggs med JCR-API:t. Du kan även fråga AEM JCR genom att använda JCR-API:t i ett OSGi-paket. Mer information finns i [Fråga Adobe Experience Manager-data med JCR API](https://experienceleague.adobe.com/docs/experience-manager-65/developing/platform/query-builder/querybuilder-api.html).

## Gruppsession {#gem-session}

[AEM Gems](https://experienceleague.adobe.com/docs/events/experience-manager-gems-recordings/overview.html?lang=en) är en serie tekniska djupdykningar i Adobe Experience Manager som levereras av experter från Adobe.

Du kan [Granska sessionen som är dedikerad till frågebyggaren](https://experienceleague.adobe.com/docs/events/experience-manager-gems-recordings/gems2017/aem-search-forms-using-querybuilder.html?lang=en) om du vill se en översikt över och använda verktyget.

## Exempelfrågor {#sample-queries}

Dessa exempel anges i Java™-egenskapsformatsnotation. Om du vill använda dem med Java™ API:n använder du en Java™ `HashMap` som i följande API-exempel.

För `QueryBuilder` JSON Servlet innehåller varje exempel en exempellänk till en AEM (på standardplatsen, `http://<host>:<port>`). Logga in på AEM innan du använder länkarna.

>[!CAUTION]
>
>Som standard visas maximalt tio träffar i JSON-servleten för frågebyggaren.
>
>Om du lägger till följande parameter kan servleten visa alla frågeresultat:
>
>`p.limit=-1`

>[!NOTE]
>
>Om du vill visa returnerade JSON-data i webbläsaren kan du använda ett plugin-program som JSONView för Firefox.

### Returnera alla resultat {#returning-all-results}

Följande fråga **returnerar tio resultat** (eller för att vara exakt, max tio), men informerar dig om **Antal träffar:** som är tillgänglig:

`http://<host>:<port>/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=wknd/components/structure/page&1_property.operation=like&orderby=path`

```xml
path=/content
1_property=sling:resourceType
1_property.value=wknd/components/structure/page
1_property.operation=like
orderby=path
```

Samma fråga (med parametern `p.limit=-1`) **returnerar alla resultat** (det kan vara ett högt tal beroende på din instans):

`http://<host>:<port>/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=wknd/components/structure/page&1_property.operation=like&orderby=path&p.limit=-1`

```xml
path=/content
1_property=sling:resourceType
1_property.value=wknd/components/structure/page
1_property.operation=like
p.limit=-1
orderby=path
```

### Använda p.gissningssumma för att returnera resultat {#using-p-guesstotal-to-return-the-results}

Syftet med `p.guessTotal` parametern är att returnera rätt antal resultat som kan visas genom att kombinera minsta möjliga `p.offset` och `p.limit` värden. Fördelen med den här parametern är bättre prestanda med stora resultatuppsättningar. Med den här parametern undviker du också att beräkna hela summan (till exempel anropa `result.getSize()`) och att hela resultatmängden läses, optimeras ända ned till Oak-motorn och indexeras. Den här processen kan vara en stor skillnad när det finns hundratusentals resultat, både när det gäller körningstid och minnesanvändning.

Nackdelen med parametern är att användarna inte ser exakt summa. Men du kan ange ett minimiantal som `p.guessTotal=1000` så den alltid kan läsa upp till 1000. På så sätt får du exakta summor för mindre resultatuppsättningar, men om det är fler kan du bara visa &quot;och mer&quot;.

Lägg till `p.guessTotal=true` till frågan nedan för att se hur den fungerar:

`http://<host>:<port>/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=wknd/components/structure/page&1_property.operation=like&p.guessTotal=true&orderby=path`

```xml
path=/content
1_property=sling:resourceType
1_property.value=wknd/components/structure/page
1_property.operation=like
p.guessTotal=true
orderby=path
```

Frågan returnerar `p.limit` standard för `10` resultat med `0` offset:

```xml
"success": true,
"results": 10,
"total": 10,
"more": true,
"offset": 0,
```

Du kan också använda ett numeriskt värde för att räkna upp till ett anpassat antal maximala resultat. Använd samma fråga som ovan, men ändra värdet för `p.guessTotal` till `50`:

`http://<host>:<port>/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=wknd/components/structure/page&1_property.operation=like&p.guessTotal=50&orderby=path`

Den returnerar ett tal som är lika med standardgränsen på 10 resultat med förskjutningen 0, men visar bara maximalt 50 resultat:

```xml
"success": true,
"results": 10,
"total": 50,
"more": true,
"offset": 0,
```

### Implementera sidnumrering {#implementing-pagination}

Som standard ger Query Builder även antalet träffar. Beroende på den resulterande storleken kan det ta lång tid att fastställa det korrekta antalet genom att kontrollera alla resultat för åtkomstkontroll. För det mesta används summan för att implementera sidnumrering för slutanvändarens användargränssnitt. Eftersom det exakta antalet kan vara långsamt bör du använda funktionen gissningTotal för att implementera sidnumreringen.

Gränssnittet kan till exempel anpassa följande metod:

* Hämta och visa korrekt antal av totalt antal träffar ([SearchResult.getTotalMatches()](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/result/SearchResult.html#getTotalMatches) eller totalt i `querybuilder.json` svar) är mindre än eller lika med 100,
* Ange `guessTotal` till 100 anropar Query Builder.

* Svaret kan ha följande resultat:

   * `total=43`, `more=false` - Anger att det totala antalet träffar är 43. Gränssnittet kan visa upp till tio resultat som en del av den första sidan och ge sidnumrering för de kommande tre sidorna. Du kan också använda den här implementeringen för att visa en beskrivande text som **&quot;43 resultat hittades&quot;**.
   * `total=100`, `more=true` - Anger att det totala antalet träffar är större än 100 och att det exakta antalet inte är känt. Gränssnittet kan visas upp till tio som en del av den första sidan och sidnumreringen kan göras för de kommande tio sidorna. Du kan också använda den här funktionen för att visa text som **&quot;fler än 100 resultat hittades&quot;**. När användaren går till nästa sida kommer ett anrop till Query Builder att öka gränsen för `guessTotal` och även `offset` och `limit` parametrar.

Använd också `guessTotal` i de fall där användargränssnittet måste använda oändlig rullning för att undvika att Query Builder avgör det exakta träffantalet.

### Hitta burkfiler och beställ dem, senaste först {#find-jar-files-and-order-them-newest-first}

`http://<host>:<port>/bin/querybuilder.json?type=nt:file&nodename=*.jar&orderby=@jcr:content/jcr:lastModified&orderby.sort=desc`

```xml
type=nt:file
nodename=*.jar
orderby=@jcr:content/jcr:lastModified
orderby.sort=desc
```

### Sök efter alla sidor och sortera dem efter senast ändrade {#find-all-pages-and-order-them-by-last-modified}

`http://<host>:<port>/bin/querybuilder.json?type=cq:Page&orderby=@jcr:content/cq:lastModified`

```xml
type=cq:Page
orderby=@jcr:content/cq:lastModified
```

### Sök efter alla sidor och sortera dem efter senast ändrade, fallande {#find-all-pages-and-order-them-by-last-modified-but-descending}

`http://<host>:<port>/bin/querybuilder.json?type=cq:Page&orderby=@jcr:content/cq:lastModified&orderby.sort=desc`

```xml
type=cq:Page
orderby=@jcr:content/cq:lastModified
orderby.sort=desc
```

### Fulltextsökning, sorterad efter poäng {#fulltext-search-ordered-by-score}

`http://<host>:<port>/bin/querybuilder.json?fulltext=Management&orderby=@jcr:score&orderby.sort=desc`

```xml
fulltext=Management
orderby=@jcr:score
orderby.sort=desc
```

### Sök efter sidor med en viss tagg {#search-for-pages-tagged-with-a-certain-tag}

`http://<host>:<port>/bin/querybuilder.json?type=cq:Page&tagid=wknd:activity/cycling&tagid.property=jcr:content/cq:tags`

```xml
type=cq:Page
tagid=wknd:activity/cycling
tagid.property=jcr:content/cq:tags
```

Använd `tagid` som i exemplet om du känner till det explicita tagg-ID:t.

Använd `tag` förutse taggens titelsökväg (utan blanksteg).

I föregående exempel söker du efter sidor (`cq:Page` noder) använder du den relativa sökvägen från den noden för `tagid.property` predikat, vilket `jcr:content/cq:tags`. Som standard är `tagid.property` skulle vara `cq:tags`.

### Sök i flera banor (med grupper) {#search-under-multiple-paths-using-groups}

`http://<host>:<port>/bin/querybuilder.json?fulltext=Experience&group.1_path=/content/wknd/us/en/magazine&group.2_path=/content/wknd/us/en/adventures&group.p.or=true`

```xml
fulltext=Experience
group.p.or=true
group.1_path=/content/wknd/us/en/magazine
group.2_path=/content/wknd/us/en/adventures
```

Den här frågan använder en *grupp* (namngiven `group`), som används för att avgränsa deluttryck i en fråga, på samma sätt som parenteser gör i fler standardtecken. Den föregående frågan kan till exempel uttryckas i ett mer välbekant format som:

`"Experience" and ("/content/wknd/us/en/magazine" or "/content/wknd/us/en/adventures")`

Inuti gruppen i exemplet finns `path` predikatet används flera gånger. Om du vill differentiera och ordna de två instanserna av predikatet (ordningen krävs för vissa predikat) måste du prefix prefixet med `N_` där `N` är ordningsindex. I föregående exempel är resultatpredikaten `1_path` och `2_path`.

The `p` in `p.or` är en särskild avgränsare som anger att följande (i det här fallet en `or`) är *parameter* i gruppen, i motsats till ett underpredikt för gruppen, såsom `1_path`.

Om nej `p.or` anges, så sammanställs alla predikat med AND, vilket innebär att varje resultat måste uppfylla alla predikat.

>[!NOTE]
>
>Du kan inte använda samma numeriska prefix i en enda fråga, inte ens för olika predikat.

### Sök efter egenskaper {#search-for-properties}

Här söker du efter alla sidor i en viss mall med hjälp av `cq:template` egenskap:

`http://<host>:<port>/bin/querybuilder.json?property=cq%3atemplate&property.value=%2fconf%2fwknd%2fsettings%2fwcm%2ftemplates%2fadventure-page-template&type=cq%3aPageContent`

```xml
type=cq:PageContent
property=cq:template
property.value=/conf/wknd/settings/wcm/templates/adventure-page-template
```

Nackdelen är att `jcr:content` noder på sidorna, inte själva sidorna, returneras. Du kan lösa det här problemet genom att söka efter relativ sökväg:

`http://<host>:<port>/bin/querybuilder.json?property=jcr%3acontent%2fcq%3atemplate&property.value=%2fconf%2fwknd%2fsettings%2fwcm%2ftemplates%2fadventure-page-template&type=cq%3aPage`

```xml
type=cq:Page
property=jcr:content/cq:template
property.value=/conf/wknd/settings/wcm/templates/adventure-page-template
```

### Sök efter flera egenskaper {#search-for-multiple-properties}

När du använder egenskapspredikatet flera gånger måste du lägga till nummerprefixen igen:

`http://<host>:<port>/bin/querybuilder.json?1_property=jcr%3acontent%2fcq%3atemplate&1_property.value=%2fconf%2fwknd%2fsettings%2fwcm%2ftemplates%2fadventure-page-template&2_property=jcr%3acontent%2fjcr%3atitle&2_property.value=Cycling%20Tuscany&type=cq%3aPage`

```xml
type=cq:Page
1_property=jcr:content/cq:template
1_property.value=/conf/wknd/settings/wcm/templates/adventure-page-template
2_property=jcr:content/jcr:title
2_property.value=Cycling Tuscany
```

### Sök efter flera egenskapsvärden {#search-for-multiple-property-values}

Så här undviker du stora grupper när du vill söka efter flera värden för en egenskap (`"A" or "B" or "C"`) kan du ange flera värden för `property` predikat:

`http://<host>:<port>/bin/querybuilder.json?property=jcr%3atitle&property.1_value=Cycling%20Tuscany&property.2_value=Ski%20Touring&property.3_value=Whistler%20Mountain%20Biking`

```xml
property=jcr:title
property.1_value=Cycling Tuscany
property.2_value=Ski Touring
property.3_value=Whistler Mountain Biking
```

För flervärdesegenskaper kan du även kräva att flera värden matchar (`"A" and "B" and "C"`):

`http://<host>:<port>/bin/querybuilder.json?property=jcr%3atitle&property.and=true&property.1_value=Cycling%20Tuscany&property.2_value=Ski%20Touring&property.3_value=Whistler%20Mountain%20Biking`

```xml
property=jcr:title
property.and=true
property.1_value=Cycling Tuscany
property.2_value=Ski Touring
property.3_value=Whistler Mountain Biking
```

## Förfina vad som returneras {#refining-what-is-returned}

Som standard returnerar JSON-servern för QueryBuilder en standarduppsättning med egenskaper för varje nod i sökresultatet (till exempel sökväg, namn och titel). Du kan kontrollera vilka egenskaper som returneras genom att göra något av följande:

Ange

```xml
p.hits=full
```

I så fall inkluderas alla egenskaper för varje nod:

`http://<host>:<port>/bin/querybuilder.json?p.hits=full&property=jcr%3atitle&property.value=Cycling%20Tuscany`

```xml
property=jcr:title
property.value=Cycling Tuscany
p.hits=full
```

Använd

```xml
p.hits=selective
```

Och ange de egenskaper som du vill hämta in

```xml
p.properties
```

Separerat med ett blanksteg:

`http://<host>:<port>/bin/querybuilder.json?p.hits=selective&p.properties=sling%3aresourceType%20jcr%3aprimaryType&property=jcr%3atitle&property.value=Cycling%20Tuscany`

```xml
property=jcr:title
property.value=Cycling Tuscany
p.hits=selective
p.properties=sling:resourceType jcr:primaryType
```

En annan sak du kan göra är att inkludera underordnade noder i svaret i Query Builder. Ange

```xml
p.nodedepth=n
```

Plats `n` är antalet nivåer som du vill att frågan ska returnera. För att en underordnad nod ska kunna returneras måste den anges av egenskapsväljaren

```xml
p.hits=full
```

Exempel:

`http://<host>:<port>/bin/querybuilder.json?p.hits=full&p.nodedepth=5&property=jcr%3atitle&property.value=Cycling%20Tuscany`

```xml
property=jcr:title
property.value=Cycling Tuscany
p.hits=full
p.nodedepth=5
```

## Fler prognoser {#morepredicates}

Mer information om fler predikt finns i [Referenssida för Query Builder-prediktion](query-builder-predicates.md).

Du kan även kontrollera [Javadoc för `PredicateEvaluator` klasser](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/eval/PredicateEvaluator.html). Javadoc för dessa klasser innehåller en lista med egenskaper som du kan använda.

Klassnamnets prefix (till exempel `similar` in [`SimilarityPredicateEvaluator`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/eval/SimilarityPredicateEvaluator.html)) är *huvudegenskap* av klassen. Den här egenskapen är också namnet på predikatet som ska användas i frågan (i gemener).

För sådana huvudegenskaper kan du förkorta frågan och använda `similar=/content/en` i stället för den fullständigt kvalificerade varianten `similar.similar=/content/en`. Det fullständiga, kvalificerade formuläret måste användas för alla icke-huvudsakliga egenskaper i en klass.

## Exempel på API-användning för frågebyggaren {#example-query-builder-api-usage}

```java
   String fulltextSearchTerm = "WKND";

    // create query description as hash map (simplest way, same as form post)
    Map<String, String> map = new HashMap<String, String>();

// create query description as hash map (simplest way, same as form post)
    map.put("path", "/content");
    map.put("type", "cq:Page");
    map.put("group.p.or", "true"); // combine this group with OR
    map.put("group.1_fulltext", fulltextSearchTerm);
    map.put("group.1_fulltext.relPath", "jcr:content");
    map.put("group.2_fulltext", fulltextSearchTerm);
    map.put("group.2_fulltext.relPath", "jcr:content/@cq:tags");

    // can be done in map or with Query methods
    map.put("p.offset", "0"); // same as query.setStart(0) below
    map.put("p.limit", "20"); // same as query.setHitsPerPage(20) below

    Query query = builder.createQuery(PredicateGroup.create(map), session);
    query.setStart(0);
    query.setHitsPerPage(20);

    SearchResult result = query.getResult();

    // paging metadata
    int hitsPerPage = result.getHits().size(); // 20 (set above) or lower
    long totalMatches = result.getTotalMatches();
    long offset = result.getStartIndex();
    long numberOfPages = totalMatches / 20;

    //Place the results in XML to return to client
    DocumentBuilderFactory factory = DocumentBuilderFactory.newInstance();
    DocumentBuilder builder = factory.newDocumentBuilder();
    Document doc = builder.newDocument();

    //Start building the XML to pass back to the AEM client
    Element root = doc.createElement( "results" );
    doc.appendChild( root );

    // iterating over the results
    for (Hit hit : result.getHits()) {
       String path = hit.getPath();

      //Create a result element
      Element resultel = doc.createElement( "result" );
      root.appendChild( resultel );

      Element pathel = doc.createElement( "path" );
      pathel.appendChild( doc.createTextNode(path ) );
      resultel.appendChild( pathel );
    }
```

Samma fråga som körs över HTTP med JSON-servern (Query Builder):

`http://<host>:<port>/bin/querybuilder.json?path=/content&type=cq:Page&group.p.or=true&group.1_fulltext=WKND&group.1_fulltext.relPath=jcr:content&group.2_fulltext=WKND&group.2_fulltext.relPath=jcr:content/@cq:tags&p.offset=0&p.limit=20`

## Lagra och läsa in frågor {#storing-and-loading-queries}

Frågor kan lagras i databasen så att du kan använda dem senare. The `QueryBuilder` ger `storeQuery` metod med följande signatur:

```java
void storeQuery(Query query, String path, boolean createFile, Session session) throws RepositoryException, IOException;
```

När du använder [`QueryBuilder#storeQuery`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/QueryBuilder.html#storeQuery-com.day.cq.search.Query-java.lang.String-boolean-javax.jcr.Session-) metod, den givna `Query` lagras i databasen som en fil eller som en egenskap enligt `createFile` argumentvärde. I följande exempel visas hur du sparar en `Query` till banan `/mypath/getfiles` som en fil:

```java
builder.storeQuery(query, "/mypath/getfiles", true, session);
```

Tidigare lagrade frågor kan läsas in från databasen med [`QueryBuilder#loadQuery`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/QueryBuilder.html#loadQuery-java.lang.String-javax.jcr.Session-) metod:

```java
Query loadQuery(String path, Session session) throws RepositoryException, IOException
```

Till exempel en `Query` lagras i sökvägen `/mypath/getfiles` kan läsas in med följande kodfragment:

```java
Query loadedQuery = builder.loadQuery("/mypath/getfiles", session);
```

## Testning och felsökning {#testing-and-debugging}

Om du vill spela upp frågor runt och felsöka frågor i Frågebyggaren kan du använda felsökningskonsolen i Query Builder på

`http://<host>:<port>/libs/cq/search/content/querydebug.html`

Alternativt kan du använda JSON-servern Query Builder på

`http://<host>:<port>/bin/querybuilder.json?path=/tmp`

The `path=/tmp` är endast ett exempel.

### Allmän felsökning av Recommendations {#general-debugging-recommendations}

### Få förklarlig XPath via loggning {#obtain-explain-able-xpath-via-logging}

Förklara **alla** frågar under utvecklingscykeln mot målindexuppsättningen.

1. Aktivera DEBUG-loggar för QueryBuilder för att få underliggande, förklarlig XPath-fråga
   * Navigera till `https://<host>:<port>/system/console/slinglog`. Skapa en loggare för `com.day.cq.search.impl.builder.QueryImpl` på **FELSÖKNING**.
1. När DEBUG är aktiverat för ovanstående klass visar loggarna den XPath som genererats av Query Builder.
1. Kopiera XPath-frågan från loggposten för den associerade Query Builder-frågan, till exempel:
   * `com.day.cq.search.impl.builder.QueryImpl XPath query: /jcr:root/content//element(*, cq:Page)[(jcr:contains(jcr:content, "WKND") or jcr:contains(jcr:content/@cq:tags, "WKND"))]`
1. Klistra in XPath-frågan i Förklara fråga som XPath så att du kan hämta frågeplanen.

### Hämta förklarlig XPath via Felsökning i Query Builder {#obtain-explain-able-xpath-via-the-query-builder-debugger}

Använd felsökningsprogrammet AEM Query Builder för att generera en förklarlig XPath-fråga.

![Query Builder-felsökning](assets/query-builder-debugger.png)

1. Ange frågan i Query Builder i felsökningsprogrammet i Query Builder
1. Utför sökningen
1. Hämta genererad XPath
1. Klistra in XPath-frågan i XPath som XPath så att du kan hämta frågeplanen

>[!NOTE]
>
>Frågor som inte är Query Builder (XPath, JCR-SQL2) kan skickas direkt till Förklara fråga.

## Felsöka frågor med loggning {#debugging-queries-with-logging}

>[!NOTE]
>
>Loggarnas konfiguration beskrivs i dokumentet [Loggning](/help/implementing/developing/introduction/logging.md).

Loggutdata (INFO-nivå) för frågebyggarimplementeringen när frågan som beskrivs i föregående avsnitt körs [Testning och felsökning:](#testing-and-debugging)

```xml
com.day.cq.search.impl.builder.QueryImpl executing query (predicate tree):
null=group: limit=20, offset=0[
    {group=group: or=true[
        {1_fulltext=fulltext: fulltext=WKND, relPath=jcr:content}
        {2_fulltext=fulltext: fulltext=WKND, relPath=jcr:content/@cq:tags}
    ]}
    {path=path: path=/content}
    {type=type: type=cq:Page}
]
com.day.cq.search.impl.builder.QueryImpl XPath query: /jcr:root/content//element(*, cq:Page)[(jcr:contains(jcr:content, "WKND") or jcr:contains(jcr:content/@cq:tags, "WKND"))]
com.day.cq.search.impl.builder.QueryImpl no filtering predicates
com.day.cq.search.impl.builder.QueryImpl query execution took 69 ms
```

Om du har en fråga med prediktiva utvärderare som filtrerar eller som använder en anpassad ordning efter jämförelseoperatorn, beskrivs den i frågan:

```xml
com.day.cq.search.impl.builder.QueryImpl executing query (predicate tree):
null=group: [
    {nodename=nodename: nodename=*.jar}
    {orderby=orderby: orderby=@jcr:content/jcr:lastModified}
    {type=type: type=nt:file}
]
com.day.cq.search.impl.builder.QueryImpl custom order by comparator: jcr:content/jcr:lastModified
com.day.cq.search.impl.builder.QueryImpl XPath query: //element(*, nt:file)
com.day.cq.search.impl.builder.QueryImpl filtering predicates: {nodename=nodename: nodename=*.jar}
com.day.cq.search.impl.builder.QueryImpl query execution took 272 ms
```

## Javadoc-länkar {#javadoc-links}

| **Javadoc** | **Beskrivning** |
|---|---|
| [com.day.cq.search](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/package-summary.html) | Basic Query Builder och Query API |
| [com.day.cq.search.result](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/result/package-summary.html) | Resultat-API |
| [com.day.cq.search.facets](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/facets/package-summary.html) | Fasetter |
| [com.day.cq.search.facets.bufickor](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/facets/buckets/package-summary.html) | Bucklar (inneslutna i facets) |
| [com.day.cq.search.eval](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/eval/package-summary.html) | Förutse utvärderare |
| [com.day.cq.search.facets.extractor](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/facets/extractors/package-summary.html) | Fasettextraherare (för utvärderare) |
| [com.day.cq.search.writer](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/writer/package-summary.html) | JSON Result Hit Writer for Query Builder-serverlet (`/bin/querybuilder.json`) |

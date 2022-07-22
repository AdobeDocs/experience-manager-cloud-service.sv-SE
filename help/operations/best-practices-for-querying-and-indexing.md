---
title: Metodtips för frågor och indexering
seo-title: Best Practices for Queries and Indexing
description: Den här artikeln innehåller riktlinjer för hur du optimerar index och frågor.
seo-description: This article provides guidelines on how to optimize your indexes and queries.
topic-tags: best-practices
source-git-commit: 85cbdaa6e6d01856005cb47f289d391fb44bd65e
workflow-type: tm+mt
source-wordcount: '1573'
ht-degree: 0%

---


# Metodtips för frågor och indexering{#best-practices-for-queries-and-indexing}

Till skillnad från tidigare versioner i AEM as a Cloud Service automatiseras alla operativa aspekter av indexering. Detta gör att utvecklare kan fokusera på att skapa effektiva frågor och deras motsvarande indexdefinitioner.

## När frågor ska användas {#when-to-use-queries}

Frågor är ett sätt att få tillgång till innehåll, men inte den enda. Därför måste den utvärderas om frågor är det bästa och mest prestandavänliga sättet att få tillgång till innehåll. I många situationer kan innehåll i databasen nås på ett mer prestandaförbättrat sätt.

### Databas- och taxonomidesign {#repository-and-taxonomy-design}

När du utformar taxonomin för en databas måste flera faktorer beaktas. Dessa omfattar bland annat åtkomstkontroller, lokalisering, komponent- och sidegenskapsarv.

När du utformar en taxonomi som tar upp dessa problem är det också viktigt att tänka på hur&quot;genomskinlighet&quot; är i indexdesignen. I det här sammanhanget är möjligheten att gå igenom en taxonomi som gör att innehållet kan läsas på ett förutsägbart sätt baserat på dess sökväg. Detta ger ett mer prestandasystem som är enklare att underhålla än ett som kräver många frågor.

När du utformar en taxonomi är det dessutom viktigt att tänka på om det är viktigt att beställa. I de fall där explicit ordning inte krävs och ett stort antal noder på samma nivå förväntas, är det att föredra att använda en oordnad nodtyp som `sling:Folder` eller `oak:Unstructured`. Om det krävs en beställning `nt:unstructured` och `sling:OrderedFolder` skulle vara lämpligare.

### Frågor i komponenter {#queries-in-components}

Eftersom frågor kan vara en av de mer beskattningsbara åtgärder som utförs i ett AEM är det bra att undvika dem i dina komponenter. Om flera frågor körs varje gång en sida återges kan det ofta försämra systemets prestanda. Det finns två strategier som du kan använda för att undvika att köra frågor när du återger komponenter: **gå igenom noder** och **förhämta resultat**.

### Går igenom noder {#traversing-nodes}

Om databasen är utformad på ett sådant sätt att det går att på förhand känna till platsen för de data som krävs, kan kod som hämtar dessa data från de nödvändiga sökvägarna distribueras utan att behöva köra frågor för att hitta dem.

Ett exempel på detta är att återge innehåll som passar inom en viss kategori. Ett sätt är att ordna innehållet med en kategoriegenskap som kan efterfrågas för att fylla i en komponent som visar objekt i en kategori.

Ett bättre sätt är att strukturera innehållet i en taxonomi efter kategori så att det kan hämtas manuellt.

Om innehållet till exempel lagras i en taxonomi som liknar:

```xml
/content/myUnstructuredContent/parentCategory/childCategory/contentPiece
```

den `/content/myUnstructuredContent/parentCategory/childCategory` noden kan bara hämtas, dess underordnade noder kan tolkas och användas för att återge komponenten.

När du har att göra med en liten eller homogen resultatmängd kan det dessutom vara snabbare att gå igenom databasen och samla ihop de noder som behövs, i stället för att skapa en fråga som returnerar samma resultatmängd. Generellt sett bör frågor undvikas där det är möjligt att göra detta.

### Förhämtningsresultat {#prefetching-results}

Ibland tillåter inte innehållet eller kraven runt komponenten att nodgenomgång används som ett sätt att hämta nödvändiga data. I dessa fall måste de nödvändiga frågorna köras innan komponenten återges, så att optimala prestanda säkerställs.

Om de resultat som krävs för komponenten kan beräknas när den redigeras och det inte finns någon förväntad tid för att innehållet ska ändras, kan frågan köras när en ändring har gjorts.

Om data eller innehåll ändras regelbundet, kan frågan köras enligt ett schema eller via en avlyssnare för uppdateringar av underliggande data. Sedan kan resultaten skrivas till en delad plats i databasen. Alla komponenter som behöver dessa data kan sedan hämta värden från den här noden utan att behöva köra en fråga vid körning.
En liknande strategi kan användas för att behålla resultatet i en minnescache, som fylls i vid start och uppdateras när ändringar görs (med en JCR-observationsavlyssnare eller en Sling ResourceChangeListener).

## Optimera frågor {#optimizing-queries}

Oak-dokumentationen innehåller en [överblick över hur frågor körs](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#query-processing). Detta utgör grunden för alla optimeringsaktiviteter som beskrivs i det här dokumentet.

AEM som molntjänst har frågeprestandaverktyget som är utformat för att ge stöd åt implementering av effektiva frågor.
* Här visas redan utförda frågor med relevanta prestandaegenskaper och frågeplanen.
* Det gör att du kan utföra ad hoc-frågor på olika nivåer, från att bara visa frågeplanen tills den fullständiga frågan körs.

Det går att nå frågeprestandaverktyget via [Developer Console i Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console.html#queries). Till skillnad från prestandaverktyget Fråga i tidigare versioner av AEM 6.x, innehåller prestandafrågeverktyget för AEM as a Cloud Service mer information om frågekörningen, vilket är användbart för att förbättra en fråga.


Det allmänna sättet att använda verktyget Frågeprestanda för att optimera frågor beskrivs i det här diagrammet.
![Frågeoptimeringsflöde](assets/query-optimization-flow.png)



### Använda ett index {#use-an-index}

Alla frågor bör använda ett index för att ge optimala prestanda. I de flesta fall bör befintliga färdiga index vara tillräckliga för att hantera frågor.
Ibland måste anpassade egenskaper läggas till i ett befintligt index, så ytterligare begränsningar kan efterfrågas med detta index. Se [Innehållssökning och indexering](/help/operations/indexing.md#changing-an-index) för mer information. The [JCR-frågekarta](#jcr-query-cheatsheet) beskriver hur en egenskapsdefinition i ett index måste se ut att stödja en viss frågetyp.



### Använd rätt villkor

Den primära begränsningen för en fråga bör vara en egenskapsmatchning, eftersom detta är den mest effektiva typen. Om du lägger till fler egenskapsbegränsningar begränsas resultatet ytterligare.
Frågemotorn ser bara ett enda index. det innebär att ett befintligt index kan och bör anpassas genom att fler anpassade indexegenskaper läggs till i det.

The [JCR-frågekarta](#jcr-query-cheatsheet) visar de tillgängliga begränsningarna och även hur en indexdefinition måste se ut så att den plockas upp. Använd [Prestandaverktyg för fråga](#query-performance-tool) för att testa frågan och för att se till att rätt index används och att frågemotorn inte behöver utvärdera begränsningar utanför indexet.


### Beställning

Om en viss resultatordning begärs finns det två sätt för frågemotorn att uppnå detta:

1. Antingen kan indexet leverera resultatet helt och i rätt ordning, fungerar om de egenskaper som används för beställning kommenteras med ```ordered=true``` i indexdefinitionen.
2. Om Frågemotorn behöver utföra filtrering utanför indexet eller om egenskapen order inte är kommenterad med ```ordered=true``` -egenskapen utför även frågemotorn beställningsprocessen. I det här fallet måste hela resultatuppsättningen läsas i minnet för sortering, vilket är mycket långsammare än det första alternativet.





### Begränsa resultatstorleken

Den hämtade storleken på frågeresultatet är en viktig faktor för frågeprestanda. Eftersom resultatet hämtas på ett lat sätt är det skillnad på att bara hämta de första 20 resultaten jämfört med att hämta 10 000 resultat, både i körtid och minnesanvändning.

Det innebär också att storleken på resultatmängden bara kan bestämmas korrekt om alla resultat hämtas. Därför bör den hämtade resultatmängden alltid begränsas, antingen genom att frågan utökas (se [JCR-frågekarta](#jcr-query-cheatsheet) om du vill ha mer information) eller genom att begränsa resultatens läsningar.
En sådan gräns förhindrar även att frågemotorn hissar på **traversal limit** av 100 000 noder, vilket leder till att frågan måste stoppas.

Se avsnittet [Frågor med stora resultat](#queries-with-large-result-sets) nedan om en potentiellt stor resultatmängd måste behandlas fullständigt.


## JCR-frågekarta

För att skapa effektiva JCR-frågor och indexdefinitioner har [JCR Query Cheat Sheet](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/practices/best-practices-for-queries-and-indexing.html#jcrquerycheatsheet) finns att hämta och använda som referens under utvecklingen. Den innehåller exempelfrågor för QueryBuilder, XPath och SQL-2, som omfattar flera scenarier som beter sig på olika sätt när det gäller frågeprestanda. Här finns också rekommendationer för hur du skapar eller anpassar ekindexeringar. Innehållet i detta värmeblad gäller AEM 6.5 och AEM as a Cloud Service.


## Frågor med stora resultatuppsättningar

Du bör undvika frågor med en stor resultatuppsättning, men det finns giltiga fall där stora resultat måste behandlas. Resultatet är ofta okänt i förgrunden och därför bör man vidta vissa försiktighetsåtgärder för att göra bearbetningen tillförlitlig.

* frågan inte ska utföras inom en begäran, i stället ska frågan köras som en del av ett Sling-jobb eller ett AEM arbetsflöde. Dessa har inga begränsningar i den totala körtiden och startas om om instansen skulle gå ned under bearbetningen av frågan och dess resultat.
* För att komma förbi frågegränsen på 100 000 noder bör du överväga att använda [Sidnumrering av nyckeluppsättning](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Keyset_Pagination) och dela frågan i flera underfrågor.



## Fråga i databasen

Frågor som går igenom databasen använder inte ett index och loggar meddelanden enligt följande:

```text
28.06.2022 13:32:52.804 *WARN* [127.0.0.1 [1656415972414] POST /libs/settings/granite/operations/diagnosis/granite_queryperformance.explain.json HTTP/1.1] org.apache.jackrabbit.oak.plugins.index.Cursors$TraversingCursor Traversed 98000 nodes with filter Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a /* xpath: //* */, path=*) called by com.adobe.granite.queries.impl.explain.query.ExplainQueryServlet.getHeuristics; consider creating an index or changing the query
```

Det här loggfragmentet innehåller relevant information:

* själva frågan: ```//* ```
* den java-kod som utförde frågan: ```com.adobe.granite.queries.impl.explain.query.ExplainQueryServlet::getHeuristics```; detta hjälper till att identifiera vem som skapat frågan.

Med den här informationen är det möjligt att optimera frågan med hjälp av metoderna som beskrivs i [Optimera frågor](#optimizing-queries).
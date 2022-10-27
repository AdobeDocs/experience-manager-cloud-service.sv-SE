---
title: Predikatreferens för Query Builder
description: Predikatreferens för Query Builder API.
exl-id: 77118ef7-4d29-470d-9c4b-20537a408940
source-git-commit: 3c7e6d2213e059b1b8a90feea4672a4436873a01
workflow-type: tm+mt
source-wordcount: '2268'
ht-degree: 1%

---

# Predikatreferens för Query Builder {#query-builder-predicate-reference}

## Allmänt {#general}

### root {#root}

Detta är rotpredikatgruppen. Den har stöd för alla funktioner i en grupp och tillåter inställning av globala frågeparametrar.

Namnet &quot;root&quot; används aldrig i en fråga, det är underförstått.

#### Egenskaper {#properties-18}

* **`p.offset`** - tal som anger början på resultatsidan, dvs hur många objekt som ska hoppas över
* **`p.limit`** - siffra som anger sidstorleken
* **`p.guessTotal`** - rekommenderas: Undvik att beräkna det totala resultatet som kan vara kostsamt. antingen en siffra som anger den högsta summan att räkna upp till (t.ex. 1000, ett tal som ger användarna tillräckligt med feedback på grovstorleken och exakta tal för mindre resultat) eller `true` för att räkna endast upp till det minsta nödvändiga `p.offset` + `p.limit`
* **`p.excerpt`** - om inställt på `true`, inkludera utdrag av fullständig text i resultatet
* **`p.hits`** - (endast för JSON-servern) väljer du hur träffar skrivs som JSON, med dessa standardinställningar (utbyggbara via ResultHitWriter-tjänsten):
   * **`simple`** - minimala objekt som `path`, `title`, `lastmodified`, `excerpt` (om angivet)
   * **`full`** - sling JSON rendering av noden, med `jcr:path` som anger träffens sökväg: som standard visas bara de direkta egenskaperna för noden, inklusive ett djupare träd med `p.nodedepth=N`, med 0 avses hela det oändliga underträdet, add `p.acls=true` för att inkludera JCR-behörigheterna för den aktuella sessionen för det angivna resultatobjektet (mappningar: `create` = `add_node`, `modify` = `set_property`, `delete` = `remove`)
   * **`selective`** - endast egenskaper angivna i `p.properties`, som är ett blanksteg (använd `+` i URL:er) lista över relativa sökvägar, om den relativa sökvägen har ett djup `>1` dessa kommer att representeras som underordnade objekt, specialerbjudandet `jcr:path` egenskapen innehåller sökvägen till träffen

### grupp {#group}

Det här predikatet gör det möjligt att bygga kapslade villkor. Grupper kan innehålla kapslade grupper. Allt i en Query Builder-fråga ingår implicit i en rotgrupp som kan ha `p.or` och `p.not` parametrar också.

Följande är ett exempel på matchning av en av två egenskaper mot ett värde:

```text
group.p.or=true
group.1_property=jcr:title
group.1_property.value=My Page
group.2_property=navTitle
group.2_property.value=My Page
```

Detta är begreppsmässigt `(1_property` ELLER `2_property)`.

Följande är ett exempel för kapslade grupper:

```text
fulltext=Management
group.p.or=true
group.1_group.path=/content/wknd/ch/de
group.1_group.type=cq:Page
group.2_group.path=/content/dam/wknd
group.2_group.type=dam:Asset
```

Detta söker efter termen **Förvaltning** på sidor i `/content/wknd/ch/de` eller i tillgångar i `/content/dam/wknd`.

Detta är begreppsmässigt `fulltext AND ( (path AND type) OR (path AND type) )`. Observera att sådana OR-kopplingar behöver bra index av prestandaskäl.

#### Egenskaper {#properties-6}

* **`p.or`** - om inställt på `true`måste bara ett predikat i gruppen matcha. Standardvärdet är `false`, vilket innebär att alla måste matcha
* **`p.not`** - om inställt på `true`negeras gruppen (standardvärdet är `false`)
* **`<predicate>`** - lägger till kapslade predikat
* **`N_<predicate>`** - lägger till flera kapslade predikat samtidigt, som `1_property, 2_property, ...`

### orderby {#orderby}

Med det här predikatet kan du sortera resultaten. Om det krävs en ordning med flera egenskaper måste det här prefixet läggas till flera gånger med hjälp av talprefixet, till exempel `1_orderby=first`, `2_oderby=second`.

#### Egenskaper {#properties-13}

* **`orderby`** - antingen JCR-egenskapsnamnet som anges av radavståndet @, till exempel `@jcr:lastModified` eller `@jcr:content/jcr:title`eller ett annat predikat i frågan, till exempel `2_property`som sorteringen ska göras på
* **`sort`** - sorteringsriktning, antingen `desc` för fallande eller `asc` för stigande (standard)
* **`case`** - om inställt på `ignore` gör sorteringsskiftläget okänsligt, vilket betyder `a` kommer före `B`; om den är tom eller utelämnad är sorteringen skiftlägeskänslig, vilket betyder `B` kommer före `a`

## Predikat {#predicates}

### boolproperty {#boolproperty}

Det här predikatet matchar JCR-booleska egenskaper. Accepterar endast värdena `true` och `false`. Om `false`matchar den om egenskapen har värdet `false` eller om den inte finns alls. Detta kan vara användbart för att kontrollera om det finns booleska flaggor som bara är inställda när de är aktiverade.

Den ärvda `operation` parametern har ingen betydelse.

Det här predikatet har stöd för facetextrahering och erbjuder bucket för varje `true` eller `false` värde, men bara för befintliga egenskaper.

#### Egenskaper {#properties}

* **`boolproperty`** - relativ sökväg till egenskap, till exempel `myFeatureEnabled` eller `jcr:content/myFeatureEnabled`
* **`value`** - värde för att kontrollera egenskapen för `true` eller `false`

### innehållfragment {#contentfragment}

Detta predikat begränsar resultatet till innehållsfragment.

* Det stöder inte filtrering.
* Det stöder inte facetextrahering.

#### Egenskaper {#properties-1}

* **`contentfragment`** - Den kan användas med vilket värde som helst för att kontrollera om det finns innehållsfragment.

### `dateComparison` {#datecomparison}

Detta predikat jämför två JCR-datumegenskaper med varandra. Kan testa om de är lika, olika, större än eller större än eller lika med.

Detta är ett predikat som bara kan filtreras och kan inte utnyttja ett sökindex.

#### Egenskaper {#properties-2}

* **`property1`** - path to first date property
* **`property2`** - egenskapen path to second date
* **`operation`**
   * `=` för exakt matchning (standard)
   * `!=` för jämförelser av olikhet
   * `>` for `property1` större än `property2`
   * `>=` for `property1` större än eller lika med `property2`

### daterange {#daterange}

Detta predikat matchar JCR-datumegenskaper mot ett datum-/tidsintervall. Detta använder ISO8601-formatet för datum och tider (`YYYY-MM-DDTHH:mm:ss.SSSZ`) och tillåter även partiella representationer, som `YYYY-MM-DD`. Alternativt kan tidsstämpeln anges som POSIX-tid.

Du kan söka efter vad som helst mellan två tidsstämplar, vad som helst nyare eller äldre än ett visst datum, och du kan även välja mellan inkluderande och öppna intervall.

Den har stöd för ansiktsextrahering och ger bucklor `today`, `this week`, `this month`, `last 3 months`, `this year`, `last year`och `earlier than last year`.

Det stöder inte filtrering.

#### Egenskaper {#properties-3}

* **`property`** - relativ sökväg till en `DATE` egenskap, till exempel `jcr:lastModified`
* **`lowerBound`** - nedre gräns för att kontrollera egenskap, till exempel `2014-10-01`
* **`lowerOperation`** - `>` (nyare) eller `>=` (på eller nyare), gäller för `lowerBound`. Standardvärdet är `>`
* **`upperBound`** - övre gräns för att kontrollera egenskap för, till exempel `2014-10-01T12:15:00`
* **`upperOperation`** - `<` (äldre) eller `<=` (på eller tidigare) gäller för `upperBound`. Standardvärdet är `<`
* **`timeZone`** - ID för den tidszon som ska användas när den inte anges som en ISO-8601-datumsträng. Standardvärdet är systemets standardtidszon.

### exkluderingsdjup {#excludepaths}

Detta predikat utesluter noder från resultatet där deras sökväg matchar ett reguljärt uttryck.

Detta är ett predikat som bara kan filtreras och kan inte utnyttja ett sökindex.

Det stöder inte facetextrahering.

#### Egenskaper {#properties-4}

* **`excludepaths`** - reguljära uttryck som matchas mot resultatsökvägar, utan matchande sökvägar från resultatet.

### fulltext {#fulltext}

Det här predikatet söker efter termer i fulltextindexet.

Det stöder inte filtrering.

Det stöder inte facetextrahering.

#### Egenskaper {#properties-5}

* **`fulltext`** - fulltextsöktermer
* **`relPath`** - den relativa sökvägen som ska sökas i egenskapen eller undernoden. Den här egenskapen är valfri.

### hasPermission {#haspermission}

Detta predikat begränsar resultatet till objekt där den aktuella sessionen har den angivna [JCR-behörighet.](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html#16.2.3%20Standard%20Privileges)

Detta är ett predikat som bara kan filtreras och kan inte utnyttja ett sökindex. Det stöder inte facetextrahering.

#### Egenskaper {#properties-7}

* **`hasPermission`** - kommaavgränsade JCR-behörigheter som den aktuella användarsessionen måste ha för noden i fråga. till exempel `jcr:write`, `jcr:modifyAccessControl`

### language {#language}

Det här predikatet hittar AEM sidor på ett visst språk. Det här tittar både på sidspråksegenskapen och sidsökvägen, som ofta innehåller språket eller språket i en webbplatsstruktur på den översta nivån.

Detta är ett predikat som bara kan filtreras och kan inte utnyttja ett sökindex.

Programmet har stöd för facetextrahering och innehåller hinkar för varje unik språkkod.

#### Egenskaper {#properties-8}

* **`language`** - ISO-språkkod, till exempel `de`

### huvudtillgång {#mainasset}

Detta predikat kontrollerar om en nod är en DAM-huvudresurs och inte en underresurs. Detta är i stort sett alla noder som inte finns i en underresursnod. Observera att detta inte kontrollerar `dam:Asset` nodtyp. Om du vill använda det här predikatet anger du bara `mainasset=true` eller `mainasset=false`. Det finns inga fler egenskaper.

Detta är ett predikat som bara kan filtreras och kan inte utnyttja ett sökindex.

Det stöder facet-extrahering och erbjuder två buffertar för huvud- och delresurser.

#### Egenskaper {#properties-9}

* **`mainasset`** - boolesk, `true` för huvudtillgångar, `false` för deltillgångar

### medlemOf {#memberof}

Det här predikatet hittar objekt som är medlemmar av en viss [resursinsamling för sling](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/resource/collection/ResourceCollection.html).

Detta är ett predikat som bara kan filtreras och kan inte utnyttja ett sökindex.

Det stöder inte facetextrahering.

#### Egenskaper {#properties-10}

* **`memberOf`** - sökväg till Sling-resurssamling

### nodename {#nodename}

Detta predikat matchar JCR-nodnamn.

Det har stöd för facet-extrahering och innehåller bucket för varje unikt nodnamn (filnamn).

#### Egenskaper {#properties-11}

* **`nodename`** - nodnamnsmönster som tillåter jokertecken: `*` = ett eller inga tecken, `?` = any char, `[abc]` = endast tecken inom hakparentes

### inte utgånget {#notexpired}

Detta predikat matchar objekt genom att kontrollera om en JCR-datumegenskap är större eller lika med den aktuella servertiden. Detta kan användas för att kontrollera en `expiresAt` Endast de som ännu inte har gått ut (`notexpired=true`) eller som redan har gått ut (`notexpired=false`).

Det stöder inte filtrering.

Det stöder extrahering av ansikten på samma sätt som [`daterange`](#daterange) förutsäga.

#### Egenskaper {#properties-12}

* **`notexpired`** - boolesk, `true` för ännu ej utgången (datum i framtiden eller lika med), `false` för utgången (tidigare datum) (obligatoriskt)
* **`property`** - relativ sökväg till `DATE` egenskap som ska kontrolleras (obligatoriskt)

### path {#path}

Det här predikatet söker i en angiven sökväg.

Det stöder inte facetextrahering.

#### Egenskaper {#properties-14}

* **`path`** - Detta definierar banmönstret.
   * Beroende på `exact` egenskapen matchar antingen hela underträdet (som att lägga till `//*` i xpath, men observera att detta inte inkluderar basbanan) eller bara en exakt sökvägsmatchning, som kan innehålla jokertecken (`*`).
      * Standardvärdet är `true`

<!---   * If the `self`property is set, the entire subtree including the base node will be searched.--->
* **`exact`** - if `exact` är `true`måste den exakta sökvägen matcha, men den kan innehålla enkla jokertecken (`*`), som matchar namn, men inte `/`; om det `false` (standard) alla underordnade inkluderas (valfritt)
* **`flat`** - söker endast efter direkt underordnade (som att lägga till `/*` in xpath) (används endast om `exact` är inte true, valfritt)
* **`self`** - söker i underträdet men inkluderar basnoden som angetts som sökväg (inga jokertecken).
   * *Viktigt*: Ett problem har identifierats med `self` -egenskapen i den aktuella implementeringen av querybuilder och användningen av den i frågor kanske inte ger rätt sökresultat. Ändra den aktuella implementeringen av `self` Egenskapen är inte heller möjlig eftersom den kan bryta mot befintliga program som förlitar sig på den. På grund av detta `self` egenskapen har tagits bort och du bör undvika att använda den.

### property {#property}

Detta predikat matchar JCR-egenskaperna och deras värden.

Det har stöd för facetextrahering och innehåller bucket för varje unikt egenskapsvärde i resultatet.

#### Egenskaper {#properties-15}

* **`property`** - relativ sökväg till egenskap, till exempel `jcr:title`
* **`value`** - värde för att kontrollera egenskapen; följer egenskapstypen JCR till strängkonverteringar
* **`N_value`** - användning `1_value`, `2_value`, ... för att kontrollera om det finns flera värden (i kombination med `OR` som standard, med `AND` if `and=true`)
* **`and`** - ställs in på `true` för att kombinera flera värden (`N_value`) med `AND`
* **`operation`**
   * `equals` för exakt matchning (standard)
   * `unequals` för jämförelser av olikhet
   * `like` för att använda `jcr:like` xpath-funktion (valfri)
   * `not` för ingen matchning (till exempel `not(@prop)` in xpath, value param will be ignore)
   * `exists` för existenskontroll
      * `true` egenskapen måste finnas
      * `false` är samma som `not` och är standard
* **`depth`** - antalet jokernivåer under vilka egenskapen/den relativa sökvägen kan finnas (t.ex. `property=size depth=2` kommer att kontrollera `node/size`, `node/*/size` och `node/*/*/size`)

### rangegenskap {#rangeproperty}

Detta predikat matchar en JCR-egenskap mot ett intervall. Detta gäller egenskaper med linjär typ som `LONG`, `DOUBLE` och `DECIMAL`. För `DATE` se [`daterange`](#daterange) som har optimerade indata för datumformat.

Du kan definiera en nedre gräns, en övre gräns eller båda. Åtgärden (t.ex. mindre än eller lika med) kan också anges separat för den nedre och övre gränsen.

Det stöder inte facetextrahering.

#### Egenskaper {#properties-16}

* **`property`** - relativ sökväg till egenskap
* **`lowerBound`** - nedre gräns för check-egenskap
* **`lowerOperation`** - `>` (standard) eller `>=`gäller för `lowerValue`
* **`upperBound`** - övre gräns för check-egenskap
* **`upperOperation`** - `<` (standard) eller `<=`gäller för `lowerValue`
* **`decimal`** - `true` om egenskapen checked är av typen Decimal

### relativ {#relativedaterange}

Detta predikat matchar `JCR DATE` egenskaper mot ett datum/tidsintervall med tidsförskjutningar i förhållande till den aktuella servertiden. Du kan ange `lowerBound` och `upperBound` med ett millisekundvärde eller Bugzilla-syntaxen `1s 2m 3h 4d 5w 6M 7y` (en sekund, två minuter, tre timmar, fyra dagar, fem veckor, sex månader, sju år). Prefix med `-` om du vill ange en negativ förskjutning före den aktuella tiden. Om du bara anger `lowerBound` eller `upperBound`blir den andra standardvärdet `0`, som representerar aktuell tid.

Till exempel:

* `upperBound=1h` (och nej) `lowerBound`) markerar allt under nästa timme
* `lowerBound=-1d` (och nej) `upperBound`) markerar något de senaste 24 timmarna
* `lowerBound=-6M` och `upperBound=-3M` väljer något under de senaste 3 till 6 månaderna
* `lowerBound=-1500` och `upperBound=5500` väljer något mellan 1 500 millisekunder och 5 500 millisekunder i framtiden
* `lowerBound=1d` och `upperBound=2d` markerar allt i övermorgon

Observera att programmet inte tar hänsyn till skottår och att alla månader är 30 dagar.

Det stöder inte filtrering.

Det stöder extrahering av ansikten på samma sätt som [`daterange`](#daterange) förutsäga.

#### Egenskaper {#properties-17}

* **`upperBound`** - övre gräns för datum i millisekunder eller `1s 2m 3h 4d 5w 6M 7y` (en sekund, två minuter, tre timmar, fyra dagar, fem veckor, sex månader, sju år) i förhållande till aktuell servertid, använd `-` för negativ förskjutning
* **`lowerBound`** - undre gräns för datum i millisekunder eller `1s 2m 3h 4d 5w 6M 7y` (en sekund, två minuter, tre timmar, fyra dagar, fem veckor, sex månader, sju år) i förhållande till aktuell servertid, använd `-` för negativ förskjutning

### sparad fråga {#savedquery}

Detta predikat inkluderar alla predikat för en beständig Query Builder-fråga i den aktuella frågan som ett undergruppsprediat.

Observera att detta inte kör en extra fråga utan utökar den aktuella frågan.

Frågor kan sparas programmatiskt med `QueryBuilder#storeQuery()`. Formatet kan vara en flerradig `String` egenskap eller `nt:file` nod som innehåller frågan som en textfil i Java-egenskapsformat.

Det stöder inte facetextrahering för predikaten i den sparade frågan.

#### Egenskaper {#properties-19}

* **`savedquery`** - sökväg till den sparade frågan (`String` egenskap eller `nt:file` nod)

### liknande {#similar}

Det här predikatet är en likhetssökning som använder JCR XPath:s `rep:similar()`.

Det stöder inte filtrering och inte facetextrahering.

#### Egenskaper {#properties-20}

* **`similar`** - absolut sökväg till noden där liknande noder ska hittas
* **`local`** - en relativ sökväg till en underordnad nod eller `.` för den aktuella noden (valfritt) är standard `.`)

### tag {#tag}

Det här predikatet söker efter innehåll som taggats med en eller flera taggar genom att ange sökvägar för taggtiteln.

Det har stöd för facet-extrahering och tillhandahåller bucket för varje unik tagg med hjälp av deras aktuella namnsökväg.

#### Egenskaper {#properties-21}

* **`tag`** - taggens titelsökväg att söka efter, till exempel `properties:orientation/landscape`
* **`N_value`** - användning `1_value`, `2_value`, ... att söka efter flera taggar (i kombination med `OR` som standard, med `AND` if `and=true`)
* **`property`** - egenskap (eller relativ sökväg till egenskap) att titta på (standard) `cq:tags`)

### tagid {#tagid}

Det här predikatet söker efter innehåll som taggats med en eller flera taggar genom att ange tagg-ID:n.

Det har stöd för facet-extrahering och tillhandahåller bucket för varje unik tagg med hjälp av deras aktuella tagg-ID.

#### Egenskaper {#properties-22}

* **`tagid`** - tagg-ID att söka efter, till exempel `properties:orientation/landscape`
* **`N_value`** - användning `1_value`, `2_value`, ... att söka efter flera tagg-ID:n (i kombination med `OR` som standard, med `AND` if `and=true`)
* **`property`** - egenskap (eller relativ sökväg till egenskap) att titta på (standard) `cq:tags`)

### tagsearch {#tagsearch}

Det här predikatet söker efter innehåll som taggats med en eller flera taggar genom att ange nyckelord. Då söker du först efter taggar som innehåller dessa nyckelord i deras titlar och begränsar sedan resultatet till enbart objekt som taggats med dessa.

Det stöder inte facetextrahering.

#### Egenskaper {#Properties-1}

* **`tagsearch`** - nyckelord att söka efter i taggtitlar
* **`property`** - egenskap (eller relativ sökväg till egenskap) som ska övervägas (standard) `cq:tags`)
* **`lang`** - om du bara vill söka i en viss lokaliserad taggtitel (till exempel `de`)
* **`all`** - booleskt värde om du vill söka efter hela taggens fulltext, dvs. alla titlar, beskrivning osv. (har företräde framför `lang`)

### type {#type}

Detta predikat begränsar resultatet till en viss JCR-nodtyp, både primära nodtyper och mixin-typer. Detta söker även efter undertyper av den nodtypen. Observera att databasens sökindex måste omfatta nodtyperna för effektiv körning.

Det har stöd för facetextrahering och innehåller bucket för varje unik typ i resultatet.

#### Egenskaper {#Properties-2}

* **`type`** - nodtyp eller blandnamn att söka efter, till exempel `cq:Page`

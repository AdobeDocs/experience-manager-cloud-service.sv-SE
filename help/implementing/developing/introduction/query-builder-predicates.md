---
title: Predikatreferens för Query Builder
description: Förutse referens för Query Builder API på AEM as a Cloud Service.
exl-id: 77118ef7-4d29-470d-9c4b-20537a408940
source-git-commit: 2d4ffd5518d671a55e45a1ab6f1fc41ac021fd80
workflow-type: tm+mt
source-wordcount: '2270'
ht-degree: 0%

---

# Predikatreferens för Query Builder {#query-builder-predicate-reference}

## Allmänt {#general}

### root {#root}

Rotpredikatgruppen. Den stöder alla funktioner i en grupp och tillåter inställning av globala frågeparametrar.

Namnet&quot;root&quot; används aldrig i en fråga, utan är implicit.

#### Egenskaper {#properties-18}

* **`p.offset`** - ett tal som anger början på resultatsidan, det vill säga hur många objekt som ska hoppas över.
* **`p.limit`** - ett tal som anger sidstorleken.
* **`p.guessTotal`** - rekommenderas: undvik att beräkna det totala resultatet, vilket kan vara kostsamt. Antingen en siffra som anger den högsta summan som ska räknas upp till (till exempel 1 000, ett tal som ger användarna tillräckligt med feedback på grovstorleken och exakta tal för mindre resultat). Eller `true` för att räkna endast upp till det minsta nödvändiga `p.offset` + `p.limit`.
* **`p.excerpt`** - om inställt på `true`, inkludera utdrag av fullständig text i resultatet.
* **`p.indexTag`** - om den anges kommer att innehålla ett alternativ för indextagg i frågan (se [Indextagg för frågealternativ](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#query-option-index-tag)).
* **`p.facetStrategy`** - om inställt på `oak`kommer Query Builder att delegera facetextraheringen till Oak (se [Fasetter](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#facets)).
* **`p.hits`** - (endast för JSON-servleten) väljer du hur träffar skrivs som JSON, med dessa standardträffar (utbyggbara med hjälp av tjänsten ResultHitWriter).
   * **`simple`** - minimala objekt som `path`, `title`, `lastmodified`, `excerpt` (om angivet).
   * **`full`** - sling JSON rendering av noden, med `jcr:path` som anger träffens sökväg. Som standard listas bara nodens direkta egenskaper, inklusive ett djupare träd med `p.nodedepth=N`, med 0 betyder hela det oändliga underträdet. Lägg till `p.acls=true` för att inkludera JCR-behörigheterna för den aktuella sessionen för det angivna resultatobjektet (mappningar: `create` = `add_node`, `modify` = `set_property`, `delete` = `remove`).
   * **`selective`** - endast egenskaper som anges i `p.properties`, som är en blankstegsavgränsad (använd `+` i URL:er) lista över relativa sökvägar. Om den relativa sökvägen har ett djup `>1`, representeras dessa egenskaper som underordnade objekt. Specialtecknet `jcr:path` -egenskapen innehåller träffens sökväg.

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

Konceptuellt är det `(1_property` ELLER `2_property)`.

Följande är ett exempel för kapslade grupper:

```text
fulltext=Management
group.p.or=true
group.1_group.path=/content/wknd/ch/de
group.1_group.type=cq:Page
group.2_group.path=/content/dam/wknd
group.2_group.type=dam:Asset
```

Söker efter termen **Förvaltning** på sidor i `/content/wknd/ch/de` eller i tillgångar i `/content/dam/wknd`.

Konceptuellt är det `fulltext AND ( (path AND type) OR (path AND type) )`. Sådana OR-kopplingar behöver bra index av prestandaskäl.

#### Egenskaper {#properties-6}

* **`p.or`** - om inställt på `true`måste bara ett predikat i gruppen matcha. Standardvärdet är `false`, vilket innebär att alla måste matcha
* **`p.not`** - om inställt på `true`negeras gruppen (standardvärdet är `false`)
* **`<predicate>`** - lägger till kapslade predikat
* **`N_<predicate>`** - lägger till flera kapslade predikat samtidigt, som `1_property, 2_property, ...`

### orderby {#orderby}

Med det här predikatet kan du sortera resultaten. Om det krävs en ordning efter flera egenskaper måste predikatet läggas till flera gånger med talprefixet, till exempel `1_orderby=first`, `2_oderby=second`.

#### Egenskaper {#properties-13}

* **`orderby`** - antingen JCR-egenskapsnamnet som anges av ett radavstånd @, till exempel `@jcr:lastModified` eller `@jcr:content/jcr:title`eller ett annat predikat i frågan, till exempel `2_property`, som sorteringen ska göras på
* **`sort`** - sorteringsriktning, antingen `desc` för fallande eller `asc` för stigande (standard)
* **`case`** - om inställt på `ignore`, vilket gör sorteringsskiftläget okänsligt, vilket betyder `a` kommer före `B`Om den är tom eller utelämnad är sorteringen skiftlägeskänslig, vilket betyder `B` kommer före `a`

## Predikat {#predicates}

### boolproperty {#boolproperty}

Detta predikat matchar JCR-booleska egenskaper. Accepterar endast värdena `true` och `false`. Om värdet är `false`matchar det om egenskapen har värdet `false`eller om den inte finns alls. Det här predikatet är användbart för att kontrollera om det finns booleska flaggor som bara är inställda när de är aktiverade.

Den ärvda `operation` parametern har ingen betydelse.

Det här predikatet har stöd för facetextrahering och erbjuder bucket för varje `true` eller `false` värde, men bara för befintliga egenskaper.

#### Egenskaper {#properties}

* **`boolproperty`** - relativ sökväg till egenskapen, till exempel `myFeatureEnabled` eller `jcr:content/myFeatureEnabled`
* **`value`** - värde för att kontrollera egenskapen för `true` eller `false`

### innehållfragment {#contentfragment}

Detta predikat begränsar resultatet till innehållsfragment.

* Det stöder inte filtrering.
* Det stöder inte facetextrahering.

#### Egenskaper {#properties-1}

* **`contentfragment`** - Den kan användas med vilket värde som helst för att kontrollera om det finns innehållsfragment.

### `dateComparison` {#datecomparison}

Detta predikat jämför två JCR-datumegenskaper med varandra. Kan testa om de är lika, olika, större än eller större än eller lika med.

Ett predikat som bara kan filtreras och som inte kan använda ett sökindex.

#### Egenskaper {#properties-2}

* **`property1`** - path to first date property
* **`property2`** - egenskapen path to second date
* **`operation`**
   * `=` för exakt matchning (standard)
   * `!=` för jämförelser av olikhet
   * `>` for `property1` större än `property2`
   * `>=` for `property1` större än eller lika med `property2`

### daterange {#daterange}

Detta predikat matchar JCR-datumegenskaper mot ett datum-/tidsintervall. Använder ISO8601-formatet för datum och tider (`YYYY-MM-DDTHH:mm:ss.SSSZ`) och tillåter även partiella representationer, som `YYYY-MM-DD`. Alternativt kan tidsstämpeln anges som POSIX-tid.

Du kan söka efter vad som helst mellan två tidsstämplar, vad som helst nyare eller äldre än ett visst datum, och du kan även välja mellan inkluderande och öppna intervall.

Den har stöd för ansiktsextrahering och ger bucklor `today`, `this week`, `this month`, `last 3 months`, `this year`, `last year`och `earlier than last year`.

Det stöder inte filtrering.

#### Egenskaper {#properties-3}

* **`property`** - relativ sökväg till en `DATE` egenskap, till exempel `jcr:lastModified`
* **`lowerBound`** - nedre gräns för att kontrollera egenskapen för exempelvis `2014-10-01`
* **`lowerOperation`** - `>` (nyare) eller `>=` (på eller nyare), gäller för `lowerBound`. Standardvärdet är `>`
* **`upperBound`** - övre gräns för att kontrollera egenskap för, till exempel `2014-10-01T12:15:00`
* **`upperOperation`** - `<` (äldre) eller `<=` (på eller tidigare) gäller för `upperBound`. Standardvärdet är `<`
* **`timeZone`** - ID för den tidszon som ska användas när den inte anges som en ISO-8601-datumsträng. Standardvärdet är systemets standardtidszon.

### exkluderingar {#excludepaths}

Detta predikat utesluter noder från resultatet där deras sökväg matchar ett reguljärt uttryck.

Ett predikat som bara kan filtreras och som inte kan använda ett sökindex.

Det stöder inte facetextrahering.

#### Egenskaper {#properties-4}

* **`excludepaths`** - reguljära uttryck som matchas mot resultatsökvägar, utan matchande sökvägar från resultatet.

### fulltext {#fulltext}

Söker efter termer i fulltextindexet.

Det stöder inte filtrering.

Det stöder inte facetextrahering.

#### Egenskaper {#properties-5}

* **`fulltext`** - fulltextsöktermer
* **`relPath`** - den relativa sökvägen som ska sökas i egenskapen eller undernoden. Den här egenskapen är valfri.

### hasPermission {#haspermission}

Detta predikat begränsar resultatet till objekt där den aktuella sessionen har den angivna [JCR-behörighet.](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html#16.2.3%20Standard%20Privileges)

Ett predikat som bara kan filtreras och som inte kan använda ett sökindex. Det stöder inte facetextrahering.

#### Egenskaper {#properties-7}

* **`hasPermission`** - alla kommaavgränsade JCR-behörigheter som den aktuella användarsessionen måste ha för noden i fråga. Till exempel: `jcr:write`, `jcr:modifyAccessControl`

### språk {#language}

Det här predikatet hittar AEM sidor på ett visst språk. Den tittar både på sidspråksegenskapen och sidsökvägen, som ofta innehåller språket eller språkinställningen i en webbplatsstruktur på den översta nivån.

Ett predikat som bara kan filtreras och som inte kan använda ett sökindex.

Programmet har stöd för facetextrahering och innehåller hinkar för varje unik språkkod.

#### Egenskaper {#properties-8}

* **`language`** - ISO-språkkod, till exempel `de`

### huvudtillgång {#mainasset}

Detta predikat kontrollerar om en nod är en DAM-huvudresurs och inte en underresurs. Det är i stort sett alla noder som inte finns i en underresursnod. Den söker inte efter `dam:Asset` nodtyp. Om du vill använda predikatet anger du `mainasset=true` eller `mainasset=false`. Det finns inga fler egenskaper.

Ett predikat som bara kan filtreras och som inte kan använda ett sökindex.

Det stöder facet-extrahering och erbjuder två buffertar för huvud- och delresurser.

#### Egenskaper {#properties-9}

* **`mainasset`** - boolesk, `true` för huvudtillgångar, `false` för deltillgångar

### medlemOf {#memberof}

Det här predikatet hittar objekt som är medlemmar av en viss [resursinsamling för sling](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/resource/collection/ResourceCollection.html).

Ett predikat som bara kan filtreras och som inte kan använda ett sökindex.

Det stöder inte facetextrahering.

#### Egenskaper {#properties-10}

* **`memberOf`** - sökväg till Sling-resurssamling

### nodename {#nodename}

Detta predikat matchar JCR-nodnamn.

Det har stöd för facet-extrahering och innehåller bucket för varje unikt nodnamn (filnamn).

#### Egenskaper {#properties-11}

* **`nodename`** - nodnamnsmönster som tillåter jokertecken: `*` = ett eller inga tecken, `?` = any char, `[abc]` = endast tecken inom hakparentes

### inte utgånget {#notexpired}

Detta predikat matchar objekt genom att kontrollera om en JCR-datumegenskap är större eller lika med den aktuella servertiden. Den kan användas för att kontrollera en `expiresAt` värdet och begränsar resultaten till endast de värden som ännu inte har gått ut (`notexpired=true`) eller som redan har gått ut (`notexpired=false`).

Det stöder inte filtrering.

Det stöder extrahering av ansikten på samma sätt som [`daterange`](#daterange) förutsäga.

#### Egenskaper {#properties-12}

* **`notexpired`** - boolesk, `true` för ännu ej utgången (datum i framtiden eller lika med), `false` för utgången (tidigare datum) (obligatoriskt)
* **`property`** - relativ sökväg till `DATE` egenskap som ska kontrolleras (obligatoriskt)

### bana {#path}

Det här predikatet söker i en angiven sökväg.

Det stöder inte facetextrahering.

#### Egenskaper {#properties-14}

* **`path`** - Definierar banmönstret.
   * Beroende på `exact` egenskapen, antingen matchar hela underträdet (som att lägga till `//*` i xpath, men observera att den inte innehåller basbanan), eller så matchar bara en exakt bana, som kan innehålla jokertecken (`*`).
      * Standardvärdet är `true`.
&lt;!— * Om `self`egenskapen är inställd söks hela underträdet inklusive basnoden igenom.—>
* **`exact`** - if `exact` är `true`måste den exakta sökvägen matcha, men den kan innehålla enkla jokertecken (`*`), som matchar namn, men inte `/`; om den är `false` (standard) alla underordnade tas med (valfritt).
* **`flat`** - söker endast efter direkt underordnade (som att lägga till `/*` in xpath) (används endast om `exact` är inte true (valfritt).
* **`self`** - söker i underträdet men inkluderar basnoden som angetts som sökväg (inga jokertecken).
   * *Viktigt*: Ett problem har identifierats med `self` -egenskapen i den aktuella implementeringen av frågebyggaren och att använda den i frågor kanske inte ger rätt sökresultat. Ändra den aktuella implementeringen av `self` egenskapen är inte heller möjlig eftersom den kan bryta mot befintliga program som förlitar sig på den. På grund av denna funktionalitet `self` egenskapen är nu föråldrad. Du bör undvika att använda den.

### property {#property}

Detta predikat matchar JCR-egenskaperna och deras värden.

Det har stöd för facetextrahering och innehåller bucket för varje unikt egenskapsvärde i resultatet.

#### Egenskaper {#properties-15}

* **`property`** - relativ sökväg till egenskapen, till exempel `jcr:title`.
* **`value`** - värde att kontrollera egenskap för; följer JCR-egenskapstypen till strängkonverteringar.
* **`N_value`** - användning `1_value`, `2_value`, ... för att kontrollera om det finns flera värden (i kombination med `OR` som standard med `AND` if `and=true`).
* **`and`** - ställs in på `true` för att kombinera flera värden (`N_value`) med `AND`
* **`operation`**
   * `equals` för exakt matchning (standard).
   * `unequals` för jämförelser av olikheter.
   * `like` för att använda `jcr:like` xpath-funktion (valfri).
   * `not` för ingen matchning (till exempel `not(@prop)` in xpath ignoreras value param).
   * `exists` för kontroll av förekomsten.
      * `true` egenskapen måste finnas.
      * `false` är samma som `not` och är standard.
* **`depth`** - antalet jokernivåer under vilka egenskapen/den relativa sökvägen kan finnas (till exempel `property=size depth=2` kontroller `node/size`, `node/*/size`och `node/*/*/size`).

### rangeProperty {#rangeproperty}

Detta predikat matchar en JCR-egenskap mot ett intervall. Det gäller egenskaper med linjära typer som `LONG`, `DOUBLE`och `DECIMAL`. För `DATE`, se [`daterange`](#daterange) som har optimerade indata för datumformat.

Du kan definiera en nedre gräns, en övre gräns eller båda. Åtgärden (t.ex. mindre än, eller mindre än eller lika med) kan också anges individuellt för nedre och övre gräns.

Det stöder inte facetextrahering.

#### Egenskaper {#properties-16}

* **`property`** - relativ sökväg till egenskap
* **`lowerBound`** - nedre gräns för check-egenskap
* **`lowerOperation`** - `>` (standard) eller `>=`gäller för `lowerValue`
* **`upperBound`** - övre gräns för check-egenskap
* **`upperOperation`** - `<` (standard) eller `<=`gäller för `lowerValue`
* **`decimal`** - `true` om egenskapen checked är av typen Decimal

### relativ {#relativedaterange}

Detta predikat matchar `JCR DATE` egenskaper mot ett datum/tidsintervall med tidsförskjutningar i förhållande till den aktuella servertiden. Du kan ange `lowerBound` och `upperBound` med ett millisekundvärde eller Bugzilla-syntaxen `1s 2m 3h 4d 5w 6M 7y` (en sekund, två minuter, tre timmar, fyra dagar, fem veckor, sex månader, sju år). Prefix med `-` om du vill ange en negativ förskjutning före den aktuella tiden. Om du bara anger `lowerBound` eller `upperBound`, den andra som standard är `0`, som representerar aktuell tid.

Till exempel:

* `upperBound=1h` (och nej) `lowerBound`) markerar allt under nästa timme
* `lowerBound=-1d` (och nej) `upperBound`) markerar något de senaste 24 timmarna
* `lowerBound=-6M` och `upperBound=-3M` väljer något under de senaste 3 till 6 månaderna
* `lowerBound=-1500` och `upperBound=5500` väljer något mellan 1 500 millisekunder och 5 500 millisekunder i framtiden
* `lowerBound=1d` och `upperBound=2d` markerar allt i övermorgon

Den tar inte hänsyn till skottår och alla månader är 30 dagar.

Det stöder inte filtrering.

Det stöder extrahering av ansikten på samma sätt som [`daterange`](#daterange) förutsäga.

#### Egenskaper {#properties-17}

* **`upperBound`** - övre gräns för datum i millisekunder eller `1s 2m 3h 4d 5w 6M 7y` (en sekund, två minuter, tre timmar, fyra dagar, fem veckor, sex månader, sju år) i förhållande till aktuell servertid, använd `-` för negativ offset
* **`lowerBound`** - undre gräns för datum i millisekunder eller `1s 2m 3h 4d 5w 6M 7y` (en sekund, två minuter, tre timmar, fyra dagar, fem veckor, sex månader, sju år) i förhållande till aktuell servertid, använd `-` för negativ offset

### sparad fråga {#savedquery}

Detta predikat inkluderar alla predikat för en beständig Query Builder-fråga i den aktuella frågan som ett undergruppsprediat.

Den kör ingen extra fråga men utökar den aktuella frågan.

Frågor kan sparas programmatiskt med `QueryBuilder#storeQuery()`. Formatet kan vara en flerradig `String` egenskap eller `nt:file` nod som innehåller frågan som en textfil i Java™-egenskapsformat.

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

* **`tag`** - sökväg till taggen som du vill söka efter, till exempel `properties:orientation/landscape`
* **`N_value`** - användning `1_value`, `2_value`, ... för att kontrollera om det finns flera taggar (i kombination med `OR` som standard med `AND` if `and=true`)
* **`property`** - egenskap (eller relativ sökväg till egenskap) att titta på (standard) `cq:tags`)

### tagid {#tagid}

Det här predikatet söker efter innehåll som taggats med en eller flera taggar genom att ange tagg-ID:n.

Det har stöd för facet-extrahering och tillhandahåller bucket för varje unik tagg med hjälp av deras aktuella tagg-ID.

#### Egenskaper {#properties-22}

* **`tagid`** - tagg-ID att söka efter, till exempel `properties:orientation/landscape`
* **`N_value`** - användning `1_value`, `2_value`, ... för att kontrollera om det finns flera tagg-ID:n (i kombination med `OR` som standard med `AND` if `and=true`)
* **`property`** - egenskap (eller relativ sökväg till egenskap) att titta på (standard) `cq:tags`)

### tagsearch {#tagsearch}

Det här predikatet söker efter innehåll som taggats med en eller flera taggar genom att ange nyckelord. Först görs en sökning efter taggar som innehåller dessa nyckelord i sina titlar och resultatet begränsas sedan till enbart objekt som taggats med dessa nyckelord.

Det stöder inte facetextrahering.

#### Egenskaper {#Properties-1}

* **`tagsearch`** - nyckelord att söka efter i taggtitlar
* **`property`** - egenskap (eller relativ sökväg till egenskap) som ska övervägas (standard) `cq:tags`)
* **`lang`** - om du bara vill söka i en viss lokaliserad taggtitel (till exempel `de`)
* **`all`** - booleskt värde för att söka efter hela taggens fulltext, det vill säga alla titlar, beskrivningar och så vidare (har företräde framför `lang`)

### type {#type}

Detta predikat begränsar resultatet till en specifik JCR-nodtyp, både primära nodtyper och `mixin` typer. Den hittar även undertyper av den nodtypen. Databasens sökindex måste omfatta nodtyperna för effektiv körning.

Det har stöd för facetextrahering och innehåller bucket för varje unik typ i resultatet.

#### Egenskaper {#Properties-2}

* **`type`** - nodtyp eller `mixin` namn att söka efter, till exempel `cq:Page`

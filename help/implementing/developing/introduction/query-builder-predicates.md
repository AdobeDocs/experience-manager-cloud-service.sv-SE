---
title: Predikatreferens för Query Builder
description: Predikatreferens för Query Builder API.
exl-id: 77118ef7-4d29-470d-9c4b-20537a408940
source-git-commit: a446efacb91f1a620d227b9413761dd857089c96
workflow-type: tm+mt
source-wordcount: '2219'
ht-degree: 1%

---

# Predikatreferens för frågebyggaren {#query-builder-predicate-reference}

## Allmänt {#general}

### root {#root}

Detta är rotpredikatgruppen. Den har stöd för alla funktioner i en grupp och tillåter inställning av globala frågeparametrar.

Namnet &quot;root&quot; används aldrig i en fråga, det är underförstått.

#### Egenskaper {#properties-18}

* **`p.offset`** - tal som anger början på resultatsidan, dvs hur många objekt som ska hoppas över
* **`p.limit`** - siffra som anger sidstorleken
* **`p.guessTotal`** - rekommenderas: Undvik att beräkna det totala resultatet som kan vara kostsamt. antingen en siffra som anger den högsta totalsumman som ska räknas upp till (t.ex. 1000, ett tal som ger användarna tillräckligt med feedback på grovstorleken och exakta tal för mindre resultat) eller  `true` att räkna upp till minsta möjliga  `p.offset` +  `p.limit`
* **`p.excerpt`** - om det är inställt på  `true`, inkludera utdrag av fullständig text i resultatet
* **`p.hits`** - (endast för JSON-servern) väljer du hur träffar skrivs som JSON, med dessa standardinställningar (utbyggbara via ResultHitWriter-tjänsten):
   * **`simple`** - minimala objekt som  `path`,  `title`,  `lastmodified`,  `excerpt` (om de anges)
   * **`full`** - Sing JSON-återgivning av noden, med  `jcr:path` information om träffens sökväg: Som standard anges bara nodens direkta egenskaper, inklusive ett djupare träd med 0 som  `p.nodedepth=N`betyder hela det oändliga underträdet, lägg  `p.acls=true` till för att inkludera JCR-behörigheterna för den aktuella sessionen för det angivna resultatobjektet (mappningar:  `create` =  `add_node`,  `modify` =  `set_property`,  `delete` =  `remove`)
   * **`selective`** - Endast egenskaper som anges i  `p.properties`, som är blankstegsavgränsade (används  `+` i URL-adresser) med relativa sökvägar. om den relativa sökvägen har ett djup  `>1` representeras dessa som underordnade objekt, den speciella  `jcr:path` egenskapen inkluderar sökvägen till träffen

### grupp {#group}

Det här predikatet gör det möjligt att bygga kapslade villkor. Grupper kan innehålla kapslade grupper. Allt i en Query Builder-fråga finns implicit i en rotgrupp som även kan ha parametrarna `p.or` och `p.not`.

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

Detta söker efter termen **hantering** på sidor i `/content/wknd/ch/de` eller i resurser i `/content/dam/wknd`.

Detta är begreppsmässigt `fulltext AND ( (path AND type) OR (path AND type) )`. Observera att sådana OR-kopplingar behöver bra index av prestandaskäl.

#### Egenskaper {#properties-6}

* **`p.or`** - om det anges till  `true`måste bara ett predikat i gruppen matcha. Standardvärdet är `false`, vilket innebär att alla måste matcha
* **`p.not`** - om den anges till  `true`, negeras gruppen (standardvärdet är  `false`)
* **`<predicate>`** - lägger till kapslade predikat
* **`N_<predicate>`** - lägger till flera kapslade predikat samtidigt, som  `1_property, 2_property, ...`

### orderby {#orderby}

Med det här predikatet kan du sortera resultaten. Om det krävs en ordning med flera egenskaper måste det här prefixet läggas till flera gånger med hjälp av talprefixet, till exempel `1_orderby=first`, `2_oderby=second`.

#### Egenskaper {#properties-13}

* **`orderby`** - antingen JCR-egenskapsnamn som anges av radavståndet @, till exempel  `@jcr:lastModified` eller  `@jcr:content/jcr:title`, eller ett annat predikat i frågan, till exempel  `2_property`som sorteringen ska göras på
* **`sort`** - sorteringsriktning, antingen  `desc` för fallande eller  `asc` för stigande (standard)
* **`case`** - om den är inställd på  `ignore` att göra sorteringsfallet okänsligt, så  `a` kommer det tidigare  `B`att betyda. om den är tom eller utelämnad är sorteringen skiftlägeskänslig, vilket betyder  `B` kommer före  `a`

## Predikat {#predicates}

### boolproperty {#boolproperty}

Det här predikatet matchar JCR-booleska egenskaper. Tar endast emot värdena `true` och `false`. Om `false` används matchar det om egenskapen har värdet `false` eller om den inte finns alls. Detta kan vara användbart för att kontrollera om det finns booleska flaggor som bara är inställda när de är aktiverade.

Den ärvda `operation`-parametern har ingen betydelse.

Det här predikatet har stöd för facetextrahering och tillhandahåller bucket för varje `true`- eller `false`-värde, men bara för befintliga egenskaper.

#### Egenskaper {#properties}

* **`boolproperty`** - relativ sökväg till egenskap, till exempel  `myFeatureEnabled` eller  `jcr:content/myFeatureEnabled`
* **`value`** - värde som du vill kontrollera egenskapen för,  `true` eller  `false`

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
   * `>` för  `property1` större än  `property2`
   * `>=` för  `property1` större än eller lika med  `property2`

### daterange {#daterange}

Detta predikat matchar JCR-datumegenskaper mot ett datum-/tidsintervall. Detta använder ISO8601
format för datum och tid (`YYYY-MM-DDTHH:mm:ss.SSSZ`) och tillåter även partiella representationer, som `YYYY-MM-DD`. Alternativt kan tidsstämpeln anges som POSIX-tid.

Du kan söka efter vad som helst mellan två tidsstämplar, vad som helst nyare eller äldre än ett visst datum, och du kan även välja mellan inkluderande och öppna intervall.

Det stöder facetextrahering och innehåller bucket `today`, `this week`, `this month`, `last 3 months`, `this year`, `last year` och `earlier than last year`.

Det stöder inte filtrering.

#### Egenskaper {#properties-3}

* **`property`** - relativ sökväg till en  `DATE` egenskap, till exempel  `jcr:lastModified`
* **`lowerBound`** - nedre gräns för att kontrollera egenskap, till exempel  `2014-10-01`
* **`lowerOperation`** -  `>` (nyare) eller  `>=` (på eller nyare), gäller för  `lowerBound`. Standardvärdet är `>`
* **`upperBound`** - övre gräns för att kontrollera egenskap för, till exempel  `2014-10-01T12:15:00`
* **`upperOperation`** -  `<` (äldre) eller  `<=` (äldre), gäller för  `upperBound`. Standardvärdet är `<`
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

Detta predikat begränsar resultatet till objekt där den aktuella sessionen har de angivna [JCR-behörigheterna.](https://docs.adobe.com/content/docs/en/spec/jcr/2.0/16_Access_Control_Management.html#16.2.3%20Standard%20Privileges)

Detta är ett predikat som bara kan filtreras och kan inte utnyttja ett sökindex. Det stöder inte facetextrahering.

#### Egenskaper {#properties-7}

* **`hasPermission`** - kommaavgränsade JCR-behörigheter som den aktuella användarsessionen måste ha för noden i fråga. t.ex.  `jcr:write`,  `jcr:modifyAccessControl`

### language {#language}

Det här predikatet hittar AEM sidor på ett visst språk. Det här tittar både på sidspråksegenskapen och sidsökvägen, som ofta innehåller språket eller språket i en webbplatsstruktur på den översta nivån.

Detta är ett predikat som bara kan filtreras och kan inte utnyttja ett sökindex.

Programmet har stöd för facetextrahering och innehåller hinkar för varje unik språkkod.

#### Egenskaper {#properties-8}

* **`language`** - ISO-språkkod, till exempel  `de`

### huvudtillgång {#mainasset}

Detta predikat kontrollerar om en nod är en DAM-huvudresurs och inte en underresurs. Detta är i stort sett alla noder som inte finns i en underresursnod. Observera att detta inte söker efter nodtypen `dam:Asset`. Om du vill använda det här predikatet anger du `mainasset=true` eller `mainasset=false`. Det finns inga fler egenskaper.

Detta är ett predikat som bara kan filtreras och kan inte utnyttja ett sökindex.

Det stöder facet-extrahering och erbjuder två buffertar för huvud- och delresurser.

#### Egenskaper {#properties-9}

* **`mainasset`** - booleskt,  `true` för huvudtillgångar,  `false` för deltillgångar

### medlemOf {#memberof}

Det här predikatet hittar objekt som är medlemmar i en specifik [sling-resurssamling](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/org/apache/sling/resource/collection/ResourceCollection.html).

Detta är ett predikat som bara kan filtreras och kan inte utnyttja ett sökindex.

Det stöder inte facetextrahering.

#### Egenskaper {#properties-10}

* **`memberOf`** - sökväg till Sling-resurssamling

### nodename {#nodename}

Detta predikat matchar JCR-nodnamn.

Det har stöd för facet-extrahering och innehåller bucket för varje unikt nodnamn (filnamn).

#### Egenskaper {#properties-11}

* **`nodename`** - nodnamnsmönster som tillåter jokertecken:  `*` = valfri eller ingen tecken,  `?` = valfri tecken,  `[abc]` = endast tecken inom hakparentes

### inte utgånget {#notexpired}

Detta predikat matchar objekt genom att kontrollera om en JCR-datumegenskap är större eller lika med den aktuella servertiden. Detta kan användas för att kontrollera ett `expiresAt`-värde och begränsa resultatet till endast de som ännu inte har gått ut (`notexpired=true`) eller som redan har gått ut (`notexpired=false`).

Det stöder inte filtrering.

Det stöder facetextrahering på samma sätt som [`daterange`](#daterange)-predikatet.

#### Egenskaper {#properties-12}

* **`notexpired`** - boolesk,  `true` för ännu inte utgången (datum i framtiden eller lika med),  `false` för utgången (datum i det förflutna) (obligatoriskt)
* **`property`** - relativ sökväg till den  `DATE` egenskap som ska kontrolleras (obligatoriskt)

### path {#path}

Det här predikatet söker i en angiven sökväg.

Det stöder inte facetextrahering.

#### Egenskaper {#properties-14}

* **`path`** - Detta definierar banmönstret.
   * Beroende på egenskapen `exact` kommer antingen hela underträdet att matcha (som att lägga till `//*` i XPath, men observera att detta inte inkluderar bassökvägen) eller bara en exakt sökvägsmatchning, som kan innehålla jokertecken (`*`).
      * Standardvärdet är `true`
   * Om egenskapen `self`anges genomsöks hela underträdet inklusive basnoden.
* **`exact`** - om  `exact` så  `true`är fallet måste den exakta sökvägen matcha, men den kan innehålla enkla jokertecken (`*`) som matchar namn, men inte  `/`. om det är  `false` (standard) inkluderas alla underordnade (valfritt)
* **`flat`** - söker endast i de direkta underordnade (som att lägga till  `/*` i XPath) (används bara om  `exact` inte är true, valfritt)
* **`self`** - söker i underträdet men inkluderar basnoden som angetts som sökväg (inga jokertecken)

### property {#property}

Detta predikat matchar JCR-egenskaperna och deras värden.

Det har stöd för facetextrahering och innehåller bucket för varje unikt egenskapsvärde i resultatet.

#### Egenskaper {#properties-15}

* **`property`** - relativ sökväg till egenskap, till exempel  `jcr:title`
* **`value`** - värde för att kontrollera egenskapen; följer egenskapstypen JCR till strängkonverteringar
* **`N_value`** - använd  `1_value`,  `2_value`, ... för att kontrollera om det finns flera värden (i kombination med  `OR` som standard, med  `AND` if  `and=true`)
* **`and`** - satt till  `true` för att kombinera flera värden (`N_value`) med  `AND`
* **`operation`**
   * `equals` för exakt matchning (standard)
   * `unequals` för jämförelser av olikhet
   * `like` för att använda funktionen  `jcr:like` xpath (valfritt)
   * `not` för ingen matchning (t.ex.  `not(@prop)` i xpath ignoreras värdeparam)
   * `exists` för existenskontroll
      * `true` egenskapen måste finnas
      * `false` är detsamma som  `not` och är standard
* **`depth`** - antalet jokernivåer under vilka egenskapen/den relativa sökvägen kan finnas (t.ex.  `property=size depth=2` kommer att kontrollera  `node/size`och  `node/*/size`   `node/*/*/size`)

### rangegenskap {#rangeproperty}

Detta predikat matchar en JCR-egenskap mot ett intervall. Detta gäller för egenskaper med linjära typer som `LONG`, `DOUBLE` och `DECIMAL`. För `DATE`, se [`daterange`](#daterange)-predikatet som har optimerade indata för datumformat.

Du kan definiera en nedre gräns, en övre gräns eller båda. Operationen (t.ex. mindre än eller lika med) kan också anges individuellt för nedre och övre gräns.

Det stöder inte facetextrahering.

#### Egenskaper {#properties-16}

* **`property`** - relativ sökväg till egenskap
* **`lowerBound`** - nedre gräns för check-egenskap
* **`lowerOperation`** -  `>` (standard) eller  `>=`, gäller  `lowerValue`
* **`upperBound`** - övre gräns för check-egenskap
* **`upperOperation`** -  `<` (standard) eller  `<=`, gäller  `lowerValue`
* **`decimal`** -  `true` om egenskapen checked är av typen Decimal

### relativ {#relativedaterange}

Det här predikatet matchar `JCR DATE`-egenskaper mot ett datum/tidsintervall med hjälp av tidsförskjutningar i förhållande till den aktuella servertiden. Du kan ange `lowerBound` och `upperBound` antingen med ett millisekundvärde eller Bugzilla-syntaxen `1s 2m 3h 4d 5w 6M 7y` (en sekund, två minuter, tre timmar, fyra dagar, fem veckor, sex månader, sju år). Prefix med `-` om du vill ange en negativ förskjutning före den aktuella tiden. Om du bara anger `lowerBound` eller `upperBound` kommer den andra att ha standardvärdet `0`, vilket representerar den aktuella tiden.

Till exempel:

* `upperBound=1h` (och nej  `lowerBound`) markerar något under nästa timme
* `lowerBound=-1d` (och nej  `upperBound`) markerar något under de senaste 24 timmarna
* `lowerBound=-6M` och  `upperBound=-3M` väljer något under de senaste 3-6 månaderna
* `lowerBound=-1500` och  `upperBound=5500` väljer allt som är mellan 1 500 millisekunder och 5 500 millisekunder i framtiden
* `lowerBound=1d` och  `upperBound=2d` väljer allt i övermorgon

Observera att programmet inte tar hänsyn till skottår och att alla månader är 30 dagar.

Det stöder inte filtrering.

Det stöder facetextrahering på samma sätt som [`daterange`](#daterange)-predikatet.

#### Egenskaper {#properties-17}

* **`upperBound`** - övre datumgräns i millisekunder eller  `1s 2m 3h 4d 5w 6M 7y` (en sekund, två minuter, tre timmar, fyra dagar, fem veckor, sex månader, sju år) i förhållande till aktuell servertid, använd  `-` för negativ offset
* **`lowerBound`** - undre datumgräns i millisekunder eller  `1s 2m 3h 4d 5w 6M 7y` (en sekund, två minuter, tre timmar, fyra dagar, fem veckor, sex månader, sju år) i förhållande till aktuell servertid, använd  `-` för negativ offset

### sparad fråga {#savedquery}

Detta predikat inkluderar alla predikat för en beständig Query Builder-fråga i den aktuella frågan som ett undergruppsprediat.

Observera att detta inte kör en extra fråga utan utökar den aktuella frågan.

Frågor kan sparas programmatiskt med `QueryBuilder#storeQuery()`. Formatet kan antingen vara en flerradig `String`-egenskap eller en `nt:file`-nod som innehåller frågan som en textfil i Java-egenskapsformat.

Det stöder inte facetextrahering för predikaten i den sparade frågan.

#### Egenskaper {#properties-19}

* **`savedquery`** - sökväg till den sparade frågan (`String` egenskap eller  `nt:file` nod)

### liknande {#similar}

Detta predikat är en likhetssökning som använder JCR XPath:s `rep:similar()`.

Det stöder inte filtrering och inte facetextrahering.

#### Egenskaper {#properties-20}

* **`similar`** - absolut sökväg till noden där liknande noder ska hittas
* **`local`** - en relativ sökväg till en underordnad nod eller  `.` för den aktuella noden (valfritt, standardvärdet är  `.`)

### tag {#tag}

Det här predikatet söker efter innehåll som taggats med en eller flera taggar genom att ange sökvägar för taggtiteln.

Det har stöd för facet-extrahering och tillhandahåller bucket för varje unik tagg med hjälp av deras aktuella namnsökväg.

#### Egenskaper {#properties-21}

* **`tag`** - taggens titelsökväg att söka efter, till exempel  `properties:orientation/landscape`
* **`N_value`** - använd  `1_value`,  `2_value`, ... för att kontrollera om det finns flera taggar (i kombination med  `OR` som standard, med  `AND` if  `and=true`)
* **`property`** - egenskap (eller relativ sökväg till egenskap) att titta på (standard  `cq:tags`)

### tagid {#tagid}

Det här predikatet söker efter innehåll som taggats med en eller flera taggar genom att ange tagg-ID:n.

Det har stöd för facet-extrahering och tillhandahåller bucket för varje unik tagg med hjälp av deras aktuella tagg-ID.

#### Egenskaper {#properties-22}

* **`tagid`** - tagg-ID att söka efter, till exempel  `properties:orientation/landscape`
* **`N_value`** - använd  `1_value`,  `2_value`, ... för att kontrollera om det finns flera tagg-ID:n (i kombination med  `OR` som standard, med  `AND` if  `and=true`)
* **`property`** - egenskap (eller relativ sökväg till egenskap) att titta på (standard  `cq:tags`)

### tagsearch {#tagsearch}

Det här predikatet söker efter innehåll som taggats med en eller flera taggar genom att ange nyckelord. Då söker du först efter taggar som innehåller dessa nyckelord i deras titlar och begränsar sedan resultatet till enbart objekt som taggats med dessa.

Det stöder inte facetextrahering.

#### Egenskaper {#Properties-1}

* **`tagsearch`** - nyckelord att söka efter i taggtitlar
* **`property`** - egenskap (eller relativ sökväg till egenskap) som ska övervägas (standard  `cq:tags`)
* **`lang`** - om du bara vill söka i en viss lokaliserad taggtitel (t.ex.  `de`)
* **`all`** - booleskt värde om du vill söka efter hela taggens fulltext, dvs. alla titlar, beskrivning osv. (har högre prioritet än `lang`)

### type {#type}

Detta predikat begränsar resultatet till en viss JCR-nodtyp, både primära nodtyper och mixin-typer. Detta söker även efter undertyper av den nodtypen. Observera att databasens sökindex måste omfatta nodtyperna för effektiv körning.

Det har stöd för facetextrahering och innehåller bucket för varje unik typ i resultatet.

#### Egenskaper {#Properties-2}

* **`type`** - nodtyp eller blandnamn att söka efter, till exempel  `cq:Page`

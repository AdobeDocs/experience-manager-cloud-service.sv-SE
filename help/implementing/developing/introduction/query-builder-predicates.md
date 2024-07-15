---
title: Predikatreferens för Query Builder
description: Predikatreferens för Query Builder API i AEM as a Cloud Service.
exl-id: 77118ef7-4d29-470d-9c4b-20537a408940
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
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

* **`p.offset`** - tal som anger början på resultatsidan, det vill säga hur många objekt som ska hoppas över.
* **`p.limit`** - siffra som anger sidstorleken.
* **`p.guessTotal`** - rekommenderas: undvik att beräkna det totala resultatet, vilket kan vara kostsamt. Antingen en siffra som anger den högsta summan som ska räknas upp till (till exempel 1 000, ett tal som ger användarna tillräckligt med feedback på grovstorleken och exakta tal för mindre resultat). Eller `true` om du bara vill räkna upp till det minsta nödvändiga `p.offset` + `p.limit`.
* **`p.excerpt`** - om värdet är `true` inkluderar du utdrag med fullständig text i resultatet.
* **`p.indexTag`** - om inställningen innehåller ett indexmärkordsalternativ i frågan (se [Indextagg för frågetyp](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#query-option-index-tag)).
* **`p.facetStrategy`** - Om värdet är `oak` delegerar Query Builder facet-extrahering till Oak (se [Fasetter](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#facets)).
* **`p.hits`** - (endast för JSON-servleten) väljer du hur träffar skrivs som JSON, med dessa standardinställningar (utbyggbara via ResultHitWriter-tjänsten).
   * **`simple`** - minimala objekt som `path`, `title`, `lastmodified`, `excerpt` (om de anges).
   * **`full`** - Sing JSON-återgivning av noden, där `jcr:path` anger träffens sökväg. Som standard listas bara de direkta egenskaperna för noden, inklusive ett djupare träd med `p.nodedepth=N`, där 0 betyder hela det oändliga underträdet. Lägg till `p.acls=true` om du vill inkludera JCR-behörigheterna för den aktuella sessionen för det angivna resultatobjektet (mappningar: `create` = `add_node`, `modify` = `set_property`, `delete` = `remove`).
   * **`selective`** - endast egenskaper angivna i `p.properties`, som är en blankstegsavgränsad (använd `+` i URL-adresser) lista med relativa sökvägar. Om den relativa sökvägen har djupet `>1` representeras dessa egenskaper som underordnade objekt. Den speciella egenskapen `jcr:path` innehåller träffens sökväg.

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

Det är `(1_property` ELLER `2_property)`.

Följande är ett exempel för kapslade grupper:

```text
fulltext=Management
group.p.or=true
group.1_group.path=/content/wknd/ch/de
group.1_group.type=cq:Page
group.2_group.path=/content/dam/wknd
group.2_group.type=dam:Asset
```

Söker efter termen **Hantering** på sidor i `/content/wknd/ch/de` eller i resurser i `/content/dam/wknd`.

Det är `fulltext AND ( (path AND type) OR (path AND type) )`. Sådana OR-kopplingar behöver bra index av prestandaskäl.

#### Egenskaper {#properties-6}

* **`p.or`** - Om värdet är `true` måste bara ett predikat i gruppen matcha. Standardvärdet är `false`, vilket innebär att alla måste matcha
* **`p.not`** - om värdet är `true` negeras gruppen (standardvärdet är `false`)
* **`<predicate>`** - lägger till kapslade predikat
* **`N_<predicate>`** - lägger till flera kapslade predikat samtidigt, som `1_property, 2_property, ...`

### orderby {#orderby}

Med det här predikatet kan du sortera resultaten. Om det krävs en ordning efter flera egenskaper måste predikatet läggas till flera gånger med hjälp av talprefixet, till exempel `1_orderby=first`, `2_oderby=second`.

#### Egenskaper {#properties-13}

* **`orderby`** - antingen JCR-egenskapsnamnet som anges av radavståndet @, till exempel `@jcr:lastModified` eller `@jcr:content/jcr:title`, eller ett annat predikat i frågan, till exempel `2_property`, som sorteringen ska göras på
* **`sort`** - sorteringsriktning, antingen `desc` för fallande eller `asc` för stigande (standard)
* **`case`** - om värdet är `ignore` blir sorteringsfallet okänsligt, vilket innebär att `a` kommer före `B`; om det är tomt eller utelämnas är sorteringen skiftlägeskänslig, vilket innebär att `B` kommer före `a`

## Predikat {#predicates}

### boolproperty {#boolproperty}

Detta predikat matchar JCR-booleska egenskaper. Endast värdena `true` och `false` godkänns. Om värdet är `false` matchar det om egenskapen har värdet `false` eller om den inte finns alls. Det här predikatet är användbart för att kontrollera om det finns booleska flaggor som bara är inställda när de är aktiverade.

Den ärvda parametern `operation` har ingen betydelse.

Det här predikatet har stöd för facetextrahering och tillhandahåller bucket för varje `true`- eller `false`-värde, men bara för befintliga egenskaper.

#### Egenskaper {#properties}

* **`boolproperty`** - relativ sökväg till egenskap, till exempel `myFeatureEnabled` eller `jcr:content/myFeatureEnabled`
* **`value`** - värde att kontrollera egenskap för, `true` eller `false`

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

* **`property1`** - sökväg till första datumegenskap
* **`property2`** - egenskapen path to second date
* **`operation`**
   * `=` för exakt matchning (standard)
   * `!=` för olikhetsjämförelse
   * `>` för `property1` större än `property2`
   * `>=` för `property1` större än eller lika med `property2`

### daterange {#daterange}

Detta predikat matchar JCR-datumegenskaper mot ett datum-/tidsintervall. Använder ISO8601
format för datum och tider (`YYYY-MM-DDTHH:mm:ss.SSSZ`) och tillåter även partiella representationer, som `YYYY-MM-DD`. Alternativt kan tidsstämpeln anges som POSIX-tid.

Du kan söka efter vad som helst mellan två tidsstämplar, vad som helst nyare eller äldre än ett visst datum, och du kan även välja mellan inkluderande och öppna intervall.

Det har stöd för ansiktsextrahering och innehåller bucket `today`, `this week`, `this month`, `last 3 months`, `this year`, `last year` och `earlier than last year`.

Det stöder inte filtrering.

#### Egenskaper {#properties-3}

* **`property`** - relativ sökväg till en `DATE`-egenskap, till exempel `jcr:lastModified`
* **`lowerBound`** - nedre gräns för att kontrollera egenskap, till exempel `2014-10-01`
* **`lowerOperation`** - `>` (nyare) eller `>=` (nyare eller senare) gäller för `lowerBound`. Standardvärdet är `>`
* **`upperBound`** - övre gräns för att kontrollera egenskap för exempelvis `2014-10-01T12:15:00`
* **`upperOperation`** - `<` (äldre) eller `<=` (äldre) gäller för `upperBound`. Standardvärdet är `<`
* **`timeZone`** - ID för tidszon som ska användas när den inte anges som en ISO-8601-datumsträng. Standardvärdet är systemets standardtidszon.

### exkluderingar {#excludepaths}

Detta predikat utesluter noder från resultatet där deras sökväg matchar ett reguljärt uttryck.

Ett predikat som bara kan filtreras och som inte kan använda ett sökindex.

Det stöder inte facetextrahering.

#### Egenskaper {#properties-4}

* **`excludepaths`** - reguljära uttryck som matchas mot resultatsökvägar, exklusive matchande sökvägar från resultatet.

### fulltext {#fulltext}

Söker efter termer i fulltextindexet.

Det stöder inte filtrering.

Det stöder inte facetextrahering.

#### Egenskaper {#properties-5}

* **`fulltext`** - fulltextsöktermerna
* **`relPath`** - den relativa sökvägen som ska sökas i egenskapen eller undernoden. Den här egenskapen är valfri.

### hasPermission {#haspermission}

Detta predikat begränsar resultatet till objekt där den aktuella sessionen har de angivna [JCR-behörigheterna.](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html#16.2.3%20Standard%20Privileges)

Ett predikat som bara kan filtreras och som inte kan använda ett sökindex. Det stöder inte facetextrahering.

#### Egenskaper {#properties-7}

* **`hasPermission`** - alla kommaavgränsade JCR-behörigheter som den aktuella användarsessionen måste ha för noden i fråga. Till exempel `jcr:write`, `jcr:modifyAccessControl`

### språk {#language}

Det här predikatet hittar AEM sidor på ett visst språk. Den tittar både på sidspråksegenskapen och sidsökvägen, som ofta innehåller språket eller språkinställningen i en webbplatsstruktur på den översta nivån.

Ett predikat som bara kan filtreras och som inte kan använda ett sökindex.

Programmet har stöd för facetextrahering och innehåller hinkar för varje unik språkkod.

#### Egenskaper {#properties-8}

* **`language`** - ISO-språkkod, till exempel `de`

### huvudtillgång {#mainasset}

Detta predikat kontrollerar om en nod är en DAM-huvudresurs och inte en underresurs. Det är i stort sett alla noder som inte finns i en underresursnod. Den söker inte efter nodtypen `dam:Asset`. Om du vill använda det här predikatet anger du `mainasset=true` eller `mainasset=false`. Det finns inga fler egenskaper.

Ett predikat som bara kan filtreras och som inte kan använda ett sökindex.

Det stöder facet-extrahering och erbjuder två buffertar för huvud- och delresurser.

#### Egenskaper {#properties-9}

* **`mainasset`** - boolesk, `true` för huvudresurser, `false` för delresurser

### medlemOf {#memberof}

Det här predikatet hittar objekt som är medlemmar i en specifik [sling-resurssamling](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/resource/collection/ResourceCollection.html).

Ett predikat som bara kan filtreras och som inte kan använda ett sökindex.

Det stöder inte facetextrahering.

#### Egenskaper {#properties-10}

* **`memberOf`** - sökväg till Sling-resurssamling

### nodename {#nodename}

Detta predikat matchar JCR-nodnamn.

Det har stöd för facet-extrahering och innehåller bucket för varje unikt nodnamn (filnamn).

#### Egenskaper {#properties-11}

* **`nodename`** - nodnamnsmönster som tillåter jokertecken: `*` = valfritt eller inget tecken, `?` = valfritt tecken, `[abc]` = endast tecken inom hakparentes

### inte utgånget {#notexpired}

Detta predikat matchar objekt genom att kontrollera om en JCR-datumegenskap är större eller lika med den aktuella servertiden. Den kan användas för att kontrollera ett `expiresAt`-värde och begränsar resultatet till endast de värden som ännu inte har upphört att gälla (`notexpired=true`) eller som redan har upphört att gälla (`notexpired=false`).

Det stöder inte filtrering.

Det stöder facetextrahering på samma sätt som predikatet [`daterange`](#daterange).

#### Egenskaper {#properties-12}

* **`notexpired`** - boolesk, `true` för ännu inte utgången (datum i framtiden eller lika med), `false` för utgången (tidigare datum) (obligatoriskt)
* **`property`** - relativ sökväg till egenskapen `DATE` som ska kontrolleras (obligatoriskt)

### bana {#path}

Det här predikatet söker i en angiven sökväg.

Det stöder inte facetextrahering.

#### Egenskaper {#properties-14}

* **`path`** - Definierar sökvägsmönstret.
   * Beroende på egenskapen `exact` matchar antingen hela underträdet (som att lägga till `//*` i XPath, men observera att det inte innehåller bassökvägen), eller så matchas bara en exakt sökväg, som kan innehålla jokertecken (`*`).
      * Standardvärdet är `true`.
&lt;!—   * Om egenskapen `self` anges genomsöks hela underträdet inklusive basnoden.—>
* **`exact`** - Om `exact` är `true` måste den exakta sökvägen matcha, men den kan innehålla enkla jokertecken (`*`) som matchar namn, men inte `/`. Om det är `false` (standard) inkluderas alla underordnade (valfritt).
* **`flat`** - söker endast i de direkta underordnade (som att bifoga `/*` i XPath) (används bara om `exact` inte är true, valfritt).
* **`self`** - söker i underträdet men inkluderar basnoden som angetts som sökväg (inga jokertecken).
   * *Viktigt!*: Ett problem har identifierats med egenskapen `self` i den aktuella implementeringen av frågebyggaren och det är inte säkert att korrekt sökresultat skapas om den används i frågor. Det går inte heller att ändra den aktuella implementeringen av egenskapen `self` eftersom den kan skada befintliga program som använder den. På grund av den här funktionen är egenskapen `self` nu föråldrad. Du bör undvika att använda den.

### property {#property}

Detta predikat matchar JCR-egenskaperna och deras värden.

Det har stöd för facetextrahering och innehåller bucket för varje unikt egenskapsvärde i resultatet.

#### Egenskaper {#properties-15}

* **`property`** - relativ sökväg till egenskap, till exempel `jcr:title`.
* **`value`** - värde att kontrollera egenskap för; följer JCR-egenskapstypen till strängkonverteringar.
* **`N_value`** - använd `1_value`, `2_value`, ... för att kontrollera flera värden (kombinerat med `OR` som standard, med `AND` if `and=true`).
* **`and`** - satt till `true` för att kombinera flera värden (`N_value`) med `AND`
* **`operation`**
   * `equals` för exakt matchning (standard).
   * `unequals` för olikhetsjämförelse.
   * `like` för användning av `jcr:like` XPath-funktionen (valfritt).
   * `not` utan matchning (till exempel `not(@prop)` i xpath ignoreras värdeparam).
   * `exists` om du vill ha en förekomstkontroll.
      * `true` egenskapen måste finnas.
      * `false` är samma som `not` och är standardvärdet.
* **`depth`** - antalet jokernivåer under vilka egenskapen/den relativa sökvägen kan finnas (till exempel `property=size depth=2` checks `node/size`, `node/*/size` och `node/*/*/size`).

### rangeProperty {#rangeproperty}

Detta predikat matchar en JCR-egenskap mot ett intervall. Det gäller för egenskaper med linjära typer som `LONG`, `DOUBLE` och `DECIMAL`. För `DATE`, se predikatet [`daterange`](#daterange) som har optimerade indata för datumformat.

Du kan definiera en nedre gräns, en övre gräns eller båda. Åtgärden (t.ex. mindre än, eller mindre än eller lika med) kan också anges individuellt för nedre och övre gräns.

Det stöder inte facetextrahering.

#### Egenskaper {#properties-16}

* **`property`** - relativ sökväg till egenskap
* **`lowerBound`** - nedre gräns för kontrollegenskap
* **`lowerOperation`** - `>` (standard) eller `>=` gäller för `lowerValue`
* **`upperBound`** - övre gräns för kontrollegenskap
* **`upperOperation`** - `<` (standard) eller `<=` gäller för `lowerValue`
* **`decimal`** - `true` om egenskapen checked är av typen Decimal

### relativ {#relativedaterange}

Det här predikatet matchar `JCR DATE` egenskaper mot ett datum/tidsintervall med hjälp av tidsförskjutningar i förhållande till den aktuella servertiden. Du kan ange `lowerBound` och `upperBound` med antingen ett millisekundvärde eller Bugzilla-syntaxen `1s 2m 3h 4d 5w 6M 7y` (en sekund, två minuter, tre timmar, fyra dagar, fem veckor, sex månader, sju år). Prefix med `-` om du vill ange en negativ förskjutning före den aktuella tiden. Om du bara anger `lowerBound` eller `upperBound` blir den andra standardvärdet `0`, vilket representerar den aktuella tiden.

Till exempel:

* `upperBound=1h` (och inte `lowerBound`) markerar något under nästa timme
* `lowerBound=-1d` (och inte `upperBound`) markerar något under de senaste 24 timmarna
* `lowerBound=-6M` och `upperBound=-3M` väljer något under de senaste 3 till sex månaderna
* `lowerBound=-1500` och `upperBound=5500` väljer något mellan 1 500 millisekunder och 5 500 millisekunder i framtiden
* `lowerBound=1d` och `upperBound=2d` markerar allt i övermorgon

Den tar inte hänsyn till skottår och alla månader är 30 dagar.

Det stöder inte filtrering.

Det stöder facetextrahering på samma sätt som predikatet [`daterange`](#daterange).

#### Egenskaper {#properties-17}

* **`upperBound`** - övre datumgräns i millisekunder eller `1s 2m 3h 4d 5w 6M 7y` (en sekund, två minuter, tre timmar, fyra dagar, fem veckor, sex månader, sju år) i förhållande till aktuell servertid, använd `-` för negativ offset
* **`lowerBound`** - undre datumgräns i millisekunder eller `1s 2m 3h 4d 5w 6M 7y` (en sekund, två minuter, tre timmar, fyra dagar, fem veckor, sex månader, sju år) i förhållande till aktuell servertid, använd `-` för negativ offset

### sparad fråga {#savedquery}

Detta predikat inkluderar alla predikat för en beständig Query Builder-fråga i den aktuella frågan som ett undergruppsprediat.

Den kör ingen extra fråga men utökar den aktuella frågan.

Frågor kan sparas programmatiskt med `QueryBuilder#storeQuery()`. Formatet kan antingen vara en flerradig `String`-egenskap eller en `nt:file`-nod som innehåller frågan som en textfil i Java™-egenskapsformat.

Det stöder inte facetextrahering för predikaten i den sparade frågan.

#### Egenskaper {#properties-19}

* **`savedquery`** - sökväg till den sparade frågan (`String` egenskap eller `nt:file` nod)

### liknande {#similar}

Det här predikatet är en likhetssökning med JCR XPath-objektet `rep:similar()`.

Det stöder inte filtrering och inte facetextrahering.

#### Egenskaper {#properties-20}

* **`similar`** - absolut sökväg till noden som liknande noder ska hittas för
* **`local`** - en relativ sökväg till en underordnad nod eller `.` för den aktuella noden (valfritt, standardvärdet är `.`)

### tag {#tag}

Det här predikatet söker efter innehåll som taggats med en eller flera taggar genom att ange sökvägar för taggtiteln.

Det har stöd för facet-extrahering och tillhandahåller bucket för varje unik tagg med hjälp av deras aktuella namnsökväg.

#### Egenskaper {#properties-21}

* **`tag`** - sökväg till taggens titel som du vill söka efter, till exempel `properties:orientation/landscape`
* **`N_value`** - använd `1_value`, `2_value`, ... för att kontrollera flera taggar (i kombination med `OR` som standard, med `AND` if `and=true`)
* **`property`** - egenskap (eller relativ sökväg till egenskap) att titta på (standard `cq:tags`)

### tagid {#tagid}

Det här predikatet söker efter innehåll som taggats med en eller flera taggar genom att ange tagg-ID:n.

Det har stöd för facet-extrahering och tillhandahåller bucket för varje unik tagg med hjälp av deras aktuella tagg-ID.

#### Egenskaper {#properties-22}

* **`tagid`** - tagg-ID att söka efter, till exempel `properties:orientation/landscape`
* **`N_value`** - använd `1_value`, `2_value`, ... för att kontrollera om det finns flera tagg-ID:n (i kombination med `OR` som standard, med `AND` if `and=true`)
* **`property`** - egenskap (eller relativ sökväg till egenskap) att titta på (standard `cq:tags`)

### tagsearch {#tagsearch}

Det här predikatet söker efter innehåll som taggats med en eller flera taggar genom att ange nyckelord. Först görs en sökning efter taggar som innehåller dessa nyckelord i sina titlar och resultatet begränsas sedan till enbart objekt som taggats med dessa nyckelord.

Det stöder inte facetextrahering.

#### Egenskaper {#Properties-1}

* **`tagsearch`** - nyckelord att söka efter i taggtitlar
* **`property`** - egenskap (eller relativ sökväg till egenskap) att överväga (standard `cq:tags`)
* **`lang`** - om du bara vill söka i en viss lokaliserad taggtitel (till exempel `de`)
* **`all`** - booleskt värde för att söka efter hela taggens fulltext, det vill säga alla titlar, beskrivningar och så vidare (har högre prioritet än `lang`)

### type {#type}

Detta predikat begränsar resultatet till en specifik JCR-nodtyp, både primära nodtyper och `mixin`-typer. Den hittar även undertyper av den nodtypen. Databasens sökindex måste omfatta nodtyperna för effektiv körning.

Det har stöd för facetextrahering och innehåller bucket för varje unik typ i resultatet.

#### Egenskaper {#Properties-2}

* **`type`** - nodtyp eller `mixin` namn att söka efter, till exempel `cq:Page`

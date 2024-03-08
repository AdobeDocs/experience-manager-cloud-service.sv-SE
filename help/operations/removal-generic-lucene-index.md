---
title: Generisk borttagning av Lucene-index
description: Lär dig mer om den planerade borttagningen av generiska Lucene-index och hur du kan påverkas.
exl-id: 3b966d4f-6897-406d-ad6e-cd5cda020076
source-git-commit: 53a66eac5ca49183221a1d61b825401d4645859e
workflow-type: tm+mt
source-wordcount: '1345'
ht-degree: 0%

---

# Generisk borttagning av Lucene-index {#generic-lucene-index-removal}

Adobe avser att ta bort det generiska Lucene-indexet (`/oak:index/lucene-*`) från Adobe Experience Manager as a Cloud Service. Detta index har tagits bort sedan AEM 6.5. I detta dokument beskrivs effekten av detta beslut tillsammans med detaljerade beskrivningar av hur man undersöker om en AEM påverkas. Det innehåller även sätt att ändra frågor så att de fortsätter att fungera utan det generiska Lucene-indexet.

## Bakgrund {#background}

I AEM används följande funktioner för fulltextfrågor:

* `jcr:contains ()` i JCR XPATH
* `CONTAINS` i JCR-SQL2

Sådana frågor kan inte returnera resultat utan att använda ett index. Till skillnad från en fråga som bara innehåller sökvägs- eller egenskapsbegränsningar returnerar alltid en fråga som innehåller en fullständig textbegränsning som det inte går att hitta något index för (och som därmed utför en genomgång) noll resultat.

Det generiska Lucene-indexet (`/oak:index/lucene-*`) har funnits sedan AEM 6.0/ak 1.0 för att ge en fullständig textsökning i de flesta databashierarkier, även om vissa sökvägar, som `/jcr:system` och `/var` har alltid uteslutits från detta. Indexet har dock i stort sett ersatts av index för mer specifika nodtyper (till exempel `damAssetLucene-*` för `dam:Asset` nodtyp), som har stöd för både fullständig text och egenskapssökningar.

I AEM 6.5 markerades det generiska Lucene-indexet som inaktuellt, vilket tyder på att det skulle tas bort i framtida versioner. Sedan dess har en WARN loggats när indexet har använts, vilket visas i följande loggutdrag:

```text
org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex This index is deprecated: /oak:index/lucene-2; it is used for query Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a where contains (*, 'search term') and isdescendantnode(a, '/content/mysite') /* xpath: /jcr:root/content/mysite//*[jcr:contains (.,"search term")] */ fullText="search" "term", path=/content/mysite//*). Change the query or the index definitions.
```

I de senaste AEM versionerna har det generiska Lucene-indexet använts för att stödja ett mycket litet antal funktioner. Dessa omarbetas för att använda andra index eller ändras på annat sätt för att ta bort beroendet av detta index.

Referenssökningsfrågor, till exempel i följande exempel, bör nu använda indexvärdet vid `/oak:index/pathreference`, som endast indexerar `String` egenskapsvärden som matchar ett reguljärt uttryck som söker efter JCR-sökvägar.

```text
//*[jcr:contains (., '"/content/dam/mysite"')]
```

För att ge stöd åt större kunddatavolymer skapar Adobe inte längre det generiska Lucene-indexet i nya AEM as a Cloud Service miljöer. Dessutom tar Adobe bort indexet från befintliga databaser. [Se tidslinjen](#timeline) i slutet av det här dokumentet om du vill ha mer information.

Adobe har redan justerat indexkostnaderna via `costPerEntry` och `costPerExecution` egenskaper för att säkerställa att andra index, som `/oak:index/pathreference` används i första hand när det är möjligt.

Kundprogram som använder frågor som fortfarande är beroende av detta index bör uppdateras omedelbart för att kunna använda andra befintliga index, som kan anpassas vid behov. Alternativt kan nya anpassade index läggas till i kundapplikationen. Fullständiga anvisningar för indexhantering i AEM as a Cloud Service finns i [indexeringsdokumentation](/help/operations/indexing.md).

## Är du påverkad? {#are-you-affected}

Det generiska Lucene-indexet används för närvarande som reserv om inget annat fulltextindex kan hantera en fråga. När detta inaktuella index används loggas ett meddelande som liknar följande på WARN-nivå:

```text
org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex This index is deprecated: /oak:index/lucene-2; it is used for query Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a where contains (*, 'test') /* xpath: //*[jcr:contains (.,"test")] */ fullText="test", path=*). Change the query or the index definitions.
```

I vissa fall kan Oak försöka använda ett annat fullständigt textindex (som `/oak:index/pathreference`) för att ge stöd åt den fullständiga textfrågan, men om frågesträngen inte matchar det reguljära uttrycket i indexdefinitionen, loggas ett meddelande på WARN-nivå och frågan kommer troligen inte att returnera några resultat.

```text
org.apache.jackrabbit.oak.query.QueryImpl Potentially improper use of index /oak:index/pathReference with queryFilterRegex (["']|^)/ to search for value "test"
```

När det generiska Lucene-indexet har tagits bort loggas ett meddelande som visas nedan på WARN-nivå om en fullständig textfråga inte kan hitta någon lämplig indexdefinition:

```text
org.apache.jackrabbit.oak.query.QueryImpl Fulltext query without index for filter Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a where contains (*, 'test') /* xpath: //*[jcr:contains (.,"test")] */ fullText="test", path=*); no results are returned
```

>[!IMPORTANT]
>
>**Kundåtgärd krävs**
>
> Om något av de ovannämnda varningsmeddelandena loggas kan du behöva omarbeta frågan för att använda ett annat fullständigt textindex, eller ange ett nytt index som stöd för frågan.
>
>I följande avsnitt finns information om vilka typer av beroenden du kan se och hur du åtgärdar dem.

## Potentiella beroenden på allmänna Lucene-index {#potential-dependencies}

Det finns flera områden där dina program och AEM kan vara beroende av generiska Lucene-index både på författare och publiceringsinstanser.

### Publiceringsinstans {#publish-instance}

#### Anpassade programfrågor {#custom-application-queries}

Den vanligaste källan med frågor som använder det generiska Lucene-indexet för en publiceringsinstans är anpassade programfrågor.

I de enklaste fallen kan det vara frågor som saknar nodtyp och som därmed betyder `nt:base` eller `nt:base` uttryckligen anges, till exempel:

```text
/jcr:root/content/mysite//*[jcr:contains (., 'search term')]
/jcr:root/content/mysite//element(*, nt:base)[jcr:contains (., 'search term')]
```

>[!IMPORTANT]
>
>**Kundåtgärd krävs**
>
>Ovannämnda frågor bör ändras så att en lämplig nodtyp används, vilket beskrivs i följande avsnitt.

Frågorna kan till exempel ändras så att de returnerar matchande sidor eller någon av de aggregat som finns under `cq:Page node`. Frågan kan alltså bli:

```text
/jcr:root/content/mysite//element(*, cq:Page)[jcr:contains (., 'search term')]
```

I andra fall kan en fråga ange en nodtyp men innehålla en fullständig textbegränsning som inte kan hanteras av ett annat fullständigt textindex, till exempel:

```text
/jcr:root/content/dam//element(*, dam:Asset)[jcr:contains (jcr:content/metadata/@cq:tags, 'NewsTopics:cateogries/domestic'))]
```

I det här fallet har frågan `dam:Asset` nodtyp, men innehåller en fullständig textbegränsning för den relativa `jcr:content/metadata/@cq:tags` -egenskap.

Den här egenskapen är inte markerad som analyserad i `damAssetLucene` index, som är det fulltextindex som oftast används för frågor mot `dam:Asset` nodtyp. Det går därför inte att använda det här indexet för den här frågan.

Frågan återgår därför till det generiska fulltextindexet där alla inkluderade egenskaper markeras som analyserade av jokerteckensmatchningen vid `/oak:index/lucene-2/indexRules/nt:base/properties/prop`.

>[!IMPORTANT]
>
>**Kundåtgärd krävs**
>
>Markera `jcr:content/metadata/@cq:tags` egenskapen så som den har analyserats i en anpassad version av `damAssetLucene` leder till att den här frågan hanteras av det här indexet och att ingen WARN loggas.

### Författarinstans {#author-instance}

Förutom frågor i kundens programservrar, OSGi-komponenter och återgivningsskript kan det finnas flera författarspecifika användningar av det generiska Lucene-indexet.

#### Referenssökning {#reference-search}

Historiskt sett har det generiska Lucene-indexet använts för att stödja referenssökning eller sökning efter innehåll som innehåller referenser till en annan innehållssökväg. Sådana frågor bör redan ha uppdaterats för att använda den nya `/oak:index/pathreference` index.

#### Sökväg till fältväljaren {#picker-search}

AEM innehåller en anpassad dialogkomponent med resurstypen Sling `granite/ui/components/coral/foundation/form/pathfield`, som innehåller en webbläsare/väljare för att välja en annan AEM. Standardväljaren för sökvägsfält, som används när ingen anpassad `pickerSrc` egenskapen definieras i innehållsstrukturen, vilket återger ett sökfält i popup-dialogrutan.

Nodtyperna som sökningen ska göras mot kan anges med `nodeTypes` -egenskap.

För närvarande, om inte `nodeTypes` egenskapen finns, den underliggande sökfrågan använder `nt:base` nodtyp, och därför sannolikt kommer att använda det generiska Lucene-indexet, som vanligtvis loggar WARN-meddelanden som liknar följande.

```text
20.01.2022 18:56:06.412 *WARN* [127.0.0.1 [1642704966377] POST /mnt/overlay/granite/ui/content/coral/foundation/form/pathfield/picker.result.single.html HTTP/1.1] org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex This index is deprecated: /oak:index/lucene-2; it is used for query Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a where contains (*, 'test') and isdescendantnode(a, '/content') /* xpath: /jcr:root/content//element(*, nt:base)[(jcr:contains (., 'test'))] order by @jcr:score descending */ fullText="test", path=/content//*). Change the query or the index definitions.
```

Innan det generiska Lucene-indexet tas bort ska `pathfield` -komponenten uppdateras så att sökrutan döljs för komponenter som använder standardväljaren, som inte har någon `nodeTypes` -egenskap.

| Sökvägsfältsväljaren med sökning | Sökvägsfältsväljaren utan sökning |
|---|---|
| ![Sökvägsfältsväljaren med sökning](assets/index-pathfield-picker-with-search.png) | ![Sökvägsfältsväljaren utan sökning](assets/index-pathfield-picker-without-search.png) |

>[!IMPORTANT]
>
>**Kundåtgärd krävs**
>
>Om kunden vill behålla sökfunktionen i sökvägsväljaren, en `nodeTypes` ska anges med en lista över de nodtyper som de vill fråga efter. Dessa kan anges som en kommaavgränsad lista med nodtyper i en `String` -egenskap. Om ingen sökning krävs krävs ingen åtgärd från kunden.

>[!NOTE]
>
>I Modellredigeraren för innehållsfragment används speciella sökvägsfält med resurstypen Sling `dam/cfm/models/editor/components/contentreference`.
>
> * För närvarande utför dessa frågor utan angivna nodtyper, vilket resulterar i att en WARN loggas på grund av användningen av det generiska Lucene-indexet.
> * Förekomster av de här komponenterna används snart automatiskt som standard `cq:Page` och `dam:Asset` nodtyper utan ytterligare kundåtgärder.
> * The `nodeTypes` kan läggas till för att åsidosätta dessa standardnodtyper.

## Tidslinje för allmän borttagning av Lucene {#timeline}

Adobe kommer att arbeta i två faser för att ta bort det generiska Lucene-indexet.

* **Fas 1** (planerad från den 31 januari 2022): Skapa inte längre `/oak:index/lucene-*` i nya AEM as a Cloud Service miljöer.
* **Fas 2** (planerad från och med den 31 mars 2022): Ta bort `/oak:index/lucene-*` index från befintliga AEM as a Cloud Service miljöer.

Adobe kommer att övervaka de loggmeddelanden som anges ovan och försöka kontakta kunder som är beroende av det generiska Lucene-indexet.

Som en kortsiktig begränsning lägger Adobe till anpassade indexdefinitioner direkt i kundsystemen för att förhindra funktions- eller prestandaproblem till följd av att det generiska Lucene-indexet tas bort vid behov.

I sådana fall får kunden den uppdaterade indexdefinitionen och vi rekommenderar att de inkluderar den i framtida versioner av programmet via Cloud Manager.

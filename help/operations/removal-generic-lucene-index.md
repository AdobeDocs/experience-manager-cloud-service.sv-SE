---
title: Borttagning av det generiska lucenindexet
description: Borttagning av det generiska lucenindexet
exl-id: fe0e00ac-f9c8-43cf-83c2-5a353f5eaeab
source-git-commit: bc7ef6567ad5baa4becd28a7e7d96bd6b579e1ad
workflow-type: tm+mt
source-wordcount: '1305'
ht-degree: 0%

---

# Borttagning av index för generiskt lucen

Adobe avser att ta bort det generiska lucene-indexet (`/oak:index/lucene-*`) från Adobe Experience Manager as a Cloud Service. Detta index har tagits bort sedan AEM 6.5. I denna dokumentation beskrivs effekten av detta beslut tillsammans med detaljerade beskrivningar av hur man undersöker om en AEM påverkas. Slutligen innehåller det sätt att ändra frågor så att de fungerar utan att det här indexet finns.

## Bakgrund

I AEM frågas &#39;fulltext&#39; som de som använder följande funktioner:

* `jcr:contains()` i JCR XPATH
* `CONTAINS` i JCR-SQL2

Sådana frågor kan inte returnera resultat utan att använda ett index. Till skillnad från en fråga som bara innehåller sökvägs- eller egenskapsbegränsningar returnerar alltid en fråga som innehåller en fulltextbegränsning för vilken inget index kan hittas (och således en genomgång utförs) 0 resultat.

Det generiska lucene-indexet (`/oak:index/lucene-*`) har funnits sedan AEM 6.0/ak 1.0 för att ge en fulltextsökning i de flesta databashierarkier (vissa sökvägar, som `/jcr:system` och `/var` har alltid undantagits från detta) men detta index har i stort sett ersatts av index för mer specifika nodtyper (till exempel `damAssetLucene-*` för noden&quot;dam:Asset&quot; som stöder både fulltext- och egenskapssökningar.

I AEM 6.5 markerades &quot;generiskt lucene&quot;-index som inaktuellt (vilket tyder på att det skulle tas bort i framtida versioner) och sedan dess har ett WARN loggats när indexet har använts:

```
org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex This index is deprecated: /oak:index/lucene-2; it is used for query Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a where contains(*, 'search term') and isdescendantnode(a, '/content/mysite') /* xpath: /jcr:root/content/mysite//*[jcr:contains(.,"search term")] */ fullText="search" "term", path=/content/mysite//*). Please change the query or the index definitions.
```

I de senaste AEM versionerna har det generiska lucene-indexet använts för att stödja ett mycket litet antal funktioner. Dessa omarbetas för att använda andra index eller ändras på annat sätt för att ta bort beroendet av detta index.
Exempelvis bör frågor om &#39;referenssökning&#39; i formuläret som visas nedan nu använda indexvärdet vid &#39;/ek:index/pathreference&#39; (som endast indexerar strängegenskapsvärden som matchar ett reguljärt uttryck som söker efter JCR-sökvägar). 

```
//*[jcr:contains(., '"/content/dam/mysite"')]
```

För att ge stöd åt större kunddatavolymer kommer Adobe inte längre att skapa indexet för &quot;generiskt lucen&quot; i nya AEM as a Cloud Service miljöer och kommer därefter att börja ta bort indexet från befintliga databaser. Vi har redan justerat indexkostnaderna (via egenskaperna costPerEntry och costPerExecution) för att säkerställa att andra index (som `/oak:index/pathreference`) används framför `/oak:index/lucene-*` där det är möjligt. 

Kundprogram som använder frågor som fortfarande är beroende av detta index bör uppdateras omedelbart för att kunna utnyttja andra befintliga index (som kan anpassas om det behövs) eller nya anpassade index bör läggas till i kundapplikationen. Fullständiga anvisningar för indexhantering i AEM as a Cloud Service finns på [indexeringsdokumentation](/help/operations/indexing.md).

## Hur kan du avgöra om ditt program är beroende av indexet &quot;generisk lucen&quot;?

Det generiska lucene-indexet används för närvarande som reserv om inget annat fulltextindex kan hantera en fråga. När detta inaktuella index används loggas ett meddelande som detta på WARN-nivå:

```
org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex This index is deprecated: /oak:index/lucene-2; it is used for query Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a where contains(*, 'test') /* xpath: //*[jcr:contains(.,"test")] */ fullText="test", path=*). Please change the query or the index definitions.
```

I vissa fall kan Oak försöka använda ett annat fulltextindex (som `/oak:index/pathreference`) för att ge stöd åt fulltextfrågan, men om frågesträngen inte matchar det reguljära uttrycket i indexdefinitionen, loggas ett meddelande på WARN-nivå och frågan returnerar troligen inga resultat.

```
org.apache.jackrabbit.oak.query.QueryImpl Potentially improper use of index /oak:index/pathReference with queryFilterRegex (["']|^)/ to search for value "test"
```

När det generiska lucene-indexet har tagits bort loggas ett meddelande som visas nedan på WARN-nivå om en fulltextfråga inte kan hitta någon lämplig indexdefinition:

```
org.apache.jackrabbit.oak.query.QueryImpl Fulltext query without index for filter Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a where contains(*, 'test') /* xpath: //*[jcr:contains(.,"test")] */ fullText="test", path=*); no results will be returned
```

Om något av dessa är loggat kan du behöva omarbeta frågan för att använda ett annat fulltextindex, eller ange ett nytt index som stöd för frågan. Information om de typer av beroenden som du kan se och hur du åtgärdar dem finns nedan.

## Potentiella beroenden av index för generiskt lucene

### Publicera

#### Anpassade programfrågor

Den vanligaste källan med frågor som använder indexet &quot;generisk lucen&quot; vid publicering är anpassade programfrågor.

I de enklaste fallen kan det vara frågor som inte har någon nodetype specificerad (som implementerar &quot;nt:base&quot;) eller nt:base som uttryckligen anges, till exempel:

```
/jcr:root/content/mysite//*[jcr:contains(., 'search term')]
/jcr:root/content/mysite//element(*, nt:base)[jcr:contains(., 'search term')]
```

Åtgärd krävs: Dessa frågor kan ändras så att de använder en lämplig nodtyp, till exempel för att returnera resultatmatchande sidor (eller någon av aggregaten under cq:Page-noden) som frågan kan bli:

```
/jcr:root/content/mysite//element(*, cq:Page)[jcr:contains(., 'search term')]
```

I andra fall kan en fråga ange en nodetype men innehålla en fulltextbegränsning som inte kan hanteras av ett annat fulltextindex, till exempel:

```
/jcr:root/content/dam//element(*, dam:Asset)[jcr:contains(jcr:content/metadata/@cq:tags, 'NewsTopics:cateogries/domestic'))]
```

I det här fallet har frågan nodtypen &quot;dam:Asset&quot;, men innehåller en fulltextbegränsning för den relativa `jcr:content/metadata/@cq:tags` -egenskap.

Den här egenskapen är inte markerad som &quot;analyserad&quot; i index damAssetLucene (det fulltextindex som oftast används för frågor mot noden &quot;dam:Asset&quot;) så det här indexet kan inte användas för den här frågan.

Frågan återgår därför till indexet&quot;allmän fulltext&quot; där alla inkluderade egenskaper markeras som analyserade av jokerteckensmatchningen vid `/oak:index/lucene-2/indexRules/nt:base/properties/prop`.

Kundåtgärd krävs: markera `jcr:content/metadata/@cq:tags` egenskapen som &#39;analyserad&#39; i en anpassad version av index damAssetLucene resulterar i att den här frågan hanteras av det här indexet och ingen WARN loggas.

### Författare 

Förutom frågor i kundtjänstservrar, OSGI-komponenter och återgivningsskript kan det finnas ett antal författarspecifika användningar av det generiska lucene-indexet. 

#### Referenssökning

Historiskt sett har indexet &quot;generisk lucen&quot; använts för att stödja &quot;referenssökning&quot; (sökning efter innehåll som innehåller referenser till en annan innehållssökväg). Sådana frågor bör redan ha flyttats för att använda det nya indexet &#39;/oak:index/pathreference&#39;.
Kundåtgärd krävs: ingen kundåtgärd krävs.


#### Sökväg till sökfältet

AEM innehåller en anpassad dialogkomponent (resurstypen Sling, granite/ui/components/coral/foundation/form/pathfield), som tillhandahåller en webbläsare (väljare) för att välja en annan AEM.  Standardsökvägsväljaren (används när ingen anpassad &#39;pickerSrc&#39;-egenskap har definierats i innehållsstrukturen) återger ett sökfält i popup-dialogrutan.
De nodtyper som ska sökas mot kan anges med egenskapen nodeTypes.

Om det för närvarande inte finns någon nodeTypes-egenskap kommer den underliggande sökfrågan att använda nodtypen nt:base, och därför troligen kommer att använda indexet för generiskt lucene (vanligtvis loggning av WARN-meddelanden som visas nedan).

```
20.01.2022 18:56:06.412 *WARN* [127.0.0.1 [1642704966377] POST /mnt/overlay/granite/ui/content/coral/foundation/form/pathfield/picker.result.single.html HTTP/1.1] org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex This index is deprecated: /oak:index/lucene-2; it is used for query Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a where contains(*, 'test') and isdescendantnode(a, '/content') /* xpath: /jcr:root/content//element(*, nt:base)[(jcr:contains(., 'test'))] order by @jcr:score descending */ fullText="test", path=/content//*). Please change the query or the index definitions.
```

Innan du tar bort &quot;generiskt lukt&quot; uppdateras banfältskomponenten så att sökrutan döljs för komponenter som använder standardväljaren, som inte har någon &quot;nodeTypes&quot;-egenskap.

| Banfältväljaren med sökning | Banfältväljaren utan sökning |
|---|---|
| ![Banfältväljaren med sökning](assets/index-pathfield-picker-with-search.png) | ![Banfältväljaren utan sökning](assets/index-pathfield-picker-without-search.png) |


Kundåtgärd krävs: Om ingen sökning krävs krävs ingen åtgärd från kunden.

Om kunden vill behålla sökfunktionen i sökvägsväljaren måste en egenskap, nodeTypes, anges med en lista över de nodtyper som de vill fråga efter. Dessa kan anges som en kommaavgränsad lista med nodtyper i en String-egenskap.


>[!NOTE]
>I Modellredigeraren för innehållsfragment används speciella sökvägar med Sling Resource Type &#39;dam/cfm/models/editor/components/contentreference&#39;.
> * För närvarande utför dessa frågor utan angivna nodtyper, vilket resulterar i att en WARN loggas på grund av användningen av det generiska lucene-indexet.
> * Förekomster av de här komponenterna kommer snart automatiskt att använda noderna&quot;cq:Page&quot; och&quot;dam:Asset&quot; utan ytterligare kundåtgärder.
> * Egenskapen nodeTypes kan läggas till för att åsidosätta dessa standardnodtyper. 





## Tidslinje för borttagning av generiskt lucen

Adobe kommer att arbeta i två faser för att ta bort det generiska lucenindexet.

**Fas 1** (planerad från 31 januari 2022): Skapa inte längre &#39;/oak:index/lucene-*&#39; i nya AEM as a Cloud Service miljöer.

**Fas 2** (planerad från 31 mars 2022): Ta bort index &#39;/ek:index/lucene-*&#39; från nya AEM as a Cloud Service miljöer.

Adobe kommer att övervaka de loggmeddelanden som anges ovan och försöka kontakta kunder som är beroende av det generiska lucene-indexet.

Som en kortsiktig begränsning kommer Adobe vid behov att lägga till anpassade indexdefinitioner direkt i kundsystemen för att förhindra funktions- eller prestandaproblem som en följd av att det generiska indexet &quot;lucene&quot; har tagits bort.

I sådana fall får kunden den uppdaterade indexdefinitionen och tillråds att inkludera den i framtida versioner av programmet via Cloud Manager.

---
title: Optimera GraphQL-frågor
description: Lär dig hur du optimerar dina GraphQL-frågor när du filtrerar, sidlägger och sorterar innehållsfragment i Adobe Experience Manager as a Cloud Service för leverans av headless-innehåll.
exl-id: 67aec373-4e1c-4afb-9c3f-a70e463118de
feature: Headless, Content Fragments,GraphQL API
role: Admin, Developer
source-git-commit: bdf3e0896eee1b3aa6edfc481011f50407835014
workflow-type: tm+mt
source-wordcount: '1874'
ht-degree: 0%

---

# Optimera GraphQL-frågor {#optimizing-graphql-queries}

>[!NOTE]
>
>Innan optimeringsrekommendationerna tillämpas bör du överväga att [uppdatera innehållsfragmenten för sidindelning och sortering i GraphQL-filtrering](/help/headless/graphql-api/graphql-optimized-filtering-content-update.md) för bästa prestanda.

Riktlinjerna är till för att förhindra prestandaproblem i dina GraphQL-frågor.

## GraphQL Checklist {#graphql-checklist}

Följande checklista hjälper dig att optimera konfigurationen och användningen av GraphQL i Adobe Experience Manager (AEM) as a Cloud Service.

### Första principerna {#first-principles}

#### Använd beständiga GraphQL-frågor {#use-persisted-graphql-queries}

**Rekommendation**

Vi rekommenderar starkt att du använder beständiga GraphQL-frågor.

Med permanenta GraphQL-frågor kan du minska frågekörningsprestanda genom att använda CDN (Content Delivery Network). Klientprogram begär beständiga frågor med GET-förfrågningar för snabb körning.

**Ytterligare referens**

Se:

* [Beständiga GraphQL-frågor](/help/headless/graphql-api/persisted-queries.md).
* [Lära sig använda GraphQL med AEM - exempelinnehåll och frågor](/help/headless/graphql-api/sample-queries.md)

### Cachestrategi {#cache-strategy}

Olika metoder för cachning kan också användas för optimering.

#### Aktivera AEM Dispatcher-cachelagring {#enable-aem-dispatcher-caching}

**Rekommendation**

[AEM Dispatcher](/help/implementing/dispatcher/overview.md) är den första nivån i AEM, före CDN-cache.

**Ytterligare referens**

Se:

* [GraphQL Persisted Queries - aktivera cachelagring i Dispatcher](/help/headless/deployment/dispatcher-caching.md)

#### Använd ett CDN (Content Delivery Network) {#use-cdn}

**Rekommendation**

GraphQL-frågor och deras JSON-svar kan cachelagras om de är riktade som `GET`-begäranden när ett CDN används. Icke cachelagrade begäranden kan däremot vara mycket (resurskrävande) och långsamma att behandla, vilket kan få ytterligare negativa effekter på ursprungsmaterialets resurser.

**Ytterligare referens**

Se:

* [CDN i AEM AS A CLOUD SERVICE](/help/implementing/dispatcher/cdn.md)

#### Ange rubriker för HTTP-cachekontroll {#set-http-cache-control-headers}

**Rekommendation**

När du använder beständiga GraphQL-frågor med ett CDN bör du ange lämpliga rubriker för HTTP-cachekontroll.

Varje beständig fråga kan ha sin egen uppsättning specifika cachekontrollrubriker. Rubrikerna kan ställas in över [GraphQL API](/help/headless/graphql-api/content-fragments.md) eller [AEM GraphiQL IDE](/help/headless/graphql-api/graphiql-ide.md) .

**Ytterligare referens**

Se:

* [Cachelagra beständiga frågor](/help/headless/graphql-api/persisted-queries.md#caching-persisted-queries)
* [Hantera cache för dina beständiga frågor](/help/headless/graphql-api/graphiql-ide.md#managing-cache)

#### Använd AEM GraphQL-förcachelagring {#use-aem-graphql-pre-caching}

**Rekommendation**

Med den här funktionen kan AEM cache-lagra innehåll ytterligare inom GraphQL-frågeintervallet som sedan kan sammanställas som block i JSON-utdata i stället för rad för rad.

**Ytterligare referens**

Kontakta Adobe för att aktivera den här funktionen för ditt AEM Cloud Service-program och -miljöer.

### GraphQL Query Optimization {#graphql-query-optimization}

I en AEM med ett stort antal innehållsfragment som delar samma modell kan GraphQL listfrågor bli dyra (i form av resurser).

Detta beror på att *alla* fragment som delar en modell som används i GraphQL-frågan måste läsas in i minnet. Detta förbrukar både tid och minne. Filtrering, som kan minska antalet objekt i den (slutliga) resultatuppsättningen, kan bara tillämpas **efter** att hela resultatuppsättningen har lästs in i minnet.

Detta kan leda till att även små resultatuppsättningar (kan) ger sämre prestanda. I själva verket beror dock avmattningen på storleken på den ursprungliga resultatmängden, eftersom den måste hanteras internt innan filtrering kan tillämpas.

För att minska prestanda- och minnesproblem måste den här första resultatmängden hållas så liten som möjligt.

I AEM finns det två sätt att optimera GraphQL-frågor:

* [Hybridfiltrering](#use-aem-graphql-hybrid-filtering)
* [Sidindelning](#use-aem-graphql-pagination) (eller sidindelning)

   * [Sortering](#use-graphql-sorting) är inte direkt relaterat till optimering, men är relaterat till sidindelning

Varje metod har sina egna användningsfall och begränsningar. I det här avsnittet finns information om Hybrid-filtrering och sidindelning, tillsammans med några av de [bästa metoderna](#best-practices) som kan användas för att optimera GraphQL-frågor.

#### Använd AEM GraphQL hybridfiltrering {#use-aem-graphql-hybrid-filtering}

**Rekommendation**

Hybridfiltrering kombinerar JCR-filtrering med AEM.

Det tillämpar ett JCR-filter (i form av en frågebegränsning) innan resultatuppsättningen läses in i minnet för AEM filtrering. Detta för att minska mängden resultat som läses in i minnet, eftersom JCR-filtret tar bort överflödiga resultat före detta.

>[!NOTE]
>
>Av tekniska skäl (t.ex. flexibilitet, kapsling av fragment) kan AEM inte delegera hela filtreringen till JCR.

Den här tekniken ger den flexibilitet som GraphQL-filter ger och delegerar så mycket av filtreringen som möjligt till JCR.

>[!NOTE]
>
>AEM Hybrid-filtrering kräver uppdatering av befintliga innehållsfragment

**Ytterligare referens**

Se:

* [Uppdatera dina innehållsfragment för sidindelning och sortering i GraphQL-filtrering](/help/headless/graphql-api/graphql-optimized-filtering-content-update.md)
* [Exempelfråga med filtrering efter _tagg-ID och utan variationer](/help/headless/graphql-api/sample-queries.md#sample-filtering-tag-not-variations)

#### Använd GraphQL sidnumrering {#use-aem-graphql-pagination}

**Rekommendation**

Svarstiden för komplexa frågor, med stora resultatuppsättningar, kan förbättras genom att svaren delas i segment med hjälp av sidnumrering, en GraphQL-standard.

GraphQL i AEM har stöd för två typer av sidnumrering:

* [begränsa/förskjutningsbaserad sidnumrering](/help/headless/graphql-api/content-fragments.md#list-offset-limit)
Detta används för listfrågor, som avslutas med `List` , till exempel `articleList` .
Om du vill använda det måste du ange positionen för det första objektet som ska returneras (`offset`) och antalet objekt som ska returneras (`limit`, eller sidstorleken).

* [markörbaserad sidnumrering](/help/headless/graphql-api/content-fragments.md#paginated-first-after) (representeras av `first` och `after`)
Detta ger ett unikt ID för varje objekt, som också kallas markör.
I frågan anger du markören för det sista objektet på föregående sida plus sidstorleken (det maximala antalet objekt som ska returneras).

  Eftersom markörbaserad sidnumrering inte passar i de listbaserade frågornas datastrukturer har AEM introducerat `Paginated`-frågetyp, till exempel `articlePaginated`. De datastrukturer och parametrar som används följer [GraphQL Cursor ConnectionSpecification](https://relay.dev/graphql/connections.htm).

  >[!NOTE]
  >
  >AEM har för närvarande stöd för framåtriktad sidindelning (med `after`/`first` parametrar).
  >
  >Bakåtväxling (med `before`/`last` parametrar) stöds inte.

**Ytterligare referens**

Se:

* [Exempelsidnumreringsfråga som använder första och efter](/help/headless/graphql-api/sample-queries.md#sample-pagination-first-after)

#### Använda GraphQL sortering {#use-graphql-sorting}

**Rekommendation**

Sortering är också en GraphQL-standard som gör att klienter kan ta emot JSON-innehåll i sorterad ordning. Detta kan minska behovet av ytterligare bearbetning på klienten.

Sortering kan bara vara effektivt om alla sorteringsvillkor är relaterade till fragment på den översta nivån.

Om sorteringsordningen innehåller ett eller flera fält som finns i ett kapslat fragment, måste alla fragment som delar modellen på den översta nivån läsas in i minnet. Detta orsakar en negativ prestandapåverkan.

>[!NOTE]
>
>Sortering av fält på den översta nivån har också (om än liten) inverkan på prestandan.

**Ytterligare referens**

Se:

* [Exempelfråga med filtrering efter _taggar ID och utan variationer, och sortera efter namn](/help/headless/graphql-api/sample-queries.md#sample-filtering-tag-not-variations)

## Bästa praxis {#best-practices}

Det främsta målet för alla optimeringsrekommendationer är att minska den inledande resultatmängden. De bästa metoderna som listas här ger olika sätt att göra detta. De kan (och bör) kombineras.

### Filtrera endast på egenskaper på den översta nivån {#filter-top-level-properties-only}

För närvarande fungerar filtrering på JCR-nivå bara för fragment på den översta nivån.

Om ett filter åtgärdar fälten i ett kapslat fragment måste AEM återgå till att läsa in (i minnet) alla fragment som delar den underliggande modellen.

Du kan fortfarande optimera sådana GraphQL-frågor genom att kombinera filteruttryck i fält med fragment på översta nivån och i fält med kapslade fragment med operatorn [AND](#logical-operations-in-filter-expressions).

### Använda innehållsstrukturen {#use-content-structure}

I AEM anses det som god praxis att använda databasstrukturen för att begränsa omfattningen av det innehåll som ska behandlas.

Detta arbetssätt bör även tillämpas på GraphQL-frågor.

Detta kan du göra genom att använda ett filter i fältet `_path` i fragmentet på den översta nivån:

```graphql
{
  someList(filter: {
    _path: {
      _expressions: [ 
        {
          value: "/content/dam/some/sub/path/",
          _operator: STARTS_WITH
        }
      ]
    }
  }) {
    items {
      # ...
    }
  }
}
```

>[!NOTE]
>
>Den avslutande `/` på `value` krävs för att uppnå bästa prestanda.

### Använd sidindelning {#use-paging}

Du kan också använda sidindelning för att minska den ursprungliga resultatmängden, särskilt om dina förfrågningar inte använder någon filtrering eller sortering.

Om du filtrerar eller sorterar efter kapslade fragment kan sidnumrerade frågor fortfarande ta lång tid eftersom AEM kan behöva läsa in större mängder fragment i minnet. Om du kombinerar filtrering och sidindelning bör du därför överväga reglerna för filtrering (som nämns ovan).

För sidindelning är sortering lika viktigt eftersom paginerade resultat alltid sorteras - antingen explicit eller implicit.

Om du i första hand är intresserad av att bara hämta de första sidorna finns det ingen större skillnad mellan att använda `...List`- och `...Paginated`-frågorna. Om ditt program är intresserat av att läsa mer än en eller två sidor bör du överväga frågan `...Paginated` eftersom den fungerar betydligt bättre med de senare sidorna.

### Logiska åtgärder i filteruttryck {#logical-operations-in-filter-expressions}

Om du filtrerar kapslade fragment kan du fortfarande tillämpa JCR-filtrering genom att tillhandahålla ett medföljande filter på ett fält på den översta nivån som kombineras med operatorn `AND`.

Ett typiskt användningsfall skulle vara att begränsa frågans omfattning med ett filter i fältet `_path` i fragmentet på den översta nivån och sedan filtrera på ytterligare fält som kan finnas på den översta nivån, eller på ett kapslat fragment.

I det här fallet kombineras de olika filteruttrycken med `AND`. Därför kan filtret på `_path` effektivt begränsa den inledande resultatmängden. Alla andra filter i fält på den översta nivån kan även hjälpa till att minska den inledande resultatmängden, så länge de kombineras med `AND`.

Filteruttryck som kombinerats med `OR` kan inte optimeras om kapslade fragment är inblandade. `OR`-uttryck kan bara optimeras om *inga* kapslade fragment är inblandade.

### Undvik filtrering i textfält med flera rader {#avoid-filtering-multiline-textfields}

Fälten i ett textfält med flera rader (html, markdown, plaintext, json) kan inte filtreras via en JCR-fråga eftersom innehållet i dessa fält måste beräknas direkt.

Om du fortfarande behöver filtrera i ett textfält med flera rader bör du begränsa storleken på den ursprungliga resultatmängden genom att lägga till ytterligare filteruttryck och kombinera dem med `AND`. Det är också bra att begränsa omfånget genom att filtrera fältet `_path`.

### Undvik filtrering i virtuella fält {#avoid-filtering-virtual-fields}

Virtuella fält (de flesta fält som börjar med `_`) beräknas medan en GraphQL-fråga körs och ligger därför utanför JCR-baserad filtrering.

Ett viktigt undantag är fältet `_path`, som kan användas effektivt för att minska storleken på den ursprungliga resultatmängden, om innehållet är strukturerat därefter (se [Använd innehållsstrukturen](#use-content-structure)).

### Filtrera: Undantag {#filtering-exclusions}

Det finns flera andra situationer där ett filteruttryck inte kan utvärderas på JCR-nivån (och därför bör undvikas för att uppnå bästa prestanda):

* Filtrera uttryck på ett `Float`-värde som använder filteralternativet `_sensitiveness` och där `_sensitiveness` är inställt på något annat än `0.0` .

* Filtrera uttryck på ett `String`-värde med filteralternativet `_ignoreCase`.

* Filtrerar på `null`-värden.

* Filter på arrayer med `_apply: ALL_OR_EMPTY`.

* Filter på arrayer med `_apply: INSTANCES`, `_instances: 0`.

* Filtrera uttryck med operatorn `CONTAINS_NOT`.

* Filtrera uttryck på ett `Calendar`-, `Date`- eller `Time`-värde som använder operatorn `NOT_AT`.

### Minimera innehållets fragmentkapsling {#minimize-content-fragment-nesting}

Att kapsla innehållsfragment är ett bra sätt att modellera anpassade innehållsstrukturer. Du kan till och med ha ett fragment med ett kapslat fragment, som också har ett kapslat fragment, som har ...och så vidare.

Om du skapar en struktur med för många nivåer kan bearbetningstiden för en GraphQL-fråga öka, eftersom GraphQL måste gå igenom hela hierarkin för alla kapslade innehållsfragment.

Djupkapsling kan också ha negativa effekter på innehållsstyrningen. I allmänhet bör du begränsa innehållets fragmentkapsling till under fem eller sex nivåer.

### Alla format skrivs inte ut (textelement med flera rader) {#do-not-output-all-formats}

AEM GraphQL kan returnera text, som har skapats i datatypen **[Flera rader](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#data-types)**, i flera format: RTF, Enkel text och Markering.

Om du skriver ut alla tre formaten ökar textutdatafilens storlek i JSON med faktorn tre. Detta i kombination med i allmänhet stora resultatuppsättningar från mycket breda frågor kan skapa mycket stora JSON-svar som därför tar lång tid att beräkna. Det är bättre att begränsa utdata till endast de textformat som krävs för återgivning av innehållet.

### Ändra innehållsfragment {#modifying-content-fragments}

Ändra bara innehållsfragment och deras resurser med hjälp av AEM gränssnitt eller API:er. Gör inga ändringar direkt i JCR.

### Testa dina frågor {#test-your-queries}

Bearbetning av GraphQL-frågor liknar bearbetning av sökfrågor och är betydligt mer komplicerat än enkel GET-all-content-API-begäran.

Att planera, testa och optimera frågor i en kontrollerad icke-produktionsmiljö är avgörande för att det ska gå bra vid senare användning i produktionen.

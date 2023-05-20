---
title: Optimera GraphQL-frågor
description: Lär dig hur du optimerar dina GraphQL-frågor när du filtrerar, sidlägger och sorterar innehållsfragment i Adobe Experience Manager as a Cloud Service för leverans av headless-innehåll.
exl-id: 67aec373-4e1c-4afb-9c3f-a70e463118de
source-git-commit: 9cff6e94b38016f008fd8177be2e071a530d80b6
workflow-type: tm+mt
source-wordcount: '1192'
ht-degree: 0%

---

# Optimera GraphQL-frågor {#optimizing-graphql-queries}

>[!NOTE]
>
>Innan optimeringsrekommendationerna tillämpas bör du överväga [Uppdatera dina innehållsfragment för sidindelning och sortering i GraphQL-filtrering](/help/headless/graphql-api/graphql-optimized-filtering-content-update.md) för bästa prestanda.

I en AEM med ett stort antal innehållsfragment som delar samma modell kan GraphQL listfrågor bli dyra (i form av resurser).

Det beror på att *alla* fragment som delar en modell som används i GraphQL-frågan måste läsas in i minnet. Detta förbrukar både tid och minne. Filtrering, som kan minska antalet objekt i den (slutliga) resultatmängden, kan bara användas **efter** läser in hela resultatuppsättningen i minnet.

Detta kan leda till att även små resultatuppsättningar (kan) ger sämre prestanda. I själva verket beror dock avmattningen på storleken på den ursprungliga resultatmängden, eftersom den måste hanteras internt innan filtrering kan tillämpas.

För att minska prestanda- och minnesproblem måste den här första resultatmängden hållas så liten som möjligt.

I AEM finns det två sätt att optimera GraphQL-frågor:

* [Hybridfiltrering](#hybrid-filtering)
* [Sidindelning](#paging) (eller sidnumrering)

   * [Sortering](#sorting) är inte direkt relaterat till optimering, men är relaterat till sidindelning

Varje metod har sina egna användningsfall och begränsningar. Det här dokumentet innehåller information om hybridfiltrering och sidindelning, med vissa [bästa praxis](#best-practices) för att optimera GraphQL-frågor.

## Hybridfiltrering {#hybrid-filtering}

Hybridfiltrering kombinerar JCR-filtrering med AEM.

Det tillämpar ett JCR-filter (i form av en frågebegränsning) innan resultatuppsättningen läses in i minnet för AEM filtrering. Detta för att minska mängden resultat som läses in i minnet, eftersom JCR-filtret tar bort överflödiga resultat före detta.

>[!NOTE]
>
>Av tekniska skäl (t.ex. flexibilitet, kapsling av fragment) kan AEM inte delegera hela filtreringen till JCR.

Den här tekniken ger den flexibilitet som GraphQL-filter ger och delegerar så mycket av filtreringen som möjligt till JCR.

## Sidindelning {#paging}

GraphQL i AEM har stöd för två typer av sidnumrering:

* [limit/offset-baserad sidnumrering](/help/headless/graphql-api/content-fragments.md#list-offset-limit)
Detta används för listfrågor. slutar med 
`List`; till exempel `articleList`.
Om du vill använda den måste du ange positionen för det första objektet som ska returneras ( `offset`) och antalet objekt som ska returneras ( `limit`, eller sidstorlek).

* [markörbaserad sidnumrering](/help/headless/graphql-api/content-fragments.md#paginated-first-after) (representeras av `first`och `after`) Detta ger ett unikt ID för varje objekt. kallas också markör.
I frågan anger du markören för det sista objektet på föregående sida plus sidstorleken (det maximala antalet objekt som ska returneras).

   Eftersom markörbaserad sidnumrering inte passar i de listbaserade frågestrukturerna har AEM infört `Paginated` frågetyp; till exempel `articlePaginated`. De datastrukturer och parametrar som används följer [GraphQL Cursor ConnectionSpecification](https://relay.dev/graphql/connections.htm).

   >[!NOTE]
   >
   >AEM har för närvarande stöd för sidväxling framåt (med `after`/`first` parametrar).
   >
   >Bakåt sidindelning (med `before`/`last` parametrar) stöds inte.

## Sortering {#sorting}

Sortering kan bara vara effektivt om alla sorteringsvillkor är relaterade till fragment på den översta nivån.

Om sorteringsordningen innehåller ett eller flera fält som finns i ett kapslat fragment, måste alla fragment som delar modellen på den översta nivån läsas in i minnet. Detta orsakar en negativ prestandapåverkan.

>[!NOTE]
>
>Sortering av fält på den översta nivån har också (om än liten) inverkan på prestandan.

## Bästa praxis {#best-practices}

Det främsta målet för alla optimeringar är att minska den inledande resultatmängden. De bästa metoderna som listas här ger olika sätt att göra detta. De kan (och bör) kombineras.

### Filtrera endast på egenskaper på den översta nivån {#filter-top-level-properties-only}

För närvarande fungerar filtrering på JCR-nivå bara för fragment på den översta nivån.

Om ett filter åtgärdar fälten i ett kapslat fragment måste AEM återgå till att läsa in (i minnet) alla fragment som delar den underliggande modellen.

Du kan fortfarande optimera sådana GraphQL-frågor genom att kombinera filteruttryck i fält med fragment på översta nivån och de på fält i kapslade fragment med [AND-operator](#logical-operations-in-filter-expressions).

### Använda innehållsstrukturen {#use-content-structure}

I AEM anses det som god praxis att använda databasstrukturen för att begränsa omfattningen av det innehåll som ska behandlas.

Detta arbetssätt bör även tillämpas på GraphQL-frågor.

Detta kan du göra genom att använda ett filter på `_path` fältet för fragmentet på den översta nivån:

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
>Efterföljande `/` på `value` krävs för att uppnå bästa prestanda.

### Använd sidindelning {#use-paging}

Du kan också använda sidindelning för att minska den inledande resultatmängden. särskilt om din begäran inte använder någon filtrering eller sortering.

Om du filtrerar eller sorterar efter kapslade fragment kan sidnumrerade frågor fortfarande ta lång tid eftersom AEM kan behöva läsa in större mängder fragment i minnet. Om du kombinerar filtrering och sidindelning bör du därför överväga reglerna för filtrering (som nämns ovan).

För sidindelning är sortering lika viktigt eftersom paginerade resultat alltid sorteras - antingen explicit eller implicit.

Om du är mest intresserad av att bara hämta de första sidorna är det ingen större skillnad mellan att använda `...List` eller `...Paginated` frågor. Om ditt program är intresserat av att läsa mer än en eller två sidor bör du överväga `...Paginated` fråga eftersom den fungerar betydligt bättre med de senare sidorna.

### Logiska åtgärder i filteruttryck {#logical-operations-in-filter-expressions}

Om du filtrerar kapslade fragment kan du fortfarande utnyttja JCR-filtrering genom att tillhandahålla ett medföljande filter på ett fält på den översta nivån som kombineras med `AND` -operator.

Ett vanligt användningsfall skulle vara att begränsa frågans omfattning med hjälp av ett filter på `_path` -fältet i fragmentet på den översta nivån och filtrera sedan efter ytterligare fält som kan finnas på den översta nivån eller på ett kapslat fragment.

I det här fallet kombineras de olika filteruttrycken med `AND`. Därför är filtret aktiverat `_path` kan effektivt begränsa den inledande resultatmängden. Alla andra filter i fält på den översta nivån kan även bidra till att minska den inledande resultatmängden, så länge som de kombineras med `AND`.

Filtrera uttryck i kombination med `OR` kan inte optimeras om kapslade fragment är inblandade. `OR` uttryck kan bara optimeras om *no* kapslade fragment är inblandade.

### Undvik filtrering i textfält med flera rader {#avoid-filtering-multiline-textfields}

Fälten i ett textfält med flera rader (html, markdown, plaintext, json) kan inte filtreras via en JCR-fråga eftersom innehållet i dessa fält måste beräknas direkt.

Om du fortfarande behöver filtrera i ett textfält med flera rader bör du begränsa storleken på det ursprungliga resultatet genom att lägga till ytterligare filteruttryck och kombinera dem med `AND`. Begränsa omfånget genom att filtrera på `_path` -fältet är också en bra metod.

### Undvik filtrering i virtuella fält {#avoid-filtering-virtual-fields}

Virtuella fält (de flesta fält börjar med `_`) beräknas medan en GraphQL-fråga körs och ligger därför utanför JCR-baserad filtrering.

Ett viktigt undantag är `_path` -fält, som kan användas effektivt för att minska storleken på den ursprungliga resultatmängden - om innehållet är strukturerat därefter (se [Använda innehållsstrukturen](#use-content-structure)).

### Filtrering: Undantag {#filtering-exclusions}

Det finns flera andra situationer där ett filteruttryck inte kan utvärderas på JCR-nivån (och därför bör undvikas för att uppnå bästa prestanda):

* Filtrera uttryck på en `Float` värdet som använder `_sensitiveness` filteralternativ, och var `_sensitiveness` är inställt på något annat än `0.0` .

* Filtrera uttryck på en `String` värdet med `_ignoreCase` filteralternativ.

* Filtrera på `null` värden.

* Filter på arrayer med `_apply: ALL_OR_EMPTY`.

* Filter på arrayer med `_apply: INSTANCES`, `_instances: 0`.

* Filtrera uttryck med `CONTAINS_NOT` -operator.

* Filtrera uttryck på en `Calendar`, `Date` eller `Time` värdet som använder `NOT_AT` -operator.

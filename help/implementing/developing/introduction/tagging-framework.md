---
title: AEM Taggningsramverk
description: Tagga innehåll och utnyttja infrastrukturen för AEM taggar för att kategorisera och organisera det.
translation-type: tm+mt
source-git-commit: 4bf023068aa69fb6b69c6f2443703ea2bbbf7d42
workflow-type: tm+mt
source-wordcount: '1567'
ht-degree: 0%

---


# AEM Taggning Framework {#aem-tagging-framework}

Taggning gör att innehållet kan kategoriseras och struktureras. Taggar kan klassificeras med ett namnutrymme och en taxonomi. Mer information om hur du använder taggar:

* Mer information om hur du taggar innehåll som innehållsförfattare finns i [Använda taggar](/help/sites-cloud/authoring/features/tags.md) .
* Se Administrera taggar för en administratörs perspektiv om hur du skapar och hanterar taggar, samt vilka innehållstaggar som har tillämpats.

Den här artikeln fokuserar på det underliggande ramverket som stöder taggning i AEM och hur det kan utnyttjas som utvecklare.

## Introduktion {#introduction}

Så här taggar du innehåll och använder infrastrukturen för AEM taggar:

* Taggen måste finnas som en nod av typen [`cq:Tag`](#cq-tag-node-type) under [taxonomirotnoden.](#taxonomy-root-node)
* Den taggade innehållsnodens `NodeType` måste innehålla [`cq:Taggable`](#taggable-content-cq-taggable-mixin) mixin.
* Innehållet [`TagID`](#tagid) läggs till i innehållsnodens [`cq:tags`](#cq-tags-property) egenskap och löses till en nod av typen [`cq:Tag`.](#cq-tag-node-type)

## cq:Tag Node Type {#cq-tag-node-type}

Deklarationen för en tagg hämtas i databasen i en nod av typen `cq:Tag.`

* En tagg kan vara ett enkelt ord (t.ex. `sky`) eller representerar en hierarkisk taxonomi (t.ex. `fruit/apple`, vilket innebär både den generiska frukten och det mer specifika äpplet).
* Taggar identifieras av unika `TagID`.
* En tagg har valfri metainformation, t.ex. en titel, lokaliserade titlar och en beskrivning. Titeln ska visas i användargränssnitt i stället för `TagID`, om det finns.

Med taggningsramverket kan du även begränsa möjligheten för författare och besökare att endast använda specifika, fördefinierade taggar.

### Märkordsegenskaper {#tag-characteristics}

* Nodtypen är `cq:Tag`.
* Nodnamnet är en komponent i [`TagID`.](#tagid)
* Det [`TagID`](#tagid) innehåller alltid ett [namnutrymme.](#tag-namespace)
* Egenskapen `jcr:title` (den titel som ska visas i användargränssnittet) är valfri.
* The `jcr:description` property is optional.
* När det innehåller underordnade noder kallas det en [behållartagg.](#container-tags)
* Taggen lagras i databasen under en bassökväg som kallas [taxonomirotnod.](#taxonomy-root-node)

### TaggID {#tagid}

En `TagID` identifierar en sökväg som löses till en taggnod i databasen.

Normalt `TagID` börjar en förkortning `TagID` med namnutrymmet eller så kan det vara en absolut `TagID` början från [taxonomirotnoden.](#taxonomy-root-node)

Om innehållet är taggat och inte finns än, läggs egenskapen till i innehållsnoden och [`cq:tags`](#cq-tags-property) läggs till i egenskapens `TagID` `String` arrayvärde.

Den `TagID` består av ett [namnutrymme](#tag-namespace) följt av det lokala `TagID`. [Behållartaggar](#container-tags) har undertaggar som representerar en hierarkisk ordning i taxonomin. Undertaggar kan användas för att referera till taggar som är identiska med andra lokala taggar `TagID`. Det är till exempel tillåtet att tagga innehåll med `fruit` , även om det är en behållartagg med undertaggar, till exempel `fruit/apple` och `fruit/banana`.

### Taxonomirotnod {#taxonomy-root-node}

Taxonomirotnoden är grundsökvägen för alla taggar i databasen. Rotnoden taxonomi får *inte* vara en nod av typen `cq:Tag`.

I AEM är bassökvägen `/content/cq:tags` och rotnoden är av typen `cq:Folder`.

### Namnutrymme för tagg {#tag-namespace}

Med namnutrymmen kan du gruppera saker. Det vanligaste användningsfallet är att ha ett namnutrymme per plats (till exempel public kontra internal) eller per större program (till exempel platser eller resurser), men namnutrymmen kan användas för olika andra behov. Namnutrymmen används i användargränssnittet för att endast visa deluppsättningen taggar (d.v.s. taggar för ett visst namnutrymme) som är tillämpliga för det aktuella innehållet.

Taggens namnutrymme är den första nivån i taxonomiunderträdet, som är noden direkt under [taxonomirotnoden.](#taxonomy-root-node) Ett namnutrymme är en nod av typen `cq:Tag` vars överordnade nod inte är en `cq:Tag` nodtyp.

Alla taggar har ett namnutrymme. Om inget namnutrymme anges tilldelas taggen standardnamnutrymmet, d.v.s. `TagID``default`. `/content/cq:tags/default`.  I så `Standard Tags`fall används standardinställningen Titel.

### Behållartaggar {#container-tags}

En behållartagg är en nod av typen `cq:Tag` som innehåller valfritt antal och typ av underordnade noder, vilket gör det möjligt att förbättra taggmodellen med anpassade metadata.

Dessutom fungerar behållartaggar (eller supertaggar) i en taxonomi som delsummering av alla undertaggar: innehåll som du till exempel taggar med `fruit/apple` också anses vara taggat med, `fruit` vilket innebär att om du söker efter innehåll som du just taggat med `fruit` så hittas även innehållet som du taggar med `fruit/apple`.

### Lösa tagg-ID:n {#resolving-tagids}

Om tagg-ID:t innehåller ett kolon (`:`) separerar kolonet namnutrymmet från taggen eller subtaxonomin, som sedan separeras med normala snedstreck (`/`). Om tagg-ID:t inte har ett kolon används standardnamnutrymmet.

Standardplatsen och den enda platsen för taggar är under `/content/cq:tags`.

Taggar som refererar till icke-befintliga sökvägar eller sökvägar som inte pekar på en `cq:Tag` nod betraktas som ogiltiga och ignoreras.

I följande tabell visas några exempel, `TagID`deras element och hur `TagID` tolkas till en absolut sökväg i databasen:

| `TagID` | Namnutrymme | Lokalt ID | Behållartaggar | Lövtagg | Databassökväg för absolut tagg |
|---|---|---|---|---|---|
| `dam:fruit/apple/braeburn` | `dam` | `fruit/apple/braeburn` | `fruit`,`apple` | `braeburn` | `content/cq:tags/dam/fruit/apple/braeburn` |
| `color/red` | `default` | `color/red` | `color` | `red` | `/content/cq:tags/default/color/red` |
| `sky` | `default` | `sky` | (inga) | `sky` | `/content/cq:tags/default/sky` |
| `dam:` | `dam` | (inga) | (inga) | (inga) | `/content/cq:tags/dam` |
| `content/cq:tags/category/car` | `category` | `car` | `car` | `car` | `content/cq:tags/category/car` |

### Lokalisering av taggtitel {#localization-of-tag-title}

När taggen innehåller den valfria titelsträngen `jcr:title`går det att lokalisera titeln för visning genom att lägga till egenskapen `jcr:title.<locale>`.

Mer information finns i:

* [Taggar på olika språk,](tagging-applications.md#tags-in-different-languages) som beskriver hur API:erna används som utvecklare
* Hantera taggar på olika språk, som beskriver hur du använder taggningskonsolen som administratör

### Åtkomstkontroll {#access-control}

Taggar finns som noder i databasen under [taxonomirotnoden.](#taxonomy-root-node) Du kan skapa taggar i ett givet namnutrymme genom att ange lämpliga åtkomstkontrollistor i databasen, så att författare och besökare kan neka eller neka åtkomst.

Om du nekar läsbehörighet för vissa taggar eller namnutrymmen kan du styra möjligheten att använda taggar för visst innehåll.

Ett typiskt exempel är:

* Tillåta skrivåtkomst för grupper/roller till alla namnutrymmen (lägg till/ändra under `tag-administrators` `/content/cq:tags`). Den här gruppen levereras med AEM.
* Ge användare/författare läsåtkomst till alla namnutrymmen som ska vara läsbara för dem (oftast alla).
* Ge användare/författare skrivåtkomst till de namnutrymmen där taggar ska kunna definieras fritt av användare/författare (`add_node` under `/content/cq:tags/some_namespace`)

## Taggbart innehåll: cq:Taggable Mixin {#taggable-content-cq-taggable-mixin}

För att programutvecklare ska kunna bifoga taggning till en innehållstyp måste nodens registrering ([CND](https://jackrabbit.apache.org/node-type-notation.html)) innehålla `cq:Taggable` mixin eller `cq:OwnerTaggable` mixin.

Den `cq:OwnerTaggable` mixin som ärver från `cq:Taggable`är avsedd att indikera att innehållet kan klassificeras av ägaren/författaren. I AEM är det bara ett attribut för `cq:PageContent` noden. Blandningen krävs inte av `cq:OwnerTaggable` taggningsramverket.

>[!NOTE]
>
>Du bör bara aktivera taggar på den översta noden i ett aggregerat innehållsobjekt (eller på dess `jcr:content` nod). Exempel:
>
>* Sidor (`cq:Page`) där `jcr:content`noden är av typen `cq:PageContent`, som innehåller `cq:Taggable` mixen.
>* Resurser (`cq:Asset`) där `jcr:content/metadata` noden alltid har `cq:Taggable` mixin.


### Nodtypsnotation (CND) {#node-type-notation-cnd}

Det finns nodtypsdefinitioner i databasen som CND-filer. CND-notation definieras som en del av [JCR-dokumentationen.](https://jackrabbit.apache.org/node-type-notation.html).

De viktigaste definitionerna för de nodtyper som ingår i AEM är följande:

```xml
[cq:Tag] > mix:title, nt:base
    orderable
    - * (undefined) multiple
    - * (undefined)
    + * (nt:base) = cq:Tag version

[cq:Taggable]
    mixin
    - cq:tags (string) multiple

[cq:OwnerTaggable] > cq:Taggable
    mixin
```

## cq:tagg, egenskap {#cq-tags-property}

Egenskapen `cq:tags` är en `String` array som används för att lagra en eller flera `TagID`s när de tillämpas på innehåll av författare eller webbplatsbesökare. Egenskapen har bara betydelse när den läggs till i en nod som definieras med [`cq:Taggable`](#taggable-content-cq-taggable-mixin) mixin.

>[!NOTE]
>
>För att utnyttja AEM taggningsfunktion bör anpassade utvecklade program inte definiera andra taggegenskaper än `cq:tags`.

## Flytta och sammanfoga taggar {#moving-and-merging-tags}

Nedan följer en beskrivning av effekterna i databasen när du flyttar eller sammanfogar taggar med hjälp av taggningskonsolen.

När tagg A flyttas eller sammanfogas till tagg B under `/content/cq:tags`:

* Tagg A tas inte bort och får en `cq:movedTo` egenskap.
   * `cq:movedTo` pekar på tagg B.
   * Den här egenskapen innebär att tagg A har flyttats eller sammanfogats till tagg B.
   * Om du flyttar tagg B uppdateras den här egenskapen i enlighet med detta.
   * Tagg A är alltså dold och sparas bara i databasen för att matcha tagg-ID:n i innehållsnoder som pekar på tagg A.
   * Taggskräpinsamlaren tar bort taggar som tagg A en gång och inga fler innehållsnoder pekar på dem.
   * Ett specialvärde för `cq:movedTo` egenskapen är `nirvana`, som används när taggen tas bort men inte kan tas bort från databasen eftersom det finns undertaggar med en `cq:movedTo` som måste behållas.

      >[!NOTE]
      >
      >Egenskapen läggs bara till i den flyttade eller sammanfogade taggen om något av följande villkor uppfylls: `cq:movedTo`
      >
      > 1. Taggen används i innehåll (vilket innebär att den har en referens). ELLER
      > 1. Taggen har underordnade objekt som redan har flyttats.


* Tagg B skapas (vid en flytt) och får en `cq:backlinks` egenskap.
   * `cq:backlinks` behåller referenserna i den andra riktningen, dvs. en lista över alla taggar som har flyttats till eller sammanfogats med tagg B.
   * Detta krävs oftast för att hålla `cq:movedTo` egenskaperna uppdaterade även när tagg B flyttas/sammanfogas/tas bort eller när tagg B aktiveras, och då måste även alla dess bakåttaggar aktiveras.

      >[!NOTE]
      >
      >Egenskapen läggs bara till i den flyttade eller sammanfogade taggen om något av följande villkor uppfylls: `cq:backlinks`
      >
      > 1. Taggen används i innehåll (vilket innebär att den har en referens). ELLER
      > 1. Taggen har underordnade objekt som redan har flyttats.


När du läser en `cq:tags` egenskap för en innehållsnod används följande upplösning:

1. Om det inte finns någon matchning under `/content/cq:tags`returneras ingen tagg.
1. Om taggen har en `cq:movedTo` egenskapsuppsättning följs det tagg-ID som refereras.
   * Det här steget upprepas så länge den efterföljande taggen har en `cq:movedTo` egenskap.
1. Om den följande taggen inte har någon `cq:movedTo` egenskap läses taggen.

Om du vill publicera ändringen när en tagg har flyttats eller sammanfogats måste noden och alla dess bakgrunder replikeras `cq:Tag` . Detta görs automatiskt när taggen aktiveras i tagghanteringskonsolen.

Senare uppdateringar av sidans `cq:tags` egenskap rensar automatiskt de gamla referenserna. Detta utlöses eftersom en flyttad tagg som löses via API returnerar måltaggen och därmed anger måltaggens ID.

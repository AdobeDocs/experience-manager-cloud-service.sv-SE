---
title: Attribut och typer
description: Läs mer om de dataattribut och datatyper som krävs för den universella redigeraren.
source-git-commit: 0e66c379e10d275610d85a699da272dc0c32a9a8
workflow-type: tm+mt
source-wordcount: '661'
ht-degree: 3%

---


# Attribut och typer {#attributes-types}

Läs mer om de dataattribut och datatyper som krävs för den universella redigeraren.

## Introduktion {#introduction}

För att ett program ska kunna redigeras av den universella redigeraren måste det vara ordentligt instrumenterat. Detta inkluderar rätt metadata så att redigeraren kan redigera innehållet i programmet. Det här dokumentet innehåller information om attributen och typerna för dessa metadata.

>[!NOTE]
>
>Innehållsvalidering utförs på serversidan. Den universella redigeraren fungerar bara med dataattributen. Verifiering av att de passar modellen/strukturen måste åtgärdas på API-nivå.

## Dataegenskaper {#data-properties}

| Dataegenskap | Beskrivning |
|---|---|
| `itemid` | URN to the resource, see the section [Instrument the Page of the document Getting Started with the Universal Editor in AEM](getting-started.md#instrument-thepage) |
| `itemprop` | Resursens attribut, se avsnittet [Instrument the Page of the document Getting Started with the Universal Editor in AEM](getting-started.md#instrument-thepage) |
| `itemtype` | Typ av redigerbart objekt (t.ex. text, bild, referens) |
| `data-editor-itemfilter` | Definierar vilka referenser som kan användas |
| `data-editor-itemlabel` | Definierar en anpassad etikett för ett markeringsbart objekt som visas i redigeraren <br>Om `itemmodel` är inställd hämtas etiketten via modellen |
| `data-editor-itemmodel` | Definierar en modell som ska användas för formulärbaserad redigering i egenskapsfältet |
| `data-editor-behavior` | Definierar beteendet för en instrumentering, t.ex. fristående text eller bild kan också efterlikna en komponent så att den kan flyttas eller tas bort |

## Objekttyper {#item-types}

| `itemtype` | Beskrivning | `itemid` | `itemprop` | `data-editor-itemfilter` | `data-editor-itemlabel` | `data-editor-itemmodel` | `data-editor-behvior` |
|---|---|---|---|---|---|---|---|
| `text` | Texten kan redigeras i HTML-taggarna, men bara i ett enkelt textformat, ingen formatering, det här används ofta för rubrikkomponenter, till exempel | Valfritt | Obligatoriskt | n/a | Valfritt | n/a | Valfritt |
| `richtext` | Texten kan redigeras med omfattande textfunktioner. RTE visas i den högra panelen | Valfritt | Obligatoriskt | n/a | Valfritt | n/a | Valfritt |
| `media` | Det redigerbara är en resurs, t.ex. bild eller video | Valfritt | Obligatoriskt | Valfritt<br>lista med bild- eller videofiltervillkor som skickas till resursväljaren | Valfritt | n/a | Valfritt |
| `container` | De redigerbara funktionerna fungerar som behållare för komponenter som kallas Styckesystem. | Beroende <br>se nedan | Beroende <br>se nedan | Valfritt<br>en lista över tillåtna komponenter | Valfritt | n/a | n/a |
| `component` | Det redigerbara är en komponent. Ingen ytterligare funktionalitet läggs till. Den krävs för att ange rörliga/borttagbara delar av DOM och för att öppna egenskapsfältet och dess fält. | Obligatoriskt | n/a | n/a | Valfritt | Valfritt | n/a |
| `reference` | Det redigerbara är en referens, t.ex. Content Fragment, Experience Fragment eller Product | Beroende <br>se nedan | Beroende <br>se nedan | Valfritt<br>lista med villkor för innehållsfragment, produkt eller Experience Fragment-filter som skickas vidare till referensväljaren | Valfritt | Valfritt | n/a |

Beroende på användningsfallet `itemprop` eller `itemid` kan vara nödvändigt eller inte. Till exempel:

* `itemid` är obligatoriskt om du skickar frågor till innehållsfragment via GraphQL och vill göra listan redigerbar i sitt sammanhang.
* `itemprop` krävs om du har en komponent som återger innehållet i ett refererat innehållsfragment och du vill uppdatera referensen i komponenten.

## Beteenden {#behaviors}

| `data-editor-behavior` | Beskrivning |
|---|---|
| `component` | Kan användas för att låta komponenter för fristående text, avancerad text och mediemimik vara flyttbara och borttagbara på sidan |

## Ytterligare resurser {#additional-resources}

Mer information om Universal Editor finns i de här dokumenten.

* [Introduktion till Universal Editor](introduction.md) - Lär dig hur den universella redigeraren möjliggör redigering av alla aspekter av innehåll i alla implementeringar för att leverera enastående upplevelser, öka innehållets hastighet och leverera en toppmodern utvecklarupplevelse.
* [Skapa innehåll med den universella redigeraren](authoring.md) - Lär dig hur enkelt och intuitivt det är för skribenter att skapa innehåll med den universella redigeraren.
* [Publicera innehåll med den universella redigeraren](publishing.md) - Lär dig hur den universella Visual Editor publicerar innehåll och hur dina appar kan hantera det publicerade innehållet.
* [Komma igång med Universal Editor i AEM](getting-started.md) - Lär dig hur du får tillgång till den universella redigeraren och hur du börjar använda den i ditt första AEM.
* [Universal Editor Architecture](architecture.md) - Lär dig mer om arkitekturen i den universella redigeraren och hur data flödar mellan tjänster och lager.
* [Autentisering av universell redigerare](authentication.md) - Lär dig hur den universella redigeraren autentiseras.

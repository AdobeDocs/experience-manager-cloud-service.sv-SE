---
title: Attribut och objekttyper
description: Läs mer om de dataattribut och objekttyper som krävs för den universella redigeraren.
exl-id: 02795a31-244a-42b4-8297-2649125d7777
source-git-commit: b42390dcecb546853380d64808bcf009680c89a3
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 1%

---


# Attribut och typer {#attributes-types}

Läs mer om de dataattribut och objekttyper som krävs för den universella redigeraren.

## Introduktion {#introduction}

För att ett program ska kunna redigeras av den universella redigeraren måste det vara ordentligt instrumenterat. Detta inkluderar rätt metadata så att redigeraren kan redigera innehållet i programmet. Det här dokumentet innehåller information om attributen och objekttyperna för dessa metadata.

>[!NOTE]
>
>Innehållsvalidering utförs på serversidan. Den universella redigeraren fungerar helt enkelt med dataattributen. Verifiering av att de passar modellen/strukturen måste åtgärdas på API-nivå.

## Dataegenskaper {#data-properties}

| Dataegenskap | Beskrivning |
|---|---|
| `data-aue-resource` | URN to the resource, see the section [Instrument the Page of the document Getting Started with the Universal Editor in AEM](getting-started.md#instrument-thepage) |
| `data-aue-prop` | Resursens attribut, se avsnittet [Instrument the Page of the document Getting Started with the Universal Editor in AEM](getting-started.md#instrument-thepage) |
| `data-aue-type` | [Typ av redigerbart objekt](#item-types) (till exempel text, bild och referens) |
| `data-aue-filter` | Definierar vilka referenser som kan användas |
| `data-aue-label` | Definierar en anpassad etikett för ett markeringsbart objekt som visas i redigeraren <br>Om `data-aue-model` är inställd hämtas etiketten med hjälp av modellen |
| `data-aue-model` | Definierar en modell som används för formulärbaserad redigering i egenskapsfältet |
| `data-aue-behavior` | Definierar [instrumentets beteende](#behaviors)fristående text eller bild kan också efterlikna en komponent så att den kan flyttas eller tas bort |

## Objekttyper {#item-types}

| `data-aue-type` | Beskrivning | `data-aue-resource` | `data-aue-prop` | `data-aue-filter` | `data-aue-label` | `data-aue-model` | `data-aue-behavior` |
|---|---|---|---|---|---|---|---|
| `text` | Texten kan redigeras i HTML-taggarna, men bara i ett enkelt textformat, ingen formatering, det här används ofta för rubrikkomponenter, till exempel | Valfritt | Obligatoriskt | n/a | Valfritt | n/a | Valfritt |
| `richtext` | Texten kan redigeras med omfattande textfunktioner. RTE visas på den högra panelen | Valfritt | Obligatoriskt | n/a | Valfritt | n/a | Valfritt |
| `media` | Det redigerbara objektet är en resurs, till exempel bild eller video | Valfritt | Obligatoriskt | Valfritt<br>lista med bild- eller videofiltervillkor som skickas till resursväljaren | Valfritt | n/a | Valfritt |
| `container` | De redigerbara funktionerna fungerar som behållare för komponenter som kallas Styckesystem. | Beroende <br>se nedan | Beroende <br>se nedan | Valfritt<br>en lista över tillåtna komponenter | Valfritt | n/a | n/a |
| `component` | Det redigerbara är en komponent. Det lägger inte till ytterligare funktioner. Det är obligatoriskt att ange flyttbara/borttagbara delar av DOM och att öppna egenskapsspåret och dess fält | Obligatoriskt | n/a | n/a | Valfritt | Valfritt | n/a |
| `reference` | Det redigerbara är en referens, till exempel Innehållsfragment, Upplevelsefragment eller Produkt | Beroende <br>se nedan | Beroende <br>se nedan | Valfritt<br>lista med villkor för innehållsfragment, produkt eller Experience Fragment-filter som skickas vidare till referensväljaren | Valfritt | Valfritt | n/a |

Beroende på användningsfallet `data-aue-prop` eller `data-aue-resource` kan vara nödvändigt eller inte. Till exempel:

* `data-aue-resource` är obligatoriskt om du skickar frågor till innehållsfragment via GraphQL och vill göra listan redigerbar i sitt sammanhang.
* `data-aue-prop` krävs om du har en komponent som återger innehållet i ett refererat innehållsfragment och du vill uppdatera referensen i komponenten.

## Beteenden {#behaviors}

| `data-aue-behavior` | Beskrivning |
|---|---|
| `component` | Används för att tillåta fristående text, fullödig text och mediemimiska komponenter så att de också kan flyttas och tas bort på sidan |
| `container` | Används för att tillåta att behållare behandlas som sina egna komponenter så att de kan flyttas och tas bort på sidan |

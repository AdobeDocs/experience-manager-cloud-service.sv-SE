---
title: Attribut och objekttyper
description: Läs mer om de dataattribut och objekttyper som krävs för den universella redigeraren.
exl-id: 02795a31-244a-42b4-8297-2649125d7777
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 0%

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
| `data-aue-resource` | URN till resursen, se avsnittet [Instrument the Page of the document Getting Started with the Universal Editor in AEM](getting-started.md#instrument-thepage) |
| `data-aue-prop` | Resursens attribut, se avsnittet [Instrument på sidan i dokumentet Getting Started with the Universal Editor i AEM](getting-started.md#instrument-thepage) |
| `data-aue-type` | [Typ av redigerbart objekt](#item-types) (till exempel text, bild och referens) |
| `data-aue-filter` | Definierar:<br> - Vilka RTE-funktioner som är aktiverade <br> - Vilka komponenter som kan läggas till i en behållare <br> - Vilka resurser som kan läggas till i en medietyp |
| `data-aue-label` | Definierar en anpassad etikett för ett markeringsbart objekt som visas i redigeraren |
| `data-aue-model` | Definierar en modell som används för formulärbaserad redigering på egenskapspanelen |
| `data-aue-behavior` | Föråldrad. Den definierade en gång beteendet hos ett instrument för att tillåta fristående text, fulltext och media att efterlikna komponenter så att de också kunde flyttas och tas bort på sidan, vilket ger ett enda möjligt värde på `component`. Den här egenskapen ignoreras nu och när ett objekt med `data-aue-resource` är direkt underordnat en behållare betraktas den automatiskt som en komponent. |

## Objekttyper {#item-types}

| `data-aue-type` | Beskrivning | `data-aue-resource` | `data-aue-prop` | `data-aue-filter` | `data-aue-label` | `data-aue-model` |
|---|---|---|---|---|---|---|
| `text` | Texten kan redigeras i HTML-taggarna, men bara i ett enkelt textformat, ingen RTF-formatering tillgänglig, används det ofta i rubrikkomponenter, till exempel | Valfritt | Obligatoriskt | n/a | Valfritt | n/a |
| `richtext` | Texten kan redigeras med omfattande textfunktioner. RTE visas på den högra panelen | Valfritt | Obligatoriskt | n/a | Valfritt | n/a |
| `media` | Det redigerbara objektet är en resurs, till exempel bild eller video | Valfritt | Obligatoriskt | Valfri<br>lista med bild- eller videofiltervillkor som skickas till resursväljaren | Valfritt | n/a |
| `container` | De redigerbara funktionerna fungerar som behållare för komponenter som kallas Styckesystem. | Beroende <br>se nedan | Beroende <br>se nedan | Valfri<br>lista över tillåtna komponenter | Valfritt | n/a |
| `component` | Det redigerbara är en komponent. Det lägger inte till ytterligare funktioner. Du måste ange flyttbara/borttagbara delar av DOM och öppna egenskapspanelen och dess fält | Obligatoriskt | n/a | n/a | Valfritt | Valfritt |
| `reference` | Det redigerbara är en referens, till exempel Innehållsfragment, Upplevelsefragment eller Produkt | Beroende <br>se nedan | Beroende <br>se nedan | Valfri<br>lista över villkor för innehållsfragment, produkt eller Experience Fragment-filter som skickas till referensväljaren | Valfritt | Valfritt |

`data-aue-resource` krävs alltid eftersom det är primärnyckeln som anger var innehållsändringar skrivs.

* Det krävs inte direkt på taggen där `data-aue-type` är inställd.
* Om det inte anges används attributet `data-aue-resource` för närmaste överordnade.

`data-aue-prop` krävs när du vill redigera i kontexten, förutom för en behållare där det är valfritt (om den anges är behållaren ett innehållsfragment och egenskapen pekar på ett fält med flera referenser).

* `data-aue-prop` är det attribut som ska uppdateras för primärnyckeln för `data-aue-resource`.

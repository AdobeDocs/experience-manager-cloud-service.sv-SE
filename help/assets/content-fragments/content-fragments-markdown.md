---
title: Markering (resurser - innehållsfragment)
description: Förstå hur Content Fragment Editor använder markeringssyntax för att enkelt skapa rubrikfritt innehåll.
feature: Content Fragments
role: User
exl-id: 7a6d4a63-faf8-4e1c-95da-90db2027a2dd
source-git-commit: c15ef1cc9b14466105e5565c8ccc15120346f0f2
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 3%

---

# Markdown {#markdown}

När du [redigering](/help/assets/content-fragments/content-fragments-variations.md#authoring-your-content)använder innehållsfragmentredigeraren *markering* så att du enkelt kan skriva headless-innehåll:

![markeringsredigerare](/help/assets/content-fragments/assets/cfm-markdown-01.png)

Du kan definiera:

* [Rubriknotation](/help/assets/content-fragments/content-fragments-markdown.md#heading-notation)
* [Stycken och radbrytningar](/help/assets/content-fragments/content-fragments-markdown.md#paragraphs-and-line-breaks)
* [Länkar](/help/assets/content-fragments/content-fragments-markdown.md#links)
* [Bilder](/help/assets/content-fragments/content-fragments-markdown.md#images)
* [Blockcitat](/help/assets/content-fragments/content-fragments-markdown.md#block-quotes)
* [Listor](/help/assets/content-fragments/content-fragments-markdown.md#lists)
* [Betoning](/help/assets/content-fragments/content-fragments-markdown.md#emphasis)
* [Kodblock](/help/assets/content-fragments/content-fragments-markdown.md#code-blocks)
* [Omvända snedstreck](/help/assets/content-fragments/content-fragments-markdown.md#backslash-escapes)

## Rubriknotation {#heading-notation}

Om du vill skapa en rubrik genom att placera en hash-tagg (#) framför rubriken. En hash-tagg (#) används för en H1, två hash-taggar (#) för en H2 osv. Du kan använda upp till 6 hash-taggar. Till exempel:

    `## This is an H2`

    `### This is an H3`

    `###### This is a H6`

Du kan också skapa en H1 genom att stryka under texten med lika stora tecken och skapa en H2 genom att stryka under texten med minustecken. Till exempel:

    `This is an H1`

    `=============`

    `This is an H2`

    `-------------`

## Stycken och radbrytningar {#paragraphs-and-line-breaks}

Ett stycke är en eller flera på varandra följande textrader, avgränsade med en eller flera tomma rader. En tom rad är en rad som bara innehåller blanksteg eller tabbar. Normala stycken får inte dras in med blanksteg eller tabbar.

En radbrytning skapas genom att en rad avslutas med två eller flera blanksteg och sedan returneras.

## Länkar {#links}

Du kan skapa textbundna länkar och referenslänkar.

I båda formaten avgränsas länktexten av hakparenteser `[]`.

Detta är exempel på textbundna länkar:

    `This is [an example](https://example.com/ "Title") inline link.`

    `This is [an example of an email link](emailto:myaddress@mydomain.info)`

    `[This link](https://example.net/) has no title attribute.`

En referenslänk har följande syntax:

    `Hey you should [checkout][0] this [cool thing][wiki] that I [made][].`

    `[0]: https://www.google.ca`

    `[wiki]: https://www.wikipedia.org`

    `[made]: https://www.stackoverflow.com`

## Bilder {#images}

Syntaxen för bilder liknar länkarna. Du kan skapa textbundna och refererade bilder.

En textbunden bild har till exempel följande syntax:

    `![Alt text](/path/to/img.jpg)`

    `![Alt text](/path/to/img.jpg "Optional title")`

Syntaxen innehåller:

* Ett utropstecken: !;
* följt av en uppsättning hakparenteser som innehåller alt-attributtexten för bilden,
* följt av en uppsättning parenteser, som innehåller URL:en eller sökvägen till bilden och ett valfritt rubrikattribut inom dubbla eller enkla citattecken.

En bild i referensstil har följande syntax:

    `![Alt text][id]`

Där &quot;id&quot; är namnet på en definierad bildreferens. Bildreferenser definieras med samma syntax som länkreferenser:

    `[id]: url/to/image "Optional title attribute"`

## Blockcitat {#block-quotes}

Du kan citera text genom att lägga till symbolen > före texten. Till exempel:

    `>This is block quotes`

    `>asdhfjlkasdhlf`

    `>asdfahsdlfasdfj`

Du kan ha kapslade blockcitattecken. Till exempel:

    `> This is the first level of quoting.`

    `>`

        `>> This is nested blockquote.`

    `>`

    `> Back to the first level.`

## Listor {#lists}

Du kan skapa både sorterade och osorterade listor.

Skapa en osorterad &amp;lista med hjälp av den sista; -symbolen före objekten i listan. Till exempel:

    `* item in list`

    `* item in list`

    `* item in list`

Om du vill skapa en ordnad lista lägger du till siffrorna, följt av en punkt, före varje objekt i listan. Till exempel:

    `1. First item in list.`

    `2. Second item in list.`

    `3. Third item in list.`

## Betoning {#emphasis}

Du kan lägga till kursiv stil eller fetstil i texten.

Så här lägger du till kursiv stil:

    `*single asterisks*`

    `_single underscores_`

    `Keyboard shortcut: Ctrl-I (Cmd-I)`

Du kan fet text enligt följande:

    `**double asterisks**`

    `__double underscores__`

    `Keyboard shortcut: Ctrl-B (Cmd-B)`

Om du vill ange ett kodomfång omsluter du det med citattecken (&grave;). Till skillnad från ett förformaterat kodblock anger ett kodintervall koden i ett normalt stycke.

Till exempel:

    ``Use the `printf()` function.``

## Kodblock {#code-blocks}

Kodblock används vanligtvis för att illustrera källkod. Du kan skapa kodblock genom att dra in koden med en tabb eller med minst fyra mellanslag. Till exempel:

    `This is a normal paragraph.`

        `This is a code block.`

## Omvända snedstreck {#backslash-escapes}

Du kan använda omvänt snedstreck för att generera litterala tecken som har en speciell betydelse för formateringssyntaxen. Om du till exempel vill omge ett ord med literala asterisker (i stället för en HTML-tagg) kan du använda omvända snedstreck före asteriskerna, enligt följande:

    `\\*literal asterisks\\*`

Omvända snedstreck är tillgängliga för följande tecken:

    ` \ backslash`

    `` ` backtick``

    ` * asterisk`

    ` _ underscore`

    ` {} curly braces`

    ` [] square brackets`

    ` () parentheses`

    ` # hash mark`

    ` + plus sign`

    ` - minus sign (hyphen)`

    ` . dot`

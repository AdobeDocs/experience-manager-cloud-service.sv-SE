---
title: Dekoration-tagg
description: När en komponent på en webbsida återges kan ett HTML-element genereras och den återgivna komponenten kapslas in i sig själv. För utvecklare har AEM en tydlig och enkel logik som styr de dekorationstaggar som omsluter de inkluderade komponenterna.
translation-type: tm+mt
source-git-commit: 0799a817095558edd49b53ddc915c9474181fef7
workflow-type: tm+mt
source-wordcount: '791'
ht-degree: 1%

---


# Dekortagg {#decoration-tag}

När en komponent på en webbsida återges kan ett HTML-element genereras och den återgivna komponenten kapslas in i sig själv. Detta har främst två syften:

* En komponent kan bara redigeras när den kapslas med ett HTML-element.
* Omslutningselementet används för att tillämpa HTML-klasser som innehåller:
   * Layoutinformation
   * Formatinformation

För utvecklare har AEM en tydlig och enkel logik som styr de dekorationstaggar som omsluter de inkluderade komponenterna. Om och hur dekorationstaggen återges definieras av en kombination av två faktorer som den här sidan kommer att dyka upp i:

* Själva komponenten kan konfigurera sin dekorationstagg med en uppsättning egenskaper.
* De skript som innehåller komponenter kan definiera aspekterna för dekorationstaggen med include-parametrar.

## Recommendations {#recommendations}

Här följer några allmänna rekommendationer för när wrapper-elementet ska tas med, som hjälper dig att undvika att stöta på oväntade problem:

* Närvaron av wrapper-elementet får inte skilja sig mellan WCMModes (redigerings- eller förhandsgranskningsläge), instanser (författare eller publicering) eller miljö (staging eller produktion), så att sidans CSS och JavaScript fungerar likadant i alla fall.
* Radbrytningselementet bör läggas till i alla komponenter som är redigerbara, så att sidredigeraren kan initiera och uppdatera dem på rätt sätt.
* För icke-redigerbara komponenter kan wrapper-elementet undvikas om det inte har någon speciell funktion, så att den resulterande koden inte blir onödigt utdragen.

## Komponentkontroller {#component-controls}

Följande egenskaper och noder kan tillämpas på komponenterna för att styra beteendet för deras dekorationstagg:

* **`cq:noDecoration {boolean}`:** Den här egenskapen kan läggas till i en komponent och ett true-värde AEM inte generera några wrapper-element över komponenten.
* **`cq:htmlTag`nod:** Den här noden kan läggas till under en komponent och kan ha följande egenskaper:
   * **`cq:tagName {String}`:** Detta kan användas för att ange en anpassad HTML-tagg som ska användas för att kapsla komponenterna i stället för DIV-standardelementet.
   * **`class {String}`:** Detta kan användas för att ange CSS-klassnamn som ska läggas till i wrapper.
   * Andra egenskapsnamn läggs till som HTML-attribut med samma String-värde som anges.

## Skriptkontroller {#script-controls}

I allmänhet kan omslutningsbeteendet i HTML sammanfattas på följande sätt:

* Ingen wrapper-DIV återges som standard (när du bara gör `data-sly-resource="foo"`).
* Alla wcm-lägen (inaktiverade, förhandsgranska, redigera både på författare och publicerade) återges identiskt.

Omslagets beteende kan också styras fullständigt.

* HTL-skriptet har fullständig kontroll över det resulterande beteendet för wrapper-taggen.
* Komponentegenskaper (som `cq:noDecoration` och `cq:tagName`) kan också definiera wrapper-taggen.

Det går att helt styra beteendet för wrapper-taggarna från HTML-skript och tillhörande logik.

Mer information om hur du utvecklar i HTML finns i [HTL-dokumentationen](https://docs.adobe.com/content/help/en/experience-manager-htl/using/overview.html).

### Beslutsträd {#decision-tree}

Detta beslutsträd sammanfattar logiken som bestämmer beteendet för wrapper-taggarna.

![Beslutsträd](assets/decoration-tag-decision-tree.png)

### Använd fall {#use-cases}

Följande tre exempel innehåller exempel på hur wrapper-taggarna hanteras, och visar också hur enkelt det är att styra det önskade beteendet för wrapper-taggarna.

Alla exempel som följer förutsätter följande innehållsstruktur och komponenter:

```
/content/test/
  @resourceType = "test/components/one"
  child/
    @resourceType = "test/components/two"
```

```
/apps/test/components/
  one/
    one.html
  two/
    two.html
    cq:htmlTag/
      @cq:tagName = "article"
      @class = "component-two"
```

#### Användningsfall 1: Inkludera en komponent för återanvändning av kod {#use-case-include-a-component-for-code-reuse}

Det vanligaste användningsfallet är när en komponent innehåller en annan komponent av kodskäl. I så fall är den inkluderade komponenten inte nödvändig för att kunna redigeras med ett eget verktygsfält och en egen dialogruta. Därför behövs ingen wrapper och komponentens `cq:htmlTag` ignoreras. Detta kan betraktas som standardbeteendet.

`one.html: <sly data-sly-resource="child"></sly>`

`two.html: Hello World!`

Resulterande utdata på `/content/test.html`:

**`Hello World!`**

Ett exempel är en komponent som innehåller en huvudbildkomponent för att visa en bild, vanligtvis med hjälp av en syntetisk resurs, som består i att ta med en virtuell underordnad komponent genom att skicka ett Map-objekt som representerar alla egenskaper som komponenten skulle ha till en dataunderordnad resurs.

#### Användningsfall 2: Inkludera en redigerbar komponent {#use-case-include-an-editable-component}

Ett annat vanligt användningsfall är när behållarkomponenter innehåller redigerbara underordnade komponenter, som en layoutbehållare. I det här fallet behöver varje underordnat objekt en wrapper för att redigeraren ska fungera (om de inte uttryckligen har inaktiverats med egenskapen `cq:noDecoration`).

Eftersom den inkluderade komponenten i det här fallet är en fristående komponent, behöver den ett wrapper-element för att redigeraren ska kunna arbeta och för att definiera dess layout och format som ska användas. Det finns ett `decoration=true`-alternativ som kan aktivera det här beteendet.

`one.html: <sly data-sly-resource="${'child' @ decoration=true}"></sly>`

`two.html: Hello World!`

Resulterande utdata på `/content/test.html`:

**`<article class="component-two">Hello World!</article>`**

#### Användningsfall 3: Anpassat beteende {#use-case-custom-behavior}

Det kan finnas ett obegränsat antal komplexa fall, som enkelt kan uppnås genom möjligheten att HTML uttryckligen anger:

* **`decorationTagName='ELEMENT_NAME'`** För att definiera elementnamnet för wrapper.
* **`cssClassName='CLASS_NAME'`** För att definiera CSS-klassnamn som ska anges för den.

`one.html: <sly data-sly-resource="${'child' @ decorationTagName='aside', cssClassName='child'}"></sly>`

`two.html: Hello World!`

Resulterande utdata `/content/test.html`:

**`<aside class="child">Hello World!</aside>`**

---
title: Begränsningar för redigerare
description: Redigeraren i det beröringsaktiverade användargränssnittet använder övertäckningar för att interagera med innehåll som begränsas i en iframe. Den här interaktionen skapar vissa begränsningar i både användningen av redigeraren och för utvecklare.
translation-type: tm+mt
source-git-commit: fee73b5f5ba69422494efe554ac5aa62c046ad86
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 0%

---


# Redigeringsbegränsningar {#editor-limitations}

Redigeraren i det beröringsaktiverade användargränssnittet använder övertäckningar för att interagera med innehåll som begränsas i en iframe. Den här interaktionen skapar vissa begränsningar i både användningen av redigeraren och för utvecklare. På den här sidan sammanfattas dessa begränsningar och lösningar eller tillfälliga lösningar ges där det är möjligt.

## Funktionsbegränsningar {#functional-limitations}

En författare kan stöta på följande funktionella begränsningar när han eller hon använder redigeraren för att skapa sidor.

### Länkar som inte är aktiva {#links-not-active}

När [redigerar en sida](/help/sites-cloud/authoring/fundamentals/editing-content.md) är länkar inte aktiva.

* [Växla till  **** ](/help/sites-cloud/authoring/fundamentals/editing-content.md#preview-mode) Förhandsgranskningsläge om du vill navigera med hjälp av länkarna i ditt innehåll.

### Struktursidor {#structure-pages}

Sidorna kan inte ha namnet `structure`. Sidor med namnet `structure` kan inte redigeras i sidredigeraren.

## CSS-begränsningar {#css-limitations}

En utvecklare kan stöta på följande begränsningar när det gäller redigerarens interaktion med CSS.

### Absolut positionerade element {#absolutely-positioned-elements}

Absolut positionerade element kan orsaka problem i positionen för deras övertäckning.

* Om det inträffar måste du kontrollera att dimensionerna för det absolut placerade elementet är korrekta eftersom redigeraren kommer att skapa en övertäckning med exakt samma dimensioner.

### vh enheter {#vh-units}

`vh` enheter stöds inte eftersom iframe-höjden måste justeras automatiskt av AEM.

### Fasta bakgrundsbilder {#fixed-background-images}

Fasta bakgrundsbilder kanske inte visas som fasta vid bläddring eftersom de är inbäddade i en iframe.

* Om du väljer **Visa sidan som Publicerad** i sidhuvudsfältets åtgärder visas sidan korrekt.

### 100 % höjd {#height}

Höjden 100 % stöds inte för en sidas body-element.

* Du kan komma runt en del av brödtexten genom att&quot;sträcka ut&quot; brödtexten enligt följande:

```xml
body {
    position: absolute;
    top: 0;
    bottom: 0;
    right: 0;
    left: 0;
}
```

### Marginalen komprimeras {#margin-collapsing}

Problem med att komprimera marginaler visas om det första underordnade elementet i body-elementet har en marginal.

* Lösningen är att lägga till ett klarfix på body-elementnivån enligt följande:

```xml
body:before, body:after{
    content: ' ';
    display: table;
}
```

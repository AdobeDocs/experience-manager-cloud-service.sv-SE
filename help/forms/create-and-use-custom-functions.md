---
title: Använda anpassade funktioner i ett adaptivt formulär
description: AEM Forms har stöd för anpassade funktioner, som gör att användare kan skapa och använda sina egna funktioner i regelredigeraren.
keywords: Lägg till en anpassad funktion, använd en anpassad funktion, skapa en anpassad funktion, använd anpassad funktion i regelredigeraren.
contentOwner: Ruchita Srivastav
content-type: reference
feature: Adaptive Forms, Core Components
exl-id: 24607dd1-2d65-480b-a831-9071e20c473d
role: User, Developer
source-git-commit: fecbebde808c545a84889da5610a79c088f2f459
workflow-type: tm+mt
source-wordcount: '1286'
ht-degree: 0%

---


# Introduktion till anpassade funktioner för adaptiv Forms baserat på kärnkomponenter

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/adaptive-forms-core-components/create-and-use-custom-functions-core-components) |
| AEM as a Cloud Service | Den här artikeln |

AEM Forms har stöd för anpassade funktioner, vilket gör att man kan definiera JavaScript-funktioner för att implementera komplexa affärsregler. Dessa anpassade funktioner gör att man kan förbättra blanketternas funktioner genom att underlätta hantering och bearbetning av inmatade data för att uppfylla specifika krav. De gör det möjligt att dynamiskt ändra formulärbeteende baserat på fördefinierade kriterier. Med anpassade funktioner kan utvecklare också använda komplex valideringslogik, utföra dynamiska beräkningar och styra visningen eller beteendet för formulärelement baserat på användarinteraktioner eller fördefinierade kriterier.

>[!NOTE]
>
> Kontrollera att [kärnkomponenten](https://github.com/adobe/aem-core-forms-components) är inställd på den senaste versionen för att använda de senaste funktionerna.

## Användning av anpassade funktioner {#uses-of-custom-function}

Fördelarna med att använda anpassade funktioner i Adaptive Forms är:
* **Databearbetning**: Anpassade funktioner hjälper dig att bearbeta data som anges i formulärfälten.
* **Validering av data**: Med anpassade funktioner kan du utföra anpassade kontroller av formulärindata och tillhandahålla angivna felmeddelanden.
* **Dynamiskt beteende**: Med anpassade funktioner kan du styra det dynamiska beteendet i dina formulär baserat på specifika villkor. Du kan till exempel visa/dölja fält, ändra fältvärden eller justera formulärlogiken dynamiskt.
* **Integration**: Du kan använda anpassade funktioner för att integrera med externa API:er eller tjänster. Det hjälper till att hämta data från externa källor, skicka data till externa Rest-slutpunkter eller utföra anpassade åtgärder baserade på externa händelser.

Anpassade funktioner är i huvudsak klientbibliotek som läggs till i JavaScript-filen. När du har skapat en anpassad funktion blir den tillgänglig i regelredigeraren så att användaren kan välja den i ett adaptivt formulär. De anpassade funktionerna identifieras av JavaScript kommentarer i regelredigeraren.

## JavaScript-anteckningar som stöds för anpassade funktioner {#js-annotations}

JavaScript-anteckningar används för att tillhandahålla metadata för JavaScript-kod. Det innehåller kommentarer som börjar med specifika symboler, till exempel /** och @. Anteckningarna innehåller viktig information om funktioner, variabler och andra element i koden. Adaptiv form stöder följande JavaScript-anteckningar för anpassade funktioner:

### Namn

Namnet används för att identifiera den anpassade funktionen i regelredigeraren för ett adaptivt formulär. Följande syntaxer används för att namnge en anpassad funktion:

* `@name [functionName] <Function Name>`
* `@function [functionName] <Function Name>`
* `@func [functionName] <Function Name>`.
  `functionName` är namnet på funktionen. Blanksteg är inte tillåtna.
  `<Function Name>` är funktionens visningsnamn i regelredigeraren för ett adaptivt formulär.
Om funktionsnamnet är identiskt med namnet på själva funktionen kan du utelämna `[functionName]` från syntaxen.

### Parameter

Parametern är en lista med argument som används av anpassade funktioner. En funktion kan ha stöd för flera parametrar. Följande syntaxer används för att definiera en parameter i en anpassad funktion:

* `@param {type} name <Parameter Description>`
* `@argument` `{type} name <Parameter Description>`
* `@arg` `{type}` `name <Parameter Description>`.
  `{type}` representerar parametertypen.  Tillåtna parametertyper är:

   * string: Representerar ett enda strängvärde.
   * number: Representerar ett numeriskt värde.
   * booleskt: Representerar ett enskilt booleskt värde (true eller false).
   * sträng []: Representerar en array med strängvärden.
   * tal[]: Representerar en matris med numeriska värden.
   * boolesk[]: Representerar en matris med booleska värden.
   * date: Representerar ett enda datumvärde.
   * date[]: Representerar en matris med datumvärden.
   * array: Representerar en generisk array som innehåller värden av olika typer.
   * object: Representerar formulärobjektet som skickas till en anpassad funktion i stället för att skicka dess värde direkt.
   * omfång: Representerar det globala objektet, som innehåller skrivskyddade variabler som formulärinstanser, målfältsinstanser och metoder för att utföra formulärändringar i anpassade funktioner. Den deklareras som den sista parametern i JavaScript-anteckningar och visas inte i regelredigeraren för ett adaptivt formulär. Omfångsparametern har åtkomst till formulärets eller komponentens objekt för att utlösa den regel eller händelse som krävs för formulärbearbetning. Om du vill ha mer information om det globala objektet och hur du använder det [klickar du här](/help/forms/custom-function-core-component-scope-function.md).

Parametertypen är inte skiftlägeskänslig och blanksteg tillåts inte i parameternamnet.

`<Parameter Description>` innehåller information om parameterns syfte. Det kan innehålla flera ord.

#### Valfria parametrar

Som standard är alla parametrar obligatoriska. Du kan definiera en parameter som valfri genom att antingen lägga till `=` efter parametertypen eller genom att omsluta parameternamnet i `[]`. Parametrar som definieras som valfria i JavaScript-anteckningar visas som valfria i regelredigeraren.
Om du vill definiera en variabel som en valfri parameter kan du använda någon av följande syntaxer:

* `@param {type=} Input1`

I ovanstående kodrad är `Input1` en valfri parameter utan något standardvärde. Så här deklarerar du valfri parameter med standardvärdet:
`@param {string=<value>} input1`

`input1` som en valfri parameter med standardvärdet `value`.

* `@param {type} [Input1]`

I ovanstående kodrad är `Input1` en valfri parameter utan något standardvärde. Så här deklarerar du valfri parameter med standardvärdet:
`@param {array} [input1=<value>]`
`input1` är en valfri parameter av arraytyp med standardvärdet `value` .
Kontrollera att parametertypen omsluts av klammerparenteser {} och att parameternamnet omges av hakparenteser.

Titta på följande kodfragment, där input2 definieras som en valfri parameter:

```javascript
        /**
         * optional parameter function
         * @name OptionalParameterFunction
         * @param {string} input1 
         * @param {string=} input2 
         * @return {string}
        */
        function OptionalParameterFunction(input1, input2) {
        let result = "Result: ";
        result += input1;
        if (input2 !== null) {
            result += " " + input2;
        }
        return result;
        }
```

Följande bild visas med den anpassade funktionen `OptionalParameterFunction` i regelredigeraren:

![Valfria eller obligatoriska parametrar ](/help/forms/assets/optional-default-params.png)

Du kan spara regeln utan att ange ett värde för de obligatoriska parametrarna, men regeln körs inte och ett varningsmeddelande visas som:

![varning om ofullständig regel](/help/forms/assets/incomplete-rule.png)

När användaren lämnar den valfria parametern tom, skickas värdet &quot;Odefinierad&quot; till den anpassade funktionen för den valfria parametern.

[Klicka här](https://jsdoc.app/tags-param) om du vill veta mer om hur du definierar valfria parametrar i JSDocs.

### Returtyp

Returtypen anger vilken typ av värde som den anpassade funktionen returnerar efter körningen. Följande syntaxer används för att definiera en returtyp i en anpassad funktion:

* `@return {type}`
* `@returns {type}`
  `{type}` representerar funktionens returtyp. Följande returtyper tillåts:
   * string: Representerar ett enda strängvärde.
   * number: Representerar ett numeriskt värde.
   * booleskt: Representerar ett enskilt booleskt värde (true eller false).
   * sträng []: Representerar en array med strängvärden.
   * tal[]: Representerar en matris med numeriska värden.
   * boolesk[]: Representerar en matris med booleska värden.
   * date: Representerar ett enda datumvärde.
   * date[]: Representerar en matris med datumvärden.
   * array: Representerar en generisk array som innehåller värden av olika typer.
   * objekt: Representerar formulärobjektet i stället för dess värde direkt.

  Returtypen är inte skiftlägeskänslig.

### Privat

Den anpassade funktionen som deklarerats som private visas inte i listan över anpassade funktioner i regelredigeraren för ett adaptivt formulär. Som standard är anpassade funktioner public. Syntaxen för att deklarera den anpassade funktionen som privat är `@private`.


## Riktlinjer när du skapar anpassade funktioner

Om du vill visa en lista över anpassade funktioner i regelredigeraren kan du använda något av följande format:

### Funktionssats med eller utan jsdoc-kommentarer

Du kan skapa en anpassad funktion med eller utan jsdoc-kommentarer.

```javascript
    function functionName(parameters) 
        {
            // code to be executed
        }
```
Om användaren inte lägger till några JavaScript-anteckningar i den anpassade funktionen visas den i regelredigeraren med sitt funktionsnamn. Vi rekommenderar dock att du tar med JavaScript-anteckningar för förbättrad läsbarhet av anpassade funktioner.

### Pilfunktion med obligatoriska JavaScript-anteckningar eller kommentarer

Du kan skapa en anpassad funktion med en pilfunktionssyntax:

```javascript
    /**
    * test function
    * @name testFunction 
    * @param {string} a parameter description
    * @param {string=} b parameter description
    * @return {string}
    */
    testFunction = (a, b) => {
    return a + b;
    };
    /** */
    testFunction1=(a) => (return a)
    /** */
    testFunction2 = a => a + 100;
    
```

Om användaren inte lägger till några JavaScript-anteckningar i den anpassade funktionen visas inte den anpassade funktionen i regelredigeraren för ett anpassat formulär.

### Funktionsuttryck med obligatoriska JavaScript-anteckningar eller kommentarer

Om du vill visa anpassade funktioner i regelredigeraren för ett adaptivt formulär skapar du anpassade funktioner i följande format:

```javascript
    /**
    * test function
    * @name testFunction 
    * @param {string} input1 parameter description
    * @param {string=} input2 parameter description
    * @return {string}
    */
    testFunction = function(input1,input2)
        {
            // code to be executed
        }
```

Om användaren inte lägger till några JavaScript-anteckningar i den anpassade funktionen visas inte den anpassade funktionen i regelredigeraren för ett anpassat formulär.

## Nästa steg

Mer information om hur du skapar och använder en anpassad funktion i ditt adaptiva formulär finns i artikeln [Skapa en anpassad funktion för ett adaptivt formulär baserat på kärnkomponenter](/help/forms/custom-function-core-component-create-function.md).

## Se även

{{see-also-rule-editor}}
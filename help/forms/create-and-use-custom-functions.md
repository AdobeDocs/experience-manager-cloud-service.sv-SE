---
title: Skapa och lägga till anpassade funktioner i ett adaptivt formulär
description: AEM Forms stöder anpassade funktioner som gör att användare kan skapa och använda sina egna funktioner i regelredigeraren.
keywords: Lägg till en anpassad funktion, använd en anpassad funktion, skapa en anpassad funktion, använd anpassad funktion i regelredigeraren.
contentOwner: Ruchita Srivastav
content-type: reference
feature: Adaptive Forms, Core Components
source-git-commit: 46fbed98a806f62dd1882eb0085d4338c5cd51a7
workflow-type: tm+mt
source-wordcount: '1100'
ht-degree: 0%

---


# Anpassade funktioner i Adaptive Forms (Core Components)

## Introduktion

AEM Forms har stöd för anpassade funktioner, vilket gör det möjligt för användare att definiera JavaScript-funktioner för implementering av komplexa affärsregler. Dessa anpassade funktioner gör att man kan förbättra blanketternas funktioner genom att underlätta hantering och bearbetning av inmatade data för att uppfylla specifika krav. De möjliggör också dynamisk ändring av formulärbeteende baserat på fördefinierade kriterier.
I Adaptiv Forms kan du använda anpassade funktioner i [regelredigerare för ett anpassat formulär](/help/forms/rule-editor-core-components.md) för att skapa specifika valideringsregler för formulärfält.

Låt oss förstå hur den anpassade funktionen används där användare anger e-postadressen och du vill se till att den angivna e-postadressen har ett visst format (den innehåller symbolen&quot;@&quot; och ett domännamn). Skapa en anpassad funktion som&quot;ValidateEmail&quot;, som tar e-postadressen som indata och returnerar true om den är giltig och i annat fall false.

```javascript
function ValidateEmail(inputText)
{
    var email = /^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})+$/;
    if(inputText.value.match(email))
        {
            alert("Valid email address!");
            return true;
        }
    else
    {
        alert("Invalid email address!");
        return false;
    }
}
```

I ovanstående exempel anropas den anpassade funktionen &quot;ValidateEmail&quot; för att kontrollera om den angivna e-postadressen är giltig när användaren försöker skicka formuläret.

### Användning av anpassade funktioner {#uses-of-custom-function}

Fördelarna med att använda anpassade funktioner i Adaptive Forms är:

* **Hantering av data**: Anpassade funktioner hanterar och bearbetar data som anges i formulärfälten.
* **Validering av data**: Med anpassade funktioner kan du utföra anpassade kontroller av formulärindata och tillhandahålla angivna felmeddelanden.
* **Dynamiskt beteende**: Med anpassade funktioner kan du styra formulärens dynamiska beteende baserat på specifika villkor. Du kan till exempel visa/dölja fält, ändra fältvärden eller justera formulärlogiken dynamiskt.
* **Integrering**: Du kan använda anpassade funktioner för att integrera med externa API:er eller tjänster. Det hjälper till att hämta data från externa källor, skicka data till externa Rest-slutpunkter eller utföra anpassade åtgärder baserade på externa händelser.

## JS-anteckningar som stöds

Se till att den anpassade funktionen som du skriver åtföljs av `jsdoc` ovanför den.

Stöds `jsdoc` taggar:

* **Privat**
Syntax: `@private`
En privat funktion ingår inte som en anpassad funktion.

* **Namn**
Syntax: `@name funcName <Function Name>`
Alternativt `,` du kan använda: `@function funcName <Function Name>` **eller** `@func` `funcName <Function Name>`.
  `funcName` är namnet på funktionen (inga blanksteg tillåts).
  `<Function Name>` är funktionens visningsnamn.

* **Parameter**
Syntax: `@param {type} name <Parameter Description>`
Du kan också använda: `@argument` `{type} name <Parameter Description>` **eller** `@arg` `{type}` `name <Parameter Description>`.
Visar parametrar som används av funktionen. En funktion kan ha flera parametertaggar, en tagg för varje parameter i ordningen för förekomst.
  `{type}` representerar parametertyp. Tillåtna parametertyper är:

   1. string
   2. tal
   3. boolesk
   4. omfång
   5. string[]
   6. tal[]
   7. boolesk[]
   8. datum
   9. datum[]
   10. array
   11. object

  `scope` refererar till ett särskilt globalt objekt som tillhandahålls av formulärkörningen. Det måste vara den sista parametern och ska inte vara synligt för användaren i regelredigeraren. Du kan använda omfång för att komma åt läsbara formulär- och fältobjekt för att läsa egenskaper, händelser som utlöste regeln och en uppsättning funktioner för att hantera formuläret.

  `object` type används för att skicka ett läsbart fältobjekt i parametern till en anpassad funktion i stället för att skicka värdet.

  Alla parametertyper kategoriseras under något av ovanstående. Ingen stöds inte. Välj en av typerna ovan. Typer är inte skiftlägeskänsliga. Blanksteg tillåts inte i parameternamnet.  Parameterbeskrivningen kan innehålla flera ord.

* **Valfri parameter**
Syntax: `@param {type=} name <Parameter Description>`
Du kan också använda: `@param {type} [name] <Parameter Description>`
Som standard är alla parametrar obligatoriska. Du kan markera en parameter som valfri genom att lägga till `=` i parameterns typ eller genom att ange parameternamn inom hakparenteser.
Låt oss till exempel deklarera `Input1` som valfri parameter:
   * `@param {type=} Input1`
   * `@param {type} [Input1]`

* **Returtyp**
Syntax: `@return {type}`
Du kan också använda `@returns {type}`.
Lägger till information om funktionen, till exempel dess mål.
{type} representerar funktionens returtyp. Följande returtyper tillåts:

   1. string
   2. tal
   3. boolesk
   4. string[]
   5. tal[]
   6. boolesk[]
   7. datum
   8. datum[]
   9. array
   10. object

Alla andra returtyper kategoriseras under en av ovanstående. Ingen stöds inte. Välj en av typerna ovan. Returtyperna är inte skiftlägeskänsliga.

## Att tänka på när du skapar anpassade funktioner {#considerations}

Om du vill visa en lista över anpassade funktioner i regelredigeraren kan du deklarera dem i något av följande format:

* **Funktionssats med eller utan jsdoc-kommentarer**

Du kan skapa en anpassad funktion med eller utan jsdoc-kommentarer.

```javascript
    function functionName(parameters) 
        {
            // code to be executed
        }
```
<!--

* **Arrow function with mandatory jsdoc comment**

Some of the examples to create Arrow functions are:
```javascript
    /**
    * test function
    * @name testFunction test function
    * @param {string} a some parameter description
    * @param {string} b another parameter description
    * @return {string}
    */
    testFunction = (a, b) => {
    return a + b;
    };
```

    * @param {string=} b another parameter description
      /** */
    testFunction1=(a) => (return a)
    /** */
    testFunction2 = a => a + 100;-->

* **Funktionsuttryck med obligatorisk jsdoc-kommentar**

Om du vill visa anpassade funktioner i regelredigeraren för ett adaptivt formulär skapar du anpassade funktioner i följande format:

```javascript
    /**
    * test function
    * @name testFunction test function
    * @param {string} input1 parameter description
    * @param {string} input2 another parameter description
    * @return {string}
    */
    testFunction = function(input1,input2)
        {
            // code to be executed
        }
```

<!--
* @param {string=} input2 another parameter description
The functions that are not supported in the custom function list are:
* Generator functions
* Async/Await functions 
* Method definitions
* Class methods
* Default parameters
* Rest parameters -->

>[!NOTE]
>
> Du kan kontrollera `error.log` om det finns fel i filen, t.ex. om anpassade funktioner inte visas i regelredigeraren.

<!--The `error.log` file also displays the methods and parameters that are not supported for custom functions. -->


## Skapa en anpassad funktion {#create-custom-function}

Skapa ett klientbibliotek för att anropa anpassade funktioner i regelredigeraren. Mer information finns i [Använda bibliotek på klientsidan](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/full-stack/clientlibs.html#developing).

Steg för att skapa anpassade funktioner är:
1. [Skapa ett klientbibliotek](#create-client-library)
1. [Lägga till klientbibliotek i ett adaptivt formulär](#use-custom-function)

### Skapa ett klientbibliotek {#create-client-library}

Du kan lägga till anpassade funktioner genom att lägga till klientbibliotek. Så här skapar du ett klientbibliotek:

1. [Klona din AEM Forms as a Cloud Service databas](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#accessing-git).
1. Skapa en mapp under `[AEM Forms as a Cloud Service repository folder]/apps/` mapp. Skapa till exempel en mapp med namnet som `experience-league`.
1. Navigera till `[AEM Forms as a Cloud Service repository folder]/apps/[AEM Project Folder]/experience-league/` och skapa `ClientLibraryFolder`. Skapa till exempel en biblioteksmapp för klient som `customclientlibs`.
1. Lägg till en egenskap `categories` med strängtypsvärde. Tilldela till exempel värdet `customfunctionscategory` till `categories` -egenskapen för `customclientlibs` mapp.

   >[!NOTE]
   >
   > Du kan välja valfritt namn för `client library folder` och `categories` -egenskap.

1. Skapa en mapp med namnet `js`.
1. Navigera till `[AEM Forms as a Cloud Service repository folder]/apps/[AEM Project Folder]/customclientlibs/js` mapp.
1. Lägg till en JavaScript-fil, till exempel `function.js`. Filen innehåller koden för den anpassade funktionen.

   >[!NOTE]
   >
   > Om JavaScript-filen som innehåller kod för anpassade funktioner har ett fel, visas inte de anpassade funktionerna i regelredigeraren i ett anpassat formulär. Du kan även kontrollera `error.log` fil för felet.

   <!-- 
    >* AEM Adaptive Form supports the caching of custom functions. If the JavaScript is modified, the caching becomes invalidated, and it is parsed. You can see a message as `Fetched following custom functions list from cache` in the `error.log` file.  -->

1. Spara `function.js` -fil.
1. Navigera till `[AEM Forms as a Cloud Service repository folder]/apps/[AEM Project Folder]/customclientlibs/js` mapp.
1. Lägg till en textfil som `js.txt`. Filen innehåller:

   ```javascript
       #base=js
       functions.js
   ```

1. Spara `js.txt` -fil.
1. Lägg till, implementera och skicka ändringarna i databasen med följande kommandon:

   ```javascript
       git add .
       git commit -a -m "Adding custom functions"
       git push
   ```

1. [Kör pipelinen.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#setup-pipeline)

När pipeline har körts blir den anpassade funktionen som lagts till i klientbiblioteket tillgänglig i din [Regelredigerare för anpassat formulär](/help/forms/rule-editor-core-components.md).

### Lägga till klientbibliotek i ett adaptivt formulär{#use-custom-function}

När du har distribuerat klientbiblioteket till Forms CS-miljön kan du använda funktionerna i ditt adaptiva formulär. Lägga till klientbiblioteket i ditt adaptiva formulär

1. Öppna formuläret i redigeringsläge. Om du vill öppna ett formulär i redigeringsläge markerar du ett formulär och väljer **[!UICONTROL Edit]**.
1. Öppna innehållsläsaren och välj **[!UICONTROL Guide Container]** som ingår i det adaptiva formuläret.
1. Klicka på egenskaperna för stödlinjebehållaren ![Stödlinjeegenskaper](/help/forms/assets/configure-icon.svg) -ikon. Dialogrutan Adaptiv formulärbehållare öppnas.
1. Öppna **[!UICONTROL Basic]** och välj namnet på **[!UICONTROL client library category]** från listrutan (i det här fallet väljer `customfunctionscategory`).

   ![Lägga till klientbiblioteket för anpassade funktioner](/help/forms/assets/clientlib-custom-function.png)

1. Klicka **[!UICONTROL Done]** .

Nu kan du skapa en regel som använder anpassade funktioner i regelredigeraren.

<!--

Create a rule to use custom function in the rule editor. 

### Support for the optional parameters in custom functions{#support-for-optional-parameter}

AEM supports including optional parameters in JSDocs. These parameters are displayed as optional in the rule editor. There are two ways to add optional parameters in JSDocs:
*  `@param {string=abc} b -- some description for b which is optional`

    In the above line of code, `b` is an optional parameter with the default value set to `abc`. 
    Alternatively, you can define `b` as an optional parameter without assigning any default value as `@param {string=} b -- some description for b which is optional`

* `@param {array} [z=[def,xyz]] - - some description for z which is optional`

    In the above line of code, `z` is an optional parameter of array type with the default value set to `[def , xyz]`. 
    Alternatively, you can define `z` as an optional parameter without assigning any default value as `@param {array} [z=] - - some description for z which is optional`

>[!NOTE]
>
> Ensure that the parameter name is enclosed in square brackets [] and the parameter type is enclosed in curly brackets {}. 

To learn more about how to define optional parameters in JSDocs, [click here](https://jsdoc.app/tags-param).

In the rule editor of an Adaptive Form, the parameters are displayed as `required`. By default the parameters are `required`, if not defined as optional in JSDocs.

  ![Optional or required parameters](/help/forms/assets/optional-default-params.png) 

  You can save the rule without specifying a value for required parameters, but the rule is not executed and displays a warning message as:

  ![incomplete rule warning message](/help/forms/assets/incomplete-rule.png) 
  
  The rule is executed even if you do not specify a value for optional parameters. Undefined values are passed for optional parameters on executing the rule.

  ### Support for field and globals objects in custom functions {#support-field-and-global-objects}

  needs to be discussed

  -->

## Se även {#see-also}

{{see-also}}






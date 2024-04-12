---
title: Skapa och lägga till anpassade funktioner i ett adaptivt formulär
description: AEM Forms stöder anpassade funktioner som gör att användare kan skapa och använda sina egna funktioner i regelredigeraren.
keywords: Lägg till en anpassad funktion, använd en anpassad funktion, skapa en anpassad funktion, använd anpassad funktion i regelredigeraren.
contentOwner: Ruchita Srivastav
content-type: reference
feature: Adaptive Forms, Core Components
exl-id: 24607dd1-2d65-480b-a831-9071e20c473d
source-git-commit: a22ecddf7c97c5894cb03eb44296e0562ac46ddb
workflow-type: tm+mt
source-wordcount: '3028'
ht-degree: 0%

---


<span class="preview"> Den här artikeln innehåller innehåll för vissa förhandsversionsfunktioner. De här förhandsversionsfunktionerna är bara tillgängliga via [kanal för förhandsversion](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html#new-features). Funktionerna i förhandsversionen är:
* Stöd för valfria parametrar i anpassade funktioner
* Cachelagringsfunktion för anpassade funktioner
* Global omfångsobjekt och fältobjekt har stöd för anpassade funktioner
* Stöd för moderna JavaScript-funktioner som låt- och pilfunktioner (ES10-stöd).
Se till att [kärnkomponenten är inställd på version 3.0.8](https://github.com/adobe/aem-core-forms-components) om du vill använda förhandsversionsfunktioner i en anpassad funktion. </span>

# Anpassade funktioner i Adaptive Forms (Core Components)

## Introduktion

AEM Forms har stöd för anpassade funktioner, vilket gör att användare kan definiera JavaScript-funktioner för implementering av komplexa affärsregler. Dessa anpassade funktioner gör att man kan förbättra blanketternas funktioner genom att underlätta hantering och bearbetning av inmatade data för att uppfylla specifika krav. De möjliggör också dynamisk ändring av formulärbeteende baserat på fördefinierade kriterier.

### Användning av anpassade funktioner {#uses-of-custom-function}

Fördelarna med att använda anpassade funktioner i Adaptive Forms är:

* **Databehandling**: Anpassade funktioner hjälper till att bearbeta data som anges i formulärfälten.
* **Validering av data**: Med anpassade funktioner kan du utföra anpassade kontroller av formulärindata och tillhandahålla angivna felmeddelanden.
* **Dynamiskt beteende**: Med anpassade funktioner kan du styra formulärens dynamiska beteende baserat på specifika villkor. Du kan till exempel visa/dölja fält, ändra fältvärden eller justera formulärlogiken dynamiskt.
* **Integrering**: Du kan använda anpassade funktioner för att integrera med externa API:er eller tjänster. Det hjälper till att hämta data från externa källor, skicka data till externa Rest-slutpunkter eller utföra anpassade åtgärder baserade på externa händelser.

Anpassade funktioner är i huvudsak klientbibliotek som läggs till i JavaScript-filen. När du har skapat en anpassad funktion blir den tillgänglig i regelredigeraren så att användaren kan välja den i ett adaptivt formulär. De anpassade funktionerna identifieras av JavaScript-anteckningarna i regelredigeraren.

### JavaScript-anteckningar som stöds för anpassade funktioner {#js-annotations}

JavaScript-anteckningar används för att tillhandahålla metadata för JavaScript-kod. Det innehåller kommentarer som börjar med specifika symboler, till exempel /** och @. Anteckningarna innehåller viktig information om funktioner, variabler och andra element i koden. Adaptiv form stöder följande JavaScript-anteckningar för anpassade funktioner:

* **Namn**
Namnet används för att identifiera den anpassade funktionen i regelredigeraren för ett adaptivt formulär. Följande syntaxer används för att namnge en anpassad funktion:
   * `@name [functionName] <Function Name>`
   * `@function [functionName] <Function Name>`
   * `@func [functionName] <Function Name>`.
     `functionName` är funktionens namn. Blanksteg är inte tillåtna.
     `<Function Name>` är visningsnamnet för funktionen i regelredigeraren för ett adaptivt formulär.
Om funktionsnamnet är identiskt med namnet på själva funktionen kan du utelämna det `[functionName]` från syntaxen. <!-- For example,  in the `calculateAge` custom function, the name is defined as:
`* @name calculateAge` -->

* **Parameter**
Parametern är en lista med argument som används av anpassade funktioner. En funktion kan ha stöd för flera parametrar. Följande syntaxer används för att definiera en parameter i en anpassad funktion:
   * `@param {type} name <Parameter Description>`
   * `@argument` `{type} name <Parameter Description>`
   * `@arg` `{type}` `name <Parameter Description>`.
     `{type}` representerar parametertypen.  Tillåtna parametertyper är:
      * string: Representerar ett enda strängvärde.
      * number: Representerar ett numeriskt värde.
      * booleskt: Representerar ett enskilt booleskt värde (true eller false).
      * string[]: Representerar en array med strängvärden.
      * tal[]: Representerar en array med numeriska värden.
      * boolesk[]: Representerar en array med booleska värden.
      * date: Representerar ett enda datumvärde.
      * datum[]: Representerar en array med datumvärden.
      * array: Representerar en generisk array som innehåller värden av olika typer.
      * object: Representerar formulärobjektet som skickas till en anpassad funktion i stället för att skicka dess värde direkt.
      * omfång: Representerar globalt objekt som används av anpassade funktioner vid körning. Den deklareras som den sista parametern i JavaScript-anteckningar och visas inte i regelredigeraren i ett adaptivt formulär. Omfångsparametern har åtkomst till formulärets eller komponentens objekt för att utlösa den regel eller händelse som krävs för formulärbearbetning.

  Parametertypen är inte skiftlägeskänslig och blanksteg tillåts inte i parameternamnet.

  `<Parameter Description>` innehåller information om parameterns syfte. Det kan innehålla flera ord.

  Som standard är alla parametrar obligatoriska. Du kan definiera en parameter som valfri genom att lägga till `=` efter parametertypen eller omslutningen av parameternamnet i  `[]`. Parametrar som definieras som valfria i JavaScript-anteckningar visas som valfria i regelredigeraren.
Om du vill definiera en variabel som en valfri parameter kan du använda någon av följande syntaxer:

   * `@param {type=} Input1`
I ovanstående kodrad `Input1` är en valfri parameter utan något standardvärde. Så här deklarerar du valfri parameter med standardvärdet:
     `@param {string=<value>} input1`

     `input1` som en valfri parameter med standardvärdet inställt på `value`.

   * `@param {type} [Input1]`
I ovanstående kodrad `Input1` är en valfri parameter utan något standardvärde. Så här deklarerar du valfri parameter med standardvärdet:
     `@param {array} [input1=<value>]`
     `input1` är en valfri parameter av arraytyp med standardvärdet inställt på `value`.
Kontrollera att parametertypen omges av klammerparenteser {} och parameternamnet omges av hakparenteser [].

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

     Följande bild visas med `OptionalParameterFunction` anpassad funktion i regelredigeraren:

     ![Valfria eller obligatoriska parametrar](/help/forms/assets/optional-default-params.png)

     Du kan spara regeln utan att ange ett värde för obligatoriska parametrar, men regeln körs inte och ett varningsmeddelande visas som:

     ![varningsmeddelande om ofullständig regel](/help/forms/assets/incomplete-rule.png)

     När användaren lämnar den valfria parametern tom, skickas värdet &quot;Odefinierad&quot; till den anpassade funktionen för den valfria parametern.

* **Returtyp**
Returtypen anger vilken typ av värde som den anpassade funktionen returnerar efter körningen. Följande syntaxer används för att definiera en returtyp i en anpassad funktion:
   * `@return {type}`
   * `@returns {type}`
     `{type}` representerar funktionens returtyp. Följande returtyper tillåts:
      * string: Representerar ett enda strängvärde.
      * number: Representerar ett numeriskt värde.
      * booleskt: Representerar ett enskilt booleskt värde (true eller false).
      * string[]: Representerar en array med strängvärden.
      * tal[]: Representerar en array med numeriska värden.
      * boolesk[]: Representerar en array med booleska värden.
      * date: Representerar ett enda datumvärde.
      * datum[]: Representerar en array med datumvärden.
      * array: Representerar en generisk array som innehåller värden av olika typer.
      * objekt: Representerar formulärobjektet i stället för dess värde direkt.

     Returtypen är inte skiftlägeskänslig.

* **Privat**
Den anpassade funktionen, som deklarerats som private, visas inte i listan över anpassade funktioner i regelredigeraren för ett adaptivt formulär. Som standard är anpassade funktioner public. Syntaxen för att deklarera den anpassade funktionen som private är `@private`.

Mer information om hur du definierar valfria parametrar i JSDocs finns i [klicka här](https://jsdoc.app/tags-param).

## Riktlinjer när du skapar anpassade funktioner {#considerations}

Om du vill visa en lista över anpassade funktioner i regelredigeraren kan du använda något av följande format:

* **Funktionssats med eller utan jsdoc-kommentarer**

Du kan skapa en anpassad funktion med eller utan jsdoc-kommentarer.

```javascript
    function functionName(parameters) 
        {
            // code to be executed
        }
```
Om användaren inte lägger till några JavaScript-anteckningar i den anpassade funktionen visas den i regelredigeraren med sitt funktionsnamn. Vi rekommenderar dock att du inkluderar JavaScript-anteckningar för förbättrad läsbarhet av anpassade funktioner.

* **Pilfunktion med obligatoriska JavaScript-anteckningar eller -kommentarer**

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

* **Funktionsuttryck med obligatoriska JavaScript-anteckningar eller -kommentarer**

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

1. [Kör pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#setup-pipeline) för att distribuera den anpassade funktionen.

När pipeline har körts blir den anpassade funktionen som lagts till i klientbiblioteket tillgänglig i din [Regelredigerare för anpassat formulär](/help/forms/rule-editor-core-components.md).

### Lägga till klientbibliotek i ett adaptivt formulär{#use-custom-function}

När du har distribuerat klientbiblioteket till Forms CS-miljön kan du använda funktionerna i ditt adaptiva formulär. Lägga till klientbiblioteket i ditt adaptiva formulär

1. Öppna formuläret i redigeringsläge. Om du vill öppna ett formulär i redigeringsläge markerar du ett formulär och väljer **[!UICONTROL Edit]**.
1. Öppna innehållsläsaren och välj **[!UICONTROL Guide Container]** som ingår i det adaptiva formuläret.
1. Klicka på egenskaperna för stödlinjebehållaren ![Stödlinjeegenskaper](/help/forms/assets/configure-icon.svg) -ikon. Dialogrutan Adaptiv formulärbehållare öppnas.
1. Öppna **[!UICONTROL Basic]** och välj namnet på **[!UICONTROL client library category]** från listrutan (i det här fallet väljer `customfunctionscategory`).

   ![Lägga till klientbiblioteket för anpassade funktioner](/help/forms/assets/clientlib-custom-function.png)

   >[!NOTE]
   >
   > Du kan lägga till flera kategorier genom att ange en kommaseparerad lista i **[!UICONTROL Client library category]** fält.

1. Klicka på **[!UICONTROL Done]**.

Du kan använda den anpassade funktionen i [regelredigerare för ett anpassat formulär](/help/forms/rule-editor-core-components.md) med [Javascript-anteckningar](##js-annotations).

## Använda en anpassad funktion i ett adaptivt formulär

I ett adaptivt formulär kan du använda [anpassade funktioner i regelredigeraren](/help/forms/rule-editor-core-components.md). Låt oss lägga till följande kod i JavaScript-filen (`Function.js` för att beräkna ålder baserat på födelsedatum (ÅÅÅÅ-MM-DD). Skapa en anpassad funktion som `calculateAge()` som tar födelsedatumet som indata och återgår till ålder:

```javascript
    /**
        * Calculates Age
        * @name calculateAge
        * @param {object} field
        * @return {string} 
    */

    function calculateAge(field) {
    var dob = new Date(field);
    var now = new Date();

    var age = now.getFullYear() - dob.getFullYear();
    var monthDiff = now.getMonth() - dob.getMonth();

    if (monthDiff < 0 || (monthDiff === 0 && now.getDate() < dob.getDate())) {
    age--;
    }

    return age;
    }
```

I exemplet ovan, när användaren anger födelsedatumet i formatet (ÅÅÅÅ-MM-DD), är den anpassade funktionen `calculateAge` anropas och returnerar åldern.

![Anpassad funktion för beräkningsagenten i regelredigeraren](/help/forms/assets/custom-function-calculate-age.png)

Låt oss förhandsgranska formuläret för att se hur de anpassade funktionerna implementeras via regelredigeraren:

![Anpassad funktion för Beräkna arbetsyta i regelredigerarens formulärförhandsgranskning](/help/forms/assets/custom-function-age-calculate-form.png)

>[!NOTE]
>
> Du kan se följande [anpassad funktion](/help/forms/assets//customfunctions.zip) mapp. Hämta och installera den här mappen i AEM med [Pakethanterare](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developer-tools/package-manager).

### Stöd för asynkrona funktioner i anpassade funktioner {#support-of-async-functions}

Asynkrona anpassade funktioner visas inte i regelredigeringslistan. Det går dock att anropa asynkrona funktioner i anpassade funktioner som skapats med synkrona funktionsuttryck.

![Synkronisera och asynkron anpassad funktion](/help/forms/assets/workflow-for-sync-async-custom-fumction.png)

>[!NOTE]
>
> Fördelen med att anropa asynkrona funktioner i anpassade funktioner är att asynkrona funktioner tillåter samtidig körning av flera åtgärder, med resultatet av varje funktion som används i de anpassade funktionerna.

Titta på koden nedan för att se hur vi kan anropa asynkrona funktioner med anpassade funktioner:

```javascript
    
    async function asyncFunction() {
    const response = await fetch('https://petstore.swagger.io/v2/store/inventory');
    const data = await response.json();
    return data;
    }

    /**
    * callAsyncFunction
    * @name callAsyncFunction callAsyncFunction
    */
    function callAsyncFunction() {
    asyncFunction()
        .then(responseData => {
        console.log('Response data:', responseData);
        })
        .catch(error => {
         console.error('Error:', error);
    });
}
```

I ovanstående exempel är funktionen asyncFunction en `asynchronous function`. Den utför en asynkron åtgärd genom att göra en `GET` begäran till `https://petstore.swagger.io/v2/store/inventory`. Det väntar på svar med `await`, tolkar svarsbrödtexten som JSON med `response.json()`och returnerar sedan data. The `callAsyncFunction` funktionen är en synkron anpassad funktion som anropar `asyncFunction` och visar svarsdata i konsolen. Även om `callAsyncFunction` funktionen är synkron, anropar den asynkrona asynkrona funktionen asyncFunction och hanterar resultatet med `then` och `catch` -programsatser.

För att se hur den fungerar kan vi lägga till en knapp och skapa en regel för knappen som anropar den asynkrona funktionen när en knapp klickas.

![skapa regel för asynkron funktion](/help/forms/assets/rule-for-async-funct.png)

Se bilden på konsolfönstret nedan för att visa att när användaren klickar på `Fetch` knapp, den anpassade funktionen `callAsyncFunction` anropas, vilket i sin tur anropar en asynkron funktion `asyncFunction`. Inspect i konsolfönstret för att visa svaret när knappen klickar:

![Konsolfönstret](/help/forms/assets/async-custom-funct-console.png)

Låt oss dyka upp i funktionerna för anpassade funktioner.

## Olika funktioner för anpassade funktioner

Du kan använda anpassade funktioner för att lägga till anpassade funktioner i formulär. Dessa funktioner har stöd för olika funktioner, som att arbeta med specifika fält, använda globala fält eller cachelagring. Tack vare denna flexibilitet kan ni anpassa formulären efter organisationens behov.

### Fält- och globala omfångsobjekt i anpassade funktioner {#support-field-and-global-objects}

Fältobjekt refererar till enskilda komponenter eller element i ett formulär, t.ex. textfält och kryssrutor. Globala omfångsobjekt refererar till globala variabler eller inställningar som är tillgängliga i hela formuläret. Vi ska titta på följande kodfragment:

```JavaScript
    /**
    * updateDateTime
    * @name updateDateTime
    * @param {object} field
    * @param {scope} globals 
    */
    function updateDateTime(field, globals) {
    // Accessing the Date object from the global scope
    var currentDate = new Date();
    // Formatting the date and time
    var formattedDateTime = currentDate.toLocaleString();
    // Updating the field value with the formatted date and time
    field.value = formattedDateTime;
    }
```

>[!NOTE]
>
> The `param {scope} globals` måste vara den sista parametern och den visas inte i regelredigeraren för ett adaptivt formulär.

I ovanstående kodfragment finns en anpassad funktion med namnet `updateDateTime` tar parametrar som fältobjekt och globala objekt. Objekten date och time nås med det globala omfånget. Fältet representerar textruteobjektet där det formaterade datum- och tidsvärdet visas i formuläret.

Låt oss lära oss hur anpassade funktioner använder fält och globala objekt med hjälp av en `Contact Us` formulär med olika användningsområden.

![Kontakta oss](/help/forms/assets/contact-us-form.png)

#### **Användningsfall**: Visa en panel med `SetProperty` regel

Lägg till följande kod i den anpassade funktionen enligt anvisningarna i [create-custom-function](#create-custom-function) för att ange formulärfältet som `Required`.

```javascript
    
	/**
    * enablePanel
    * @name enablePanel
    * @param {object} field1
    * @param {object} field2
    * @param {scope} globals 
    */

    function enablePanel(field1,field2, globals)
    {
       if(globals.functions.validate(field1).length === 0)
       {
       globals.functions.setProperty(field2, {visible: true});
       }
    }
```

>[!NOTE]
>
> Du kan konfigurera fältegenskaperna med hjälp av de tillgängliga egenskaperna i `[form-path]/jcr:content/guideContainer.model.json`.

I det här exemplet valideras `personaldetails` när du klickar på knappen. Om inga fel upptäcks på panelen visas en annan panel, `feedback` visas när du klickar på knappen.

Låt oss skapa en regel för `Next` som validerar `personaldetails` panelen och skapar `feedback`  visas när användaren klickar på `Next` -knappen.

![Ange egenskap](/help/forms/assets/custom-function-set-property.png)

Se bilden nedan för att visa var `personaldetails` panelen valideras när du klickar på `Next` -knappen. Om alla fält i `personaldetails` valideras, `feedback` visas.

![Ange förhandsgranskning av egenskapsformulär](/help/forms/assets/set-property-form-preview.png)

Om det finns fel i fälten i `personaldetails` visas de på fältnivå när du klickar på `Next` och `feedback` panelen förblir osynlig.

![Ange förhandsgranskning av egenskapsformulär](/help/forms/assets/set-property-panel.png)

#### **Användningsfall**: Verifiera fältet.

Lägg till följande kod i den anpassade funktionen enligt anvisningarna i [create-custom-function](#create-custom-function) för att validera fältet.

```javascript
    /**
    * validateField
    * @name validateField
    * @param {object} field
    * @param {scope} globals
    */
    function validateField(field,globals)
    {
    
        globals.functions.validate(field);
    
    }   
```

>[!NOTE]
>
> Om inget argument skickas i `validate()` validerar den formuläret.

I det här exemplet används ett anpassat valideringsmönster för `contact` fält. Användare måste ange ett telefonnummer som börjar med `10` följt av `8` siffror. Om användaren anger ett telefonnummer som inte börjar med `10` eller innehåller mer eller mindre än `8` siffror visas ett valideringsfelmeddelande när knappen klickar:

![Mönster för e-postadressvalidering](/help/forms/assets/custom-function-validation-pattern.png)

Nästa steg är att skapa en regel för `Next` som validerar `contact` klickar du på knappen.

![Valideringsmönster](/help/forms/assets/custom-function-validate.png)

Se bilden nedan för att visa att om användaren anger ett telefonnummer som inte börjar med `10`visas ett felmeddelande på fältnivå:

![Mönster för e-postadressvalidering](/help/forms/assets/custom-function-validate-error-message.png)

Om användaren anger ett giltigt telefonnummer och alla fält i dialogrutan `personaldetails` panelen valideras, `feedback` visas på skärmen:

![Mönster för e-postadressvalidering](/help/forms/assets/validate-form-preview-form.png)

#### **Användningsfall**: Återställ en panel

Lägg till följande kod i den anpassade funktionen enligt anvisningarna i [create-custom-function](#create-custom-function) för att återställa panelen.

```javascript
    /**
    * resetField
    * @name  resetField
    * @param {string} input1
    * @param {object} field
    * @param {scope} globals 
    */
    function  resetField(field,globals)
    {
    
        globals.functions.reset(field);
    
    }
```

>[!NOTE]
>
> Om inget argument skickas i `reset()` validerar den formuläret.

I det här exemplet `personaldetails` panelen återställs när du klickar på `Clear` -knappen. Nästa steg är att skapa en regel för `Clear` som återställer panelen när knappen klickas.

![Knappen Rensa](/help/forms/assets/custom-function-reset-field.png)

Se bilden nedan för att visa att om användaren klickar på `clear` -knappen `personaldetails` panelåterställningar:

![Återställ formulär](/help/forms/assets/custom-function-reset-form.png)

#### **Användningsfall**: Om du vill visa ett anpassat meddelande på fältnivå och markera fältet som ogiltigt

Du kan använda `markFieldAsInvalid()` för att definiera ett fält som ogiltigt och ange ett anpassat felmeddelande på fältnivå. The `fieldIdentifier` värdet kan `fieldId`, eller `field qualifiedName`, eller `field dataRef`. Värdet för objektet med namnet `option` kan `{useId: true}`, `{useQualifiedName: true}`, eller `{useDataRef: true}`.
Syntaxerna som används för att markera fält som ogiltiga och ange anpassade meddelanden är:

* `globals.functions.markFieldAsInvalid(field.$id,"[custom message]",{useId: true});`
* `globals.functions.markFieldAsInvalid(field.$qualifiedName, "[custom message]", {useQualifiedName: true});`
* `globals.functions.markFieldAsInvalid(field.$dataRef, "[custom message]", {useDataRef: true});`

Lägg till följande kod i den anpassade funktionen enligt anvisningarna i [create-custom-function](#create-custom-function) för att aktivera anpassade meddelanden på fältnivå.

```javascript
    /**
    * customMessage
    * @name customMessage
    * @param {object} field
    * @param {scope} globals 
    */
    function customMessage(field, globals) {
    const minLength = 15;
    const comments = field.$value.trim();
    if (comments.length < minLength) {
        globals.functions.markFieldAsInvalid(field.$id, "Comments must be at least 15 characters long.", { useId: true });
    }
}
```

I det här exemplet visas ett anpassat meddelande på fältnivå om användaren skriver färre än 15 tecken i textrutan för kommentarer.

Nästa steg är att skapa en regel för `comments` fält:

![Markera fältet som ogiltigt](/help/forms/assets/custom-function-invalid-field.png)

Se demonstrationen nedan för att visa att du anger negativ feedback i `comments` fältet utlöser visning av ett anpassat meddelande på fältnivå:

![Markera fältet som ogiltigt förhandsgranskningsformulär](/help/forms/assets/custom-function-invalidfield-form.png)

Om användaren skriver in mer än 15 tecken i textrutan för kommentarer valideras fältet och formuläret skickas:

![Markera fältet som ett giltigt förhandsgranskningsformulär](/help/forms/assets/custom-function-validfield-form.png)


#### **Användningsfall**: Skicka ändrade data till servern

Följande kodrad:
`globals.functions.submitForm(globals.functions.exportData(), false);` används för att skicka formulärdata efter manipulering.
* Det första argumentet är de data som ska skickas.
* Det andra argumentet anger om formuläret ska valideras innan det skickas in. Det är `optional` och ange som `true` som standard.
* Det tredje argumentet är `contentType` av inlämningen, som också `optional` med standardvärdet som `multipart/form-data`.

Lägg till följande kod i den anpassade funktionen enligt anvisningarna i [create-custom-function](#create-custom-function) för att skicka manipulerade data till servern:

```javascript
    /**
    * submitData
    * @name submitData
    * @param {object} field
    * @param {scope} globals 
    */

    function submitData(globals)
    {
    
    var data = globals.functions.exportData();
    if(!data.comments) {
    data.comments = 'NA';
    }
    console.log('After update:{}',data);
    globals.functions.submitForm(data, false);
    }
```

Om användaren i det här exemplet lämnar `comments` textrutan är tom, `NA` skickas till servern när formuläret skickas in.

Skapa nu en regel för `Submit` knapp som skickar data:

![Skicka data](/help/forms/assets/custom-function-submit-data.png)

Se bilden på `console window` nedan för att visa att om användaren lämnar `comments` textrutan är tom, sedan värdet som `NA` skickas till servern:

![Skicka data till konsolfönstret](/help/forms/assets/custom-function-submit-data-form.png)

Du kan även kontrollera konsolfönstret för att visa data som skickats till servern:

![Inspect data i konsolfönstret](/help/forms/assets/custom-function-submit-data-console-data.png)

## Cachelagringsstöd för anpassad funktion

Adaptiv Forms implementerar cachning för anpassade funktioner för att förbättra svarstiden samtidigt som den anpassade funktionslistan hämtas i regelredigeraren. Ett meddelande som `Fetched following custom functions list from cache` visas i `error.log` -fil.

![anpassad funktion med cache-stöd](/help/forms/assets/custom-function-cache-error.png)

Om de anpassade funktionerna ändras blir cachningen ogiltig och den tolkas.

## Felsökning

Om JavaScript-filen som innehåller kod för anpassade funktioner har ett fel, visas inte de anpassade funktionerna i regelredigeraren i ett anpassat formulär. Om du vill kontrollera listan med anpassade funktioner kan du navigera till `error.log` fil för felet. Om ett fel uppstår visas listan med anpassade funktioner tom:

![felloggfil](/help/forms/assets/custom-function-list-error-file.png)

Om inget fel uppstår hämtas den anpassade funktionen och visas i `error.log` -fil. Ett meddelande som `Fetched following custom functions list` visas i `error.log` fil:

![felloggfil med korrekt anpassad funktion](/help/forms/assets/custom-function-list-fetched-in-error.png)

## Överväganden

* The `parameter type` och `return type` stöder inte `None`.

* De funktioner som inte stöds i den anpassade funktionslistan är:
   * Generatorfunktioner
   * Async-/Await-funktioner
   * Metoddefinitioner
   * Klassmetoder
   * Standardparametrar
   * Restparametrar

## Se även {#see-also}

{{see-also}}



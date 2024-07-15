---
title: Skapa och lägga till anpassade funktioner i ett adaptivt formulär
description: AEM Forms har stöd för anpassade funktioner, som gör att användare kan skapa och använda sina egna funktioner i regelredigeraren.
keywords: Lägg till en anpassad funktion, använd en anpassad funktion, skapa en anpassad funktion, använd anpassad funktion i regelredigeraren.
contentOwner: Ruchita Srivastav
content-type: reference
feature: Adaptive Forms, Core Components
exl-id: 24607dd1-2d65-480b-a831-9071e20c473d
role: User, Developer
source-git-commit: 52b87073cad84705b5dc0c6530aff44d1e686609
workflow-type: tm+mt
source-wordcount: '4322'
ht-degree: 0%

---


# Anpassade funktioner i Adaptive Forms (Core Components)

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/adaptive-forms-core-components/create-and-use-custom-functions) |
| AEM as a Cloud Service | Den här artikeln |

## Introduktion

AEM Forms har stöd för anpassade funktioner, vilket gör att man kan definiera JavaScript-funktioner för att implementera komplexa affärsregler. Dessa anpassade funktioner gör att man kan förbättra blanketternas funktioner genom att underlätta hantering och bearbetning av inmatade data för att uppfylla specifika krav. De möjliggör också dynamisk ändring av formulärbeteende baserat på fördefinierade kriterier.

>[!NOTE]
>
> Kontrollera att [kärnkomponenten](https://github.com/adobe/aem-core-forms-components) är inställd på den senaste versionen för att använda de senaste funktionerna.

### Användning av anpassade funktioner {#uses-of-custom-function}

Fördelarna med att använda anpassade funktioner i Adaptive Forms är:
* **Databearbetning**: Anpassade funktioner hjälper dig att bearbeta data som anges i formulärfälten.
* **Validering av data**: Med anpassade funktioner kan du utföra anpassade kontroller av formulärindata och tillhandahålla angivna felmeddelanden.
* **Dynamiskt beteende**: Med anpassade funktioner kan du styra det dynamiska beteendet i dina formulär baserat på specifika villkor. Du kan till exempel visa/dölja fält, ändra fältvärden eller justera formulärlogiken dynamiskt.
* **Integration**: Du kan använda anpassade funktioner för att integrera med externa API:er eller tjänster. Det hjälper till att hämta data från externa källor, skicka data till externa Rest-slutpunkter eller utföra anpassade åtgärder baserade på externa händelser.

Anpassade funktioner är i huvudsak klientbibliotek som läggs till i JavaScript-filen. När du har skapat en anpassad funktion blir den tillgänglig i regelredigeraren så att användaren kan välja den i ett adaptivt formulär. De anpassade funktionerna identifieras av JavaScript kommentarer i regelredigeraren.

### JavaScript-anteckningar som stöds för anpassade funktioner {#js-annotations}

JavaScript-anteckningar används för att tillhandahålla metadata för JavaScript-kod. Det innehåller kommentarer som börjar med specifika symboler, till exempel /** och @. Anteckningarna innehåller viktig information om funktioner, variabler och andra element i koden. Adaptiv form stöder följande JavaScript-anteckningar för anpassade funktioner:

#### Namn

Namnet används för att identifiera den anpassade funktionen i regelredigeraren för ett adaptivt formulär. Följande syntaxer används för att namnge en anpassad funktion:

* `@name [functionName] <Function Name>`
* `@function [functionName] <Function Name>`
* `@func [functionName] <Function Name>`.
  `functionName` är namnet på funktionen. Blanksteg är inte tillåtna.
  `<Function Name>` är funktionens visningsnamn i regelredigeraren för ett adaptivt formulär.
Om funktionsnamnet är identiskt med namnet på själva funktionen kan du utelämna `[functionName]` från syntaxen.

#### Parameter

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
   * omfång: Representerar det globala objektet, som innehåller skrivskyddade variabler som formulärinstanser, målfältsinstanser och metoder för att utföra formulärändringar i anpassade funktioner. Den deklareras som den sista parametern i JavaScript-anteckningar och visas inte i regelredigeraren för ett adaptivt formulär. Omfångsparametern har åtkomst till formulärets eller komponentens objekt för att utlösa den regel eller händelse som krävs för formulärbearbetning. Om du vill ha mer information om det globala objektet och hur du använder det [klickar du här](/help/forms/create-and-use-custom-functions.md#support-field-and-global-objects).

Parametertypen är inte skiftlägeskänslig och blanksteg tillåts inte i parameternamnet.

`<Parameter Description>` innehåller information om parameterns syfte. Det kan innehålla flera ord.

**Valfria parametrar**
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

#### Returtyp

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

#### Privat

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

## Skapa en anpassad funktion {#create-custom-function}

Skapa ett klientbibliotek för att anropa anpassade funktioner i regelredigeraren. Mer information finns i [Använda klientbibliotek](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/full-stack/clientlibs.html#developing).

Steg för att skapa anpassade funktioner är:
1. [Skapa ett klientbibliotek](#create-client-library)
1. [Lägga till klientbibliotek i ett adaptivt formulär](#use-custom-function)


### Krav för att skapa en anpassad funktion

Innan du börjar lägga till en anpassad funktion i din adaptiva Forms måste du se till att du har följande:

**Programvara:**

* **Vanlig textredigerare (IDE)**: En integrerad utvecklingsmiljö (IDE), som Microsoft Visual Studio Code, har avancerade funktioner för enklare redigering, även om en vanlig textredigerare kan fungera.

* **Git:** Versionskontrollsystemet krävs för att hantera kodändringar. Om du inte har det installerat hämtar du det från https://git-scm.com.

### Skapa ett klientbibliotek {#create-client-library}

Du kan lägga till anpassade funktioner genom att lägga till ett klientbibliotek. Så här skapar du ett klientbibliotek:

**Klona databasen**

Klona din [AEM Forms as a Cloud Service-databas](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#accessing-git):

1. Öppna kommandoraden eller terminalfönstret.

1. Navigera till önskad plats på datorn där du vill lagra databasen.

1. Kör följande kommando för att klona databasen:

   `git clone [Git Repository URL]`

Det här kommandot hämtar databasen och skapar en lokal mapp för den klonade databasen på din dator. I hela den här handboken ser vi den här mappen som [AEMaaCS-projektkatalog].

**Lägg till en klientbiblioteksmapp**

Så här lägger du till en ny biblioteksmapp för klienten i [AEMaaCS-projektkatalogen]:

1. Öppna [AEMaaCS-projektkatalogen] i en redigerare.

   ![anpassad struktur för funktionsmapp](/help/forms/assets/custom-library-folder-structure.png)

1. Sök efter `ui.apps`.
1. Lägg till ny mapp. Lägg till exempel till en mapp med namnet `experience-league`.
1. Navigera till mappen `/experience-league/` och lägg till en `ClientLibraryFolder`. Skapa till exempel en klientbiblioteksmapp med namnet `customclientlibs`.

   `Location is: [AEMaaCS project directory]/ui.apps/src/main/content/jcr_root/apps/`

**Lägg till filer och mappar i mappen Klientbibliotek**

Lägg till följande i den tillagda klientbiblioteksmappen:

* .content.xml-fil
* js.txt, fil
* js-mapp

`Location is: [AEMaaCS project directory]/ui.apps/src/main/content/jcr_root/apps/experience-league/customclientlibs/`

1. Lägg till följande kodrader i `.content.xml`:

   ```javascript
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:cq="http://www.day.com/jcr/cq/1.0" xmlns:jcr="http://www.jcp.org/jcr/1.0"
   jcr:primaryType="cq:ClientLibraryFolder"
   categories="[customfunctionscategory]"/>
   ```

   >[!NOTE]
   >
   > Du kan välja vilket namn som helst för egenskapen `client library folder` och `categories`.

1. Lägg till följande kodrader i `js.txt`:

   ```javascript
         #base=js
       function.js
   ```
1. Lägg till javascript-filen som `function.js` i mappen `js` som innehåller de anpassade funktionerna:

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
1. Spara filerna.

![anpassad struktur för funktionsmapp](/help/forms/assets/custom-function-added-files.png)

**Inkludera den nya mappen i filter.xml**:

1. Navigera till filen `/ui.apps/src/main/content/META-INF/vault/filter.xml` i [AEMaaCS-projektkatalogen].

1. Öppna filen och lägg till följande rad i slutet:

   `<filter root="/apps/experience-league" />`
1. Spara filen.

![XML för anpassat funktionsfilter](/help/forms/assets/custom-function-filterxml.png)

**Distribuera den nyligen skapade biblioteksmappen för klienter till AEM**

Distribuera AEM as a Cloud Service, [AEMaaCS-projektkatalogen], till din Cloud Service. Så här distribuerar du till din Cloud Service:

1. Verkställ ändringarna

   1. Lägg till, implementera och skicka ändringarna i databasen med följande kommandon:

   ```javascript
       git add .
       git commit -a -m "Adding custom functions"
       git push
   ```

1. Distribuera den uppdaterade koden:

   1. Utlösa en distribution av koden via den befintliga pipeline-funktionen för hela stackar. Detta skapar och distribuerar automatiskt den uppdaterade koden.

Om du inte redan har konfigurerat en pipeline kan du läsa guiden [Konfigurera en pipeline för AEM Forms as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#setup-pipeline).

När pipeline har körts blir den anpassade funktion som lagts till i klientbiblioteket tillgänglig i regelredigeraren [Adaptiv form](/help/forms/rule-editor-core-components.md).

### Lägga till klientbibliotek i ett adaptivt formulär{#use-custom-function}

När du har distribuerat klientbiblioteket till Forms CS-miljön kan du använda funktionerna i ditt adaptiva formulär. Lägga till klientbiblioteket i ditt adaptiva formulär

1. Öppna formuläret i redigeringsläge. Om du vill öppna ett formulär i redigeringsläge markerar du ett formulär och väljer **[!UICONTROL Edit]**.
1. Öppna innehållsläsaren och markera komponenten **[!UICONTROL Guide Container]** i det adaptiva formuläret.
1. Klicka på ikonen för egenskaper för stödlinjebehållaren ![Egenskaper för stödlinje](/help/forms/assets/configure-icon.svg) . Dialogrutan Adaptiv formulärbehållare öppnas.
1. Öppna fliken **[!UICONTROL Basic]** och välj namnet på **[!UICONTROL client library category]** i listrutan (välj i det här fallet `customfunctionscategory`).

   ![Lägger till klientbiblioteket för anpassade funktioner](/help/forms/assets/clientlib-custom-function.png)

   >[!NOTE]
   >
   > Du kan lägga till flera kategorier genom att ange en kommaavgränsad lista i fältet **[!UICONTROL Client library category]**.

1. Klicka på **[!UICONTROL Done]**.

Du kan använda den anpassade funktionen i [regelredigeraren för ett adaptivt formulär](/help/forms/rule-editor-core-components.md) med [JavaScript-anteckningar](##js-annotations).

## Använda en anpassad funktion i ett adaptivt formulär

I ett anpassat formulär kan du använda [anpassade funktioner i regelredigeraren](/help/forms/rule-editor-core-components.md). Låt oss lägga till följande kod i JavaScript-filen (`Function.js`) för att beräkna ålder baserat på födelsedatum (ÅÅÅÅ-MM-DD). Skapa en anpassad funktion som `calculateAge()` som tar födelsedatumet som indata och returnerar ålder:

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

I ovanstående exempel anropas den anpassade funktionen `calculateAge` när användaren anger födelsedatumet i formatet (ÅÅÅÅ-MM-DD) och sedan returnerar ålder.

![Anpassad funktion för beräkningsagenten i regelredigeraren](/help/forms/assets/custom-function-calculate-age.png)

Låt oss förhandsgranska formuläret för att se hur de anpassade funktionerna implementeras via regelredigeraren:

![Anpassad funktion för beräkning av agens i regelredigerarens formulärförhandsgranskning](/help/forms/assets/custom-function-age-calculate-form.png)

>[!NOTE]
>
> Du kan referera till följande [anpassade funktionsmapp](/help/forms/assets//customfunctions.zip). Hämta och installera den här mappen i AEM med hjälp av [Package Manager](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developer-tools/package-manager).


### Ange alternativ för listrutor med anpassade funktioner

Regelredigeraren i Core Components stöder inte egenskapen **Set Options of** för att ange alternativ för listrutelistan vid körning. Du kan dock ange alternativ för listrutor med anpassade funktioner.

Titta på koden nedan för att se hur vi kan ange alternativ för listrutor med anpassade funktioner:

```javascript
    /**
    * @name setEnums
    * @returns {string[]}
    **/
    function setEnums() {
    return ["0","1","2","3","4","5","6"];   
    }

    /**
    * @name setEnumNames
    * @returns {string[]}
    **/
    function setEnumNames() {
    return ["Sunday","Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"];
    }
```

I ovanstående kod används `setEnums` för att ange egenskapen `enum` och `setEnumNames` används för att ange egenskapen `enumNames` för listrutan.

Låt oss skapa en regel för knappen `Next`, som anger värdet för alternativet för nedrullningsbar lista när användaren klickar på knappen `Next`:

![Alternativ för nedrullningsbar lista](/help/forms/assets/drop-down-list-options.png)

Se bilden nedan för att visa var alternativen i listrutan ställs in när du klickar på knappen Visa:

![Listrutealternativ i regelredigeraren](/help/forms/assets/drop-down-option-rule-editor.png)



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

I ovanstående exempel är funktionen asyncFunction en `asynchronous function`. Den utför en asynkron åtgärd genom att göra en `GET`-begäran till `https://petstore.swagger.io/v2/store/inventory`. Det väntar på svar med `await`, tolkar svarstexten som JSON med `response.json()` och returnerar sedan data. Funktionen `callAsyncFunction` är en synkron anpassad funktion som anropar funktionen `asyncFunction` och visar svarsdata i konsolen. Även om funktionen `callAsyncFunction` är synkron anropar den asynkrona funktionen asyncFunction och hanterar resultatet med programsatserna `then` och `catch`.

För att se hur den fungerar kan vi lägga till en knapp och skapa en regel för knappen som anropar den asynkrona funktionen när en knapp klickas.

![skapar regel för asynkron funktion](/help/forms/assets/rule-for-async-funct.png)

Titta på bilden för konsolfönstret nedan för att visa att när användaren klickar på knappen `Fetch` anropas den anpassade funktionen `callAsyncFunction` som i sin tur anropar en asynkron funktion `asyncFunction`. Inspect i konsolfönstret för att visa svaret på knappen:

![Konsolfönstret](/help/forms/assets/async-custom-funct-console.png)

Låt oss dyka upp i funktionerna för anpassade funktioner.

## Olika funktioner för anpassade funktioner

Du kan använda anpassade funktioner för att lägga till anpassade funktioner i formulär. Dessa funktioner har stöd för olika funktioner, som att arbeta med specifika fält, använda globala fält eller cachelagring. Tack vare denna flexibilitet kan ni anpassa formulären efter organisationens behov.

### Fält- och globala omfångsobjekt i anpassade funktioner {#support-field-and-global-objects}

Fältobjekt refererar till de enskilda komponenterna eller elementen i ett formulär, t.ex. textfält och kryssrutor. Globals-objektet innehåller skrivskyddade variabler som formulärinstans, målfältsinstans och metoder för att göra formulärändringar i anpassade funktioner.

>[!NOTE]
>
> `param {scope} globals` måste vara den sista parametern och visas inte i regelredigeraren för ett anpassat formulär.

<!-- Let us look at the following code snippet:

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
    // Updating the field value with the formatted date and time using setProperty.
    globals.functions.setProperty(field, {value: formattedDateTime});
    }
```

In the above code snippet, a custom function named `updateDateTime` takes parameters such as a field object and a global object. The field represents the textbox object where the formatted date and time value is displayed within the form. -->

Låt oss lära oss hur anpassade funktioner använder fält och globala objekt med hjälp av ett `Contact Us`-formulär med olika användningsfall.

![Kontakta oss ](/help/forms/assets/contact-us-form.png)

+++ **Använd skiftläge**: Visa en panel med regeln `SetProperty`

Lägg till följande kod i den anpassade funktionen enligt beskrivningen i avsnittet [create-custom-function](#create-custom-function) för att ange formulärfältet som `Required`.

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
> * Du kan konfigurera fältegenskaperna med hjälp av de tillgängliga egenskaperna i `[form-path]/jcr:content/guideContainer.model.json`.
> * Ändringar som görs i formuläret med metoden `setProperty` för Global-objektet är asynkrona och återspeglas inte när den anpassade funktionen körs.

I det här exemplet valideras panelen `personaldetails` när du klickar på knappen. Om inga fel upptäcks på panelen visas en annan panel, `feedback`-panelen, när du klickar på knappen.

Låt oss skapa en regel för knappen `Next` som validerar panelen `personaldetails` och gör panelen `feedback` synlig när användaren klickar på knappen `Next`.

![Ange egenskap](/help/forms/assets/custom-function-set-property.png)

Se bilden nedan för att visa var panelen `personaldetails` valideras när du klickar på knappen `Next`. Om alla fält i `personaldetails` valideras blir panelen `feedback` synlig.

![Ange förhandsgranskning av egenskapsformulär](/help/forms/assets/set-property-form-preview.png)

Om det finns fel i fälten på panelen `personaldetails` visas de på fältnivå när du klickar på knappen `Next` och panelen `feedback` visas inte.

![Ange förhandsgranskning av egenskapsformulär](/help/forms/assets/set-property-panel.png)

+++

+++ **Använd skiftläge**: Verifiera fältet.

Lägg till följande kod i den anpassade funktionen enligt anvisningarna i avsnittet [create-custom-function](#create-custom-function) för att validera fältet.

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
> Om inget argument skickas i funktionen `validate()` valideras formuläret.

I det här exemplet används ett anpassat valideringsmönster för fältet `contact`. Användare måste ange ett telefonnummer som börjar med `10` följt av `8` siffror. Om användaren anger ett telefonnummer som inte börjar med `10` eller innehåller fler eller färre än `8` siffror visas ett valideringsfelmeddelande när knappen klickar:

![Mönster för e-postadressvalidering](/help/forms/assets/custom-function-validation-pattern.png)

Nästa steg är nu att skapa en regel för knappen `Next` som validerar fältet `contact` vid knappklicket.

![Valideringsmönster](/help/forms/assets/custom-function-validate.png)

Se bilden nedan för att visa att om användaren anger ett telefonnummer som inte börjar med `10` visas ett felmeddelande på fältnivå:

![Mönster för e-postadressvalidering](/help/forms/assets/custom-function-validate-error-message.png)

Om användaren anger ett giltigt telefonnummer och alla fält på panelen `personaldetails` valideras visas panelen `feedback` på skärmen:

![Mönster för e-postadressvalidering](/help/forms/assets/validate-form-preview-form.png)

+++

+++ **Använd skiftläge**: Återställ en panel

Lägg till följande kod i den anpassade funktionen enligt anvisningarna i avsnittet [create-custom-function](#create-custom-function) för att återställa panelen.

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
> Om inget argument skickas i funktionen `reset()` valideras formuläret.

I det här exemplet återställs panelen `personaldetails` när du klickar på knappen `Clear`. Nästa steg är att skapa en regel för knappen `Clear` som återställer panelen när du klickar på knappen.

![Knappen Rensa](/help/forms/assets/custom-function-reset-field.png)

Se bilden nedan för att visa att panelen `personaldetails` återställs om användaren klickar på knappen `clear`:

![Återställ formulär](/help/forms/assets/custom-function-reset-form.png)

+++

+++ **Använd skiftläge**: Om du vill visa ett anpassat meddelande på fältnivå och markera fältet som ogiltigt

Du kan använda funktionen `markFieldAsInvalid()` för att definiera ett fält som ogiltigt och ange ett anpassat felmeddelande på fältnivå. Värdet `fieldIdentifier` kan vara `fieldId`, `field qualifiedName` eller `field dataRef`. Värdet för objektet `option` kan vara `{useId: true}`, `{useQualifiedName: true}` eller `{useDataRef: true}`.
Syntaxerna som används för att markera ett fält som ogiltigt och ange ett anpassat meddelande är:

* `globals.functions.markFieldAsInvalid(field.$id,"[custom message]",{useId: true});`
* `globals.functions.markFieldAsInvalid(field.$qualifiedName, "[custom message]", {useQualifiedName: true});`
* `globals.functions.markFieldAsInvalid(field.$dataRef, "[custom message]", {useDataRef: true});`

Lägg till följande kod i den anpassade funktionen enligt beskrivningen i avsnittet [create-custom-function](#create-custom-function) för att aktivera ett anpassat meddelande på fältnivå.

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

Nästa steg är att skapa en regel för fältet `comments`:

![Markera fältet som ogiltigt](/help/forms/assets/custom-function-invalid-field.png)

Se demonstrationen nedan för att visa att om du anger negativ feedback i fältet `comments` utlöses visningen av ett anpassat meddelande på fältnivå:

![Markera fältet som ogiltigt förhandsgranskningsformulär](/help/forms/assets/custom-function-invalidfield-form.png)

Om användaren skriver in mer än 15 tecken i textrutan för kommentarer valideras fältet och formuläret skickas:

![Markera fältet som ett giltigt förhandsgranskningsformulär](/help/forms/assets/custom-function-validfield-form.png)

+++

+++ **Använd skiftläge**: Skicka ändrade data till servern

Följande kodrad:
`globals.functions.submitForm(globals.functions.exportData(), false);` används för att skicka formulärdata efter manipulering.
* Det första argumentet är de data som ska skickas.
* Det andra argumentet anger om formuläret ska valideras innan det skickas in. Det är `optional` och inställt som `true` som standard.
* Det tredje argumentet är `contentType` i överföringen, som också är valfritt med standardvärdet som `multipart/form-data`. De andra värdena kan vara `application/json` och `application/x-www-form-urlencoded`.

Lägg till följande kod i den anpassade funktionen enligt beskrivningen i avsnittet [create-custom-function](#create-custom-function) för att skicka manipulerade data till servern:

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

I det här exemplet skickas `NA` till servern när formuläret skickas om användaren lämnar textrutan `comments` tom.

Skapa nu en regel för knappen `Submit` som skickar data:

![Skicka data](/help/forms/assets/custom-function-submit-data.png)

Titta på bilden för `console window` nedan för att visa att om användaren lämnar textrutan `comments` tom så skickas värdet som `NA` på servern:

![Skicka data i konsolfönstret](/help/forms/assets/custom-function-submit-data-form.png)

Du kan även kontrollera konsolfönstret för att visa data som skickats till servern:

![Inspect-data i konsolfönstret](/help/forms/assets/custom-function-submit-data-console-data.png)

+++

+++ **Använd skiftläge**: Åsidosätt formulärskickning och felhanterare

Lägg till följande kodrad enligt beskrivningen i avsnittet [create-custom-function](#create-custom-function) för att anpassa överförings- eller felmeddelandet för formulärinskickning och visa formulärinskickningsmeddelandena i en modal ruta:

```javascript
/**
 * Handles the success response after a form submission.
 *
 * @param {scope} globals - This object contains a read-only form instance, target field instance, triggered event, and methods for performing form modifications within custom functions.
 * @returns {void}
 */
function customSubmitSuccessHandler(globals) {
    var event = globals.event;
    var submitSuccessResponse = event.payload.body;
    var form = globals.form;

    if (submitSuccessResponse) {
        if (submitSuccessResponse.redirectUrl) {
            window.location.href = encodeURI(submitSuccessResponse.redirectUrl);
        } else if (submitSuccessResponse.thankYouMessage) {
            showModal("success", submitSuccessResponse.thankYouMessage);
        }
    }
}

/**
 * Handles the error response after a form submission.
 *
 * @param {string} customSubmitErrorMessage - The custom error message.
 * @param {scope} globals - This object contains a read-only form instance, target field instance, triggered event, and methods for performing form modifications within custom functions.
 * @returns {void}
 */
function customSubmitErrorHandler(customSubmitErrorMessage, globals) {
    showModal("error", customSubmitErrorMessage);
}
function showModal(type, message) {
    // Remove any existing modals
    var existingModal = document.getElementById("modal");
    if (existingModal) {
        existingModal.remove();
    }

    // Create the modal dialog
    var modal = document.createElement("div");
    modal.setAttribute("id", "modal");
    modal.setAttribute("class", "modal");

    // Create the modal content
    var modalContent = document.createElement("div");
    modalContent.setAttribute("class", "modal-content");

    // Create the modal header
    var modalHeader = document.createElement("div");
    modalHeader.setAttribute("class", "modal-header");
    modalHeader.innerHTML = "<h2>" + (type === "success" ? "Thank You" : "Error") + "</h2>";

    // Create the modal body
    var modalBody = document.createElement("div");
    modalBody.setAttribute("class", "modal-body");
    modalBody.innerHTML = "<p class='" + type + "-message'>" + message + "</p>";

    // Create the modal footer
    var modalFooter = document.createElement("div");
    modalFooter.setAttribute("class", "modal-footer");

    // Create the close button
    var closeButton = document.createElement("button");
    closeButton.setAttribute("class", "close-button");
    closeButton.innerHTML = "Close";
    closeButton.onclick = function() {
        modal.remove();
    };

    // Append the elements to the modal content
    modalFooter.appendChild(closeButton);
    modalContent.appendChild(modalHeader);
    modalContent.appendChild(modalBody);
    modalContent.appendChild(modalFooter);

    // Append the modal content to the modal
    modal.appendChild(modalContent);

    // Append the modal to the document body
    document.body.appendChild(modal);
}
```

I det här exemplet, när användaren använder de anpassade funktionerna `customSubmitSuccessHandler` och `customSubmitErrorHandler`, visas meddelanden om lyckade och misslyckade åtgärder i ett modalt format. JavaScript-funktionen `showModal(type, message)` används för att dynamiskt skapa och visa en modal dialogruta på en skärm.

Skapa nu en regel för att skicka in formulär:

![Formuläröverföringen lyckades](/help/forms/assets/form-submission-success.png)

Se bilden nedan för att visa att när formuläret har skickats visas meddelandet om att det lyckades visas i ett modalt format:

![Meddelande om att formuläret har skickats in](/help/forms/assets/form-submission-success-message.png)

På samma sätt kan vi skapa en regel för misslyckade formulärinskickade formulär:

![Det går inte att skicka formulär](/help/forms/assets/form-submission-fail.png)

Se bilden nedan för att visa att felmeddelandet visas i ett modalt format när formuläröverföringen misslyckas:

![Misslyckat meddelande om att skicka formulär](/help/forms/assets/form-submission-fail-message.png)

Funktionerna `Default submit Form Success Handler` och `Default submit Form Error Handler` är tillgängliga i paketet om du vill visa om formuläret har skickats in eller misslyckats på ett standardsätt.

Om den anpassade överföringshanteraren inte fungerar som förväntat i befintliga AEM projekt eller formulär, se avsnittet [felsökning](#troubleshooting).

+++

+++ **Använd skiftläge**: Utför åtgärder i en specifik instans av den repeterbara panelen

Regler som skapas med den visuella regelredigeraren på en repeterbar panel tillämpas på den sista instansen av den repeterbara panelen. Om du vill skriva en regel för en viss instans av den repeterbara panelen kan vi använda en anpassad funktion.

Låt oss skapa ett annat formulär för att samla in information om resenärer som är på väg till en destination. En resande panel läggs till som en upprepningsbar panel, där användaren kan lägga till information för 5 resenärer med knappen `Add Traveler`.

![Resenärinformation](/help/forms/assets/traveler-info-form.png)

Lägg till följande kodrad enligt beskrivningen i avsnittet [create-custom-function](#create-custom-function) för att utföra åtgärder i en specifik instans av den repeterbara panelen, förutom den sista:

```javascript
/**
* @name hidePanelInRepeatablePanel
* @param {scope} globals
*/
function hidePanelInRepeatablePanel(globals)
{    
    var repeatablePanel = globals.form.travelerinfo;
    // hides a panel inside second instance of repeatable panel
    globals.functions.setProperty(repeatablePanel[1].traveler, {visible : false});
}  
```

I det här exemplet utför den anpassade funktionen `hidePanelInRepeatablePanel` en åtgärd i en specifik instans av den repeterbara panelen. I ovanstående kod representerar `travelerinfo` den repeterbara panelen. Koden `repeatablePanel[1].traveler, {visible: false}` döljer panelen i den andra instansen av den repeterbara panelen.

Låt oss lägga till en knapp med etiketten `Hide` och lägga till en regel som döljer den andra instansen av en repeterbar panel.

![Dölj panelregel](/help/forms/assets/custom-function-hidepanel-rule.png)

Titta på videon nedan för att visa att panelen i den andra upprepningsbara instansen döljs när användaren klickar på `Hide`:

>[!VIDEO](https://video.tv.adobe.com/v/3429554?quality=12&learn=on)

+++

+++ **Använd**: Fyll i fältet i förväg med ett värde när formuläret läses in

Lägg till följande kodrad, enligt beskrivningen i avsnittet [create-custom-function](#create-custom-function) , för att läsa in det förfyllda värdet i ett fält när formuläret initieras:

```javascript
/**
 * Tests import data
 * @name testImportData
 * @param {scope} globals
 */
function testImportData(globals)
{
    globals.functions.importData(Object.fromEntries([['amount','10000']]));
} 
```

I ovanstående kod fyller funktionen `testImportData` i förväg i textrutefältet `Booking Amount` när formuläret läses in. Låt oss anta att bokningsformuläret kräver att det minsta bokningsbeloppet är `10,000`.

Låt oss skapa en regel vid formulärinitiering, där värdet i textrutefältet `Booking Amount` är förifyllt med ett angivet värde när formuläret läses in:

![Importera dataregel](/help/forms/assets/custom-function-import-data.png)

Titta på skärmbilden nedan som visar att när formuläret läses in är värdet i textrutan `Booking Amount` förifyllt med ett angivet värde:

![Importera dataregelformulär](/help/forms/assets/custom-function-prefill-form.png)

+++

+++ **Använd**: Ange fokus på det specifika fältet

Lägg till följande kodrad, enligt beskrivningen i avsnittet [create-custom-function](#create-custom-function) , för att ange fokus på det angivna fältet när användaren klickar på knappen `Submit`:

```javascript
/**
 * @name testSetFocus
 * @param {object} emailField
 * @param {scope} globals
 */
    function testSetFocus(field, globals)
    {
        globals.functions.setFocus(field);
    }
```

Låt oss lägga till en regel till knappen `Submit` för att ställa in fokus på fältet `Email ID` när någon klickar på det:

![Ange fokusregel](/help/forms/assets/custom-function-set-focus.png)

Titta på skärmbilden nedan som visar att när användaren klickar på knappen `Submit` ställs fokus in på fältet `Email ID`:

![Ange fokusregel](/help/forms/assets/custom-function-set-focus-form.png)

>[!NOTE]
>
> Du kan använda den valfria parametern `$focusOption` om du vill fokusera på nästa eller föregående fält i förhållande till fältet `email`.

+++

+++ **Använd**: Lägg till eller ta bort upprepningsbar panel med egenskapen `dispatchEvent`

Lägg till följande kodrad, enligt beskrivningen i avsnittet [create-custom-function](#create-custom-function) , för att lägga till en panel när användaren klickar på knappen `Add Traveler` med egenskapen `dispatchEvent` :

```javascript
/**
 * Tests add instance with dispatchEvent
 * @name testAddInstance
 * @param {scope} globals
 */
function testAddInstance(globals)
{
    var repeatablePanel = globals.form.traveler;
    globals.functions.dispatchEvent(repeatablePanel,'addInstance');
}
```

Låt oss lägga till en regel till knappen `Add Traveler` för att lägga till den repeterbara panelen när någon klickar på den:

![Lägg till panelregel](/help/forms/assets/custom-function-add-panel.png)

Se gif nedan som visar att panelen läggs till med egenskapen `dispatchEvent` när användaren klickar på knappen `Add Traveler`:

![Lägg till panel](/help/forms/assets/custom-function-add-panel.gif)

Lägg på samma sätt till följande kodrad, enligt beskrivningen i avsnittet [create-custom-function](#create-custom-function) , för att ta bort en panel när användaren klickar på knappen `Delete Traveler` med egenskapen `dispatchEvent` :

```javascript
/**
 
 * @name testRemoveInstance
 * @param {scope} globals
 */
function testRemoveInstance(globals)
{
    var repeatablePanel = globals.form.traveler;
    globals.functions.dispatchEvent(repeatablePanel, 'removeInstance');
} 
```

Låt oss lägga till en regel till knappen `Delete Traveler` för att ta bort den repeterbara panelen när någon klickar på den:

![Ta bort panelregel](/help/forms/assets/custom-function-delete-panel.png)

Se gif nedan som visar att när användaren klickar på knappen `Delete Traveler` tas den resande panelen bort med egenskapen `dispatchEvent`:

![Ta bort panel](/help/forms/assets/custom-function-delete-panel.gif)

+++

## Cachelagringsstöd för anpassad funktion

Adaptiv Forms implementerar cachning för anpassade funktioner för att förbättra svarstiden samtidigt som den anpassade funktionslistan hämtas i regelredigeraren. Ett meddelande som `Fetched following custom functions list from cache` visas i filen `error.log`.

![anpassad funktion med cachestöd](/help/forms/assets/custom-function-cache-error.png)

Om de anpassade funktionerna ändras blir cachningen ogiltig och den tolkas.

## Felsökning {#troubleshooting}

* Utför följande steg om den anpassade överföringshanteraren inte fungerar som förväntat i befintliga AEM projekt eller formulär:
   * Kontrollera att kärnkomponentversionen för [är uppdaterad till 3.0.18 och senare](https://github.com/adobe/aem-core-forms-components). För befintliga AEM och formulär finns det dock ytterligare steg att utföra:

   * För det AEM projektet bör användaren ersätta alla instanser av `submitForm('custom:submitSuccess', 'custom:submitError')` med `submitForm()` och distribuera projektet via Cloud Manager pipeline.

   * Om de anpassade överföringshanterarna inte fungerar som de ska i befintliga formulär måste användaren öppna och spara regeln `submitForm` på knappen **Skicka** med regelredigeraren. Den här åtgärden ersätter den befintliga regeln från `submitForm('custom:submitSuccess', 'custom:submitError')` med `submitForm()` i formuläret.


* Om det uppstår ett fel i JavaScript-filen som innehåller kod för anpassade funktioner visas inte de anpassade funktionerna i regelredigeraren i ett anpassat formulär. Om du vill kontrollera listan med anpassade funktioner kan du navigera till filen `error.log` för felet. Om ett fel uppstår visas listan med anpassade funktioner tom:

  ![felloggfil](/help/forms/assets/custom-function-list-error-file.png)

  Om det inte finns något fel hämtas den anpassade funktionen och visas i filen `error.log`. Ett meddelande som `Fetched following custom functions list` visas i filen `error.log`:

  ![felloggfil med rätt anpassad funktion](/help/forms/assets/custom-function-list-fetched-in-error.png)

## Överväganden

* `parameter type` och `return type` stöder inte `None`.

* De funktioner som inte stöds i den anpassade funktionslistan är:
   * Generatorfunktioner
   * Async-/Await-funktioner
   * Metoddefinitioner
   * Klassmetoder
   * Standardparametrar
   * Restparametrar

## Se även {#see-also}

{{see-also}}



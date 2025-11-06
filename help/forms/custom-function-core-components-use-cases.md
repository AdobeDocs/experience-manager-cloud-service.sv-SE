---
title: I den här artikeln beskrivs olika användningsfall för en anpassad funktion i ett adaptivt formulär baserat på kärnkomponenter.
description: Artikeln beskriver olika användningsfall för en anpassad funktion i ett adaptivt formulär baserat på kärnkomponenter. Anpassade funktioner används i regelredigeraren för att skapa anpassade regler för formuläret.
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner, Intermediate
exl-id: df92b91e-f3b0-4a08-bd40-e99edc9a50a5
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '2184'
ht-degree: 0%

---

# Exempel på utveckling och användning av anpassade funktioner

Artikeln innehåller detaljerade exempel på anpassade funktioner för ett adaptivt formulär baserat på kärnkomponenter, och ger värdefulla insikter om hur de kan implementeras i olika scenarier. Anpassade funktioner används i regelredigeraren för en AEM Forms, vilket gör att utvecklare kan definiera och styra logiken som styr formulärbeteendet.
I den här artikeln beskrivs olika implementeringar av anpassade funktioner, och den visar hur de kan användas för att skräddarsy formulär för att uppfylla specifika krav och förbättra den övergripande funktionaliteten.

## Fylla i alternativen i listrutan med anpassade funktioner

Regelredigeraren i kärnkomponenterna stöder inte egenskapen **Set Options** för att fylla i listrutealternativ dynamiskt vid körning. Du kan dock fylla i alternativ för listrutor med anpassade funktioner, som gör att du kan hämta alternativ baserat på en viss logik. Anpassade funktioner ger större flexibilitet och kontroll över hur och när listrutorna fylls i, vilket förbättrar användarupplevelsen.

Om du vill fylla i alternativen i listrutan med en anpassad funktion lägger du till följande kod enligt beskrivningen i avsnittet [create-custom-function](/help/forms/custom-function-core-component-create-function.md) :


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

## Visa en panel med regeln `SetProperty`

Låt oss lära oss hur anpassade funktioner använder fält och globala objekt med hjälp av ett `Contact Us`-formulär.

![Kontakta oss ](/help/forms/assets/contact-us-form.png)

Lägg till följande kod i den anpassade funktionen enligt beskrivningen i avsnittet [create-custom-function](/help/forms/custom-function-core-component-create-function.md) för att ange formulärfältet som `Required`.

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

## Validera fältet

Låt oss lära oss hur anpassade funktioner använder fält och globala objekt för att validera fältet med hjälp av ett `Contact Us`-formulär.

Lägg till följande kod i den anpassade funktionen enligt anvisningarna i avsnittet [create-custom-function](/help/forms/custom-function-core-component-create-function.md) för att validera fältet.

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

## Återställ en panel

Låt oss lära oss hur anpassade funktioner använder fält och globala objekt för att återställa fältet med hjälp av ett `Contact Us`-formulär.

Lägg till följande kod i den anpassade funktionen enligt anvisningarna i avsnittet [create-custom-function](/help/forms/custom-function-core-component-create-function.md) för att återställa panelen.

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

Se bilden nedan för att visa att panelen `clear` återställs om användaren klickar på knappen `personaldetails`:

![Återställ formulär](/help/forms/assets/custom-function-reset-form.png)

## Visa ett anpassat meddelande på fältnivå och markera fältet som ogiltigt

Låt oss lära oss hur anpassade funktioner använder fält och globala objekt för att visa ett anpassat meddelande på fältnivå och markera fältet som ogiltigt med hjälp av ett `Contact Us`-formulär.

Du kan använda funktionen `markFieldAsInvalid()` för att definiera ett fält som ogiltigt och ange ett anpassat felmeddelande på fältnivå. Värdet `fieldIdentifier` kan vara `fieldId`, `field qualifiedName` eller `field dataRef`. Värdet för objektet `option` kan vara `{useId: true}`, `{useQualifiedName: true}` eller `{useDataRef: true}`.
Syntaxerna som används för att markera ett fält som ogiltigt och ange ett anpassat meddelande är:

* `globals.functions.markFieldAsInvalid(field.$id,"[custom message]",{useId: true});`
* `globals.functions.markFieldAsInvalid(field.$qualifiedName, "[custom message]", {useQualifiedName: true});`
* `globals.functions.markFieldAsInvalid(field.$dataRef, "[custom message]", {useDataRef: true});`

Lägg till följande kod i den anpassade funktionen enligt beskrivningen i avsnittet [create-custom-function](/help/forms/custom-function-core-component-create-function.md) för att aktivera ett anpassat meddelande på fältnivå.

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

## Skicka ändrade data till servern

Låt oss lära oss hur anpassade funktioner använder fält och globala objekt för att skicka manipulerade data på servern med hjälp av ett `Contact Us`-formulär.

Följande kodrad:
`globals.functions.submitForm(globals.functions.exportData(), false);` används för att skicka formulärdata efter manipulering.

* Det första argumentet är de data som ska skickas.
* Det andra argumentet anger om formuläret ska valideras innan det skickas in. Det är `optional` och inställt som `true` som standard.
* Det tredje argumentet är `contentType` i överföringen, som också är valfritt med standardvärdet som `multipart/form-data`. De andra värdena kan vara `application/json` och `application/x-www-form-urlencoded`.

Lägg till följande kod i den anpassade funktionen enligt beskrivningen i avsnittet [create-custom-function](/help/forms/custom-function-core-component-create-function.md) för att skicka manipulerade data till servern:

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

I det här exemplet skickas `comments` till servern när formuläret skickas om användaren lämnar textrutan `NA` tom.

Skapa nu en regel för knappen `Submit` som skickar data:

![Skicka data](/help/forms/assets/custom-function-submit-data.png)

Titta på bilden för `console window` nedan för att visa att om användaren lämnar textrutan `comments` tom så skickas värdet som `NA` på servern:

![Skicka data i konsolfönstret](/help/forms/assets/custom-function-submit-data-form.png)

Du kan även kontrollera konsolfönstret för att visa data som skickats till servern:

![Inspektera data i konsolfönstret](/help/forms/assets/custom-function-submit-data-console-data.png)

## Åsidosätt formulärskickning och felhantering

Låt oss lära oss hur anpassade funktioner använder fält och globala objekt för att åsidosätta inskickningshanterare med hjälp av ett `Contact Us`-formulär.

Lägg till följande kodrad enligt anvisningarna i avsnittet [create-custom-functions](/help/forms/custom-function-core-component-create-function.md) för att anpassa överförings- eller felmeddelandet för formulärinskickning och visa formulärinskickningsmeddelandena i en modal ruta:

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

Om den anpassade överföringshanteraren inte fungerar som förväntat i befintliga AEM-projekt eller formulär, se avsnittet [felsökning](#troubleshooting).

## Utför åtgärder i en specifik instans av den repeterbara panelen

Regler som skapas med den visuella regelredigeraren på en repeterbar panel tillämpas på den sista instansen av den repeterbara panelen. Om du vill skriva en regel för en viss instans av den repeterbara panelen kan vi använda en anpassad funktion.

Låt oss skapa ett annat formulär som `Booking Form` för att samla in information om resenärer som är på väg till en destination. En resande panel läggs till som en upprepningsbar panel, där användaren kan lägga till information för 5 resenärer med knappen `Add Traveler`.

![Resenärinformation](/help/forms/assets/traveler-info-form.png)

Lägg till följande kodrad enligt beskrivningen i avsnittet [create-custom-function](/help/forms/custom-function-core-component-create-function.md) för att utföra åtgärder i en specifik instans av den repeterbara panelen, förutom den sista:

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

## Fyll i fältet i förväg med ett värde när formuläret läses in

Låt oss lära oss hur anpassade funktioner använder fält och globala objekt för att förifylla fält med hjälp av en `Booking Form`.

Lägg till följande kodrad, enligt beskrivningen i avsnittet [create-custom-function](/help/forms/custom-function-core-component-create-function.md) , för att läsa in det förfyllda värdet i ett fält när formuläret initieras:

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

## Sätt fokus på det specifika fältet

Låt oss lära oss hur anpassade funktioner använder fält och globala objekt för att sätta fokus på specifika fält med hjälp av en `Booking Form`.

Lägg till följande kodrad, enligt beskrivningen i avsnittet [create-custom-function](/help/forms/custom-function-core-component-create-function.md) , för att ange fokus på det angivna fältet när användaren klickar på knappen `Submit`:

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

## Lägg till eller ta bort upprepningsbar panel med egenskapen `dispatchEvent`

Låt oss lära oss hur anpassade funktioner använder fält och globala objekt för att lägga till eller ta bort repeterbara paneler med egenskapen `dispatchEvent` med hjälp av en `Booking Form`.

Lägg till följande kodrad, enligt beskrivningen i avsnittet [create-custom-function](/help/forms/custom-function-core-component-create-function.md) , för att lägga till en panel när användaren klickar på knappen `Add Traveler` med egenskapen `dispatchEvent` :

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

Se gif nedan som visar att panelen läggs till med egenskapen `Add Traveler` när användaren klickar på knappen `dispatchEvent`:

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

## Känt fel

* Anpassade funktioner stöder inte JavaScript reguljära uttryckslitteraler. Om du använder regex-litteraler i en anpassad funktion uppstår fel under körningen. Till exempel:
  `const pattern = /^abc$/;`

  För att säkerställa kompatibilitet använder du RegExp-konstruktorn i de anpassade funktionerna.

  `const pattern = new RegExp("^abc$");`
Använd reguljära uttryck för att använda RegExp-konstruktorn för att säkerställa en konsekvent och tillförlitlig exekvering.

## Felsökning

* Utför följande steg om den anpassade överföringshanteraren inte fungerar som förväntat i befintliga AEM-projekt eller formulär:
   * Kontrollera att kärnkomponentversionen för [är uppdaterad till 3.0.18 och senare](https://github.com/adobe/aem-core-forms-components). För befintliga AEM-projekt och -formulär finns det dock ytterligare steg att utföra:

   * För AEM-projektet bör användaren ersätta alla instanser av `submitForm('custom:submitSuccess', 'custom:submitError')` med `submitForm()` och distribuera projektet via Cloud Manager pipeline.

   * Om de anpassade överföringshanterarna inte fungerar som de ska i befintliga formulär måste användaren öppna och spara regeln `submitForm` på knappen **Skicka** med regelredigeraren. Den här åtgärden ersätter den befintliga regeln från `submitForm('custom:submitSuccess', 'custom:submitError')` med `submitForm()` i formuläret.

## Se även

{{see-also-rule-editor}}

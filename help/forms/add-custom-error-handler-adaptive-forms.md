---
title: Lägg till en anpassad felhanterare i Adaptive Forms för AEM Adaptive Forms
seo-title: Error Handlers in Adaptive Forms for AEM Adaptive Forms
description: AEM Forms har körklara hanterare och felhanterare för ett formulär som använder REST-slutpunkten som konfigurerats för att anropa en extern tjänst. Du kan lägga till en standardfelhanterare samt en anpassad felhanterare i en AEM anpassad form.
seo-description: Error handler function and Rule Editor in Adaptive Forms helps you to effectively manage and customize error handling. You can add a default error handler as well as custom error handler in an AEM Adaptive Form.
keywords: Lägg till en anpassad felhanterare, lägg till en standardfelhanterare, lägg till en felhanterare i formuläret, använd regelredigerarens anropstjänst för att lägga till en anpassad felhanterare, konfigurera regelredigeraren för att lägga till en anpassad felhanterare, lägg till en anpassad felhanterare med regelredigeraren
contentOwner: Ruchita Srivastav
content-type: reference
feature: Adaptive Forms
source-git-commit: 09ed1ae61e7748da2cc182b005a9dd26853cb3f7
workflow-type: tm+mt
source-wordcount: '1962'
ht-degree: 0%

---

# Felhanterare i adaptiv Forms {#error-handlers-in-adaptive-form}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/standard-validation-error-messages-adaptive-forms.html) |
| AEM as a Cloud Service | Den här artikeln |

AEM Forms har färdiga funktioner och felhanterare för att skicka in formulär. Den innehåller även funktioner för att anpassa felhanterarfunktioner. Du kan till exempel anropa ett anpassat arbetsflöde i serverdelen för specifika felkoder eller informera kunden om att tjänsten inte fungerar. Hanterare är funktioner på klientsidan som körs baserat på serversvaret. När en extern tjänst anropas med API:er överförs data till servern för validering, som returnerar ett svar till klienten med information om lyckad eller felhändelse för överföringen. Informationen skickas som parametrar till den relevanta hanteraren för att köra funktionen. En felhanterare hjälper till att hantera och visa fel eller valideringsproblem som påträffats.

![felhanterararbetsflöde för att förstå hur du lägger till anpassad felhanterare i formulär](/help/forms/assets/error-handler-workflow.png)

Det adaptiva formuläret validerar de indata du anger i fält baserat på förinställda valideringskriterier och söker efter olika fel som returneras av REST-slutpunkten som konfigurerats för att anropa en extern tjänst. Du kan ange valideringskriterier baserat på den datakälla som du använder med det adaptiva formuläret. Om du till exempel använder RESTful-webbtjänster som datakälla kan du definiera valideringskriterierna i en Swagger-definitionsfil.

Om indatavärdena uppfyller valideringskriterierna skickas värdena till datakällan i annat fall visas ett felmeddelande i Adaptiv form med hjälp av en felhanterare. På samma sätt som detta arbetssätt integreras Adaptive Forms med anpassade felhanterare för datavalidering. Om indatavärdena inte uppfyller valideringskriterierna visas felmeddelandena på fältnivå i det adaptiva formuläret. Detta inträffar när det valideringsfelmeddelande som returneras av servern har standardmeddelandeformatet.


## Användning av felhanterare {#uses-of-error-handler}

Felhanterare används för olika syften. Några av användningsområdena för felhanterarfunktioner visas nedan:
* **Utför validering**: Felhanteringen börjar med att validera användarindata mot fördefinierade regler eller villkor. När användarna fyller i ett adaptivt formulär validerar felhanteraren indata så att det uppfyller det format, den längd eller andra begränsningar som krävs.

* **Ge feedback i realtid**: När ett fel upptäcks visar felhanteraren direkt feedback till användaren, t.ex. textbundna felmeddelanden under motsvarande formulärfält. Denna feedback hjälper användarna att identifiera och åtgärda fel utan att behöva skicka in formuläret och vänta på ett svar.


* **Visa felmeddelanden**: När en sändning med adaptiva formulär stöter på ett valideringsfel visas ett felmeddelande i felhanteraren. Felmeddelandena ska vara tydliga, koncisa och markera de specifika fält som behöver åtgärdas.

* **Markerar det felaktiga fältet**: För att dra användarens uppmärksamhet till specifika felaktiga fält markeras eller visas motsvarande fält. Den utförs genom att ändra bakgrundsfärgen, lägga till en ikon eller kantlinje eller någon annan visuell indikator som hjälper användarna att snabbt hitta och åtgärda felen.


## Fel-/felsvarsformat {#failure-response-format}

I ett adaptivt formulär visas felen på fältnivå om servervalideringsfelmeddelanden är i följande standardformat.
Koden nedan visar den befintliga strukturen för felsvar:

```javascript
   {
    errorCausedBy : "SERVER_SIDE_VALIDATION/SERVICE_INVOCATION_FAILURE"
    errors : [
        {
             somExpression  : <somexpr>
             errorMessage / errorMessages : <validationMsg> / [<validationMsg>, <validationMsg>]
        }
    ]
    originCode : <target error Code>
    originMessage : <unstructured error message returned by service>
}
```


Var:

* `errorCausedBy` beskriver orsaken till felet.
* `errors` Ange SOM-uttrycket för de fält som underkändes i valideringskriterierna tillsammans med valideringsfelmeddelandet.
* `originCode` fält som lagts till av AEM och innehåller http-statuskoden som returneras av den externa tjänsten.
* `originMessage` fält som lagts till av AEM och innehåller rådata som returnerats av den externa tjänsten.

Med förbättringarna i funktioner och efterföljande uppdateringar i AEM Forms-versionerna har den befintliga felsvarsstrukturen ändrats till ett nytt format baserat på RFC7807, som är bakåtkompatibel med den befintliga felsvarsstrukturen:

```javascript
    {
        "type": "SERVER_SIDE_VALIDATION/FORM_SUBMISSION/SERVICE_INVOCATION/FAILURE/VALIDATION_ERROR", (required)
        "title": "Server side validation failed/Third party service invocation failed", (optional)
        "detail": "", (optional)
        "instance": "", (optional)
        "validationErrors" : [ (required)
            {
                "fieldName":"<SOM expression of the field whose data sent is invalid>",
                "dataRef":<JSONPath (or XPath) of the data element which is invalid>
                "details": ["Error Message(s) for the field"] (required)
    
            }
        ],
        "originCode": <Origin http status code>, (optional - in case of SERVER_SIDE_VALIDATION)
        "originMessage" : "<unstructured error message returned by service>" (optional - in case of SERVER_SIDE_VALIDATION)
    }
```


>[!NOTE]
>
> * Kontrollera att felsvarsstrukturen innehåller antingen **fieldName** eller **dataRef**.
> * Se till att **ContentType** header is **application/problem+json**.

Var:
* `type (required)` anger feltypen. Det kan vara något av följande värden:
   * `SERVER_SIDE_VALIDATION` indikerar ett fel på grund av validering på serversidan.
   * `FORM_SUBMISSION` anger ett fel när formulär skickas
   * `SERVICE_INVOCATION` indikerar ett fel under ett anrop till en tjänst från tredje part.
   * `FAILURE` anger ett allmänt fel.
   * `VALIDATION_ERROR` indikerar ett fel på grund av ett valideringsfel.

* `title (optional)` innehåller en titel eller kort beskrivning av felet.
* `detail (optional)` innehåller ytterligare information om felet om det behövs.
* `instance (optional)` representerar en instans eller identifierare som är associerad med felet och hjälper till att spåra eller identifiera den specifika förekomsten av felet.
* `validationErrors (required)` innehåller information om valideringsfel. Den innehåller följande fält:
   * `fieldname` omnämns SOM-uttrycket för de fält som underkändes i valideringskriterierna.
   * `dataRef` representerar JSON-sökvägen eller XPath för de fält som underkändes vid valideringen.
   * `details` innehåller valideringsfelmeddelandet med det felaktiga fältet.
* `originCode (optional)` fält som lagts till av AEM och innehåller http-statuskoden som returneras av den externa tjänsten
* `originMessage (optional)` fält som lagts till av AEM och innehåller rådata som returnerats av den externa tjänsten.

### Exempel på felsvarsformat {#sample-error-response-format}

Vissa av alternativen för att visa felsvaren är:

+++  Baserat på egenskapen Adaptive Form fieldName


* **`Header:`** `content-type:application/problem+json`
* **`Response:`**

      &quot;javascript
      {
      &quot;type&quot;: &quot;VALIDATION_ERROR&quot;,
      &quot;validationErrors&quot;: [
      {
      &quot;fieldName&quot;: &quot;guide[0].guide1[0].guideRootPanel[0].textbox1686647736683[0]&quot;,
      &quot;dataRef&quot;: &quot;&quot;,
      &quot;details&quot;: [
      &quot;Ett ogiltigt ID har angetts. Angivet värde är inte korrekt!&quot;
      ]
      }
      ]}
      &quot;
  
  Du kan visa SOM-uttrycket för vilket fält som helst i ett adaptivt formulär genom att trycka på fältet och välja **[!UICONTROL View SOM Expression]**.

  ![Som uttryck för ett adaptivt formulärfält för att visa felsvar i en anpassad felhanterare](/help/forms/assets/custom-error-handler-somexpression.png)

+++


+++ Baserat på egenskapen dataRef för adaptiv form

* **`Header:`** `content-type:application/problem+json`
* **`Response:`**

  ```javascript
  {
      "type": "VALIDATION_ERROR",
      "validationErrors": [
      {
          "fieldName": "",
          "dataRef": "/Pet/id",
          "details": [
          "Invalid ID supplied. Provided value is not correct!"
          ]
          }
  ]}
  ```

  ![Datareferens för ett adaptivt formulärfält som visar felsvar i en anpassad felhanterare](/help/forms/assets/custom-errorhandler-dataref.png)

Du kan visa värdet för dataRef i **[!UICONTROL Properties]** -fönstret för en formulärkomponent.

+++


## Lägg till felhanterare med Regelredigeraren {#add-error-handler-using-rule-editor}

Använda [Regelredigerarens anropstjänst](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/rule-editor.html?lang=en#invoke) definierar du valideringskriterierna baserat på den datakälla som du använder med det adaptiva formuläret. Om du använder RESTful-webbtjänster som datakälla kan du definiera valideringskriterierna i en Swagger-definitionsfil. Genom att använda felhanteringsfunktionerna och regelredigeraren i Adaptive Forms kan du effektivt hantera och anpassa felhanteringen. Du definierar villkoren med Regelredigeraren och konfigurerar de åtgärder som ska utföras när regeln aktiveras. Adaptiv form validerar indata som du anger i fält baserat på förinställda valideringskriterier. Om indatavärdena inte uppfyller valideringskriterierna visas felmeddelandena på fältnivån i ett adaptivt formulär.

>[!NOTE]
>
> * Konfigurera Adaptiv Forms med en formulärdatamodell om du vill använda felhanterare med åtgärden Invoke i regelredigeraren.
> * En standardfelhanterare tillhandahålls som standard för att visa felmeddelanden i fält om felsvaret finns i standardschemat. Standardfelhanteraren kan även anropa den anpassade felhanteraren om felsvaret inte överensstämmer med standardschemat.

<!-- 
Using Rule Editor, you can:
* [Add default error handler function](#add-default-errror-handler)
* [Add custom error handler function](#add-custom-errror-handler)


### Add default error handler function {#add-default-errror-handler}

A default error handler is supported by default to display error messages on fields if the error response is in standard schema or in server-side validation failure. 
To understand how to use a default error handler using the [Rule Editor's Invoke Service](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/rule-editor.html?lang=en#invoke) action, take an example of a simple Adaptive Form with two fields, **Pet ID** and **Pet Name** and use a default error handler at the **Pet ID** field to check for various errors returned by the REST endpoint configured to invoke an external service, for example, `200 - OK`,`404 - Not Found`, `400 - Bad Request`. To add a default error handler using the Rule Editor's Invoke Service action, execute the following steps:

1. Open an Adaptive Form in authoring mode, select a form component and tap **[!UICONTROL Rule Editor]** to open the rule editor.
1. Tap **[!UICONTROL Create]**.
1. Create a condition in the **When** section of the rule. For example, **When[Name of Pet ID field]** is changed. Select is changed from the **Select State** drop-down list.
1. In the **Then** section, select **[!UICONTROL Invoke Service]** from the **Select Action** drop-down list.
1. Select a **Post service** and its corresponding data bindings from the **Input** section. For example, to validate **Pet ID**, select a **Post service** as **GET /pet/{petId}** and select **Pet ID** in the **Input** section.
1. Select the data bindings from the **Output** section. Select **Pet Name** in the **Output** section.
1. Select **[!UICONTROL Default Error Handler]** from the **Error Handler** section. 
1. Click **[!UICONTROL Done]**.

 ![add a default error handler for a field validation checks in a form](/help/forms/assets/default-error-handler.png)

As a result of this rule, the values you enter for **Pet ID** checks validation for **Pet Name** using external service invoked by REST endpoint. If the validation criteria based on the data source fail, the error messages are displayed at the field level.

 ![display the default error message when you add a default error handler in a form to handle error responses](/help/forms/assets/default-error-message.png)

-->

### Lägg till anpassad felhanterarfunktion {#add-custom-errror-handler}

Du kan lägga till en anpassad felhanterarfunktion för att utföra några av åtgärderna:
* hantera felsvar som använder icke-standard- eller standardfelsvar. Observera att dessa felsvar som inte är standard inte följer [standardschema för felsvar](#failure-response-format).
* skicka analyshändelser till alla analysplattformar. Exempel: Adobe Analytics.
* visa modal dialog med felmeddelanden.

Förutom de ovannämnda åtgärderna kan de anpassade felhanterarna användas för att utföra anpassade funktioner som uppfyller specifika användarkrav.

Den anpassade felhanteraren är en funktion (klientbibliotek) som är utformad för att svara på fel som returneras av en extern tjänst och leverera ett anpassat svar till slutanvändarna. Alla klientbibliotek med anteckningar `@errorHandler` betraktas som en anpassad felhanterarfunktion. Den här anteckningen hjälper till att identifiera felhanterarfunktionen som anges i `.js` -fil.
Så här skapar och använder du en anpassad felhanterare med [Regelredigerarens anropstjänst](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/rule-editor.html?lang=en#invoke) åtgärd, låt oss ta ett exempel på Adaptiv form med två fält, **Djurs-ID** och **Djurnamn** och använda en anpassad felhanterare på **Djurs-ID** fält för att kontrollera olika fel som returneras av REST-slutpunkten som konfigurerats för att anropa en extern tjänst, till exempel `200 - OK`,`404 - Not Found`, `400 - Bad Request`.

Så här lägger du till och använder en anpassad felhanterare i ett adaptivt formulär:
1. [Skapa en anpassad felhanterare](#create-custom-error-message)
1. [Använd regelredigeraren för att konfigurera en anpassad felhanterare](#use-custom-error-handler)

#### 1. Skapa en anpassad felhanterare {#create-custom-error-message}

Så här skapar du en anpassad felfunktion:
1. [Klona din AEM Forms as a Cloud Service databas.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#accessing-git).
1. Navigera till `[AEM Forms as a Cloud Service repository folder]/apps/[AEM Project Folder]/clientlibs/`.
1. Skapa en mapp med namnet `js`.
1. Navigera till `[AEM Forms as a Cloud Service repository folder]/apps/[AEM Project Folder]/clientlibs/js` mapp.
1. Lägg till en JavaScript-fil, till exempel `function.js`. Filen innehåller koden för den anpassade felhanteraren.
Låt oss lägga till följande kod i JavaScript-filen för att visa svar och rubriker som tagits emot från REST-tjänstens slutpunkt i webbläsarkonsolen.

       &quot;javascript
       /**
       * Anpassad felhanterare
       * @name customErrorHandler anpassad felhanterarfunktion
       * @errorHandler
       */
       function customErrorHandler(response, headers)
       {
       console.log(&quot;Custom Error Handler processing start...&quot;);
       console.log(&quot;response:&quot;+JSON.stringify(response));
       console.log(&quot;headers:&quot;+JSON.stringify(headers));
       console.log(&quot;Custom Error Handler processing end..&quot;);
       }
       &quot;
   
   <!--  To call the default error handler after the custom error handler, the following line of the sample code is used:
        `guidelib.dataIntegrationUtils.defaultErrorHandler(response, headers) `-->
1. Spara `function.js` -fil.
1. Navigera till `[AEM Forms as a Cloud Service repository folder]/apps/[AEM Project Folder]/clientlibs/js` mapp.
1. Lägg till en textfil som `js.txt`. Filen innehåller:

   ```javascript
       #base=js
       functions.js
   ```

1. Spara `js.txt` -fil.

   >[!NOTE]
   >
   > Om du vill veta mer om hur du skapar anpassade funktioner klickar du på [anpassade funktioner i regelredigeraren](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/add-rules-and-use-expressions-in-an-adaptive-form/rule-editor.html?lang=en#write-rules).

1. Lägg till, implementera och skicka ändringarna i databasen med följande kommandon:

   ```javascript
       git add .
       git commit -a -m "Adding error handling files"
       git push
   ```

1. [Kör pipeline.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#setup-pipeline)

När pipeline har körts blir den anpassade felhanteraren tillgänglig i regelredigeraren för adaptiva formulär. Nu ska vi förstå hur du konfigurerar och använder en anpassad felhanterare med hjälp av regelredigerarens Invoke-tjänst i AEM Forms.

#### 2. Använd regelredigeraren för att konfigurera en anpassad felhanterare {#use-custom-error-handler}

Använda en anpassad felhanterare med **[!UICONTROL Rule Editor's Invoke Service]** åtgärd:

1. Öppna ett adaptivt formulär i redigeringsläge, markera en formulärkomponent och tryck på **[!UICONTROL Rule Editor]** för att öppna regelredigeraren.
1. Tryck på **[!UICONTROL Create]**.
1. Skapa ett villkor i **När** -delen av regeln. Till exempel När **[Namn på Pet ID-fält]** ändras, välj **ändras** från **Välj läge** nedrullningsbar lista.
1. I **Sedan** avsnitt, markera **[!UICONTROL Invoke Service]** från **Välj åtgärd** nedrullningsbar lista.
1. Välj en **Bokför tjänst** och dess motsvarande databindningar från **Indata** -avsnitt. Till exempel för att validera **Djurs-ID** väljer du en **Bokför tjänst** as **GET /husdjur/{petId}** och markera **Djurs-ID** i **Indata** -avsnitt.
1. Välj databindningar i listrutan **Utdata** -avsnitt. Välj till exempel **Djurnamn** i **Utdata** -avsnitt.
1. Välj **[!UICONTROL Custom Error Handler]** från **[!UICONTROL Error Handler]** -avsnitt.
1. Klicka på **[!UICONTROL Done]**.

![lägga till anpassad felhanterare i ett formulär för att hantera felsvar](/help/forms/assets/custom-error-handler.png)


Som ett resultat av den här regeln anger du värden för **Djurs-ID** kontrollerar validering för **Djurnamn** med en extern tjänst som anropas av REST-slutpunkten. Om valideringskriterierna som baseras på datakällan misslyckas, visas felmeddelandena på fältnivå.


![lägga till en anpassad felhanterare i ett formulär för att hantera felsvar](/help/forms/assets/custom-error-handler-message.png)

Öppna webbläsarkonsolen och kontrollera svaret och rubriken som tagits emot från REST-tjänstens slutpunkt för valideringsfelmeddelandet.


Den anpassade felhanterarfunktionen ansvarar för att utföra ytterligare åtgärder, som att visa en modal dialogruta eller skicka en analyshändelse, baserat på felsvaret. En anpassad felhanterarfunktion ger flexibilitet att anpassa felhanteringen efter specifika användarkrav.

<!-- 

## Configure Adaptive Form submission to add custom handlers {#configure-adaptive-form-submission}

If the server validation error message does not display in the standard format, you can enable asynchronous submission and add a custom error handler on Adaptive Form submission to convert the message into a standard format.

### Configure asynchronous Adaptive Form submission {#configure-asynchronous-adaptive-form-submission}

Before adding custom handler, you must configure the adaptive form for asynchronous submission. Execute the following steps:

1. In adaptive form authoring mode, select the Form Container object and tap ![adaptive form properties](assets/configure_icon.png) to open its properties.
1. In the **[!UICONTROL Submission]** properties section, enable **[!UICONTROL Use asynchronous submission]**.
1. Select **[!UICONTROL Revalidate on server]** to validate the input field values on server before submission.
1. Select the Submit Action:

    * Select **[!UICONTROL Submit using Form Data Model]** and select the appropriate data model, if you are using RESTful web service based [form data model](work-with-form-data-model.md) as the data source.
    * Select **[!UICONTROL Submit to REST Service endpoint]** and specify the **[!UICONTROL Redirect URL/Path]**, if you are using RESTful web services as the data source.

    ![adaptive form submission properties](assets/af_submission_properties.png)

1. Tap ![Save](assets/save_icon.png) to save the properties.

### Add custom error handler on Adaptive Form submission {#add-custom-error-handler-af-submission}

AEM Forms provides out-of-the-box success and error handlers for form submissions. Handlers are client-side functions that execute based on the server response. When an Adaptive Form is submitted, the data is transmitted to the server for validation, which returns a response to the client with information about the success or error event for the submission. The information is passed as parameters to the relevant handler to execute the function.

Execute the following steps to add custom error handler on Adaptive Form submission:

1. Open an Adaptive Form in authoring mode, select any form object, and tap  to open the rule editor.
1. Select **[!UICONTROL Form]** in the Form Objects tree and tap **[!UICONTROL Create]**.
1. Select **[!UICONTROL Error in Submission]** from the Event drop-down list.
1. Write a rule to convert custom error structure to the standard error structure and tap **[!UICONTROL Done]** to save the rule.

The following is a sample code to convert a custom error structure to the standard error structure:

```javascript
var data = $event.data;
var som_map = {
    "id": "guide[0].guide1[0].guideRootPanel[0].Pet[0].id_1[0]",
    "name": "guide[0].guide1[0].guideRootPanel[0].Pet[0].name_2[0]",
    "status": "guide[0].guide1[0].guideRootPanel[0].Pet[0].status[0]"
};

var errorJson = {};
errorJson.errors = [];

if (data) {
    if (data.originMessage) {
        var errorData;
        try {
            errorData = JSON.parse(data.originMessage);
        } catch (err) {
            // not in json format
        }

        if (errorData) {
            Object.keys(errorData).forEach(function(key) {
                var som_key = som_map[key];
                if (som_key) {
                    var error = {};
                    error.somExpression = som_key;
                    error.errorMessage = errorData[key];
                    errorJson.errors.push(error);
                }
            });
        }
        window.guideBridge.handleServerValidationError(errorJson);
    } else {
        window.guideBridge.handleServerValidationError(data);
    }
}
```

The `var som_map` lists the SOM expression of the Adaptive Form fields that you want to transform into the standard format. You can view the SOM expression of any field in an adaptive form by tapping the field and selecting **[!UICONTROL View SOM Expression]**.

Using this custom error handler, the adaptive form converts the fields listed in `var som_map` to standard error message format. As a result, the validation error messages display at field-level in the adaptive form.

 -->
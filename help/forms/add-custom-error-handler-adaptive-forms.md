---
title: Lägg till en anpassad felhanterare i Adaptive Forms för AEM Adaptive Forms
description: AEM Forms har körklara hanterare och felhanterare för ett formulär som använder REST-slutpunkten som konfigurerats för att anropa en extern tjänst. Du kan lägga till en standardfelhanterare och en anpassad felhanterare i en AEM anpassad form.
keywords: Lägg till en anpassad felhanterare, lägg till en standardfelhanterare, lägg till en felhanterare i formuläret, använd regelredigerarens anropstjänst för att lägga till en anpassad felhanterare, konfigurera regelredigeraren för att lägga till en anpassad felhanterare, lägg till en anpassad felhanterare med regelredigeraren
contentOwner: Ruchita Srivastav
content-type: reference
feature: Adaptive Forms, Foundation Components
exl-id: 198a26a9-d6bb-457d-aab8-0a5d15177c48
role: User, Developer
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '2292'
ht-degree: 0%

---

# Lägg till anpassade felhanterare i AEM Adaptive Forms {#error-handlers-in-adaptive-form}

>[!NOTE]
>
> Adobe rekommenderar att du använder den moderna och utbyggbara datainhämtningen [Core Components](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html) för [att skapa nya adaptiva Forms](/help/forms/creating-adaptive-form-core-components.md) eller [lägga till adaptiva Forms på AEM Sites-sidor](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md). De här komponenterna utgör ett betydande framsteg när det gäller att skapa adaptiva Forms-filer, vilket ger imponerande användarupplevelser. I den här artikeln beskrivs det äldre sättet att skapa Adaptiv Forms med baskomponenter.

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/standard-validation-error-messages-adaptive-forms.html) |
| AEM as a Cloud Service | Den här artikeln |

AEM Forms har färdiga funktioner och felhanterare för att skicka in formulär. Den innehåller även funktioner för att anpassa felhanterarfunktioner. Du kan till exempel anropa ett anpassat arbetsflöde i serverdelen för specifika felkoder eller informera kunden om att tjänsten inte fungerar. Hanterare är funktioner på klientsidan som körs baserat på serversvaret. När en extern tjänst anropas med API:er överförs data till servern för validering, som returnerar ett svar till klienten med information om lyckad eller felhändelse för överföringen. Informationen skickas som parametrar till den relevanta hanteraren för att köra funktionen. En felhanterare hjälper till att hantera och visa fel eller valideringsproblem som påträffats.

![felhanterararbetsflöde för att förstå hur du lägger till en anpassad felhanterare i formulär](/help/forms/assets/error-handler-workflow.png)

Det adaptiva formuläret validerar indata som du anger i fält baserat på förinställda valideringskriterier och söker efter olika fel som returneras av REST-slutpunkten som konfigurerats för att anropa en extern tjänst. Du kan ange valideringskriterier baserat på den datakälla som du använder med det adaptiva formuläret. Om du till exempel använder RESTful-webbtjänster som datakälla kan du definiera valideringskriterierna i en Swagger-definitionsfil.

Om indatavärdena uppfyller valideringskriterierna skickas värdena till datakällan i annat fall visas ett felmeddelande i Adaptiv form med hjälp av en felhanterare. På samma sätt som detta arbetssätt integreras Adaptive Forms med anpassade felhanterare för datavalidering. Om indatavärdena inte uppfyller valideringskriterierna visas felmeddelandena på fältnivå i det adaptiva formuläret. Detta inträffar när det valideringsfelmeddelande som returneras av servern har standardmeddelandeformatet.


## Användning av felhanterare {#uses-of-error-handler}

Felhanterare används för olika syften. Några av användningsområdena för felhanterarfunktioner visas nedan:
* **Utför validering**: Felhanteringen börjar med att användarindata valideras mot fördefinierade regler eller villkor. När användarna fyller i ett adaptivt formulär validerar felhanteraren indata så att det uppfyller det format, den längd eller andra begränsningar som krävs.

* **Ge feedback i realtid**: När ett fel upptäcks visar felhanteraren direkt feedback till användaren, till exempel textbundna felmeddelanden under motsvarande formulärfält. Denna feedback hjälper användarna att identifiera och åtgärda fel utan att behöva skicka in formuläret och vänta på ett svar.


* **Visa felmeddelanden**: När en sändning med adaptiva formulär påträffar ett valideringsfel visar felhanteraren ett felmeddelande. Felmeddelandena ska vara tydliga, koncisa och markera de specifika fält som behöver åtgärdas.

* **Markerar det felaktiga fältet**: För att dra användarens uppmärksamhet till specifika felaktiga fält markeras eller visas motsvarande fält i felhanteraren. Den utförs genom att ändra bakgrundsfärgen, lägga till en ikon eller kantlinje eller någon annan visuell indikator som hjälper användarna att snabbt hitta och åtgärda felen.


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
* `errors` anger SOM-uttrycket för de fält som underkändes i valideringskriterierna tillsammans med valideringsfelmeddelandet.
* Fältet `originCode` har lagts till av AEM och innehåller http-statuskoden som returneras av den externa tjänsten.
* Fältet `originMessage` har lagts till av AEM och innehåller råa feldata som returnerats av den externa tjänsten.

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
> * Kontrollera att rubriken **ContentType** är **application/problem+json**.

Var:
* `type (required)` anger typen av fel. Det kan vara något av följande värden:
   * `SERVER_SIDE_VALIDATION` indikerar ett fel på grund av validering på serversidan.
   * `FORM_SUBMISSION` indikerar ett fel under formuläröverföringen
   * `SERVICE_INVOCATION` indikerar ett fel under ett anrop av en tredjepartstjänst.
   * `FAILURE` indikerar ett allmänt fel.
   * `VALIDATION_ERROR` indikerar ett fel på grund av ett valideringsfel.

* `title (optional)` innehåller en titel eller en kort beskrivning av felet.
* `detail (optional)` innehåller ytterligare information om felet om det behövs.
* `instance (optional)` representerar en instans eller identifierare som är associerad med felet och hjälper till att spåra eller identifiera den specifika förekomsten av felet.
* `validationErrors (required)` innehåller information om valideringsfel. Den innehåller följande fält:
   * `fieldname` omnämns SOM-uttrycket för de fält som inte uppfyller valideringskriterierna.
   * `dataRef` representerar JSON-sökvägen eller XPath för de fält som inte kunde valideras.
   * `details` innehåller valideringsfelmeddelandet med det felaktiga fältet.
* Fältet `originCode (optional)` har lagts till av AEM och innehåller http-statuskoden som returneras av den externa tjänsten
* Fältet `originMessage (optional)` har lagts till av AEM och innehåller råa feldata som returnerats av den externa tjänsten.

### Exempel på felsvarsformat {#sample-error-response-format}

Vissa av alternativen för att visa felsvaren är:

+++  Baserat på egenskapen Adaptive Form fieldName


* **`Header:`** `content-type:application/problem+json`
* **`Response:`**

  ```javascript
          {
              "type": "VALIDATION_ERROR",
              "validationErrors": [
              {
              "fieldName": "guide[0].guide1[0].guideRootPanel[0].textbox1686647736683[0]",
              "dataRef": "",
              "details": [
              "Invalid ID supplied. Provided value is not correct!"
          ]
          }
          ]}
  ```

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

Du kan visa värdet för dataRef i **[!UICONTROL Properties]**-fönstret för en formulärkomponent.

+++


## Lägg till felhanterare med Regelredigeraren {#add-error-handler-using-rule-editor}

Med åtgärden [Anropa tjänst](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/rule-editor.html?lang=en#invoke) i regelredigeraren kan du definiera valideringskriterier baserat på datakällan som du använder med det anpassade formuläret. Om du använder RESTful-webbtjänster som datakälla kan du definiera valideringskriterierna i en Swagger-definitionsfil. Genom att använda felhanterarfunktionerna och regelredigeraren i Adaptive Forms kan du effektivt hantera och anpassa felhanteringen. Du definierar villkoren med Regelredigeraren och konfigurerar de åtgärder som ska utföras när regeln aktiveras. Adaptiv form validerar indata som du anger i fält baserat på förinställda valideringskriterier. Om indatavärdena inte uppfyller valideringskriterierna visas felmeddelandena på fältnivån i ett adaptivt formulär.

>[!NOTE]
>
> * Om du vill använda felhanterare med regelredigerarens Invoke-tjänståtgärd konfigurerar du Adaptive Forms med en formulärdatamodell (FDM).
> * En standardfelhanterare tillhandahålls för att visa felmeddelanden i fält om felsvaret finns i standardschemat. Du kan också anropa standardfelhanteraren från den anpassade felhanterarfunktionen.

Med regelredigeraren kan du:
* [Lägg till standardfelhanterarfunktion](#add-default-errror-handler)
* [Lägg till anpassad felhanterarfunktion](#add-custom-error-handler-function)


### Lägg till standardfelhanterarfunktion {#add-default-errror-handler}

En standardfelhanterare stöds för att visa felmeddelanden i fält om felsvaret är i standardschema eller i valideringsfel på serversidan.
För att förstå hur du använder en standardfelhanterare med hjälp av åtgärden [Anropa tjänst för regelredigerare](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/rule-editor.html?lang=en#invoke) ska du ta ett exempel på ett enkelt adaptivt formulär med två fält, **Pet ID** och **Pet Name** , och använda en standardfelhanterare i fältet **Pet ID** för att kontrollera om det finns olika fel som returneras av REST-slutpunkten som konfigurerats för att anropa en extern tjänst. exempel: `200 - OK`,`404 - Not Found`, `400 - Bad Request`. Så här lägger du till en standardfelhanterare med hjälp av åtgärden Anropa tjänst i regelredigeraren:

1. Öppna ett adaptivt formulär i redigeringsläge, markera en formulärkomponent och välj **[!UICONTROL Rule Editor]** för att öppna regelredigeraren.
1. Välj **[!UICONTROL Create]**.
1. Skapa ett villkor i avsnittet **När** i regeln. Till exempel ändras **När[namnet på fältet Pet-ID]** ändras. Markeringen ändras i listrutan **Välj läge**.
1. I avsnittet **Sedan** väljer du **[!UICONTROL Invoke Service]** i listrutan **Välj åtgärd** .
1. Välj en **posttjänst** och dess motsvarande databindningar i avsnittet **Indata**. Om du till exempel vill validera **Pet ID** markerar du en **Post service** som **GET /pet/{petId}** och väljer **Pet ID** i avsnittet **Indata** .
1. Välj databindningar i avsnittet **Utdata**. Välj **Djurnamn** i avsnittet **Utdata**.
1. Välj **[!UICONTROL Default Error Handler]** i avsnittet **Felhanterare**.
1. Klicka på **[!UICONTROL Done]**.

![lägg till en standardfelhanterare för fältverifieringskontroller i ett formulär](/help/forms/assets/default-error-handler.png)

Som ett resultat av den här regeln kontrollerar de värden du anger för **Pet ID** valideringen för **Pet Name** med hjälp av den externa tjänsten som anropas av REST-slutpunkten. Om valideringskriterierna som baseras på datakällan misslyckas, visas felmeddelandena på fältnivå.

![visar standardfelmeddelandet när du lägger till en standardfelhanterare i ett formulär som hanterar felsvar](/help/forms/assets/default-error-message.png)

### Lägg till anpassad felhanterarfunktion

Du kan lägga till en anpassad felhanterarfunktion för att utföra några av åtgärderna:

* hantera felsvar som använder icke-standard- eller standardfelsvar. Observera att dessa icke-standardfelsvar inte är kompatibla med [standardschemat för felsvar](#failure-response-format).
* skicka analyshändelser till alla analysplattformar. Exempel: Adobe Analytics.
* visa modal dialog med felmeddelanden.

Förutom de nämnda åtgärderna kan de anpassade felhanterarna användas för att utföra anpassade funktioner som uppfyller specifika användarkrav.

Den anpassade felhanteraren är en funktion (klientbibliotek) som är utformad för att svara på fel som returneras av en extern tjänst och leverera ett anpassat svar till slutanvändarna. Alla klientbibliotek med anteckningen `@errorHandler` betraktas som en anpassad felhanterarfunktion. Den här anteckningen hjälper till att identifiera felhanterarfunktionen som anges i filen `.js`.
För att förstå hur du skapar och använder en anpassad felhanterare med hjälp av åtgärden [Regelredigerarens anropstjänst](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/rule-editor.html?lang=en#invoke) kan vi ta ett exempel på Adaptiv form med två fält, **Pet ID** och **Pet Name**, och använda en anpassad felhanterare i fältet **Pet ID** för att kontrollera om det finns olika fel som returneras av REST-slutpunkten som konfigurerats för att anropa en extern tjänst, till exempel `200 - OK`,`404 - Not Found`, `400 - Bad Request`.

Så här lägger du till och använder en anpassad felhanterare i ett adaptivt formulär:
1. [Lägg till anpassad funktion för felhanterare](#1-add-the-custom-function-for-the-error-handler)
2. [Använd regelredigeraren för att konfigurera en anpassad felhanterare](#use-custom-error-handler)

#### 1. Lägg till den anpassade funktionen för felhanteraren

Om du vill lära dig hur du lägger till anpassade funktioner klickar du på [Skapa anpassade funktioner i ett adaptivt formulär baserat på kärnkomponenter](/help/forms/custom-function-core-component-create-function.md#create-a-custom-function).

<!-- To create a custom error function, perform the following steps:

1. [Clone your AEM Forms as a Cloud Service Repository](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#accessing-git). 
2. Create a folder under the `[AEM Forms as a Cloud Service repository folder]/apps/` folder. For example, create a folder named as `experience-league`
3. Navigate to `[AEM Forms as a Cloud Service repository folder]/apps/[AEM Project Folder]/experience-league/` and create a `ClientLibraryFolder` as `clientlibs`.
4. Create a folder named `js`.
5. Navigate to the `[AEM Forms as a Cloud Service repository folder]/apps/[AEM Project Folder]/clientlibs/js` folder. -->

1. Lägg till nedanstående kod för anpassad felhanterare i JavaScript-filen, till exempel `function.js`. Filen innehåller koden för den anpassade felhanteraren.
Låt oss lägga till följande kod i JavaScript-filen för att visa svar och rubriker som tagits emot från REST-tjänstens slutpunkt i webbläsarkonsolen.

   ```javascript
       /**
       * Custom Error handler
       * @name customErrorHandler Custom Error Handler Function
       * @errorHandler
       */
       function customErrorHandler(response, headers)
       {
           console.log("Custom Error Handler processing start...");
           console.log("response:"+JSON.stringify(response));
           console.log("headers:"+JSON.stringify(headers));
           guidelib.dataIntegrationUtils.defaultErrorHandler(response, headers);
           console.log("Custom Error Handler processing end...");
       }
   ```

   >[!NOTE]
   >
   > * Följande rad i exempelkoden används för att anropa standardfelhanteraren från din anpassade felhanterare: `guidelib.dataIntegrationUtils.defaultErrorHandler(response, headers) `
   > * Lägg till egenskaperna `allowProxy` och `categories` i filen `.content.xml` om du vill använda klientbiblioteket för anpassade felhanterare i ett adaptivt formulär.
   >
   >   * `allowProxy = [Boolean]true`
   >   * `categories= customfunctionsdemo`
   >       I det här fallet anges till exempel [custom-errorhandler-name] som `customfunctionsdemo`.


1. Lägg till, implementera och skicka ändringarna i databasen.

<!--

<!--
1. Save the `function.js` file.
1. Navigate to the `[AEM Forms as a Cloud Service repository folder]/apps/[AEM Project Folder]/clientlibs/js` folder.
2. Add a text file as `js.txt`. The file contains:

    ```javascript
        #base=js
        functions.js
    ```

3. Save the `js.txt` file.    
The created folder structure looks like:

    ![Created Client Library Folder Structure](/help/forms/assets/customclientlibrary_folderstructure.png) 
    using the below commands:
         
    ```javascript

        git add .
        git commit -a -m "Adding error handling files"
        git push
    ```
-->

1. [Kör pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#setup-pipeline).

När pipeline har körts blir den anpassade felhanteraren tillgänglig i regelredigeraren för adaptiva formulär. Nu ska vi förstå hur du konfigurerar och använder en anpassad felhanterare med hjälp av regelredigerarens Invoke-tjänst i AEM Forms.

#### 2. Använd regelredigeraren för att konfigurera en anpassad felhanterare {#use-custom-error-handler}

Innan du implementerar den anpassade felhanteraren i ett adaptivt formulär måste du se till att klientbiblioteksnamnet i **[!UICONTROL Client Library Category]** justeras med det namn som anges i kategorialternativet i filen `.content.xml` .

![Lägger till namnet på klientbiblioteket i konfigurationen för adaptiv formulärbehållare](/help/forms/assets/client-library-category-name.png)

I det här fallet anges klientbiblioteksnamnet som `customfunctionsdemo` i filen `.content.xml`.

Så här använder du en anpassad felhanterare med åtgärden **[!UICONTROL Rule Editor's Invoke Service]**:

1. Öppna ett adaptivt formulär i redigeringsläge, markera en formulärkomponent och välj **[!UICONTROL Rule Editor]** för att öppna regelredigeraren.
1. Välj **[!UICONTROL Create]**.
1. Skapa ett villkor i avsnittet **När** i regeln. Om till exempel **[namnet på fältet för Pet-ID]** ändras, ändras **väljs** i den nedrullningsbara listan **Välj läge**.
1. I avsnittet **Sedan** väljer du **[!UICONTROL Invoke Service]** i listrutan **Välj åtgärd** .
1. Välj en **posttjänst** och dess motsvarande databindningar i avsnittet **Indata**. Om du till exempel vill validera **Pet ID** markerar du en **Post service** som **GET /pet/{petId}** och väljer **Pet ID** i avsnittet **Indata** .
1. Välj databindningar i avsnittet **Utdata**. Välj till exempel **Djurnamn** i avsnittet **Utdata**.
1. Välj **[!UICONTROL Custom Error Handler]** i avsnittet **[!UICONTROL Error Handler]**.
1. Klicka på **[!UICONTROL Done]**.

![lägg till anpassad felhanterare i ett formulär för att hantera felsvar](/help/forms/assets/custom-error-handler.png)

Som ett resultat av den här regeln kontrollerar de värden du anger för **Pet ID** valideringen för **Pet Name** med hjälp av den externa tjänsten som anropas av REST-slutpunkten. Om valideringskriterierna som baseras på datakällan misslyckas, visas felmeddelandena på fältnivå.

![lägg till en anpassad felhanterare i ett formulär för att hantera felsvar](/help/forms/assets/custom-error-handler-message.png)

Öppna webbläsarkonsolen och kontrollera svaret och rubriken som tagits emot från REST-tjänstens slutpunkt för valideringsfelmeddelandet.


Den anpassade felhanterarfunktionen ansvarar för att utföra ytterligare åtgärder, som att visa en modal dialogruta eller skicka en analyshändelse, baserat på felsvaret. En anpassad felhanterarfunktion ger flexibilitet att anpassa felhanteringen efter specifika användarkrav.

<!-- 

## Configure Adaptive Form submission to add custom handlers {#configure-adaptive-form-submission}

If the server validation error message does not display in the standard format, you can enable asynchronous submission and add a custom error handler on Adaptive Form submission to convert the message into a standard format.

### Configure asynchronous Adaptive Form submission {#configure-asynchronous-adaptive-form-submission}

Before adding custom handler, you must configure the adaptive form for asynchronous submission. Execute the following steps:

1. In adaptive form authoring mode, select the Form Container object and select ![adaptive form properties](assets/configure_icon.png) to open its properties.
1. In the **[!UICONTROL Submission]** properties section, enable **[!UICONTROL Use asynchronous submission]**.
1. Select **[!UICONTROL Revalidate on server]** to validate the input field values on server before submission.
1. Select the Submit Action:

    * Select **[!UICONTROL Submit using Form Data Model (FDM)]** and select the appropriate data model, if you are using RESTful web service based [form data model (FDM)](work-with-form-data-model.md) as the data source.
    * Select **[!UICONTROL Submit to REST Service endpoint]** and specify the **[!UICONTROL Redirect URL/Path]**, if you are using RESTful web services as the data source.

    ![adaptive form submission properties](assets/af_submission_properties.png)

1. Select ![Save](assets/save_icon.png) to save the properties.

### Add custom error handler on Adaptive Form submission {#add-custom-error-handler-af-submission}

AEM Forms provides out-of-the-box success and error handlers for form submissions. Handlers are client-side functions that execute based on the server response. When an Adaptive Form is submitted, the data is transmitted to the server for validation, which returns a response to the client with information about the success or error event for the submission. The information is passed as parameters to the relevant handler to execute the function.

Execute the following steps to add custom error handler on Adaptive Form submission:

1. Open an Adaptive Form in authoring mode, select any form object, and select  to open the rule editor.
1. Select **[!UICONTROL Form]** in the Form Objects tree and select **[!UICONTROL Create]**.
1. Select **[!UICONTROL Error in Submission]** from the Event drop-down list.
1. Write a rule to convert custom error structure to the standard error structure and select **[!UICONTROL Done]** to save the rule.

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
            Object.keys (errorData).forEach(function(key) {
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


## Se även {#see-also}

{{see-also}}
* [Skapa och använda anpassade felhanterare i Adaptive Forms (Core Components)](/help/forms/add-custom-error-handler-adaptive-forms-core-components.md)

<!--

>[!MORELIKETHIS]
>
>* [Create style or themes for your forms](/help/forms/using-themes-in-core-components.md)
>* [Create or add an Adaptive Form to AEM Sites page](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)

-->

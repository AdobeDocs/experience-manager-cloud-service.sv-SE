---
title: Konfigurera en Skicka-åtgärd för ett anpassat formulär
description: Ett anpassat formulär innehåller flera överföringsåtgärder. En Skicka-åtgärd definierar hur ett anpassat formulär ska bearbetas när det har skickats in. Du kan använda inbyggda Skicka-åtgärder eller skapa egna.
exl-id: a4ebedeb-920a-4ed4-98b3-2c4aad8e5f78
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '1642'
ht-degree: 0%

---

# Inlämningsåtgärd för anpassat formulär {#configuring-the-submit-action}

En Skicka-åtgärd aktiveras när en användare klickar på **[!UICONTROL Submit]** på ett adaptivt formulär. Adaptiv Forms innehåller vissa inskickningsåtgärder. De Skicka-åtgärder som är tillgängliga är:

* [Skicka till REST-slutpunkt](#submit-to-rest-endpoint)
* [Skicka e-post](#send-email)
* [Skicka med formulärdatamodell](#submit-using-form-data-model)
* [Anropa ett AEM arbetsflöde](#invoke-an-aem-workflow)

Du kan också [utöka standardskickaåtgärder](custom-submit-action-form.md) för att skapa en egen Skicka-åtgärd.

Du kan konfigurera en Skicka-åtgärd i **[!UICONTROL Submission]** i egenskaperna för den adaptiva formulärbehållaren i sidlisten.

![Konfigurera Skicka-åtgärd](assets/submission.png)


<!-- [!NOTE]
>
>Send PDF via Email Submit Action is applicable only to Adaptive Forms that use XFA template as form model. 

>[!NOTE]
>
>Ensure that the [AEM_Installation_Directory]\crx-quickstart\temp\datamanager\ASM folder
>exists. The directory is required to temporarily store attachments. If the directory does not exist, create it. -->

<!--

>[!CAUTION]
>
>If you  [prefill](prepopulate-adaptive-form-fields.md) a form template,  a Form Data Model or schema based Adaptive Form with XML or JSON data complaint to a schema (XML schema, JSON schema , form template, or form data model) that is data does not contain &lt;afData&gt;, &lt;afBoundData&gt;, and &lt;/afUnboundData&gt; tags, then the data of unbounded fields (Unbounded fields are Adaptive Form fields without [bindref](prepopulate-adaptive-form-fields.md) property) of the Adaptive Form is lost. 

>[!CAUTION]
>
>If you [prefill](prepopulate-adaptive-form-fields.md) a form template, a Form Data Model or schema based Adaptive Form with XML or JSON data complaint to a schema (XML schema, JSON schema, or form data model) that does not contain &lt;afData&gt;, &lt;afBoundData&gt;, and &lt;/afUnboundData&gt; tags, then the data of unbounded fields (Unbounded fields are Adaptive Form fields without [bindref](prepopulate-adaptive-form-fields.md) property) of the Adaptive Form is lost.


-->




## Skicka till REST-slutpunkt {#submit-to-rest-endpoint}

Använd **[!UICONTROL Submit to REST Endpoint]** åtgärd för att skicka skickade data till en rest-URL. URL:en kan vara en intern (servern som formuläret återges på) eller en extern server.

Om du vill skicka data till en intern server anger du sökvägen till resursen. Data bokförs som resurssökväg. Till exempel /content/restEndPoint. För sådana efterfrågningar används autentiseringsinformationen i förfrågan.

Ange en URL om du vill skicka data till en extern server. URL-formatet är `https://host:port/path_to_rest_end_point`. Se till att du konfigurerar sökvägen så att den hanterar POSTENS begäran anonymt.

![Mappning för fältvärden skickas som Tack-sidan-parametrar](assets/post-enabled-actionconfig.png)

I exemplet ovan har användaren angett information i `textbox` hämtas med parameter `param1`. Syntax för att bokföra data som samlats in med `param1` är:

`String data=request.getParameter("param1");`

På samma sätt är parametrar som du använder för att bokföra XML-data och bifogade filer `dataXml` och `attachments`.

Du kan till exempel använda de här två parametrarna i skriptet för att tolka data till en slutpunkt. Du använder följande syntax för att lagra och analysera data:

`String data=request.getParameter("dataXml");`
`String att=request.getParameter("attachments");`

I det här exemplet `data` lagrar XML-data, och `att` lagrar data för bifogade filer.

The **[!UICONTROL Submit to REST endpoint]** Skicka åtgärd skickar data som är ifyllda i formuläret till en konfigurerad bekräftelsesida som en del av HTTP GET-begäran. Du kan lägga till namnet på fälten som ska begäras. Begäran har följande format:

`{fieldName}={request parameter name}`

Som visas i bilden nedan `param1` och `param2` skickas som parametrar med värden som kopierats från **textruta** och **numerisk** fält för nästa åtgärd.

![Konfigurerar åtgärden Skicka för resterande slutpunkt](assets/action-config.png)

Du kan också **[!UICONTROL Enable POST request]** och ange en URL för att skicka begäran. Om du vill skicka data till den AEM servern som är värd för formuläret använder du en relativ sökväg som motsvarar rotsökvägen för AEM. Till exempel, `/content/forms/af/SampleForm.html`. Om du vill skicka data till en annan server använder du den absoluta sökvägen.

>[!NOTE]
>
>Om du vill skicka fälten som parametrar i en REST-URL måste alla fält ha olika elementnamn, även om fälten placeras på olika paneler.

## Skicka e-post {#send-email}

Du kan använda **[!UICONTROL Send Email]** Skicka åtgärd för att skicka ett e-postmeddelande till en eller flera mottagare när formuläret har skickats. E-postmeddelandet som genereras kan innehålla formulärdata i ett fördefinierat format. I följande mall hämtas till exempel kundnamn, leveransadress, namn på stat och postnummer från skickade formulärdata.

    &quot;
    
    Hej ${customer_Name},
    
    Följande anges som standardleveransadress:
    ${customer_Name},
    ${customer_Shipping_Address},
    ${customer_State},
    ${customer_ZIPCode}
    
    Med vänlig hälsning
    WKND
    
    &quot;

>[!NOTE]
>
> * Alla formulärfält måste ha olika elementnamn, även om fälten placeras på olika paneler i ett anpassat formulär.
> * AEM as a Cloud Service kräver att utgående e-post krypteras. Som standard är utgående e-post inaktiverad. Om du vill aktivera det skickar du en supportanmälan till [Begär åtkomst](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=en#sending-email).


Du kan även bifoga bilagor och ett DoR-dokument (Document of Record) till e-postmeddelandet. Aktivera **[!UICONTROL Attach Document of Record]** konfigurerar du det adaptiva formuläret för att generera ett dokument för inspelning (DoR). Du kan aktivera alternativet att generera ett postdokument från egenskaper för anpassat formulär.



<!-- ## Send PDF via Email {#send-pdf-via-email}

The **Send PDF via Email** Submit Action sends an email with a PDF containing form data, to one or more recipients on successful submission of the form.

>[!NOTE]
>
>This Submit Action is available for XFA-based Adaptive Forms and XSD-based adaption forms that have the Document of Record template. -->

<!-- ## Invoke a forms workflow {#invoke-a-forms-workflow}

The **Submit to Forms workflow** submit option sends a data xml and file attachments (if any) to an existing Adobe LiveCycle or [!DNL AEM Forms] on JEE process.

For information about how to configure the Submit to forms workflow Submit Action, see [Submitting and processing your form data using forms workflows](submit-form-data-livecycle-process.md). -->

## Skicka med formulärdatamodell {#submit-using-form-data-model}

The **[!UICONTROL Submit using Form Data Model]** Skicka åtgärd skriver skickade adaptiva formulärdata för det angivna datamodellsobjektet i en formulärdatamodell till datakällan. När du konfigurerar åtgärden Skicka kan du välja ett datamodellsobjekt vars skickade data du vill skriva tillbaka till dess datakälla.

Dessutom kan du skicka en bifogad fil med en formulärdatamodell och en DoR-fil (Document of Record) till datakällan. Mer information om formulärdatamodell finns i [[!DNL AEM Forms] Dataintegrering](data-integration.md).

<!--
## Forms Portal Submit Action {#forms-portal-submit-action}

The **Forms Portal Submit Action** option makes form data available through an [!DNL AEM Forms] portal.

For more information about the Forms Portal and Submit Action, see [Drafts and submissions component](draft-submission-component.md). -->

## Anropa ett AEM arbetsflöde {#invoke-an-aem-workflow}

The **[!UICONTROL Invoke an AEM Workflow]** Åtgärden Skicka associerar ett anpassat formulär med ett [AEM](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=en#extending-aem). När ett formulär skickas startar det associerade arbetsflödet automatiskt på författarinstansen. Åtgärden Skicka placerar följande på arbetsflödets nyttolastplats:

* **Datafil**: Den innehåller data som skickats till den adaptiva formen. Du kan använda **[!UICONTROL Data File Path]** om du vill ange filens namn och sökväg i förhållande till nyttolasten. Till exempel `/addresschange/data.xml` sökväg skapar en mapp med namnet `addresschange` och placerar den i förhållande till nyttolasten. Du kan också bara ange `data.xml` om du bara vill skicka skickade data utan att skapa en mapphierarki.

* **Bifogade filer**: Du kan använda **[!UICONTROL Attachment Path]** om du vill ange mappnamnet för lagring av de bilagor som överförts till det adaptiva formuläret. Mappen skapas i förhållande till nyttolasten.

* **Dokument**: Det innehåller det dokument med post som genererats för det adaptiva formuläret. Du kan använda **[!UICONTROL Document of Record Path]** om du vill ange namnet på filen Dokument för post och sökvägen till filen i förhållande till nyttolasten. Till exempel `/addresschange/DoR.pdf` sökväg skapar en mapp med namnet `addresschange` i förhållande till nyttolasten och placerar `DoR.pdf` i förhållande till nyttolast. Du kan också bara ange `DoR.pdf` om du bara vill spara postdokument utan att skapa en mapphierarki.

Innan du använder **[!UICONTROL Invoke an AEM Workflow]** Skicka åtgärd konfigurera följande för **[!UICONTROL AEM DS settings service]** konfiguration:

* **[!UICONTROL Processing Server URL]**: Bearbetningsservern är den server där Forms- eller AEM-arbetsflödet aktiveras. Detta kan vara samma som URL:en för AEM författarinstans eller en annan server.

* **[!UICONTROL Processing Server User Name]**: Användarnamn för arbetsflöde

* **[!UICONTROL Processing Server Password]**: Lösenord för arbetsflödesanvändare

Så här anger du värden för en konfiguration: [Generera OSGi-konfigurationer med AEM SDK](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#generating-osgi-configurations-using-the-aem-sdk-quickstart)och [distribuera konfigurationen](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#deployment-process) till din Cloud Service.

## Använd synkron eller asynkron sändning {#use-synchronous-or-asynchronous-submission}

En Skicka-åtgärd kan använda synkron eller asynkron sändning.

**Synkron överföring**: Som standard är webbformulär konfigurerade att skicka synkront. När användare skickar ett formulär omdirigeras de i en synkron sändning till en bekräftelsesida, en tacksida eller en felsida om det uppstår ett överföringsfel. Du kan välja **[!UICONTROL Use asynchronous submission]** för att dirigera om användarna till en webbsida eller visa ett meddelande när de skickas.

![Konfigurera Skicka-åtgärd](assets/thank-you-setting.png)

**Asynkron överföring**: Moderna webbupplevelser som single page-applikationer blir allt populärare där webbsidan förblir statisk medan klient-server-interaktion sker i bakgrunden. Nu kan du använda Adaptive Forms via [konfigurera asynkron överföring](asynchronous-submissions-adaptive-forms.md).

## Förtroende på serversidan i adaptiv form {#server-side-revalidation-in-adaptive-form}

I alla onlinesystem för datainhämtning lägger utvecklare vanligtvis in JavaScript-valideringar på klientsidan för att tillämpa några få affärsregler. Men i moderna webbläsare kan slutanvändarna kringgå valideringarna och skicka in dokument manuellt med hjälp av olika tekniker, till exempel DevTools Console för webbläsare. Sådana tekniker gäller även för Adaptive Forms. En formulärutvecklare kan skapa olika valideringslogik, men tekniskt sett kan slutanvändarna kringgå dessa valideringslogik och skicka ogiltiga data till servern. Ogiltiga data skulle bryta mot de affärsregler som en formulärförfattare har infört.

Med funktionen för omvalidering på serversidan kan du även köra de valideringar som en adaptiv Forms-författare har tillhandahållit när han eller hon utformar ett adaptivt formulär på servern. Det förhindrar att inskickade data äventyras och affärsregelöverträdelser som representeras i form av formulärvalidering.

### Vad ska valideras på servern? {#what-to-validate-on-server-br}

Alla valideringar av ett adaptivt formulär som körs på servern i fältet OOTB (OOTB) är:

* Krävs
* Valideringsbildsats
* Valideringsuttryck

### Aktivera validering på serversidan {#enabling-server-side-validation-br}

Använd **[!UICONTROL Revalidate on server]** under Adaptiv formulärbehållare i sidofältet för att aktivera eller inaktivera validering på serversidan för det aktuella formuläret.

![Aktivera validering på serversidan](assets/revalidate-on-server.png)

Aktivera validering på serversidan

Om slutanvändaren åsidosätter dessa valideringar och skickar formulären utför servern valideringen igen. Om valideringen misslyckas vid serverslutet stoppas skicka-transaktionen. Slutanvändaren får originalformuläret igen. Insamlade data och skickade data visas för användaren som ett fel.

>[!NOTE]
>
>Validering på serversidan validerar formulärmodellen. Du rekommenderas att skapa ett separat klientbibliotek för validering och inte blanda det med andra saker som formatering av HTML och DOM-manipulering i samma klientbibliotek.

### Stöd för anpassade funktioner i valideringsuttryck {#supporting-custom-functions-in-validation-expressions-br}

Ibland, om det finns **komplexa valideringsregler**, finns det exakta valideringsskriptet i anpassade funktioner och författaren anropar dessa anpassade funktioner från fältvalideringsuttryck. Om du vill att det här anpassade funktionsbiblioteket ska vara känt och tillgängligt vid validering på serversidan kan formulärförfattaren konfigurera namnet på AEM klientbibliotek under **[!UICONTROL Basic]** fliken med egenskaper för adaptiv formulärbehållare enligt nedan.

![Stöd för anpassade funktioner i valideringsuttryck](assets/clientlib-cat.png)

Stöd för anpassade funktioner i valideringsuttryck

Författaren kan konfigurera customJavaScript-bibliotek per adaptiv form. I biblioteket behåller du bara återanvändbara funktioner som är beroende av jquery- och underscore.js-bibliotek från tredje part.

## Felhantering vid Skicka-åtgärd {#error-handling-on-submit-action}

Som en del av AEM riktlinjer för säkerhet och skärpa konfigurerar du anpassade felsidor som 400.jsp, 404.jsp och 500.jsp. Dessa hanterare anropas när ett formulär 400-, 404- eller 500-fel skickas. Hanterarna anropas också när dessa felkoder aktiveras på noden Publicera. Du kan också skapa JSP-sidor för andra HTTP-felkoder.

När du förifyller en formulärdatamodell eller ett schemabaserat adaptivt formulär med XML- eller JSON-data klagar till ett schema som inte innehåller data `<afData>`, `<afBoundData>`och `</afUnboundData>` -taggar, försvinner data i obegränsade fält i det adaptiva formuläret. Schemat kan vara ett XML-schema, JSON-schema eller en formulärdatamodell. Obegränsade fält är adaptiva formulärfält utan `bindref` -egenskap.

<!-- For more information, see [Customizing Pages shown by the Error Handler](/help/sites-developing/customizing-errorhandler-pages.md). -->

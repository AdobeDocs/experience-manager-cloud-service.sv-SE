---
title: Konfigurera en Skicka-åtgärd för ett anpassat formulär
description: Ett anpassat formulär innehåller flera överföringsåtgärder. En Skicka-åtgärd definierar hur ett anpassat formulär ska bearbetas när det har skickats in. Du kan använda inbyggda Skicka-åtgärder eller skapa egna.
exl-id: a4ebedeb-920a-4ed4-98b3-2c4aad8e5f78
source-git-commit: 921dc0f109b1faaa6d53086c4ca29627cb30bef8
workflow-type: tm+mt
source-wordcount: '2959'
ht-degree: 0%

---

# Inlämningsåtgärd för anpassat formulär {#configuring-the-submit-action}

En Skicka-åtgärd aktiveras när en användare klickar på **[!UICONTROL Submit]** på ett adaptivt formulär. Adaptiv Forms innehåller vissa inskickningsåtgärder. De Skicka-åtgärder som är tillgängliga är:

* [Skicka till REST-slutpunkt](#submit-to-rest-endpoint)
* [Skicka e-post](#send-email)
* [Skicka med formulärdatamodell](#submit-using-form-data-model)
* [Anropa ett AEM arbetsflöde](#invoke-an-aem-workflow)
* [Skicka till SharePoint](#submit-to-sharedrive)
* [Skicka till OneDrive](#submit-to-onedrive)
* [Skicka till Azure Blob Storage](#azure-blob-storage)

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

The **[!UICONTROL Invoke an AEM Workflow]** Åtgärden Skicka associerar ett anpassat formulär med ett [AEM](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=en#extending-aem). När ett formulär skickas startar det associerade arbetsflödet automatiskt på författarinstansen. Du kan spara datafilen, bifogade filer och postdokument på arbetsflödets nyttolastplats eller i en variabel. Om arbetsflödet är markerat för extern datalagring och konfigurerat för en extern datalagring är endast variabelalternativet tillgängligt. Du kan välja i listan över variabler som är tillgängliga för arbetsflödesmodellen. Om arbetsflödet markeras för extern datalagring i ett senare skede och inte när arbetsflödet skapas, kontrollerar du att de variabelkonfigurationer som krävs finns på plats.

Åtgärden Skicka placerar följande på arbetsflödets nyttolastplats, eller variabeln om arbetsflödet har markerats för extern datalagring:

* **Datafil**: Den innehåller data som skickats till den adaptiva formen. Du kan använda **[!UICONTROL Data File Path]** om du vill ange filens namn och sökväg i förhållande till nyttolasten. Till exempel `/addresschange/data.xml` sökväg skapar en mapp med namnet `addresschange` och placerar den i förhållande till nyttolasten. Du kan också bara ange `data.xml` om du bara vill skicka skickade data utan att skapa en mapphierarki. Om arbetsflödet är markerat för extern datalagring använder du variabelalternativet och väljer variabeln i listan med variabler som är tillgängliga för arbetsflödesmodellen.

* **Bifogade filer**: Du kan använda **[!UICONTROL Attachment Path]** om du vill ange mappnamnet för lagring av de bilagor som överförts till det adaptiva formuläret. Mappen skapas i förhållande till nyttolasten. Om arbetsflödet är markerat för extern datalagring använder du variabelalternativet och väljer variabeln i listan med variabler som är tillgängliga för arbetsflödesmodellen.

* **Dokument**: Det innehåller det dokument med post som genererats för det adaptiva formuläret. Du kan använda **[!UICONTROL Document of Record Path]** om du vill ange namnet på filen Dokument för post och sökvägen till filen i förhållande till nyttolasten. Till exempel `/addresschange/DoR.pdf` sökväg skapar en mapp med namnet `addresschange` i förhållande till nyttolasten och placerar `DoR.pdf` i förhållande till nyttolast. Du kan också bara ange `DoR.pdf` om du bara vill spara postdokument utan att skapa en mapphierarki. Om arbetsflödet är markerat för extern datalagring använder du variabelalternativet och väljer variabeln i listan med variabler som är tillgängliga för arbetsflödesmodellen.

Innan du använder **[!UICONTROL Invoke an AEM Workflow]** Skicka åtgärd konfigurera följande för **[!UICONTROL AEM DS settings service]** konfiguration:

* **[!UICONTROL Processing Server URL]**: Bearbetningsservern är den server där Forms- eller AEM-arbetsflödet aktiveras. Detta kan vara samma som URL:en för AEM författarinstans eller en annan server.

* **[!UICONTROL Processing Server User Name]**: Användarnamn för arbetsflöde

* **[!UICONTROL Processing Server Password]**: Lösenord för arbetsflödesanvändare

## Skicka till SharePoint {#submit-to-sharedrive}

The **[!UICONTROL Submit to SharePoint]** Skicka åtgärd kopplar ett adaptivt formulär till en Microsoft® SharePoint-lagring. Du kan skicka formulärdatafilen, bifogade filer eller arkivdokument till den anslutna Microsoft® Sharepoint-lagringsplatsen. Så här använder du **[!UICONTROL Submit to SharePoint]** Skicka åtgärd i anpassad form:

1. [Skapa en SharePoint-konfiguration](#create-a-sharepoint-configuration-create-sharepoint-configuration): Den kopplar AEM Forms till din Microsoft® Sharepoint-lagring.
2. [Använda Skicka till SharePoint-åtgärden i ett anpassat formulär](#use-sharepoint-configuartion-in-af): Den kopplar ditt adaptiva formulär till konfigurerade Microsoft® SharePoint.

### Skapa en SharePoint-konfiguration {#create-sharepoint-configuration}

Så här ansluter du AEM Forms till din Microsoft® Sharepoint-lagring:

1. Gå till **AEM Forms Author** instans > **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** >  **[!UICONTROL Microsoft® SharePoint]**.
1. När du har valt **[!UICONTROL Microsoft® SharePoint]** omdirigeras du till **[!UICONTROL SharePoint Browser]**.
1. Välj en **Konfigurationsbehållare**. Konfigurationen lagras i den valda konfigurationsbehållaren.
1. Klicka på **[!UICONTROL Create]**. Konfigurationsguiden för SharePoint visas.
   ![SharePoint-konfiguration](/help/forms/assets/sharepoint_configuration.png)
1. Ange **[!UICONTROL Title]**, **[!UICONTROL Client ID]**, **[!UICONTROL Client Secret]** och **[!UICONTROL OAuth URL]**. Mer information om hur du hämtar klient-ID, klienthemlighet, klient-ID för OAuth-URL finns i [Microsoft® Documentation](https://learn.microsoft.com/en-us/graph/auth-register-app-v2).
   * Du kan hämta `Client ID` och `Client Secret` från Microsoft® Azure-portalen.
   * Lägg till omdirigerings-URI som i Microsoft® Azure-portalen som `https://[author-instance]/libs/cq/sharepoint/content/configurations/wizard.html`. Ersätt `[author-instance]` med webbadressen till din Author-instans.
   * Lägg till API-behörigheter `offline_access` och `Sites.Manage.All` för att ge läs- och skrivbehörigheter.
   * Använd OAuth-URL: `https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize`. Ersätt `<tenant-id>` med `tenant-id` från Microsoft® Azure-portalen.

   >[!NOTE]
   >
   > The **klienthemlighet** fältet är obligatoriskt eller valfritt beroende på din Azure Active Directory-programkonfiguration. Om ditt program är konfigurerat att använda en klienthemlighet är det obligatoriskt att ange klienthemligheten.

1. Klicka på **[!UICONTROL Connect]**. Vid en lyckad anslutning visas `Connection Successful` visas.

1. Välj nu **SharePoint Site** > **Dokumentbibliotek** > **SharePoint-mapp**, för att spara data.

   >[!NOTE]
   >
   >* Som standard `forms-ootb-storage-adaptive-forms-submission` finns på den valda SharePoint-webbplatsen.
   >* Skapa en mapp som `forms-ootb-storage-adaptive-forms-submission`, om de inte redan finns i `Documents` bibliotek för den valda SharePoint-webbplatsen genom att klicka på **Skapa mapp**.


Nu kan du använda den här SharePoint Sites-konfigurationen för att skicka-åtgärden i ett adaptivt formulär.

### Använda SharePoint Configuration i en adaptiv form {#use-sharepoint-configuartion-in-af}

Du kan använda den skapade SharePoint-konfigurationen i ett adaptivt formulär för att spara data eller skapa ett postdokument i en SharePoint-mapp. Så här använder du en SharePoint-lagringskonfiguration i ett adaptivt format:
1. Skapa en [Adaptiv form](/help/forms/creating-adaptive-form.md).

   >[!NOTE]
   >
   > * Välj samma [!UICONTROL Configuration Container] för ett adaptivt formulär där du har skapat din SharePoint-lagring.
   > * Om nej [!UICONTROL Configuration Container] markeras och sedan den globala [!UICONTROL Storage Configuration] visas i egenskapsfönstret för Skicka åtgärd.


1. Välj **Skicka åtgärd** as **[!UICONTROL Submit to SharePoint]**.
   ![SharePoint GIF](/help/forms/assets/sharedrive-video.gif)
1. Välj **[!UICONTROL Storage Configuration]**, där du vill spara dina data.
1. Klicka **[!UICONTROL Save]** för att spara Skicka-inställningarna.

När du skickar formuläret sparas data i den angivna Microsoft® Sharepoint-lagringsplatsen.
Mappstrukturen som data ska sparas i är `/folder_name/form_name/year/month/date/submission_id/data`.

## Skicka till OneDrive {#submit-to-onedrive}

The **[!UICONTROL Submit to OneDrive]** Skicka åtgärd kopplar ett anpassat formulär till en Microsoft® OneDrive. Du kan skicka formulärdata, filer, bilagor eller arkivdokument till den anslutna Microsoft® OneDrive-lagringsplatsen. Så här använder du [!UICONTROL Submit to OneDrive] Skicka åtgärd i anpassad form:

1. [Skapa en OneDrive-konfiguration](#create-a-onedrive-configuration-create-onedrive-configuration): Den ansluter AEM Forms till din Microsoft® OneDrive-lagring.
2. [Använd Skicka till OneDrive-åtgärden i ett anpassat formulär](#use-onedrive-configuration-in-an-adaptive-form-use-onedrive-configuartion-in-af): Det kopplar ditt adaptiva formulär till konfigurerade Microsoft® OneDrive.

### Skapa en OneDrive-konfiguration {#create-onedrice-configuration}

Så här ansluter du AEM Forms till din Microsoft® OneDrive-lagring:

1. Gå till **AEM Forms Author** instans > **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** >  **[!UICONTROL Microsoft® OneDrive]**.
1. När du har valt **[!UICONTROL Microsoft® OneDrive]** omdirigeras du till **[!UICONTROL OneDrive Browser]**.
1. Välj en **Konfigurationsbehållare**. Konfigurationen lagras i den valda konfigurationsbehållaren.
1. Klicka på **[!UICONTROL Create]**. Konfigurationsguiden för OneDrive visas.

   ![Konfigurationsskärm för OneDrive](/help/forms/assets/onedrive-configuration.png)

1. Ange **[!UICONTROL Title]**, **[!UICONTROL Client ID]**, **[!UICONTROL Client Secret]** och **[!UICONTROL OAuth URL]**. Mer information om hur du hämtar klient-ID, klienthemlighet, klient-ID för OAuth-URL finns i [Microsoft® Documentation](https://learn.microsoft.com/en-us/graph/auth-register-app-v2).
   * Du kan hämta `Client ID` och `Client Secret` från Microsoft® Azure-portalen.
   * Lägg till omdirigerings-URI som i Microsoft® Azure-portalen som `https://[author-instance]/libs/cq/onedrive/content/configurations/wizard.html`. Ersätt `[author-instance]` med webbadressen till din Author-instans.
   * Lägg till API-behörigheter `offline_access` och `Files.ReadWrite.All` för att ge läs- och skrivbehörigheter.
   * Använd OAuth-URL: `https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize`. Ersätt `<tenant-id>` med `tenant-id` från Microsoft® Azure-portalen.

   >[!NOTE]
   >
   > The **klienthemlighet** fältet är obligatoriskt eller valfritt beroende på din Azure Active Directory-programkonfiguration. Om ditt program är konfigurerat att använda en klienthemlighet är det obligatoriskt att ange klienthemligheten.

1. Klicka på **[!UICONTROL Connect]**. Vid en lyckad anslutning visas `Connection Successful` visas.

1. Välj nu **[!UICONTROL OneDrive Container]** > **[OneDrive-mapp]**  för att spara data.

   >[!NOTE]
   >
   >* Som standard `forms-ootb-storage-adaptive-forms-submission` finns i OneDrive-behållaren.
   > * Skapa en mapp som `forms-ootb-storage-adaptive-forms-submission`, om den inte redan finns genom att klicka **Skapa mapp**.


Nu kan du använda den här lagringskonfigurationen för OneDrive för att skicka-åtgärden i ett adaptivt formulär.

### Använd OneDrive-konfiguration i ett adaptivt formulär {#use-onedrive-configuartion-in-af}

Du kan använda den skapade OneDrive-lagringskonfigurationen i ett adaptivt formulär för att spara data eller skapa ett postdokument i en OneDrive-mapp. Utför följande steg om du vill använda OneDrive-lagringskonfigurationen i en adaptiv form:
1. Skapa en [Adaptiv form](/help/forms/creating-adaptive-form.md).

   >[!NOTE]
   >
   > * Välj samma [!UICONTROL Configuration Container] för ett adaptivt formulär, där du har skapat din OneDrive-lagring.
   > * Om nej [!UICONTROL Configuration Container] markeras och sedan den globala [!UICONTROL Storage Configuration] visas i egenskapsfönstret för Skicka åtgärd.


1. Välj **Skicka åtgärd** as **[!UICONTROL Submit to OneDrive]**.
   ![OneDrive GIF](/help/forms/assets/onedrive-video.gif)
1. Välj **[!UICONTROL Storage Configuration]**, där du vill spara dina data.
1. Klicka **[!UICONTROL Save]** för att spara Skicka-inställningarna.

När du skickar formuläret sparas data i den angivna Microsoft® OneDrive-lagringsplatsen.
Mappstrukturen som data ska sparas i är `/folder_name/form_name/year/month/date/submission_id/data`.

## Skicka till Azure Blob Storage {#submit-to-azure-blob-storage}

The **[!UICONTROL Submit to Azure Blob Storage]**  Skicka åtgärd kopplar ett anpassat formulär till en Microsoft® Azure-portal. Du kan skicka formulärdata, filer, bilagor eller arkivdokument till de anslutna Azure Storage-behållarna. Så här använder du åtgärden Skicka för Azure Blob Storage:

1. [Skapa en Azure Blob Storage-behållare](#create-a-azure-blob-storage-container-create-azure-configuration): Den ansluter AEM Forms till Azure Storage-behållare.
2. [Använd Azure Storage-konfigurationen i ett adaptivt formulär ](#use-azure-storage-configuration-in-an-adaptive-form-use-azure-storage-configuartion-in-af): Det kopplar ditt adaptiva formulär till konfigurerade Azure-lagringsbehållare.

### Skapa en Azure Blob Storage-behållare {#create-azure-configuration}

Så här ansluter du AEM Forms till dina Azure-lagringsbehållare:
1. Gå till **AEM Forms Author** instans > **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** >  **[!UICONTROL Azure Storage]**.
1. När du har valt **[!UICONTROL Azure Storage]** omdirigeras du till **[!UICONTROL Azure Storage Browser]**.
1. Välj en **Konfigurationsbehållare**. Konfigurationen lagras i den valda konfigurationsbehållaren.
1. Klicka på **[!UICONTROL Create]**. Guiden Skapa Azure Storage Configuration visas.

   ![Azure Storage-konfiguration](/help/forms/assets/azure-storage-configuration.png)

1. Ange **[!UICONTROL Title]**, **[!UICONTROL Azure Storage Account]** och **[!UICONTROL Azure Access key]**.

   * Du kan hämta `Azure Storage Account` namn och `Azure Access key` från lagringskonton i Microsoft® Azure-portalen.

1. Klicka på **[!UICONTROL Save]**.

Nu kan du använda den här Azure Storage-behållarkonfigurationen för överföringsåtgärden i ett adaptivt formulär.

### Använd Azure Storage-konfigurationen i ett adaptivt formulär {#use-azure-storage-configuartion-in-af}

Du kan använda den skapade Azure Storage-behållarkonfigurationen i ett adaptivt formulär för att spara data eller skapa ett dokument av posten i Azure Storage-behållaren. Utför följande steg för att använda konfigurationen av Azure Storage-behållaren i ett adaptivt formulär som:
1. Skapa en [Adaptiv form](/help/forms/creating-adaptive-form.md).

   >[!NOTE]
   >
   > * Välj samma [!UICONTROL Configuration Container] för ett adaptivt formulär, där du har skapat din OneDrive-lagring.
   > * Om nej [!UICONTROL Configuration Container] markeras och sedan den globala [!UICONTROL Storage Configuration] visas i egenskapsfönstret för Skicka åtgärd.


1. Välj **Skicka åtgärd** as **[!UICONTROL Submit to Azure Blob Storage]**.
   ![Azure Blob Storage GIF](/help/forms/assets/azure-submit-video.gif)

1. Välj **[!UICONTROL Storage Configuration]**, där du vill spara dina data.
1. Klicka **[!UICONTROL Save]** för att spara Skicka-inställningarna.

När du skickar formuläret sparas data i den angivna Azure Storage-behållarkonfigurationen.
Mappstrukturen som data ska sparas i är `/configuration_container/form_name/year/month/date/submission_id/data`.

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

* Obligatoriskt
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

---
title: Hur konfigurerar man en Skicka-åtgärd för ett anpassat formulär?
description: Ett anpassat formulär innehåller flera överföringsåtgärder. En Skicka-åtgärd definierar hur ett anpassat formulär ska bearbetas när det har skickats in. Du kan använda inbyggda Skicka-åtgärder eller skapa egna.
feature: Adaptive Forms, Foundation Components
exl-id: a4ebedeb-920a-4ed4-98b3-2c4aad8e5f78
role: User, Developer
source-git-commit: db0487ab11f48690cb36b410b895324e0d4cf684
workflow-type: tm+mt
source-wordcount: '3725'
ht-degree: 0%

---

# Inlämningsåtgärd för anpassat formulär {#configuring-the-submit-action}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/configuring-submit-actions.html) |
| AEM as a Cloud Service (kärnkomponenter) | [Klicka här](/help/forms/configure-submit-actions-core-components.md) |
| AEM as a Cloud Service (Foundation Components) | Den här artikeln |

**Gäller för**: ✔️ adaptiva formulärets Foundation-komponenter. ❌ [Kärnkomponenter för adaptiv form](/help/forms/configure-submit-actions-core-components.md). Adobe rekommenderar att du använder kärnkomponenter för att [lägga till adaptiv Forms på en AEM Sites-sida](create-or-add-an-adaptive-form-to-aem-sites-page.md) eller för att [skapa fristående adaptiv Forms](creating-adaptive-form-core-components.md).

En Skicka-åtgärd utlöses när en användare klickar på knappen **[!UICONTROL Submit]** i ett anpassat formulär. Forms as a Cloud Service tillhandahåller följande Skicka-åtgärder direkt.

* [Skicka till REST-slutpunkt](#submit-to-rest-endpoint)
* [Skicka e-post](#send-email)
* [Skicka med FDM (Form Data Mode)](#submit-using-form-data-model)
* [Anropa ett AEM](#invoke-an-aem-workflow)
* [Skicka till SharePoint](#submit-to-sharedrive)
* [Skicka till OneDrive](#submit-to-onedrive)
* [Skicka till Azure Blob Storage](#azure-blob-storage)
* [Skicka till Power Automate](#microsoft-power-automate)
* [Skicka till Workfront Fusion](#workfront-fusion)
* [Skicka till Marketo Engage](/help/forms/integrate-form-to-marketo-engage.md)

Du kan också [utöka standardåtgärden för att skicka ](custom-submit-action-form.md) och skapa en egen åtgärd för att skicka.

Du kan konfigurera en Skicka-åtgärd i avsnittet **[!UICONTROL Submission]** i egenskaperna för den anpassade formulärbehållaren i sidofältet.

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

Använd åtgärden **[!UICONTROL Submit to REST Endpoint]** för att skicka skickade data till en rest-URL. URL:en kan vara en intern (servern som formuläret återges på) eller en extern server.

Om du vill skicka data till en intern server anger du sökvägen till resursen. Data bokförs som resurssökväg. Till exempel /content/restEndPoint. För sådana efterfrågningar används autentiseringsinformationen i förfrågan.

Ange en URL om du vill skicka data till en extern server. URL-formatet är `https://host:port/path_to_rest_end_point`. Se till att du konfigurerar sökvägen så att den hanterar POSTENS begäran anonymt.

![Mappning för fältvärden skickas som parametrar för Tack-sidan](assets/post-enabled-actionconfig.png)

I exemplet ovan hämtas användarinformationen i `textbox` med parametern `param1`. Syntaxen för att bokföra data som har hämtats med `param1` är:

`String data=request.getParameter("param1");`

På samma sätt är parametrar som du använder för att skicka XML-data och bifogade filer `dataXml` och `attachments`.

Du kan till exempel använda de här två parametrarna i skriptet för att tolka data till en slutpunkt. Du använder följande syntax för att lagra och analysera data:

`String data=request.getParameter("dataXml");`
`String att=request.getParameter("attachments");`

I det här exemplet lagrar `data` XML-data och `att` lagrar data för bifogade filer.

Åtgärden **[!UICONTROL Submit to REST endpoint]** Skicka skickar data som är ifyllda i formuläret till en konfigurerad bekräftelsesida som en del av HTTP GET-begäran. Du kan lägga till namnet på fälten som ska begäras. Begäran har följande format:

`{fieldName}={request parameter name}`

Som visas i bilden nedan skickas `param1` och `param2` som parametrar med värden som kopierats från fälten **texbox** och **numerbox** för nästa åtgärd.

![Konfigurerar åtgärden Skicka för resterande slutpunkt](assets/action-config.png)

Du kan också **[!UICONTROL Enable POST request]** och ange en URL för att skicka begäran. Om du vill skicka data till den AEM servern som är värd för formuläret använder du en relativ sökväg som motsvarar rotsökvägen för AEM. Exempel: `/content/forms/af/SampleForm.html`. Om du vill skicka data till en annan server använder du den absoluta sökvägen.

>[!NOTE]
>
>Om du vill skicka fälten som parametrar i en REST-URL måste alla fält ha olika elementnamn, även om fälten placeras på olika paneler.

## Skicka e-post {#send-email}

Du kan använda åtgärden **[!UICONTROL Send Email]** Skicka för att skicka ett e-postmeddelande till en eller flera mottagare när formuläret har skickats. E-postmeddelandet som genereras kan innehålla formulärdata i ett fördefinierat format. I följande mall hämtas till exempel kundnamn, leveransadress, namn på stat och postnummer från skickade formulärdata.

    &quot;
    
    Hej ${customer_Name},
    
    Följande anges som standardleveransadress:
    ${customer_Name},
    ${customer_Shipping_Address},
    ${customer_State},
    ${customer_ZIPCode}
    
    Med vänlig hälsning,
    WKND
    
    &quot;

>[!NOTE]
>
> * Alla formulärfält måste ha olika elementnamn, även om fälten placeras på olika paneler i ett anpassat formulär.
> * AEM as a Cloud Service kräver att utgående e-post krypteras. Som standard är utgående e-post inaktiverad. Om du vill aktivera den skickar du en supportanmälan till [Begär åtkomst](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=en#sending-email).

Du kan även bifoga bilagor och ett DoR-dokument (Document of Record) till e-postmeddelandet. Om du vill aktivera alternativet **[!UICONTROL Attach Document of Record]** konfigurerar du det adaptiva formuläret så att det skapar ett dokument för post (DoR). Du kan aktivera alternativet att generera ett postdokument från egenskaper för anpassat formulär.



<!-- ## Send PDF via Email {#send-pdf-via-email}

The **Send PDF via Email** Submit Action sends an email with a PDF containing form data, to one or more recipients on successful submission of the form.

>[!NOTE]
>
>This Submit Action is available for XFA-based Adaptive Forms and XSD-based adaption forms that have the Document of Record template. -->

<!-- ## Invoke a forms workflow {#invoke-a-forms-workflow}

The **Submit to Forms workflow** submit option sends a data xml and file attachments (if any) to an existing Adobe LiveCycle or [!DNL AEM Forms] on JEE process.

For information about how to configure the Submit to forms workflow Submit Action, see [Submitting and processing your form data using forms workflows](submit-form-data-livecycle-process.md). -->

## Skicka med hjälp av formulärdatamodell (FDM) {#submit-using-form-data-model}

Åtgärden **[!UICONTROL Submit using Form Data Model]** Skicka skriver skickade adaptiva formulärdata för det angivna datamodellobjektet i en formulärdatamodell (FDM) till datakällan. När du konfigurerar åtgärden Skicka kan du välja ett datamodellsobjekt vars skickade data du vill skriva tillbaka till dess datakälla.

Dessutom kan du skicka en bifogad fil med en FDM (Form Data Model) och ett DoR-dokument (Document of Record) till datakällan. Mer information om formulärdatamodell (FDM) finns i [[!DNL AEM Forms] Dataintegrering](data-integration.md).

<!--
## Forms Portal Submit Action {#forms-portal-submit-action}

The **Forms Portal Submit Action** option makes form data available through an [!DNL AEM Forms] portal.

For more information about the Forms Portal and Submit Action, see [Drafts and submissions component](draft-submission-component.md). -->

## Anropa ett AEM {#invoke-an-aem-workflow}

Åtgärden **[!UICONTROL Invoke an AEM Workflow]** Skicka associerar ett anpassat formulär med ett [AEM arbetsflöde](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=en#extending-aem). När ett formulär skickas startar det associerade arbetsflödet automatiskt på författarinstansen. Du kan spara datafilen, bifogade filer och postdokument på arbetsflödets nyttolastplats eller i en variabel. Om arbetsflödet är markerat för extern datalagring och konfigurerat för en extern datalagring är endast variabelalternativet tillgängligt. Du kan välja i listan över variabler som är tillgängliga för arbetsflödesmodellen. Om arbetsflödet markeras för extern datalagring i ett senare skede och inte när arbetsflödet skapas, kontrollerar du att de variabelkonfigurationer som krävs finns på plats.

Åtgärden Skicka placerar följande på arbetsflödets nyttolastplats, eller variabeln om arbetsflödet har markerats för extern datalagring:

* **Datafil**: Den innehåller data som har skickats till det adaptiva formuläret. Du kan använda alternativet **[!UICONTROL Data File Path]** för att ange filens namn och sökväg i förhållande till nyttolasten. Sökvägen `/addresschange/data.xml` skapar till exempel en mapp med namnet `addresschange` och placerar den i förhållande till nyttolasten. Du kan också ange att bara `data.xml` ska skicka skickade data utan att skapa en mapphierarki. Om arbetsflödet är markerat för extern datalagring använder du variabelalternativet och väljer variabeln i listan med variabler som är tillgängliga för arbetsflödesmodellen.

* **Bifogade filer**: Du kan använda alternativet **[!UICONTROL Attachment Path]** för att ange mappnamnet för att lagra de bifogade filer som överförts till det anpassade formuläret. Mappen skapas i förhållande till nyttolasten. Om arbetsflödet är markerat för extern datalagring använder du variabelalternativet och väljer variabeln i listan med variabler som är tillgängliga för arbetsflödesmodellen.

* **Postdokument**: Det innehåller det postdokument som genererats för det adaptiva formuläret. Du kan använda alternativet **[!UICONTROL Document of Record Path]** för att ange namnet på filen Dokument för post och sökvägen till filen i förhållande till nyttolasten. Sökvägen `/addresschange/DoR.pdf` skapar till exempel en mapp med namnet `addresschange` relativt till nyttolasten och placerar `DoR.pdf` relativt nyttolasten. Du kan även ange att bara `DoR.pdf` ska spara postdokument utan att skapa en mapphierarki. Om arbetsflödet är markerat för extern datalagring använder du variabelalternativet och väljer variabeln i listan med variabler som är tillgängliga för arbetsflödesmodellen.

Innan du använder åtgärden **[!UICONTROL Invoke an AEM Workflow]** Skicka ska du konfigurera följande för konfigurationen **[!UICONTROL AEM DS settings service]**:

* **[!UICONTROL Processing Server URL]**: Bearbetningsservern är den server där Forms- eller AEM-arbetsflödet aktiveras. Detta kan vara samma som URL:en för AEM författarinstans eller en annan server.

* **[!UICONTROL Processing Server User Name]**: Användarnamn för arbetsflöde

* **[!UICONTROL Processing Server Password]**: Arbetsflödets användarlösenord

## Skicka till SharePoint {#submit-to-sharedrive}

Åtgärden **[!UICONTROL Submit to SharePoint]** för att skicka kopplar ett anpassat formulär till en Microsoft® SharePoint-lagring. Du kan skicka formulärdatafilen, bifogade filer eller arkivdokument till den anslutna Microsoft® Sharepoint-lagringsplatsen.

Med Skicka till SharePoint kan du
* [Ansluta ett anpassat formulär till SharePoint Document Library](#connect-af-sharepoint-doc-library)
* [Anslut ett anpassat formulär till SharePoint List](#connect-af-sharepoint-list)


### Ansluta ett anpassat formulär till SharePoint Document Library {#connect-af-sharepoint-doc-library}

Så här använder du åtgärden **[!UICONTROL Submit to SharePoint Document Library]** Skicka i en anpassad form:

1. [Skapa en SharePoint-dokumentbibliotekskonfiguration](#create-a-sharepoint-configuration-create-sharepoint-configuration): Den ansluter AEM Forms till din Microsoft® Sharepoint-lagring.
2. [Använd åtgärden Skicka till SharePoint i ett adaptivt formulär](#use-sharepoint-configuartion-in-af): Det kopplar ditt adaptiva formulär till konfigurerade Microsoft® SharePoint.

#### Skapa en SharePoint Document Library-konfiguration {#create-sharepoint-configuration}

Så här ansluter du AEM Forms till Microsoft® Sharepoint Document Library:

1. Gå till din **AEM Forms Author**-instans > **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Microsoft® SharePoint]**.
1. När du har valt **[!UICONTROL Microsoft® SharePoint]** omdirigeras du till **[!UICONTROL SharePoint Browser]**.
1. Välj en **konfigurationsbehållare**. Konfigurationen lagras i den valda konfigurationsbehållaren.
1. Klicka på **[!UICONTROL Create]** > **[!UICONTROL SharePoint Document Library]** i listrutan. Konfigurationsguiden för SharePoint visas.

   ![SharePoint-konfiguration](/help/forms/assets/sharepoint_configuration.png)
1. Ange **[!UICONTROL Title]**, **[!UICONTROL Client ID]**, **[!UICONTROL Client Secret]** och **[!UICONTROL OAuth URL]**. Mer information om hur du hämtar klient-ID, klienthemlighet, klient-ID för OAuth URL finns i [Microsoft®-dokumentation](https://learn.microsoft.com/en-us/graph/auth-register-app-v2).
   * Du kan hämta `Client ID` och `Client Secret` för din app från Microsoft® Azure-portalen.
   * Lägg till omdirigerings-URI som `https://[author-instance]/libs/cq/sharepoint/content/configurations/wizard.html` i Microsoft® Azure-portalen. Ersätt `[author-instance]` med URL:en för din Author-instans.
   * Lägg till API-behörigheterna `offline_access` och `Sites.Manage.All` för att ge läs-/skrivbehörigheter.
   * Använd OAuth-URL: `https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize`. Ersätt `<tenant-id>` med `tenant-id` för din app från Microsoft® Azure-portalen.

   >[!NOTE]
   >
   > Fältet **klienthemlighet** är obligatoriskt eller valfritt beroende på din Azure Active Directory-programkonfiguration. Om ditt program är konfigurerat att använda en klienthemlighet är det obligatoriskt att ange klienthemligheten.

1. Klicka på **[!UICONTROL Connect]**. Om anslutningen lyckas visas meddelandet `Connection Successful`.

1. Välj nu **SharePoint-plats** > **Dokumentbibliotek** > **SharePoint-mapp** för att spara data.

   >[!NOTE]
   >
   >* Som standard finns `forms-ootb-storage-adaptive-forms-submission` på den valda SharePoint-webbplatsen.
   >* Skapa en mapp som `forms-ootb-storage-adaptive-forms-submission`, om den inte redan finns i `Documents`-biblioteket för den valda SharePoint-platsen genom att klicka på **Skapa mapp**.

Nu kan du använda den här SharePoint Sites-konfigurationen för att skicka-åtgärden i ett adaptivt formulär.

#### Använda SharePoint Document Library Configuration i ett adaptivt formulär {#use-sharepoint-configuartion-in-af}

Du kan använda den skapade SharePoint Document Library-konfigurationen i ett adaptivt formulär för att spara data eller generera Document of Record i en SharePoint-mapp. Utför följande steg för att använda lagringskonfigurationen för SharePoint Document Library i ett adaptivt formulär som:

1. Skapa ett [anpassat formulär](/help/forms/creating-adaptive-form.md).

   >[!NOTE]
   >
   > * Välj samma [!UICONTROL Configuration Container] för ett adaptivt formulär, där du har skapat ditt SharePoint Document Library-lagringsutrymme.
   > * Om [!UICONTROL Configuration Container] inte är markerat visas de globala [!UICONTROL Storage Configuration]-mapparna i egenskapsfönstret för Skicka åtgärd.

1. Välj **Skicka åtgärd** som **[!UICONTROL Submit to SharePoint]**.
   ![SharePoint GIF](/help/forms/assets/sharedrive-video.gif)
1. Markera **[!UICONTROL Storage Configuration]** där du vill spara dina data.
1. Klicka på **[!UICONTROL Save]** om du vill spara Skicka-inställningarna.

När du skickar formuläret sparas data i den angivna Microsoft® Sharepoint-dokumentbibliotekslagringen.
Mappstrukturen som data ska sparas i är `/folder_name/form_name/year/month/date/submission_id/data`.

### Ansluta ett anpassat formulär till Microsoft® SharePoint List {#connect-af-sharepoint-list}

>[!VIDEO](https://video.tv.adobe.com/v/3424820/connect-aem-adaptive-form-to-sharepointlist/?quality=12&learn=on)

Så här använder du åtgärden [!UICONTROL Submit to SharePoint List] Skicka i en anpassad form:

1. [Skapa en SharePoint-listkonfiguration](#create-sharepoint-list-configuration): Den ansluter AEM Forms till din Microsoft® Sharepoint-listlagring.
1. [Använd Skicka med FDM (Form Data Model) i ett adaptivt formulär](#use-submit-using-fdm): Det kopplar ditt adaptiva formulär till konfigurerade Microsoft® SharePoint.

#### Skapa en listkonfiguration för SharePoint {#create-sharepoint-list-configuration}

Så här ansluter du AEM Forms till din Microsoft® Sharepoint-lista:

1. Gå till **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Microsoft® SharePoint]**.
1. Välj en **konfigurationsbehållare**. Konfigurationen lagras i den valda konfigurationsbehållaren.
1. Klicka på **[!UICONTROL Create]** > **[!UICONTROL SharePoint List]** i listrutan. Konfigurationsguiden för SharePoint visas.
1. Ange **[!UICONTROL Title]**, **[!UICONTROL Client ID]**, **[!UICONTROL Client Secret]** och **[!UICONTROL OAuth URL]**. Mer information om hur du hämtar klient-ID, klienthemlighet, klient-ID för OAuth URL finns i [Microsoft®-dokumentation](https://learn.microsoft.com/en-us/graph/auth-register-app-v2).
   * Du kan hämta `Client ID` och `Client Secret` för din app från Microsoft® Azure-portalen.
   * Lägg till omdirigerings-URI som `https://[author-instance]/libs/cq/sharepointlist/content/configurations/wizard.html` i Microsoft® Azure-portalen. Ersätt `[author-instance]` med URL:en för din Author-instans.
   * Lägg till API-behörigheterna `offline_access` och `Sites.Manage.All` på fliken **Microsoft® Graph** för att ge läs-/skrivbehörigheter. Lägg till behörigheten `AllSites.Manage` på fliken **Sharepoint** om du vill fjärrinteragera med SharePoint-data.
   * Använd OAuth-URL: `https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize`. Ersätt `<tenant-id>` med `tenant-id` för din app från Microsoft® Azure-portalen.

     >[!NOTE]
     >
     > Fältet **klienthemlighet** är obligatoriskt eller valfritt beroende på din Azure Active Directory-programkonfiguration. Om ditt program är konfigurerat att använda en klienthemlighet är det obligatoriskt att ange klienthemligheten.

1. Klicka på **[!UICONTROL Connect]**. Om anslutningen lyckas visas meddelandet `Connection Successful`.
1. Välj **[!UICONTROL SharePoint Site]** och **[!UICONTROL SharePoint List]** i listrutan.
1. Välj **[!UICONTROL Create]** om du vill skapa molnkonfigurationen för Microsoft® SharePointList.


#### Använda Skicka med hjälp av formulärdatamodell (FDM) i ett anpassat formulär {#use-submit-using-fdm}

Du kan använda den skapade SharePoint List-konfigurationen i ett adaptivt formulär för att spara data eller skapa ett postdokument i en SharePoint List. Utför följande steg om du vill använda en lagringskonfiguration i SharePoint List i en anpassad form:

1. [Skapa en formulärdatamodell (FDM) med Microsoft® SharePoint List configuration](/help/forms/create-form-data-models.md)
1. [Konfigurera FDM (Form Data Model) för att hämta och skicka data](/help/forms/work-with-form-data-model.md#configure-services)
1. [Skapa ett adaptivt formulär](/help/forms/creating-adaptive-form.md)
1. [Konfigurera åtgärden Skicka med en formulärdatamodell (FDM)](/help/forms/configuring-submit-actions.md#submit-using-form-data-model)

När du skickar formuläret sparas data i det angivna lagringsutrymmet för Microsoft® Sharepoint-listan.

>[!NOTE]
>
> I Microsoft® SharePoint List stöds inte följande kolumntyper:
> * bildkolumn
> * metadatakolumn
> * personkolumn
> * extern datakolumn


## Skicka till OneDrive {#submit-to-onedrive}

Åtgärden **[!UICONTROL Submit to OneDrive]** kopplar ett anpassat formulär till en Microsoft® OneDrive. Du kan skicka formulärdata, filer, bilagor eller arkivdokument till den anslutna Microsoft® OneDrive-lagringsplatsen. Så här använder du åtgärden [!UICONTROL Submit to OneDrive] Skicka i en anpassad form:

1. [Skapa en OneDrive-konfiguration](#create-a-onedrive-configuration-create-onedrive-configuration): Den ansluter AEM Forms till din Microsoft® OneDrive-lagring.
2. [Använd åtgärden Skicka till OneDrive i ett anpassat formulär](#use-onedrive-configuration-in-an-adaptive-form-use-onedrive-configuartion-in-af): Det kopplar ditt adaptiva formulär till
konfigurerade Microsoft® OneDrive.

### Skapa en OneDrive-konfiguration {#create-onedrice-configuration}

Så här ansluter du AEM Forms till din Microsoft® OneDrive-lagring:

1. Gå till din **AEM Forms Author**-instans > **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Microsoft® OneDrive]**.
1. När du har valt **[!UICONTROL Microsoft® OneDrive]** omdirigeras du till **[!UICONTROL OneDrive Browser]**.
1. Välj en **konfigurationsbehållare**. Konfigurationen lagras i den valda konfigurationsbehållaren.
1. Klicka på **[!UICONTROL Create]**. Konfigurationsguiden för OneDrive visas.

   ![Konfigurationsskärmen för OneDrive](/help/forms/assets/onedrive-configuration.png)

1. Ange **[!UICONTROL Title]**, **[!UICONTROL Client ID]**, **[!UICONTROL Client Secret]** och **[!UICONTROL OAuth URL]**. Mer information om hur du hämtar klient-ID, klienthemlighet, klient-ID för OAuth URL finns i [Microsoft®-dokumentation](https://learn.microsoft.com/en-us/graph/auth-register-app-v2).
   * Du kan hämta `Client ID` och `Client Secret` för din app från Microsoft® Azure-portalen.
   * Lägg till omdirigerings-URI som `https://[author-instance]/libs/cq/onedrive/content/configurations/wizard.html` i Microsoft® Azure-portalen. Ersätt `[author-instance]` med URL:en för din Author-instans.
   * Lägg till API-behörigheterna `offline_access` och `Files.ReadWrite.All` för att ge läs-/skrivbehörigheter.
   * Använd OAuth-URL: `https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize`. Ersätt `<tenant-id>` med `tenant-id` för din app från Microsoft® Azure-portalen.

   >[!NOTE]
   >
   > Fältet **klienthemlighet** är obligatoriskt eller valfritt beroende på din Azure Active Directory-programkonfiguration. Om ditt program är konfigurerat att använda en klienthemlighet är det obligatoriskt att ange klienthemligheten.

1. Klicka på **[!UICONTROL Connect]**. Om anslutningen lyckas visas meddelandet `Connection Successful`.

1. Välj nu **[!UICONTROL OneDrive Container]** > **[OneDrive-mapp]** för att spara data.

   >[!NOTE]
   >
   >* Som standard finns `forms-ootb-storage-adaptive-forms-submission` i OneDrive-behållaren.
   > * Skapa en mapp som `forms-ootb-storage-adaptive-forms-submission`, om den inte redan finns, genom att klicka på **Skapa mapp**.

Nu kan du använda den här lagringskonfigurationen för OneDrive för att skicka-åtgärden i ett adaptivt formulär.

### Använd OneDrive-konfiguration i ett adaptivt formulär {#use-onedrive-configuartion-in-af}

Du kan använda den skapade OneDrive-lagringskonfigurationen i ett adaptivt formulär för att spara data eller skapa ett postdokument i en OneDrive-mapp. Utför följande steg för att använda OneDrive-lagringskonfigurationen i ett adaptivt formulär som:
1. Skapa ett [anpassat formulär](/help/forms/creating-adaptive-form.md).

   >[!NOTE]
   >
   > * Välj samma [!UICONTROL Configuration Container] för ett adaptivt formulär, där du har skapat ditt OneDrive-lagringsutrymme.
   > * Om [!UICONTROL Configuration Container] inte är markerat visas de globala [!UICONTROL Storage Configuration]-mapparna i egenskapsfönstret för Skicka åtgärd.

1. Välj **Skicka åtgärd** som **[!UICONTROL Submit to OneDrive]**.
   ![OneDrive GIF](/help/forms/assets/onedrive-video.gif)
1. Markera **[!UICONTROL Storage Configuration]** där du vill spara dina data.
1. Klicka på **[!UICONTROL Save]** om du vill spara Skicka-inställningarna.

När du skickar formuläret sparas data i den angivna Microsoft® OneDrive-lagringsplatsen.
Mappstrukturen som data ska sparas i är `/folder_name/form_name/year/month/date/submission_id/data`.

## Skicka till Azure Blob Storage {#submit-to-azure-blob-storage}

Åtgärden **[!UICONTROL Submit to Azure Blob Storage]** för att skicka kopplar ett anpassat formulär till en Microsoft® Azure-portal. Du kan skicka formulärdata, filer, bilagor eller arkivdokument till de anslutna Azure Storage-behållarna. Så här använder du åtgärden Skicka för Azure Blob Storage:

1. [Skapa en Azure Blob Storage-behållare](#create-a-azure-blob-storage-container-create-azure-configuration): Den ansluter AEM Forms till Azure Storage-behållare.
2. [Använd Azure Storage-konfigurationen i ett adaptivt formulär](#use-azure-storage-configuration-in-an-adaptive-form-use-azure-storage-configuartion-in-af): Den ansluter ditt adaptiva formulär till konfigurerade Azure Storage-behållare.

### Skapa en Azure Blob Storage-behållare {#create-azure-configuration}

Så här ansluter du AEM Forms till dina Azure-lagringsbehållare:
1. Gå till din **AEM Forms Author**-instans > **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Azure Storage]**.
1. När du har valt **[!UICONTROL Azure Storage]** omdirigeras du till **[!UICONTROL Azure Storage Browser]**.
1. Välj en **konfigurationsbehållare**. Konfigurationen lagras i den valda konfigurationsbehållaren.
1. Klicka på **[!UICONTROL Create]**. Guiden Skapa Azure Storage Configuration visas.

   ![Azure-lagringskonfiguration](/help/forms/assets/azure-storage-configuration.png)

1. Ange **[!UICONTROL Title]**, **[!UICONTROL Azure Storage Account]** och **[!UICONTROL Azure Access key]**.

   * Du kan hämta `Azure Storage Account`-namn och `Azure Access key` från lagringskonton på Microsoft® Azure-portalen.

1. Klicka på **[!UICONTROL Save]**.

Nu kan du använda den här Azure Storage-behållarkonfigurationen för överföringsåtgärden i ett adaptivt formulär.

### Använd Azure Storage-konfigurationen i ett adaptivt formulär {#use-azure-storage-configuartion-in-af}

Du kan använda den skapade Azure Storage-behållarkonfigurationen i ett adaptivt formulär för att spara data eller skapa ett dokument av posten i Azure Storage-behållaren. Utför följande steg för att använda konfigurationen av Azure Storage-behållaren i ett adaptivt formulär som:
1. Skapa ett [anpassat formulär](/help/forms/creating-adaptive-form.md).

   >[!NOTE]
   >
   > * Välj samma [!UICONTROL Configuration Container] för ett adaptivt formulär, där du har skapat ditt OneDrive-lagringsutrymme.
   > * Om [!UICONTROL Configuration Container] inte är markerat visas de globala [!UICONTROL Storage Configuration]-mapparna i egenskapsfönstret för Skicka åtgärd.

1. Välj **Skicka åtgärd** som **[!UICONTROL Submit to Azure Blob Storage]**.
   ![Azure Blob Storage GIF](/help/forms/assets/azure-submit-video.gif)

1. Markera **[!UICONTROL Storage Configuration]** där du vill spara dina data.
1. Klicka på **[!UICONTROL Save]** om du vill spara Skicka-inställningarna.

När du skickar formuläret sparas data i den angivna Azure Storage-behållarkonfigurationen.
Mappstrukturen som data ska sparas i är `/configuration_container/form_name/year/month/date/submission_id/data`.

[Generera OSGi-konfigurationer med AEM SDK](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#generating-osgi-configurations-using-the-aem-sdk-quickstart) och [distribuera konfigurationen](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#deployment-process) till din Cloud Service om du vill ange värden för en konfiguration.


## Skicka till Power Automate {#microsoft-power-automate}

Du kan konfigurera ett adaptivt formulär så att det kör ett Microsoft® Power Automate Cloud-flöde när du skickar in det. Den konfigurerade adaptiva formen skickar inhämtade data, bilagor och arkivdokument till Power Automate Cloud Flow för bearbetning. Det hjälper er att bygga upp en anpassad datainhämtningsupplevelse och samtidigt utnyttja kraften i Microsoft® Power Automate för att skapa affärslogik kring insamlade data och automatisera kundarbetsflöden. Här är några exempel på vad du kan göra efter att ha integrerat ett adaptivt formulär med Microsoft® Power Automate:

* Använd adaptiva Forms-data i en Power Automate-affärsprocess
* Använd Power Automate för att skicka inhämtade data till fler än 500 datakällor eller till något offentligt tillgängligt API
* Utför komplexa beräkningar på inhämtade data
* Spara adaptiva Forms-data i lagringssystemen enligt ett fördefinierat schema

Den adaptiva Forms-redigeraren tillhandahåller **Anropa ett Microsoft® Power Automate-flöde** för att skicka adaptiva formulärdata, bilagor och arkivdokument som skickas till Power Automate Cloud Flow. Om du vill använda åtgärden Skicka för att skicka hämtade data till Microsoft® Power Automate [ansluter du Forms as a Cloud Service-instansen till Microsoft® Power Automate](forms-microsoft-power-automate-integration.md)

När konfigurationen är klar kan du använda åtgärden [Anropa ett Microsoft® Power Automate-flöde](forms-microsoft-power-automate-integration.md#use-the-invoke-a-microsoft&reg;-power-automate-flow-submit-action-to-send-data-to-a-power-automate-flow-use-the-invoke-microsoft-power-automate-flow-submit-action) för att skicka data till ett Power Automate-flöde.

## Skicka till Workfront Fusion {#workfront-fusion}

Du kan konfigurera ett adaptivt formulär så att data skickas till Workfront Fusion när de skickas. Med Workfront Fusion kan man automatisera processer så att man kan koncentrera sig på nya uppgifter istället för att upprepa samma uppgifter om och om igen. Den automatiserar både enkla och komplexa uppgifter, sparar tid och säkerställer ett konsekvent processutförande.

Den adaptiva Forms-redigeraren innehåller **Anropa ett Workfront Fusion-scenario** som skickar adaptiva Forms-data eller bilagor till ett Workfront Fusion-scenario. Om du vill använda åtgärden Skicka för att skicka hämtade data till ett Workfront Fusion-scenario läser du [Skicka ett anpassat formulär till Adobe Workfront Fusion](/help/forms/submit-adaptive-form-to-workfront-fusion.md).

## Använd synkron eller asynkron sändning {#use-synchronous-or-asynchronous-submission}

En Skicka-åtgärd kan använda synkron eller asynkron sändning.

**Synkron sändning**: Webbformulär har vanligtvis konfigurerats att skicka synkront. När användare skickar ett formulär omdirigeras de i en synkron sändning till en bekräftelsesida, en tacksida eller en felsida om det uppstår ett överföringsfel. Du kan välja alternativet **[!UICONTROL Use asynchronous submission]** om du vill dirigera om användarna till en webbsida eller visa ett meddelande när de skickas.

![Konfigurera Skicka-åtgärd](assets/thank-you-setting.png)

**Asynkron överföring**: Moderna webbupplevelser som enkelsidiga program blir allt populärare där webbsidan förblir statisk medan klient-server-interaktion sker i bakgrunden. Du kan nu tillhandahålla den här upplevelsen med Adaptive Forms genom att [konfigurera asynkron sändning](asynchronous-submissions-adaptive-forms.md).

## Förtroende på serversidan i adaptiv form {#server-side-revalidation-in-adaptive-form}

I alla onlinesystem för datainhämtning lägger utvecklare vanligtvis in JavaScript-valideringar på klientsidan för att tillämpa några få affärsregler. Men i moderna webbläsare kan slutanvändarna kringgå valideringarna och skicka in dokument manuellt med hjälp av olika tekniker, till exempel DevTools Console för webbläsare. Sådana tekniker gäller även för Adaptive Forms. En formulärutvecklare kan skapa olika valideringslogik, men tekniskt sett kan slutanvändarna kringgå dessa valideringslogik och skicka ogiltiga data till servern. Ogiltiga data skulle bryta mot de affärsregler som en formulärförfattare har infört.

Med funktionen för omvalidering på serversidan kan du även köra de valideringar som en adaptiv Forms-författare har tillhandahållit när han eller hon utformar ett adaptivt formulär på servern. Det förhindrar att inskickade data äventyras och affärsregelöverträdelser som representeras i form av formulärvalidering.

### Vad ska valideras på servern? {#what-to-validate-on-server-br}

Alla valideringar av ett adaptivt formulär som körs på servern i fältet OOTB (OOTB) är:

* Obligatoriskt
* Valideringsbildsats
* Valideringsuttryck

### Aktivera validering på serversidan {#enabling-server-side-validation-br}

Använd **[!UICONTROL Revalidate on server]** under Adaptiv formulärbehållare i sidlisten för att aktivera eller inaktivera validering på serversidan för det aktuella formuläret.

![Aktivera validering på serversidan](assets/revalidate-on-server.png)

Aktivera validering på serversidan

Om slutanvändaren åsidosätter dessa valideringar och skickar formulären utför servern valideringen igen. Om valideringen misslyckas vid serverslutet stoppas skicka-transaktionen. Användaren får det ursprungliga formuläret igen. Insamlade data och skickade data visas för användaren som ett fel.

>[!NOTE]
>
>Validering på serversidan validerar formulärmodellen. Du rekommenderas att skapa ett separat klientbibliotek för validering och inte blanda det med andra saker som formatering av HTML och DOM-manipulering i samma klientbibliotek.

### Stöd för anpassade funktioner i valideringsuttryck {#supporting-custom-functions-in-validation-expressions-br}

Om det finns **komplexa valideringsregler** finns ibland det exakta valideringsskriptet i anpassade funktioner och författaren anropar dessa anpassade funktioner från fältvalideringsuttryck. Om du vill att det här anpassade funktionsbiblioteket ska vara känt och tillgängligt vid validering på serversidan kan formulärförfattaren konfigurera namnet på AEM klientbibliotek på fliken **[!UICONTROL Basic]** i egenskaperna för adaptiv formulärbehållare enligt nedan.

![Stöd för anpassade funktioner i valideringsuttryck](assets/clientlib-cat.png)

Stöd för anpassade funktioner i valideringsuttryck

Författaren kan konfigurera customJavaScript-bibliotek per adaptiv form. I biblioteket behåller du bara återanvändbara funktioner som är beroende av jquery- och underscore.js-bibliotek från tredje part.

## Felhantering vid Skicka-åtgärd {#error-handling-on-submit-action}

Som en del av AEM riktlinjer för säkerhet och skärpa konfigurerar du anpassade felsidor som 400.jsp, 404.jsp och 500.jsp. Dessa hanterare anropas när ett formulär 400-, 404- eller 500-fel skickas. Hanterarna anropas också när dessa felkoder aktiveras på Publish-noden. Du kan också skapa JSP-sidor för andra HTTP-felkoder.

När du förifyller en formulärdatamodell (FDM), eller schemabaserad adaptiv form med XML- eller JSON-dataklagomål till ett schema som inte innehåller `<afData>` -, `<afBoundData>` - och `</afUnboundData>` -taggar, förloras data i obegränsade fält i det adaptiva formuläret. Schemat kan vara ett XML-schema, ett JSON-schema eller en FDM (Form Data Model). Obegränsade fält är adaptiva formulärfält utan egenskapen `bindref`.

<!-- For more information, see [Customizing Pages shown by the Error Handler](/help/sites-developing/customizing-errorhandler-pages.md). -->

>[!MORELIKETHIS]
>
>* [Skapa en anpassad Skicka-åtgärd för Adaptiv Forms](/help/forms/custom-submit-action-form.md)

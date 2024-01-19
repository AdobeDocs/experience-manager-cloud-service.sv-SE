---
title: Hur konfigurerar man en Skicka-åtgärd för ett anpassat formulär?
description: Ett anpassat formulär innehåller flera överföringsåtgärder. En Skicka-åtgärd definierar hur ett anpassat formulär ska bearbetas när det har skickats in. Du kan använda inbyggda Skicka-åtgärder eller skapa egna
keywords: hur du väljer en inskickningsåtgärd för ett tilläggsformulär, kopplar ett adaptivt formulär till SharePoint-listan, kopplar ett adaptivt formulär till SharePoint-dokumentbiblioteket, kopplar ett adaptivt formulär till formulärdatamodellen
feature: Adaptive Forms, Core Components
exl-id: 495948e8-30a7-4e7c-952f-c71de15520f0
source-git-commit: 2f567d45a6ba2dfb4dd3346e8510bcb04113eefb
workflow-type: tm+mt
source-wordcount: '667'
ht-degree: 0%

---


# Inlämningsåtgärd för anpassat formulär {#configuring-the-submit-action}

<span class="preview"> Adobe rekommenderar att du använder kärnkomponenter för att [lägga till adaptiv Forms på en AEM Sites-sida](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md) eller till [skapa fristående Adaptive Forms](/help/forms/creating-adaptive-form-core-components.md). </span>


| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/configuring-submit-actions.html) |
| AEM as a Cloud Service | Den här artikeln |

Med en Skicka-åtgärd kan du välja målet för data som har hämtats via ett anpassat formulär. Den aktiveras när en användare klickar på **[!UICONTROL Submit]** på ett adaptivt formulär. Forms as a Cloud Service, för Adaptive Forms baserat på kärnkomponenter, erbjuder en mängd färdiga Submit-åtgärder. Dessa färdiga sändningsåtgärder ger dig möjlighet att:

* Skicka enkelt formulärdata via e-post.
* Initiera Microsoft® Power Automate-flöden eller AEM arbetsflöden när data skickas.
* Skicka formulärdata direkt till Microsoft® SharePoint Server, Microsoft® Azure Blob Storage eller Microsoft® OneDrive.
* Skicka smidigt data till en konfigurerad datakälla med hjälp av formulärdatamodellen.
* Skicka enkelt data till en REST-slutpunkt.

Du kan [utöka standardåtgärderna för att skicka](custom-submit-action-form.md). Du kan också anpassa Skicka-åtgärder för organisationsspecifika krav.

Om du vill definiera en Skicka-åtgärd för en anpassad version använder du dialogrutan Konfigurera för en **Adaptiv formulärbehållare** -komponenten. Dialogrutan Konfigurera för **Adaptiv formulärbehållare** ingår:
* Fliken Grundläggande
* Fliken Formulärdatamodell
* Fliken Skicka

Du kan definiera egenskaperna för formulärbehållaren i dialogrutan Konfigurera. Mer information om dialogrutan Konfigurera för en formulärbehållarkomponent finns i [klicka här.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/form-container.html)

## Välj och konfigurera en Skicka-åtgärd för ett anpassat formulär {#select-and-configure-submit-action}

Så här väljer och konfigurerar du en Skicka-åtgärd för formuläret:

1. Öppna innehållsläsaren och välj **[!UICONTROL Guide Container]** som ingår i det adaptiva formuläret.
1. Klicka på egenskaperna för stödlinjebehållaren ![Stödlinjeegenskaper](/help/forms/assets/configure-icon.svg) -ikon. Dialogrutan Adaptiv formulärbehållare öppnas.

1. Klicka på  **[!UICONTROL Submission]** -fliken.

   ![Klicka på skiftningsikonen för att öppna dialogrutan Adaptiv formulärbehållare och konfigurera en sändningsåtgärd](/help/forms/assets/adaptive-forms-submit-message.png)

1. Välj och konfigurera en **[!UICONTROL Submit action]**, baserat på era behov.

Du kan också konfigurera olika åtgärder för att skicka in anpassade formulär.
* **Omdirigerings-URL/sökväg** - Med det här alternativet kan användaren konfigurera en sida för varje formulär som formuläranvändarna omdirigeras till efter att ha skickat in ett adaptivt formulär.
* **Visa meddelande** - Med det här alternativet kan användare lägga till ett meddelande som visas när det adaptiva formuläret har skickats. Den fördefinierade texten tas med i dialogrutan och kan ändras av användaren.

Mer information om följande Skicka-åtgärder finns i:

* [Skicka e-post](/help/forms/configure-submit-action-send-email.md)
* [Anropa ett Power Automate-flöde](/help/forms/forms-microsoft-power-automate-integration.md)
* [Skicka till SharePoint](/help/forms/configure-submit-action-sharepoint.md)
* [Anropa en Workfront Fusion](/help/forms/submit-adaptive-form-to-workfront-fusion.md)
* [Skicka med formulärdatamodell](/help/forms/using-form-data-model.md)
* [Skicka till Azure Blob Storage](/help/forms/configure-submit-action-azure-blob-storage.md)
* [Skicka till REST-slutpunkt](/help/forms/configure-submit-action-restpoint.md)
* [Skicka till OneDrive](/help/forms/configure-submit-action-onedrive.md)
* [Anropa ett AEM](/help/forms/configure-submit-action-workflow.md)

Du kan även skicka ett adaptivt formulär till andra lagringskonfigurationer:

* [Ansluta anpassat formulär till Salesforce-program](/help/forms/oauth2-client-credentials-flow-for-server-to-server-integration.md)
* [Ansluta ett anpassat formulär till Microsoft® Dynamics OData](/help/forms/ms-dynamics-odata-configuration.md)

Du kan [anpassa standardåtgärderna för att skicka](custom-submit-action-form.md). Dessutom kan du anpassa Skicka-åtgärder så att de passar specifika organisatoriska krav.


<!--
## Send Email {#send-email}

To send an email to one or more recipients upon successful submission of the form, you can use the **[!UICONTROL Send Email]** Submit Action. 

Refer to [configure the send email submit action for an Adaptive Form](/help/forms/configure-submit-action-send-email.md) to learn how to set up an Adaptive Form to send an email upon successful submission.
[!NOTE]
>
>Send PDF via Email Submit Action is applicable only to Adaptive Forms that use XFA template as form model. 

>[!NOTE]
>
>Ensure that the [AEM_Installation_Directory]\crx-quickstart\temp\datamanager\ASM folder
>exists. The directory is required to temporarily store attachments. If the directory does not exist, create it.


>[!CAUTION]
>
>If you  [prefill](prepopulate-adaptive-form-fields.md) a form template,  a Form Data Model or schema based Adaptive Form with XML or JSON data complaint to a schema (XML schema, JSON schema , form template, or form data model) that is data does not contain &lt;afData&gt;, &lt;afBoundData&gt;, and &lt;/afUnboundData&gt; tags, then the data of unbounded fields (Unbounded fields are Adaptive Form fields without [bindref](prepopulate-adaptive-form-fields.md) property) of the Adaptive Form is lost. 

>[!CAUTION]
>
>If you [prefill](prepopulate-adaptive-form-fields.md) a form template, a Form Data Model or schema based Adaptive Form with XML or JSON data complaint to a schema (XML schema, JSON schema, or form data model) that does not contain &lt;afData&gt;, &lt;afBoundData&gt;, and &lt;/afUnboundData&gt; tags, then the data of unbounded fields (Unbounded fields are Adaptive Form fields without [bindref](prepopulate-adaptive-form-fields.md) property) of the Adaptive Form is lost.

## Submit to Microsoft® SharePoint {#submit-to-sharedrive}

The **[!UICONTROL Submit to SharePoint]** Submit Action connects an Adaptive Form with a Microsoft&reg; SharePoint Storage. You can submit the form data files, attachments, or Document of Record to the connected Microsoft&reg; Sharepoint Storage. 

Integration of AEM Adaptive Form with Microsoft® SharePoint enables the submission, retrieval, or storage of data, files, and other relevant information within the SharePoint storage. To learn how to configure submit to SharePoint submit action for an Adaptive Form, [click here.](/help/forms/configure-submit-action-sharepoint.md) 

## Submit using Form Data Model {#submit-using-form-data-model}

The **[!UICONTROL Submit using Form Data Model]** Submit Action writes submitted Adaptive Form data for the specified data model object in a Form Data Model to its data source. When configuring the Submit Action, you can choose a data model object whose submitted data you want to write back to its data source.

When a user submits a form based on a form data model, you can [configure the form to write the submitted data to the data sources associated with the data model object.](/help/forms/using-form-data-model.md#write-submitted-adaptive-form-data-into-data-sources-write-af)

## Submit to REST endpoint {#submit-to-rest-endpoint}

The **[!UICONTROL Submit to REST Endpoint]** submit action sends the submitted data to a REST URL. This URL can be either an internal server (the server where the form is displayed) or an external server. The data of an Adaptive Form is submitted to a REST URL using the **[!UICONTROL Submit to REST endpoint]** Submit Action.

For a comprehensive guide on the detailed steps to post or submit data to a REST URL, refer to [configure submit to REST Endpoint submit action for Adaptive Forms.](/help/forms/configure-submit-action-restpoint.md)

## Invoke an AEM Workflow {#invoke-an-aem-workflow}

The **[!UICONTROL Invoke an AEM Workflow]** Submit Action integrates an Adaptive Form with an [AEM Workflow](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=en#extending-aem). When a form is submitted, the selected workflow starts automatically. 

 [Integrate AEM Adaptive Form with AEM Workflow: Streamlining Business Processes](/help/forms/configure-submit-action-workflow.md) provides step-by-step instructions to seamlessly integrate AEM Workflow with Adaptive Forms, optimizing business processes and enhancing workflow automation.

## Submit to OneDrive {#submit-to-onedrive}

The **[!UICONTROL Submit to OneDrive]** Submit Action connects an Adaptive Form with a Microsoft&reg; OneDrive. You can submit the form data, files, attachments, or Document of Record to the connected Microsoft&reg; OneDrive Storage. 

AEM Forms Cloud Service with Microsoft® OneDrive helps in optimize data submission. Explore the steps of [integrating OneDrive with AEM Forms](/help/forms/configure-submit-action-onedrive.md) for streamlined and secure storage.

## Submit to Azure Blob Storage {#submit-to-azure-blob-storage}

The **[!UICONTROL Submit to Azure Blob Storage]** Submit Action connects an Adaptive Form with a Microsoft® Azure portal and allows you to submit various elements such as form data, files, attachments, or Document of Record to the associated Azure Storage containers.

AEM as a Cloud Service allows submitting data to Azure Storage from AEM Adaptive Forms. Learn how to [create and use Azure Blob Storage configuration in AEM Forms](/help/forms/configure-submit-action-azure-blob-storage.md) for efficient data storage. 

To set values of a configuration, [Generate OSGi Configurations using the AEM SDK](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#generating-osgi-configurations-using-the-aem-sdk-quickstart), and [deploy the configuration](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#deployment-process) to your Cloud Service instance.

## Submit to Power Automate {#microsoft-power-automate}

You can configure an Adaptive Form to run a Microsoft&reg; Power Automate Cloud Flow on submission. The configured Adaptive Form sends captured data, attachments, and Document Of Record to Power Automate Cloud Flow for processing. It helps you build custom data capture experience while harnessing the power of Microsoft&reg; Power Automate to build business logics around captured data and automate customer workflows. 
Adaptive Forms editor provides the **Invoke a Microsoft&reg; Power Automate flow** submit action to send adaptive forms data, attachments, and Document Of Record to Power Automate Cloud Flow. To use the Submit action to send captured data to Microsoft&reg; Power Automate, [Connect your Forms as a Cloud Service instance with Microsoft&reg; Power Automate](forms-microsoft-power-automate-integration.md)  

After a successful configuration, use the [Invoke a Microsoft&reg; Power Automate flow](forms-microsoft-power-automate-integration.md#use-the-invoke-a-microsoft&reg;-power-automate-flow-submit-action-to-send-data-to-a-power-automate-flow-use-the-invoke-microsoft-power-automate-flow-submit-action) submit action to send data to a Power Automate Flow.  

## Submit to Workfront Fusion {#workfront-fusion}

You can configure an Adaptive Form to submit data to Workfront Fusion on submission. Workfront Fusion allows automation of processes so that user can concentrate on new tasks rather than repeating the same tasks again and again. It automates both simple and complex tasks, saving time and ensuring consistent process execution.

The Adaptive Forms editor provides the **Invoke a WorkFront Fusion Scenario** submit action to send Adaptive Forms data or attachments to a Workfront Fusion scenario. To use the submit action for sending captured data to a Workfront Fusion scenario, refer to [Submit an Adaptive Form to Adobe Workfront Fusion](/help/forms/submit-adaptive-form-to-workfront-fusion.md).

## Send PDF via Email {#send-pdf-via-email}

The **Send PDF via Email** Submit Action sends an email with a PDF containing form data, to one or more recipients on successful submission of the form.

>[!NOTE]
>
>This Submit Action is available for XFA-based Adaptive Forms and XSD-based adaption forms that have the Document of Record template. 
## Invoke a forms workflow {#invoke-a-forms-workflow}

The **Submit to Forms workflow** submit option sends a data xml and file attachments (if any) to an existing Adobe LiveCycle or [!DNL AEM Forms] on JEE process.

For information about how to configure the Submit to forms workflow Submit Action, see [Submitting and processing your form data using forms workflows](submit-form-data-livecycle-process.md). 
## Forms Portal Submit Action {#forms-portal-submit-action}

The **Forms Portal Submit Action** option makes form data available through an [!DNL AEM Forms] portal.

For more information about the Forms Portal and Submit Action, see [Drafts and submissions component](draft-submission-component.md). 

## Use synchronous or asynchronous submission {#use-synchronous-or-asynchronous-submission}

A Submit Action can use synchronous or asynchronous submission.

**Synchronous submission**: Traditionally, web forms are configured to submit synchronously. In a synchronous submission, when users submit a form, they are redirected to an acknowledgment page, a thank you page, or if there is submission failure, an error page. You can select the **[!UICONTROL Use asynchronous submission]** option to redirect the users to a webpage or show a message on submission.  

![Configure Submit Action](assets/thank-you-setting.png)

**Asynchronous submission**: Modern web experiences like single page applications are gaining popularity where the web page remains static while client-server interaction happens in the background. You can now provide this experience with Adaptive Forms by [configuring asynchronous submission](asynchronous-submissions-adaptive-forms.md).

## Server-Side Revalidation in Adaptive Form {#server-side-revalidation-in-adaptive-form}

Typically, in any online data capture system, developers place someJavaScript validations on client side to enforce a few business rules. But in modern browsers, end users have way to bypass those validations and manually do submissions using various techniques, Such as Web Browser DevTools Console. Such techniques are also valid for Adaptive Forms. A forms developer can create various validation logics, but technically, end users can bypass those validation logics and submit invalid data to the server. Invalid data would break the business rules that a form author has enforced.

The server-side revalidation feature provides the ability to run the validations that an Adaptive Forms author has provided while designing an Adaptive Form on the server. It prevents any possible compromise of data submissions and business rules violations represented in terms of form validations.

### What to validate on Server? {#what-to-validate-on-server-br}

All out of the box (OOTB) field validations of an Adaptive Form that are rerun at the server are:

* Required
* Validation Picture Clause
* Validation Expression

### Enabling Server-side Validation {#enabling-server-side-validation-br}

Use the **[!UICONTROL Revalidate on server]** under Adaptive Form Container in the sidebar to enable or disable server-side validation for the current form.

![Enabling Server-Side Validation](assets/revalidate-on-server.png)

Enabling Server-Side Validation

If end-user bypass those validations and submit the forms, the server again performs the validation. If the validation fails at server end, then the submit transaction is stopped. The user is presented with the original form again. The captured data and submitted data are presented to the user as an error.

>[!NOTE]
>
>Server-side validation validates the form model. You are recommended to create a separate client library for validations and not mix it with other things like HTML styling and DOM manipulation in the same client library.
-->

## Felhantering vid Skicka-åtgärd {#error-handling-on-submit-action}

Som en del av AEM riktlinjer för säkerhet och skärpa konfigurerar du anpassade felsidor som 400.jsp, 404.jsp och 500.jsp. Dessa hanterare anropas när ett formulär 400-, 404- eller 500-fel skickas. Hanterarna anropas också när dessa felkoder aktiveras på noden Publicera. Du kan också skapa JSP-sidor för andra HTTP-felkoder.

När du förifyller en formulärdatamodell eller ett schemabaserat adaptivt formulär med XML- eller JSON-data klagar till ett schema som inte innehåller data `<afData>`, `<afBoundData>`och `</afUnboundData>` -taggar, försvinner data i obegränsade fält i det adaptiva formuläret. Schemat kan vara ett XML-schema, JSON-schema eller en formulärdatamodell. Obegränsade fält är adaptiva formulärfält utan `bindref` -egenskap.

<!-- For more information, see [Customizing Pages shown by the Error Handler](/help/sites-developing/customizing-errorhandler-pages.md). -->


<!--
## See next

* [Create style or themes for your forms](using-themes-in-core-components.md)
* [Create an Adaptive Form (core components)](/help/forms/creating-adaptive-form-core-components.md)
* [Create a custom Submit Action for Adaptive Forms](/help/forms/custom-submit-action-form.md)

-->

## Se även {#see-also}

{{see-also}}


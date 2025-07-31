---
title: Hur konfigurerar man en Skicka-åtgärd för ett anpassat formulär?
description: Ett anpassat formulär innehåller flera överföringsåtgärder. En Skicka-åtgärd definierar hur ett anpassat formulär ska bearbetas när det har skickats in. Du kan använda inbyggda Skicka-åtgärder eller skapa egna.
feature: Adaptive Forms, Foundation Components, Edge Delivery Services, Core Components
role: User, Developer
source-git-commit: c0df3c6eaf4e3530cca04157e1a5810ebf5b4055
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 0%

---


# Skicka åtgärder som stöds av Adaptive Forms

Med adaptiva Forms kan du skapa engagerande, responsiva, dynamiska och anpassningsbara formulär. De har ett intuitivt användargränssnitt och en uppsättning färdiga komponenter för effektiv formulärdesign och hantering. Du kan konfigurera olika skicka-åtgärder för att skicka formulärdata till tjänster som OneDrive, SharePoint, Workfront Fusion med flera.

En sändningsåtgärd utlöses när en användare klickar på knappen **[!UICONTROL Submit]** i ett anpassat formulär. Forms as a Cloud Service innehåller flera inskickningsåtgärder. De inbyggda Skicka-åtgärderna ger dig möjlighet att:

* Skicka enkelt formulärdata via e-post
* Initiera Microsoft® Power Automate-flöden eller AEM-arbetsflöden när data skickas.
* Skicka formulärdata direkt till Microsoft® SharePoint Server, Microsoft® Azure Blob Storage eller Microsoft® OneDrive.
* Skicka smidigt data till en konfigurerad datakälla med hjälp av FDM (Form Data Model).
* Skicka enkelt data till en REST-slutpunkt.

## Skicka åtgärder som stöds av Adaptive Forms

AEM-formulär innehåller följande färdiga inlämningsåtgärder:

* [Skicka e-post](/help/forms/configure-submit-action-send-email.md)
* [Anropa ett Power Automate-flöde](/help/forms/forms-microsoft-power-automate-integration.md)
* [Skicka till SharePoint](/help/forms/configure-submit-action-sharepoint.md)
* [Anropa en Workfront Fusion](/help/forms/submit-adaptive-form-to-workfront-fusion.md)
* [Skicka med hjälp av formulärdatamodell (FDM)](/help/forms/using-form-data-model.md)
* [Skicka till Azure Blob Storage](/help/forms/configure-submit-action-azure-blob-storage.md)
* [Skicka till REST-slutpunkt](/help/forms/configure-submit-action-restpoint.md)
* [Skicka till OneDrive](/help/forms/configure-submit-action-onedrive.md)
* [Starta ett AEM-arbetsflöde](/help/forms/configure-submit-action-workflow.md)
* [Skicka till Marketo](/help/forms/submit-adaptive-form-to-marketo-engage.md)
* [Skicka till Adobe Experience Platform (AEP)](/help/forms/aem-forms-aep-connector.md)
* [Skicka till kalkylblad](/help/forms/forms-submission-service.md)

Du kan även skicka ett adaptivt formulär till andra lagringskonfigurationer:

* [Ansluta anpassat formulär till Salesforce](/help/forms/aem-forms-salesforce-integration.md)
* [Ansluta ett adaptivt formulär till Microsoft](/help/forms/ms-dynamics-odata-configuration.md)

## Skicka åtgärdsstöd för olika redigeringstyper

Tabellen nedan visar vilka skicka-åtgärder som stöds baserat på den formulärredigeringsmetod som används i AEM Forms:

| Skicka åtgärd | [Foundation Components](/help/forms/configuring-submit-actions.md) | [Kärnkomponenter](/help/forms/configure-submit-actions-core-components.md) | [Universell redigerare](/help/forms/configure-submit-action-eds-forms.md#submit-actions-supported-by-adaptive-forms-created-in-universal-editor) | [Dokumentbaserad Forms](/help/forms/configure-submit-action-eds-forms.md#supported-submit-actions-for-document-based-forms) |
|----------------------------|------------------------|------------------|------------------|------------------------|
| Skicka e-post | ✅ stöds | ✅ stöds | ✅ stöds |                        |
| Power Automate Flow | ✅ stöds | ✅ stöds | ✅ stöds |                        |
| Skicka till SharePoint | ✅ stöds | ✅ stöds | ✅ stöds |                        |
| Workfront Fusion | ✅ stöds | ✅ stöds | ✅ stöds |                        |
| Skicka med FDM | ✅ stöds | ✅ stöds | ✅ stöds |                        |
| Skicka till AEP | ✅ stöds | ✅ stöds | ✅ stöds |                        |
| Azure Blob Storage | ✅ stöds | ✅ stöds | ✅ stöds |                        |
| Skicka till REST-slutpunkt | ✅ stöds | ✅ stöds | ✅ stöds |                        |
| Skicka till Marketo Engage | ✅ stöds | ✅ stöds | ✅ stöds |                        |
| Skicka till OneDrive | ✅ stöds | ✅ stöds | ✅ stöds |                        |
| Anropa AEM Workflow | ✅ stöds | ✅ stöds | ✅ stöds |                        |
| Skicka till kalkylblad |                        |                  | ✅ stöds | ✅ stöds |


## Förtroende på serversidan i adaptiv form

I alla onlinesystem för datainhämtning lägger utvecklare vanligtvis in JavaScript-valideringar på klientsidan för att tillämpa några få affärsregler. Men i moderna webbläsare kan slutanvändarna kringgå valideringarna och skicka in dokument manuellt med hjälp av olika tekniker, till exempel DevTools Console för webbläsare. Sådana tekniker gäller även för Adaptive Forms. En formulärutvecklare kan skapa olika valideringslogik, men tekniskt sett kan slutanvändarna kringgå dessa valideringslogik och skicka ogiltiga data till servern. Ogiltiga data skulle bryta mot de affärsregler som en formulärförfattare har infört.

Med funktionen för omvalidering på serversidan kan du även köra de valideringar som en adaptiv Forms-författare har tillhandahållit när han eller hon utformar ett adaptivt formulär på servern. Det förhindrar att inskickade data äventyras och affärsregelöverträdelser som representeras i form av formulärvalidering.


### Vad ska valideras på servern?

Alla valideringar av ett adaptivt formulär som körs på servern i fältet OOTB (OOTB) är:

* Obligatoriskt
* Valideringsbildsats
* Valideringsuttryck

Använd **[!UICONTROL Revalidate on server]** under Adaptiv formulärbehållare i sidlisten för att aktivera eller inaktivera validering på serversidan för det aktuella formuläret.

![Aktivera validering på serversidan](assets/revalidate-on-server.png)

**Aktivera validering på serversidan**

Om slutanvändaren åsidosätter dessa valideringar och skickar formulären utför servern valideringen igen. Om valideringen misslyckas vid serverslutet stoppas skicka-transaktionen. Användaren får det ursprungliga formuläret igen. Insamlade data och skickade data visas för användaren som ett fel.

>[!NOTE]
>
>Validering på serversidan validerar formulärmodellen. Du rekommenderas att skapa ett separat klientbibliotek för validering och inte blanda det med andra saker som HTML-formatering och DOM-manipulering i samma klientbibliotek.

<!--### Supporting Custom functions in Validation Expressions {#supporting-custom-functions-in-validation-expressions-br}

At times, if there are **complex validation rules**, the exact validation script reside in custom functions and author calls these custom functions from field validation expression. To make this custom function library known and available while performing server-side validations, the form author can configure the name of AEM client library under the **[!UICONTROL Basic]** tab of Adaptive Form Container properties as shown below.

![Supporting Custom functions in Validation Expressions](assets/clientlib-cat.png)

Supporting Custom functions in Validation Expressions

Author can configure customJavaScript library per Adaptive Form. In the library, only keep the reusable functions, which have dependency on jquery and underscore.js third-party libraries.

Refer to the following articles to learn how to create custom functions for:

* [Adaptive Forms based on Foundation Components](/help/forms/rule-editor.md#custom-functions-in-rule-editor)
* [Adaptive Forms based on Core Components](/help/forms/create-and-use-custom-functions.md)
* [Adaptive Forms authored using Document-Based Authoring](/help/edge/docs/forms/rules-forms.md#create-a-custom-function)
* [Adaptive Forms created using the Universal Editor](/help/edge/docs/forms/universal-editor/rule-editor-universal-editor.md#create-a-custom-function)

## Error handling on Submit Action {#error-handling-on-submit-action}

As a part of AEM security and hardening guidelines, configure custom error pages such as 400.jsp, 404.jsp, and 500.jsp. These handlers are called, when on submitting a form 400, 404, or 500 errors appear. The handlers are also called when these error codes are triggered on the Publish node. You can also create JSP pages for other HTTP error codes.

When you prefill a form data model (FDM), or schema based Adaptive Form with XML or JSON data complaint to a schema that is data does not contain `<afData>`, `<afBoundData>`, and `</afUnboundData>` tags, then the data of unbounded fields of the Adaptive Form is lost. The schema can be an XML schema, JSON schema, or a Form Data Model (FDM). Unbounded fields are Adaptive Form fields without the `bindref` property.-->

## Se även

{{af-submit-action}}


---
title: Hur konfigurerar jag en Skicka-åtgärd för ett anpassat formulär?
description: Ett anpassat formulär innehåller flera överföringsåtgärder. En Skicka-åtgärd definierar hur ett anpassat formulär ska bearbetas när det har skickats in. Du kan använda inbyggda Skicka-åtgärder eller skapa egna.
keywords: hur du väljer en åtgärd för att skicka ett anpassat formulär, kopplar ett anpassat formulär till SharePoint-listan, ansluter ett anpassat formulär till SharePoint-dokumentbiblioteket, ansluter ett anpassat formulär till formulärdatamodellen (FDM)
feature: Adaptive Forms, Edge Delivery Services
role: User, Developer
source-git-commit: c0df3c6eaf4e3530cca04157e1a5810ebf5b4055
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 0%

---


# Skicka funktionsmakron för Edge Delivery Services Forms

| Version | Artikellänk |
|---------|-----------------------------|
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/configuring-submit-actions.html?lang=sv-SE) |
| AEM as a Cloud Service (Foundation Components) | [Klicka här](/help/forms/configuring-submit-actions.md) |
| AEM as a Cloud Service (kärnkomponenter) | [Klicka här](/help/forms/configure-submit-actions-core-components.md) |
| AEM as a Cloud Service (Edge Delivery Services) | Den här artikeln |

Inlämningsåtgärder definierar vad som händer när en användare skickar ett formulär, t.ex. när data lagras, arbetsflöden utlöses eller integreras med tredjepartssystem. Vilken typ av överföringsåtgärder du kan konfigurera beror på vilken redigeringsmetod som används för att skapa Edge Delivery Services Forms.

Du kan skapa Edge Delivery Services Forms med [Universal Editor](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md) eller med hjälp av [dokumentbaserad Forms](/help/edge/docs/forms/overview.md)-redigering och konfigurera formulären med olika överföringsåtgärder.

## Skicka funktionsmakron för Forms som har skapats i Universal Editor

Följande inskickningsåtgärder stöds av [Adaptiv Forms som har skapats i Universal Editor](/help/edge/docs/forms/universal-editor/create-forms.md):

* [Skicka e-post](/help/forms/configure-submit-action-send-email.md)
* [Anropa ett Power Automate-flöde](/help/forms/forms-microsoft-power-automate-integration.md)
* [Skicka till SharePoint](/help/forms/configure-submit-action-sharepoint.md)
* [Anropa Workfront Fusion](/help/forms/submit-adaptive-form-to-workfront-fusion.md)
* [Skicka med hjälp av formulärdatamodell (FDM)](/help/forms/using-form-data-model.md)
* [Skicka till Azure Blob Storage](/help/forms/configure-submit-action-azure-blob-storage.md)
* [Skicka till REST-slutpunkt](/help/forms/configure-submit-action-restpoint.md)
* [Skicka till OneDrive](/help/forms/configure-submit-action-onedrive.md)
* [Starta ett AEM-arbetsflöde](/help/forms/configure-submit-action-workflow.md)
* [Skicka till Marketo Engage](/help/forms/submit-adaptive-form-to-marketo-engage.md)
* [Skicka till Adobe Experience Platform (AEP)](/help/forms/aem-forms-aep-connector.md)
* [Skicka till kalkylblad](/help/forms/forms-submission-service.md)

<!--You can also submit an Adaptive Form in the Universal Editor to other storage or CRM integrations:

* [Connect Adaptive Form to Salesforce](/help/forms/aem-forms-salesforce-integration.md)
* [Connect an Adaptive Form to Microsoft&reg; Dynamics OData](/help/forms/ms-dynamics-odata-configuration.md)-->

Du kan konfigurera åtgärden skicka för formulär som har skapats i den universella redigeraren med fliken **Skicka** i tillägget **Redigera formuläregenskaper** .

<!--**How to Configure Submit Action for Forms authored in Universal Editor?**
You can configure the submit action for forms created in the Universal Editor using the **Submission** tab of the **Edit Form Properties** extension.

![Form properties icon](/help/forms/assets/ue-form-properties-icon.png)

![Universal Editor Form Properties](/help/forms/assets/ue-form-properties.png)-->

>[!NOTE]
>
> * Om ikonen **Redigera formuläregenskaper** inte visas i det universella redigeringsgränssnittet aktiverar du tillägget **Redigera formuläregenskaper** i Extension Manager.
> * Läs artikeln [Extension Manager Feature Highlights](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions) om du vill veta hur du aktiverar eller inaktiverar tillägg i den universella redigeraren.

## Skicka funktionsmakron för dokumentbaserad Forms

Dokumentbaserad Forms kan endast skickas till kalkylblad. Mer information om hur du konfigurerar kalkylbladet så att det tar emot skickade data finns i instruktionerna i [Konfigurera dina Google-blad eller Microsoft Excel-filer så att du kan börja ta emot data](/help/edge/docs/forms/submit-forms.md) -artikeln.

## Se även {#see-also}

{{af-submit-action}}


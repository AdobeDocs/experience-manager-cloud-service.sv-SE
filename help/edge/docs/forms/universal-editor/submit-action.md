---
title: Hur konfigurerar jag en Skicka-åtgärd för ett anpassat formulär?
description: Ett anpassat formulär innehåller flera överföringsåtgärder. En Skicka-åtgärd definierar hur ett anpassat formulär ska bearbetas när det har skickats in. Du kan använda inbyggda Skicka-åtgärder eller skapa egna.
keywords: hur du väljer en åtgärd för att skicka ett anpassat formulär, kopplar ett anpassat formulär till SharePoint-listan, ansluter ett anpassat formulär till SharePoint-dokumentbiblioteket, ansluter ett anpassat formulär till formulärdatamodellen (FDM)
feature: Adaptive Forms, Edge Delivery Services
role: User, Developer
source-git-commit: cfff846e594b39aa38ffbd3ef80cce1a72749245
workflow-type: tm+mt
source-wordcount: '414'
ht-degree: 0%

---

# Inlämningsåtgärd för anpassat formulär

| Version | Artikellänk |
|---------|-----------------------------|
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/configuring-submit-actions.html) |
| AEM as a Cloud Service (Foundation Components) | [Klicka här](/help/forms/configuring-submit-actions.md) |
| AEM as a Cloud Service (kärnkomponenter) | [Klicka här](/help/forms/configure-submit-actions-core-components.md) |
| AEM as a Cloud Service (Edge Delivery Services) | Den här artikeln |


Inlämning av blanketter är det avgörande steget i användarens resa - där insamlade data behandlas och åtgärder vidtas. Det här dokumentet innehåller en omfattande guide till hur du konfigurerar och hanterar Skicka-åtgärder för Adaptive Forms i Universal Editor.

### Vad du kommer att lära dig

I slutet av det här dokumentet kommer du att förstå hur du:

- Konfigurera olika typer av skicka-åtgärder för formulären
- Ställ in REST-slutpunktsöverföringar för integrering med externa system
- Konfigurera e-postöverföringar för formulärsvar
- Implementera anpassade skicka-åtgärder för specifika affärsbehov
- Hantera formulärvalidering och felscenarier vid inlämning

### Målgrupp

Den här guiden är utformad för:

- **Formulärutvecklare** som implementerar inskickningslogik
- **Systemintegratörer** ansluter formulär till backend-system
- **Affärsanalytiker** definierar formulärarbetsflöden
- **Teknikarkitekter** formger formuläröverföringsprocesser

## Skicka funktionsmakron för Forms som har skapats i Universal Editor

Följande inskickningsåtgärder stöds av [Adaptiv Forms som har skapats i Universal Editor](/help/edge/docs/forms/universal-editor/create-forms.md):

- [Skicka e-post](/help/forms/configure-submit-action-send-email.md)
- [Anropa ett Power Automate-flöde](/help/forms/forms-microsoft-power-automate-integration.md)
- [Skicka till SharePoint](/help/forms/configure-submit-action-sharepoint.md)
- [Anropa Workfront Fusion](/help/forms/submit-adaptive-form-to-workfront-fusion.md)
- [Skicka med hjälp av formulärdatamodell (FDM)](/help/forms/integrate-adaptive-form-with-fdm.md)
- [Skicka till Azure Blob Storage](/help/forms/configure-submit-action-azure-blob-storage.md)
- [Skicka till REST-slutpunkt](/help/forms/configure-submit-action-restpoint.md)
- [Skicka till OneDrive](/help/forms/configure-submit-action-onedrive.md)
- [Starta ett AEM-arbetsflöde](/help/forms/configure-submit-action-workflow.md)
- [Skicka till Marketo Engage](/help/forms/submit-adaptive-form-to-marketo-engage.md)
- [Skicka till Adobe Experience Platform (AEP)](/help/forms/aem-forms-aep-connector.md)
- [Skicka till kalkylblad](/help/forms/forms-submission-service.md)

<!--You can also submit an Adaptive Form in the Universal Editor to other storage or CRM integrations:

* [Connect Adaptive Form to Salesforce](/help/forms/aem-forms-salesforce-integration.md)
* [Connect an Adaptive Form to Microsoft&reg; Dynamics OData](/help/forms/ms-dynamics-odata-configuration.md)-->

Du kan konfigurera åtgärden skicka för formulär som har skapats i den universella redigeraren med fliken **Skicka** i tillägget **Redigera formuläregenskaper** .

**Hur konfigurerar jag Skicka-åtgärd för Forms som har skapats i Universal Editor?**
Du kan konfigurera åtgärden skicka för formulär som har skapats i den universella redigeraren på fliken **Skicka** i tillägget **Redigera formuläregenskaper** .

![Ikon för formuläregenskaper](/help/forms/assets/ue-form-properties-icon.png)

![Formuläregenskaper för Universal Editor](/help/forms/assets/ue-form-properties.png)

>[!NOTE]
>
> - Om ikonen **Redigera formuläregenskaper** inte visas i det universella redigeringsgränssnittet aktiverar du tillägget **Redigera formuläregenskaper** i Extension Manager.
> - Läs artikeln [Extension Manager Feature Highlights](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions) om du vill veta hur du aktiverar eller inaktiverar tillägg i den universella redigeraren.




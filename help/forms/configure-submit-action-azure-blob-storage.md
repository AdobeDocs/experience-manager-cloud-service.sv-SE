---
Title: How to connect AEM Adaptive Forms with Azure Blob Storage?
Description: Learn how to create an Azure Blob Storage Configuration in AEM Forms and use it within your Adaptive Forms for efficient data storage.
keywords: Azure Blob Storage-integrering med AEM Forms, skicka data till Azure Storage, skapa Azure Storage-konfiguration i AEM Forms, använda Azure Blob Storage i adaptiv Forms Submit Action
feature: Adaptive Forms, Foundation Components, Edge Delivery Services, Core Components
exl-id: 0c9f8f85-c4e9-4c79-bd0b-abdcac99a2d4
title: Hur konfigurerar man en Skicka-åtgärd för ett anpassat formulär?
role: User, Developer
source-git-commit: c0df3c6eaf4e3530cca04157e1a5810ebf5b4055
workflow-type: tm+mt
source-wordcount: '733'
ht-degree: 1%

---

# Skicka ett anpassat formulär till Azure Blob Storage

Åtgärden **[!UICONTROL Submit to Azure Blob Storage]** för att skicka kopplar ett anpassat formulär till en Microsoft® Azure-portal. Du kan skicka formulärdata, filer, bilagor eller arkivdokument till de anslutna Azure Storage-behållarna.

AEM as a Cloud Service erbjuder olika inskickningsåtgärder för att hantera inskickade formulär. Du kan läsa mer om de här alternativen i artikeln [Åtgärd för att skicka anpassade formulär](/help/forms/aem-forms-submit-action.md).

## Fördelar

Några av fördelarna med Azure Blob Storage-integrering med AEM Forms är:

* Det underlättar när det gäller att effektivisera processen att skicka data, filer, bilagor och arkivdokument till Azure-lagringsbehållare.
* Den använder Azure Blob Storage för centraliserad och ordnad lagring av inskickade adaptiva formulär.

## Anslut AEM Forms med Microsoft® Azure Blob Storage

Så här använder du Azure Blob Storage i Adaptive Forms Submit Action:

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
<!--

    >[!NOTE]
    >
    > The URL for **[!UICONTROL Azure Blob Endpoint]** is automatically appended to the textbox when a value is entered for **[!UICONTROL Azure Storage Account]**. You can update the Azure Blob End Point URL with your custom domain. Steps to update URL for **[!UICONTROL Azure Blob End Point]**:
    > 1. [Enable the AEM Advance Networking VPN support](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/networking/advanced-networking.html?lang=sv-SE)
    > 1. [Enable dedicated egress IP link](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/networking/advanced-networking.html?lang=sv-SE)
    > 1. [Map custom domain to azure blob storage](https://learn.microsoft.com/en-us/azure/storage/blobs/storage-custom-domain-name?tabs=azure-portal)
-->

1. Klicka på **[!UICONTROL Save]**.

Nu kan du använda den här Azure Storage-behållarkonfigurationen för överföringsåtgärden i ett adaptivt formulär.

### Använd Azure Storage-konfigurationen i ett adaptivt formulär {#use-azure-storage-configuartion-in-af}

Du kan använda den skapade Azure Storage-behållarkonfigurationen i ett adaptivt formulär för att spara data eller skapa ett dokument av posten i Azure Storage-behållaren.

>[!NOTE]
>
> * Välj samma [!UICONTROL Configuration Container] för ett adaptivt formulär, där du har skapat ditt OneDrive-lagringsutrymme.
> * Om [!UICONTROL Configuration Container] inte är markerat visas de globala [!UICONTROL Storage Configuration]-mapparna i egenskapsfönstret för Skicka åtgärd.

>[!BEGINTABS]

>[!TAB Foundation Component]

Utför följande steg för att använda konfigurationen av Azure Storage-behållaren i ett adaptivt formulär baserat på Foundation-komponenter som:

1. Öppna det adaptiva formuläret för redigering och navigera till avsnittet **[!UICONTROL Submission]** i egenskaperna för den adaptiva formulärbehållaren.
1. I listrutan **[!UICONTROL Submit Action]** väljer du **[!UICONTROL Submit to Azure Blob Storage]**.

   ![Azure Blob Storage GIF](/help/forms/assets/submit-to-azure-blob-fc.png){width=50%,height=50%}

   Du kan också spara DoR-dokument (Document of Record) i Azure Blob Storage.

1. Markera **[!UICONTROL Storage Configuration]** där du vill spara dina data.
1. Klicka på **[!UICONTROL Save]** om du vill spara Skicka-inställningarna.

När du skickar formuläret sparas data i den angivna Azure Storage-behållarkonfigurationen.
Mappstrukturen som data ska sparas i är `/configuration_container/form_name/year/month/date/submission_id/data`.

>[!TAB Kärnkomponent]

Utför följande steg för att använda konfigurationen av Azure Storage-behållaren i ett adaptivt formulär baserat på kärnkomponenter som:

1. Öppna innehållsläsaren och markera komponenten **[!UICONTROL Guide Container]** i det adaptiva formuläret.
1. Klicka på ikonen för egenskaper för stödlinjebehållaren ![Egenskaper för stödlinje](/help/forms/assets/configure-icon.svg) . Dialogrutan Adaptiv formulärbehållare öppnas.
1. Klicka på fliken **[!UICONTROL Submission]**.
1. I listrutan **[!UICONTROL Submit Action]** väljer du **[!UICONTROL Submit to Azure Blob Storage]**.

   ![Azure Blob Storage GIF](/help/forms/assets/azure-submit-video.gif)

   Du kan också spara DoR-dokument (Document of Record) i Azure Blob Storage.

1. Markera **[!UICONTROL Storage Configuration]** där du vill spara dina data.
1. Klicka på **[!UICONTROL Save]** om du vill spara Skicka-inställningarna.

När du skickar formuläret sparas data i den angivna Azure Storage-behållarkonfigurationen.
Mappstrukturen som data ska sparas i är `/configuration_container/form_name/year/month/date/submission_id/data`.

>[!TAB Universell redigerare]

Utför följande steg för att använda konfigurationen för Azure Storage-behållaren i ett adaptivt formulär som har skapats i den universella redigeraren:

1. Öppna det adaptiva formuläret för redigering.
1. Klicka på tillägget **Redigera formuläregenskaper** i redigeraren.
Dialogrutan **Formuläregenskaper** visas.

   >[!NOTE]
   >
   > * Om ikonen **Redigera formuläregenskaper** inte visas i det universella redigeringsgränssnittet aktiverar du tillägget **Redigera formuläregenskaper** i Extension Manager.
   > * Läs artikeln [Extension Manager Feature Highlights](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions) om du vill veta hur du aktiverar eller inaktiverar tillägg i den universella redigeraren.

1. Klicka på fliken **Skicka** och välj åtgärden **[!UICONTROL Submit to Azure Blob Storage]** Skicka.
   ![Azure Blob Storage](/help/forms/assets/azure-blob-storage-ue.png)

   Om du väljer **Spara bifogade filer med ursprungligt namn** lagras de bifogade filerna i mappen med sina ursprungliga filnamn. Du kan också spara DoR-dokument (Document of Record) i Azure Blob Storage.

1. Markera **[!UICONTROL Storage Configuration]** där du vill spara dina data.
1. Klicka på **[!UICONTROL Save&Close]** om du vill spara Skicka-inställningarna.

När du skickar formuläret sparas data i den angivna Azure Storage-behållarkonfigurationen.
Mappstrukturen som data ska sparas i är `/configuration_container/form_name/year/month/date/submission_id/data`.

>[!ENDTABS]

## Relaterade artiklar

{{af-submit-action}}

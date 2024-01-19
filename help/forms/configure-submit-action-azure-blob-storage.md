---
Title: How to connect AEM Adaptive Forms with Azure Blob Storage?
Description: Learn how to create an Azure Blob Storage Configuration in AEM Forms and use it within your Adaptive Forms for efficient data storage.
keywords: Azure Blob Storage-integrering med AEM Forms, skicka data till Azure Storage, skapa Azure Storage-konfiguration i AEM Forms, använda Azure Blob Storage i adaptiv Forms Submit Action
feature: Adaptive Forms, Core Components
source-git-commit: 8784c0bcd05eeae41a472faa5ecad03cbdd8a9b6
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 0%

---


# Skicka ett anpassat formulär till Azure Blob Storage

The **[!UICONTROL Submit to Azure Blob Storage]**  Skicka åtgärd kopplar ett anpassat formulär till en Microsoft® Azure-portal. Du kan skicka formulärdata, filer, bilagor eller arkivdokument till de anslutna Azure Storage-behållarna.

AEM as a Cloud Service erbjuder olika åtgärder för att skicka in formulär. Du kan läsa mer om de här alternativen i [Inlämningsåtgärd för anpassat formulär](/help/forms/configure-submit-actions-core-components.md) artikel.

## Fördelar

Några av fördelarna med Azure Blob Storage-integrering med AEM Forms är:

* Det underlättar när det gäller att effektivisera processen att skicka data, filer, bilagor och arkivdokument till Azure-lagringsbehållare.
* Den använder Azure Blob Storage för centraliserad och ordnad lagring av inskickade adaptiva formulär.

## Anslut AEM Forms med Microsoft® Azure Blob Storage

Så här använder du Azure Blob Storage i Adaptive Forms Submit Action:

1. [Skapa en Azure Blob Storage-behållare](#create-a-azure-blob-storage-container-create-azure-configuration): Den ansluter AEM Forms till Azure Storage-behållare.
2. [Använd Azure Storage-konfigurationen i ett adaptivt formulär](#use-azure-storage-configuration-in-an-adaptive-form-use-azure-storage-configuartion-in-af): Det kopplar ditt adaptiva formulär till konfigurerade Azure-lagringsbehållare.

### Skapa en Azure Blob Storage-behållare {#create-azure-configuration}

Så här ansluter du AEM Forms till dina Azure-lagringsbehållare:
1. Gå till **AEM Forms Author** instans > **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** >  **[!UICONTROL Azure Storage]**.
1. När du valt **[!UICONTROL Azure Storage]** omdirigeras du till **[!UICONTROL Azure Storage Browser]**.
1. Välj en **Konfigurationsbehållare**. Konfigurationen lagras i den valda konfigurationsbehållaren.
1. Klicka på **[!UICONTROL Create]**. Guiden Skapa Azure Storage Configuration visas.

   ![Azure Storage-konfiguration](/help/forms/assets/azure-storage-configuration.png)

1. Ange **[!UICONTROL Title]**, **[!UICONTROL Azure Storage Account]** och **[!UICONTROL Azure Access key]**.

   * Du kan hämta `Azure Storage Account` namn och `Azure Access key` från lagringskonton i Microsoft® Azure-portalen.

1. Klicka på **[!UICONTROL Save]**.

Nu kan du använda den här Azure Storage-behållarkonfigurationen för överföringsåtgärden i ett adaptivt formulär.

### Använd Azure Storage-konfigurationen i ett adaptivt formulär {#use-azure-storage-configuartion-in-af}

Du kan använda den skapade Azure Storage-behållarkonfigurationen i ett adaptivt formulär för att spara data eller skapa ett dokument av posten i Azure Storage-behållaren. Utför följande steg för att använda konfigurationen av Azure Storage-behållaren i ett adaptivt formulär som:
1. Skapa en [Adaptiv form](/help/forms/creating-adaptive-form-core-components.md).

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

## Relaterade artiklar

{{af-submit-action}}
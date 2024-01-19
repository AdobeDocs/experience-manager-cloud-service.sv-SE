---
Title: How to submit data from an Adaptive Form to Microsoft® OneDrive?
Description: Explore the streamlined process of connecting AEM Forms with Microsoft® OneDrive using the Submit to OneDrive Submit Action. Learn the step-by-step guide to configure OneDrive and set up submission actions for efficient data storage and retrieval
keywords: AEM Forms OneDrive-integrering, Anslut till Microsoft OneDrive, Konfigurationsinställningar för OneDrive med AEM formulär
feature: Adaptive Forms, Core Components
source-git-commit: 95af49839d206f67ac02116730229f5b0531c5bb
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 0%

---


# Skicka ett anpassat formulär till Microsoft® OneDrive

The **[!UICONTROL Submit to OneDrive]** Skicka åtgärd kopplar ett anpassat formulär till en Microsoft® OneDrive. Du kan skicka formulärdata, filer, bilagor eller arkivdokument till den anslutna Microsoft® OneDrive-lagringsplatsen.

AEM as a Cloud Service erbjuder olika åtgärder för att skicka in formulär. Du kan läsa mer om de här alternativen i [Inlämningsåtgärd för anpassat formulär](/help/forms/configure-submit-actions-core-components.md)  artikel.

## Fördelar

Några av fördelarna med smidig integrering av AEM Forms och Microsoft® OneDrive är:

* Enhetsövergripande åtkomst till OneDrive säkerställer att lagrade formulärdata är tillgängliga på olika plattformar. Användarna kan komma åt inskickade data, bilagor och dokument från stationära datorer, bärbara datorer, surfplattor och mobila enheter, vilket förbättrar tillgängligheten och flexibiliteten.
* OneDrive-integrering med AEM ger en tillförlitlig och skalbar lösning för effektiv datalagring. Alla inskickade anpassade formulär, som filer, bilagor och arkivdokument, kan enkelt sparas i OneDrive för att säkerställa att alla data är välorganiserade och tillgängliga.

## Ansluta OneDrive till en adaptiv

>[!VIDEO](https://video.tv.adobe.com/v/3424864/connect-aem-adaptive-form-to-onedrive/?quality=12&learn=on)

Så här konfigurerar du OneDrive för AEM Forms-överföring:

1. [Skapa en OneDrive-konfiguration](#create-a-onedrive-configuration-create-onedrive-configuration): Den ansluter AEM Forms till din Microsoft® OneDrive-lagring.
2. [Använd Skicka till OneDrive-åtgärden i ett anpassat formulär](#use-onedrive-configuration-in-an-adaptive-form-use-onedrive-configuartion-in-af): Det kopplar ditt adaptiva formulär till konfigurerade Microsoft® OneDrive.

### Skapa en OneDrive-konfiguration {#create-onedrice-configuration}

Så här ansluter du AEM Forms till din Microsoft® OneDrive-lagring:

1. Gå till **AEM Forms Author** instans > **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** >  **[!UICONTROL Microsoft® OneDrive]**.
1. När du valt **[!UICONTROL Microsoft® OneDrive]** omdirigeras du till **[!UICONTROL OneDrive Browser]**.
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

1. Klicka på **[!UICONTROL Connect]**. Vid en lyckad anslutning `Connection Successful` visas.

1. Välj nu **[!UICONTROL OneDrive Container]** > **[OneDrive-mapp]**  för att spara data.

   >[!NOTE]
   >
   >* Som standard `forms-ootb-storage-adaptive-forms-submission` finns i OneDrive-behållaren.
   > * Skapa en mapp som `forms-ootb-storage-adaptive-forms-submission`, om den inte redan finns genom att klicka **Skapa mapp**.

Nu kan du använda den här lagringskonfigurationen för OneDrive för att skicka-åtgärden i ett adaptivt formulär.

### Använd OneDrive-konfiguration i ett adaptivt formulär {#use-onedrive-configuartion-in-af}

Du kan använda den skapade OneDrive-lagringskonfigurationen i ett adaptivt formulär för att spara data eller skapa ett postdokument i en OneDrive-mapp. Utför följande steg för att använda OneDrive-lagringskonfigurationen i ett adaptivt formulär som:
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

## Relaterade artiklar

{{af-submit-action}}
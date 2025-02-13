---
Title: How to integrate Adaptive Form to a SharePoint Document Library?
Description: This article explains how to send data from your Adaptive Form to a SharePoint  Document library when you submit the form.
keywords: Ansluta SharePoint dokumentbibliotek till ett tilläggsformulär, Skicka till SharePoint, Skapa en SharePoint Document Library-konfiguration, Använd åtgärden Skicka till SharePoint i ett adaptivt formulär, AEM Forms Data Model SharePoint Document Library, Forms Data Model SharePoint Document Library, Integrate Forms Data Model för att SharePoint dokumentbiblioteket
feature: Adaptive Forms, Core Components
role: User, Developer
source-git-commit: 55e8f142e242f5f4010653a155a241ffcf801470
workflow-type: tm+mt
source-wordcount: '566'
ht-degree: 0%

---


# Ansluta ett anpassat formulär till Microsoft® SharePoint Document Library {#connect-af-sharepoint-doc-library}

>[!VIDEO](https://video.tv.adobe.com/v/3444368/formautomation-productivitytools-adaptiveforms--sharepointintegration-documentlibrary/?quality=12&learn=on)

Så här använder du åtgärden **[!UICONTROL Submit to SharePoint Document Library]** Skicka i en anpassad form:

1. [Skapa en SharePoint-dokumentbibliotekskonfiguration](#1-create-a-sharepoint-document-library-configuration): Den ansluter AEM Forms till din Microsoft® Sharepoint-lagring.
2. [Använd åtgärden Skicka till SharePoint i ett adaptivt formulär](#2-use-sharepoint-document-library-configuration-in-an-adaptive-form): Det kopplar ditt adaptiva formulär till konfigurerade Microsoft® SharePoint.

## 1. Skapa en SharePoint Document Library-konfiguration

Så här ansluter du AEM Forms till din Microsoft® Sharepoint Document Library-lagring:

1. Gå till din **AEM Forms Author**-instans > **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Microsoft® SharePoint]**.
1. När du har valt **[!UICONTROL Microsoft® SharePoint]** omdirigeras du till **[!UICONTROL SharePoint Browser]**.
1. Välj en **konfigurationsbehållare**. Konfigurationen lagras i den valda konfigurationsbehållaren.
1. Klicka på **[!UICONTROL Create]** > **[!UICONTROL SharePoint Document Library]** i listrutan. Konfigurationsguiden för SharePoint visas.

   ![SharePoint-konfiguration](/help/forms/assets/sharepoint_configuration.png)

1. Ange **[!UICONTROL Title]**, **[!UICONTROL Client ID]**, **[!UICONTROL Client Secret]** och **[!UICONTROL OAuth URL]**. Mer information om hur du hämtar klient-ID, klienthemlighet, klient-ID för OAuth URL finns i [Microsoft®-dokumentation](https://learn.microsoft.com/en-us/graph/auth-register-app-v2).
   * Du kan hämta `Client ID` och `Client Secret` för din app från Microsoft® Azure-portalen.
   * Lägg till omdirigerings-URI som `https://[author-instance]/libs/cq/sharepoint/content/configurations/wizard.html` i Microsoft® Azure-portalen. Ersätt `[author-instance]` med URL:en för din Author-instans.
   * Lägg till API-behörigheterna `offline_access` och `Sites.Manage.All` för att ge läs-/skrivbehörigheter. `Sites.Manage.All` är ett behörighetsområde i Microsoft Graph API som ger ett program möjlighet att hantera alla aspekter av SharePoint Sites, till exempel att ta bort eller ändra platser.

     >[!NOTE]
     >
     > Du kan också [konfigurera SharePoint-webbplatser med begränsad åtkomst](/help/forms/configure-sharepoint-site-limited-access.md) genom att använda behörighetsomfånget `Sites.Selected` i Microsoft Graph API. `Sites.Selected` är ett behörighetsområde i Microsoft Graph API som ger mer detaljerad och begränsad åtkomst till SharePoint webbplatser.

   * Använd OAuth-URL: `https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize`. Ersätt `<tenant-id>` med `tenant-id` för din app från Microsoft® Azure-portalen.

     >[!NOTE]
     >
     > Fältet **klienthemlighet** är obligatoriskt eller valfritt beroende på din Azure Active Directory-programkonfiguration. Om ditt program är konfigurerat att använda en klienthemlighet är det obligatoriskt att ange klienthemligheten.

1. Behörighetsomfånget `offline_access Sites.Selected` i Microsoft Graph API som ger mer detaljerad och begränsad åtkomst till SharePoint webbplatser. Behörighetsomfånget `offline_access Sites.Manage.All` i Microsoft Graph API som ger fullständig åtkomst till SharePoint webbplatser.
1. Klicka på **[!UICONTROL Connect]**. Om anslutningen lyckas visas meddelandet `Connection Successful`.

1. Välj nu **SharePoint-plats** > **Dokumentbibliotek** > **SharePoint-mapp** för att spara data.

   >[!NOTE]
   >
   >* Som standard finns `forms-ootb-storage-adaptive-forms-submission` på den valda SharePoint-webbplatsen.
   >* Skapa en mapp som `forms-ootb-storage-adaptive-forms-submission`, om den inte redan finns i `Documents`-biblioteket för den valda SharePoint-platsen genom att klicka på **Skapa mapp**.

Nu kan du använda den här SharePoint Sites-konfigurationen för att skicka-åtgärden i ett adaptivt formulär.

### 2. Använd SharePoint Document Library Configuration i ett adaptivt format

Du kan använda den skapade SharePoint Document Library-konfigurationen i ett adaptivt formulär för att spara data eller generera Document of Record i en SharePoint-mapp. Utför följande steg för att använda lagringskonfigurationen för SharePoint Document Library i ett adaptivt formulär som:

1. Skapa ett [anpassat formulär](/help/forms/creating-adaptive-form-core-components.md).

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

## Relaterade artiklar

{{af-submit-action}}
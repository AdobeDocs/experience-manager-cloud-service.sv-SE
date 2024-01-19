---
Title: How to send data to a SharePoint storage on submission of an Adaptive Form?
Description: Learn how to send data from your Adaptive Form to a SharePoint storage like a SharePoint list or Document library when you submit the form.
keywords: Hur ansluter man SharePoint lista till ett tilläggsformulär?, Hur man ansluter SharePoint dokumentbibliotek till ett tilläggsformulär, Skicka till SharePoint, Skapa en konfiguration för SharePoint dokumentbibliotek, Använd åtgärden Skicka till SharePoint i ett adaptivt formulär, Ansluta ett adaptivt formulär till Microsoft&reg; SharePoint List.
feature: Adaptive Forms, Core Components
source-git-commit: 8784c0bcd05eeae41a472faa5ecad03cbdd8a9b6
workflow-type: tm+mt
source-wordcount: '968'
ht-degree: 0%

---


# Ansluta ett adaptivt formulär till Microsoft® SharePoint

The **[!UICONTROL Submit to SharePoint]** kan du smidigt koppla ditt adaptiva formulär till en Microsoft® SharePoint-lagring. Formulärdatat skickas till den SharePoint-lagring du väljer när du har skickat in formuläret.

AEM as a Cloud Service erbjuder olika åtgärder för att skicka in formulär. Du kan läsa mer om de här alternativen i [Inlämningsåtgärd för anpassat formulär](/help/forms/configure-submit-actions-core-components.md)  artikel.

## Fördelar

Några fördelar med att skicka data från ett adaptivt formulär till SharePoint:

* Det underlättar direkt inlämning av blankettdata till SharePoint och gör det enkelt att centralt lagra och hantera informationen.
* Genom att använda SharePoint funktioner för åtkomstkontroll och behörigheter ser programmet till att endast behöriga personer kan visa eller ändra inskickade data.

Använda **[!UICONTROL Submit to SharePoint]** kan du:

* [Ansluta ett anpassat formulär till SharePoint Document Library](#connect-af-sharepoint-doc-library)
* [Ansluta ett anpassat formulär till SharePoint List](#connect-af-sharepoint-list)

## Ansluta ett anpassat formulär till SharePoint Document Library {#connect-af-sharepoint-doc-library}

Använd **[!UICONTROL Submit to SharePoint Document Library]** Skicka åtgärd i anpassad form:

1. [Skapa en SharePoint Document Library-konfiguration](#create-a-sharepoint-configuration-create-sharepoint-configuration): Den ansluter AEM Forms till din Microsoft® Sharepoint-lagring.
2. [Använda Skicka till SharePoint-åtgärden i ett anpassat formulär](#use-sharepoint-configuartion-in-af): Det kopplar ditt adaptiva formulär till konfigurerade Microsoft® SharePoint.

### Skapa en SharePoint Document Library-konfiguration {#create-sharepoint-configuration}

Så här ansluter du AEM Forms till din Microsoft® Sharepoint Document Library-lagring:

1. Gå till **AEM Forms Author** instans > **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** >  **[!UICONTROL Microsoft® SharePoint]**.
1. När du valt **[!UICONTROL Microsoft® SharePoint]** omdirigeras du till **[!UICONTROL SharePoint Browser]**.
1. Välj en **Konfigurationsbehållare**. Konfigurationen lagras i den valda konfigurationsbehållaren.
1. Klicka **[!UICONTROL Create]** > **[!UICONTROL SharePoint Document Library]** i listrutan. Konfigurationsguiden för SharePoint visas.

   ![SharePoint-konfiguration](/help/forms/assets/sharepoint_configuration.png)
1. Ange **[!UICONTROL Title]**, **[!UICONTROL Client ID]**, **[!UICONTROL Client Secret]** och **[!UICONTROL OAuth URL]**. Mer information om hur du hämtar klient-ID, klienthemlighet, klient-ID för OAuth-URL finns i [Microsoft® Documentation](https://learn.microsoft.com/en-us/graph/auth-register-app-v2).
   * Du kan hämta `Client ID` och `Client Secret` från Microsoft® Azure-portalen.
   * Lägg till omdirigerings-URI som i Microsoft® Azure-portalen som `https://[author-instance]/libs/cq/sharepoint/content/configurations/wizard.html`. Ersätt `[author-instance]` med webbadressen till din Author-instans.
   * Lägg till API-behörigheter `offline_access` och `Sites.Manage.All` för att ge läs- och skrivbehörigheter.
   * Använd OAuth-URL: `https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize`. Ersätt `<tenant-id>` med `tenant-id` från Microsoft® Azure-portalen.

   >[!NOTE]
   >
   > The **klienthemlighet** fältet är obligatoriskt eller valfritt beroende på din Azure Active Directory-programkonfiguration. Om ditt program är konfigurerat att använda en klienthemlighet är det obligatoriskt att ange klienthemligheten.

1. Klicka på **[!UICONTROL Connect]**. Vid en lyckad anslutning `Connection Successful` visas.

1. Välj nu **SharePoint Site** > **Dokumentbibliotek** > **SharePoint-mapp**, för att spara data.

   >[!NOTE]
   >
   >* Som standard `forms-ootb-storage-adaptive-forms-submission` finns på den valda SharePoint-webbplatsen.
   >* Skapa en mapp som `forms-ootb-storage-adaptive-forms-submission`, om de inte redan finns i `Documents` bibliotek för den valda SharePoint-webbplatsen genom att klicka på **Skapa mapp**.

Nu kan du använda den här SharePoint Sites-konfigurationen för att skicka-åtgärden i ett adaptivt formulär.

### Använda SharePoint Document Library Configuration i ett adaptivt formulär {#use-sharepoint-configuartion-in-af}

Du kan använda den skapade SharePoint Document Library-konfigurationen i ett adaptivt formulär för att spara data eller generera Document of Record i en SharePoint-mapp. Utför följande steg för att använda lagringskonfigurationen för SharePoint Document Library i ett adaptivt formulär som:

1. Skapa en [Adaptiv form](/help/forms/creating-adaptive-form-core-components.md).

   >[!NOTE]
   >
   > * Välj samma [!UICONTROL Configuration Container] för ett adaptivt formulär där du har skapat ditt SharePoint Document Library-lagringsutrymme.
   > * Om nej [!UICONTROL Configuration Container] markeras och sedan den globala [!UICONTROL Storage Configuration] visas i egenskapsfönstret för Skicka åtgärd.

1. Välj **Skicka åtgärd** as **[!UICONTROL Submit to SharePoint]**.
   ![SharePoint GIF](/help/forms/assets/sharedrive-video.gif)
1. Välj **[!UICONTROL Storage Configuration]**, där du vill spara dina data.
1. Klicka **[!UICONTROL Save]** för att spara Skicka-inställningarna.

När du skickar formuläret sparas data i den angivna Microsoft® Sharepoint-dokumentbibliotekslagringen.
Mappstrukturen som data ska sparas i är `/folder_name/form_name/year/month/date/submission_id/data`.

## Ansluta ett anpassat formulär till Microsoft® SharePoint List {#connect-af-sharepoint-list}

>[!VIDEO](https://video.tv.adobe.com/v/3424820/connect-aem-adaptive-form-to-sharepointlist/?quality=12&learn=on)

Använd [!UICONTROL Submit to SharePoint List] Skicka åtgärd i anpassad form:

1. [Skapa en listkonfiguration för SharePoint](#create-sharepoint-list-configuration): Den ansluter AEM Forms till Microsoft® Sharepoint List Storage.
1. [Använda Skicka med formulärdatamodellen i ett anpassat formulär](#use-submit-using-fdm): Det kopplar ditt adaptiva formulär till konfigurerade Microsoft® SharePoint.

### Skapa en listkonfiguration för SharePoint {#create-sharepoint-list-configuration}

Så här ansluter du AEM Forms till din Microsoft® Sharepoint-lista:

1. Gå till **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** >  **[!UICONTROL Microsoft® SharePoint]**.
1. Välj en **Konfigurationsbehållare**. Konfigurationen lagras i den valda konfigurationsbehållaren.
1. Klicka **[!UICONTROL Create]** > **[!UICONTROL SharePoint List]** i listrutan. Konfigurationsguiden för SharePoint visas.
1. Ange **[!UICONTROL Title]**, **[!UICONTROL Client ID]**, **[!UICONTROL Client Secret]** och **[!UICONTROL OAuth URL]**. Mer information om hur du hämtar klient-ID, klienthemlighet, klient-ID för OAuth-URL finns i [Microsoft® Documentation](https://learn.microsoft.com/en-us/graph/auth-register-app-v2).
   * Du kan hämta `Client ID` och `Client Secret` från Microsoft® Azure-portalen.
   * Lägg till omdirigerings-URI som i Microsoft® Azure-portalen som `https://[author-instance]/libs/cq/sharepointlist/content/configurations/wizard.html`. Ersätt `[author-instance]` med webbadressen till din Author-instans.
   * Lägg till API-behörigheter `offline_access` och `Sites.Manage.All` i **Microsoft® Graph** för att ange läs-/skrivbehörigheter. Lägg till `AllSites.Manage` behörighet i **Sharepoint** för att fjärrinteragera med data från SharePoint.
   * Använd OAuth-URL: `https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize`. Ersätt `<tenant-id>` med `tenant-id` från Microsoft® Azure-portalen.

     >[!NOTE]
     >
     > The **klienthemlighet** fältet är obligatoriskt eller valfritt beroende på din Azure Active Directory-programkonfiguration. Om ditt program är konfigurerat att använda en klienthemlighet är det obligatoriskt att ange klienthemligheten.

1. Klicka på **[!UICONTROL Connect]**. Vid en lyckad anslutning `Connection Successful` visas.
1. Välj **[!UICONTROL SharePoint Site]** och **[!UICONTROL SharePoint List]** i listrutan.
1. Välj **[!UICONTROL Create]** för att skapa molnkonfigurationen för Microsoft® SharePointList.


### Använda Skicka med formulärdatamodellen i ett anpassat formulär {#use-submit-using-fdm}

Du kan använda den skapade SharePoint List-konfigurationen i ett adaptivt formulär för att spara data eller skapa ett postdokument i en SharePoint List. Så här använder du en SharePoint List i ett adaptivt format:

1. [Skapa en formulärdatamodell med Microsoft](/help/forms/create-form-data-models.md)
1. [Konfigurera formulärdatamodellen för att hämta och skicka data](/help/forms/work-with-form-data-model.md#configure-services)
1. [Skapa ett adaptivt formulär](/help/forms/creating-adaptive-form-core-components.md)
1. [Konfigurera åtgärden Skicka med en formulärdatamodell](/help/forms/using-form-data-model.md)

När du skickar formuläret sparas data i det angivna lagringsutrymmet för Microsoft® Sharepoint-listan.

>[!NOTE]
>
> I Microsoft® SharePoint List stöds inte följande kolumntyper:
* bildkolumn
* metadatakolumn
* personkolumn
* extern datakolumn

## Relaterade artiklar

{{af-submit-action}}
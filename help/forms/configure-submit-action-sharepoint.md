---
Title: How to send data to a SharePoint storage on submission of an Adaptive Form?
Description: Learn how to send data from your Adaptive Form to a SharePoint storage like a SharePoint list or Document library when you submit the form.
keywords: Hur ansluter man SharePoint lista till ett tilläggsformulär?, Hur man ansluter SharePoint dokumentbibliotek till ett tilläggsformulär, Skicka till SharePoint, Skapa en konfiguration för SharePoint dokumentbibliotek, Använd åtgärden Skicka till SharePoint i ett adaptivt formulär, Ansluta ett adaptivt formulär till Microsoft&reg; SharePoint List.
feature: Adaptive Forms, Core Components
exl-id: e925a750-5fb5-4950-afd3-78551eec985d
title: "Hur konfigurerar jag en Skicka-åtgärd för ett anpassat formulär?"
role: User, Developer
source-git-commit: 2b76f1be2dda99c8638deb9633055e71312fbf1e
workflow-type: tm+mt
source-wordcount: '983'
ht-degree: 0%

---

# Ansluta ett adaptivt formulär till Microsoft® SharePoint

Med åtgärden **[!UICONTROL Submit to SharePoint]** kan du sömlöst ansluta ditt adaptiva formulär till ett Microsoft® SharePoint-lagringsutrymme. Formulärdatat skickas till den SharePoint-lagring du väljer när du har skickat in formuläret.

AEM as a Cloud Service erbjuder olika inskickningsåtgärder för att hantera inskickade formulär. Du kan läsa mer om de här alternativen i artikeln [Åtgärd för att skicka anpassade formulär](/help/forms/configure-submit-actions-core-components.md).

## Fördelar

Några fördelar med att skicka data från ett adaptivt formulär till SharePoint:

* Det underlättar direkt inlämning av blankettdata till SharePoint och gör det enkelt att centralt lagra och hantera informationen.
* Genom att använda SharePoint funktioner för åtkomstkontroll och behörigheter ser programmet till att endast behöriga personer kan visa eller ändra inskickade data.

Med **[!UICONTROL Submit to SharePoint]** kan du:

* [Ansluta ett anpassat formulär till SharePoint Document Library](#connect-af-sharepoint-doc-library)
* [Ansluta ett anpassat formulär till SharePoint List](#connect-af-sharepoint-list)

## Ansluta ett anpassat formulär till SharePoint Document Library {#connect-af-sharepoint-doc-library}

Så här använder du åtgärden **[!UICONTROL Submit to SharePoint Document Library]** Skicka i en anpassad form:

1. [Skapa en SharePoint-dokumentbibliotekskonfiguration](#create-a-sharepoint-configuration-create-sharepoint-configuration): Den ansluter AEM Forms till din Microsoft® Sharepoint-lagring.
2. [Använd åtgärden Skicka till SharePoint i ett adaptivt formulär](#use-sharepoint-configuartion-in-af): Det kopplar ditt adaptiva formulär till konfigurerade Microsoft® SharePoint.

### Skapa en SharePoint Document Library-konfiguration {#create-sharepoint-configuration}

Så här ansluter du AEM Forms till din Microsoft® Sharepoint Document Library-lagring:

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

### Använda SharePoint Document Library Configuration i ett adaptivt formulär {#use-sharepoint-configuartion-in-af}

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

## Ansluta ett anpassat formulär till Microsoft® SharePoint List {#connect-af-sharepoint-list}

>[!VIDEO](https://video.tv.adobe.com/v/3424820/connect-aem-adaptive-form-to-sharepointlist/?quality=12&learn=on)

Så här använder du åtgärden [!UICONTROL Submit to SharePoint List] Skicka i en anpassad form:

1. [Skapa en SharePoint-listkonfiguration](#create-sharepoint-list-configuration): Den ansluter AEM Forms till din Microsoft® Sharepoint-listlagring.
1. [Använd Skicka med FDM (Form Data Model) i ett adaptivt formulär](#use-submit-using-fdm): Det kopplar ditt adaptiva formulär till konfigurerade Microsoft® SharePoint.

### Skapa en listkonfiguration för SharePoint {#create-sharepoint-list-configuration}

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


### Använda Skicka med hjälp av formulärdatamodell (FDM) i ett anpassat formulär {#use-submit-using-fdm}

Du kan använda den skapade SharePoint List-konfigurationen i ett adaptivt formulär för att spara data eller skapa ett postdokument i en SharePoint List. Så här använder du en SharePoint List i ett adaptivt format:

1. [Skapa en formulärdatamodell (FDM) med Microsoft](/help/forms/create-form-data-models.md)
1. [Konfigurera FDM (Form Data Model) för att hämta och skicka data](/help/forms/work-with-form-data-model.md#configure-services)
1. [Skapa ett adaptivt formulär](/help/forms/creating-adaptive-form-core-components.md)
1. [Konfigurera åtgärden Skicka med en formulärdatamodell (FDM)](/help/forms/using-form-data-model.md)

När du skickar formuläret sparas data i det angivna lagringsutrymmet för Microsoft® Sharepoint-listan.

>[!NOTE]
>
> I Microsoft® SharePoint List stöds inte följande kolumntyper:
> * bildkolumn
> * metadatakolumn
> * personkolumn
> * extern datakolumn

## Relaterade artiklar

{{af-submit-action}}

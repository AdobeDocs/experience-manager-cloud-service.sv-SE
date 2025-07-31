---
Title: How to send data to a SharePoint List storage on submission of an Adaptive Form?
Description: Learn how to send data from your Adaptive Form to a SharePoint storage like a SharePoint list when you submit the form.
keywords: Hur ansluter man SharePoint lista till ett tilläggsformulär?, Skicka till SharePoint, Skapa en SharePoint List Configuration, Använd åtgärden Skicka till SharePoint i ett adaptivt format, Ansluta ett adaptivt formulär till Microsoft&reg; SharePoint List.
feature: Adaptive Forms, Core Components, Foundation Components, Edge Delivery Services
title: Hur konfigurerar man en Skicka-åtgärd för ett anpassat formulär?
role: User, Developer
exl-id: 9ac3e7be-c6fa-4dbc-9aba-b81741ba6c55
source-git-commit: 64edcfe1bf94638ae5d9510a5a6ac660cf1bcd0a
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 0%

---

# Ansluta ett anpassat formulär till Microsoft® SharePoint List {#connect-af-sharepoint-list}

>[!VIDEO](https://video.tv.adobe.com/v/3424820/connect-aem-adaptive-form-to-sharepointlist/?quality=12&learn=on)

Så här använder du åtgärden [!UICONTROL Submit to SharePoint List] Skicka i en anpassad form:

1. [Skapa en SharePoint-listkonfiguration](#1-create-a-sharepoint-list-configuration): Den ansluter AEM Forms till din Microsoft® Sharepoint-listlagring.
1. [Använd Skicka med FDM (Form Data Model) i ett adaptivt formulär](#2-use-the-submit-using-form-data-model-fdm-in-an-adaptive-form-use-submit-using-fdm): Det kopplar ditt adaptiva formulär till konfigurerade Microsoft® SharePoint.

## &#x200B;1. Skapa en SharePoint List-konfiguration

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


## &#x200B;2. Använd Skicka med FDM (Form Data Model) i ett anpassat formulär {#use-submit-using-fdm}

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

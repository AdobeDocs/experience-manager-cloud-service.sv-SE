---
title: Hur konfigurerar man en SharePoint Site med begränsad åtkomst med hjälp av behörighetsomfånget?
description: Lär dig hur du konfigurerar SharePoint Site med begränsad åtkomst med hjälp av behörighetsomfånget.
keywords: Hur man konfigurerar SharePoint Site med begränsad åtkomst?, Konfigurera SharePoint med begränsad åtkomst, Använda behörighetsområde för att begränsa åtkomst till SharePoint Site.
feature: Adaptive Forms, Core Components
role: User, Developer
exl-id: 3230bab2-c1aa-409d-9f01-c42cf88b1135
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '821'
ht-degree: 0%

---

# Konfigurera SharePoint Site med begränsad åtkomst med hjälp av behörighetsomfattning

<span class="preview"> Funktionen är tillgänglig under det tidiga adopterprogrammet. Du kan skriva till aem-forms-ea@adobe.com från ditt officiella e-post-id för att gå med i det tidiga adopterprogrammet och begära åtkomst till funktionen. </span>

Syftet med begränsad eller begränsad åtkomst är att förbättra säkerhetshanteringen genom att tillåta administratörer att styra åtkomsten till en viss SharePoint-webbplats eller en grupp av SharePoint-webbplatser. Behörighetsnivån är användbar när du behöver ge en användare eller grupp åtkomst till en specifik webbplats utan att tillåta dem att visa andra otillåtna SharePoint-platser.

## Fördelar med att konfigurera SharePoint Site med begränsad åtkomst

Fördelar med begränsad åtkomst till SharePoint Site:

* **Förbättrat skydd**: Genom att begränsa åtkomsten kan du se till att endast behörig personal kan visa eller ändra känslig information, vilket minskar risken för obehörig åtkomst.

* **Principen om minst privilegium**: Den ger användarna den lägsta åtkomstnivå (eller de behörigheter) som krävs för att de ska kunna utföra sina jobbfunktioner. Detta minimerar varje användares exponering för känsliga delar av nätverket, vilket kan skydda mot potentiella interna hot.

* **Dataskydd**: Begränsad åtkomst hjälper till att skydda viktiga data mot exponering. Det säkerställer att endast användare som behöver kunna se data har tillgång till dem, vilket är nödvändigt för att uppfylla reglerna för skydd av personuppgifter.

* **Förebyggande av dataförlust vid olyckshändelse**: Med färre personer som kan ändra innehåll minskar risken för oavsiktliga borttagningar eller ändringar av viktiga data avsevärt.

* **Kontrollerat dataflöde**: Det hjälper till att styra informationsflödet inom och utanför organisationen och säkerställer att data inte hamnar i orätta händer.

## Konfigurera SharePoint med begränsad åtkomst med hjälp av auktoriseringsomfattning

Följ stegen nedan för att konfigurera SharePoint Sites med begränsad åtkomst med hjälp av behörighetsområden:

1. [Skapa ett program med ](#create-an-application-with-the-limited-permission-in-the-azure-portal)
1. [Ange auktoriseringsomfånget på AEM-instansen](#set-the-authorization-scope-at-aem-instance)

### Skapa ett program med begränsad behörighet i Azure-portalen

Skapa ett program i [Microsoft Azure-portalen](https://portal.azure.com/#home) med behörighetsomfånget `Sites.Selected` i Microsoft Graph API.

![SharePoint har valt plats](/help/forms/assets/sharepoint-selected-site.png)

Mer information om hur du hämtar `Client ID`, `Client Secret` och `Tenant ID` för `OAuth URL` finns i [Microsoft®-dokumentation](https://learn.microsoft.com/en-us/graph/auth-register-app-v2).

* Lägg till omdirigerings-URI som `https://[author-instance]/libs/cq/sharepoint/content/configurations/wizard.html` i Microsoft® Azure-portalen. Ersätt `[author-instance]` med URL:en för din Author-instans.
* Lägg till behörighetsomfånget `offline_access` och `Sites.Selected` i Microsoft Graph API för att ge begränsad åtkomst till webbplatser.
* För OAuth-URL: `https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize`. Ersätt `<tenant-id>` med `tenant-id` för din app från Microsoft® Azure-portalen.

Om du vill använda API-behörigheten `Sites.Selected` måste du ha ett program som är registrerat i Azure-portalen med rätt behörigheter för SharePoint Online Sites. Installationen säkerställer att programmet har den behörighet som krävs för att interagera med SharePoint Site inom det definierade området, vilket ger den begränsade åtkomst som krävs.

Mer information om hur du utvecklar program som använder [-behörigheter för SharePoint Online-platser finns i ](https://techcommunity.microsoft.com/t5/microsoft-sharepoint-blog/develop-applications-that-use-sites-selected-permissions-for-spo/ba-p/3790476)bloggartikeln - Utveckla program som använder platser.Markerade behörigheter för SPO-webbplatser`Sites.Selected`.

### Ange auktoriseringsomfånget på AEM-instansen

För att ge begränsad åtkomst till en Microsoft SharePoint Site är det viktigt att ange behörighetsomfånget korrekt. Så här anger du auktoriseringsomfång och ansluter AEM Forms till din Microsoft® SharePoint-lagring:

1. Gå till din **AEM Forms Author**-instans > **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Microsoft® SharePoint]**.
1. När du har valt **[!UICONTROL Microsoft® SharePoint]** omdirigeras du till **[!UICONTROL SharePoint Browser]**.
1. Välj en **konfigurationsbehållare**. Konfigurationen lagras i den valda konfigurationsbehållaren.
1. Klicka på **[!UICONTROL Create]** > **[!UICONTROL SharePoint Document Library]** i listrutan. Konfigurationsguiden för SharePoint visas.

   ![SharePoint Site Limited Site Access](/help/forms/assets/sharepoint-doc-library-limited-scopes.png)

1. Ange **[!UICONTROL Title]**, **[!UICONTROL Client ID]** och **[!UICONTROL Client Secret]**. Mer information om hur du hämtar klient-ID och klienthemlighet finns i [Microsoft®-dokumentation](https://learn.microsoft.com/en-us/graph/auth-register-app-v2).

1. Använd OAuth-URL som `https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize`. Ersätt `<tenant-id>` med `tenant-id` för din app från Microsoft® Azure-portalen.

   >[!NOTE]
   >
   > Fältet **klienthemlighet** är obligatoriskt eller valfritt beroende på din Azure Active Directory-programkonfiguration. Om ditt program är konfigurerat att använda en klienthemlighet är det obligatoriskt att ange klienthemligheten.

1. Lägg till `offline_access Sites.Selected` i fältet `Authorization Scope`. När du lägger till omfånget `offline_access Sites.Selected` i textrutefältet `Authorization Scope` visas textrutan `SharePoint Site ID` på skärmen.

1. Ange SharePoint webbplats-ID. Mer information om hur du hämtar SharePoint Site ID finns i avsnittet [Extra Bytes](#extra-bytes).

1. Klicka på **[!UICONTROL Check Site Connection]**. Om anslutningen lyckas visas meddelandet `Connection Successful`.

1. Välj nu **SharePoint-plats** > **Dokumentbibliotek** > **SharePoint-mapp** för att spara data.

   >[!NOTE]
   >
   >* Som standard finns `forms-ootb-storage-adaptive-forms-submission` på den valda SharePoint-webbplatsen.
   >* Skapa en mapp som `forms-ootb-storage-adaptive-forms-submission`, om den inte redan finns i `Documents`-biblioteket för den valda SharePoint-platsen genom att klicka på **Skapa mapp**.

Nu kan du använda den här [SharePoint Sites-konfigurationen för att skicka-åtgärden i ett adaptivt formulär](/help/forms/configure-submit-action-sharepoint.md#use-sharepoint-document-library-configuration-in-an-adaptive-form-use-sharepoint-configuartion-in-af).

## Extra byte

Så här hämtar du värdet för `SharePoint Site ID`:

1. Gå till [API:erna för Microsoft Graph Explorer](https://developer.microsoft.com/en-us/graph/graph-explorer).
1. Klicka på `SharePoint Sites` i den vänstra rutan under API:erna för `Search for a SharePoint site by keyword`.
1. Ersätt platshållaren `contoso` med det faktiska namnet på din SharePoint-webbplats för att hämta motsvarande plats-ID.

   ![SharePoint-dokumentbiblioteks-ID](/help/forms/assets/sharepoint-site-id.png)

När du klickar på knappen `Run Query` visas plats-ID:t på skärmen.

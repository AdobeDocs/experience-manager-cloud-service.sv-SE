---
title: Hur konfigurerar jag  [!DNL Microsoft Dynamics] OData för AEM Forms?
description: Lär dig skapa FDM (Form Data Model) baserat på entiteter, attribut och tjänster som definierats i  [!DNL Microsoft Dynamics] tjänsten.
feature: Adaptive Forms, Form Data Model
role: User, Developer
level: Beginner
exl-id: cb7b41f0-fd4f-4ba6-9f45-792a66ba6368
hide: true
hidefromtoc: true
source-git-commit: 3a12fff170f521f6051f0c24a4eb28a12439eec1
workflow-type: tm+mt
source-wordcount: '966'
ht-degree: 1%

---

# [!DNL Microsoft Dynamics] OData-konfiguration {#microsoft-dynamics-odata-configuration}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/ms-dynamics-odata-configuration.html) |
| AEM as a Cloud Service | Den här artikeln |

![dataintegrering](assets/data-integeration.png)

[!DNL Microsoft Dynamics] är ett CRM- och ERP-program (Enterprise Resource Planning) som innehåller företagslösningar för att skapa och hantera kundkonton, kontakter, leads, möjligheter och ärenden. [[!DNL Experience Manager Forms] Dataintegrering](data-integration.md) tillhandahåller en OData-molntjänstkonfiguration som integrerar Forms med både online- och lokal [!DNL Microsoft Dynamics]-server. Det gör att du kan skapa FDM (Form Data Model) baserat på entiteter, attribut och tjänster som definierats i tjänsten [!DNL Microsoft Dynamics]. Formulärdatamodellen (FDM) kan användas för att skapa adaptiv Forms som interagerar med [!DNL Microsoft Dynamics]-servern för att aktivera affärsarbetsflöden. Till exempel:

* Fråga [!DNL Microsoft Dynamics]-servern efter data och förifyll adaptiva Forms
* Skriv data i [!DNL Microsoft Dynamics] vid sändning av anpassat formulär
* Skriv data i [!DNL Microsoft Dynamics] via anpassade entiteter som definierats i FDM (Form Data Model) och omvänt

<!--[!DNL Experience Manager Forms] add-on package also includes reference OData configuration that you can use to quickly integrate [!DNL Microsoft Dynamics] with [!DNL Experience Manager Forms].-->

<!--When the package is installed, the following entities and services are available on your [!DNL Experience Manager Forms] instance:

* MS Dynamics OData Cloud Service (OData Service)-->
<!--* Form Data Model with preconfigured [!DNL Microsoft Dynamics] entities and services.-->

<!-- Preconfigured [!DNL Microsoft Dynamics] entities and services in a Form Data Model are available on your [!DNL Experience Manager Forms] instance only if the run mode for the [!DNL Experience Manager] instance is set as `samplecontent` (default). -->  MS Dynamics OData Cloud Service (OData Service) är tillgänglig med alla körningslägen. Mer information om hur du konfigurerar körningslägen för en [!DNL Experience Manager]-instans finns i [Körningslägen](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html#runmodes).

AEM as a Cloud Service erbjuder olika inskickningsåtgärder för att hantera inskickade formulär. Du kan läsa mer om de här alternativen i artikeln [Åtgärd för att skicka anpassade formulär](/help/forms/configure-submit-actions-core-components.md).


## Förutsättningar {#prerequisites}

Innan du börjar konfigurera och konfigurera [!DNL Microsoft Dynamics] måste du kontrollera att du har:

<!--* Installed the [[!DNL Experience Manager Forms] add-on package](installing-configuring-aem-forms-osgi.md) -->
* Konfigurerade [!DNL Microsoft Dynamics] 365 online eller installerade en instans av någon av följande [!DNL Microsoft Dynamics]-versioner:

   * [!DNL Microsoft Dynamics] 365 lokal
   * [!DNL Microsoft Dynamics] 2016 lokal

* [Programmet för  [!DNL Microsoft Dynamics] onlinetjänsten  [!DNL Microsoft Azure] Active Directory](https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/walkthrough-register-dynamics-365-app-azure-active-directory) har registrerats. Notera värdena för klient-ID (kallas även program-ID) och klienthemlighet för den registrerade tjänsten. Dessa värden används när [molntjänsten konfigureras för din [!DNL Microsoft Dynamics] tjänst](#configure-cloud-service-for-your-microsoft-dynamics-service).

## Ange svars-URL för registrerat [!DNL Microsoft Dynamics]-program {#set-reply-url-for-registered-microsoft-dynamics-application}

Gör följande för att ange svars-URL:en för det registrerade [!DNL Microsoft Dynamics]-programmet:

>[!NOTE]
>
>Använd bara den här proceduren när du integrerar [!DNL Experience Manager Forms] med [!DNL Microsoft Dynamics]-onlineservern.

1. Gå till [!DNL Microsoft Azure] Active Directory-konto och lägg till följande URL för molntjänstkonfiguration i **[!UICONTROL Reply URLs]**-inställningarna för det registrerade programmet:

   `https://[server]:[port]/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html`

   ![Azure-katalog](assets/azure_directory_new.png)

1. Spara konfigurationen.

## Konfigurera [!DNL Microsoft Dynamics] för IFD {#configure-microsoft-dynamics-for-ifd}

[!DNL Microsoft Dynamics] använder anspråksbaserad autentisering för att ge åtkomst till data på [!DNL Microsoft Dynamics] CRM-servern till externa användare. Om du vill aktivera detta gör du följande för att konfigurera [!DNL Microsoft Dynamics] för IFD (Internet-motstående distribution) och konfigurera anspråksinställningarna.

>[!NOTE]
>
> Använd bara den här proceduren när du integrerar [!DNL Experience Manager Forms] med den lokala [!DNL Microsoft Dynamics]-servern.

1. Konfigurera den lokala instansen [!DNL Microsoft Dynamics] för IFD enligt beskrivningen i [Konfigurera IFD för [!DNL Microsoft Dynamics]](https://technet.microsoft.com/en-us/library/dn609803.aspx).
1. Kör följande kommandon med Windows PowerShell för att konfigurera anspråksinställningar för IFD-aktiverad [!DNL Microsoft Dynamics]:

   ```shell
   Add-PSSnapin Microsoft.Crm.PowerShell
    $ClaimsSettings = Get-CrmSetting -SettingType OAuthClaimsSettings
    $ClaimsSettings.Enabled = $true
    Set-CrmSetting -Setting $ClaimsSettings
   ```

   Mer information finns i [Appregistrering för lokal CRM (IFD)](https://msdn.microsoft.com/sl-si/library/dn531010(v=crm.7).aspx#bkmk_ifd).

## Konfigurera OAuth-klient på AD FS-dator {#configure-oauth-client-on-ad-fs-machine}

Gör följande för att registrera en OAuth-klient på AD FS-datorn (Active Directory Federation Services) och bevilja åtkomst på AD FS-datorn:

>[!NOTE]
>
>Använd bara den här proceduren när du integrerar [!DNL Experience Manager Forms] med den lokala [!DNL Microsoft Dynamics]-servern.

1. Kör följande kommando:

   `Add-AdfsClient -ClientId “<Client-ID>” -Name "<name>" -RedirectUri "<redirect-uri>" -GenerateClientSecret`

   Var:

   * `Client-ID` är ett klient-ID som du kan generera med valfri GUID-generator.
   * `redirect-uri` är URL:en till molntjänsten [!DNL Microsoft Dynamics] OData på [!DNL Experience Manager Forms]. Standardmolntjänsten som installeras med [!DNL Experience Manager Forms] distribueras på följande URL:
     `https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html`

1. Kör följande kommando för att bevilja åtkomst på AD FS-datorn:

   `Grant-AdfsApplicationPermission -ClientRoleIdentifier “<Client-ID>” -ServerRoleIdentifier <resource> -ScopeNames openid`

   Var:

   * `resource` är [!DNL Microsoft Dynamics] organisations-URL.

1. [!DNL Microsoft Dynamics] använder HTTPS-protokoll. Om du vill anropa AD FS-slutpunkter från [!DNL Forms]-servern installerar du [!DNL Microsoft Dynamics] platscertifikatet till Java-certifikatarkivet med kommandot `keytool` på datorn som kör [!DNL Experience Manager Forms].

## Konfigurera molntjänsten för din [!DNL Microsoft Dynamics]-tjänst {#configure-cloud-service-for-your-microsoft-dynamics-service}

En OData-tjänst identifieras av tjänstens rot-URL. Om du vill konfigurera en OData-tjänst i [!DNL Experience Manager] as a Cloud Service kontrollerar du att du har tjänstens rot-URL och gör följande:

<!--The **MS Dynamics OData Cloud Service (OData Service)** configuration comes with default OData configuration. To configure it to connect with your [!DNL Microsoft Dynamics] service, do the following.-->

>[!NOTE]
>
>Stegvisa anvisningar om hur du konfigurerar [!DNL Microsoft Dynamics 365], online eller lokalt, finns i [[!DNL Microsoft Dynamics] OData-konfiguration](ms-dynamics-odata-configuration.md).

1. Gå till **[!UICONTROL Tools > Cloud Services > Data Sources]**. Välj den mapp där du vill skapa en molnkonfiguration.

   Mer information om hur du skapar och konfigurerar en mapp för molntjänstkonfigurationer finns i [Konfigurera mapp för molntjänstkonfigurationer](#cloud-folder).

1. Välj **[!UICONTROL Create]** för att öppna **[!UICONTROL Create Data Source Configuration wizard]**. Ange ett namn och eventuellt en rubrik för konfigurationen, välj **[!UICONTROL OData Service]** i listrutan **[!UICONTROL Service Type]**, bläddra och välj en miniatyrbild för konfigurationen och välj **[!UICONTROL Next]**.
På fliken **[!UICONTROL Authentication Settings]**:

   1. Ange värdet för fältet **[!UICONTROL Service Root]**. Gå till Dynamics-instansen och navigera till **[!UICONTROL Developer Resources]** för att visa värdet för fältet Tjänstrot. Till exempel https://&lt;tenant-name>/api/data/v9.1/

   1. Välj **[!UICONTROL OAuth 2.0]** som autentiseringstyp.

   1. Ersätt standardvärdena i fälten **[!UICONTROL Client Id]** (kallas även **program-ID**), **[!UICONTROL Client Secret]**, **[!UICONTROL OAuth URL]**, **[!UICONTROL Refresh Token URL]**, **[!UICONTROL Access Token URL]** och **[!UICONTROL Resource]** med värden från din [!DNL Microsoft Dynamics]-tjänstkonfiguration. Det är obligatoriskt att ange den dynamiska instansens URL i fältet **[!UICONTROL Resource]** för att konfigurera [!DNL Microsoft Dynamics] med en formulärdatamodell (FDM). Använd tjänstens rot-URL för att härleda den dynamiska instansens URL. Exempel: [https://org.crm.dynamics.com](https://org.crm.dynamics.com/).

   1. Ange **[!UICONTROL openid]** i fältet **[!UICONTROL Authorization Scope]** för auktoriseringsprocess på [!DNL Microsoft Dynamics].

      ![Autentiseringsinställningar](assets/dynamics_authentication_settings_new.png)
FDM (Form Data Model)
1. Klicka på **[!UICONTROL Connect to OAuth]**. Du omdirigeras till inloggningssidan för [!DNL Microsoft Dynamics].
1. Logga in med dina [!DNL Microsoft Dynamics]-autentiseringsuppgifter och godkänn för att tillåta molntjänstkonfigurationen att ansluta till [!DNL Microsoft Dynamics]-tjänsten. Det är en engångsuppgift att skapa en FDM (Form Data Model) för molntjänsten och tjänsten.

   Du är formulärdatamodellen på konfigurationssidan för molntjänsten, som visar ett meddelande om att OData-konfigurationen har sparats.

Molntjänsten MS Dynamics OData Cloud Service (OData Service) är konfigurerad och ansluten till Dynamics-tjänsten. FDM (Form Data Model)

## Skapa formulärdatamodell (FDM) {#create-form-data-model}

<!--When you install the [!DNL Experience Manager Forms] package, a form data model, **[!DNL Microsoft Dynamics] FDM**, is deployed on your [!DNL Experience Manager] instance. By default, the Form Data Model uses [!DNL Microsoft Dynamics] service configured in the MS Dynamics OData Cloud Service (OData Service) as its data source.

On opening the Form Data Model for the first time, it connects to the configured [!DNL Microsoft Dynamics] service and fetches entities from your [!DNL Microsoft Dynamics] instance. The "contact" and "lead" entities from [!DNL Microsoft Dynamics] are already added in the form data model.

To review the form data model, go to **[!UICONTROL Form Data Model egrations]**. Select **[!DNL Microsoft Dynamics] FDM** and click **[!UICONTROL Edit]** to open the Form Data Model in edit mode. Alternatively, you can open the Form Data Model directly from the following URL:

`https://'[server]:[port]'/aem/fdm/editor.html/content/dam/formsanddocuments-fdm/ms-dynamics-fdm`
 Form Data Model 
![default-fdm-1](assets/default-fdm-1.png)-->

När du har konfigurerat molntjänsten MS Dynamics OData kan du använda tjänsten när du skapar formulärdatamodell (FDM). Mer information finns i [Skapa formulärdatamodell (FDM)](create-form-data-models.md).

Därefter kan du skapa en FDM (Adaptive Form Data Model) och använda den i olika användningsområden för adaptiva formulär, till exempel:

* Förifyll anpassat formulär genom att fråga efter information från [!DNL Microsoft Dynamics] enheter och tjänster
* Anropa [!DNL Microsoft Dynamics] serveråtgärder som definierats i en FDM (Form Data Model) med hjälp av regler för anpassat formulär
* Skriv skickade formulärdata till [!DNL Microsoft Dynamics] entiteter

<!--It is recommended to create a copy of the Form Data Model provided with the [!DNL Experience Manager Forms] package and configure data models and services to suit your requirements. It will ensure that any future updates to the package do not override your form data model.-->

Du kan [konfigurera åtgärden Skicka formulärdatamodell](/help/forms/using-form-data-model.md) för ett anpassat formulär att skicka data till Microsoft Dynamics OData.

Mer information om hur du skapar och använder FDM (Form Data Model) i arbetsflöden finns i [Dataintegrering](data-integration.md).

## Relaterade artiklar

{{af-submit-action}}

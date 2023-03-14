---
title: Konfigurera [!DNL Microsoft Dynamics] OData?
description: Lär dig hur du skapar formulärdatamodell baserat på de entiteter, attribut och tjänster som definieras i [!DNL Microsoft Dynamics] service. Formulärdatamodellen kan användas för att skapa adaptiv Forms som interagerar med [!DNL Microsoft Dynamics] för att möjliggöra arbetsflöden.
feature: Form Data Model
role: User, Developer
level: Beginner
exl-id: cb7b41f0-fd4f-4ba6-9f45-792a66ba6368
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '937'
ht-degree: 0%

---

# [!DNL Microsoft Dynamics] OData-konfiguration {#microsoft-dynamics-odata-configuration}

![dataintegrering](assets/data-integeration.png)

[!DNL Microsoft Dynamics] är ett CRM- och ERP-program (Enterprise Resource Planning) som innehåller företagslösningar för att skapa och hantera kundkonton, kontakter, leads, möjligheter och ärenden. [[!DNL Experience Manager Forms] Dataintegrering](data-integration.md) erbjuder en OData-molntjänstkonfiguration som integrerar Forms med både online och lokalt [!DNL Microsoft Dynamics] server. Det gör att du kan skapa formulärdatamodell baserat på de enheter, attribut och tjänster som definieras i [!DNL Microsoft Dynamics] service. Formulärdatamodellen kan användas för att skapa adaptiv Forms som interagerar med [!DNL Microsoft Dynamics] för att möjliggöra arbetsflöden. Till exempel:

* Fråga [!DNL Microsoft Dynamics] server för data och förifylla Adaptive Forms
* Skriv data i [!DNL Microsoft Dynamics] om inlämning av anpassade formulär
* Skriv data i [!DNL Microsoft Dynamics] via anpassade entiteter som definierats i formulärdatamodellen och vice versa

<!--[!DNL Experience Manager Forms] add-on package also includes reference OData configuration that you can use to quickly integrate [!DNL Microsoft Dynamics] with [!DNL Experience Manager Forms].-->

<!--When the package is installed, the following entities and services are available on your [!DNL Experience Manager Forms] instance:

* MS Dynamics OData Cloud Service (OData Service)-->
<!--* Form Data Model with preconfigured [!DNL Microsoft Dynamics] entities and services.-->

<!-- Preconfigured [!DNL Microsoft Dynamics] entities and services in a Form Data Model are available on your [!DNL Experience Manager Forms] instance only if the run mode for the [!DNL Experience Manager] instance is set as `samplecontent` (default). -->  MS Dynamics OData-Cloud Servicen (OData-tjänsten) är tillgänglig med alla körningslägen. Mer information om hur du konfigurerar körningslägen för en [!DNL Experience Manager] -instans, se [Körningslägen](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html#runmodes).

## Förutsättningar {#prerequisites}

Innan du börjar konfigurera och konfigurera [!DNL Microsoft Dynamics]måste du se till att du har:

<!--* Installed the [[!DNL Experience Manager Forms] add-on package](installing-configuring-aem-forms-osgi.md) -->
* Konfigurerad [!DNL Microsoft Dynamics] 365 online eller installerat en instans av något av följande [!DNL Microsoft Dynamics] versioner:

   * [!DNL Microsoft Dynamics] 365 lokal
   * [!DNL Microsoft Dynamics] 2016 lokal

* [Registrerade ansökan för [!DNL Microsoft Dynamics] onlinetjänst med [!DNL Microsoft Azure] Active Directory](https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/walkthrough-register-dynamics-365-app-azure-active-directory). Notera värdena för klient-ID (kallas även program-ID) och klienthemlighet för den registrerade tjänsten. Dessa värden används medan [konfigurera molntjänster för [!DNL Microsoft Dynamics] service](#configure-cloud-service-for-your-microsoft-dynamics-service).

## Ange URL för svar för registrerad [!DNL Microsoft Dynamics] program {#set-reply-url-for-registered-microsoft-dynamics-application}

Gör följande för att ange svars-URL för registrerad [!DNL Microsoft Dynamics] program:

>[!NOTE]
>
>Använd bara den här proceduren när du integrerar [!DNL Experience Manager Forms] med online [!DNL Microsoft Dynamics] server.

1. Gå till [!DNL Microsoft Azure] Active Directory-konto och lägg till följande URL för molntjänstkonfiguration i **[!UICONTROL Reply URLs]** inställningar för ditt registrerade program:

   `https://[server]:[port]/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html`

   ![Azure-katalog](assets/azure_directory_new.png)

1. Spara konfigurationen.

## Konfigurera [!DNL Microsoft Dynamics] för IFD {#configure-microsoft-dynamics-for-ifd}

[!DNL Microsoft Dynamics] använder anspråksbaserad autentisering för att ge åtkomst till data på [!DNL Microsoft Dynamics] CRM-server till externa användare. Så här aktiverar du det här: [!DNL Microsoft Dynamics] för installation mot Internet (IFD) och konfigurera anspråksinställningar.

>[!NOTE]
>
>Använd bara den här proceduren när du integrerar [!DNL Experience Manager Forms] med lokal [!DNL Microsoft Dynamics] server.

1. Konfigurera [!DNL Microsoft Dynamics] lokal instans av IFD enligt beskrivningen i [Konfigurera IFD för [!DNL Microsoft Dynamics]](https://technet.microsoft.com/en-us/library/dn609803.aspx).
1. Kör följande kommandon med Windows PowerShell för att konfigurera anspråksinställningar för IFD-aktiverad [!DNL Microsoft Dynamics]:

   ```shell
   Add-PSSnapin Microsoft.Crm.PowerShell
    $ClaimsSettings = Get-CrmSetting -SettingType OAuthClaimsSettings
    $ClaimsSettings.Enabled = $true
    Set-CrmSetting -Setting $ClaimsSettings
   ```

   Se [Appregistrering för CRM lokalt (IFD)](https://msdn.microsoft.com/sl-si/library/dn531010(v=crm.7).aspx#bkmk_ifd) för mer information.

## Konfigurera OAuth-klient på AD FS-dator {#configure-oauth-client-on-ad-fs-machine}

Gör följande för att registrera en OAuth-klient på AD FS-datorn (Active Directory Federation Services) och bevilja åtkomst på AD FS-datorn:

>[!NOTE]
>
>Använd bara den här proceduren när du integrerar [!DNL Experience Manager Forms] med lokal [!DNL Microsoft Dynamics] server.

1. Kör följande kommando:

   `Add-AdfsClient -ClientId “<Client-ID>” -Name "<name>" -RedirectUri "<redirect-uri>" -GenerateClientSecret`

   Var:

   * `Client-ID` är ett klient-ID som du kan generera med valfri GUID-generator.
   * `redirect-uri` är URL:en till [!DNL Microsoft Dynamics] OData-molntjänst på [!DNL Experience Manager Forms]. Standardmolntjänsten som installeras med [!DNL Experience Manager Forms] distribueras på följande URL:
      `https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html`

1. Kör följande kommando för att bevilja åtkomst på AD FS-datorn:

   `Grant-AdfsApplicationPermission -ClientRoleIdentifier “<Client-ID>” -ServerRoleIdentifier <resource> -ScopeNames openid`

   Var:

   * `resource` är [!DNL Microsoft Dynamics] organisations-URL.

1. [!DNL Microsoft Dynamics] använder HTTPS-protokoll. Anropa AD FS-slutpunkter från [!DNL Forms] server, installera [!DNL Microsoft Dynamics] platscertifikat till Java-certifikatarkiv med `keytool` kommando på datorn som körs [!DNL Experience Manager Forms].

## Konfigurera molntjänsten för [!DNL Microsoft Dynamics] service {#configure-cloud-service-for-your-microsoft-dynamics-service}

En OData-tjänst identifieras av tjänstens rot-URL. Konfigurera en OData-tjänst i [!DNL Experience Manager] as a Cloud Service, kontrollera att du har tjänstens rot-URL och gör följande:

<!--The **MS Dynamics OData Cloud Service (OData Service)** configuration comes with default OData configuration. To configure it to connect with your [!DNL Microsoft Dynamics] service, do the following.-->

>[!NOTE]
>
>Om du vill konfigurera steg-för-steg-guiden [!DNL Microsoft Dynamics 365], online eller lokalt, se [[!DNL Microsoft Dynamics] OData-konfiguration](ms-dynamics-odata-configuration.md).

1. Gå till **[!UICONTROL Tools > Cloud Services > Data Sources]**. Tryck för att välja den mapp där du vill skapa en molnkonfiguration.

   Se [Konfigurera mapp för molntjänstkonfigurationer](#cloud-folder) om du vill ha information om hur du skapar och konfigurerar en mapp för molntjänstkonfigurationer.

1. Tryck **[!UICONTROL Create]** för att öppna **[!UICONTROL Create Data Source Configuration wizard]**. Ange ett namn och eventuellt en rubrik för konfigurationen, välj **[!UICONTROL OData Service]** från **[!UICONTROL Service Type]** nedrullningsbar meny, där du kan bläddra och välja en miniatyrbild för konfigurationen, och trycka på **[!UICONTROL Next]**.
I **[!UICONTROL Authentication Settings]** tab:

   1. Ange värdet för **[!UICONTROL Service Root]** fält. Gå till Dynamics-instansen och navigera till **[!UICONTROL Developer Resources]** för att visa värdet för fältet Tjänstrot. Till exempel https://&lt;tenant-name>/api/data/v9.1/

   1. Välj **[!UICONTROL OAuth 2.0]** som autentiseringstyp.

   1. Ersätt standardvärdena i dialogrutan **[!UICONTROL Client Id]** (kallas även **Program-ID**), **[!UICONTROL Client Secret]**, **[!UICONTROL OAuth URL]**, **[!UICONTROL Refresh Token URL]**, **[!UICONTROL Access Token URL]** och **[!UICONTROL Resource]** fält med värden från [!DNL Microsoft Dynamics] tjänstkonfiguration. Det är obligatoriskt att ange dynamicinstansens URL i **[!UICONTROL Resource]** fält att konfigurera [!DNL Microsoft Dynamics] med en formulärdatamodell. Använd tjänstens rot-URL för att härleda den dynamiska instansens URL. Till exempel: [https://org.crm.dynamics.com](https://org.crm.dynamics.com/).

   1. Ange **[!UICONTROL openid]** i **[!UICONTROL Authorization Scope]** fält för auktoriseringsprocess på [!DNL Microsoft Dynamics].

      ![Autentiseringsinställningar](assets/dynamics_authentication_settings_new.png)
Formulärdatamodell
1. Klicka på **[!UICONTROL Connect to OAuth]**. Du omdirigeras till [!DNL Microsoft Dynamics] inloggningssida.
1. Logga in med [!DNL Microsoft Dynamics] autentiseringsuppgifter och acceptera för att tillåta molntjänstkonfigurationen att ansluta till [!DNL Microsoft Dynamics] service. Det är en engångsuppgift att skapa en formulärdatamodell mellan molntjänsten och tjänsten.

   Du är formulärdatamodellen på konfigurationssidan för molntjänsten, som visar ett meddelande om att OData-konfigurationen har sparats.

Molntjänsten MS Dynamics OData Cloud Service (OData Service) är konfigurerad och ansluten till Dynamics-tjänsten. Formulärdatamodell för formulärdata

## Skapa formulärdatamodell {#create-form-data-model}

<!--When you install the [!DNL Experience Manager Forms] package, a form data model, **[!DNL Microsoft Dynamics] FDM**, is deployed on your [!DNL Experience Manager] instance. By default, the Form Data Model uses [!DNL Microsoft Dynamics] service configured in the MS Dynamics OData Cloud Service (OData Service) as its data source.

On opening the Form Data Model for the first time, it connects to the configured [!DNL Microsoft Dynamics] service and fetches entities from your [!DNL Microsoft Dynamics] instance. The "contact" and "lead" entities from [!DNL Microsoft Dynamics] are already added in the form data model.

To review the form data model, go to **[!UICONTROL Form Data Model egrations]**. Select **[!DNL Microsoft Dynamics] FDM** and click **[!UICONTROL Edit]** to open the Form Data Model in edit mode. Alternatively, you can open the Form Data Model directly from the following URL:

`https://'[server]:[port]'/aem/fdm/editor.html/content/dam/formsanddocuments-fdm/ms-dynamics-fdm`
 Form Data Model 
![default-fdm-1](assets/default-fdm-1.png)-->

När du har konfigurerat molntjänsten MS Dynamics OData Cloud Ser Form Data Model ce) kan du använda tjänsten när du skapar formulärdatamodeller. Mer information finns i [Skapa formulärdatamodell](create-form-data-models.md).

Därefter kan du skapa ett adaptivt formulär baserat på formulärdatamodellen och använda det i olika användningsområden för adaptiva formulär, till exempel:

* Förifyll anpassat formulär genom att fråga efter information från [!DNL Microsoft Dynamics] enheter och tjänster
* Anropa [!DNL Microsoft Dynamics] serveråtgärder som definieras i en formulärdatamodell med hjälp av adaptiva formulärregler
* Skriv skickade formulärdata till [!DNL Microsoft Dynamics] enheter

<!--It is recommended to create a copy of the Form Data Model provided with the [!DNL Experience Manager Forms] package and configure data models and services to suit your requirements. It will ensure that any future updates to the package do not override your form data model.-->

Mer information om hur du skapar och använder formulärdatamodell i affärsarbetsflöden finns i [Dataintegrering](data-integration.md).

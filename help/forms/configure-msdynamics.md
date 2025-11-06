---
title: Hur konfigurerar jag Microsoft Dynamics 365 ur kartongen med formulärdatamodeller för Adaptive Forms?
description: Lär dig hur du integrerar Microsoft Dynamics 365 med Adaptive Forms.
feature: Adaptive Forms, Form Data Model
role: User, Developer
exl-id: 29ee324c-cd4c-403b-bb3d-b1eda8e8ad88
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '869'
ht-degree: 0%

---


# Konfigurera Microsoft® Dynamics 365 för AEM Forms

Adobe Experience Manager Forms Data Integration innehåller en molntjänstkonfiguration som integrerar formulär med Microsoft Dynamics server. Det gör att du kan skapa FDM (Form Data Model) baserat på de enheter, attribut och tjänster som definieras i Microsoft Dynamics. Formulärdatamodellen (FDM) kan användas för att skapa adaptiv Forms som samverkar med Microsoft Dynamics-servern för att möjliggöra affärsarbetsflöden. Till exempel:

* Fråga Microsoft Dynamics-servern efter data och fyll i adaptiva Forms i förväg.
* Skriv data i Microsoft Dynamics när ni skickar in anpassade blanketter.
* Skriv data i Microsoft Dynamics via anpassade entiteter som definieras i FDM (Form Data Model).

AEM as a Cloud Service erbjuder olika inskickningsåtgärder för att hantera inskickade formulär. Du kan läsa mer om de här alternativen i artikeln [Åtgärd för att skicka anpassade formulär](/help/forms/configure-submit-actions-core-components.md).

<!-- 
[[!DNL Experience Manager Forms] Data Integration](data-integration.md) provides [!DNL Microsoft&reg; Dynamics 365] Cloud Services to integrate Adaptive Forms with out of the box Form Data Model (FDM). The Adaptive Forms can then interact with [!DNL Microsoft&reg; Dynamics 365] servers to enable business workflows. For example:

* Write data into [!DNL Microsoft&reg; Dynamics 365] on Adaptive Form submission.
* Write data in [!DNL Microsoft&reg; Dynamics 365] through custom entities defined in Form Data Model (FDM) and conversely.
* Query [!DNL Microsoft&reg; Dynamics 365]server for data and prepopulate Adaptive Forms.
* Read data from [!DNL Microsoft&reg; Dynamics 365] server.

[!DNL Microsoft&reg; Dynamics 365] cloud services and Form Data Model (FDM) are available out of the box on the [!DNL AEM Forms] Server after you [set up a development project for Forms based on Experience Manager archetype](setup-local-development-environment.md#forms-cloud-service-local-development-environment).

>[!NOTE]
>
>Microsoft&reg; Dynamics 365 cloud services and Form Data Model (FDM) are available out of the box only if you set up an [!DNL Experience Manager Forms] as a [!DNL Cloud Service] project based on [AEM Archetype 30](https://github.com/adobe/aem-project-archetype/releases/tag/aem-project-archetype-30) or later.-->

## Förutsättningar

Kontrollera att du har utfört följande steg innan du integrerar [!DNL Microsoft® Dynamics 365] med AEM Forms as a Cloud Service:


1. **Konfigurera kontot i Microsoft Dynamics 365**

   Följ stegen som förklaras i videon för att konfigurera ett Microsoft Dynamics 365-konto. I den här videon skapas ett provkonto för demonstrationssyften.

   >[!VIDEO](https://video.tv.adobe.com/v/3444389/)

1. **Skapa ett konto i Power Platform Admin Center**

   Skapa ett konto i **Power Platform Admin Center** för att:

   * Lägg till dataversion
   * Aktivera Microsoft Dynamics 365-program

   Följ stegen i videon för att skapa ett konto i Power Platform Admin Center. I den här videon har ett provkonto skapats i demonstrationssyfte.

   >[!VIDEO](https://video.tv.adobe.com/v/3444388)

1. **Registrera ett program för [!DNL Microsoft® Dynamics 365] i Azure Active Directory**

   Följ stegen i videon för att registrera ett program för [!DNL Microsoft® Dynamics 365] i Azure Active Directory.

   >[!VIDEO](https://video.tv.adobe.com/v/3444369/dynamics365integration-microsoftdynamics-apiaccess-azuread-appregistration)

   >[!NOTE]
   >
   >* Om du vill skapa det anslutna [!DNL Microsoft® Dynamics 365]-programmet väljer du **Webb** som plattform och anger **Omdirigerings-URI** i följande format: `https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/fdm.html`.
   >* Spara klient-ID:t (även kallat program-ID) och klienthemligheten för framtida referens.

## Anslut Forms till Microsoft® Dynamics 365

När du har konfigurerat ovanstående krav kan du fortsätta integrera Adaptive Forms med Microsoft® Dynamics 365. Så här skickar du data till Microsoft® Dynamics 365 när du skickar in formulär:

[&#x200B;1. Konfigurera molntjänstkonfiguration för Microsoft Dynamics](#1-configure-cloud-service-configuration-for-microsoft-dynamics)

[&#x200B;2. Skapa FDM (Form Data Model)](#2-create-form-data-model-fdm)

### &#x200B;1. Konfigurera molntjänstkonfiguration för Microsoft Dynamics

>[!VIDEO](https://video.tv.adobe.com/v/3444370/cloudconfiguration-dataintegration-adobeexperiencemanager-aemforms-microsoftdynamics)

Utför följande steg för att konfigurera molntjänstkonfigurationen [!DNL Microsoft® Dynamics 365]:

1. Navigera till **[!UICONTROL Tools]** ![hammer](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Data Sources]** på [!DNL AEM Forms]-författarinstansen.

   ![Välj molndata för Source](/help/forms/assets/dynamics-data-source.png)
1. Välj en konfigurationsbehållare. Konfigurationen lagras i den valda konfigurationsbehållaren.
1. Klicka på **[!UICONTROL Create]**.

   ![Skapa molnkonfiguration](/help/forms/assets/dynamics-select-configuration.png)

   Konfigurationsguiden **Skapa Source-konfiguration** visas.

   ![Guiden Skapa Source-konfiguration för data](/help/forms/assets/dynamics-create-data-configuration.png)

1. Ange **[!UICONTROL Title]**, **[!UICONTROL Name]** och välj **[!UICONTROL Service Type]** som **OData-tjänst**.
1. Klicka på **[!UICONTROL Next]**. Fliken **Autentisering** visas.

   ![Autentiseringsflik](/help/forms/assets/dynamics-authentication-tab.png)

1. Ange värdet för fältet **[!UICONTROL Service Root]**.

   Gå till din Dynamics-instans i **Power Platform Admin Center** och navigera till [Developer Resources](https://docs.microsoft.com/en-us/powerapps/developer/data-platform/view-download-developer-resources) för att visa värdet för **Service Root**. **Webb-API-slutpunkten** representerar **tjänstroten**-värdet för Dynamics-instansen som du vill integrera med Adaptiv Forms. URL:en för **tjänstroten** har följande format: `https://<tenant-name>.dynamics.com/api/data/v9.1/`

   ![Tjänstens rotfält](/help/forms/assets/dynamics-service-root.png)

1. Välj **[!UICONTROL Authentication Type]** som **OAuth2.0**.
1. Ange **klient-ID** (kallas program-ID) och **klienthemlighet** för det anslutna programmet.
Du kan hämta **klient-ID** och **klienthemlighet** från Azure Active Directory-programmet.

   ![Klient-ID och klienthemlighet](/help/forms/assets/dynamics-azure-app-resgistration.png)

1. Ange följande i fälten **[!UICONTROL OAuth URL]**, **[!UICONTROL Refresh Token URL]** och **[!UICONTROL Access Token URL]**.
Du kan hämta **[!UICONTROL OAuth URL]**, **[!UICONTROL Refresh Token URL]** och **[!UICONTROL Access Token URL]** från avsnittet **Endpoints** i ditt Azure Active Directory-program.

   ![Azure App Endpoints](/help/forms/assets/dynamics-azure-app-endpoints.png)

1. Ange `openid` i fältet **[!UICONTROL Authorization Scope]** för auktoriseringsprocess på [!DNL Microsoft® Dynamics 365].
1. Ange URL:en för dynamicinstansen i fältet **[!UICONTROL Resource]** om du vill konfigurera [!DNL Microsoft® Dynamics 365] med en formulärdatamodell (FDM).
Du kan kopiera **miljö-URL:en** från **Power Platform Admin Center** eller härleda Dynamics-instansens URL med hjälp av **Service Root** -URL:en. Resurs-URL har följande format: `https://<tenant-name>.dynamics.com`.

   ![Power App Resource Field](/help/forms/assets/dynamics-resource-field.png)

1. Logga in med dina [!DNL Microsoft® Dynamics 365]-autentiseringsuppgifter och godkänn för att tillåta molntjänstkonfigurationen att ansluta till [!DNL Microsoft® Dynamics 365]-tjänsten. Om anslutningen lyckas omdirigeras du till konfigurationssidan för molntjänsten [!DNL Microsoft® Dynamics 365] som visar ett meddelande om att anslutningen lyckades.
1. Välj **[!UICONTROL Create]** om du vill spara konfigurationen.

### &#x200B;2. Skapa FDM (Form Data Model)

>[!VIDEO](https://video.tv.adobe.com/v/3444367/aemforms-adobeexperiencemanager-formdatamodel--dataintegration-digitalforms)

Du kan använda molnkonfigurationen [!DNL Microsoft® Dynamics 365] för att skapa formulärdatamodellen (FDM). Så här skapar du en formulärdatamodell:

1. Navigera till **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Data Integrations]**.
   ![Skapa formulärdatamodell](/help/forms/assets/dynamics-create-fdm.png)

1. Klicka på **[!UICONTROL Create]** och välj **[!UICONTROL Form data Model]**.
   ![Välj formulärdatamodell](/help/forms/assets/dynamics-select-fdm.png)

   Guiden **Skapa formulärdatamodell** visas.
1. Klicka på **[!UICONTROL Next]**.
1. Välj den skapade molnkonfigurationen på fliken **Välj datakälla**.
   ![Välj molnkonfiguration](/help/forms/assets/dynamics-select-cloud-config.png)

1. Klicka på ikonen Redigera ![Redigera](assets/edit.png) för att visa och konfigurera formulärdatamodellen (FDM).

Därefter kan du [konfigurera formulärdatamodellen (FDM)](/help/forms/work-with-form-data-model.md#configure-services) och använda den i olika användningsområden för adaptiva formulär, till exempel:

* Förifyll anpassat formulär genom att fråga efter information från [!DNL Microsoft Dynamics] enheter och tjänster
* Anropa [!DNL Microsoft Dynamics] serveråtgärder som definierats i en FDM (Form Data Model) med hjälp av regler för anpassat formulär
* Skriv skickade formulärdata till [!DNL Microsoft Dynamics] entiteter
* Du kan konfigurera formulärdatamodellens överföringsåtgärd för ett anpassat formulär så att data skickas till [!DNL Microsoft Dynamics].

Du kan sedan använda alternativet [Skicka med FDM (Form Data Model)](/help/forms/using-form-data-model.md) i ett **anpassat formulär** för att överföra data från formuläret till det konfigurerade [!DNL Microsoft® Dynamics 365].


>[!MORELIKETHIS]
>
>* [Konfigurera datakällor för AEM Forms](/help/forms/configure-data-sources.md)
>* [Konfigurera Azure-lagring för AEM Forms](/help/forms/configure-azure-storage.md)
>  [Lägg till Forms Portal på en AEM Sites-sida &#x200B;](/help/forms/configure-forms-portal.md)

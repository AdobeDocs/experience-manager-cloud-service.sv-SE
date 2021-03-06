---
title: Hur konfigurerar jag Microsoft Dynamics 365 och Salesforce från formulärdatamodeller för anpassningsbara formulär?
description: Lär dig hur du integrerar Microsoft Dynamics 365 och Salesforce med adaptiva formulär.
exl-id: 2a43b2db-2dfb-4c79-88be-ea770b44dac1
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '869'
ht-degree: 0%

---

# Konfigurera [!DNL Microsoft Dynamics 365] och [!DNL Salesforce] molntjänster {#configure-azure-storage}

[[!DNL Experience Manager Forms] Dataintegrering](data-integration.md) innehåller [!DNL Microsoft Dynamics 365] och [!DNL Salesforce] molntjänster för att integrera adaptiva formulär med formulärdatamodeller. Den adaptiva Forms kan sedan interagera med [!DNL Microsoft Dynamics 365] och [!DNL Salesforce] servrar för att möjliggöra arbetsflöden. Till exempel:

* Skriv data i [!DNL Microsoft Dynamics 365] och [!DNL Salesforce] om inlämning av anpassade blanketter.
* Skriv data i [!DNL Microsoft Dynamics 365] och [!DNL Salesforce] via anpassade entiteter som definierats i formulärdatamodellen och vice versa.
* Fråga [!DNL Microsoft Dynamics 365] och [!DNL Salesforce] för data och förifylla Adaptive Forms.
* Läs data från [!DNL Microsoft Dynamics 365] och [!DNL Salesforce] server.

[!DNL Microsoft Dynamics 365] och [!DNL Salesforce] molntjänster och formulärdatamodeller är tillgängliga direkt i [!DNL AEM Forms] efter [skapa ett utvecklingsprojekt för Forms baserat på Experience Manager-arkitypen](setup-local-development-environment.md##forms-cloud-service-local-development-environment).

>[!NOTE]
>
>Microsoft Dynamics 365 och [!DNL Salesforce] molntjänster och formulärdatamodeller är bara tillgängliga när du konfigurerar en [!DNL Experience Manager Forms] som [!DNL Cloud Service] projekt baserat på [AEM Archetype 30](https://github.com/adobe/aem-project-archetype/releases/tag/aem-project-archetype-30) eller senare.

## Konfigurera [!DNL Salesforce] molntjänst {#configure-salesforce-cloud-service}

Innan du konfigurerar [!DNL Salesforce] molntjänster, se till att du utför följande uppgifter:

* [Skapa en ansluten OAuth-aktiverad [!DNL Salesforce] program](https://help.salesforce.com/s/articleView?id=sf.connected_app_create_api_integration.htm&amp;type=5). När du skapar de anslutna [!DNL Salesforce] anger du återanrops-URL i följande format:

   ```
   https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html
   ```

   Där server och port refererar till värdnamnet och portnumret för [!DNL AEM Forms] server.

* När du skapar den anslutna [!DNL Salesforce] program, ange `full` och `offline_access` som värden för OAuth-omfånget.

* Notera värdena för klient-ID:t (kallas konsumentnyckel) och klienthemlighet (kallas konsumenthemlighet) för det anslutna programmet.

Utför följande steg för att konfigurera [!DNL Salesforce] molntjänst:

1. På [!DNL AEM Forms] författarinstans, navigera till **[!UICONTROL Tools]** ![hammare](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Data Sources]**. I listan över tillgängliga omslutningsmappar finns en mapp med den rubrik som har angetts för `DappTitle`  while [generera AEM arkivtypsprojekt](setup-local-development-environment.md##forms-cloud-service-local-development-environment).
1. Tryck på mappnamnet och välj **[!UICONTROL Salesforce Cloud Config]** och trycka **[!UICONTROL Properties]**.
1. I **[!UICONTROL Authentication Settings]** tab:
   1. Ange [!DNL Salesforce] Domänens URL i **[!UICONTROL Host]** fält. Till exempel: [Domännamn].my.salesforce.com.
   1. Ange klient-ID (kallas konsumentnyckel) och klienthemlighet (kallas konsumenthemlighet) för det anslutna programmet.
   1. Ange **full offline_access** (`full` och `offine_access` värden som avgränsas av ett blanksteg) i **[!UICONTROL Authorization Scope]** fält.
   1. Tryck på **[!UICONTROL Connect to OAuth]**. Du omdirigeras till [!DNL Microsoft Dynamics] inloggningssida.
   1. Logga in med [!DNL Salesforce] autentiseringsuppgifter och acceptera för att tillåta molntjänstkonfigurationen att ansluta till [!DNL Salesforce] service. Om anslutningen lyckas omdirigeras du till [!DNL Salesforce] konfigurationssida för molntjänster, som visar ett meddelande om att molntjänsten lyckades.
1. Tryck **[!UICONTROL Save & Close]** för att slutföra konfigurationsinställningarna.

### Åtkomst direkt [!DNL Salesforce] Formulärdatamodell

A [!DNL Salesforce] Formulärdatamodellen är tillgänglig direkt i dialogrutan [!DNL AEM Forms] efter [skapa ett utvecklingsprojekt för Forms baserat på Experience Manager-arkitypen](setup-local-development-environment.md##forms-cloud-service-local-development-environment).

Om du vill komma åt formulärdatamodellen går du till **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Data Integrations]**. Listan med tillgängliga mappar innehåller en mapp med den titel som angetts för `DappTitle`  while [generera AEM arkivtypsprojekt](setup-local-development-environment.md##forms-cloud-service-local-development-environment). Tryck på mappnamnet och välj **[!UICONTROL Salesforce Data Model]** och tryck på Redigera ![Redigera](assets/edit.png) om du vill visa formulärdatamodellen.

När du har konfigurerat [[!DNL Salesforce] Konfigurationstjänst för molnet](#configure-salesforce-cloud-service)kan du integrera adaptiva formulär direkt [!DNL Salesforce] Datamodell.

## Konfigurera [!DNL Microsoft Dynamics 365] molntjänst {#configure-dynamics-cloud-service}

Innan du konfigurerar [!DNL Microsoft Dynamics 365] molntjänst, se till att du utför följande uppgifter:

* [Registrera en ansökan för [!DNL Microsoft Dynamics 365] med Azure Active Directory](https://docs.microsoft.com/en-us/powerapps/developer/data-platform/walkthrough-register-app-azure-active-directory). När du skapar de anslutna [!DNL Microsoft Dynamics 365] anger du svars-URL:erna i följande format:

   ```
   https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html
   ```

   Där server och port refererar till värdnamnet och portnumret för [!DNL AEM Forms] server.

* Notera värdena för klient-ID (kallas även program-ID) och klienthemlighet för det anslutna programmet.

Utför följande steg för att konfigurera [!DNL Microsoft Dynamics 365] molntjänst:

1. På [!DNL AEM Forms] författarinstans, navigera till **[!UICONTROL Tools]** ![hammare](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Data Sources]**. I listan över tillgängliga omslutningsmappar finns en mapp med den rubrik som har angetts för `DappTitle`  while [generera AEM arkivtypsprojekt](setup-local-development-environment.md##forms-cloud-service-local-development-environment).
1. Tryck på mappnamnet och välj **[!UICONTROL Microsoft Dynamics 365 Cloud Config]** och trycka **[!UICONTROL Properties]**.
1. I **[!UICONTROL Authentication Settings]** tab:
   1. Ange värdet för **[!UICONTROL Service Root]** fält. Gå till Dynamics-instansen och navigera till [Resurser för utvecklare](https://docs.microsoft.com/en-us/powerapps/developer/data-platform/view-download-developer-resources) för att visa värdet för fältet Tjänstrot. Till exempel, `https://<tenant-name>.dynamics.com/api/data/v9.1/`
   1. Ange klient-ID (kallas program-ID) och klienthemlighet för det anslutna programmet.
   1. Ersätt `{tenant}` med ett klient-ID i **[!UICONTROL OAuth URL]**, **[!UICONTROL Refresh Token URL]** och **[!UICONTROL Access Token URL]** fält.
   1. Ange URL:en för dynamicinstansen i **[!UICONTROL Resource]** fält att konfigurera [!UICONTROL Microsoft Dynamics] med en formulärdatamodell. Använd tjänstens rot-URL för att härleda Dynamics-instansens URL. Till exempel, `https://<tenant-name>.dynamics.com`.

   1. Ange `openid` i **[!UICONTROL Authorization Scope]** fält för auktoriseringsprocess på [!DNL Microsoft Dynamics 365].
   1. Logga in med [!DNL Microsoft Dynamics 365] autentiseringsuppgifter och acceptera för att tillåta molntjänstkonfigurationen att ansluta till [!DNL Microsoft Dynamics 365] service. Om anslutningen lyckas omdirigeras du till [!DNL Microsoft Dynamics 365] konfigurationssida för molntjänster, som visar ett meddelande om att molntjänsten lyckades.
1. Tryck **[!UICONTROL Save & Close]** för att slutföra konfigurationsinställningarna.

### Åtkomst direkt [!DNL Microsoft Dynamics 365] Formulärdatamodell

A [!DNL Microsoft Dynamics 365] Formulärdatamodellen är tillgänglig direkt i dialogrutan [!DNL AEM Forms] efter [skapa ett utvecklingsprojekt för Forms baserat på Experience Manager-arkitypen](setup-local-development-environment.md##forms-cloud-service-local-development-environment).

Om du vill komma åt formulärdatamodellen går du till **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Data Integrations]**. Listan med tillgängliga mappar innehåller en mapp med den titel som angetts för `DappTitle`  while [generera AEM arkivtypsprojekt](setup-local-development-environment.md##forms-cloud-service-local-development-environment). Tryck på mappnamnet och välj **[!UICONTROL Microsoft Dynamics 365 Data Model]** och tryck på Redigera ![Redigera](assets/edit.png) om du vill visa formulärdatamodellen.

När du har konfigurerat [[!DNL Microsoft Dynamics 365] Konfigurationstjänst för molnet](#configure-dynamics-cloud-service)kan du integrera adaptiva formulär direkt [!DNL Microsoft Dynamics 365] Datamodell.

---
title: Hur konfigurerar jag Microsoft Dynamics 365 och Salesforce från kartongdatamodeller för Adaptiv Forms?
description: Lär dig hur du integrerar Microsoft Dynamics 365 och Salesforce med Adaptiv Forms.
feature: Adaptive Forms, Form Data Model
role: User, Developer
exl-id: 2a43b2db-2dfb-4c79-88be-ea770b44dac1
source-git-commit: 7b31a2ea016567979288c7a8e55ed5bf8dfc181d
workflow-type: tm+mt
source-wordcount: '896'
ht-degree: 1%

---

# Konfigurera Microsoft® Dynamics 365 eller Salesforce för AEM Forms {#configure-azure-storage}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/oauth2-client-credentials-flow-for-server-to-server-integration.html) |
| AEM as a Cloud Service | Den här artikeln |

[[!DNL Experience Manager Forms] Dataintegrering](data-integration.md) tillhandahåller [!DNL Microsoft® Dynamics 365]- och [!DNL Salesforce]-molntjänster för att integrera adaptiva formulär med FDM (Form Data Model). Den adaptiva Forms-servern kan sedan interagera med [!DNL Microsoft® Dynamics 365]- och [!DNL Salesforce]-servrar för att möjliggöra affärsarbetsflöden. Till exempel:

* Skriv data i [!DNL Microsoft® Dynamics 365] och [!DNL Salesforce] när du skickar adaptiva formulär.
* Skriv data i [!DNL Microsoft® Dynamics 365] och [!DNL Salesforce] via anpassade entiteter som definierats i formulärdatamodellen (FDM) och omvänt.
* Fråga [!DNL Microsoft® Dynamics 365] och [!DNL Salesforce]-servern efter data och fyll i anpassad Forms i förväg.
* Läs data från [!DNL Microsoft® Dynamics 365] och [!DNL Salesforce]-servern.

[!DNL Microsoft® Dynamics 365] och [!DNL Salesforce] molntjänster och FDM (Form Data Model) är tillgängliga direkt på [!DNL AEM Forms]-servern efter att du [har konfigurerat ett utvecklingsprojekt för Forms baserat på Experience Manager-typen](setup-local-development-environment.md#forms-cloud-service-local-development-environment).

>[!NOTE]
>
>Microsoft® Dynamics 365- och [!DNL Salesforce]-molntjänster och FDM (Form Data Model) är bara tillgängliga direkt om du konfigurerar ett [!DNL Experience Manager Forms] som [!DNL Cloud Service] -projekt baserat på [AEM Archetype 30](https://github.com/adobe/aem-project-archetype/releases/tag/aem-project-archetype-30) eller senare.

## Konfigurera molntjänsten [!DNL Salesforce] {#configure-salesforce-cloud-service}

Innan du konfigurerar molntjänsterna [!DNL Salesforce] måste du utföra följande åtgärder:

* [Skapa ett anslutet OAuth-aktiverat [!DNL Salesforce] program](https://help.salesforce.com/s/articleView?id=sf.connected_app_create_api_integration.htm&amp;type=5). När du skapar det anslutna [!DNL Salesforce]-programmet anger du återanrops-URL:en i följande format:

  ```
  https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html
  ```

  Där server och port refererar till värdnamnet och portnumret för servern [!DNL AEM Forms].

* När du skapar det anslutna [!DNL Salesforce]-programmet anger du `full` och `offline_access` som värden för OAuth-omfånget.

* Notera värdena för klient-ID:t (kallas konsumentnyckel) och klienthemlighet (kallas konsumenthemlighet) för det anslutna programmet.

Utför följande steg för att konfigurera molntjänsten [!DNL Salesforce]:

1. På [!DNL AEM Forms]-författarinstansen går du till **[!UICONTROL Tools]** ![hammer](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Data Sources]**. Listan med tillgängliga omslutningsmappar innehåller en mapp med den rubrik som har angetts för `DappTitle` när det AEM arkivtypsprojektet [ genereras](setup-local-development-environment.md#forms-cloud-service-local-development-environment).
1. Markera mappnamnet, markera **[!UICONTROL Salesforce Cloud Config]** och välj **[!UICONTROL Properties]**.
1. På fliken **[!UICONTROL Authentication Settings]**:
   1. Ange [!DNL Salesforce]-domänens URL i fältet **[!UICONTROL Host]**. Exempel: [Domännamn].my.salesforce.com.
   1. Ange klient-ID (kallas konsumentnyckel) och klienthemlighet (kallas konsumenthemlighet) för det anslutna programmet.
   1. Ange **fullständig offline_access** (`full` och `offine_access` värden avgränsade med blanksteg) i fältet **[!UICONTROL Authorization Scope]**.
   1. Välj **[!UICONTROL Connect to OAuth]**. Du omdirigeras till inloggningssidan för [!DNL Microsoft® Dynamics].
   1. Logga in med dina [!DNL Salesforce]-autentiseringsuppgifter och godkänn för att tillåta molntjänstkonfigurationen att ansluta till [!DNL Salesforce]-tjänsten. Om anslutningen lyckas omdirigeras du till konfigurationssidan för molntjänsten [!DNL Salesforce] som visar ett meddelande om att anslutningen lyckades.
1. Välj **[!UICONTROL Save & Close]** för att slutföra konfigurationsinställningarna.

### Åtkomst från rutan [!DNL Salesforce] i FDM (Form Data Model)

En [!DNL Salesforce]-formulärdatamodell (FDM) är tillgänglig direkt på [!DNL AEM Forms]-servern när du [har konfigurerat ett utvecklingsprojekt för Forms baserat på Experience Manager-arketypen](setup-local-development-environment.md#forms-cloud-service-local-development-environment).

Om du vill komma åt formulärdatamodellen (FDM) går du till **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Data Integrations]**. Listan med tillgängliga mappar innehåller en mapp med den rubrik som har angetts för `DappTitle` när det AEM arkivtypsprojektet [ genereras](setup-local-development-environment.md#forms-cloud-service-local-development-environment). Markera mappnamnet, markera **[!UICONTROL Salesforce Data Model]** och välj ikonen Redigera ![Redigera](assets/edit.png) för att visa formulärdatamodellen (FDM).

När du har konfigurerat [[!DNL Salesforce] Cloud Config-tjänsten](#configure-salesforce-cloud-service) kan du integrera adaptiva formulär med datamodellen [!DNL Salesforce] som finns i kartongen.

## Konfigurera molntjänsten [!DNL Microsoft® Dynamics 365] {#configure-dynamics-cloud-service}

Innan du konfigurerar molntjänsten [!DNL Microsoft® Dynamics 365] måste du utföra följande åtgärder:

* [Registrera ett program för  [!DNL Microsoft® Dynamics 365] med Azure Active Directory](https://docs.microsoft.com/en-us/powerapps/developer/data-platform/walkthrough-register-app-azure-active-directory). När du skapar det anslutna [!DNL Microsoft® Dynamics 365]-programmet anger du svars-URL:erna i följande format:

  ```
  https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html
  ```

  Där server och port refererar till värdnamnet och portnumret för servern [!DNL AEM Forms].

* Notera värdena för klient-ID (kallas även program-ID) och klienthemlighet för det anslutna programmet.

Utför följande steg för att konfigurera molntjänsten [!DNL Microsoft® Dynamics 365]:

1. På [!DNL AEM Forms]-författarinstansen går du till **[!UICONTROL Tools]** ![hammer](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Data Sources]**. Listan med tillgängliga omslutningsmappar innehåller en mapp med den rubrik som har angetts för `DappTitle` när det AEM arkivtypsprojektet [ genereras](setup-local-development-environment.md#forms-cloud-service-local-development-environment).
1. Markera mappnamnet, markera **[!UICONTROL Microsoft® Dynamics 365 Cloud Config]** och välj **[!UICONTROL Properties]**.
1. På fliken **[!UICONTROL Authentication Settings]**:
   1. Ange värdet för fältet **[!UICONTROL Service Root]**. Gå till Dynamics-instansen och navigera till [Resurser för utvecklare](https://docs.microsoft.com/en-us/powerapps/developer/data-platform/view-download-developer-resources) för att visa värdet för fältet Tjänstrot. Exempel: `https://<tenant-name>.dynamics.com/api/data/v9.1/`
   1. Ange klient-ID (kallas program-ID) och klienthemlighet för det anslutna programmet.
   1. Ersätt `{tenant}` med ett klient-ID i fälten **[!UICONTROL OAuth URL]**, **[!UICONTROL Refresh Token URL]** och **[!UICONTROL Access Token URL]**.
   1. Ange URL:en för dynamicinstansen i fältet **[!UICONTROL Resource]** om du vill konfigurera [!UICONTROL Microsoft® Dynamics] med en formulärdatamodell (FDM). Använd tjänstens rot-URL för att härleda Dynamics-instansens URL. Exempel: `https://<tenant-name>.dynamics.com`.

   1. Ange `openid` i fältet **[!UICONTROL Authorization Scope]** för auktoriseringsprocess på [!DNL Microsoft® Dynamics 365].
   1. Logga in med dina [!DNL Microsoft® Dynamics 365]-autentiseringsuppgifter och godkänn för att tillåta molntjänstkonfigurationen att ansluta till [!DNL Microsoft® Dynamics 365]-tjänsten. Om anslutningen lyckas omdirigeras du till konfigurationssidan för molntjänsten [!DNL Microsoft® Dynamics 365] som visar ett meddelande om att anslutningen lyckades.
1. Välj **[!UICONTROL Save & Close]** för att slutföra konfigurationsinställningarna.

### Åtkomst från rutan [!DNL Microsoft® Dynamics 365] i FDM (Form Data Model)

En [!DNL Microsoft® Dynamics 365]-formulärdatamodell (FDM) är tillgänglig direkt på [!DNL AEM Forms]-servern när du [har konfigurerat ett utvecklingsprojekt för Forms baserat på Experience Manager-arketypen](setup-local-development-environment.md##forms-cloud-service-local-development-environment).

Om du vill komma åt formulärdatamodellen (FDM) går du till **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Data Integrations]**. Listan med tillgängliga mappar innehåller en mapp med den rubrik som har angetts för `DappTitle` när det AEM arkivtypsprojektet [ genereras](setup-local-development-environment.md#forms-cloud-service-local-development-environment). Markera mappnamnet, markera **[!UICONTROL Microsoft® Dynamics 365 Data Model]** och välj ikonen Redigera ![Redigera](assets/edit.png) för att visa formulärdatamodellen (FDM).

När du har konfigurerat [[!DNL Microsoft® Dynamics 365] Cloud Config-tjänsten](#configure-dynamics-cloud-service) kan du integrera adaptiva formulär med datamodellen [!DNL Microsoft® Dynamics 365] som finns i kartongen.

>[!MORELIKETHIS]
>
>* [Konfigurera datakällor för AEM Forms](/help/forms/configure-data-sources.md)
>* [Konfigurera Azure-lagring för AEM Forms](/help/forms/configure-azure-storage.md)
>  [Lägg till Forms Portal på en AEM Sites-sida ](/help/forms/configure-forms-portal.md)

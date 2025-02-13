---
title: Hur konfigurerar man Salesforce från sin egen kartong för adaptiva Forms?
description: Lär dig hur du integrerar Salesforce med Adaptive Forms.
feature: Adaptive Forms, Form Data Model
role: User, Developer
source-git-commit: 3a12fff170f521f6051f0c24a4eb28a12439eec1
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 0%

---


# Konfigurera Salesforce för AEM Forms {#configure-azure-storage}

[[!DNL Experience Manager Forms] Dataintegrering](data-integration.md) tillhandahåller [!DNL Salesforce] molntjänster för integrering av adaptiv Forms med OTB-formulärdatamodell (FDM). Den adaptiva Forms-servern kan sedan interagera med [!DNL Salesforce]-servrar för att möjliggöra affärsarbetsflöden. Till exempel:

* Skriv data i [!DNL Salesforce] när adaptiva formulär skickas.
* Skriv data i [!DNL Salesforce] via anpassade entiteter som definierats i formulärdatamodellen (FDM) och omvänt.
* Fråga [!DNL Salesforce]-servern efter data och fylla i Adaptiv Forms i förväg.
* Läs data från servern [!DNL Salesforce].

[!DNL Salesforce] molntjänster och FDM (Form Data Model) är tillgängliga direkt på [!DNL AEM Forms]-servern efter att du [har konfigurerat ett utvecklingsprojekt för Forms baserat på Experience Manager arkivtyp](setup-local-development-environment.md#forms-cloud-service-local-development-environment).

>[!NOTE]
>
>[!DNL Salesforce] molntjänster och FDM (Form Data Model) är bara tillgängliga i paketet om du konfigurerar ett [!DNL Experience Manager Forms] som ett [!DNL Cloud Service]-projekt baserat på [AEM Archetype 30](https://github.com/adobe/aem-project-archetype/releases/tag/aem-project-archetype-30) eller senare.

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

1. På [!DNL AEM Forms]-författarinstansen går du till **[!UICONTROL Tools]** ![hammer](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Data Sources]**.
2. Markera mappnamnet, markera **[!UICONTROL Salesforce Cloud Config]** och välj **[!UICONTROL Properties]**.
3. På fliken **[!UICONTROL Authentication Settings]**:
   1. Ange [!DNL Salesforce]-domänens URL i fältet **[!UICONTROL Host]**. Exempel: [Domännamn].my.salesforce.com.
   2. Ange klient-ID (kallas konsumentnyckel) och klienthemlighet (kallas konsumenthemlighet) för det anslutna programmet.
   3. Ange **fullständig offline_access** (`full` och `offine_access` värden avgränsade med blanksteg) i fältet **[!UICONTROL Authorization Scope]**.
   4. Välj **[!UICONTROL Connect to OAuth]**. Du omdirigeras till inloggningssidan för [!DNL Salesforce].
   5. Logga in med dina [!DNL Salesforce]-autentiseringsuppgifter och godkänn för att tillåta molntjänstkonfigurationen att ansluta till [!DNL Salesforce]-tjänsten. Om anslutningen lyckas omdirigeras du till konfigurationssidan för molntjänsten [!DNL Salesforce] som visar ett meddelande om att anslutningen lyckades.
4. Välj **[!UICONTROL Save & Close]** för att slutföra konfigurationsinställningarna.

### Åtkomst från rutan [!DNL Salesforce] i FDM (Form Data Model)

En [!DNL Salesforce]-formulärdatamodell (FDM) är tillgänglig direkt på [!DNL AEM Forms]-servern efter att du [har konfigurerat ett utvecklingsprojekt för Forms baserat på Experience Manager-arkityp](setup-local-development-environment.md#forms-cloud-service-local-development-environment).

Så här kommer du åt formulärdatamodellen (FDM):
1. Navigera till **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Data Integrations]**.
1. Markera mappnamnet, markera **[!UICONTROL Salesforce Data Model]** och välj ikonen Redigera ![Redigera](assets/edit.png) för att visa formulärdatamodellen (FDM).

När du har konfigurerat [[!DNL Salesforce] Cloud Config-tjänsten](#configure-salesforce-cloud-service) kan du integrera adaptiva formulär med datamodellen [!DNL Salesforce] som finns i kartongen.

>[!MORELIKETHIS]
>
>* [Konfigurera datakällor för AEM Forms](/help/forms/configure-data-sources.md)
>* [Konfigurera Azure-lagring för AEM Forms](/help/forms/configure-azure-storage.md)
>  [Lägg till Forms Portal på en AEM Sites-sida ](/help/forms/configure-forms-portal.md)

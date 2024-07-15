---
title: Konfigurera AEM Assets som en [!DNL Cloud Service] med Brand Portal
description: Lär dig hur du konfigurerar AEM Assets med Brand Portal. Med konfigurationen kan du publicera godkända varumärkesresurser från en AEM till Brand Portal och distribuera dem till Brand Portal-användare.
contentOwner: AK
feature: Brand Portal, Asset Distribution, Configuration
role: Admin
exl-id: 078e522f-bcd8-4734-95db-ddc8772de785
source-git-commit: ab2cf8007546f538ce54ff3e0b92bb0ef399c758
workflow-type: tm+mt
source-wordcount: '1717'
ht-degree: 7%

---

# Konfigurera Experience Manager Assets med Brand Portal {#configure-aem-assets-with-brand-portal}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/assets/brandportal/configure-aem-assets-with-brand-portal.html?lang=en) |
| AEM as a Cloud Service | Den här artikeln |

När du konfigurerar Adobe Experience Manager Assets Brand Portal kan du publicera godkända varumärkesresurser från Adobe Experience Manager Assets som en [!DNL Cloud Service]-instans till Brand Portal och distribuera dem till Brand Portal-användare.

## Aktivera Brand Portal med Cloud Manager {#activate-brand-portal}

Cloud Manager-användaren aktiverar Brand Portal för en Experience Manager Assets som en [!DNL Cloud Service]-instans. Aktiveringsarbetsflödet skapar de nödvändiga konfigurationerna (auktoriseringstoken, IMS-konfiguration och Brand Portal molntjänst) i backend och återspeglar statusen för Brand Portal-klientorganisationen i Cloud Manager. Genom att aktivera Brand Portal kan Experience Manager Assets-användare publicera material till Brand Portal och distribuera dem till Brand Portal-användare.

**Förutsättningar**

Du behöver följande för att aktivera Brand Portal på din Experience Manager Assets som en [!DNL Cloud Service]-instans:

* En Experience Manager Assets som körs som en [!DNL Cloud Service]-instans.
* En användare som har tillgång till Cloud Manager, tilldelad till Profiler för Cloud Manager-produkten. Mer information finns i [Åtkomst till Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html#accessing-cloud-manager).

>[!NOTE]
>
>En konfigurerad produktionsmiljö krävs för en Experience Manager Assets som en [!DNL Cloud Service]-instans för att ansluta till Brand Portal-klientorganisationen.

**Steg för att aktivera Brand Portal**

Du kan aktivera Brand Portal när du skapar produktionsmiljöer för din Experience Manager Assets som en [!DNL Cloud Service]-instans, eller separat. Låt oss anta att miljön redan har skapats, och du måste nu aktivera Brand Portal.

1. Logga in på Adobe Cloud Manager och gå till **[!UICONTROL Environments]**.

   Sidan **[!UICONTROL Environments]** visar en lista över alla befintliga miljöer.

1. Välj miljöer (en efter en) i listan för att visa miljöinformationen.

   Brand Portal har rätt till en av de tillgängliga miljöerna och återspeglas under **[!UICONTROL Environment Information]**.

   När du har hittat den miljö som är associerad med Brand Portal klickar du på knappen **[!UICONTROL Activate Brand Portal]** för att starta aktiveringsarbetsflödet.

   ![Aktivera Brand Portal](assets/create-environment4.png)

1. Det tar några minuter att aktivera Brand Portal-klienten när aktiveringsarbetsflödet skapar de nödvändiga konfigurationerna i backend-läget. När Brand Portal-klienten har aktiverats ändras statusen till Aktiverad.

   ![Visa status](assets/create-environment5.png)


>[!NOTE]
>
>Brand Portal måste aktiveras på samma IMS-organisation som Experience Manager Assets som en [!DNL Cloud Service]-instans.
>
>Om du har en befintlig molnkonfiguration för Brand Portal ([konfigurerad manuellt med Adobe Developer Console](#manual-configuration)) för en IMS-organisation (org1-befintlig) och din Experience Manager Assets som [!DNL Cloud Service]-instans har konfigurerats för en annan IMS-organisation (org2-new), återställs Brand Portal IMS-organisationen till `org2-new` när du aktiverar Brand Portal från Cloud Manager. Även om den manuellt konfigurerade molnkonfigurationen på `org1-existing` är synlig i Experience Manager Assets-författarinstansen, men kommer inte längre att användas när Brand Portal har aktiverats från Cloud Manager.
>
>Om den befintliga Brand Portal-molnkonfigurationen och Experience Manager Assets som en [!DNL Cloud Service]-instans använder samma IMS-organisation (org1) behöver du bara aktivera Brand Portal från Cloud Manager.
>
>Ändra inte några autogenererade inställningar.

**Se även**:

* [Lägg till användare och roller i Experience Manager Assets as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html)

* [Hantera miljöer i Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html#adding-environments)


**Logga in på din Brand Portal-klient**:

När du har aktiverat din Brand Portal-klient i Cloud Manager kan du logga in på Brand Portal från Admin Console eller direkt med klientens URL.

Brand Portal-klientens standardwebbadress är: `https://<tenant-id>.brand-portal.adobe.com/`.

Där är innehavar-ID:t IMS-organisationen.


Utför följande steg om du inte är säker på Brand Portal URL:

1. Logga in på [Admin Console](https://adminconsole.adobe.com/) och navigera till **[!UICONTROL Products]**.
1. Välj **[!UICONTROL Adobe Experience Manager Brand Portal – Brand Portal]** i den vänstra panelen.
1. Klicka på **[!UICONTROL Go to Brand Portal]** om du vill öppna Brand Portal direkt i webbläsaren.

   Eller kopiera Brand Portal klientorganisations-URL:en från länken **[!UICONTROL Go to Brand Portal]** och klistra in den i webbläsaren för att öppna Brand Portal gränssnitt.

   ![Öppna Brand Portal](assets/access-bp-on-cloud.png)


**Testa anslutningen**

Utför följande steg för att validera anslutningen mellan din Experience Manager Assets som en [!DNL Cloud Service]-instans och Brand Portal-klientorganisation:

1. Logga in på Experience Manager Assets.

1. Navigera till **[!UICONTROL Deployment]** > **[!UICONTROL Distribution]** från panelen **Verktyg**.

   ![Navigera till distributionsalternativet](assets/test-bpconfig1.png)

   En Brand Portal-distributionsagent (**[!UICONTROL bpdistributionagent0]**) har skapats under **[!UICONTROL Publish to Brand Portal]**.

   ![Skapa distributionsagent](assets/test-bpconfig2.png)

1. Klicka på **[!UICONTROL Publish to Brand Portal]** för att öppna distributionsagenten.

   Du kan se distributionsköerna på fliken **[!UICONTROL Status]**.

   En distributionsagent har två köer:
   * **processing-queue**: för distribution av resurser till varumärkesportalen.

   * **error-queue**: för resurser där distributionen misslyckades.

   >[!NOTE]
   >
   >Vi rekommenderar att du regelbundet granskar felen och rensar **error-queue**.

   ![Bearbetar kön för distribution av resurser](assets/test-bpconfig3.png)

1. Om du vill verifiera anslutningen mellan Experience Manager Assets som [!DNL Cloud Service] och Brand Portal klickar du på ikonen **[!UICONTROL Test Connection]** .

   ![Kontrollera anslutningen mellan AEM och Brand Portal](assets/test-bpconfig4.png)

   Ett meddelande visas om att *testpaketet har levererats*.

   >[!NOTE]
   >
   >Undvik att inaktivera distributionsagenten eftersom det kan göra att distributionen av resurserna (i kön) misslyckas.

Om du vill verifiera anslutningen mellan din Experience Manager Assets som en [!DNL Cloud Service]-instans och Brand Portal-klient publicerar du en resurs från Experience Manager Assets till Brand Portal. Om anslutningen lyckas visas den publicerade resursen i Brand Portal-gränssnittet.


Du kan nu:

* [Publish-material från Experience Manager Assets till Brand Portal](publish-to-brand-portal.md)
* [Publish-mappar från Experience Manager Assets till Brand Portal](publish-to-brand-portal.md#publish-folders-to-brand-portal)
* [Publish-kollektioner från Experience Manager Assets till Brand Portal](publish-to-brand-portal.md#publish-collections-to-brand-portal)
* [Publish-resurser från Brand Portal till Experience Manager Assets](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html) - Resurshantering i Brand Portal
* [Publicera förinställningar, scheman och fasetter på varumärkesportalen](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/publish-schema-search-facets-presets.html)
* [Publicera taggar på varumärkesportalen](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/brand-portal-publish-tags.html)

Mer information finns i [Brand Portal-dokumentationen](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html).

**Distributionsloggar**

Du kan övervaka distributionsagentloggarna för publiceringsarbetsflödet.

Låt oss nu publicera en mediefil från Experience Manager Assets till Brand Portal och se loggarna.

1. Följ stegen (från 1 till 4) enligt avsnittet **Testanslutning** och navigera till distributionsagentsidan.
1. Klicka på **[!UICONTROL Logs]** om du vill visa bearbetnings- och felloggarna.

   ![Bearbetnings- och felloggar](assets/test-bpconfig5.png)

Distributionsagenten har genererat följande loggar:

* INFO: Det är en systemgenererad logg som utlöser en lyckad konfiguration av distributionsagenten.
* DSTRQ1 (Begäran 1): Utlöses vid testanslutning.

Följande begärande- och svarsloggar genereras när resursen publiceras:

**Begäranden från distributionsagenten**:

* DSTRQ2 (Begäran 2): Begäran om publicering av resurser utlöses.
* DSTRQ3 (begäran 3): Systemet utlöser en annan begäran om att publicera Experience Manager Assets-mappen (där resursen finns) och replikerar mappen i Brand Portal.

**Svar från distributionsagenten**:

* queue-bpdistributionagent0 (DSTRQ2): Resursen publiceras på varumärkesportalen.
* queue-bpdistributagent0 (DSTRQ3): Systemet replikerar Experience Manager Assets-mappen (som innehåller resursen) i Brand Portal.

I exemplet ovan utlöses ytterligare en begäran och ett svar. Det gick inte att hitta den överordnade mappen (Lägg till sökväg) i Brand Portal eftersom resursen publicerades för första gången. Därför utlöstes en ytterligare begäran om att skapa en överordnad mapp med samma namn i Brand Portal där resursen publiceras.

>[!NOTE]
>
>Ytterligare begäran genereras om den överordnade mappen inte finns i Brand Portal eller har ändrats i Experience Manager Assets.

Förutom automatiseringsarbetsflödet för att aktivera Brand Portal på Experience Manager Assets som [!DNL Cloud Service] finns det en annan metod för att manuellt konfigurera Experience Manager Assets som en [!DNL Cloud Service] med Brand Portal med hjälp av Adobe Developer Console som inte längre rekommenderas.

>[!NOTE]
>
>Kontakta kundsupport om du har problem med att aktivera din Brand Portal-klient.

## Manuell konfiguration med Adobe Developer Console {#manual-configuration}

>[!NOTE]
>
> Du kan inte skapa nya JWT-autentiseringsuppgifter från och med juni 2024. Härifrån skapas endast OAuth-autentiseringsuppgifter.
> Se mer [skapa en OAuth-konfiguration](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/security/setting-up-ims-integrations-for-aem-as-a-cloud-service#creating-oauth-configuration:~:text=For%20example%3A-,Creating%20an%20OAuth%20configuration,-To%20create%20a).

I följande avsnitt beskrivs hur du konfigurerar Experience Manager Assets manuellt som en [!DNL Cloud Service] med Brand Portal med Adobe Developer Console.

Tidigare konfigurerades Experience Manager Assets som [!DNL Cloud Service] manuellt med Brand Portal via Adobe Developer Console, som anskaffar en kontotoken för Adobe Identity Management Services (IMS) för auktorisering av Brand Portal-klienten. Det kräver konfigurationer i både Experience Manager Assets och Adobe Developer Console.

<!--1. In Experience Manager Assets, create an IMS account and generate a public key (certificate).-->
<!--1. Under the project, configure an API using the public key to create a service account connection.
1. Get the service account credentials and JSON Web Token (JWT) payload information.
1. In Experience Manager Assets, configure the IMS account using the service account credentials and JWT payload.-->
1. I Adobe Developer Console skapar du ett projekt för din Brand Portal-klient (organisation).
1. I Experience Manager Assets konfigurerar du Brand Portal molntjänst med hjälp av IMS-kontot och Brand Portal slutpunkt (organisations-URL).
1. Testa konfigurationen genom att publicera en resurs från Experience Manager Assets till Brand Portal.

>[!NOTE]
>
>En Experience Manager Assets som en [!DNL Cloud Service]-instans får endast konfigureras med en Brand Portal-klientorganisation.

**Förutsättningar**

Du behöver följande för att konfigurera Experience Manager Assets med Brand Portal:

* En Experience Manager Assets som körs som en [!DNL Cloud Service]-instans
* En Brand Portal tenant-URL
* En användare med systemadministratörsbehörighet för IMS-organisationen för Brand Portal-klienten

## Skapa konfiguration {#create-new-configuration}

Utför följande steg i den angivna sekvensen för att konfigurera Experience Manager Assets med Brand Portal.

1. [Konfigurera OAuth-autentiseringsuppgifterna i Adobe Developer Console](#config-oauth)
1. [Skapa en ny Adobe IMS-integrering med OAuth](#create-ims-account-configuration)
1. [Konfigurera molntjänsten](#configure-cloud-service)
   <!--1. [Obtain public certificate](#public-certificate)-->
<!--1. [Create service account (JWT) connection](#createnewintegration) 
1. [Configure IMS account](#create-ims-account-configuration)-->

<!--
### Create IMS configuration {#create-ims-configuration}

The IMS configuration authenticates your Experience Manager Assets as a [!DNL Cloud Service] instance with the Brand Portal tenant. 

IMS configuration includes two steps:

* [Obtain public certificate](#public-certificate) 
* [Configure IMS account](#create-ims-account-configuration)
-->
<!--

### Obtain public certificate {#public-certificate}

The public key (certificate) authenticates your profile on Adobe Developer Console.

1. Login to Experience Manager Assets.
1. From the **Tools** panel, navigate to **[!UICONTROL Security]** > **[!UICONTROL Adobe IMS Configurations]**.
1. In Adobe IMS Configurations page, click **[!UICONTROL Create]**. It will redirect to the **[!UICONTROL Adobe IMS Technical Account Configuration]** page. By default, the **Certificate** tab opens.
1. Select **[!UICONTROL Adobe Brand Portal]** in the **[!UICONTROL Cloud Solution]** drop-down list.  
1. Select the **[!UICONTROL Create new certificate]** check box and specify an **alias** for the public key. The alias serves as name of the public key. 
1. Click **[!UICONTROL Create certificate]**. Then, click **[!UICONTROL OK]** to generate the public key.

   ![Create Certificate](assets/ims-config2.png)

1. Click the **[!UICONTROL Download Public Key]** icon and save the public key (CRT) file on your machine.

   The public key is used later to configure API for your Brand Portal tenant and generate service account credentials in Adobe Developer Console.  

   ![Download Certificate](assets/ims-config3.png)

1. Click **[!UICONTROL Next]**.

    In the **Account** tab, Adobe IMS account is created which requires the service account credentials that are generated in Adobe Developer Console. Keep this page open for now.

    Open a new tab and [create a service account (JWT) connection in Adobe Developer Console](#createnewintegration) to get the credentials and JWT payload for configuring the IMS account. 
-->
<!--

### Create service account (JWT) connection {#createnewintegration}

In Adobe Developer Console, projects and APIs are configured at Brand Portal tenant (organization) level. Configuring an API creates a service account (JWT) connection. There are two methods to configure API, by generating a key pair (private and public keys) or by uploading a public key. To configure Experience Manager Assets with Brand Portal, you must generate a public key (certificate) in Experience Manager Assets and create credentials in Adobe Developer Console by uploading the public key. These credentials are required to configure the IMS account in Experience Manager Assets. Once the IMS account is configured, you can configure the Brand Portal cloud service in Experience Manager Assets.

Perform the following steps to generate the service account credentials and JWT payload:

1. Login to Adobe Developer Console with system administrator privileges on the IMS organization (Brand Portal tenant). The default URL is [https://www.adobe.com/go/devs_console_ui](https://www.adobe.com/go/devs_console_ui).


   >[!NOTE]
   >
   >Ensure that you have selected the correct IMS organization (Brand Portal tenant) from the drop-down (organization) list located at the upper-right corner.

1. Click **[!UICONTROL Create new project]**. A blank project with a system-generated name is created for your organization. 

   Click **[!UICONTROL Edit project]** to update the **[!UICONTROL Project Title]** and **[!UICONTROL Description]**, and click **[!UICONTROL Save]**.
   
1. In the **[!UICONTROL Project overview]** tab, click **[!UICONTROL Add API]**.

1. In the **[!UICONTROL Add an API window]**, select **[!UICONTROL AEM Brand Portal]** and click **[!UICONTROL Next]**. 

   Ensure that you have access to the Experience Manager Brand Portal service.

1. In the **[!UICONTROL Configure API]** window, click **[!UICONTROL Upload your public key]**. Then, click **[!UICONTROL Select a File]** and upload the public key (.crt file) that you have downloaded in the [obtain public certificate](#public-certificate) section. 

   Click **[!UICONTROL Next]**.

   ![Upload Public Key](assets/service-account3.png)

1. Verify the public key and click **[!UICONTROL Next]**.

1. Select **[!UICONTROL Assets Brand Portal]** as the default product profile and click **[!UICONTROL Save configured API]**. 

   ![Select Product Profile](assets/service-account4.png)

1. Once the API is configured, you are redirected to the API overview page. From the left navigation under **[!UICONTROL Credentials]**, click the **[!UICONTROL Service Account (JWT)]** option.

   >[!NOTE] 
   >
   >* You can view the credentials and perform actions such as generate JWT tokens, copy credential details, retrieve client secret, and so on.
   >* Currently, only the Adobe's Developer Console Service Account (JWT) credential type is supported. Do not use the `OAuth Server-to-Server` credential type until it is supported in mid-April. Read more at [JWT Credentials Deprecation in Adobe Developer Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/jwt-credentials-deprecation-in-adobe-developer-console.html).

1. From the **[!UICONTROL Client Credentials]** tab, copy the **[!UICONTROL client ID]**. 

   Click **[!UICONTROL Retrieve Client Secret]** and copy the **[!UICONTROL client secret]**.

   ![Service Account Credentials](assets/service-account5.png)

1. Navigate to the **[!UICONTROL Generate JWT]** tab and copy the **[!UICONTROL JWT Payload]** information. 

You can now use the client ID (API key), client secret, and JWT payload to [configure the IMS account](#create-ims-account-configuration) in Experience Manager Assets.
-->
<!--
1. Click **[!UICONTROL Create Integration]**.

1. Select **[!UICONTROL Access an API]**, and click **[!UICONTROL Continue]**.

   ![Create New Integration](assets/create-new-integration1.png)

1. Create an integration page. 
   
   Select your organization from the drop-down list.

   In **[!UICONTROL Experience Cloud]**, Select **[!UICONTROL AEM Brand Portal]** and click **[!UICONTROL Continue]**. 

   If the Brand Portal option is disabled for you, ensure that you have selected correct organization from the drop-down box above the **[!UICONTROL Adobe Services]** option. If you do not know your organization, contact your administrator.

   ![Create Integration](assets/create-new-integration2.png)

1. Specify a name and description for the integration. Click **[!UICONTROL Select a File from your computer]** and upload the `AEM-Adobe-IMS.crt` file downloaded in the [obtain public certificates](#public-certificate) section.

1. Select the profile of your organization. 

   Or, select the default profile **[!UICONTROL Assets Brand Portal]** and click **[!UICONTROL Create Integration]**. The integration is created.

1. Click **[!UICONTROL Continue to integration details]** to view the integration information. 

   Copy the **[!UICONTROL API Key]** 
   
   Click **[!UICONTROL Retrieve Client Secret]** and copy the Client Secret key.

   ![API Key, Client Secret, and payload information of an integration](assets/create-new-integration3.png)

1. Navigate to **[!UICONTROL JWT]** tab, and copy the **[!UICONTROL JWT payload]**.

   The API Key, Client Secret key, and JWT payload information is used to create IMS account configuration.

-->

### Konfigurera OAuth-autentiseringsuppgifterna i Adobe Developer Console {#config-oauth}

[Konfigurera OAuth-autentiseringsuppgifterna i Adobe Developer Console](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/security/setting-up-ims-integrations-for-aem-as-a-cloud-service#credentials-in-the-developer-console) och välj Brand Portal API.

### Skapa ny Adobe IMS-integrering med OAuth {#create-ims-account-configuration}

[Skapa en ny Adobe IMS-integrering med OAuth](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/security/setting-up-ims-integrations-for-aem-as-a-cloud-service#creating-oauth-configuration) och välj Brand Portal i listrutan under Cloud Solution.

<!--
Ensure that you have performed the following steps:

* [Obtain public certificate](#public-certificate)
* [Create service account (JWT) connection](#createnewintegration)
-->

<!--1. Open the IMS Configuration and navigate to the **[!UICONTROL Account]** tab. Keep the page open while [obtaining the public certificate](#public-certificate).

1. Specify a **[!UICONTROL Title]** for the IMS account.

   In the **[!UICONTROL Authorization Server]** field, specify the URL: [https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/)  
-->
<!--
1. Complete the configuration based on details from the [Developer Console](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation/). Click **[!UICONTROL Create]**.
-->
<!--Specify client ID in the **[!UICONTROL API key]** field, **[!UICONTROL Client Secret]**, and **[!UICONTROL Payload]** (JWT payload) that you have copied while [creating the service account (JWT) connection](#createnewintegration).

   The IMS account is configured. 

   ![IMS Account configuration](assets/create-new-integration6.png)

 <!--  
1. Select the IMS account configuration and click **[!UICONTROL Check Health]**.

   Click **[!UICONTROL Check]** in the dialog box. On successful configuration, a message appears that the *Token is retrieved successfully*.

   ![Adobe IMS Configurations Check Health.](assets/create-new-integration5.png)
-->
<!--
>[!CAUTION]
>
>You must have only one IMS configuration.
>
>Ensure that the IMS configuration passes the health check. If the configuration does not pass the health check, it is invalid. You must delete it and create another valid configuration.
-->

### Konfigurera molntjänst {#configure-cloud-service}

Så här konfigurerar du molntjänsten i Brand Portal:

1. Logga in på Experience Manager Assets.

1. Navigera till **[!UICONTROL Cloud Services]** > **[!UICONTROL AEM Brand Portal]** från panelen **Verktyg**.

1. Klicka på **[!UICONTROL Create]** på sidan Brand Portal-konfigurationer.

1. Ange en **[!UICONTROL Title]** för konfigurationen.

   Välj den IMS-konfiguration som du skapade när du [konfigurerade IMS-kontot](#create-ims-account-configuration).

   I fältet **[!UICONTROL Service URL]** anger du din Brand Portal tenant-URL (organisation).

   ![Dialogrutan Brand Portal-konfiguration.](assets/create-cloud-service.png)

1. Klicka på **[!UICONTROL Save & Close]**. Molnkonfigurationen skapas.

   Din Experience Manager Assets som en [!DNL Cloud Service]-instans har nu konfigurerats med Brand Portal-klienten.

Du kan nu testa konfigurationen genom att kontrollera distributionsagenten och publicera resurser på Brand Portal.

**Tillåtslista IP-adresser i SPS om säker förhandsvisning är aktiverat**
Om du använder Dynamic Media-Scene7 med [säker förhandsvisning aktiverat](#https://experienceleague.adobe.com/docs/dynamic-media-classic/using/upload-publish/testing-assets-making-them-public.html?lang=en) för ett företag rekommenderar vi att Scene7 företagsadministratör [tillåtslista IP-adresserna för offentliga utgångar ](#https://experienceleague.adobe.com/docs/dynamic-media-classic/using/upload-publish/testing-assets-making-them-public.html?lang=en#testing-the-secure-testing-service) för respektive region med hjälp av SPS (Scene7 Publishing System) flash UI.
IP-adresserna för utgångar är följande:

| **Region** | **Utreses-IP** |
|--- |--- |
| NA | 130.248.160.68, 20.94.203.130 |
| EMEA | 51.132.146.75, 130.248.244.202, 130.248.244.203, 130.248.244.204, 130.2 48.244.210, 130.248.244.211, 130.248.244.212 |
| APAC | 63.140.44.54 |

<!--
### Test configuration {#test-configuration}

Perform the following steps to validate the configuration:

1. Login to AEM Assets.

1. From the **Tools** panel, navigate to **[!UICONTROL Deployment]** > **[!UICONTROL Distribution]**.

    ![test-bpconfig1](assets/test-bpconfig1.png)

   A Brand Portal distribution agent (**[!UICONTROL bpdistributionagent0]**) is created under **[!UICONTROL Publish to Brand Portal]**.

   ![test-bpconfig2](assets/test-bpconfig2.png)


1. Click **[!UICONTROL Publish to Brand Portal]** to open the distribution agent. 

   You can see the distribution queues under the **[!UICONTROL Status]** tab. 
   
   A distribution agent contains two queues: 
   * **processing-queue**: for the distribution of assets to Brand Portal. 

   * **error-queue**: for the assets where distribution has failed. 
   
   >[!NOTE]
   >
   >It is recommended to review the failures and  clear the **error-queue** periodically.  

   ![test-bpconfig3](assets/test-bpconfig3.png)

1. To verify the connection between AEM Assets as a [!DNL Cloud Service] and Brand Portal, click the **[!UICONTROL Test Connection]** icon.

   ![test-bpconfig4](assets/test-bpconfig4.png)

   A message appears that your *test package is successfully delivered*.

   >[!NOTE]
   >
   >Avoid disabling the distribution agent, as it can cause the distribution of the assets (running-in-queue) to fail.

You can now:

* [Publish assets from AEM Assets to Brand Portal](publish-to-brand-portal.md)
* [Publish folders from AEM Assets to Brand Portal](publish-to-brand-portal.md#publish-folders-to-brand-portal)
* [Publish collections from AEM Assets to Brand Portal](publish-to-brand-portal.md#publish-collections-to-brand-portal)
* [Publish assets from Brand Portal to AEM Assets](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html) - Asset Sourcing in Brand Portal
* [Publish presets, schemas, and facets to Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/publish-schema-search-facets-presets.html)
* [Publish tags to Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/brand-portal-publish-tags.html)

See [Brand Portal documentation](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) for more information.

## Distribution logs {#distribution-logs}

You can monitor the distribution agent logs for the asset publishing workflow. 

For example, we have published an asset from AEM Assets to Brand Portal to validate the configuration. 

1. Follow the steps (from 1 to 4) as shown in the [Test Configuration](#test-configuration) section and navigate to the distribution agent page.
1. Click **[!UICONTROL Logs]** to view the processing and error logs.

   ![ctest-bpconfig4](assets/ctest-bpconfig4.png)

The distribution agent has generated the following logs:

* INFO: This is a system-generated log that triggers on successful configuration of the distribution agent. 
* DSTRQ1 (Request 1): Triggers on test connection.

On publishing the asset, the following request and response logs are generated:

**Distribution agent request**:

* DSTRQ2 (Request 2): The asset publishing request is triggered.
* DSTRQ3 (Request 3): The system triggers another request to publish the AEM Assets folder (in which the asset exists) and replicates the folder in Brand Portal.

**Distribution agent response**:

* queue-bpdistributionagent0 (DSTRQ2): The asset is published to Brand Portal.
* queue-bpdistributionagent0 (DSTRQ3): The system replicates the AEM Assets folder (containing the asset) in Brand Portal.

In the above example, an additional request and response is triggered. The system could not find the parent folder (Add Path) in Brand Portal because the asset was published for the first time, therefore, it triggered an additional request to create a parent folder with the same name in Brand Portal where the asset is published.  

>[!NOTE]
>
>Additional request is generated in case the parent folder does not exist in Brand Portal or has been modified in AEM Assets. 
-->

<!--

## Additional information {#additional-information}

Go to `/system/console/slingmetrics` for statistics related to the distributed content:

1. **Counter metrics**
   * sling: `mac_sync_request_failure`
   * sling: `mac_sync_request_received`
   * sling: `mac_sync_request_success`

1. **Time metrics**
   * sling: `mac_sync_distribution_duration`
   * sling: `mac_sync_enqueue_package_duration`
   * sling: `mac_sync_setup_request_duration`

-->

<!--
   Comment Type: draft

   <li> </li>
   -->

<!--
   Comment Type: draft

   <li>Step text</li>
-->

**Se även**

* [Översätt Assets](translate-assets.md)
* [ASSETS HTTP API](mac-api-assets.md)
* [Filformat som stöds av Assets](file-format-support.md)
* [Sök resurser](search-assets.md)
* [Anslutna resurser](use-assets-across-connected-assets-instances.md)
* [Resursrapporter](asset-reports.md)
* [Metadata-scheman](metadata-schemas.md)
* [Hämta resurser](download-assets-from-aem.md)
* [Hantera metadata](manage-metadata.md)
* [Sök efter ansikten](search-facets.md)
* [Hantera samlingar](manage-collections.md)
* [Import av massmetadata](metadata-import-export.md)
* [Publish Assets till AEM och Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)

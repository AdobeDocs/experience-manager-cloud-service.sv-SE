---
title: Konfigurera AEM Assets som en [!DNL Cloud Service] med varumärkesportalen
description: Konfigurera AEM Assets med varumärkesportalen.
contentOwner: Vishabh Gupta
feature: Brand Portal,Asset Distribution,Configuration
role: Administrator
exl-id: 078e522f-bcd8-4734-95db-ddc8772de785
translation-type: tm+mt
source-git-commit: d3c19e460f72a980e058ef6117f6352bda4d1e8a
workflow-type: tm+mt
source-wordcount: '2274'
ht-degree: 13%

---

# Konfigurera AEM Assets som en [!DNL Cloud Service] med varumärkesportalen {#configure-aem-assets-with-brand-portal}

När du konfigurerar Adobe Experience Manager Assets Brand Portal kan du publicera godkända varumärkesresurser från Adobe Experience Manager Assets som en [!DNL Cloud Service]-instans på varumärkesportalen och distribuera dem till användarna på varumärkesportalen.

## Aktivera varumärkesportalen med hjälp av Cloud Manager {#activate-brand-portal}

Cloud Manager-användaren aktiverar varumärkesportalen för en AEM Assets som en [!DNL Cloud Service]-instans. Aktiveringsarbetsflödet skapar de nödvändiga konfigurationerna (auktoriseringstoken, IMS-konfiguration och molntjänsten Brand Portal) i bakgrunden och speglar statusen för innehavaren av varumärkesportalen i Cloud Manager. Genom att aktivera Brand Portal kan AEM Assets-användare publicera material på Brand Portal och distribuera dem till Brand Portal-användarna.

**Förutsättningar**

Du behöver följande för att aktivera varumärkesportalen på din AEM Assets som en [!DNL Cloud Service]-instans:

* En AEM Assets som körs som en [!DNL Cloud Service]-instans.
* En användare som har åtkomst till Cloud Manager som tilldelats profiler för Cloud Manager-produkten. Mer information finns i [Åtkomst till Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html?lang=en#accessing-cloud-manager).

>[!NOTE]
>
>En AEM Assets som [!DNL Cloud Service]-instans har bara rätt att ansluta till en Brand Portal-klient. Du kan ha flera miljöer (utveckling, produktion och scen) för din AEM Assets som en [!DNL Cloud Service]-instans, där Brand Portal aktiveras i en miljö.

**Steg för att aktivera varumärkesportalen**

Du kan aktivera Brand Portal när du skapar miljöer för din AEM Assets som en [!DNL Cloud Service]-instans, eller separat. Låt oss anta att miljöerna redan har skapats, och du måste nu aktivera Brand Portal.

1. Logga in på Adobe Cloud Manager och navigera till **[!UICONTROL Environments]**.

   På sidan **[!UICONTROL Environments]** visas en lista över alla befintliga miljöer.

1. Välj miljöer (en efter en) i listan för att visa miljöinformationen.

   Varumärkesportalen har rätt till en av de tillgängliga miljöerna och visas under **[!UICONTROL Environment Information]**.

   När du har hittat den miljö som är kopplad till varumärkesportalen klickar du på knappen **[!UICONTROL Activate Brand Portal]** för att starta aktiveringsarbetsflödet.

   ![Aktivera varumärkesportal](assets/create-environment4.png)

1. Det tar några minuter att aktivera innehavaren av varumärkesportalen när aktiveringsarbetsflödet skapar de nödvändiga konfigurationerna i serverdelen. När klienten för varumärkesportalen har aktiverats ändras statusen till Aktiverad.

   ![Visa status](assets/create-environment5.png)


>[!NOTE]
>
>Varumärkesportalen måste aktiveras i samma IMS-organisation som i AEM Assets som en [!DNL Cloud Service]-instans.
>
>Om du har en befintlig Brand Portal-molnkonfiguration ([manuellt konfigurerad med hjälp av Adobe Developer Console](#manual-configuration)) för en IMS-organisation (org1-befintlig) och din AEM Assets som en [!DNL Cloud Service]-instans är konfigurerad för en annan IMS-organisation (org2-new), återställs Brand Portal från Cloud Manager till `org2-new` . Även om den manuellt konfigurerade molnkonfigurationen på `org1-existing` kommer att visas i AEM Assets författarinstans, men kommer inte längre att användas efter att du har aktiverat Varumärksportal från molnhanteraren.
>
>Om den befintliga Brand Portal-molnkonfigurationen och AEM Assets som en [!DNL Cloud Service]-instans använder samma IMS-organisation (org1) behöver du bara aktivera Brand Portal från Cloud Manager.

**Se även**:
* [Lägga till användare och roller i AEM Assets som en Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/what-is-required/add-users-roles.html?lang=en#role-definitions)

* [Hantera miljöer i Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html?lang=en#adding-environments)


**Logga in på din klient** för varumärkesportalen:

När du har aktiverat din klient för varumärkesportalen i Cloud Manager kan du logga in på Brand Portal från Admin Console eller direkt via innehavarens URL.

Din varumärksportals standardwebbadress är: `https://<tenant-id>.brand-portal.adobe.com/`.

Där är innehavar-ID:t IMS-organisationen.

Utför följande steg om du inte är säker på varumärkesportalens URL:

1. Logga in på [Admin Console](http://adminconsole.adobe.com/) och navigera till **[!UICONTROL Products]**.
1. Välj **[!UICONTROL Adobe Experience Manager Brand Portal – Brand Portal]** i den vänstra listen.
1. Klicka på **[!UICONTROL Go to Brand Portal]** för att öppna varumärkesportalen direkt i webbläsaren.

   Du kan också kopiera innehavar-URL:en för varumärkesportalen från länken **[!UICONTROL Go to Brand Portal]** och klistra in den i webbläsaren för att öppna gränssnittet för varumärkesportalen.

   ![Åtkomst till varumärkesportal](assets/access-bp-on-cloud.png)


**Testanslutning**

Utför följande steg för att validera anslutningen mellan din AEM Assets som en [!DNL Cloud Service]-instans och innehavaren av varumärkesportalen:

1. Logga in på AEM Assets.

1. Gå till **[!UICONTROL Deployment]** > **[!UICONTROL Distribution]** på panelen **Verktyg**.

   ![](assets/test-bpconfig1.png)

   En agent för varumärkesportaldistribution (**[!UICONTROL bpdistributionagent0]**) skapas under **[!UICONTROL Publish to Brand Portal]**.

   ![](assets/test-bpconfig2.png)


1. Klicka på **[!UICONTROL Publish to Brand Portal]** för att öppna distributionsagenten.

   Du kan se distributionsköerna på fliken **[!UICONTROL Status]**.

   En distributionsagent har två köer:
   * **processing-queue**: för distribution av resurser till varumärkesportalen.

   * **error-queue**: för resurser där distributionen misslyckades.
   >[!NOTE]
   >
   >Vi rekommenderar att du regelbundet granskar felen och rensar **error-queue**.

   ![](assets/test-bpconfig3.png)

1. Om du vill verifiera anslutningen mellan AEM Assets som en [!DNL Cloud Service]- och varumärkesportal klickar du på ikonen **[!UICONTROL Test Connection]**.

   ![](assets/test-bpconfig4.png)

   Ett meddelande visas om att ditt *testpaket har levererats*.

   >[!NOTE]
   >
   >Undvik att inaktivera distributionsagenten eftersom det kan göra att distributionen av resurserna (i kön) misslyckas.

Om du vill verifiera anslutningen mellan din AEM Assets som en [!DNL Cloud Service]-instans och innehavaren av varumärkesportalen publicerar du en mediefil från AEM Assets till varumärkesportalen. Om anslutningen lyckas visas den publicerade resursen i gränssnittet för varumärkesportalen.


Du kan nu:

* [Publicera resurser från AEM Assets till varumärkesportalen](publish-to-brand-portal.md)
* [Publicera mappar från AEM Assets till varumärkesportalen](publish-to-brand-portal.md#publish-folders-to-brand-portal)
* [Publicera samlingar från AEM Assets till varumärkesportalen](publish-to-brand-portal.md#publish-collections-to-brand-portal)
* [Publicera material från Brand Portal till AEM Assets](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html?lang=en)  - Resurser i varumärkesportalen
* [Publicera förinställningar, scheman och fasetter på varumärkesportalen](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/publish/publish-schema-search-facets-presets.html)
* [Publicera taggar på varumärkesportalen](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/publish/brand-portal-publish-tags.html)

Mer information finns i [varumärkesportaldokumentationen](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/home.html).

**Distributionsloggar**

Du kan övervaka distributionsagentloggarna för publiceringsarbetsflödet.

Låt oss nu publicera en mediefil från AEM Assets till Brand Portal och se loggarna.

1. Följ stegen (från 1 till 4) som visas i avsnittet **Testa anslutningen** och navigera till sidan för distributionsagenten.
1. Klicka på **[!UICONTROL Logs]** för att visa bearbetnings- och felloggarna.

   ![](assets/test-bpconfig5.png)

Distributionsagenten har genererat följande loggar:

* INFORMATION: Det är en systemgenererad logg som utlöser en lyckad konfiguration av distributionsagenten.
* DSTRQ1 (Begäran 1): Utlöses vid testanslutning.

Följande begärande- och svarsloggar genereras när resursen publiceras:

**Begäranden från distributionsagenten**:

* DSTRQ2 (Begäran 2): Begäran om publicering av resurser utlöses.
* DSTRQ3 (Request 3): Systemet utlöser en annan begäran om att publicera AEM Assets-mappen (där resursen finns) och replikerar mappen i varumärkesportalen.

**Svar från distributionsagenten**:

* queue-bpdistributionagent0 (DSTRQ2): Resursen publiceras på varumärkesportalen.
* queue-bpdistributagent0 (DSTRQ3): Systemet replikerar AEM Assets-mappen (som innehåller resursen) i varumärkesportalen.

I exemplet ovan utlöses ytterligare en begäran och ett svar. Det gick inte att hitta den överordnade mappen (Lägg till sökväg) i varumärkesportalen eftersom resursen publicerades för första gången. Därför utlöstes en ytterligare begäran om att skapa en överordnad mapp med samma namn i varumärkesportalen där resursen publiceras.

>[!NOTE]
>
>Ytterligare begäran genereras om den överordnade mappen inte finns i varumärkesportalen eller har ändrats i AEM Assets.

Förutom automatiseringsarbetsflödet för att aktivera Brand Portal på AEM Assets som [!DNL Cloud Service] finns det en annan metod för att manuellt konfigurera AEM Assets som [!DNL Cloud Service] med Brand Portal med Adobe Developer Console som inte längre rekommenderas.

>[!NOTE]
>
>Kontakta Adobe Support om du har problem med att aktivera din varumärkesportal-klient.

## Manuell konfiguration med Adobe Developer Console {#manual-configuration}

I följande avsnitt beskrivs hur du konfigurerar AEM Assets manuellt som en [!DNL Cloud Service] med varumärkesportalen med hjälp av Adobe Developer Console.

Tidigare konfigurerades AEM Assets som [!DNL Cloud Service] manuellt med Brand Portal via Adobe Developer Console, som köper en kontotoken för Adobe Identity Management Services (IMS) för godkännande av Brand Portal-klienten. Det kräver konfigurationer i båda programmen, AEM Assets och Adobe Developer Console.

1. Skapa ett IMS-konto i AEM Assets och generera en offentlig nyckel (certifikat).
1. Skapa ett projekt för din varumärksportal (organisation) i Adobe Developer Console.
1. Under projektet konfigurerar du ett API med den offentliga nyckeln för att skapa en tjänstkontoanslutning.
1. Hämta tjänstkontots autentiseringsuppgifter och JSON Web Token-nyttolastinformation (JWT).
1. I AEM Assets konfigurerar du IMS-kontot med tjänstkontots autentiseringsuppgifter och JWT-nyttolast.
1. Konfigurera molntjänsten Brand Portal i AEM Assets med hjälp av IMS-kontot och varumärkesportalens slutpunkt (organisations-URL).
1. Testa konfigurationen genom att publicera en resurs från AEM Assets till varumärkesportalen.

>[!NOTE]
>
>En AEM Assets som en [!DNL Cloud Service]-instans ska bara konfigureras med en Brand Portal-klient.

**Förutsättningar**

Du behöver följande för att konfigurera AEM Assets med varumärkesportalen:

* En AEM Assets som körs som en [!DNL Cloud Service]-instans
* En klientorganisations-URL
* En användare med systemadministratörsbehörighet på IMS-organisationen för varumärkesportalens klient

## Skapa en konfiguration {#create-new-configuration}

Utför följande steg i den angivna sekvensen för att konfigurera AEM Assets med varumärkesportalen.

1. [Hämta ett offentligt certifikat](#public-certificate)
1. [Skapa JWT-anslutning (Service Account)](#createnewintegration)
1. [Konfigurera IMS-konto](#create-ims-account-configuration)
1. [Konfigurera molntjänsten](#configure-the-cloud-service)

### Skapa IMS-konfigurationen {#create-ims-configuration}

IMS-konfigurationen autentiserar din AEM Assets som en [!DNL Cloud Service]-instans med innehavaren av varumärkesportalen.

IMS-konfigurationen har två steg:

* [Hämta ett offentligt certifikat](#public-certificate)
* [Konfigurera IMS-konto](#create-ims-account-configuration)

### Hämta ett offentligt certifikat {#public-certificate}

Den offentliga nyckeln (certifikatet) autentiserar din profil på Adobe Developer Console.

1. Logga in på AEM Assets.
1. Gå till **[!UICONTROL Security]** > **[!UICONTROL Adobe IMS Configurations]** på panelen **Verktyg**.
1. Klicka på **[!UICONTROL Create]** på sidan Adobe IMS-konfigurationer. Det dirigeras om till sidan **[!UICONTROL Adobe IMS Technical Account Configuration]**. Som standard öppnas fliken **Certificate**.
1. Välj **[!UICONTROL Adobe Brand Portal]** i listrutan **[!UICONTROL Cloud Solution]**.
1. Markera kryssrutan **[!UICONTROL Create new certificate]** och ange ett **alias** för den offentliga nyckeln. Aliaset används som namn på den offentliga nyckeln.
1. Klicka på **[!UICONTROL Create certificate]**. Klicka sedan på **[!UICONTROL OK]** för att generera den offentliga nyckeln.

   ![Skapa ett certifikat](assets/ims-config2.png)

1. Klicka på ikonen **[!UICONTROL Download Public Key]** och spara filen med den offentliga nyckeln (CRT) på datorn.

   Den offentliga nyckeln används senare för att konfigurera API för din varumärksportal och generera autentiseringsuppgifter för tjänstkontot i Adobe Developer Console.

   ![Hämta certifikatet](assets/ims-config3.png)

1. Klicka på **[!UICONTROL Next]**.

   På fliken **Konto** skapas ett Adobe IMS-konto som kräver inloggningsuppgifterna för tjänstkontot som genereras i Adobe Developer Console. Håll den här sidan öppen tills vidare.

   Öppna en ny flik och [skapa en JWT-anslutning i Adobe Developer Console](#createnewintegration) för att hämta autentiseringsuppgifter och JWT-nyttolast för konfigurering av IMS-kontot.

### Skapa tjänstkontoanslutning (JWT) {#createnewintegration}

I Adobe Developer Console konfigureras projekt och API:er på innehavarnivå för varumärkesportalen (organisation). När du konfigurerar ett API skapas en JWT-anslutning (Service Account). Det finns två metoder för att konfigurera API, genom att generera ett nyckelpar (privata och offentliga nycklar) eller genom att överföra en offentlig nyckel. Om du vill konfigurera AEM Assets med varumärkesportalen måste du skapa en offentlig nyckel (certifikat) i AEM Assets och skapa autentiseringsuppgifter i Adobe Developer Console genom att överföra den offentliga nyckeln. Dessa autentiseringsuppgifter krävs för att konfigurera IMS-kontot i AEM Assets. När IMS-kontot har konfigurerats kan du konfigurera molntjänsten Brand Portal i AEM Assets.

Utför följande steg för att generera autentiseringsuppgifter för tjänstkontot och JWT-nyttolast:

1. Logga in på Adobe Developer Console med systemadministratörsbehörighet för IMS-organisationen (innehavaren av varumärkesportalen). Standardwebbadressen är [https://www.adobe.com/go/devs_console_ui](https://www.adobe.com/go/devs_console_ui).


   >[!NOTE]
   >
   >Se till att du har valt rätt IMS-organisation (innehavaren av varumärkesportalen) i listrutan (organisationen) längst upp till höger.

1. Klicka på **[!UICONTROL Create new project]**. Ett tomt projekt med ett systemgenererat namn skapas för din organisation.

   Klicka på **[!UICONTROL Edit project]** för att uppdatera **[!UICONTROL Project Title]** och **[!UICONTROL Description]** och klicka på **[!UICONTROL Save]**.

1. Klicka på **[!UICONTROL Add API]** på fliken **[!UICONTROL Project overview]**.

1. I **[!UICONTROL Add an API window]** väljer du **[!UICONTROL AEM Brand Portal]** och klickar på **[!UICONTROL Next]**.

   Se till att du har tillgång till tjänsten AEM varumärkesportalen.

1. Klicka på **[!UICONTROL Upload your public key]** i fönstret **[!UICONTROL Configure API]**. Klicka sedan på **[!UICONTROL Select a File]** och överför den publika nyckeln (.crt-filen) som du har hämtat i [Hämta det publika certifikatet](#public-certificate)-avsnittet.

   Klicka på **[!UICONTROL Next]**.

   ![Överför offentlig nyckel](assets/service-account3.png)

1. Kontrollera den offentliga nyckeln och klicka på **[!UICONTROL Next]**.

1. Välj **[!UICONTROL Assets Brand Portal]** som standardproduktprofil och klicka på **[!UICONTROL Save configured API]**.

   <!-- 
   In Brand Portal, a default profile is created for each organization. The Product Profiles are created in admin console for assigning users to groups (based on the roles and permissions). For configuration with Brand Portal, the OAuth token is created at organization level. Therefore, you must configure the default Product Profile for your organization. 
   -->

   ![Välj produktprofil](assets/service-account4.png)

1. När API:t har konfigurerats omdirigeras du till API-översiktssidan. Klicka på alternativet **[!UICONTROL Service Account (JWT)]** i den vänstra navigeringen under **[!UICONTROL Credentials]**.

   >[!NOTE]
   >
   >Du kan visa autentiseringsuppgifterna och utföra åtgärder som att generera JWT-tokens, kopiera autentiseringsuppgifter, hämta klienthemlighet osv.

1. Kopiera **[!UICONTROL client ID]** från fliken **[!UICONTROL Client Credentials]**.

   Klicka på **[!UICONTROL Retrieve Client Secret]** och kopiera **[!UICONTROL client secret]**.

   ![Autentiseringsuppgifter för tjänstkonto](assets/service-account5.png)

1. Navigera till fliken **[!UICONTROL Generate JWT]** och kopiera **[!UICONTROL JWT Payload]**-informationen.

Du kan nu använda klient-ID (API-nyckel), klienthemlighet och JWT-nyttolast för att [konfigurera IMS-kontot](#create-ims-account-configuration) i AEM Assets.

<!--
1. Click **[!UICONTROL Create Integration]**.

1. Select **[!UICONTROL Access an API]**, and click **[!UICONTROL Continue]**.

   ![Create New Integration](assets/create-new-integration1.png)

1. Create a new integration page opens. 
   
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

   The API Key, Client Secret key, and JWT payload information will be used to create IMS account configuration.

-->

### Konfigurera IMS-konto {#create-ims-account-configuration}

Kontrollera att du har utfört följande steg:

* [Hämta ett offentligt certifikat](#public-certificate)
* [Skapa JWT-anslutning (Service Account)](#createnewintegration)

Utför följande steg för att konfigurera IMS-kontot.

1. Öppna IMS-konfigurationen och gå till fliken **[!UICONTROL Account]**. Du höll sidan öppen medan [du hämtade det offentliga certifikatet](#public-certificate).

1. Ange en **[!UICONTROL Title]** för IMS-kontot.

   Ange URL-adressen i fältet **[!UICONTROL Authorization Server]**: [https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/)

   Ange klient-ID i fältet **[!UICONTROL API key]**, **[!UICONTROL Client Secret]** och **[!UICONTROL Payload]** (JWT-nyttolast) som du kopierade när du [skapade tjänstkontoanslutningen (JWT)](#createnewintegration).

   Klicka på **[!UICONTROL Create]**.

   IMS-kontot är konfigurerat.

   ![Konfiguration av ett IMS-konto](assets/create-new-integration6.png)


1. Välj IMS-kontokonfigurationen och klicka på **[!UICONTROL Check Health]**.

   Klicka på **[!UICONTROL Check]** i dialogrutan. När konfigurationen är klar visas ett meddelande om att *token har hämtats*.

   ![](assets/create-new-integration5.png)

>[!CAUTION]
>
>Du får bara ha en IMS-konfiguration.
>
>Kontrollera att IMS-konfigurationen klarar hälsokontrollen. Om konfigurationen inte godkänns i hälsokontrollen är den ogiltig. Du måste ta bort den och skapa en ny, giltig konfiguration.

### Konfigurera molntjänsten{#configure-the-cloud-service}

Så här konfigurerar du molntjänsten Brand Portal:

1. Logga in på AEM Assets.

1. Gå till **[!UICONTROL Cloud Services]** > **[!UICONTROL AEM Brand Portal]** på panelen **Verktyg**.

1. Klicka på **[!UICONTROL Create]** på sidan Konfigurationer för varumärkesportalen.

1. Ange en **[!UICONTROL Title]** för konfigurationen.

   Välj den IMS-konfiguration som du skapade när du konfigurerade IMS-kontot](#create-ims-account-configuration).[

   I fältet **[!UICONTROL Service URL]** anger du din webbadress till innehavaren av varumärkesportalen (organisation).

   ![](assets/create-cloud-service.png)

1. Klicka på **[!UICONTROL Save & Close]**. Molnkonfigurationen har skapats.

   Din AEM Assets som en [!DNL Cloud Service]-instans har nu konfigurerats med innehavaren av varumärkesportalen.

Du kan nu testa konfigurationen genom att kontrollera distributionsagenten och publicera resurser på varumärkesportalen.

<!--
### Test configuration {#test-configuration}

Perform the following steps to validate the configuration:

1. Log in to AEM Assets.

1. From the **Tools** panel, navigate to **[!UICONTROL Deployment]** > **[!UICONTROL Distribution]**.

    ![](assets/test-bpconfig1.png)

   A Brand Portal distribution agent (**[!UICONTROL bpdistributionagent0]**) is created under **[!UICONTROL Publish to Brand Portal]**.

   ![](assets/test-bpconfig2.png)


1. Click **[!UICONTROL Publish to Brand Portal]** to open the distribution agent. 

   You can see the distribution queues under the **[!UICONTROL Status]** tab. 
   
   A distribution agent contains two queues: 
   * **processing-queue**: for the distribution of assets to Brand Portal. 

   * **error-queue**: for the assets where distribution has failed. 
   
   >[!NOTE]
   >
   >It is recommended to review the failures and  clear the **error-queue** periodically.  

   ![](assets/test-bpconfig3.png)

1. To verify the connection between AEM Assets as a [!DNL Cloud Service] and Brand Portal, click on the **[!UICONTROL Test Connection]** icon.

   ![](assets/test-bpconfig4.png)

   A message appears that your *test package is successfully delivered*.

   >[!NOTE]
   >
   >Avoid disabling the distribution agent, as it can cause the distribution of the assets (running-in-queue) to fail.

You can now:

* [Publish assets from AEM Assets to Brand Portal](publish-to-brand-portal.md)
* [Publish folders from AEM Assets to Brand Portal](publish-to-brand-portal.md#publish-folders-to-brand-portal)
* [Publish collections from AEM Assets to Brand Portal](publish-to-brand-portal.md#publish-collections-to-brand-portal)
* [Publish assets from Brand Portal to AEM Assets](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html?lang=en) - Asset Sourcing in Brand Portal
* [Publish presets, schemas, and facets to Brand Portal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/publish/publish-schema-search-facets-presets.html)
* [Publish tags to Brand Portal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/publish/brand-portal-publish-tags.html)

See [Brand Portal documentation](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/home.html) for more information.

## Distribution logs {#distribution-logs}

You can monitor the distribution agent logs for the asset publishing workflow. 

For example, we have published an asset from AEM Assets to Brand Portal to validate the configuration. 

1. Follow the steps (from 1 to 4) as shown in the [Test Configuration](#test-configuration) section and navigate to the distribution agent page.
1. Click **[!UICONTROL Logs]** to view the processing and error logs.

   ![](assets/test-bpconfig5.png)

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

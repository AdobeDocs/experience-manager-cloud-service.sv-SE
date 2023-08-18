---
title: Konfigurera AEM Assets som [!DNL Cloud Service] med Brand Portal
description: Lär dig hur du konfigurerar AEM Assets med Brand Portal. Med konfigurationen kan du publicera godkända varumärkesresurser från en AEM till Brand Portal och distribuera dem till Brand Portal-användare.
contentOwner: AK
feature: Brand Portal,Asset Distribution,Configuration
role: Admin
exl-id: 078e522f-bcd8-4734-95db-ddc8772de785
source-git-commit: 2c8bac8627ed660d2780f93f4018c8fa980e569a
workflow-type: tm+mt
source-wordcount: '2447'
ht-degree: 11%

---

# Konfigurera Experience Manager Assets med Brand Portal {#configure-aem-assets-with-brand-portal}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/assets/brandportal/configure-aem-assets-with-brand-portal.html?lang=en) |
| AEM as a Cloud Service | Den här artikeln |

Om du konfigurerar Adobe Experience Manager Assets Brand Portal kan du publicera godkända varumärkesresurser från Adobe Experience Manager Assets som en [!DNL Cloud Service] till Brand Portal och distribuera dem till Brand Portal-användare.

## Aktivera Brand Portal med Cloud Manager {#activate-brand-portal}

Cloud Manager-användaren aktiverar Brand Portal för en Experience Manager Assets som [!DNL Cloud Service] -instans. Aktiveringsarbetsflödet skapar de nödvändiga konfigurationerna (auktoriseringstoken, IMS-konfiguration och Brand Portal molntjänst) i serverdelen och återspeglar statusen för Brand Portal-klienten i Cloud Manager. Genom att aktivera Brand Portal kan Experience Manager Assets-användare publicera material till Brand Portal och distribuera dem till Brand Portal-användare.

**Förutsättningar**

Du behöver följande för att aktivera Brand Portal på din Experience Manager Assets som [!DNL Cloud Service] instans:

* En Experience Manager Assets som körs som [!DNL Cloud Service] -instans.
* En användare som har åtkomst till Cloud Manager som tilldelats profiler för Cloud Manager-produkten. Se [åtkomst till Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html#accessing-cloud-manager) för mer information.

>[!NOTE]
>
>En konfigurerad produktionsmiljö krävs för en Experience Manager Assets som [!DNL Cloud Service] -instans för att ansluta till Brand Portal tenant.

**Steg för att aktivera Brand Portal**

Du kan aktivera Brand Portal när du skapar produktionsmiljöer för din Experience Manager Assets som en [!DNL Cloud Service] eller separat. Låt oss anta att miljön redan har skapats, och du måste nu aktivera Brand Portal.

1. Logga in på Adobe Cloud Manager och navigera till **[!UICONTROL Environments]**.

   The **[!UICONTROL Environments]** visas en lista med alla befintliga miljöer.

1. Välj miljöer (en efter en) i listan för att visa miljöinformationen.

   Brand Portal har rätt till en av de tillgängliga miljöerna och återspeglas i **[!UICONTROL Environment Information]**.

   När du har hittat den miljö som är kopplad till Brand Portal klickar du på **[!UICONTROL Activate Brand Portal]** för att starta aktiveringsarbetsflödet.

   ![Aktivera Brand Portal](assets/create-environment4.png)

1. Det tar några minuter att aktivera Brand Portal-klienten när aktiveringsarbetsflödet skapar de nödvändiga konfigurationerna i backend-läget. När Brand Portal-klienten har aktiverats ändras statusen till Aktiverad.

   ![Visa status](assets/create-environment5.png)


>[!NOTE]
>
>Brand Portal måste aktiveras i samma IMS-organisation som Experience Manager Assets som [!DNL Cloud Service] -instans.
>
>Om du har en befintlig Brand Portal molnkonfiguration ([konfigureras manuellt med Adobe Developer Console](#manual-configuration)) för en IMS-organisation (org1-existing) och din Experience Manager Assets som [!DNL Cloud Service] -instansen är konfigurerad för en annan IMS-organisation (org2-new), och när du aktiverar Brand Portal från Cloud Manager återställs Brand Portal IMS-organisation till `org2-new`. Även om den manuellt konfigurerade molnkonfigurationen är på `org1-existing` är synligt i Experience Manager Assets författarinstans, men kommer inte längre att användas när Brand Portal har aktiverats från Cloud Manager.
>
>Om Brand Portal molnkonfiguration och Experience Manager Assets är [!DNL Cloud Service] -instansen använder samma IMS-organisation (org1), du behöver bara aktivera Brand Portal från Cloud Manager.
>
>Ändra inte några autogenererade inställningar.

**Se även**:

* [Lägga till användare och roller i Experience Manager Assets as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html)

* [Hantera miljöer i Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html#adding-environments)


**Logga in på din Brand Portal-klient**:

När du har aktiverat din Brand Portal-klient i Cloud Manager kan du logga in på Brand Portal från Admin Console eller direkt med klientens URL.

Brand Portal-klientens standardwebbadress är: `https://<tenant-id>.brand-portal.adobe.com/`.

Där är innehavar-ID:t IMS-organisationen.

Utför följande steg om du inte är säker på Brand Portal URL:

1. Logga in på [Admin Console](https://adminconsole.adobe.com/) och navigera till **[!UICONTROL Products]**.
1. Välj **[!UICONTROL Adobe Experience Manager Brand Portal – Brand Portal]**.
1. Klicka på **[!UICONTROL Go to Brand Portal]** för att öppna Brand Portal direkt i webbläsaren.

   Eller kopiera Brand Portal tenant-URL:en från **[!UICONTROL Go to Brand Portal]** och klistra in den i webbläsaren för att öppna Brand Portal gränssnitt.

   ![Använd Brand Portal](assets/access-bp-on-cloud.png)


**Testanslutning**

Följ de här stegen för att validera anslutningen mellan din Experience Manager Assets som en [!DNL Cloud Service] instans och Brand Portal tenant:

1. Logga in på Experience Manager Assets.

1. Från **verktyg** navigera till **[!UICONTROL Deployment]** > **[!UICONTROL Distribution]**.

   ![Navigera till distributionsalternativet](assets/test-bpconfig1.png)

   En Brand Portal-distributionsagent (**[!UICONTROL bpdistributionagent0]**) skapas under **[!UICONTROL Publish to Brand Portal]**.

   ![Skapa distributionsagent](assets/test-bpconfig2.png)


1. Klicka **[!UICONTROL Publish to Brand Portal]** för att öppna distributionsagenten.

   Du kan se distributionsköerna under **[!UICONTROL Status]** -fliken.

   En distributionsagent har två köer:
   * **processing-queue**: för distribution av resurser till varumärkesportalen.

   * **error-queue**: för resurser där distributionen misslyckades.

   >[!NOTE]
   >
   >Vi rekommenderar att du regelbundet granskar felen och rensar **error-queue**.

   ![Bearbetningskön för distribution av resurser](assets/test-bpconfig3.png)

1. Så här verifierar du anslutningen mellan Experience Manager Assets som [!DNL Cloud Service] och Brand Portal klickar du på **[!UICONTROL Test Connection]** -ikon.

   ![Verifiera anslutningen mellan AEM och Brand Portal](assets/test-bpconfig4.png)

   Ett meddelande visas om att *testpaketet har levererats*.

   >[!NOTE]
   >
   >Undvik att inaktivera distributionsagenten eftersom det kan göra att distributionen av resurserna (i kön) misslyckas.

Så här verifierar du anslutningen mellan din Experience Manager Assets som en [!DNL Cloud Service] -instans och Brand Portal tenant, publicera en mediefil från Experience Manager Assets till Brand Portal. Om anslutningen lyckas visas den publicerade resursen i Brand Portal-gränssnittet.


Du kan nu:

* [Publicera material från Experience Manager Assets till Brand Portal](publish-to-brand-portal.md)
* [Publicera mappar från Experience Manager Assets till Brand Portal](publish-to-brand-portal.md#publish-folders-to-brand-portal)
* [Publicera samlingar från Experience Manager Assets till Brand Portal](publish-to-brand-portal.md#publish-collections-to-brand-portal)
* [Publicera material från Brand Portal till Experience Manager Assets](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html) - Resurshantering i Brand Portal
* [Publicera förinställningar, scheman och fasetter på varumärkesportalen](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/publish-schema-search-facets-presets.html)
* [Publicera taggar på varumärkesportalen](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/brand-portal-publish-tags.html)

Se [Brand Portal-dokumentation](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) för mer information.

**Distributionsloggar**

Du kan övervaka distributionsagentloggarna för publiceringsarbetsflödet.

Låt oss nu publicera en mediefil från Experience Manager Assets till Brand Portal och se loggarna.

1. Följ stegen (från 1 till 4) enligt anvisningarna i **Testanslutning** och navigera till distributionsagentsidan.
1. Klicka **[!UICONTROL Logs]** för att visa bearbetnings- och felloggarna.

   ![Bearbetning och felloggar](assets/test-bpconfig5.png)

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

tillsammans med automatiseringsarbetsflödet för att aktivera Brand Portal på Experience Manager Assets som en [!DNL Cloud Service]finns det en annan metod för att manuellt konfigurera Experience Manager Assets som [!DNL Cloud Service] med Brand Portal som använder Adobe Developer Console, vilket inte längre rekommenderas.

>[!NOTE]
>
>Kontakta kundsupport om du har problem med att aktivera din Brand Portal-klient.

## Manuell konfiguration med Adobe Developer Console {#manual-configuration}

I följande avsnitt beskrivs hur du konfigurerar Experience Manager Assets manuellt som [!DNL Cloud Service] med Brand Portal via Adobe Developer Console.

Tidigare var Experience Manager Assets [!DNL Cloud Service] konfigurerades manuellt med Brand Portal via Adobe Developer Console, som köper en kontotoken för Adobe Identity Management Services (IMS) för auktorisering av Brand Portal-klienten. Den kräver konfigurationer i både Experience Manager Assets och Adobe Developer Console.

1. Skapa ett IMS-konto i Experience Manager Assets och generera en offentlig nyckel (certifikat).
1. Skapa ett projekt för din Brand Portal-klient (organisation) i Adobe Developer Console.
1. Under projektet konfigurerar du ett API med den offentliga nyckeln för att skapa en tjänstkontoanslutning.
1. Hämta tjänstkontots autentiseringsuppgifter och JSON Web Token-nyttolastinformation.
1. I Experience Manager Assets konfigurerar du IMS-kontot med tjänstkontots autentiseringsuppgifter och JWT-nyttolast.
1. I Experience Manager Assets konfigurerar du Brand Portal molntjänst med hjälp av IMS-kontot och Brand Portal slutpunkt (organisations-URL).
1. Testa konfigurationen genom att publicera en resurs från Experience Manager Assets till Brand Portal.

>[!NOTE]
>
>En Experience Manager Assets som [!DNL Cloud Service] instans ska endast konfigureras med en Brand Portal-klient.

**Förutsättningar**

Du behöver följande för att konfigurera Experience Manager Assets med Brand Portal:

* En Experience Manager Assets som körs som [!DNL Cloud Service] instance
* En Brand Portal tenant-URL
* En användare med systemadministratörsbehörighet på IMS-organisationen för varumärkesportalens klient

## Skapa en konfiguration {#create-new-configuration}

Utför följande steg i den angivna sekvensen för att konfigurera Experience Manager Assets med Brand Portal.

1. [Hämta ett offentligt certifikat](#public-certificate)
1. [Skapa JWT-anslutning (Service Account)](#createnewintegration)
1. [Konfigurera IMS-konto](#create-ims-account-configuration)
1. [Konfigurera molntjänsten](#configure-the-cloud-service)

### Skapa IMS-konfigurationen {#create-ims-configuration}

IMS-konfigurationen autentiserar din Experience Manager Assets som en [!DNL Cloud Service] -instans med Brand Portal-klienten.

IMS-konfigurationen har två steg:

* [Hämta ett offentligt certifikat](#public-certificate)
* [Konfigurera IMS-konto](#create-ims-account-configuration)

### Hämta ett offentligt certifikat {#public-certificate}

Den offentliga nyckeln (certifikatet) autentiserar din profil på Adobe Developer Console.

1. Logga in på Experience Manager Assets.
1. Från **verktyg** navigera till **[!UICONTROL Security]** > **[!UICONTROL Adobe IMS Configurations]**.
1. På sidan Adobe IMS-konfigurationer klickar du på **[!UICONTROL Create]**. Den kommer att omdirigeras till **[!UICONTROL Adobe IMS Technical Account Configuration]** sida. Som standard är **Certifikat** -fliken öppnas.
1. Välj **[!UICONTROL Adobe Brand Portal]** i **[!UICONTROL Cloud Solution]** listruta.
1. Välj **[!UICONTROL Create new certificate]** kryssruta och ange en **alias** för den offentliga nyckeln. Aliaset används som namn på den offentliga nyckeln.
1. Klicka på **[!UICONTROL Create certificate]**. Klicka sedan på **[!UICONTROL OK]** för att generera den offentliga nyckeln.

   ![Skapa ett certifikat](assets/ims-config2.png)

1. Klicka på **[!UICONTROL Download Public Key]** och spara filen med den offentliga nyckeln (CRT) på datorn.

   Den offentliga nyckeln används senare för att konfigurera API för din Brand Portal-klient och generera autentiseringsuppgifter för tjänstkontot i Adobe Developer Console.

   ![Hämta certifikatet](assets/ims-config3.png)

1. Klicka på **[!UICONTROL Next]**.

   I **Konto** skapas ett Adobe IMS-konto som kräver inloggningsuppgifterna för tjänstkontot som genereras i Adobe Developer Console. Håll den här sidan öppen tills vidare.

   Öppna en ny flik och [skapa en JWT-anslutning (Service Account) i Adobe Developer Console](#createnewintegration) för att hämta autentiseringsuppgifter och JWT-nyttolast för konfigurering av IMS-kontot.

### Skapa JWT-anslutning (Service Account) {#createnewintegration}

I Adobe Developer Console konfigureras projekt och API:er på Brand Portal klientnivå (organisationsnivå). När du konfigurerar ett API skapas en JWT-anslutning (Service Account). Det finns två metoder för att konfigurera API, genom att generera ett nyckelpar (privata och offentliga nycklar) eller genom att överföra en offentlig nyckel. Om du vill konfigurera Experience Manager Assets med Brand Portal måste du skapa en offentlig nyckel (certifikat) i Experience Manager Assets och skapa autentiseringsuppgifter i Adobe Developer Console genom att överföra den offentliga nyckeln. Dessa autentiseringsuppgifter krävs för att konfigurera IMS-kontot i Experience Manager Assets. När IMS-kontot har konfigurerats kan du konfigurera Brand Portal molntjänst i Experience Manager Assets.

Utför följande steg för att generera autentiseringsuppgifter för tjänstkontot och JWT-nyttolast:

1. Logga in på Adobe Developer Console med systemadministratörsbehörighet för IMS-organisationen (Brand Portal tenant). Standardwebbadressen är [https://www.adobe.com/go/devs_console_ui](https://www.adobe.com/go/devs_console_ui).


   >[!NOTE]
   >
   >Kontrollera att du har valt rätt IMS-organisation (Brand Portal-klientorganisation) i listrutan (organisationen) längst upp till höger.

1. Klicka på **[!UICONTROL Create new project]**. Ett tomt projekt med ett systemgenererat namn skapas för din organisation.

   Klicka **[!UICONTROL Edit project]** för att uppdatera **[!UICONTROL Project Title]** och **[!UICONTROL Description]** och klicka **[!UICONTROL Save]**.

1. I **[!UICONTROL Project overview]** flik, klicka **[!UICONTROL Add API]**.

1. I **[!UICONTROL Add an API window]**, markera **[!UICONTROL AEM Brand Portal]** och klicka **[!UICONTROL Next]**.

   Se till att du har tillgång till tjänsten Experience Manager Brand Portal.

1. I **[!UICONTROL Configure API]** fönster, klicka **[!UICONTROL Upload your public key]**. Klicka sedan på **[!UICONTROL Select a File]** och ladda upp den publika nyckeln (.crt-filen) som du har laddat ned i [hämta offentligt certifikat](#public-certificate) -avsnitt.

   Klicka på **[!UICONTROL Next]**.

   ![Överför offentlig nyckel](assets/service-account3.png)

1. Verifiera den offentliga nyckeln och klicka på **[!UICONTROL Next]**.

1. Välj **[!UICONTROL Assets Brand Portal]** som standardproduktprofil och klicka på **[!UICONTROL Save configured API]**.

   ![Välj produktprofil](assets/service-account4.png)

1. När API:t har konfigurerats omdirigeras du till API-översikten. Från vänster navigering under **[!UICONTROL Credentials]** klickar du på **[!UICONTROL Service Account (JWT)]** alternativ.

   >[!NOTE]
   >
   >Du kan visa autentiseringsuppgifterna och utföra åtgärder som att generera JWT-tokens, kopiera autentiseringsuppgifter, hämta klienthemlighet osv.

1. Från **[!UICONTROL Client Credentials]** -fliken, kopiera **[!UICONTROL client ID]**.

   Klicka **[!UICONTROL Retrieve Client Secret]** och kopiera **[!UICONTROL client secret]**.

   ![Autentiseringsuppgifter för tjänstkonto](assets/service-account5.png)

1. Navigera till **[!UICONTROL Generate JWT]** och kopiera **[!UICONTROL JWT Payload]** information.

Du kan nu använda klient-ID (API-nyckel), klienthemlighet och JWT-nyttolast för att [konfigurera IMS-kontot](#create-ims-account-configuration) i Experience Manager Assets.

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

   The API Key, Client Secret key, and JWT payload information is used to create IMS account configuration.

-->

### Konfigurera IMS-konto {#create-ims-account-configuration}

Kontrollera att du har utfört följande steg:

* [Hämta ett offentligt certifikat](#public-certificate)
* [Skapa JWT-anslutning (Service Account)](#createnewintegration)

Utför följande steg för att konfigurera IMS-kontot.

1. Öppna IMS-konfigurationen och gå till **[!UICONTROL Account]** -fliken. Du höll sidan öppen medan [erhålla det offentliga certifikatet](#public-certificate).

1. Ange en **[!UICONTROL Title]** för IMS-kontot.

   I **[!UICONTROL Authorization Server]** anger du URL-adressen: [https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/)

   Ange klient-ID i **[!UICONTROL API key]** fält, **[!UICONTROL Client Secret]** och **[!UICONTROL Payload]** (JWT-nyttolast) som du har kopierat när [skapar tjänstkontoanslutningen (JWT)](#createnewintegration).

   Klicka på **[!UICONTROL Create]**.

   IMS-kontot är konfigurerat.

   ![Konfiguration av ett IMS-konto](assets/create-new-integration6.png)


1. Välj IMS-kontokonfigurationen och klicka på **[!UICONTROL Check Health]**.

   Klicka **[!UICONTROL Check]** i dialogrutan. När konfigurationen är klar visas ett meddelande om att *Token har hämtats*.

   ![Adobe IMS Configurations Check Health.](assets/create-new-integration5.png)

>[!CAUTION]
>
>Du får bara ha en IMS-konfiguration.
>
>Kontrollera att IMS-konfigurationen klarar hälsokontrollen. Om konfigurationen inte godkänns i hälsokontrollen är den ogiltig. Du måste ta bort den och skapa en ny, giltig konfiguration.

### Konfigurera molntjänsten {#configure-the-cloud-service}

Så här konfigurerar du molntjänsten i Brand Portal:

1. Logga in på Experience Manager Assets.

1. Från **verktyg** navigera till **[!UICONTROL Cloud Services]** > **[!UICONTROL AEM Brand Portal]**.

1. På sidan Brand Portal Configurations klickar du på **[!UICONTROL Create]**.

1. Ange en **[!UICONTROL Title]** för konfigurationen.

   Välj den IMS-konfiguration som du skapade när [konfigurera IMS-kontot](#create-ims-account-configuration).

   I **[!UICONTROL Service URL]** anger du din Brand Portal tenant-URL (organisation).

   ![Dialogrutan Brand Portal Configuration.](assets/create-cloud-service.png)

1. Klicka på **[!UICONTROL Save & Close]**. Molnkonfigurationen har skapats.

   Din Experience Manager Assets som [!DNL Cloud Service] -instansen har nu konfigurerats med Brand Portal-klientorganisationen.

Du kan nu testa konfigurationen genom att kontrollera distributionsagenten och publicera resurser på Brand Portal.

**Tillåtslista IP-adresser i SPS om säker förhandsvisning är aktiverat**
Om du använder Dynamic Media-Scene7 med [säker förhandsvisning aktiverad](#https://experienceleague.adobe.com/docs/dynamic-media-classic/using/upload-publish/testing-assets-making-them-public.html?lang=en) för ett företag) rekommenderar vi att Scene7 företagsadministratör [tillåtslista IP-adresserna till utgångarna](#https://experienceleague.adobe.com/docs/dynamic-media-classic/using/upload-publish/testing-assets-making-them-public.html?lang=en#testing-the-secure-testing-service) för respektive region som använder användargränssnittet SPS (Scene7 Publishing System) flash.
IP-adresserna för utgångar är följande:

| **Län** | **IP-adress för ägg** |
|--- |--- |
| NA | 130.248.160.68, 20.94.203.130 |
| EMEA | 51.132.146.75, 130.248.244.202, 130.248.244.203, 130.248.244.204, 130.248.244.210, 130.248.244.211, 130.248.244.212 |
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

1. To verify the connection between AEM Assets as a [!DNL Cloud Service] and Brand Portal, click on the **[!UICONTROL Test Connection]** icon.

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

* [Översätt resurser](translate-assets.md)
* [HTTP API för Assets](mac-api-assets.md)
* [Resurser som stöds i filformat](file-format-support.md)
* [Söka efter resurser](search-assets.md)
* [Anslutna resurser](use-assets-across-connected-assets-instances.md)
* [Materialrapporter](asset-reports.md)
* [Metadata-scheman](metadata-schemas.md)
* [Hämta resurser](download-assets-from-aem.md)
* [Hantera metadata](manage-metadata.md)
* [Söka efter fasetter](search-facets.md)
* [Hantera samlingar](manage-collections.md)
* [Import av massmetadata](metadata-import-export.md)

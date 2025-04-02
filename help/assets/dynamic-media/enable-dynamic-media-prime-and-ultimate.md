---
title: Aktivera [!DNL Dynamic Media] Prime och Ultimate
description: Lär dig hur du aktiverar  [!DNL Dynamic Media] Prime- och Ultimate-erbjudanden.
feature: Asset Management
role: User, Admin
exl-id: 0ee161f5-bf44-41f1-928e-c07574fd43cc
source-git-commit: c36938e80d0b159c5f89d450aaa228c37c4f5276
workflow-type: tm+mt
source-wordcount: '981'
ht-degree: 0%

---

# Aktivera [!DNL Dynamic Media] Prime och Ultimate {#enable-dynamic-media-prime-and-ultimate}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime och Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM Assets-integrering med Edge Delivery Services</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>UI-utökningsbarhet</b></a>
        </td>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>Sök efter bästa praxis</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>Metadata - bästa praxis</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Content Hub</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>Dynamiska media med OpenAPI-funktioner</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>AEM Assets-dokumentation för utvecklare</b></a>
        </td>
    </tr>
</table>

[!DNL Adobe Experience Manager] as a Cloud Service ger dig tillgång till [!DNL Dynamic Media] Prime- och Ultimate-erbjudanden för att effektivisera dina digitala arbetsflöden och optimera innehållshanteringen. Se [Dynamic Media Prime och Ultimate](/help/assets/dynamic-media/dm-prime-ultimate.md) för att förstå deras fördelar och de viktigaste skillnaderna mellan dem.

Den här artikeln innehåller ett komplett arbetsflöde för att aktivera Prime- och Ultimate-erbjudanden för [!DNL Dynamic Media].

## Aktivera [!DNL Dynamic Media] Ultimate {#enable-dynamic-media-ultimate}

Så här aktiverar du [!DNL Dynamic Media] Ultimate:

1. [Aktivera [!DNL Dynamic Media with OpenAPI]](#activate-dynamic-media-with-openapi)
1. [Konfigurera [!DNL Dynamic Media] lösningar](#configure-dynamic-media-solutions)
1. [Skapa och lista [!DNL Dynamic Media] företag](#create-and-list-dynamic-media-companies)
1. [Konfigurera anpassad domän i leveransnivå](#configure-custom-domain-in-delivery-tier)

<!--
1. [Onboard API keys using the [!DNL AEM] [!DNL Dynamic Media] API card](#onboarding-api-keys)
-->

Om du behöver aktivera [!DNL Dynamic Media Prime] läser du snabblänkarna i [Aktivera [!DNL Dynamic Media Prime]](#enable-dynamic-media-prime).

### Aktivera [!DNL Dynamic Media with OpenAPI] {#activate-dynamic-media-with-openapi}

[!DNL Dynamic Media] med OpenAPI-funktioner sätter DAM i centrum för ett flexibelt och effektivt ekosystem i innehållsförsörjningskedjan för att säkerställa resursstyrning och leverans.

Det första steget i processen att aktivera [!DNL Dynamic Media] Ultimate är att aktivera [[!DNL Dynamic Media]  med OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) för din Cloud Service-miljö.

#### Förbered dig för att komma igång {#prerequisites}

Kontrollera att du uppfyller följande krav innan du startar aktiveringsprocessen:

1. [Åtkomst till Cloud Manager](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/onboarding/journey/cloud-manager).
1. [Programmet innehåller [!DNL Dynamic Media] lösningar](#configure-dynamic-media-solutions).
1. Du har [!DNL Dynamic Media] Prime- eller Ultimate-licens.

#### Aktivera [!DNL Dynamic Media with OpenAPI]-funktioner i din Cloud Service-miljö {#enable-dynamic-media-with-openapi-capabilites-in-your-CS-environment}

Gör så här för att aktivera [!DNL Dynamic Media with OpenAPI] för din molntjänstmiljö:

1. [Navigera till Cloud Manager-gränssnittet](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/onboarding/journey/cloud-manager).

1. [Skapa en miljö](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/onboarding/journey/create-environments) om du inte har tillgång till en befintlig miljö.

1. Välj **[!UICONTROL Click to activate]** på raden **[!UICONTROL Dynamic Media]** i avsnittet **[!UICONTROL Environment Information]** på sidan Miljöinformation.

   ![aktivera dynamiska media med OpenAPI-funktioner](/help/assets/assets/activate-adv-capabiliites-of-dm-openAPI.png)

1. Klicka på **[!UICONTROL Activate]** i bekräftelsedialogrutan för att starta aktiveringsprocessen för [!DNL Dynamic Media with OpenAPI]. När aktiveringen är klar visas följande statusuppdateringar:
   1. **[!UICONTROL Environment stage]**: **[!UICONTROL Running]**
   1. ![DM har aktiverats ](/help/assets/assets/Images_icon.svg)**[!UICONTROL Dynamic Media]**:**[!UICONTROL OpenAPI capabilities are activated]**

      ![aktiveringen lyckades](/help/assets/assets/activation-successful.png){width="700" align="left"}

#### Försök aktivera igen {#retry-activation}

Om aktiveringen misslyckas visas följande statusuppdateringar i Cloud Manager:

* **[!UICONTROL Environment stage]**: **[!UICONTROL DM with OpenAPI Failed]**
* ![DM har aktiverats ](/help/assets/assets/Images_icon.svg)**[!UICONTROL Dynamic Media]**:**[!UICONTROL OpenAPI capabilities failed to activate]**

  ![försök aktivera igen](/help/assets/assets/retry-dm-openapi-failed-activation.png){width="700" align="left"}

Välj **[!UICONTROL Click to retry]** om du vill starta om aktiveringen.

Du kan även utföra följande steg för att starta om aktiveringsprocessen:

1. Navigera till sidan med en lista över alla miljöer.

1. Klicka på fler alternativ (![fler alternativ](/help/assets/assets/three-dots.svg)) i slutet av miljöraden.

1. Välj **[!UICONTROL Retry DM with OpenAPI Activation]** om du vill starta om aktiveringen.

   ![Försök aktivera igen från sidan med miljöinformation](/help/assets/assets/restart-activation-process-from-list-environment-page.png)

### Konfigurera [!DNL Dynamic Media] lösningar {#configure-dynamic-media-solutions}

Konfigurera [!UICONTROL Dynamic Media]-lösningar så att de grundläggande och avancerade funktionerna i [Dynamic Media med OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) används i befintliga eller nya miljöer i Cloud Manager.

#### Förbered dig för att komma igång {#prerequisites-to-configure-dynamic-media-solutions}

Kontrollera att du har följande för att konfigurera [!UICONTROL Dynamic Media] lösningar:

1. [Åtkomst till Cloud Manager](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/onboarding/journey/cloud-manager).
1. Du har [!DNL Dynamic Media] Ultimate-licens.

#### Konfigurera [!DNL Dynamic Media] lösningar för leverans av resurser {#configure-dynamic-media-solutions-for-asset-delivery}

Utför följande steg:

1. [Skapa ett nytt program](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/onboarding/journey/create-program) eller navigera till ett befintligt program och klicka på **[!UICONTROL Edit]**. Sidan **[!UICONTROL Set up for production]** visar fliken **[!UICONTROL Solutions & Add-ons]**.

1. Välj **[!UICONTROL Assets]**, **[!UICONTROL Assets Prime]**, **[!UICONTROL Assets Ultimate]** eller **[!UICONTROL Sites]** för att lägga till lösningen **[!UICONTROL Dynamic Media]** i ditt program.

1. Välj lösningen **[!UICONTROL Dynamic Media]** och klicka på **[!UICONTROL Continue]** för att lägga till lösningen **[!UICONTROL Dynamic Media]** i programmet. Den här åtgärden startar om alla befintliga miljöer i programmet och lägger till lösningen [!DNL Dynamic Media] till dem. Dessutom får alla nya miljöer som du skapar under ditt program automatiskt [!DNL Dynamic Media].

   ![har konfigurerats för produktion](/help/assets/assets/set-up-for-prod.png){width="500" align="left"}

Se [Aktivera [!DNL Dynamic Media with OpenAPI]](#activate-dynamic-media-with-openapi) om du vill börja använda funktionerna i [!DNL Dynamic Media] med OpenAPI-funktioner i din miljö.

### Skapa och lista [!DNL Dynamic Media] företag {#create-and-list-dynamic-media-companies}

Skapa och lista [!DNL Dynamic Media] företag i din molntjänstmiljö i AEM för att hantera konfigurationer i din AEM-miljö.

#### Förbered dig för att komma igång {#prerequisites-to-create-and-list-dynamic-media-companies}

Om du vill visa befintliga företag (konton) eller lägga till ett nytt [!DNL Dynamic Media]-företag (konto) i din IMS-organisation måste du ha:

1. [Åtkomst till Cloud Manager](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/onboarding/journey/cloud-manager).

1. Du har [!DNL Dynamic Media] Ultimate-licens.

#### Skapa och lista [!DNL Dynamic Media] företag i din IMS-organisation {#create-and-list-dynamic-media-companies-in-your-ims-organisation}

Utför de här stegen för att skapa och lista ett nytt [!DNL Dynamic Media]-företag (konto) som kan konfigureras i din [!DNL AEM]-miljö:

1. Gå till [licenssidan för Cloud Manager](https://experience-stage.adobe.com/#/@ssahnichstage/cloud-manager/license).

1. Klicka på **[!UICONTROL Add Company]** så visas dialogrutan **[!UICONTROL Create Dynamic Media Company]**.

1. Ange ett unikt [!DNL Dynamic Media]-företagsnamn, välj en företagsregion och lägg till en lista med företagets administratörs-e-post-ID:n avgränsade med kommatecken.

   ![Skapa företaget Dynamic Media](/help/assets/assets/create-dynamic-media-company.png){width="500" align="left"}

1. Klicka på **[!UICONTROL Create]** för att börja skapa ditt företag. Den här åtgärden lägger till en ny rad i avsnittet **[!UICONTROL [!DNL Dynamic Media] companies]** och visar **[!UICONTROL Setting up]** som företagets **[!UICONTROL STATUS]**.

   ![startade företaget Dynamic Media](/help/assets/assets/dm-company-creation-initiated.png)

1. **Valfritt:** Klicka på ![informationsikonen](/help/assets/assets/info-icon-solid-black.svg) om du vill visa information om företaget. **[!UICONTROL STATUS]** uppdaterar till **[!UICONTROL Ready]** när företaget skapas.

   ![Företagsinformation för dynamiska media](/help/assets/assets/dm-company-information.png)

1. Som Dynamic Media Administrator kan du kontrollera i din postlåda om du vill få ett välkomstmeddelande med en lista över steg för att [konfigurera [!DNL Dynamic Media]](/help/assets/dynamic-media/config-dm.md#architecture-diagram-of-dynamic-media) företag i din [!DNL AEM] Cloud Service-miljö för att komma igång.

   ![välkomstmeddelande](/help/assets/assets/welcome-email.png)

#### Försök att skapa företag igen {#retry-company-creation}

Om det inte går att skapa företaget [!DNL Dynamic Media] utför du följande steg baserat på felstatusen:

1. Om **[!UICONTROL Status]** väntar tar du upp problemet för kundsupport för att åtgärda det.


   ![väntande status](/help/assets/assets/company-creation-pending-status.png){width="350" align="center"}



1. Om **[!UICONTROL Status]** misslyckas försöker du igen baserat på orsaken till felet.

   ![misslyckades status](/help/assets/assets/company-creation-failure-status.png){width="380" align="center"}

### Valfritt: Konfigurera anpassad domän i leveransnivå {#configure-custom-domain-in-delivery-tier}

När AEM as a Cloud Service har en standarddomän kan du anpassa den efter dina behov. Koppla en anpassad domän till leveransnivån med Cloud Manager.

#### Förbered dig för att komma igång {#prerequisites-to-configure-custom-domain-in-delivery-tier}

Kontrollera att du uppfyller följande krav innan du startar konfigurationsprocessen:

1. [Åtkomst till Cloud Manager](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/onboarding/journey/cloud-manager).
1. [Har redan aktiverats [!DNL Dynamic Media with OpenAPI] i din miljö](#activate-dynamic-media-with-openapi).
1. [!DNL Dynamic Media with OpenAPI] har aktiverats i klart läge.
1. EV- eller OV-typcertifikat för domänen som ska användas för leveransnivån. Mer information finns i [Introduktion till SSL-certifikat](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/introduction-to-ssl-certificates).

#### Konfigurera anpassad domän i leveransnivå med Cloud Manager {#configure-custom-domain-in-delivery-tier-using-cloud-manager}

Utför följande steg i Cloud Manager för att konfigurera en anpassad domän i leveransnivån:

1. [Lägg till ett kundhanterat SSL-certifikat](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/add-ssl-certificate#add-customer-managed-ssl-cert).

1. [Lägg till ett anpassat domännamn](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/custom-domain-names/add-custom-domain-name#adding-cdn-settings).

1. Navigera till sidan med miljöinformation och [lägg till en CDN-konfiguration](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/cdn-configurations/add-cdn-config). När du lägger till konfigurationen väljer du **[!UICONTROL Delivery]** i fältet **[!UICONTROL Tier]** i dialogrutan **[!UICONTROL Configure CDN]**.

   ![Konfigurera CDN](/help/assets/assets/select-delivery-tier-in-configure-cdn-form.png)

   När du har lagt till konfigurationerna uppdateras **[!UICONTROL STATUS]** av **[!UICONTROL CDN Configurations]** till **[!UICONTROL Applied]**.

   ![Konfigurera CDN-distributionsstatus](/help/assets/assets/cdn-configuration-deployment-status.png)

1. Klicka på fler alternativ (![fler alternativ](/help/assets/assets/three-dots.svg)) och välj **[!UICONTROL Go live readiness]** för att visa dialogrutan **[!UICONTROL Go live readiness]**.

   ![gå live-beredskapsalternativ](/help/assets/assets/go-live-readiness-option.png)

1. Kör **[!UICONTROL Configure CNAME]** steg för att mappa [ cdn.adobeaemcloud.com](http://cdn.adobeaemcloud.com/) (CNAME-post) i DNS-posten för DNS-tjänstleverantören. Denna mappning säkerställer att begäranden som tas emot på den anpassade domänen dirigeras om till Adobe CDN.

   ![gå live-dialogruta för beredskap](/help/assets/assets/go-live-readiness-dialogbox.png){width="500" align="left"}

1. Klicka på **[!UICONTROL Ok]**, **[!UICONTROL STATUS]** uppdateras till **[!UICONTROL Verified]**. Den anpassade domänen är klar att användas i leverans-URL:en.


   ![Konfigurera CDN](/help/assets/assets/cdn-configurations-varified.png)



<!--
### Onboard API keys {#onboarding-api-keys}

Create an API key to access [!DNL Dynamic Media] with OpenAPIs and the delivery tier backed Asset Selector.

#### Prepare yourself for API keys onboarding process {#prerequisites-for-onboarding-api-keys} 

To start the API keys onboarding process, ensure you have:

1. [Access to Cloud Manager](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/onboarding/journey/cloud-manager).
1. [Activated [!DNL Dynamic Media with OpenAPI] in your environment](#activate-dynamic-media-with-openapi).
1. [Access to the Adobe Developer Console](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-apis/invoke-openapi-based-aem-apis#create-adobe-developer-console-adc-project).

#### Onboard the API keys using [!DNL AEM Dynamic Media] API card {#onboarding-api-keys-using-aem-dynamic-media-api-card}

Use the [Adobe Developer Console](https://developer.adobe.com/developer-console/) to onboard the API keys to:

1. [Access Dynamic Media APIs](#access-dynamic-media-apis)
1. [Access Delivery tier backed Asset Selector](#access-delivery-tier-backed-asset-selector)

#### Create an API key to access [!DNL Dynamic Media] with OpenAPIs {#access-dynamic-media-apis}

Execute the following steps to create an API key to access [!DNL Dynamic Media] with OpenAPIs:

1. Navigate to the **[!UICONTROL Admin Console]**. The Admin Console displays the **[!UICONTROL author]**, **[!UICONTROL delivery]** and **[!UICONTROL publish]** instances.
![instances on admin console](/help/assets/assets/delivery-instance-admin-console.png)
1. Select the **[!UICONTROL delivery]** instance to display the product profile with **[!UICONTROL AEM Dynamic Media enable API Services]** enabled by default. The product profile looks like this: **[!UICONTROL AEM Assets DM OpenAPI Users - delivery  - Program [ID Number] - Environment [ID Number]]**. 

   ![product profile on admin console](/help/assets/assets/admin-console-product-profile.png)

   >[!NOTE]
   >
   >This delivery instance is common for [!DNL Content Hub] and [!DNL Dynamic Media] with OpenAPI capabilities.

1. Navigate to the [Adobe Developer console](https://developer.adobe.com/console) and [create a new project](https://developer.adobe.com/dep/guides/dev-console/create-project/). See [Invoke OpenAPI-based AEM APIs for server to server authentication](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-apis/invoke-openapi-based-aem-apis) to learn about creating a new project.
1. Select **[!UICONTROL AEM Dynamic Media API]** to access to the [!DNL Dynamic Media with OpenAPI capabilities] and click **[!UICONTROL Next]**.
![adobe developer console](/help/assets/assets/adobe-developer-console.png)
1. Select **[!UICONTROL Server-to-Server Authentication]** and click **[!UICONTROL Next]**. See [Server to Server authentication](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/) to learn more about this authentication type.
![server-to-server-authentication](/help/assets/assets/server-to-server-authentication.png)
1. Select **[!UICONTROL OAuth Server-to-Server]**, specify a unique **[!UICONTROL Credential name]** and click **[!UICONTROL Next]**.
![oauth server to server credential](/help/assets/assets/oauth-server-server-and-credential-name.png)
1. Select your product profile (mentioned in step 2) to access the APIs using the environment's delivery endpoint and click **[!UICONTROL Save configured API]**.
![select product profile](/help/assets/assets/select-product-profile.png)
1. Select **[!UICONTROL AEM Dynamic Media API]**. Use the **[!UICONTROL OAuth Server-to-Server]** to fetch the **X-API-key** and access the token for the **authorization** header. 
![oauth server to server](/help/assets/assets/oauth-server-to-server-credentials.png)
Execute the below steps to use [Dynamic Media with OpenAPIs](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/) using the **[!UICONTROL OAuth Server-to-Server]** credentials. 
    1. Copy the **[!UICONTROL API KEY (Client ID)]** and replace the `X-Api-Key` in the cURL.
    1. Click **[!UICONTROL Generate access token]** to generate an access token and replace `YOUR_JWT_HERE` with the token in the cURL.

The cURL looks like this:
```
headers: {
    'Content-Type': 'application/json',
      'X-Adobe-Accept-Experimental': '1',
      Authorization: 'Bearer <YOUR_JWT_HERE>',
      'X-Api-Key': 'YOUR_API_KEY_HERE'
    `},
```
See [Search Assets API](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dynamic-media-open-apis/search-assets-api#search-assets-api-header) for more information.

### Access Delivery tier backed Asset Selector {#access-delivery-tier-backed-asset-selector}

TBD: Wiki in progress..
-->

## Aktivera [!DNL Dynamic Media] Prime {#enable-dynamic-media-prime}

Så här aktiverar du [!DNL Dynamic Media] Prime:

1. [Aktivera dynamiska media med OpenAPI](#activate-dynamic-media-with-openapi)
1. [Valfritt: Konfigurera anpassad domän i leveransnivå](#configure-custom-domain-in-delivery-tier)

<!--
1. [Onboard API keys using the AEM Dynamic Media API card](#onboarding-api-keys)
-->

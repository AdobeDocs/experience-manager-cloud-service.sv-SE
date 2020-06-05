---
title: Förbättrade smarta taggar
description: Använd kontextuella och beskrivande taggar med Adobe Senseis AI- och ML-tjänst för att förbättra tillgångsidentifieringen och innehållets hastighet.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 41684858f1fe516046b9601c1d869fff180320e0
workflow-type: tm+mt
source-wordcount: '859'
ht-degree: 5%

---


# Konfigurera Experience Manager för smart taggning av resurser {#configure-aem-for-smart-tagging}

Genom att tagga resurser med taxonomistyrd vokabulär kan du enkelt identifiera och hämta dem genom taggbaserade sökningar. Adobe tillhandahåller smarta taggar som använder artificiell intelligens och algoritmer för maskininlärning för att utbilda bilder. Smarta taggar använder ett artificiellt intelligensramverk i [Adobe Sensei](https://www.adobe.com/sensei/experience-cloud-artificial-intelligence.html) för att utbilda sin bildigenkänningsalgoritm i din taggstruktur och i din affärsmiljö.

Funktionen Smarta taggar kan köpas som tillägg till [!DNL Experience Manager]. När du har köpt programmet skickas ett e-postmeddelande till administratören för organisationen med en länk till Adobe Developer Console. Administratören kommer åt länken för att integrera smarta taggar med [!DNL Experience Manager] Adobe Developer Console.

<!-- TBD: 
1. Can a similar flowchart be created about how training works in CS? ![flowchart](assets/flowchart.gif)
2. Is there a link to buy SCS or initiate a sales call.
3. Keystroke all steps and check all screenshots.
4. Post-GA, if time permits, create a video.
-->

## Integrera med Adobe Developer Console {#aio-integration}

Innan du kan tagga bilderna med SCS måste du integrera [!DNL Adobe Experience Manager] med tjänsten Smarta taggar med Adobe Developer Console. I bakänden autentiserar [!DNL Experience Manager] servern dina inloggningsuppgifter med Adobe Developer Console-gatewayen innan din begäran vidarebefordras till tjänsten.

* Skapa en konfiguration i [!DNL Experience Manager] för att generera en offentlig nyckel. Hämta ett offentligt certifikat för OAuth-integrering.
* Skapa en integrering i Adobe Developer Console och överför den genererade offentliga nyckeln.
* Konfigurera din [!DNL Experience Manager] instans med API-nyckeln och andra autentiseringsuppgifter från Adobe Developer Console.
* Du kan även aktivera automatisk taggning vid överföring av resurser.

### Krav för Adobe Developer Console-integrering {#prerequisite-for-aio-integration}

Innan du kan använda smarta taggar måste du göra följande för att skapa en integrering på Adobe Developer Console:

* Ett Adobe ID-konto som har administratörsbehörighet för organisationen.
* Smarta taggar är aktiverade för din organisation.

### Obtain a public certificate {#obtain-public-certificate}

Med ett offentligt certifikat kan du autentisera din profil på Adobe Developer Console. Du skapar ett certifikat inifrån [!DNL Experience Manager].

1. I [!DNL Experience Manager] användargränssnittet går du till **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Adobe IMS Configurations]**.

1. På [!UICONTROL Adobe IMS Configurations] sidan klickar du på **[!UICONTROL Create]**. From **[!UICONTROL Cloud Solution]** menu, select **[!UICONTROL Smart Tags]**.

1. Välj **[!UICONTROL Create new certificate]**. Ange ett namn och klicka på **[!UICONTROL Create certificate]**. Klicka på **[!UICONTROL OK]**.

1. Klicka på **[!UICONTROL Download Public Key]**.

   ![Smarta taggar i Experience Manager skapar en offentlig nyckel](assets/aem_smarttags-config1.png)

### Konfigurera om ett certifikat upphör att gälla {#certrenew}

När certifikatet upphör att gälla är det inte längre tillförlitligt. Följ de här stegen för att lägga till ett nytt certifikat. Du kan inte förnya ett certifikat som har upphört att gälla.

1. Log in your [!DNL Experience Manager] deployment as an administrator. Klicka på **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Users]**.

1. Leta reda på och klicka på **[!UICONTROL dam-update-service]** användaren. Klicka på **[!UICONTROL Keystore]** fliken.
1. Ta bort den befintliga **[!UICONTROL similaritysearch]** nyckelbehållaren med det certifikat som upphört att gälla. Klicka på **[!UICONTROL Save & Close]**.

   ![Ta bort befintlig likhetssökningspost i nyckelbehållaren om du vill lägga till ett nytt säkerhetscertifikat](assets/smarttags_delete_similaritysearch_keystore.png)

   *Bild: Ta bort den befintliga`similaritysearch`posten i nyckelbehållaren om du vill lägga till ett nytt säkerhetscertifikat.*

1. I [!DNL Experience Manager] användargränssnittet går du till **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Adobe IMS Configurations]**. Öppna den tillgängliga konfigurationen för smarta taggar. Om du vill hämta ett offentligt certifikat klickar du på **[!UICONTROL Download Public Certificate]**.

1. Gå till [https://console.adobe.io](https://console.adobe.io) och navigera till den befintliga tjänsten i projektet. Överför det nya certifikatet och konfigurera det. Mer information om konfiguration finns i anvisningarna i Integrering [med](#create-aio-integration)Skapa Adobe Developer Console.

### Skapa en integrering {#create-aio-integration}

Om du vill använda smarta taggar skapar du en integrering i Adobe Developer Console för att generera API-nyckel, ID för tekniskt konto, organisations-ID och klienthemlighet.

1. Öppna [https://console.adobe.io](https://console.adobe.io/) i en webbläsare. Välj rätt konto och kontrollera att den associerade organisationsrollen är systemadministratör.
1. Skapa ett projekt med valfritt namn. Klicka på **[!UICONTROL Add API]**.
1. Markera **[!UICONTROL Add an API]** och markera på **[!UICONTROL Experience Cloud]** sidan **[!UICONTROL Smart Content]**. Klicka på **[!UICONTROL Next]**.
1. Välj **[!UICONTROL Upload your public key]**. Ange certifikatfilen som hämtats från [!DNL Experience Manager]. Ett meddelande [!UICONTROL Public key(s) uploaded successfully] visas. Klicka på **[!UICONTROL Next]**.
1. [!UICONTROL Create a new Service Account (JWT) credential] visas den offentliga nyckeln för det tjänstkonto som precis konfigurerats. Klicka på **[!UICONTROL Next]**.
1. Markera på **[!UICONTROL Select product profiles]** sidan **[!UICONTROL Smart Content Services]**. Klicka **[!UICONTROL Save configured API]**. På en sida visas mer information om konfigurationen. Håll den här sidan öppen om du vill kopiera och lägga till de här värdena i Experience Manager när du konfigurerar smarta taggar i [!DNL Experience Manager].

   ![På fliken Översikt kan du granska den information som finns för integrering.](assets/integration_details.png)

### Konfigurera smarta taggar {#configure-smart-content-service}

Om du vill konfigurera integreringen använder du nyckelfälten Payload, Client Secret, Authorization Server och API från Adobe Developer Console-integreringen.

1. I [!DNL Experience Manager] användargränssnittet går du till **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Adobe IMS Configurations]**.
1. Öppna **[!UICONTROL Adobe IMS Technical Account Configuration]** sidan, ange önskat **[!UICONTROL Title]**.
1. Ange **[!UICONTROL Authorization Server]** URL i `https://ims-na1.adobelogin.com` fältet.
1. I **[!UICONTROL API Key]** fältet anger du **[!UICONTROL Client ID]** från [!DNL Adobe Developer Console].
1. I **[!UICONTROL Client Secret]** fältet anger du **[!UICONTROL Client Secret]** från [!DNL Adobe Developer Console]. Klicka på **[!UICONTROL Retrieve Client Secret]** alternativet om du vill se det.
1. I [!DNL Adobe Developer Console]ditt projekt klickar du **[!UICONTROL Service Account (JWT)]** från den vänstra marginalen. Klicka på **[!UICONTROL Generate JWT]** flik. Klicka **[!UICONTROL Copy]** för att kopiera den visade bilden **[!UICONTROL JWT Payload]**. Ange det här värdet i **[!UICONTROL Payload]** fältet i [!DNL Experience Manager]. Klicka på **[!UICONTROL Create]**.

### Validera konfigurationen {#validate-the-configuration}

När du har slutfört konfigurationen följer du de här stegen för att validera konfigurationen.

1. I [!DNL Experience Manager] användargränssnittet går du till **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Adobe IMS Configurations]**.

1. Välj konfigurationen för smarta taggar. Klicka **[!UICONTROL Check Health]** i verktygsfältet. Klicka på **[!UICONTROL Check]**. En dialogruta med [!UICONTROL Healthy configuration] ett meddelande bekräftar att konfigurationen fungerar.

![Verifiera konfigurationen av smarta taggar](assets/smart-tag-config-validation.png)

## Aktivera smart taggning för nyligen överförda resurser (valfritt) {#enable-smart-tagging-for-uploaded-assets}

1. In [!DNL Experience Manager], gå till **[!UICONTROL Tools > Workflow > Models]**.
1. Välj arbetsflödesmodell **[!UICONTROL DAM Update Asset]** på sidan **[!UICONTROL Workflow Models]**.
1. Klicka **[!UICONTROL Edit]** i verktygsfältet.
1. Expandera sidopanelen för att visa stegen. Dra steget **[!UICONTROL Smart Tag Asset]** som finns i avsnittet med DAM-arbetsflöden och placera det efter steget **[!UICONTROL Process Thumbnails]**.

   ![Lägg till resurssteget för smarta taggar efter steget med processminiatyrer i arbetsflödet för DAM-uppdatering av resurs](assets/chlimage_1-105.png)

   *Bild: Lägg till resurssteget för smarta taggar efter steget med processminiatyrer i arbetsflödet för DAM-uppdatering av resurser.*

1. Öppna steget som ska konfigureras. Under **[!UICONTROL Advanced Settings]** kontrollerar du att **[!UICONTROL Handler Advance]** alternativet är markerat.

   ![Anger att hanteraren ska gå vidare till nästa steg i arbetsflödet.](assets/smart-tags-workflow-handler-setting.png)

1. Markera på **[!UICONTROL Arguments]** fliken **[!UICONTROL Ignore Errors]** om du vill att fel ska ignoreras i arbetsflödet när taggar beräknas. Om du vill tagga resurser när de överförs, oavsett om smart taggning är aktiverat för mappar eller inte, markerar du **[!UICONTROL Ignore Smart Tag Flag]**.

1. Klicka **[!UICONTROL OK]** för att stänga processsteget och spara sedan arbetsflödet. Klicka på **[!UICONTROL Sync]**.

>[!MORELIKETHIS]
>
>* [Tagga resurser med smarta tjänster](smart-tags.md)


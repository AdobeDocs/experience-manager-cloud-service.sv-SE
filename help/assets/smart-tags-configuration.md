---
title: Förbättrade smarta taggar
description: Använd kontextuella och beskrivande taggar med Adobe Senseis AI- och ML-tjänst för att förbättra tillgångsidentifieringen och innehållets hastighet.
contentOwner: AG
translation-type: tm+mt
source-git-commit: bf7bb91dd488f39181a08adc592971d6314817de
workflow-type: tm+mt
source-wordcount: '882'
ht-degree: 8%

---


# Konfigurera Experience Manager för smart taggning av resurser {#configure-aem-for-smart-tagging}

Genom att tagga resurser med taxonomistyrd vokabulär kan du enkelt identifiera och hämta dem genom taggbaserade sökningar. Adobe tillhandahåller smarta taggar som använder artificiell intelligens och algoritmer för maskininlärning för att utbilda bilder. Smarta taggar använder ett artificiellt intelligensramverk i [Adobe Sensei](https://www.adobe.com/sensei/experience-cloud-artificial-intelligence.html) för att utbilda sin bildigenkänningsalgoritm i din taggstruktur och i din affärsmiljö.

Funktionen Smarta taggar kan köpas som tillägg till [!DNL Experience Manager]. När du har köpt produkten skickas ett e-postmeddelande med en länk till Adobe I/O till administratören för organisationen. Administratören kommer åt länken för att integrera smarta taggar med [!DNL Experience Manager] hjälp av Adobe I/O.

<!-- TBD: 
1. Can a similar flowchart be created about how training works in CS? ![flowchart](assets/flowchart.gif)
2. Is there a link to buy SCS or initiate a sales call.
3. Keystroke all steps and check all screenshots.
4. Post-GA, if time permits, create a video.
-->

## Integrera med Adobe I/O {#aio-integration}

Innan du kan tagga bilderna med SCS måste du integrera [!DNL Adobe Experience Manager] med tjänsten Smarta taggar med hjälp av Adobe I/O. I bakänden autentiserar [!DNL Experience Manager] servern dina inloggningsuppgifter med Adobe I/O-gatewayen innan din begäran vidarebefordras till tjänsten.

* Skapa en konfiguration i [!DNL Experience Manager] för att generera en offentlig nyckel. Hämta ett offentligt certifikat för OAuth-integrering.
* Skapa en integrering i Adobe I/O och överför den genererade publika nyckeln.
* Konfigurera din [!DNL Experience Manager] instans med API-nyckeln och andra autentiseringsuppgifter från Adobe I/O.
* Du kan även aktivera automatisk taggning vid överföring av resurser.

### Krav för Adobe I/O-integrering {#prerequisite-for-aio-integration}

Innan du kan använda smarta taggar måste du göra följande för att skapa en integrering med Adobe I/O:

* Ett Adobe ID-konto som har administratörsbehörighet för organisationen.
* Smarta taggar är aktiverade för din organisation.

### Obtain a public certificate {#obtain-public-certificate}

Med ett offentligt certifikat kan du autentisera din profil på Adobe I/O.

1. I [!DNL Experience Manager] användargränssnittet går du till **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Legacy Cloud Services]**.

1. On the Cloud Services page, click **[!UICONTROL Configure Now]** under **[!UICONTROL Assets Smart Tags]**.

1. I **[!UICONTROL Create Configuration]** dialogrutan anger du en rubrik och ett namn för konfigurationen av smarta taggar. Klicka på **[!UICONTROL Create]**.

1. Använd följande värden i **[!UICONTROL AEM Smart Content Service]** dialogrutan:

   **[!UICONTROL Service URL]**: `https://mc.adobe.io/marketingcloud/smartcontent`

   **[!UICONTROL Authorization Server]**: `https://ims-na1.adobelogin.com`

   Lämna de andra fälten tomma (kommer senare). Klicka på **[!UICONTROL OK]**.

   ![Dialogrutan Experience Manager Smart Content Service för att tillhandahålla innehållstjänstens URL](assets/aem_scs.png)

1. Klicka **[!UICONTROL Download Public Certificate for OAuth Integration]** och hämta den offentliga certifikatfilen `AEM-SmartTags.crt`.

   ![Inställningar som har skapats för tjänsten för smart taggning](assets/download_link.png)

### Konfigurera om ett certifikat upphör att gälla {#certrenew}

När certifikatet upphör att gälla är det inte längre tillförlitligt. Följ de här stegen för att lägga till ett nytt certifikat. Du kan inte förnya ett certifikat som har upphört att gälla.

1. Log in your [!DNL Experience Manager] deployment as an administrator. Klicka på **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Users]**.

1. Leta reda på och klicka på **[!UICONTROL dam-update-service]** användaren. Klicka på **[!UICONTROL Keystore]** fliken.
1. Ta bort den befintliga **[!UICONTROL similaritysearch]** nyckelbehållaren med det certifikat som upphört att gälla. Klicka på **[!UICONTROL Save & Close]**.

   ![Ta bort befintlig likhetssökningspost i nyckelbehållaren om du vill lägga till ett nytt säkerhetscertifikat](assets/smarttags_delete_similaritysearch_keystore.png)

   *Bild: Ta bort den befintliga`similaritysearch`posten i nyckelbehållaren om du vill lägga till ett nytt säkerhetscertifikat.*

1. Navigera till **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Legacy Cloud Services]**. Klicka på **[!UICONTROL Asset Smart Tags]** > **[!UICONTROL Show Configuration]** > **[!UICONTROL Available Configurations]**. Klicka på önskad konfiguration.

1. Om du vill hämta ett offentligt certifikat klickar du på **[!UICONTROL Download Public Certificate for OAuth Integration]**.

1. Gå till [https://console.adobe.io](https://console.adobe.io) och navigera till den befintliga tjänsten i projektet. Överför det nya certifikatet. Mer information finns i anvisningarna i [Skapa Adobe I/O-integrering](#create-aio-integration).

### Skapa en integrering {#create-aio-integration}

Om du vill använda API:er för smarta taggar skapar du en integrering i Adobe I/O för att generera API-nyckel, ID för tekniskt konto, organisations-ID och klienthemlighet.

1. Gå till [https://console.adobe.io](https://console.adobe.io/).
1. Välj rätt konto och kontrollera att den associerade organisationsrollen är systemadministratör. Skapa ett projekt eller öppna ett befintligt projekt. Klicka på på projektsidan **[!UICONTROL Add API]**.
1. Markera **[!UICONTROL Add an API]** och markera på **[!UICONTROL Experience Cloud]** sidan **[!UICONTROL Smart Content]**. Klicka på **[!UICONTROL Continue]**.
1. På nästa sida väljer du **[!UICONTROL New integration]**. Klicka på **[!UICONTROL Continue]**.
1. På **[!UICONTROL Integration Details]** sidan anger du ett namn för integreringsgatewayen och lägger till en beskrivning.
1. I **[!UICONTROL Public keys certificates]**&#x200B;överför du `AEM-SmartTags.crt` filen som du laddade ned ovan.
1. Klicka på **[!UICONTROL Create Integration]**.
1. Om du vill visa integreringsinformationen klickar du på **[!UICONTROL Continue to integration details]**.

   ![På fliken Översikt kan du granska den information som finns för integrering.](assets/integration_details.png)

### Konfigurera smarta taggar {#configure-smart-content-service}

Om du vill konfigurera integreringen använder du nyckelfälten Teknisk konto-ID, Organisations-ID, Klienthemlighet, Auktoriseringsserver och API från Adobe I/O-integreringen. Om du skapar en molnkonfiguration för smarta taggar kan du autentisera API-begäranden från [!DNL Experience Manager] instansen.

1. I [!DNL Experience Manager]navigerar du till **[!UICONTROL Tools > Cloud Service > Legacy Cloud Services]** för att öppna [!UICONTROL Cloud Services] konsolen.
1. Öppna konfigurationen som skapats ovan under **[!UICONTROL Assets Smart Tags]**. Klicka på på tjänstinställningssidan **[!UICONTROL Edit]**.
1. I dialogrutan **[!UICONTROL AEM Smart Content Service]** använder du de förifyllda värdena för fälten **[!UICONTROL Service URL]** och **[!UICONTROL Authorization Server]**.
1. För fälten **[!UICONTROL API Key]**, **[!UICONTROL Technical Account Id]**, **[!UICONTROL Organization Id]** och **[!UICONTROL Client Secret]** använder du värdena som genereras ovan.

### Validera konfigurationen {#validate-the-configuration}

När du är klar med konfigurationen kan du använda en JMX MBean för att validera konfigurationen. Följ de här stegen för att validera.

1. Gå till din [!DNL Experience Manager] server på `https://[aem_server]:[port]`.

1. Gå till OSGi-konsolen **[!UICONTROL Tools > Operations > Web Console]** för att öppna den. Klicka på **[!UICONTROL Main > JMX]**.
1. Klicka på **[!UICONTROL com.day.cq.dam.similaritysearch.internal.impl]**. Den öppnas **[!UICONTROL SimilaritySearch Miscellaneous Tasks.]**.
1. Klicka på **[!UICONTROL validateConfigs()]**. In the **[!UICONTROL Validate Configurations]** dialog, click **[!UICONTROL Invoke]**.

   Valideringsresultatet visas i samma dialogruta.

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


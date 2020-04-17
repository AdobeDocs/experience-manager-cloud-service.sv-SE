---
title: Konfigurera AEM Assets as a Cloud Service med varumärkesportalen
description: Konfigurera AEM Assets as a Cloud Service med varumärkesportalen.
contentOwner: Vishabh Gupta
translation-type: tm+mt
source-git-commit: d644fc348ff6d62c03100941b96c03049f345763

---


# Konfigurera AEM Assets med varumärkesportalen {#configure-aem-assets-with-brand-portal}

Adobe Experience Manager (AEM) Assets konfigureras med varumärkesportalen via Adobe I/O, som hämtar en IMS-token för auktorisering av varumärkesportalens klient.

## Förutsättningar {#prerequisites}

Du behöver följande för att konfigurera AEM Assets med varumärkesportalen:

* En AEM Assets-molninstans som körs.
* Varumärkesportalens klientorganisations-URL.
* En användare med systemadministratörsbehörighet på IMS-organisationen för varumärkesportalens klient.

**Kontakta supporten** för mer information.

## Skapa en konfiguration {#create-new-configuration}

Du kan skapa en konfiguration på Adobe I/O för att konfigurera din AEM Assets-molninstans med varumärkesportalen.

Utför följande steg i den angivna ordningen:
1. [Hämta ett offentligt certifikat](#public-certificate)
1. [Skapa en Adobe I/O-integrering](#createnewintegration)
1. [Skapa en konfiguration för IMS-kontot](#create-ims-account-configuration)
1. [Konfigurera molntjänsten](#configure-the-cloud-service)
1. [Testa konfigurationen](#test-configuration)

### Skapa IMS-konfigurationen {#create-ims-configuration}

IMS-konfigurationen autentiserar varumärkesportalens klient med författarinstansen för AEM Assets.

IMS-konfigurationen har två steg:

* [Hämta ett offentligt certifikat](#public-certificate)
* [Skapa en konfiguration för IMS-kontot](#create-ims-account-configuration)

### Hämta ett offentligt certifikat {#public-certificate}

Med ett offentligt certifikat kan du autentisera din profil på Adobe I/O.

1. Logga in på AEM Assets-molninstansen.

1. Gå till **Säkerhet** > ![Adobe IMS-konfigurationer](assets/tools.png) på verktygspanelen **** Verktyg ****.

   ![Användargränssnittet för konfiguration av Adobe IMS-kontot](assets/ims-configuration1.png)

1. Sidan Adobe IMS-konfigurationer öppnas.

   Klicka på **[!UICONTROL Skapa]**.

   Du kommer till sidan Konfiguration **[!UICONTROL av]** Adobe IMS-konto.

1. Fliken **Certifikat** öppnas som standard.

   I **molnlösning** väljer du **[!UICONTROL Adobe Brand Portal]**.

1. Markera kryssrutan **[!UICONTROL Skapa nytt certifikat]** och ange ett **alias** för certifikatet. Aliaset används som namn på dialogrutan.

1. Klicka på **[!UICONTROL Skapa certifikat]**. En dialogruta visas. Click **[!UICONTROL OK]** to generate the public certificate.

   ![Skapa ett certifikat](assets/ims-config2.png)

1. Click **[!UICONTROL Download Public Key]** and save the *AEM-Adobe-IMS.crt* certificate file on your machine. Certifikatfilen används för att [skapa Adobe I/O-integreringen](#createnewintegration).

   ![Hämta certifikatet](assets/ims-config3.png)

1. Klicka på **[!UICONTROL Nästa]**.

   Du skapar Adobe IMS-kontot på fliken **Konto**, men för det behöver du integreringsinformationen. Håll den här sidan öppen tills vidare.

   Öppna en ny flik och [skapa Adobe I/O-integreringen](#createnewintegration) för att få tillgång till integreringsinformationen för IMS-kontokonfigurationerna.

### Skapa en Adobe I/O-integrering{#createnewintegration}

Adobe I/O-integreringen genererar en API-nyckel, en klienthemlighet och en nyttolast (JWT), som krävs för att konfigurera IMS-kontokonfigurationer.

1. Logga in på konsolen Adobe I/O med systemadministratörsbehörighet på IMS-organisationen för varumärkesportalens klient.

   Standard-URL: [https://console.adobe.io/](https://console.adobe.io/)

1. Klicka på **[!UICONTROL Skapa integrering]**.

1. Välj **[!UICONTROL Åtkomst till ett API]** och klicka på **[!UICONTROL Fortsätt]**.

   ![Skapa en ny integrering](assets/create-new-integration1.png)

1. Sidan Skapa en ny integrering öppnas.

   Välj din organisation i listrutan.

   I **[!UICONTROL Experience Cloud]** väljer du **[!UICONTROL AEM Brand Portal]** och klickar på **[!UICONTROL Fortsätt]**.

   If the Brand Portal option is disabled for you, ensure that you have selected correct organization from the drop-down box above the **[!UICONTROL Adobe Services]** option. Kontakta administratören om du inte känner till din organisation.

   ![Skapa en integrering](assets/create-new-integration2.png)

1. Ange ett namn och en beskrivning för integrationen. Klicka på **[!UICONTROL Välj en fil på datorn]** och överför den `AEM-Adobe-IMS.crt` fil som laddats ned i avsnittet [Hämta offentliga certifikat](#public-certificate) .

1. Välj organisationens profil.

   Du kan också välja standardprofilens **[!UICONTROL resursportal]** och klicka på **[!UICONTROL Skapa integrering]**. Integreringen skapas.

1. Klicka på **[!UICONTROL Fortsätt om du vill visa integreringsinformationen]** .

   Kopiera **[!UICONTROL API-nyckeln]**

   Klicka på **[!UICONTROL Hämta klienthemlighet]** och kopiera klienthemlighet.

   ![API-nyckel, klienthemlighet och nyttolastinformation för en integrering](assets/create-new-integration3.png)

1. Navigera till **[!UICONTROL JWT]** -fliken och kopiera **[!UICONTROL JWT-nyttolasten]**.

   API-nyckeln, nyckeln för klienthemligheten och informationen för JWT-nyttolasten används för att skapa en IMS-kontokonfiguration.

### Skapa en konfiguration för IMS-kontot {#create-ims-account-configuration}

Kontrollera att du har utfört följande steg:

* [Hämta ett offentligt certifikat](#public-certificate)
* [Skapa en Adobe I/O-integrering](#createnewintegration)

**Så här skapar du en IMS-kontokonfiguration:**

1. Open the IMS Configuration page, **[!UICONTROL Accounts]** tab. Du lämnade den här sidan öppen i slutet av avsnittet [Hämta ett offentligt certifikat ](#public-certificate).

1. Specify a **[!UICONTROL Title]** for the IMS account.

   In **[!UICONTROL Authorization Server]**, enter the URL: [https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/)

   Klistra in API-nyckeln, klienthemligheten och JWT-nyttolasten som du kopierade i slutet av [Skapa en Adobe I/O-integrering](#createnewintegration).

   Klicka på **[!UICONTROL Skapa]**.

   Integreringen skapas.

   ![Konfiguration av ett IMS-konto](assets/create-new-integration6.png)


1. Select the IMS configuration and click **[!UICONTROL Check Health]**. En dialogruta visas.

   Klicka på **[!UICONTROL Kontrollera]**. Meddelandet *Token har hämtats* visas när en anslutning har skapats.

   ![](assets/create-new-integration5.png)

>[!CAUTION]
>
>Du får bara ha en IMS-konfiguration som klarar hälsokontrollen. Skapa inte flera IMS-konfigurationer.
>
>Om konfigurationen inte godkänns i hälsokontrollen är den ogiltig. Du måste ta bort den och skapa en ny, giltig konfiguration.



### Konfigurera molntjänsten{#configure-the-cloud-service}

Gör så här för att skapa molntjänstkonfigurationen för varumärkesportalen:

1. Logga in på AEM Assets-molninstansen.

1. Gå till **Cloud Services** > ![AEM Brand Portal](assets/tools.png) från verktygspanelen **** Verktyg ****.

   Sidan Konfigurationer för varumärkesportalen öppnas.

1. Klicka på **[!UICONTROL Skapa]**.

1. Specify a **[!UICONTROL Title]** for the configuration.

   Välj den IMS-konfiguration som du har skapat i steget [Skapa en konfiguration för IMS-kontot](#create-ims-account-configuration).

   In **[!UICONTROL Service URL]**, enter your Brand Portal tenant URL.

   ![](assets/create-cloud-service.png)

1. Klicka på **[!UICONTROL Spara och stäng]**. Molnkonfigurationen har skapats. AEM Assets-molninstansen är nu konfigurerad med varumärkesportalens klient.

### Testa konfigurationen {#test-configuration}

1. Logga in på AEM Assets-molninstansen.

1. Gå till **Distribution** > ![Distribution](assets/tools.png) på verktygspanelen **** Verktyg ****.

   ![](assets/test-bpconfig1.png)

1. Sidan Distribution öppnas.

   En varumärkesportaldistributionsagent `bpdistributionagent0` skapas under **[!UICONTROL Publicera till varumärkesportal]**.

   Klicka på **[!UICONTROL Publicera på varumärkesportal]**.

   ![](assets/test-bpconfig2.png)

   >[!NOTE]
   >
   >Som standard skapas en distributionsagent för varumärkesportalens klient.

1. Sidan Distributionsagent öppnas. By default, the **[!UICONTROL Status]** tab opens which populates the distribution queues.

   En distributionsagent har två köer:
   * **processing-queue**: för distribution av tillgångar till varumärkesportalen.

   * **felkö**: för resurser där distributionen misslyckades.
   >[!NOTE]
   >
   >Vi rekommenderar att du regelbundet granskar felen och rensar **felkön** .

   ![](assets/test-bpconfig3.png)

1. To verify the connection between AEM Assets and Brand Portal, click **[!UICONTROL Test Connection]**.

   ![](assets/test-bpconfig4.png)

   Ett meddelande visas längst ned på sidan om att testpaketet har levererats.

   >[!NOTE]
   >
   >Undvik att inaktivera distributionsagenten eftersom det kan göra att distributionen av resurserna (i kön) misslyckas.


Din AEM Assets-molninstans har konfigurerats med varumärkesportalen och du kan nu:

* [Publicera resurser från AEM Assets till varumärkesportalen](publish-to-brand-portal.md)
* [Publicera mappar från AEM Assets till varumärkesportalen](publish-to-brand-portal.md#publish-folders-to-brand-portal)
* [Publicera samlingar från AEM Assets till varumärkesportalen](publish-to-brand-portal.md#publish-collections-to-brand-portal)

Förutom ovanstående kan du även publicera metadatamatcheman, bildförinställningar, sökfaktorer och taggar från AEM Assets till Brand Portal.

* [Publicera förinställningar, scheman och ansiktsuttryck på varumärkesportalen](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/publish/publish-schema-search-facets-presets.html)
* [Publicera taggar i varumärkesportalen](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/publish/brand-portal-publish-tags.html)


Mer information finns i dokumentationen [till](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/home.html) varumärkesportalen.


## Distributionsloggar {#distribution-logs}

Du kan kontrollera loggarna och se detaljerad information om de åtgärder som har utförts på distributionsagenten.

Vi har till exempel publicerat en resurs från AEM Assets till varumärkesportalen för att verifiera konfigurationen.

1. Follow the steps (Step 1 - 4) as shown in **[!UICONTROL Test Connection]** and navigate to the distribution agent page.

1. Klicka på **[!UICONTROL Loggar]** för att visa distributionsloggarna. Bearbetnings- och felloggarna visas här.

   ![](assets/test-bpconfig5.png)

Distributionsagenten genererar följande loggar:

* INFORMATION: Detta är en systemgenererad logg som utlöser lyckad konfiguration som aktiverar distributionsagenten.
* DSTRQ1 (Request 1): Utlösare vid testanslutning.

Följande begärande- och svarsloggar genereras när resursen publiceras:

**Begäranden från distributionsagenten**:
* DSTRQ2 (Begäran 2): Begäran om publicering av resurser utlöses.
* DSTRQ3 (Request 3): Systemet utlöser en annan begäran om att publicera mappen där resursen finns och replikerar mappen i varumärkesportalen.

**Svar från distributionsagenten**:
* queue-bpdistributionagent0 (DSTRQ2): Resursen publiceras på varumärkesportalen.
* queue-bpdistributionagent0 (DSTRQ3): Systemet replikerar mappen som innehåller resursen i varumärkesportalen.

I exemplet ovan utlöses ytterligare en begäran och ett svar. Systemet kunde inte hitta den överordnade mappen (alias Lägg till sökväg) i varumärkesportalen eftersom resursen publicerades för första gången. Därför utlöses en ytterligare begäran om att skapa en överordnad mapp med samma namn i varumärkesportalen där resursen publiceras.

>[!NOTE]
>
>Ytterligare begäran genereras om den överordnade mappen inte finns i varumärkesportalen (i exemplet ovan) eller om den överordnade mappen har ändrats i AEM Resurser.



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

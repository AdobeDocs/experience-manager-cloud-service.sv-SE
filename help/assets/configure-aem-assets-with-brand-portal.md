---
title: Konfigurera AEM Assets as a Cloud Service med varumärkesportalen
description: Konfigurera AEM Assets as a Cloud Service med varumärkesportalen.
contentOwner: Vishabh Gupta
translation-type: tm+mt
source-git-commit: 00e37e9493bc3dde8a4d83c562a889a67587ada0
workflow-type: tm+mt
source-wordcount: '1240'
ht-degree: 99%

---


# Konfigurera AEM Assets med varumärkesportalen {#configure-aem-assets-with-brand-portal}

Adobe Experience Manager (AEM) Assets konfigureras med varumärkesportalen via Adobe I/O, som hämtar en IMS-token för auktorisering av varumärkesportalens klient.

## Förutsättningar {#prerequisites}

Du behöver följande för att konfigurera AEM Assets med varumärkesportalen:

* En AEM Assets-molninstans som körs.
* Varumärkesportalens klientorganisations-URL.
* En användare med systemadministratörsbehörighet på IMS-organisationen för varumärkesportalens klient.

**Kontakta kundtjänst** om du vill ha fler frågor.

## Skapa en konfiguration {#create-new-configuration}

Du kan skapa en konfiguration på Adobe I/O för att konfigurera AEM Assets-molninstansen med varumärkesportalen.

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

1. Gå till **[!UICONTROL Security]** > **[!UICONTROL Adobe IMS Configurations]** från **verktygspanelen** ![Tools](assets/tools.png).

   ![Användargränssnittet för konfiguration av Adobe IMS-kontot](assets/ims-configuration1.png)

1. Sidan Adobe IMS-konfigurationer öppnas.

   Klicka på **[!UICONTROL Create]**.

   Sidan **[!UICONTROL Adobe IMS Technical Account Configuration]** öppnas.

1. Fliken **Certifikat** öppnas som standard.

   Välj **[!UICONTROL Adobe Brand Portal]** i **Molnlösning**,

1. Markera kryssrutan **[!UICONTROL Create new certificate]** och ange ett **alias** för certifikatet. Aliaset används som namn på dialogrutan.

1. Klicka på **[!UICONTROL Create certificate]**. En dialogruta visas. Klicka på **[!UICONTROL OK]** för att generera det offentliga certifikatet.

   ![Skapa ett certifikat](assets/ims-config2.png)

1. Klicka på **[!UICONTROL Download Public Key]** och spara certifikatfilen *AEM-Adobe-IMS.crt* på datorn. Certifikatfilen används för att [skapa Adobe I/O-integreringen](#createnewintegration).

   ![Hämta certifikatet](assets/ims-config3.png)

1. Klicka på **[!UICONTROL Next]**.

   Du skapar Adobe IMS-kontot på fliken **Konto**, men för det behöver du integreringsinformationen. Håll den här sidan öppen tills vidare.

   Öppna en ny flik och [skapa Adobe I/O-integreringen](#createnewintegration) för att få tillgång till integreringsinformationen för IMS-kontokonfigurationerna.

### Skapa en Adobe I/O-integrering{#createnewintegration}

Adobe I/O-integreringen genererar en API-nyckel, en klienthemlighet och en nyttolast (JWT), som krävs för att konfigurera IMS-kontokonfigurationer.

1. Logga in på konsolen Adobe I/O med systemadministratörsbehörighet på IMS-organisationen för varumärkesportalens klient.

   Standard-URL: [https://console.adobe.io/](https://console.adobe.io/)

1. Klicka på **[!UICONTROL Create Integration]**.

1. Markera **[!UICONTROL Access an API]** och klicka på **[!UICONTROL Continue]**.

   ![Skapa en ny integrering](assets/create-new-integration1.png)

1. Sidan Skapa en ny integrering öppnas.

   Välj din organisation i listrutan.

   Välj **[!UICONTROL AEM Brand Portal]** och klicka på **[!UICONTROL Continue]** i **[!UICONTROL Experience Cloud]**.

   Kontrollera att du har valt rätt organisation i listrutan ovanför alternativet **[!UICONTROL Adobe Services]** om alternativet Varumärkesportal är inaktiverat. Kontakta administratören om du inte känner till din organisation.

   ![Skapa en integrering](assets/create-new-integration2.png)

1. Ange ett namn och en beskrivning för integrationen. Klicka på **[!UICONTROL Select a File from your computer]** och överför filen `AEM-Adobe-IMS.crt` som laddades ner under [Hämta ett offentligt certifikat](#public-certificate) .

1. Välj organisationens profil.

   Du kan också markera standardprofilen **[!UICONTROL Assets Brand Portal]** och klicka på **[!UICONTROL Create Integration]**. Integreringen skapas.

1. Klicka på **[!UICONTROL Continue to integration details]** för att visa integreringsinformationen.

   Kopiera **[!UICONTROL API Key]**

   Klicka på **[!UICONTROL Retrieve Client Secret]** och kopiera nyckeln för klienthemligheten.

   ![API-nyckel, klienthemlighet och nyttolastinformation för en integrering](assets/create-new-integration3.png)

1. Gå till fliken **[!UICONTROL JWT]** och kopiera **[!UICONTROL JWT payload]**.

   API-nyckeln, nyckeln för klienthemligheten och informationen för JWT-nyttolasten används för att skapa en IMS-kontokonfiguration.

### Skapa en konfiguration för IMS-kontot {#create-ims-account-configuration}

Kontrollera att du har utfört följande steg:

* [Hämta ett offentligt certifikat](#public-certificate)
* [Skapa en Adobe I/O-integrering](#createnewintegration)

**Så här skapar du en IMS-kontokonfiguration:**

1. Öppna sidan IMS-konfiguration och fliken **[!UICONTROL Accounts]**. Du lämnade den här sidan öppen i slutet av avsnittet [Hämta ett offentligt certifikat ](#public-certificate).

1. Ange en **[!UICONTROL Title]** för IMS-kontot.

   Ange URL:en [https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/) i **[!UICONTROL Authorization Server]**.

   Klistra in API-nyckeln, klienthemligheten och JWT-nyttolasten som du kopierade i slutet av [Skapa en Adobe I/O-integrering](#createnewintegration).

   Klicka på **[!UICONTROL Create]**.

   Integreringen skapas.

   ![Konfiguration av ett IMS-konto](assets/create-new-integration6.png)


1. Markera IMS-konfigurationen och klicka på **[!UICONTROL Check Health]**. En dialogruta visas.

   Klicka på **[!UICONTROL Check]**. Meddelandet *Token har hämtats* visas när en anslutning har skapats.

   ![](assets/create-new-integration5.png)

>[!CAUTION]
>
>Du får bara ha en IMS-konfiguration. Skapa inte flera IMS-konfigurationer.
>
>Kontrollera att IMS-konfigurationen klarar hälsokontrollen. Om konfigurationen inte godkänns i hälsokontrollen är den ogiltig. Du måste ta bort den och skapa en ny, giltig konfiguration.



### Konfigurera molntjänsten{#configure-the-cloud-service}

Gör så här för att skapa molntjänstkonfigurationen för varumärkesportalen:

1. Logga in på AEM Assets-molninstansen.

1. Gå till **[!UICONTROL Cloud Services]** > **[!UICONTROL AEM Brand Portal]** från **verktygspanelen** ![Tools](assets/tools.png).

   Sidan Konfigurationer för varumärkesportalen öppnas.

1. Klicka på **[!UICONTROL Create]**.

1. Ange en **[!UICONTROL Title]** för konfigurationen.

   Välj den IMS-konfiguration som du har skapat i steget [Skapa en konfiguration för IMS-kontot](#create-ims-account-configuration).

   Ange varumärkesportalens klientorganisations-URL i **[!UICONTROL Service URL]**.

   ![](assets/create-cloud-service.png)

1. Klicka på **[!UICONTROL Save and Close]**. Molnkonfigurationen har skapats. AEM Assets-molninstansen är nu konfigurerad med varumärkesportalens klient.

### Testa konfigurationen {#test-configuration}

1. Logga in på AEM Assets-molninstansen.

1. Gå till **[!UICONTROL Deployment]** > **[!UICONTROL Distribution]** från **verktygspanelen** ![Tools](assets/tools.png).

   ![](assets/test-bpconfig1.png)

1. Sidan Distribution öppnas.

   En distributionsagent `bpdistributionagent0` för varumärkesportalen skapas under **[!UICONTROL Publish to Brand Portal]**.

   Klicka på **[!UICONTROL Publish to Brand Portal]**.

   ![](assets/test-bpconfig2.png)

   >[!NOTE]
   >
   >Som standard skapas en distributionsagent för varumärkesportalens klient.

1. Sidan Distributionsagent öppnas. Som standard öppnas fliken **[!UICONTROL Status]** som fyller i distributionsköerna.

   En distributionsagent har två köer:
   * **processing-queue**: för distribution av resurser till varumärkesportalen.

   * **error-queue**: för resurser där distributionen misslyckades.
   >[!NOTE]
   >
   >Vi rekommenderar att du regelbundet granskar felen och rensar **error-queue**.

   ![](assets/test-bpconfig3.png)

1. Kontrollera anslutningen mellan AEM Assets och varumärkesportalen genom att klicka på **[!UICONTROL Test Connection]**.

   ![](assets/test-bpconfig4.png)

   Ett meddelande visas längst ned på sidan om att testpaketet har levererats.

   >[!NOTE]
   >
   >Undvik att inaktivera distributionsagenten eftersom det kan göra att distributionen av resurserna (i kön) misslyckas.


Din AEM Assets-molninstans har konfigurerats med varumärkesportalen och du kan nu:

* [Publicera resurser från AEM Assets till varumärkesportalen](publish-to-brand-portal.md)
* [Publicera mappar från AEM Assets till varumärkesportalen](publish-to-brand-portal.md#publish-folders-to-brand-portal)
* [Publicera samlingar från AEM Assets till varumärkesportalen](publish-to-brand-portal.md#publish-collections-to-brand-portal)

Förutom ovanstående kan du även publicera metadatascheman, bildförinställningar, sökfasetter och taggar från AEM Assets till varumärkesportalen.

* [Publicera förinställningar, scheman och fasetter på varumärkesportalen](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/publish/publish-schema-search-facets-presets.html)
* [Publicera taggar på varumärkesportalen](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/publish/brand-portal-publish-tags.html)


Mer information finns i [dokumentationen till varumärkesportalen](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/home.html).


## Distributionsloggar {#distribution-logs}

Du kan kontrollera loggarna och se detaljerad information om de åtgärder som har utförts på distributionsagenten.

Vi har till exempel publicerat en resurs från AEM Assets till varumärkesportalen för att verifiera konfigurationen.

1. Följ stegen (steg 1 till 4) som visas i **[!UICONTROL Test Connection]** och gå till sidan för distributionsagenten.

1. Klicka på **[!UICONTROL Logs]** för att visa distributionsloggarna. Bearbetnings- och felloggarna visas här.

   ![](assets/test-bpconfig5.png)

Distributionsagenten genererar följande loggar:

* INFO: En systemgenererad logg som utlöses när en konfiguration aktiverar distributionsagenten.
* DSTRQ1 (Begäran 1): Utlöses vid testanslutning.

Följande begärande- och svarsloggar genereras när resursen publiceras:

**Begäranden från distributionsagenten**:
* DSTRQ2 (Begäran 2): Begäran om publicering av resurser utlöses.
* DSTRQ3 (Begäran 3): Systemet utlöser en annan begäran om att publicera mappen där resursen finns och replikerar mappen i varumärkesportalen.

**Svar från distributionsagenten**:
* queue-bpdistributionagent0 (DSTRQ2): Resursen publiceras på varumärkesportalen.
* queue-bpdistributionagent0 (DSTRQ3): Systemet replikerar mappen som innehåller resursen i varumärkesportalen.

I exemplet ovan utlöses ytterligare en begäran och ett svar. Systemet kunde inte hitta den överordnade mappen (dvs. Lägg till sökväg) i varumärkesportalen eftersom resursen publicerades för första gången. Därför utlöses en ytterligare begäran om att skapa en överordnad mapp med samma namn i varumärkesportalen där resursen publiceras.

>[!NOTE]
>
>Ytterligare en begäran skapas om den överordnade mappen inte finns i varumärkesportalen (som i exemplet ovan) eller om den överordnade mappen har ändrats i AEM Assets.



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

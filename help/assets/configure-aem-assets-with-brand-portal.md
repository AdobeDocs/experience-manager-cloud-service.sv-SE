---
title: Konfigurera molntjänsten AEM Assets med varumärkesportalen
description: Konfigurera molntjänsten AEM Assets med varumärkesportalen.
contentOwner: Vishabh Gupta
translation-type: tm+mt
source-git-commit: 4677a8771c5891b8c9846e0adb58025304a71bdd

---


# Konfigurera AEM-resurser med varumärkesportalen {#configure-aem-assets-with-brand-portal}

Adobe Experience Manager Assets (AEM) är konfigurerat med varumärkesportalen via Adobe I/O, som anskaffar en IMS-token för auktorisering av er varumärkesportal.

## Förutsättningar {#prerequisites}

Du behöver följande för att konfigurera AEM Assets med varumärkesportalen:

* En AEM Assets-molninstans som körs.
* Klient-URL för varumärkesportalen.
* En användare med systemadministratörsbehörighet för IMS-organisationen för innehavaren av varumärkesportalen.

**Kontakta supporten** om du vill ha fler frågor.

## Skapa konfiguration {#create-new-configuration}

Du kan skapa en ny konfiguration på Adobe I/O för att konfigurera din AEM Assets-molninstans med varumärkesportalen.

Utför följande steg i den listade sekvensen:
1. [Hämta offentligt certifikat](#public-certificate)
1. [Skapa Adobe I/O-integration](#createnewintegration)
1. [Skapa konfiguration för IMS-konto](#create-ims-account-configuration)
1. [Konfigurera molntjänst](#configure-the-cloud-service)
1. [Testa konfiguration](#test-configuration)

### Skapa IMS-konfiguration {#create-ims-configuration}

IMS-konfigurationen autentiserar din klient för varumärkesportalen med författarinstansen för AEM Assets.

IMS-konfigurationen innehåller två steg:

* [Hämta offentligt certifikat](#public-certificate)
* [Skapa konfiguration för IMS-konto](#create-ims-account-configuration)

### Hämta offentligt certifikat {#public-certificate}

Med ett offentligt certifikat kan du autentisera din profil på Adobe I/O.

1. Logga in på din AEM Assets-molninstans

1. Gå till **Säkerhet** > ![Adobe IMS-konfigurationer](assets/tools.png) på panelen Verktyg **** Verktyg ****.

   ![Användargränssnitt för Adobe IMS-kontokonfiguration](assets/ims-configuration1.png)

1. Sidan Adobe IMS-konfigurationer öppnas.

   Klicka på **[!UICONTROL Skapa]**.

   Du kommer nu till sidan Konfiguration **[!UICONTROL av]** Adobe IMS Technical Account.

1. Fliken **Certifikat** öppnas som standard.

   I **molnlösning** väljer du **[!UICONTROL Adobe Brand Portal]**.

1. Markera kryssrutan **[!UICONTROL Skapa nytt certifikat]** och ange ett **alias** för certifikatet. Aliaset fungerar som namn på dialogrutan.

1. Klicka på **[!UICONTROL Skapa certifikat]**. En dialogruta visas. Klicka på **[!UICONTROL OK]** för att generera det offentliga certifikatet.

   ![Skapa certifikat](assets/ims-config2.png)

1. Klicka på **[!UICONTROL Hämta offentlig nyckel]** och spara *certifikatfilen AEM-Adobe-IMS.crt* på datorn. Certifikatfilen används för att [skapa Adobe I/O-integrering](#createnewintegration).

   ![Hämta certifikat](assets/ims-config3.png)

1. Click **[!UICONTROL Next]**.

   På fliken **Konto** skapar du Adobe IMS-kontot, men för det behöver du integreringsinformationen. Håll den här sidan öppen tills vidare.

   Öppna en ny flik och [skapa Adobe I/O-integrering](#createnewintegration) för att få integreringsinformation för IMS-kontokonfigurationer.

### Skapa Adobe I/O-integration {#createnewintegration}

Adobe I/O-integrering genererar API-nyckel, klienthemlighet och nyttolast (JWT) som krävs för att konfigurera IMS-kontokonfigurationer.

1. Logga in på Adobe I/O Console med systemadministratörsbehörighet för IMS-organisationen för innehavaren av varumärkesportalen.

   Standard-URL: [https://console.adobe.io/](https://console.adobe.io/)

1. Klicka på **[!UICONTROL Skapa integrering]**.

1. Välj **[!UICONTROL Åtkomst till ett API]** och klicka på **[!UICONTROL Fortsätt]**.

   ![Skapa ny integrering](assets/create-new-integration1.png)

1. Skapa en ny integreringssida öppnas.

   Välj din organisation i listrutan.

   I **[!UICONTROL Experience Cloud]** väljer du **[!UICONTROL AEM Brand Portal]** och klickar på **[!UICONTROL Fortsätt]**.

   Om alternativet Varumärksportal är inaktiverat för dig kontrollerar du att du har valt rätt organisation i listrutan ovanför alternativet **[!UICONTROL Adobe-tjänster]** . Kontakta administratören om du inte känner till din organisation.

   ![Skapa integrering](assets/create-new-integration2.png)

1. Ange ett namn och en beskrivning för integreringen. Klicka på **[!UICONTROL Välj en fil på datorn]** och överför den `AEM-Adobe-IMS.crt` fil som laddats ned i avsnittet [Hämta offentliga certifikat](#public-certificate) .

1. Välj profil för din organisation.

   Du kan också välja standardprofilens **[!UICONTROL resursportal]** och klicka på **[!UICONTROL Skapa integrering]**. Integrationen skapas.

1. Klicka på **[!UICONTROL Fortsätt om du vill visa integreringsinformationen]** .

   Kopiera **[!UICONTROL API-nyckeln]**

   Klicka på **[!UICONTROL Hämta klienthemlighet]** och kopiera klienthemlighet.

   ![API-nyckel, klienthemlighet och nyttolastinformation för en integrering](assets/create-new-integration3.png)

1. Navigera till **[!UICONTROL JWT]** -fliken och kopiera **[!UICONTROL JWT-nyttolasten]**.

   API-nyckeln, klienthemlig nyckel och JWT-nyttolastinformationen används för att skapa en IMS-kontokonfiguration.

### Skapa konfiguration för IMS-konto {#create-ims-account-configuration}

Kontrollera att du har utfört följande steg:

* [Hämta offentligt certifikat](#public-certificate)
* [Skapa Adobe I/O-integration](#createnewintegration)

**Steg för att skapa IMS-kontokonfiguration:**

1. Öppna sidan IMS-konfiguration på fliken **[!UICONTROL Konton]** . Du höll sidan öppen i slutet av avsnittet [Hämta offentligt certifikat](#public-certificate).

1. Ange en **[!UICONTROL titel]** för IMS-kontot.

   Ange URL:en i **[!UICONTROL Authorization Server]**: [https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/)

   Klistra in API-nyckeln, klienthemligheten och JWT-nyttolasten som du har kopierat i slutet av [Skapa Adobe I/O-integrering](#createnewintegration).

   Klicka på **[!UICONTROL Skapa]**.

   Integrationen skapas.

   ![Konfiguration av IMS-konto](assets/create-new-integration6.png)


1. Välj IMS-konfigurationen och klicka på **[!UICONTROL Kontrollera hälsa]**. En dialogruta visas.

   Klicka på **[!UICONTROL Kontrollera]**. När anslutningen är klar visas meddelandet *Token har* hämtats.

   ![](assets/create-new-integration5.png)

>[!CAUTION]
>
>Skapa endast en giltig IMS-konfiguration. Skapa inte flera IMS-konfigurationer.
>
> Kontrollera att konfigurationen är felfri. Om konfigurationen inte är felfri tar du bort den och skapar en ny felfri konfiguration.


### Konfigurera molntjänst {#configure-the-cloud-service}

Så här skapar du molntjänstkonfigurationen Brand Portal:

1. Logga in på din AEM Assets-molninstans

1. Gå till **Cloud Services** > ![AEM Brand Portal](assets/tools.png) på panelen Verktyg **** Verktyg ****.

   Sidan Konfigurationer för varumärkesportalen öppnas.

1. Klicka på **[!UICONTROL Skapa]**.

1. Ange en **[!UICONTROL titel]** för konfigurationen.

   Välj den IMS-konfiguration som du har skapat i steget och [skapa en IMS-kontokonfiguration](#create-ims-account-configuration).

   Ange din klientorganisations-URL i **[!UICONTROL Service URL]**.

   ![](assets/create-cloud-service.png)

1. Klicka på **[!UICONTROL Spara och stäng]**. Molnkonfigurationen skapas. Din AEM Assets-molninstans är nu konfigurerad med innehavaren av varumärkesportalen.

### Testa konfiguration {#test-configuration}

1. Logga in på din AEM Assets-molninstans.

1. Gå till **Distribution** > ![Distribution](assets/tools.png) på panelen Verktyg **** och gå till **[!UICONTROL Distribution]**>Distribution.

   ![](assets/test-bpconfig1.png)

1. Distributionssidan öppnas.

   En varumärkesportaldistributionsagent `bpdistributionagent0` skapas under **[!UICONTROL Publicera till varumärkesportal]**.

   Klicka på **[!UICONTROL Publicera på varumärkesportal]**.

   ![](assets/test-bpconfig2.png)

   >[!NOTE]
   >
   >Som standard skapas en distributionsagent för en innehavare av en varumärksportal.

1. Distributionsagentsidan öppnas. Som standard öppnas fliken **[!UICONTROL Status]** som fyller i distributionsköerna.

   En distributionsagent innehåller två köer:
   * En bearbetningskö för distribution av resurser till varumärkesportalen.
   * En felkö för resurserna där distributionen misslyckades.
   ![](assets/test-bpconfig3.png)

1. Kontrollera anslutningen mellan AEM Assets och Brand Portal genom att klicka på **[!UICONTROL Testa anslutning]**.

   ![](assets/test-bpconfig4.png)

   Ett meddelande visas längst ned på sidan om att testpaketet har levererats.

   >[!NOTE]
   >
   >Undvik att inaktivera distributionsagenten eftersom det kan göra att distributionen av resurserna (i kö) misslyckas.


Din AEM Assets-molninstans har konfigurerats med varumärkesportalen och du kan nu:

* [Publicera resurser från AEM Assets till varumärkesportalen](publish-to-brand-portal.md)
* [Publicera mappar från AEM Assets till varumärkesportalen](publish-to-brand-portal.md#publish-folders-to-brand-portal)
* [Publicera samlingar från AEM Assets till varumärkesportalen](publish-to-brand-portal.md#publish-collections-to-brand-portal)

Förutom ovanstående kan du även publicera metadatamatcheman, bildförinställningar, sökfaktorer och taggar från AEM Assets till Brand Portal.

* [Publicera förinställningar, scheman och ansiktsuttryck på varumärkesportalen](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/publish/publish-schema-search-facets-presets.html)
* [Publicera taggar i varumärkesportalen](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/publish/brand-portal-publish-tags.html)


Mer information finns i dokumentationen [till](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/home.html) varumärkesportalen.


## Distributionsloggar {#distribution-logs}

Du kan kontrollera loggarna för detaljerad information om de åtgärder som har utförts på distributionsagenten.

Vi har till exempel publicerat en resurs från AEM Assets till varumärkesportalen för att verifiera konfigurationen.

1. Följ stegen (steg 1 till 4) som visas i **[!UICONTROL Testanslutning]** och navigera till distributionsagentsidan.

1. Klicka på **[!UICONTROL Loggar]** för att visa distributionsloggarna. Bearbetnings- och felloggarna visas här.

   ![](assets/test-bpconfig5.png)

Distributionsagenten genererar följande loggar:

* INFORMATION: Detta är en systemgenererad logg som triggas på en lyckad konfiguration som aktiverar distributionsagenten.
* DSTRQ1 (Request 1): Testanslutningen är påslagen.

När resursen publiceras genereras följande begärande- och svarsloggar:

**Begäran** om distributionsagent:
* DSTRQ2 (Request 2): Begäran om publicering av tillgångar utlöses.
* DSTRQ3 (Request 3): Systemet utlöser en annan begäran om att publicera mappen där resursen finns och replikerar mappen i varumärkesportalen.

**Svar från** distributionsagent:
* queue-bpdistributagent0 (DSTRQ2): Resursen publiceras på varumärkesportalen.
* queue-bpdistributagent0 (DSTRQ3): Systemet replikerar mappen som innehåller resursen i varumärkesportalen.

I exemplet ovan utlöses ytterligare en begäran och ett svar. Systemet kunde inte hitta den överordnade mappen (alias Lägg till sökväg) i varumärkesportalen eftersom resursen publicerades för första gången. Därför utlöses en ytterligare begäran om att skapa en överordnad mapp med samma namn i varumärkesportalen där resursen publiceras.

>[!NOTE]
>
>Ytterligare begäran genereras om den överordnade mappen inte finns i varumärkesportalen (i exemplet ovan) eller om den överordnade mappen har ändrats i AEM Resurser.


## Ytterligare information {#additional-information}

Gå till `/system/console/slingmetrics` för statistik om det distribuerade innehållet:

1. **Räknarstatistik**
   * sling: `mac_sync_request_failure`
   * sling: `mac_sync_request_received`
   * sling: `mac_sync_request_success`

1. **Tidsmått**
   * sling: `mac_sync_distribution_duration`
   * sling: `mac_sync_enqueue_package_duration`
   * sling: `mac_sync_setup_request_duration`



<!--
   Comment Type: draft

   <li> </li>
   -->

<!--
   Comment Type: draft

   <li>Step text</li>
   -->

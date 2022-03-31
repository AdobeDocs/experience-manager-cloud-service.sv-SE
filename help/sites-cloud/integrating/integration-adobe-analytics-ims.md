---
title: IMS-konfiguration som ska användas vid integrering med Adobe Analytics
description: Läs mer om IMS-konfiguration för användning vid integrering med Adobe Analytics
source-git-commit: 7686329de2ef621f69899e07efa9af16e50a35f9
workflow-type: tm+mt
source-wordcount: '925'
ht-degree: 1%

---

# IMS-konfiguration som ska användas vid integrering med Adobe Analytics {#ims-configuration-for-integration-with-adobe-analytics}

Integrationen av Adobe Experience Manager as a Cloud Service (AEMaaCS) med Adobe Analytics via API:t för Analytics Standard kräver att du konfigurerar Adobe IMS (Identity Management System). Konfigurationen görs med Adobe Developer Console.

>[!NOTE]
> 
>Den här funktionen är tillgänglig i prerelease-kanalen.
>
>Se [Dokumentation för prerelease Channel](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html#enable-prerelease) om du vill ha information om hur du aktiverar funktionen för din miljö.

>[!NOTE]
>
>Stöd för Adobe Analytics Standard API 2.0 är nytt i AEMaaCS 202.2.0. Den här versionen av API:t stöder IMS-autentisering.
>
>API-valet styrs av den autentiseringsmetod som används för AEM-/Analytics-integrering.
>
>Ytterligare information finns också tillgänglig under [Migrera till 2.0 API:er](https://developer.adobe.com/analytics-apis/docs/2.0/guides/migration/).

## Förutsättningar {#prerequisites}

Innan du börjar med den här proceduren:

* [Stöd för Adobe](https://helpx.adobe.com/se/contact/enterprise-support.ec.html) måste tillhandahålla ditt konto för:

   * Adobe Console
   * Adobe Developer Console
   * Adobe Analytics och
   * Adobe IMS (Identity Management System)

* Din organisations systemadministratör bör använda Admin Console för att lägga till de utvecklare som behövs i organisationen till de relevanta produktprofilerna.

   * Detta ger specifika utvecklare behörighet att aktivera integreringar med Adobe Developer Console.
   * Mer information finns i [Hantera utvecklare](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/manage-developers.ug.html).


## Konfigurera en IMS-konfiguration - Generera en offentlig nyckel {#configuring-ims-generating-a-public-key}

Det första steget i konfigurationen är att skapa en IMS-konfiguration i AEM och generera den offentliga nyckeln.

1. Öppna AEM **verktyg** -menyn.
1. I **Säkerhet** avsnittsmarkera **Adobe IMS-konfigurationer**.
1. Välj **Skapa** för att öppna **Adobe IMS Technical Account Configuration**.
1. Använda listrutan under **Molnkonfiguration**, markera **Adobe Analytics**.
1. Aktivera **Skapa nytt certifikat** och ange ett nytt alias.
1. Bekräfta med **Skapa certifikat**.

   ![Skapa ett certifikat](assets/integrate-analytics-ims-01.png)

1. Välj **Hämta** (eller **Hämta offentlig nyckel**) för att hämta filen till den lokala hårddisken, så att den är klar att användas när [konfigurera IMS för Adobe Analytics-integrering med AEM](#configuring-ims-adobe-analytics-integration-with-aem).

   >[!CAUTION]
   >
   >Låt konfigurationen vara öppen, den behövs igen när [Slutför IMS-konfigurationen i AEM](#completing-the-ims-configuration-in-aem).

   ![Hämta certifikatet](assets/integrate-analytics-ims-02.png)

## Konfigurera IMS för Adobe Analytics-integrering med AEM {#configuring-ims-adobe-analytics-integration-with-aem}

Med Adobe Developer Console måste du skapa ett projekt (integration) med Adobe Analytics (för AEM) och sedan tilldela de behörigheter som krävs.

### Skapa projektet {#creating-the-project}

Öppna Adobe Developer Console för att skapa ett projekt med Adobe Analytics som AEM ska använda:

1. Öppna Adobe Developer Console for Projects:

   [https://developer.adobe.com/console/projects](https://developer.adobe.com/console/projects)

1. Alla projekt du har visas. Välj **Skapa nytt projekt** - platsen och användningen beror på:

   * Om du inte har något projekt än **Skapa nytt projekt** kommer att vara i mitten, nederst.
      ![Skapa nytt projekt - första projektet](assets/integration-analytics-ims-02.png)
   * Om du redan har befintliga projekt listas dessa och **Skapa nytt projekt** kommer att vara överst till höger.
      ![Skapa nytt projekt - flera projekt](assets/integration-analytics-ims-03.png)


1. Välj **Lägg till i projekt** följt av **API**:

   ![Kom igång med ditt nya projekt](assets/integration-analytics-ims-10.png)

1. Välj **Adobe Analytics** sedan **Nästa**:

   >[!NOTE]
   >
   >Om du prenumererar på Adobe Analytics, men inte ser det i listan, bör du kontrollera [Förutsättningar](#prerequisites).

   ![Lägg till ett API](assets/integration-analytics-ims-12.png)

1. Välj **Tjänstkonto (JWT)** som typ av autentisering fortsätter du med **Nästa**:

   ![Välj typ av autentisering](assets/integration-analytics-ims-12a.png)

1. **Överför din offentliga nyckel** och när det är klart fortsätter du med **Nästa**:

   ![Överför din offentliga nyckel](assets/integration-analytics-ims-13.png)

1. Granska inloggningsuppgifterna och fortsätt med **Nästa**:

   ![Granska autentiseringsuppgifter](assets/integration-analytics-ims-15.png)

1. Välj önskade produktprofiler och fortsätt med **Spara konfigurerat API**:

   ![Välj önskade produktprofiler](assets/integration-analytics-ims-16.png)

1. Konfigurationen kommer att bekräftas.

### Tilldela behörigheter till integreringen {#assigning-privileges-to-the-integration}

Du måste nu tilldela nödvändig behörighet till integreringen:

1. Öppna Adobe **Admin Console**:

   * [https://adminconsole.adobe.com](https://adminconsole.adobe.com/)

1. Navigera till **Produkter** (övre verktygsfältet) och sedan välja **Adobe Analytics - &lt;*din-tenant-id*>** (från den vänstra panelen).
1. Välj **Produktprofiler** och sedan den arbetsyta du behöver i den lista som visas. Exempel: Standardarbetsyta.
1. Välj **API-autentiseringsuppgifter** och sedan den integreringskonfiguration som krävs.
1. Välj **Redigerare** som **Produktroll**; i stället för **Observer**.

## Information lagrad för integreringsprojektet i Adobe Developer Console {#details-stored-for-the-ims-integration-project}

På Adobe Developer Console - Projekt kan du se en lista över alla dina integrationsprojekt:

* [https://developer.adobe.com/console/projects](https://developer.adobe.com/console/projects)

Välj en specifik projektpost om du vill visa mer information om konfigurationen. Bland dessa finns:

* Projektöversikt
* Insikter
* Autentiseringsuppgifter
   * Tjänstkonto (JWT)
      * Information om autentiseringsuppgifter
      * Generera JWT
* APIS
   * Exempel: Adobe Analytics

Vissa av dessa behöver du för att slutföra integreringen av Adobe Analytics i AEM baserat på IMS.

## Slutför IMS-konfigurationen i AEM {#completing-the-ims-configuration-in-aem}

Om du går tillbaka till AEM kan du slutföra IMS-konfigurationen genom att lägga till obligatoriska värden från IMS-integreringen för Analytics:

1. Återgå till [IMS-konfiguration öppnas i AEM](#configuring-ims-generating-a-public-key).
1. Välj **Nästa**.

1. Här kan du använda [information från projektkonfigurationen i Adobe Developer Console](#details-stored-for-the-ims-integration-project):

   * **Titel**: Din text.
   * **Auktoriseringsserver**: Kopiera/klistra in detta från `aud` rad i **Nyttolast** avsnitt nedan, t.ex. `https://ims-na1.adobelogin.com` i exemplet nedan
   * **API-nyckel**: Kopiera detta från **Autentiseringsuppgifter** i [Projektöversikt](#details-stored-for-the-ims-integration-project)
   * **Klienthemlighet**: Generera detta i [Fliken Klienthemlighet i avsnittet Tjänstkonto (JWT)](#details-stored-for-the-ims-integration-project)och kopiera
   * **Nyttolast**: Kopiera detta från [Generera JWT-flik i avsnittet Tjänstkonto (JWT)](#details-stored-for-the-ims-integration-project)

   ![Information om AEM IMS-konfiguration](assets/integrate-analytics-ims-10.png)

1. Bekräfta med **Skapa**.

1. Din Adobe Analytics-konfiguration visas i AEM.

   ![IMS-konfiguration](assets/integrate-analytics-ims-11.png)

## Bekräfta IMS-konfigurationen {#confirming-the-ims-configuration}

Så här bekräftar du att konfigurationen fungerar som förväntat:

1. Öppna:

   * `https://localhost<port>/libs/cq/adobeims-configuration/content/configurations.html`

   Till exempel:

   * `https://localhost:4502/libs/cq/adobeims-configuration/content/configurations.html`


1. Välj din konfiguration.
1. Välj **Kontrollera hälsa** i verktygsfältet, följt av **Kontrollera**.

   ![IMS-konfiguration - kontrollera hälsa](assets/integrate-analytics-ims-12.png)

1. Om du lyckas visas ett bekräftelsemeddelande.

## Slutför integrationen med Adobe Analytics {#complete-the-integration-with-adobe-analytics}

Nu kan du använda den här IMS-konfigurationen för att slutföra [integrering med Adobe Analytics](/help/sites-cloud/integrating/integrating-adobe-analytics.md).

<!--
## Configuring the Adobe Analytics Cloud Service {#configuring-the-adobe-analytics-cloud-service}

The configuration can now be referenced for a Cloud Service to use the Analytics Standard API:

1. Open the **Tools** menu. Then, within the **Cloud Services** section, select **Legacy Cloud Services**.
1. Scroll down to **Adobe Analytics** and select **Configure now**.

   The **Create Configuration** dialog will open.

1. Enter a **Title** and, if you want, a **Name** (if left blank this will be generated from the title).

   You can also select the required template (if more than one is available).

1. Confirm with **Create**.

   The **Edit Component** dialog will open.

1. Enter the details in the **Analytics Settings** tab:

    * **Authentication**: IMS

    * **IMS Configuration**: select the name of the IMS Configuration

1. Click **Connect to Analytics** to initialize the connection with Adobe Analytics.

   If the connection is successful, the message **Connection successful** is displayed.

1. Select **OK** on the message.

1. Complete other parameters as required, followed by **OK** on the dialog to confirm the configuration.

1. You can now proceed to [Adding an Analytics Framework](/help/sites-administering/adobeanalytics-connect.md) to configure parameters that will be sent to Adobe Analytics. 
-->

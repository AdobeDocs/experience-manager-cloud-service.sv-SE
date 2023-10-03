---
title: Hur konfigurerar jag datakällor?
description: Lär dig konfigurera RESTful-webbtjänster, SOAP-baserade webbtjänster och OData-tjänster som datakällor för en formulärdatamodell.
feature: Form Data Model
role: User, Developer
level: Beginner
exl-id: cb77a840-d705-4406-a94d-c85a6efc8f5d
source-git-commit: 7e3eb3426002408a90e08bee9c2a8b7a7bfebb61
workflow-type: tm+mt
source-wordcount: '2022'
ht-degree: 0%

---

# Konfigurera datakällor {#configure-data-sources}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/configure-data-sources.html) |
| AEM as a Cloud Service | Den här artikeln |

![Dataintegrering](do-not-localize/data-integeration.png)

[!DNL Experience Manager Forms] Med dataintegrering kan du konfigurera och ansluta till olika datakällor. Följande typer stöds:

* Relationsdatabaser - MySQL, [!DNL Microsoft SQL Server], [!DNL IBM DB2]och [!DNL Oracle RDBMS]
* RESTful web services
* SOAP-baserade webbtjänster
* OData-tjänster (version 4.0)
* Microsoft® Dynamics
* SalesForce
* Microsoft® Azure Blob Storage

Dataintegrering stöder OAuth2.0([Auktoriseringskod](https://oauth.net/2/grant-types/authorization-code/), [Klientautentiseringsuppgifter](https://oauth.net/2/grant-types/client-credentials/)), grundläggande autentisering och API-nyckelautentiseringstyper är körklara och tillåter implementering av anpassad autentisering för åtkomst till webbtjänster. SOAP-baserade tjänster och OData-tjänster är konfigurerade i RESTful [!DNL Experience Manager] as a Cloud Service, JDBC för relationsdatabaser och anslutningsprogram för [!DNL Experience Manager] användarprofilen är konfigurerad i [!DNL Experience Manager] webbkonsol.

## Konfigurera relationsdatabas {#configure-relational-database}

### Förutsättningar

Innan du konfigurerar relationsdatabaser med [!DNL Experience Manager] Konfiguration av webbkonsol, det är obligatoriskt att:
* [Aktivera avancerat nätverk via molnhanterings-API](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/networking/advanced-networking.html), eftersom portar är inaktiverade som standard.
* [Lägg till JDBC-drivrutinsberoenden i Maven](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/networking/examples/sql-datasourcepool.html?lang=en#mysql-driver-dependencies).


### Steg för att konfigurera relationsdatabas

Du kan konfigurera relationsdatabaser med [!DNL Experience Manager] Konfiguration av webbkonsol. Gör följande:

1. Gå till [!DNL Experience Manager] webbkonsol på `https://server:host/system/console/configMgr`.
1. Sök **[!UICONTROL Day Commons JDBC Connections Pools]** konfiguration. Tryck för att öppna konfigurationen i redigeringsläge.

   ![JDBC Connector Pool](/help/forms/assets/jdbc_connector.png)

1. I konfigurationsdialogrutan anger du information för den databas som du vill konfigurera, till exempel:

   * Java™-klassnamn för JDBC-drivrutinen
   * URI för JDBC-anslutning
   * Användarnamn och lösenord för anslutning till JDBC-drivrutinen
   * Ange en SQL SELECT-fråga i **[!UICONTROL Validation Query]** fält för att validera anslutningar från poolen. Frågan måste returnera minst en rad. Baserat på din databas anger du något av följande:
      * SELECT 1 (MySQL och MS SQL)
      * VÄLJ 1 från dubbla (Oracle)
   * Datakällans namn

   Exempelsträngar för konfigurering av relationsdatabas:

   ```text
      "datasource.name": "sqldatasourcename-mysql",
      "jdbc.driver.class": "com.mysql.jdbc.Driver",
      "jdbc.connection.uri": "jdbc:mysql://$[env:AEM_PROXY_HOST;default=proxy.tunnel]:30001/sqldatasourcename"
   ```

   >[!NOTE]
   >
   > Se [SQL-anslutningar med JDBC DataSourcePool](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/networking/examples/sql-datasourcepool.html) för mer detaljerad information.

1. Tryck **[!UICONTROL Save]** för att spara konfigurationen.

Nu kan du använda den konfigurerade relationsdatabasen med din formulärdatamodell.

<!-- ## Configure [!DNL Experience Manager] user profile {#configure-aem-user-profile}

You can configure [!DNL Experience Manager] user profile using User Profile Connector configuration in [!DNL Experience Manager] Web Console. Do the following:

1. Go to [!DNL Experience Manager] web console at `https://[server]:[port]/system/console/configMgr`.
1. Look for **[!UICONTROL AEM Forms Data Integrations - User Profile Connector Configuration]** and tap to open the configuration in edit mode.
1. In the User Profile Connector Configuration dialog, you can add, remove, or update user profile properties. The specified properties are available for use in form data model. Use the following format to specify user profile properties:

   `name=[property_name_with_location_in_user_profile],type=[property_type]`

   Examples:

    * `name=profile/phoneNumber,type=string`
    * `name=profile/empLocation/*/city,type=string`

   >[!NOTE]
   >
   >The **&#42;** in the above example denotes all nodes under the `profile/empLocation/` node in [!DNL Experience Manager] user profile in CRXDE structure. It means that the Form Data Model can access the `city` property of type `string` present in any node under the `profile/empLocation/` node. However, the nodes that contain the specified property must follow a consistent structure.

1. Tap **[!UICONTROL Save]** to save the configuration. -->

## Konfigurera mapp för molntjänstkonfigurationer {#cloud-folder}

Konfiguration för molntjänstmappen krävs för konfigurering av molntjänster för RESTful-, SOAP- och OData-tjänster.

Alla molntjänstkonfigurationer i [!DNL Experience Manager] konsolideras i `/conf` mapp i [!DNL Experience Manager] databas. Som standard är `conf` mappen innehåller `global` mapp där du kan skapa molntjänstkonfigurationer. Du måste dock manuellt aktivera det för molnkonfigurationer. Du kan även skapa ytterligare mappar i `conf` för att skapa och organisera molntjänstkonfigurationer.

Så här konfigurerar du mappen för molntjänstkonfigurationer:

1. Gå till **[!UICONTROL Tools > General > Configuration Browser]**.
   * Se [Konfigurationsläsaren](https://experienceleague.adobe.com/docs/experience-manager-65/administering/introduction/configurations.html) mer information.
1. Gör följande för att aktivera den globala mappen för molnkonfigurationer eller hoppa över det här steget för att skapa och konfigurera en annan mapp för molntjänstkonfigurationer.

   1. I **[!UICONTROL Configuration Browser]** väljer du `global` mapp och tryck **[!UICONTROL Properties]**.

   1. I **[!UICONTROL Configuration Properties]** dialogruta, aktivera **[!UICONTROL Cloud Configurations]**.

   1. Tryck **[!UICONTROL Save & Close]** för att spara konfigurationen och stänga dialogrutan.

1. I **[!UICONTROL Configuration Browser]**, trycka **[!UICONTROL Create]**.
1. I **[!UICONTROL Create Configuration]** anger du en rubrik för mappen och aktiverar **[!UICONTROL Cloud Configurations]**.
1. Tryck **[!UICONTROL Create]** för att skapa en mapp som är aktiverad för molntjänstkonfigurationer.

## Konfigurera RESTful-webbtjänster {#configure-restful-web-services}

RESTful-webbtjänsten kan beskrivas med [Swagger-specifikationer](https://swagger.io/specification/v2/) i JSON- eller YAML-format i [!DNL Swagger] definitionsfil. Konfigurera RESTful-webbtjänsten i [!DNL Experience Manager] as a Cloud Service, se till att du har antingen [!DNL Swagger] fil ([Swagger version 2.0](https://swagger.io/specification/v2/)) eller [!DNL Swagger] fil ([Swagger version 3.0](https://swagger.io/specification/v3/)) i filsystemet eller den URL där filen finns.

### Konfigurera RESTful-tjänster för Open API Specification version 2.0 {#configure-restful-services-open-api-2.0}

1. Gå till **[!UICONTROL Tools > Cloud Services > Data Sources]**. Tryck för att välja den mapp där du vill skapa en molnkonfiguration.

   Se [Konfigurera mapp för molntjänstkonfigurationer](configure-data-sources.md#cloud-folder) för information om hur du skapar och konfigurerar en mapp för molntjänstkonfigurationer.

1. Tryck **[!UICONTROL Create]** för att öppna **[!UICONTROL Create Data Source Configuration wizard]**. Ange ett namn och eventuellt en rubrik för konfigurationen, välj **[!UICONTROL RESTful Service]** från **[!UICONTROL Service Type]** nedrullningsbar meny, där du kan bläddra och välja en miniatyrbild för konfigurationen, och trycka på **[!UICONTROL Next]**.
1. Ange följande information för RESTful-tjänsten:

   * Välj URL eller fil på menyn [!UICONTROL Swagger Source] och ange [!DNL Swagger URL] till[!DNL  Swagger] definitionsfil eller ladda upp [!DNL Swagger] från det lokala filsystemet.
   * Baserat på[!DNL  Swagger] Källindata., följande fält är förifyllda med värden:

      * Schema: De överföringsprotokoll som används av REST API. Antalet schematyper som visas i listrutan beror på scheman som definieras i [!DNL Swagger] källa.
      * Värd: Domännamnet eller IP-adressen för värden som använder REST API. Det är ett obligatoriskt fält.
      * Bassökväg: URL-prefixet för alla API-sökvägar. Det är ett valfritt fält.\
        Om det behövs kan du redigera de förifyllda värdena för dessa fält.

   * Välj autentiseringstyp - Ingen, OAuth2.0([Auktoriseringskod](https://oauth.net/2/grant-types/authorization-code/), [Klientautentiseringsuppgifter](https://oauth.net/2/grant-types/client-credentials/)), Basic Authentication, API Key eller Custom Authentication - för att få åtkomst till RESTful-tjänsten och ange därmed information för autentisering.

   Om du väljer **[!UICONTROL API Key]** Ange värdet för API-nyckeln som autentiseringstyp. API-nyckeln kan skickas som en begäranderubrik eller som en frågeparameter. Välj ett av dessa alternativ på menyn **[!UICONTROL Location]** nedrullningsbar lista och ange namnet på huvudet eller frågeparametern i **[!UICONTROL Parameter Name]** efter behov.

   <!--If you select **[!UICONTROL Mutual Authentication]** as the authentication type, see [Certificate-based mutual authentication for RESTful and SOAP web services](#mutual-authentication).-->

1. Tryck **[!UICONTROL Create]** för att skapa molnkonfigurationen för RESTful-tjänsten.

### Konfigurera RESTful-tjänster för Open API Specification version 3.0 {#configure-restful-services-open-api-3.0}

1. Gå till **[!UICONTROL Tools > Cloud Services > Data Sources]**. Tryck för att välja den mapp där du vill skapa en molnkonfiguration.

   Se [Konfigurera mapp för molntjänstkonfigurationer](configure-data-sources.md#cloud-folder) för information om hur du skapar och konfigurerar en mapp för molntjänstkonfigurationer.

1. Tryck **[!UICONTROL Create]** för att öppna **[!UICONTROL Create Data Source Configuration wizard]**. Ange ett namn och eventuellt en rubrik för konfigurationen, välj **[!UICONTROL RESTful Service]** från **[!UICONTROL Service Type]** nedrullningsbar meny, där du kan bläddra och välja en miniatyrbild för konfigurationen, och trycka på **[!UICONTROL Next]**.
1. Ange följande information för RESTful-tjänsten:

   * Välj URL eller fil på menyn [!UICONTROL Swagger Source] och ange [!DNL Swagger 3.0 URL] till[!DNL  Swagger] definitionsfil eller ladda upp [!DNL Swagger] från det lokala filsystemet.
   * Baserat på[!DNL  Swagger] Källindata, anslutningsinformationen med målservern visas.
   * Välj autentiseringstyp - Ingen, OAuth2.0([Auktoriseringskod](https://oauth.net/2/grant-types/authorization-code/), [Klientautentiseringsuppgifter](https://oauth.net/2/grant-types/client-credentials/)), Basic Authentication, API Key eller Custom Authentication - för att få åtkomst till RESTful-tjänsten och ange därmed information för autentisering.

   Om du väljer **[!UICONTROL API Key]** Ange värdet för API-nyckeln som autentiseringstyp. API-nyckeln kan skickas som en begäranderubrik eller som en frågeparameter. Välj ett av dessa alternativ på menyn **[!UICONTROL Location]** nedrullningsbar lista och ange namnet på huvudet eller frågeparametern i **[!UICONTROL Parameter Name]** efter behov.

   <!--If you select **[!UICONTROL Mutual Authentication]** as the authentication type, see [Certificate-based mutual authentication for RESTful and SOAP web services](#mutual-authentication).-->

1. Tryck **[!UICONTROL Create]** för att skapa molnkonfigurationen för RESTful-tjänsten.

En del åtgärder som inte stöds av RESTful services Open API Specification version 3.0 är:
* Återanrop
* en/något av
* Fjärrreferens
* Länkar
* Olika begärande organ för olika MIME-typer för en enda operation

Se [OpenAPI 3.0-specifikation](https://swagger.io/specification/v3/) för detaljerad information.

### HTTP-klientkonfiguration för formulärdatamodell för optimering av prestanda {#fdm-http-client-configuration}

[!DNL Experience Manager Forms] formulärdatamodell vid integrering med RESTful-webbtjänster som datakälla inkluderar HTTP-klientkonfigurationer för prestandaoptimering.

Ange följande egenskaper för **[!UICONTROL Form Data Model HTTP Client Configuration for REST data source]** konfiguration som anger det reguljära uttrycket:

* Använd `http.connection.max.per.route` -egenskap för att ange maximalt antal tillåtna anslutningar mellan formulärdatamodell och RESTful-webbtjänster. Standardvärdet är 20 anslutningar.

* Använd `http.connection.max` egenskapen för att ange maximalt antal tillåtna anslutningar för varje flöde. Standardvärdet är 40 anslutningar.

* Använd `http.connection.keep.alive.duration` egenskapen för att ange varaktigheten för vilken en beständig HTTP-anslutning hålls vid liv. Standardvärdet är 15 sekunder.

* Använd `http.connection.timeout` egenskapen för att ange varaktigheten, för vilken [!DNL Experience Manager Forms] servern väntar på att en anslutning ska upprättas. Standardvärdet är 10 sekunder.

* Använd `http.socket.timeout` för att ange den maximala tidsperioden för inaktivitet mellan två datapaket. Standardvärdet är 30 sekunder.

I följande JSON-fil visas ett exempel:


```json
{   
   "http.connection.keep.alive.duration":"15",   
   "http.connection.max.per.route":"20",   
   "http.connection.timeout":"10",   
   "http.socket.timeout":"30",   
   "http.connection.idle.connection.timeout":"15",   
   "http.connection.max":"40" 
} 
```

1. Tryck på **[!UICONTROL Form Data Model HTTP Client Configuration for REST data source]**.

1. I [!UICONTROL Form Data Model HTTP Client Configuration for REST data source] dialog:

   * Ange maximalt antal tillåtna anslutningar mellan formulärdatamodellen och RESTful-webbtjänster i dialogrutan **[!UICONTROL Connection limit in total]** fält. Standardvärdet är 20 anslutningar.

   * Ange maximalt antal tillåtna anslutningar för varje flöde i dialogrutan **[!UICONTROL Connection limit on per route basis]** fält. Standardvärdet är två anslutningar.

   * Ange hur länge en beständig HTTP-anslutning ska vara aktiv i **[!UICONTROL Keep alive]** fält. Standardvärdet är 15 sekunder.

   * Ange varaktigheten som [!DNL Experience Manager Forms] servern väntar på att en anslutning ska upprättas i **[!UICONTROL Connection timeout]** fält. Standardvärdet är 10 sekunder.

   * Ange den maximala tidsperioden för inaktivitet mellan två datapaket i **[!UICONTROL Socket timeout]** fält. Standardvärdet är 30 sekunder.

## Konfigurera SOAP-webbtjänster {#configure-soap-web-services}

SOAP-baserade webbtjänster beskrivs med [WSDL-specifikationer (Web Services Description Language)](https://www.w3.org/TR/wsdl). [!DNL Experience Manager Forms] saknar stöd för WSDL-modellen i RPC-format.

Konfigurera SOAP-baserad webbtjänst i [!DNL Experience Manager] as a Cloud Service, kontrollera att du har WSDL-URL:en för webbtjänsten och gör följande:

1. Gå till **[!UICONTROL Tools > Cloud Services > Data Sources]**. Tryck för att välja den mapp där du vill skapa en molnkonfiguration.

   Se [Konfigurera mapp för molntjänstkonfigurationer](configure-data-sources.md#cloud-folder) för information om hur du skapar och konfigurerar en mapp för molntjänstkonfigurationer.

1. Tryck **[!UICONTROL Create]** för att öppna **[!UICONTROL Create Data Source Configuration wizard]**. Ange ett namn och eventuellt en rubrik för konfigurationen, välj **[!UICONTROL SOAP Web Service]** från **[!UICONTROL Service Type]** nedrullningsbar meny, där du kan bläddra och välja en miniatyrbild för konfigurationen, och trycka på **[!UICONTROL Next]**.
1. Ange följande för SOAP-webbtjänsten:

   * WSDL-URL för webbtjänsten.
   * Tjänstslutpunkt. Ange ett värde i det här fältet om du vill åsidosätta tjänstslutpunkten som anges i WSDL.
   * Välj autentiseringstyp - Ingen, OAuth2.0([Auktoriseringskod](https://oauth.net/2/grant-types/authorization-code/), [Klientautentiseringsuppgifter](https://oauth.net/2/grant-types/client-credentials/)), Basic Authentication eller Custom Authentication - för att få åtkomst till SOAP-tjänsten och därmed ange information för autentisering.

     <!--If you select **[!UICONTROL X509 Token]** as the Authentication type, configure the X509 certificate. For more information, see [Set up certificates](install-configure-document-services.md#set-up-certificates-for-reader-extension-and-encryption-service).-->
     <!--Specify the KeyStore alias for the X509 certificate in the **[!UICONTROL Key Alias]** field. Specify the time, in seconds, until the authentication request remains valid, in the **[!UICONTROL Time To Live]** field. Optionally, select to sign the message body or timestamp header or both.-->

     <!--If you select **[!UICONTROL Mutual Authentication]** as the authentication type, see [Certificate-based mutual authentication for RESTful and SOAP web services](#mutual-authentication).-->

1. Tryck **[!UICONTROL Create]** för att skapa molnkonfigurationen för SOAP-webbtjänsten.

### Aktivera användning av importsatser i SOAP-webbtjänster WSDL {#enable-import-statements}

Du kan ange ett reguljärt uttryck som fungerar som filter för absoluta URL:er som tillåts som importsatser i SWDL för SOAP-webbtjänster. Som standard finns det inget värde i det här fältet. Detta resulterar i [!DNL Experience Manager] blockerar alla importsatser som är tillgängliga i WSDL. Om du anger `.*` som värdet i detta fält, [!DNL Experience Manager] tillåter alla importsatser.

Ange `importAllowlistPattern` egenskapen för **[!UICONTROL Form Data Model SOAP Web Services Import Allowlist]** -konfiguration för att ange det reguljära uttrycket. I följande JSON-fil visas ett exempel:


```json
{
  "importAllowlistPattern": ".*"
}
```


Så här anger du värden för en konfiguration: [Generera OSGi-konfigurationer med AEM SDK](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#generating-osgi-configurations-using-the-aem-sdk-quickstart)och [distribuera konfigurationen](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#deployment-process) till din Cloud Service.

## Konfigurera OData-tjänster {#config-odata}

En OData-tjänst identifieras av tjänstens rot-URL. Konfigurera en OData-tjänst i [!DNL Experience Manager] as a Cloud Service, kontrollera att du har tjänstens rot-URL och gör följande:

>[!NOTE]
>
> Formulärdatamodellen stöder [OData version 4](https://www.odata.org/documentation/).
>Stegvisa anvisningar för konfiguration [!DNL Microsoft® Dynamics 365], online eller lokalt, se [[!DNL Microsoft® Dynamics] OData-konfiguration](ms-dynamics-odata-configuration.md).

1. Gå till **[!UICONTROL Tools > Cloud Services > Data Sources]**. Tryck för att välja den mapp där du vill skapa en molnkonfiguration.

   Se [Konfigurera mapp för molntjänstkonfigurationer](#cloud-folder) för information om hur du skapar och konfigurerar en mapp för molntjänstkonfigurationer.

1. Tryck **[!UICONTROL Create]** för att öppna **[!UICONTROL Create Data Source Configuration wizard]**. Ange ett namn och eventuellt en rubrik för konfigurationen, välj **[!UICONTROL OData Service]** från **[!UICONTROL Service Type]** nedrullningsbar meny, där du kan bläddra och välja en miniatyrbild för konfigurationen, och trycka på **[!UICONTROL Next]**.
1. Ange följande information för OData-tjänsten:

   * Tjänstens rot-URL för OData-tjänsten som ska konfigureras.
   * Välj autentiseringstyp - Ingen, OAuth2.0([Auktoriseringskod](https://oauth.net/2/grant-types/authorization-code/), [Klientautentiseringsuppgifter](https://oauth.net/2/grant-types/client-credentials/)), Basic Authentication, API Key eller Custom Authentication - för att få åtkomst till OData-tjänsten och därmed ange autentiseringsinformationen.

   Om du väljer **[!UICONTROL API Key]** Ange värdet för API-nyckeln som autentiseringstyp. API-nyckeln kan skickas som en begäranderubrik eller som en frågeparameter. Välj ett av dessa alternativ på menyn **[!UICONTROL Location]** nedrullningsbar lista och ange namnet på huvudet eller frågeparametern i **[!UICONTROL Parameter Name]** efter behov.

   >[!NOTE]
   >
   Du måste välja autentiseringstypen OAuth 2.0 för att kunna ansluta med [!DNL Microsoft® Dynamics] tjänster där OData-slutpunkten används som tjänstrot.

1. Tryck **[!UICONTROL Create]** för att skapa molnkonfigurationen för OData-tjänsten.

<!--## Certificate-based mutual authentication for RESTful and SOAP web services {#mutual-authentication}

When you enable mutual authentication for form data model, both the data source and [!DNL Experience Manager] Server running Form Data Model authenticate each other's identity before sharing any data. You can use mutual authentication for REST and SOAP-based connections (data sources). To configure mutual authentication for a Form Data Model on your [!DNL Experience Manager Forms] environment:

1. Upload the private key (certificate) to [!DNL Experience Manager Forms] server. To upload the private key:
   1. Log in to your [!DNL Experience Manager Forms] server as an administrator.
   1. Navigate to **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Users]**. Select the `fd-cloudservice` user and tap **[!UICONTROL Properties]**.
   1. Open the **[!UICONTROL Keystore]** tab, expand the **[!UICONTROL Add Private Key from KeyStore file]** option, upload the KeyStore File, specify the aliases, passwords, and tap **[!UICONTROL Submit]**. The Certificate is uploaded.  The private key alias is mentioned in the certificate and set while creating the certificate.
1. Upload trust certificate to Global Trust Store. To upload the certificate:
   1. Navigate to **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Trust Store]**.
   1. Expand the **[!UICONTROL Add Certificate from CER file]** option, tap **[!UICONTROL Select Certificate File]**, upload the certificate, and tap **[!UICONTROL Submit]**.
1. Configure [SOAP](#configure-soap-web-services) or [RESTful](#configure-restful-web-services) web services as the data source and select **[!UICONTROL Mutual authentication]** as the authentication type. If you configure multiple self-signed certificates for `fd-cloudservice` user, specify the Key Alias name for the certificate.-->

## Nästa steg {#next-steps}

Du har konfigurerat datakällorna. Därefter kan du skapa en formulärdatamodell eller, om du redan har skapat en formulärdatamodell utan en datakälla, associera den med de datakällor du konfigurerade. Se [Skapa formulärdatamodell](create-form-data-models.md) för mer information.

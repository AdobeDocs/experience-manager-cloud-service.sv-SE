---
title: Hur konfigurerar jag datakällor?
description: Lär dig konfigurera RESTful-webbtjänster, SOAP-baserade webbtjänster och OData-tjänster som datakällor för en formulärdatamodell (FDM).
feature: Adaptive Forms, Form Data Model
role: User, Developer
level: Beginner
exl-id: cb77a840-d705-4406-a94d-c85a6efc8f5d
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '2144'
ht-degree: 0%

---


# Konfigurera datakällor {#configure-data-sources}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/configure-data-sources.html?lang=sv-SE) |
| AEM as a Cloud Service | Den här artikeln |

![Dataintegrering](do-not-localize/data-integeration.png)

Med dataintegrering i [!DNL Experience Manager Forms] kan du konfigurera och ansluta till olika datakällor. Följande typer stöds:

* Relationsdatabaser - MySQL, [!DNL Microsoft® SQL Server], [!DNL IBM® DB2®], postgreSQL och [!DNL Oracle RDBMS]
* RESTful web services
* SOAP-baserade webbtjänster
* OData-tjänster (version 4.0)
* Microsoft® Dynamics
* Salesforce
* Microsoft® Azure Blob Storage

Dataintegrering har stöd för autentiseringstyperna OAuth2.0([Auktoriseringskod](https://oauth.net/2/grant-types/authorization-code/), [Klientautentiseringsuppgifter](https://oauth.net/2/grant-types/client-credentials/)), Grundläggande autentisering och API-nyckelautentisering som är körklara och tillåter implementering av anpassad autentisering för åtkomst till webbtjänster. Medan RESTful, SOAP-baserade tjänster och OData-tjänster konfigureras i [!DNL Experience Manager] as a Cloud Service, konfigureras JDBC för relationsdatabaser och koppling för användarprofilen [!DNL Experience Manager] i webbkonsolen [!DNL Experience Manager].

## Konfigurera relationsdatabas {#configure-relational-database}

### Förutsättningar

Innan du konfigurerar relationsdatabaser med hjälp av webbkonsolkonfigurationen i [!DNL Experience Manager] måste du:

* [Aktivera avancerade nätverk via molnhanterings-API:t](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/networking/advanced-networking.html?lang=sv-SE) eftersom portar är inaktiverade som standard.
* [Lägg till JDBC-drivrutinsberoenden i Maven](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/networking/examples/sql-datasourcepool.html?lang=sv-SE#mysql-driver-dependencies).


### Steg för att konfigurera en relationsdatabas

Du kan konfigurera relationsdatabaser med hjälp av webbkonsolkonfigurationen för [!DNL Experience Manager]. Gör följande:

1. Gå till webbkonsolen [!DNL Experience Manager] på `https://server:host/system/console/configMgr`.
1. Leta reda på konfigurationen för **[!UICONTROL Day Commons JDBC Connections Pools]**. Välj det här alternativet om du vill öppna konfigurationen i redigeringsläge.

   ![JDBC-kopplingspool](/help/forms/assets/jdbc_connector.png)

1. I konfigurationsdialogrutan anger du information för den databas som du vill konfigurera, till exempel:

   * Java™-klassnamn för JDBC-drivrutinen
   * URI för JDBC-anslutning
   * Användarnamn och lösenord för anslutning till JDBC-drivrutinen
   * Ange en SELECT-fråga (SQL) i fältet **[!UICONTROL Validation Query]** om du vill validera anslutningar från poolen. Frågan måste returnera minst en rad. Baserat på din databas anger du något av följande:
      * SELECT 1 (MySQL och MS® SQL)
      * SELECT 1 from dual (Oracle)
   * Datakällans namn

   Exempelsträngar för att konfigurera en relationsdatabas:

   ```text
      "datasource.name": "sqldatasourcename-mysql",
      "jdbc.driver.class": "com.mysql.jdbc.Driver",
      "jdbc.connection.uri": "jdbc:mysql://$[env:AEM_PROXY_HOST;default=proxy.tunnel]:30001/sqldatasourcename"
   ```

   >[!NOTE]
   >
   > Mer information finns i [SQL-anslutningar med JDBC DataSourcePool](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/networking/examples/sql-datasourcepool.html?lang=sv-SE).

1. Välj **[!UICONTROL Save]** om du vill spara konfigurationen.

Nu kan du använda den konfigurerade relationsdatabasen med din formulärdatamodell (FDM).

<!-- ## Configure [!DNL Experience Manager] user profile {#configure-aem-user-profile}

You can configure [!DNL Experience Manager] user profile using User Profile Connector configuration in [!DNL Experience Manager] Web Console. Do the following:

1. Go to [!DNL Experience Manager] web console at `https://[server]:[port]/system/console/configMgr`.
1. Look for **[!UICONTROL AEM Forms Data Integrations - User Profile Connector Configuration]** and select to open the configuration in edit mode.
1. In the User Profile Connector Configuration dialog, you can add, remove, or update user profile properties. The specified properties are available for use in form data model (FDM). Use the following format to specify user profile properties:

   `name=[property_name_with_location_in_user_profile],type=[property_type]`

   Examples:

    * `name=profile/phoneNumber,type=string`
    * `name=profile/empLocation/*/city,type=string`

   >[!NOTE]
   >
   >The **&#42;** in the above example denotes all nodes under the `profile/empLocation/` node in [!DNL Experience Manager] user profile in CRXDE structure. It means that the Form Data Model (FDM) can access the `city` property of type `string` present in any node under the `profile/empLocation/` node. However, the nodes that contain the specified property must follow a consistent structure.

1. Select **[!UICONTROL Save]** to save the configuration. -->

## Konfigurera mapp för molntjänstkonfigurationer {#cloud-folder}

Konfiguration för molntjänstmappen krävs för konfigurering av molntjänster för RESTful-, SOAP- och OData-tjänster.

Alla molntjänstkonfigurationer i [!DNL Experience Manager] konsolideras i mappen `/conf` i databasen [!DNL Experience Manager]. Mappen `conf` innehåller som standard mappen `global` där du kan skapa molntjänstkonfigurationer. Du måste dock manuellt aktivera det för molnkonfigurationer. Du kan också skapa ytterligare mappar i `conf` för att skapa och organisera molntjänstkonfigurationer.

Så här konfigurerar du mappen för molntjänstkonfigurationer:

1. Gå till **[!UICONTROL Tools > General > Configuration Browser]**.
   * Mer information finns i dokumentationen för [Configuration Browser](https://experienceleague.adobe.com/docs/experience-manager-65/administering/introduction/configurations.html?lang=sv-SE).
1. Gör följande för att aktivera den globala mappen för molnkonfigurationer eller hoppa över det här steget för att skapa och konfigurera en annan mapp för molntjänstkonfigurationer.

   1. I **[!UICONTROL Configuration Browser]** markerar du mappen `global` och väljer **[!UICONTROL Properties]**.

   1. Aktivera **[!UICONTROL Configuration Properties]** i dialogrutan **[!UICONTROL Cloud Configurations]**.

   1. Välj **[!UICONTROL Save & Close]** om du vill spara konfigurationen och stänga dialogrutan.

1. I **[!UICONTROL Configuration Browser]** väljer du **[!UICONTROL Create]**.
1. Ange en rubrik för mappen i dialogrutan **[!UICONTROL Create Configuration]** och aktivera **[!UICONTROL Cloud Configurations]**.
1. Välj **[!UICONTROL Create]** om du vill skapa den mapp som är aktiverad för molntjänstkonfigurationer.

## Konfigurera RESTful-webbtjänster {#configure-restful-web-services}

RESTful-webbtjänster kan beskrivas med [Swagger-specifikationer](https://swagger.io/specification/v2/) i JSON- eller YAML-format i en [!DNL Swagger] definitionsfil eller en Service Endpoint.

>[!NOTE]
> Om du vill konfigurera RESTful-webbtjänsten i [!DNL Experience Manager] as a Cloud Service måste du ha antingen filen [!DNL Swagger] ([Swagger Version 2.0](https://swagger.io/specification/v2/)) eller filen [!DNL Swagger] ([Swagger Version 3.0](https://swagger.io/specification/v3/)) i filsystemet eller URL:en där filen finns.

### Konfigurera RESTful-tjänster för Open API Specification version 2.0 {#configure-restful-services-open-api-2.0}

1. Gå till **[!UICONTROL Tools > Cloud Services > Data Sources]**. Välj den mapp där du vill skapa en molnkonfiguration.

   Mer information om hur du skapar och konfigurerar en mapp för molntjänstkonfigurationer finns i [Konfigurera mapp för molntjänstkonfigurationer](configure-data-sources.md#cloud-folder).

1. Välj **[!UICONTROL Create]** för att öppna **[!UICONTROL Create Data Source Configuration wizard]**. Ange ett namn och eventuellt en rubrik för konfigurationen, välj **[!UICONTROL RESTful Service]** i listrutan **[!UICONTROL Service Type]**, bläddra och välj en miniatyrbild för konfigurationen och välj **[!UICONTROL Next]**.
1. Ange följande information för RESTful-tjänsten:

   * Välj en URL eller fil i listrutan [!UICONTROL Swagger Source] och ange därför [!DNL Swagger URL] till definitionsfilen [!DNL &#x200B; Swagger] eller överför filen [!DNL Swagger] från det lokala filsystemet.
   * Baserat på indata från [!DNL &#x200B; Swagger] Source är följande fält förifyllda med värden:

      * Schema: De överföringsprotokoll som används av REST API. Antalet schematyper som visas i den nedrullningsbara listan beror på scheman som definierats i källan [!DNL Swagger].
      * Värd: Domännamnet eller IP-adressen för värden som använder REST API. Det är ett obligatoriskt fält.
      * Bassökväg: URL-prefixet för alla API-sökvägar. Det är ett valfritt fält.\
        Om det behövs kan du redigera de förifyllda värdena för dessa fält.

   * Välj autentiseringstypen - Ingen, OAuth2.0([Auktoriseringskod](https://oauth.net/2/grant-types/authorization-code/), [Klientautentiseringsuppgifter](https://oauth.net/2/grant-types/client-credentials/)), Grundläggande autentisering, API-nyckel eller Anpassad autentisering - för att få åtkomst till RESTful-tjänsten och ange därmed information för autentisering.

   Om du väljer **[!UICONTROL API Key]** som autentiseringstyp anger du värdet för API-nyckeln. API-nyckeln kan skickas som en begäranderubrik eller som en frågeparameter. Välj något av dessa alternativ i listrutan **[!UICONTROL Location]** och ange namnet på huvudet eller frågeparametern i fältet **[!UICONTROL Parameter Name]** i enlighet med detta.

   <!--If you select **[!UICONTROL Mutual Authentication]** as the authentication type, see [Certificate-based mutual authentication for RESTful and SOAP web services](#mutual-authentication).-->

1. Välj **[!UICONTROL Create]** om du vill skapa molnkonfigurationen för RESTful-tjänsten.

### Konfigurera RESTful-tjänster för Open API Specification version 3.0 {#configure-restful-services-open-api-3.0}

1. Gå till **[!UICONTROL Tools > Cloud Services > Data Sources]**. Välj den mapp där du vill skapa en molnkonfiguration.

   Mer information om hur du skapar och konfigurerar en mapp för molntjänstkonfigurationer finns i [Konfigurera mapp för molntjänstkonfigurationer](configure-data-sources.md#cloud-folder).

1. Välj **[!UICONTROL Create]** för att öppna **[!UICONTROL Create Data Source Configuration wizard]**. Ange ett namn och eventuellt en rubrik för konfigurationen, välj **[!UICONTROL RESTful Service]** i listrutan **[!UICONTROL Service Type]**, bläddra och välj en miniatyrbild för konfigurationen och välj **[!UICONTROL Next]**.
1. Ange följande information för RESTful-tjänsten:

   * Välj en URL eller fil i listrutan [!UICONTROL Swagger Source] och ange därför [!DNL Swagger 3.0 URL] till definitionsfilen [!DNL &#x200B; Swagger] eller överför filen [!DNL Swagger] från det lokala filsystemet.
   * Baserat på indata från [!DNL &#x200B; Swagger] Source visas anslutningsinformationen med målservern.
   * Välj autentiseringstypen - Ingen, OAuth2.0([Auktoriseringskod](https://oauth.net/2/grant-types/authorization-code/), [Klientautentiseringsuppgifter](https://oauth.net/2/grant-types/client-credentials/)), Grundläggande autentisering, API-nyckel eller Anpassad autentisering - för att få åtkomst till RESTful-tjänsten och ange därmed information för autentisering.

   Om du väljer **[!UICONTROL API Key]** som autentiseringstyp anger du värdet för API-nyckeln. API-nyckeln kan skickas som en begäranderubrik eller som en frågeparameter. Välj något av dessa alternativ i listrutan **[!UICONTROL Location]** och ange namnet på huvudet eller frågeparametern i fältet **[!UICONTROL Parameter Name]** i enlighet med detta.

   <!--If you select **[!UICONTROL Mutual Authentication]** as the authentication type, see [Certificate-based mutual authentication for RESTful and SOAP web services](#mutual-authentication).-->

1. Välj **[!UICONTROL Create]** om du vill skapa molnkonfigurationen för RESTful-tjänsten.

En del åtgärder som inte stöds av RESTful services Open API Specification version 3.0 är:

* Återanrop
* en/något av
* Fjärrreferens
* Länkar
* Olika begärande organ för olika MIME-typer för en enda operation

Mer information finns i [OpenAPI 3.0-specifikationen](https://swagger.io/specification/v3/).

### Konfigurera RESTful-tjänster med hjälp av tjänstslutpunkten {#configure-restful-services-service-endpoint}

<span class="preview"> Funktionen för tjänstslutpunkt finns i programmet för tidig Adobe-åtgärd och kan endast användas för kärnkomponenter. Du kan skriva till aem-forms-ea@adobe.com från ditt officiella e-post-id för att gå med i det tidiga adopterprogrammet och begära åtkomst till funktionen. </span>

1. Gå till **[!UICONTROL Tools > Cloud Services > Data Sources]**. Välj den mapp där du vill skapa en molnkonfiguration.

   Mer information om hur du skapar och konfigurerar en mapp för molntjänstkonfigurationer finns i [Konfigurera mapp för molntjänstkonfigurationer](configure-data-sources.md#cloud-folder).

1. Välj **[!UICONTROL Create]** för att öppna **[!UICONTROL Create Data Source Configuration wizard]**.

1. Ange ett namn och eventuellt en rubrik för konfigurationen, välj **[!UICONTROL RESTful Service]** i listrutan **[!UICONTROL Service Type]**, bläddra och välj en miniatyrbild för konfigurationen och välj **[!UICONTROL Next]**.

1. På nästa sida väljer du **[!UICONTROL Service Endpoint]** från **[!UICONTROL RESTful Service dropdown]**.

   ![Tjänstslutpunkt](/help/forms/assets/select-service-endpoint.png)

1. Ange **[!UICONTROL Service Endpoint URL]**.

   >[!NOTE]
   > Som standard är metodtypen POST.
1. Välj en innehållstyp som du vill välja i listrutan. Innehållstyper är formulärdata med flera delar, JSON och URL-kodade (Key-Value Pair).
1. Nu väljer du någon av autentiseringstyperna OAuth 2.0, Basic Authentication, API Key, Custom Authentication i listrutan.
   ![Autentiseringstyp för tjänstslutpunkt](/help/forms/assets/service-endpoint-authtype.png)
1. Klicka på Skapa.

### HTTP-klientkonfiguration för formulärdatamodell (FDM) för optimering av prestanda {#fdm-http-client-configuration}

[!DNL Experience Manager Forms] utgör en datamodell när de integreras med RESTful-webbtjänster som datakälla, och innehåller HTTP-klientkonfigurationer för prestandaoptimering.

Ange följande egenskaper för konfigurationen **[!UICONTROL Form Data Model HTTP Client Configuration for REST data source]** för att ange det reguljära uttrycket:

* Använd egenskapen `http.connection.max.per.route` för att ange maximalt antal tillåtna anslutningar mellan formulärdatamodellen (FDM) och RESTful-webbtjänster. Standardvärdet är 20 anslutningar.

* Använd egenskapen `http.connection.max` för att ange maximalt antal tillåtna anslutningar för varje flöde. Standardvärdet är 40 anslutningar.

* Använd egenskapen `http.connection.keep.alive.duration` för att ange varaktigheten för vilken en beständig HTTP-anslutning hålls aktiv. Standardvärdet är 15 sekunder.

* Använd egenskapen `http.connection.timeout` för att ange varaktigheten som [!DNL Experience Manager Forms]-servern väntar på att upprätta en anslutning. Standardvärdet är 10 sekunder.

* Använd egenskapen `http.socket.timeout` för att ange den maximala tidsperioden för inaktivitet mellan två datapaket. Standardvärdet är 30 sekunder.

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

1. Välj **[!UICONTROL Form Data Model HTTP Client Configuration for REST data source]**.

1. I dialogrutan [!UICONTROL Form Data Model HTTP Client Configuration for REST data source]:

   * Ange maximalt antal tillåtna anslutningar mellan formulärdatamodellen (FDM) och RESTful-webbtjänster i fältet **[!UICONTROL Connection limit in total]**. Standardvärdet är 20 anslutningar.

   * Ange maximalt antal tillåtna anslutningar för varje väg i fältet **[!UICONTROL Connection limit on per route basis]**. Standardvärdet är två anslutningar.

   * Ange varaktigheten, för vilken en beständig HTTP-anslutning hålls aktiv, i fältet **[!UICONTROL Keep alive]**. Standardvärdet är 15 sekunder.

   * Ange varaktigheten, som servern [!DNL Experience Manager Forms] väntar på att en anslutning ska upprättas för, i fältet **[!UICONTROL Connection timeout]**. Standardvärdet är 10 sekunder.

   * Ange den maximala tidsperioden för inaktivitet mellan två datapaket i fältet **[!UICONTROL Socket timeout]**. Standardvärdet är 30 sekunder.

## Konfigurera SOAP webbtjänster {#configure-soap-web-services}

SOAP-baserade webbtjänster beskrivs med hjälp av [WSDL-specifikationerna (Web Services Description Language)](https://www.w3.org/TR/wsdl). [!DNL Experience Manager Forms] stöder inte WSDL-modellen av RPC-typ.

Om du vill konfigurera en SOAP-baserad webbtjänst i [!DNL Experience Manager] as a Cloud Service kontrollerar du att du har WSDL-URL:en för webbtjänsten och gör följande:

1. Gå till **[!UICONTROL Tools > Cloud Services > Data Sources]**. Välj den mapp där du vill skapa en molnkonfiguration.

   Mer information om hur du skapar och konfigurerar en mapp för molntjänstkonfigurationer finns i [Konfigurera mapp för molntjänstkonfigurationer](configure-data-sources.md#cloud-folder).

1. Välj **[!UICONTROL Create]** för att öppna **[!UICONTROL Create Data Source Configuration wizard]**. Ange ett namn och eventuellt en rubrik för konfigurationen, välj **[!UICONTROL SOAP Web Service]** i listrutan **[!UICONTROL Service Type]**, bläddra och välj en miniatyrbild för konfigurationen och välj **[!UICONTROL Next]**.
1. Ange följande för SOAP webbtjänst:

   * WSDL-URL för webbtjänsten.
   * Tjänstslutpunkt. Ange ett värde i det här fältet om du vill åsidosätta tjänstslutpunkten som anges i WSDL.
   * Välj autentiseringstyp - Ingen, OAuth2.0([Auktoriseringskod](https://oauth.net/2/grant-types/authorization-code/), [Klientautentiseringsuppgifter](https://oauth.net/2/grant-types/client-credentials/)), Grundläggande autentisering eller Anpassad autentisering - för att få åtkomst till SOAP-tjänsten och ange därefter information för autentisering.

     <!--If you select **[!UICONTROL X509 Token]** as the Authentication type, configure the X509 certificate. For more information, see [Set up certificates](install-configure-document-services.md#set-up-certificates-for-reader-extension-and-encryption-service).-->
     <!--Specify the KeyStore alias for the X509 certificate in the **[!UICONTROL Key Alias]** field. Specify the time, in seconds, until the authentication request remains valid, in the **[!UICONTROL Time To Live]** field. Optionally, select to sign the message body or timestamp header or both.-->

     <!--If you select **[!UICONTROL Mutual Authentication]** as the authentication type, see [Certificate-based mutual authentication for RESTful and SOAP web services](#mutual-authentication).-->

1. Välj **[!UICONTROL Create]** om du vill skapa molnkonfigurationen för SOAP webbtjänst.

### Aktivera användning av importsatser i SOAP webbtjänster WSDL {#enable-import-statements}

Du kan ange ett reguljärt uttryck som fungerar som filter för absoluta URL:er som tillåts som importsatser i SOAP webbtjänster WSDL. Som standard finns det inget värde i det här fältet. Därför blockerar [!DNL Experience Manager] alla importsatser som är tillgängliga i WSDL. Om du anger `.*` som värde i det här fältet tillåter [!DNL Experience Manager] alla importsatser.

Ange egenskapen `importAllowlistPattern` för konfigurationen **[!UICONTROL Form Data Model SOAP Web Services Import Allowlist]** för att ange det reguljära uttrycket. I följande JSON-fil visas ett exempel:

```json
{
  "importAllowlistPattern": ".*"
}
```

[Generera OSGi-konfigurationer med AEM SDK](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=sv-SE#generating-osgi-configurations-using-the-aem-sdk-quickstart) och [distribuera konfigurationen](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=sv-SE#deployment-process) till din Cloud Service-instans om du vill ange värden för en konfiguration.

## Konfigurera OData-tjänster {#config-odata}

En OData-tjänst identifieras av tjänstens rot-URL. Om du vill konfigurera en OData-tjänst i [!DNL Experience Manager] as a Cloud Service kontrollerar du att du har tjänstens rot-URL och gör följande:

>[!NOTE]
>
> Formulärdatamodellen (FDM) stöder [OData version 4](https://www.odata.org/documentation/).
>En steg-för-steg-guide om hur du konfigurerar [!DNL Microsoft®® Dynamics 365], online eller lokalt, finns i [[!DNL Microsoft® Dynamics] OData-konfiguration](ms-dynamics-odata-configuration.md).

1. Gå till **[!UICONTROL Tools > Cloud Services > Data Sources]**. Välj den mapp där du vill skapa en molnkonfiguration.

   Mer information om hur du skapar och konfigurerar en mapp för molntjänstkonfigurationer finns i [Konfigurera mapp för molntjänstkonfigurationer](#cloud-folder).

1. Välj **[!UICONTROL Create]** för att öppna **[!UICONTROL Create Data Source Configuration wizard]**. Ange ett namn och eventuellt en rubrik för konfigurationen, välj **[!UICONTROL OData Service]** i listrutan **[!UICONTROL Service Type]**, bläddra och välj en miniatyrbild för konfigurationen och välj **[!UICONTROL Next]**.
1. Ange följande information för OData-tjänsten:

   * Tjänstens rot-URL för OData-tjänsten som ska konfigureras.
   * Välj autentiseringstypen - Ingen, OAuth2.0([Auktoriseringskod](https://oauth.net/2/grant-types/authorization-code/), [Klientautentiseringsuppgifter](https://oauth.net/2/grant-types/client-credentials/)), Grundläggande autentisering, API-nyckel eller Anpassad autentisering - för att få åtkomst till OData-tjänsten och ange därför informationen för autentisering.

   Om du väljer **[!UICONTROL API Key]** som autentiseringstyp anger du värdet för API-nyckeln. API-nyckeln kan skickas som en begäranderubrik eller som en frågeparameter. Välj något av dessa alternativ i listrutan **[!UICONTROL Location]** och ange namnet på huvudet eller frågeparametern i fältet **[!UICONTROL Parameter Name]** i enlighet med detta.

   >[!NOTE]
   >
   >Välj autentiseringstypen OAuth 2.0 om du vill ansluta till [!DNL Microsoft®® Dynamics]-tjänster med OData-slutpunkten som tjänstrot.

1. Välj **[!UICONTROL Create]** om du vill skapa molnkonfigurationen för OData-tjänsten.

<!--
## Configure Microsoft&reg; SharePoint List {#config-sharepoint-list}

<span class="preview"> This is a pre-release feature and accessible through our [pre-release channel](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=sv-SE#new-features). </span>

To save data in a tabular form use, Microsoft&reg; SharePoint List. To configure a Microsoft SharePoint List in [!DNL Experience Manager] as a Cloud Service, do the following:

1. Go to **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** >  **[!UICONTROL Microsoft&reg; SharePoint]**.   
1. Select a **Configuration Container**. The configuration is stored in the selected Configuration Container. 
1. Click **[!UICONTROL Create]** > **[!UICONTROL SharePoint List]** from the drop-down list. The SharePoint configuration wizard appears.  
1. Specify the **[!UICONTROL Title]**, **[!UICONTROL Client ID]**, **[!UICONTROL Client Secret]** and **[!UICONTROL OAuth URL]**. For information on how to retrieve Client ID, Client Secret, Tenant ID for OAuth URL, see [Microsoft&reg; Documentation](https://learn.microsoft.com/en-us/graph/auth-register-app-v2).
    * You can retrieve the `Client ID` and `Client Secret` of your app from the Microsoft&reg; Azure portal.
    * In the Microsoft&reg; Azure portal, add the Redirect URI as `https://[author-instance]/libs/cq/sharepointlist/content/configurations/wizard.html`. Replace `[author-instance]` with the URL of your Author instance.
    * Add the API permissions `offline_access` and `Sites.Manage.All` in the **Microsoft&reg; Graph** tab to provide read/write permissions. Add `AllSites.Manage` permission in the **Sharepoint** tab to interact remotely with SharePoint data.
    * Use OAuth URL: `https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize`. Replace `<tenant-id>` with the `tenant-id` of your app from the Microsoft&reg; Azure portal.

      >[!NOTE]
      >
      > The **client secret** field is mandatory or optional depends upon your Azure Active Directory application configuration. If your application is configured to use a client secret, it is mandatory to provide the client secret.

1. Click **[!UICONTROL Connect]**. On a successful connection, the `Connection Successful` message appears.
1. Select **[!UICONTROL SharePoint Site]** and **[!UICONTROL SharePoint List]** from the drop-down list.
1. Select **[!UICONTROL Create]** to create the cloud configuration for the Microsoft&reg; SharePointList.

-->

<!--## Certificate-based mutual authentication for RESTful and SOAP web services {#mutual-authentication}

When you enable mutual authentication for form data model (FDM), both the data source and [!DNL Experience Manager] Server running Form Data Model (FDM) authenticate each other's identity before sharing any data. You can use mutual authentication for REST and SOAP-based connections (data sources). To configure mutual authentication for a Form Data Model (FDM) on your [!DNL Experience Manager Forms] environment:

1. Upload the private key (certificate) to [!DNL Experience Manager Forms] server. To upload the private key:
   1. Log in to your [!DNL Experience Manager Forms] server as an administrator.
   1. Navigate to **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Users]**. Select the `fd-cloudservice` user and select **[!UICONTROL Properties]**.
   1. Open the **[!UICONTROL Keystore]** tab, expand the **[!UICONTROL Add Private Key from KeyStore file]** option, upload the KeyStore File, specify the aliases, passwords, and select **[!UICONTROL Submit]**. The Certificate is uploaded.  The private key alias is mentioned in the certificate and set while creating the certificate.
1. Upload trust certificate to Global Trust Store. To upload the certificate:
   1. Navigate to **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Trust Store]**.
   1. Expand the **[!UICONTROL Add Certificate from CER file]** option, select **[!UICONTROL Select Certificate File]**, upload the certificate, and select **[!UICONTROL Submit]**.
1. Configure [SOAP](#configure-soap-web-services) or [RESTful](#configure-restful-web-services) web services as the data source and select **[!UICONTROL Mutual authentication]** as the authentication type. If you configure multiple self-signed certificates for `fd-cloudservice` user, specify the Key Alias name for the certificate.-->

## Nästa steg {#next-steps}

Du har konfigurerat datakällorna. Därefter kan du skapa en formulärdatamodell (FDM) eller, om du redan har skapat en formulärdatamodell (FDM) utan en datakälla, associera den med de datakällor du konfigurerade. Mer information finns i [Skapa formulärdatamodell](create-form-data-models.md).

<!--

>[!MORELIKETHIS]
>
>* [Configure Azure storage for AEM Forms](/help/forms/configure-azure-storage.md)
>* [Integrate Microsoft Dynamics 365 and Salesforce with Adaptive Forms](/help/forms/configure-msdynamics-salesforce.md)
>*  [Add Forms Portal to an AEM Sites page](/help/forms/configure-forms-portal.md)

-->
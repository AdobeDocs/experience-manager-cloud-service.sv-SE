---
title: Hur konfigurerar jag datakällor?
description: Med Experience Manager Forms dataintegrering kan du konfigurera och ansluta till olika datakällor. Lär dig hur du konfigurerar RESTful-webbtjänster, SOAP-baserade webbtjänster och OData-tjänster som datakällor och använder dem för att skapa formulärdatamodeller.
feature: Form Data Model
role: User, Developer
level: Beginner
exl-id: cb77a840-d705-4406-a94d-c85a6efc8f5d
source-git-commit: 7d3f553765580c1d81a80bea456e9df908939bc0
workflow-type: tm+mt
source-wordcount: '1230'
ht-degree: 0%

---

# Konfigurera datakällor {#configure-data-sources}

![Dataintegrering](do-not-localize/data-integeration.png)

[!DNL Experience Manager Forms] Med dataintegrering kan du konfigurera och ansluta till olika datakällor. Följande typer stöds inte. Men med liten anpassning kan ni också integrera andra datakällor.

<!-- * Relational databases - MySQL, [!DNL Microsoft SQL Server], [!DNL IBM DB2], and [!DNL Oracle RDBMS] 
* [!DNL Experience Manager] user profile  -->
* RESTful web services
* SOAP-baserade webbtjänster
* OData-tjänster

Dataintegrering har stöd för autentiseringstyperna OAuth2.0, Grundläggande autentisering och API Key som är färdiga och tillåter implementering av anpassad autentisering för åtkomst till webbtjänster. SOAP-baserade tjänster och OData-tjänster är konfigurerade i RESTful [!DNL Experience Manager] as a Cloud Service <!--, JDBC for relational databases --> och anslutning för [!DNL Experience Manager] användarprofilen är konfigurerad i [!DNL Experience Manager] webbkonsol.

>[!NOTE]
>
>[!UICONTROL Experience Manager Forms] stöder inte relationsdatabaser.

<!-- ## Configure relational database {#configure-relational-database}

You can configure relational databases using [!DNL Experience Manager] Web Console Configuration. Do the following:

1. Go to [!DNL Experience Manager] web console at `https://server:host/system/console/configMgr`.
1. Look for **[!UICONTROL Apache Sling Connection Pooled DataSource]** configuration. Tap to open the configuration in edit mode.
1. In the configuration dialog, specify the details for the database you want to configure, such as:

    * Name of the data source
    * Data source service property that stores the data source name
    * Java class name for the JDBC driver
    * JDBC connection URI
    * Username and password to establish connection with the JDBC driver

   >[!NOTE]
   >
   >Ensure that you encrypt sensitive information like passwords before configuring the data source. To encrypt:
   >
   >    
   >    
   >    1. Go to https://'[server]:[port]'/system/console/crypto.
   >    1. In the **[!UICONTROL Plain Text]** field, specify the password or any string to encrypt and tap **[!UICONTROL Protect]**.
   >    
   >    
   >    
   >The encrypted text appears in the Protected Text field that you can specify in the configuration.

1. Enable **[!UICONTROL Test on Borrow]** or **[!UICONTROL Test on Return]** to specify that the objects are validated before being borrowed or returned from and to the pool, respectively.
1. Specify a SQL SELECT query in the **[!UICONTROL Validation Query]** field to validate connections from the pool. The query must return at least one row. Based on your database, specify one of the following:

    * SELECT 1 (MySQL and MS SQL) 
    * SELECT 1 from dual (Oracle)

1. Tap **[!UICONTROL Save]** to save the configuration. -->

<!-- ## Configure [!DNL Experience Manager] user profile {#configure-aem-user-profile}

You can configure [!DNL Experience Manager] user profile using User Profile Connector configuration in [!DNL Experience Manager] Web Console. Do the following:

1. Go to [!DNL Experience Manager] web console at `https://[server]:[port]/system/console/configMgr`.
1. Look for **[!UICONTROL AEM Forms Data Integrations - User Profile Connector Configuration]** and tap to open the configuration in edit mode.
1. In the User Profile Connector Configuration dialog, you can add, remove, or update user profile properties. The specified properties will be available for use in form data model. Use the following format to specify user profile properties:

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
1. I **[!UICONTROL Create Configuration]** dialogruta, ange en rubrik för mappen och aktivera **[!UICONTROL Cloud Configurations]**.
1. Tryck **[!UICONTROL Create]** för att skapa en mapp som är aktiverad för molntjänstkonfigurationer.

## Konfigurera RESTful-webbtjänster {#configure-restful-web-services}

RESTful-webbtjänsten kan beskrivas med [Swagger-specifikationer](https://swagger.io/specification/) i JSON- eller YAML-format i en [!DNL Swagger] definitionsfil. Konfigurera RESTful-webbtjänsten i [!DNL Experience Manager] as a Cloud Service, se till att du har antingen [!DNL Swagger] på filsystemet eller den URL där filen finns.

Gör följande för att konfigurera RESTful-tjänster:

1. Gå till **[!UICONTROL Tools > Cloud Services > Data Sources]**. Tryck för att välja den mapp där du vill skapa en molnkonfiguration.

   Se [Konfigurera mapp för molntjänstkonfigurationer](configure-data-sources.md#cloud-folder) om du vill ha information om hur du skapar och konfigurerar en mapp för molntjänstkonfigurationer.

1. Tryck **[!UICONTROL Create]** för att öppna **[!UICONTROL Create Data Source Configuration wizard]**. Ange ett namn och eventuellt en rubrik för konfigurationen, välj **[!UICONTROL RESTful Service]** från **[!UICONTROL Service Type]** nedrullningsbar meny, där du kan bläddra och välja en miniatyrbild för konfigurationen, och trycka på **[!UICONTROL Next]**.
1. Ange följande information för RESTful-tjänsten:

   * Välj URL eller fil på menyn [!UICONTROL Swagger Source] och ange [!DNL Swagger URL] till[!DNL  Swagger] definitionsfil eller ladda upp [!DNL Swagger] från det lokala filsystemet.
   * Baserat på[!DNL  Swagger] Källindata, följande fält är förifyllda med värden:

      * Schema: De överföringsprotokoll som används av REST API. Antalet schematyper som visas i listrutan beror på scheman som definieras i [!DNL Swagger] källa.
      * Värd: Domännamnet eller IP-adressen för värden som använder REST API. Det är ett obligatoriskt fält.
      * Grundsökväg: URL-prefixet för alla API-sökvägar. Det är ett valfritt fält.\
         Om det behövs kan du redigera de förifyllda värdena för dessa fält.
   * Välj autentiseringstyp - Ingen, OAuth2.0, Grundläggande autentisering, API-nyckel eller Anpassad autentisering - för att få åtkomst till RESTful-tjänsten och ange därefter information för autentisering.

   Om du väljer **[!UICONTROL API Key]** Ange värdet för API-nyckeln som autentiseringstyp. API-nyckeln kan skickas som en begäranderubrik eller som en frågeparameter. Välj ett av dessa alternativ på menyn **[!UICONTROL Location]** nedrullningsbar lista och ange namnet på huvudet eller frågeparametern i **[!UICONTROL Parameter Name]** i enlighet med detta.

   <!--If you select **[!UICONTROL Mutual Authentication]** as the authentication type, see [Certificate-based mutual authentication for RESTful and SOAP web services](#mutual-authentication).-->

1. Tryck **[!UICONTROL Create]** för att skapa molnkonfigurationen för RESTful-tjänsten.

## Konfigurera SOAP-webbtjänster {#configure-soap-web-services}

SOAP-baserade webbtjänster beskrivs med [WSDL-specifikationer (Web Services Description Language)](https://www.w3.org/TR/wsdl). [!DNL Experience Manager Forms] saknar stöd för WSDL-modellen i RPC-format.

Konfigurera SOAP-baserad webbtjänst i [!DNL Experience Manager] as a Cloud Service, kontrollera att du har WSDL-URL:en för webbtjänsten och gör följande:

1. Gå till **[!UICONTROL Tools > Cloud Services > Data Sources]**. Tryck för att välja den mapp där du vill skapa en molnkonfiguration.

   Se [Konfigurera mapp för molntjänstkonfigurationer](configure-data-sources.md#cloud-folder) om du vill ha information om hur du skapar och konfigurerar en mapp för molntjänstkonfigurationer.

1. Tryck **[!UICONTROL Create]** för att öppna **[!UICONTROL Create Data Source Configuration wizard]**. Ange ett namn och eventuellt en rubrik för konfigurationen, välj **[!UICONTROL SOAP Web Service]** från **[!UICONTROL Service Type]** nedrullningsbar meny, där du kan bläddra och välja en miniatyrbild för konfigurationen, och trycka på **[!UICONTROL Next]**.
1. Ange följande för SOAP-webbtjänsten:

   * WSDL-URL för webbtjänsten.
   * Tjänstslutpunkt. Ange ett värde i det här fältet om du vill åsidosätta tjänstslutpunkten som anges i WSDL.
   * Välj autentiseringstyp - Ingen, OAuth2.0, Grundläggande autentisering eller Anpassad autentisering - för att få åtkomst till SOAP-tjänsten och ange därefter information för autentisering.

      <!--If you select **[!UICONTROL X509 Token]** as the Authentication type, configure the X509 certificate. For more information, see [Set up certificates](install-configure-document-services.md#set-up-certificates-for-reader-extension-and-encryption-service).-->
      <!--Specify the KeyStore alias for the X509 certificate in the **[!UICONTROL Key Alias]** field. Specify the time, in seconds, until the authentication request remains valid, in the **[!UICONTROL Time To Live]** field. Optionally, select to sign the message body or timestamp header or both.-->

      <!--If you select **[!UICONTROL Mutual Authentication]** as the authentication type, see [Certificate-based mutual authentication for RESTful and SOAP web services](#mutual-authentication).-->

1. Tryck **[!UICONTROL Create]** för att skapa molnkonfigurationen för SOAP-webbtjänsten.

### Aktivera användning av importsatser i SOAP-webbtjänster WSDL {#enable-import-statements}

Du kan ange ett reguljärt uttryck som fungerar som filter för absoluta URL:er som tillåts som importsatser i SWDL för SOAP-webbtjänster. Som standard finns det inget värde i det här fältet. Som en följd av detta [!DNL Experience Manager] blockerar alla importsatser som är tillgängliga i WSDL. Om du anger `.*` som värdet i detta fält, [!DNL Experience Manager] tillåter alla importsatser.

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
>Om du vill konfigurera steg-för-steg-guiden [!DNL Microsoft Dynamics 365], online eller lokalt, se [[!DNL Microsoft Dynamics] OData-konfiguration](ms-dynamics-odata-configuration.md).

1. Gå till **[!UICONTROL Tools > Cloud Services > Data Sources]**. Tryck för att välja den mapp där du vill skapa en molnkonfiguration.

   Se [Konfigurera mapp för molntjänstkonfigurationer](#cloud-folder) om du vill ha information om hur du skapar och konfigurerar en mapp för molntjänstkonfigurationer.

1. Tryck **[!UICONTROL Create]** för att öppna **[!UICONTROL Create Data Source Configuration wizard]**. Ange ett namn och eventuellt en rubrik för konfigurationen, välj **[!UICONTROL OData Service]** från **[!UICONTROL Service Type]** nedrullningsbar meny, där du kan bläddra och välja en miniatyrbild för konfigurationen, och trycka på **[!UICONTROL Next]**.
1. Ange följande information för OData-tjänsten:

   * Tjänstens rot-URL för OData-tjänsten som ska konfigureras.
   * Välj autentiseringstyp - Ingen, OAuth2.0, Grundläggande autentisering, API-nyckel eller Anpassad autentisering - för att få åtkomst till OData-tjänsten och ange därefter autentiseringsinformationen.

   Om du väljer **[!UICONTROL API Key]** Ange värdet för API-nyckeln som autentiseringstyp. API-nyckeln kan skickas som en begäranderubrik eller som en frågeparameter. Välj ett av dessa alternativ på menyn **[!UICONTROL Location]** nedrullningsbar lista och ange namnet på huvudet eller frågeparametern i **[!UICONTROL Parameter Name]** i enlighet med detta.

   >[!NOTE]
   >
   >Du måste välja autentiseringstypen OAuth 2.0 för att kunna ansluta med [!DNL Microsoft Dynamics] tjänster där OData-slutpunkten används som tjänstrot.

1. Tryck **[!UICONTROL Create]** för att skapa molnkonfigurationen för OData-tjänsten.

<!--## Certificate-based mutual authentication for RESTful and SOAP web services {#mutual-authentication}

When you enable mutual authentication for form data model, both the data source and [!DNL Experience Manager] Server running Form Data Model authenticate each other’s identity before sharing any data. You can use mutual authentication for REST and SOAP-based connections (data sources). To configure mutual authentication for a Form Data Model on your [!DNL Experience Manager Forms] environment:

1. Upload the private key (certificate) to [!DNL Experience Manager Forms] server. To upload the private key:
   1. Log in to your [!DNL Experience Manager Forms] server as an administrator.
   1. Navigate to **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Users]**. Select the `fd-cloudservice` user and tap **[!UICONTROL Properties]**.
   1. Open the **[!UICONTROL Keystore]** tab, expand the **[!UICONTROL Add Private Key from KeyStore file]** option, upload the KeyStore File, specify the aliases, passwords, and tap **[!UICONTROL Submit]**. The Certificate is uploaded.  The private key alias is mentioned in the certificate and set while creating the certificate.
1. Upload trust certificate to Global Trust Store. To upload the certificate:
   1. Navigate to **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Trust Store]**.
   1. Expand the **[!UICONTROL Add Certificate from CER file]** option, tap **[!UICONTROL Select Certificate File]**, upload the certificate, and tap **[!UICONTROL Submit]**.
1. Configure [SOAP](#configure-soap-web-services) or [RESTful](#configure-restful-web-services) web services as the data source and select **[!UICONTROL Mutual authentication]** as the authentication type. If you configure multiple self-signed certificates for `fd-cloudservice` user, specify the Key Alias name for the certificate.-->

## Nästa steg {#next-steps}

Du har konfigurerat datakällorna. Därefter kan du skapa en formulärdatamodell eller, om du redan har skapat en formulärdatamodell utan en datakälla, associera den med de datakällor du just konfigurerade. Se [Skapa formulärdatamodell](create-form-data-models.md) för mer information.

---
title: Hur integrerar man Salesforce med OAuth 2.0-klientautentiseringsflödet med AEM Forms?
description: Lär dig integrera Salesforce med AEM Forms med OAuth 2.0-klientautentiseringsflödet.
Keywords: Integration of Salesforce using OAuth 2.0 client credential flow, salesforce integration with oauth2 using client credential flow, salesforce and client credential integration
exl-id: 2c2029ab-6fb4-41a6-846c-175c3a79d921
source-git-commit: f70e18b1c21fd530587694f91c3969e831cfc640
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 2%

---

# Ansluta anpassat formulär till Salesforce med OAuth 2.0-klientens autentiseringsflöde {#configure-salesforce-with-ouath-2.0-client-credential}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/oauth2-client-credentials-flow-for-server-to-server-integration.html) |
| AEM as a Cloud Service | Den här artikeln |

Du kan använda klientautentiseringsuppgifter för OAuth 2.0 för att integrera AEM Forms med Salesforce-programmet. OAuth 2.0-klientens autentiseringsuppgifter är en standard och säker metod för direkt kommunikation utan användarinblandning.

![Arbetsflöde vid inställning av kommunikation mellan AEM Forms och Salesforce-program](/help/forms/assets/salesforce-workflow.png)

AEM Forms utbyter klientautentiseringsuppgifterna (konsumentnyckel och hemlighet), som definieras i det Salesforce-anslutna programmet, för att få en åtkomsttoken.

Det finns många fördelar med att använda OAuth 2.0-klientautentiseringsuppgifter för autentisering över autentisering av Authorization Code Flow:

* Autentisering med OAuth 2.0-klientautentiseringsuppgifter tillåter mer än fem anslutningar per användare.
* AEM datakällkonfiguration fortsätter att arbeta med inaktivering, åtkomständringar och lösenordsuppdatering för en AEM användare.

## Förutsättningar {#prerequisites}

Innan du ställer in kommunikation mellan ett Salesforce-program och en AEM-miljö:

* Skapa en [Salesforce-ansluten app med OAuth 2.0-klientautentiseringsflöde](https://help.salesforce.com/s/articleView?id=sf.connected_app_client_credentials_setup.htm&amp;type=5) och en användare som bara har API för din organisation och som får tillgång till konsumentnyckeln och konsumenthemligheten för appen.

* Kontrollera att Swagger-filen är rätt konfigurerad för att matcha organisationens API:er. Du kan också välja att [skapa en Swagger-fil](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/forms/integrate-with-salesforce/describe-rest-api.html) från scratch, skräddarsytt för användning i AEM.


## Konfigurera Salesforce-program med OAuth 2.0-klientautentiseringsflöde {#steps-to-create-aem-datasource-configuration}

Så här ansluter du adaptivt formulär till Salesforce-programmet med autentiseringsinställningarna för OAuth 2.0-klientautentisering:

1. Logga in på din Author-instans.
1. Gå till **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Data Sources]**.
1. Välj konfigurationsmappen.
1. Klicka **[!UICONTROL Create]** och **[!UICONTROL Create Data Source Configuration]** visas.
1. Ange **[!UICONTROL Title]** och väljer **[!UICONTROL Service Type]** as **[!UICONTROL RESTful Service]**.
1. Klicka på **[!UICONTROL Next]**.
1. Välj **[!UICONTROL Swagger Source]** as **[!UICONTROL File].**

   >[!NOTE]
   >
   > När swagger-filen väljs fylls schemat, värdnamnet och bassökvägen i automatiskt.

1. Överför den skapade swagger-filen från den lokala datorn genom att klicka på **[!UICONTROL Browse]**.
1. Välj **[!UICONTROL Authentication Type]** as **[!UICONTROL OAuth 2.0]** och **[!UICONTROL Authentication Settings]** visas.
1. Välj **[!UICONTROL Grant Type]** as **[!UICONTROL Client Credential]**.
1. Ange **[!UICONTROL Client Id]** och **[!UICONTROL Client Secret]** som hämtats från Salesforce-appen som är ansluten.
1. Ange **[!UICONTROL Access Token URL]** i format
   `https://[MyDomainName].my.salesforce.com/services/oauth2/token`.

   >[!NOTE]
   >
   > Varje organisation har ett eget specifikt domännamn.

1. Klicka på **[!UICONTROL Test Connection]**.
1. Om anslutningen lyckas klickar du på **[!UICONTROL Create]** -knappen.

Nu kan du [skapa formulärdatamodellen](/help/forms/create-form-data-models.md) för att skicka anpassat formulär till Salesforce-programmet.



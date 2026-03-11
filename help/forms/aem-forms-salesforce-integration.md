---
title: Hur integrerar man Salesforce med OAuth 2.0-klientautentiseringsflödet med AEM Forms?
description: Lär dig integrera Salesforce med AEM Forms med OAuth 2.0-klientautentiseringsflödet. Här visas steg för integrering med AEM Forms Salesforce.
Keywords: Integration of Salesforce using OAuth 2.0 client credential flow, salesforce integration with oauth2 using client credential flow, salesforce and client credential integration, AEM Forms Salesforce integration
feature: Adaptive Forms, Form Data Model
role: User, Developer
badgeSaas: label="AEM Forms" type="Positive" tooltip="Gäller AEM Forms)."
exl-id: 2c2029ab-6fb4-41a6-846c-175c3a79d921
source-git-commit: 89b0f2a8ca9d2f60365a5c3962b0b4e826f79b3e
workflow-type: tm+mt
source-wordcount: '518'
ht-degree: 1%

---

# Integrera adaptiv form med Salesforce {#configure-salesforce-with-ouath-2.0-client-credential}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/oauth2-client-credentials-flow-for-server-to-server-integration.html?lang=sv-SE) |
| AEM as a Cloud Service | Den här artikeln |

Adobe Experience Manager (AEM) Forms-integrering med Salesforce gör att man kan effektivisera processerna genom att koppla blankettgenereringen och blanketthanteringen till Salesforce. Om du kopplar ett adaptivt formulär till Salesforce kan du utbyta data på ett smidigt sätt mellan de två plattformarna. När användare skickar formulär synkroniseras data automatiskt med Salesforce. Det säkerställer att all kundinformation är aktuell och centraliserad inom systemet.

Du kan använda klientautentiseringsuppgifter för OAuth 2.0 för att integrera AEM Forms med Salesforce-programmet. OAuth 2.0-klientens autentiseringsuppgifter är en standard och säker metod för direkt kommunikation utan användarinblandning.

![Arbetsflöde vid inställning av kommunikation mellan AEM Forms- och Salesforce-program](/help/forms/assets/salesforce-workflow.png)

AEM Forms utbyter klientens inloggningsuppgifter (konsumentnyckel och hemlighet), som definieras i det program som är anslutet till Salesforce, för att erhålla en åtkomsttoken.

AEM as a Cloud Service erbjuder olika inskickningsåtgärder för att hantera inskickade formulär. Du kan läsa mer om de här alternativen i artikeln [Åtgärd för att skicka anpassade formulär](/help/forms/configure-submit-actions-core-components.md).

Det finns många fördelar med att använda OAuth 2.0-klientautentiseringsuppgifter för autentisering över autentisering av Authorization Code Flow:

* Autentisering med OAuth 2.0-klientautentiseringsuppgifter tillåter mer än fem anslutningar per användare.
* AEM datakällkonfiguration fortsätter att arbeta med inaktivering, åtkomständringar och lösenordsuppdatering för en AEM-användare.

## Förutsättningar {#prerequisites}

Innan du anger kommunikation mellan ett Salesforce-program och en AEM-miljö:

* Skapa en [Salesforce-ansluten app med OAuth 2.0-klientautentiseringsflöde](https://help.salesforce.com/s/articleView?id=sf.connected_app_client_credentials_setup.htm&type=5) och en API-användare för din organisation och hämta konsumentnyckeln och konsumenthemligheten för appen.

* Kontrollera att Swagger-filen är rätt konfigurerad för att matcha organisationens API:er. Du kan också välja att [skapa en Swagger-fil](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/forms/integrate-with-salesforce/describe-rest-api.html?lang=sv-SE) från början, som är anpassad för användning i din AEM-miljö.


## Konfigurera Salesforce-program med OAuth 2.0 Client Credential-flöde {#steps-to-create-aem-datasource-configuration}

Så här ansluter du det adaptiva formuläret till Salesforce-programmet med autentiseringsinställningarna för OAuth 2.0-klientautentisering:

1. Logga in på din Author-instans.
1. Gå till **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Data Sources]**.
1. Välj konfigurationsmappen.
1. Klicka på **[!UICONTROL Create]** så visas **[!UICONTROL Create Data Source Configuration]**.
1. Ange **[!UICONTROL Title]** och välj **[!UICONTROL Service Type]** som **[!UICONTROL RESTful Service]**.
1. Klicka på **[!UICONTROL Next]**.
1. Välj **[!UICONTROL Swagger Source]** som **[!UICONTROL File].**

   >[!NOTE]
   >
   > När swagger-filen väljs fylls schemat, värdnamnet och bassökvägen i automatiskt.

1. Överför den skapade swagger-filen från den lokala datorn genom att klicka på **[!UICONTROL Browse]**.
1. Markera **[!UICONTROL Authentication Type]** som **[!UICONTROL OAuth 2.0]** så visas panelen **[!UICONTROL Authentication Settings]**.
1. Välj **[!UICONTROL Grant Type]** som **[!UICONTROL Client Credential]**.
1. Ange **[!UICONTROL Client Id]** och **[!UICONTROL Client Secret]** från den Salesforce-anslutna appen.
1. Ange **[!UICONTROL Access Token URL]** i format
   `https://[MyDomainName].my.salesforce.com/services/oauth2/token`.

   >[!NOTE]
   >
   > Varje organisation har ett eget specifikt domännamn.

1. Klicka på **[!UICONTROL Test Connection]**.
1. Om anslutningen lyckas klickar du på knappen **[!UICONTROL Create]**.


När du har konfigurerat Salesforce-programmet kan du använda konfigurationen när du skapar en formulärdatamodell (FDM). Mer information finns i [Skapa formulärdatamodell (FDM)](create-form-data-models.md). [Konfigurera formulärdatamodellens överföringsåtgärd](/help/forms/using-form-data-model.md) för ett anpassat formulär för att skicka data till Salesforce-program.

Mer information om hur du skapar och använder FDM (Form Data Model) i arbetsflöden finns i [Dataintegrering](data-integration.md).

## Relaterade artiklar

{{af-submit-action}}



---
title: Hur integrerar man Adobe Sign med AEM Forms?
description: Lär dig konfigurera Adobe Sign för [!DNL AEM Forms] as a Cloud Service?
feature: Adaptive Forms
role: User
level: Intermediate
exl-id: 609c3072-1c3d-43fa-898a-b4e62db8483b
source-git-commit: 72c53bf69c36c265d25d136c0d2887cac2fe98fc
workflow-type: tm+mt
source-wordcount: '963'
ht-degree: 0%

---

# Integrera [!DNL Adobe Sign] med [!DNL AEM Forms] as a Cloud Service  {#integrate-adobe-sign-with-aem-forms}

[!DNL Adobe Sign] möjliggör e-signaturarbetsflöden för Adaptive Forms. E-signaturer förbättrar arbetsflödena för att bearbeta dokument inom juridik, försäljning, löneadministration, personaladministration och många andra områden.

I en typisk [!DNL Adobe Sign] och Adaptiv Forms fyller en användare i ett adaptivt formulär som kan användas för en tjänst. Till exempel kan en kreditkortsansökan och en medborgare få förmåner. När en användare fyller i, skickar och signerar ansökningsformuläret skickas formuläret till tjänsteleverantören för ytterligare åtgärder. Tjänsteleverantören granskar programmet och använder [!DNL Adobe Sign] för att markera ansökan som godkänd. Om du vill aktivera liknande arbetsflöden för elektroniska signaturer kan du integrera [!DNL Adobe Sign] med [!DNL AEM Forms].

Används [!DNL Adobe Sign] med [!DNL AEM Forms], konfigurera [!DNL Adobe Sign] i AEM Cloud Services:

## Förutsättningar {#prerequisites}

Du behöver följande för att kunna integrera [!DNL Adobe Sign] med [!DNL AEM Forms]:

* En aktiv [Adobe Sign utvecklarkonto](https://acrobat.adobe.com/us/en/sign/developer-form.html).
* An [Adobe Sign API-program](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/create_app.md).
* Autentiseringsuppgifter (klient-ID och klienthemlighet) för [!DNL Adobe Sign] API-program.
* Använd [identisk krypteringsnyckel](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security-checklist.html?lang=en#make-sure-you-properly-replicate-encryption-keys-when-needed) för författare och publiceringsinstanser.
* (Endast för autentisering med myndighets-ID) [Aktivera autentiseringsmetoden](https://helpx.adobe.com/sign/using/adobesign-authentication-government-id.html#AuditReport) för autentisering av myndighets-ID.

## Konfigurera [!DNL Adobe Sign] med [!DNL AEM Forms] {#configure-adobe-sign-with-aem-forms}

Utför följande steg för att konfigurera [!DNL Adobe Sign] med [!DNL AEM Forms] på Author-instanserna.

1. I AEM Forms-författarinstansen går du till **[!UICONTROL Tools]** ![hammare](assets/hammer.png) > **[!UICONTROL General]** > **[!UICONTROL Configuration Browser]**.
1. På **[!UICONTROL Configuration Browser]** sida, tryck **[!UICONTROL Create]**.
1. I **[!UICONTROL Create Configuration]** dialogruta, ange **[!UICONTROL Title]** för konfigurationen, aktivera **[!UICONTROL Cloud Configurations]** och trycka **[!UICONTROL Create]**. Den skapar en konfigurationsbehållare för lagring av Cloud Services. Kontrollera att mappnamnet inte innehåller något utrymme.
1. Navigera till **[!UICONTROL Tools]** ![hammare](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]** och öppna konfigurationsbehållaren som du skapade i föregående steg.

   >[!NOTE]
   >
   >När du skapar ett adaptivt formulär anger du behållarnamnet i dialogrutan **[!UICONTROL Configuration Container]** fält.

1. Tryck på **[!UICONTROL Create]** att skapa [!DNL Adobe Sign] i AEM Forms.
1. I **[!UICONTROL General]** -fliken i **[!UICONTROL Create Adobe Sign Configuration]** sida, ange en **[!UICONTROL Name]** för konfigurationen och tryck på **[!UICONTROL Next]**. Du kan också ange en **[!UICONTROL Title]** och bläddra för att välja **[!UICONTROL Thumbnail]** för konfigurationen.

1. Kopiera URL-adressen i det aktuella webbläsarfönstret till en anteckningsruta. URL:en krävs för att konfigurera [!DNL Adobe Sign] program med [!DNL AEM Forms] i ett senare steg. Tryck på **[!UICONTROL Next]**.

1. I **[!UICONTROL Settings]** -fliken **[!UICONTROL OAuth URL]** -fältet innehåller standard-URL:en. URL-formatet är:

   `https://<shard>/public/oAuth/v2`

   Till exempel:
   `https://secure.na1.echosign.com/public/oauth/v2`

   där:

   **na1** refererar till standarddatabasfragmentet. Du kan ändra värdet för databasdelningen. Se till att [!DNL  Adobe Sign] Molnkonfigurationer pekar mot [korrigera Shard](https://helpx.adobe.com/sign/using/identify-account-shard.html).

   Om du skapar en annan [!DNL Adobe Sign] för en Adobe Experience Manager-funktion eller -komponent, se till att alla [!DNL Adobe Sign] Molnkonfigurationer pekar på samma fragment.

   >[!NOTE]
   >
   > Behåll **Skapa Adobe Sign-konfiguration** sidan öppnas. Stäng den inte. Du kan hämta **Klient-ID** och **Klienthemlighet** efter konfigurering av OAuth-inställningar för [!DNL Adobe Sign] som beskrivs i kommande steg.


1. Konfigurera OAuth-inställningar för [!DNL Adobe Sign] program:

   1. Öppna ett webbläsarfönster och logga in på [!DNL Adobe Sign] utvecklarkonto.
   1. Välj det program som konfigurerats för [!DNL AEM Forms]och trycka **[!UICONTROL Configure OAuth for Application]**.
   1. I **[!UICONTROL Redirect URL]** lägger du till URL-adressen som kopierades i ett tidigare steg (steg 7) och klickar på **[!UICONTROL Save]**.
   1. Aktivera följande scope för [!DNL Adobe Sign] program och klicka **[!UICONTROL Save]**.
   * [!DNL aggrement_read]
   * [!DNL aggrement_write]
   * [!DNL aggrement_send]
   * [!DNL widget_read]
   * [!DNL widget_write]
   * [!DNL workflow_read]

   Om du vill ha stegvis information om hur du konfigurerar OAuth-inställningar för en [!DNL Adobe Sign] program och hämta nycklarna, se [Konfigurera autentiseringsinställningar för programmet](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/configure_oauth.md) dokumentation för utvecklare.

   ![OAuth-konfiguration](assets/oauthconfig_new.png)

1. Gå tillbaka till **[!UICONTROL Create Adobe Sign Configuration]** sida. I **[!UICONTROL Settings]** -fliken, ange [**[!UICONTROL Client ID]** (kallas även program-ID) och **[!UICONTROL Client Secret]**]. Använd [Klient-ID och klienthemlighet för Adobe Sign-program](https://opensource.adobe.com/acrobat-sign/developer_guide/helloworld.html#get-the-app-id-and-secret) du skapade i föregående steg.

1. Välj **[!UICONTROL Enable Adobe Sign for attachments]** möjlighet att lägga till filer som är kopplade till ett adaptivt formulär i motsvarande [!DNL Adobe Sign] dokumentet har skickats för signering.

1. Tryck på **[!UICONTROL Connect to Adobe Sign]**. Ange användarnamn och lösenord för kontot som används när du skapar inloggningsuppgifter [!DNL Adobe Sign] program. När du ombeds att bekräfta åtkomsten för `your developer account`, klicka **[!UICONTROL Allow Access]**. Om autentiseringsuppgifterna är korrekta och du tillåter [!DNL AEM Forms] för att få tillgång till [!DNL Adobe Sign] utvecklarkontot visas ett meddelande om att åtgärden lyckades.

   ![Konfigurationen av Adobe Sign Cloud lyckades](assets/adobe-sign-cloud-configuration-success.png)

1. Tryck **[!UICONTROL Create]** för att skapa [!DNL Adobe Sign] konfiguration.

1. Välj konfigurationen och klicka på **[!UICONTROL Publish]**, markera konfigurationen och klicka på **[!UICONTROL Publish]**. Konfigurationen replikeras till motsvarande publiceringsmiljöer.

1. Upprepa alla ovanstående steg på utvecklaren, scenen och produktionsinstanserna (beroende på vad som återstår) för att slutföra konfigurationen [!DNL Adobe Sign] med [!DNL AEM Forms] för din miljö.

Nu kan du [använda lägg till Adobe Sign-fält i ett adaptivt formulär](working-with-adobe-sign.md). Se till att du lägger till konfigurationsbehållaren som används för Cloud Servicen i alla adaptiva Forms som aktiveras för [!DNL Adobe Sign]. Du kan ange en konfigurationsbehållare bland egenskaperna för ett adaptivt formulär.

## (Endast för AEM arbetsflöden) Konfigurera [!DNL Adobe Sign] schemaläggaren för att synkronisera signeringsstatusen {#configure-adobe-sign-scheduler-to-sync-the-signing-status}

När du använder [!DNL Adobe Sign] Arbetsflödessteg för att signera ett adaptivt formulär kan skickas mellan signerare efter varandra eller kan skickas till alla signerare samtidigt, beroende på arbetsflödesstegets konfiguration. [!DNL Adobe Sign] Adaptiv Forms som aktiverats skickas till Experience Manager Forms Server först när alla signerare har slutfört signeringsprocessen.

Som standard är [!DNL Adobe Sign] Tjänsten Scheduler kontrollerar (enkäter) signerarens svar efter var 24:e timme. Du kan ändra standardintervallet för din miljö.

Om du vill ändra standardintervallet anger du en [cron-uttryck](https://en.wikipedia.org/wiki/Cron#CRON_expression) för **sign.status.exp** egenskapen för **Konfigurationstjänst för Adobe Sign** konfiguration.

Om du till exempel vill köra konfigurationstjänsten varje dag klockan 00:00 anger du **sign.status.exp** egenskapen för **Konfigurationstjänst för Adobe Sign** konfiguration som ska anges `0 0 0 1/1 * ? *`. I följande JSON-fil visas exemplet som ska köra konfigurationstjänsten varje dag klockan 00:00:

```json
{
  "sign.status.exp":"0 0 0 1/1 * ? *"
}
```

Så här anger du värden för en konfiguration: [Generera OSGi-konfigurationer med AEM SDK](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#generating-osgi-configurations-using-the-aem-sdk-quickstart)och [distribuera konfigurationen](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#deployment-process) till din Cloud Service.

<!-- , perform the following steps:

1. Log in to [!DNL AEM Forms] Server with admin credentials and navigate to **[!UICONTROL Tools]** &gt;**[!UICONTROL Operations]** &gt; **[!UICONTROL Web Console]**.

   You can also open the following URL in a browser window:
   `https://server/system/console/configMgr`

1. Locate and open the **[!UICONTROL Adobe Sign Configuration Service]** option. Specify a [cron expression](https://en.wikipedia.org/wiki/Cron#CRON_expression) in the **Status Update Scheduler Expression** field and click **Save**. For example, to run the configuration service daily at 00:00 am, specify `0 0 0 1/1 * ? *` in the **Status Update Scheduler Expression** field.

Default interval to sync status of [!DNL Adobe Sign] is now changed. -->

## Relaterade artiklar {#related-articles}

* [Använda Adobe Sign i en adaptiv form](working-with-adobe-sign.md)

* [Bästa sättet att använda Adobe Sign med Adaptiv Forms](https://medium.com/adobetech/using-adobe-sign-to-e-sign-an-adaptive-form-heres-the-best-way-to-do-it-dc3e15f9b684)

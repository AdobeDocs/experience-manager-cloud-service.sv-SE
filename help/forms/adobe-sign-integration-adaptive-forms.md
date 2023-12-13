---
title: Hur integrerar man Adobe Acrobat Sign med AEM Forms?
description: Lär dig konfigurera Adobe Acrobat Sign för [!DNL AEM Forms] as a Cloud Service?
feature: Adaptive Forms
role: User
level: Intermediate
exl-id: 609c3072-1c3d-43fa-898a-b4e62db8483b
source-git-commit: 821c243ab2d8ce1468c80c36d01b5c4c8f2bec76
workflow-type: tm+mt
source-wordcount: '1869'
ht-degree: 0%

---

# Anslut [!DNL AEM Forms] as a Cloud Service med [!DNL Adobe Acrobat Sign] {#integrate-adobe-sign-with-aem-forms}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/adobe-sign-integration-adaptive-forms.html#adobe-acrobat-sign-for-government) |
| AEM as a Cloud Service | Den här artikeln |

[!DNL Adobe Acrobat Sign] möjliggör arbetsflöden för e-signaturer i anpassningsbara Forms- och AEM arbetsflöden. E-signaturer förbättrar arbetsflödena för att bearbeta dokument inom juridik, försäljning, löneadministration, personaladministration och många andra områden.

I en typisk [!DNL Adobe Acrobat Sign] och Adaptiv Forms fyller en användare i ett adaptivt formulär som kan användas för en tjänst. Till exempel kan en kreditkortsansökan och en medborgare få förmåner. När en användare fyller i, skickar och signerar ansökningsformuläret skickas formuläret till tjänsteleverantören för ytterligare åtgärder. Tjänsteleverantören granskar programmet och använder [!DNL Adobe Acrobat Sign] för att markera ansökan som godkänd. AEM Forms stöder både Adobe Acrobat Sign och Adobe Acrobat Sign Solutions for Government. Beroende på licens och krav kan du integrera eller ansluta AEM Forms med någon av lösningarna:

* [Anslut AEM Forms till Adobe Acrobat Sign](#adobe-sign)
* [Koppla AEM Forms till Adobe Acrobat Sign Solutions för myndigheter](#adobe-acrobat-sign-for-government)

## Anslut AEM Forms till Adobe Acrobat Sign {#adobe-sign}

Ansluta **[!DNL AEM Forms]** med **[!DNL Adobe Acrobat Sign]**, ställer in programvaran och kontona som listas i avsnittet Krav och konfigurerar Adobe Sign Cloud Service i Forms as a Cloud Service Author och Publish:

### Krav för att ansluta AEM Forms till Adobe Acrobat Sign {#prerequisites-for-adobe-sign}

Du behöver följande inställningar för att kunna integrera [!DNL Adobe Acrobat Sign] med [!DNL AEM Forms]:

1. En aktiv [Adobe Acrobat Sign utvecklarkonto](https://acrobat.adobe.com/us/en/sign/developer-form.html).
1. An [Adobe Acrobat Sign API-program](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/create_app.md).
1. Autentiseringsuppgifter (klient-ID och klienthemlighet) för [!DNL Adobe Acrobat Sign] API-program.
1. (Endast för autentisering med myndighets-ID) [Aktivera autentiseringsmetoden](https://helpx.adobe.com/sign/using/adobesign-authentication-government-id.html#AuditReport) för autentisering av myndighets-ID.

### Koppla samman AEM Forms Author och publicera förekomster med Adobe Acrobat Sign {#configure-adobe-sign-with-aem-forms}

Utför följande steg för att konfigurera [!DNL Adobe Acrobat Sign] med [!DNL AEM Forms] på Author-instanserna.

1. I AEM Forms-författarinstansen går du till **[!UICONTROL Tools]** ![hammare](assets/hammer.png) > **[!UICONTROL General]** > **[!UICONTROL Configuration Browser]**.
1. På **[!UICONTROL Configuration Browser]** sida, markera **[!UICONTROL Create]**.
1. I **[!UICONTROL Create Configuration]** dialogruta, ange **[!UICONTROL Title]** för konfigurationen, aktivera **[!UICONTROL Cloud Configurations]** och markera **[!UICONTROL Create]**. Den skapar en konfigurationsbehållare för lagring av Cloud Service. Kontrollera att mappnamnet inte innehåller något utrymme.
1. Navigera till **[!UICONTROL Tools]** ![hammare](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Acrobat Sign]** och öppna konfigurationsbehållaren som du skapade i föregående steg.

   >[!NOTE]
   >
   >När du skapar ett adaptivt formulär anger du behållarnamnet i dialogrutan **[!UICONTROL Configuration Container]** fält.

1. Välj på konfigurationssidan **[!UICONTROL Create]** att skapa [!DNL Adobe Acrobat Sign] i AEM Forms.
1. I **[!UICONTROL General]** -fliken i **[!UICONTROL Create Adobe Acrobat Sign Configuration]** sida, ange en **[!UICONTROL Name]** för konfigurationen och välj **[!UICONTROL Next]**. Du kan också ange en **[!UICONTROL Title]** och bläddra för att välja **[!UICONTROL Thumbnail]** för konfigurationen.

1. Nu kan du **[!UICONTROL Select solution]** för att markera [!DNL Adobe Acrobat Sign].

   ![Adobe Acrobat Sign Solutions](assets/adobe-sign-solution.png)

<!--

[create URL](#create-a-redirect-url-for-your-aem-instance)
 -->

1. Kopiera URL:en som finns i det aktuella webbläsarfönstret till en anteckningsruta och ta bort delen `/ui#/aem` från webbadressen. Den ändrade URL:en måste sedan konfigureras [!DNL Adobe Acrobat Sign] program med [!DNL AEM Forms], i ett senare steg. Välj **[!UICONTROL Next]**.

1. I **[!UICONTROL Settings]** tab,
   * den **[!UICONTROL OAuth URL]** -fältet innehåller standardwebbadressen som innehåller Adobe Sign-databasdelning. URL-formatet är:

     `https://<shard>/public/oauth/v2`

     Till exempel:
     `https://secure.na1.echosign.com/public/oauth/v2`

   * den **[!UICONTROL Access token URL]** -fältet innehåller standardwebbadressen som innehåller Adobe Sign-databasdelning. URL-formatet är:

     `https://<shard>/oauth/v2/token`

     Till exempel:
     `https://api.na1.echosign.com/oauth/v2/token`

   där:

   **na1** refererar till standarddatabasfragmentet. Du kan ändra värdet för databasdelningen. Se till att [!DNL  Adobe Acrobat Sign] Molnkonfigurationer pekar mot [korrigera Shard](https://helpx.adobe.com/sign/using/identify-account-shard.html).

   >[!NOTE]
   >
   >* Behåll **Skapa Adobe Acrobat Sign-konfiguration** sidan öppnas. Stäng den inte. Du kan hämta **Klient-ID** och **Klienthemlighet** efter konfigurering av OAuth-inställningar för [!DNL Adobe Acrobat Sign] som beskrivs i kommande steg.
   > * När du har loggat in på ditt Adobe Sign-konto går du till **[!UICONTROL Acrobat Sign API]** > **[!UICONTROL API Information]** > **[!UICONTROL REST API Methods Documentation]** > **[!UICONTROL OAuth Access Token]** för att få tillgång till information om Adobe Sign OAuth URL och Access Token URL.

1. Konfigurera OAuth-inställningar för [!DNL Adobe Acrobat Sign] program:

   1. Öppna ett webbläsarfönster och logga in på [!DNL Adobe Acrobat Sign] utvecklarkonto.
   1. Välj det program som konfigurerats för [!DNL AEM Forms]och markera **[!UICONTROL Configure OAuth for Application]**.
   1. I **[!UICONTROL Redirect URL]** lägger du till URL-adressen som kopierades i ett tidigare steg (steg 8) och klickar på **[!UICONTROL Save]**.
   1. Aktivera följande scope för [!DNL Adobe Acrobat Sign] program och klickar på **[!UICONTROL Save]**.

   * [!DNL aggrement_read]
   * [!DNL aggrement_write]
   * [!DNL aggrement_send]
   * [!DNL widget_read]
   * [!DNL widget_write]
   * [!DNL workflow_read]

   Om du vill ha stegvis information om hur du konfigurerar OAuth-inställningar för en [!DNL Adobe Acrobat Sign] program och hämta nycklarna, se [Konfigurera autentiseringsinställningar för programmet](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/configure_oauth.md) dokumentation för utvecklare.

   ![OAuth-konfiguration](/help/forms/assets/oauthconfig-new.png)

1. Gå tillbaka till **[!UICONTROL Create Adobe Acrobat Sign Configuration]** sida. I **[!UICONTROL Settings]** -fliken, ange [**[!UICONTROL Client ID]** (kallas även program-ID) och **[!UICONTROL Client Secret]**]. Använd [Klient-ID och klienthemlighet för Adobe Acrobat Sign-program](https://opensource.adobe.com/acrobat-sign/developer_guide/helloworld.html#get-the-app-id-and-secret) som du skapade i föregående steg.

1. Välj **[!UICONTROL Enable Adobe Acrobat Sign for attachments]** möjlighet att lägga till filer som är kopplade till ett adaptivt formulär i motsvarande [!DNL Adobe Acrobat Sign] dokumentet har skickats för signering.

1. Välj **[!UICONTROL Connect to Adobe Acrobat Sign]**. När du uppmanas att ange autentiseringsuppgifter anger du **användarnamn** och **lösenord** av kontot som användes när [!DNL Adobe Acrobat Sign] program. När du ombeds att bekräfta har du åtkomst till `your developer account`, klicka **[!UICONTROL Allow Access]**. Om autentiseringsuppgifterna är korrekta och du tillåter [!DNL AEM Forms] för att få tillgång till [!DNL Adobe Acrobat Sign] utvecklarkontot visas ett meddelande om att åtgärden lyckades.

   ![Konfigurationen av Adobe Acrobat Sign Cloud lyckades](assets/adobe-sign-cloud-configuration-success.png)

1. Välj **[!UICONTROL Create]** för att skapa [!DNL Adobe Acrobat Sign] konfiguration.

1. Välj konfigurationen och klicka på **[!UICONTROL Publish]**, markera konfigurationen och klicka på **[!UICONTROL Publish]**. Konfigurationen replikeras till motsvarande publiceringsmiljöer.

1. Upprepa alla ovanstående steg på utvecklaren, scenen och produktionsinstanserna (beroende på vad som återstår) för att slutföra konfigurationen [!DNL Adobe Acrobat Sign] med [!DNL AEM Forms] för din miljö.

Nu kan du [använda lägg till Adobe Acrobat Sign-fält i ett adaptivt formulär](working-with-adobe-sign.md). Se till att du lägger till konfigurationsbehållaren som används för Cloud Servicen i alla adaptiva Forms som aktiveras för [!DNL Adobe Acrobat Sign]. Du kan ange en konfigurationsbehållare bland egenskaperna för ett adaptivt formulär.

>[!NOTE]
>
> Om du vill konfigurera Adobe Sign-sandlådan kan du följa samma konfigurationssteg som beskrivs i [Adobe Sign](#adobe-sign).

## Koppla AEM Forms till Adobe Acrobat Sign Solutions för myndigheter {#adobe-acrobat-sign-for-government}

Att knyta AEM Forms till Adobe Acrobat Sign Solutions för myndigheter är en flerstegsprocess. Den innehåller följande uppgifter:

* Skapar omdirigerings-URL för dina AEM
* Dela omdirigerings-URL:er och omfattningar med Adobe Sign Solutions for Government-teamet
* Få inloggningsuppgifter från Adobe Sign team
* Använda inloggningsuppgifterna för att ansluta AEM Forms till Adobe Acrobat Sign Solutions för myndigheter

![Adobe Sign Government Workflow](/help/forms/assets/adobe-acrobat-sign-govt-workflow.png)


AEM Forms as a Cloud Service tillhandahåller utvecklings-, scen- och produktionsmiljöer. Du kan börja med att ansluta utvecklingsmiljön för med Adobe Acrobat Sign Solutions för myndigheter och senare koppla samman scen- och produktionsmiljöerna.

### Innan du börjar {#prerequisites-for-adobe-sign-for-acrobat-sign-for-government}

Innan du börjar ansluta AEM Forms med Adobe Acrobat Sign Solution måste du se till att [Adobe Acrobat Sign Solutions för myndigheter](https://opensource.adobe.com/acrobat-sign/signgov/gstarted.html#account-provisioning) kontot har etablerats.


### Anslut AEM Forms as a Cloud Service till Adobe Acrobat Sign Solutions för myndigheter {#connect-adobe-acrobat-sign-for-government}

#### Skapa en omdirigerings-URL för AEM

1. På Forms as a Cloud Service författarinstans går du till **[!UICONTROL Tools]** ![hammare](assets/hammer.png) > **[!UICONTROL General]** > **[!UICONTROL Configuration Browser]**.
1. På **[!UICONTROL Configuration Browser]** sida, markera **[!UICONTROL Create]**.
1. I **[!UICONTROL Create Configuration]** dialogruta, ange **[!UICONTROL Title]** för konfigurationen, aktivera **[!UICONTROL Cloud Configurations]** och markera **[!UICONTROL Create]**. Den skapar en konfigurationsbehållare för lagring av Cloud Service. Kontrollera att mappnamnet inte innehåller något utrymme.
1. Navigera till **[!UICONTROL Tools]** ![hammare](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Acrobat Sign]** och öppna konfigurationsbehållaren som du skapade i föregående steg. När du skapar ett adaptivt formulär anger du behållarnamnet i dialogrutan **[!UICONTROL Configuration Container]** fält.
1. Välj på konfigurationssidan **[!UICONTROL Create]** att skapa [!DNL Adobe Acrobat Sign] i AEM Forms.
1. Kopiera URL-adressen till det aktuella webbläsarfönstret till ett anteckningsblock och ta bort `/ui#/aem` från webbadressen. Denna URL kallas `re-direct URL`.
I nästa avsnitt delar du `re-direct URL` och `Scopes` med Adobe Sign team och begära inloggningsuppgifter (klient-ID och klienthemlighet).

#### Dela omdirigerings-URL:en och omfattningarna med Adobe Sign team och få inloggningsuppgifter

Adobe Acrobat Sign for Government Solutions-teamet kräver `re-direct URL` och vilka scope som ska aktiveras för ditt Adobe Acrobat Sign-program (se nedan) för att generera autentiseringsuppgifter (klient-ID och klienthemlighet) som gör att du kan ansluta AEM Forms till Adobe Acrobat Sign Solutions för myndigheter.

Dela `scopes` (visas nedan) och `re-direct URL` skapat och noterat i sista steget i föregående avsnitt med en representant för Adobe Acrobat Sign for Government Solution ([Adobe Professional Services teammedlem](https://opensource.adobe.com/acrobat-sign/signgov/gstarted.html#password)).

**_Omfång_**

* [!DNL aggrement_read]
* [!DNL aggrement_write]
* [!DNL aggrement_send]
* [!DNL widget_read]
* [!DNL widget_write]
* [!DNL workflow_read]
* [!DNL offline_access]

Representanten genererar och delar uppgifter med dig. I nästa avsnitt använder du inloggningsuppgifterna (Klient-ID och Klienthemlighet) för att ansluta AEM Forms till Adobe Acrobat Sign Solutions för myndigheter.

#### Använd de inloggningsuppgifter som tas emot för att ansluta AEM Forms till Adobe Acrobat Sign Solutions för offentlig sektor

1. Öppna `re-direct URL` i webbläsaren. Du skapade och antecknade i `re-direct URL` i det sista steget i [skapa en omdirigerings-URL för din AEM](#create-a-redirect-url-for-your-aem-instance) -avsnitt.

1. I **[!UICONTROL General]** -fliken i **[!UICONTROL Create Adobe Sign Configuration]** sida, ange en **[!UICONTROL Name]** för konfigurationen och välj **[!UICONTROL Next]**. Du kan också ange en **[!UICONTROL Title]** och bläddra för att välja **[!UICONTROL Thumbnail]** för konfigurationen. Klicka på **[!UICONTROL Next]**.

1. I **[!UICONTROL Settings]** -fliken i **[!UICONTROL Create Adobe Sign Configuration]** sida, för **[!UICONTROL Select solution]** alternativ, markera [!DNL Adobe Acrobat Sign Solutions for Government].


   ![Adobe Acrobat Sign Solutions för myndigheter](assets/adobe-sign-for-govt.png)

1. I **[!UICONTROL Email]** anges den e-postadress som är kopplad till ditt Adobe Acrobat Sign Solutions for Government-konto.

1. I **[!UICONTROL Settings]** tab,
   * den **[!UICONTROL OAuth URL]** -fältet innehåller standardwebbadressen som innehåller Adobe Sign-databasdelning. URL-formatet är:

     `https://<shard>/api/gateway/adobesignauthservice/api/v1/authorize`

     Till exempel:
     `https://secure.na1.adobesign.us/api/gateway/adobesignauthservice/api/v1/authorize`

   * den **[!UICONTROL Access token URL]** -fältet innehåller standardwebbadressen som innehåller Adobe Sign-databasdelning. URL-formatet är:

     `https://<shard>/api/gateway/adobesignauthservice/api/v1/token`

     Till exempel:
     `https://secure.na1.adobesign.us/api/gateway/adobesignauthservice/api/v1/token`

   där:

   **na1** refererar till standarddatabasfragmentet. Du kan ändra värdet för databasdelningen. Se till att [!DNL  Adobe Acrobat Sign] Molnkonfigurationer pekar mot [korrigera Shard](https://helpx.adobe.com/sign/using/identify-account-shard.html).

   >[!NOTE]
   >
   > * När du har loggat in på ditt Adobe Sign-konto går du till **[!UICONTROL Acrobat Sign API]** > **[!UICONTROL API Information]** > **[!UICONTROL REST API Methods Documentation]** > **[!UICONTROL OAuth Access Token]** för att få tillgång till information om Adobe Sign Autentiserings-URL och Access Token-URL.

1. Använd autentiseringsuppgifterna som delas av Adobe Acrobat Sign för handläggare ([Adobe Professional Services teammedlem]) i föregående avsnitt som [**[!UICONTROL Client ID]** och **[!UICONTROL Client Secret]**].

1. Välj **[!UICONTROL Enable Adobe Acrobat Sign for attachments]** möjlighet att lägga till filer som är kopplade till ett adaptivt formulär i motsvarande [!DNL Adobe Acrobat Sign] dokumentet har skickats för signering.

1. Välj **[!UICONTROL Connect to Adobe Sign]**. Ange användarnamn och lösenord för kontot som används när du skapar inloggningsuppgifter [!DNL Adobe Acrobat Sign] program. När du ombeds att bekräfta åtkomsten för `your developer account`, klicka **[!UICONTROL Allow Access]**. Om autentiseringsuppgifterna är korrekta och du tillåter [!DNL AEM Forms] för att få tillgång till [!DNL Adobe Acrobat Sign] utvecklarkontot visas ett meddelande om att åtgärden lyckades.

   ![Konfigurationen av Adobe Acrobat Sign Cloud lyckades](assets/adobe-sign-cloud-configuration-success.png)

   <!-- > When prompted for credentials, provide username and password of the account used while creating [!DNL Adobe Acrobat Sign] application. When asked to confirm access for `your developer account`, Click **[!UICONTROL Allow Access]**. -->

1. Välj **[!UICONTROL Create]** för att skapa konfigurationen.

1. Välj konfigurationen och klicka på **[!UICONTROL Publish]**, markera konfigurationen och klicka på **[!UICONTROL Publish]**. Konfigurationen replikeras till motsvarande publiceringsmiljöer.

1. Upprepa alla ovanstående steg på utvecklaren, scenen och produktionsinstanserna (beroende på vad som återstår) för att slutföra konfigurationen [!DNL Adobe Acrobat Sign Solutions for Government] med [!DNL AEM Forms] för din miljö.

Nu kan du [använda lägg till Adobe Acrobat Sign-fält i ett adaptivt formulär](working-with-adobe-sign.md) eller [AEM](/help/forms/aem-forms-workflow-step-reference.md#sign-document-step-sign-document-step). Se till att du lägger till konfigurationsbehållaren som används för konfigurationen av Cloud Servicen i alla adaptiva Forms som aktiveras för [!DNL Adobe Acrobat Sign]. Du kan ange en konfigurationsbehållare bland egenskaperna för ett adaptivt formulär.

## Konfigurera [!DNL Adobe Acrobat Sign] schemaläggaren för att synkronisera signeringsstatusen {#configure-adobe-sign-scheduler-to-sync-the-signing-status}

AEM Forms as a Cloud Service tillhandahåller en schemaläggningstjänst som kontrollerar signerarnas status med definierade intervall. Scenerna där du konfigurerar schemaläggningstjänsten:

* Om du [Skicka formuläret (när alla mottagare har slutfört signeringsceremonin)](/help/forms/working-with-adobe-sign.md#select-adobe-sign-cloud-service-and-signing-order) om du vill signera ett dokument skickas formuläret bara när alla signerare har signerat formuläret.
* Om du använder [Signera steget i ett AEM arbetsflöde](/help/forms/aem-forms-workflow-step-reference.md#sign-document-step) om du vill signera ett dokument väntar signeringssteget på att alla signerare ska signera dokumentet innan nästa steg i arbetsflödet.

Som standard är [!DNL Adobe Acrobat Sign] Tjänsten Scheduler kontrollerar (enkäter) signerarens svar efter var 24:e timme. Du kan ändra standardintervallet för din miljö.

Om du vill ändra standardintervallet anger du en [cron-uttryck](https://en.wikipedia.org/wiki/Cron#CRON_expression) för **sign.status.exp** egenskapen för **Konfigurationstjänst för Adobe Acrobat Sign** konfiguration.

Om du till exempel vill köra konfigurationstjänsten varje dag klockan 00:00 anger du **sign.status.exp** egenskapen för **Konfigurationstjänst för Adobe Acrobat Sign** konfiguration som ska anges `0 0 0 1/1 * ? *`. I följande JSON-fil visas exemplet som ska köra konfigurationstjänsten varje dag klockan 00:00:

```json
{
  "sign.status.exp":"0 0 0 1/1 * ? *"
}
```

Så här anger du värden för en konfiguration: [Generera OSGi-konfigurationer med AEM SDK](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#generating-osgi-configurations-using-the-aem-sdk-quickstart)och [distribuera konfigurationen](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#deployment-process) till din Cloud Service.


>[!MORELIKETHIS]
>
>* [E-signera ett formulär med hjälp av klottersignaturer](/help/forms/signing-forms-using-scribble.md)
>* [Bästa tillvägagångssätt för att använda Adobe Acrobat Sign med Adaptiv Forms](https://medium.com/adobetech/using-adobe-sign-to-e-sign-an-adaptive-form-heres-the-best-way-to-do-it-dc3e15f9b684)
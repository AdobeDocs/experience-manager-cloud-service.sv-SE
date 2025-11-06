---
title: Hur integrerar man Adobe Acrobat Sign med AEM Forms?
description: Lär dig hur du konfigurerar Adobe Acrobat Sign för [!DNL AEM Forms] as a Cloud Service?
feature: Adaptive Forms, Acrobat Sign
role: Admin, User
level: Intermediate
exl-id: 609c3072-1c3d-43fa-898a-b4e62db8483b
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '2024'
ht-degree: 0%

---

# Anslut [!DNL AEM Forms] as a Cloud Service med [!DNL Adobe Acrobat Sign] {#integrate-adobe-sign-with-aem-forms}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/adobe-sign-integration-adaptive-forms.html#adobe-acrobat-sign-for-government) |
| AEM as a Cloud Service | Den här artikeln |

[!DNL Adobe Acrobat Sign] aktiverar e-signaturarbetsflöden för adaptiva Forms- och AEM-arbetsflöden. E-signaturer förbättrar arbetsflödena för att bearbeta dokument inom juridik, försäljning, löneadministration, personaladministration och många andra områden.

I ett typiskt [!DNL Adobe Acrobat Sign]- och Adaptivt Forms-scenario fyller en användare i ett adaptivt formulär som kan användas för en tjänst. Till exempel kan en kreditkortsansökan och en medborgare få förmåner. När en användare fyller i, skickar och signerar ansökningsformuläret skickas formuläret till tjänsteleverantören för ytterligare åtgärder. Tjänsteleverantören granskar programmet och använder [!DNL Adobe Acrobat Sign] för att markera programmet som godkänt. AEM Forms stöder både Adobe Acrobat Sign och Adobe Acrobat Sign Solutions for Government. Beroende på licens och krav kan du integrera eller ansluta AEM Forms med någon av lösningarna:

* [Anslut AEM Forms till Adobe Acrobat Sign](#adobe-sign)
* [Koppla AEM Forms till Adobe Acrobat Sign Solutions för myndigheter](#adobe-acrobat-sign-for-government)

## Anslut AEM Forms till Adobe Acrobat Sign {#adobe-sign}

Om du vill ansluta **[!DNL AEM Forms]** till **[!DNL Adobe Acrobat Sign]** ställer du in programvaran och kontona som listas i avsnittet Krav och konfigurerar Adobe Sign Cloud Service i Forms as a Cloud Service Author och Publish:

### Krav för att ansluta AEM Forms till Adobe Acrobat Sign {#prerequisites-for-adobe-sign}

Du behöver följande konfiguration för att integrera [!DNL Adobe Acrobat Sign] med [!DNL AEM Forms]:

1. Ett aktivt [Adobe Acrobat Sign-utvecklarkonto.](https://www.adobe.com/acrobat/business/developer-form.html)
1. Ett [Adobe Acrobat Sign API-program](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/create_app.md).
1. Autentiseringsuppgifter (klient-ID och klienthemlighet) för API-programmet [!DNL Adobe Acrobat Sign].
1. (Endast för myndighets-ID-baserad autentisering) [Aktivera autentiseringsmetoden](https://helpx.adobe.com/sign/using/adobesign-authentication-government-id.html#AuditReport) för autentisering av myndighets-ID.

### Koppla samman AEM Forms Author och publicera förekomster med Adobe Acrobat Sign {#configure-adobe-sign-with-aem-forms}

När förutsättningarna är uppfyllda utför du följande steg för att konfigurera [!DNL Adobe Acrobat Sign] med [!DNL AEM Forms] på författarinstanserna.

1. I AEM Forms-författarinstans går du till **[!UICONTROL Tools]** ![hammer](assets/hammer.png) > **[!UICONTROL General]** > **[!UICONTROL Configuration Browser]**.
1. Välj **[!UICONTROL Configuration Browser]** på sidan **[!UICONTROL Create]**.
1. I dialogrutan **[!UICONTROL Create Configuration]** anger du **[!UICONTROL Title]** för konfigurationen, aktiverar **[!UICONTROL Cloud Configurations]** och väljer **[!UICONTROL Create]**. Den skapar en konfigurationsbehållare för lagring av molntjänster. Kontrollera att mappnamnet inte innehåller något utrymme.
1. Navigera till **[!UICONTROL Tools]** ![hammer](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Acrobat Sign]** och öppna konfigurationsbehållaren som du skapade i föregående steg.

   >[!NOTE]
   >
   >När du skapar ett adaptivt formulär anger du behållarnamnet i fältet **[!UICONTROL Configuration Container]**.

1. På konfigurationssidan väljer du **[!UICONTROL Create]** för att skapa [!DNL Adobe Acrobat Sign]-konfigurationen i AEM Forms.
1. På fliken **[!UICONTROL General]** på sidan **[!UICONTROL Create Adobe Acrobat Sign Configuration]** anger du **[!UICONTROL Name]** för konfigurationen och väljer **[!UICONTROL Next]**. Du kan också ange en **[!UICONTROL Title]** och bläddra för att välja en **[!UICONTROL Thumbnail]** för konfigurationen.

1. Nu kan du **[!UICONTROL Select solution]** välja [!DNL Adobe Acrobat Sign].

   <!--![Adobe Acrobat Sign Solutions](assets/adobe-sign-solution.png)-->
   ![Adobe Acrobat Sign Solutions-konfiguration](assets/adobe-sign-solution-config.png)

<!--

[create URL](#create-a-redirect-url-for-your-aem-instance)
 -->

1. Kopiera URL:en som finns i det aktuella webbläsarfönstret till ett anteckningsblock och ta bort delen `/ui#/aem` från URL:en. Den ändrade URL:en krävs sedan för att konfigurera [!DNL Adobe Acrobat Sign]-programmet med [!DNL AEM Forms], i ett senare steg. Välj **[!UICONTROL Next]**.

1. På fliken **[!UICONTROL Settings]**
   * fältet **[!UICONTROL OAuth URL]** innehåller standard-URL:en som innehåller Adobe Sign-databasdelning. URL-formatet är:

     `https://<shard>/public/oauth/v2`

     Till exempel:
     `https://secure.na1.echosign.com/public/oauth/v2`

   * fältet **[!UICONTROL Access token URL]** innehåller standard-URL:en som innehåller Adobe Sign-databasdelning. URL-formatet är:

     `https://<shard>/oauth/v2/token`

     Till exempel:
     `https://api.na1.echosign.com/oauth/v2/token`

   där:

   **na1** refererar till standarddatabasdelningen. Du kan ändra värdet för databasdelningen. Kontrollera att [!DNL &#x200B; Adobe Acrobat Sign]-molnkonfigurationerna pekar på [rätt kort](https://helpx.adobe.com/sign/using/identify-account-shard.html).

   >[!NOTE]
   >
   >* Håll sidan **Skapa Adobe Acrobat Sign-konfiguration** öppen. Stäng den inte. Du kan hämta **klient-ID** och **klienthemlighet** efter att OAuth-inställningarna för [!DNL Adobe Acrobat Sign]-programmet har konfigurerats, vilket beskrivs i kommande steg.
   >* När du har loggat in på ditt Adobe Sign-konto går du till **[!UICONTROL Acrobat Sign API]** > **[!UICONTROL API Information]** > **[!UICONTROL REST API Methods Documentation]** > **[!UICONTROL OAuth Access Token]** för att komma åt information som rör Adobe Sign OAuth-URL och Access Token URL.

1. Konfigurera OAuth-inställningar för programmet [!DNL Adobe Acrobat Sign]:

   1. Öppna ett webbläsarfönster och logga in på ditt [!DNL Adobe Acrobat Sign]-utvecklarkonto.
   1. Markera programmet som är konfigurerat för [!DNL AEM Forms] och välj **[!UICONTROL Configure OAuth for Application]**.
   1. I rutan **[!UICONTROL Redirect URL]** lägger du till den URL som kopierades i ett tidigare steg (steg 8) och klickar på **[!UICONTROL Save]**.
   1. Aktivera följande scope för programmet [!DNL Adobe Acrobat Sign] och klicka på **[!UICONTROL Save]**.

   * [!DNL aggrement_read]
   * [!DNL aggrement_write]
   * [!DNL aggrement_send]
   * [!DNL widget_read]
   * [!DNL widget_write]
   * [!DNL workflow_read]

   >[!NOTE]
   > Du kan ändra omfattningsmodifieraren från `self` till `account` direkt från AEM-gränssnittet enligt steg 12.

   Stegvis information om hur du konfigurerar OAuth-inställningar för ett [!DNL Adobe Acrobat Sign]-program och hämtar nycklarna finns i [Konfigurera autentiseringsinställningar för programmets &#x200B;](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/configure_oauth.md) utvecklardokumentation.

   ![OAuth-konfiguration](/help/forms/assets/oauthconfig-new.png)

1. Gå tillbaka till sidan **[!UICONTROL Create Adobe Acrobat Sign Configuration]**. På fliken **[!UICONTROL Settings]** anger du [**[!UICONTROL Client ID]** (kallas även program-ID) och **[!UICONTROL Client Secret]**]. Använd [Klient-ID och Klienthemlighet för det Adobe Acrobat Sign-program](https://opensource.adobe.com/acrobat-sign/developer_guide/helloworld.html#get-the-app-id-and-secret) som du skapade i föregående steg.

1. I avsnittet [!UICONTROL Authorization Scope] kan du ändra scopen till antingen &quot;account&quot; eller &quot;self&quot; genom att lägga till prefixet &quot;self&quot; eller &quot;account&quot; i scopen efter behov.
   ![Auktoriseringsomfång](/help/forms/assets/authorization-scope.png)

1. Välj alternativet **[!UICONTROL Enable Adobe Acrobat Sign for attachments]** om du vill lägga till filer som är kopplade till ett adaptivt formulär i motsvarande [!DNL Adobe Acrobat Sign] -dokument som skickats för signering.

1. Välj **[!UICONTROL Connect to Adobe Acrobat Sign]**. När du uppmanas att ange autentiseringsuppgifter anger du **användarnamn** och **lösenord** för kontot som används när [!DNL Adobe Acrobat Sign]-programmet skapas. Åtkomst till `your developer account`, klicka på **[!UICONTROL Allow Access]** när du uppmanas att bekräfta. Om inloggningsuppgifterna är korrekta och du tillåter [!DNL AEM Forms] att få åtkomst till ditt [!DNL Adobe Acrobat Sign]-utvecklarkonto, visas ett meddelande om att åtgärden lyckades som det nedan.

   ![Konfigurationen av Adobe Acrobat Sign Cloud lyckades](assets/adobe-sign-cloud-configuration-success.png)

1. Välj **[!UICONTROL Create]** om du vill skapa [!DNL Adobe Acrobat Sign]-konfigurationen.

1. Markera konfigurationen och klicka på **[!UICONTROL Publish]**, markera konfigurationen och klicka på **[!UICONTROL Publish]**. Konfigurationen replikeras till motsvarande publiceringsmiljöer.

1. Upprepa alla ovanstående steg på din utvecklare, scen och produktionsinstanser (beroende på vad som återstår) för att slutföra konfigurationen av [!DNL Adobe Acrobat Sign] med [!DNL AEM Forms] för din miljö.

Nu kan du [använda för att lägga till Adobe Acrobat Sign-fält i ett anpassat formulär](working-with-adobe-sign.md). Se till att du lägger till konfigurationsbehållaren som används för Cloud Service i alla adaptiva Forms som aktiveras för [!DNL Adobe Acrobat Sign]. Du kan ange en konfigurationsbehållare bland egenskaperna för ett adaptivt formulär.

>[!NOTE]
>
> Om du vill konfigurera Adobe Sign-sandlådan kan du följa samma konfigurationssteg som beskrivs i [Adobe Sign](#adobe-sign).

#### Felsökning {#resolve-config-error}

När du ansluter [!DNL Adobe Acrobat Sign] till [!DNL AEM Forms] och hittar ett fel `Unable to authorize access because the client configuration is invalid: invalid_request` som visas i bilden nedan. Du löser detta genom att följa stegen nedan:

![Konfigurationsfel](/help/forms/assets/config_error_sign.png)

1. Kopiera URL:en som finns i det aktuella webbläsarfönstret till ett anteckningsblock och ta bort delen `/ui#/aem` från URL:en.
1. Öppna ett webbläsarfönster och logga in på ditt [!DNL Adobe Acrobat Sign]-utvecklarkonto.
1. Markera programmet som är konfigurerat för [!DNL AEM Forms] och välj **[!UICONTROL Configure OAuth for Application]**.
1. I rutan **[!UICONTROL Redirect URL]** lägger du till den URL som kopierades i ett tidigare steg och klickar på **[!UICONTROL Save]**.

## Koppla AEM Forms till Adobe Acrobat Sign Solutions för myndigheter {#adobe-acrobat-sign-for-government}

Att knyta AEM Forms till Adobe Acrobat Sign Solutions för myndigheter är en flerstegsprocess. Den innehåller följande uppgifter:

* Skapa omdirigerings-URL för dina AEM-instanser
* Dela omdirigerings-URL:er och omfattningar med Adobe Sign-lösningar för myndighetsteamet
* Få inloggningsuppgifter från Adobe Sign-teamet
* Använda inloggningsuppgifterna för att ansluta AEM Forms till Adobe Acrobat Sign Solutions för myndigheter

![Adobe Sign - arbetsflöde för myndigheter](/help/forms/assets/adobe-acrobat-sign-govt-workflow.png)


AEM Forms as a Cloud Service erbjuder utvecklings-, scen- och produktionsmiljöer. Du kan börja med att ansluta utvecklingsmiljön för med Adobe Acrobat Sign Solutions för myndigheter och senare koppla samman scen- och produktionsmiljöerna.

### Innan du börjar {#prerequisites-for-adobe-sign-for-acrobat-sign-for-government}

Innan du börjar ansluta AEM Forms med Adobe Acrobat Sign Solution måste du kontrollera att ditt [Adobe Acrobat Sign Solutions for Government](https://opensource.adobe.com/acrobat-sign/signgov/gstarted.html#account-provisioning)-konto har etablerats.


### Koppla AEM Forms as a Cloud Service till Adobe Acrobat Sign Solutions för myndigheter {#connect-adobe-acrobat-sign-for-government}

#### Skapa en omdirigerings-URL för din AEM-instans

1. På författarinstansen för Forms as a Cloud Service går du till **[!UICONTROL Tools]** ![hammer](assets/hammer.png) > **[!UICONTROL General]** > **[!UICONTROL Configuration Browser]**.
1. Välj **[!UICONTROL Configuration Browser]** på sidan **[!UICONTROL Create]**.
1. I dialogrutan **[!UICONTROL Create Configuration]** anger du **[!UICONTROL Title]** för konfigurationen, aktiverar **[!UICONTROL Cloud Configurations]** och väljer **[!UICONTROL Create]**. Den skapar en konfigurationsbehållare för lagring av molntjänster. Kontrollera att mappnamnet inte innehåller något utrymme.
1. Navigera till **[!UICONTROL Tools]** ![hammer](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Acrobat Sign]** och öppna konfigurationsbehållaren som du skapade i föregående steg. När du skapar ett adaptivt formulär anger du behållarnamnet i fältet **[!UICONTROL Configuration Container]**.
1. På konfigurationssidan väljer du **[!UICONTROL Create]** för att skapa [!DNL Adobe Acrobat Sign]-konfigurationen i AEM Forms.
1. Kopiera URL-adressen för det aktuella webbläsarfönstret till ett anteckningsblock och ta bort `/ui#/aem` från URL-adressen. Denna URL kallas `re-direct URL`.
I nästa avsnitt delar du `re-direct URL` och `Scopes` med Adobe Sign-teamet och begär inloggningsuppgifter (klient-ID och klienthemlighet).

#### Dela omdirigerings-URL:en och omfattningarna med Adobe Sign-teamet och få inloggningsuppgifter

Adobe Acrobat Sign for Government Solutions-teamet kräver att `re-direct URL` och vissa omfattningar är aktiverade för ditt Adobe Acrobat Sign-program (se nedan) för att generera autentiseringsuppgifter (klient-ID och klienthemlighet) som gör att du kan ansluta AEM Forms till Adobe Acrobat Sign Solutions för myndigheter.

Dela `scopes` (visas nedan) och `re-direct URL` skapade och noterade det sista steget i föregående avsnitt med din Adobe Acrobat Sign for Government Solution-representant ([Adobe Professional Services-teammedlem](https://opensource.adobe.com/acrobat-sign/signgov/gstarted.html#password)).

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

1. Öppna `re-direct URL` i webbläsaren. Du skapade och noterade `re-direct URL` i det sista steget i avsnittet [Skapa en omdirigerings-URL i din AEM-instans](#create-a-redirect-url-for-your-aem-instance).

1. På fliken **[!UICONTROL General]** på sidan **[!UICONTROL Create Adobe Sign Configuration]** anger du **[!UICONTROL Name]** för konfigurationen och väljer **[!UICONTROL Next]**. Du kan också ange en **[!UICONTROL Title]** och bläddra för att välja en **[!UICONTROL Thumbnail]** för konfigurationen. Klicka på **[!UICONTROL Next]**.

1. Välj **[!UICONTROL Settings]** för alternativet **[!UICONTROL Create Adobe Sign Configuration]** på fliken **[!UICONTROL Select solution]** på sidan [!DNL Adobe Acrobat Sign Solutions for Government].


   ![Adobe Acrobat Sign Solutions för offentlig sektor](assets/adobe-sign-for-govt.png)

1. I fältet **[!UICONTROL Email]** anger du den e-postadress som är kopplad till ditt Adobe Acrobat Sign Solutions for Government-konto.

1. På fliken **[!UICONTROL Settings]**
   * fältet **[!UICONTROL OAuth URL]** innehåller standard-URL:en som innehåller Adobe Sign-databasdelning. URL-formatet är:

     `https://<shard>/api/gateway/adobesignauthservice/api/v1/authorize`

     Till exempel:
     `https://secure.na1.adobesign.us/api/gateway/adobesignauthservice/api/v1/authorize`

   * fältet **[!UICONTROL Access token URL]** innehåller standard-URL:en som innehåller Adobe Sign-databasdelning. URL-formatet är:

     `https://<shard>/api/gateway/adobesignauthservice/api/v1/token`

     Till exempel:
     `https://secure.na1.adobesign.us/api/gateway/adobesignauthservice/api/v1/token`

   där:

   **na1** refererar till standarddatabasdelningen. Du kan ändra värdet för databasdelningen. Kontrollera att [!DNL &#x200B; Adobe Acrobat Sign]-molnkonfigurationerna pekar på [rätt kort](https://helpx.adobe.com/sign/using/identify-account-shard.html).

   >[!NOTE]
   >
   > * När du har loggat in på ditt Adobe Sign-konto går du till **[!UICONTROL Acrobat Sign API]** > **[!UICONTROL API Information]** > **[!UICONTROL REST API Methods Documentation]** > **[!UICONTROL OAuth Access Token]** för att få tillgång till information om Adobe Sign-autentiserings-URL och åtkomsttoken-URL.

1. Använd de inloggningsuppgifter som delas av Adobe Acrobat Sign for Government Solution manager ([Adobe Professional Services team member]) i föregående avsnitt som [**[!UICONTROL Client ID]** och **[!UICONTROL Client Secret]**].

1. Välj alternativet **[!UICONTROL Enable Adobe Acrobat Sign for attachments]** om du vill lägga till filer som är kopplade till ett adaptivt formulär i motsvarande [!DNL Adobe Acrobat Sign] -dokument som skickats för signering.

1. Välj **[!UICONTROL Connect to Adobe Sign]**. När du uppmanas att ange autentiseringsuppgifter anger du användarnamn och lösenord för kontot som används när programmet [!DNL Adobe Acrobat Sign] skapas. När du uppmanas att bekräfta åtkomst för `your developer account` klickar du på **[!UICONTROL Allow Access]**. Om inloggningsuppgifterna är korrekta och du tillåter [!DNL AEM Forms] att få åtkomst till ditt [!DNL Adobe Acrobat Sign]-utvecklarkonto, visas ett meddelande om att åtgärden lyckades som det nedan.

   ![Konfigurationen av Adobe Acrobat Sign Cloud lyckades](assets/adobe-sign-cloud-configuration-success.png)

   <!-- 
      > When prompted for credentials, provide username and password of the account used while creating [!DNL Adobe Acrobat Sign] application. When asked to confirm access for `your developer account`, Click **[!UICONTROL Allow Access]**. 
      -->

1. Välj **[!UICONTROL Create]** för att skapa konfigurationen.

1. Markera konfigurationen och klicka på **[!UICONTROL Publish]**, markera konfigurationen och klicka på **[!UICONTROL Publish]**. Konfigurationen replikeras till motsvarande publiceringsmiljöer.

1. Upprepa alla ovanstående steg på din utvecklare, scen och produktionsinstanser (beroende på vad som återstår) för att slutföra konfigurationen av [!DNL Adobe Acrobat Sign Solutions for Government] med [!DNL AEM Forms] för din miljö.

Nu kan du [använda Adobe Acrobat Sign-fält i ett adaptivt formulär](working-with-adobe-sign.md) eller [AEM Workflow](/help/forms/aem-forms-workflow-step-reference.md#sign-document-step-sign-document-step). Se till att du lägger till konfigurationsbehållaren som används för Cloud Service-konfigurationen i alla adaptiva Forms som aktiveras för [!DNL Adobe Acrobat Sign]. Du kan ange en konfigurationsbehållare bland egenskaperna för ett adaptivt formulär.

## Konfigurera schemaläggaren för [!DNL Adobe Acrobat Sign] för att synkronisera signeringsstatusen {#configure-adobe-sign-scheduler-to-sync-the-signing-status}

AEM Forms as a Cloud Service tillhandahåller en schemaläggningstjänst som kontrollerar signerarnas status med definierade intervall. Scenerna där du konfigurerar schemaläggningstjänsten:

* Om du använder [Skicka formuläret (när alla mottagare har slutfört signeringsceremonin)](/help/forms/working-with-adobe-sign.md#select-adobe-sign-cloud-service-and-signing-order) för att signera ett dokument, skickas formuläret endast när alla signerare har signerat formuläret.
* Om du använder [Signeringssteget i ett AEM-arbetsflöde](/help/forms/aem-forms-workflow-step-reference.md#sign-document-step) för att signera ett dokument väntar signeringssteget på att alla signerare ska signera dokumentet innan du fortsätter till nästa steg i arbetsflödet.

Som standard kontrollerar [!DNL Adobe Acrobat Sign] Scheduler Services (enkäter) signerarens svar efter var 24:e timme. Du kan ändra standardintervallet för din miljö.

Om du vill ändra standardintervallet anger du ett [cron-uttryck](https://en.wikipedia.org/wiki/Cron#CRON_expression) för egenskapen **sign.status.exp** i konfigurationen för **Adobe Acrobat Sign Configuration Service**.

Om du till exempel vill köra konfigurationstjänsten dagligen klockan 00:00 ställer du in egenskapen **sign.status.exp** för konfigurationen **Adobe Acrobat Sign Configuration Service** så att den anger `0 0 0 1/1 * ? *`. I följande JSON-fil visas exemplet för att köra konfigurationstjänsten varje dag klockan 00:00::00

```json
{
  "sign.status.exp":"0 0 0 1/1 * ? *"
}
```

[Generera OSGi-konfigurationer med AEM SDK](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#generating-osgi-configurations-using-the-aem-sdk-quickstart) och [distribuera konfigurationen](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#deployment-process) till din Cloud Service-instans om du vill ange värden för en konfiguration.

## Vanliga frågor

* **F: Kan jag återge Adobe Sign GovCloud-signatursidan i en iframe?**
* **S:** Ja, du kan återge Adobe Sign GovCloud-signatursidan i en iframe.

>[!MORELIKETHIS]
>
>* [E-signera ett formulär med signaturer via skript](/help/forms/signing-forms-using-scribble.md)
>* [Bästa tillvägagångssätt för att använda Adobe Acrobat Sign med Adaptiv Forms](https://medium.com/adobetech/using-adobe-sign-to-e-sign-an-adaptive-form-heres-the-best-way-to-do-it-dc3e15f9b684)

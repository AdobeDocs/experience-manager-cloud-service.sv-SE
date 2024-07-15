---
title: Integrering av Adobe Workfront Fusion med AEM Forms Submission
description: Med Adobe Workfront Fusion kan du fokusera på nya uppgifter istället för att fokusera på repetitiva uppgifter. Du kan ansluta Adobe Workfront Fusion till ett adaptivt formulär genom att skicka formulär.
keywords: Skicka in ett adaptivt formulär till Adobe Workfront Fusion, Integration of Adobe Workfront Fusion with AEM Forms Submission, Adobe Workfront Fusion with AEM Forms, Workfront Fusion with AEM Forms, Connect Workfront Fusion to AEM Forms, AEM Forms and Workfront Fusion, How to connect Workfront Fusion with AEM Forms?, Connect Workfront Fusion to a Form
topic-tags: author, developer
feature: Adaptive Forms
role: Admin, User
exl-id: d3efb450-a879-40ae-8958-0040f99bdafc
source-git-commit: 559b4afa975dcd2204cd06c95f19ed38da00033e
workflow-type: tm+mt
source-wordcount: '1174'
ht-degree: 0%

---

# Skicka ett anpassat formulär till Adobe Workfront Fusion

<span class="preview"> Funktionen är tillgänglig i ett program för tidig användning. Du kan skriva till aem-forms-ea@adobe.com från ditt officiella e-post-id för att gå med i det tidiga adopterprogrammet och begära åtkomst till funktionen. </span>

[Adobe Workfront Fusion](https://experienceleague.adobe.com/docs/workfront/using/adobe-workfront-fusion/get-started-with-workfront-fusion/workfront-fusion-overview.html) automatiserar processen för att upprepa samma uppgifter, som dokumentgodkännandearbetsflöden, e-postfiltrering och sortering, så att du kan fokusera på nya uppgifter i stället för återkommande. Adobe Workfront Fusion innehåller flera scenarier. Ett scenario består av en serie moduler som utför dataöverföring mellan program och webbtjänster. I ett scenario lägger du till olika steg (moduler) för att automatisera en uppgift.

Med Workfront Fusion kan du till exempel skapa ett scenario där du samlar in data med adaptiv form, bearbetar data och skickar data till ett datalager för arkivering. När ett scenario har konfigurerats utför Workfront Fusion automatiskt uppgifterna när en användare fyller i ett formulär och uppdaterar datalagret sömlöst.

AEM Forms as a Cloud Service har en OOTB-anslutning för att ansluta och skicka ett adaptivt formulär till Adobe Workfront Fusion. Att skicka in ett formulär till Adobe Workfront Fusion kan ge flera fördelar:
* Man kunde smidigt överföra data från inskickade formulär till Workfront Fusion-arbetsflöden.
* Det hjälper till att automatisera olika uppgifter som triggas av inskickade formulär. Det kan vara att initiera projekt, tilldela uppgifter till specifika teammedlemmar, skicka meddelanden och uppdatera projektstatus - allt utan manuell åtgärd.
* Alla inskickade formulär som samlats in i Workfront Fusion kan vara en enda källa till sanning för projektrelaterad information


<!--  AEM as a Cloud Service offers various out of the box submit actions for handling form submissions. You can learn more about these options in the [Adaptive Form Submit Action](/help/forms/configure-submit-actions-core-components.md)  article.-->

>[!VIDEO](https://video.tv.adobe.com/v/3427145/adaptive-forms-adobe-workfront-af-workfront-workfront-aem-forms/?quality=12&learn=on)

## Krav för att integrera AEM Forms med Adobe Workfront Fusion {#prerequisites}

För att upprätta en anslutning mellan Workfront Fusion och AEM Forms krävs följande:

* En giltig [Workfront- och Workfront Fusion-licens](https://experienceleague.adobe.com/docs/workfront/using/adobe-workfront-fusion/get-started-with-workfront-fusion/license-automation-vs-integration.html).
* En AEM användare med behörighet att komma åt [Dev Console](https://my.cloudmanager.adobe.com/) för att [hämta tjänstens autentiseringsuppgifter](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html).

## Integrera AEM Forms med Adobe Workfront Fusion

### 1. Skapa ett Workfront-scenario {#workflow-scenario}

Så här skapar du ett Workfront-scenario:

1. [Skapa ett scenario](#create-scenario)
1. [Lägga till en webbkrok i ett scenario](#add-webhook)
1. [Lägga till en anslutning till en webkrok](#add-connection)

#### Skapa ett scenario {#create-scenario}

Så här skapar du ett scenario:
1. Logga in på ditt [Workfront Fusion-konto](https://app-qa.workfrontfusion.com/).
1. Klicka på **[!UICONTROL Scenarios]** ![Delningsikonen](/help/forms/assets/Smock_ShareAndroid_18_N.svg) i den vänstra panelen.
1. Klicka på **[!UICONTROL Create a new scenario]** i det övre högra hörnet på sidan. En sida för att skapa ett nytt scenario visas på skärmen.
1. Välj **[!UICONTROL New scenario]** i det övre vänstra hörnet på sidan och skriv ett korrekt namn för scenariot.
1. Klicka på frågetecknet och kontrollera att du lägger till den första modulen som **[!UICONTROL AEM Forms]**.

   ![Lägg till en AEM Forms-modul](/help/forms/assets/workfront-aemforms.png)

   Dialogrutan **[!UICONTROL Watch for Form Events]** visas.

   >[!NOTE]
   >
   > Den första modulen måste läggas till som **[!UICONTROL AEM Forms]**.

1. Välj dialogrutan **[!UICONTROL Watch for Form Events]** så visas ett fönster där du kan lägga till en webkrok.

#### Lägg till en webkrok {#add-webhook}

![Lägg till en webkrok](/help/forms/assets/workfront-add-webhook.png)

Så här lägger du till en webkrok:

1. Klicka på **[!UICONTROL Add]** så visas en **[!UICONTROL Add a webhook]**-dialogruta.
1. Ange ett webbkroknamn.

   >[!NOTE]
   >
   > Vi rekommenderar att du noga väljer ditt webkrok-namn eftersom det angivna webkroknamnet visas i AEM.

1. Klicka på **[!UICONTROL Add]** om du vill lägga till en ny anslutning. Dialogrutan **[!UICONTROL Create a Connection]** visas.

#### Lägga till en anslutning till en webkrok {#add-connection}

![Lägg till en anslutning](/help/forms/assets/workfront-add-connection.png)

Så här lägger du till en anslutning:

1. Ange **[!UICONTROL Connection Name]** i dialogrutan **[!UICONTROL Create a Connection]**.

1. Välj **Miljö** och **Typ** i listrutan.

1. Ange **instans-URL**.

   >[!NOTE]
   >
   > Instans-URL är den unika webbadressen som pekar på en viss AEM Forms-instans.

   Du kan hämta inloggningsuppgifterna för [tjänsten från utvecklarkonsolen](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html) som krävs för att skapa en anslutning.

1. Ersätt `ims-na1.adobelogin.com` i **IMS-slutpunkten** med värdet **imsEndpoint** från autentiseringsuppgifterna för tjänsten i utvecklarkonsolen.

   >[!NOTE]
   >
   > Behåll `https://` i textrutan **IMS-slutpunkt** när du lägger till URL:en `imsEndpoint`.

1. Ange följande värden i dialogrutan **[!UICONTROL Create a Connection]**:
   * Ange **klient-ID** med värdet **clientId** från tjänstens autentiseringsuppgifter i utvecklarkonsolen.
   * Ange **Klienthemlighet** med värdet **clientSecret** från tjänstautentiseringsuppgifterna i utvecklarkonsolen.
   * Ange **ID för tekniskt konto** med värdet **id** från tjänstens autentiseringsuppgifter i utvecklarkonsolen.
   * Ange **organisations-ID** med värdet **org** från tjänstens autentiseringsuppgifter i utvecklarkonsolen.
   * **Metaomfång** med värdet **metascopes** från tjänstens autentiseringsuppgifter i utvecklarkonsolen.
   * **Privata nycklar** med värdet **privateKey** från tjänstens autentiseringsuppgifter i utvecklarkonsolen.

   >[!NOTE]
   >
   >* Ta bort `\r\n` från värdet för **Privat nyckel**.
   >  Om värdet för den privata nyckeln till exempel är:
   >`\r\nIJAVO8GDYAOZ9jMA0GCSqGSIb3DQEBCwUAMDAxL\r\nMy1lMTUxODMxLWNtc3RnLWludGVncmF0aW9uLTAw`, sedan efter att `\r\n` tagits bort från den privata nyckeln, skulle nyckeln se ut så här, med båda värdena på en separat rad:
   >
   >   `IJAVO8GDYAOZ9jMA0GCSqGSIb3DQEBCwUAMDAxL`
   >
   >   `My1lMTUxODMxLWNtc3RnLWludGVncmF0aW9uLTAw`
   > 
   >* Du kan också hämta en privat nyckel eller ett certifikat från filen genom att välja knappen **Extrahera** .

1. Klicka på **Fortsätt**.

   Den skapade anslutningen visas i listrutan för **[!UICONTROL Connection]** i dialogrutan **[!UICONTROL Add a webhook]**.

1. Välj den skapade anslutningen **[!UICONTROL Connection]** i listrutan.
1. Klicka på **[!UICONTROL Save]**.
1. Klicka på **[!UICONTROL OK]** och spara ändringarna för scenariot.
1. Aktivera scenariot genom att klicka på knappen PÅ/AV i scenarieredigeraren.

>[!NOTE]
>
> Om du inte aktiverar Workfront-scenariot kan det inte identifieras och om du ställer in skicka-åtgärden på Workfront blir överföringen misslyckad.

### 2. Konfigurera en åtgärd för att skicka ett adaptivt formulär för Workfront Fusion

Du kan konfigurera skicka-åtgärden för Workfront Fusion för:
* [Ny adaptiv Forms](#new-af-submit-action)
* [Befintliga adaptiva formulär](#existing-af-submit-action)

#### Konfigurera åtgärden skicka för det nya adaptiva formuläret för Workfront Fusion {#new-af-submit-action}

Så här konfigurerar du skickaåtgärden för det nya adaptiva formuläret för Workfront Fusion:

1. Logga in på din AEM.
1. Gå till **[!UICONTROL Forms]** > **[!UICONTROL Forms and Documents]** > **[!UICONTROL Create]** > **[!UICONTROL Adaptive Form]**. Guiden **[!UICONTROL Create Form]** visas.
1. Välj en anpassad formulärmall på fliken **[!UICONTROL Source]**.
1. Välj ett tema på fliken **[!UICONTROL Style]**.

   ![Skicka-åtgärd för Workfront Fusion](/help/forms/assets/workfront-scenario-new-af.png)

1. Välj **[!UICONTROL Invoke a WorkFront Fusion Scenario]** på fliken **[!UICONTROL Submission]**.
1. Välj den skapade webkroken på fliken **[!UICONTROL Options]** i fönstret **[!UICONTROL Properties]**.

   >[!NOTE]
   >
   > Webkroknamnet för Workfront-scenariot visas i listrutan **Alternativ**.

1. Klicka på **[!UICONTROL Create]**.
1. Ange namnet på det nya adaptiva formuläret och klicka på **[!UICONTROL Create]**.

#### Konfigurera skicka-åtgärd för befintligt adaptivt formulär för Workfront Fusion {#existing-af-submit-action}

Så här konfigurerar du skickaåtgärden för det befintliga adaptiva formuläret för Workfront Fusion:

1. Logga in på din AEM.
1. Gå till **[!UICONTROL Forms]** > **[!UICONTROL Forms and Documents]**.
1. Markera ett adaptivt formulär och öppna formuläret i redigeringsläge.
1. Öppna innehållsläsaren och markera komponenten **[!UICONTROL Guide Container]** i det adaptiva formuläret.
1. Klicka på ikonen för egenskaper för stödlinjebehållaren ![Egenskaper för stödlinje](/help/forms/assets/configure-icon.svg) . Dialogrutan Adaptiv formulärbehållare öppnas.

   ![Skicka-åtgärd för Workfront Fusion](/help/forms/assets/workfront-scenario-existing-af.png)

1. Öppna fliken **[!UICONTROL Submission]**.
1. Välj **[!UICONTROL Submit action]** som **[!UICONTROL Invoke a WorkFront Fusion Scenario]**
1. Välj **[!UICONTROL Workfront Fusion scenario]** i listrutan.
1. Klicka på **[!UICONTROL Done]**.

## Bästa praxis {#best-practices}

* Vi rekommenderar att du noga väljer webbhollänsnamn eftersom det inte finns något sätt att hämta scenarionamnet vid AEM. Om du ändrar webkroknamnet i framtiden återspeglas det inte i listrutan för AEM Forms-åtgärden Skicka.
* Ett scenario kan ha flera webkroklänkar, men vid en tidpunkt är bara en webkrok aktiv. Vi rekommenderar att du tar bort den olänkade webkroken så att den inte visas i listrutan AEM Forms Skicka-åtgärd.

<!-- During testing or development of Workfront, add the Author URL to the instance URL. However, when deploying Workfront Fusion in a production environment, it is recommended to replicate the scenario URLs for the Publish instance. -->

## Relaterade artiklar

{{af-submit-action}}
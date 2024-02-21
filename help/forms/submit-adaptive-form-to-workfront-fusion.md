---
title: Integrering av Adobe Workfront Fusion med AEM Forms Submission
description: Med Adobe Workfront Fusion kan du fokusera på nya uppgifter istället för att fokusera på repetitiva uppgifter. Du kan ansluta Adobe Workfront Fusion till ett adaptivt formulär genom att skicka formulär.
keywords: Skicka in ett adaptivt formulär till Adobe Workfront Fusion, Integration of Adobe Workfront Fusion with AEM Forms Submission, Adobe Workfront Fusion with AEM Forms, Workfront Fusion with AEM Forms, Connect Workfront Fusion to AEM Forms, AEM Forms and Workfront Fusion, How to connect Workfront Fusion with AEM Forms?, Connect Workfront Fusion to a Form
topic-tags: author, developer
feature: Adaptive Forms
role: Admin, User
exl-id: d3efb450-a879-40ae-8958-0040f99bdafc
source-git-commit: 8923bfbb0e46961485ff360c0135ebdde6d8cab3
workflow-type: tm+mt
source-wordcount: '1174'
ht-degree: 0%

---

# Skicka ett anpassat formulär till Adobe Workfront Fusion

<span class="preview"> Funktionen är tillgänglig i ett program för tidig användning. Du kan skriva till aem-forms-early-adopter-program@adobe.com från ditt officiella e-post-id för att gå med i det tidiga adopterprogrammet och begära åtkomst till funktionen. </span>

[Adobe Workfront Fusion](https://experienceleague.adobe.com/docs/workfront/using/adobe-workfront-fusion/get-started-with-workfront-fusion/workfront-fusion-overview.html) automatiserar processen för att upprepa samma uppgifter, som dokumentgodkännandearbetsflöden, e-postfiltrering och sortering, så att du kan fokusera på nya uppgifter istället för på återkommande. Adobe Workfront Fusion innehåller flera scenarier. Ett scenario består av en serie moduler som utför dataöverföring mellan program och webbtjänster. I ett scenario lägger du till olika steg (moduler) för att automatisera en uppgift.

Med Workfront Fusion kan du till exempel skapa ett scenario där du samlar in data med adaptiv form, bearbetar data och skickar data till ett datalager för arkivering. När ett scenario har konfigurerats utför Workfront Fusion automatiskt uppgifterna när en användare fyller i ett formulär och uppdaterar datalagret sömlöst.

AEM Forms as a Cloud Service har en OOTB-anslutning för att ansluta och skicka ett adaptivt formulär till Adobe Workfront Fusion. Att skicka in ett formulär till Adobe Workfront Fusion kan ge flera fördelar:
* Man kunde smidigt överföra data från inskickade formulär till Workfront Fusion-arbetsflöden.
* Det hjälper till att automatisera olika uppgifter som triggas av inskickade formulär. Det kan vara att initiera projekt, tilldela uppgifter till specifika teammedlemmar, skicka meddelanden och uppdatera projektstatus - allt utan manuell åtgärd.
* Alla inskickade formulär som samlats in i Workfront Fusion kan vara en enda källa till sanning för projektrelaterad information


<!--  AEM as a Cloud Service offers various out of the box submit actions for handling form submissions. You can learn more about these options in the [Adaptive Form Submit Action](/help/forms/configure-submit-actions-core-components.md)  article.-->

>[!VIDEO](https://video.tv.adobe.com/v/3427145/adaptive-forms-adobe-workfront-af-workfront-workfront-aem-forms/?quality=12&learn=on)

## Krav för att integrera AEM Forms med Adobe Workfront Fusion {#prerequisites}

För att upprätta en anslutning mellan Workfront Fusion och AEM Forms krävs följande:

* Ett giltigt [Workfront- och Workfront Fusion-licens](https://experienceleague.adobe.com/docs/workfront/using/adobe-workfront-fusion/get-started-with-workfront-fusion/license-automation-vs-integration.html).
* En AEM användare med behörighet att komma åt [Dev Console](https://my.cloudmanager.adobe.com/) till [hämta inloggningsuppgifterna för tjänsten](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html).

## Integrera AEM Forms med Adobe Workfront Fusion

### 1. Skapa ett Workfront-scenario {#workflow-scenario}

Så här skapar du ett Workfront-scenario:

1. [Skapa ett scenario](#create-scenario)
1. [Lägga till en webbkrok i ett scenario](#add-webhook)
1. [Lägga till en anslutning till en webkrok](#add-connection)

#### Skapa ett scenario {#create-scenario}

Så här skapar du ett scenario:
1. Logga in på [Workfront Fusion Account](https://app-qa.workfrontfusion.com/).
1. Klicka **[!UICONTROL Scenarios]** ![Delningsikon](/help/forms/assets/Smock_ShareAndroid_18_N.svg) till vänster.
1. Klicka **[!UICONTROL Create a new scenario]** i det övre högra hörnet på sidan. En sida för att skapa ett nytt scenario visas på skärmen.
1. Välj **[!UICONTROL New scenario]** i det övre vänstra hörnet på sidan och skriv ett namn för scenariot.
1. Klicka på frågetecknet och kontrollera att du lägger till den första modulen som **[!UICONTROL AEM Forms]**.

   ![Lägga till en AEM Forms-modul](/help/forms/assets/workfront-aemforms.png)

   The **[!UICONTROL Watch for Form Events]** visas.

   >[!NOTE]
   >
   > Den första modulen måste läggas till som **[!UICONTROL AEM Forms]**.

1. Välj **[!UICONTROL Watch for Form Events]** visas en dialogruta och ett fönster där du kan lägga till en webkrok.

#### Lägg till en webkrok {#add-webhook}

![Lägg till en webkrok](/help/forms/assets/workfront-add-webhook.png)

Så här lägger du till en webkrok:

1. Klicka **[!UICONTROL Add]** och **[!UICONTROL Add a webhook]** visas.
1. Ange ett webbkroknamn.

   >[!NOTE]
   >
   > Vi rekommenderar att du noga väljer ditt webkrok-namn eftersom det angivna webkroknamnet visas i AEM.

1. Klicka **[!UICONTROL Add]** för att lägga till en ny anslutning. The **[!UICONTROL Create a Connection]** visas.

#### Lägga till en anslutning till en webkrok {#add-connection}

![Lägg till en anslutning](/help/forms/assets/workfront-add-connection.png)

Så här lägger du till en anslutning:

1. Ange en **[!UICONTROL Connection Name]** i **[!UICONTROL Create a Connection]** -dialogrutan.

1. Välj **Miljö** och **Typ** i listrutan.

1. Ange **Instans-URL**.

   >[!NOTE]
   >
   > Instans-URL är den unika webbadressen som pekar på en viss AEM Forms-instans.

   Du kan hämta [inloggningsuppgifter från utvecklarkonsolen](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html) krävs för att skapa en anslutning.

1. Ersätt `ims-na1.adobelogin.com` i **IMS-slutpunkt** med värdet för **imsEndpoint** från inloggningsuppgifterna för tjänsten i Developer Console.

   >[!NOTE]
   >
   > Behåll `https://` i **IMS-slutpunkt** textrutan när du lägger till `imsEndpoint` URL.

1. Ange följande värden i dialogrutan **[!UICONTROL Create a Connection]** dialogruta:
   * Ange **Klient-ID** med värdet för **clientId** från inloggningsuppgifterna för tjänsten i Developer Console.
   * Ange **Klienthemlighet** med värdet för **clientSecret** från inloggningsuppgifterna för tjänsten i Developer Console.
   * Ange **Tekniskt konto-ID**  med värdet för **id** från inloggningsuppgifterna för tjänsten i Developer Console.
   * Ange **Organisations-ID**  med värdet för **org** från inloggningsuppgifterna för tjänsten i Developer Console.
   * **Meta-omfång**  med värdet för **metasskop** från inloggningsuppgifterna för tjänsten i Developer Console.
   * **Privata nycklar**  med värdet för **privateKey** från inloggningsuppgifterna för tjänsten i Developer Console.

   >[!NOTE]
   >
   >* För **Privat nyckel**, ta bort `\r\n` från värdet.
   >  Om värdet för den privata nyckeln till exempel är:
   >`\r\nIJAVO8GDYAOZ9jMA0GCSqGSIb3DQEBCwUAMDAxL\r\nMy1lMTUxODMxLWNtc3RnLWludGVncmF0aW9uLTAw`efter att du tagit bort `\r\n` från den privata nyckeln ser nyckeln ut så här, med båda värdena på en separat rad:
   >
   >   `IJAVO8GDYAOZ9jMA0GCSqGSIb3DQEBCwUAMDAxL`
   >
   >   `My1lMTUxODMxLWNtc3RnLWludGVncmF0aW9uLTAw`
   > 
   >* Du kan också hämta en privat nyckel eller ett certifikat från filen genom att välja **Extract** -knappen.

1. Klicka **Fortsätt**.

   Den skapade anslutningen visas i listrutan i **[!UICONTROL Connection]** i **[!UICONTROL Add a webhook]** -dialogrutan.

1. Välj den skapade anslutningen **[!UICONTROL Connection]** i listrutan.
1. Klicka på **[!UICONTROL Save]**.
1. Klicka **[!UICONTROL OK]** och spara ändringarna för scenariot.
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
1. Gå till **[!UICONTROL Forms]** > **[!UICONTROL Forms and Documents]** > **[!UICONTROL Create]** > **[!UICONTROL Adaptive Form]**. The **[!UICONTROL Create Form]** visas.
1. Välj en adaptiv formulärmall från **[!UICONTROL Source]** -fliken.
1. Välj ett tema på menyn **[!UICONTROL Style]** -fliken.

   ![Skicka åtgärd för Workfront Fusion](/help/forms/assets/workfront-scenario-new-af.png)

1. Välj **[!UICONTROL Invoke a WorkFront Fusion Scenario]** från **[!UICONTROL Submission]** -fliken.
1. Välj den skapade webbkroken på menyn **[!UICONTROL Options]** i **[!UICONTROL Properties]** -fönstret.

   >[!NOTE]
   >
   > Webbkroknamnet för Workfront-scenariot visas i **Alternativ** listruta.

1. Klicka på **[!UICONTROL Create]**.
1. Ange namnet på det nya adaptiva formuläret och klicka på **[!UICONTROL Create]**.

#### Konfigurera skicka-åtgärd för befintligt adaptivt formulär för Workfront Fusion {#existing-af-submit-action}

Så här konfigurerar du skickaåtgärden för det befintliga adaptiva formuläret för Workfront Fusion:

1. Logga in på din AEM.
1. Gå till **[!UICONTROL Forms]** > **[!UICONTROL Forms and Documents]**.
1. Markera ett adaptivt formulär och öppna formuläret i redigeringsläge.
1. Öppna innehållsläsaren och välj **[!UICONTROL Guide Container]** som ingår i det adaptiva formuläret.
1. Klicka på egenskaperna för stödlinjebehållaren ![Stödlinjeegenskaper](/help/forms/assets/configure-icon.svg) -ikon. Dialogrutan Adaptiv formulärbehållare öppnas.

   ![Skicka åtgärd för Workfront Fusion](/help/forms/assets/workfront-scenario-existing-af.png)

1. Öppna **[!UICONTROL Submission]** -fliken.
1. Välj **[!UICONTROL Submit action]** as **[!UICONTROL Invoke a WorkFront Fusion Scenario]**
1. Välj **[!UICONTROL Workfront Fusion scenario]** i listrutan.
1. Klicka på **[!UICONTROL Done]**.

## Bästa praxis {#best-practices}

* Vi rekommenderar att du noga väljer webbhollänsnamn eftersom det inte finns något sätt att hämta scenarionamnet vid AEM. Om du ändrar webkroknamnet i framtiden återspeglas det inte i listrutan för AEM Forms-åtgärden Skicka.
* Ett scenario kan ha flera webkroklänkar, men vid en tidpunkt är bara en webkrok aktiv. Vi rekommenderar att du tar bort den olänkade webkroken så att den inte visas i listrutan AEM Forms Skicka-åtgärd.

<!-- During testing or development of Workfront, add the Author URL to the instance URL. However, when deploying Workfront Fusion in a production environment, it is recommended to replicate the scenario URLs for the Publish instance. -->

## Relaterade artiklar

{{af-submit-action}}
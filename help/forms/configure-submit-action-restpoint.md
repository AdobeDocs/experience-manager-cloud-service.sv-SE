---
Title: How to configure submit to Rest Endpoint submit action for an Adaptive Form?
Description: Discover the steps to set up Rest Endpoint when submitting an Adaptive Form.
keywords: AEM Forms REST Endpoint, Submit to REST Endpoint, Post Data to REST URL, Configure REST Endpoint Action
feature: Adaptive Forms, Core Components, Foundation Components, Edge Delivery Services
title: Hur konfigurerar man en Skicka-åtgärd för ett anpassat formulär?
role: User, Developer
exl-id: 58c63ba6-aec5-4961-a70a-265990ab9cc8
source-git-commit: c0df3c6eaf4e3530cca04157e1a5810ebf5b4055
workflow-type: tm+mt
source-wordcount: '1403'
ht-degree: 0%

---

# Konfigurera ett anpassat formulär för REST-slutpunktsåtgärd

<span class="preview"> Möjligheten att ange REST-slutpunkten med hjälp av konfigurationen är ett tidigt Adobe-program och kan endast användas för kärnkomponenter och Edge Delivery Services Forms. Du kan skriva till `aem-forms-ea@adobe.com` från ditt officiella e-post-id för att gå med i det tidiga adopterprogrammet och begära åtkomst till funktionen. </span>

Använd åtgärden **[!UICONTROL Submit to REST Endpoint]** för att skicka skickade data till en REST-URL. URL:en kan vara en intern (servern som formuläret återges på) eller en extern server.

AEM as a Cloud Service erbjuder olika inskickningsåtgärder för att hantera inskickade formulär. Du kan läsa mer om de här alternativen i artikeln [Åtgärd för att skicka anpassade formulär](/help/forms/aem-forms-submit-action.md).

## Fördelar

Några av fördelarna med att konfigurera **[!UICONTROL Submit to REST endpoint]**-sändningsåtgärden för Adaptiv Forms är:

* Det möjliggör smidig integrering av formulärdata med externa system och tjänster via RESTful API:er.
* Det ger flexibilitet vid hantering av data som skickas från Adaptive Forms, vilket ger stöd för dynamiska och komplexa datastrukturer.
* Det har stöd för dynamisk mappning av formulärfält till parametrar i REST-slutpunkts-URL, vilket möjliggör anpassningsbara och anpassningsbara dataöverföringar.


## Konfigurera åtgärden Skicka till REST-slutpunkt {#steps-to-configure-submit-to-restendpoint-submit-action}

>[!BEGINTABS]

>[!TAB Foundation Component]

Så här konfigurerar du en skicka-åtgärd baserat på Swagger Open API-specifikationen för Adaptive Form som baseras på Foundation-komponenter:

1. Öppna det adaptiva formuläret för redigering och navigera till avsnittet **[!UICONTROL Submission]** i egenskaperna för den adaptiva formulärbehållaren.
1. I listrutan **[!UICONTROL Submit Action]** väljer du **[!UICONTROL Submit to Rest endpoint]**.

   ![Åtgärdskonfiguration för slutpunkten Skicka till vila](/help/forms/assets/submit-action-restendpoint.png)

   Om du vill skicka data till en intern server anger du sökvägen till resursen. Data bokförs som resurssökväg. Exempel: `/content/restEndPoint`. För sådana efterfrågningar används autentiseringsinformationen i förfrågan.
Med det här alternativet kan du ange REST-målslutpunkten direkt.
Ange en URL om du vill skicka data till en extern server. URL-formatet är `https://host:port/path_to_rest_end_point`. Se till att du konfigurerar sökvägen så att den hanterar POST-begäran anonymt.
   ![Mappning för fältvärden skickas som parametrar för Tack-sidan](assets/post-enabled-actionconfig.png)

   I exemplet ovan hämtas användarinformationen i `textbox` med parametern `param1`. Syntaxen för att bokföra data som har hämtats med `param1` är:

   `String data=request.getParameter("param1");`

   På samma sätt är parametrar som du använder för att skicka XML-data och bifogade filer `dataXml` och `attachments`.

   Du kan till exempel använda de här två parametrarna i skriptet för att tolka data till en slutpunkt. Du använder följande syntax för att lagra och analysera data:

   `String data=request.getParameter("dataXml");`
   `String att=request.getParameter("attachments");`

   I det här exemplet lagrar `data` XML-data och `att` lagrar data för bifogade filer.
Åtgärden **[!UICONTROL Submit to REST endpoint]** Skicka skickar data som är ifyllda i formuläret till en konfigurerad bekräftelsesida som en del av HTTP GET-begäran. Du kan lägga till namnet på fältet som ska begäras. Begäran har följande format:
   `{fieldName}={request parameter name}`

   Som visas i bilden nedan skickas `param1` och `param2` som parametrar med värden som kopierats från fälten **texbox** och **numerbox** för nästa åtgärd.

   ![Konfigurerar åtgärden Skicka för resterande slutpunkt](assets/action-config.png)

   Du kan också **[!UICONTROL Enable POST request]** och ange en URL för att skicka begäran. Om du vill skicka data till den AEM-server som är värd för formuläret använder du en relativ sökväg som motsvarar rotsökvägen för AEM-servern. Exempel: `/content/forms/af/SampleForm.html`. Om du vill skicka data till en annan server använder du den absoluta sökvägen.

1. Klicka på **[!UICONTROL Done]**.

>[!TAB Kärnkomponent]

Så här konfigurerar du en överföringsåtgärd baserad på Swagger Open API-specifikationen för adaptiva formulär baserade på kärnkomponenter:

1. Öppna innehållsläsaren och markera komponenten **[!UICONTROL Guide Container]** i det adaptiva formuläret.
1. Klicka på ikonen för egenskaper för stödlinjebehållaren ![Egenskaper för stödlinje](/help/forms/assets/configure-icon.svg) . Dialogrutan Adaptiv formulärbehållare öppnas.
1. Klicka på fliken **[!UICONTROL Submission]**.
1. I listrutan **[!UICONTROL Submit Action]** väljer du **[!UICONTROL Submit to Rest endpoint]**.

   ![Konfigurerar resterande slutpunkt](assets/rest-service-endpoint-config.png)

   Om du vill skicka data till en intern server anger du sökvägen till resursen. Data bokförs som resurssökväg. Exempel: `/content/restEndPoint`. För sådana efterfrågningar används autentiseringsinformationen i förfrågan.

   Det finns två alternativ för att ange REST-slutpunkten:

   +++URL

   Med det här alternativet kan du ange REST-målslutpunkten direkt.
Ange en URL om du vill skicka data till en extern server. URL-formatet är `https://host:port/path_to_rest_end_point`. Se till att du konfigurerar sökvägen så att den hanterar POST-begäran anonymt.

   ![Mappning för fältvärden skickas som parametrar för Tack-sidan](assets/post-enabled-actionconfig.png)

   I exemplet ovan hämtas användarinformationen i `textbox` med parametern `param1`. Syntaxen för att bokföra data som har hämtats med `param1` är:

   `String data=request.getParameter("param1");`

   På samma sätt är parametrar som du använder för att skicka XML-data och bifogade filer `dataXml` och `attachments`.

   Du kan till exempel använda de här två parametrarna i skriptet för att tolka data till en slutpunkt. Du använder följande syntax för att lagra och analysera data:

   `String data=request.getParameter("dataXml");`
   `String att=request.getParameter("attachments");`

   I det här exemplet lagrar `data` XML-data och `att` lagrar data för bifogade filer.

   Åtgärden **[!UICONTROL Submit to REST endpoint]** Skicka skickar data som är ifyllda i formuläret till en konfigurerad bekräftelsesida som en del av HTTP GET-begäran. Du kan lägga till namnet på fältet som ska begäras. Begäran har följande format:

   `{fieldName}={request parameter name}`

   Som visas i bilden nedan skickas `param1` och `param2` som parametrar med värden som kopierats från fälten **texbox** och **numerbox** för nästa åtgärd.

   ![Konfigurerar åtgärden Skicka för resterande slutpunkt](assets/action-config.png)

   Du kan också **[!UICONTROL Enable POST request]** och ange en URL för att skicka begäran. Om du vill skicka data till den AEM-server som är värd för formuläret använder du en relativ sökväg som motsvarar rotsökvägen för AEM-servern. Exempel: `/content/forms/af/SampleForm.html`. Om du vill skicka data till en annan server använder du den absoluta sökvägen.

   +++

   +++Konfiguration

   Med det här alternativet kan du lägga till en fördefinierad HTTP-konfiguration som hanteras via AEM Configuration Browser. Du kan välja den konfiguration som har skapats för tjänstens autentiseringstyp för återställningsslutpunkt och innehållstyper. Mer information om autentiseringstyp och innehållstyper finns på [Konfigurera datakällor](/help/forms/configure-data-sources.md#configure-restful-services-using-service-endpoint-configure-restful-services-service-endpoint)

   +++

1. Klicka på **[!UICONTROL Done]**.

>[!TAB Universell redigerare]

Så här konfigurerar du en åtgärd som baseras på Swagger Open API-specifikationen för Adaptive Form som har skapats i Universal Editor:

1. Öppna det adaptiva formuläret för redigering.
1. Klicka på tillägget **Redigera formuläregenskaper** i redigeraren.
Dialogrutan **Formuläregenskaper** visas.
   >[!NOTE]
   >
   > * Om ikonen **Redigera formuläregenskaper** inte visas i det universella redigeringsgränssnittet aktiverar du tillägget **Redigera formuläregenskaper** i Extension Manager.
   > * Läs artikeln [Extension Manager Feature Highlights](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions) om du vill veta hur du aktiverar eller inaktiverar tillägg i den universella redigeraren.
1. Klicka på fliken **Skicka** och välj åtgärden **[!UICONTROL Submit to Rest endpoint]** Skicka.

   Om du vill skicka data till en intern server anger du sökvägen till resursen. Data bokförs som resurssökväg. Exempel: `/content/restEndPoint`. För sådana efterfrågningar används autentiseringsinformationen i förfrågan.

   Det finns två alternativ för att ange REST-slutpunkten:

   +++URL

   Med det här alternativet kan du ange REST-målslutpunkten direkt.
Ange en URL om du vill skicka data till en extern server. URL-formatet är `https://host:port/path_to_rest_end_point`. Se till att du konfigurerar sökvägen så att den hanterar POST-begäran anonymt.

   ![Mappning för fältvärden skickas som parametrar för Tack-sidan](assets/post-enabled-actionconfig.png)

   I exemplet ovan hämtas användarinformationen i `textbox` med parametern `param1`. Syntaxen för att bokföra data som har hämtats med `param1` är:

   `String data=request.getParameter("param1");`

   På samma sätt är parametrar som du använder för att skicka XML-data och bifogade filer `dataXml` och `attachments`.

   Du kan till exempel använda de här två parametrarna i skriptet för att tolka data till en slutpunkt. Du använder följande syntax för att lagra och analysera data:

   `String data=request.getParameter("dataXml");`
   `String att=request.getParameter("attachments");`

   I det här exemplet lagrar `data` XML-data och `att` lagrar data för bifogade filer.

   Åtgärden **[!UICONTROL Submit to REST endpoint]** Skicka skickar data som är ifyllda i formuläret till en konfigurerad bekräftelsesida som en del av HTTP GET-begäran. Du kan lägga till namnet på fältet som ska begäras. Begäran har följande format:

   `{fieldName}={request parameter name}`

   Som visas i bilden nedan skickas `param1` och `param2` som parametrar med värden som kopierats från fälten **texbox** och **numerbox** för nästa åtgärd.

   ![Konfigurerar åtgärden Skicka för resterande slutpunkt](/help/forms/assets/submit-to-rest-endpoint-ue.png)

   Du kan också **[!UICONTROL Enable POST request]** och ange en URL för att skicka begäran. Om du vill skicka data till den AEM-server som är värd för formuläret använder du en relativ sökväg som motsvarar rotsökvägen för AEM-servern. Exempel: `/content/forms/af/SampleForm.html`. Om du vill skicka data till en annan server använder du den absoluta sökvägen.

   +++

   +++Konfiguration

   Med det här alternativet kan du lägga till en fördefinierad HTTP-konfiguration som hanteras via AEM Configuration Browser. Du kan välja den konfiguration som har skapats för tjänstens autentiseringstyp för återställningsslutpunkt och innehållstyper. Mer information om autentiseringstyp och innehållstyper finns på [Konfigurera datakällor](/help/forms/configure-data-sources.md#configure-restful-services-using-service-endpoint-configure-restful-services-service-endpoint)

   +++

1. Klicka på **[!UICONTROL Save&Close]**.

>[!ENDTABS]

<!-- ### Configure submit action based on Service Rest Endpoint {#config-service-endpoint-auth}



1. Open the Content browser, and select the **[!UICONTROL Guide Container]** component of your Adaptive Form.
2. Click the Guide Container properties ![Guide properties](/help/forms/assets/configure-icon.svg) icon. The Adaptive Form Container dialog box opens. 
3. Click the  **[!UICONTROL Submission]** tab. 
4. From the **[!UICONTROL Submit Action]** drop-down list, select **[!UICONTROL Submit to Rest endpoint]**.
5. Enable the POST request.
6. Specify the REST endpoint URL.
7. Select the Configuration you have created for your Service Rest Endpoint Authentication Type and the Content Types. To know more about Authentication Type and the Content Types, visit [configure data sources](/help/forms/configure-data-sources.md#configure-restful-services-using-service-endpoint-configure-restful-services-service-endpoint).
    ![Configuring Rest Endpoint](assets/rest-service-endpoint-config.png)
8. Click Done. -->



## Bästa praxis

* När du skickar data till en extern server ska du kontrollera att URL:en är säker och konfigurera sökvägen så att POST-begäran hanteras anonymt för att skydda känslig information.
* Om du vill skicka fälten som parametrar i en REST-URL måste alla fält ha olika elementnamn, även om fälten placeras på olika paneler.

## Relaterade artiklar

{{af-submit-action}}

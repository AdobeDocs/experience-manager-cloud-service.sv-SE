---
Title: How to configure submit to Rest Endpoint submit action for an Adaptive Form?
Description: Discover the steps to set up Rest Endpoint when submitting an Adaptive Form.
keywords: AEM Forms REST Endpoint, Submit to REST Endpoint, Post Data to REST URL, Configure REST Endpoint Action
feature: Adaptive Forms, Core Components
source-git-commit: 8784c0bcd05eeae41a472faa5ecad03cbdd8a9b6
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 1%

---


# Konfigurera ett anpassat formulär för REST-slutpunktsåtgärd

Använd **[!UICONTROL Submit to REST Endpoint]** åtgärd för att skicka skickade data till en REST-URL. URL:en kan vara en intern (servern som formuläret återges på) eller en extern server.

AEM as a Cloud Service erbjuder olika åtgärder för att skicka in formulär. Du kan läsa mer om de här alternativen i [Inlämningsåtgärd för anpassat formulär](/help/forms/configure-submit-actions-core-components.md)  artikel.

## Fördelar

Några av fördelarna med att konfigurera **[!UICONTROL Submit to REST endpoint]** Skicka-åtgärd för Adaptive Forms är:

* Det möjliggör smidig integrering av formulärdata med externa system och tjänster via RESTful API:er.
* Det ger flexibilitet vid hantering av data som skickas från Adaptive Forms, vilket ger stöd för dynamiska och komplexa datastrukturer.
* Det har stöd för dynamisk mappning av formulärfält till parametrar i REST-slutpunkts-URL, vilket möjliggör anpassningsbara och anpassningsbara dataöverföringar.


## Konfigurera åtgärden Skicka till REST-slutpunkt {#steps-to-configure-submit-to-restendpoint-submit-action}

Så här konfigurerar du åtgärden skicka:

1. Öppna innehållsläsaren och välj **[!UICONTROL Guide Container]** som ingår i det adaptiva formuläret.
1. Klicka på egenskaperna för stödlinjebehållaren ![Stödlinjeegenskaper](/help/forms/assets/configure-icon.svg) -ikon. Dialogrutan Adaptiv formulärbehållare öppnas.
1. Klicka på  **[!UICONTROL Submission]** -fliken.
1. I listrutan **[!UICONTROL Submit Action]** väljer du **[!UICONTROL Submit to Rest endpoint]**.
   ![Åtgärdskonfiguration för Skicka till resterande slutpunkt](/help/forms/assets/submit-action-restendpoint.png)

   Om du vill skicka data till en intern server anger du sökvägen till resursen. Data bokförs som resurssökväg. Till exempel: `/content/restEndPoint`. För sådana efterfrågningar används autentiseringsinformationen i förfrågan.

   Ange en URL om du vill skicka data till en extern server. URL-formatet är `https://host:port/path_to_rest_end_point`. Se till att du konfigurerar sökvägen så att den hanterar POSTENS begäran anonymt.

   ![Mappning för fältvärden skickas som Tack-sidan-parametrar](assets/post-enabled-actionconfig.png)

   I exemplet ovan har användaren angett information i `textbox` hämtas med parameter `param1`. Syntax för att bokföra data som samlats in med `param1` är:

   `String data=request.getParameter("param1");`

   På samma sätt är parametrar som du använder för att bokföra XML-data och bifogade filer `dataXml` och `attachments`.

   Du kan till exempel använda de här två parametrarna i skriptet för att tolka data till en slutpunkt. Du använder följande syntax för att lagra och analysera data:

   `String data=request.getParameter("dataXml");`
   `String att=request.getParameter("attachments");`

   I detta exempel `data` lagrar XML-data, och `att` lagrar data för bifogade filer.

   The **[!UICONTROL Submit to REST endpoint]** Skicka åtgärd skickar data som är ifyllda i formuläret till en konfigurerad bekräftelsesida som en del av HTTP GET-begäran. Du kan lägga till namnet på fältet som ska begäras. Begäran har följande format:

   `{fieldName}={request parameter name}`

   Som visas i bilden nedan, `param1` och `param2` skickas som parametrar med värden som kopierats från **textruta** och **numerisk** fält för nästa åtgärd.

   ![Konfigurerar åtgärden Skicka för resterande slutpunkt](assets/action-config.png)

   Du kan också **[!UICONTROL Enable POST request]** och ange en URL för att skicka begäran. Om du vill skicka data till den AEM servern som är värd för formuläret använder du en relativ sökväg som motsvarar rotsökvägen för AEM. Till exempel: `/content/forms/af/SampleForm.html`. Om du vill skicka data till en annan server använder du den absoluta sökvägen.

1. Klicka på **[!UICONTROL Done]**.

## Bästa praxis

* När du skickar data till en extern server måste du se till att URL:en är säker och konfigurera sökvägen så att den hanterar POSTENS förfrågan anonymt för att skydda känslig information.
* Om du vill skicka fälten som parametrar i en REST-URL måste alla fält ha olika elementnamn, även om fälten placeras på olika paneler.

## Relaterade artiklar

{{af-submit-action}}


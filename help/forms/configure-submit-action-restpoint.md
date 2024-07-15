---
Title: How to configure submit to Rest Endpoint submit action for an Adaptive Form?
Description: Discover the steps to set up Rest Endpoint when submitting an Adaptive Form.
keywords: AEM Forms REST Endpoint, Submit to REST Endpoint, Post Data to REST URL, Configure REST Endpoint Action
feature: Adaptive Forms, Core Components
exl-id: 58c63ba6-aec5-4961-a70a-265990ab9cc8
title: "Hur konfigurerar jag en Skicka-åtgärd för ett anpassat formulär?"
role: User, Developer
source-git-commit: 2b76f1be2dda99c8638deb9633055e71312fbf1e
workflow-type: tm+mt
source-wordcount: '535'
ht-degree: 1%

---

# Konfigurera ett anpassat formulär för REST-slutpunktsåtgärd

Använd åtgärden **[!UICONTROL Submit to REST Endpoint]** för att skicka skickade data till en REST-URL. URL:en kan vara en intern (servern som formuläret återges på) eller en extern server.

AEM as a Cloud Service erbjuder olika inskickningsåtgärder för att hantera inskickade formulär. Du kan läsa mer om de här alternativen i artikeln [Åtgärd för att skicka anpassade formulär](/help/forms/configure-submit-actions-core-components.md).

## Fördelar

Några av fördelarna med att konfigurera **[!UICONTROL Submit to REST endpoint]**-sändningsåtgärden för Adaptiv Forms är:

* Det möjliggör smidig integrering av formulärdata med externa system och tjänster via RESTful API:er.
* Det ger flexibilitet vid hantering av data som skickas från Adaptive Forms, vilket ger stöd för dynamiska och komplexa datastrukturer.
* Det har stöd för dynamisk mappning av formulärfält till parametrar i REST-slutpunkts-URL, vilket möjliggör anpassningsbara och anpassningsbara dataöverföringar.


## Konfigurera åtgärden Skicka till REST-slutpunkt {#steps-to-configure-submit-to-restendpoint-submit-action}

Så här konfigurerar du åtgärden skicka:

1. Öppna innehållsläsaren och markera komponenten **[!UICONTROL Guide Container]** i det adaptiva formuläret.
1. Klicka på ikonen för egenskaper för stödlinjebehållaren ![Egenskaper för stödlinje](/help/forms/assets/configure-icon.svg) . Dialogrutan Adaptiv formulärbehållare öppnas.
1. Klicka på fliken **[!UICONTROL Submission]**.
1. I listrutan **[!UICONTROL Submit Action]** väljer du **[!UICONTROL Submit to Rest endpoint]**.
   ![Åtgärdskonfiguration för slutpunkten Skicka till vila](/help/forms/assets/submit-action-restendpoint.png)

   Om du vill skicka data till en intern server anger du sökvägen till resursen. Data bokförs som resurssökväg. Exempel: `/content/restEndPoint`. För sådana efterfrågningar används autentiseringsinformationen i förfrågan.

   Ange en URL om du vill skicka data till en extern server. URL-formatet är `https://host:port/path_to_rest_end_point`. Se till att du konfigurerar sökvägen så att den hanterar POSTENS begäran anonymt.

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

   Du kan också **[!UICONTROL Enable POST request]** och ange en URL för att skicka begäran. Om du vill skicka data till den AEM servern som är värd för formuläret använder du en relativ sökväg som motsvarar rotsökvägen för AEM. Exempel: `/content/forms/af/SampleForm.html`. Om du vill skicka data till en annan server använder du den absoluta sökvägen.

1. Klicka på **[!UICONTROL Done]**.

## Bästa praxis

* När du skickar data till en extern server måste du se till att URL:en är säker och konfigurera sökvägen så att den hanterar POSTENS förfrågan anonymt för att skydda känslig information.
* Om du vill skicka fälten som parametrar i en REST-URL måste alla fält ha olika elementnamn, även om fälten placeras på olika paneler.

## Relaterade artiklar

{{af-submit-action}}

---
Title: How to send an email on submission of an Adaptive Form?
Description: Explore the process to set up email notifications when submitting an Adaptive Form.
keywords: Skicka ett e-postmeddelande för ett tilläggsformulär, Skicka med e-post, Adaptiv e-post, Skicka e-post med formulär, Skicka e-postguide
feature: Adaptive Forms, Core Components
exl-id: 70386e57-345b-4edb-97f1-3fd52ea9ff4f
title: "Hur konfigurerar jag en Skicka-åtgärd för ett anpassat formulär?"
role: User, Developer
source-git-commit: 2b76f1be2dda99c8638deb9633055e71312fbf1e
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 1%

---

# Konfigurera åtgärden Skicka e-post för ett anpassat formulär

Med åtgärden **[!UICONTROL Send Email]** Skicka kan du skicka ett e-postmeddelande till en eller flera mottagare när formuläret har skickats. Med denna Skicka-åtgärd kan du skapa ett e-postmeddelande som kan innehålla formulärdata i ett fördefinierat format. Ta till exempel följande mall där kundnamn, leveransadress, delstatsnamn och postnummer hämtas från skickade formulärdata:


    &quot;
    Hej ${customer_Name},
    
    Följande anges som standardleveransadress:
    ${customer_Name},
    ${customer_Shipping_Address},
    ${customer_State},
    ${customer_ZIPCode}
    
    Med vänlig hälsning,
    WKND
    
    &quot;


## Fördelar

Några fördelar med att konfigurera ett anpassat formulär med Skicka e-post-åtgärden är:

* Det möjliggör snabb kommunikation när formulärdata skickas direkt till angivna e-postmottagare.
* Det effektiviserar arbetsflödet genom att direkt integrera inskickade formulär i e-postmeddelanden.
* Det hjälper organisationer att anpassa e-postinnehållet och på så sätt göra det lämpligt för specifika kommunikationsbehov.

## Konfigurera åtgärd för att skicka e-post {#steps-to-configure-send-email-submit-action}

Så här konfigurerar du åtgärden Skicka:

1. Öppna innehållsläsaren och markera komponenten **[!UICONTROL Guide Container]** i det adaptiva formuläret.
1. Klicka på ikonen för egenskaper för stödlinjebehållaren ![Egenskaper för stödlinje](/help/forms/assets/configure-icon.svg) . Dialogrutan Adaptiv formulärbehållare öppnas.
1. Klicka på fliken **[!UICONTROL Submission]**.
1. I listrutan **[!UICONTROL Submit Action]** väljer du **[!UICONTROL Send email]**.

   ![Åtgärdskonfiguration för Skicka e-post](/help/forms/assets/send-email-action-configuration.gif)
1. Ange avsändarens e-post-ID i textrutan **[!UICONTROL From]**.
1. Lägg till mottagarens e-post-ID i textrutan **[!UICONTROL To]**. Du kan lägga till flera mottagare genom att klicka på knappen **[!UICONTROL Add]**.
1. [Valfritt] Lägg till mottagaren för CC och Hemlig kopia genom att klicka på knappen **[!UICONTROL Add]**.
1. Ange en ämnesrad i textrutan **[!UICONTROL Subject]**.
1. Lägg till en e-postmall för att konfigurera åtgärden skicka e-post.
   * Du kan ange sökvägen till den externa e-postmallen som sparats i dina AEM resurser med alternativet **[!UICONTROL External Template Path]**.
   * Du kan också lägga till en anpassad e-postmall för formuläröverföringen i textrutan **[!UICONTROL Email Template]**.
1. [Valfritt] Med åtgärden **[!UICONTROL Send Email]** Skicka kan du inkludera bilagor och ett [dokument med post (DoR)](generate-document-of-record-core-components.md) med e-postmeddelandet.
1. Klicka på **[!UICONTROL Done]**.

## Bästa praxis {#best-practices}

* Vi rekommenderar att du håller e-postinnehållet klart och koncist. Användarna bör förstå syftet med e-postmeddelandet och de åtgärder de behöver vidta.
* Det rekommenderas att alla formulärfält har unika elementnamn, även om de finns på olika paneler i ett adaptivt formulär.
* När du använder AEM as a Cloud Service kräver utgående e-post kryptering. Som standard är funktionen för utgående e-post inaktiverad. Om du vill aktivera det skickar du en supportanmälan till [begär åtkomst](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=en#sending-email).


## Relaterade artiklar

{{af-submit-action}}

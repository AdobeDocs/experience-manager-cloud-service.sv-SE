---
Title: How to send an email on submission of an Adaptive Form?
Description: Explore the process to set up email notifications when submitting an Adaptive Form.
keywords: Skicka ett e-postmeddelande för ett tilläggsformulär, Skicka med e-post, Adaptiv e-post, Skicka e-post med formulär, Skicka e-postguide
feature: Adaptive Forms, Core Components
source-git-commit: f1db04e6cd1f78c1530aefd29f5f036ca5e70873
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 1%

---


# Konfigurera åtgärden Skicka e-post för ett anpassat formulär

The **[!UICONTROL Send Email]** Med Skicka-åtgärd kan du skicka ett e-postmeddelande till en eller flera mottagare när formuläret har skickats. Med denna Skicka-åtgärd kan du skapa ett e-postmeddelande som kan innehålla formulärdata i ett fördefinierat format. Ta till exempel följande mall där kundnamn, leveransadress, delstatsnamn och postnummer hämtas från skickade formulärdata:


    &quot;
    Hej ${customer_Name},
    
    Följande anges som standardleveransadress:
    ${customer_Name},
    ${customer_Shipping_Address},
    ${customer_State},
    ${customer_ZIPCode}
    
    Med vänlig hälsning
    WKND
    
    &quot;


## Fördelar

Några fördelar med att konfigurera ett anpassat formulär med Skicka e-post-åtgärden är:

* Det möjliggör snabb kommunikation när formulärdata skickas direkt till angivna e-postmottagare.
* Det effektiviserar arbetsflödet genom att direkt integrera inskickade formulär i e-postmeddelanden.
* Det hjälper organisationer att anpassa e-postinnehållet och på så sätt göra det lämpligt för specifika kommunikationsbehov.

## Konfigurera åtgärd för att skicka e-post {#steps-to-configure-send-email-submit-action}

Så här konfigurerar du åtgärden Skicka:

1. Öppna innehållsläsaren och välj **[!UICONTROL Guide Container]** som ingår i det adaptiva formuläret.
1. Klicka på egenskaperna för stödlinjebehållaren ![Stödlinjeegenskaper](/help/forms/assets/configure-icon.svg) -ikon. Dialogrutan Adaptiv formulärbehållare öppnas.
1. Klicka på  **[!UICONTROL Submission]** -fliken.
1. I listrutan **[!UICONTROL Submit Action]** väljer du **[!UICONTROL Send email]**.

   ![Åtgärdskonfiguration för Skicka e-post](/help/forms/assets/send-email-action-configuration.gif)
1. Ange avsändarens e-post-ID i dialogrutan **[!UICONTROL From]** textruta.
1. Lägg till mottagarens e-post-ID i **[!UICONTROL To]** textruta. Du kan lägga till flera mottagare genom att klicka på **[!UICONTROL Add]** -knappen.
1. [Valfritt] Lägg till mottagaren för CC och BCC genom att klicka på **[!UICONTROL Add]** -knappen.
1. Ange en ämnesrad i dialogrutan **[!UICONTROL Subject]** textruta.
1. Lägg till en e-postmall för att konfigurera åtgärden skicka e-post.
   * Du kan ange sökvägen till den externa e-postmallen som sparats i dina AEM resurser med hjälp av **[!UICONTROL External Template Path]** alternativ.
   * Du kan också lägga till en anpassad e-postmall för formulärinskickning i **[!UICONTROL Email Template]** textruta.
1. [Valfritt] The **[!UICONTROL Send Email]** Skicka åtgärd ger möjlighet att inkludera bilagor och en [Dokumentation (DoR)](generate-document-of-record-core-components.md) i mejlet.
1. Klicka på **[!UICONTROL Done]**.

## Bästa praxis {#best-practices}

* Vi rekommenderar att du håller e-postinnehållet klart och koncist. Användarna bör förstå syftet med e-postmeddelandet och de åtgärder de behöver vidta.
* Det rekommenderas att alla formulärfält har unika elementnamn, även om de finns på olika paneler i ett adaptivt formulär.
* När du använder AEM as a Cloud Service måste du kryptera utgående e-post. Som standard är funktionen för utgående e-post inaktiverad. Om du vill aktivera det skickar du en supportanmälan till [begära åtkomst](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=en#sending-email).


## Relaterade artiklar

{{af-submit-action}}



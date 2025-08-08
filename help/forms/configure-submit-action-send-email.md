---
description: Utforska processen för att skapa e-postmeddelanden när du skickar in ett adaptivt formulär.
keywords: Skicka ett e-postmeddelande för ett tilläggsformulär, Skicka med e-post, Adaptiv e-post, Skicka e-post med formulär, Skicka e-postguide
feature: Adaptive Forms, Core Components, Foundation Components, Edge Delivery Services
exl-id: 70386e57-345b-4edb-97f1-3fd52ea9ff4f
title: Hur konfigurerar man en Skicka-åtgärd för ett anpassat formulär?
role: User, Developer
source-git-commit: 1be7bafc1d93a65a81eeb2f7e86cac33cde7aa35
workflow-type: tm+mt
source-wordcount: '796'
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

>[!BEGINTABS]

>[!TAB Foundation Component]

Så här konfigurerar du en Skicka e-post-åtgärd för Foundation-komponent:

1. Öppna det adaptiva formuläret för redigering och navigera till avsnittet **[!UICONTROL Submission]** i egenskaperna för den adaptiva formulärbehållaren.
1. I listrutan **[!UICONTROL Submit Action]** väljer du **[!UICONTROL Send email]**.

   ![Åtgärdskonfiguration för Skicka e-post](/help/forms/assets/send-email-fc.png)

1. Ange avsändarens e-post-ID i textrutan **[!UICONTROL From]**.
1. Lägg till mottagarens e-post-ID i textrutan **[!UICONTROL To]**. Du kan lägga till flera mottagare genom att klicka på knappen **[!UICONTROL Add]**.
1. [Valfritt] Lägg till mottagaren för CC och Hemlig kopia genom att klicka på knappen **[!UICONTROL Add]**.
1. Ange en ämnesrad i textrutan **[!UICONTROL Subject]**.
1. Lägg till en e-postmall för att konfigurera åtgärden skicka e-post.
   * Du kan ange sökvägen till den externa e-postmallen som sparats i dina AEM-resurser med alternativet **[!UICONTROL External Template Path]**.
   * Du kan också lägga till en anpassad e-postmall för formuläröverföringen i textrutan **[!UICONTROL Email Template]**.
1. [Valfritt] Med åtgärden **[!UICONTROL Send Email]** Skicka kan du inkludera bilagor och ett [dokument med post (DoR)](generate-document-of-record-core-components.md) med e-postmeddelandet.
1. Klicka på **[!UICONTROL Done]**.

>[!TAB Kärnkomponent]

Så här konfigurerar du åtgärden Skicka e-post för kärnkomponenten:

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
   * Du kan ange sökvägen till den externa e-postmallen som sparats i dina AEM-resurser med alternativet **[!UICONTROL External Template Path]**.
   * Du kan också lägga till en anpassad e-postmall för formuläröverföringen i textrutan **[!UICONTROL Email Template]**.
1. [Valfritt] Med åtgärden **[!UICONTROL Send Email]** Skicka kan du inkludera bilagor och ett [dokument med post (DoR)](generate-document-of-record-core-components.md) med e-postmeddelandet.
1. Klicka på **[!UICONTROL Done]**.

>[!TAB Universell redigerare]

Så här konfigurerar du åtgärden Skicka e-post i Universell redigerare:

1. Öppna det adaptiva formuläret för redigering.
1. Klicka på tillägget **Redigera formuläregenskaper** i redigeraren.
Dialogrutan **Formuläregenskaper** visas.

   >[!NOTE]
   >
   > * Om ikonen **Redigera formuläregenskaper** inte visas i det universella redigeringsgränssnittet aktiverar du tillägget **Redigera formuläregenskaper** i Extension Manager.
   > * Läs artikeln [Extension Manager Feature Highlights](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions) om du vill veta hur du aktiverar eller inaktiverar tillägg i den universella redigeraren.


1. Klicka på fliken **Skicka** och välj åtgärden **[!UICONTROL Send email]** Skicka.

   ![Skicka e-postuniversell redigerare](/help/forms/assets/send-email-ue.png)

1. Ange avsändarens e-post-ID i textrutan **[!UICONTROL From]**.
1. Lägg till mottagarens e-post-ID i textrutan **[!UICONTROL To]**. Du kan lägga till flera mottagare genom att klicka på knappen **[!UICONTROL Add]**.
1. [Valfritt] Lägg till mottagaren för CC och Hemlig kopia genom att klicka på knappen **[!UICONTROL Add]**.
1. Ange en ämnesrad i textrutan **[!UICONTROL Subject]**.
1. Lägg till en e-postmall för att konfigurera åtgärden skicka e-post.
   * Du kan ange sökvägen till den externa e-postmallen som sparats i dina AEM-resurser med alternativet **[!UICONTROL External Template Path]**.
   * Du kan också lägga till en anpassad e-postmall för formuläröverföringen i textrutan **[!UICONTROL Email Template]**.
1. [Valfritt] Med åtgärden **[!UICONTROL Send Email]** Skicka kan du inkludera bilagor och ett [dokument med post (DoR)](generate-document-of-record-core-components.md) med e-postmeddelandet.
1. Klicka på **[!UICONTROL Save&Close]**.

>[!ENDTABS]

## Bästa praxis {#best-practices}

* Vi rekommenderar att du håller e-postinnehållet klart och koncist. Användarna bör förstå syftet med e-postmeddelandet och de åtgärder de behöver vidta.
* Det rekommenderas att alla formulärfält har unika elementnamn, även om de finns på olika paneler i ett adaptivt formulär.
* När du använder AEM as a Cloud Service kräver utgående e-post kryptering. Som standard är funktionen för utgående e-post inaktiverad. Om du vill aktivera det skickar du en supportanmälan till [begär åtkomst](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=en#sending-email).

## Relaterade artiklar

{{af-submit-action}}

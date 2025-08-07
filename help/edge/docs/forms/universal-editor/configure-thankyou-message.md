---
title: Hur man konfigurerar en omdirigeringssida eller ett tackmeddelande?
description: Lär dig hur användare kan visa ett tackmeddelande eller omdirigeras till en webbsida som formulärförfattare kan konfigurera när de skapar formuläret.
feature: Adaptive Forms, Edge Delivery Services
role: User
level: Intermediate
source-git-commit: 958891216e117acc03c50446ae92f85108d275a7
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 0%

---

# Konfigurera omdirigering eller tackmeddelande

I formulär som skapats med den universella redigeraren kan formulärförfattare konfigurera vad som ska hända när en användare skickar ett formulär. Du kan antingen visa ett tackmeddelande eller dirigera om användaren till en viss webbsida via fliken Skicka i tillägget Redigera formuläregenskaper.

Du kan konfigurera Thankyou-meddelandet eller Rediect URL:er för formulär som har skapats i Universal Editor med fliken **Submission** i tillägget **AEM Form Properties**.

## Förutsättningar

Du kan konfigurera åtgärden skicka för formulär som har skapats i den universella redigeraren med fliken **Skicka** i tillägget **Redigera formuläregenskaper** .

![Ikon för formuläregenskaper](/help/forms/assets/ue-form-properties-icon.png)

![Formuläregenskaper för Universal Editor](/help/forms/assets/ue-form-properties.png)

>[!NOTE]
>
> * Om ikonen **Formuläregenskaper** inte visas i det universella redigeringsgränssnittet aktiverar du tillägget **Redigera formuläregenskaper** i Extension Manager.
> * Läs artikeln [Extension Manager Feature Highlights](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions) om du vill veta hur du aktiverar eller inaktiverar tillägg i den universella redigeraren.

## Hur konfigurerar jag omdirigering eller tackar för ditt meddelande?

När du skickar ett formulär kan du dirigera om användaren till en annan webbsida eller visa ett meddelande.

Så här konfigurerar du omdirigeringssidan eller tackar för meddelandet:

1. Öppna det adaptiva formuläret för redigering.
2. Öppna innehållsträdet och välj **[!UICONTROL Guide Container]**.
3. Klicka på ikonen för den adaptiva formulärbehållaren ![Egenskaper för den adaptiva formulärbehållaren](/help/forms/assets/configure-icon.svg) . Dialogrutan Adaptiv formulärbehållare öppnas för att konfigurera datamodeller.
4. Öppna fliken **[!UICONTROL Submission]**. Alternativ för att konfigurera en omdirigeringssida eller ett meddelande visas:

   ![Dialogrutan Skicka i Guide Container för att konfigurera en omdirigeringssida eller ett meddelande](/help/forms/assets/adaptive-forms-core-components-redirect-page-or-thank-you-message.png)

**Konfigurera omdirigerings-URL:er**

* Om du vill konfigurera en omdirigerings-URL för alternativet Skicka markerar du **[!UICONTROL Redirect to URL option]** och anger en absolut adress eller en omdirigerings-URL eller relativ sökväg för en AEM Sites-sida.

![omdirigering](/help/edge/docs/forms/universal-editor/assets/redirect-ue.png)

**Konfigurera tackmeddelande**

* Om du vill konfigurera ett anpassat meddelande eller ett tackmeddelande väljer du alternativet **[!UICONTROL Show Message]** och anger ett meddelande i rutan Meddelandeinnehåll. Det är en RTF-ruta som du kan använda helskärmsalternativet för att visa alla tillgängliga RTF-objekt.

![tack](/help/edge/docs/forms/universal-editor/assets/thankyou-ue.png)

Formulärförfattare kan konfigurera en sida för varje formulär som formuläranvändarna omdirigeras till efter att de har skickat in formuläret.



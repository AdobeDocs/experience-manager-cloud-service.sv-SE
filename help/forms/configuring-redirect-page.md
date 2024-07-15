---
title: Hur konfigurerar jag en omdirigeringssida?
description: Lär dig hur användare kan dirigeras om till en webbsida som formulärförfattare kan konfigurera när de skapar formuläret.
feature: Adaptive Forms, Foundation Components
role: User, Developer
level: Intermediate
exl-id: e4dc01d2-7c89-4bd8-af0a-1d2df4676a9a
source-git-commit: 2b76f1be2dda99c8638deb9633055e71312fbf1e
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 2%

---

# Konfigurerar omdirigeringssida {#configuring-redirect-page}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/configuring-redirect-page.html) |
| AEM as a Cloud Service | Den här artikeln |

Formulärförfattare kan konfigurera en sida för varje formulär som formuläranvändarna omdirigeras till efter att de har skickat in formuläret.

1. Markera en komponent i redigeringsläget, klicka på ![fältnivå](assets/select_parent_icon.svg) > **[!UICONTROL Adaptive Form Container]** och klicka sedan på ![cmpr](assets/configure-icon.svg).

1. Klicka på **[!UICONTROL Submission]** i sidlisten.

1. Ange URL:en för omdirigeringssidan under **[!UICONTROL Redirect URL/Path]** i avsnittet **[!UICONTROL Submission]**.
1. Under Skicka-åtgärd kan du som alternativ konfigurera parametern som ska skickas till omdirigeringssidan för slutpunktsåtgärden Skicka till REST.

   ![Konfiguration av omdirigeringssida](assets/redirect-url.png)

   Omdirigeringssidkonfiguration

Formulärförfattare kan använda följande parametrar som skickas till sidan Tack. `status`- och `owner`-parametrar skickas för alla tillgängliga överföringsåtgärder. Förutom dessa två parametrar skickas ytterligare några parametrar för följande Skicka-åtgärder:

* **[!UICONTROL Submit to REST endpoint]**: Parametrar som har lagts till för mappning mellan fältparametrar skickas. Parametrarna `status` och `owner` skickas inte i den här åtgärden. Mer information finns i [Konfigurera åtgärden Skicka till REST-slutpunkt](configuring-submit-actions.md).

>[!MORELIKETHIS]
>
>* [Konfigurera en omdirigeringssida eller tacka dig för meddelandet](/help/forms/configure-redirect-page-or-thank-you-message.md)

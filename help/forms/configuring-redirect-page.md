---
title: Hur konfigurerar jag en omdirigeringssida?
description: Lär dig hur användare kan dirigeras om till en webbsida som formulärförfattare kan konfigurera när de skapar formuläret.
feature: Adaptive Forms
role: User
level: Intermediate
exl-id: e4dc01d2-7c89-4bd8-af0a-1d2df4676a9a
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '174'
ht-degree: 0%

---

# Konfigurerar omdirigeringssida {#configuring-redirect-page}

Formulärförfattare kan konfigurera en sida för varje formulär som formuläranvändarna omdirigeras till efter att de har skickat in formuläret.

1. Markera en komponent i redigeringsläget och klicka sedan på ![fältnivå](assets/select_parent_icon.svg) > **[!UICONTROL Adaptive Form Container]** och klicka sedan på ![cmppr](assets/configure-icon.svg).

1. Klicka på **[!UICONTROL Submission]**.

1. Ange URL:en för omdirigeringssidan under **[!UICONTROL Redirect URL/Path]** i **[!UICONTROL Submission]** -avsnitt.
1. Under Skicka-åtgärd kan du som alternativ konfigurera parametern som ska skickas till omdirigeringssidan för slutpunktsåtgärden Skicka till REST.

   ![Omdirigeringssidkonfiguration](assets/redirect-url.png)

   Omdirigeringssidkonfiguration

Formulärförfattare kan använda följande parametrar som skickas till sidan Tack. För alla tillgängliga Skicka-åtgärder `status` och `owner` parametrar skickas. Förutom dessa två parametrar skickas ytterligare några parametrar för följande Skicka-åtgärder:

* **[!UICONTROL Submit to REST endpoint]**: Parametrar som lagts till för mappning mellan fältparametrar skickas. `status` och `owner` parametrar skickas inte i den här åtgärden. Mer information finns i [Konfigurera åtgärden Skicka till REST-slutpunkt](configuring-submit-actions.md).

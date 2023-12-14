---
title: Identifiera duplicerade resurser för [!DNL Adobe Experience Manager] som [!DNL Cloud Service]
description: Lär dig hur du identifierar dubblettresurser
contentOwner: KK
mini-toc-levels: 3
feature: Asset Management,Publishing,Collaboration,Asset Processing
role: User,Architect,Admin
exl-id: 40f63933-4f4e-4318-8d42-4b5c9b01f7cd
source-git-commit: f18b8cf1922f05c0d7da2c58fb0a57bc5ff3d3b7
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 3%

---


| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM as a Cloud Service | Den här artikeln |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/duplicate-detection.html?lang=en) |

# Identifiera duplicerade resurser {#detect-duplicate-assets}

Om en DAM-användare överför en eller flera resurser som redan finns i databasen, [!DNL Experience Manager] identifierar dupliceringen och meddelar användaren. Dubblettidentifiering är inaktiverat som standard eftersom det kan påverka prestanda beroende på databasens storlek och antalet överförda resurser.

Så här aktiverar du funktionen:

1. Navigera till **[!UICONTROL Tools > Assets > Assets Configurations]**.

1. Klicka på **[!UICONTROL Asset Duplication Detector]**.

1. På [!UICONTROL Asset Duplication Detector page], klicka **[!UICONTROL Enabled]**.

   `dam:sha1` värdet för fältet Identifiera metadata ser till att duplicerade resurser identifieras även om filnamnen är olika.

1. Klicka på **[!UICONTROL Save]**.

   ![Identifierare för resursduplicering](assets/asset-duplication-detector.png)

>[!NOTE]
>
>Om du har konfigurerat dupliceringsavkännaren med `/apps/example/config.author/com.adobe.cq.assetcompute.impl.assetprocessor.AssetDuplicationDetector.cfg.json` konfigurationsfilen (OSGi-konfiguration) kan du fortsätta att använda den, men Adobe rekommenderar att du använder den nya metoden.


När den är aktiverad skickar Experience Manager meddelanden om duplicerade resurser till Inkorgen Experience Manager. Det är ett aggregerat resultat för flera dubbletter. Användarna kan välja att ta bort resurserna baserat på resultatet.

![Inkorgsmeddelande för duplicerade resurser](assets/duplicate-detect-inbox-notification.png)

>[!NOTE]
>
>När du överför resurser till databasen upptäcker Experience Manager duplicering och meddelar dig om de första 100 duplicerade resurserna.

---
title: Identifiera duplicerade resurser för  [!DNL Adobe Experience Manager]  som en [!DNL Cloud Service]
description: Lär dig hur du identifierar dubblettresurser
contentOwner: KK
mini-toc-levels: 3
feature: Asset Management, Publishing,Collaboration, Asset Processing
role: User, Developer, Admin
exl-id: 40f63933-4f4e-4318-8d42-4b5c9b01f7cd
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 3%

---


# Identifiera duplicerade resurser {#detect-duplicate-assets}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/duplicate-detection.html?lang=en) |
| AEM as a Cloud Service | Den här artikeln |

Om en DAM-användare överför en eller flera resurser som redan finns i databasen, upptäcker [!DNL Experience Manager] dupliceringen och meddelar användaren. Dubblettidentifiering är inaktiverat som standard eftersom det kan påverka prestanda beroende på databasens storlek och antalet överförda resurser.

Så här aktiverar du funktionen:

1. Navigera till **[!UICONTROL Tools > Assets > Assets Configurations]**.

1. Klicka på **[!UICONTROL Asset Duplication Detector]**.

1. Klicka på [!UICONTROL Asset Duplication Detector page] på **[!UICONTROL Enabled]**.

   Värdet `dam:sha1` för fältet Identifiera metadata ser till att dubblettresurser identifieras även om filnamnen är olika.

1. Klicka på **[!UICONTROL Save]**.

   ![Identifierare för resursduplicering](assets/asset-duplication-detector.png)

>[!NOTE]
>
>Om du har konfigurerat Duplication Detector med konfigurationsfilen `/apps/example/config.author/com.adobe.cq.assetcompute.impl.assetprocessor.AssetDuplicationDetector.cfg.json` (OSGi-konfiguration) kan du fortsätta att använda den, men Adobe rekommenderar att du använder den nya metoden.


När den är aktiverad skickar Experience Manager meddelanden om duplicerade resurser till Experience Manager Inbox. Det är ett aggregerat resultat för flera dubbletter. Användarna kan välja att ta bort resurserna baserat på resultatet.

![Inkorgsmeddelande för duplicerade resurser](assets/duplicate-detect-inbox-notification.png)

>[!NOTE]
>
>När du överför resurser till databasen upptäcker Experience Manager duplicering och meddelar dig om de första 100 duplicerade resurserna.

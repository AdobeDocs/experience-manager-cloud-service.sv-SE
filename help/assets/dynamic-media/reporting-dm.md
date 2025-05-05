---
title: Rapportering i Dynamic Media
description: Lär dig hur du begär en felrapport för Dynamic Media-leverans av URL:er som misslyckas.
contentOwner: Rick Brough
feature: Asset Management
role: User
hide: true
hidefromtoc: true
exl-id: 2488f813-df15-4dbb-8747-f827ee5925e1
source-git-commit: 36ab36ba7e14962eba3947865545b8a3f29f6bbc
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---

# Begär en felrapport för dynamiska medieleverans URL:er som inte fungerar

Du kan begära en felrapport som identifierar dynamiska medie-URL:er som misslyckades vid leveransen. Rapporten är en sammanställning av data upp till fem dagar och är tillgänglig i CSV-format. Felrapporten innehåller följande information:

* Misslyckad URL för leverans av dynamiska media - En felaktig URL är en URL som genereras av dynamiska media och som inte kan producera något innehåll vid leveransen.
* Referens-URL - Den refererande URL som den felaktiga leverans-URL:en anropas från.
* Antal fel - Det antal gånger som leverans-URL:en lästes in som resulterade i ett fel.

När du begär felrapporten mejlar Adobe Dynamic Media-teamet rapporten till dig i CSV-format. Det täcker en femdagarsperiod från den dag då din begäran gjordes.

Du kan begära en felrapport en gång i månaden för ett visst företag.

**Om du vill begära en felrapport för dynamiska medieleverans URL:er som inte fungerar:**

1. [Skicka ett e-postmeddelande till reports-dynamic-media@adobe.com](mailto:reports-dynamic-media@adobe.com) med det företagsnamn som är associerat med ditt Dynamic Media-konto.

   Om du inte känner till företagsnamnet kan du gå till sidan [Dynamisk mediekonfiguration](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/config-dm.html?lang=sv-SE#configuring-dynamic-media-cloud-services) i **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Dynamic Media Configuation]**. Klicka på **[!UICONTROL global]** på sidan Dynamic Media Configuration Browser, markera kryssrutan *[Dynamic_Media_folder_icon]* och välj sedan **[!UICONTROL Edit]**. Du måste ha administratörsbehörighet i AEM för att få åtkomst till sidan Dynamic Media Configuration.

   ![Öppnar sidan för dynamisk mediekonfiguration.](/help/assets/dynamic-media/assets/reporting-accessdmconfig.png)

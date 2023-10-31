---
title: Rapportering i Dynamic Media
description: Lär dig hur du begär en felrapport för att Dynamic Media ska kunna leverera URL:er som inte fungerar.
contentOwner: Rick Brough
feature: Asset Management
role: User
hide: true
hidefromtoc: true
exl-id: 2488f813-df15-4dbb-8747-f827ee5925e1
source-git-commit: aa7429d9ca9f67979303c0b85c9dbd5b8c74c05c
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 0%

---

# Begär en felrapport för Dynamic Media-leverans-URL:er som misslyckas

Du kan begära en felrapport som identifierar Dynamic Media-URL:er som misslyckades vid leveransen. Rapporten är en sammanställning av data upp till fem dagar och är tillgänglig i CSV-format. Felrapporten innehåller följande information:

* Misslyckad Dynamic Media-leverans-URL - En felaktig URL är en URL som genererats av Dynamic Media och som inte kan producera något innehåll vid leveranstillfället.
* Referens-URL - Den refererande URL som den felaktiga leverans-URL:en anropas från.
* Antal fel - Det antal gånger som leverans-URL:en lästes in som resulterade i ett fel.

När du begär felrapporten skickar Adobe Dynamic Media-teamet rapporten med e-post till dig i CSV-format. Det täcker en femdagarsperiod från den dag då din begäran gjordes.

Du kan begära en felrapport en gång i månaden för ett visst företag.

**Så här begär du en felrapport för Dynamic Media URL:er som inte kan levereras:**

1. [Skicka e-post till reports-dynamic-media@adobe.com](mailto:reports-dynamic-media@adobe.com) med det företagsnamn som är kopplat till ditt Dynamic Media-konto.

   Om du inte känner till företagsnamnet kan du läsa [Dynamic Media Configuration](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/config-dm.html?lang=en#configuring-dynamic-media-cloud-services) sida in **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Dynamic Media Configuation]**. Klicka på Dynamic Media Configuration Browser **[!UICONTROL global]** väljer du *[Dynamic_Media_folder_icon]* kryssruta och sedan markera **[!UICONTROL Edit]**. Du måste ha administratörsbehörighet i AEM för att komma åt sidan Dynamic Media-konfiguration.

   ![Öppnar konfigurationssidan för Dynamic Media.](/help/assets/dynamic-media/assets/reporting-accessdmconfig.png)

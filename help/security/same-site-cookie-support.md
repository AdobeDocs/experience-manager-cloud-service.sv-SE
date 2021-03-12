---
title: Stöd för samma webbplats-cookie för Adobe Experience Manager som en Cloud Service
description: Stöd för samma webbplats-cookie för Adobe Experience Manager som en Cloud Service
translation-type: tm+mt
source-git-commit: e51d9c3e4691fb58f3c4b6a2565cc8cad2a1acb0
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 0%

---


# Stöd för samma webbplats-cookie för Adobe Experience Manager som en Cloud Service {#same-site-cookie-support-for-adobe-experience-manager-as-a-cloud-service}

Sedan version 80 har Chrome och senare Safari introducerat en ny modell för cookie-säkerhet. Det här läget är utformat för att införa säkerhetskontroller runt tillgängligheten av cookies till tredjepartswebbplatser, via en inställning som heter `SameSite`. Mer information finns i den här [artikeln](https://web.dev/samesite-cookies-explained/).

Standardvärdet för den här inställningen (`SameSite=Lax`) kan göra att autentisering mellan AEM instanser eller tjänster inte fungerar. Detta beror på att domänerna eller URL-strukturerna för dessa tjänster kanske inte omfattas av begränsningarna i den här cookie-principen.

För att komma runt detta måste du ange attributet SameSite cookie till `None` för inloggningstoken.

Du kan göra detta genom att följa stegen nedan:

1. Installera en version av AEM SDK Quickstart lokalt
1. Gå till webbkonsolen på `http://serveraddress:serverport/system/console/configMgr`
1. Sök efter och klicka på **Autentiseringshanteraren för Adobe Granite-token**
1. Ange **SameSite-attributet för cookie** för inloggningstoken till `None`, vilket visas i bilden nedan
   ![samma webbplats](/help/security/assets/samesite1.png)
1. Klicka på Spara
1. Generera JSON-formatkonfigurationer för den här inställningen genom att följa stegen som beskrivs i [Generera OSGi-konfigurationer med AEM SDK QuickStart](/help/implementing/deploying/configuring-osgi.md#generating-osgi-configurations-using-the-aem-sdk-quickstart)
1. Använd inställningarna genom att följa stegen i [API-formatet för Cloud Manager för att ställa in egenskaper](/help/implementing/deploying/configuring-osgi.md#cloud-manager-api-format-for-setting-properties) OSGi-dokumentationen.

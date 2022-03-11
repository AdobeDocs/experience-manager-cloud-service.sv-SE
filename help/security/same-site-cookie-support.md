---
title: Stöd för samma webbplats-cookie för Adobe Experience Manager as a Cloud Service
description: Stöd för samma webbplats-cookie för Adobe Experience Manager as a Cloud Service
exl-id: 2cec7202-4450-456f-8e62-b7ed3791505c
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 0%

---

# Stöd för samma webbplats-cookie för Adobe Experience Manager as a Cloud Service {#same-site-cookie-support-for-adobe-experience-manager-as-a-cloud-service}

Sedan version 80 har Chrome och senare Safari introducerat en ny modell för cookie-säkerhet. Det här läget är utformat för att införa säkerhetskontroller för tillgänglighet av cookies för tredjepartswebbplatser via en inställning som kallas `SameSite`. Mer detaljerad information finns i [artikel](https://web.dev/samesite-cookies-explained/).

Standardvärdet för den här inställningen (`SameSite=Lax`) kan leda till att autentisering mellan AEM instanser eller tjänster inte fungerar. Detta beror på att domänerna eller URL-strukturerna för dessa tjänster kanske inte omfattas av begränsningarna i den här cookie-principen.

För att komma runt detta måste du ange attributet SameSite cookie till `None` för inloggningstoken.

Du kan göra detta genom att följa stegen nedan:

1. Installera en version av AEM SDK Quickstart lokalt
1. Gå till webbkonsolen på `http://serveraddress:serverport/system/console/configMgr`
1. Sök efter och klicka på **Autentiseringshanterare för Adobe Granite-token**
1. Ange **Attributet SameSite för cookie-filen för inloggningstoken** till `None`, vilket visas i bilden nedan
   ![samma webbplats](/help/security/assets/samesite1.png)
1. Klicka på Spara
1. Generera JSON-formatkonfigurationer för den här inställningen genom att följa stegen som beskrivs i [Generera OSGi-konfigurationer med AEM SDK QuickStart](/help/implementing/deploying/configuring-osgi.md#generating-osgi-configurations-using-the-aem-sdk-quickstart)
1. Använd inställningarna genom att följa stegen i [API-format för Cloud Manager för att ange egenskaper](/help/implementing/deploying/configuring-osgi.md#cloud-manager-api-format-for-setting-properties) OSGi-dokumentation.

När den här inställningen har uppdaterats och användarna har loggat ut och loggat in igen, `login-token` cookies har `None` och kommer att inkluderas i förfrågningar mellan webbplatser.

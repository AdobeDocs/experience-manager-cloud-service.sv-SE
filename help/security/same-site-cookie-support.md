---
title: Stöd för samma webbplats-cookie för Adobe Experience Manager as a Cloud Service
description: Stöd för samma webbplats-cookie för Adobe Experience Manager as a Cloud Service.
exl-id: 2cec7202-4450-456f-8e62-b7ed3791505c
feature: Security
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%

---

# Stöd för samma webbplats-cookie för Adobe Experience Manager as a Cloud Service {#same-site-cookie-support-for-adobe-experience-manager-as-a-cloud-service}

Sedan version 80 har Chrome och senare Safari infört en ny modell för cookie-säkerhet. Det här läget är utformat för att införa säkerhetskontroller för tillgänglighet av cookies till tredjepartswebbplatser, via en inställning som kallas `SameSite`. Mer detaljerad information finns i den här [artikeln](https://web.dev/articles/samesite-cookies-explained).

Standardvärdet för den här inställningen (`SameSite=Lax`) kan göra att autentisering mellan AEM instanser eller tjänster inte fungerar. Detta beror på att domänerna eller URL-strukturerna för dessa tjänster kanske inte omfattas av begränsningarna i den här cookie-principen.

Du kan undvika detta genom att ange attributet SameSite cookie till `None` för inloggningstoken.

>[!CAUTION]
>
>Inställningen `SameSite=None` används bara om protokollet är säkert (HTTPS).
>
>Om protokollet inte är säkert (HTTP) ignoreras inställningen och det här varningsmeddelandet visas på servern:
>
>`WARN com.day.crx.security.token.TokenCookie Skip 'SameSite=None'`

Du kan lägga till inställningen genom att följa stegen nedan:

1. Installera en version av AEM SDK Quickstart lokalt
1. Gå till webbkonsolen på `http://serveraddress:serverport/system/console/configMgr`
1. Sök efter och klicka på autentiseringshanteraren **Adobe Granite**
1. Ange attributet **SameSite för cookien** för inloggningstoken till `None`, vilket visas i bilden nedan
   ![samesite](/help/security/assets/samesite1.png)
1. Klicka på Spara
1. Generera JSON-formatkonfigurationer för den här inställningen genom att följa stegen i [Generera OSGi-konfigurationer med AEM SDK QuickStart](/help/implementing/deploying/configuring-osgi.md#generating-osgi-configurations-using-the-aem-sdk-quickstart)
1. Använd inställningarna genom att följa stegen i dokumentationen för [Cloud Manager API-format för inställning av egenskaper](/help/implementing/deploying/configuring-osgi.md#cloud-manager-api-format-for-setting-properties) för OSGi.

När den här inställningen har uppdaterats och användarna har loggat ut och loggat in igen, har `login-token` cookies attributet `None` angivet och ingår i förfrågningar mellan webbplatser.

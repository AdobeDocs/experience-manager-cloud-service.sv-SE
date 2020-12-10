---
title: Introduktion - Hantera SSL-certifikat
description: Introduktion - Hantera SSL-certifikat
translation-type: tm+mt
source-git-commit: 5ebe94c8562b952521effa3b67267c3eab925d16
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---


# Introduktion {#introduction}

Med Cloud Manager kan kunderna själva installera SSL-certifikat via användargränssnittet i Cloud Manager. Cloud Manager använder en TLS-tjänst för plattform för att hantera SSL-certifikat och privata nycklar som ägs av kunder och vanligtvis hämtas från tredjepartscertifikatutfärdare, till exempel Låt oss kryptera.

>[!IMPORTANT]
>Molnhanteraren tillhandahåller inte SSL-certifikat eller privata nycklar. Dessa måste inhämtas från certifieringsmyndigheter från tredje part. Mer information finns i [Hämta ett SSL-certifikat](/help/implementing/cloud-manager/managing-ssl-certifications/get-ssl-certificate.md).

>[!NOTE]
>AEM som Cloud Service har bara stöd för säkra https-platser. Kunder med flera anpassade domäner vill inte överföra ett certifikat varje gång de lägger till en domän. Detta innebär att sådana kunder kan dra nytta av att få ett certifikat med flera domäner.

Cloud Manager stöder följande SSL-certifikatkrav för kunder:

* Ett SSL-certifikat kan användas i flera miljöer, det vill säga lägga till en gång och använda flera gånger.
* Varje Cloud Manager-miljö kan använda flera certifikat.
* En privat nyckel kan utfärda flera SSL-certifikat.
* Varje certifikat innehåller vanligtvis flera domäner.
* Plattformens TLS-tjänst skickar förfrågningar till kundens CDN-tjänst baserat på det SSL-certifikat som används för att avsluta och den CDN-tjänst som är värd för domänen.

Med hjälp av SSL-certifikat för användargränssnittet i Cloud Manager kan en användare med behörighet utföra flera åtgärder för att hantera SSL-certifikat för ett program:

* Lägga till ett SSL-certifikat
* Visa, uppdatera eller ersätta ett SSL-certifikat
   >[!NOTE]
   >Med de här åtgärderna kan du visa information eller ersätta ett certifikat som snart upphör att gälla.
* Ta bort ett SSL-certifikat
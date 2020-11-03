---
title: Introduktion - Hantera SSL-certifikat
description: Introduktion - Hantera SSL-certifikat
translation-type: tm+mt
source-git-commit: 74cc587874c4d0a0ef9b542549801198d4f2d7a5
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---


# Introduktion {#introduction}

Med Cloud Manager kan kunderna själva installera SSL-certifikat via användargränssnittet i Cloud Manager. Cloud Manager använder en TLS-tjänst för plattform för att hantera SSL-certifikat och privata nycklar som ägs av kunder och vanligtvis hämtas från tredjepartscertifikatutfärdare, till exempel Låt oss kryptera.

>[!IMPORTANT]
>Molnhanteraren tillhandahåller inte SSL-certifikat eller privata nycklar. Dessa måste inhämtas från certifieringsmyndigheter från tredje part. Mer information finns i Så här får du ett SSL-certifikat. INFOGA LÄNK

>[!NOTE]
>AEM som Cloud Service har bara stöd för säkra https-platser. Kunder med flera anpassade domäner vill inte överföra ett certifikat varje gång de lägger till en domän. Detta innebär att sådana kunder kan dra nytta av att få ett certifikat med flera domäner.

Cloud Manager stöder följande SSL-certifikatkrav för kunder:

* Ett SSL-certifikat kan användas i flera miljöer - Lägg till en gång och använd flera gånger.
* Varje Cloud Manager-miljö kan använda flera certifikat.
* En privat nyckel kan utfärda flera SSL-certifikat.
* Varje certifikat innehåller vanligtvis flera domäner.
* Plattformens TLS-tjänst skickar förfrågningar till kundens CDN-tjänst baserat på det SSL-certifikat som används för att avsluta och den CDN-tjänst som är värd för domänen.

Med hjälp av SSL-certifikat för användargränssnittet i Cloud Manager kan en användare med behörighet utföra flera åtgärder för att hantera SSL-certifikat för ett program:

* Lägger till ett SSL-certifikat.
* Visa, uppdatera eller ersätta ett SSL-certifikat. Med de här åtgärderna kan du visa information eller ersätta ett certifikat som snart upphör att gälla.
* Tar bort ett SSL-certifikat.
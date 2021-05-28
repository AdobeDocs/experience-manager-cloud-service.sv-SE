---
title: Introduktion - Hantera SSL-certifikat
description: Introduktion - Hantera SSL-certifikat
exl-id: 0d41723c-c096-4882-a3fd-050b7c9996d8
source-git-commit: dfbd0f38017d02810da05ccadbc5f2fbd5826aa3
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 0%

---

# Introduktion {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_sslcert"
>title="Hantera SSL-certifikat"
>abstract="Med Cloud Manager kan kunderna själva installera SSL-certifikat via användargränssnittet i Cloud Manager. Cloud Manager använder en TLS-tjänst för plattform för att hantera SSL-certifikat och privata nycklar som ägs av kunder och vanligtvis hämtas från tredjepartscertifikatutfärdare."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-ssl-certificates/view-update-replace-ssl-certificate.html" text="Visa, uppdatera och ersätta ett SSL-certifikat"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-ssl-certificates/check-status-ssl-certificate.html" text="Kontrollera status för ett SSL-certifikat"


Med Cloud Manager kan kunderna själva installera SSL-certifikat via användargränssnittet i Cloud Manager. Cloud Manager använder en TLS-tjänst för plattform för att hantera SSL-certifikat och privata nycklar som ägs av kunder och vanligtvis hämtas från tredjepartscertifikatutfärdare, till exempel *Låt oss kryptera*.

## Viktiga överväganden {#important-considerations}

* Molnhanteraren tillhandahåller inte SSL-certifikat eller privata nycklar. Dessa måste inhämtas från certifieringsmyndigheter från tredje part. Mer information finns i [Hämta ett SSL-certifikat](/help/implementing/cloud-manager/managing-ssl-certifications/get-ssl-certificate.md).

* AEM som Cloud Service har bara stöd för säkra `https`-platser. Kunder med flera anpassade domäner vill inte överföra ett certifikat varje gång de lägger till en domän. Detta innebär att sådana kunder kan dra nytta av att få ett certifikat med flera domäner.

* AEM som Cloud Service accepterar endast OV- (Organization Validation) eller EV-certifikat (Extended Validation). DV-certifikat (domänvalidering) godkänns inte. Dessutom måste alla certifikat vara ett X.509 TLS-certifikat från en betrodd certifikatutfärdare (CA) med en matchande 2 048-bitars RSA privat nyckel.

* AEM som Cloud Service accepterar SSL-jokertecken för en domän.

Cloud Manager stöder följande SSL-certifikatkrav för kunder:

* Ett SSL-certifikat kan användas i flera miljöer, det vill säga lägga till en gång och använda flera gånger.
* Varje Cloud Manager-miljö kan använda flera certifikat.
* En privat nyckel kan utfärda flera SSL-certifikat.
* Varje certifikat innehåller vanligtvis flera domäner.
* Plattformens TLS-tjänst skickar förfrågningar till kundens CDN-tjänst baserat på det SSL-certifikat som används för att avsluta och den CDN-tjänst som är värd för domänen.

Med hjälp av SSL-certifikat för användargränssnittet i Cloud Manager kan en användare med behörighet utföra flera åtgärder för att hantera SSL-certifikat för ett program:

* [Lägga till ett SSL-certifikat](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)
* [Visa, uppdatera eller ersätta ett SSL-certifikat](/help/implementing/cloud-manager/managing-ssl-certifications/view-update-replace-ssl-certificate.md)
   >[!NOTE]
   >Med de här åtgärderna kan du visa information eller ersätta ett certifikat som snart upphör att gälla.
* [Ta bort ett SSL-certifikat](/help/implementing/cloud-manager/managing-ssl-certifications/delete-ssl-certificate.md)

---
title: Introduktion - Hantera SSL-certifikat
description: Introduktion - Hantera SSL-certifikat
exl-id: 0d41723c-c096-4882-a3fd-050b7c9996d8
source-git-commit: 09a2c24b848364954dc5621995d0d0dc24059011
workflow-type: tm+mt
source-wordcount: '463'
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

* Molnhanteraren tillhandahåller inte SSL-certifikat eller privata nycklar. Dessa måste inhämtas från certifieringsmyndigheter från tredje part. Se [Hämta ett SSL-certifikat](/help/implementing/cloud-manager/managing-ssl-certifications/get-ssl-certificate.md) om du vill veta mer.

* AEM as a Cloud Service stöder endast `https` webbplatser. Kunder med flera anpassade domäner vill inte överföra ett certifikat varje gång de lägger till en domän. Detta innebär att sådana kunder kan dra nytta av att få ett certifikat med flera domäner.

* AEM as a Cloud Service godkänner endast certifikat som överensstämmer med OV- (Organization Validation) eller EV-principen (Extended Validation). DV-principen (Domain Validation) accepteras inte. Dessutom måste alla certifikat vara ett X.509 TLS-certifikat från en betrodd certifikatutfärdare (CA) med en matchande 2 048-bitars RSA privat nyckel.

* AEM as a Cloud Service godkänner SSL-jokertecken för en domän.

* Molnhanteraren tillåter vid en given tidpunkt högst 50 SSL-certifikat som kan kopplas till en eller flera miljöer i ditt program, även om ett certifikat har gått ut. Molnhanterarens användargränssnitt tillåter dock att upp till 50 SSL-certifikat installeras i programmet med den här begränsningen. Ett certifikat kan vanligtvis omfatta flera domäner (upp till 100 SAN-nätverk). Överväg därför att gruppera flera domäner i samma certifikat för att hålla sig inom denna gräns.

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

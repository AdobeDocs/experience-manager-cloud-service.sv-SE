---
title: Introduktion till IP Tillåtelselista
description: Lär dig hur IP tillåtelselista kan begränsa från vilka adresser användare kan få åtkomst till domäner AEM as a Cloud Service.
exl-id: 352fae8e-d116-40b0-ba54-d7f001f076e8
source-git-commit: f0edd0e3deeba89dcbd2dc1a07859138b24e2220
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---


# Introduktion till IP Tillåtelselista {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_ipallowlist"
>title="Hantera IP-tillåtelselista"
>abstract="AEM som molntjänst är tillgänglig via Internet och skyddas genom användarautentisering och behörighet. Cloud Managers IP-tillåtelselista kan användas för att begränsa och styra åtkomsten enbart till betrodda IP-adresser. Användare av Cloud Manager med lämplig behörighet kan skapa tillåtelselista med betrodda IP-adresser från vilka webbplatsens användare kan komma åt sina AEM domäner."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/ip-allow-lists/add-ip-allow-lists.html" text="Lägg till en IP-Tillåtelselista"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/ip-allow-lists/managing-ip-allow-lists.html" text="Visa och uppdatera en IP-Tillåtelselista"

AEM som molntjänst är som standard tillgänglig via Internet. Säkerhet hanteras genom användarautentisering och -auktorisering, men IP-registrering är ett sätt att begränsa åtkomsten enbart till betrodda IP-adresser.

Cloud Managers IP-tillåtelselista kan användas för att begränsa och styra åtkomsten enbart till sådana betrodda IP-adresser. Cloud Manager-användare med lämplig behörighet kan [skapa tillåtelselista](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md) av betrodda IP-adresser från vilka webbplatsens användare kan komma åt sina AEM domäner.

När du har lagt till [IP-tillåtelselista kan tillämpas/inte tillämpas](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) flera gånger som en enhet eller enhet till en författare och/eller utgivartjänst i en miljö.

>[!NOTE]
>
>Om ingen IP-tillåtelselista används tillåts som standard alla IP-adresser. När ett IP-tillåtelselista används tillåts inga IP-adresser förutom adresser på IP-tillåtelselista.

## Begränsningar {#limitations}

Det finns flera begränsningar för IP-tillåtelselista att tänka på.

* Högst 50 IP-tillåtelselista kan läggas till i programmet
* Högst 50 IP/CIDR-adresser kan läggas till i varje IP-tillåtelselista.
* Namn på IP-tillåtelselista stöds i Cloud Manager för författare, publiceringstjänst, eller båda, i en miljö.

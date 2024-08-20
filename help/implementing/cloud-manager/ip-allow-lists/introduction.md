---
title: Introduktion till IP Tillåtelselista
description: Lär dig hur IP Tillåtelselista kan begränsa från vilka adresser användare kan få åtkomst till domäner i AEM as a Cloud Service.
exl-id: 352fae8e-d116-40b0-ba54-d7f001f076e8
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: f4c6331491bb08e81964476ad58065c1ee022967
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---


# Introduktion till IP Tillåtelselista {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_ipallowlist"
>title="Hantera IP-Tillåtelselista"
>abstract="AEM as a Cloud Service är tillgängligt via Internet och skyddas genom användarautentisering och behörighet. Cloud Manager IP Tillåtelselista kan användas för att begränsa och styra åtkomsten enbart till betrodda IP-adresser. Cloud Manager-användare med lämplig behörighet kan skapa tillåtelselista med betrodda IP-adresser från vilka webbplatsens användare kan komma åt sina AEM domäner."
>additional-url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/ip-allow-lists/add-ip-allow-lists" text="Lägg till en IP-Tillåtelselista"
>additional-url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/ip-allow-lists/managing-ip-allow-lists" text="Visa och uppdatera en IP-Tillåtelselista"

AEM som molntjänst är som standard tillgänglig via Internet. Säkerhet hanteras genom användarautentisering och -auktorisering, men IP-registrering är ett sätt att begränsa åtkomsten enbart till betrodda IP-adresser.

Cloud Manager IP Tillåtelselista kan bara användas för att begränsa och styra åtkomsten till betrodda IP-adresser. Cloud Manager-användare med lämplig behörighet kan [skapa IP-Tillåtelselista](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md) med betrodda IP-adresser som webbplatsens användare kan komma åt sina AEM.

När du har lagt till [IP-Tillåtelselista kan det användas eller tas bort ](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) flera gånger som en enhet eller entitet i en författartjänst, en utgivartjänst eller båda delarna, i en miljö.

>[!NOTE]
>
>Om IP Tillåtelselista inte används tillåts som standard alla IP-adresser. När ett IP-Tillåtelselista används tillåts inga IP-adresser förutom adresser på IP-Tillåtelselista.

## Begränsningar {#limitations}

Det finns flera begränsningar för IP-Tillåtelselista att tänka på.

* Högst 50 IP-Tillåtelselista kan läggas till i programmet.
* Högst 50 IP/CIDR-adresser kan läggas till i varje IP-Tillåtelselista.
* IP-Tillåtelselista-namn stöds i Cloud Manager för författartjänsten, eller publiceringstjänsten, eller båda, i en miljö.

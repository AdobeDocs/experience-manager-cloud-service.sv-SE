---
title: Introduktion till IP Tillåtelselista
description: Lär dig hur IP tillåtelselista kan begränsa från vilka adresser användare kan få åtkomst till dina AEM as a Cloud Service domäner.
exl-id: 352fae8e-d116-40b0-ba54-d7f001f076e8
source-git-commit: 8d1680fa8dbaaefa297cf8c6698097b3c7acc48d
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 0%

---


# Introduktion till IP Tillåtelselista {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_ipallowlist"
>title="Hantera IP-Tillåtelselista"
>abstract="AEM som molntjänst är tillgänglig via Internet och skyddas genom användarautentisering och auktorisering. Cloud Managers IP-tillåtelselista kan användas för att begränsa och styra åtkomsten enbart till betrodda IP-adresser. Användare av Cloud Manager med lämplig behörighet kan skapa tillåtelselista med betrodda IP-adresser från vilka webbplatsens användare kan komma åt sina AEM domäner."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/ip-allow-lists/add-ip-allow-lists.html" text="Lägg till en IP-Tillåtelselista"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/ip-allow-lists/view-update-ip-allow-list.html" text="Visa och uppdatera en IP-Tillåtelselista"

AEM som molntjänst är tillgänglig via Internet och skyddas genom användarautentisering och auktorisering. Cloud Managers IP-tillåtelselista kan användas för att begränsa och styra åtkomsten enbart till betrodda IP-adresser. Användare av Cloud Manager med lämplig behörighet kan skapa tillåtelselista med betrodda IP-adresser från vilka webbplatsens användare kan komma åt sina AEM domäner.

IP-tillåtelselista kan läggas till en gång och tillämpas/tas bort flera gånger som en enhet eller enhet till en författare och/eller utgivartjänst i en miljö.

## Begränsningar {#limitations}

Det finns ett antal begränsningar för IP-tillståndslistor att tänka på.

* Du kan lägga till högst 50 IP-tillåtelselista i programmet
* Högst 50 IP/CIDR-adresser kan läggas till i varje IP-tillåtelselista.
* IP tillåtelselista-namn stöds i Cloud Manager för författare och/eller publiceringstjänst i en miljö.

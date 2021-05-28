---
title: Introduktion - IP-Tillåtelselista i Cloud Manager
description: Introduktion - IP-Tillåtelselista i Cloud Manager
exl-id: 352fae8e-d116-40b0-ba54-d7f001f076e8
source-git-commit: dfbd0f38017d02810da05ccadbc5f2fbd5826aa3
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 0%

---

# Introduktion {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_ipallowlist"
>title="Hantera IP-Tillåtelselista"
>abstract="AEM som en molntjänst är öppen för Internet och säkerheten hanteras via användarautentisering och behörighet. Listan över tillåtna IP-adresser är en funktion i Cloud Manager som används för att begränsa och styra åtkomsten enbart till betrodda användare. Med den här funktionen kan användare med behörigheter skapa Tillåt-listor med betrodda IP-adresser som deras webbplatsanvändare kan komma åt sina AEM domäner från."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/ip-allow-lists/add-ip-allow-lists.html" text="Lägg till en IP-Tillåtelselista"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/ip-allow-lists/view-update-ip-allow-list.html" text="Visa och uppdatera en IP-Tillåtelselista"

AEM som en molntjänst är öppen för Internet och säkerheten hanteras via användarautentisering och behörighet. Listan över tillåtna IP-adresser är en funktion i Cloud Manager som används för att begränsa och styra åtkomsten enbart till betrodda användare. Med den här funktionen kan användare med behörigheter skapa Tillåt-listor med betrodda IP-adresser som deras webbplatsanvändare kan komma åt sina AEM domäner från.

IP-Tillåtelselista kan läggas till en gång och tillämpas/tas bort flera gånger som en enhet eller enhet i en författare- och/eller utgivartjänst i en miljö.

>[!NOTE]
>IP Tillåtelselista-namn stöds i Cloud Manager för författare och/eller publiceringstjänst i en miljö.

Med hjälp av IP-Tillåtelselista-sidan för användargränssnittet i Cloud Manager eller miljöinformationssidan kan en användare med behörighet utföra flera åtgärder för att hantera IP-Tillåtelselista för dina miljöer, bland annat:

* [Lägga till en IP-Tillåtelselista](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md)
   >[!NOTE]
   > Du kan lägga till en gång och återanvända eller tillämpa regeln hur många gånger som helst mellan olika tjänster i programmet.
* [Visa eller uppdatera en IP-Tillåtelselista](/help/implementing/cloud-manager/ip-allow-lists/view-update-ip-allow-list.md)
* [Använda eller ta bort tillämpning av ett IP-Tillåtelselista](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md)
* [Ta bort en IP-Tillåtelselista](/help/implementing/cloud-manager/ip-allow-lists/delete-ip-allow-list.md)

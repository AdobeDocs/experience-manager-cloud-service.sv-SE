---
title: Använd och inaktivera IP-Tillåtelselista
description: Lär dig hur du använder och tar bort användningen av IP Tillåtelselista i Cloud Manager-miljöer.
exl-id: 7158496c-b0c4-4228-a306-71dc51003c57
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 593b8c704c5b016bb55ae6a25420b577044b4126
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 0%

---


# Använd och ta bort tillämpning av IP-Tillåtelselista {#apply-allow-list}

När du använder IP Tillåtelselista kopplas alla IP-intervall som ingår i listdefinitionen till en författare eller publiceringstjänst i en miljö. Att ta bort en lista är omvänt.

{{add-cm-allowlist-frontend-pipeline}}
{{ip-allow-lists-ue}}

## Använd IP-Tillåtelselista {#applying}

En användare i rollen **Affärsägare** eller **Distributionshanterare** kan följa de här stegen för att tillämpa en IP-Tillåtelselista.

**Så här använder du IP-Tillåtelselista:**

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/).
1. Välj lämplig organisation.
1. Välj programmet på konsolen **[Mina program](/help/implementing/cloud-manager/navigation.md#my-programs)**.
1. Navigera från sidan **Översikt** till skärmen **Miljö**.
1. Navigera till sidan med miljöinformation på skärmen **Miljö**.
1. Navigera till tabellen **IP Tillåtelselista**.
1. Använd inmatningsfälten högst upp i tabellen så att du kan välja IP-Tillåtelselista och den redigerings-, publicerings- eller förhandsgranskningstjänst som du vill använda den på.
IP-Tillåtelselista måste redan finnas i Cloud Manager för att det ska kunna användas. Se [Lägg till IP-Tillåtelselista](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md).
1. Klicka på ![Lägg till ikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Add_18_N.svg) **Använd** och bekräfta överföringen.

## Ta bort IP-Tillåtelselista {#un-applying}

En användare i rollen **Affärsägare** eller **Distributionshanterare** kan följa de här stegen för att ta bort en IP-Tillåtelselista.

**Så här tar du bort IP-Tillåtelselista:**

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/).
1. Välj lämplig organisation.
1. Välj programmet på konsolen **[Mina program](/help/implementing/cloud-manager/navigation.md#my-programs)**.
1. Gå till sidan **Miljö** från sidan **Översikt**.
1. Navigera till den specifika sidan med miljöinformation.
1. Bläddra från fliken Allmänt till tabellen **IP Tillåtelselista**.
1. Identifiera den rad i IP-Tillåtelselista som du vill ta bort.
1. Klicka på ikonen ![Mer](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) till höger om den identifierade raden.
1. Klicka på **Ta bort**.
1. Klicka på **Ta bort tillämpning** i dialogrutan **Ta bort IP-Tillåtelselista**.

---
title: Använda och inte använda IP-Tillåtelselista
description: Lär dig hur du använder och tar bort användningen av IP-tillåtelselista i miljöer.
exl-id: 7158496c-b0c4-4228-a306-71dc51003c57
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 0%

---


# Använda och inte använda IP-Tillåtelselista {#apply-allow-list}

När du använder en IP-tillåtelselista kopplas alla IP-intervall som ingår i listdefinitionen till en författare eller publiceringstjänst i en miljö. Att ta bort en lista är omvänt.

## Använder IP-Tillåtelselista {#applying}

En användare i rollen **Affärsägare** eller **Distributionshanterare** kan följa de här stegen för att tillämpa en IP-tillåtelselista.

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj lämplig organisation.

1. Välj programmet på konsolen **[Mina program](/help/implementing/cloud-manager/navigation.md#my-programs)**.
1. Gå till skärmen **Miljö** från sidan **Översikt**.
1. Navigera till den specifika miljöinformationssidan på skärmen **Miljöer** och navigera till tabellen **IP Tillåtelselista**.
1. Använd inmatningsfälten högst upp i tabellen så att du kan välja IP tillåtelselista och författaren eller publiceringstjänsten som du vill använda den på.
   * IP-Tillåtelselista måste finnas i Cloud Manager för att det ska kunna användas.
1. Klicka på **Använd** och bekräfta ditt bidrag.

## Tillåtelselista som inte används {#un-applying}

En användare i rollen **Affärsägare** eller **Distributionshanterare** kan följa de här stegen för att ta bort en IP-tillåtelselista.

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj rätt organisation och program.
1. Gå till skärmen **Miljö** från sidan **Översikt**.
1. Navigera till den specifika miljöinformationssidan på skärmen **Miljöer** och navigera till tabellen **IP Tillåtelselista**.
1. Identifiera raden i IP-tillåtelselista som du vill ta bort.
1. Markera ellipsknappen längst till höger på raden.
1. Välj alternativet **Ta bort tillämpning** och bekräfta överföringen.

---
title: Använda och inte använda IP-Tillåtelselista
description: Lär dig hur du använder och tar bort användningen av IP-tillåtelselista i miljöer.
exl-id: 7158496c-b0c4-4228-a306-71dc51003c57
source-git-commit: 90250c13c5074422e24186baf78f84c56c9e3c4f
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 0%

---


# Använda och inte använda IP-Tillåtelselista {#apply-allow-list}

När du använder en IP-tillåtelselista kopplas alla IP-intervall som ingår i listdefinitionen till en författare eller publiceringstjänst i en miljö. Att ta bort en lista är omvänt.

## Använder IP-Tillåtelselista {#applying}

En användare i **Företagsägare** eller **Distributionshanteraren** kan följa de här stegen för att använda en IP-tillåtelselista.

1. Logga in i Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välja lämplig organisation.

1. På **[Mina program](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md#my-programs)** väljer du programmet.
1. Navigera till **Miljö** från **Ökning** sida.
1. Navigera till den specifika miljöinformationssidan på sidan **Miljö** och navigera till **IP TILLÅTELSELISTA** tabell.
1. Använd inmatningsfälten högst upp i tabellen så att du kan välja IP tillåtelselista och författaren eller publiceringstjänsten som du vill använda den på.
   * IP-Tillåtelselista måste finnas i Cloud Manager för att det ska kunna användas.
1. Klicka **Använd** och bekräfta ditt bidrag.

## Tillåtelselista som inte används {#un-applying}

En användare i **Företagsägare** eller **Distributionshanteraren** kan följa de här stegen för att ta bort en IP-tillåtelselista.

1. Logga in i Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välja lämplig organisation och lämpligt program.
1. Navigera till **Miljö** från **Ökning** sida.
1. Navigera till den specifika miljöinformationssidan på sidan **Miljö** och navigera till **IP TILLÅTELSELISTA** tabell.
1. Identifiera raden i IP-tillåtelselista som du vill ta bort.
1. Markera ellipsknappen längst till höger på raden.
1. Välj **Oanvänd** och bekräfta ditt bidrag.

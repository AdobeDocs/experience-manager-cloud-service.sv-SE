---
title: Lägger till IP-Tillåtelselista
description: Lär dig hur du lägger till egna IP-tillåtelselista med hjälp av Cloud Manager.
exl-id: 769be71f-5c11-4f98-8906-7a5667a25aee
source-git-commit: 5ad33f0173afd68d8868b088ff5e20fc9f58ad5a
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---


# Lägga till en IP-Tillåtelselista {#add-ip-allow-list}

Lär dig hur du lägger till egna IP-tillåtelselista med hjälp av Cloud Manager.

En användare i **Företagsägare** eller **Distributionshanteraren** kan följa de här stegen för att lägga till ett IP-tillåtelselista.

1. Logga in i Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välja lämplig organisation och lämpligt program.

1. Navigera till **Miljö** från **Ökning** sida.

1. Navigera till **IP-Tillåtelselista** sidan från **Miljö** skärm.

   ![Alternativet IP-tillåtelselista på sidopanelen](/help/implementing/cloud-manager/assets/ip-allow-list/ip-allow-list-create.png)

1. Klicka **Lägg till IP Tillåtelselista** för att öppna **Lägg till IP Tillåtelselista** -dialogrutan.

   ![Dialogrutan Lägg till IP-Tillåtelselista](/help/implementing/cloud-manager/assets/ip-allow-list/ip-allow-list-create02.png)

1. Ange ett namn som du vill använda som referens för tillåtelselista i dialogrutan **IP-Tillåtelselista namn** fält.

   * Namnet är endast informativt och bör vara beskrivande så att du lättare kan identifiera listan.

1. Ange ett IP- eller IP CIDR-block i dialogrutan **IP-adress/CIDR** fält.

   * Flera block kan avgränsas med kommatecken eller tabbar.

1. Klicka **Spara** för att bekräfta ditt bidrag.

När du har sparat visas det nyligen skapade IP-tillåtelselista som en rad i tabellen i **IP-Tillåtelselista** sida.

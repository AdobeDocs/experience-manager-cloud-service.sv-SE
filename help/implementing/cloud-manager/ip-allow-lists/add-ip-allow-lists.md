---
title: Lägger till IP-Tillåtelselista
description: Lär dig hur du lägger till egna IP-tillåtelselista med Cloud Manager.
exl-id: 769be71f-5c11-4f98-8906-7a5667a25aee
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 0%

---


# Lägga till en IP-Tillåtelselista {#add-ip-allow-list}

Lär dig hur du lägger till egna IP-tillåtelselista med Cloud Manager.

En användare i rollen **Affärsägare** eller **Distributionshanterare** kan följa de här stegen för att lägga till ett IP-tillåtelselista.

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj lämplig organisation.

1. Välj programmet på konsolen **[Mina program](/help/implementing/cloud-manager/navigation.md#my-programs)**.

1. Navigera från sidan **Översikt** till sidan **IP-Tillåtelselista** med hjälp av sidnavigeringsfliken.

   ![Alternativet IP-tillåtelselista på sidpanelen](/help/implementing/cloud-manager/assets/ip-allow-list/ip-allow-list-create.png)

1. Klicka på **Lägg till IP Tillåtelselista**.

   ![Dialogrutan Lägg till IP-Tillåtelselista](/help/implementing/cloud-manager/assets/ip-allow-list/ip-allow-list-create02.png)

1. I dialogrutan **Lägg till IP Tillåtelselista** anger du ett namn som du vill använda för att referera till tillåtelselista i fältet **IP-Tillåtelselista namn**.

   * Namnet är endast informativt och bör vara beskrivande så att du lättare kan identifiera listan.

1. Ange ett IP- eller IP CIDR-block i fältet **IP-adress/CIDR**.

   * Flera block kan avgränsas med kommatecken eller tabbar.

1. Klicka på **Spara**.

När du har sparat visas det nyligen skapade IP-tillåtelselista som en rad i tabellen på sidan **IP Tillåtelselista**.

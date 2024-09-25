---
title: Lägg till IP-Tillåtelselista
description: Lär dig hur du lägger till egna IP-Tillåtelselista med Cloud Manager.
exl-id: 769be71f-5c11-4f98-8906-7a5667a25aee
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: b9fb178760b74cb0e101506b6a9ff5ae30c18490
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 0%

---


# Lägg till en IP-Tillåtelselista {#add-ip-allow-list}

Lär dig hur du lägger till egna IP-Tillåtelselista med Cloud Manager.

En användare i rollen **Affärsägare** eller **Distributionshanterare** kan följa de här stegen för att lägga till en IP-Tillåtelselista.

{{add-cm-allowlist-frontend-pipeline}}

**Så här lägger du till en IP-Tillåtelselista:**

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj lämplig organisation.

1. Välj programmet på konsolen **[Mina program](/help/implementing/cloud-manager/navigation.md#my-programs)**.

1. På sidan **Programöversikt** klickar du med sidopanelen (du kan behöva klicka på ![Visa menyikonen](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) i det övre vänstra hörnet för att visa panelen) på ![ikonen för uppgiftslistan](https://spectrum.adobe.com/static/icons/workflow_18/Smock_TaskList_18_N.svg) **IP-Tillåtelselista**.

   ![Alternativet IP-Tillåtelselista på sidpanelen](/help/implementing/cloud-manager/assets/ip-allow-list/ip-allow-list-create.png)

1. Klicka på **Lägg till IP Tillåtelselista** i det övre högra hörnet på IP Tillåtelselista-sidan.

   ![Dialogrutan Lägg till IP-Tillåtelselista](/help/implementing/cloud-manager/assets/ip-allow-list/ip-allow-list-create02.png)

1. I dialogrutan **Lägg till IP Tillåtelselista** anger du ett namn som du vill använda som referens för IP-Tillåtelselista i fältet **IP-Tillåtelselista**. Det här namnet är endast information. Se till att det är tillräckligt beskrivande för att du ska kunna identifiera listan.

1. Ange ett IP- eller IP CIDR-block i fältet **IP-adress/CIDR**. Avgränsa flera block med kommatecken eller tabbar.

1. Klicka på **Spara**.

När du har sparat visas den nyligen skapade IP-Tillåtelselista som en rad i tabellen på sidan **IP Tillåtelselista**.


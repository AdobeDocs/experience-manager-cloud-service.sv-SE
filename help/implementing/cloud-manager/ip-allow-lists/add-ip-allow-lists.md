---
title: Lägg till IP-Tillåtelselista
description: Lär dig hur du lägger till egna IP-Tillåtelselista med Cloud Manager.
exl-id: 769be71f-5c11-4f98-8906-7a5667a25aee
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 1415d07235641262814e81362c806572bcf582ba
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 0%

---


# Lägg till en IP-Tillåtelselista {#add-ip-allow-list}

Lär dig hur du lägger till egna IP-Tillåtelselista med Cloud Manager.

En användare i rollen **Affärsägare** eller **Distributionshanterare** kan följa de här stegen för att lägga till en IP-Tillåtelselista.

{{add-cm-allowlist-frontend-pipeline}}

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj lämplig organisation.

1. Välj programmet på konsolen **[Mina program](/help/implementing/cloud-manager/navigation.md#my-programs)**.

1. På sidan **Programöversikt** klickar du på **IP-Tillåtelselista** med sidopanelen till vänster (du kan behöva klicka på hamburgikonen i det övre vänstra hörnet för att se panelen).

   ![Alternativet IP-Tillåtelselista på sidpanelen](/help/implementing/cloud-manager/assets/ip-allow-list/ip-allow-list-create.png)

1. Klicka på **Lägg till IP Tillåtelselista** i det övre högra hörnet på IP Tillåtelselista-sidan.

   ![Dialogrutan Lägg till IP-Tillåtelselista](/help/implementing/cloud-manager/assets/ip-allow-list/ip-allow-list-create02.png)

1. I dialogrutan **Lägg till IP Tillåtelselista** anger du ett namn som du vill använda som referens för IP-Tillåtelselista i fältet **IP-Tillåtelselista**. Det här namnet är endast information. Se till att det är tillräckligt beskrivande för att du ska kunna identifiera listan.

1. Ange ett IP- eller IP CIDR-block i fältet **IP-adress/CIDR**. Avgränsa flera block med kommatecken eller tabbar.

1. Klicka på **Spara**.

När du har sparat visas den nyligen skapade IP-Tillåtelselista som en rad i tabellen på sidan **IP Tillåtelselista**.

## Lägg till Cloud Manager IP Tillåtelselista {#add-cm-allowlist}

För detta krävs att följande Cloud Manager IP Tillåtelselista läggs till i förväg.

**Cloud Manager IP Tillåtelselista**

`52.254.106.192/28,20.186.185.181,52.254.106.240/28,52.254.107.128/28,52.254.105.192/28,52.254.106.176/28,20.186.185.227,52.254.106.144/28,52.254.107.64/28,20.186.185.239,20.22.83.112,52.254.107.80/28,52.254.107.144/28,52.254.106.224/28,20.14.241.153,52.254.107.0/28,52.254.107.32/28,52.254.106.208/28,40.70.154.136/29,52.254.106.160/28,52.254.107.16/28,52.254.106.0/28,4.152.211.251`

Om du vill undvika avbrott i körningen av frontendpipeline måste du se till att den här Cloud Manager IP-Tillåtelselista har lagts till och sedan tillämpas på miljöns författartjänst *innan* du aktiverar pipelinen.

**Så här lägger du till Cloud Manager IP Tillåtelselista:**

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj lämplig organisation.

1. Välj programmet på konsolen **[Mina program](/help/implementing/cloud-manager/navigation.md#my-programs)**.

1. På sidan **Programöversikt** klickar du på **IP-Tillåtelselista** med sidopanelen till vänster (du kan behöva klicka på hamburgikonen i det övre vänstra hörnet för att se panelen).

1. Klicka på **Lägg till IP Tillåtelselista** i det övre högra hörnet på IP Tillåtelselista-sidan.

1. I dialogrutan **Lägg till IP Tillåtelselista** skriver du *`Cloud Manager`* i fältet **IP Tillåtelselista name**.

1. Kopiera blocket med Cloud Manager IP Tillåtelselista-adresser ovan. Varje adress är redan avgränsad med kommatecken.

1. Klistra in blocket i fältet **IP-adress/CIDR** i dialogrutan **Lägg till IP-Tillåtelselista**.

1. Placera markören precis efter det första kommatecknet i adresslistan och tryck på **Retur**.

1. Klicka på **Spara**.

[Använd nu Cloud Manager IP Tillåtelselista](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) i dina programmiljöer.




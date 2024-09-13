---
title: Hantera CDN-konfigurationer
description: Lär dig hur du använder Cloud Manager för att redigera och uppdatera eller ta bort CDN-konfigurationer för en Edge Delivery-webbplats eller en Cloud Manager-miljö.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 70f99cfb2cd00278d9ebbb7972ef455af7a87a1b
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 0%

---


# Hantera CDN-konfigurationer {#manage-cdn-configurations}

Lär dig hur du använder Cloud Manager för att redigera och uppdatera eller ta bort CDN-konfigurationer för en Edge Delivery-webbplats eller en Cloud Manager-miljö.

## Redigera en CDN-konfiguration {#edit-cdn}

När du redigerar en CDN-konfiguration kan du justera inställningar som miljöns nivå (Publish eller Preview) eller SSL-certifikat, utan att helt ta bort den befintliga konfigurationen. Ändringarna gäller den valda miljön, till exempel staging eller production, och kan påverka hur innehållet levereras och skyddas.

En användare måste vara medlem i rollen **Affärsägare** eller **Distributionshanterare** för att den här aktiviteten ska kunna slutföras.

**Så här redigerar du en CDN-konfiguration:**

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj rätt organisation och program.

1. Klicka på **CDN-konfigurationer** under **Tjänster** i den vänstra navigeringspanelen.

1. I tabellen **CDN-konfigurationer** klickar du på ellipsen i slutet av en rad vars CDN du vill uppdatera.

   ![Redigera en CDN-konfiguration](/help/implementing/cloud-manager/assets/cdn-config-edit.png)

1. Klicka på **Redigera**.

1. I dialogrutan **Redigera CDN** anger du ett eller flera alternativ i respektive listruta.

   Vilka alternativ som visas i dialogrutan kan variera beroende på om du använder ett CDN som hanteras av Adobe eller ett kundhanterat CDN.

1. Klicka på **Uppdatera**.

   Statusen för det redigerade CDN uppdateras i tabellen **CDN-konfigurationer** för att återspegla de ändringar du har gjort.


## Ta bort en CDN-konfiguration {#delete-cdn}

När du tar bort en CDN-konfiguration som hanteras av Adobe eller hanteras av kund i Adobe Cloud Manager tas den associerade domänens inställningar för routning och SSL-certifikat bort. Domänen använder inte längre CDN för trafikleveranser och eventuella säkerhets- eller prestandaförbättringar som tillhandahålls av CDN går förlorade. Tjänsten kan avbrytas tills en ny konfiguration har konfigurerats, oavsett om du lägger till det borttagna CDN-numret igen eller lägger till ett nytt.

En användare måste vara medlem i rollen **Affärsägare** eller **Distributionshanterare** för att den här aktiviteten ska kunna slutföras.

**Så här tar du bort en CDN-konfiguration:**

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj rätt organisation och program.

1. Klicka på **CDN-konfigurationer** under **Tjänster** i den vänstra navigeringspanelen.

1. I tabellen CDN-konfigurationer klickar du på ellipsen i slutet av en rad vars CDN du vill ta bort.

   ![Tar bort en CDN-konfiguration](/help/implementing/cloud-manager/assets/cdn-config-delete.png)

1. Klicka på **Ta bort**.
1. Klicka på **Ta bort** igen för att bekräfta borttagningen av platsens CDN.



---
title: Hantera domänmappningar
description: Lär dig hur du använder Cloud Manager för att redigera och uppdatera eller ta bort CDN-konfigurationer för en Edge Delivery-webbplats eller en Cloud Manager-miljö.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
exl-id: 2ec16c91-0195-4732-a26d-ac223e10afb9
source-git-commit: 1683d53491e06ebe2dfcc96184ce251539ecf732
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 0%

---

# Hantera domänmappningar {#manage-cdn-configurations}

Lär dig hur du använder Cloud Manager för att redigera eller ta bort CDN-konfigurationer för en Edge Delivery-webbplats eller en Cloud Manager-miljö.

## Redigera en CDN-konfiguration från sidan Domänmappningar {#edit-cdn}

I Adobe Cloud Manager kan du av flera anledningar redigera en CDN-konfiguration (Content Delivery Network), inklusive miljönivån (Publish eller Preview) och SSL-certifikat.

* **Miljöförändringar**: Justering av nivån hjälper dig att matcha CDN-inställningarna med rätt miljö, oavsett om det gäller direktproduktion (Publish) eller testning (förhandstitt).
* **Säkerhetsförbättringar**: Det kan vara nödvändigt att välja ett annat SSL-certifikat när du uppdaterar certifikat eller åtgärdar kompatibilitets- och säkerhetsbehov.
* **Optimera prestanda**: Om du redigerar konfigurationen säkerställs att rätt CDN-inställningar används för att leverera innehåll baserat på förändrade operativa behov.

Du kan redigera en konfiguration utan att helt ta bort den befintliga konfigurationen. Ändringarna gäller den valda miljön, till exempel staging eller production, och kan påverka hur innehållet levereras och skyddas.

En användare måste vara medlem i rollen **Affärsägare** eller **Distributionshanterare** för att den här aktiviteten ska kunna slutföras.

**Så här redigerar du en CDN-konfiguration från sidan Domänmappningar:**

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj rätt organisation och program.
1. Klicka på ikonen ![Sociala nätverk](https://spectrum.adobe.com/static/icons/workflow_18/Smock_SocialNetwork_18_N.svg) **Domänmappningar** på den vänstra menyn under **Tjänster**.
1. I tabellen **Domänmappningar** klickar du på ikonen ![Mer](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) i slutet av en rad vars CDN-konfiguration du vill uppdatera.

1. Klicka på **Redigera** i listrutan.

1. I dialogrutan **Redigera CDN-konfiguration** anger du ett eller flera alternativ i respektive listruta.

   Vilka alternativ som visas i dialogrutan beror på om du använder en **CDN som hanteras av Adobe** eller en **annan CDN-leverantör** (kundhanterad CDN).

1. Klicka på **Uppdatera**.

   Statusen för det redigerade CDN uppdateras i tabellen **Domänmappningar** för att återspegla de ändringar du har gjort.


## Redigera en CDN-konfiguration från sidan Miljöer

Stegen för att redigera en CDN-konfiguration från sidan **Miljö** är nästan samma som när du [redigerar en CDN-konfiguration från sidan Domänmappningar](#edit-cdn), men startpunkten skiljer sig åt.

**Så här redigerar du en CDN-konfiguration från miljösidan:**

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj rätt organisation och program.

1. Klicka på ikonen ![Data](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Data_18_N.svg) **Miljö** på den vänstra menyn.

1. Välj en miljö av intresse på sidan **Miljö**.

1. På sidan med miljöinformation i grupperingen Domänmappningar klickar du på ikonen ![Mer](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) som motsvarar den CDN-konfiguration som du vill redigera.

1. Klicka på **Redigera** på snabbmenyn.

1. I dialogrutan **Redigera CDN-konfiguration** anger du ett eller flera alternativ i respektive listruta.

   Vilka alternativ som visas i dialogrutan beror på om du använder en **CDN som hanteras av Adobe** eller en **annan CDN-leverantör** (kundhanterad CDN).

1. Klicka på **Uppdatera**.


<!-- ## Go live readiness {#go-live-readiness} 

1. ADD STEPS -->


## Ta bort en CDN-konfiguration {#delete-cdn}

När du tar bort en CDN-konfiguration som hanteras av Adobe eller hanteras av kund i Cloud Manager tas den associerade domänens inställningar för routning och SSL-certifikat bort. Domänen använder inte längre CDN för trafikleveranser och eventuella säkerhets- eller prestandaförbättringar som tillhandahålls av CDN går förlorade. Tjänsten kan avbrytas tills en ny konfiguration har konfigurerats, oavsett om du lägger till det borttagna CDN-numret igen eller lägger till ett nytt.

En användare måste vara medlem i rollen **Affärsägare** eller **Distributionshanterare** för att den här aktiviteten ska kunna slutföras.

**Så här tar du bort en CDN-konfiguration:**

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj rätt organisation och program.

1. Klicka på ikonen ![Sociala nätverk](https://spectrum.adobe.com/static/icons/workflow_18/Smock_SocialNetwork_18_N.svg) **Domänmappningar** på den vänstra menyn under **Tjänster**.

1. I tabellen Domänmappningar klickar du på ikonen ![Mer](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) i slutet av en rad som motsvarar det CDN som du vill ta bort och sedan på **Ta bort**.

1. Klicka på **Ta bort** i dialogrutan **Ta bort CDN-konfiguration**.

1. Klicka på **Ta bort** igen för att bekräfta borttagningen av platsens CDN.


## Ta bort en CDN-konfiguration från miljösidan

Stegen för att ta bort en CDN-konfiguration från sidan **Miljö** är nästan samma som när [en CDN-konfiguration tas bort från sidan Domänmappningar](#edit-cdn), men startpunkten skiljer sig åt.

**Så här tar du bort en CDN-konfiguration från miljösidan:**

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj rätt organisation och program.

1. Klicka på ikonen ![Data](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Data_18_N.svg) **Miljö** på den vänstra menyn.

1. Välj en miljö av intresse på sidan **Miljö**.

1. På sidan med miljöinformation i grupperingen **Domänmappningar** klickar du på ikonen ![Mer](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) som motsvarar den CDN-konfiguration som du vill ta bort och sedan på **Ta bort**.

1. Klicka på **Ta bort** i dialogrutan **Ta bort CDN-konfiguration**.

1. Klicka på **Ta bort** igen för att bekräfta borttagningen av platsens CDN.

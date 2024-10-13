---
title: Hantera CDN-konfigurationer
description: Lär dig hur du använder Cloud Manager för att redigera och uppdatera eller ta bort CDN-konfigurationer för en Edge Delivery-webbplats eller en Cloud Manager-miljö.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 42b30c12f17106610cfb7f7b4c04c5ab703bab45
workflow-type: tm+mt
source-wordcount: '650'
ht-degree: 0%

---


# Hantera CDN-konfigurationer (Content Delivery Network) {#manage-cdn-configurations}

Lär dig hur du använder Cloud Manager för att redigera och uppdatera eller ta bort CDN-konfigurationer för en Edge Delivery-webbplats eller en Cloud Manager-miljö.

## Redigera en CDN-konfiguration från sidan CDN-konfigurationer {#edit-cdn}

I Adobe Cloud Manager kan det finnas flera skäl till att du vill redigera en CDN-konfiguration, inklusive miljönivån (Publish eller Förhandsgranska) och SSL-certifikatet.

* **Miljöförändringar**: Justering av nivån hjälper dig att matcha CDN-inställningarna med rätt miljö, oavsett om det gäller direktproduktion (Publish) eller testning (förhandstitt).
* **Säkerhetsförbättringar**: Det kan vara nödvändigt att välja ett annat SSL-certifikat när du uppdaterar certifikat eller åtgärdar kompatibilitets- och säkerhetsbehov.
* **Optimera prestanda**: Om du redigerar konfigurationen säkerställs att rätt CDN-inställningar används för att leverera innehåll baserat på förändrade operativa behov.

Du kan redigera en konfiguration utan att helt ta bort den befintliga konfigurationen. Ändringarna gäller den valda miljön, till exempel staging eller production, och kan påverka hur innehållet levereras och skyddas.

En användare måste vara medlem i rollen **Affärsägare** eller **Distributionshanterare** för att den här aktiviteten ska kunna slutföras.

**Så här redigerar du en CDN-konfiguration från sidan CDN-konfigurationer:**

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj rätt organisation och program.
1. Klicka på ikonen ![Sociala nätverk](https://spectrum.adobe.com/static/icons/workflow_18/Smock_SocialNetwork_18_N.svg) **CDN-konfigurationer** i sidopanelen under **Tjänster**.
1. I tabellen **CDN-konfigurationer** klickar du på ikonen ![Mer](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) i slutet av en rad vars CDN-konfiguration du vill uppdatera.

   ![Redigera en CDN-konfiguration](/help/implementing/cloud-manager/assets/cdn-config-edit.png)

1. Klicka på **Redigera** i listrutan.
1. I dialogrutan **Redigera CDN-konfiguration** anger du ett eller flera alternativ i respektive listruta.

   Vilka alternativ som visas i dialogrutan beror på om du använder en **CDN som hanteras av Adobe** eller en **annan CDN-leverantör** (kundhanterad CDN).

1. Klicka på **Uppdatera**.

   Statusen för det redigerade CDN uppdateras i tabellen **CDN-konfigurationer** för att återspegla de ändringar du har gjort.

## Redigera en CDN-konfiguration från sidan Miljöer

Stegen för redigering av en CDN-konfiguration från sidan **Miljö** är nästan samma som när du [redigerar en CDN-konfiguration från sidan CDN-konfigurationer](#edit-cdn), men startpunkten skiljer sig åt.

**Så här redigerar du en CDN-konfiguration från miljösidan:**

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj rätt organisation och program.

1. Klicka på **Miljö** på den vänstra menyn.

1. Välj en miljö av intresse på sidan **Miljö**.

1. På sidan med miljöinformation i gruppen CDN-konfigurationer klickar du på ikonen ![Mer](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) som motsvarar den CDN-konfiguration som du vill redigera.

   ![Ange domännamn på sidan Miljöinformation](/help/implementing/cloud-manager/assets/cdn/environments-cdn-config.png)

1. Klicka på **Redigera** på snabbmenyn.

1. I dialogrutan **Redigera konfiguration** anger du ett eller flera alternativ i respektive listruta.

Vilka alternativ som visas i dialogrutan beror på om du använder en **CDN som hanteras av Adobe** eller en **annan CDN-leverantör** (kundhanterad CDN).

1. Klicka på **Uppdatera**.


<!-- ## Go live readiness {#go-live-readiness} 

1. ADD STEPS -->


## Ta bort en CDN-konfiguration {#delete-cdn}

När du tar bort en CDN-konfiguration som hanteras av Adobe eller hanteras av kund i Cloud Manager tas den associerade domänens inställningar för routning och SSL-certifikat bort. Domänen använder inte längre CDN för trafikleveranser och eventuella säkerhets- eller prestandaförbättringar som tillhandahålls av CDN går förlorade. Tjänsten kan avbrytas tills en ny konfiguration har konfigurerats, oavsett om du lägger till det borttagna CDN-numret igen eller lägger till ett nytt.

En användare måste vara medlem i rollen **Affärsägare** eller **Distributionshanterare** för att den här aktiviteten ska kunna slutföras.

**Så här tar du bort en CDN-konfiguration:**

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj rätt organisation och program.

1. Klicka på **CDN-konfigurationer** under **Tjänster** på den vänstra panelen.

1. I tabellen CDN-konfigurationer klickar du på ellipsen i slutet av en rad vars CDN du vill ta bort.

   ![Tar bort en CDN-konfiguration](/help/implementing/cloud-manager/assets/cdn-config-delete.png)

1. Klicka på **Ta bort**.

1. Klicka på **Ta bort** igen för att bekräfta borttagningen av platsens CDN.



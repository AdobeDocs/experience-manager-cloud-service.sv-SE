---
title: Hantera CDN-konfigurationer
description: Lär dig hur du använder Cloud Manager för att redigera och uppdatera eller ta bort CDN-konfigurationer för en Edge Delivery-webbplats eller en Cloud Manager-miljö.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: ff8c7fb21b4d8bcf395d28c194a7351281eef45b
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 0%

---


# Hantera CDN-konfigurationer (Content Delivery Network) {#manage-cdn-configurations}

Lär dig hur du använder Cloud Manager för att redigera och uppdatera eller ta bort CDN-konfigurationer för en Edge Delivery-webbplats eller en Cloud Manager-miljö.

## Redigera en CDN-konfiguration {#edit-cdn}

I Adobe Cloud Manager kan det finnas flera skäl till att du vill redigera en CDN-konfiguration, inklusive miljönivån (Publish eller Förhandsgranska) och SSL-certifikatet.

* **Miljöförändringar**: Justering av nivån hjälper dig att matcha CDN-inställningarna med rätt miljö, oavsett om det gäller direktproduktion (Publish) eller testning (förhandstitt).
* **Säkerhetsförbättringar**: Det kan vara nödvändigt att välja ett annat SSL-certifikat när du uppdaterar certifikat eller åtgärdar kompatibilitets- och säkerhetsbehov.
* **Optimera prestanda**: Om du redigerar konfigurationen säkerställs att rätt CDN-inställningar används för att leverera innehåll baserat på förändrade operativa behov.

Du kan redigera en konfiguration utan att helt ta bort den befintliga konfigurationen. Ändringarna gäller den valda miljön, till exempel staging eller production, och kan påverka hur innehållet levereras och skyddas.

En användare måste vara medlem i rollen **Affärsägare** eller **Distributionshanterare** för att den här aktiviteten ska kunna slutföras.

**Så här redigerar du en CDN-konfiguration:**

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj rätt organisation och program.
1. Klicka på ikonen ![Sociala nätverk](https://spectrum.adobe.com/static/icons/workflow_18/Smock_SocialNetwork_18_N.svg) **CDN-konfigurationer** i sidopanelen under **Tjänster**.
1. I tabellen **CDN-konfigurationer** klickar du på ikonen ![Mer](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) i slutet av en rad vars CDN-konfiguration du vill uppdatera.

   ![Redigera en CDN-konfiguration](/help/implementing/cloud-manager/assets/cdn-config-edit.png)

1. Klicka på **Redigera** i listrutan.
1. I dialogrutan **Redigera CDN-konfiguration** anger du ett eller flera alternativ i respektive listruta.

   Vilka alternativ som visas i dialogrutan kan variera beroende på om du använder ett CDN som hanteras av Adobe eller ett kundhanterat CDN.

1. Klicka på **Uppdatera**.

   Statusen för det redigerade CDN uppdateras i tabellen **CDN-konfigurationer** för att återspegla de ändringar du har gjort.

<!-- ## ALTERNATE METHOD FOR EDITING A CDN CONFIGURATION from the Environments page
    
    The steps for adding a custom domain name from the **Environments** page are the same as when [adding a custom domain name from the Domain Settings page](#adding-cdn-settings), but the entry point differs. Follow these steps to add a custom domain name from the **Environments** page.
    
    1. Log into Cloud Manager at [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) and select the appropriate organization and program.
    
    1. Navigate to the **Environments Detail** detail page for the environment of interest.
    
       ![Entering domain name on the Environment Details page](/help/implementing/cloud-manager/assets/cdn/environments-cdn-config.png)
    
    1. Use the **Domain Names** table to submit the custom domain name.
    
       1. Enter the custom domain name.
       1. Select the SSL certificate associated with this name from the drop-down list.
       1. Click ![Add icon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Add_18_N.svg) **Add**.
    
       ![Add a custom domain name](/help/implementing/cloud-manager/assets/cdn/cdn-create3.png)
    
    1. The **Add domain name** dialog box opens to the **Domain Name** tab. Continue as you would for [adding a custom domain name from the Domain Settings page](#adding-cdn-settings). -->

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



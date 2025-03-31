---
title: Hantera domänmappningar
description: Lär dig hur du använder Cloud Manager för att redigera och uppdatera eller ta bort CDN-konfigurationer för en Edge Delivery-webbplats eller en Cloud Manager-miljö.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
exl-id: 2ec16c91-0195-4732-a26d-ac223e10afb9
source-git-commit: e3a8afaee6c3baeb593eb69a46648b0a8d2a069f
workflow-type: tm+mt
source-wordcount: '1073'
ht-degree: 0%

---

# Hantera domänmappningar {#manage-cdn-configurations}

Lär dig hur du använder Cloud Manager för att redigera eller ta bort CDN-konfigurationer för en Edge Delivery-webbplats eller en Cloud Manager-miljö.

## Redigera en CDN-konfiguration från sidan Domänmappningar {#edit-cdn}

I Adobe Cloud Manager kan du av flera anledningar redigera en CDN-konfiguration (Content Delivery Network), inklusive miljönivån (Publicera eller Förhandsgranska) och SSL-certifikat.

* **Miljöförändringar**: Justering av nivån hjälper dig att matcha CDN-inställningarna med rätt miljö, oavsett om det gäller liveproduktion (Publicera) eller testning (Förhandsgranska).
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

   Vilka alternativ som visas i dialogrutan beror på om du använder en **hanterad CDN** från Adobe eller en **annan CDN-leverantör** (kundhanterad CDN).

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

   Vilka alternativ som visas i dialogrutan beror på om du använder en **hanterad CDN** från Adobe eller en **annan CDN-leverantör** (kundhanterad CDN).

1. Klicka på **Uppdatera**.


## Gör dig redo live: Konfigurera DNS-inställningar för en anpassad domän {#go-live-readiness}

Innan en anpassad domän kan hantera trafik måste du slutföra DNS-konfigurationen med din DNS-leverantör. När du har distribuerat en domänmappning och klickat på **Go live** visar Cloud Manager en dialogruta som hjälper dig genom DNS-postkonfigurationen. Du kan välja att publicera genom att lägga till antingen en CNAME-posttyp eller en A-posttyp.

<!-- See also [APEX record](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md#adobe-managed-cert-cname-record#adobe-managed-cert-apex-record) and [CNAME record](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md#adobe-managed-cert-cname-record). -->

**Så här konfigurerar du Go live-beredskap:**

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj rätt organisation och program.
1. Klicka på ikonen ![Sociala nätverk](https://spectrum.adobe.com/static/icons/workflow_18/Smock_SocialNetwork_18_N.svg) **Domänmappningar** på den vänstra menyn under **Tjänster**.
1. I tabellen Domänmappningar klickar du på **Gå live** i slutet av en rad som motsvarar ett CDN vars live-beredskap du vill konfigurera.

   ![Dialogrutan Gå live-beredskap](/help/implementing/cloud-manager/assets/domain-mappings-go-live-readiness.png)

1. Gör något av följande i dialogrutan **Go live readiness** :

   | Alternativ | Steg |
   | --- | --- |
   | Konfigurera EN POST | Rekommenderas för rotdomäner som `example.com`<br><ol><li>Logga in på din DNS-tjänstleverantörs portal.<li>Gå till avsnittet DNS-poster.<li>Skapa en A-post för att peka på alla IP-adresser som visas.</li></ol> |
   | Konfigurera CNAME | Rekommenderas för anpassade domäner som `www.example.com`<br><ol><li>Logga in på DMS-tjänsteleverantörens portal.<li>Gå till avsnittet DNS-poster.<li>Mappa [cdn.adobeaemcloud.com](https://cdn.adobeaemcloud.com/) (CNAME-post) i DNS-posten för DNS-tjänstleverantören (din anpassade domän). Denna mappning säkerställer att begäranden som tas emot på den anpassade domänen dirigeras om till Adobe CDN.</li></ol> |

1. Klicka på **OK** i dialogrutan **Gå live-beredskap** för att spara posten.

   Vänta på DNS-spridning. Det kan ta flera minuter till några timmar.

   När kolumnen **[!UICONTROL Status]** i tabellen Domänmappningar uppdateras till **[!UICONTROL Verified]** är den anpassade domänen klar att användas. Du kan behöva klicka på ikonen ![Uppdatera](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Refresh_18_N.svg) för att uppdatera statusen.

## Ta bort en CDN-konfiguration {#delete-cdn}

När du tar bort en CDN-konfiguration som hanteras av Adobe eller av en kund i Cloud Manager tas den associerade domänens inställningar för routning och SSL-certifikat bort. Domänen använder inte längre CDN för trafikleveranser och eventuella säkerhets- eller prestandaförbättringar som tillhandahålls av CDN går förlorade. Tjänsten kan avbrytas tills en ny konfiguration har konfigurerats, oavsett om du lägger till det borttagna CDN-numret igen eller lägger till ett nytt.

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

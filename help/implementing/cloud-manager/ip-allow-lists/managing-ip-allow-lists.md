---
title: Hantera IP-Tillåtelselista
description: Lär dig hur du visar, redigerar, tar bort och kontrollerar status för IP-tillåtelselista i Cloud Manager.
exl-id: 6efabe53-3f45-47d4-ac1f-979cae0ab33e
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '789'
ht-degree: 0%

---

# Hantera IP-Tillåtelselista {#manage-ip-allow-lists}

Lär dig hur du visar, redigerar, tar bort och kontrollerar status för IP-tillåtelselista i Cloud Manager.

## Visa och uppdatera IP-Tillåtelselista {#update-ip-allow-lists}

En användare i rollen **Affärsägare** eller **Distributionshanterare** kan följa de här stegen för att visa och uppdatera ett IP-tillåtelselista.

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj lämplig organisation.
1. Välj programmet på konsolen **[Mina program](/help/implementing/cloud-manager/navigation.md#my-programs)**.
1. Gå till skärmen **Miljö** från sidan **Översikt**.
1. Navigera till sidan **IP Tillåtelselista** från skärmen **Environment**.
1. Identifiera raden för de IP-tillåtelselista som du vill visa eller uppdatera.
1. Klicka på ellipsknappen till höger om raden.
1. Välj alternativet **Visa och uppdatera**.
1. Guiden **Visa och uppdatera** visar namn, IP-adresser (eller intervall) som definierar regeln samt de miljöer och tjänster som regeln tillämpas på.
1. Ändra namn eller IP-adresser efter behov och bekräfta ditt bidrag.

Om du lägger till eller tar bort ett nytt IP-intervall i ett IP-tillåtelselista används/tas det automatiskt bort från alla motsvarande miljöer/tjänster som det tidigare tillämpades på.

Det går inte att uppdatera en IP-tillåtelselista medan en tidigare uppdatering pågår och inte har slutförts.

## Kontrollerar IP-Tillåtelselista status {#check-allow-list-status}

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj rätt organisation och program.

1. Gå till skärmen **Miljö** från sidan **Översikt**.

1. Klicka på ikonen **Status** för IP-tillåtelselista i tabellen på skärmen **Miljö** och markera sidan **IP Tillåtelselista**.

1. Cloud Manager visar status för tillåtelselista enligt beskrivningen [i följande avsnitt.](#status)

### Status för IP-Tillåtelselista {#status}

[Vid kontroll av status för IP-tillåtelselista kan ](#check-allow-list-status) ha något av följande värden.

* **Används** - IP-tillåtelselista har tillämpats på en eller flera miljöer.

* **Uppdaterar** - En uppdatering av IP-tillåtelselista pågår, vilket kan innehålla ett eller flera program eller att listan inte används.

   * Varje program/program som inte körs visas tillsammans med dess egen status **Inte startat**, **Pågår**, **Fullständigt** eller **Misslyckades**.

* **Misslyckades** - En eller flera program- eller avprogramprocesser för en uppdatering misslyckades.
   * Alla program och avaktiverade program visas tillsammans med programmets status.
      * Statusen är **Misslyckad** om ett program/ett program i uppdateringen misslyckas.
      * Statusen förblir **Misslyckad** tills alla fel har rensats.
         * Välj ikonen **Försök igen** bredvid statusen så att du kan åtgärda felet.
      * Du kan inte uppdatera eller ta bort en IP-tillåtelselista med statusen **Misslyckades**.

* **Tar bort** - en borttagning av ett IP-tillåtelselista pågår.
   * Borttagning innebär att listan inte används för alla tjänster.
   * Varje icke-program visas tillsammans med sin egen status **Inte startad**, **Pågår**, **Fullständigt** eller **Misslyckad**.
   * När borttagningen är klar:
      * IP-tillåtelselista visas inte i registret IP tillåtelselista.
      * IP-tillåtelselista används inte för någon tjänst i Cloud Manager.

* **Borttagningen misslyckades** - Ett eller flera program som inte kunde tas bort misslyckades under en borttagningsåtgärd.

   * Varje icke-program visas tillsammans med statusen **Fullständigt** eller **Misslyckat**.
   * Statusen blir **Ta bort misslyckades** om ett av programmen misslyckas.
   * Statusen förblir **Ta bort misslyckades** tills alla fel har rensats.
      * Välj **Ta bort** på ellipsmenyn längst till höger om raden i tabellen så att du kan ta bort eventuella fel.
   * Du kan inte uppdatera en IP-tillåtelselista när statusen är **Misslyckad**.

## Ta bort en IP-Tillåtelselista {#delete-allow-list}

En användare i rollen **Affärsägare** eller **Distributionshanterare** kan följa de här stegen för att visa och uppdatera ett IP-tillåtelselista.

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj rätt organisation och program.
1. Gå till skärmen **Miljö** från sidan **Översikt**.
1. Navigera till sidan **IP Tillåtelselista** från skärmen **Environment**.
1. Identifiera raden i IP-tillåtelselista som du vill ta bort.
1. Välj ellipsmenyn längst till höger på raden.
1. Klicka på **Ta bort**.
1. Bekräfta ditt bidrag.

Om du tar bort ett IP-tillåtelselista tas det automatiskt bort från alla tjänster och tas bort från tabellen.

## Befintliga CDN-konfigurationer {#pre-existing-cdn}

Om du har en befintlig CDN-konfiguration för dina IP-tillåtelselista finns det ett informationsmeddelande på sidan **IP Tillåtelselista**. Meddelandet uppmanar dig att lägga till dessa konfigurationer via användargränssnittet så att de är synliga och konfigurerbara i Cloud Manager.

Meddelandet försvinner när alla befintliga miljökonfigurationer migreras med användargränssnittet. Det kan ta 1-2 arbetsdagar innan meddelandet försvinner.

Mer information finns i [Lägga till en IP-Tillåtelselista](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md).

Ett liknande meddelande finns också på sidorna **SSL-certifikat** och **Miljö** för miljöer som har befintliga CDN-konfigurationer för SSL-certifikat eller anpassade domännamn.

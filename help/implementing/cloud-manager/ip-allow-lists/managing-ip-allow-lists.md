---
title: Hantera IP-Tillåtelselista
description: Lär dig hur du visar, redigerar, tar bort och kontrollerar status för IP-tillåtelselista i Cloud Manager.
exl-id: 6efabe53-3f45-47d4-ac1f-979cae0ab33e
source-git-commit: d67c5c9baafb9b7478f1d1c2ad924f5a8250a1ee
workflow-type: tm+mt
source-wordcount: '784'
ht-degree: 0%

---

# Hantera IP-Tillåtelselista {#manage-ip-allow-lists}

Lär dig hur du visar, redigerar, tar bort och kontrollerar status för IP-tillåtelselista i Cloud Manager.

## Visa och uppdatera IP-Tillåtelselista {#update-ip-allow-lists}

En användare i **Företagsägare** eller **Distributionshanteraren** kan följa de här stegen för att visa och uppdatera en IP-tillåtelselista.

1. Logga in i Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välja lämplig organisation och lämpligt program.
1. Navigera till **Miljö** från **Ökning** sida.
1. Navigera till **IP-Tillåtelselista** sidan från **Miljö** skärm.
1. Identifiera raden för de IP-tillåtelselista som du vill visa eller uppdatera.
1. Klicka på ellipsknappen till höger om raden.
1. Välj **Visa och uppdatera** alternativ.
1. The **Visa och uppdatera** visas namn, IP-adresser (eller intervall) som definierar regeln tillsammans med de miljöer och tjänster som regeln tillämpas på.
1. Ändra namn eller IP-adresser efter behov och bekräfta ditt bidrag.

Om du lägger till eller tar bort ett nytt IP-intervall i ett IP-tillåtelselista används/tas det automatiskt bort från alla motsvarande miljöer/tjänster som det tidigare tillämpades på.

Det går inte att uppdatera en IP-tillåtelselista medan en tidigare uppdatering pågår och inte har slutförts.

## Kontrollerar IP-Tillåtelselista status {#check-allow-list-status}

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välja lämplig organisation och lämpligt program.

1. Navigera till **Miljö** från **Ökning** sida.

1. Klicka på **Status** ikonen för IP-tillåtelselista från tabellen på **Miljö** och väljer **IP-Tillåtelselista** sida.

1. I Cloud Manager visas tillåtelselista status enligt beskrivningen [i följande avsnitt.](#status)

### Status för IP-Tillåtelselista {#status}

[Vid kontroll av status för IP-tillåtelselista](#check-allow-list-status) de kan ha något av följande värden.

* **Används** - IP-tillåtelselista har tillämpats på en eller flera miljöer.

* **Uppdaterar** - En uppdatering av IP-tillåtelselista pågår, vilket kan inkludera ett eller flera program eller att listan inte används.

   * Varje program/program som inte används visas tillsammans med dess egen status **Har inte startats**, **Pågår**, **Complete**, eller **Misslyckades**.

* **Misslyckades** - En eller flera program- eller avprogramprocesser för en uppdatering misslyckades.
   * Alla program och avaktiverade program visas tillsammans med programmets status.
      * Statusen är **Misslyckades** om ett program/ett program i uppdateringen misslyckas.
      * Statusen ändras inte **Misslyckades** tills alla fel har åtgärdats.
         * Välj **Försök igen** -ikonen bredvid statusen så att du kan ta bort felet.
      * Du kan inte uppdatera eller ta bort ett IP-tillåtelselista med en **Misslyckades** status.

* **Tar bort** - En borttagning av ett IP-tillåtelselista pågår.
   * Borttagning innebär att listan inte används för alla tjänster.
   * Varje program som inte används visas tillsammans med sin egen status på **Har inte startats**, **Pågår**, **Complete**, eller **Misslyckades**.
   * När borttagningen är klar:
      * IP-tillåtelselista visas inte i registret IP tillåtelselista.
      * IP-tillåtelselista används inte för någon tjänst i programmet i Cloud Manager.

* **Borttagningen misslyckades** - Ett eller flera icke-program misslyckades under en borttagningsåtgärd.

   * Varje program som inte används visas tillsammans med statusen **Complete** eller **Misslyckades**.
   * Statusen blir **Borttagningen misslyckades** om ett avaktiveringsfel inträffar.
   * Statusen ändras inte **Borttagningen misslyckades** tills alla fel har åtgärdats.
      * Välj **Ta bort** på ellipsmenyn längst till höger om raden i tabellen så att du kan ta bort eventuella fel.
   * Du kan inte uppdatera ett IP-tillåtelselista när statusen är **Misslyckades**.

## Ta bort en IP-Tillåtelselista {#delete-allow-list}

En användare i **Företagsägare** eller **Distributionshanteraren** kan följa de här stegen för att visa och uppdatera en IP-tillåtelselista.

1. Logga in i Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välja lämplig organisation och lämpligt program.
1. Navigera till **Miljö** från **Ökning** sida.
1. Navigera till **IP-Tillåtelselista** sidan från **Miljö** skärm.
1. Identifiera den rad i IP-tillåtelselista som du vill ta bort.
1. Välj ellipsmenyn längst till höger på raden.
1. Klicka **Ta bort**.
1. Bekräfta ditt bidrag.

Om du tar bort ett IP-tillåtelselista tas det automatiskt bort från alla tjänster och tas bort från tabellen.

## Befintliga CDN-konfigurationer {#pre-existing-cdn}

Om du har en befintlig CDN-konfiguration för dina IP-tillåtelselista visas ett informationsmeddelande på **IP TILLÅTELSELISTA** sida. Meddelandet uppmanar dig att lägga till dessa konfigurationer via användargränssnittet så att de är synliga och konfigurerbara i Cloud Manager.

Meddelandet försvinner när alla befintliga miljökonfigurationer migreras med användargränssnittet. Det kan ta 1-2 arbetsdagar innan meddelandet försvinner.

Se [Lägga till en IP-Tillåtelselista](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md) för mer information.

Ett liknande meddelande finns också på **SSL-certifikat** och **Miljö** sidor för miljöer som har befintliga CDN-konfigurationer för SSL-certifikat eller anpassade domännamn.

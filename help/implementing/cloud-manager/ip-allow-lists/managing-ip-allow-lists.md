---
title: Hantera IP-Tillåtelselista
description: Lär dig hur du visar, redigerar, tar bort och kontrollerar status för din IP-tillåtelselista i Cloud Manager.
source-git-commit: 878381f9c5780864f218a00a272b1600d578dcca
workflow-type: tm+mt
source-wordcount: '821'
ht-degree: 0%

---


# Hantera IP-Tillåtelselista {#manage-ip-allow-lists}

Lär dig hur du visar, redigerar, tar bort och kontrollerar status för din IP-tillåtelselista i Cloud Manager.

## Visa och uppdatera IP-Tillåtelselista {#update-ip-allow-lists}

En användare i **Företagsägare** eller **Distributionshanteraren** kan följa de här stegen för att visa och uppdatera ett IP-tillåtelselista.

1. Logga in i Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välja lämplig organisation och lämpligt program.
1. Navigera till **Miljö** från **Översikt** sida.
1. Navigera till **IP-Tillåtelselista** sidan från **Miljö** skärm.
1. Identifiera raden för IP-tillåtelselista som du vill visa eller uppdatera.
1. Klicka på ellipsknappen till höger om raden.
1. Välj **Visa och uppdatera** alternativ.
1. The **Visa och uppdatera** I guiden visas namn, IP-adresser (eller intervall) som definierar regeln tillsammans med de miljöer och tjänster som regeln tillämpas på.
1. Gör ändringar i namnet eller IP-adressen och bekräfta din inskickning.

Om du lägger till eller tar bort ett nytt IP-intervall i ett IP-tillåtelselista används/tas det automatiskt bort från alla motsvarande miljöer/tjänster som det tidigare tillämpades på.

Det går inte att uppdatera IP-tillåtelselista medan en tidigare uppdatering pågår och inte har slutförts.

## Kontrollerar IP-Tillåtelselista status {#check-allow-list-status}

Följ de här stegen för att kontrollera IP-tillåtelselista status.

1. Logga in i Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välja lämplig organisation och lämpligt program.

1. Navigera till **Miljö** från **Översikt** sida.

1. Klicka på **Status** ikonen för IP-tillåtelselista från tabellen på **Miljö** och väljer **IP-Tillåtelselista** sida.

1. Cloud Manager visar tillåtelselista status enligt beskrivningen [i följande avsnitt.](#status)

### Status för IP-Tillåtelselista {#status}

[Vid kontroll av IP-tillåtelselista status](#check-allow-list-status) de kan ha något av följande värden.

* **Används** - IP-tillåtelselista används i en eller flera miljöer.

* **Uppdaterar** - En uppdatering av IP tillåtelselista pågår, vilket kan inkludera ett eller flera program eller att listan inte används.

   * Varje program/program som inte används visas tillsammans med dess egen status **Har inte startats**, **Pågår**, **Slutförd**, eller **Misslyckades**.

* **Misslyckades** - En eller flera program- eller avprogramprocesser för en uppdatering misslyckades.
   * Alla program och icke-program visas tillsammans med status.
      * Statusen är **Misslyckades** om ett program/ett program i uppdateringen misslyckas.
      * Statusen ändras inte **Misslyckades** tills alla fel har åtgärdats.
         * Du måste välja **Försök igen** -ikonen bredvid statusen för att rensa felet.
      * Du kan inte uppdatera eller ta bort en IP-tillåtelselista med en **Misslyckades** status.

* **Tar bort** - En borttagning av IP-tillåtelselista pågår.
   * Borttagning innebär att listan inte används för alla tjänster.
   * Alla program som inte används visas tillsammans med programmets egen status: **Har inte startats**, **Pågår**, **Slutförd**, eller **Misslyckades**.
   * När borttagningen är klar kommer IP tillåtelselista att:
      * Visas inte längre i IP tillåtelselista-tabellen.
      * Tillämpas inte längre på någon tjänst i programmet i Cloud Manager.

* **Borttagningen misslyckades** - Ett eller flera icke-program misslyckades under en borttagningsåtgärd.

   * Alla program som inte används visas tillsammans med status **Slutförd** eller **Misslyckades**.
   * Statusen blir **Borttagningen misslyckades** om ett icke-program misslyckas.
   * Statusen ändras inte **Borttagningen misslyckades** tills alla fel har åtgärdats.
      * Du måste välja **Ta bort** på ellipsmenyn längst till höger om raden i tabellen för att ta bort eventuella fel.
   * Du kan inte uppdatera ett IP-tillåtelselista när statusen är **Misslyckades**.

## Ta bort en IP-Tillåtelselista {#delete-allow-list}

En användare i **Företagsägare** eller **Distributionshanteraren** kan följa de här stegen för att visa och uppdatera ett IP-tillåtelselista.

1. Logga in i Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välja lämplig organisation och lämpligt program.
1. Navigera till **Miljö** från **Översikt** sida.
1. Navigera till **IP-Tillåtelselista** sidan från **Miljö** skärm.
1. Identifiera den rad i IP-tillåtelselista som du vill ta bort.
1. Välj ellipsmenyn längst till höger på raden.
1. Klicka **Ta bort**.
1. Bekräfta ditt tävlingsbidrag.

Om du tar bort ett IP-tillåtelselista tas det automatiskt bort från alla tjänster och tas bort från tabellen.

## Befintliga CDN-konfigurationer {#pre-existing-cdn}

Om du har en befintlig CDN-konfiguration för IP-tillåtelselista visas ett informationsmeddelande på **IP Tillåtelselista** som uppmanar dig att lägga till dessa konfigurationer via användargränssnittet så att de är synliga och konfigurerbara i Cloud Manager.

Meddelandet försvinner när alla befintliga miljökonfigurationer migreras med användargränssnittet. Det kan ta 1-2 arbetsdagar innan meddelandet försvinner.

Se dokumentet [Lägga till en IP-tillåtelselista](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md) för mer information.

Ett liknande meddelande finns också på **SSL-certifikat** och **Miljö** sidor för miljöer som har befintliga CDN-konfigurationer för SSL-certifikat eller anpassade domännamn.

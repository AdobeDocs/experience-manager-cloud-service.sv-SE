---
title: Hantera IP-Tillåtelselista
description: Lär dig hur du visar, redigerar, tar bort och kontrollerar status för IP-Tillåtelselista i Cloud Manager.
exl-id: 6efabe53-3f45-47d4-ac1f-979cae0ab33e
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '841'
ht-degree: 0%

---

# Hantera IP-Tillåtelselista {#manage-ip-allow-lists}

Lär dig hur du visar, redigerar, tar bort och kontrollerar status för IP-Tillåtelselista i Cloud Manager.

## Visa och uppdatera IP-Tillåtelselista {#update-ip-allow-lists}

En användare i rollen **Affärsägare** eller **Distributionshanterare** kan följa de här stegen för att visa och uppdatera ett IP-Tillåtelselista.

**Så här visar och uppdaterar du IP-Tillåtelselista:**

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj rätt organisation och program.
1. På sidan **Översikt**, på den vänstra menyn, under **Tjänster**, klickar du på ikonen ![Åtgärdslista](https://spectrum.adobe.com/static/icons/workflow_18/Smock_TaskList_18_N.svg) **IP-Tillåtelselista**.
1. Identifiera raden för IP-Tillåtelselista som du vill visa eller uppdatera.
1. Klicka på ikonen ![Mer](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) till höger om raden.
1. Klicka på **Visa och uppdatera** i listrutan.
I dialogrutan **Visa och uppdatera IP Tillåtelselista** visas namnet, IP-adresserna (eller intervallen) som definierar regeln samt de miljöer och tjänster som regeln används i.
1. Ändra namn eller IP-adresser efter behov.

   Om du lägger till eller tar bort ett nytt IP-intervall i ett IP-Tillåtelselista används/tas det automatiskt bort från alla motsvarande miljöer/tjänster som det tidigare tillämpades på.

   Det går inte att göra uppdateringar till IP-Tillåtelselista när en tidigare uppdatering pågår och inte har slutförts.

1. Klicka på **Uppdatera**.

## Kontrollera IP-Tillåtelselista status {#check-allow-list-status}

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj rätt organisation och program.

1. På sidan **Översikt**, på den vänstra menyn, under **Tjänster**, klickar du på ikonen ![Åtgärdslista](https://spectrum.adobe.com/static/icons/workflow_18/Smock_TaskList_18_N.svg) **IP-Tillåtelselista**.

1. I kolumnen **Status** i IP Tillåtelselista-tabellen håller du muspekaren över ett IP-Tillåtelselista som är grönt (används) för att se en eller flera tjänster som används.

   Statusvärdena i tabellen har följande betydelse:

   | Status för IP Tillåtelselista | Beskrivning |
   | --- | --- |
   | Används | IP-Tillåtelselista används i en eller flera miljöer. |
   | Uppdaterar | En uppdatering av IP Tillåtelselista pågår, vilket kan inkludera ett eller flera program eller att listan inte används. Varje program/program som inte körs visas tillsammans med dess egen status **Inte startat**, **Pågår**, **Fullständigt** eller **Misslyckades**. |
   | Misslyckades | En eller flera program- eller avprogramprocesser för en uppdatering misslyckades.<br> ・ Alla program och avprogram visas tillsammans med programmets status.<br> ・ Statusen är **Misslyckad** om ett program/ett program som inte används i uppdateringen misslyckas. Statusen förblir **Misslyckad** tills alla fel har rensats.<br> ・ Klicka på ikonen **Försök igen** bredvid statusen så att du kan ta bort felet.<br> ・ Du kan inte uppdatera eller ta bort en IP-Tillåtelselista med statusen **Misslyckades**. |
   | Tar bort | En borttagning av IP-Tillåtelselista pågår.<br> ・ Att ta bort innebär att listan tas bort från alla tjänster.<br> ・ Varje program som inte används visas tillsammans med dess egen status **Inte startat**, **Pågår**, **Fullständigt** eller **Misslyckades**.<br> ・ När borttagningsåtgärden har slutförts visas IP-Tillåtelselista inte i IP Tillåtelselista-tabellen. IP Tillåtelselista används inte heller för någon tjänst i Cloud Manager. |
   | Borttagningen misslyckades | Ett eller flera icke-program misslyckades under en borttagningsåtgärd.<br> ・ Varje program som inte används visas tillsammans med statusen **Fullständigt** eller **Misslyckat**.<br> ・ Statusen blir **Ta bort misslyckades** om ett av programmen misslyckas. Statusen förblir **Ta bort misslyckades** tills alla fel har rensats. Klicka på ikonen ![Mer](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) längst till höger i tabellraden och klicka sedan på **Ta bort** i listrutan för att ta bort eventuella fel.<br> ・ Du kan inte uppdatera ett IP-Tillåtelselista när statusen är **Misslyckad**. |

## Ta bort en IP-Tillåtelselista {#delete-allow-list}

När du tar bort ett IP-Tillåtelselista tas listan automatiskt bort från alla tjänster och tas bort från IP Tillåtelselista-tabellen.

En användare i rollen **Affärsägare** eller **Distributionshanterare** kan följa de här stegen för att visa och uppdatera ett IP-Tillåtelselista.

**Så här tar du bort en IP-Tillåtelselista:**

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj rätt organisation och program.
1. På sidan **Översikt**, på den vänstra menyn, under **Tjänster**, klickar du på ikonen ![Åtgärdslista](https://spectrum.adobe.com/static/icons/workflow_18/Smock_TaskList_18_N.svg) **IP-Tillåtelselista**.
1. Identifiera raden för IP-Tillåtelselista som du vill ta bort, klicka på ikonen ![Mer](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) till höger om raden och klicka sedan på **Ta bort**.
1. Klicka på **Ta bort** i dialogrutan **Ta bort IP Tillåtelselista**.

## Redan befintliga CDN-konfigurationer {#pre-existing-cdn}

Om du har en befintlig CDN-konfiguration (Content Delivery Network) för IP-Tillåtelselista visas ett informativt meddelande på **IP Tillåtelselista** -sidan. Meddelandet uppmanar dig att lägga till dessa konfigurationer via användargränssnittet så att de är synliga och konfigurerbara i Cloud Manager.

Meddelandet försvinner när alla befintliga miljökonfigurationer migreras med användargränssnittet. Det kan ta 1-2 arbetsdagar innan meddelandet försvinner.

Mer information finns i [Lägg till en IP-Tillåtelselista](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md).

Ett liknande meddelande finns också på sidorna **SSL-certifikat** och **Miljö** för miljöer som har befintliga CDN-konfigurationer för SSL-certifikat eller anpassade domännamn.

---
title: Kontrollerar IP Tillåtelselista-status
description: Kontrollerar IP Tillåtelselista-status
translation-type: tm+mt
source-git-commit: e6a8d69ea87ac56a51cde2f131c4accff1bea527
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---


# Kontrollerar IP Tillåtelselista-status {#check-allow-list-status}

Följ stegen nedan för att fastställa status för uppdateringar av IP-Tillåtelselista:

1. Klicka på statusikonen för IP-Tillåtelselista i tabellen på **skärmen** och välj **IP-Tillåtelselista**.

1. I Cloud Manager visas en av följande statusar, vilket nämns i avsnittet nedan.

## Status för en IP-Tillåtelselista {#status}

Nedan följer definitioner av status som visas i ett IP-Tillåtelselista:

* **Används**: IP Tillåtelselista används i miljöer.  Miljöerna och tjänsterna visas på bilden nedan.

* **Uppdaterar**: En uppdatering av IP Tillåtelselista som kan innehålla en eller flera tillämpliga eller ej tillämpliga håller på att göras. Alla Tillämpa och Avanvänd visas tillsammans med Ej påbörjat/Pågående/Slutfört eller Misslyckat.

* **Misslyckades**: En eller flera tillämpnings- eller avanvändningsprocesser i en uppdatering misslyckades. Alla Tillämpa och Ångra visas tillsammans med Fullständigt eller Misslyckat.
   * Statusen är Misslyckad, även om en tillämpning/avtillämpning i uppdateringen misslyckas.
   * Statusen kommer att förbli Misslyckad tills alla fel har rensats. Användaren måste markera ikonen för nytt försök bredvid statusen för att åtgärda felet.
   * Användaren kan inte uppdatera eller ta bort IP Tillåtelselista när statusen är Misslyckad.

* **Tar bort**: Borttagningsbegäran pågår. Detta innebär att alla tjänster inte används. Alla Unapply visas tillsammans med Not Started/In Progress/Complete eller Failed.
När borttagningen är klar kommer IP Tillåtelselista att:
   * Visas inte längre i IP Tillåtelselista-tabellen.
   * Tillämpas inte längre på någon tjänst i programmet i Cloud Manager.

* **Borttagningen misslyckades**: En eller flera processer som inte används i en borttagningsåtgärd misslyckades. Alla Unapply visas tillsammans med Complete eller Failed.

   * Statusen är Ta bort misslyckades, även om ett av dem misslyckas.
   * Statusen för Ta bort misslyckades tills alla fel har rensats. Användaren måste välja Ta bort från **..**-menyn längst till höger om raden i tabellen för att ta bort eventuella fel.
   * Användaren kan inte uppdatera IP Tillåtelselista medan statusen misslyckades.


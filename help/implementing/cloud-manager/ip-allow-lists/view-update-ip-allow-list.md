---
title: Visa och uppdatera - IP Tillåtelselista i Could Manager
description: Visa och uppdatera - IP Tillåtelselista i Could Manager
translation-type: tm+mt
source-git-commit: 4635cb6360707d12cf512b0ee21f05169a153114
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---


# Visa och uppdatera IP-Tillåtelselista {#view-update}

Du kan visa och uppdatera IP-Tillåtelselista i följande scenarier:

* Om du vill visa och uppdatera-menyn behöver du bara visa information om en eller flera IP-Tillåtelselista.
* Så här redigerar du ett eller flera av följande:
   * IP-intervall i definitionen av regelnamnet
   * Eget namn på IP Tillåtelselista-regeln

## Uppdatera IP-Tillåtelselista {#update-ip-allow-lists}


En användare i rollen Business Owner eller Deployment Manager måste vara inloggad för att det ska gå att uppdatera ett IP-Tillåtelselista.

>[!NOTE]
>Guiden Visa och uppdatera visar namn, IP-intervall eller IP-intervall som definierar regeln. Dessutom visas de miljöer och tjänster som regeln tillämpas på.

Följ stegen nedan för att uppdatera ett IP-Tillåtelselista:

1. Navigera till sidan **IP Tillåtelselista** från skärmen **Environment**.
1. Identifiera raden där IP Tillåtelselista-regeln som du vill visa/uppdatera finns.
1. Välj **..**-menyn längst till höger på raden.
1. Välj alternativet **Visa och uppdatera**.
1. Gör ändringar i namnet eller IP-adresserna och bekräfta ditt bidrag.

## Viktigt att tänka på när du lägger till, uppdaterar eller tar bort IP-Tillåtelselista {#considerations}

* Om du lägger till ett nytt IP-intervall till IP-Tillåtelselista används det automatiskt för alla motsvarande miljötjänster.
* Om du tar bort ett IP-intervall från IP Tillåtelselista tas det automatiskt bort från alla motsvarande miljötjänster.
* Det går inte att göra uppdateringar till IP-Tillåtelselista när en tidigare uppdatering pågår och inte har slutförts.
* Det går inte att uppdatera ett IP-Tillåtelselista om det finns fel från en tidigare uppdatering. Alla fel måste rensas genom att du försöker uppdatera igen.
Mer information finns i [Kontrollera IP Tillåtelselista-status](/help/implementing/cloud-manager/ip-allow-lists/check-ip-allow-list-status.md).
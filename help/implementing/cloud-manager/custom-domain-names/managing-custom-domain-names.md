---
title: Hantera anpassade domännamn
description: Lär dig hur du använder Cloud Manager för att visa, uppdatera, ersätta och ta bort anpassade domännamn.
exl-id: 6cab8cf2-22c0-4f4b-9c54-a1425e74ddd0
source-git-commit: c8599d4a0c3093bf3cff630745ada95e64124fef
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 0%

---

# Hantera anpassade domännamn {#managing-custom-domain-names}

Med Cloud Manager kan du visa, uppdatera, ersätta och ta bort anpassade domännamn.

## Visa och uppdatera {#view-and-update}

Använd **Visa och uppdatera** om du vill visa information om dina anpassade domännamn.

1. Logga in i Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välja lämplig organisation och lämpligt program.

1. Navigera till **Miljö** från **Översikt** sida.

1. Identifiera raden i det anpassade domännamnet som du vill visa eller uppdatera.

1. Klicka på ellipsknappen längst till höger på raden.

1. Välj **Visa och uppdatera** alternativ.

## Uppdaterar det anpassade domännamnets SSL-certifikat {#update-cert}

Du kan följa [samma steg för att visa och uppdatera ett anpassat domännamn](#view-and-update) för att uppdatera ett anpassat domännamns SSL-certifikat.

>[!NOTE]
>
>SSL-certifikatet måste vara giltigt, [redan konfigurerad,](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md) och innehåller det anpassade domännamn som du uppdaterar.

## Ta bort ett anpassat domännamn {#deleting}

En användare med **Företagsägare** eller **Distributionshanteraren** kan använda Cloud Manager för att ta bort ett anpassat domännamn.

### Ta bort ett anpassat domännamn från alla associerade miljöer {#delete-cdn-all}

1. Logga in i Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välja lämplig organisation och lämpligt program.

1. Navigera till **Miljö** från **Översikt** sida.

1. Navigera till **Domäninställningar** sidan från **Miljö** skärm.

1. Identifiera raden för det anpassade domännamn som du vill ta bort.

1. Klicka på ellipsknappen längst till höger på raden.

1. Välj **Ta bort**.

   ![Tar bort anpassade domännamn](/help/implementing/cloud-manager/assets/cdn/cdn-delete.png)

1. Bekräfta ditt tävlingsbidrag.

### Ta bort ett anpassat domännamn från en viss miljö {#delete-cdn-specific}

1. Logga in i Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välja lämplig organisation och lämpligt program.
1. Navigera till **Miljö** från **Översikt** sida.
1. Från **Miljö** navigera till informationsskärmen för den aktuella miljön.
1. Identifiera raden med det anpassade domännamnet som du vill ta bort i tabellen över domännamn.
1. Klicka på ellipsknappen längst till höger på raden.
1. Välj **Ta bort**.
1. Bekräfta ditt tävlingsbidrag.

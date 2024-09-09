---
title: Hantera anpassade domännamn
description: Lär dig hur du använder Cloud Manager för att visa, uppdatera, ersätta och ta bort anpassade domännamn.
exl-id: 6cab8cf2-22c0-4f4b-9c54-a1425e74ddd0
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 4e887b753eaf09e104c68484792f00dcb08ee304
workflow-type: tm+mt
source-wordcount: '342'
ht-degree: 0%

---


# Hantera anpassade domännamn {#managing-custom-domain-names}

Med Cloud Manager kan du visa, uppdatera, ersätta och ta bort anpassade domännamn.

## Visa och uppdatera ett anpassat domännamn {#view-and-update}

Använd menyn **Visa och uppdatera** om du vill visa information om dina anpassade domännamn.

**Så här visar och uppdaterar du ett anpassat domännamn:**

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj lämplig organisation.

1. Välj programmet på konsolen **[Mina program](/help/implementing/cloud-manager/navigation.md#my-programs)**.

1. Gå till skärmen **Miljö** från sidan **Översikt**.

1. Identifiera raden i det anpassade domännamnet som du vill visa eller uppdatera.

1. Klicka på ellipsknappen längst till höger på raden.

1. Välj alternativet **Visa och uppdatera**.

## Uppdatera ett anpassat domännamns SSL-certifikat {#update-cert}

Du kan följa [samma steg för att visa och uppdatera ett anpassat domännamn](#view-and-update) för att uppdatera ett anpassat domännamns SSL-certifikat.

>[!NOTE]
>
>SSL-certifikatet måste vara giltigt, [redan konfigurerat](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md), och innehålla det anpassade domännamn som du uppdaterar.

## Ta bort ett anpassat domännamn {#deleting}

En användare med rollen **Business Owner** eller **Deployment Manager** kan använda Cloud Manager för att ta bort ett anpassat domännamn.

### Ta bort ett anpassat domännamn från alla associerade miljöer {#delete-cdn-all}

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj rätt organisation och program.

1. Gå till sidan **Domäninställningar** från skärmen **Översikt**.

1. Identifiera raden med det anpassade domännamn som du vill ta bort.

1. Klicka på ellipsknappen längst till höger på raden.

1. Välj **Ta bort**.

1. Bekräfta ditt bidrag.

### Ta bort ett anpassat domännamn från en viss miljö {#delete-cdn-specific}

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj rätt organisation och program.
1. Gå till skärmen **Miljö** från sidan **Översikt**.
1. Navigera från sidan **Miljö** till en informationsskärm om den miljö som är av intresse.
1. Identifiera raden med det anpassade domännamnet som du vill ta bort i tabellen över domännamn.
1. Klicka på ellipsknappen längst till höger på raden.
1. Välj **Ta bort**.
1. Bekräfta ditt bidrag.

---
title: Redigeringsprogram
description: Lär dig hur du redigerar produktions- och sandlådeprogram för att justera deras alternativ efter att du har skapat dem.
exl-id: 819e4a6e-f77a-4594-a402-a300dcbdf510
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 0%

---


# Redigeringsprogram {#editing-programs}

Om du vill hantera och redigera program börjar du på konsolen [**Mina program**.](/help/implementing/cloud-manager/navigation.md) Sidan **Mina program** innehåller en översikt över alla program som du har tillgång till. När du väljer ett enskilt program visas en översikt över programmet på sidan **Programöversikt**.

I **programöversikten** kan användare med nödvändig behörighet redigera [produktionsprogram som skapats i din organisation](creating-production-programs.md) och [ sandlådeprogram som skapats i din organisation.](creating-sandbox-programs.md) Genom att redigera ett program kan du:

* Lägg till Sites-lösning i ett befintligt program med Assets och omvänt.
* Ta bort Sites eller Assets från ett befintligt program med både Sites och Assets.
* Lägg till ett andra, oanvänt lösningsberättigande, antingen till ett befintligt program eller som ett nytt program.
* Ta bort sandlådeprogram.

## Behörigheter {#permissions}

Du måste vara medlem i rollen **Affärsägare** för att kunna redigera program eller ta bort sandlådeprogram samt för att få tillgång till licensinstrumentpanelen.

## Redigera ett program {#editing}

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj lämplig organisation.

1. På sidan **[Mina program](#my-programs)** klickar du på det program du vill redigera för att visa information om det.

1. Klicka på programnamnet i det övre vänstra hörnet på sidan och välj **Redigera program**.

   ![Redigera programalternativ](assets/edit-program-overview.png)

1. Sidan **Redigera program** öppnas på fliken **Allmänt** .

   ![Fliken Allmänt](assets/edit-program-prod1.png)

1. De alternativ som är tillgängliga för redigering av programmet är desamma som när du skapar programmet.
   * Mer information om de enskilda alternativen finns i dokumenten [Skapa produktionsprogram](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md) och [Skapa sandlådeprogram](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md) .
   * [Ytterligare alternativ](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#options) kan vara tillgängliga för ditt produktionsprogram beroende på organisationens rättigheter.

1. Klicka på **Uppdatera** om du vill spara ändringarna i programmet.

Ändringarna sparas.

>[!NOTE]
>
>Varje gång ett program redigeras, som att lägga till eller ta bort en lösning eller ett tillägg, börjar ändringarna gälla efter nästa distribution.

## Tar bort sandlådeprogram {#delete-sandbox-program}

Om du tar bort ett sandlådeprogram tas alla miljöer och rörledningar som är kopplade till det bort.

>[!TIP]
>
>Användare med rollerna **Business Owner** eller **Deployment Manager** kan ta bort produktions- och scenmiljöer i stället för hela sandlådeprogrammet.

Så här tar du bort ett sandlådeprogram.

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj lämplig organisation.

1. På sidan **[Mina program](#my-programs)** klickar du på det program du vill redigera för att visa information om det.

1. Klicka på programnamnet längst upp till vänster på sidan och välj **Ta bort program**.

   ![Ta bort programalternativ](assets/delete-sandbox1.png)

Du kan också klicka på ellipsknappen på programkortet på Cloud Manager översiktssida och välja **Ta bort program**.

![Ta bort sandlådan från programkortet](assets/delete-sandbox2.png)

>[!NOTE]
>
>Endast sandlådeprogram kan tas bort. Det går inte att ta bort produktionsprogram.

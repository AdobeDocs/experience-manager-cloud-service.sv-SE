---
title: Redigeringsprogram
description: Lär dig hur du redigerar produktions- och sandlådeprogram för att justera deras alternativ efter att du har skapat dem.
exl-id: 819e4a6e-f77a-4594-a402-a300dcbdf510
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '389'
ht-degree: 0%

---

# Redigeringsprogram {#editing-programs}

Användare med nödvändig behörighet kan redigera [produktionsprogram som har skapats i din organisation](creating-production-programs.md) och [sandlådeprogram som har skapats i din organisation.](creating-sandbox-programs.md) Genom att redigera ett program kan du

* Lägg till Sites-lösning i ett befintligt program med Assets och vice versa.
* Ta bort platser eller resurser från ett befintligt program med både platser och resurser.
* Lägg till ett andra, oanvänt lösningsberättigande till antingen ett befintligt program eller som ett nytt program.
* Ta bort sandlådeprogram.

>[!NOTE]
>
>Du måste vara medlem i **Företagsägare** roll för att redigera program eller ta bort sandlådeprogram.

Följ de här stegen för att redigera ett program.

1. Logga in i Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välja lämplig organisation.

1. Klicka på det program du vill redigera för att visa information om det.

1. Klicka på programnamnet längst upp till vänster på sidan och välj **Redigera program**.

   ![Redigera programalternativ](assets/edit-program-overview.png)

1. The **Redigera program** sidan visar två flikar: **Allmänt** och **Lösningar och tillägg**. Välj **Allmänt** för att redigera programnamnet och beskrivningen.

   * Minst en lösning måste väljas för ett program.

   ![Fliken Allmänt](assets/edit-program-prod1.png)

1. Välj **Lösningar och tillägg** för att ändra lösningarna för programmet.

   ![Välj lösningar](assets/edit-prg.png)

1. Klicka på avrivningen före lösningsnamnen för att visa valfria tillägg, som att välja **Handel** tilläggsalternativ under **Webbplatser**.

   ![Redigera tillägg](assets/edit-program-add-on.png)

1. Klicka på **Uppdatera** för att spara ändringarna i programmet.

När uppdateringarna är klara träder ändringarna i kraft efter nästa driftsättning om de valda lösningarna har ändrats.

## Tar bort sandlådeprogram {#delete-sandbox-program}

Om du tar bort ett sandlådeprogram tas alla miljöer och rörledningar som är kopplade till det bort.

>[!TIP]
>
>Användare med **Företagsägare** eller **Distributionshanteraren** roller kan också ta bort sin produktions- och scenmiljö i stället för hela sandlådeprogrammet.

Följ de här stegen för att ta bort ett sandlådeprogram.

1. Logga in i Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välja lämplig organisation.

1. Klicka på det program du vill redigera för att visa information om det.

1. Klicka på programnamnet längst upp till vänster på sidan och välj **Ta bort program**.

   ![Ta bort programalternativ](assets/delete-sandbox1.png)

Du kan också klicka på ellipsknappen på programmets kort på översiktssidan för Cloud Manager och välja **Ta bort program**.

![Ta bort sandlåda från programkort](assets/delete-sandbox2.png)

>[!NOTE]
>
>Endast sandlådeprogram kan tas bort. Det går inte att ta bort produktionsprogram.

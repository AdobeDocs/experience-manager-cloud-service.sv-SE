---
title: 'Redigera ett produktionsprogram '
description: Redigera ett produktionsprogram
exl-id: 745c10af-f0a0-49e9-bb79-3fd058fad16c
source-git-commit: 8974217f8a3db6cfe96082fe2ed0277c243fa7e1
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 0%

---

# Redigera ett produktionsprogram {#create-production-program}

Användare med nödvändig behörighet kan nu redigera ett produktionsprogram och göra följande på ett självbetjäningssätt:

* Lägg till Sites-lösning i ett befintligt program med Assets (eller vice versa).
* Ta bort platser (eller resurser) från ett befintligt program med både platser och resurser.
* Lägg till andra, outnyttjade lösningsberättigande antingen till ett befintligt program eller som ett nytt program.

   >[!NOTE]
   >En användare i rollen Business Owner måste vara inloggad för att programmet ska kunna redigeras.

Följ stegen nedan för att redigera ett produktionsprogram:

1. Klicka på alternativet **Redigera program** på sidan *Översikt* i Cloud Manager

   ![](assets/edit-program-overview.png)

1. På sidan **Redigera program** visas två flikar **Allmänt** och **Lösningar och tillägg**.

   Navigera till fliken **Allmänt** för att redigera programbeskrivningen.

   ![](assets/edit-program-prod1.png)

   På fliken **Lösningar och tillägg** visas två alternativ, till exempel **Platser** och **Resurser** för både produktions- och sandlådeprogram. Du kan också välja alternativet **Commerce**, som är tillgängligt under **Platser**, vilket visas i bilden nedan.

   ![](assets/edit-prg.png)

   >[!NOTE]
   >Minst en lösning måste väljas för ett program, det vill säga användaren får inte avmarkera alla lösningar under redigeringsprogrammets arbetsflöde.

1. Klicka på **Uppdatera** för att slutföra redigeringsprogrammet.


## Att tänka på när du redigerar ett program {#considerations-editing}

Tänk på följande när du redigerar ett program:

* Minst en lösning måste väljas för ett program, det vill säga användaren får inte avmarkera alla lösningar under redigeringsprogrammets arbetsflöde.

* Om du klickar på knappen **Spara** och de valda lösningarna har ändrats kommer lösningsuppdateringar i miljöer att börja gälla efter nästa distribution.

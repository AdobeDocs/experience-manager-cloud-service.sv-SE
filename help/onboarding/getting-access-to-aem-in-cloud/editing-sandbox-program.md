---
title: 'Redigera ett sandlådeprogram '
description: Redigera ett sandlådeprogram
exl-id: e4545f7e-5329-40ad-81bb-a383c68f5d66
translation-type: tm+mt
source-git-commit: 26cbd2369762050eb2e85d714b8f6b0ff129f171
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 0%

---

# Redigera ett sandlådeprogram {#create-sandbox-program}

Användare med nödvändig behörighet kan nu redigera ett produktionsprogram och göra följande på ett självbetjäningssätt:

* Lägg till Sites-lösning i ett befintligt program med Assets (eller vice versa).
* Ta bort platser (eller resurser) från ett befintligt program med både platser och resurser.
* Lägg till andra, outnyttjade lösningsberättigande antingen till ett befintligt program eller som ett nytt program.

   >[!NOTE]
   >En användare i rollen Business Owner måste vara inloggad för att programmet ska kunna redigeras.

Följ stegen nedan för att redigera ett sandlådeprogram:

1. Klicka på alternativet **Redigera program** på sidan *Översikt* i Cloud Manager

   ![](assets/edit-program-overview.png)

1. På sidan **Redigera program** visas två flikar **Allmänt** och **Lösningar och tillägg**.

   Navigera till fliken **Allmänt** för att redigera programbeskrivningen.

   ![](assets/edit-program-general.png)

   På fliken **Lösningar och tillägg** visas två alternativ, till exempel **Platser** och **Resurser** för både produktions- och sandlådeprogram. Dessutom kan du välja alternativet **Commerce**, som är tillgängligt under **Platser**, vilket visas i bilden nedan.

   ![](assets/edit-prg.png)

   >[!NOTE]
   >Minst en lösning måste väljas för ett program, vilket innebär att användaren inte får avmarkera alla lösningar under redigeringsprogrammets arbetsflöde.

1. Klicka på **Spara** för att slutföra redigeringsprogramprocessen.


## Att tänka på när du redigerar ett program {#considerations-editing}

Tänk på följande när du redigerar ett program:

* Minst en lösning måste väljas för ett program, vilket innebär att det inte går att avmarkera alla lösningar under redigeringsprogrammets arbetsflöde.

* Om du klickar på knappen **Spara** och de valda lösningarna har ändrats kommer lösningsuppdateringar i miljöer att börja gälla efter nästa distribution.

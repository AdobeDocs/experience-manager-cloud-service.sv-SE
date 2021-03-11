---
title: 'Redigera ett produktionsprogram '
description: 'Redigera ett produktionsprogram '
translation-type: tm+mt
source-git-commit: 751f611ecccc39ef4650a1c7a9941655a6b2aedd
workflow-type: tm+mt
source-wordcount: '228'
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

1. 
   1. Gå till sidan **Redigera program** i Cloud Managers *Översikt*

1. Sidan **Redigera program** visar två flikar (Allmänt och Lösningar) för både Production- och Sandbox-program.

   ![](assets/edit-program.png)

   >[!NOTE]
   >Även om både Sites och Assets visas kan en av dem inaktiveras baserat på vad som har köpts och inte använts. I synnerhet om organisationen inte har oanvända tillstånd för en viss lösning, kommer den lösningen att visas men inaktiveras.

## Att tänka på när du redigerar ett program {#considerations-editing}

Tänk på följande när du redigerar ett program:

* Minst en lösning måste väljas för ett program, vilket innebär att det inte går att avmarkera alla lösningar under redigeringsprogrammets arbetsflöde.

* Om du klickar på knappen **Spara** och de valda lösningarna har ändrats kommer lösningsuppdateringar i miljöer att börja gälla efter nästa distribution.
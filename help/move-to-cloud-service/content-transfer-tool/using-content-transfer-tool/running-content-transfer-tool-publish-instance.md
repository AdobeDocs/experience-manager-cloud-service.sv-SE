---
title: Köra verktyget Innehållsöverföring på en publiceringsinstans
description: Köra verktyget Innehållsöverföring på en publiceringsinstans
source-git-commit: 27e68cd282414da4cc23c3ba276b0fb3c330d49c
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 0%

---


# Köra verktyget Innehållsöverföring på en publiceringsinstans {#run-content-transfer-tool-publish-instance}

## Introduktion {#introduction}

Innehållsöverföringsverktyget (CTT) utför ingen typ av innehållsanalys innan innehåll överförs från källinstansen till målinstansen. CTT skiljer till exempel inte mellan publicerat och opublicerat innehåll när innehåll hämtas till en publiceringsmiljö. Det innehåll som anges i migreringsuppsättningen hämtas till den valda målinstansen. Användaren kan importera en migreringsuppsättning till en Author-instans eller en Publish-instans eller både och. Vi rekommenderar att CTT installeras på källinstansen Author för att flytta innehåll till målinstansen Author när du flyttar innehåll till en Production-instans och att CTT på källinstansen av Publish installeras för att flytta innehåll till målpubliceringsinstansen.

>[!NOTE]
>Vi rekommenderar att verktyget Innehållsöverföring installeras på publiceringskällan när du flyttar innehåll till en publiceringsinstans, så att innehållet flyttas till publiceringsinstansen. Mer information finns i avsnittet [Rekommenderad strategi](#recommended-approach) nedan.

## Rekommenderat tillvägagångssätt {#recommended-approach}

Följ de rekommenderade tillvägagångssätten som beskrivs nedan:

* Använd samma version av CTT som användes på Author-instansen.

* Endast en publiceringsnod behöver migreras. Den bör avlägsnas från belastningsutjämnaren innan extraheringen påbörjas.

* När du skapar en migreringsuppsättning använder du URL:en till författarens AEMaaCS-miljö.

* Under publiceringsprocessen kommer publiceringsnivån INTE att förminskas (till skillnad från författaren). Som en försiktighetsåtgärd bör du undvika att användare startar skrivåtgärder som:

   * Innehållsdistribution från AEM as a Cloud Service Author till Publish i den miljön
   * Användarsynkronisering mellan publiceringsinstanser

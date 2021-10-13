---
title: Köra verktyget Innehållsöverföring på en publiceringsinstans
description: Köra verktyget Innehållsöverföring på en publiceringsinstans
source-git-commit: 5ae76fbc3926f5e2cd7ed5597a9d4521adc9ddb1
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 0%

---


# Köra verktyget Innehållsöverföring på en publiceringsinstans {#run-content-transfer-tool-publish-instance}

## Introduktion {#introduction}

Innehållsöverföringsverktyget (CTT) utför ingen typ av innehållsanalys innan innehåll överförs från källinstansen till målinstansen. CTT skiljer till exempel inte mellan publicerat och opublicerat innehåll när innehåll hämtas till en publiceringsmiljö. Det innehåll som anges i migreringsuppsättningen hämtas till den valda målinstansen. Användaren kan importera en migreringsuppsättning till en Author-instans eller en Publish-instans eller både och.

>[!NOTE]
>Vi rekommenderar att du installerar Content Transfer Tool på källinstansen Author när du flyttar innehåll till målinstansen Author, och på samma sätt installerar Content Transfer Tool på källinstansen Publish för att flytta innehåll till målinstansen Publish. Mer information finns i avsnittet [Rekommenderad strategi](#recommended-approach) nedan.

## Rekommenderat tillvägagångssätt {#recommended-approach}

Följ de rekommenderade tillvägagångssätten som beskrivs nedan:

* Använd samma version av CTT som användes på Author-instansen.

* Endast en publiceringsnod behöver migreras. Den bör avlägsnas från belastningsutjämnaren innan extraheringen påbörjas.

* När du skapar en migreringsuppsättning använder du URL:en till författarens AEMaaCS-miljö.

* Under publiceringsprocessen kommer publiceringsnivån INTE att förminskas (till skillnad från författaren). Som en försiktighetsåtgärd bör du undvika att användare startar skrivåtgärder som:

   * Innehållsdistribution från AEM as a Cloud Service Author till Publish i den miljön
   * Användarsynkronisering mellan publiceringsinstanser

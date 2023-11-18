---
title: Köra verktyget Innehållsöverföring på en publiceringsinstans
description: Köra verktyget Innehållsöverföring på en publiceringsinstans
exl-id: 01faab94-a939-4004-b094-e9eb8f67b96e
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 0%

---

# Köra verktyget Innehållsöverföring på en publiceringsinstans {#run-content-transfer-tool-publish-instance}

## Introduktion {#introduction}

Innehållsöverföringsverktyget (CTT) utför ingen typ av innehållsanalys innan innehåll överförs från källinstansen till målinstansen. CTT skiljer till exempel inte mellan publicerat och opublicerat innehåll när innehåll hämtas till en publiceringsmiljö. Det innehåll som anges i migreringsuppsättningen hämtas till den valda målinstansen. Användaren kan importera en migreringsuppsättning till en Author-instans eller en Publish-instans eller både och.

>[!NOTE]
>Vi rekommenderar att du installerar Content Transfer Tool på källinstansen Author när du flyttar innehåll till målinstansen Author, och på samma sätt installerar Content Transfer Tool på källinstansen Publish för att flytta innehåll till målinstansen Publish. Se [Rekommenderat tillvägagångssätt](#recommended-approach) för mer information.

## Rekommenderat tillvägagångssätt {#recommended-approach}

Följ de rekommenderade tillvägagångssätten som beskrivs nedan:

* Använd samma version av verktyget Innehållsöverföring som användes på författarinstansen.

* Endast en publiceringsnod får migreras. Den bör avlägsnas från belastningsutjämnaren innan extraheringen påbörjas.

* Publiceringsnivån skalas inte ned under publiceringsprocessen (till skillnad från författaren).

  >[!IMPORTANT]
  >Som en försiktighetsåtgärd bör du undvika alla användarinitierade skrivåtgärder, som:
  > * Innehållsdistribution från AEM as a Cloud Service Author till Publish i den miljön
  > * Användarsynkronisering mellan publiceringsinstanser

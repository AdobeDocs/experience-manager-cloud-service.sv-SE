---
title: Köra verktyget Innehållsöverföring på en Publish-instans
description: Köra verktyget Innehållsöverföring på en Publish-instans
exl-id: 01faab94-a939-4004-b094-e9eb8f67b96e
feature: Migration
role: Admin
source-git-commit: 4408f15ef85d0fc2c6a0e2b45038dc900d212187
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 0%

---

# Köra verktyget Innehållsöverföring på en Publish-instans {#run-content-transfer-tool-publish-instance}

## Introduktion {#introduction}

Innehållsöverföringsverktyget (CTT) utför ingen typ av innehållsanalys innan innehåll överförs från källinstansen till målinstansen. CTT skiljer till exempel inte mellan publicerat och opublicerat innehåll när innehåll hämtas till en Publish-miljö. Det innehåll som anges i migreringsuppsättningen hämtas till den valda målinstansen. En användare kan importera en migreringsuppsättning till en Author-instans eller en Publish-instans eller både och.

>[!NOTE]
>Vi rekommenderar att du installerar Content Transfer Tool på källinstansen Author när du flyttar innehåll till målinstansen Author och på samma sätt installerar Content Transfer Tool på Publish-källinstansen för att flytta innehåll till Publish-målinstansen. Mer information finns i avsnittet [Rekommenderad metod](#recommended-approach) nedan.

## Rekommenderat tillvägagångssätt {#recommended-approach}

Följ de rekommenderade tillvägagångssätten som beskrivs nedan:

* Använd samma version av verktyget Innehållsöverföring som användes på författarinstansen.

* Endast en publiceringsnod får migreras. Den bör avlägsnas från belastningsutjämnaren innan extraheringen påbörjas.

* Publiceringsnivån skalas inte ned under publiceringsprocessen (till skillnad från författaren).

  >[!IMPORTANT]
  >Som en försiktighetsåtgärd bör du undvika alla användarinitierade skrivåtgärder, som:
  > * Innehållsdistribution från AEM as a Cloud Service Author till Publish i den miljön
  > * Användarsynkronisering mellan publiceringsinstanser

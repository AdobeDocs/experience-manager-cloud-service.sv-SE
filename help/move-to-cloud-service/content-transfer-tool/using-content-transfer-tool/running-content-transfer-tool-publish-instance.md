---
title: Köra verktyget Innehållsöverföring på en publiceringsinstans
description: Köra verktyget Innehållsöverföring på en publiceringsinstans
source-git-commit: 86b118e05b1e6947610c6032ed973394ba4b68e5
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 0%

---


# Köra verktyget Innehållsöverföring på en publiceringsinstans {#run-content-transfer-tool-publish-instance}

## Introduktion {#introduction}

Innehållsöverföringsverktyget (CTT) utför ingen typ av innehållsanalys innan innehåll överförs från källinstansen till målinstansen. CTT skiljer till exempel inte mellan publicerat och opublicerat innehåll när innehåll hämtas till en publiceringsmiljö. Det innehåll som anges i migreringsuppsättningen hämtas till den valda målinstansen. Användaren kan importera en migreringsuppsättning till en Author-instans eller en Publish-instans eller både och.

>[!NOTE]
>Vi rekommenderar att du installerar Content Transfer Tool på källinstansen Author när du flyttar innehåll till målinstansen Author, och på samma sätt installerar Content Transfer Tool på källinstansen Publish för att flytta innehåll till målinstansen Publish. Mer information finns i avsnittet [Rekommenderad strategi](#recommended-approach) nedan.

## Rekommenderat tillvägagångssätt {#recommended-approach}

Följ de rekommenderade tillvägagångssätten som beskrivs nedan:

* Använd samma version av verktyget Innehållsöverföring som användes på författarinstansen.

* Endast en publiceringsnod behöver migreras. Den bör avlägsnas från belastningsutjämnaren innan extraheringen påbörjas.

* När du skapar migreringsuppsättningen använder du URL:en för författaren AEM den as a Cloud Service miljön.

* Publiceringsnivån skalas inte ned under publiceringsprocessen (till skillnad från författaren).

   >[!IMPORTANT]
   >Som en försiktighetsåtgärd bör du undvika att användare startar skrivåtgärder, som:
   > * Innehållsdistribution från AEM as a Cloud Service Author till Publish i den miljön
   > * Användarsynkronisering mellan publiceringsinstanser


---
title: Översikt över verktyget Innehållsöverföring (äldre)
description: Översikt över Content Transfer Tool
hide: true
hidefromtoc: true
source-git-commit: 1fb4d0f2a3b3f9a27f5ab1228ec2d419149e0764
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 62%

---

# Översikt över verktyget Innehållsöverföring (äldre) {#overview-content-transfer-tool}

Content Transfer Tool är ett verktyg som utvecklats av Adobe och som kan användas för att flytta befintligt innehåll från en AEM-källinstans (On-premise eller AMS) till målinstansen av AEM Cloud Service.

Med det här verktyget överförs även huvudkonton (användare eller grupper) automatiskt.

## Phases in Content Transfer Tool {#phases-content-transfer-tool}

Det finns två faser som är associerade med innehållsöverföring:

1. **Extrahering**: Extrahering avser att extrahera innehåll från AEM-källinstansen till ett temporärt område som kallas *migreringsuppsättning*. En *migreringsuppsättning* är ett molnlagringsutrymme som finns hos Adobe för att tillfälligt lagra det överförda innehållet mellan AEM-källinstansen och Cloud Service AEM-instansen.

   Mer information finns i [Extraheringsprocess i innehållsöverföring](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/extracting-content.html).

   >[!NOTE]
   > Vi rekommenderar att du kör verktyget för användarmappning som en del av extraheringsfasen. Se [Använda verktyget för användarmappning](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/user-mapping-tool/using-user-mapping-tool.html) för mer information.

1. **Inmatning**: Inmatning avser att hämta innehåll från *migreringsuppsättningen* till Cloud Service-instansen.

   Se [Inmatningsprocess i innehållsöverföring](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/ingesting-content.html) för mer information.

## Attribut för en migreringsuppsättning {#attributes-migration-set}

En migreringsuppsättning har följande attribut:

* Högst tio migreringsuppsättningar kan skapas och underhållas samtidigt under innehållsöverföringsaktiviteten.
* Varje migreringsuppsättning ska ha ett unikt namn.
* Om en migreringsuppsättning har varit inaktiv i mer än 30 dagar tas den bort automatiskt.
* När du skapar en migreringsuppsättning kopplas den till en viss miljö. Du kan bara importera till en författar- eller en publiceringsinstans av samma miljö.


Content Transfer Tool har en funktion för differentiell innehållsuppdatering som gör att du kan överföra enbart de ändringar som gjorts sedan den föregående innehållsöverföringen.

>[!NOTE]
>Efter den första innehållsöverföringen bör du göra regelbundna tillägg av differentiellt innehåll för att förkorta innehållets frysningsperiod för den slutliga differentiella innehållsöverföringen innan du börjar använda Cloud Service.

I extraheringsfasen måste alternativet för ***overwrite*** vara inaktiverat för att en befintlig migreringsuppsättning ska kunna *uppdateras*. Mer information finns i [Extrahering av ändringar](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/extracting-content.html?lang=en#top-up-extraction-process).

För att delta-innehållet ska kunna tillämpas ovanpå det aktuella innehållet måste alternativet *wipe* vara inaktiverat i inmatningsfasen. Mer information finns i [Uppdatera inmatning](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/ingesting-content.html?lang=en#top-up-ingestion-process).

## What&#39;s Next {#whats-next}

När du har lärt dig om verktyget Innehållsöverföring och dess översikt som beskriver det här verktyget kan användas för att flytta befintligt innehåll från en AEM (lokalt eller AMS) till målförekomsten i AEM Cloud Service måste du granska [Krav för verktyget Innehållsöverföring](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/prerequisites-content-transfer-tool.html?lang=en).

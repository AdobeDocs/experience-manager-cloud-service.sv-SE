---
title: Översikt över Content Transfer Tool
description: Lär dig hur du använder verktyget Innehållsöverföring för att överföra innehåll från en lokal AEM till AEM as a Cloud Service
exl-id: cfc0366a-2139-4d9d-b5bc-0b65bef4013c
source-git-commit: 8c73805b6ed1b7a03c65b4d21a4252c1412a5742
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 31%

---

# Översikt {#overview-content-transfer-tool}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_overview"
>title="Översikt"
>abstract="Verktyget Innehållsöverföring är ett verktyg som utvecklats av Adobe och som kan användas för att initiera migreringen av befintligt innehåll från en AEM (lokalt eller AMS) till AEM Cloud Service-målinstansen. Med det här verktyget överförs även huvudkonton (användare eller grupper) automatiskt."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html" text="Riktlinjer och bästa praxis"

Verktyget Innehållsöverföring är ett verktyg som utvecklats av Adobe och som kan användas för att initiera migreringen av befintligt innehåll från en AEM (lokalt eller AMS) till AEM Cloud Service-målinstansen.

Med det här verktyget överförs även huvudkonton (användare eller grupper) automatiskt.  Se [Användarmappning och huvudmigrering](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/user-mapping-and-migration.md) för mer information.

Innehållsöverföringsverktyget integrerar innehållsöverföringsprocessen med Cloud Acceleration Manager. Detta ger användaren alla fördelar den ger:

* Självbetjäningssätt att extrahera en migreringsuppsättning en gång och importera den i flera miljöer parallellt
* Förbättrad användarupplevelse tack vare bättre inläsningstillstånd, skyddsräcken och felhantering
* Inmatningsloggarna är beständiga och är alltid tillgängliga för felsökning
* Validerings- och huvudmigreringsrapporter finns tillgängliga för validering

## Phases in Content Transfer Tool {#phases-content-transfer-tool}

Det finns två faser som är associerade med innehållsöverföring:

1. **Extrahering**: Extrahering avser att extrahera innehåll från AEM-källinstansen till ett temporärt område som kallas *migreringsuppsättning*. En *migreringsuppsättning* är ett molnlagringsutrymme som finns hos Adobe för att tillfälligt lagra det överförda innehållet mellan AEM-källinstansen och Cloud Service AEM-instansen.

   Se [Extraheringsprocess i innehållsöverföring](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md) för mer information.

   >[!NOTE]
   >Användarmappning körs nu automatiskt som en del av extraheringsfasen på författaren (men kan även inaktiveras på författaren eller aktiveras vid publicering). Se [Användarmappning och huvudmigrering](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/user-mapping-and-migration.md) för mer information.

1. **Inmatning**: Inmatning avser att hämta innehåll från *migreringsuppsättningen* till Cloud Service-instansen.

   Se [Inmatningsprocess i innehållsöverföring](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md) för mer information.

## Attribut för en migreringsuppsättning {#attributes-migration-set}

En migreringsuppsättning har följande attribut:

* Med den nya versionen kan du skapa maximalt fem migreringsuppsättningar i ett projekt som skapats i Cloud Acceleration Manager.
* Varje migreringsuppsättning ska ha ett unikt namn.

Content Transfer Tool har en funktion för differentiell innehållsuppdatering som gör att du kan överföra enbart de ändringar som gjorts sedan den föregående innehållsöverföringen.

>[!NOTE]
>Efter den första innehållsöverföringen bör du göra regelbundna tillägg av differentiellt innehåll för att förkorta innehållets frysningsperiod för den slutliga differentiella innehållsöverföringen innan du börjar använda Cloud Service.

I extraheringsfasen måste alternativet för ***overwrite*** vara inaktiverat för att en befintlig migreringsuppsättning ska kunna *uppdateras*. Se [Extrahering uppifrån](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process) för mer information.

För att delta-innehållet ska kunna tillämpas ovanpå det aktuella innehållet måste alternativet *wipe* vara inaktiverat i inmatningsfasen. Se [Övre inmatning](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process) för mer information.

## Förfallotid för migreringsuppsättning {#migration-set-expiry}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_migrationset_expiry"
>title="Förfallodatum för en migreringsuppsättning"
>abstract="Lär dig mer om när en migreringsuppsättning upphör att gälla."

Alla migreringsuppsättningar upphör så småningom efter en längre inaktivitetsperiod på ungefär 90 dagar. När indikatorerna visas på projektkortet och migreringsjobbtabellraderna under en tidsperiod, kommer migreringsuppsättningen att upphöra att gälla och dess data kommer inte längre att vara tillgängliga. Utgångsdatumet kan enkelt förlängas genom att du agerar på migreringsuppsättningen genom att:

* redigera sin beskrivning
* hämta extraheringsnyckeln
* utföra extrahering
* utföra ett intag från den

En migreringsuppsättnings förfallodatum kan övervakas på raden Migreringsuppsättning. En användbar visuell indikator på att en migreringsuppsättning närmar sig förfallodatumet har även lagt till projektets kort.

![bild](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam29.png)


## What&#39;s Next {#whats-next}

När du har lärt dig om verktyget Innehållsöverföring och dess översikt som beskriver det här verktyget kan användas för att flytta befintligt innehåll från en AEM (lokalt eller AMS) till målförekomsten i AEM Cloud Service måste du granska [Krav för verktyget Innehållsöverföring](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/prerequisites-content-transfer-tool.md).

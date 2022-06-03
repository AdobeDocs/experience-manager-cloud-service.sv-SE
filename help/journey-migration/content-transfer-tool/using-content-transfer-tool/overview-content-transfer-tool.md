---
title: Översikt över Content Transfer Tool
description: Översikt över Content Transfer Tool
exl-id: cfc0366a-2139-4d9d-b5bc-0b65bef4013c
source-git-commit: 3bf12642e94076a67010e4701715a54138a490ee
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 43%

---

# Översikt {#overview-content-transfer-tool}


>[!CONTEXTUALHELP]
>id="aemcloud_ctt_overview"
>title="Översikt"
>abstract="Verktyget Innehållsöverföring är ett verktyg som utvecklats av Adobe och som kan användas för att flytta befintligt innehåll från en AEM (lokalt eller AMS) till AEM Cloud Service-målinstansen. Med det här verktyget överförs även huvudkonton (användare eller grupper) automatiskt."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html?lang=en" text="Riktlinjer och bästa praxis"

<!-- Alexandru: Old version of contextual help, keep for failover/debugging
>[!CONTEXTUALHELP]
>id="aemcloud_ctt_overview"
>title="Overview"
>abstract="Content Transfer Tool is a tool developed by Adobe that can be used to move existing content over from a source AEM instance (on-premise or AMS) to the target AEM Cloud Service instance. This tool also transfers principals (users or groups) automatically."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#extraction-process" text="Extraction Process"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#ingestion-process" text="Ingestion Process" -->

Content Transfer Tool är ett verktyg som utvecklats av Adobe och som kan användas för att flytta befintligt innehåll från en AEM-källinstans (On-premise eller AMS) till målinstansen av AEM Cloud Service.

Med det här verktyget överförs även huvudkonton (användare eller grupper) automatiskt.

Det finns en ny version av verktyget Innehållsöverföring som integrerar innehållsöverföringsprocessen med Cloud Acceleration Manager. Vi rekommenderar att du går över till den nya versionen för att utnyttja alla fördelar den ger:

* Självbetjäningssätt att extrahera en migreringsuppsättning en gång och importera den i flera miljöer parallellt
* Förbättrad användarupplevelse tack vare bättre inläsningstillstånd, skyddsräcken och felhantering
* Inmatningsloggarna är beständiga och finns alltid tillgängliga för felsökning

Så här börjar du använda den nya versionen (v2.0.10) <!-- update when version is available --> du måste avinstallera äldre versioner av verktyget Innehållsöverföring eftersom det har skett en stor förändring i arkitekturen.

>[!NOTE]
>
> I situationer där en migrering redan pågår kan du fortsätta använda den tidigare versionen av CTT tills migreringen är klar. Dokumentation om föregående version av CTT finns i [äldre dokumentation](/help/journey-migration/content-transfer-tool/ctt-legacy/overview-content-transfer-tool-legacy.md).

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

* Med den nya versionen kan du skapa maximalt fem migreringsuppsättningar i ett projekt som skapats i Cloud Acceleration Manager.
* Varje migreringsuppsättning ska ha ett unikt namn.

Content Transfer Tool har en funktion för differentiell innehållsuppdatering som gör att du kan överföra enbart de ändringar som gjorts sedan den föregående innehållsöverföringen.

>[!NOTE]
>Efter den första innehållsöverföringen bör du göra regelbundna tillägg av differentiellt innehåll för att förkorta innehållets frysningsperiod för den slutliga differentiella innehållsöverföringen innan du börjar använda Cloud Service.

I extraheringsfasen måste alternativet för ***overwrite*** vara inaktiverat för att en befintlig migreringsuppsättning ska kunna *uppdateras*. Mer information finns i [Extrahering av ändringar](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/extracting-content.html?lang=en#top-up-extraction-process).

För att delta-innehållet ska kunna tillämpas ovanpå det aktuella innehållet måste alternativet *wipe* vara inaktiverat i inmatningsfasen. Mer information finns i [Uppdatera inmatning](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/ingesting-content.html?lang=en#top-up-ingestion-process).

## What&#39;s Next {#whats-next}

När du har lärt dig om verktyget Innehållsöverföring och dess översikt som beskriver det här verktyget kan användas för att flytta befintligt innehåll från en AEM (lokalt eller AMS) till målförekomsten i AEM Cloud Service måste du granska [Krav för verktyget Innehållsöverföring](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/prerequisites-content-transfer-tool.html?lang=en).

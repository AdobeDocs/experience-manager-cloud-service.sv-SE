---
title: Översikt över verktyget Innehållsöverföring
description: Översikt över verktyget Innehållsöverföring
translation-type: tm+mt
source-git-commit: 3478827949356c4a4f5133b54c6cf809f416efef
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 0%

---


# Översikt {#overview-content-transfer-tool}

Verktyget Innehållsöverföring är ett verktyg som utvecklats av Adobe och som kan användas för att flytta befintligt innehåll från en AEM-källinstans (lokalt eller AMS) till målinstansen av AEM Cloud-tjänsten.

Med det här verktyget överförs även huvudkonton (användare eller grupper) automatiskt.

Det finns två faser som är associerade med innehållsöverföring:

1. **Extrahering**:  Extrahering avser att extrahera innehåll från AEM-källinstansen till ett temporärt område som kallas *migreringsuppsättning*. En *migreringsuppsättning* är ett molnlagringsutrymme som tillhandahålls av Adobe för att tillfälligt lagra det överförda innehållet mellan AEM-källinstansen och AEM-instansen i molntjänsten.

   Mer information finns i [Extraheringsprocess i Innehållsöverföring](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#extraction-process) .

2. **Inmatning**: Inmatning avser att hämta innehåll från *migreringsuppsättningen* till målmolntjänstinstansen.

   Mer information finns i [Inmatningsprocessen i Innehållsöverföring](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#ingestion-process) .

En *migreringsuppsättning* har följande attribut:

* Högst fyra migreringsuppsättningar kan skapas och underhållas samtidigt under innehållsöverföringsaktiviteten.
* Varje migreringsuppsättning ska ha ett unikt namn.
* Om en migreringsuppsättning har varit inaktiv i mer än 30 dagar tas den bort automatiskt.
* När du skapar en migreringsuppsättning kopplas den till en viss miljö. Du kan bara importera till en författare eller en publiceringsinstans av samma miljö.

Verktyget Innehållsöverföring har en funktion som har stöd för differentiell innehållsuppsättning där det endast är möjligt att överföra ändringar som gjorts sedan föregående innehållsöverföringsaktivitet.

>[!NOTE]
> Efter den första innehållsöverföringen bör du göra regelbundna tillägg av differentiellt innehåll för att förkorta innehållets frysningsperiod för den slutliga differentiella innehållsöverföringen innan du börjar använda molntjänsten.

I extraheringsfasen måste alternativet för ***överskrivning*** vara inaktiverat för att en befintlig migreringsuppsättning ska kunna visas ** överst. Mer information finns i Extrahering [uppifrån](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#top-up-extraction-process) .

För att delta-innehållet ska kunna tillämpas ovanpå det aktuella innehållet måste *rensningsalternativet* vara inaktiverat i överföringsfasen. Mer information finns i [Uppåtinmatning](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#top-up-ingestion-process) .


## Riktlinjer och bästa praxis {#best-practices}

Följ nedanstående avsnitt för att få information om riktlinjer och bästa metoder för att använda verktyget Innehållsöverföring:

* Det är tillrådligt att köra komprimering, konsekvenskontroller av datalager på databaserna innan du upptäcker potentiella problem och även minska skräpinsamlingen i databasen.

* Om konfigurationen för AEM Cloud Author Content Delivery Network (CDN) har en vitlista över IP-adresser måste du se till att även IP-adresserna för källmiljön läggs till i vitlistan så att källmiljön och AEM Cloud-miljön kan kommunicera med varandra.

* I inmatningsfasen rekommenderas att du kör inmatningen med *svepningsläget* aktiverat där den befintliga databasen (författaren eller publiceringen) i AEM Cloud-måltjänstmiljön tas bort helt och sedan uppdateras med migreringsuppsättningsdata. Det här läget är mycket snabbare än icke-svepningsläget, där migreringsuppsättningen används ovanpå det aktuella innehållet.

* När innehållsöverföringsaktiviteten har slutförts krävs rätt projektstruktur i molntjänstmiljön för att se till att innehållet återges korrekt i molntjänstmiljön.
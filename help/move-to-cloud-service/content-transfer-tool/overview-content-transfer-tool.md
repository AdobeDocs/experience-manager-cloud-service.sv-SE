---
title: Översikt över Content Transfer Tool
description: Översikt över Content Transfer Tool
exl-id: 4715937e-4c4c-4680-af15-016db4fe7db9
translation-type: tm+mt
source-git-commit: 7bdf8f1e6d8ef1f37663434e7b14798aeb8883f4
workflow-type: tm+mt
source-wordcount: '813'
ht-degree: 79%

---

# Översikt {#overview-content-transfer-tool}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_overview"
>title="Översikt"
>abstract="Verktyget Innehållsöverföring är ett verktyg som utvecklats av Adobe och som kan användas för att flytta befintligt innehåll från en AEM (lokalt eller AMS) till AEM Cloud Service. Med det här verktyget överförs även huvudkonton (användare eller grupper) automatiskt."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#extraction-process" text="Extraheringsprocess"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#ingestion-process" text="Inmatningsprocess"

Content Transfer Tool är ett verktyg som utvecklats av Adobe och som kan användas för att flytta befintligt innehåll från en AEM-källinstans (On-premise eller AMS) till målinstansen av AEM Cloud Service.

Med det här verktyget överförs även huvudkonton (användare eller grupper) automatiskt.

Det finns två faser som är associerade med innehållsöverföring:

1. **Extrahering**: Extrahering avser att extrahera innehåll från AEM-källinstansen till ett temporärt område som kallas *migreringsuppsättning*. En *migreringsuppsättning* är ett molnlagringsutrymme som finns hos Adobe för att tillfälligt lagra det överförda innehållet mellan AEM-källinstansen och Cloud Service AEM-instansen.

   Mer information finns i [Extraheringsprocess i innehållsöverföring](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#extraction-process).

>[!NOTE]
>
> Vi rekommenderar att du kör verktyget för användarmappning som en del av extraheringsfasen. Mer information finns i [Använda verktyget för användarmappning](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#cloud-migration).

1. **Inmatning**: Inmatning avser att hämta innehåll från *migreringsuppsättningen* till Cloud Service-instansen.

   Mer information finns i [Inmatningsprocess i innehållsöverföring](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#ingestion-process).

En *migreringsuppsättning* har följande attribut:

* Högst fyra migreringsuppsättningar kan skapas och underhållas samtidigt under innehållsöverföringen.
* Varje migreringsuppsättning ska ha ett unikt namn.
* Om en migreringsuppsättning har varit inaktiv i mer än 30 dagar tas den bort automatiskt.
* När du skapar en migreringsuppsättning kopplas den till en viss miljö. Du kan bara importera till en författar- eller en publiceringsinstans av samma miljö.

Content Transfer Tool har en funktion för differentiell innehållsuppdatering som gör att du kan överföra enbart de ändringar som gjorts sedan den föregående innehållsöverföringen.

>[!NOTE]
>
>Efter den första innehållsöverföringen bör du göra regelbundna tillägg av differentiellt innehåll för att förkorta innehållets frysningsperiod för den slutliga differentiella innehållsöverföringen innan du börjar använda Cloud Service.

I extraheringsfasen måste alternativet för ***overwrite*** vara inaktiverat för att en befintlig migreringsuppsättning ska kunna *uppdateras*. Mer information finns i [Extrahering av ändringar](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#top-up-extraction-process).

För att delta-innehållet ska kunna tillämpas ovanpå det aktuella innehållet måste alternativet *wipe* vara inaktiverat i inmatningsfasen. Mer information finns i [Uppdatera inmatning](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#top-up-ingestion-process).


## Riktlinjer och bästa praxis {#best-practices}

>id=&quot;aemcloud_ctt_guidelines&quot;
>title=&quot;Guidelines and Best Practices&quot;
>abstract=&quot;Riktlinjer och bästa praxis för användning av verktyget Innehållsöverföring, inklusive rensning av revisioner, diskutrymme med mera.&quot;
>additional-url=&quot;https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#pre-reqs&quot; text=&quot;Viktigt att tänka på vid användning av verktyget Innehållsöverföring&quot;
>additional-url=&quot;https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#important-considerations&quot; text=&quot;Viktigt att tänka på vid användning av verktyget för användarmappning&quot;

Följ nedanstående avsnitt för att få information om riktlinjer och bästa praxis för att använda Content Transfer Tool:

* Du bör köra [Revision Cleanup](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/deploying/revision-cleanup.html) och [databasens konsekvenskontroller](https://helpx.adobe.com/experience-manager/kb/How-to-run-a-datastore-consistency-check-via-oak-run-AEM.html) på **källdatabasen** för att identifiera potentiella problem och minska databasens storlek.

* Om konfigurationen för AEM Cloud Author Content Delivery Network (CDN) har en vitlista över IP-adresser måste du se till att IP-adresserna för källmiljön läggs till i den tillåtna listan så att källmiljön och AEM Cloud-miljön kan kommunicera med varandra.

* I inmatningsfasen rekommenderas att du kör inmatningen med *wipe*-läget aktiverat där den befintliga databasen (Author eller Publish) i AEM Cloud Service-miljön tas bort helt och sedan uppdateras med migreringsuppsättningsdata. Det här läget är mycket snabbare än non-wipe-läget, där migreringsuppsättningen tillämpas ovanpå det aktuella innehållet.

* När innehållsöverföringen har slutförts krävs rätt projektstruktur i Cloud Service-miljön så att innehållet återges korrekt i denna miljö.

* Innan du kör verktyget Content Transfer Tool måste du se till att det finns tillräckligt med diskutrymme i AEM-källinstansens underkatalog `crx-quickstart`. Det beror på att Content Transfer Tool skapar en lokal kopia av databasen som senare överförs till migreringsuppsättningen.
Den allmänna formeln för att beräkna hur mycket ledigt diskutrymme som krävs är följande:
   `data store size + node store size * 1.5`

   * *databasens storlek*: Content Transfer Tool använder 64 GB, även om den faktiska databasen är större.
   * *noddatabasens storlek*: storlek på segmentdatabaskatalogen eller storlek på MongoDB-databasen.
För en segmentdatabasstorlek på 20 GB krävs därför 94 GB ledigt diskutrymme.

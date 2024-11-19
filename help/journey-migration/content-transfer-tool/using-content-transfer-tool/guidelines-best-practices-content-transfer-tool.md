---
title: Riktlinjer och bästa praxis för användning av verktyget Innehållsöverföring
description: Lär dig riktlinjerna och de bästa sätten att använda verktyget Innehållsöverföring.
exl-id: d1975c34-85d4-42e0-bb1a-968bdb3bf85d
feature: Migration
role: Admin
source-git-commit: 943685ed9c33ba42c4dd1cb941b2eca1cce8bfe8
workflow-type: tm+mt
source-wordcount: '1389'
ht-degree: 11%

---


# Riktlinjer och bästa metoder för att använda verktyget Innehållsöverföring {#guidelines}

## Riktlinjer och bästa praxis {#best-practices}

<!-- Alexandru: hiding for now

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_guidelines"
>title="Guidelines and Best Practices"
>abstract="Review guidelines and best practices to use the Content Transfer tool including revision cleanup tasks, Disk space considerations and more."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html" text="Important Considerations for using Content Transfer Tool"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/group-migration.md#important-considerations" text="Important Considerations when Migrating Groups" 

-->

Innehållsöverföringsverktyget integrerar innehållsöverföringsprocessen med Cloud Acceleration Manager. Du måste använda den här versionen (2.0 eller senare, men version 3.0 rekommenderas nu) för att få alla fördelar den ger:

* Självbetjäningssätt att extrahera en migreringsuppsättning en gång och importera den i flera miljöer parallellt
* Förbättrad användarupplevelse genom bättre inläsningstillstånd, skyddsutkast och felhantering
* Inmatningsloggarna är beständiga och är alltid tillgängliga för felsökning

Om du vill börja använda den senaste versionen avinstallerar du tidigare versioner av verktyget Innehållsöverföring. Med version 2.0 och senare skapar du migreringsuppsättningar och kör extraheringen och intaget på uppsättningarna igen.
Versioner som är tidigare än 2.0.0 stöds inte och du bör använda den senaste versionen.

Följande riktlinjer och bästa praxis gäller för den nya versionen av verktyget Innehållsöverföring:

* Kör [Konsekvenskontroll av revideringsrensning](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/revision-cleanup.html) och [datalagret](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-16550.html) på **source**-databasen så att du kan identifiera potentiella problem och minska storleken på databasen.

* I inmatningsfasen rekommenderar Adobe att du kör inmatningen med läget *svep* aktiverat där den befintliga databasen (författare eller Publish) i målmiljön för Adobe Experience Manager (AEM) tas bort. Uppdatera sedan med data för migreringsuppsättningen. Det här läget är snabbare än icke-svepningsläget, där migreringsuppsättningen används ovanpå det aktuella innehållet.

* När innehållsöverföringen har slutförts krävs rätt projektstruktur i Cloud Service-miljön så att innehållet återges korrekt i denna miljö.

* Innan du kör verktyget Content Transfer Tool måste du se till att det finns tillräckligt med diskutrymme i AEM-källinstansens underkatalog `crx-quickstart`. Det beror på att Content Transfer Tool skapar en lokal kopia av databasen som senare överförs till migreringsuppsättningen.
Den allmänna formeln för beräkning av ledigt diskutrymme är följande:
  `data store size + node store size * 1.5`

* *databasens storlek*: Content Transfer Tool använder 64 GB, även om den faktiska databasen är större.
* *noddatabasens storlek*: storlek på segmentdatabaskatalogen eller storlek på MongoDB-databasen.
För en segmentdatabasstorlek på 20 GB krävs därför 94 GB ledigt diskutrymme.

* En migreringsuppsättning måste finnas under hela innehållsöverföringsaktiviteten för att det ska gå att göra innehållsöverläggningar. Högst 10 migreringsuppsättningar per projekt i Cloud Acceleration Manager kan skapas och underhållas samtidigt under innehållsöverföringsaktiviteten. Om det behövs fler än 10 migreringsuppsättningar skapar du ett andra projekt i Cloud Acceleration Manager. Detta kräver dock ytterligare projekthantering och styrning utanför produkten för att undvika att flera användare skriver över innehåll på målet.

* Ändra inte installationskatalogen för CTT-verktyget. Installationen görs som standard i sökvägen crx-quickstart/cloud-migration. Den här platsen används internt av andra bibliotek. Om du ändrar den här sökvägen kan det uppstå extraheringsproblem.

## Viktigt att tänka på innan du använder verktyget Innehållsöverföring {#important-considerations}

Följ avsnittet nedan om du vill veta mer om viktiga aspekter när du använder Content Transfer Tool:

* Systemkraven för Content Transfer Tool är AEM 6.3 + och Java™ 8. Om du har en lägre AEM uppgraderar du ditt innehållsarkiv till AEM 6.5 för att använda verktyget för innehållsöverföring.

* Java™ måste konfigureras i AEM så att kommandot `java` kan köras av den användare som startar AEM.

* Verktyget Innehållsöverföring kan användas med följande typer av datalager: File Data Store, S3 Data Store, Shared S3 Data Store och Azure Blob Store Data Store.

* Om du använder en *sandlådemiljö* kontrollerar du att miljön är aktuell och uppgraderad till den senaste versionen. Om du använder en *produktionsmiljö* uppdateras den automatiskt.

* Om du vill påbörja ett inlägg måste du tillhöra den lokala gruppen AEM **administratörer** i den Cloud Service som du överför innehåll till. Obehöriga användare kan inte starta inmatningar utan att ange migreringstoken manuellt.

* Om inställningen **Rensa befintligt innehåll i molninstansen innan** har aktiverats, tas hela den befintliga databasen bort och en ny databas skapas för att importera innehåll till. Det innebär att alla inställningar återställs, inklusive behörigheter för målinstansen av Cloud Servicen. Det gäller även för en administratörsanvändare som har lagts till i gruppen **administratörer**. Användaren måste läsas till gruppen **administratörer** för att hämta åtkomsttoken för verktyget Innehållsöverföring.

* Extraheringsnyckeln gäller i 14 dagar från den tidpunkt då den skapades eller förnyades. Den kan förnyas när som helst. Om extraheringsnyckeln har upphört att gälla kan du inte utföra en extrahering.

* Innehållsöverföringsverktyget (CTT) utför ingen typ av innehållsanalys innan innehåll överförs från källinstansen till målinstansen. CTT skiljer till exempel inte mellan publicerat och opublicerat innehåll när innehåll hämtas till en Publish-miljö. Det innehåll som anges i migreringsuppsättningen hämtas till den valda målinstansen. En användare kan importera en migreringsuppsättning till en Author-instans eller en Publish-instans eller både och. Adobe rekommenderar att CTT installeras på källförfattarinstansen när innehåll flyttas till en Production-instans för att flytta innehållet till målförfattarinstansen. Du kan även installera CTT på Publish-källinstansen för att flytta innehåll till Publish-målinstansen. Mer information finns i [Köra verktyget Innehållsöverföring på en Publish-instans](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html#running-tool).

* De grupper som överförs av verktyget Innehållsöverföring är bara de grupper som krävs för att innehållet ska uppfylla behörigheterna. Processen _Extrahering_ kopierar hela `/home/groups` till migreringsuppsättningen. Mer information finns i [Gruppmigrering](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/group-migration.md). Processen _Inmatning_ kopierar alla grupper som refereras i de migrerade innehålls-ACL:erna. Se [Migrera stängda användargrupper](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/closed-user-groups-migration.md) om du vill ha mer information om grupper som används i en CUG-princip (Closed User Group).

* Under extraheringsfasen körs Content Transfer Tool på en aktiv AEM-källinstans.

* *Inmatningsfasen* för författaren skalas ned i hela författardistributionen. Det innebär att författarens AEM inte är tillgängligt under hela importen. Se även till att inga Cloud Manager-pipelines körs när du kör *Ingput* -fasen.

* När du använder `Amazon S3` eller `Azure` som datalager på AEM, bör datalagret konfigureras så att de lagrade blobbarna inte kan tas bort (skräpsamling). Detta garanterar indexdataintegritet och om detta inte konfigureras på det här sättet kan det leda till misslyckade extraheringar på grund av att dessa indexdata saknar integritet.

* Om du använder anpassade index måste du se till att konfigurera anpassade index med noden `tika` innan du kör verktyget Innehållsöverföring. Mer information finns i [Förbereder den nya indexdefinitionen](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/indexing.html#preparing-the-new-index-definition).

* Om du tänker göra toppuppsättningar får innehållsstrukturen i det befintliga innehållet inte ändras från den tidpunkt då den första extraheringen utförs till den tidpunkt då extraheringen av toppuppsättningar körs. Det går inte att köra uppsättningar på innehåll vars struktur har ändrats sedan den första extraheringen. Kontrollera att du begränsar detta under migreringsprocessen.

* Om du tänker ta med versioner som en del av en migreringsuppsättning och utför tilläggsprogram med `wipe=false`, måste du inaktivera versionsrensning på grund av en aktuell begränsning i verktyget Innehållsöverföring. Om du föredrar att behålla versionsrensning aktiverad och utför toppuppsättningar i en migreringsuppsättning, måste du utföra det som `wipe=true`.

* Innehållsöverföringsverktyget (CTT) stöder inte sammanfogningsförslag. Om du vill konsolidera innehåll från flera system till en enda instans av Cloud Servicen kan endast versioner från ett källsystem migreras. Den här processen kräver att migreringar med parametern wipe=false används, vilket kan ge utökad inmatningstid på grund av åtgärdens inkrementella karaktär. Om det är möjligt bör du konsolidera innehåll i ett enda källsystem innan du påbörjar migreringen, så att du slipper lägga samman innehåll.

* Ett migreringsset upphör att gälla efter en längre inaktivitetsperiod, efter vilken dess data inte längre är tillgängliga. Granska [migreringsuppsättningen upphör](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html#migration-set-expiry) om du vill ha mer information.

## What&#39;s Next {#whats-next}

När du har lärt dig riktlinjerna, de bästa metoderna och de viktiga sakerna att tänka på när du använder verktyget Innehållsöverföring är du nu redo att installera och använda verktyget, och börja med att skapa en migreringsuppsättning. Se [Komma igång med verktyget Innehållsöverföring](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/getting-started-content-transfer-tool.md).

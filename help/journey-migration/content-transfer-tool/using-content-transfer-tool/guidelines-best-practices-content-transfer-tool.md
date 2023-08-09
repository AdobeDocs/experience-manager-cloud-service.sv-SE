---
title: Riktlinjer och bästa metoder för att använda verktyget Innehållsöverföring
description: Riktlinjer och bästa metoder för att använda verktyget Innehållsöverföring
exl-id: d1975c34-85d4-42e0-bb1a-968bdb3bf85d
source-git-commit: 83c6c3c8c069059e49b632f332e24946e1712cb7
workflow-type: tm+mt
source-wordcount: '1562'
ht-degree: 14%

---

# Riktlinjer och bästa metoder för att använda verktyget Innehållsöverföring {#guidelines}

## Riktlinjer och bästa praxis {#best-practices}

<!-- Alexandru: hiding for now

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_guidelines"
>title="Guidelines and Best Practices"
>abstract="Review guidelines and best practices to use the Content Transfer tool including revision cleanup tasks, Disk space considerations and more."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html" text="Important Considerations for using Content Transfer Tool"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/user-mapping-and-migration.md#important-considerations" text="Important Considerations when Mapping and Migrating Users" 

-->

Det finns en ny version av verktyget Innehållsöverföring som integrerar innehållsöverföringsprocessen med Cloud Acceleration Manager. Vi rekommenderar att du går över till den nya versionen för att utnyttja alla fördelar den ger:

* Självbetjäningssätt att extrahera en migreringsuppsättning en gång och importera den i flera miljöer parallellt
* Förbättrad användarupplevelse tack vare bättre inläsningstillstånd, skyddsräcken och felhantering
* Inmatningsloggarna är beständiga och är alltid tillgängliga för felsökning

Om du vill börja använda den nya versionen måste du avinstallera tidigare versioner av verktyget Innehållsöverföring. Detta behövs eftersom den nya versionen innehåller en stor arkitektoniska förändring. Med version 2.x måste du skapa nya migreringsuppsättningar och köra extraheringen och inmatningen på nytt för de nya migreringsuppsättningarna.
Versioner som är tidigare än 2.0.0 stöds inte längre och du bör använda den senaste versionen.

Följande riktlinjer och bästa praxis gäller för den nya versionen av verktyget Innehållsöverföring:

* Du bör köra [Revision Cleanup](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/revision-cleanup.html) och [databasens konsekvenskontroller](https://helpx.adobe.com/experience-manager/kb/How-to-run-a-datastore-consistency-check-via-oak-run-AEM.html) på **källdatabasen** för att identifiera potentiella problem och minska databasens storlek.

* I matningsfasen rekommenderas att man kör *svepa* aktiverat läge där den befintliga databasen (författare eller publicerad) i AEM Cloud Service-målmiljön tas bort helt och sedan uppdateras med data för migreringsuppsättningen. Det här läget är mycket snabbare än non-wipe-läget, där migreringsuppsättningen tillämpas ovanpå det aktuella innehållet.

* När innehållsöverföringen har slutförts krävs rätt projektstruktur i Cloud Service-miljön så att innehållet återges korrekt i denna miljö.

* Innan du kör verktyget Content Transfer Tool måste du se till att det finns tillräckligt med diskutrymme i AEM-källinstansens underkatalog `crx-quickstart`. Det beror på att Content Transfer Tool skapar en lokal kopia av databasen som senare överförs till migreringsuppsättningen.
Den allmänna formeln för beräkning av ledigt diskutrymme är följande:
  `data store size + node store size * 1.5`

   * *databasens storlek*: Content Transfer Tool använder 64 GB, även om den faktiska databasen är större.
   * *noddatabasens storlek*: storlek på segmentdatabaskatalogen eller storlek på MongoDB-databasen.
För en segmentdatabasstorlek på 20 GB krävs därför 94 GB ledigt diskutrymme.

* En migreringsuppsättning måste bibehållas under hela innehållsöverföringsaktiviteten för att kunna stödja innehållsöverläggningar. Högst fem migreringsuppsättningar per projekt i Cloud Acceleration Manager kan skapas och underhållas samtidigt under innehållsöverföringsaktiviteten. Om det behövs fler än fem migreringsuppsättningar måste du skapa ett andra projekt i Cloud Acceleration Manager. Detta kräver dock ytterligare projekthantering och styrning utanför produkten för att undvika att flera användare skriver över innehåll på målet.

## Viktigt att tänka på innan du använder verktyget Innehållsöverföring {#important-considerations}

Följ avsnittet nedan om du vill veta mer om viktiga aspekter när du använder Content Transfer Tool:

* Lägsta systemkrav för Content Transfer Tool är AEM 6.3 + och JAVA 8. Om du har en lägre AEM måste du uppgradera ditt innehållsarkiv till AEM 6.5 för att kunna använda verktyget för innehållsöverföring.

* Java måste konfigureras i AEM-miljön så att `java` kommandot kan köras av den användare som startar AEM.

* Verktyget Innehållsöverföring kan användas med följande typer av datalager: File Data Store, S3 Data Store, Shared S3 Data Store och Azure Blob Store Data Store.

* Om du använder en *Sandlådemiljö*, se till att din miljö är aktuell och uppgraderad till den senaste versionen. Om du använder en *produktionsmiljö* uppdateras den automatiskt.

* För att påbörja ett intag måste du tillhöra den lokala AEM **administratörer** i den Cloud Service som du överför innehåll till. Obehöriga användare kommer inte att kunna starta frågor utan att behöva ange migreringstoken manuellt.

* Om inställningen **Rensa befintligt innehåll i molninstansen före intag** om du aktiverar det här alternativet tas hela den befintliga databasen bort och en ny databas skapas där innehållet kan importeras till. Det innebär att alla inställningar återställs, inklusive behörigheter för målinstansen av Cloud Servicen. Detta gäller även för en admin-användare som har lagts till i **administratörer** grupp. Användaren måste läggas till på nytt i **administratörer** grupp för att hämta åtkomsttoken för verktyget Innehållsöverföring.

* Det finns inga funktioner för att sammanfoga innehåll från flera källor till målkällinstansen om Cloud Servicen från de två källorna flyttas till samma sökvägar i målet. Om du vill flytta innehåll från flera olika källor till en enda instans av målsökvägen måste du se till att det inte finns någon överlappning mellan innehållssökvägarna från Cloud Servicen.

* Extraheringsnyckeln gäller i 14 dagar från den tidpunkt den skapades/förnyades. Den kan förnyas när som helst. Om extraheringsnyckeln har gått ut kan du inte utföra en extrahering.

* Innehållsöverföringsverktyget (CTT) utför ingen typ av innehållsanalys innan innehåll överförs från källinstansen till målinstansen. CTT skiljer till exempel inte mellan publicerat och opublicerat innehåll när innehåll hämtas till en publiceringsmiljö. Det innehåll som anges i migreringsuppsättningen hämtas till den valda målinstansen. Användaren kan importera en migreringsuppsättning till en Author-instans eller en Publish-instans eller både och. Vi rekommenderar att CTT installeras på källinstansen Author för att flytta innehåll till målinstansen Author när du flyttar innehåll till en Production-instans och att CTT på källinstansen av Publish installeras för att flytta innehåll till målpubliceringsinstansen. Se [Köra verktyget Innehållsöverföring på en publiceringsinstans](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html#running-tool) för mer information.

* De användare och grupper som överförs av verktyget Innehållsöverföring är bara de som krävs för att innehållet ska uppfylla behörigheterna. The _Extrahering_ processen kopierar hela `/home` i migreringsuppsättningen, och det gör användarmappning genom att lägga till ett fält som är gjort från varje användares e-postadress. Mer information finns i [Användarmappning och huvudmigrering](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/user-mapping-and-migration.md). The _Inmatning_ process kopierar alla användare och grupper som refereras i de migrerade innehålls-ACL:erna. Se [Migrerar stängda användargrupper](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/closed-user-groups-migration.md) om du vill ha mer information om grupper som används i en CUG-princip (Closed User Group).

* Under extraheringsfasen körs Content Transfer Tool på en aktiv AEM-källinstans.

* När du är klar med *Extrahering* fas i innehållsöverföringsprocessen och innan du påbörjar *Inmatningsfas* att lägga in innehåll i AEM as a Cloud Service *Scen* eller *Produktion* -instanser måste du logga en supportanmälan för att meddela Adobe om din avsikt att köra *Inmatning* så att Adobe kan säkerställa att inga avbrott inträffar under *Inmatning* -processen. Du måste logga supportbiljetten en vecka före ditt planerade *Inmatning* datum. När du har skickat in supportanmälan ger supportteamet vägledning om nästa steg. Du kan logga en supportanmälan med följande information:

   * Exakt datum och beräknad tid (med din tidszon) när du tänker starta *Inmatning* fas.
   * Miljötyp (Stage eller Production) som du vill importera data till.
   * Program-ID.

* The *Inmatningsfas* för författaren skalas ned för hela författardistributionen. Det innebär att författarens AEM inte är tillgängligt under hela importen. Se även till att inga rörledningar för Cloud Manager körs när du kör *Inmatning* fas.

* När du använder `Amazon S3` eller `Azure` som datalager i AEM bör datalagret konfigureras så att de lagrade blobblarna inte kan tas bort (skräpinsamlade). Detta garanterar indexdataintegritet och om detta inte konfigureras på det här sättet kan det leda till misslyckade extraheringar på grund av att dessa indexdata saknar integritet.

* Om du använder anpassade index måste du se till att konfigurera anpassade index med `tika` innan innehållsöverföringsverktyget körs. Se [Förbereder den nya indexdefinitionen](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html#preparing-the-new-index-definition) för mer information.

* Om du tänker göra toppuppsättningar är det viktigt att innehållsstrukturen i befintligt innehåll inte ändras från den tidpunkt då den första extraheringen utförs till den tidpunkt då den övre extraheringen körs. Det går inte att köra uppsättningar på innehåll vars struktur har ändrats sedan den första extraheringen. Kontrollera att du begränsar detta under migreringsprocessen.

* Om du tänker ta med versioner som en del av en migreringsuppsättning och utför uppsättningar med `wipe=false`måste du inaktivera versionsrensning på grund av en aktuell begränsning i verktyget Innehållsöverföring. Om du föredrar att behålla versionsrensning aktiverad och utför summeringar i en migreringsuppsättning, måste du utföra inmatningen som `wipe=true`.

* Ett migreringsset upphör att gälla efter en längre inaktivitetsperiod, efter vilken dess data inte längre är tillgängliga. Granska [Förfallotid för migreringsuppsättning](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html#migration-set-expiry) för mer information.

## What&#39;s Next {#whats-next}

När du har lärt dig riktlinjerna, de bästa metoderna och de viktiga sakerna att tänka på när du använder verktyget Innehållsöverföring är du nu redo att installera och använda verktyget, och börja med att skapa en migreringsuppsättning. Se [Komma igång med verktyget Innehållsöverföring](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/getting-started-content-transfer-tool.md) om du vill veta mer.

---
title: Riktlinjer och bästa praxis för användning av verktyget Innehållsöverföring (äldre)
description: Riktlinjer och bästa metoder för att använda verktyget Innehållsöverföring
hide: true
hidefromtoc: true
exl-id: 03449606-0fb4-4a9f-9abb-6b17c27a6046
source-git-commit: 3c8035e4db5729f58bae29136a32a0b9944d6a2f
workflow-type: tm+mt
source-wordcount: '1477'
ht-degree: 13%

---

# Riktlinjer och bästa praxis för användning av verktyget Innehållsöverföring (äldre) {#guidelines}

## Riktlinjer och bästa praxis {#best-practices}

Följ nedanstående avsnitt för att få information om riktlinjer och bästa praxis för att använda Content Transfer Tool:

* Kör [Revision Cleanup](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/revision-cleanup.html) och [konsekvenskontroll för datalager](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-16550.html?lang=en) på **källa** för att identifiera potentiella problem och minska storleken på databasen.

* Om CDN-konfigurationen (AEM Cloud Author Content Delivery Network) är konfigurerad att ha en tillåtelselista av IP-adresser kontrollerar du att även IP-adresserna för källmiljön läggs till i tillåtelselista. Detta säkerställer att källmiljön och AEM Cloud-miljön kan kommunicera med varandra.

* Kör intaget med *svepa* läge aktiveras där den befintliga databasen (författare eller publicerad) i AEM Cloud Service-målmiljön tas bort och sedan uppdateras med data för migreringsuppsättningen. Det här läget är mycket snabbare än non-wipe-läget, där migreringsuppsättningen tillämpas ovanpå det aktuella innehållet.

* När innehållsöverföringen har slutförts krävs rätt projektstruktur i Cloud Service-miljön så att innehållet återges korrekt i denna miljö.

* Innan du kör verktyget Content Transfer Tool måste du se till att det finns tillräckligt med diskutrymme i AEM-källinstansens underkatalog `crx-quickstart`. Det beror på att Content Transfer Tool skapar en lokal kopia av databasen som senare överförs till migreringsuppsättningen.
Den allmänna formeln för beräkning av ledigt diskutrymme är följande:
   `data store size + node store size * 1.5`

   * *databasens storlek*: Content Transfer Tool använder 64 GB, även om den faktiska databasen är större.
   * *noddatabasens storlek*: storlek på segmentdatabaskatalogen eller storlek på MongoDB-databasen.
För en segmentdatabasstorlek på 20 GB krävs därför 94 GB ledigt diskutrymme.

* En migreringsuppsättning måste finnas under hela innehållsöverföringsaktiviteten för att det ska gå att göra innehållsöverläggningar. Eftersom maximalt tio migreringsuppsättningar kan skapas och underhållas samtidigt under innehållsöverföringsaktiviteten bör innehållsdatabasen delas upp i enlighet med detta. Om du gör det ser du till att du inte får slut på migreringsuppsättningar.

## Viktigt att tänka på innan du använder verktyget Innehållsöverföring {#important-considerations}

Följ avsnittet nedan om du vill veta mer om viktiga aspekter när du använder Content Transfer Tool:

* Systemkraven för Content Transfer Tool är AEM 6.3 + och Java™ 8. Om du har en lägre AEM måste du uppgradera ditt innehållsarkiv till AEM 6.5 för att kunna använda verktyget för innehållsöverföring.

* Java™ måste vara konfigurerat i AEM-miljön så att `java` kommandot kan köras av den användare som startar AEM.

* Avinstallera tidigare versioner av verktyget Innehållsöverföring när du installerar version 1.3.0 eftersom det fanns en stor arkitektoniska förändring i verktyget. Med 1.3.0 bör du också skapa migreringsuppsättningar och köra extraheringen och intaget på nytt på de nya migreringsuppsättningarna.

* Verktyget Innehållsöverföring kan användas med följande typer av datalager: File Data Store, S3 Data Store, Shared S3 Data Store och Azure Blob Store Data Store.

* Om du använder en *Sandlådemiljö*, se till att din miljö är aktuell och uppgraderad till den senaste versionen. Om du använder en *produktionsmiljö* uppdateras den automatiskt.

* Om du vill använda verktyget Innehållsöverföring måste du vara en adminanvändare på källinstansen och tillhöra den lokala AEM **administratörer** i den Cloud Service som du överför innehåll till. Obehöriga användare kan inte hämta åtkomsttoken för att använda verktyget Innehållsöverföring.

* Om inställningen **Rensa befintligt innehåll i molninstansen före intag** om du aktiverar det här alternativet tas hela den befintliga databasen bort och en databas skapas där innehållet kan importeras till. Det här arbetsflödet innebär att alla inställningar återställs, inklusive behörigheter för målinstansen av Cloud Servicen. Detta gäller även för en admin-användare som läggs till i **administratörens** grupp. Användaren måste läsas till **administratörens** för att hämta åtkomsttoken för verktyget Innehållsöverföring.

* Verktyget Innehållsöverföring stöder inte sammanfogning av innehåll från flera källor till målkällinstansen om Cloud Servicen från de två källorna flyttas till samma sökvägar på målet. Om du vill flytta innehåll från flera olika källor till en enda instans av målsökvägen måste du se till att det inte finns någon överlappning mellan innehållssökvägarna från Cloud Servicen.

* Åtkomsttoken kan upphöra att gälla regelbundet antingen efter en viss tidsperiod eller efter att Cloud Servicens miljö har uppgraderats. Om åtkomsttoken har upphört att gälla kan du inte ansluta till Cloud Servicen. I så fall måste du hämta den nya åtkomsttoken. Statusikonen för en befintlig migreringsuppsättning ändras till ett rött moln och visar ett meddelande när du hovrar över den.

* Innehållsöverföringsverktyget (CTT) utför ingen typ av innehållsanalys innan innehåll överförs från källinstansen till målinstansen. CTT skiljer till exempel inte mellan publicerat och opublicerat innehåll när innehåll hämtas till en publiceringsmiljö. Det innehåll som anges i migreringsuppsättningen hämtas till den valda målinstansen. Användaren kan importera en migreringsuppsättning till en Author-instans eller en Publish-instans eller både och. När du flyttar innehåll till en Production-instans installerar du CTT på källförfattarinstansen för att flytta innehåll till målförfattarinstansen. Du kan även installera CTT på källinstansen Publish för att flytta innehåll till målinstansen Publish. Se [Köra verktyget Innehållsöverföring på en publiceringsinstans](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=en#running-tool) för mer information.

* De användare och grupper som överförs av verktyget Innehållsöverföring är bara de som krävs för att innehållet ska uppfylla behörigheterna. The *Extrahering* processen kopierar hela `/home` till migreringsuppsättningen och *Inmatning* process kopierar alla användare och grupper som refereras i de migrerade innehålls-ACL:erna. Om du vill mappa befintliga användare och grupper automatiskt till deras IMS-ID:n läser du [Använda verktyget för användarmappning](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/legacy-user-mapping-tool/using-user-mapping-tool-legacy.html?lang=en).

* Under extraheringsfasen körs Content Transfer Tool på en aktiv AEM-källinstans.

* När du är klar med *Extrahering* fas i innehållsöverföringsprocessen och innan du påbörjar *Inmatningsfas* att lägga in innehåll i AEM as a Cloud Service *Scen* eller *Produktion* instanser loggar du en supportanmälan. Meddela Adobe om din avsikt att springa *Inmatning* så att Adobe kan säkerställa att inga avbrott inträffar under *Inmatning* -processen. Logga supportanmälan en vecka före ditt planerade *Inmatning* datum. När du har skickat in supportanmälan ger supportteamet vägledning om nästa steg. Logga en supportanmälan med följande information:

   * Exakt datum och beräknad tid (med din tidszon) när du tänker starta *Inmatning* fas.
   * Miljötyp (Stage eller Production) som du vill importera data till.
   * Program-ID.

* The *Inmatningsfas* för författaren skalas ned för hela författardistributionen. Detta innebär att författarens AEM inte är tillgänglig under hela importen. Kontrollera också att inga rörledningar för Cloud Manager körs när du kör *Inmatning* fas.

* När du använder `Amazon S3` eller `Azure` som datalager i AEM bör datalagret konfigureras så att de lagrade blobblarna inte kan tas bort (skräpinsamlade). Detta garanterar indexdataintegritet och om detta inte konfigureras på det här sättet kan det leda till misslyckade extraheringar på grund av att dessa indexdata saknar integritet.

* Om du använder anpassade index måste du se till att konfigurera anpassade index med `tika` innan innehållsöverföringsverktyget körs. Se [Förbereder den nya indexdefinitionen](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/indexing.html?lang=en#preparing-the-new-index-definition) för mer information.

* Om du tänker göra toppuppsättningar ska du se till att innehållsstrukturen i det befintliga innehållet inte ändras från den tidpunkt då den första extraheringen görs till den tidpunkt då extraheringen av den översta körs. De översta fotona kan inte köras på innehåll vars struktur har ändrats sedan den första extraheringen. Kontrollera att du begränsar detta under migreringsprocessen.

* Om du tänker ta med versioner som en del av en migreringsuppsättning och utför uppsättningar med `wipe=false`måste du inaktivera versionsrensning på grund av en aktuell begränsning i verktyget Innehållsöverföring. Om du föredrar att behålla versionsrensning aktiverad och utför summeringar i en migreringsuppsättning, måste du utföra inmatningen som `wipe=true`.

## What&#39;s Next {#whats-next}

När du har lärt dig riktlinjerna, de bästa metoderna och de viktiga sakerna att tänka på när du använder verktyget Innehållsöverföring är du nu redo att installera och använda verktyget, och börja med att skapa en migreringsuppsättning. Se [Komma igång med verktyget Innehållsöverföring](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=en) om du vill veta mer.

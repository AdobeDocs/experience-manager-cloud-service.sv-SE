---
title: Riktlinjer och bästa metoder för att använda verktyget Innehållsöverföring
description: Riktlinjer och bästa metoder för att använda verktyget Innehållsöverföring
exl-id: d1975c34-85d4-42e0-bb1a-968bdb3bf85d
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '1503'
ht-degree: 25%

---

# Riktlinjer och bästa metoder för att använda verktyget Innehållsöverföring {#guidelines}

## Riktlinjer och bästa praxis {#best-practices}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_guidelines"
>title="Riktlinjer och bästa praxis"
>abstract="Granska riktlinjer och metodtips om hur du använder verktyget Innehållsöverföring, t.ex. när det gäller att rensa bort ändringar, diskutrymme med mera."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#pre-reqs" text="Viktigt att tänka på när du använder verktyget Innehållsöverföring"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#important-considerations" text="Viktigt att tänka på när du använder verktyget för användarmappning"

Följ nedanstående avsnitt för att få information om riktlinjer och bästa praxis för att använda Content Transfer Tool:

* Du bör köra [Revision Cleanup](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/revision-cleanup.html) och [databasens konsekvenskontroller](https://helpx.adobe.com/experience-manager/kb/How-to-run-a-datastore-consistency-check-via-oak-run-AEM.html) på **källdatabasen** för att identifiera potentiella problem och minska databasens storlek.

* Om konfigurationen för AEM Cloud Author Content Delivery Network (CDN) har en vitlista över IP-adresser måste du se till att IP-adresserna för källmiljön läggs till i den tillåtna listan så att källmiljön och AEM Cloud-miljön kan kommunicera med varandra.

* I inmatningsfasen rekommenderas att du kör inmatningen med *wipe*-läget aktiverat där den befintliga databasen (Author eller Publish) i AEM Cloud Service-miljön tas bort helt och sedan uppdateras med migreringsuppsättningsdata. Det här läget är mycket snabbare än non-wipe-läget, där migreringsuppsättningen tillämpas ovanpå det aktuella innehållet.

* När innehållsöverföringen har slutförts krävs rätt projektstruktur i Cloud Service-miljön så att innehållet återges korrekt i denna miljö.

* Innan du kör verktyget Content Transfer Tool måste du se till att det finns tillräckligt med diskutrymme i AEM-källinstansens underkatalog `crx-quickstart`. Det beror på att Content Transfer Tool skapar en lokal kopia av databasen som senare överförs till migreringsuppsättningen.
Den allmänna formeln för att beräkna hur mycket ledigt diskutrymme som krävs är följande:
   `data store size + node store size * 1.5`

   * *databasens storlek*: Content Transfer Tool använder 64 GB, även om den faktiska databasen är större.
   * *noddatabasens storlek*: storlek på segmentdatabaskatalogen eller storlek på MongoDB-databasen.
För en segmentdatabasstorlek på 20 GB krävs därför 94 GB ledigt diskutrymme.

* En migreringsuppsättning måste bibehållas under hela innehållsöverföringsaktiviteten för att kunna stödja innehållsöverläggningar. Eftersom maximalt tio migreringsuppsättningar kan skapas och underhållas samtidigt under innehållsöverföringsaktiviteten bör du dela upp innehållsdatabasen i enlighet med detta för att se till att du inte får slut på migreringsuppsättningar.

## Viktigt att tänka på innan du använder verktyget Innehållsöverföring {#important-considerations}

Följ avsnittet nedan om du vill veta mer om viktiga aspekter när du använder Content Transfer Tool:

* Lägsta systemkrav för Content Transfer Tool är AEM 6.3 + och JAVA 8. Om du har en lägre AEM måste du uppgradera ditt innehållsarkiv till AEM 6.5 för att kunna använda verktyget för innehållsöverföring.

* Java måste konfigureras i AEM-miljön så att `java` kommandot kan köras av den användare som startar AEM.

* Vi rekommenderar att du avinstallerar äldre versioner av verktyget Innehållsöverföring när du installerar version 1.3.0 eftersom det har skett en stor förändring i arkitekturen i verktyget. Med 1.3.0 bör du också skapa nya migreringsuppsättningar och köra extrahering och förtäring på nytt för de nya migreringsuppsättningarna.

* Verktyget Innehållsöverföring kan användas med följande typer av datalager: File Data Store, S3 Data Store, Shared S3 Data Store och Azure Blob Store Data Store.

* Om du använder en *Sandlådemiljö*, se till att din miljö är aktuell och uppgraderad till den senaste versionen. Om du använder en *produktionsmiljö* uppdateras den automatiskt.

* Om du vill använda verktyget Innehållsöverföring måste du vara en adminanvändare på källinstansen och tillhöra den lokala AEM **administratörer** i den Cloud Service som du överför innehåll till. Obehöriga användare kan inte hämta åtkomsttoken för att använda Content Transfer Tool.

* Om inställningen **Rensa befintligt innehåll i molninstansen före intag** om du aktiverar det här alternativet tas hela den befintliga databasen bort och en ny databas skapas där innehållet kan importeras till. Det innebär att alla inställningar återställs, inklusive behörigheter för målinstansen av Cloud Servicen. Detta gäller även för en admin-användare som har lagts till i **administratörer** grupp. Användaren måste läggas till på nytt i **administratörer** grupp för att hämta åtkomsttoken för CTT.

* Åtkomsttoken kan upphöra att gälla regelbundet antingen efter en viss tidsperiod eller efter att Cloud Servicens miljö har uppgraderats. Om åtkomsttoken har upphört att gälla kan du inte ansluta till Cloud Servicen och du måste hämta den nya åtkomsttoken. Statusikonen som är kopplad till en befintlig migreringsuppsättning ändras till ett rött moln och ett meddelande visas när du hovrar över den.

* Innehållsöverföringsverktyget (CTT) utför ingen typ av innehållsanalys innan innehåll överförs från källinstansen till målinstansen. CTT skiljer till exempel inte mellan publicerat och opublicerat innehåll när innehåll hämtas till en publiceringsmiljö. Det innehåll som anges i migreringsuppsättningen hämtas till den valda målinstansen. Användaren kan importera en migreringsuppsättning till en Author-instans eller en Publish-instans eller både och. Vi rekommenderar att CTT installeras på källinstansen Author för att flytta innehåll till målinstansen Author när du flyttar innehåll till en Production-instans och att CTT på källinstansen av Publish installeras för att flytta innehåll till målpubliceringsinstansen. Se [Köra verktyget Innehållsöverföring på en publiceringsinstans](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#running-ctt-on-publish) för mer information.

* De användare och grupper som överförs av verktyget Innehållsöverföring är bara de som krävs för att innehållet ska uppfylla behörigheterna. The *Extrahering* processen kopierar hela `/home` till migreringsuppsättningen och *Inmatning* process kopierar alla användare och grupper som refereras i de migrerade innehålls-ACL:erna. Om du vill mappa befintliga användare och grupper automatiskt till deras IMS-ID:n läser du [Använda verktyget för användarmappning](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#cloud-migration).

* Under extraheringsfasen körs Content Transfer Tool på en aktiv AEM-källinstans.

* När du är klar med *Extrahering* fas i innehållsöverföringsprocessen och innan du påbörjar *Inmatningsfas* att lägga in innehåll i AEM as a Cloud Service *Scen* eller *Produktion* -instanser måste du logga en supportanmälan för att meddela Adobe om din avsikt att köra *Inmatning* så att Adobe kan säkerställa att inga avbrott inträffar under *Inmatning* -processen. Du måste logga supportbiljetten en vecka före ditt planerade *Inmatning* datum. När du har skickat in supportanmälan kommer supportteamet att ge vägledning om nästa steg. Du kan logga en supportanmälan med följande information:

   * Exakt datum och beräknad tid (med din tidszon) när du tänker starta *Inmatning* fas.
   * Miljötyp (Stage eller Production) som du vill importera data till.
   * Program-ID.

* The *Inmatningsfas* för författaren skalas ned för hela författardistributionen. Detta innebär att författar-AEM inte är tillgängligt under hela importen. Kontrollera också att inga rörledningar för Cloud Manager körs när du kör *Inmatning* fas.

* När du använder `Amazon S3` eller `Azure` som datalager i AEM bör datalagret konfigureras så att de lagrade blobblarna inte kan tas bort (skräpinsamlade). Detta garanterar indexdataintegritet och om detta inte konfigureras på det här sättet kan det leda till misslyckade extraheringar på grund av att dessa indexdata saknar integritet.

* Om du använder anpassade index måste du se till att konfigurera anpassade index med `tika` innan innehållsöverföringsverktyget körs. Se [Förbereder den nya indexdefinitionen](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=en#preparing-the-new-index-definition) för mer information.

* Om du tänker göra toppuppsättningar är det viktigt att innehållsstrukturen i befintligt innehåll inte ändras från den tidpunkt då den första extraheringen utförs till den tidpunkt då den övre extraheringen körs. Det går inte att köra uppsättningar på innehåll vars struktur har ändrats sedan den första extraheringen. Kontrollera att du begränsar detta under migreringsprocessen.

* Om du tänker ta med versioner som en del av en migreringsuppsättning och utför uppsättningar med `wipe=false`måste du inaktivera versionsrensning på grund av en aktuell begränsning i verktyget Innehållsöverföring. Om du föredrar att behålla versionsrensning aktiverad och utför summeringar i en migreringsuppsättning, måste du utföra inmatningen som `wipe=true`.

## What&#39;s Next {#whats-next}

När du har lärt dig riktlinjerna, de bästa metoderna och de viktiga sakerna att tänka på när du använder verktyget Innehållsöverföring är du nu redo att installera och använda verktyget, och börja med att skapa en migreringsuppsättning. Se [Komma igång med verktyget Innehållsöverföring](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=en) om du vill veta mer.

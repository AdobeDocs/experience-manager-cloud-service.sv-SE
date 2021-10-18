---
title: Riktlinjer och bästa metoder för att använda verktyget Innehållsöverföring
description: Riktlinjer och bästa metoder för att använda verktyget Innehållsöverföring
source-git-commit: fa7e5d07ed52a71999de95bbf6299ae5eb7af537
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

* En migreringsuppsättning måste bibehållas under hela innehållsöverföringsaktiviteten för att kunna stödja innehållsöverläggningar. Since a maximum of ten migration sets can be created and maintained at a time during the content transfer activity, it is recommended to break up the content repository accordingly to ensure that you do not run out of migration sets.

## Viktigt att tänka på innan du använder verktyget Innehållsöverföring {#important-considerations}

Följ avsnittet nedan om du vill veta mer om viktiga aspekter när du använder Content Transfer Tool:

* Lägsta systemkrav för Content Transfer Tool är AEM 6.3 + och JAVA 8. If you are on a lower AEM version, you need to upgrade your content repository to AEM 6.5 to use the Content Transfer Tool.

* Java måste vara konfigurerat i AEM så att kommandot `java` kan köras av den användare som startar AEM.

* Vi rekommenderar att du avinstallerar äldre versioner av verktyget Innehållsöverföring när du installerar version 1.3.0 eftersom det har skett en stor förändring i arkitekturen i verktyget. Med 1.3.0 bör du också skapa nya migreringsuppsättningar och köra extrahering och förtäring på nytt för de nya migreringsuppsättningarna.

* Verktyget Innehållsöverföring kan användas med följande typer av datalager: File Data Store, S3 Data Store, Shared S3 Data Store och Azure Blob Store Data Store.

* Om du använder en *sandlådemiljö* kontrollerar du att miljön är aktuell och uppgraderad till den senaste versionen. Om du använder en *produktionsmiljö* uppdateras den automatiskt.

* Om du vill använda verktyget Innehållsöverföring måste du vara en adminanvändare i källinstansen och tillhöra den lokala gruppen **administratörer** i den Cloud Service du överför innehåll till. Obehöriga användare kan inte hämta åtkomsttoken för att använda Content Transfer Tool.

* Om inställningen **Rensa befintligt innehåll i molninstansen innan du använder**, tas hela den befintliga databasen bort och en ny databas skapas för att importera innehåll till. This means that it resets all settings including permissions on the target Cloud Service instance. Detta gäller även för en admin-användare som har lagts till i gruppen **administratörer**. Användaren måste läggas till på nytt i gruppen **administratörer** för att hämta åtkomsttoken för CTT.

* Åtkomsttoken kan upphöra att gälla regelbundet antingen efter en viss tidsperiod eller efter att Cloud Servicens miljö har uppgraderats. Om åtkomsttoken har upphört att gälla kan du inte ansluta till Cloud Servicen och du måste hämta den nya åtkomsttoken. Statusikonen som är kopplad till en befintlig migreringsuppsättning ändras till ett rött moln och ett meddelande visas när du hovrar över den.

* Innehållsöverföringsverktyget (CTT) utför ingen typ av innehållsanalys innan innehåll överförs från källinstansen till målinstansen. CTT skiljer till exempel inte mellan publicerat och opublicerat innehåll när innehåll hämtas till en publiceringsmiljö. Whatever content is specified in the migration set will be ingested into the chosen target instance. Användaren kan importera en migreringsuppsättning till en Author-instans eller en Publish-instans eller både och. Vi rekommenderar att CTT installeras på källinstansen Author för att flytta innehåll till målinstansen Author när du flyttar innehåll till en Production-instans och att CTT på källinstansen av Publish installeras för att flytta innehåll till målpubliceringsinstansen. Refer to [Running the Content Transfer Tool on a Publish instance](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#running-ctt-on-publish) for more details.

* De användare och grupper som överförs av verktyget Innehållsöverföring är bara de som krävs för att innehållet ska uppfylla behörigheterna. Processen *Extrahering* kopierar hela `/home` till migreringsuppsättningen och processen *Ing* kopierar alla användare och grupper som refereras i de migrerade innehålls-ACL:erna. To automatically map the existing users and groups to their IMS IDs, please refer to [Using User Mapping Tool](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#cloud-migration).

* Under extraheringsfasen körs Content Transfer Tool på en aktiv AEM-källinstans.

* After completing the *Extraction* phase of the content transfer process and before starting the *Ingestion Phase* to ingest content into your AEM as a Cloud Service *Stage* or *Production* instances, you will need to log a support ticket to notify Adobe of your intention to run *Ingestion* so that Adobe can ensure that no interruptions occur during the *Ingestion* process. Du måste logga supportbiljetten en vecka före ditt planerade *intag*-datum. När du har skickat in supportanmälan kommer supportteamet att ge vägledning om nästa steg. Du kan logga en supportanmälan med följande information:

   * Exakt datum och beräknad tid (med din tidszon) när du tänker starta fasen *Inmatning*.
   * Miljötyp (Stage eller Production) som du vill importera data till.
   * Program-ID.

* *Inmatningsfasen* för författaren skalas ned för hela författardistributionen. Detta innebär att författar-AEM inte är tillgängligt under hela importen. Se även till att inga rörledningar för Cloud Manager körs när du kör fasen *Inmatning*.

* När du använder `Amazon S3` eller `Azure` som datalager i AEM, bör datalagret konfigureras så att de lagrade blobbarna inte kan tas bort (skräpsamling). Detta garanterar indexdataintegritet och om detta inte konfigureras på det här sättet kan det leda till misslyckade extraheringar på grund av att dessa indexdata saknar integritet.

* Om du använder anpassade index måste du se till att konfigurera anpassade index med noden `tika` innan du kör verktyget Innehållsöverföring. Mer information finns i [Förbereda den nya indexdefinitionen](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=en#preparing-the-new-index-definition).

* Om du tänker göra toppuppsättningar är det viktigt att innehållsstrukturen i befintligt innehåll inte ändras från den tidpunkt då den första extraheringen utförs till den tidpunkt då den övre extraheringen körs. Det går inte att köra uppsättningar på innehåll vars struktur har ändrats sedan den första extraheringen. Please ensure you restrict this during the migration process.

* Om du tänker ta med versioner som en del av en migreringsuppsättning och utför uppsättningar med `wipe=false`, måste du inaktivera versionsrensning på grund av en aktuell begränsning i verktyget Innehållsöverföring. If you prefer to keep version purge enabled and are performing top-ups into a migration set, then you must perform the ingestion as `wipe=true`.

## What&#39;s Next {#whats-next}

När du har lärt dig riktlinjerna, de bästa metoderna och de viktiga sakerna att tänka på när du använder verktyget Innehållsöverföring är du nu redo att installera och använda verktyget, och börja med att skapa en migreringsuppsättning. Mer information finns i [Komma igång med verktyget Innehållsöverföring](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=en).

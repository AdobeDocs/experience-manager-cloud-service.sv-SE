---
title: Använda Content Transfer Tool
description: Använda Content Transfer Tool
exl-id: a19b8424-33ab-488a-91b3-47f0d3c8abf5
translation-type: tm+mt
source-git-commit: 7bdf8f1e6d8ef1f37663434e7b14798aeb8883f4
workflow-type: tm+mt
source-wordcount: '2685'
ht-degree: 47%

---

# Använda Content Transfer Tool {#using-content-transfer-tool}

## Viktigt att tänka på när du använder Content Transfer Tool {#pre-reqs}

>id=&quot;aemcloud_ctt_prereqs&quot;
>title=&quot;Viktigt att tänka på vid användning av verktyget Innehållsöverföring&quot;
>abstract=&quot;Granska viktiga aspekter av att använda verktyget för innehållsöverföring, inklusive Java- och AEM-versioner, datastortyper som stöds, användargruppöverväganden med mera.&quot;
>additional-url=&quot;https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang=en#best-practices&quot; text=&quot;Best Practices and Guidelines&quot;
>additional-url=&quot;https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#availability&quot; text=&quot;Download Content Transfer Tool&quot;

Följ avsnittet nedan om du vill veta mer om viktiga aspekter när du använder Content Transfer Tool:

* Lägsta systemkrav för Content Transfer Tool är AEM 6.3 + och JAVA 8. Om du har en tidigare AEM-version måste du uppgradera din innehållsdatabas till AEM 6.5 för att kunna använda Content Transfer Tool.

* Java måste konfigureras i AEM så att kommandot `java` kan köras av den användare som startar AEM.

* Vi rekommenderar att du avinstallerar äldre versioner av verktyget Innehållsöverföring när du installerar version 1.3.0 eftersom det har skett en stor förändring i arkitekturen i verktyget. Med 1.3.0 bör du också skapa nya migreringsuppsättningar och köra extrahering och förtäring på nytt för de nya migreringsuppsättningarna.

* Verktyget Innehållsöverföring kan användas med följande typer av datalager: File Data Store, S3 Data Store, Shared S3 Data Store och Azure Blob Store Data Store.

* Om du använder en *sandlådemiljö* kontrollerar du att miljön är aktuell och uppgraderad till den senaste versionen. Om du använder en *produktionsmiljö* uppdateras den automatiskt.

* Om du vill använda verktyget Innehållsöverföring måste du vara en adminanvändare i källinstansen och tillhöra den lokala gruppen **administratörer** i den Cloud Service du överför innehåll till. Obehöriga användare kan inte hämta åtkomsttoken för att använda Content Transfer Tool.

* Om inställningen **Rensa befintligt innehåll i molninstansen innan du använder**, tas hela den befintliga databasen bort och en ny databas skapas för att importera innehåll till. Det innebär att alla inställningar återställs, inklusive behörigheter för målinstansen av Cloud Servicen. Detta gäller även för en admin-användare som har lagts till i gruppen **administratörer**. Användaren måste läggas till på nytt i gruppen **administratörer** för att hämta åtkomsttoken för CTT.

* Åtkomsttoken kan upphöra att gälla regelbundet antingen efter en viss tidsperiod eller efter att Cloud Servicens miljö har uppgraderats. Om åtkomsttoken har upphört att gälla kan du inte ansluta till Cloud Servicen och du måste hämta den nya åtkomsttoken. Statusikonen som är kopplad till en befintlig migreringsuppsättning ändras till ett rött moln och ett meddelande visas när du hovrar över den.

* Innehållsöverföringsverktyget utför ingen typ av innehållsanalys innan innehåll överförs från källinstansen till målinstansen. CTT skiljer t.ex. inte mellan publicerat och opublicerat innehåll när innehållet hämtas till en publiceringsmiljö. Det innehåll som anges i migreringsuppsättningen hämtas till den valda målinstansen. Användaren kan importera en migreringsuppsättning till en Author-instans eller en Publish-instans eller både och. Vi rekommenderar att CTT installeras som källförfattarinstans när innehåll flyttas till målförfattarinstansen och att CTT installeras på källpubliceringsinstansen för att flytta innehållet till målpubliceringsinstansen. På liknande sätt installeras CTT på källpubliceringsinstansen för att flytta innehållet till målpubliceringsinstansen.

* De användare och grupper som överförs av verktyget Innehållsöverföring är bara de som krävs för att innehållet ska uppfylla behörigheterna. Processen *Extrahering* kopierar hela `/home` till migreringsuppsättningen och processen *Ing* kopierar alla användare och grupper som refereras i de migrerade innehålls-ACL:erna. Om du vill mappa befintliga användare och grupper automatiskt till deras IMS-ID:n läser du [Använda verktyget för användarmappning](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#cloud-migration).

* Under extraheringsfasen körs Content Transfer Tool på en aktiv AEM-källinstans.

* När du har slutfört *extraheringsfasen* av innehållsöverföringsprocessen och innan du startar *överföringsfasen* för att importera innehåll till din AEM som en Cloud Service *Stage* eller *Produktion*-instanser måste du logga en supportanmälan för att meddela Adobe om din avsikt att köra *Input överbelastning* så att Adobe kan säkerställa att inga avbrott inträffar under *Inmatningsprocessen*. Du måste logga supportbiljetten en vecka före ditt planerade *intag*-datum. När du har skickat in supportanmälan kommer supportteamet att ge vägledning om nästa steg.
   * Logga en supportanmälan med följande information:
      * Exakt datum och beräknad tid (med din tidszon) när du tänker starta fasen *Inmatning*.
      * Miljötyp (Stage eller Production) som du vill importera data till.
      * Program-ID.

* Författarens *inmatningsfas* kommer att skalas ned för hela författardriftsättningen. Detta innebär att författar-AEM inte är tillgängligt under hela importen. Se även till att inga rörledningar för Cloud Manager körs när du kör fasen *Inmatning*.


## Tillgänglighet {#availability}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_download"
>title="Hämta"
>abstract="Innehållsöverföringsverktyget kan laddas ned som en zip-fil från Software Distribution Portal. Du kan installera paketet via pakethanteraren på din källinstans av Adobe Experience Manager (AEM). Glöm inte att hämta den senaste versionen."
>additional-url="https://docs.adobe.com/content/help/en/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html" text="Versionsinformation"
>additional-url="https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html" text="Programdistributionsportal"

Innehållsöverföringsverktyget kan laddas ned som en zip-fil från Software Distribution Portal. Du kan installera paketet via pakethanteraren på din källinstans av Adobe Experience Manager (AEM). Glöm inte att hämta den senaste versionen. Mer information om den senaste versionen finns i [Versionsinformation](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html).

>[!NOTE]
>Hämta Content Transfer Tool från [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)-portalen.

## Köra Content Transfer Tool {#running-tool}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_demo"
>title="Verktyget Innehållsöverföring körs"
>abstract="Lär dig hur du använder verktyget Innehållsöverföring för att migrera innehållet till AEM som en Cloud Service (Författare/Publicera)."
>additional-url="https://video.tv.adobe.com/v/35460/?quality=12&amp;learn=on" text=" Se demo"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/migration/content-transfer-tool.html?lang=en#migration" text="Självstudiekurs - använda verktyget Innehållsöverföring"

>[!VIDEO](https://video.tv.adobe.com/v/35460/?quality=12&learn=on)


Följ det här avsnittet för att lära dig hur du använder Content Transfer Tool för att migrera innehållet till AEM as a Cloud Service (Author/Publish):

1. Markera Adobe Experience Manager och navigera till verktyg -> **Åtgärder** -> **Innehållsmigrering**.

   ![bild](/help/move-to-cloud-service/content-transfer-tool/assets/ctt-entry-card01.png)

1. Välj alternativet **Innehållsöverföring** i guiden **Innehållsmigrering**.

   ![bild](/help/move-to-cloud-service/content-transfer-tool/assets/ctt-entry-card02.png)


1. Konsolen nedan visas när du skapar den första migreringsuppsättningen. Klicka på **Create Migration Set** om du vill skapa en ny migreringsuppsättning.

   ![bild](/help/move-to-cloud-service/content-transfer-tool/assets/01-create-migrationset.png)


   >[!NOTE]
   >Om du har befintliga migreringsuppsättningar visas en lista med befintliga migreringsuppsättningar med aktuell status.

   Klicka på **Skapa konfiguration för användarmappning** för att komma åt [verktyget för användarmappning](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#using-user-mapping-tool).

1. Fyll i fälten på **skärmen Skapa migreringsuppsättning** enligt beskrivningen nedan.

   ![bild](/help/move-to-cloud-service/content-transfer-tool/assets/migration-set-creation-04.png)

   1. **Name**: Ange namnet på migreringsuppsättningen.
      >[!NOTE]
      >Inga specialtecken tillåts för migreringsuppsättningens namn.

   1. **Cloud Service Configuration**: Ange målförfattar-URL för AEM as a Cloud Service.

      >[!NOTE]
      >Du kan skapa och underhålla högst fyra migreringsuppsättningar åt gången under innehållsöverföringen.
      >Dessutom måste du skapa en migrering separat för varje specifik miljö – *Stage*, *Development* eller *Production*.

   1. **Access Token**: Ange åtkomsttoken.

      >[!NOTE]
      >Du kan hämta åtkomsttoken med knappen **Öppna åtkomsttoken**. Du måste kontrollera att du tillhör gruppen AEM administratörer i målinstansen av Cloud Service.

   1. **Parameters**: Välj följande parametrar för att skapa migreringsuppsättningen:

      1. **Include Version**: Välj det som behövs.

      1. **Inkludera mappning från IMS-användare och -grupper**: Välj alternativet att inkludera mappning från IMS-användare och -grupper.
Mer information finns i [Användarmappningsverktyget](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html).

      1. **Paths to be included**: Använd sökvägsläsaren för att välja sökvägar som behöver migreras. Banväljaren accepterar indata genom att skriva eller genom att välja.

         >[!IMPORTANT]
         >Följande sökvägar är begränsade när du skapar en migreringsuppsättning:
         >* `/apps`
         >* `/libs`
         >* `/home`
         >* `/etc` (vissa  `/etc` banor kan markeras i CTT)


1. Klicka på **Spara** när du har fyllt i alla fält i **informationsskärmen för Skapa migreringsuppsättning**.

1. Migreringsuppsättningen visas på sidan *Overview*.

   ![bild](/help/move-to-cloud-service/content-transfer-tool/assets/04-item-selection-and-quick-actions.png)

   Alla befintliga migreringsuppsättningar på den här skärmen visas på sidan *Overview* med aktuell status och statusinformation. Du kan se några av dessa ikoner som beskrivs nedan.

   * Ett *rött moln* anger att du inte kan slutföra extraheringsprocessen.
   * Ett *grönt moln* anger att du kan slutföra extraheringsprocessen.
   * En *gul ikon* anger att du inte har skapat den befintliga migreringsuppsättningen och att den specifika skapas av en annan användare i samma instans.

1. Välj en migreringsuppsättning från översiktssidan och klicka på **Properties** för att visa eller redigera migreringsuppsättningens egenskaper. När du redigerar egenskaper går det inte att ändra behållarnamnet eller tjänst-URL:en.


### Extraheringsprocess i innehållsöverföring {#extraction-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_extraction"
>title="Innehållsextrahering"
>abstract="Extrahering avser att extrahera innehåll från AEM till ett temporärt område som kallas migreringsuppsättning. En migreringsuppsättning är ett molnlagringsutrymme som finns hos Adobe för att tillfälligt lagra det överförda innehållet mellan AEM-källinstansen och Cloud Service AEM-instansen."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#ingestion-process" text="Inmatningsprocess"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#top-up-extraction-process" text="Extrahering uppifrån"

Följ stegen nedan för att extrahera migreringsuppsättningen från Content Transfer Tool:

1. Välj en migreringsuppsättning på sidan *Overview* och klicka på **Extract** för att påbörja extraheringen. Dialogrutan **Extrahering av migreringsuppsättning** visas och klicka på **Extract** för att starta extraheringsfasen.

   ![bild](/help/move-to-cloud-service/content-transfer-tool/assets/06-content-extraction.png)

   >[!NOTE]
   >Du kan skriva över mellanlagringsbehållaren under extraheringsfasen.


1. Fältet **EXTRACTION** visar nu statusen **RUNNING** för att ange att extraheringen pågår.

   ![bild](/help/move-to-cloud-service/content-transfer-tool/assets/07-extraction-job-running.png)

   När extraheringen är klar uppdateras migreringsuppsättningens status till **FINISHED** och en *solid grön* molnikon visas under **INFO**-fältet.

   ![bild](/help/move-to-cloud-service/content-transfer-tool/assets/10-extraction-complete.png)

   >[!NOTE]
   >Gränssnittet har en automatisk inläsningsfunktion som laddar om översiktssidan var 30:e sekund.
   >När extraheringsfasen startas skapas ett skrivlås som frisläpps efter *60 sekunder*. Om extraheringen avbryts måste du alltså vänta en minut på att låset ska frisläppas innan du startar extraheringen igen.

#### Uppdateringsextrahering {#top-up-extraction-process}

Content Transfer Tool har en funktion för differentiell innehållsuppdatering som gör att du kan överföra enbart de ändringar som gjorts sedan den föregående innehållsöverföringen.

>[!NOTE]
>Efter den första innehållsöverföringen bör du göra regelbundna tillägg av differentiellt innehåll för att förkorta innehållets frysningsperiod för den slutliga differentiella innehållsöverföringen innan du börjar använda Cloud Service.

När extraheringen är klar kan du överföra delta-innehåll med extraheringsmetoden för uppdateringar. Följ stegen nedan:

1. Gå till sidan *Overview* och välj den migreringsuppsättning som du vill utföra ändringsextraheringen för. Klicka på **Extract** för att starta uppdateringsextraheringen. Dialogrutan **Migration Set extraction** visas.

   >[!IMPORTANT]
   >
   >Du bör inaktivera alternativet **Overwrite staging container during extraction**.
   >
   >![bild](/help/move-to-cloud-service/content-transfer-tool/assets/11-topup-extraction.png)

### Inmatningsprocess i innehållsöverföring {#ingestion-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion"
>title="Innehållsintag"
>abstract="Inmatningen hänvisar till inmatning av innehåll från *migreringsuppsättningen* till målinstansen för Cloud Service. Content Transfer Tool har en funktion för differentiell innehållsuppdatering som gör att du kan överföra enbart de ändringar som gjorts sedan den föregående innehållsöverföringen."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#extraction-process" text="Extraheringsprocess"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#top-up-ingestion-process" text="Uppdatera inmatning"

Följ stegen nedan för att importera migreringsuppsättningen från Content Transfer Tool:

1. Välj en migreringsuppsättning på sidan *Overview* och klicka på **Ingest** för att påbörja extraheringen. Dialogrutan **Migration Set ingestion** visas. Klicka på **Ingest** för att starta intagningsfasen. Det går att importera innehåll till Author och Publish samtidigt.

   >[!IMPORTANT]
   >När alternativet **Rensa befintligt innehåll i molninstansen innan inmatning** är aktiverat, tas hela den befintliga databasen bort och en ny databas skapas för inmatning av innehåll i. Det innebär att alla inställningar återställs, inklusive behörigheter för målinstansen av Cloud Servicen. Detta gäller även för en admin-användare som har lagts till i gruppen **administratörer**.

   ![bild](/help/move-to-cloud-service/content-transfer-tool/assets/content-ingestion-01.png)

   Klicka på **Kundtjänst** för att logga en biljett, vilket visas i bilden ovan. Se även [Viktiga överväganden för att använda verktyget Innehållsöverföring](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#pre-reqs) om du vill veta mer.

1. När importen är klar uppdateras statusen i **PUBLISH INGESTION**-fältet till **FINISHED**.

   ![bild](/help/move-to-cloud-service/content-transfer-tool/assets/15-ingestion-complete.png)

#### Uppdatera inmatning {#top-up-ingestion-process}

Content Transfer Tool har en funktion för differentiell *innehållsuppdatering* som gör att du kan överföra enbart de ändringar som gjorts sedan den föregående innehållsöverföringen.

>[!NOTE]
>
>Efter den första innehållsöverföringen bör du göra regelbundna tillägg av differentiellt innehåll för att förkorta innehållets frysningsperiod för den slutliga differentiella innehållsöverföringen innan du börjar använda Cloud Service.

När inmatningen är klar kan du använda delta-innehåll med hjälp av inmatningsmetoden för uppdateringar. Följ stegen nedan:

1. Navigera till sidan *Overview* och välj den migreringsuppsättning som du vill utföra uppdateringsinmatningen för. Klicka på **Ingest** för att starta uppdateringsextraheringen. Dialogrutan **Migration Set ingestion** visas.

   ![bild](/help/move-to-cloud-service/content-transfer-tool/assets/content-ingestion-01.png)

   >[!IMPORTANT]
   >Du bör inaktivera alternativet **Rensa befintligt innehåll i molninstansen före intag**, för att förhindra att befintligt innehåll tas bort från den tidigare intagsaktiviteten. Klicka på **Kundtjänst** för att logga en biljett, vilket visas i föregående bild.


### Visa loggar för en migreringsuppsättning {#viewing-logs-migration-set}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_logs"
>title="Visa loggar"
>abstract="När extraheringen av intag har slutförts bör du kontrollera om det finns några fel eller varningar i loggarna. Felen bör åtgärdas omedelbart, antingen genom att man hanterar de rapporterade problemen eller genom att man kontaktar Adobe support."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#troubleshooting" text="Felsökning"
>additional-url="https://helpx.adobe.com/ca/enterprise/admin-guide.html/ca/enterprise/using/support-for-experience-cloud.ug.html" text="Kontakta supporten för Adobe"

När varje steg har slutförts (extrahering och förtäring) kontrollerar du loggarna och söker efter fel.  Felen bör åtgärdas omedelbart, antingen genom att man hanterar de rapporterade problemen eller genom att man kontaktar Adobe support.

Du kan visa loggar för en befintlig migreringsuppsättning på sidan *Overview*.
Följ stegen nedan:

1. Navigera till sidan *Overview* och markera den migreringsuppsättning som du vill ta bort. Klicka sedan på **View Log** i åtgärdsfältet.

   ![bild](/help/move-to-cloud-service/content-transfer-tool/assets/view-log1.png)

1. Dialogrutan **Logs** visas. Klicka på **Extraction Logs** för att visa loggarna på en ny flik.

   ![bild](/help/move-to-cloud-service/content-transfer-tool/assets/view-log2.png)
Eller:

   Du kan även visa loggar för din migreringsuppsättning på skärmen *Overview*. Markera migreringsuppsättningen och klicka på statusen under fältet **EXTRACTION**. I det här fallet klickar du på **FINISHED** för att visa loggarna på en ny flik.

   ![bild](/help/move-to-cloud-service/content-transfer-tool/assets/view-log3.png)

1. Om du vill bifoga loggarna utan att använda användargränssnittet kan du använda SSH i AEM-källmiljön och lägga till `crx-quickstart/cloud-migration/extraction-XXXXX/output.log file`.

### Ta bort en migreringsuppsättning {#deleting-migration-set}

Du kan ta bort migreringsuppsättningen från sidan *Overview*.
Följ stegen nedan:

1. Navigera till sidan *Overview* och markera den migreringsuppsättning som du vill ta bort. Klicka sedan på **Delete** i åtgärdsfältet.

   ![bild](/help/move-to-cloud-service/content-transfer-tool/assets/delete-1.png)

1. Klicka på **Delete** i dialogrutan **Delete Migration Set** för att bekräfta borttagningen.

   ![bild](/help/move-to-cloud-service/content-transfer-tool/assets/delete-3.png)

## Felsökning {#troubleshooting}

### Blobb-ID saknas {#missing-blobs}

Om blobb-ID saknas, som nämns nedan, måste en konsekvenskontroll utföras i den befintliga databasen och de saknade blobbarna återställas.
`ERROR o.a.j.o.p.b.AbstractSharedCachingDataStore - Error retrieving record [ba45c53f8b687e7056c85dceebf8156a0e6abc7e]`

Följande kommando körs

>[!NOTE]
>
>`--verbose`-flaggan krävs för att rapportera nodsökvägar som refererar till blobbarna.

**För databaser AEM 6.5 (Oak 1.8 och tidigare)**

```shell
java -jar oak-run.jar datastorecheck --consistency --store [<SEGMENT_STORE_PATH>|<MONGO_URI>] --[s3ds|fds] <DATASTORE_CFG> --verbose <OUT_DIR> --dump
```

**För databaser med Oak > 1.10**

```shell
java -jar oak-run.jar datastore --check-consistency [<SEGMENT_STORE_PATH>|<MONGO_URI>] --[s3ds|fds|azureds] <DATASTORE_CFG> --out-dir <OUT_DIR> --work-dir <TEMP_DIR> --verbose
```

Mer information finns i [Oak Runable Jar](https://github.com/apache/jackrabbit-oak/tree/trunk/oak-run).

Filerna som skapas i *OUT_DIR* som anges ovan för överensstämmelse, kan sedan kontrolleras för sökvägar som saknar binärfiler och lämpliga åtgärder kan vidtas, till exempel återställning från en säkerhetskopia, borttagning av sökvägar och omindexering.


### Gränssnittsbeteende {#ui-behavior}

Som användare kan du se följande beteendeförändringar i användargränssnittet i Content Transfer Tool:

* Ikonerna i gränssnittet för verktyget för innehållsöverföring kan se annorlunda ut än skärmbilderna som visas i den här handboken, eller också visas de inte alls beroende på versionen av AEM-källinstansen.

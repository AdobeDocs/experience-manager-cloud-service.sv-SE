---
title: Använda Content Transfer Tool
description: Använda Content Transfer Tool
translation-type: tm+mt
source-git-commit: 01ffc349891ac1e11af4f4bc8a539069b8f6cd5e
workflow-type: tm+mt
source-wordcount: '1617'
ht-degree: 97%

---


# Använda Content Transfer Tool {#using-content-transfer-tool}

## Viktigt att tänka på när du använder Content Transfer Tool {#pre-reqs}

Följ avsnittet nedan om du vill veta mer om viktiga aspekter när du använder Content Transfer Tool:

* Lägsta systemkrav för Content Transfer Tool är AEM 6.3 + och JAVA 8. Om du har en tidigare AEM-version måste du uppgradera din innehållsdatabas till AEM 6.5 för att kunna använda Content Transfer Tool.

* Verktyget Innehållsöverföring kan användas med följande typer av datalager: File Data Store, S3 Data Store och Shared S3 Data Store. Den stöder för närvarande inte Azure Blob Store-datalagret.

* Om du använder en *sandlådemiljö* måste du uppgradera din miljö till version 10 juni 2020 eller senare. Om du använder en *produktionsmiljö* uppdateras den automatiskt.

* Om du vill använda Content Transfer Tool måste du vara adminanvändare i källinstansen och tillhöra administrationsgruppen för AEM i den Cloud Service-instans som du överför innehåll till. Obehöriga användare kan inte hämta åtkomsttoken för att använda Content Transfer Tool.

* Under extraheringsfasen körs Content Transfer Tool på en aktiv AEM-källinstans.

* Författarens *inmatningsfas* kommer att skalas ned för hela författardriftsättningen. Detta innebär att författar-AEM inte är tillgängligt under hela importen.

* Den rekommenderade övre storleksgränsen på databasen som Content Transfer Tool har stöd för är 20 GB.

## Tillgänglighet {#availability}

Content Transfer Tool kan laddas ned som en zip-fil (Content Transfer Tool v1.0.0) från Software Distribution Portal. Du kan installera paketet via pakethanteraren på din källinstans av Adobe Experience Manager (AEM).

>[!NOTE]
>Hämta Content Transfer Tool från [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)-portalen.

## Köra Content Transfer Tool {#running-tool}

>[!VIDEO](https://video.tv.adobe.com/v/35460/?quality=12&learn=on)

Följ det här avsnittet för att lära dig hur du använder Content Transfer Tool för att migrera innehållet till AEM as a Cloud Service (Author/Publish):

1. Välj Adobe Experience Manager och navigera till tools -> **Operations** -> **Content Transfer**.

   ![bild](/help/move-to-cloud-service/content-transfer-tool/assets/content1.png)

1. Klicka på **Create Migration Set** om du vill skapa en ny migreringsuppsättning. Information om **innehållsmigreringsuppsättningen** visas.

   >[!NOTE]
   >Du kommer att visa de befintliga migreringsuppsättningarna på den här skärmen med deras aktuella status.

   ![bild](/help/move-to-cloud-service/content-transfer-tool/assets/ctt-img4.png)

1. Fyll i fälten på skärmen för **innehållsmigreringsuppsättningen** enligt beskrivningen nedan.

   ![bild](/help/move-to-cloud-service/content-transfer-tool/assets/content-3.png)


   1. **Name**: Ange namnet på migreringsuppsättningen.
      >[!NOTE]
      >Inga specialtecken tillåts för migreringsuppsättningens namn.

   1. **Cloud Service Configuration**: Ange målförfattar-URL för AEM as a Cloud Service.

      >[!NOTE]
      >Du kan skapa och underhålla högst fyra migreringsuppsättningar åt gången under innehållsöverföringen.
      >Dessutom måste du skapa en migrering separat för varje specifik miljö – *Stage*, *Development* eller *Production*.

   1. **Access Token**: Ange åtkomsttoken.

      >[!NOTE]
      >Du kan hämta åtkomsttoken från författarinstansen genom att gå till `/libs/granite/migration/token.json`. Åtkomsttoken hämtas från Cloud Service-författarinstansen.

   1. **Parameters**: Välj följande parametrar för att skapa migreringsuppsättningen:

      1. **Include Version**: Välj det som behövs.

      1. **Paths to be included**: Använd sökvägsläsaren för att välja sökvägar som behöver migreras.

         >[!IMPORTANT]
         >Följande sökvägar är begränsade när du skapar en migreringsuppsättning:
         >* `/apps`
         >* `/libs`
         >* `/home`
         >* `/etc`


1. Klicka på **Save** när du har fyllt i alla fält på skärmen **Content Migrations Set details**.

1. Migreringsuppsättningen visas på sidan *Overview*.

   ![bild](/help/move-to-cloud-service/content-transfer-tool/assets/ctt-img4.png)

   Alla befintliga migreringsuppsättningar på den här skärmen visas på sidan *Overview* med aktuell status och statusinformation.

   * Ett *rött moln* anger att du inte kan slutföra extraheringsprocessen.
   * Ett *grönt moln* anger att du kan slutföra extraheringsprocessen.
   * En *gul ikon* anger att du inte har skapat den befintliga migreringsuppsättningen och att den specifika skapas av en annan användare i samma instans.

1. Välj en migreringsuppsättning från översiktssidan och klicka på **Properties** för att visa eller redigera migreringsuppsättningens egenskaper.

   ![bild](/help/move-to-cloud-service/content-transfer-tool/assets/ctt-img6.png)

### Extraheringsprocess i innehållsöverföring {#extraction-process}

Följ stegen nedan för att extrahera migreringsuppsättningen från Content Transfer Tool:

1. Välj en migreringsuppsättning på sidan *Overview* och klicka på **Extract** för att påbörja extraheringen.

   ![bild](/help/move-to-cloud-service/content-transfer-tool/assets/extraction-img1.png)

1. Dialogrutan **Migration Set extraction** visas och du klickar på **Extract** för att slutföra extraheringsfasen.

   >[!NOTE]
   >Du kan skriva över mellanlagringsbehållaren under extraheringsfasen.

   ![bild](/help/move-to-cloud-service/content-transfer-tool/assets/extract-2.png)

1. Fältet **EXTRACTION** visar nu **körningsstatus** för den pågående extraheringsprocessen.

   ![bild](/help/move-to-cloud-service/content-transfer-tool/assets/extract-3.png)

   När extraheringen är klar uppdateras migreringsuppsättningens status till **FINISHED** och en *solid grön* molnikon visas under **INFO**-fältet.

   ![bild](/help/move-to-cloud-service/content-transfer-tool/assets/extract-4.png)

   >[!NOTE]
   >Du måste uppdatera sidan för att visa den uppdaterade statusen.
   >När extraheringsfasen startas skapas ett skrivlås som frisläpps efter *60 sekunder*. Om extraheringen avbryts måste du alltså vänta en minut på att låset ska frisläppas innan du startar extraheringen igen.

#### Uppdateringsextrahering {#top-up-extraction-process}

Content Transfer Tool har en funktion för differentiell innehållsuppdatering som gör att du kan överföra enbart de ändringar som gjorts sedan den föregående innehållsöverföringen.

>[!NOTE]
>Efter den första innehållsöverföringen bör du göra regelbundna tillägg av differentiellt innehåll för att förkorta innehållets frysningsperiod för den slutliga differentiella innehållsöverföringen innan du börjar använda Cloud Service.

När extraheringen är klar kan du överföra delta-innehåll med extraheringsmetoden för uppdateringar. Följ stegen nedan:

1. Gå till sidan *Overview* och välj den migreringsuppsättning som du vill utföra ändringsextraheringen för.

1. Klicka på **Extract** för att starta uppdateringsextraheringen.

   ![bild](/help/move-to-cloud-service/content-transfer-tool/assets/extraction-img1.png)

1. Dialogrutan **Migration Set extraction** visas.

   >[!IMPORTANT]
   >Du bör inaktivera alternativet **Overwrite staging container during extraction**.
   ![bild](/help/move-to-cloud-service/content-transfer-tool/assets/extract-topup-1.png)

### Inmatningsprocess i innehållsöverföring {#ingestion-process}

Följ stegen nedan för att importera migreringsuppsättningen från Content Transfer Tool:

1. Välj en migreringsuppsättning på sidan *Overview* och klicka på **Ingest** för att påbörja extraheringen.

   ![bild](/help/move-to-cloud-service/content-transfer-tool/assets/ingest-1.png)

1. Dialogrutan **Migration Set ingestion** visas.

   ![bild](/help/move-to-cloud-service/content-transfer-tool/assets/ingest-2.png)

   I demonstrationssyfte är alternativet **Ingest content to Author instance** inaktiverat. Det går att importera innehåll till Author och Publish samtidigt.

   ![bild](/help/move-to-cloud-service/content-transfer-tool/assets/ingest-3.png)

   Klicka på **Ingest** för att slutföra inmatningen.

1. När inmatningen är klar uppdateras statusen i fältet **AUTHOR INGESTION** till **FINISHED** och en solid grön molnikon visas under **INFO**.
   ![bild](/help/move-to-cloud-service/content-transfer-tool/assets/ingest-4.png)

   >[!NOTE]
   > Du måste uppdatera sidan för att visa den uppdaterade statusen.

#### Uppdatera inmatning {#top-up-ingestion-process}

Content Transfer Tool har en funktion för differentiell *innehållsuppdatering* som gör att du kan överföra enbart de ändringar som gjorts sedan den föregående innehållsöverföringen.

>[!NOTE]
>Efter den första innehållsöverföringen bör du göra regelbundna tillägg av differentiellt innehåll för att förkorta innehållets frysningsperiod för den slutliga differentiella innehållsöverföringen innan du börjar använda Cloud Service.

När inmatningen är klar kan du använda delta-innehåll med hjälp av inmatningsmetoden för uppdateringar. Följ stegen nedan:

1. Navigera till sidan *Overview* och välj den migreringsuppsättning som du vill utföra uppdateringsinmatningen för.

1. Klicka på **Ingest** för att starta uppdateringsextraheringen.

   ![bild](/help/move-to-cloud-service/content-transfer-tool/assets/ingest-1.png)

1. Dialogrutan **Migration Set Ingestion** visas.

   >[!NOTE]
   >Du bör inaktivera alternativet *Wipe* för att förhindra att befintligt innehåll tas bort från den tidigare inmatningsaktiviteten.
   ![bild](/help/move-to-cloud-service/content-transfer-tool/assets/ingest-topup-1.png)

### Visa loggar för en migreringsuppsättning {#viewing-logs-migration-set}

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

* Användaren skapar en migreringsuppsättning för en författares URL (Development/Stage/Production) och utför extrahering och inmatning.

* Användaren skapar sedan en ny migreringsuppsättning för samma författar-URL och utför extrahering och inmatning på den nya migreringsuppsättningen. Gränssnittet visar att den första migreringsuppsättningens inmatningsstatus ändras till **FAILED** och att inga loggar är tillgängliga.

* Detta innebär inte att inmatningen för den första migreringsuppsättningen misslyckades. Det här beteendet visas eftersom det tidigare inmatningsjobbet tas bort när ett nytt inmatningsjobb startas. Därför bör ändringsstatusen för den första migreringsuppsättningen ignoreras.

* Ikonerna i gränssnittet för verktyget för innehållsöverföring kan se annorlunda ut än skärmbilderna som visas i den här handboken, eller också visas de inte alls beroende på versionen av AEM-källinstansen.



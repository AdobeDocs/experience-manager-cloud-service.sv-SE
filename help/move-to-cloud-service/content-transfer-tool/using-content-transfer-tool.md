---
title: Använda verktyget Innehållsöverföring
description: Använda verktyget Innehållsöverföring
translation-type: tm+mt
source-git-commit: f2a6b67e3673bf6dfeb63d445074f6d1e05971cf
workflow-type: tm+mt
source-wordcount: '1543'
ht-degree: 1%

---


# Använda verktyget Innehållsöverföring {#using-content-transfer-tool}

## Viktigt att tänka på när du använder verktyget Innehållsöverföring {#pre-reqs}

Följ avsnittet nedan om du vill veta mer om viktiga aspekter när du kör verktyget Innehållsöverföring:

* Systemkravet för verktyget Innehållsöverföring är AEM 6.3 + och JAVA 8. Om du har en lägre AEM-version måste du uppgradera din innehållsdatabas till AEM 6.5 för att kunna använda verktyget för innehållsöverföring.

* Om du använder en *sandlådemiljö* måste du uppgradera din miljö till version 10 juni 2020 eller senare. Om du använder en *produktionsmiljö* uppdateras den automatiskt.

* Om du vill använda verktyget Innehållsöverföring måste du vara en adminanvändare i källinstansen och tillhöra gruppen AEM-administratörer i den molntjänstinstans du överför innehåll till. Obehöriga användare kan inte hämta åtkomsttoken för att använda verktyget Innehållsöverföring.

* Under extraheringsfasen körs verktyget Innehållsöverföring på en aktiv AEM-källinstans.

* Författarens *matningsfas* kommer att skalas ned för hela författardistributionen. Detta innebär att författaren AEM inte är tillgänglig under hela importen.

## Tillgänglighet {#availability}

Verktyget Innehållsöverföring kan laddas ned som en zip-fil (Content Transfer Tool v1.0.0) från portalen för programdistribution. Du kan installera paketet via Package Manager på din källinstans av Adobe Experience Manager (AEM).

>[!NOTE]
>Hämta verktyget Innehållsöverföring från [Software Distribution Portal](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html).

## Använda verktyget Innehållsöverföring {#running-tool}

Följ det här avsnittet för att lära dig hur du använder verktyget Innehållsöverföring för att migrera innehållet till AEM som en molntjänst (Författare/Publicera):

1. Välj Adobe Experience Manager och navigera till verktyg -> **Åtgärder** -> **Innehållsöverföring**.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/content1.png)

1. Klicka på **Skapa migreringsuppsättning** för att skapa en ny migreringsuppsättning. Information om **innehållsmigreringsuppsättningen** visas.

   >[!NOTE]
   >Du kommer att visa de befintliga migreringsuppsättningarna på den här skärmen med deras aktuella status.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/ctt-img4.png)

1. Fyll i fälten på skärmen **Innehållsmigreringar Ange information** enligt beskrivningen nedan.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/content-3.png)


   1. **Namn**: Ange namnet på migreringsuppsättningen.
      >[!NOTE]
      >Inga specialtecken tillåts för migreringsuppsättningens namn.

   1. **Konfiguration** av molntjänst: Ange mål-AEM som en URL för molntjänstförfattare.

      >[!NOTE]
      >Du kan skapa och underhålla högst fyra migreringsuppsättningar åt gången under innehållsöverföringsaktiviteten.
      >Dessutom måste du skapa en migrering separat för varje specifik miljö - *Stage*, *Development* eller *Production*.

   1. **Åtkomsttoken**: Ange åtkomsttoken.

      >[!NOTE]
      >Du kan hämta åtkomsttoken från författarinstansen genom att gå till `/libs/granite/migration/token.json`. Åtkomsttoken hämtas från molntjänstens författarinstans.

   1. **Parametrar**: Välj följande parametrar för att skapa migreringsuppsättningen:

      1. **Inkludera version**: Välj det som behövs.

      1. **Banor som ska inkluderas**: Använd sökvägsläsaren för att välja sökvägar som behöver migreras.

         >[!IMPORTANT]
         >Följande sökvägar är begränsade när du skapar en migreringsuppsättning:
         >* `/apps`
         >* `/libs`
         >* `/home`
         >* `/etc`


1. Klicka på **Spara** när du har fyllt i alla fält på skärmen **Innehållsmigreringar Ange detaljer** .

1. Migreringsuppsättningen visas på sidan *Översikt* .

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/ctt-img4.png)

   Alla befintliga migreringsuppsättningar på den här skärmen visas på sidan *Översikt* med aktuell status- och statusinformation.

   * Ett *rött moln* anger att du inte kan slutföra extraheringsprocessen.
   * Ett *grönt moln* anger att du kan slutföra extraheringsprocessen.
   * En *gul ikon* anger att du inte har skapat den befintliga migreringsuppsättningen och att den specifika skapas av en annan användare i samma instans.

1. Välj en migreringsuppsättning från översiktssidan och klicka på **Egenskaper** för att visa eller redigera migreringsuppsättningens egenskaper.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/ctt-img6.png)

### Extraheringsprocess i innehållsöverföring {#extraction-process}

Följ stegen nedan för att extrahera din migreringsuppsättning från verktyget Innehållsöverföring:

1. Välj en migreringsuppsättning på sidan *Översikt* och klicka på **Extrahera** för att påbörja extraheringen.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/extraction-img1.png)

1. Extraheringsdialogrutan för **migreringsuppsättning** visas och klicka på **Extrahera** för att slutföra extraheringsfasen.

   >[!NOTE]
   >Du kan skriva över mellanlagringsbehållaren under extraheringsfasen.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/extract-2.png)

1. Fältet **EXTRACTION** visar nu **körningsstatus** för den pågående extraheringsprocessen.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/extract-3.png)

   När extraheringen är klar uppdateras migreringsuppsättningens status till **FINISHED** och en *solid grön* molnikon visas under **INFO** -fältet.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/extract-4.png)

   >[!NOTE]
   >Du måste uppdatera sidan för att visa den uppdaterade statusen.
   >När extraheringsfasen startas skapas ett skrivlås som släpps efter *60 sekunder*. Om extraheringen stoppas måste du alltså vänta en minut på att låset ska frisläppas innan du startar extraheringen igen.

#### Extrahering uppifrån och ned {#top-up-extraction-process}

Verktyget Innehållsöverföring har en funktion som har stöd för differentiell innehållsuppsättning där det endast är möjligt att överföra ändringar som gjorts sedan föregående innehållsöverföringsaktivitet.

>[!NOTE]
>Efter den första innehållsöverföringen bör du göra regelbundna tillägg av differentiellt innehåll för att förkorta innehållets frysningsperiod för den slutliga differentiella innehållsöverföringen innan du börjar använda molntjänsten.

När extraheringen är klar kan du överföra delta-innehåll med extraheringsmetoden top-up. Följ stegen nedan:

1. Navigera till sidan *Översikt* och välj den migreringsuppsättning som du vill utföra extraheringen för uppifrån.

1. Klicka på **Extrahera** för att starta extraheringen uppifrån.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/extraction-img1.png)

1. Dialogrutan Extrahering av **migreringsuppsättning** visas.

   >[!IMPORTANT]
   >Du bör inaktivera **Skriv över mellanlagringsbehållaren under extraheringen** .
   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/extract-topup-1.png)

### Inmatningsprocess i innehållsöverföring {#ingestion-process}

Följ stegen nedan för att importera din migreringsuppsättning från verktyget Innehållsöverföring:

1. Välj en migreringsuppsättning på *sidan Översikt* och klicka på **Infoga** för att påbörja extraheringen.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/ingest-1.png)

1. Dialogrutan **Migreringsuppsättning** visas.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/ingest-2.png)

   I demonstrationssyfte är alternativet **Ingest content to Author instance** inaktiverat. Det går att importera innehåll till författare och publicera samtidigt.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/ingest-3.png)

   Klicka på **Ingest** för att slutföra intagningsfasen.

1. När importen är klar uppdateras statusen i fältet **FÖRFATTNING** till **FINISHED** och en solid grön molnikon visas under **INFO**.
   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/ingest-4.png)

   >[!NOTE]
   > Du måste uppdatera sidan för att visa den uppdaterade statusen.

#### Övre inmatning {#top-up-ingestion-process}

Verktyget Innehållsöverföring har en funktion som har stöd för *uppräkning* av differentiellt innehåll där det endast är möjligt att överföra ändringar som gjorts sedan den tidigare aktiviteten för innehållsöverföring.

>[!NOTE]
>Efter den första innehållsöverföringen bör du göra regelbundna tillägg av differentiellt innehåll för att förkorta innehållets frysningsperiod för den slutliga differentiella innehållsöverföringen innan du börjar använda molntjänsten.

När intagsprocessen är klar kan du använda delta-innehåll med hjälp av den översta intagsmetoden. Följ stegen nedan:

1. Navigera till sidan *Översikt* och välj den migreringsuppsättning som du vill använda för det översta intaget.

1. Klicka på **Ingest** för att starta extraheringen uppifrån.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/ingest-1.png)

1. Dialogrutan **Migreringsuppsättning för inmatning** visas.

   >[!NOTE]
   >Du bör inaktivera alternativet *Svep* för att förhindra att befintligt innehåll tas bort från den tidigare intagsaktiviteten.
   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/ingest-topup-1.png)

### Visa loggar för en migreringsuppsättning {#viewing-logs-migration-set}

Du kan visa loggar för en befintlig migreringsuppsättning från sidan *Översikt* .
Följ stegen nedan:

1. Navigera till sidan *Översikt* och markera den migreringsuppsättning som du vill ta bort. Klicka sedan på **Visa logg** i åtgärdsfältet.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/view-log1.png)

1. Dialogrutan **Loggar** visas. Klicka på **Extraheringsloggar** för att visa loggarna på en ny flik.

   ![bild](/help/move-to-cloud-service/content-transfer-tool/assets/view-log2.png)eller

   Du kan även visa loggar för din migreringsuppsättning från *översiktsskärmen* . Välj migreringsuppsättningen och klicka på statusen under **EXTRACTION** -fältet. I så fall klickar du på **FINISHED** för att visa loggarna på en ny flik.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/view-log3.png)

### Ta bort en migreringsuppsättning {#deleting-migration-set}

Du kan ta bort migreringsuppsättningen från sidan *Översikt* .
Följ stegen nedan:

1. Navigera till sidan *Översikt* och markera den migreringsuppsättning som du vill ta bort. Klicka sedan på **Ta bort** i åtgärdsfältet.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/delete-1.png)

1. Klicka på **Ta bort** från dialogrutan **Ta bort migreringsuppsättning** för att bekräfta borttagningen.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/delete-3.png)

## Felsökning {#troubleshooting}

### Blobb-ID saknas {#missing-blobs}

Om det saknas blob-ID:n rapporterade, som nämns nedan, måste en konsekvenskontroll utföras i den befintliga databasen och de saknade blobbarna återställas.
`ERROR o.a.j.o.p.b.AbstractSharedCachingDataStore - Error retrieving record [ba45c53f8b687e7056c85dceebf8156a0e6abc7e]`

Följande kommando körs

>[!NOTE]
> `--verbose` -flaggan krävs för att rapportera nodsökvägarna som blobben refererar till från.

**För databaser AEM 6.5 (Oak 1.8 och tidigare)**

```shell
java -jar oak-run.jar datastorecheck --consistency --store [<SEGMENT_STORE_PATH>|<MONGO_URI>] --[s3ds|fds] <DATASTORE_CFG> --verbose <OUT_DIR> --dump
```

**För databaser med Oak > 1.10**

```shell
java -jar oak-run.jar datastore --check-consistency [<SEGMENT_STORE_PATH>|<MONGO_URI>] --[s3ds|fds|azureds] <DATASTORE_CFG> --out-dir <OUT_DIR> --work-dir <TEMP_DIR> --verbose
```

Mer information finns i [Oak Runable Jar](https://github.com/apache/jackrabbit-oak/tree/trunk/oak-run) .

Filerna som skapas i *OUT_DIR* som anges ovan för enhetlighet kan sedan kontrolleras för sökvägar som saknar binärfiler och lämpliga åtgärder kan vidtas, till exempel återställning från en säkerhetskopia, borttagning av sökvägar, omindexering.

### Gränssnittsbeteende {#ui-behavior}

Som användare kan du se följande beteendeförändringar i användargränssnittet för verktyget Innehållsöverföring:

* Användaren skapar en migreringsuppsättning för en författares URL (Utveckling/scen/Produktion) och utför extrahering och förtäring.

* Användaren skapar sedan en ny migreringsuppsättning för samma författar-URL och utför extrahering och förtäring på den nya migreringsuppsättningen. Gränssnittet visar att den första migreringsuppsättningens inmatningsstatus ändras till **MISSLYCKAD** och att inga loggar är tillgängliga.

* Detta innebär inte att det inte gick att lägga till den första migreringsuppsättningen. Det här beteendet syns eftersom det tidigare intagningsjobbet tas bort när ett nytt intagsjobb startas. Därför bör ändringsstatusen för den första migreringsuppsättningen ignoreras.

* Ikonerna i gränssnittet för verktyget Innehållsöverföring kan se annorlunda ut än skärmbilderna som visas i den här guiden, eller så visas de inte alls beroende på version av AEM-källinstansen.



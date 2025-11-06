---
title: Komma igång med verktyget Innehållsöverföring
description: Lär dig hur du kommer igång med verktyget Innehållsöverföring
exl-id: c0cecf65-f419-484b-9d55-3cbd561e8dcd
feature: Migration
role: Admin
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1653'
ht-degree: 2%

---


# Komma igång med verktyget Innehållsöverföring {#getting-started-content-transfer-tool}


## Tillgänglighet {#availability}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_download"
>title="Ladda ned"
>abstract="Innehållsöverföringsverktyget kan laddas ned som en zip-fil från Software Distribution Portal. Du kan installera paketet via Package Manager på Adobe Experience Manager-källinstansen (AEM). Glöm inte att hämta den senaste versionen."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/release-notes/release-notes-current.html" text="Versionsinformation"
>additional-url="https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html" text="Programdistributionsportal"

Innehållsöverföringsverktyget kan laddas ned som en zip-fil från Software Distribution Portal. Du kan installera paketet med hjälp av [Package Manager](/help/implementing/developing/tools/package-manager.md) på Adobe Experience Manager-källinstansen (AEM). Glöm inte att hämta den senaste versionen. Mer information om den senaste versionen finns i [Versionsinformation](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/release-notes/release-notes-current.html).

Endast version 2.0.0 och senare stöds, och du bör använda den senaste versionen.

>[!NOTE]
>Hämta Content Transfer Tool från [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)-portalen.

## Source Environment Connectivity {#source-environment-connectivity}

>[!NOTE]
>
>Ett anslutningsfel kan också uppstå om en migreringsuppsättning har tagits bort från Cloud Acceleration Manager.

Källinstansen av AEM kanske körs bakom en brandvägg där den bara kan nå vissa värdar som har lagts till i Tillåtelselista. Följande slutpunkter måste vara tillgängliga från den instans som kör AEM för att det ska gå att köra en extrahering:

* Azure-blobblagringstjänsten: `casstorageprod.blob.core.windows.net`

>[!NOTE]
>Om extraheringen misslyckas på grund av följande fel:&quot;javax.net.ssl.SSLHandshakeException: sun.security.validator.ValidatorException: PKIX path building failed: sun.security.provider.certpath.SunCertPathBuilderException: unable to requested target&quot;, kan detta lösas genom import av relevant certifikatutfärdarcertifikat.

### Aktivera SSL-loggning {#enable-ssl-logging}

Det kan vara svårt att förstå SSL-/TLS-anslutningsproblem. Om du vill felsöka anslutningsproblem under en extraheringsprocess kan du aktivera SSL-loggning via systemkonsolen i AEM-källmiljön genom att följa dessa steg:

1. Gå till Adobe Experience Manager Web Console på källinstansen genom att gå till **Verktyg > Åtgärder > Webbkonsol** eller direkt till URL:en på *https://serveraddress:serverport/system/console/configMgr*
1. Sök efter **Konfiguration av extraheringstjänst för innehållsöverföringsverktyg**
1. Använd pennikonknappen för att redigera dess konfigurationsvärden
1. Aktivera inställningen **Aktivera SSL-loggning för extrahering** och tryck sedan på **Spara**:

   ![bild](/help/journey-migration/content-transfer-tool/assets/enable_ssl_logging.png)

>[!NOTE]
>
>Den här flaggan används endast för felsökning av SSL-problem. Se till att flaggan är inaktiverad innan du kör extraheringen, eftersom det kan kräva mycket diskutrymme. Detta kan potentiellt fylla diskkapaciteten och orsaka att extraheringsprocessen misslyckas.

## Använda verktyget Innehållsöverföring {#running-tool}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_demo"
>title="Verktyget Innehållsöverföring körs"
>abstract="Lär dig hur du använder verktyget Innehållsöverföring för att migrera innehåll till AEM as a Cloud Service (författare/publicera)."
>additional-url="https://video.tv.adobe.com/v/35460/?quality=12&learn=on" text=" Se demo"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/migration/content-transfer-tool.html#migration" text="Självstudiekurs - använda verktyget Innehållsöverföring"

Följande avsnitt gäller för den nya versionen av verktyget Innehållsöverföring. Följ det här avsnittet för att lära dig hur du använder verktyget Innehållsöverföring för att migrera innehåll till AEM as a Cloud Service:

### Installationsfas för extrahering {#extraction-setup-phase}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_extraction_setup"
>title="Installationsfas för extrahering"
>abstract="Lär dig skapa och hantera en migreringsuppsättning och hur du kopierar extraheringsnyckeln."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/migration/content-transfer-tool.html#migration" text="Självstudiekurs - använda verktyget Innehållsöverföring"

<!-- Contextualhelp id "aemcloud_ctt_extraction_setup" must be added here -->

1. Logga in på Cloud Acceleration Manager (CAM) och klicka på CAM-projektet som du skapat tidigare för att utvärdera om du är redo att gå över till AEM as a Cloud Service. Om du inte har skapat något CAM-projekt, se Skapa och hantera ett projekt i CAM.

1. Klicka på kortet **Innehållsöverföring** för att öppna vyn med listan över migreringsuppsättningar.

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam1.png)

1. Skapa en migreringsuppsättning genom att klicka på **Skapa migreringsuppsättning**.

   >[!NOTE]
   >
   >Högst 10 migreringsuppsättningar, inklusive uppsättningar som gått ut, kan skapas per projekt i Cloud Acceleration Manager.

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam2.png)

   Följande dialogruta visas. Observera att ett migreringsuppsättning upphör att gälla efter en längre inaktivitetsperiod. När varningar visas på projektkortet och migreringsjobbtabellsraderna för en tidsperiod, kommer migreringsuppsättningen att upphöra att gälla och dess data kommer inte längre att vara tillgängliga. Granska [migreringsuppsättningen upphör](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/overview-content-transfer-tool.md#migration-set-expiry) om du vill ha mer information.

   När du skapar en migreringsuppsättning kan du välja det geografiska område där data för den tillfälliga migreringen ska lagras.  Vi rekommenderar att du väljer den region som ligger närmast din målmolnmiljö för att få optimala prestanda vid inmatning.  Regionen kan inte ändras efter att en migreringsuppsättning har skapats. Om du vill använda en annan region måste du skapa en ny migreringsuppsättning.

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam3.png)

   >[!NOTE]
   >
   >Namnet måste följa samma konventioner för en AEM-nod så det får inte innehålla något av följande tecken: `. / : [ ] | * < > ^ ? { } % # ` eller ovanliga symboler eller uttryck.

1. Nu bör du se din migreringslista i listvyn. Markera symbolen med tre punkter (**..**) för att öppna listrutan och välj **Kopiera extraheringsnyckel**. Du behöver den här nyckeln under extraheringsfasen. Kopiera den här extraheringsnyckeln.

   >[!NOTE]
   >
   >Extraheringsnyckeln gör det möjligt för din AEM-källmiljö att ansluta säkert till migreringsuppsättningen. Behandla den här nyckeln med samma noggrannhet som du skulle ha gjort med ett lösenord och dela det aldrig på ett osäkert medium som e-post.

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam4.png)

### Fyller i migreringsuppsättningen {#populating-the-migration-set}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_populate_migrationset"
>title="Fyll i migreringsuppsättning"
>abstract="När du har skapat en migreringsuppsättning måste den fyllas i med innehållet från källinstansen som måste flyttas till AEM as a Cloud Service-miljön. För att göra detta måste verktyget Innehållsöverföring vara installerat på källinstansen."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/extracting-content.html" text="Extraherar innehåll"

Om du vill fylla i den migreringsuppsättning du skapade i Cloud Acceleration Manager installerar du den senaste versionen av verktyget Innehållsöverföring på Adobe Experience Manager-källinstansen (AEM). Följ det här avsnittet om du vill lära dig hur du fyller i migreringsuppsättningen.

1. När du har installerat den senaste versionen av verktyget Innehållsöverföring på Adobe Experience Manager-källinstansen går du till **Åtgärder - Innehållsmigrering**

1. Klicka på **Skapa migreringsuppsättning**.

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam5.png)

1. Klistra in extraheringsnyckeln som kopierades från CAM tidigare i indatafältet för extraheringsnyckeln i formuläret **Skapa migreringsuppsättning**. När du har gjort det fylls namnen på migreringsuppsättningen och projektnamnet för Cloud Acceleration Manager (CAM) i automatiskt. Dessa ska matcha namnet på migreringsuppsättningen i CAM och namnet på CAM-projektet som du skapade. Nu kan du lägga till innehållssökvägar. Spara migreringsuppsättningen när du har lagt till innehållssökvägar. Du kan köra extraheringen med antingen versioner inkluderade eller exkluderade.

   >[!NOTE]
   >
   >Kontrollera att extraheringsnyckeln är giltig och att den inte är i närheten av utgångsdatumet. Du kan hämta den här informationen i dialogrutan **Skapa migreringsuppsättning** när du har klistrat in extraheringsnyckeln. Om du får ett anslutningsfel finns mer information i [Source Environment Connectivity](#source-environment-connectivity) .

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/createMigrationSet.png)

1. Välj sedan följande parametrar för att skapa en migreringsuppsättning:

   1. **Inkludera version**: Välj det som behövs. När versioner inkluderas inkluderas sökvägen `/var/audit` automatiskt för att migrera granskningshändelser.

      ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/includeVersion.png)

      >[!NOTE]
      >Om du tänker ta med versioner som en del av en migreringsuppsättning och utför tilläggsprogram med `wipe=false`, måste du inaktivera versionsrensning på grund av en aktuell begränsning i verktyget Innehållsöverföring. Om du föredrar att behålla versionsrensning aktiverad och utför toppuppsättningar i en migreringsuppsättning, måste du utföra det som `wipe=true`.

      >[!NOTE]
      >Från och med CTT-versionen (3.0.24) har nya funktioner inkluderats i verktyget Innehållsöverföring, vilket förbättrar processen att inkludera och exkludera banor. Tidigare var sökvägarna tvungna att väljas en i taget, vilket var tidsödande och tidsödande. Nu kan användare inkludera sökvägar direkt från användargränssnittet eller överföra en CSV-fil enligt sina önskemål.  CSV-filen måste ha en sökväg per rad och inga kommatecken.

   1. **Sökvägar som ska inkluderas**: Använd sökvägsläsaren för att välja sökvägar som ska migreras. Banväljaren accepterar indata genom att skriva eller genom att välja. Användare kan bara välja ett alternativ för att inkludera sökvägar: antingen från användargränssnittet eller genom att överföra en CSV-fil.

      >[!IMPORTANT]
      >Följande sökvägar är begränsade när du skapar en migreringsuppsättning:
      >
      >* `/apps`
      >* `/libs`
      >* `/home`
      >* `/etc` (vissa `/etc` sökvägar kan väljas i CTT)

      ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/includeAndExcludePath.png)

      1. Det går bara att välja sökväg, och minst en sökväg måste finnas. Om ingen sökväg är markerad inträffar ett serverfel.

         ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/ServerError.png)

      1. När du använder **CSV-överföringsalternativet** måste CSV-filen innehålla giltiga sökvägar.

         ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/validCsvUpload.png)

      1. Om du vill växla tillbaka till sökvägsväljaren måste användarna uppdatera sidan och börja om från början.

      1. Om **ogiltiga sökvägar** hittas i den överförda CSV-filen visas de ogiltiga sökvägarna i en separat dialogruta.

         ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/invalidPathsInCsv.png)

      1. Användarna måste korrigera CSV-filen och överföra den igen eller uppdatera användargränssnittet för att välja sökvägar via sökvägsväljaren.

   1. **Sökvägar som ska uteslutas**: En ny funktion gör att användare kan exkludera specifika sökvägar om de inte vill att de ska tas med. Om sökvägen i inkluderingsavsnittet till exempel är /content/dam kan användare nu utesluta sökvägar som /content/dam/catalogs.

      ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/excludePathHighlighted.png)

1. Klicka på **Spara** när du har fyllt i alla fält på informationsskärmen för **Skapa migreringsuppsättning**.

<!-- 1. You will view your migration set in the **Content Transfer** wizard, as shown in the figure below.

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/ctt07.png)

   All the existing migration sets are displayed on the **Content Transfer** wizard with their current status and status information. You may see some of these icons described below.

   * A *red cloud* indicates that you cannot complete the extraction process.
   * A *green cloud* indicates that you can complete the extraction process.
   * A *yellow icon* indicates that you did not create the existing migration set and the specific one is created by some other user in the same instance.

1. Select a migration set and click **Properties** to view or edit the migration set properties. While editing properties, it is not possible to change the **Migration Set name** or the **Service URL**. 

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/ctt06.png) -->

### Bestämma migreringsuppsättningens storlek {#migration-set-size}

När du har skapat en migreringsuppsättning rekommenderar vi att du kör en storlekskontroll på migreringsuppsättningen innan du startar en extraheringsprocess.
Genom att köra en storlekskontroll på migreringsuppsättningen kan du:

* Kontrollera om det finns tillräckligt med diskutrymme i underkatalogen `crx-quickstart` för att slutföra extraheringen.
* Kontrollera om migreringsuppsättningens storlek ligger inom de produktgränser som stöds och undvik misslyckade innehållsfrågor.

Följ stegen nedan för att göra en storlekskontroll:

1. Välj en migreringsuppsättning och klicka på **Kontrollera storlek**.

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam8.png)

1. Dialogrutan **Kontrollera storlek** öppnas.

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/checkMigrationSetSize.png)

1. Klicka på **Kontrollera storlek** för att starta processen. Du kommer sedan tillbaka till vyn med migreringsuppsättningslistor och du bör se ett meddelande om att **Kontrollera storlek** körs.

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam10.png)

1. När **Kontrollera storlek**-processen har slutförts ändras statusen till **SLUTFÖRD**. Välj samma migreringsuppsättning och klicka på **Kontrollera storlek** för att visa resultatet. Nedan visas ett exempel på **Kontrollera storlek** utan varningar.

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/checkSizeAfterFinished.png)

1. Om resultatet **Kontrollera storlek** visar att det antingen inte finns tillräckligt med diskutrymme, eller att migreringsuppsättningen överskrider produktgränserna, eller båda, visas en **VARNING** -status.

<!--   ![image](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image6.png)
   
   Below is an example of **Check Size** results with warnings.
 
   ![image](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image7.png) -->


## What&#39;s Next {#whats-next}

När du har lärt dig hur du skapar en migreringsuppsättning kan du nu lära dig mer om extraherings- och inmatningsprocesser i verktyget Innehållsöverföring. Innan du lär dig dessa processer måste du granska [Hantera stora innehållsdatabaser](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md) för att avsevärt snabba upp extraherings- och inmatningsfaserna i innehållsöverföringsaktiviteten så att innehåll flyttas till AEM as a Cloud Service.

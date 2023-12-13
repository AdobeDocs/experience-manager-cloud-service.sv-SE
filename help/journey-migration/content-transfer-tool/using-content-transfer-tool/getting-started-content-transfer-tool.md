---
title: Komma igång med verktyget Innehållsöverföring
description: Lär dig hur du kommer igång med verktyget Innehållsöverföring
exl-id: c0cecf65-f419-484b-9d55-3cbd561e8dcd
source-git-commit: 0161477e5248267224fe6d637a192f409161f6d3
workflow-type: tm+mt
source-wordcount: '1362'
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

Innehållsöverföringsverktyget kan laddas ned som en zip-fil från Software Distribution Portal. Du kan installera paketet via [Pakethanteraren](/help/implementing/developing/tools/package-manager.md) på din källinstans av Adobe Experience Manager (AEM). Glöm inte att hämta den senaste versionen. Mer information om den senaste versionen finns på [Versionsinformation](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/release-notes/release-notes-current.html).

Endast version 2.0.0 och senare stöds, och du bör använda den senaste versionen.

>[!NOTE]
>Hämta Content Transfer Tool från [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)-portalen.

## Anslutning för källmiljö {#source-environment-connectivity}

>[!NOTE]
>
>Ett anslutningsfel kan också uppstå om en migreringsuppsättning har tagits bort från Cloud Acceleration Manager.

Källinstansen AEM kanske köras bakom en brandvägg där den bara kan nå vissa värdar som har lagts till i Tillåtelselista. Följande slutpunkter måste vara tillgängliga från den instans som kör AEM för att det ska gå att köra en extrahering:

* Azure-blobblagringstjänsten: `casstorageprod.blob.core.windows.net`

>[!NOTE]
>Om extraheringen misslyckas på grund av följande fel:&quot;javax.net.ssl.SSLHandshakeException: sun.security.validator.ValidatorException: PKIX path building failed: sun.security.provider.certpath.SunCertPathBuilderException: unable to requested target&quot;, kan detta lösas genom import av relevant certifikatutfärdarcertifikat.

### Aktivera SSL-loggning {#enable-ssl-logging}

Det kan vara svårt att förstå SSL-/TLS-anslutningsproblem. Om du vill felsöka anslutningsproblem under en extraheringsprocess kan du aktivera SSL-loggning via systemkonsolen i AEM genom att följa dessa steg:

1. Navigera till Adobe Experience Manager Web Console i källinstansen genom att gå till **Verktyg > Åtgärder > Webbkonsol** eller direkt till URL:en på *https://serveraddress:serverport/system/console/configMgr*
1. Sök efter **Konfiguration av extraheringstjänst för innehållsöverföringsverktyg**
1. Använd pennikonknappen för att redigera dess konfigurationsvärden
1. Aktivera **Aktivera SSL-loggning för extrahering** ställa in och sedan trycka **Spara**:

   ![bild](/help/journey-migration/content-transfer-tool/assets/enable_ssl_logging.png)

>[!NOTE]
>Den här flaggan används endast för felsökning av SSL-problem. Se till att flaggan är inaktiverad innan du kör extraheringen, eftersom det kan kräva mycket diskutrymme. Detta kan potentiellt fylla diskkapaciteten och orsaka att extraheringsprocessen misslyckas.

## Använda verktyget Innehållsöverföring {#running-tool}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_demo"
>title="Verktyget Innehållsöverföring körs"
>abstract="Lär dig hur du använder verktyget Innehållsöverföring för att migrera innehållet till AEM as a Cloud Service (Författare/Publicera)."
>additional-url="https://video.tv.adobe.com/v/35460/?quality=12&amp;learn=on" text=" Se demo"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/migration/content-transfer-tool.html#migration" text="Självstudiekurs - använda verktyget Innehållsöverföring"

Följande avsnitt gäller för den nya versionen av verktyget Innehållsöverföring. Följ det här avsnittet för att lära dig hur du använder verktyget Innehållsöverföring för att migrera innehåll till AEM as a Cloud Service:

### Installationsfas för extrahering {#extraction-setup-phase}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_extraction_setup"
>title="Installationsfas för extrahering"
>abstract="Lär dig skapa och hantera en migreringsuppsättning och hur du kopierar extraheringsnyckeln."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/migration/content-transfer-tool.html#migration" text="Självstudiekurs - använda verktyget Innehållsöverföring"

<!-- Contextualhelp id "aemcloud_ctt_extraction_setup" must be added here -->

1. Logga in på CAM (Cloud Acceleration Manager) och klicka på CAM-projektet som du skapat tidigare för att utvärdera om du är redo att gå AEM as a Cloud Service. Om du inte har skapat något CAM-projekt, se Skapa och hantera ett projekt i CAM.

1. Klicka på **Innehållsöverföring** för att öppna vyn Migreringsuppsättningslista.

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam1.png)

1. Skapa en migreringsuppsättning genom att klicka på **Skapa migreringsuppsättning**.

   >[!NOTE]
   >
   >Högst 20 migreringsuppsättningar, inklusive utgångna uppsättningar, kan skapas per projekt i Cloud Acceleration Manager.

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam2.png)

   Följande dialogruta visas. Observera att ett migreringsuppsättning upphör att gälla efter en längre inaktivitetsperiod. När varningar visas på projektkortet och migreringsjobbtabellsraderna för en tidsperiod, kommer migreringsuppsättningen att upphöra att gälla och dess data kommer inte längre att vara tillgängliga. Granska [Förfallotid för migreringsuppsättning](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/overview-content-transfer-tool.md#migration-set-expiry) för mer information.

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam3.png)

   >[!NOTE]
   >
   >Namnet måste följa samma konventioner som en AEM nod så det får inte innehålla något av följande tecken: . / : [ ] | *

1. Nu bör du se din migreringslista i listvyn. Markera symbolen med tre punkter (**...**) för att öppna listrutan och välja **Kopiera extraheringsnyckel**. Du behöver den här nyckeln under extraheringsfasen. Kopiera den här extraheringsnyckeln.

   >[!NOTE]
   >
   >Extraheringsnyckeln gör att AEM kan ansluta säkert till migreringsuppsättningen. Behandla den här nyckeln med samma noggrannhet som du skulle ha gjort med ett lösenord och dela det aldrig på ett osäkert medium som e-post.

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam4.png)

### Fyller i migreringsuppsättningen {#populating-the-migration-set}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_populate_migrationset"
>title="Fyll i migreringsuppsättning"
>abstract="När du har skapat en migreringsuppsättning måste den fyllas i med innehållet från källinstansen som måste flyttas till den AEM as a Cloud Service miljön. För att göra detta måste verktyget Innehållsöverföring vara installerat på källinstansen."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/extracting-content.html" text="Extraherar innehåll"

Om du vill fylla i den migreringsuppsättning du skapade i Cloud Acceleration Manager installerar du den senaste versionen av verktyget Innehållsöverföring på din Adobe Experience Manager-källinstans (AEM). Följ det här avsnittet om du vill lära dig hur du fyller i migreringsuppsättningen.

1. När du har installerat den senaste versionen av verktyget Innehållsöverföring på Adobe Experience Manager-källinstansen går du till **Åtgärder - innehållsmigrering**

1. Klicka **Skapa migreringsuppsättning**.

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam5.png)

1. Klistra in extraheringsnyckeln som kopierades från CAM tidigare i indatafältet för extraheringsnyckeln i **Skapa migreringsuppsättning** formulär. När du har gjort det fylls namnen på migreringsuppsättningen och CAM-projektnamnen i automatiskt. Dessa ska matcha namnet på migreringsuppsättningen i CAM och namnet på CAM-projektet som du skapade. Nu kan du lägga till innehållssökvägar. Spara migreringsuppsättningen när du har lagt till innehållssökvägar. Du kan köra extraheringen med antingen versioner inkluderade eller exkluderade.

   >[!NOTE]
   >
   >Kontrollera att extraheringsnyckeln är giltig och att den inte är i närheten av utgångsdatumet. Du kan hämta den här informationen i **Skapa migreringsuppsättning** när du har klistrat in extraheringsnyckeln. Om du får ett anslutningsfel kan du läsa [Anslutning för källmiljö](#source-environment-connectivity) för mer information.

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam6.png)

1. Välj sedan följande parametrar för att skapa en migreringsuppsättning:

   1. **Inkludera version**: Välj det som behövs. När versioner inkluderas, banan `/var/audit` inkluderas automatiskt för att migrera granskningshändelser.

      ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam7.png)

      >[!NOTE]
      >Om du tänker ta med versioner som en del av en migreringsuppsättning och utför uppsättningar med `wipe=false`måste du inaktivera versionsrensning på grund av en aktuell begränsning i verktyget Innehållsöverföring. Om du föredrar att behålla versionsrensning aktiverad och utför summeringar i en migreringsuppsättning, måste du utföra inmatningen som `wipe=true`.


   1. **Banor som ska inkluderas**: Använd sökvägsläsaren för att välja sökvägar som ska migreras. Banväljaren accepterar indata genom att skriva eller genom att välja.

      >[!IMPORTANT]
      >Följande sökvägar är begränsade när du skapar en migreringsuppsättning:
      >* `/apps`
      >* `/libs`
      >* `/home`
      >* `/etc` (vissa `/etc` banor kan markeras i CTT)

1. Klicka **Spara** när du har fyllt i alla fält i **Skapa migreringsuppsättning** informationsskärmen.

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

* Kontrollera om det finns tillräckligt med diskutrymme i `crx-quickstart` underkatalog för att slutföra extraheringen.
* Kontrollera om migreringsuppsättningens storlek ligger inom de produktgränser som stöds och undvik misslyckade innehållsfrågor.

Följ stegen nedan för att göra en storlekskontroll:

1. Välj en migreringsuppsättning och klicka på **Kontrollera storlek**.

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam8.png)

1. Då öppnas **Kontrollera storlek** -dialogrutan.

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam9.png)

1. Klicka **Kontrollera storlek** för att starta processen. Du kommer sedan tillbaka till vyn med migreringsuppsättningslistor och du bör se ett meddelande som anger att **Kontrollera storlek** är igång.

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam10.png)

1. Efter **Kontrollera storlek** processen är slutförd, statusen ändras till **SLUTFÖRD**. Välj samma migreringsuppsättning och klicka på **Kontrollera storlek** för att visa resultaten. Nedan visas ett exempel på **Kontrollera storlek** resultat utan varningar.

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam11.png)

1. Om **Kontrollera storlek** resultatet visar att det antingen inte finns tillräckligt med diskutrymme eller att migreringsuppsättningen överskrider produktgränserna, eller både och **VARNING** status visas.

<!--   ![image](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image6.png)
   
   Below is an example of **Check Size** results with warnings.
 
   ![image](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image7.png) -->


## What&#39;s Next {#whats-next}

När du har lärt dig hur du skapar en migreringsuppsättning kan du nu lära dig mer om extraherings- och inmatningsprocesser i verktyget Innehållsöverföring. Innan du lär dig dessa processer måste du granska [Hantera stora innehållsdatabaser](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md) för att avsevärt snabba upp extraherings- och intagsfaserna i innehållsöverföringsaktiviteten för att flytta innehåll till AEM as a Cloud Service.

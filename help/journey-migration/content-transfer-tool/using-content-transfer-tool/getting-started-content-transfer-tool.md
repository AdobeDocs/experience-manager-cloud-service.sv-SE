---
title: Komma igång med verktyget Innehållsöverföring
description: Komma igång med verktyget Innehållsöverföring
exl-id: c0cecf65-f419-484b-9d55-3cbd561e8dcd
source-git-commit: 7bebdff5095786005d5c4c91b7b699d71f9813a7
workflow-type: tm+mt
source-wordcount: '1341'
ht-degree: 6%

---

# Komma igång med verktyget Innehållsöverföring {#getting-started-content-transfer-tool}


## Tillgänglighet {#availability}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_download"
>title="Hämta"
>abstract="Innehållsöverföringsverktyget kan laddas ned som en zip-fil från Software Distribution Portal. Du kan installera paketet via pakethanteraren på din källinstans av Adobe Experience Manager (AEM). Glöm inte att hämta den senaste versionen."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html" text="Versionsinformation"
>additional-url="https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html" text="Programdistributionsportal"

Innehållsöverföringsverktyget kan laddas ned som en zip-fil från Software Distribution Portal. Du kan installera paketet via [Pakethanteraren](/help/implementing/developing/tools/package-manager.md) på din källinstans av Adobe Experience Manager (AEM). Glöm inte att hämta den senaste versionen. Mer information om den senaste versionen finns i [Versionsinformation](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html).

>[!NOTE]
>Hämta Content Transfer Tool från [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)-portalen.

## Anslutning för källmiljö {#source-environment-connectivity}

>[!NOTE]
>
>Ett anslutningsfel kan också uppstå om en migreringsuppsättning har tagits bort från Cloud Acceleration Manager.

Källinstansen AEM kanske köras bakom en brandvägg där den bara kan nå vissa värdar som har lagts till i Tillåtelselista. För att en extrahering ska kunna köras måste följande slutpunkter vara tillgängliga från den instans som körs AEM:

* Målet AEM den as a Cloud Service miljön: `author-p<program_id>-e<env_id>.adobeaemcloud.com`
* Azure-blobblagringstjänsten: `*.blob.core.windows.net`
* I/O-slutpunkten för användarmappning: `usermanagement.adobe.io`

Om du vill testa anslutningen till AEM as a Cloud Service målmiljön skickar du följande cURL-kommando från skalet för källinstansen (ersätt `program_id`, `environment_id`och `migration_token`):

`curl -i https://author-p<program_id>-e<environment_id>.adobeaemcloud.com/api/migration/migrationSet -H "Authorization: Bearer <migration_token>"`

>[!NOTE]
>Om en `HTTP/2 200` har tagits emot har en anslutning till AEM as a Cloud Service upprättats.

### Aktivera SSL-loggning {#enable-ssl-logging}

Det kan vara svårt att förstå SSL-/TLS-anslutningsproblem. Om du vill felsöka anslutningsproblem under en extraheringsprocess kan du aktivera SSL-loggning via systemkonsolen i AEM genom att följa dessa steg:

1. Navigera till Adobe Experience Manager Web Console i källinstansen genom att gå till **Verktyg - Åtgärder - Webbkonsol** eller direkt till URL:en på *https://serveraddress:serverport/system/console/configMgr*
1. Sök efter **Konfiguration av extraheringstjänst för innehållsöverföringsverktyg**
1. Använd pennikonknappen för att redigera dess konfigurationsvärden
1. Aktivera **Aktivera SSL-loggning för extrahering** ställa in och sedan trycka **Spara**:

   ![bild](/help/journey-migration/content-transfer-tool/assets/enable_ssl_logging.png)


## Köra Content Transfer Tool {#running-tool}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_demo"
>title="Verktyget Innehållsöverföring körs"
>abstract="Lär dig hur du använder verktyget Innehållsöverföring för att migrera innehållet till AEM as a Cloud Service (Författare/Publicera)."
>additional-url="https://video.tv.adobe.com/v/35460/?quality=12&amp;learn=on" text=" Se demo"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/migration/content-transfer-tool.html?lang=en#migration" text="Självstudiekurs - använda verktyget Innehållsöverföring"

>[!VIDEO](https://video.tv.adobe.com/v/35460/?quality=12&learn=on)
<!-- Need to remove the video -->

Följande avsnitt gäller för den nya versionen av verktyget Innehållsöverföring. Följ det här avsnittet för att lära dig hur du använder verktyget Innehållsöverföring för att migrera innehåll till AEM as a Cloud Service:

### Installationsfas för extrahering {#extraction-setup-phase}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_extraction_setup"
>title="Installationsfas för extrahering"
>abstract="Lär dig hur du skapar en migreringsuppsättning och kopierar extraheringsnyckeln."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/migration/content-transfer-tool.html?lang=en#migration" text="Självstudiekurs - använda verktyget Innehållsöverföring"

<!-- Contextualhelp id "aemcloud_ctt_extraction_setup" needs to be added here -->

1. Logga in på CAM (Cloud Acceleration Manager) och klicka på CAM-projektet som du skapat tidigare för att utvärdera om du är redo att gå AEM as a Cloud Service. Om du inte har skapat något CAM-projekt, se Skapa och hantera ett projekt i CAM.

1. Klicka på **Innehållsöverföring** kort. Du kommer nu till vyn Migreringsuppsättningslista.

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam1.png)

1. Skapa en migreringsuppsättning genom att klicka på **Skapa migreringsuppsättning**.

   >[!NOTE]
   >
   >Högst fem migreringsuppsättningar kan skapas per projekt i Cloud Acceleration Manager.

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam2.png)

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam3.png)

1. Nu bör du se din migreringslista i listvyn. Klicka på symbolen med tre punkter (**...**) för att öppna listrutan och klicka på **Kopiera extraheringsnyckel**. Du behöver den här nyckeln under extraheringsfasen. Kopiera den här extraheringsnyckeln.

   >[!NOTE]
   >
   >Extraheringsnyckeln gör att AEM kan ansluta säkert till migreringsuppsättningen. Behandla den här nyckeln med samma omsorg som du gör om ett lösenord och dela det aldrig på ett osäkert medium som e-post.

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam4.png)

### Fyller i migreringsuppsättningen {#populating-the-migration-set}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_populate_migrationset"
>title="Fyll i migreringsuppsättning&quot; abstract=&quot;När du har skapat en migreringsuppsättning måste den fyllas i med innehållet från källinstansen som måste flyttas till den AEM as a Cloud Service miljön. För att göra detta måste verktyget Innehållsöverföring vara installerat på källinstansen."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/extracting-content.html" text="Extraherar innehåll"

Om du vill fylla i den migreringsuppsättning du skapade i Cloud Acceleration Manager måste du installera den senaste versionen av verktyget för innehållsöverföring på din Adobe Experience Manager-källinstans (AEM). Följ det här avsnittet för att lära dig hur du fyller i migreringsuppsättningen.

1. När du har installerat den senaste versionen (v2.0.10) av verktyget Innehållsöverföring på din Adobe Experience Manager-källinstans går du till **Åtgärder - innehållsmigrering**

1. Klicka på **Skapa migreringsuppsättning**

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam5.png)

1. Klistra in extraheringsnyckeln som kopierades från CAM tidigare i indatafältet för extraheringsnyckeln i **Skapa migreringsuppsättning** formulär. När du gör det fylls fälten för migreringsuppsättningens namn och projektnamnet för Cloud Acceleration Manager (CAM) automatiskt i. Dessa ska matcha namnet på migreringsuppsättningen i CAM och namnet på CAM-projektet som du skapade. Nu kan du lägga till innehållssökvägar. När du har lagt till innehållssökvägar kan du spara migreringsuppsättningen. Du kan köra extraheringen med antingen versioner inkluderade eller exkluderade.

   >[!NOTE]
   >
   >Kontrollera att extraheringsnyckeln är giltig och att den inte ligger nära utgångsdatumet. Du kan hämta den här informationen i **Skapa migreringsuppsättning** när du har klistrat in extraheringsnyckeln. Om du får ett anslutningsfel kan du läsa [Anslutning för källmiljö](#source-environment-connectivity) för mer information.

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam6.png)

1. Välj sedan följande parametrar för att skapa en migreringsuppsättning:

   1. **Include Version**: Välj det som behövs. När versioner inkluderas, banan `/var/audit` inkluderas automatiskt för att migrera granskningshändelser.

      ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam7.png)

      >[!NOTE]
      >Om du tänker ta med versioner som en del av en migreringsuppsättning och utför uppsättningar med `wipe=false`måste du inaktivera versionsrensning på grund av en aktuell begränsning i verktyget Innehållsöverföring. Om du föredrar att behålla versionsrensning aktiverad och utför summeringar i en migreringsuppsättning, måste du utföra inmatningen som `wipe=true`.


   1. **Paths to be included**: Använd sökvägsläsaren för att välja sökvägar som behöver migreras. Banväljaren accepterar indata genom att skriva eller genom att välja.

      >[!IMPORTANT]
      >Följande sökvägar är begränsade när du skapar en migreringsuppsättning:
      >* `/apps`
      >* `/libs`
      >* `/home`
      >* `/etc` (vissa `/etc` banor kan markeras i CTT)


1. Klicka på **Spara** när du har fyllt i alla fält i **Skapa migreringsuppsättning** informationsskärmen.

<!-- 1. You will view your migration set in the **Content Transfer** wizard, as shown in the figure below.

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/ctt07.png)

   All the existing migration sets are displayed on the **Content Transfer** wizard with their current status and status information. You may see some of these icons described below.

   * A *red cloud* indicates that you cannot complete the extraction process.
   * A *green cloud* indicates that you can complete the extraction process.
   * A *yellow icon* indicates that you did not create the existing migration set and the specific one is created by some other user in the same instance.

1. Select a migration set and click on **Properties** to view or edit the migration set properties. While editing properties, it is not possible to change the **Migration Set name** or the **Service URL**. 

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/ctt06.png) -->

### Bestämma migreringsuppsättningens storlek {#migration-set-size}

När du har skapat en migreringsuppsättning rekommenderar vi att du kör en storlekskontroll på migreringsuppsättningen innan du startar en extraheringsprocess.
Genom att köra en storlekskontroll på migreringsuppsättningen kan du:
* Kontrollera om det finns tillräckligt med diskutrymme i `crx-quickstart` underkatalog för att slutföra extraheringen.
* Kontrollera om migreringsuppsättningens storlek ligger inom de produktgränser som stöds och undvik misslyckade innehållsfrågor.

Följ stegen nedan för att göra en storlekskontroll:

1. Välj en migreringsuppsättning och klicka på **Kontrollera storlek**.

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam8.png)

1. Detta öppnar **Kontrollera storlek** -dialogrutan.

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam9.png)

1. Klicka på **Kontrollera storlek** för att starta processen. Du kommer sedan tillbaka till vyn med migreringsuppsättningslistor och du bör se ett meddelande som anger att **Kontrollera storlek** är igång.

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam10.png)

1. En gång **Kontrollera storlek** processen är slutförd, statusen ändras till **SLUTFÖRD**. Välj samma migreringsuppsättning och klicka på **Kontrollera storlek** för att visa resultaten. Nedan visas ett exempel på **Kontrollera storlek** resultat utan varningar.

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam11.png)

1. Om **Kontrollera storlek** resultaten visar att det antingen inte finns tillräckligt med diskutrymme och/eller att migreringsuppsättningen överskrider produktgränserna, **VARNING** status visas.

<!--   ![image](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image6.png)
   
   Below is an example of **Check Size** results with warnings.
 
   ![image](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image7.png) -->


## What&#39;s Next {#whats-next}

När du har lärt dig hur du skapar en migreringsuppsättning kan du nu lära dig mer om extraherings- och inmatningsprocesser i verktyget Innehållsöverföring. Innan du lär dig dessa processer måste du granska [Hantera stora innehållsdatabaser](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en) för att avsevärt snabba upp extraherings- och intagsfaserna i innehållsöverföringsaktiviteten för att flytta innehåll till AEM as a Cloud Service.

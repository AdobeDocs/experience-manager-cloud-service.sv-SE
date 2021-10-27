---
title: Komma igång med verktyget Innehållsöverföring
description: Komma igång med verktyget Innehållsöverföring
exl-id: a19b8424-33ab-488a-91b3-47f0d3c8abf5
source-git-commit: 2ff6f6be922c3c6a1d13945a4cd1c4d927829186
workflow-type: tm+mt
source-wordcount: '860'
ht-degree: 27%

---

# Komma igång med verktyget Innehållsöverföring {#getting-started-content-transfer-tool}

## Anslutning för källmiljö

Källinstansen AEM kanske köras bakom en brandvägg där den bara kan nå vissa värdar som har lagts till i Tillåtelselista. För att en extrahering ska kunna köras måste följande slutpunkter vara tillgängliga från den instans som körs AEM:

* Målet AEM den as a Cloud Service miljön:
   `author-p<program_id>-e<env_id>.adobeaemcloud.com`
* Azure-blobblagringstjänsten:
   `*.blob.core.windows.net`
* I/O-slutpunkten för användarmappning:
   `usermanagement.adobe.io`

Om du vill testa anslutningen till AEM as a Cloud Service målmiljön skickar du följande cURL-kommando från skalet för källinstansen (ersätt `program_id`, `environment_id`och `migration_token`):

```
curl -i https://author-p<program_id>-e<environment_id>.adobeaemcloud.com/api/migration/migrationSet -H "Authorization: Bearer <migration_token>"
```

Om en `HTTP/2 200` har tagits emot har en anslutning till AEM as a Cloud Service upprättats.

## Tillgänglighet {#availability}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_download"
>title="Hämta"
>abstract="Innehållsöverföringsverktyget kan laddas ned som en zip-fil från Software Distribution Portal. Du kan installera paketet via pakethanteraren på din källinstans av Adobe Experience Manager (AEM). Glöm inte att hämta den senaste versionen."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html" text="Versionsinformation"
>additional-url="https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html" text="Programdistributionsportal"

Innehållsöverföringsverktyget kan laddas ned som en zip-fil från Software Distribution Portal. Du kan installera paketet via pakethanteraren på din källinstans av Adobe Experience Manager (AEM). Glöm inte att hämta den senaste versionen. Mer information om den senaste versionen finns i [Versionsinformation](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html).

>[!NOTE]
>Hämta Content Transfer Tool från [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)-portalen.

## Köra Content Transfer Tool {#running-tool}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_demo"
>title="Verktyget Innehållsöverföring körs"
>abstract="Lär dig hur du använder verktyget Innehållsöverföring för att migrera innehållet till AEM as a Cloud Service (Författare/Publicera)."
>additional-url="https://video.tv.adobe.com/v/35460/?quality=12&amp;learn=on" text=" Se demo"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/migration/content-transfer-tool.html?lang=en#migration" text="Självstudiekurs - använda verktyget Innehållsöverföring"

>[!VIDEO](https://video.tv.adobe.com/v/35460/?quality=12&learn=on)


Följ det här avsnittet för att lära dig hur du använder Content Transfer Tool för att migrera innehållet till AEM as a Cloud Service (Author/Publish):

1. Markera Adobe Experience Manager och gå till verktygen -> **Operationer** -> **Innehållsmigrering**.

   ![bild](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/ctt01.png)

1. Välj **Innehållsöverföring** alternativ från **Innehållsmigrering** guide.

   ![bild](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/ctt02.png)


1. Konsolen nedan visas när du skapar den första migreringsuppsättningen. Klicka på **Create Migration Set** om du vill skapa en ny migreringsuppsättning.

   ![bild](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/ctt03.png)

   >[!NOTE]
   >Om du har befintliga migreringsuppsättningar visas en lista med befintliga migreringsuppsättningar med aktuell status.


1. Fyll i fälten i **Skapa migreringsuppsättning** skärm enligt beskrivningen nedan.

   ![bild](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/ctt04.png)

   1. **Name**: Ange namnet på migreringsuppsättningen.
      >[!NOTE]
      >Inga specialtecken tillåts för migreringsuppsättningens namn.

   1. **Cloud Service Configuration**: Ange målförfattar-URL för AEM as a Cloud Service.

      >[!NOTE]
      >Du kan skapa och underhålla högst tio migreringsuppsättningar åt gången under innehållsöverföringsaktiviteten.
      >Dessutom måste du skapa en migrering separat för varje specifik miljö – *Stage*, *Development* eller *Production*.

   1. **Access Token**: Ange åtkomsttoken.

      >[!NOTE]
      >Du kan hämta åtkomsttoken med **Öppen åtkomsttoken** -knappen. Du måste kontrollera att du tillhör gruppen AEM administratörer i målinstansen av Cloud Service.

   1. **Parameters**: Välj följande parametrar för att skapa migreringsuppsättningen:

      1. **Include Version**: Välj det som behövs. När versioner inkluderas, banan `/var/audit` inkluderas automatiskt för att migrera granskningshändelser.

         ![bild](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/ctt05.png)

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

1. Du kan visa din migreringsuppsättning i **Innehållsöverföring** guiden, enligt bilden nedan.

   ![bild](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/ctt07.png)

   Alla befintliga migreringsuppsättningar visas på **Innehållsöverföring** guide med aktuell status- och statusinformation. Du kan se några av dessa ikoner som beskrivs nedan.

   * Ett *rött moln* anger att du inte kan slutföra extraheringsprocessen.
   * A *grönt moln* anger att du kan slutföra extraheringsprocessen.
   * En *gul ikon* anger att du inte har skapat den befintliga migreringsuppsättningen och att den specifika skapas av en annan användare i samma instans.

1. Välj en migreringsuppsättning och klicka på **Egenskaper** om du vill visa eller redigera migreringsuppsättningens egenskaper. När du redigerar egenskaper går det inte att ändra **Namn på migreringsuppsättning** eller **Tjänst-URL**.

   ![bild](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/ctt06.png)


## What&#39;s Next {#whats-next}

När du har lärt dig hur du skapar en migreringsuppsättning kan du nu lära dig mer om extraherings- och inmatningsprocesser i verktyget Innehållsöverföring. Innan du lär dig dessa processer måste du granska [Hantera stora innehållsdatabaser](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en) för att avsevärt snabba upp extraherings- och intagsfaserna i innehållsöverföringsaktiviteten för att flytta innehåll till AEM as a Cloud Service.

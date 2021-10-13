---
title: Komma igång med verktyget Innehållsöverföring
description: Komma igång med verktyget Innehållsöverföring
exl-id: a19b8424-33ab-488a-91b3-47f0d3c8abf5
source-git-commit: eae5b6a8903f68d4736e44db9a9e598716a15b75
workflow-type: tm+mt
source-wordcount: '776'
ht-degree: 30%

---

# Komma igång med verktyget Innehållsöverföring {#getting-started-content-transfer-tool}

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

1. Markera Adobe Experience Manager och navigera till verktyg -> **Åtgärder** -> **Innehållsmigrering**.

   ![bild](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/ctt01.png)

1. Välj alternativet **Innehållsöverföring** i guiden **Innehållsmigrering**.

   ![bild](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/ctt02.png)


1. Konsolen nedan visas när du skapar den första migreringsuppsättningen. Klicka på **Create Migration Set** om du vill skapa en ny migreringsuppsättning.

   ![bild](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/ctt03.png)

   >[!NOTE]
   >Om du har befintliga migreringsuppsättningar visas en lista med befintliga migreringsuppsättningar med aktuell status.


1. Fyll i fälten på **skärmen Skapa migreringsuppsättning** enligt beskrivningen nedan.

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
      >Du kan hämta åtkomsttoken med knappen **Öppna åtkomsttoken**. Du måste kontrollera att du tillhör gruppen AEM administratörer i målinstansen av Cloud Service.

   1. **Parameters**: Välj följande parametrar för att skapa migreringsuppsättningen:

      1. **Include Version**: Välj det som behövs. När versioner inkluderas inkluderas sökvägen `/var/audit` automatiskt för att migrera granskningshändelser.

      ![bild](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/ctt05.png)

      >[!NOTE]
      >Om du tänker ta med versioner som en del av en migreringsuppsättning och utför uppsättningar med `wipe=false`, måste du inaktivera versionsrensning på grund av en aktuell begränsning i verktyget Innehållsöverföring. Om du föredrar att behålla versionsrensning aktiverad och utför toppuppsättningar i en migreringsuppsättning, måste du utföra intaget som `wipe=true`.

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

1. Du kommer att visa din migreringsuppsättning i guiden **Innehållsöverföring**, vilket visas i bilden nedan.

   ![bild](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/ctt07.png)

   Alla befintliga migreringsuppsättningar visas i guiden **Innehållsöverföring** med aktuell status- och statusinformation. Du kan se några av dessa ikoner som beskrivs nedan.

   * Ett *rött moln* anger att du inte kan slutföra extraheringsprocessen.
   * Ett *grönt moln* anger att du kan slutföra extraheringsprocessen.
   * En *gul ikon* anger att du inte har skapat den befintliga migreringsuppsättningen och att den specifika skapas av en annan användare i samma instans.

1. Välj en migreringsuppsättning och klicka på **Egenskaper** för att visa eller redigera migreringsuppsättningsegenskaperna. När du redigerar egenskaper går det inte att ändra **migreringsuppsättningens namn** eller **tjänst-URL**.

   ![bild](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/ctt06.png)


## What&#39;s Next {#whats-next}

När du har lärt dig hur du skapar en migreringsuppsättning kan du nu lära dig mer om extraherings- och inmatningsprocesser i verktyget Innehållsöverföring. Innan du lär dig dessa processer måste du granska [Hantera stora innehållsdatabaser](help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md) för att avsevärt snabba upp extraherings- och intagsfaserna i innehållsöverföringsaktiviteten så att innehållet flyttas till AEM as a Cloud Service.

---
title: Inmatning av innehåll i mål (äldre)
description: Infoga innehåll i mål
hide: true
hidefromtoc: true
source-git-commit: 1fb4d0f2a3b3f9a27f5ab1228ec2d419149e0764
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 26%

---

# Inmatning av innehåll i mål (äldre) {#ingesting-content}

## Inmatningsprocess i verktyget Innehållsöverföring {#ingestion-process}

Följ stegen nedan för att importera migreringsuppsättningen från Content Transfer Tool:
>[!NOTE]
>Du kan köra det valfria förkopieringssteget för att avsevärt snabba upp intagningsfasen. Se [Ingesting with AzCopy](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en#ingesting-azcopy) för mer information.

1. Välj en migreringsuppsättning från **Innehållsöverföring** sida och klicka **Ingest** för att börja intag.

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-01.png)

1. Dialogrutan **Migration Set ingestion** visas. Innehållet kan importeras till antingen Author-instansen eller Publish-instansen åt gången. Markera instansen som du vill importera innehåll till. Klicka på **Ingest** för att starta matningsfasen.

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-02.png)

   >[!IMPORTANT]
   >Om du använder inmatning med förkopia (för S3 eller Azure Data Store) bör du endast köra Author-intagning. Detta snabbar upp inläsningen av publiceringen när den körs senare.

   >[!IMPORTANT]
   >När **Rensa befintligt innehåll i molninstansen före intag** om du aktiverar det här alternativet tas hela den befintliga databasen bort och en ny databas skapas där innehållet kan importeras till. Det innebär att alla inställningar återställs, inklusive behörigheter för målinstansen av Cloud Servicen. Detta gäller även för en admin-användare som har lagts till i **administratörer** grupp.

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-03.png)

   Klicka på **Kundtjänst** att logga en biljett, vilket visas i figuren nedan.

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-04.png)

   Se även [Viktigt att tänka på när du använder verktyget Innehållsöverföring](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html?lang=en#important-considerations) om du vill veta mer.

1. När intaget är slutfört är statusen under **Intag av författare** uppdateringar till **SLUTFÖRD**.

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-05.png)

## Uppdatera inmatning {#top-up-ingestion-process}

Content Transfer Tool har en funktion för differentiell *innehållsuppdatering* som gör att du kan överföra enbart de ändringar som gjorts sedan den föregående innehållsöverföringen.

>[!NOTE]
>Efter den första innehållsöverföringen bör du göra regelbundna tillägg av differentiellt innehåll för att förkorta innehållets frysningsperiod för den slutliga differentiella innehållsöverföringen innan du börjar använda Cloud Service.

När inmatningen är klar kan du använda delta-innehåll med hjälp av inmatningsmetoden för uppdateringar. Följ stegen nedan:

1. Navigera till **Innehållsöverföring** och välj den migreringsuppsättning som du vill utföra det övre intaget för. Klicka på **Ingest** för att starta uppdateringsextraheringen.

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/topup-ingest1.png)


1. Dialogrutan **Migration Set ingestion** visas.

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/topup-ingest2.png)

   >[!IMPORTANT]
   >Du bör inaktivera **Rensa befintligt innehåll i molninstansen före intag** om du vill förhindra att befintligt innehåll tas bort från den tidigare importen. Klicka på **Kundtjänst** för att logga en biljett, vilket visas i föregående bild.

## What&#39;s Next {#whats-next}

När du har lärt dig Inkludera innehåll i mål i verktyget för innehållsöverföring kan du visa loggar när varje steg har slutförts (extrahering och förtäring) och leta efter fel. Se [Visa loggar för en migreringsuppsättning](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/viewing-logs.html?lang=en) om du vill veta mer.

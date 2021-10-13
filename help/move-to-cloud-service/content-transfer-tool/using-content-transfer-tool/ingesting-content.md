---
title: Infoga innehåll i mål i verktyget Innehållsöverföring
description: Infoga innehåll i mål i verktyget Innehållsöverföring
source-git-commit: 65847fc03770fe973c3bfee4a515748f7e487ab6
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 34%

---


# Infoga innehåll i mål i verktyget Innehållsöverföring {#ingesting-content}

## Inmatningsprocess i verktyget Innehållsöverföring {#ingestion-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion"
>title="Innehållsintag"
>abstract="Inmatning avser att hämta innehåll från migreringsuppsättningen till målinstansen för Cloud Service. Content Transfer Tool har en funktion för differentiell innehållsuppdatering som gör att du kan överföra enbart de ändringar som gjorts sedan den föregående innehållsöverföringen."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#top-up-ingestion-process" text="Uppdatera inmatning"

Följ stegen nedan för att importera migreringsuppsättningen från Content Transfer Tool:
>[!NOTE]
>Om Amazon S3 eller Azure Data Store används som typ av datalager kan du köra det valfria förkopieringssteget för att avsevärt snabba upp inmatningsfasen. Mer information finns i [Ingesting with AzCopy](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en#ingesting-azcopy).

1. Välj en migreringsuppsättning på sidan *Översikt* och klicka på **Infoga** för att starta importen. Dialogrutan **Migration Set ingestion** visas. Innehållet kan importeras till antingen Author-instansen eller Publish-instansen åt gången. Markera instansen som du vill importera innehåll till. Klicka på **Ingest** för att starta intagningsfasen.

   >[!IMPORTANT]
   >Om du använder inmatning med förkopia (för S3 eller Azure Data Store) bör du endast köra Author-intagning. Detta snabbar upp inläsningen av publiceringen när den körs senare.

   >[!IMPORTANT]
   >När alternativet **Rensa befintligt innehåll i molninstansen innan inmatning** är aktiverat, tas hela den befintliga databasen bort och en ny databas skapas för inmatning av innehåll i. Det innebär att alla inställningar återställs, inklusive behörigheter för målinstansen av Cloud Servicen. Detta gäller även för en admin-användare som har lagts till i gruppen **administratörer**.

   ![bild](/help/move-to-cloud-service/content-transfer-tool/assets/content-ingestion-03.png)

   Klicka på **Kundtjänst** för att logga en biljett, vilket visas i bilden ovan. Se även [Viktiga överväganden för att använda verktyget Innehållsöverföring](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html?lang=en#important-considerations) om du vill veta mer.

1. När importen är klar uppdateras statusen till **FINISHED**.

   ![bild](/help/move-to-cloud-service/content-transfer-tool/assets/15-ingestion-complete.png)

## Uppdatera inmatning {#top-up-ingestion-process}

Content Transfer Tool har en funktion för differentiell *innehållsuppdatering* som gör att du kan överföra enbart de ändringar som gjorts sedan den föregående innehållsöverföringen.

>[!NOTE]
>
>Efter den första innehållsöverföringen bör du göra regelbundna tillägg av differentiellt innehåll för att förkorta innehållets frysningsperiod för den slutliga differentiella innehållsöverföringen innan du börjar använda Cloud Service.

När inmatningen är klar kan du använda delta-innehåll med hjälp av inmatningsmetoden för uppdateringar. Följ stegen nedan:

1. Navigera till sidan *Overview* och välj den migreringsuppsättning som du vill utföra uppdateringsinmatningen för. Klicka på **Ingest** för att starta uppdateringsextraheringen. Dialogrutan **Migration Set ingestion** visas.

   ![bild](/help/move-to-cloud-service/content-transfer-tool/assets/content-ingestion-02.png)

   >[!IMPORTANT]
   >Du bör inaktivera alternativet **Rensa befintligt innehåll i molninstansen före intag**, för att förhindra att befintligt innehåll tas bort från den tidigare intagsaktiviteten. Klicka på **Kundtjänst** för att logga en biljett, vilket visas i föregående bild.

---
title: Extraherar innehåll från källa
description: Extraherar innehåll från källa
source-git-commit: fa7e5d07ed52a71999de95bbf6299ae5eb7af537
workflow-type: tm+mt
source-wordcount: '518'
ht-degree: 42%

---


# Extraherar innehåll från källa {#extracting-content}

## Extraheringsprocess i verktyget Innehållsöverföring {#extraction-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_extraction"
>title="Content Extraction"
>abstract="Extrahering avser att extrahera innehåll från AEM till ett temporärt område som kallas migreringsuppsättning. En migreringsuppsättning är ett molnlagringsutrymme som finns hos Adobe för att tillfälligt lagra det överförda innehållet mellan AEM-källinstansen och Cloud Service AEM-instansen."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#top-up-extraction-process" text="Extrahering uppifrån"

Följ stegen nedan för att extrahera migreringsuppsättningen från Content Transfer Tool:
>[!NOTE]
>Om Amazon S3 eller Azure Data Store används som typ av datalager kan du köra det valfria förkopieringssteget för att avsevärt snabba upp extraheringsfasen. To do so you will need to configure an `azcopy.config` file before running extraction. Mer information finns i [Hantera stora innehållsdatabaser](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en).

1. Select a migration set from **Content Transfer** wizard and click **Extract** to start extraction.

   ![bild](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/extraction-01.png)

1. The **Migration Set extraction** dialog box displays and click on **Extract** to start the extraction phase.

   ![bild](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/extraction-02.png)

   >[!NOTE]
   >Du kan skriva över mellanlagringsbehållaren under extraheringsfasen.

1. Fältet **Extrahering** visar nu statusen **RUNNING** för att ange att extraheringen pågår.

   ![bild](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/extraction-03.png)

   När extraheringen är klar uppdateras migreringsuppsättningens status till **FINISHED** och en *solid grön* molnikon visas under **INFO**-fältet.

   ![bild](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/extraction-04.png)

   >[!IMPORTANT]
   >Användargränssnittet har en funktion för automatisk inläsning som laddar om guiden **Innehållsöverföring** var 30:e sekund.
   >När extraheringsfasen startas skapas ett skrivlås som frisläpps efter *60 sekunder*. Om extraheringen avbryts måste du alltså vänta en minut på att låset ska frisläppas innan du startar extraheringen igen.

## Uppdateringsextrahering {#top-up-extraction-process}

Content Transfer Tool har en funktion för differentiell innehållsuppdatering som gör att du kan överföra enbart de ändringar som gjorts sedan den föregående innehållsöverföringen.

>[!NOTE]
>Efter den första innehållsöverföringen bör du göra regelbundna tillägg av differentiellt innehåll för att förkorta innehållets frysningsperiod för den slutliga differentiella innehållsöverföringen innan du börjar använda Cloud Service.
>Additionally, it is essential that the content structure of existing content is not changed from the time the initial extraction is taken to when the top-up extraction is run. Det går inte att köra uppsättningar på innehåll vars struktur har ändrats sedan den första extraheringen. Kontrollera att du begränsar detta under migreringsprocessen.

När extraheringen är klar kan du överföra delta-innehåll med extraheringsmetoden för uppdateringar.

Följ stegen nedan:

1. Navigate to the **Content Transfer** wizard and select the migration set for which you want to perform the top-up extraction. Klicka på **Extract** för att starta uppdateringsextraheringen.

   ![bild](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/extraction-05.png)

1. The **Migration Set extraction** dialog box displays. Click on **Extract**.

   >[!IMPORTANT]
   >Du bör inaktivera alternativet **Overwrite staging container during extraction**.
   >![bild](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/extraction-06.png)


## What&#39;s Next {#whats-next}

När du har lärt dig hur du extraherar innehåll från källan i verktyget Innehållsöverföring är du nu redo att lära dig Inmatningsprocessen i verktyget Innehållsöverföring. Se [Inkludera innehåll i mål](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool/ingesting-content.md) för att lära dig hur du importerar din migreringsuppsättning från verktyget Innehållsöverföring.

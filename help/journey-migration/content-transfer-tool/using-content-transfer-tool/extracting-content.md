---
title: Extrahera innehåll från Source
description: Lär dig hur du extraherar innehåll från en Adobe Experience Manager-källinstans (AEM) och senare överför det till en Cloud Service AEM-instans.
exl-id: c5c08c4e-d5c3-4a66-873e-96986e094fd3
feature: Migration
role: Admin
source-git-commit: d568619bd8ebb42a6914211401df680352c921ab
workflow-type: tm+mt
source-wordcount: '789'
ht-degree: 8%

---

# Extrahera innehåll från Source {#extracting-content}

## Extraheringsprocess i verktyget Innehållsöverföring {#extraction-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_extraction"
>title="Innehållsextrahering"
>abstract="Extrahering avser att extrahera innehåll från Adobe Experience Manager-källinstansen (AEM) till ett tillfälligt område som kallas migreringsuppsättning. En migreringsuppsättning är ett molnlagringsutrymme som tillhandahålls av Adobe för att tillfälligt lagra det överförda innehållet mellan AEM-källinstansen och Cloud Service AEM-instansen."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html#top-up-extraction-process" text="Extrahering uppifrån"


Följ stegen nedan för att extrahera migreringsuppsättningen från Content Transfer Tool:

>[!NOTE]
>Om Amazon S3, Azure Data Store eller File Data Store används som typ av datalager kan du köra det valfria förkopieringssteget för att öka extraheringsfasens hastighet. Steg före kopiering är mest effektivt för första fullständiga extrahering och förtäring. Mer information finns i [Hantera stora innehållsdatabaser](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md).

1. Välj en migreringsuppsättning i guiden **Innehållsöverföring** och klicka på **Extrahera** för att starta extraheringen.

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam12.png)

   >[!TIP]
   >Ett intag kan nu schemaläggas att starta automatiskt omedelbart efter att en extrahering har slutförts. Mer information finns i [Inkluderar innehåll i mål](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md).

   >[!IMPORTANT]
   >
   >Kontrollera att Extraheringsnyckeln är giltig och att den inte är i närheten av utgångsdatumet. Om den ligger nära sitt förfallodatum kan du förnya extraheringsnyckeln genom att markera migreringsuppsättningen och klicka på Egenskaper. Klicka på **Förnya**. Detta tar dig till Cloud Acceleration Manager där du kan klicka på **Kopiera extraheringsnyckel**. Varje gång du klickar på **Kopiera extraheringsnyckel** skapas en ny extraheringsnyckel som är giltig i 14 dagar från det att den skapades.
   >![bild](/help/journey-migration/content-transfer-tool/assets-ctt/migrationSetDetails.png)

1. Då öppnas dialogrutan Extrahering. Klicka på **Extrahera** för att starta extraheringsfasen.

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/migrationSetExtraction.png)

   >[!NOTE]
   >Du kan också skriva över mellanlagringsbehållaren under extraheringsfasen. Om **Skriv över mellanlagringsbehållaren** är inaktiverad kan extraheringarna för efterföljande migreringar snabbas upp om innehållssökvägarna eller inkluderingsversionsinställningarna inte har ändrats. Om innehållssökvägarna eller inkluderingsversionsinställningarna har ändrats bör **Skriv över mellanlagringsbehållaren** aktiveras.

1. Fältet **Extrahering** visar nu statusen **RUNNING** som anger att extraheringen pågår.

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam15.png)

   Du kan klicka på **Visa förlopp** för att få en detaljerad vy över den pågående extraheringen.

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/viewProgress.png)

   Du kan också övervaka extraheringsfasens förlopp från Cloud Acceleration Manager genom att gå till sidan Innehållsöverföring och visa den mer i detalj genom att klicka på **..** > **Visa information**.

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam17.png)

1. När extraheringen är klar granskar du andra kolumner som **Source** och **Banor** för information om den migreringsuppsättning som du har fyllt i. Klicka på **..** > **Visa information** om du vill se information, inklusive längden för varje steg i extraheringen. Visa den här dialogrutan under extraheringen så att du kan se hur stegen utvecklas.

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam18b.png)


## Extrahering uppifrån och ned {#top-up-extraction-process}

Content Transfer Tool har en funktion för differentiell innehållsuppdatering som gör att du kan överföra enbart de ändringar som gjorts sedan den föregående innehållsöverföringen.

>[!NOTE]
>Efter den initiala innehållsöverföringen bör du göra regelbundna tillägg av differentiellt innehåll för att förkorta innehållets frysningsperiod för den slutliga differentiella innehållsöverföringen innan du publicerar på Cloud Service. Om du har använt förkopieringssteget för den första fullständiga extraheringen kan du hoppa över förkopieringen för efterföljande extraheringar (om den övre migreringsuppsättningsstorleken är mindre än 200 GB). Orsaken är att det kan lägga till tid i hela processen.
>Det är också viktigt att innehållsstrukturen i befintligt innehåll inte ändras från den tidpunkt då den första extraheringen utförs till den tidpunkt då extraheringen görs. Det går inte att köra uppsättningar på innehåll vars struktur har ändrats sedan den första extraheringen. Kontrollera att du begränsar detta under migreringsprocessen.

>[!NOTE]
>När innehållssökvägar har migrerats till mellanlagringsbehållaren kan dessa sökvägar eller eventuella delsökvägar i dem inte tas bort eller uteslutas från efterföljande toppmigreringar.
>Exempel: Inledande migrering: content/dam/weRetail,
>Nästa försök till undantag uppifrån: content/dam/weRetail/ab.
>I det här scenariot går det inte att utesluta content/dam/weRetail/ab eftersom data redan har migrerats till mellanlagringsbehållaren.

När extraheringen är klar kan du överföra delta-innehåll med extraheringsmetoden top-up.

Följ stegen nedan:

1. Navigera till guiden **Innehållsöverföring** och välj den migreringsuppsättning som du vill utföra extraheringen för. Klicka på **Extract** för att starta uppdateringsextraheringen.

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam19.png)

1. Dialogrutan **Extrahering av migreringsuppsättning** visas. Klicka på **Extract**.

   >[!IMPORTANT]
   >Du bör inaktivera alternativet **Overwrite staging container during extraction**.
   >![bild](/help/journey-migration/content-transfer-tool/assets-ctt/overwriteStagingContainer.png)


## What&#39;s Next {#whats-next}

När du har lärt dig hur du extraherar innehåll från Source i verktyget Innehållsöverföring är du nu redo att lära dig hur du använder verktyget för innehållsöverföring. Se [Inkludera innehåll i mål](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md) där du kan lära dig hur du importerar din migreringsuppsättning från verktyget Innehållsöverföring.

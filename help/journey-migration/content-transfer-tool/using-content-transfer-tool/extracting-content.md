---
title: Extraherar innehåll från källa
description: Lär dig hur du extraherar innehåll från en Adobe Experience Manager-källinstans (AEM) och senare överför det till en Cloud Service AEM.
exl-id: c5c08c4e-d5c3-4a66-873e-96986e094fd3
source-git-commit: 858e10f99e2015a1488bb9e1d0990a553c5f6d04
workflow-type: tm+mt
source-wordcount: '728'
ht-degree: 9%

---

# Extraherar innehåll från källa {#extracting-content}

## Extraheringsprocess i verktyget Innehållsöverföring {#extraction-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_extraction"
>title="Innehållsextrahering"
>abstract="Extrahering avser att extrahera innehåll från Adobe Experience Manager-källinstansen (AEM) till ett temporärt område som kallas migreringsuppsättning. En migreringsuppsättning är ett molnlagringsutrymme som tillhandahålls av Adobe för att tillfälligt lagra det överförda innehållet mellan AEM och Cloud Service AEM."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html#top-up-extraction-process" text="Extrahering uppifrån"


Följ stegen nedan för att extrahera migreringsuppsättningen från Content Transfer Tool:

>[!NOTE]
>Om Amazon S3, Azure Data Store eller File Data Store används som typ av datalager kan du köra det valfria förkopieringssteget för att öka extraheringsfasens hastighet. Steg före kopiering är mest effektivt för första fullständiga extrahering och förtäring. Se [Hantera stora innehållsdatabaser](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md) för mer information.

1. Välj en migreringsuppsättning från **Innehållsöverföring** guide och klicka **Extract** för att påbörja extraheringen.

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam12.png)

   >[!TIP]
   >Ett intag kan nu schemaläggas att starta automatiskt omedelbart efter att en extrahering har slutförts. Se [Infoga innehåll i mål](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md) för mer information.

   >[!IMPORTANT]
   >
   >Kontrollera att Extraheringsnyckeln är giltig och att den inte är i närheten av utgångsdatumet. Om den ligger nära sitt förfallodatum kan du förnya extraheringsnyckeln genom att markera migreringsuppsättningen och klicka på Egenskaper. Klicka **Förnya**. Då kommer du till Cloud Acceleration Manager där du kan klicka **Kopiera extraheringsnyckel**. Varje gång du klickar **Kopiera extraheringsnyckel**skapas en ny extraheringsnyckel som är giltig i 14 dagar från det att den skapades.
   >![bild](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam13.png)

1. Då öppnas dialogrutan Extrahering. Klicka **Extract** för att starta extraheringsfasen.

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam14b.png)

   >[!NOTE]
   >Du kan också skriva över mellanlagringsbehållaren under extraheringsfasen. If **Skriv över mellanlagringsbehållare** är inaktiverat kan extraheringen för efterföljande migreringar snabbas upp om innehållssökvägarna eller inkluderingsversionsinställningarna inte har ändrats. Om innehållssökvägarna eller inkluderingsversionsinställningarna har ändrats **Skriv över mellanlagringsbehållare** ska vara aktiverat.

1. The **Extrahering** fältet visas nu **KÖRS** status för att ange att extraheringen pågår.

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam15.png)

   Klicka **Visa förlopp** för att få en detaljerad bild av den pågående extraheringen.

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam16.png)

   Du kan också övervaka extraheringsfasens förlopp från Cloud Acceleration Manager genom att gå till sidan Innehållsöverföring och se den mer i detalj genom att klicka på **...** > **Visa detaljer**.

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam17.png)

1. När extraheringen är klar granskar du de andra kolumnerna som **Källa** och **Banor** om du vill ha information om den migreringsuppsättning som du har fyllt i. Klicka **...** > **Visa detaljer** för att se detaljer, inklusive varaktigheten för varje steg i extraheringen. Visa den här dialogrutan under extraheringen så att du kan se hur stegen utvecklas.

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam18b.png)


## Extrahering uppifrån och ned {#top-up-extraction-process}

Content Transfer Tool har en funktion för differentiell innehållsuppdatering som gör att du kan överföra enbart de ändringar som gjorts sedan den föregående innehållsöverföringen.

>[!NOTE]
>Efter den initiala innehållsöverföringen bör du göra regelbundna tillägg av differentiellt innehåll för att förkorta innehållets frysningsperiod för den slutliga differentiella innehållsöverföringen innan du publicerar på Cloud Servicen. Om du har använt förkopieringssteget för den första fullständiga extraheringen kan du hoppa över förkopieringen för efterföljande extraheringar (om den övre migreringsuppsättningsstorleken är mindre än 200 GB). Orsaken är att det kan lägga till tid i hela processen.
>Det är också viktigt att innehållsstrukturen i befintligt innehåll inte ändras från den tidpunkt då den första extraheringen utförs till den tidpunkt då extraheringen görs. Det går inte att köra uppsättningar på innehåll vars struktur har ändrats sedan den första extraheringen. Kontrollera att du begränsar detta under migreringsprocessen.

När extraheringen är klar kan du överföra delta-innehåll med extraheringsmetoden top-up.

Följ stegen nedan:

1. Navigera till **Innehållsöverföring** och välj den migreringsuppsättning som du vill utföra extraheringen för uppifrån. Klicka på **Extract** för att starta uppdateringsextraheringen.

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam19.png)

1. The **Extrahering av migreringsuppsättning** visas. Klicka **Extract**.

   >[!IMPORTANT]
   >Du bör inaktivera alternativet **Overwrite staging container during extraction**.
   >![bild](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam20.png)


## What&#39;s Next {#whats-next}

När du har lärt dig hur du extraherar innehåll från källan i verktyget Innehållsöverföring är du nu redo att lära dig Inmatningsprocessen i verktyget Innehållsöverföring. Se [Infoga innehåll i mål](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md) där du kan lära dig hur du importerar dina migreringsuppsättningar från verktyget Innehållsöverföring.

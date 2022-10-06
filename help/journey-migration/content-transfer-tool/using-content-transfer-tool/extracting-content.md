---
title: Extraherar innehåll från källa
description: Extraherar innehåll från källa
exl-id: c5c08c4e-d5c3-4a66-873e-96986e094fd3
source-git-commit: 509715eb6324a370e28d681111ee0fd3fa2a7b44
workflow-type: tm+mt
source-wordcount: '765'
ht-degree: 19%

---

# Extraherar innehåll från källa {#extracting-content}

## Extraheringsprocess i verktyget Innehållsöverföring {#extraction-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_extraction"
>title="Innehållsextrahering"
>abstract="Extrahering avser att extrahera innehåll från AEM till ett temporärt område som kallas migreringsuppsättning. En migreringsuppsättning är ett molnlagringsutrymme som finns hos Adobe för att tillfälligt lagra det överförda innehållet mellan AEM-källinstansen och Cloud Service AEM-instansen."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#top-up-extraction-process" text="Extrahering uppifrån"


Följ stegen nedan för att extrahera migreringsuppsättningen från Content Transfer Tool:

>[!NOTE]
>Om Amazon S3, Azure Data Store eller File Data Store används som typ av datalager kan du köra det valfria förkopieringssteget för att avsevärt snabba upp extraheringsfasen. Steg före kopiering är mest effektivt för första fullständiga extrahering och förtäring. Om du vill göra det måste du konfigurera en `azcopy.config` filen innan extraheringen körs. Se [Hantera stora innehållsdatabaser](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en) för mer information.

>[!IMPORTANT]
>Du bör köra verktyget för användarmappning innan du extraherar innehåll från källan. Se [Använda verktyget för användarmappning](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/user-mapping-tool/using-user-mapping-tool.html?lang=en) för mer information.

1. Välj en migreringsuppsättning från **Innehållsöverföring** guide och klicka **Extract** för att påbörja extraheringen.

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam12.png)

   >[!IMPORTANT]
   >
   >Kontrollera att Extraheringsnyckeln är giltig och att den inte ligger nära utgångsdatumet. Om den ligger nära sitt förfallodatum kan du förnya extraheringsnyckeln genom att markera migreringsuppsättningen och klicka på Egenskaper. Klicka på **Förnya**. Då kommer du till Cloud Acceleration Manager där du kan klicka på **Kopiera extraheringsnyckel**. Varje gång du klickar på **Kopiera extraheringsnyckel**skapas en ny extraheringsnyckel som är giltig i 14 dagar från det att den skapades.
   >![bild](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam13.png)

1. Då öppnas dialogrutan Extrahering. Klicka på **Extract** för att starta extraheringsfasen.

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam14.png)

   >[!NOTE]
   >Du kan skriva över mellanlagringsbehållaren under extraheringsfasen. If **Skriv över mellanlagringsbehållare** är inaktiverat kan det snabba upp extraheringar för efterföljande migreringar där innehållssökvägarna eller inkluderingsversionsinställningarna inte har ändrats. Om innehållssökvägarna eller inkluderingsversionsinställningarna har ändrats **Skriv över mellanlagringsbehållare** ska vara aktiverat.

   >[!IMPORTANT]
   >Om Användarmappning inte har körts på den här migreringsuppsättningen innan innehåll extraheras från källan visas en varning om att steget Användarmappning väntar, vilket visas i bilden ovan. Klicka på **Mappa användare** för att köra verktyget för användarmappning.

1. The **Extrahering** fältet visas nu **KÖRS** status för att ange att extraheringen pågår.

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam15.png)

   Du kan klicka på **Visa förlopp** för att få en detaljerad bild av den pågående extraheringen.

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam16.png)

   Du kan också övervaka extraheringsfasens förlopp från Cloud Acceleration Manager genom att gå till sidan Innehållsöverföring.

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam17.png)

1. När extraheringen är klar kan du granska de andra kolumnerna som **Källa** och **Banor** för information om den migreringsuppsättning som du fyllde i genom att klicka på **...** och sedan **Visa detaljer**.

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam18.png)


## Uppdateringsextrahering {#top-up-extraction-process}

Content Transfer Tool har en funktion för differentiell innehållsuppdatering som gör att du kan överföra enbart de ändringar som gjorts sedan den föregående innehållsöverföringen.

>[!NOTE]
>Efter den första innehållsöverföringen bör du göra regelbundna tillägg av differentiellt innehåll för att förkorta innehållets frysningsperiod för den slutliga differentiella innehållsöverföringen innan du börjar använda Cloud Service. Om du har använt förkopieringssteget för den första fullständiga extraheringen kan du hoppa över förkopieringen för efterföljande extraheringar i den övre delen (om den översta migreringsuppsättningsstorleken är mindre än 200 GB) eftersom det kan göra hela processen tidsödande.
>Dessutom är det viktigt att innehållsstrukturen i befintligt innehåll inte ändras från den tidpunkt då den första extraheringen utförs till den tidpunkt då extraheringen av den övre delen körs. Det går inte att köra uppsättningar på innehåll vars struktur har ändrats sedan den första extraheringen. Kontrollera att du begränsar detta under migreringsprocessen.

När extraheringen är klar kan du överföra delta-innehåll med extraheringsmetoden för uppdateringar.

Följ stegen nedan:

1. Navigera till **Innehållsöverföring** och välj den migreringsuppsättning som du vill utföra extraheringen för uppifrån. Klicka på **Extract** för att starta uppdateringsextraheringen.

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam19.png)

1. The **Extrahering av migreringsuppsättning** visas. Klicka på **Extract**.

   >[!IMPORTANT]
   >Du bör inaktivera alternativet **Overwrite staging container during extraction**.
   >![bild](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam20.png)


## What&#39;s Next {#whats-next}

När du har lärt dig hur du extraherar innehåll från källan i verktyget Innehållsöverföring är du nu redo att lära dig Inmatningsprocessen i verktyget Innehållsöverföring. Se [Infoga innehåll i mål](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md) om du vill lära dig hur du importerar din migreringsuppsättning från verktyget Innehållsöverföring.

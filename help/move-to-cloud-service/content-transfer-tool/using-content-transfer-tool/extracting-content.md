---
title: Extrahera innehåll från källan i verktyget Innehållsöverföring
description: Extrahera innehåll från källan i verktyget Innehållsöverföring
source-git-commit: 0316ba8ee66695836a676ab764ce1f0cb415f95d
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 41%

---


# Extrahera innehåll från källan i verktyget Innehållsöverföring {#extracting-content}

## Extraheringsprocess i verktyget Innehållsöverföring {#extraction-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_extraction"
>title="Innehållsextrahering"
>abstract="Extrahering avser att extrahera innehåll från AEM till ett temporärt område som kallas migreringsuppsättning. En migreringsuppsättning är ett molnlagringsutrymme som finns hos Adobe för att tillfälligt lagra det överförda innehållet mellan AEM-källinstansen och Cloud Service AEM-instansen."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#top-up-extraction-process" text="Extrahering uppifrån"

Följ stegen nedan för att extrahera migreringsuppsättningen från Content Transfer Tool:
>[!NOTE]
>Om Amazon S3 eller Azure Data Store används som typ av datalager kan du köra det valfria förkopieringssteget för att avsevärt snabba upp extraheringsfasen. Om du vill göra det måste du konfigurera en `azcopy.config`-fil innan du kör extraheringen. Mer information finns i [Hantera stora innehållsdatabaser](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en).

1. Välj en migreringsuppsättning i guiden **Innehållsöverföring** och klicka på **Extract** för att starta extraheringen.

   ![bild](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/extraction-01.png)

1. Dialogrutan **Extrahering av migreringsuppsättning** visas och klicka på **Extract** för att starta extraheringsfasen.

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
>Dessutom är det viktigt att innehållsstrukturen i befintligt innehåll inte ändras från den tidpunkt då den första extraheringen utförs till den tidpunkt då extraheringen av den övre delen körs. Det går inte att köra uppsättningar på innehåll vars struktur har ändrats sedan den första extraheringen. Kontrollera att du begränsar detta under migreringsprocessen.

När extraheringen är klar kan du överföra delta-innehåll med extraheringsmetoden för uppdateringar.

Följ stegen nedan:

1. Navigera till guiden **Innehållsöverföring** och välj den migreringsuppsättning som du vill utföra extraheringen för. Klicka på **Extract** för att starta uppdateringsextraheringen.

   ![bild](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/extraction-05.png)

1. Dialogrutan **Extrahering av migreringsuppsättning** visas. Klicka på **Extract**.

   >[!IMPORTANT]
   >Du bör inaktivera alternativet **Overwrite staging container during extraction**.
   >![bild](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/extraction-06.png)


## What&#39;s Next {#whats-next}

När du har lärt dig hur du extraherar innehåll från källan i verktyget Innehållsöverföring är du nu redo att lära dig Inmatningsprocessen i verktyget Innehållsöverföring. Se [Inkludera innehåll i mål i verktyget Innehållsöverföring](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool/ingesting-content.md) om du vill veta hur du importerar din migreringsuppsättning från verktyget Innehållsöverföring.

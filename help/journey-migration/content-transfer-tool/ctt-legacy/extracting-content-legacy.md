---
title: Extrahera innehåll från källa (äldre)
description: Extraherar innehåll från källa
hide: true
hidefromtoc: true
exl-id: 9f43356c-ba51-48bc-97f5-f1f5db81e7f3
source-git-commit: 22bbf15e33ab3d5608dc01ed293bb04b07cb6c8c
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 35%

---

# Extrahera innehåll från källa (äldre) {#extracting-content}

## Extraheringsprocess i verktyget Innehållsöverföring {#extraction-process}

Följ stegen nedan för att extrahera migreringsuppsättningen från Content Transfer Tool:
>[!NOTE]
>Om Amazon S3 eller Azure Data Store används som typ av datalager kan du köra det valfria förkopieringssteget för att avsevärt snabba upp extraheringsfasen. Om du vill göra det måste du konfigurera en `azcopy.config` filen innan extraheringen körs. Se [Hantera stora innehållsdatabaser](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en) för mer information.

>[!IMPORTANT]
>Du bör köra verktyget för användarmappning innan du extraherar innehåll från källan. Se [Använda verktyget för användarmappning](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/user-mapping-tool/using-user-mapping-tool.html?lang=en) för mer information.

1. Välj en migreringsuppsättning från **Innehållsöverföring** guide och klicka **Extract** för att påbörja extraheringen.

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/extraction-01.png)

1. The **Extrahering av migreringsuppsättning** visas och klicka på **Extract** för att starta extraheringsfasen.

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/extraction-02.png)

   >[!NOTE]
   >Du kan skriva över mellanlagringsbehållaren under extraheringsfasen.

   >[!IMPORTANT]
   >Om Användarmappning inte har körts på den här migreringsuppsättningen innan innehåll extraheras från källan visas en varning om att steget Användarmappning väntar, vilket visas i bilden nedan. Klicka på **Mappa användare** för att köra verktyget för användarmappning.
   >![bild](/help/journey-migration/content-transfer-tool/assets-ctt/user-mapping-extract.png)

1. The **Extrahering** fältet visas nu **KÖRS** status för att ange att extraheringen pågår.

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/extraction-03.png)

   När extraheringen är klar uppdateras migreringsuppsättningens status till **FINISHED** och en *solid grön* molnikon visas under **INFO**-fältet.

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/extraction-04.png)

   >[!IMPORTANT]
   >Användargränssnittet har en funktion för automatisk inläsning som läser in **Innehållsöverföring** var 30:e sekund.
   >När extraheringsfasen startas skapas ett skrivlås som frisläpps efter *60 sekunder*. Om extraheringen avbryts måste du alltså vänta en minut på att låset ska frisläppas innan du startar extraheringen igen.

## Uppdateringsextrahering {#top-up-extraction-process}

Content Transfer Tool har en funktion för differentiell innehållsuppdatering som gör att du kan överföra enbart de ändringar som gjorts sedan den föregående innehållsöverföringen.

>[!NOTE]
>Efter den första innehållsöverföringen bör du göra regelbundna tillägg av differentiellt innehåll för att förkorta innehållets frysningsperiod för den slutliga differentiella innehållsöverföringen innan du börjar använda Cloud Service.
>Dessutom är det viktigt att innehållsstrukturen i befintligt innehåll inte ändras från den tidpunkt då den första extraheringen utförs till den tidpunkt då extraheringen av den övre delen körs. Det går inte att köra uppsättningar på innehåll vars struktur har ändrats sedan den första extraheringen. Kontrollera att du begränsar detta under migreringsprocessen.

När extraheringen är klar kan du överföra delta-innehåll med extraheringsmetoden för uppdateringar.

Följ stegen nedan:

1. Navigera till **Innehållsöverföring** och välj den migreringsuppsättning som du vill utföra extraheringen för uppifrån. Klicka på **Extract** för att starta uppdateringsextraheringen.

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/extraction-05.png)

1. The **Extrahering av migreringsuppsättning** visas. Klicka på **Extract**.

   >[!IMPORTANT]
   >Du bör inaktivera alternativet **Overwrite staging container during extraction**.
   >![bild](/help/journey-migration/content-transfer-tool/assets-ctt/extraction-06.png)


## What&#39;s Next {#whats-next}

När du har lärt dig hur du extraherar innehåll från källan i verktyget Innehållsöverföring är du nu redo att lära dig Inmatningsprocessen i verktyget Innehållsöverföring. Se [Infoga innehåll i mål](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md) om du vill lära dig hur du importerar din migreringsuppsättning från verktyget Innehållsöverföring.

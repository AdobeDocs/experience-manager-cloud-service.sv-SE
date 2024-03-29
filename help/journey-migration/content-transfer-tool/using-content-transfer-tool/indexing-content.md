---
title: Indexering efter migrering av innehåll
description: Lär dig hur migreringsprocessen indexerar det inkapslade Cloud Servicen i målinstansen.
exl-id: a13d5df4-b351-410a-9336-1b34a8af21b6
source-git-commit: 58195fcb10312c89042f555665d4c8b3642f82ba
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 0%

---

# Indexering efter migrering av innehåll {#Indexing-content}

## Indexering {#aem-indexing-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_indexing"
>title="Innehållsindexering"
>abstract="AEM indexering avser indexering av Cloud Servicens innehåll efter att innehållet har migrerats till den. Indexering krävs för att det ska gå att söka efter innehåll i den instansen."

När Cloud Acceleration Manager har slutfört inmatningen av innehåll i din Cloud Service är det klart att användas. Till att börja med är innehållet inte indexerat, vilket sannolikt leder till en instabil miljö där problem som till exempel osökbart innehåll och försämrade prestanda kan förväntas. För optimala prestanda för instansen kommer migreringsprocessen automatiskt att starta indexeringen av innehållet. Det finns inget att göra förutom att övervaka indexeringsförloppet.

> Mer information om hur du påbörjar ett intag finns i [Infoga innehåll i Cloud Service](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md).

Följande steg visar det allmänna flöde som du kan förvänta dig att se i användargränssnittet vid indexering. En del etiketter har ett användbart sammanhang i verktygstipsen, så se till att du håller muspekaren över objekten för att lära dig mer om den aktuella indexeringsstatusen.

Börja med att gå till Cloud Acceleration Manager. Klicka på projektkortet och klicka sedan på kortet för innehållsöverföring. Navigera till **Inmatningsjobb** och se jobben.

>[!NOTE]
>Du kan visa eller ladda ned indexeringsloggarna med hjälp av funktionsmakrona i jobbet med hjälp av listrutan ..... Loggarna finns i
> Indexeringslogg-åtgärdsavsnitt, när indexeringsjobbet har slutförts

### Väntande

Så här visas matningsjobbets rad när matningen körs, innan indexeringsjobbet har startats. Användaren behöver inte utföra någon åtgärd. Om intaget misslyckas av någon anledning kommer köningen av indexjobbet att avbrytas och inte startas.

![bild](/help/journey-migration/content-transfer-tool/assets-indexing/pending.png)

### Körs

När importen är klar initieras indexeringsjobbet automatiskt. Inmatningsjobbraden visar en förloppsikon för AEM indexeringsstatus. Du kan öppna dialogrutan för varaktighet för att se förloppet för jobbet.

![bild](/help/journey-migration/content-transfer-tool/assets-indexing/running.png)

### Complete

När indexeringsjobbet lyckas är instansen klar att användas med optimala prestanda. Nu kan du visa eller ladda ned indexeringsjobbloggar för att inspektera dem.

![bild](/help/journey-migration/content-transfer-tool/assets-indexing/complete.png)

### Fel

Indexeringen av målinstansen kommer troligtvis att lyckas. I vissa fall kan det misslyckas och raden för ingrepp visas enligt följande. I samtliga fall kan du ta reda på lite detaljer om felet genom att hovra över felstatusen, och du kan få mer information som hjälper dig att avgöra nästa steg. Nu kan du visa eller ladda ned indexeringsjobbloggar för att hitta felets källa. Om nästa steg inte är klart kontaktar du Adobe Support med information om intaget och indexeringsloggen.

>[!TIP]
>
> Om indexeringsjobbet verkar vara för långt bör du kontrollera att [IP-Tillåtelselista har inte tillämpats](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) via Cloud Manager eftersom det förhindrar att Cloud Acceleration Manager når migreringstjänsten.

![bild](/help/journey-migration/content-transfer-tool/assets-indexing/failed.png)

## What&#39;s Next {#whats-next}

När målmolntjänstinstansen har indexerats kan du visa loggar för indexeringsjobben och söka efter information och fel.

Migreringen är klar. Testning och validering av målmolntjänstinstansen kan börja.

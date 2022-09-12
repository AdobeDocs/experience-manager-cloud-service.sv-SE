---
title: Visa loggar för en migreringsuppsättning i verktyget Innehållsöverföring (äldre)
description: Visa loggar för en migreringsuppsättning i verktyget Innehållsöverföring
hide: true
hidefromtoc: true
exl-id: 01c8afd3-c594-4a41-b905-8c3a2d74db6f
source-git-commit: 22bbf15e33ab3d5608dc01ed293bb04b07cb6c8c
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 64%

---

# Visa loggar för en migreringsuppsättning (äldre) {#view-logs-content-transfer-tool}

När varje steg har slutförts (extrahering och förtäring) kontrollerar du loggarna och söker efter fel.  Felen bör åtgärdas omedelbart, antingen genom att man hanterar de rapporterade problemen eller genom att man kontaktar Adobe support.

## Steg för att visa loggar {#viewing-logs}

Du kan visa loggar för en befintlig migreringsuppsättning på sidan *Overview*.
Följ stegen nedan:

1. Navigera till sidan *Overview* och markera den migreringsuppsättning som du vill ta bort. Klicka sedan på **View Log** i åtgärdsfältet.

   ![bild](/help/journey-migration/content-transfer-tool/assets/view-log1.png)

1. Dialogrutan **Logs** visas. Klicka på **Extraction Logs** för att visa loggarna på en ny flik.

   ![bild](/help/journey-migration/content-transfer-tool/assets/view-log2.png)
Eller:

   Du kan även visa loggar för din migreringsuppsättning på skärmen *Overview*. Markera migreringsuppsättningen och klicka på statusen under fältet **EXTRACTION**. I det här fallet klickar du på **FINISHED** för att visa loggarna på en ny flik.

   ![bild](/help/journey-migration/content-transfer-tool/assets/view-log3.png)

1. Om du vill bifoga loggarna utan att använda användargränssnittet kan du använda SSH i AEM-källmiljön och lägga till `crx-quickstart/cloud-migration/extraction-XXXXX/output.log file`.

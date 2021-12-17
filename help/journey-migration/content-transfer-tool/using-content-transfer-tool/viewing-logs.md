---
title: Visa loggar för en migreringsuppsättning i verktyget Innehållsöverföring
description: Visa loggar för en migreringsuppsättning i verktyget Innehållsöverföring
source-git-commit: bcbf4e4ba1330bef9f2c8c473419903e40ac0e58
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 52%

---


# Visa loggar för en migreringsuppsättning {#view-logs-content-transfer-tool}


>[!CONTEXTUALHELP]
>id="aemcloud_ctt_logs"
>title="Visa loggar"
>abstract="När extraheringen av intag har slutförts kontrollerar du om det finns några fel/varningar i loggarna. Felen bör åtgärdas omedelbart, antingen genom att man hanterar de rapporterade problemen eller genom att man kontaktar Adobe support."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#troubleshooting" text="Felsökning"
>additional-url="https://helpx.adobe.com/ca/enterprise/admin-guide.html/ca/enterprise/using/support-for-experience-cloud.ug.html" text="Kontakta supporten för Adobe"

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

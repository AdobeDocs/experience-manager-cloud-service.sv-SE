---
title: Visa loggar för en migreringsuppsättning i verktyget Innehållsöverföring
description: Visa loggar för en migreringsuppsättning i verktyget Innehållsöverföring
exl-id: aed1ac83-a2fb-425e-aca4-39cd0bb42fd3
feature: Migration
role: Admin
source-git-commit: e1089810b3bf3db0cc440bb397e5549ade6eac37
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 9%

---

# Visa loggar för en migreringsuppsättning {#view-logs-content-transfer-tool}


>[!CONTEXTUALHELP]
>id="aemcloud_ctt_logs"
>title="Visa loggar"
>abstract="När extraheringen av intag har slutförts kontrollerar du om det finns några fel/varningar i loggarna. Felen bör åtgärdas omedelbart, antingen genom att man hanterar de rapporterade problemen eller genom att man kontaktar Adobe support."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html#troubleshooting" text="Felsökning"
>additional-url="https://helpx.adobe.com/ca/enterprise/using/support-for-experience-cloud.html" text="Kontakta Adobe Support"

När varje steg har slutförts (extrahering och förtäring) kontrollerar du loggarna och söker efter fel.  Felen bör åtgärdas omedelbart, antingen genom att man hanterar de rapporterade problemen eller genom att man kontaktar Adobe support.

## Steg för att visa loggar {#viewing-logs}

### Extraheringsloggar

Om du vill visa extraheringsloggarna går du till Adobe Experience Manager-källinstansen och väljer önskad migreringsuppsättning.

Följ sedan stegen nedan:

1. Välj en migreringsuppsättning och klicka på **Visa logg** i åtgärdsfältet. Dialogrutan Logs öppnas. Klicka på **Extraheringslogg** för att visa loggarna på en ny flik.

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/logs.png) \
   Du kan också klicka på statusen **SLUTFÖRD** om du vill visa loggarna på en ny flik.

1. Om du vill bifoga loggarna utan att använda användargränssnittet kan du använda SSH i AEM-källmiljön och lägga till `crx-quickstart/cloud-migration/extraction-XXXXX/output.log file`.

### Inmatningsloggar

Om du vill visa loggar för inmatning går du till listan Inmatningsjobb i Cloud Acceleration Manager, letar upp önskat migreringsjobb och klickar på de tre punkterna (**..**) för jobbet. Du kan sedan klicka på **Hämta logg** för att hämta loggar.

![bild](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam28.png)

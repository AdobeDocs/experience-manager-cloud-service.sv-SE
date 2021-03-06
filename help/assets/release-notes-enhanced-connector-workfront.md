---
title: Versionsinformation för [!DNL Workfront for Experience Manager enhanced connector]
description: Versionsinformation för [!DNL Workfront for Experience Manager enhanced connector]
exl-id: 12de589d-fe5d-4bd6-b96b-48ec8f1ebcb6
source-git-commit: d763bacb0844a438ebea6ef206dfa184a49993fe
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 0%

---

# Versionsinformation för [!DNL Workfront for Experience Manager enhanced connector] {#release-notes-enhanced-connector-workfront}

I följande avsnitt beskrivs den allmänna versionsinformationen för [!DNL Workfront for Experience Manager enhanced connector].

## Releasedatum {#release-date}

Releasedatum för den senaste versionen, 1.9.1 av [!DNL Workfront for Experience Manager enhanced connector] är 1 juli 2022.

## Frigör högdagrar {#release-highlights}

Den senaste versionen av [!DNL Workfront for Experience Manager enhanced connector] innehåller följande förbättringar och felkorrigeringar:

* Stöd för autentisering mellan Experience Manager- och Workfront-program har lagts till med Workfront API-nyckel för instanser som migreras till Adobe IMS.

* När du länkar externa filer eller mappar visas `SERVER_ERROR` felmeddelande. Felmeddelandet refererar till ett otillåtet undantag på grund av en felmatchning i API-nycklar.

* När du kör ett arbetsflöde för Skapa uppgift för en resurs visas undantaget Null-pekare i loggmeddelandena.

* När du aktiverar `Replace Spaces with DASH` konfigurationsalternativet under Avancerade inställningar i Experience Manager resulterar i att en dubblett av mapparna skapas i Workfront.

>[!IMPORTANT]
>
>Adobe rekommenderar att du [uppgradera till den senaste 1.9.1-versionen](../assets/update-workfront-enhanced-connector.md) i [!DNL Workfront for Experience Manager enhanced connector].

## Kända fel {#known-issues}

* När projektlänkade mappar konfigureras med AEM 6.4 sparar Experience Manager inte värdena för **[!UICONTROL sub-folders]** och **[!UICONTROL Create linked folder in projects with portfolio]** fält. Värdet för **[!UICONTROL sub-folders]** fältuppdateringar till **[!UICONTROL undefined]** och värdet för **[!UICONTROL Create linked folder in projects with portfolio]** fältuppdateringar till **[!UICONTROL Default Portfolio]** automatiskt när konfigurationen har sparats.

* När du använder den klassiska Workfront-upplevelsen är **[!UICONTROL Send to]** finns i **[!UICONTROL More]** I listrutan kan du inte välja målmål i Experience Manager. The **[!UICONTROL Send to]** fungerar korrekt med **[!UICONTROL Document Actions]** listruta. The **[!UICONTROL Send to]** alternativet fungerar korrekt för **[!UICONTROL More]** listrutan samt **[!UICONTROL Document Actions]** nedrullningsbar lista som finns i den nya Workfront-upplevelsen.

## Tidigare versioner {#previous-releases}

### Juniversion 2022 {#june-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] innehåller nu följande uppdateringar:

* När du överför via en länkad mapp eller använder `Send To` åtgärd som är tillgänglig i Workfront för att överföra resurser till Experience Manager as a Cloud Service, resursen eller resurserna skadas och kan inte öppnas i Adobe Photoshop.

### Mars 2022-utgåvan {#march-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] innehåller nu följande uppdateringar:

* Nu kan du skapa länkade mappar mellan Adobe Workfront och AEM Assets as a Cloud Service även om det finns flera projektlänkade mappkonfigurationer.

* Stöd för sidnumrering av händelseabonnemang har lagts till.

* Stöd för AEM 6.4.x har lagts till.

* Stöd för proxymiljöer har lagts till.

* Flera felkorrigeringar baseras på feedback från partner och kunder.

>[!MORELIKETHIS]
>
>* [Integrera [!DNL Workfront for Experience Manager enhanced connector] med Experience Manager 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-integrations.html?lang=en)
>* [Integrera [!DNL Workfront for Experience Manager enhanced connector] med Experience Manager 6.4](https://experienceleague.adobe.com/docs/experience-manager-64/assets/integrations/workfront-integrations.html?lang=en)


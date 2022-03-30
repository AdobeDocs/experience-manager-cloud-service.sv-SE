---
title: Versionsinformation för [!DNL Workfront for Experience Manager enhanced connector]
description: Versionsinformation för [!DNL Workfront for Experience Manager enhanced connector]
source-git-commit: 02df53e47d2b8617c9a81f5c438814996af92340
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---


# Versionsinformation för [!DNL Workfront for Experience Manager enhanced connector] {#release-notes-enhanced-connector-workfront}

I följande avsnitt beskrivs den allmänna versionsinformationen för [!DNL Workfront for Experience Manager enhanced connector].

## Releasedatum {#release-date}

Releasedatum för den senaste versionen av [!DNL Workfront for Experience Manager enhanced connector] är 28 mars 2022.

## Frigör högdagrar {#release-highlights}

[!DNL Workfront for Experience Manager enhanced connector] innehåller nu följande uppdateringar:

* Nu kan du skapa länkade mappar mellan Adobe Workfront och AEM Assets as a Cloud Service även om det finns flera projektlänkade mappkonfigurationer.

* Stöd för sidnumrering av händelseabonnemang har lagts till.

* Stöd för AEM 6.4.x har lagts till.

* Stöd för proxymiljöer har lagts till.

* Flera felkorrigeringar baseras på feedback från partner och kunder.

## Kända fel {#known-issues}

* När projektlänkade mappar konfigureras med AEM 6.4 sparar Experience Manager inte värdena för **[!UICONTROL sub-folders]** och **[!UICONTROL Create linked folder in projects with portfolio]** fält. Värdet för **[!UICONTROL sub-folders]** fältuppdateringar till **[!UICONTROL undefined]** och värdet för **[!UICONTROL Create linked folder in projects with portfolio]** fältuppdateringar till **[!UICONTROL Default Portfolio]** automatiskt när konfigurationen har sparats.

* När du använder den klassiska Workfront-upplevelsen är **[!UICONTROL Send to]** finns i **[!UICONTROL More]** I listrutan kan du inte välja målmål i Experience Manager. The **[!UICONTROL Send to]** fungerar korrekt med **[!UICONTROL Document Actions]** listruta. The **[!UICONTROL Send to]** alternativet fungerar korrekt för **[!UICONTROL More]** listrutan samt **[!UICONTROL Document Actions]** nedrullningsbar lista som finns i den nya Workfront-upplevelsen.

>[!MORELIKETHIS]
>
>* [Integrera [!DNL Workfront for Experience Manager enhanced connector] med Experience Manager 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-integrations.html?lang=en)
>* [Integrera [!DNL Workfront for Experience Manager enhanced connector] med Experience Manager 6.4](https://experienceleague.adobe.com/docs/experience-manager-64/assets/integrations/workfront-integrations.html?lang=en)



---
title: Versionsinformation för [!DNL Workfront for Experience Manager enhanced connector]
description: Versionsinformation för [!DNL Workfront for Experience Manager enhanced connector]
exl-id: 12de589d-fe5d-4bd6-b96b-48ec8f1ebcb6
source-git-commit: 14b779c476b88ff1ee9d2798296add14f337dbfa
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 0%

---

# Versionsinformation för [!DNL Workfront for Experience Manager enhanced connector] {#release-notes-enhanced-connector-workfront}

I följande avsnitt beskrivs den allmänna versionsinformationen för [!DNL Workfront for Experience Manager enhanced connector].

## Releasedatum {#release-date}

Releasedatum för den senaste versionen, 1.9.3 av [!DNL Workfront for Experience Manager enhanced connector] är 16 september 2022.

## Frigör högdagrar {#release-highlights}

Den senaste versionen av [!DNL Workfront for Experience Manager enhanced connector] innehåller följande förbättringar och felkorrigeringar:

* Det går inte att överföra en fil som är större än 8 GB.
* Problem vid automatisk publicering av resurser som skickas från Workfront till AEM.
* Fältet Rotsökväg är inte tillgängligt för fältet Taggar när du redigerar ett standardformulär för metadataschema.
* Problem med att lägga till nya versioner i Workfront med AEM arbetsflöden.
* När du utför en AEM sökning efter resurser som är tillgängliga i Workfront visas ett felmeddelande i AEM.
* När du skapar ett AEM arbetsflöde för att skapa uppgifter från en resurs och inte definierar något överordnat aktivitetsnamn, skapas inte uppgiften i Workfront.



>[!IMPORTANT]
>
>Adobe rekommenderar att du [uppgradera till den senaste 1.9.3-versionen](../assets/update-workfront-enhanced-connector.md) i [!DNL Workfront for Experience Manager enhanced connector].

## Kända fel {#known-issues}

* När projektlänkade mappar konfigureras med AEM 6.4 sparar Experience Manager inte värdena för **[!UICONTROL sub-folders]** och **[!UICONTROL Create linked folder in projects with portfolio]** fält. Värdet för **[!UICONTROL sub-folders]** fältuppdateringar till **[!UICONTROL undefined]** och värdet för **[!UICONTROL Create linked folder in projects with portfolio]** fältuppdateringar till **[!UICONTROL Default Portfolio]** automatiskt när konfigurationen har sparats.

* När du använder den klassiska Workfront-upplevelsen är **[!UICONTROL Send to]** finns i **[!UICONTROL More]** I listrutan kan du inte välja målmål i Experience Manager. The **[!UICONTROL Send to]** fungerar korrekt med **[!UICONTROL Document Actions]** listruta. The **[!UICONTROL Send to]** alternativet fungerar korrekt för **[!UICONTROL More]** listrutan samt **[!UICONTROL Document Actions]** nedrullningsbar lista som finns i den nya Workfront-upplevelsen.

* Workfront visar en `SERVER_ERROR` när dokument länkas till AEM efter uppgradering till version 8316. Lös problemet genom att tilldela `rep:readProperties` till `content/dam/collections` for `wf-workfront-user` AEM användargrupp.

## Tidigare versioner {#previous-releases}

### Version från augusti 2022 {#august-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] version 1.9.2, släppt den 3 augusti, innehåller följande uppdateringar:

* The **[!UICONTROL Upload Document]** arbetsflödessteget kan inte bifoga ett dokument till Workfront.

* The **[!UICONTROL Upload Document]** arbetsflödessteget kan inte bifoga ett dokument till uppgifter och ärenden i Workfront. Arbetsflödessteget kopplar ett dokument till projekt.

### juliversion 2022 {#july-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] version 1.9.1 innehåller följande uppdateringar:

* Stöd för autentisering mellan Experience Manager- och Workfront-program har lagts till med Workfront API-nyckel för instanser som migreras till Adobe IMS.

* När du länkar externa filer eller mappar visas `SERVER_ERROR` felmeddelande. Felmeddelandet refererar till ett otillåtet undantag på grund av en felmatchning i API-nycklar.

* När du kör ett arbetsflöde för Skapa uppgift för en resurs visas undantaget Null-pekare i loggmeddelandena.

* När du aktiverar `Replace Spaces with DASH` konfigurationsalternativet under Avancerade inställningar i Experience Manager resulterar i att en dubblett av mapparna skapas i Workfront.

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


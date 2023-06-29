---
title: Versionsinformation för [!DNL Workfront for Experience Manager enhanced connector]
description: Versionsinformation för [!DNL Workfront for Experience Manager enhanced connector]
exl-id: 12de589d-fe5d-4bd6-b96b-48ec8f1ebcb6
source-git-commit: 87aeebad2576e91472530a2617b23bece4cd453f
workflow-type: tm+mt
source-wordcount: '1103'
ht-degree: 0%

---

# Versionsinformation för [!DNL Workfront for Experience Manager enhanced connector] {#release-notes-enhanced-connector-workfront}

I följande avsnitt beskrivs den allmänna versionsinformationen för [!DNL Workfront for Experience Manager enhanced connector].

## Releasedatum {#release-date}

Releasedatum för den senaste versionen, 1.9.11 av [!DNL Workfront for Experience Manager enhanced connector] är 19 juni 2023.

## Frigör högdagrar {#release-highlights}

Den senaste versionen av [!DNL Workfront for Experience Manager enhanced connector] innehåller följande uppdateringar:

* När du har konfigurerat avancerade nätverk kan det uppstå problem när du skickar innehåll från Adobe Workfront till AEM as a Cloud Service.

>[!NOTE]
>
>AEM 6.4 har nått slutet på det utökade stödet. Mer information finns i [teknisk supportperiod](https://helpx.adobe.com/support/programs/eol-matrix.html). Hitta de versioner som stöds [här](https://experienceleague.adobe.com/docs/?lang=en).


>[!IMPORTANT]
>
>Adobe rekommenderar dig [uppgradera till den senaste 1.9.11-versionen](/help/assets/workfront-connector-install.md) i [!DNL Workfront for Experience Manager enhanced connector].

## Kända fel {#known-issues}

* När projektlänkade mappar konfigureras med AEM 6.4 sparar Experience Manager inte värdena för **[!UICONTROL sub-folders]** och **[!UICONTROL Create linked folder in projects with portfolio]** fält. Värdet för **[!UICONTROL sub-folders]** fältuppdateringar till **[!UICONTROL undefined]** och värdet för **[!UICONTROL Create linked folder in projects with portfolio]** fältuppdateringar till **[!UICONTROL Default Portfolio]** automatiskt när konfigurationen har sparats.

* När du använder den klassiska Workfront-upplevelsen är **[!UICONTROL Send to]** finns i **[!UICONTROL More]** I listrutan kan du inte välja målmål i Experience Manager. The **[!UICONTROL Send to]** fungerar korrekt med **[!UICONTROL Document Actions]** nedrullningsbar lista. The **[!UICONTROL Send to]** alternativet fungerar korrekt för **[!UICONTROL More]** nedrullningsbar lista och **[!UICONTROL Document Actions]** nedrullningsbar lista som finns i nya Workfront.

## Tidigare versioner {#previous-releases}

### Version från maj 2023 {#may-2023-release}

* Workfront returnerar ett 409 HTTP-svar för dubblerade händelseprenumerationer baserat på ett REST-anrop från Experience Manager till Workfront, vilket leder till ett null-pekarundantag.

### April 2023-utgåvan {#april-2023-release}

[!DNL Workfront for Experience Manager enhanced connector] version 1.9.9, släppt 10 april 2023 innehåller följande uppdateringar:

* Experience Manager visar en `DateTimeParseException` undantagsfel när det tar emot det senaste ändringsdatumet från Workfront när en länkad mapp skapas.

* Problem vid skapande av flera länkade projektmappar på kort tid.

* Det går inte att konfigurera en tröskelgräns för antalet nya uppsättningar av projektlänkade mappar.

### Mars 2023-utgåvan {#march-2023-release}

[!DNL Workfront for Experience Manager enhanced connector] version 1.9.8, släppt 2023-03-03 innehåller följande uppdateringar:

* Prestandaförbättringar i Experience Manager när länkade projektmappar skapas i Workfront.

* Kommentarsborttagningar i Workfront visas nu i Experience Manager.

* Möjlighet att hantera blockerande nya kunder på Experience Manager as a Cloud Service från att konfigurera anslutningen.


### Januariversion 2023 {#january-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] version 1.9.7, släppt 2023-02-02 innehåller följande uppdateringar:

* Metadataredigeraren visar inte Workfront anpassade formuläregenskaper efter installationen av version 1.9.6.

* Dev-konsolen visas `/content/dam/jcr:content/metadata/wfProjectURL not found` felmeddelande när du har installerat Workfront Enhanced Connector och öppnat Assets-startsidan.

### December 2022-utgåvan {#december-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] version 1.9.6 släppt den 9 december innehåller följande uppdateringar:

**Förbättring**

<!--

* Workfront enhanced connector now allows you to use new search parameters to be more specific while defining folder names on large repositories.

-->

* Workfront förbättrade anslutning stöder nu fulltextsökning av resurser och mappar.

**Felkorrigeringar**

* Metadata för dokumentversion synkroniseras inte korrekt mellan Workfront och Experience Manager.
* Problem vid skapande av en mapp som är länkad till Experience Manager i Workfront när mappen använder ett schema som saknar definition i den globala konfigurationen.
* Formuläret för metadataschemats svarar inte när du klickar på ett fält på grund av en inläsningstid som är längre än förväntat. Specifik OSGi-konfiguration för anpassade formulär har lagts till för att lösa problemet. Namnen på de anpassade formulär som du lägger till i metadataschemats är tillgängliga i loggarna.

### November 2022-utgåvan {#november-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] version 1.9.5, släppt den 11 november, innehåller följande uppdateringar:

* När du bara definierar ett värde för ett fält med flera värden i Workfront mappas fältvärdet inte korrekt till Experience Manager.

* Experience Manager visar `SERVER_ERROR` på **[!UICONTROL Link External Files and Folders]** skärm vid åtkomst av resursmappar på grund av ogiltiga behörigheter på `/content/dam/collections`.

* Aktivera **[!UICONTROL Publish Assets to Brand Portal]** på konfigurationssidan för Workfront Enhanced Connector skapar en felaktig händelse. Händelsen tas inte bort även efter att alternativet har inaktiverats.

  Så här löser du problemet:

   1. Uppgradera till version 1.9.5 av den förbättrade anslutningen.

   1. Inaktivera **[!UICONTROL Publish Assets to Brand Portal]** under avancerade inställningar.

   1. Aktivera **[!UICONTROL Publish Assets to Brand Portal]** alternativ.

   1. Ta bort fel händelseprenumerationer.

      1. Utför GET samtal till `/attask/eventsubscription/api/v1/subscriptions?page=<page-number>`

         Kör ett API-anrop för varje sidnummer.

      1. Sök efter följande text för att hitta händelseprenumerationer som matchar följande URL och som inte har någon `objId`:

         ```
              "objId": "",
             "url": "<your-aem-domain>/bin/workfront-tools/events/linkedfolderprojectupdate<your-aem-domain>/
         ```

         Se till att innehållet mellan `"objId": "",` och `"url"` matchar JSON-svaret. Den rekommenderade metoden är att kopiera från en Event-prenumeration som har en `objId` och ta sedan bort numret.

      1. Observera händelsens prenumerations-ID.

      1. Ta bort fel händelseprenumeration. Gör ett Delete API-anrop till `<your-aem-domain>/attask/eventsubscription/api/v1/subscriptions/<event-subscription-ID-from-previous-step>`

         `200` eftersom svarskoden innebär att felaktiga händelseprenumerationer tas bort.
  >[!NOTE]
  >
  >Om du redan har tagit bort fel händelseprenumerationer innan du utför de steg som beskrivs i den här proceduren kan du hoppa över det sista steget i den här proceduren.

### Oktober 2022-versionen {#october-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] version 1.9.4, släppt i oktober 2007, innehåller följande uppdateringar:

* Det går inte att visa fliken Händelseprenumerationer på den utökade konfigurationssidan för anslutningsprogrammet på grund av många händelser.

* Workfront kan inte hämta listan över befintliga mappar i ett projekt, vilket resulterar i att dubblettmappar skapas.

### September 2022-utgåvan {#september-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] version 1.9.3, släppt 16 september, innehåller följande uppdateringar:

* Det går inte att överföra en fil som är större än 8 GB.
* Problem vid automatisk publicering av resurser som skickas från Workfront till AEM.
* Fältet Rotsökväg är inte tillgängligt för fältet Taggar när du redigerar ett standardformulär för metadataschema.
* Problem med att lägga till nya versioner i Workfront med AEM arbetsflöden.
* När du utför en AEM sökning efter resurser som är tillgängliga i Workfront visas ett felmeddelande i AEM.
* När du skapar ett AEM arbetsflöde för att skapa uppgifter från en resurs och inte definierar något överordnat aktivitetsnamn, skapas inte uppgiften i Workfront.

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

* När du överför via en länkad mapp eller använder `Send To` åtgärden som är tillgänglig i Workfront för att överföra resurser till Experience Manager as a Cloud Service, är skadad och kan inte öppnas i Adobe Photoshop.

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

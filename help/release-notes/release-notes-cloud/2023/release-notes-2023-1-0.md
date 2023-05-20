---
title: Versionsinformation om 2023.1.0-utgåvan av [!DNL Adobe Experience Manager] as a Cloud Service.
description: Versionsinformation om 2023.1.0-utgåvan av [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: f134fdbc-224b-404c-b20f-44cae8bad681
source-git-commit: 9cff6e94b38016f008fd8177be2e071a530d80b6
workflow-type: tm+mt
source-wordcount: '978'
ht-degree: 0%

---

# Versionsinformation 2023.1.0 för [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

I följande avsnitt beskrivs versionsinformationen för 2023.1.0-versionen av [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Härifrån kan du navigera till versionsinformation för tidigare versioner; till exempel för 2021, 2022 och så vidare.
>
>Ta en titt på [Roadmap för lansering av Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html) om de kommande funktionsaktiviteterna för [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Se [Senaste dokumentationsuppdateringar](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html) för information om dokumentationsuppdateringar som inte är direkt relaterade till en release.

## Releasedatum {#release-date}

Releasedatum [!DNL Adobe Experience Manager] som [!DNL Cloud Service] 2023.1.0-versionen är 9 februari 2023. Nästa funktionsversion (2023.2.0) är planerad till 12 april 2023.

## Släpp video {#release-video}

Titta på videon med versionsöversikten från januari 2023 om du vill se en sammanfattning av funktioner som lagts till i version 2023.1.0:

>[!VIDEO](https://video.tv.adobe.com/v/3413479/?quality=12)

## [!DNL Experience Manager Sites] som [!DNL Cloud Service] {#sites}

### Nya funktioner i [!DNL Sites] prerelease {#prerelease-features-sites}

* AEM GraphQL API för innehållsleverans har nu stöd för GraphQL [Sidindelning](/help/headless/graphql-api/content-fragments.md#paging) och [Sortering](/help/headless/graphql-api/content-fragments.md#sorting)för att göra det enklare att hämta och återge stora innehållsuppsättningar. Med GraphQL sidnumrering kan svarstiden för frågor förbättras genom att resultaten returneras i delmängder i motsats till alla samtidigt. Med GraphQL sortering kan du placera innehållsuppsättningar i önskad ordning, vilket gör det enklare för ett klientprogram att bearbeta innehållet.  Svarstiden för frågor har förbättrats ytterligare med Hybrid Filtering i den AEM GraphQL-motorn. Innehållet läses nu från JCR i mindre uppsättningar som motsvarar frågefilter.

## [!DNL Experience Manager Assets] som [!DNL Cloud Service] {#assets}

### Nya funktioner i [!DNL Assets] {#assets-features}

* Resursrapporter innehåller nu funktioner för administratörer att [generera rapporter om hämtning av resurser](/help/assets/asset-reports.md) från Experience Manager Assets as a Cloud Service driftsättning. Dessa data ger ytterligare möjligheter för administratörer att få insikt i viktiga framgångsmått för att mäta användningen av resurser inom företaget och av kunderna.

   ![PDF-återgivning för andra format](/help/release-notes/assets/choose_report.png)

* Experience Manager Assets nu [stöder SAS-token](/help/assets/add-assets.md#asset-bulk-ingestor) utöver åtkomstnyckeln för autentisering vid anslutning till Azure Blob Storage-datakällan för inmatning av resurser med verktyget för massimport.

* Förbättrad hantering av CMYK-bilder i Asset compute, vilket gör att du kan generera smarta beskärningar och smarta taggar för CMYK-bilder.

### Nya funktioner i [!DNL Assets] prerelease {#prerelease-features-assets}

* Experience Manager Assets har nu stöd för [storskalig import av resurser från Google Cloud Platform](/help/assets/add-assets.md#asset-bulk-ingestor) med verktyget Massimport.

## [!DNL Experience Manager Forms] som [!DNL Cloud Service] {#forms}

### Nya funktioner i [!DNL Forms] {#new-features-available-in-channel}

* **[Arbetsflödessteg för att generera icke-interaktiva PDF-dokument och utskrifter](/help/forms/aem-forms-workflow-step-reference.md)**: Automatisera framtagningen av icke-interaktiva PDF-dokument och utskrivbara dokument för era affärsprocesser med AEM arbetsflödessteg, effektivisera dokumentgenereringsprocessen och spara tid.
* **[Använd fotnoter för att ange citat eller extra information i Adaptive Forms](/help/forms/footnotes-richtextsupport.md)**: Använd Fotnoter i ett anpassat formulär för att visa information om hur du fyller i eller använder ett formulär. Du kan också använda den för att tillhandahålla parentetisk information, upphovsrättsbehörigheter och annan användbar information.

### Nya funktioner i [!DNL Forms] prerelease {#prerelease-features-forms}

* **[Använd kärnkomponenterna för datainhämtning för att bygga adaptiva Forms](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=en)**: [Använda adaptiv Forms-redigerare](/help/forms/creating-adaptive-form-core-components.md) för att skapa formulär baserade på standardiserade datainhämtningskomponenter (kärnkomponenter). Dessa komponenter har anpassningsmöjligheter, kortare utvecklingstid och lägre underhållskostnader för era digitala registreringsupplevelser.
* **[Stöd för Frontend-pipeline för styling core Component-baserad Adaptive Forms](/help/forms/using-themes-in-core-components.md)**: Använd enkelt anpassningsbara BEM-baserade teman för Core Components-baserade Adaptive Forms genom att använda dem med Frontend Deployment Pipeline för att förbättra utseendet och känslan i era formulär.
* **[Generera arkivdokument för centrala komponentbaserade adaptiva Forms](/help/forms/generate-document-of-record-core-components.md)**: Skapa en post för centrala komponentbaserade adaptiva formulär när de skickas för långtidsarkivering, i tryck eller i dokumentformat.

![https://www.aemcomponents.dev/](/help/forms/assets/sample-core-components-based-adaptive-form.png)

* **[Skicka anpassningsbara Forms till Microsoft SharePoint och Microsoft OneDrive](/help/forms/configuring-submit-actions.md)**: Effektivisera inlämningen av data med möjlighet att skicka data direkt till både Microsoft SharePoint och Microsoft OneDrive. Du kan skicka både schemabaserade och schemafria data. Dessa Skicka-åtgärder är utöver de som redan finns tillgängliga.
* **[Skapa formulär effektivt med funktionen Spara ett anpassat formulär som mall](/help/forms/template-editor.md#save-an-adaptive-form-as-template-saving-adaptive-form-as-template)**: Effektivisera formulärbyggandet genom att spara ett adaptivt formulär som en mall och återanvända mallarna för nästa adaptiva formulär.
* **[Ansluta AEM Forms till JDBC-databaser](/help/forms/configure-data-sources.md#configure-relational-database-configure-relational-database)**: Koppla enkelt din AEM Forms datamodell till databaser som stöder JDBC, så att du kan läsa och skriva data sömlöst.
* **[Integrera med REST-slutpunkter med Open API 3.0](/help/forms/configure-data-sources.md#configure-restful-services-open-api-specification-version-20-configure-restful-services-swagger-version30)**: Koppla samman AEM Forms as a Cloud Service Form Data Models till REST-slutpunkter med stöd för Open API-specifikationen version 3.0, så att du enkelt kan skicka och ta emot data.
* **[Dela ett adaptivt formulär för granskning](/help/forms/create-reviews-forms.md)**: Använd den adaptiva Forms granskningsfunktionen för att låta en eller flera granskare granska formuläret.

## [!DNL Experience Manager as a Cloud Service] Foundation {#foundation}

### Vad är nytt? {#what-is-new-foundation}

* [Snabba utvecklingsmiljöer](/help/implementing/developing/introduction/rapid-development-environments.md) - De tekniska utvecklingsverktygen gör det möjligt för utvecklare att snabbt felsöka problem och driftsätta nya funktioner på AEM as a Cloud Service.

   Snabba utvecklingsmiljöer är en ny typ av molnmiljö som är avsedd som ett snabbt, konsekvent och utbyggbart sätt att validera att koden fungerar lokalt, vilket också fungerar som väntat i molnet. Med kommandoradsverktygen kan du snabbt&quot;synkronisera&quot; innehållspaket, paket, innehållsfiler, OSGI-konfiguration eller dispatcherkonfiguration till RDE. Se hur det fungerar i videon nedan:

   >[!VIDEO](https://video.tv.adobe.com/v/3413508/?quality=12&learn=on)

   När du har validerat koden i den lokala utvecklingsmiljön bör du distribuera den till en molnutvecklingsmiljö för att träna Cloud Managers kvalitetsportar innan du distribuerar den via produktionsflödet till scen- och produktionsmiljöer.

   Varje program innehåller en RDE och eventuellt kan fler licensieras.

   >[!NOTE]
   >
   >De regionala utvecklingsföretagen kommer gradvis att byggas ut under de närmaste veckorna. Du kan skicka ett e-postmeddelande till aemcs-rde-support@adobe.com om du vill hoppa längst fram på raden.

* [Utökat stöd för API-åtkomsttoken på serversidan](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md) - Du kan nu generera flera autentiseringsuppgifter, vilket är användbart för scenarier där API:er har olika egenskaper. Nu går det även att återkalla inloggningsuppgifter på ett sätt som bygger på självbetjäning.

## Versionsinformation om underhåll {#maintenance}

Du kan hitta den senaste underhållsreleasenumerationen [här](/help/release-notes/maintenance/latest.md).

## Cloud Manager {#cloud-manager}

Du hittar en fullständig lista över månatliga utgåvor av Cloud Manager [här.](/help/implementing/cloud-manager/release-notes/current.md)

## Migreringsverktyg {#migration-tools}

Du hittar en fullständig lista över versioner av migreringsverktyg [här](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).

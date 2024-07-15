---
title: Versionsinformation för version 2023.1.0 av  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Versionsinformation för version 2023.1.0 av  [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: f134fdbc-224b-404c-b20f-44cae8bad681
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '975'
ht-degree: 0%

---

# Versionsinformation 2023.1.0 för [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

I följande avsnitt beskrivs versionsinformationen för funktionen för 2023.1.0-versionen av [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Härifrån kan du navigera till versionsinformation för tidigare versioner, till exempel för versionerna 2021, 2022 och så vidare.
>
>Ta en titt på [Experience Manager Releases Roadmap](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html) för att lära dig mer om kommande funktionsaktiveringar för [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Mer information om dokumentationsuppdateringar som inte är direkt relaterade till en release finns i [Senaste dokumentationsuppdateringar](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html).

## Releasedatum {#release-date}

Releasedatum [!DNL Adobe Experience Manager] som [!DNL Cloud Service] 2023.1.0-version är 9 februari 2023. Nästa funktionsversion (2023.2.0) är planerad till 12 april 2023.

## Släpp video {#release-video}

Titta på videon med versionsöversikten från januari 2023 om du vill se en sammanfattning av funktioner som lagts till i version 2023.1.0:

>[!VIDEO](https://video.tv.adobe.com/v/3413479/?quality=12)

## [!DNL Experience Manager Sites] som en [!DNL Cloud Service] {#sites}

### Nya funktioner i förhandsversionen av [!DNL Sites] {#prerelease-features-sites}

* AEM GraphQL API för innehållsleverans har nu stöd för GraphQL [Paging](/help/headless/graphql-api/content-fragments.md#paging) och [Sorting](/help/headless/graphql-api/content-fragments.md#sorting), vilket gör det enklare att hämta och återge stora innehållsuppsättningar. Med GraphQL sidnumrering kan svarstiden för frågor förbättras genom att resultaten returneras i delmängder i motsats till alla samtidigt. Med GraphQL sortering kan du placera innehållsuppsättningar i önskad ordning, vilket gör det enklare för ett klientprogram att bearbeta innehållet.  Svarstiden för frågor har förbättrats ytterligare med Hybrid Filtering i den AEM GraphQL-motorn. Innehållet läses nu från JCR i mindre uppsättningar som motsvarar frågefilter.

## [!DNL Experience Manager Assets] som en [!DNL Cloud Service] {#assets}

### Nya funktioner i [!DNL Assets] {#assets-features}

* Assets-rapporter innehåller nu möjligheten för administratörer att [generera rapporter om hämtning av resurser](/help/assets/asset-reports.md) från Experience Manager Assets as a Cloud Service-distributionen. Dessa data ger ytterligare möjligheter för administratörer att få insikt i viktiga framgångsmått för att mäta hur väl Assets används i ert företag och av era kunder.

  ![PDF-återgivning för andra format](/help/release-notes/assets/choose_report.png)

* Experience Manager Assets [har nu stöd för SAS-token](/help/assets/add-assets.md#asset-bulk-ingestor) förutom åtkomstnyckeln för autentisering vid anslutning till Azure Blob Storage-datakällan för inhämtning av resurser med verktyget för massimport.

* Förbättrad hantering av CMYK-bilder i Asset compute, vilket gör att du kan generera smarta beskärningar och smarta taggar för CMYK-bilder.

### Nya funktioner i förhandsversionen av [!DNL Assets] {#prerelease-features-assets}

* Experience Manager Assets har nu stöd för [storskalig import av resurser från Google Cloud-plattformen](/help/assets/add-assets.md#asset-bulk-ingestor) med verktyget Massimport.

## [!DNL Experience Manager Forms] som en [!DNL Cloud Service] {#forms}

### Nya funktioner tillgängliga i [!DNL Forms] {#new-features-available-in-channel}

* **[Arbetsflödessteg för att generera icke-interaktiva PDF-dokument och utskrivbara utdata](/help/forms/aem-forms-workflow-step-reference.md)**: Automatisera skapandet av icke-interaktiva PDF-dokument och utskrivbara utdata för affärsprocesserna med AEM arbetsflödessteg, effektivisera dokumentgenereringsprocessen och spara tid.
* **[Använd fotnoter för att ange citat eller extra information i Adaptiv Forms](/help/forms/footnotes-richtextsupport.md)**: Använd fotnoter i ett adaptiv formulär för att visa information om hur du fyller i eller använder ett formulär. Du kan också använda den för att tillhandahålla parentetisk information, upphovsrättsbehörigheter och annan användbar information.

### Nya funktioner i förhandsversionen av [!DNL Forms] {#prerelease-features-forms}

* **[Använd kärnkomponenter för datainhämtning för att skapa adaptiva Forms](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)**: [Använd den adaptiva Forms-redigeraren](/help/forms/creating-adaptive-form-core-components.md) för att skapa formulär baserade på standardiserade datainhämtningskomponenter (kärnkomponenter). Dessa komponenter har anpassningsmöjligheter, kortare utvecklingstid och lägre underhållskostnader för era digitala registreringsupplevelser.
* **[Stöd för frontend-pipeline för att utforma kärnkomponentbaserade adaptiva Forms](/help/forms/using-themes-in-core-components.md)**: Använd enkelt anpassningsbara BEM-baserade teman för Core Components-baserade Adaptive Forms genom att distribuera dem med Frontend Deployment Pipeline för att förbättra utseendet och känslan i formulären.
* **[Generera arkivdokument för huvudkomponentbaserade adaptiva Forms](/help/forms/generate-document-of-record-core-components.md)**: Skapa en post för huvudkomponentbaserade adaptiva formulär när de skickas för långtidsarkivering, i utskrift eller i dokumentformat.

![https://www.aemcomponents.dev/](/help/forms/assets/sample-core-components-based-adaptive-form.png)

* **[Skicka adaptiv Forms till Microsoft SharePoint och Microsoft OneDrive](/help/forms/configuring-submit-actions.md)**: Effektivisera dataöverföringen genom att skicka adaptiva formulärdata direkt till både Microsoft SharePoint och Microsoft OneDrive. Du kan skicka både schemabaserade och schemafria data. Dessa Skicka-åtgärder är utöver de som redan finns tillgängliga.
* **[Effektiv formulärutveckling med funktionen Spara ett adaptivt formulär som en mall](/help/forms/template-editor.md#save-an-adaptive-form-as-template-saving-adaptive-form-as-template)**: Effektiv formulärgenereringsprocess genom att spara ett adaptivt formulär som en mall och återanvända mallarna för nästa adaptiva formulär.
* **[Anslut AEM Forms till JDBC-stödda databaser](/help/forms/configure-data-sources.md#configure-relational-database-configure-relational-database)**: Anslut enkelt AEM Forms-datamodellen till databaser som stöder JDBC, så att du kan läsa och skriva data sömlöst.
* **[Integrera med REST-slutpunkter med Open API 3.0](/help/forms/configure-data-sources.md#configure-restful-services-open-api-specification-version-20-configure-restful-services-swagger-version30)**: Anslut AEM Forms as a Cloud Service formulärdatamodeller till REST-slutpunkter med stöd för Open API-specifikation version 3.0, så att du enkelt kan skicka och ta emot data.
* **[Dela ett anpassat formulär för granskning](/help/forms/create-reviews-forms.md)**: Använd den adaptiva Forms-granskningsfunktionen för att tillåta en eller flera granskare att granska formuläret.

## [!DNL Experience Manager as a Cloud Service] Foundation {#foundation}

### Nyheter {#what-is-new-foundation}

* [Snabba utvecklingsmiljöer](/help/implementing/developing/introduction/rapid-development-environments.md) - Med RDE kan utvecklare snabbt felsöka problem och distribuera nya funktioner på AEM as a Cloud Service.

  Snabba utvecklingsmiljöer är en ny typ av molnmiljö som är avsedd som ett snabbt, konsekvent och utbyggbart sätt att validera att koden fungerar lokalt, vilket också fungerar som väntat i molnet. Med kommandoradsverktygen kan du snabbt&quot;synkronisera&quot; innehållspaket, paket, innehållsfiler, OSGI-konfiguration eller dispatcherkonfiguration till RDE. Se hur det fungerar i videon nedan:

  >[!VIDEO](https://video.tv.adobe.com/v/3413508/?quality=12&learn=on)

  När du har validerat koden i den lokala utvecklingsmiljön bör du distribuera den till en molnutvecklingsmiljö för att utnyttja Cloud Manager-kvalitetsgates innan du distribuerar den via produktionsflödet till scen- och produktionsmiljöer.

  Varje program innehåller en RDE och eventuellt kan fler licensieras.

  >[!NOTE]
  >
  >De kommer gradvis att lanseras under de närmaste veckorna. Du kan skicka ett e-postmeddelande till aemcs-rde-support@adobe.com och hoppa till radens framsida.

* [Utökat stöd för API-åtkomsttoken på serversidan](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md) - Du kan nu generera flera autentiseringsuppgifter, vilket är användbart för scenarier där API:er har olika egenskaper. Nu går det även att återkalla inloggningsuppgifter på ett sätt som bygger på självbetjäning.

## Versionsinformation om underhåll {#maintenance}

Du hittar den senaste underhållsversionsinformationen [här](/help/release-notes/maintenance/latest.md).

## Cloud Manager {#cloud-manager}

Du hittar en fullständig lista över månadsutgåvor av Cloud Manager [här](/help/implementing/cloud-manager/release-notes/current.md).

## Migreringsverktyg {#migration-tools}

Du hittar en fullständig lista över migreringsverktygen [här](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).

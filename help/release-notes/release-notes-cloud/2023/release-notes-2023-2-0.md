---
title: Versionsinformation om 2023.2.0-utgåvan av  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Versionsinformation om 2023.2.0-utgåvan av  [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: 671056e6-84cc-4c2c-bca3-fde68d5cc835
feature: Release Information
role: Admin
source-git-commit: b4ffcddddfcd990c359380071f19b5442dee9eb2
workflow-type: tm+mt
source-wordcount: '716'
ht-degree: 0%

---

# Versionsinformation 2023.2.0 för [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

I följande avsnitt beskrivs versionsinformationen för funktionen för 2023.2.0-versionen av [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Härifrån kan du navigera till versionsinformation för tidigare versioner, till exempel för versionerna 2021, 2022 och så vidare.
>
>Ta en titt på [Experience Manager Releases Roadmap](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=sv-SE) om du vill veta mer om kommande funktionsaktiveringar för [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Mer information om dokumentationsuppdateringar som inte är direkt relaterade till en release finns i [Senaste dokumentationsuppdateringar](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=sv-SE).

## Releasedatum {#release-date}

Releasedatum för [!DNL Adobe Experience Manager] som [!DNL Cloud Service] aktuell funktionsversion (2023.2.0) är 12 april 2023. Nästa version (2023.4.0) är planerad till 7 juni 2023.

## Släpp video {#release-video}

Titta på videon med versionsöversikten från februari 2023 om du vill se en sammanfattning av funktioner som lagts till i version 2023.2.0:

>[!VIDEO](https://video.tv.adobe.com/v/3416885/?quality=12)

## [!DNL Experience Manager Sites] som en [!DNL Cloud Service] {#sites}

### Nya funktioner i förhandsversionen av [!DNL Experience Manager Sites] {#prerelease-sites}

* Exportera innehållsfragment från AEM som en molntjänst till Adobe som JSON erbjuder.
* Stöd för sidnumrering och sortering i GraphQL, tillsammans med förbättringar för intern cachning, hjälper nu till att förbättra prestanda i fristående klientprogram när du hämtar stora innehållsuppsättningar från AEM med komplexa GraphQL-frågor och filter.

## [!DNL Experience Manager Assets] som en [!DNL Cloud Service] {#assets}

### Nya funktioner i [!DNL Assets] {#assets-features}

* Stöd för nytt protokoll (DASH - Dynamic Adaptive Streaming over HTTP) har startats för adaptiv strömning i Dynamic Media Video Delivery (med CMAF aktiverat):
   * Adaptiv direktuppspelning (DASH/HLS) ger en bättre användarupplevelse för videor
   * DASH är det internationella standardprotokollet för strömning av adaptiv video och används ofta i branschen

* Stöd för WebP-bilder som automatiskt extraherar metadata, genererar miniatyrbilder och anpassade renderingar. Funktioner för smarta taggar och smart beskärning stöds nu även för dessa filer.

## [!DNL Experience Manager Forms] som en [!DNL Cloud Service] {#forms}

### Nya funktioner tillgängliga i [!DNL Forms] {#new-features-available-in-channel}

* **[Använd kärnkomponenter för datainhämtning för att skapa adaptiva Forms](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=sv-SE)**: [Använd den adaptiva Forms-redigeraren](/help/forms/creating-adaptive-form-core-components.md) för att skapa formulär baserade på standardiserade datainhämtningskomponenter (kärnkomponenter). Dessa komponenter har anpassningsmöjligheter, kortare utvecklingstid och lägre underhållskostnader för era digitala registreringsupplevelser.

* **[Stöd för frontend-pipeline för att utforma kärnkomponentbaserade adaptiva Forms](/help/forms/using-themes-in-core-components.md)**: Använd standardiserade BEM-baserade teman för Core Components-baserade Adaptive Forms genom att distribuera dem med Frontend Deployment Pipeline för att förbättra utseendet på och känslan i formulären och anpassa dem efter företagets varumärkesgodkända riktlinjer för designen.

* **[Generera arkivdokument för huvudkomponentbaserade adaptiva Forms](/help/forms/generate-document-of-record-core-components.md)**: Skapa ett dokument med inskickade data för adaptiva Forms som skapats med hjälp av kärnkomponenter för arkivering eller referens till slutanvändare, i utskrift eller i dokumentformat.

![https://www.aemcomponents.dev/](/help/forms/assets/sample-core-components-based-adaptive-form.png)

* **[Effektiv formulärutveckling med funktionen Spara ett anpassat formulär som en mall](/help/forms/template-editor.md#save-an-adaptive-form-as-template-saving-adaptive-form-as-template)**: Snabba upp och standardisera formulärutvecklingen genom att spara befintliga varumärkesgodkända formulär som formulärmallar för snabb återanvändning.

* **[Anslut AEM Forms till JDBC-stödda databaser](/help/forms/configure-data-sources.md#configure-relational-database-configure-relational-database)**: Anslut till företagsdatabaser direkt från AEM Cloud-tjänsten med JDBC-protokoll, utan att behöva visa dem via REST API.

* **[Integrera med REST-slutpunkter med Open API 3.0](/help/forms/configure-data-sources.md#configure-restful-services-open-api-specification-version-20-configure-restful-services-swagger-version30)**: Integrera sömlöst i postsystem som stöder Open API 3.0 för att lagra och hämta data med hjälp av formulärdatamodeller.

* **[Dela ett anpassat formulär för granskning](/help/forms/create-reviews-forms.md)**: Använd den adaptiva Forms-granskningsfunktionen för att tillåta en eller flera granskare att granska formuläret.


### Funktioner i förhandsversionen av [!DNL Forms] {#prerelease-features-forms}

* **[Skicka adaptiva Forms till Microsoft SharePoint och Microsoft OneDrive](/help/forms/configuring-submit-actions.md)**: Förbättra affärsanvändarnas möjlighet att snabbt starta nya formulär och lagra inskickade data i vardagliga verktyg som de använder, som Microsoft SharePoint webbplats eller OneDrive-mapp.

![Skicka anpassad Forms till Microsoft SharePoint och Microsoft OneDrive](/help/forms/assets/onedrive-and-sharepoint.jpg)


## Headless Adaptive Forms early adopter {#forms-early-adopter}

Med Headless Adaptive Forms kan utvecklarna skapa, publicera och hantera interaktiva blanketter som kan öppnas och interagera med via API:er i stället för via ett traditionellt grafiskt användargränssnitt. Headless adaptive forms help you:

* bygga högkvalitativa flerkanalsformulär på valfritt programmeringsspråk
* integrera formulär direkt i era datorprogram och mobilappar, webbplatser och chattapplikationer
* återanvända era egna gränssnittskomponenter med blankettapplikationer
* använder kraften i Adobe Experience Manager Forms

Du kan skicka ett e-postmeddelande till aem-forms-headless@adobe.com från ditt officiella e-post-ID för att gå med i det tidiga adopterprogrammet.

## Versionsinformation om underhåll {#maintenance}

Du hittar den senaste underhållsversionsinformationen [här](/help/release-notes/maintenance/latest.md).

## Cloud Manager {#cloud-manager}

Du hittar en fullständig lista över månadsutgåvor av Cloud Manager [här](/help/implementing/cloud-manager/release-notes/current.md).

## Migreringsverktyg {#migration-tools}

Du hittar en fullständig lista över migreringsverktygen [här](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).

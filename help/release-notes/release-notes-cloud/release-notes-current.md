---
title: Aktuell versionsinformation för [!DNL Adobe Experience Manager] as a Cloud Service.
description: Aktuell versionsinformation för [!DNL Adobe Experience Manager] as a Cloud Service.
mini-toc-levels: 1
source-git-commit: 085ce15ebe4d48d32a437f13e728f60cfc57d0fa
workflow-type: tm+mt
source-wordcount: '733'
ht-degree: 0%

---


# Aktuell versionsinformation för [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

I följande avsnitt beskrivs versionsinformationen för funktionen för den aktuella (senaste) versionen av [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Härifrån kan du navigera till versionsinformation för tidigare versioner; till exempel för 2021, 2022 och så vidare.
>
>Ta en titt på [Roadmap för lansering av Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html) om de kommande funktionsaktiviteterna för [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Se [Senaste dokumentationsuppdateringar](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html) för information om dokumentationsuppdateringar som inte är direkt relaterade till en release.

## Releasedatum {#release-date}

Releasedatum [!DNL Adobe Experience Manager] som [!DNL Cloud Service] aktuell version (2023.2.0) är 12 april 2023. Nästa funktionsversion (2023.4.0) är planerad till 27 april 2023.

## Släpp video {#release-video}

Titta på videon med versionsöversikten från februari 2023 om du vill se en sammanfattning av funktioner som lagts till i version 2023.2.0:

>[!VIDEO](https://video.tv.adobe.com/v/3416885/?quality=12)

## [!DNL Experience Manager Sites] som [!DNL Cloud Service] {#sites}

### Nya funktioner i [!DNL Experience Manager Sites] förleasa {#prerelease-sites}

* Exportera innehållsfragment från AEM som en molntjänst till Adobe som JSON erbjuder.
* Stöd för sidnumrering och sortering i GraphQL, tillsammans med förbättringar för intern cachning, hjälper nu till att förbättra prestanda i fristående klientprogram när du hämtar stora innehållsuppsättningar från AEM med komplexa GraphQL-frågor och filter.

## [!DNL Experience Manager Assets] som [!DNL Cloud Service] {#assets}

### Nya funktioner i [!DNL Assets] {#assets-features}

* Stöd för nytt protokoll (DASH - Dynamic Adaptive Streaming over HTTP) har startats för adaptiv strömning i Dynamic Media (med CMAF aktiverat):
   * Adaptiv direktuppspelning (DASH/HLS) ger en bättre visningsupplevelse för videor
   * DASH är det internationella standardprotokollet för strömning av adaptiv video och används ofta i branschen
   * Finns i NA, att aktiveras via supportanmälan, kommer snart i APAC, EMEA

* Stöd för WebP-bilder som automatiskt extraherar metadata, genererar miniatyrbilder och anpassade renderingar. Funktioner för smarta taggar och smart beskärning stöds nu även för dessa filer.

## [!DNL Experience Manager Forms] som [!DNL Cloud Service] {#forms}

### Nya funktioner i [!DNL Forms] {#new-features-available-in-channel}

* **[Använd kärnkomponenterna för datainhämtning för att bygga adaptiva Forms](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=en)**: [Använda adaptiv Forms-redigerare](/help/forms/creating-adaptive-form-core-components.md) för att skapa formulär baserade på standardiserade datainhämtningskomponenter (kärnkomponenter). Dessa komponenter har anpassningsmöjligheter, kortare utvecklingstid och lägre underhållskostnader för era digitala registreringsupplevelser.

* **[Stöd för Frontend-pipeline för styling core Component-baserad Adaptive Forms](/help/forms/using-themes-in-core-components.md)**: Utnyttja standardiserade BEM-baserade teman för Core Components-baserade Adaptive Forms genom att använda dem med Frontend Deployment Pipeline för att förbättra utseendet och känslan i era formulär och anpassa dem efter företagets varumärkesgodkända riktlinjer.

* **[Generera arkivdokument för centrala komponentbaserade adaptiva Forms](/help/forms/generate-document-of-record-core-components.md)**: Skapa ett urkunder som innehåller inlämnade data för Adaptive Forms som byggts med hjälp av centrala komponenter för arkivering eller referens till slutanvändare, i utskrift eller i dokumentformat.

![https://www.aemcomponents.dev/](/help/forms/assets/sample-core-components-based-adaptive-form.png)

* **[Skapa formulär effektivt med funktionen Spara ett anpassat formulär som mall](/help/forms/template-editor.md#save-an-adaptive-form-as-template-saving-adaptive-form-as-template)**: Snabba upp och standardisera blankettutvecklingen genom att spara befintliga blanketter som godkänts av varumärket som blankettmallar för snabb återanvändning.

* **[Ansluta AEM Forms till JDBC-databaser](/help/forms/configure-data-sources.md#configure-relational-database-configure-relational-database)**: Anslut till företagsdatabaser direkt från AEM Cloud-tjänsten med JDBC-protokoll, utan att behöva visa dem via REST API.

* **[Integrera med REST-slutpunkter med Open API 3.0](/help/forms/configure-data-sources.md#configure-restful-services-open-api-specification-version-20-configure-restful-services-swagger-version30)**: Integrera smidigt i databassystem som stöder Open API 3.0 för att lagra och hämta data med hjälp av formulärdatamodeller.

* **[Dela ett adaptivt formulär för granskning](/help/forms/create-reviews-forms.md)**: Använd den adaptiva Forms granskningsfunktionen för att låta en eller flera granskare granska formuläret.


### Funktioner i [!DNL Forms] prerelease {#prerelease-features-forms}

* **[Skicka anpassningsbara Forms till Microsoft SharePoint och Microsoft OneDrive](/help/forms/configuring-submit-actions.md)**: Förbättra affärsanvändarnas möjligheter att snabbt öppna nya formulär och lagra inlämnade data i vardagliga verktyg som de använder som Microsoft SharePoint webbplats eller OneDrive-mapp.

![Skicka anpassningsbara Forms till Microsoft SharePoint och Microsoft OneDrive](/help/forms/assets/onedrive-and-sharepoint.jpg)


## Headless Adaptive Forms early adopter {#forms-early-adopter}

Med Headless Adaptive Forms kan utvecklarna skapa, publicera och hantera interaktiva blanketter som kan öppnas och interagera med via API:er i stället för via ett traditionellt grafiskt användargränssnitt. Headless adaptive forms help you:

* bygga högkvalitativa flerkanalsformulär på valfritt programmeringsspråk
* integrera formulär direkt i era datorprogram och mobilappar, webbplatser och chattapplikationer
* återanvända era egna gränssnittskomponenter med blankettapplikationer
* utnyttja kraften i Adobe Experience Manager Forms

Du kan skicka ett e-postmeddelande till aem-forms-headless@adobe.com från ditt officiella e-post-ID för att gå med i det tidiga adopterprogrammet.

## Versionsinformation om underhåll {#maintenance}

Du kan hitta den senaste underhållsreleasenumerationen [här](/help/release-notes/maintenance/latest.md).

## Cloud Manager {#cloud-manager}

Du hittar en fullständig lista över månatliga utgåvor av Cloud Manager [här.](/help/implementing/cloud-manager/release-notes/current.md)

## Migreringsverktyg {#migration-tools}

Du hittar en fullständig lista över versioner av migreringsverktyg [här](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).

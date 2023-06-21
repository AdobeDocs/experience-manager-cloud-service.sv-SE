---
title: Aktuell versionsinformation för [!DNL Adobe Experience Manager] as a Cloud Service.
description: Aktuell versionsinformation för [!DNL Adobe Experience Manager] as a Cloud Service.
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
source-git-commit: ca4046a94301cebae9e7a46e055977419fedd14e
workflow-type: tm+mt
source-wordcount: '1095'
ht-degree: 0%

---

# Aktuell versionsinformation för [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

I följande avsnitt beskrivs versionsinformationen för funktionen för den aktuella (senaste) versionen av [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Härifrån kan du navigera till versionsinformation för tidigare versioner som 2021 eller 2022.
>
>Ta en titt på [Roadmap för lansering av Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html) om de kommande funktionsaktiviteterna för [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Se [Senaste dokumentationsuppdateringar](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html) för information om dokumentationsuppdateringar som inte är direkt relaterade till en release.

## Releasedatum {#release-date}

Releasedatum [!DNL Adobe Experience Manager] som [!DNL Cloud Service] aktuell version (2023.4.0) är 7 juni 2023. Nästa version (2023.6.0) är planerad till 29 juni 2023.

## Släpp video {#release-video}

Titta på videon med versionsöversikten för april 2023 om du vill se en sammanfattning av funktioner som lagts till i version 2023.4.0:

>[!VIDEO](https://video.tv.adobe.com/v/3418681/?quality=12)

## [!DNL Experience Manager Sites] som [!DNL Cloud Service] {#sites}

### Nya funktioner i [!DNL Experience Manager Sites] {#sites-features}

* Exportera innehållsfragment från AEM som en molntjänst till Adobe som JSON erbjuder.
* Stöd för sidnumrering och sortering i GraphQL, tillsammans med förbättringar för intern cachning, hjälper nu till att förbättra prestanda i fristående klientprogram när du hämtar stora innehållsuppsättningar från AEM med komplexa GraphQL-frågor och filter.

### Nya funktioner i [!DNL Experience Manager Sites] prerelease {#prerelease-sites}

* Innehållsfragment och deras referenser kan nu publiceras i [Tjänsten AEM Preview](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-environments.html?lang=en#access-preview-service) med [Konsol för innehållsfragment](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/content-fragments/content-fragments-console.html?lang=en), vilket gör att användarna kan förhandsgranska slutresultatet i ett fristående förhandsvisningsprogram innan de publicerar.

## [!DNL Experience Manager Assets] som [!DNL Cloud Service] {#assets}

### Nya funktioner i [!DNL Assets] {#assets-features}

* Stöd för WebP-bilder som automatiskt extraherar metadata, genererar miniatyrbilder och anpassade renderingar. Funktionen Smarta taggar stöds nu även för dessa filer. Dynamic Media-funktioner stöds inte för WebP som indataformat.

* [Förbättrade sökupplevelser](/help/assets/search-assets.md#aftersearch) - Du kan nu snabbt utföra följande åtgärder på resurserna som visas i sökresultaten:

   * Skapa ett arbetsflöde
   * Skapa en version
   * Relatera eller inte relatera tillgångar

     Du behöver inte navigera till resursplatsen och visa dess egenskaper för att utföra dessa åtgärder.

* Förbättrad användbarhet för färgsökningsaspekten - Indatafältet för färgvärden kan nu redigeras och sökresultaten uppdateras endast när du avslutar färgväljaren.

* Nytt protokollstöd har startats (DASH - Dynamic Adaptive Streaming over HTTP) för adaptiv strömning i Dynamic Media (med CMAF aktiverat):
   * Adaptiv direktuppspelning (DASH/HLS) ger en bättre visningsupplevelse för videor
   * DASH är det internationella standardprotokollet för strömning av adaptiv video och används ofta i branschen
   * Tillgängligt i alla regioner, för att aktiveras via supportanmälan

* Dynamic Media _Ögonblicksbild_ - Experimentera med testbilder eller Dynamic Media-URL:er för att se utdata från olika bildmodifierare och utvärdera smarta bildoptimeringar för filstorlek (med WebP- och AVIF-leverans), nätverksbandbredd och Device Pixel Ratio. Se [Dynamic Media Snapshot](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-snapshot.html).

### Funktion i [!DNL Assets] prerelease {#prerelease-feature-assets}

* Dynamic Media - Användargränssnittet för vissa Smart Crop-relaterade fält i en bildprofil har nu uppdaterats för att återspegla de aktuella riktlinjerna för att definiera en smart beskärning. Se [Beskärningsalternativ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/image-profiles.html?lang=en#crop-options).

## [!DNL Experience Manager Forms] som [!DNL Cloud Service] {#forms}

### Nya funktioner i [!DNL Forms] {#new-features-available-in-channel}

* **[Skicka anpassningsbara Forms till Microsoft® SharePoint och Microsoft® OneDrive](/help/forms/configuring-submit-actions.md)**: Öka användarflexibiliteten så att ni snabbt kan starta nya formulär och lagra inlämnade data i vardagliga verktyg som Microsoft® SharePoint eller OneDrive.

### Funktioner i [!DNL Forms] prerelease {#prerelease-features-forms}

* [Adaptiv Forms i AEM Page Editor](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md): Nu kan du använda AEM Page Editor för att snabbt skapa och lägga till flera formulär på webbplatsens sidor. Med den här funktionen kan skribenter skapa sömlösa datainhämtningsmöjligheter på webbplatssidor med hjälp av kraften i adaptiva formulärkomponenter, inklusive dynamiskt beteende, validering, dataintegrering, generering av dokument för post- och affärsprocessautomatisering. Du kan:

   * Skapa ett anpassat formulär genom att dra och släppa formulärkomponenter i den adaptiva Forms Container-komponenten i AEM Sites Editor eller Experience Fragments.
   * Använd Adaptive Forms Wizard i AEM Sites Editor för att skapa formulär oberoende av sajtsidor, vilket ger dig frihet att återanvända sådana formulär på flera sidor.
   * Lägg till flera formulär på en webbplatssida, effektivisera användarupplevelsen och ge större flexibilitet.

     >[!VIDEO](https://video.tv.adobe.com/v/3419284?quality=12&learn=on)

* [Förbättrad integrering och efterlevnad av Adobe Acrobat Sign](/help/forms/adobe-sign-integration-adaptive-forms.md): AEM Forms kan nu integreras med Adobe Acrobat Sign för myndigheter. Integreringen ger en avancerad nivå av regelefterlevnad och säkerhet för e-signaturer med inskickade adaptiva formulär för myndighetskonton (myndigheter och myndigheter).

  Integrationen med Adobe Acrobat Sign for Government gör det möjligt för Adobe och myndighetskunder att använda elektroniska signaturer i Adaptive Forms för några av de mest verksamhetskritiska och känsliga verksamhetsområdena. Detta extra säkerhetsskikt säkerställer att alla e-signaturer är helt kompatibla med FedRAMP Moderate-kompatibiliteten, vilket ger Adobe myndighetskunder sinnesro.

* Förbättrad felhantering med anpassade felhanterare i regelredigeraren. Du kan nu anropa en anpassad funktion (med Klientbibliotek) som svar på ett fel som returnerats av en extern tjänst och ge ett skräddarsytt svar till slutanvändarna. Du kan också vidta specifika åtgärder för fel som returneras av en tjänst. Du kan till exempel anropa ett anpassat arbetsflöde i serverdelen för specifika felkoder eller informera kunden om att tjänsten inte fungerar.

  Den här funktionen förbättrar den övergripande felhanteringskapaciteten genom att införa standardbaserade felsvar som är bakåtkompatibla med OOTB-felhanterare, med större flexibilitet och kontroll.

### Headless Adaptive Forms early adopter {#forms-early-adopter}

Med Headless Adaptive Forms kan utvecklarna skapa, publicera och hantera interaktiva blanketter som kan öppnas och interagera med via API:er i stället för via ett traditionellt grafiskt användargränssnitt. Headless adaptive forms help you:

* bygga högkvalitativa flerkanalsformulär på valfritt programmeringsspråk
* integrera formulär direkt i era datorprogram och mobilappar, webbplatser och chattapplikationer
* återanvända era egna gränssnittskomponenter med blankettapplikationer
* använder kraften i Adobe Experience Manager Forms

Du kan skicka ett e-postmeddelande till `aem-forms-headless@adobe.com` från ditt officiella e-post-ID till att gå med i det tidiga adopterprogrammet.

## [!DNL Experience Manager] som [!DNL Cloud Service] Foundation {#foundation}

### Vad är nytt? {#what-is-new-foundation}

* Ytterligare publiceringsregioner: Webbplatser Kunder kan licensiera upp till tre publiceringsregioner utöver den primära regionen. Trafiken dirigeras till ytterligare publiceringsanläggningar, vilket leder till minskad fördröjning för vissa förfrågningar och ökad motståndskraft mot regionala avbrott. Kontakta kontohanteraren för Adobe om du vill ha information om licensiering [Ytterligare publiceringsregioner](/help/operations/additional-publish-regions.md) för programmen.

## Versionsinformation om underhåll {#maintenance}

Du kan hitta den senaste underhållsreleasenumerationen [här](/help/release-notes/maintenance/latest.md).

## Cloud Manager {#cloud-manager}

Du hittar en fullständig lista över månatliga utgåvor av Cloud Manager [här.](/help/implementing/cloud-manager/release-notes/current.md)

## Migreringsverktyg {#migration-tools}

Du hittar en fullständig lista över versioner av migreringsverktyg [här](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).

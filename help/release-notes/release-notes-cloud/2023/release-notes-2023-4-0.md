---
title: Versionsinformation om 2023.4.0-utgåvan av  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Versionsinformation om 2023.4.0-utgåvan av  [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: c34aedee-e45a-4e2a-ae7f-930bc0cc026f
feature: Release Information
role: Admin
source-git-commit: b4ffcddddfcd990c359380071f19b5442dee9eb2
workflow-type: tm+mt
source-wordcount: '1112'
ht-degree: 0%

---

# Versionsinformation 2023.4.0 för [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

I följande avsnitt beskrivs versionsinformationen för funktionen för 2023.4.0-versionen av [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Härifrån kan du navigera till versionsinformation för tidigare versioner som 2021 eller 2022.
>
>Ta en titt på [Experience Manager Releases Roadmap](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html) om du vill veta mer om kommande funktionsaktiveringar för [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Mer information om dokumentationsuppdateringar som inte är direkt relaterade till en release finns i [Senaste dokumentationsuppdateringar](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html).

## Releasedatum {#release-date}

Releasedatum för [!DNL Adobe Experience Manager] som aktuell funktionsversion av [!DNL Cloud Service] (2023.4.0) är 7 juni 2023. Nästa version (2023.6.0) är planerad till 29 juni 2023.

## Släpp video {#release-video}

Titta på videon med versionsöversikten för april 2023 om du vill se en sammanfattning av funktioner som lagts till i version 2023.4.0:

>[!VIDEO](https://video.tv.adobe.com/v/3418681/?quality=12)

## [!DNL Experience Manager Sites] som en [!DNL Cloud Service] {#sites}

### Nya funktioner i [!DNL Experience Manager Sites] {#sites-features}

* Exportera innehållsfragment från AEM as a Cloud Service till Adobe Target i JSON-format och skapa motsvarande JSON-erbjudanden i Target.
* Stöd för sidnumrering och sortering i GraphQL, tillsammans med förbättringar för intern cachning, hjälper nu till att förbättra prestanda i fristående klientprogram när du hämtar stora innehållsuppsättningar från AEM med komplexa GraphQL-frågor och filter.

### Nya funktioner i förhandsversionen av [!DNL Experience Manager Sites] {#prerelease-sites}

* Innehållsfragment och deras referenser kan nu publiceras till [AEM Preview Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-environments.html#access-preview-service) med [Content Fragment Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/content-fragments/content-fragments-console.html) så att användarna kan förhandsgranska slutresultatet i ett fristående förhandsvisningsprogram innan de publiceras.
* Bilderna kan nu optimeras dynamiskt för webbleverans i headless-scenarier med AEM GraphQL. [Frågevariabler](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/how-to/images.html#query-variables) kan definieras i GraphQL-frågor för att tillåta att fristående klientprogram begär optimerade bilder från AEM.
* Taggar på [Variationer för innehållsfragment](https://experienceleague.adobe.com/docs/experience-manager-65/assets/content-fragments/content-fragments-variations.html) kan nu skrivas ut till JSON med AEM GraphQL-innehållets leverans-API.

## [!DNL Experience Manager Assets] som en [!DNL Cloud Service] {#assets}

### Nya funktioner i [!DNL Assets] {#assets-features}

* Stöd för WebP-bilder som automatiskt extraherar metadata, genererar miniatyrbilder och anpassade renderingar. Funktionen Smarta taggar stöds nu även för dessa filer. Dynamiska mediefunktioner stöds inte för WebP som indataformat.

* [Förbättringar av sökupplevelsen](/help/assets/search-assets.md#aftersearch) - Nu kan du snabbt utföra följande åtgärder på resurserna som visas i sökresultaten:

   * Skapa ett arbetsflöde
   * Skapa en version
   * Relatera eller inte relatera tillgångar

     Du behöver inte navigera till resursplatsen och visa dess egenskaper för att utföra dessa åtgärder.

* Förbättrad användbarhet för färgsökningsaspekten - Indatafältet för färgvärden kan nu redigeras och sökresultaten uppdateras endast när du avslutar färgväljaren.

* Nytt protokollstöd har startats (DASH - Dynamic Adaptive Streaming over HTTP) för adaptiv strömning i Dynamic Media-leverans (med CMAF aktiverat):
   * Adaptiv direktuppspelning (DASH/HLS) ger en bättre användarupplevelse för videor
   * DASH är det internationella standardprotokollet för strömning av adaptiv video och används ofta i branschen

* Dynamic Media _Snapshot_ - Experimentera med testbilder eller dynamiska medie-URL:er för att se utdata från olika bildmodifierare och utvärdera optimeringarna av smarta bilder för filstorlek (med WebP- och AVIF-leverans), nätverksbandbredd och enhetspixelproportioner. Se [Dynamisk medieögonblicksbild](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-snapshot.html).

### Funktion i förhandsversionen av [!DNL Assets] {#prerelease-feature-assets}

* Dynamiska media - Användargränssnittet för vissa Smart Crop-relaterade fält i en bildprofil har nu uppdaterats för att återspegla de aktuella riktlinjerna för att definiera en smart beskärning. Se [Beskärningsalternativ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/image-profiles.html#crop-options).

## [!DNL Experience Manager Forms] som en [!DNL Cloud Service] {#forms}

### Nya funktioner tillgängliga i [!DNL Forms] {#new-features-available-in-channel}

* **[Skicka adaptiva Forms till Microsoft® SharePoint och Microsoft® OneDrive](/help/forms/configuring-submit-actions.md)**: Förbättra användarflexibiliteten så att du snabbt kan starta nya formulär och lagra inskickade data i vanliga verktyg som Microsoft® SharePoint eller OneDrive-mappen.

### Funktioner i förhandsversionen av [!DNL Forms] {#prerelease-features-forms}

* [Adaptiv Forms i AEM sidredigerare](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md): Nu kan du använda AEM sidredigerare för att snabbt skapa och lägga till flera formulär på webbplatsens sidor. Med den här funktionen kan skribenter skapa sömlösa datainhämtningsmöjligheter på webbplatssidor med hjälp av kraften i adaptiva formulärkomponenter, inklusive dynamiskt beteende, validering, dataintegrering, generering av dokument för post- och affärsprocessautomatisering. Du kan:

   * Skapa ett anpassat formulär genom att dra och släppa formulärkomponenter i den adaptiva Forms Container-komponenten i AEM Sites Editor eller Experience Fragments.
   * Använd Adaptive Forms Wizard i AEM Sites Editor för att skapa formulär oberoende av sajtsidor, vilket ger dig frihet att återanvända sådana formulär på flera sidor.
   * Lägg till flera formulär på en webbplatssida, effektivisera användarupplevelsen och ge större flexibilitet.

     >[!VIDEO](https://video.tv.adobe.com/v/3419284?quality=12&learn=on)

* [Adobe Acrobat Sign Solutions för offentlig sektor](/help/forms/adobe-sign-integration-adaptive-forms.md): AEM Forms kan nu integreras med Adobe Acrobat Sign Solutions för offentlig sektor. Integreringen ger en avancerad nivå av regelefterlevnad och säkerhet för e-signaturer med inskickade adaptiva formulär för myndighetskonton (myndigheter och myndigheter).

  Integreringen med Adobe Acrobat Sign for Government gör det möjligt för Adobe partners och myndighetskunder att använda elektroniska signaturer i Adaptive Forms för några av de mest verksamhetskritiska och känsliga verksamhetsområdena. Detta extra säkerhetsskikt säkerställer att alla e-signaturer är helt kompatibla med FedRAMP Moderate och ger Adobe myndighetskunder sinnesro.

* Förbättrad felhantering med anpassade felhanterare i regelredigeraren: Du kan nu anropa en anpassad funktion (med Klientbibliotek) som svar på ett fel som returnerats av en extern tjänst och ge ett skräddarsytt svar till slutanvändarna. Du kan också vidta specifika åtgärder för fel som returneras av en tjänst. Du kan till exempel anropa ett anpassat arbetsflöde i serverdelen för specifika felkoder eller informera kunden om att tjänsten inte fungerar.

  Den här funktionen förbättrar den övergripande felhanteringskapaciteten genom att införa standardbaserade felsvar som är bakåtkompatibla med OOTB-felhanterare, med större flexibilitet och kontroll.

### Headless Adaptive Forms early adopter {#forms-early-adopter}

Med Headless Adaptive Forms kan utvecklarna skapa, publicera och hantera interaktiva blanketter som kan öppnas och interagera med via API:er i stället för via ett traditionellt grafiskt användargränssnitt. Headless adaptive forms help you:

* bygga högkvalitativa flerkanalsformulär på valfritt programmeringsspråk
* integrera formulär direkt i era datorprogram och mobilappar, webbplatser och chattapplikationer
* återanvända era egna gränssnittskomponenter med blankettapplikationer
* använder kraften i Adobe Experience Manager Forms

Du kan skicka ett e-postmeddelande till `aem-forms-headless@adobe.com` från ditt officiella e-post-ID för att gå med i det tidiga adopterprogrammet.

## [!DNL Experience Manager] som en [!DNL Cloud Service]-grund {#foundation}

### Nyheter {#what-is-new-foundation}

* Ytterligare publiceringsregioner: Webbplatskunder kan licensiera upp till tre publiceringsregioner utöver den primära regionen. Trafiken dirigeras till ytterligare publiceringsanläggningar, vilket leder till minskad fördröjning för vissa förfrågningar och ökad motståndskraft mot regionala avbrott. Kontakta din kontohanterare för Adobe för information om licensiering av [ytterligare publiceringsregioner](/help/operations/additional-publish-regions.md) för dina program.

## Versionsinformation om underhåll {#maintenance}

Du hittar den senaste underhållsversionsinformationen [här](/help/release-notes/maintenance/latest.md).

## Cloud Manager {#cloud-manager}

Du hittar en fullständig lista över månadsutgåvor av Cloud Manager [här](/help/implementing/cloud-manager/release-notes/current.md).

## Migreringsverktyg {#migration-tools}

Du hittar en fullständig lista över migreringsverktygen [här](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).

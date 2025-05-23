---
title: Versionsinformation för version 2023.6.0 av  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Versionsinformation för version 2023.6.0 av  [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: 29cf9548-e413-4e4f-b233-d6bb04918b22
feature: Release Information
role: Admin
source-git-commit: f28f212574dda0ece2cedb56a714d381e5bd7d3c
workflow-type: tm+mt
source-wordcount: '1322'
ht-degree: 0%

---

# Versionsinformation 2023.6.0 för [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

I följande avsnitt beskrivs versionsinformationen för funktionen för 2023.6.0-versionen av [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Härifrån kan du navigera till versionsinformation för tidigare versioner som 2021 eller 2022.
>
>Ta en titt på [Experience Manager Releases Roadmap](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=sv-SE) för att lära dig mer om kommande funktionsaktiveringar för [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Mer information om dokumentationsuppdateringar som inte är direkt relaterade till en release finns i [Senaste dokumentationsuppdateringar](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=sv-SE).

## Releasedatum {#release-date}

Releasedatum för [!DNL Adobe Experience Manager] som [!DNL Cloud Service] aktuell funktionsversion (2023.6.0) är 29 juni 2023. Nästa funktionsversion (2023.7.0) är planerad till 27 juli 2023.

## Släpp video {#release-video}

Titta på videon om versionsöversikten för juni 2023 om du vill se en sammanfattning av funktioner som lagts till i version 2023.6.0:

>[!VIDEO](https://video.tv.adobe.com/v/3420971/?quality=12)

## [!DNL Experience Manager Sites] som en [!DNL Cloud Service] {#sites}

### Nya funktioner i [!DNL Experience Manager Sites] {#sites-features}

* Innehållsfragment och deras referenser kan nu publiceras till [AEM förhandsvisningstjänsten](/help/implementing/cloud-manager/manage-environments.md#access-preview-service) med [Content Fragment Console](/help/sites-cloud/administering/content-fragments/managing.md#content-fragments-console), vilket gör att användarna kan förhandsgranska slutresultatet i ett fristående förhandsgranskningsprogram innan de publiceras.

![Förhandsgranska i konsolen för innehållsfragment](/help/assets/content-fragments-console-preview.png)

* Bilderna kan nu optimeras dynamiskt för webbleverans i headless-scenarier med AEM GraphQL. [Frågevariabler](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/how-to/images.html?lang=sv-SE#query-variables) kan definieras i GraphQL-frågor för att tillåta att fristående klientprogram begär optimerade bilder från AEM.
* Taggar på [Variationer för innehållsfragment](https://experienceleague.adobe.com/docs/experience-manager-65/assets/content-fragments/content-fragments-variations.html?lang=sv-SE) kan nu skrivas ut till JSON med hjälp av det AEM GraphQL-innehållsleverans-API:t.

## [!DNL Experience Manager Assets] som en [!DNL Cloud Service] {#assets}

### Nya funktioner i [!DNL Assets] {#assets-features}

**Tillgänglighet för ny Assets-vy**

Den [nya Assets-vyn](/help/assets/assets-view-introduction.md) är nu tillgänglig i Experience Manager Assets. Assets View har ett förenklat användargränssnitt som gör det enkelt att hantera, identifiera och distribuera digitala resurser. Upplevelsen riktar sig till kreatörer, skrivskyddade mediekonsumenter och användare med mindre vikt-DAM.

![Tagghantering](/help/assets/assets/my-workspace.png)

**Förbättrade sökupplevelser**

Experience Manager Assets ger dig nu möjlighet att göra mer med sökresultatgränssnittet: nu kan du:

* [Utför en sökning inom den aktuella databasplatsen](/help/assets/search-assets.md) som standard i stället för att söka efter nyckelordet i hela databasen.

* [Navigera till mapplatsen](/help/assets/search-assets.md#aftersearch) för resurser som visas i sökresultaten.

**Miniatyrförhandsvisningar för 3D-resurser**

[!DNL Experience Manager Assets] genererar nu [miniatyrförhandsvisningar för vanliga 3D-filformat](/help/assets/file-format-support.md) inklusive gLB, USDz, FBX, 3DS, OBJ och SBSAR. När dessa filer överförs genereras miniatyrbilder automatiskt som standard.

**Dynamic Media: Uppdaterade fält relaterade till smart beskärning i bildprofilen**

Användargränssnittet för vissa Smart Crop-relaterade fält i en bildprofil har nu uppdaterats för att återspegla de aktuella riktlinjerna för att definiera en smart beskärning. Se [Beskärningsalternativ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/image-profiles.html?lang=sv-SE#crop-options).

### Nya funktioner i vyn Assets {#assets-view-features}

**Hierarkisk taggning av resurser för snabbare sökupplevelse**

Platta listor med kontrollerade vokabulärer blir ohanterliga över tid. Assets-vyn har nu stöd för [hierarkisk taggningsstruktur](/help/assets/tagging-management-assets-view.md) som gör det lättare att använda relevanta metadata, kategorisera resurser, söka, återanvända taggar, förbättra upptäckbarheten och så vidare.

![Tagghantering](/help/assets/assets/tags-hierarchy.png)

**Fäst filer, mappar och samlingar för snabb åtkomst**

Du kan nu [fästa filer, mappar och samlingar så att du snabbare kommer åt](/help/assets/my-workspace-assets-view.md) när du behöver dem senare. De fästa objekten visas i avsnittet **Snabbåtkomst** i Min Workspace. Du kan komma åt dem med Mitt Workspace i stället för att navigera till den plats där de sparas i databasen.

![Uppgifter i Workspace](/help/assets/assets/quick-access.png)

**Filtrera resurser i papperskorgen**

I Assets-vyn kan du nu [filtrera resurser som är tillgängliga i papperskorgen](/help/assets/navigate-assets-view.md). Du kan använda standardfilter eller anpassade filter för att söka efter lämpliga resurser i papperskorgen för att antingen återställa eller ta bort dem permanent.

**Miniatyrförhandsvisningar för 3D-resurser**

I Assets-vyn genereras nu miniatyrbilder för vanliga 3D-filformat, bland annat gLB, USDz, FBX, 3DS, OBJ och SBSAR. När dessa filer överförs till Assets-vyn genereras miniatyrbilder automatiskt av systemet som standard.

![Uppgifter i Workspace](/help/assets/assets/3d-preview.png)

**Visa de mest sökta termerna**

Assets-vyn har nu stöd för [att visa de mest sökbara termerna i din distribution](/help/assets/my-workspace-assets-view.md) med hjälp av avsnittet **Insikter** i Min Workspace. Du kan även navigera till detaljerade insikter för att visa de vanligaste sökningarna under de senaste 30 dagarna eller 12 månaderna.

![Uppgifter i Workspace](/help/assets/assets/insights-top-searches.png)

**Förbättringar av metadataformulär**

I Assets-vyn kan du nu [lägga till text med flera värden och egenskapskomponenter för nedrullningsbara listor](/help/assets/metadata-assets-view.md#property-components) i metadataformulären.

## [!DNL Experience Manager Forms] som en [!DNL Cloud Service] {#forms}

### Nya funktioner tillgängliga i [!DNL Forms] {#new-features-available-in-channel}

* [Adaptiv Forms i AEM sidredigeraren](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md): Nu kan du använda AEM sidredigeraren för att snabbt skapa och lägga till flera formulär på webbplatsens sidor. Med den här funktionen kan skribenter skapa sömlösa datainhämtningsmöjligheter på webbplatssidor med hjälp av kraften i adaptiva formulärkomponenter, inklusive dynamiskt beteende, validering, dataintegrering, generering av dokument för post- och affärsprocessautomatisering. Du kan:

   * Skapa ett anpassat formulär genom att dra och släppa formulärkomponenter i den adaptiva Forms Container-komponenten i AEM Sites Editor eller Experience Fragments.
   * Använd Adaptive Forms Wizard i AEM Sites Editor för att skapa formulär oberoende av sajtsidor, vilket ger dig frihet att återanvända sådana formulär på flera sidor.
   * Lägg till flera formulär på en webbplatssida, effektivisera användarupplevelsen och ge större flexibilitet.

     >[!VIDEO](https://video.tv.adobe.com/v/3419284?quality=12&learn=on)

* [Adobe Acrobat Sign Solutions för offentlig sektor](/help/forms/adobe-sign-integration-adaptive-forms.md): AEM Forms kan nu integreras med Adobe Acrobat Sign Solutions för offentlig sektor. Integreringen ger en avancerad nivå av regelefterlevnad och säkerhet för e-signaturer med inskickade adaptiva formulär för myndighetskonton (myndigheter och myndigheter).

  Integrationen med Adobe Acrobat Sign Solutions for Government gör det möjligt för Adobe och myndighetskunder att använda elektroniska signaturer i Adaptive Forms för några av de mest verksamhetskritiska och känsliga verksamhetsområdena. Detta extra säkerhetsskikt säkerställer att alla e-signaturer är helt kompatibla med FedRAMP Moderate-kompatibiliteten, vilket ger Adobe myndighetskunder sinnesro.

* [Förbättrad felhantering med anpassade felhanterare i regelredigeraren](/help/forms/add-custom-error-handler-adaptive-forms.md): Du kan nu anropa en anpassad funktion (med klientbibliotek) som svar på ett fel som returnerats av en extern tjänst och ge ett skräddarsytt svar till slutanvändarna. Du kan också vidta specifika åtgärder för fel som returneras av en tjänst. Du kan till exempel anropa ett anpassat arbetsflöde i serverdelen för specifika felkoder eller informera kunden om att tjänsten inte fungerar.

  Den här funktionen förbättrar den övergripande felhanteringskapaciteten genom att införa standardbaserade felsvar som är bakåtkompatibla med OOTB-felhanterare, med större flexibilitet och kontroll.

* [Förbättrade autentiseringsmetoder för formulärdatamodell](/help/forms/configure-data-sources.md): Förbättrad säkerhet tack vare introduktionen av klientautentiseringsuppgifter för anslutning av AEM Forms med kompatibla datakällor. Den här förbättringen eliminerar behovet av personifiering eller användarinloggning, vilket stärker skyddet av dina data.

* [Adaptiv Forms med repeterbara avsnitt](/help/forms/create-forms-repeatable-sections.md): Nu kan du skapa [dragspels](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion.html?lang=sv-SE)-, [guide](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard.html?lang=sv-SE)-, [panel](https://experienceleague.adobe.com/sv/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel)- och [horisontella flikar](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/horizontal-tabs.html?lang=sv-SE)-komponenter i en huvudkomponentbaserad adaptiv form för att skapa repeterbara avsnitt.

  >[!VIDEO](https://video.tv.adobe.com/v/3421052/adaptive-forms-repeatable-sections-repeat-sections/?quality=12&learn=on)

  Dessa upprepningsbara avsnitt låter dig ange ett obegränsat antal poster utan ett fast fältantal. Det är användbart när de nödvändiga instanserna av data är okända i förväg. Forms-användare kan enkelt lägga till eller ta bort avsnitt, göra formulären anpassningsbara till olika datainmatningsscenarier och förenkla insamlingen av flera förekomster av samma data.

* **[Skicka adaptiva Forms till Microsoft® SharePoint och Microsoft® OneDrive](/help/forms/configuring-submit-actions.md)**: Förbättra användarflexibiliteten så att du snabbt kan starta nya formulär och lagra inskickade data i vanliga verktyg som Microsoft® SharePoint eller OneDrive-mappen.

### Headless Adaptive Forms early adopter {#forms-early-adopter}

Använd [Headless Adaptive Forms](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html?lang=sv-SE) om du vill att utvecklarna ska kunna skapa, publicera och hantera interaktiva formulär som kan nås och interagera med via API:er, i stället för via ett traditionellt grafiskt användargränssnitt. Headless adaptive forms help you:

* bygga högkvalitativa flerkanalsformulär på valfritt programmeringsspråk
* integrera formulär direkt i era datorprogram och mobilappar, webbplatser och chattapplikationer
* återanvända era egna gränssnittskomponenter med blankettapplikationer
* använder kraften i Adobe Experience Manager Forms

Du kan skicka ett e-postmeddelande till `aem-forms-headless@adobe.com` från ditt officiella e-post-ID för att gå med i det tidiga adopterprogrammet.

## Versionsinformation om underhåll {#maintenance}

Du hittar den senaste underhållsversionsinformationen [här](/help/release-notes/maintenance/latest.md).

## Cloud Manager {#cloud-manager}

Du hittar en fullständig lista över månadsutgåvor av Cloud Manager [här](/help/implementing/cloud-manager/release-notes/current.md).

## Migreringsverktyg {#migration-tools}

Du hittar en fullständig lista över migreringsverktygen [här](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).

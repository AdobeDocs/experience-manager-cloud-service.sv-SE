---
title: Aktuell versionsinformation för [!DNL Adobe Experience Manager] as a Cloud Service.
description: Aktuell versionsinformation för [!DNL Adobe Experience Manager] as a Cloud Service.
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
source-git-commit: da5634dfa812268b81b2db783da772b6ecc1d7ce
workflow-type: tm+mt
source-wordcount: '1365'
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

Releasedatum [!DNL Adobe Experience Manager] som [!DNL Cloud Service] aktuell version (2023.6.0) är 29 juni 2023. Nästa funktionsversion (2023.7.0) är planerad till 27 juli 2023.

## Släpp video {#release-video}

Titta på videon om versionsöversikten för juni 2023 om du vill se en sammanfattning av funktioner som lagts till i version 2023.6.0:

>[!VIDEO](https://video.tv.adobe.com/v/3420971/?quality=12)

## [!DNL Experience Manager Sites] som [!DNL Cloud Service] {#sites}

### Nya funktioner i [!DNL Experience Manager Sites] {#sites-features}

* Innehållsfragment och deras referenser kan nu publiceras i [Tjänsten AEM Preview](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-environments.html?lang=en#access-preview-service) med [Konsol för innehållsfragment](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/content-fragments/content-fragments-console.html?lang=en), vilket gör att användarna kan förhandsgranska slutresultatet i ett fristående förhandsvisningsprogram innan de publicerar.
* Bilderna kan nu optimeras dynamiskt för webbleverans i headlessscenarier med AEM GraphQL. [Frågevariabler](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/how-to/images.html?lang=en#query-variables) kan definieras i GraphQL-frågor för att tillåta att fristående klientprogram begär optimerade bilder från AEM.
* Taggar på [Variationer för innehållsfragment](https://experienceleague.adobe.com/docs/experience-manager-65/assets/content-fragments/content-fragments-variations.html?lang=en) kan nu skrivas ut till JSON med AEM GraphQL Content Delivery API.

## [!DNL Experience Manager Assets] som [!DNL Cloud Service] {#assets}

### Nya funktioner i [!DNL Assets] {#assets-features}

**Tillgång till vyn Nya resurser**

The [ny resursvy](/help/assets/assets-view-introduction.md) finns nu i Experience Manager Assets. Resursvyn har ett förenklat användargränssnitt som gör det enkelt att hantera, identifiera och distribuera digitala resurser. Upplevelsen riktar sig till kreatörer, skrivskyddade mediekonsumenter och användare med mindre vikt-DAM.

![Tagghantering](/help/assets/assets/my-workspace.png)

**Förbättrade sökupplevelser**

Experience Manager Assets ger dig nu möjlighet att göra mer med sökresultatens användargränssnitt: Nu kan du:

* Sök som standard på den aktuella databasplatsen i stället för att söka efter nyckelordet i hela databasen.

* Navigera till mapplatsen för resurser som visas i sökresultaten.

**Miniatyrförhandsvisningar för 3D-resurser**

[!DNL Experience Manager Assets] genererar nu [miniatyrbilder för vanliga 3D-filformat](/help/assets/file-format-support.md) inklusive gLB, USDz, FBX, 3DS, OBJ och SBSAR. När dessa filer överförs genereras miniatyrbilder automatiskt som standard.

**Länkresurskonfiguration**

En ny förbättrad användarupplevelse för [skapa länkresurser](/help/assets/share-assets.md) tillsammans med en helt ny uppsättning konfigurationer som gör att administratörer kan anpassa standardbeteendet för den här funktionen för dina användare.

![Tagghantering](/help/assets/assets/config-email-service.png)

**Dynamic Media: Uppdaterade fält relaterade till smart beskärning i bildprofilen**

Användargränssnittet för vissa Smart Crop-relaterade fält i en bildprofil har nu uppdaterats för att återspegla de aktuella riktlinjerna för att definiera en smart beskärning. Se [Beskärningsalternativ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/image-profiles.html?lang=en#crop-options).

### Nya funktioner i resursvyn {#assets-view-features}

**Hierarkisk taggning av resurser för snabbare sökupplevelse**

Platta listor med kontrollerade vokabulärer blir ohanterliga över tid. Resursvyn har nu stöd för [hierarkisk taggningsstruktur](/help/assets/tagging-management-assets-view.md), som gör det enklare att använda relevanta metadata, kategorisera resurser, söka, återanvända taggar, förbättra upptäckbarheten och så vidare.

![Tagghantering](/help/assets/assets/tags-hierarchy.png)

**Fäst filer, mappar och samlingar för snabb åtkomst**

Nu kan du [fästa filer, mappar och samlingar för snabbare åtkomst](/help/assets/my-workspace-assets-view.md) till de här objekten när du behöver dem senare. De fästa objekten visas i **Snabb åtkomst** i Min arbetsyta. Du kan komma åt dem med Min arbetsyta i stället för att navigera till den plats där de sparas i databasen.

![Uppgifter på arbetsytan](/help/assets/assets/quick-access.png)

**Filtrera resurser i papperskorgen**

I resursvyn kan du nu [filterresurser som finns i papperskorgen](/help/assets/navigate-assets-view.md). Du kan använda standardfilter eller anpassade filter för att söka efter lämpliga resurser i papperskorgen för att antingen återställa eller ta bort dem permanent.

**Miniatyrförhandsvisningar för 3D-resurser**

Resursvyn genererar nu miniatyrförhandsvisningar för vanliga 3D-filformat som gLB, USDz, FBX, 3DS, OBJ och SBSAR. När dessa filer överförs till resursvyn skapas miniatyrbilder automatiskt av systemet som standard.

![Uppgifter på arbetsytan](/help/assets/assets/3d-preview.png)

**Visa de vanligaste söktermerna**

Resursvyn har nu stöd för [visa de vanligaste söktermerna i din distribution](/help/assets/my-workspace-assets-view.md) med **Insikter** i Min arbetsyta. Du kan även navigera till detaljerade insikter för att visa de vanligaste sökningarna under de senaste 30 dagarna eller 12 månaderna.

![Uppgifter på arbetsytan](/help/assets/assets/insights-top-searches.png)

**Förbättringar av metadataformulär**

I resursvyn kan du nu [lägga till text med flera värden och nedrullningsbara listegenskapskomponenter](/help/assets/metadata-assets-view.md#property-components) till metadataformulären.


## [!DNL Experience Manager Forms] som [!DNL Cloud Service] {#forms}

### Nya funktioner i [!DNL Forms] {#new-features-available-in-channel}

* [Adaptiv Forms i AEM Page Editor och Experience Fragment](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md): Nu kan du använda AEM Page Editor och Experience Fragment för att snabbt skapa och lägga till flera formulär på dina AEM Sites-sidor. Med den här funktionen kan skribenter skapa sömlösa datainhämtningsupplevelser på webbplatssidor med hjälp av kraften i adaptiva Forms-komponenter, inklusive dynamiskt beteende, validering, dataintegrering, generering av dokument för post- och affärsprocessautomatisering.

  >[!VIDEO](https://video.tv.adobe.com/v/3419284?quality=12&learn=on)

* [Använd Adobe Acrobat Sign Solutions for Government (HIPPA-klagomål) med AEM Forms](/help/forms/adobe-sign-integration-adaptive-forms.md): AEM Forms kan nu integreras med Adobe Acrobat Sign Solutions för myndigheter. Integreringen ger en avancerad nivå av regelefterlevnad och säkerhet för e-signaturer med inskickade adaptiva formulär för myndighetskonton (myndigheter och myndigheter).

  Integrationen med Adobe Acrobat Sign Solutions for Government gör det möjligt för Adobe och myndighetskunder att använda elektroniska signaturer i Adaptive Forms för några av de mest verksamhetskritiska och känsliga verksamhetsområdena. Detta extra säkerhetsskikt säkerställer att alla e-signaturer är helt kompatibla med FedRAMP Moderate-kompatibiliteten, vilket ger Adobe myndighetskunder sinnesro.

* [Förbättrad felhantering med anpassade felhanterare i regelredigeraren](/help/forms/add-custom-error-handler-adaptive-forms.md): Du kan nu anropa en anpassad funktion (med Klientbibliotek) som svar på ett fel som returnerats av en extern tjänst och ge ett skräddarsytt svar till slutanvändarna. Du kan också vidta specifika åtgärder för fel som returneras av en tjänst. Du kan till exempel anropa ett anpassat arbetsflöde i serverdelen för specifika felkoder eller informera kunden om att tjänsten inte fungerar.

  Den här funktionen förbättrar den övergripande felhanteringskapaciteten genom att införa standardbaserade felsvar som är bakåtkompatibla med OOTB-felhanterare, med större flexibilitet och kontroll.

* [Förbättrade autentiseringsmetoder för formulärdatamodell](/help/forms/configure-data-sources.md): Ökad säkerhet tack vare introduktionen av klientautentisering som kopplar AEM Forms (formulärdatamodeller) till kompatibla datakällor. Den här förbättringen eliminerar behovet av personifiering eller användarinloggning, vilket stärker skyddet av dina data.

* [Skapa adaptiv Forms med repeterbara avsnitt](/help/forms/create-forms-repeatable-sections.md): Nu kan du [Dragspel](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion.html), [guide](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard.html), [Panel](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel-container.html)och [Vågräta flikar](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/horizontal-tabs.html) komponenter i en Core Components-baserad adaptiv form för att skapa repeterbara avsnitt.

  >[!VIDEO](https://video.tv.adobe.com/v/3421052/adaptive-forms-repeatable-sections-repeat-sections/?quality=12&learn=on)

  Dessa upprepningsbara avsnitt låter dig ange ett obegränsat antal poster utan ett fast fältantal. Det är användbart när de nödvändiga instanserna av data är okända i förväg. Forms-användare kan enkelt lägga till eller ta bort avsnitt, göra formulären anpassningsbara till olika datainmatningsscenarier och förenkla insamlingen av flera förekomster av samma data.

* **[Skicka anpassningsbara Forms till Microsoft® SharePoint och Microsoft® OneDrive](/help/forms/configuring-submit-actions.md)**: Nu kan du skicka adaptiva Forms-data till vanliga verktyg som Microsoft® SharePoint Site eller Microsoft® OneDrive.

### Headless Adaptive Forms early adopter {#forms-early-adopter}

Använd [Headless Adaptive Forms](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html) för att ge utvecklarna möjlighet att skapa, publicera och hantera interaktiva formulär som kan öppnas och interagera med via API:er, i stället för via ett traditionellt grafiskt användargränssnitt. Headless adaptive forms help you:

* bygga högkvalitativa flerkanalsformulär på valfritt programmeringsspråk
* integrera formulär direkt i era datorprogram och mobilappar, webbplatser och chattapplikationer
* återanvända era egna gränssnittskomponenter med blankettapplikationer
* använder kraften i Adobe Experience Manager Forms

Du kan skicka ett e-postmeddelande till `aem-forms-headless@adobe.com` från ditt officiella e-post-ID till att gå med i det tidiga adopterprogrammet.


## Versionsinformation om underhåll {#maintenance}

Du kan hitta den senaste underhållsreleasenumerationen [här](/help/release-notes/maintenance/latest.md).

## Cloud Manager {#cloud-manager}

Du hittar en fullständig lista över månatliga utgåvor av Cloud Manager [här](/help/implementing/cloud-manager/release-notes/current.md).

## Migreringsverktyg {#migration-tools}

Du hittar en fullständig lista över versioner av migreringsverktyg [här](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).

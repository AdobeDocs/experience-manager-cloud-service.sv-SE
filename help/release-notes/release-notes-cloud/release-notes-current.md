---
title: Aktuell versionsinformation för [!DNL Adobe Experience Manager] as a Cloud Service.
description: Aktuell versionsinformation för [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
mini-toc-levels: 1
source-git-commit: a96824cede31414963ff7e6f5ef1315bd35a51c1
workflow-type: tm+mt
source-wordcount: '1099'
ht-degree: 0%

---


# Aktuell versionsinformation för [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

I följande avsnitt beskrivs den allmänna versionsinformationen för den aktuella (senaste) versionen av [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Härifrån kan du navigera till versionsinformation för tidigare versioner; till exempel för 2020, 2021 och så vidare.

>[!NOTE]
>
>Se [Senaste dokumentationsuppdateringar](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html) för information om dokumentationsuppdateringar som inte är direkt relaterade till en release.

## Releasedatum {#release-date}

Releasedatum [!DNL Adobe Experience Manager] som [!DNL Cloud Service] aktuell version (2022.3.0) är 31 mars 2022.
Följande version (2022.4.0) är den 28 april 2022.

## Släpp video {#release-video}

Ta en titt på [Mars 2022 - versionsöversikt](https://video.tv.adobe.com/v/341465) video med en sammanfattning av funktioner som lagts till i version 2022.3.0.

## [!DNL Experience Manager Assets] som [!DNL Cloud Service] {#assets}

### Nya funktioner i [!DNL Assets] {#assets-features}

* [!DNL AEM Dynamic Media] ger nu flexibilitet att [konfigurera ett aliaskonto](/help/assets/dynamic-media/dm-alias-account.md) i användargränssnittet, vilket säkerställer att färdiga Dynamic Media-URL:er och inbäddningskod för visningsprogram uppdateras. Detta påverkar SEO positivt för att återspegla uppdateringar som gjorts i ert företagskontext, t.ex. omprofilering.

* Nu kan du använda [!DNL Experience Manager Assets] till

   * Konfigurera [identifiering av duplicerade resurser](/help/assets/manage-digital-assets.md#detect-duplicate-assets) i en databas.

   * Konfigurera [lägga till digitala vattenstämplar](/help/assets/watermark-assets.md) till bilder.

* Administratörerna kan nu konfigurera e-posttjänsten för stora hämtningar. Det gör att användarna kan [aktivera e-postmeddelanden för stora nedladdningar](/help/assets/download-assets-from-aem.md#enable-email-notifications-for-large-downloads) från [!DNL Experience Manager Assets] gränssnitt. Användaren får ett e-postmeddelande med nedladdningslänken för den arkiverade zip-mappen när nedladdningen är klar.

* The [Hantera publikation](/help/assets/manage-publication.md) har förbättrats med ett förbättrat användargränssnitt. Användarna kan publicera eller avpublicera innehåll till och från det valda målet, [Lägg till innehåll](/help/assets/manage-publication.md#add-content) till publiceringslistan från DAM-databasen, [Inkludera mappinställningar](/help/assets/manage-publication.md#include-folder-settings) för att publicera innehållet i de valda mapparna och tillämpa filter, och [schemaläggning](/help/assets/manage-publication.md#publish-assets-later) till ett senare datum eller en senare tid.

### Nya funktioner i [!DNL Assets] prerelease channel {#prerelease-features-assets}

* Du kan [sortera taggar](/help/assets/organize-assets.md#use-tags-to-organize-assets) när du skapar smarta taggar och när du använder sökfilter med hjälp av taggpredikatet.

## [!DNL Experience Manager Forms] som [!DNL Cloud Service] {#forms}

### Nyheter i [!DNL Forms] {#what-is-new-forms}

* **[!DNL Communications - Document Generation APIs]**: [API:er för dokumentgenerering](/help/forms/aem-forms-cloud-service-communications.md) kan du kombinera, ordna om och validera PDF-dokument. Med tjänsten kan du generera dokument i synkront läge. Med API:erna kan du skapa program som gör att du kan:

   * Sammanställ dokument från PDF.
   * Disassemblera PDF-dokument.
   * Konvertera till och validera dokument som följer PDF/A-standarden.

* **Konvertera automatiskt PDF forms som är större än 15 sidor till anpassningsbara formulär**: Du kan nu använda tjänsten automated forms conversion för att konvertera PDF forms med upp till 40 sidor till anpassningsbara formulär. Tjänsten erbjuder nu alternativ för att konvertera avsnitt av formulär som är större än 15 sidor till anpassningsbara formulärfragment. Det förbättrar återgivningshastigheten för konverterade formulär och gör det enklare att läsa in stora formulär i en adaptiv formulärredigerare.

### Nya funktioner i [!DNL Forms] prerelease channel {#prerelease-features-forms}

* **Använd anpassad XCI för att generera ett postdokument**: Du kan nu använda en anpassad XCI-fil för att ange olika egenskaper för ett dokument för post. Den åsidosätter det överordnad XCI med de anpassade ändringarna.

* **Använd osynlig CAPTCHA i ett adaptivt formulär**: Du kan använda den osynliga CAPTCHA-funktionen för att visa CAPTCHA-utmaningen endast om en misstänkt aktivitet inträffar. Om ingen misstänkt aktivitet hittas visas inte CAPTCHA-utmaningen.

## CIF-tillägg {#cloud-services-cif}

### Vad är nytt? {#what-is-new-cif}

* Beta: AEM CIF Search Core Component support Commerce LiveSearch
* Förbättrad SEO för scenarier med flera butiker: URL-format för PDP/PLP kan nu konfigureras på en butiksnivå via CIF Cloud Config-egenskaper
* Produktväljaren har stöd för mellanlagrade produkter via ett nytt filteralternativ i användargränssnittet.  Detta gör att innehållsutvecklare kan förbereda innehållshantering för kommande produktlanseringar
* Förenklad CIF-konfigurationshantering och felhantering genom att använda CIF Cloud Config-namn i stället för konfigurationsproxy-URL
* Manuellt kategorival för produktlista och Carousel-komponenter. På så sätt kan innehållsutvecklare använda dessa komponenter på innehållssidor, utanför katalogupplevelsen

## [!DNL Experience Manager] som [!DNL Cloud Service] Foundation {#foundation}

### Vad är nytt? {#what-is-new-foundation}

* För effektivare och effektivare felsökning av anpassade funktioner i molnmiljöer har vi släppt ett nytt utvecklarverktyg - [Databasläsaren](/help/implementing/developing/tools/repository-browser.md). Det är en lättviktig, skrivskyddad webbläsare i HTML som du kan starta från Developer Console. Få insyn i innehållslagringsplatsen på utgivar-, författar- och förhandsgranskningsnivå - och i alla miljöer, inklusive produktion, scener och utveckling. Bläddra i innehållsstrukturen, visa egenskaper samt förhandsgranska och hämta binärfiler.

   ![repoblästeranteckningar](/help/release-notes/assets/repobrowserrelnotes.png)

* Autentiseringsuppgifterna som används för att autentisera API-anrop från server till server (t.ex. för GraphQL API-begäranden) kan nu uppdateras på ett självbetjäningssätt från utvecklarkonsolen innan de förfaller. Se [dokumentation](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md#refresh-credentials) för mer information.

* Underhållsuppgifter för rensning av versioner och granskningslogg som inte tidigare aktiverats kommer att aktiveras för nya miljöer. Se de associerade värdena i [Underhållsaktivitet](/help/operations/maintenance.md) artikel.

* AEM as a Cloud Service SDK Dispatcher Tools har nu stöd för Mac datorer med M1-chipet

## Cloud Manager {#cloud-manager}

Du hittar en fullständig lista över månatliga utgåvor av Cloud Manager [här](/help/implementing/cloud-manager/release-notes-cloud-manager/release-notes-cm-current.md).

## Content Transfer Tool {#ctt-release}

### Releasedatum {#release-date-ctt}

Releasedatum för Content Transfer Tool v1.9.0 är 28 februari 2022.

### Nyheter {#what-is-new-ctt}

* Kontrollera storleksordrar - Funktionen Kontrollera storlek för verktyget Innehållsöverföring hjälper till att minska misslyckade innehållsöverföringar.  Med funktionen Kontrollera storlek kan användarna 1) avgöra om de har tillräckligt med diskutrymme i `crx-quickstart` underkatalog före extrahering och 2) beräkna storleken på migreringsuppsättningen och kontrollera om den stöds. Om en av eller båda dessa kontroller överträds visas varningar i användargränssnittet för aktuell tid. Med den här skyddsguiden kan du undvika innehållsöverföringsfel och proaktivt diskutera migreringsalternativ med Adobe kundtjänst. Se [Bestämma migreringsuppsättningens storlek och diskutrymme](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=en#migration-set-size) för mer information.

## Best Practices Analyzer {#bpa-release}

### Releasedatum {#release-date-bpa}

Releasedatum för Best Practices Analyzer v2.1.26 är 16 mars 2022.

### Nyheter {#what-is-new-bpa}

* Möjlighet att upptäcka obearbetade resurser. Om obearbetade resurser upptäcks måste dessa resurser antingen ställas in på bearbetad eller tas bort från migreringsuppsättningen under innehållsöverföring för att undvika problem under innehållsimporten.
* Möjlighet att identifiera om innehållet har fler än 1000 ogiltiga URL:er. Det är inte bra att använda ett stort antal användar-URL:er eftersom en belastning läggs på Dispatcher- och Publish-servrar.
* Möjlighet att identifiera problem relaterade till indexdefinitioner för ekon och upptäcka inkompatibilitet med AEM as a Cloud Service.
* Möjlighet att upptäcka och rapportera om användningen av Externalizer-konfigurationer. I AEM as a Cloud Service externaliserarkonfigurationer anges av Cloud Manager, och därför måste befintliga Externalizer-konfigurationer omfaktoriseras för att bibehålla kompatibiliteten.

### Felkorrigeringar {#bug-fixes-bpa}

* I vissa scenarier gick det inte att köra BPA på grund av att FormsSelectiveFeaturesAnalysis genererade ett kontrollfel. Den här har åtgärdats.
* BPA rapporterade fynd relaterade till WRK-mönstret som MAJOR i stället för CRITICAL. Den här har åtgärdats.
* BPA rapporterade felaktigt resultat relaterade till OAK-indexdefinitioner i ui.apps som CRITICAL. Detta har åtgärdats

---
title: Versionsinformation för version 2022.3.0 av  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Versionsinformation för version 2022.3.0 av  [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: 761f1605-c421-4f3a-8f90-af23f4f047b1
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '1158'
ht-degree: 0%

---

# Versionsinformation 2022.3.0 för [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

I följande avsnitt beskrivs versionsinformationen för funktionen för 2022.3.0-versionen av [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Härifrån kan du navigera till versionsinformation för tidigare versioner, till exempel för versionerna 2020, 2021 och så vidare.

>[!NOTE]
>
>Mer information om dokumentationsuppdateringar som inte är direkt relaterade till en release finns i [Senaste dokumentationsuppdateringar](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=sv-SE).

## Releasedatum {#release-date}

Releasedatum för [!DNL Adobe Experience Manager] som aktuell [!DNL Cloud Service]-version (2022.3.0) är 31 mars 2022.
Nästa version (2022.4.0) är planerad till 5 maj 2022.

## Släpp video {#release-video}

Titta på videon [Mars 2022 Release Overview](https://video.tv.adobe.com/v/341465) om du vill se en sammanfattning av funktioner som lagts till i version 2022.3.0.

## [!DNL Experience Manager Sites] som en [!DNL Cloud Service] {#sites}

### Nya funktioner som är tillgängliga i betaversionskanalen i [!DNL Sites] {#prerelease-features-sites}

* Datatyperna för innehållsmodellen kan nu definieras som översättningsbara med en enkel kryssruta i innehållsmodellens redigerare. Dessutom uppdateras AEM översättningsregler och -konfigurationer automatiskt.

## [!DNL Experience Manager Assets] som en [!DNL Cloud Service] {#assets}

### Nya funktioner i [!DNL Assets] {#assets-features}

* [!DNL AEM Dynamic Media] ger nu flexibilitet att [konfigurera ett aliaskonto](/help/assets/dynamic-media/dm-alias-account.md) i användargränssnittet och säkerställer därmed att körklara Dynamic Media-URL:er och inbäddningskod för visningsprogram uppdateras. Detta påverkar SEO positivt för att återspegla uppdateringar som gjorts i ert företagskontext, t.ex. omprofilering.

* Du kan nu använda användargränssnittet [!DNL Experience Manager Assets] för att:

   * Konfigurera identifiering [av dubblettresurser](/help/assets/detect-duplicate-assets.md) i en databas.

   * Konfigurera [att lägga till digitala vattenstämplar](/help/assets/watermark-assets.md) i bilder.

* Administratörerna kan nu konfigurera e-posttjänsten för stora hämtningar. Det gör att användarna kan [aktivera e-postmeddelanden för stora hämtningar](/help/assets/download-assets-from-aem.md#enable-email-notifications-for-large-downloads) från gränssnittet [!DNL Experience Manager Assets]. Användaren får ett e-postmeddelande med nedladdningslänken för den arkiverade zip-mappen när nedladdningen är klar.

* Funktionen [Hantera publikation](/help/assets/manage-publication.md) har förbättrats med ett förbättrat användargränssnitt. Användarna kan publicera eller avpublicera innehåll till och från det valda målet, [Lägg till innehåll](/help/assets/manage-publication.md#add-content) i publiceringslistan från hela DAM-databasen, [Inkludera mappinställningar](/help/assets/manage-publication.md#include-folder-settings) för att publicera innehåll i de valda mapparna och tillämpa filter, och [schemalägga publicering](/help/assets/manage-publication.md#publish-assets-later) för ett senare datum eller tid.

### Nya funktioner som är tillgängliga i betaversionskanalen i [!DNL Assets] {#prerelease-features-assets}

* Du kan nu [sortera taggar](/help/assets/organize-assets.md#use-tags-to-organize-assets) i taggväljarfönstret i stigande eller fallande ordning baserat på taggnamn, skapandedatum eller ändringsdatum.

## [!DNL Experience Manager Forms] som en [!DNL Cloud Service] {#forms}

### Nyheter i [!DNL Forms] {#what-is-new-forms}

* **[!DNL Communications - Document Generation APIs]**: [API:er för dokumentgenerering](/help/forms/aem-forms-cloud-service-communications.md) hjälper dig att kombinera, ordna om och validera PDF-dokument. Med tjänsten kan du generera dokument i synkront läge. Med API:erna kan du skapa program som gör att du kan:

   * Sammanställ dokument från PDF.
   * Disassemblera PDF-dokument.
   * Konvertera till och validera dokument som följer PDF/A-standarden.

* **Konvertera PDF forms som är större än 15 sidor automatiskt till anpassningsbara formulär**: nu kan du använda tjänsten automated forms conversion för att konvertera PDF forms med upp till 40 sidor till anpassningsbara formulär. Tjänsten erbjuder nu alternativ för att konvertera avsnitt av formulär som är större än 15 sidor till anpassningsbara formulärfragment. Det förbättrar återgivningshastigheten för konverterade formulär och gör det enklare att läsa in stora formulär i en adaptiv formulärredigerare.

### Nya funktioner som är tillgängliga i betaversionskanalen i [!DNL Forms] {#prerelease-features-forms}

* **Använd anpassad XCI för att generera ett postdokument**: Du kan nu använda en anpassad XCI-fil för att ange olika egenskaper för ett postdokument. Det åsidosätter huvud-XCI med de anpassade ändringarna.

* **Använd osynlig CAPTCHA i adaptiv form**: Du kan använda den osynliga CAPTCHA-kontrollen för att visa CAPTCHA-anropet endast om en misstänkt aktivitet inträffar. Om ingen misstänkt aktivitet hittas visas inte CAPTCHA-utmaningen.

## CIF {#cloud-services-cif}

### Nyheter {#what-is-new-cif}

* Förbättrad SEO för scenarier med flera butiker: URL-format för PDP/PLP kan nu konfigureras på en butiksnivå via CIF Cloud Config-egenskaper
* Produktväljaren stöder mellanlagrade produkter genom ett nytt filteralternativ i användargränssnittet.  Detta gör att innehållsutvecklare kan förbereda innehållshantering för kommande produktlanseringar
* Förenklad CIF och felhantering genom att använda CIF Cloud Config-namn i stället för config proxy-URL
* Manuellt kategorival för produktlista och Carousel-komponenter. På så sätt kan innehållsutvecklare använda dessa komponenter på innehållssidor, utanför katalogupplevelsen

### Nya funktioner i CIF prerelease channel {#prerelease-features-cif}

* AEM CIF Search Core Component har stöd för Commerce LiveSearch

## [!DNL Experience Manager] som en [!DNL Cloud Service]-grund {#foundation}

### Nyheter {#what-is-new-foundation}

* För effektivare och effektivare felsökning av anpassade funktioner i molnmiljöer har vi släppt ett nytt utvecklarverktyg - [Databasläsaren](/help/implementing/developing/tools/repository-browser.md). Det är en lättviktig, skrivskyddad HTML-webbläsare som du kan starta från Developer Console. Få insyn i innehållslagringsplatsen på utgivar-, författar- och förhandsgranskningsnivå - och i alla miljöer, inklusive produktion, scener och utveckling. Bläddra i innehållsstrukturen, visa egenskaper samt förhandsgranska och hämta binärfiler.

  ![repobrowserrelnotes](/help/release-notes/assets/repobrowserrelnotes.png)

* Autentiseringsuppgifterna som används för att autentisera API-anrop från server till server (t.ex. för GraphQL API-begäranden) kan nu uppdateras före förfallodatum på ett självbetjäningssätt från Developer Console. Mer information finns i [dokumentationen](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md#refresh-credentials).

* Underhållsuppgifter för rensning av versioner och granskningsloggar, som inte tidigare hade aktiverats, har nu aktiverats för nya miljöer. Se de associerade värdena i artikeln [Underhållsaktivitet](/help/operations/maintenance.md).

* AEM as a Cloud Service SDK Dispatcher Tools har nu stöd för Mac datorer med M1-chipet

## Cloud Manager {#cloud-manager}

Du hittar en fullständig lista över månadsutgåvor av Cloud Manager [här](/help/implementing/cloud-manager/release-notes/current.md).

## Verktyget Innehållsöverföring {#ctt-release}

### Releasedatum {#release-date-ctt}

Releasedatum för Content Transfer Tool v1.9.0 är 28 februari 2022.

### Nyheter {#what-is-new-ctt}

* Kontrollera storleksordrar - Funktionen Kontrollera storlek för verktyget Innehållsöverföring hjälper till att minska misslyckade innehållsöverföringar.  Med funktionen Kontrollera storlek kan användarna 1) avgöra om de har tillräckligt med diskutrymme i underkatalogen `crx-quickstart` innan de extraherar och 2) beräkna storleken på migreringsuppsättningen och verifiera om den stöds. Om en av eller båda dessa kontroller överträds visas varningar i användargränssnittet för aktuell tid. Med den här skyddsguiden kan du undvika innehållsöverföringsfel och proaktivt diskutera migreringsalternativ med Adobe kundtjänst. Mer information finns i [Bestämma migreringsuppsättningens storlek och diskutrymme](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=sv-SE#migration-set-size).

## Best Practices Analyzer {#bpa-release}

### Releasedatum {#release-date-bpa}

Releasedatum för Best Practices Analyzer v2.1.26 är 16 mars 2022.

### Nyheter {#what-is-new-bpa}

* Möjlighet att upptäcka obearbetade resurser. Om obearbetade resurser upptäcks måste dessa resurser antingen ställas in på bearbetad eller tas bort från migreringsuppsättningen under innehållsöverföring för att undvika problem under innehållsimporten.
* Möjlighet att identifiera om innehållet har fler än 1000 ogiltiga URL:er. Det är inte bra att använda ett stort antal användar-URL:er eftersom det belastar Dispatcher- och Publish-servrar.
* Möjlighet att identifiera problem relaterade till Oak indexdefinitioner och upptäcka inkompatibilitet med AEM as a Cloud Service.
* Möjlighet att upptäcka och rapportera om användningen av Externalizer-konfigurationer. I AEM as a Cloud Service Externalizer-konfigurationer anges av Cloud Manager, vilket innebär att befintliga Externalizer-konfigurationer måste ändras för att bibehålla kompatibiliteten.

### Felkorrigeringar {#bug-fixes-bpa}

* I vissa scenarier gick det inte att köra BPA på grund av att FormsSelectiveFeaturesAnalysis genererade ett kontrollfel. Den här har åtgärdats.
* BPA rapporterade fynd relaterade till WRK-mönstret som MAJOR i stället för CRITICAL. Den här har åtgärdats.
* BPA rapporterade felaktigt resultat relaterade till OAK indexdefinitioner i ui.apps som CRITICAL. Detta har åtgärdats

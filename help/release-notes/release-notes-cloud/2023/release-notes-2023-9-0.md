---
title: Versionsinformation för 2023.9.0-utgåvan av [!DNL Adobe Experience Manager] as a Cloud Service.
description: Versionsinformation för 2023.9.0-utgåvan av [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: d747f58b-8d6c-418d-9d2b-ec3ae4b6dc03
source-git-commit: 3f934add7521586caf728c4bfa37f2d1a82b144a
workflow-type: tm+mt
source-wordcount: '1441'
ht-degree: 0%

---


# Versionsinformation 2023.9.0 för [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

I följande avsnitt beskrivs versionsinformationen för den aktuella (senaste) versionen av [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Härifrån kan du navigera till versionsinformation för tidigare versioner som 2021 eller 2022.
>
>Ta en titt på [Roadmap för lanseringar av Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html) om de kommande funktionsaktiviteterna för [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Se [Senaste dokumentationsuppdateringar](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html) för information om dokumentationsuppdateringar som inte är direkt relaterade till en release.

## Releasedatum {#release-date}

Utgivningsdatumet [!DNL Adobe Experience Manager] som [!DNL Cloud Service] aktuell version (2023.9.0) är 28 september 2023. Nästa funktionsrelease (2023.10.0) planeras till 26 oktober 2023.

## Versionsinformation om underhåll {#maintenance}

Du kan hitta den senaste underhållsreleasenumerationen [här](/help/release-notes/maintenance/latest.md).

## Släpp video {#release-video}

Titta på videon med versionsöversikten för september 2023 om du vill se en sammanfattning av funktioner som lagts till i version 2023.9.0:

>[!VIDEO](https://video.tv.adobe.com/v/3424826/?quality=12)

## AEM Edge Delivery Services {#edge-delivery}

Edge Delivery är en ny uppsättning sammanställningsbara tjänster med fokus på att maximera innehållets effekt och få mätbara affärsresultat vid kundinteraktionen.

Läs mer om Edge Delivery Services i artikeln [här](/help/edge/overview.md).

## [!DNL Experience Manager Assets] som [!DNL Cloud Service] {#assets}

### Nya funktioner i resursvyn {#assets-view-features}

**Tilldela metadataformulär till en mapp**

Nu kan du tilldela metadataformulär till en viss mapp i distributionen. Alla resurser i mappen, inklusive resurser i undermapparna, visar sedan egenskaper som definierats i det tilldelade metadataformuläret.

![tilldela metadataformulär till en mapp](/help/release-notes/assets/assign-to-folder.png)

### Nya funktioner i administrationsvyn {#admin-view-features}

* **Integrera AEM Assets as a Cloud Service med dokumentbaserad framtagning av Edge Delivery Services**: Integrera AEM Assets med dokumentbaserad redigering för Edge Delivery Services så att webbutvecklare kan [använda bilder som finns i AEM Assets-databaser när du redigerar dokument i Microsoft Word eller Google Docs](/help/edge/using.md#integrate-assets-edge).

* **Extract ZIP-arkiv**: Möjlighet att välja ZIP-arkiv som hanteras i Experience Manager och [extrahera filerna direkt i Experience Manager](/help/assets/manage-digital-assets.md#extract-zip-archives) utan att ladda ned dem.

  ![Fäst objekt för grupper](/help/release-notes/assets/extract-archive.png)

### Förhandsversioner av funktioner som finns i [!DNL Experience Manager Assets] {#prerelease-features-assets}

* **Dynamic Media**: [Stöd för flera undertexter och flerljudspår för videor i Dynamic Media](/help/assets/dynamic-media/video.md#about-msma)—Nu kan du enkelt lägga till flera undertexter och flera ljudspår i en primär video. Detta innebär att videoklippen är tillgängliga för alla mottagare världen över. Du kan anpassa en enda publicerad primär video till en global publik på flera språk och följa riktlinjer för tillgänglighet för olika geografiska regioner. Författare kan också hantera undertexter och ljudspår från en enda flik i användargränssnittet.

  ![Fliken Undertexter och Ljudspår på sidan Egenskaper för en vald videoresurs.](/help/release-notes/assets/msma-aem-cs.png)*Fliken Undertexter och Ljudspår på sidan Egenskaper för en vald videoresurs.*

## [!DNL Experience Manager Forms] som [!DNL Cloud Service] {#forms}

### Nya funktioner i [!DNL Experience Manager Forms] {#forms-features}

* [**Google reCAPTCHA - företagssupport**](/help/forms/captcha-adaptive-forms-core-components.md): Använd Google reCAPTCHA Enterprise i en adaptiv form för att få bättre skydd mot bedräglig aktivitet och skräppost, vilket ger en säkrare användarupplevelse. Med avancerad riskanalys och smidig integrering kan äkta användare enkelt skicka in formulär medan bots blockeras effektivt.

* [**Adobe Analytics med Experience Cloud Setup Automation för Forms**](/help/forms/enable-adobe-analytics-adaptive-form-using-experience-cloud-setup-automation.md): Nu kan du aktivera Adobe Analytics med Experience Cloud Setup Automation (Automatisering av installationsprogram) med ett par knappar. Det gör att ni kan koppla AEM Forms as a Cloud Service till Experience Platform-taggar och Adobe Analytics för att hämta in och spåra prestandamått för era publicerade formulär.

  >[!VIDEO](https://video.tv.adobe.com/v/3424577/enable-adobe-analytics/?quality=12&learn=on)

* [**Adobe Analytics rapportmall för Adaptiv Forms**](/help/forms/view-understand-aem-forms-analytics-reports.md): Forms as a Cloud Service tillhandahåller nu en Adobe Analytics-rapport, OOTB. Det hjälper er att förstå hur era formulär fungerar. Med hjälp av formulärnivåstatistik får du insikt i hur formuläret fungerar med flera nyckeltal (KPI) som återgivningar, besökare, inskickat material, genomsnittlig fyllnadstid. Genom att följa upp användarbeteenden och feedback kan du identifiera områden i formuläret som orsakar förvirring och vägleda förbättringar av formulärets design och funktion.

  ![Analysrapport om användarinteraktion med adaptiva formulär](/help/forms/assets/forms-analytics-report.png)

* **[Form Fragment in Adaptive Forms based on Core Components](/help/forms/adaptive-form-fragments-core-components.md)**: Ta farväl av dubbelarbete, optimera det digitala arkivet och förbättra samarbetet när ni utökar upplevelsen av formulärgenereringen med formulärfragment. Dessa återanvändbara komponenter kan smidigt integreras i flera formulär, vilket effektiviserar skapandet av enhetliga och proffsiga formulär. Form Fragments säkerställer återanvändbarhet, standardisering och enhetlig varumärkesexponering genom funktionen&quot;change once and mirror everywhere&quot;. Upplev bättre underhålls- och effektivitetsvinster i takt med att uppdateringar som görs på ett och samma ställe sprids automatiskt i alla formulär som använder dessa fragment.

* **[Förbättrat arbetsflöde i Adobe Sign](/help/forms/aem-forms-workflow-step-reference.md#sign-document-step-sign-document-step)**: Adobe Sign Workflow-steget har förbättrats och innehåller följande:
   * **Myndighets-ID-baserad autentisering för Adobe Sign**: Adobe Acrobat Sign Government ID-Based Authentication erbjuder ytterligare ett verifieringslager genom att användarna kan autentisera sin identitet med hjälp av foto-ID:n (körkort, nationellt ID, pass). Genom att använda pålitliga identifieringsdokument ger den här förbättringen ytterligare tillförlitlighet i signeringsprocessen, vilket gör den idealisk för scenarier som kräver högre säkerhet, regelefterlevnad och användarvalidering.

   * **Granskningsspår för Adobe Sign-dokument**: Använd funktionen Granskningsspår för att få detaljerade insikter om livscykeln för dina Adobe Sign-dokument. Med granskningsspåret kan du nu föra ett omfattande register över alla åtgärder och interaktioner som rör dina dokument. Detta inkluderar information som vem som visade, redigerade eller signerade dokumentet, tillsammans med tidsstämplar för varje händelse. Den här förbättringen är avgörande för att upprätthålla regelefterlevnaden, lösa tvister och säkerställa integriteten för dina digitala avtal.

   * **Nya roller för avtalsmottagare utöver bara signeraren**: Adobe Acrobat Sign har möjlighet att utöka rollerna för avtalsmottagare utöver bara signeraren för att bättre matcha deras arbetsflödesbehov. När det här alternativet är aktiverat kan varje mottagare i ett avtal konfigureras individuellt, med signerare som standard.

* **Stöd för sidantal i kommunikations-API:er**: Nu kan du, tillsammans med att hämta ditt dokument via kommunikations-API:erna, även få värdefull information om antalet sidor i dokumentet.

* **[Felhantering med anpassade felhanterare i regelredigeraren](/help/forms/add-custom-error-handler-adaptive-forms-core-components.md)**: Du kan nu anropa en anpassad funktion som svar på ett fel som returnerats av en extern tjänst och ge ett skräddarsytt svar till slutanvändarna. Du kan till exempel anropa ett anpassat arbetsflöde i serverdelen för specifika felkoder eller informera kunden om att tjänsten inte fungerar.

* **[64-bitarsversion av AEM Forms Designer](/help/forms/installing-configuring-designer.md)**: 64-bitarsversionen av AEM Forms Designer ger bättre prestanda, skalbarhet och minneshantering så att du kan skapa formulär. Med 64-bitarsarkitekturen kan du enkelt hantera ännu större och mer komplexa projekt, vilket ger smidiga designarbetsflöden och optimerad effektivitet. Utöka dina formulärdesignmöjligheter och ta till vara framtiden för AEM Forms Designer med den här banbrytande releasen.

### Program för tidig användning {#forms-early-adopter}

* **[Protect dina dokument med DocAssurance API:er (del av kommunikations-API:er)](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**: Med API:erna för DocAssurance kan du skydda känslig information genom att signera och kryptera dokumenten. Genom kryptering omvandlas innehållet i ett dokument till ett oläsligt format så att bara behöriga användare kan få åtkomst till det. Detta förstärkta skydd skyddar inte bara värdefulla data från obehöriga ögon, utan ger även sinnesro. Med signatur-API:erna kan din organisation skydda säkerheten och sekretessen för Adobe PDF-dokument som den distribuerar och tar emot. Den här tjänsten använder digitala signaturer och certifiering för att säkerställa att endast avsedda mottagare kan ändra dokument.

  Du kan skriva till `aem-forms-early-adopter-program@adobe.com` från ditt officiella e-post-id för att gå med i programmet för tidiga användare och begära åtkomst till funktionen.

* **[Headless Adaptive Forms](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html)**: Använd Headless Adaptive Forms för att ge utvecklarna möjlighet att skapa, publicera och hantera interaktiva formulär som kan öppnas och interagera med via API:er, i stället för via ett traditionellt grafiskt användargränssnitt. Headless adaptive forms help you:

   * bygga högkvalitativa flerkanalsformulär på valfritt programmeringsspråk
   * integrera formulär direkt i era datorprogram och mobilappar, webbplatser och chattapplikationer
   * återanvända era egna gränssnittskomponenter med blankettapplikationer
   * använder kraften i Adobe Experience Manager Forms

  Du kan skicka ett e-postmeddelande till `aem-forms-headless@adobe.com` från ditt officiella e-post-ID till att gå med i det tidiga adopterprogrammet.

## [!DNL Experience Manager] som [!DNL Cloud Service] Foundation {#foundation}

### Nytt CDN-cachningsbeteende för kampanjrelaterade URL-parametrar {#cache-url-params}

I nya miljöer tar CDN bort marknadsföringsrelaterade frågeparametrar som standard, vilket ökar marknadsföringskampanjens prestanda och cachelagrar träfffrekvenser. Befintliga miljöer påverkas inte. [Läs mer.](/help/implementing/dispatcher/caching.md#marketing-parameters)

### Trafikfilterregler (inklusive WAF-regler) program för tidig användning {#waf-early-adopter}

Filtrera trafiken vid CDN baserat på:

* begäranrubriker och egenskaper (t.ex. IP-adress)
* trafikmönster som man vet är associerade med skadlig trafik

Är du intresserad av att testa funktionen och ge feedback? Skicka e-post till **aemcs-waf-adopter@adobe.com** från ditt officiella e-post-ID om du vill veta mer om programmet för tidig användning. Utrymmet är begränsat.

Läs mer om funktionen i artikeln [här](/help/security/traffic-filter-rules-including-waf.md).

## Cloud Manager {#cloud-manager}

Du hittar en fullständig lista över månatliga utgåvor av Cloud Manager [här](/help/implementing/cloud-manager/release-notes/current.md).

## Migreringsverktyg {#migration-tools}

Du hittar en fullständig lista över versioner av migreringsverktyg [här](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).

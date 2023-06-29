---
title: Versionsinformation om 2020.8.0-utgåvan av [!DNL Adobe Experience Manager] as a Cloud Service.
description: "[!DNL Adobe Experience Manager] as a Cloud Service Release Notes for 2020.8.0."
exl-id: 83413130-ae90-4419-bcf7-42fdc740452b
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '1033'
ht-degree: 1%

---

# Versionsinformation för [!DNL Adobe Experience Manager] as a Cloud Service 2020.8.0 {#release-notes}

I följande avsnitt beskrivs den allmänna versionsinformationen för Experience Manager as a Cloud Service 2020.8.0.


## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

### Nyheter i [!DNL Sites] {#what-is-new-sites}

* Möjlighet att [återställa sidor och undersidor (sidträd) till en tidigare version](/help/sites-cloud/authoring/features/page-versions.md#reinstating-versions).

* Möjlighet att [skapa startprogram](/help/sites-cloud/authoring/launches/overview.md) i AEM [SPA](/help/implementing/developing/hybrid/introduction.md).


## [!DNL Adobe Experience Manager Assets] as a Cloud Service {#assets}

### Nyheter i [!DNL Assets] {#what-is-new-assets}

* Videoomkodning stöds nu med tillgångsmikrotjänster. Ett nytt avsnitt i [!UICONTROL Processing Profiles] kan du ange videobithastighet och -mått. Utdataformatet är MP4 med H.264-kodeken. Mer information finns i [hantera videoresurser](/help/assets/manage-video-assets.md#transcode-video). För fler omkodningsalternativ och för videoleverans kan du använda [!DNL Dynamic Media] tillägg.

* Vid ny [!DNL Experience Manager Assets] -distributioner är funktionen för smart taggning nu konfigurerad som standard. Du behöver inte integrera manuellt med [!DNL Adobe Developer Console]. I befintliga distributioner konfigurerar administratörer smart taggintegrering som tidigare.

* En ny [upplevelse vid hämtning av resurser](/help/assets/download-assets-from-aem.md) tillåter,

   * Asynkron nedladdning för stora nedladdningar så att användarna inte behöver vänta.
   * Ett nytt modulärt API för utbyggbarhet för utvecklare.

* Extrahering av metadata för tillgångsmikrotjänster har förbättrat prestandan. Det ökar den totala genomströmningen av tillgångsintag.

* Använd en bearbetningsprofil för att generera anpassade metadata med hjälp av beräkningstjänsten. Se [Anpassade metadata med bearbetningsprofil](/help/assets/manage-metadata.md#metadata-compute-service).

* En enklare nedladdningsupplevelse för Brand Portal-användare som administratörer kan konfigurera. Se [översikt över nedladdningsupplevelsen](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/whats-new.html#download-configurations).

* Inbyggda förhandsvisningar och förhandsgranskningar av originaltrogna PDF är nu tillgängliga i Brand Portal. Se [dokumentvisningsprogram - översikt](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/whats-new.html#doc-viewer).

* Nu kan du göra CDN-cachen (Content Delivery Network) ogiltig direkt från [!DNL Dynamic Media] i AEM as a Cloud Service (till skillnad från att använda [!DNL Dynamic Media Classic]). Det säkerställer att de senaste tillgångarna hanteras på några minuter istället för timmar. Se [CDN-cachen har inte verifierats via Dynamic Media](/help/assets/dynamic-media/invalidate-cdn-cache-dynamic-media.md).

* Förbättrat stöd för hjälpmedel finns i användargränssnittskontroller, navigering, bläddring och sökning i [!DNL Assets].

   * Om du trycker på Esc efter att du har markerat [!UICONTROL Add Rendition] så återgår fokus till verktygsfältet. <!-- via CQ-4293594-->
   * Tangentbordsfokus fungerar som väntat när kombinationsrutan E-post används. <!-- via CQ-4286215 -->
   * Elementen dragspelspaneler i sökfilteravsnittet tolkas som utökningsbara standarddragspel. <!-- via CQ-4273103 -->
   * När du använder en tagg på en resurs visas taggarna som trädelement i dialogrutan. ARIA-attributen tillämpas på trädelementen så att de blir tillgängliga nu. <!-- via CQ-4272964 -->

* [!DNL AEM Desktop app] 2.0.3-versionen är nu tillgänglig. Det förbättrar kompatibiliteten med [!DNL Experience Manager] 6.5.5 service pack och har en uppdaterad lista över kompatibiliteter för klientoperativsystem. [!DNL Windows] 7 och [!DNL macOS] versioner tidigare än 10.14 stöds inte.

### Fel som har åtgärdats i [!DNL Assets] {#bugs-fixed}

* Alternativet Relatera och ta bort relatering fungerar inte när användaren klickar på det för första gången. (CQ-4299022)
* När du hämtar en resurs skickas inte e-postmeddelandet om du väljer att ta emot den via e-post. (CQ-4299146)

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Nyheter {#what-is-new-commerce}

* Funktionen produktkonsol är nu tillgänglig. Detta gör att marknadsförare/författare i AEM kan visa och navigera bland kategorier och produkter som lagras i e-handelsservern. Det finns även stöd för egenskaper för kategorier och produkter i produktkonsolen.

* Produkt- och kategoriväljarna har förbättrats så att marknadsförarna kan välja produkt via SKU eller välja kategori via kategori-ID.

## Cloud Manager {#cloud-manager}

### Releasedatum {#release-date-cm}

Releasedatum för [!UICONTROL Cloud Manager] Version 2020.8.0 är 6 augusti 2020.

### Nyheter {#what-is-new-cloud-manager}

* Content Audit är en funktion som är aktiverad i produktionsstegen för Cloud Manager Sites. Konfigurationen av produktionspipeline för program med Sites innehåller nu en tredje flik med namnet **Granskning av innehåll**. När en produktionsprocess körs inkluderas ett nytt Content Audit-steg i produktionsflödet efter anpassad funktionstestning som utvärderar webbplatsen mot ett antal dimensioner, inklusive prestanda, SEO (sökmotoroptimering), tillgänglighet, bästa praxis och PWA (Progressive Web App).


  >[!NOTE]
  >Namnet på Content Audit har ändrats till Experience Audit.

  Se [Testning av Experience Audit](/help/implementing/cloud-manager/experience-audit-testing.md) för mer information.

* Nyligen skapade miljöer i Assets-program konfigureras nu automatiskt med Smart Content Services.

* Vilolägen miljö kan tas bort från viloläget via Cloud Managers **Översikt** sida.

* Möjlighet att utföra Experience Checks på sidor som drivs av Google Lighthuse. Som en del av molnhanterarens pipeline kan upp till 25 sidor kontrolleras och valideras mot upplevelsenyckeltal, och poängen visas i användargränssnittet för molnhanteraren.

### Felkorrigeringar {#bug-fixes-cm}

* Vissa onödiga och oönskade SonarQube-plugin-program kördes som en del av kodkvalitetskontrollen.

* På sidan för pipeline-körning var förgreningsnamnet felaktigt formaterat.

* I vissa fall kunde slutförda pipeline-körningar inte registreras som slutförda, vilket hindrade nya körningar av pipeline.

* Pipeline-exekveringar får ibland *fast* på grund av interna kommunikationsproblem.

* När en ny organisation etablerades fick vissa användare med andra administrativa roller än systemadministratörer felaktigt åtkomst till Cloud Manager.

* Under vissa förhållanden startades uppdateringsindexjobbet flera gånger parallellt, vilket resulterade i ett distributionsfel.

* Verktygstipset på programkorten var inte konsekvent korrekt.

* Användargränssnittet tillät felaktigt försök att utföra åtgärder i en miljö medan det togs bort.

* Ett färgmatchningsfel uppstod i Cloud Managers **Översikt** sida.

### Kända fel {#known-issues-cm}

* Ogiltiga sidor inkluderas för att få medelpoängen för innehållsgranskning under vad de ska vara.

* På fliken Innehållsgranskning visas bas-URL:en felaktigt med författardomänen i stället för publiceringsdomänen.

* Om du vill aktivera steget för innehållsgranskning måste användarna redigera pipeline och, om så önskas, lägga till sidor. Om inga sidor läggs till granskas hemsidan.

## Content Transfer Tool {#content-transfer-tool}

Följ det här avsnittet för att lära dig mer om nyheter och uppdateringar för Content Transfer Tool Release v1.0.4.

### Nyheter {#what-is-new-ctt}

* Innehållsöverföringsverktyget har nu stöd för Shared S3 DataStore.

### Felkorrigeringar {#ctt-bug-fixes}

* Ytterligare tidsgränser har lagts till för att verktyget ska kunna slutföra åtgärder.

* Tidigare version av användargränssnittet kunde ibland extraheras trots att loggen visade fel.

## Verktyg för omstrukturering av kod {#code-refactoring-tools}

Följ det här avsnittet för att lära dig mer om nyheter och uppdateringar för verktygen för kodkorrigering.

### Nyheter {#what-is-new-refactoring}

* AIO-CLI-plugin för att sammanställa kodomfaktoriseringsverktygen så att utvecklare kan anropa och köra verktyg för kodomfaktorisering från ett och samma ställe. Se [Git-resurs: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration) för mer information.

* AEM Dispatcher Converter har utökats med stöd för konverteringar av konfigurationer för lokal och Adobe Managed Services Dispatcher till AEM as a Cloud Service Dispatcher-konfigurationer. Se [Git-resurs: AEM Cloud Service Dispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter) för mer information.

* AEM Dispatcher Converter skrevs om i ` node.js ` och integreras med AIO-CLI-plugin.

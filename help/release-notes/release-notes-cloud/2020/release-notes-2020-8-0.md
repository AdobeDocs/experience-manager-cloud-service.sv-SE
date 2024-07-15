---
title: Versionsinformation för version 2020.8.0 av  [!DNL Adobe Experience Manager] as a Cloud Service.
description: "[!DNL Adobe Experience Manager] as a Cloud Service versionsinformation för 2020.8.0."
exl-id: 83413130-ae90-4419-bcf7-42fdc740452b
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '1025'
ht-degree: 0%

---

# Versionsinformation för [!DNL Adobe Experience Manager] as a Cloud Service 2020.8.0 {#release-notes}

I följande avsnitt beskrivs den allmänna versionsinformationen för Experience Manager as a Cloud Service 2020.8.0.


## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

### Nyheter i [!DNL Sites] {#what-is-new-sites}

* Möjlighet att [återställa sidor och undersidor (sidträd) till en tidigare version](/help/sites-cloud/authoring/sites-console/page-versions.md#reinstating-versions).

* Möjlighet att [skapa starter](/help/sites-cloud/authoring/launches/overview.md) i AEM [SPA ](/help/implementing/developing/hybrid/introduction.md).


## [!DNL Adobe Experience Manager Assets] as a Cloud Service {#assets}

### Nyheter i [!DNL Assets] {#what-is-new-assets}

* Videoomkodning stöds nu med tillgångsmikrotjänster. Med ett nytt avsnitt i [!UICONTROL Processing Profiles]-konfigurationen kan du ange videobithastighet och -mått. Utdataformatet är MP4 med H.264-kodeken. Mer information finns i [Hantera videomaterial](/help/assets/manage-video-assets.md#transcode-video). Använd tillägget [!DNL Dynamic Media] om du vill ha fler omkodningsalternativ och för videoleverans.

* I nya [!DNL Experience Manager Assets]-distributioner är funktionen för smart taggning nu konfigurerad som standard. Du behöver inte integrera manuellt med [!DNL Adobe Developer Console]. I befintliga distributioner konfigurerar administratörer smart taggintegrering som tidigare.

* En ny [resurshämtning](/help/assets/download-assets-from-aem.md) tillåter,

   * Asynkron nedladdning för stora nedladdningar så att användarna inte behöver vänta.
   * Ett nytt modulärt API för utbyggbarhet för utvecklare.

* Extrahering av metadata för tillgångsmikrotjänster har förbättrat prestandan. Det ökar den totala genomströmningen av tillgångsintag.

* Använd en bearbetningsprofil för att generera anpassade metadata med hjälp av beräkningstjänsten. Se [Anpassade metadata med bearbetningsprofilen](/help/assets/manage-metadata.md#metadata-compute-service).

* En enklare nedladdningsupplevelse för Brand Portal-användare som administratörer kan konfigurera. Se [översikt över nedladdningsfunktionen](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/whats-new.html#download-configurations).

* Inbyggda förhandsvisningar och förhandsgranskningar av originaltrogna PDF är nu tillgängliga i Brand Portal. Se [översikt över dokumentvisningsprogrammet](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/whats-new.html#doc-viewer).

* Du kan nu göra CDN-cachen (Content Delivery Network) ogiltig direkt från [!DNL Dynamic Media] i AEM as a Cloud Service (till skillnad från att använda [!DNL Dynamic Media Classic]). Det säkerställer att de senaste tillgångarna hanteras på några minuter istället för timmar. Se [Cacheminnet för CDN har inte verifierats med Dynamic Media](/help/assets/dynamic-media/invalidate-cdn-cache-dynamic-media.md).

* Förbättrat stöd för hjälpmedel har lagts till i användargränssnittskontroller, navigering, bläddring och sökupplevelse i [!DNL Assets].

   * Om du trycker på Esc-tangenten när du har valt alternativet [!UICONTROL Add Rendition] återgår fokus till verktygsfältet. <!-- via CQ-4293594-->
   * Tangentbordsfokus fungerar som väntat när kombinationsrutan E-post används. <!-- via CQ-4286215 -->
   * Elementen dragspelspaneler i sökfilteravsnittet tolkas som utökningsbara standarddragspel. <!-- via CQ-4273103 -->
   * När du använder en tagg på en resurs visas taggarna som trädelement i dialogrutan. ARIA-attributen tillämpas på trädelementen så att de blir tillgängliga nu. <!-- via CQ-4272964 -->

* [!DNL AEM Desktop app] version 2.0.3 är nu tillgänglig. Den förbättrar kompatibiliteten med [!DNL Experience Manager] 6.5.5 Service Pack och har en uppdaterad lista över kompatibiliteter för klientoperativsystem. [!DNL Windows] 7- och [!DNL macOS]-versioner tidigare än 10.14 stöds inte.

### Fel som har åtgärdats i [!DNL Assets] {#bugs-fixed}

* Alternativet Relatera och ta bort relatering fungerar inte när användaren klickar på det för första gången. (CQ-4299022)
* När du hämtar en resurs skickas inte e-postmeddelandet om du väljer att ta emot den via e-post. (CQ-4299146)

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Nyheter {#what-is-new-commerce}

* Funktionen produktkonsol är nu tillgänglig. Detta gör att marknadsförare/författare i AEM kan visa och navigera bland kategorier och produkter som lagras i e-handelsservern. Det finns även stöd för egenskaper för kategorier och produkter i produktkonsolen.

* Produkt- och kategoriväljarna har förbättrats så att marknadsförarna kan välja produkt via SKU eller välja kategori via kategori-ID.

## Cloud Manager {#cloud-manager}

### Releasedatum {#release-date-cm}

Releasedatum för [!UICONTROL Cloud Manager] version 2020.8.0 är 6 augusti 2020.

### Nyheter {#what-is-new-cloud-manager}

* Content Audit är en funktion som aktiveras i Cloud Manager Sites Production Pipelines. Konfigurationen av produktionspipeline för program med platser innehåller nu en tredje flik med namnet **Content Audit**. När en produktionsprocess körs inkluderas ett nytt steg för innehållsgranskning efter en anpassad funktionstestning, som utvärderar webbplatsen mot flera dimensioner, inklusive prestanda, SEO (sökmotoroptimering), tillgänglighet, bästa praxis och PWA (Progressive Web App).


  >[!NOTE]
  >Namnet på Content Audit har ändrats till Experience Audit.

  Mer information finns i [Experience Audit Testing](/help/implementing/cloud-manager/experience-audit-testing.md).

* Nya miljöer i Assets-program konfigureras nu automatiskt med Smart Content Services.

* Vilolägda miljöer kan tas bort från viloläget på Cloud Manager **Översikt** -sida.

* Möjlighet att utföra Experience Checks på sidor som drivs av Google Lighthuse. Som en del av Cloud Manager pipeline kan upp till 25 sidor kontrolleras och valideras mot upplevelsenyckeltal, och poängen visas i Cloud Manager användargränssnitt.

### Felkorrigeringar {#bug-fixes-cm}

* Vissa onödiga och oönskade SonarQube-plugin-program kördes som en del av kodkvalitetskontrollen.

* På sidan för pipeline-körning var förgreningsnamnet felaktigt formaterat.

* I vissa fall kunde slutförda pipeline-körningar inte registreras som slutförda, vilket hindrade nya körningar av pipeline.

* Pipeline-körningar får ibland *fast* på grund av interna kommunikationsproblem.

* När en ny organisation etablerades gavs en del användare med andra administrativa roller än systemadministratörer felaktigt åtkomst till Cloud Manager.

* Under vissa förhållanden startades uppdateringsindexjobbet flera gånger parallellt, vilket resulterade i ett distributionsfel.

* Verktygstipset på programkorten var inte konsekvent korrekt.

* Användargränssnittet tillät felaktigt försök att utföra åtgärder i en miljö medan det togs bort.

* Färgmatchningsfelet uppstod på sidan **Översikt** för Cloud Manager.

### Kända fel {#known-issues-cm}

* Ogiltiga sidor inkluderas för att få medelpoängen för innehållsgranskning under vad de ska vara.

* På fliken Innehållsgranskning visas bas-URL:en felaktigt med författardomänen i stället för publiceringsdomänen.

* Om du vill aktivera steget för innehållsgranskning måste användarna redigera pipeline och, om så önskas, lägga till sidor. Om inga sidor läggs till granskas hemsidan.

## Verktyget Innehållsöverföring {#content-transfer-tool}

Följ det här avsnittet för att lära dig mer om nyheter och uppdateringar för Content Transfer Tool Release v1.0.4.

### Nyheter {#what-is-new-ctt}

* Innehållsöverföringsverktyget har nu stöd för Shared S3 DataStore.

### Felkorrigeringar {#ctt-bug-fixes}

* Ytterligare tidsgränser har lagts till för att verktyget ska kunna slutföra åtgärder.

* Tidigare version av användargränssnittet kunde ibland extraheras trots att loggen visade fel.

## Kodomfaktoriseringsverktyg {#code-refactoring-tools}

Följ det här avsnittet för att lära dig mer om nyheter och uppdateringar för verktygen för kodkorrigering.

### Nyheter {#what-is-new-refactoring}

* AIO-CLI-plugin för att sammanställa kodomfaktoriseringsverktygen så att utvecklare kan anropa och köra verktyg för kodomfaktorisering från ett och samma ställe. Mer information finns i [Git-resurs: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration).

* AEM Dispatcher Converter har utökats med stöd för konverteringar av Managed Services Dispatcher-konfigurationer på plats och Adobe till AEM as a Cloud Service-kompatibla Dispatcher-konfigurationer. Mer information finns i [Git-resurs: AEM Cloud Service Dispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter).

* AEM Dispatcher Converter skrevs om i ` node.js ` och är integrerat med AIO-CLI-plugin.

---
title: Versionsinformation för 2020.8.0-utgåvan [!DNL Adobe Experience Manager] av en Cloud Service.
description: '[!DNL Adobe Experience Manager] som Cloud Service versionsinformation för 2020.8.0.'
translation-type: tm+mt
source-git-commit: ff50361ca66a5c3685d7701432069fec9521f0d7
workflow-type: tm+mt
source-wordcount: '1043'
ht-degree: 0%

---


# Versionsinformation för [!DNL Adobe Experience Manager] som Cloud Service 2020.8.0 {#release-notes}

I följande avsnitt beskrivs den allmänna versionsinformationen för Experience Manager som Cloud Service 2020.8.0.

## Releasedatum {#release-date}

Releasedatum för [!DNL Experience Manager] Cloud Service 2020.8.0 är 27 augusti 2020.

## [!DNL Adobe Experience Manager Sites] som en Cloud Service {#sites}

### What is new in [!DNL Sites] {#what-is-new-sites}

* Möjlighet att [återställa sidor och undersidor (sidträd) till en tidigare version](/help/sites-cloud/authoring/features/page-versions.md#reinstating-versions).

* Möjlighet att skapa startprogram AEM SPA Editor.

## [!DNL Adobe Experience Manager Assets] som en Cloud Service {#assets}

### What is new in [!DNL Assets] {#what-is-new-assets}

* Videoomkodning stöds nu med tillgångsmikrotjänster, med ett nytt Video-avsnitt på skärmen som stöder konfiguration av videobithastighet och dimensioner (utdataformatet är MP4 med H.264-kodek). [!UICONTROL Processing Profiles] Mer information finns i [Hantera videomaterial](/help/assets/manage-video-assets.md#transcode-video). För fler omkodningsalternativ och [!DNL Dynamic Media] tillägg för videoleverans kan användas.

* I nya [!DNL Experience Manager Assets] distributioner är funktionen för smart taggning nu konfigurerad som standard. Du behöver inte integrera manuellt med [!DNL Adobe Developer Console]. I befintliga distributioner [konfigurerar administratörer smart taggintegrering](/help/assets/smart-tags-configuration.md#aio-integration) som tidigare.

* Med en ny [resurshämtning](/help/assets/download-assets-from-aem.md) kan

   * Asynkron nedladdning för stora nedladdningar så att användarna inte behöver vänta.

   * Ett nytt modulärt API för utbyggbarhet för utvecklare.

* [!DNL Experience Manager] har förbättrat prestandan för metadataextrahering för tillgångsmikrotjänster. Det ökar den totala genomströmningen av tillgångsintag.

* Använd bearbetningsprofil för att generera anpassade metadata med hjälp av beräkningstjänsten. Se [Anpassade metadata med bearbetningsprofil](/help/assets/manage-metadata.md#metadata-compute-service)

* En enklare nedladdningsupplevelse för användare av varumärkesportalen som administratörer kan konfigurera. Se Översikt över [nedladdningsupplevelsen](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/introduction/whats-new.html#download-configurations).

* Inbyggda förhandsgranskningar av PDF-dokument med hög originalåtergivning finns nu tillgängliga i varumärkesportalen. Se Översikt över [dokumentvisningsprogrammet](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/introduction/whats-new.html#doc-viewer).

* Nu kan du göra CDN-cachen (Content Delivery Network) ogiltig direkt från [!DNL Dynamic Media] AEM som en Cloud Service (till skillnad från att använda [!DNL Dynamic Media Classic]) för att se till att de senaste resurserna hanteras på några minuter istället för timmar. Se [Invalidera CDN-cachen med hjälp av Dynamic Media](/help/assets/dynamic-media/invalidate-cdn-cache-dynamic-media.md)

* Förbättrat stöd för hjälpmedel finns i användargränssnittskontroller, navigering, bläddring och sökupplevelser i [!DNL Assets].

   * Om du trycker på Esc när du har valt [!UICONTROL Add Rendition] alternativet återgår fokus till verktygsfältet. <!-- via CQ-4293594-->
   * Tangentbordsfokus fungerar som väntat när kombinationsrutan E-post används. <!-- via CQ-4286215 -->
   * Elementen dragspelspaneler i sökfilteravsnittet tolkas som utökningsbara standarddragspel. <!-- via CQ-4273103 -->
   * När du använder en tagg på en resurs visas taggarna som trädelement i dialogrutan. ARIA-attributen tillämpas på trädelementen så att de blir tillgängliga nu. <!-- via CQ-4272964 -->

* [!DNL AEM Desktop app] 2.0.3-versionen är nu tillgänglig, vilket förbättrar kompatibiliteten med [!DNL AEM] 6.5.5 [!DNL Service Pack] och uppdaterar klientens OS-kompatibilitetslista (7 och [!DNL Windows] [!DNL MacOS] tidigare versioner än 10.14 tas bort).

### Fel som har åtgärdats i [!DNL Assets] {#bugs-fixed}

* Alternativet Relatera och ta bort relatering fungerar inte när användaren klickar på det för första gången. (CQ-4299022)
* När du hämtar en resurs skickas inte e-postmeddelandet om du väljer att ta emot den via e-post. (CQ-4299146)

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### What&#39;s New {#what-is-new-commerce}

* Funktionen produktkonsol är nu tillgänglig. Detta gör att marknadsförare/författare i AEM kan visa och navigera bland kategorier och produkter som lagras i e-handelsservern. Det finns även stöd för egenskaper för kategorier och produkter i produktkonsolen.

* Produkt- och kategoriväljarna har förbättrats så att marknadsförarna kan välja produkt via SKU eller välja kategori via kategori-ID.

## Cloud Manager {#cloud-manager}

### Releasedatum {#release-date-cm}

Releasedatum för [!UICONTROL Cloud Manager] version 2020.8.0 är 6 augusti 2020.

### What&#39;s New {#what-is-new-cloud-manager}

* Content Audit är en funktion som är aktiverad i produktionsstegen för Cloud Manager Sites. Konfigurationen av produktionspipeline för program med platser innehåller nu en tredje flik med namnet **Content Audit**. När en produktionsprocess körs inkluderas ett nytt Content Audit-steg i produktionsflödet efter anpassad funktionstestning som utvärderar webbplatsen mot ett antal dimensioner, inklusive prestanda, SEO (sökmotoroptimering), tillgänglighet, bästa praxis och PWA (Progressive Web App).

   Refer to [Content Audit Testing](/help/implementing/cloud-manager/content-audit-testing.md) for more details.

* Nyligen skapade miljöer i Assets-program konfigureras nu automatiskt med Smart Content Services.

* Vilolägda miljöer kan tas bort från vänteläget på sidan **Översikt** i Cloud Manager.

* Möjlighet att utföra Experience Checks på sidor med Google Lighthuse som bas. Som en del av molnhanterarens pipeline kan upp till 25 sidor kontrolleras och valideras mot upplevelsenyckeltal, och poängen visas i användargränssnittet för molnhanteraren.

### Bug Fixes {#bug-fixes-cm}

* Vissa onödiga och oönskade SonarQube-plugin-program kördes som en del av kodkvalitetskontrollen.

* På sidan för pipeline-körning var förgreningsnamnet felaktigt formaterat.

* I vissa fall kunde slutförda pipeline-körningar inte registreras som slutförda, vilket hindrade nya körningar av pipeline.

* Körningar av rörledningar *fastnar* ibland på grund av interna kommunikationsproblem.

* När en ny organisation etablerades fick vissa användare med andra administrativa roller än systemadministratörer felaktigt åtkomst till Cloud Manager.

* Under vissa förhållanden startades uppdateringsindexjobbet flera gånger parallellt, vilket resulterade i ett distributionsfel.

* Verktygstipset på programkorten var inte konsekvent korrekt.

* Användargränssnittet tillät felaktigt försök att utföra åtgärder i en miljö medan det togs bort.

* Det fanns ett färgmatchningsfel på sidan **Översikt** i Cloud Manager.

### Kända fel {#known-issues-cm}

* Ogiltiga sidor inkluderas för att få medelpoängen för innehållsgranskning under vad de ska vara.

* På fliken Innehållsgranskning visas bas-URL:en felaktigt med författardomänen i stället för publiceringsdomänen.

* För att aktivera steget Innehållsgranskning måste användarna redigera pipeline och, om så önskas, lägga till sidor. Om inga sidor läggs till granskas hemsidan.

## Content Transfer Tool {#content-transfer-tool}

Följ det här avsnittet för att lära dig mer om nyheter och uppdateringar för Content Transfer Tool Release v1.0.4.

### What&#39;s New {#what-is-new-ctt}

* Innehållsöverföringsverktyget har nu stöd för Shared S3 DataStore.

### Bug Fixes {#ctt-bug-fixes}

* Ytterligare tidsgränser har lagts till för att verktyget ska kunna slutföra åtgärder.

* Tidigare version av användargränssnittet kunde ibland extraheras trots att loggen visade fel.

## Verktyg för omstrukturering av kod {#code-refactoring-tools}

Följ det här avsnittet för att lära dig mer om nyheter och uppdateringar för verktygen för kodkorrigering.

### What&#39;s New {#what-is-new-refactoring}

* AIO-CLI-plugin för att sammanställa kodomfaktoriseringsverktygen så att utvecklare kan anropa och köra verktyg för kodomfaktorisering från ett och samma ställe. Se [Git-resurs: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration) för mer information.

* AEM Dispatcher Converter har utökats med stöd för konverteringar av konfigurationer för lokal och Adobe Managed Services Dispatcher till AEM som en Cloud Service-kompatibel Dispatcher-konfigurationer. Se [Git-resurs: AEM Cloud Service Dispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter) för mer information.

* AEM Dispatcher Converter skrivs om i ` node.js ` och integreras med AIO-CLI-pluginprogrammet.

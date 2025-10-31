---
title: Versionsinformation om 2025.9.0-utgåvan av  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Versionsinformation om 2025.9.0-utgåvan av  [!DNL Adobe Experience Manager] as a Cloud Service.
feature: Release Information
role: Admin
source-git-commit: ed51ff8df6d1e387960e8580c6dfb543a09ef8fa
workflow-type: tm+mt
source-wordcount: '2083'
ht-degree: 0%

---

# Versionsinformation 2025.9.0 för [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

I följande avsnitt beskrivs versionsinformationen för funktionen för 2025.9.0-versionen av [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Härifrån kan du navigera till versionsinformation för tidigare versioner som 2023 eller 2024.
>
>Ta en titt på [Experience Manager Releases Roadmap](https://experienceleague.adobe.com/sv/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) om du vill veta mer om kommande funktionsaktiveringar för [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Om du vill få ett månatligt e-postmeddelande om uppdateringar av Experience Cloud versionsinformation prenumererar du på [Adobe Priority Product Update](https://www.adobe.com/subscription/priority-product-update.html).

## Releasedatum {#release-date}

Releasedatum för [!DNL Adobe Experience Manager] som [!DNL Cloud Service] aktuell funktionsversion (2025.9.0) är 25 september 2025. Nästa funktionsrelease (2025.10.0) planeras till 30 oktober 2025.

## Versionsinformation om underhåll {#maintenance}

Du hittar den senaste underhållsversionsinformationen [här](/help/release-notes/maintenance/latest.md).

<!-- 

## Release Video {#release-video}

Have a look at the July 2025 Release Overview video for a summary of the features added in the 2025.7.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3440920?quality=12)

-->

## [!DNL Experience Manager Sites] som en [!DNL Cloud Service] {#sites}

### Nya funktioner i Experience Manager Sites Prerelease {#prerelease-sites}

Innehållsmodellredigeraren för AEM Content Fragments har moderniserats för att passa ihop med andra React Spectrum-baserade gränssnitt i AEM. Implementeringen av användargränssnittet och utbyggbarhetsmodellen överensstämmer nu med Content Fragment Editor och Universal Editor. Den nya modellredigeraren är nu standard när den öppnas från det nya gränssnittet för innehållsmodelladministratör. Om du öppnar en innehållsmodell i Touch-gränssnittet öppnas Touch UI-redigeraren och den nya redigeraren erbjuds att testa.

## [!DNL Experience Manager Assets] som en [!DNL Cloud Service] {#assets}

### Nya funktioner i vyn Assets {#new-features-assets-view}

**Förbättrad textformatering med delsträngar i dynamiska mediamallar**

Du kan nu använda formatering på delsträngar i textlager i mallen Dynamic Media. Ett markerat ord eller en fras behandlas som ett separat lager så att du kan justera teckensnitt, teckenstorlek, färg med mera. Delsträngslagret parametriseras så att du kan uppdatera det i realtid med mallens leverans-URL

### Nya funktioner i Dynamic Media med OpenAPI-funktioner {#new-features-dynamic-media-with-openapi}

**URL:er för varumärkesprofilerad och läsbar tillgångsleverans**

Gör Dynamic Media med OpenAPI-URL:er mer läsbara genom att utnyttja Vanity-URL:er i Dynamic Media med OpenAPI. Vanity-URL:er gör det möjligt att ersätta långa, systemgenererade, svåra att memorera UUID:n i URL:er för tillgångsleverans med korta, varumärkesstyrda identifierare. Detta gör Vanity-URL:er kortare, enklare att läsa och dela och ger bättre anpassning till ert varumärke eller era kampanjer. Vanity-URL:er löses automatiskt till det ursprungliga resurs-UUID:t vid körning utan att befintliga arbetsflöden avbryts.

>[!NOTE]
>
>Den här funktionen är tillgänglig som en begränsad tillgänglighetsfunktion. Se den här [artikeln](/help/assets/vanity-urls.md) för att komma igång.

### Nya funktioner i Content Hub {#new-features-content-hub}

**Markera samlingar som favoriter**

Nu kan du markera samlingar som favoriter i Content Hub, vilket gör det enklare att ordna och hämta dem. När du har lagt till dina favoritsamlingar kan du enkelt komma åt dem från fliken Favoriter på Content Hub hemsida.


**Fäst samlingar för snabb åtkomst**

Content Hub-administratörer kan nu fästa samlingar i Content Hub för snabb åtkomst. Fastnålade samlingar visas i ett särskilt avsnitt på startsidan för samlingar, vilket gör det enklare att hålla viktiga samlingar tillgängliga.

>[!IMPORTANT]
>
>De här funktionerna är tillgängliga som funktioner för begränsad tillgänglighet. Du kan [skapa och skicka ett Adobe kundsupportärende](https://helpx.adobe.com/se/enterprise/using/support-for-experience-cloud.html) för att aktivera det för din distribution.

<!--

### New Features in Content Hub {#new-features-content-hub}

**Mark Collections as Favourites**

You can now mark collections as Favorites in Content Hub, making it easier to organize and retrieve them. Once added, your favourite collections are conveniently available from the **Favourites** tab on the Content Hub home page.

**Pin collections for quick access**

Content Hub Administrators can now pin collections in Content Hub for quick access. Pinned collections are displayed in a dedicated **Pinned** section on the Collections home page, making it easier to keep important collections within reach.

>[!NOTE]
>
>These features are available as Limited Availability features. You can [create and submit an Adobe Customer Support case](https://helpx.adobe.com/se/enterprise/using/support-for-experience-cloud.html) to enable it for your deployment.

-->

## [!DNL Experience Manager Forms] som en [!DNL Cloud Service] {#forms}

### Nya funktioner i Experience Manager Forms {#new-features-forms}

**Starta arbetsflödessteget för formulärdatamodell för SharePoint-listbilagor**

Arbetsflödessteget Anropa formulärdatamodell har nu stöd för hantering av metadata på arbetsflödessidan för Base64-kodade bilagematriser i SharePoint List-baserade formulärdatamodeller. Med den här förbättringen kan arbetsflödessteget skicka, lagra och hämta metadata som filnamn, MIME-typ och anpassade egenskaper för varje bifogad fil. Denna funktion möjliggör mer omfattande datahantering och underlättar smidig integrering längre fram i kedjan. Mer information finns i [Utökat stöd i arbetsflödessteget Anropa formulärdatamodell för SharePoint List-bilagor](/help/forms/aem-forms-workflow-step-reference.md#invoke-form-data-model-fdm-service-step).

<!-- ### Pre-Release features in AEM Forms -->

### Nya funktioner för tidig åtkomst i AEM Forms {#forms-new-early-access-features}

AEM Forms Early Access Program ger dig unika möjligheter att få exklusiv tillgång till de senaste innovationerna och hjälpa till att utforma deras utveckling.

I versionsinformationen visas de innovationer som levererats i den aktuella versionen. En fullständig lista över de innovationer som är tillgängliga under Tidig åtkomst-programmet finns i [AEM Forms Tidig åtkomst-programdokumentation](/help/forms/early-access-ea-features.md).

* **PDF Preview i Interactive Communication Editor**

  Användare kan förhandsgranska interaktiva dokument utan data, med lokala JSON-datafiler eller med data från en datamodell, vilket möjliggör flexibel datadriven testning. Mer information finns i [PDF Preview i den interaktiva kommunikationsredigeraren](/help/forms/interactive-communication/pdf-preview-in-interactive-communication-editor-with-different-data-options.md).

* **Stöd för anpassade teckensnitt i interaktiv kommunikation**

  Med funktionen för anpassade teckensnitt kan man bädda in anpassade eller organisationsgodkända teckensnitt i Interactive Communications för att säkerställa enhetlig och varumärkesprofilerad PDF-återgivning på olika enheter och plattformar. Mer information finns i [Stöd för anpassade teckensnitt i interaktiv kommunikation](/help/forms/interactive-communication/add-custom-fonts-to-interactive-communication-editor.md).

* **Importera och exportera interaktiv kommunikation**

  Med den här funktionen kan du migrera och återanvända interaktiv kommunikation i olika miljöer. Nu kan du exportera en interaktiv kommunikation tillsammans med tillhörande fragment och datamodeller från en miljö och importera den till en annan. Mer information finns i [Importera och exportera interaktiv kommunikation](/help/forms/interactive-communication/import-and-export-interactive-communications.md).

* **Förbättringar i regelredigeraren**

  Regelredigeraren har nu stöd för förbättrad navigering och tillåter användning av funktioner och matematiska uttryck i indataparametrar.

   * **Förbättrad navigering med stöd för händelsenyttolast**: Åtgärden `Navigate To` i Invoke Service-hanterarna har nu stöd för `EVENT_PAYLOAD`, vilket gör att formulärförfattare kan konfigurera uppföljningsåtgärder baserat på händelsesvar. Den här förbättringen ger större flexibilitet vid utformningen av arbetsflöden efter inskickandet, vilket ger smidigare övergångar och mer personaliserade användarupplevelser. Mer information finns i [Förbättrad navigering med stöd för händelsenyttolast](/help/forms/invoke-service-enhancements-rule-editor.md#use-case-5-use-event-payload-in-navigate-to-action-in-invoke-service).

   * **Stöd för funktioner och matematiska uttryck i indataparametrar**: Indataparametrarna har nu stöd för både funktionsanrop och matematiska uttryck, vilket gör att formulärförfattare kan skicka dynamiskt beräknade värden direkt. Den här förbättringen effektiviserar regelkonfigurationer, eliminerar behovet av extra fält och gör formulär mer anpassningsbara till komplexa logiska och beräkningsdrivna scenarier. Mer information finns i [Funktion och stöd för matematiska uttryck i Indataparametrar](/help/forms/rule-editor-core-components-user-interface.md#function-and-mathematical-expression-support-in-input-parameters).

<!--
**Forms Optimization opportunities**

Forms Optimization uses AI to analyze your forms and suggest improvements for better performance. It highlights forms with low engagement, flags accessibility issues, and generates AI-powered variations to help increase conversion rates and compliance with WCAG standards.

>[!VIDEO](https://video.tv.adobe.com/v/3469472/) 

Key optimization opportunities include:

* Increasing visibility for forms with low views
* Improving completion rates for forms with low conversions
* Addressing accessibility compliance issues
* Streamlining navigation to enhance user experience

With Forms Optimization, you get automated, data-driven recommendations and variations, making it easier to boost engagement and ensure your forms are effective and inclusive. 
-->

## [!DNL Experience Manager] som en [!DNL Cloud Service]-grund {#foundation}

### Nya funktioner i versionshantering {#new-features-release-management}

**Pausa automatiska underhållsuppdateringar**

Dagar live, live event, toppförsäljning - dessa stunder kan inte brytas. [Våra nya självbetjäningsfunktioner](/help/implementing/deploying/quiet-hours-update-free-periods.md) avbryter automatiskt underhåll av uppdateringar när det behövs, så att era team kan fokusera.

* Tysta timmar: Blockera automatiskt underhåll under fasta tider varje dag. Idealiskt för arbetstider, nattkörningar eller morgonavslutningar.
* Uppdateringsfri period: Blockera automatiskt underhåll under en hel vecka. Använd den för lanseringar, kampanjer eller årsfrysningar.

>[!NOTE]
>
>Tillgänglig som begränsad tillgänglighet den 25 september.
>&#x200B;>Skicka ett e-postmeddelande till [aemcs-update-free@adobe.com](mailto:aemcs-update-free@adobe.com) om du vill aktivera det i dina program.

### Ny version av AEM Developer Tools for Eclipse {#aem-develeper-tools-for-eclipse}

Version 1.4.0 av AEM Developer Tools för Eclipse har släppts. Den här versionen har stöd för Eclipse IDE 2022-12 eller senare och har validerats med den aktuella versionen (2025-09). Verktygen fungerar nu med moderna versioner av AEM Project Archetype och innehåller förbättringar från Sling IDE Tooling 1.3.0.

Installera från [Eclipse Marketplace](https://marketplace.eclipse.org/content/aem-developer-tools-eclipse) och se sidan [AEM Developer Tools](https://eclipse.adobe.com) för mer information.

### Kommande Java API-borttagningar {#java-api-deprecation}

Flera inaktuella API:er markerades för borttagning den 31 augusti och bör därför inte längre refereras. Du får meddelanden från Åtgärdscenter om föråldrad API-användning upptäcks i koden, och efter den 13 november visas meddelanden under Cloud Manager-byggen för att förstärka vikten av att ta bort användningen. Mer information finns i artikeln [som inte längre används](/help/release-notes/deprecated-removed-features.md#aem-apis), men dessa API:er finns i listan nedan för att underlätta:

+++ Expandera om du vill visa Java API-borttagningar

* `org.apache.sling.commons.auth`
* `org.apache.felix.webconsole`
* `org.eclipse.jetty`
* `com.mongodb`
* `org.apache.abdera`
* `org.apache.felix.http.whiteboard`
* `org.apache.cocoon.xml`
* `ch.qos.logback`
* `org.slf4j.spi`
* `org.slf4j.event`
* `org.apache.log4j`
* `com.google.common`
* `com.drew`
* `org.bson`
* `org.apache.jackrabbit.oak.plugins.blob`
* `org.apache.jackrabbit.oak.plugins.memory`

+++

<!--
OSGi properties:

* `org.apache.sling.commons.log.LogManager` (all properties)
* `org.apache.sling.commons.log.LogManager.factory.config` (`org.apache.sling.commons.log.file`, `org.apache.sling.commons.log.pattern`)
* 

-->

### Java 11 Runtime Deprecation {#java11-runtime-deprecation}

*Java 11-miljön* är föråldrad och de flesta miljöer har redan uppgraderats till **Java 21-miljön** med högre prestanda.

Om din miljö inte kunde uppgraderas på grund av beroenden som inte stöds (se [Java 21-körningskraven](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements)) bör du ha fått ett e-postmeddelande från Adobe med nästa steg. Så som beskrivs nedan uppgraderade Adobe din **Dev** - och **RDE** -miljö den **18 september 2025** så att du kan validera din plats och dina processer och åtgärda eventuella problem. Uppgraderingar för **Stage** och **Production** fortsätter den **14 oktober 2025**.

>[!NOTE]
>
>Körningsversionen är skild från koden. Vi rekommenderar att du bygger med Java 21, men Java 11-byggen är fortfarande godkända för tillfället. Ett separat meddelande om borttagning av Java 11-byggen kommer att delas i framtiden.

### Tillämpning av konfigurationspolicy för AEM Java-loggar {#logconfig-policy}

Som framgår av versionsinformationen för april måste AEM Java-loggarna följa ett standardformat för att säkerställa tillförlitlig övervakning i alla kundmiljöer. Anpassade loggkonfigurationer, t.ex. ändringar i loggformatering, utdatafiler eller standardloggnivåer, stöds inte längre. Loggar måste vara dirigerade till standardfilerna och standardloggnivåerna för AEM-produktkoden måste bevaras. Mer information finns i artikeln [Loggning](/help/implementing/developing/introduction/logging.md#configuration-loggers).

Med början den **30 oktober** kommer alla anpassade loggningsåsidosättningar som inte stöds att ignoreras. Baserat på vår analys kommer de flesta kunder inte att påverkas och Adobe har kontaktat kunder vars nuvarande konfiguration kan påverkas.

Granska och uppdatera alla processer som är beroende av anpassat loggningsbeteende. Till exempel:

* Om ditt system för vidarebefordring av loggar förväntar sig ett anpassat loggformat kan du behöva justera dina regler för inmatning.
* Om du tidigare har minskat loggens utförlighet genom att ändra loggnivåerna bör du tänka på att en återställning till standardnivåerna kan öka loggvolymen.

### Edge Computing (Beta Program) {#edge-computing}

Med Edge kan du köra JavaScript på CDN-lagret, vilket tar databearbetningen närmare slutanvändaren. Detta minskar latensen och möjliggör responsiva, dynamiska upplevelser i framkanten.

Exempel på vanliga användningsområden:

* Anpassa innehåll baserat på geografisk placering, enhetstyp eller användarattribut
* Fungerar som mellanvara mellan CDN och ditt ursprung
* Formatera om svar från tredjeparts-API:er (och kanske samla in flera API-svar) innan de skickas till webbläsaren
* Skapa och leverera serveråtergivna HTML i toppklass med material som sammanfogats från olika bakgrunder
* Exponera en MCP-server för LLM-program som ChatGPT och Claude för att få tillgång till anpassade verktyg

Vi har ett begränsat antal möjligheter, antingen för AEM Publish Delivery eller för Edge Delivery Services-projekt, för produktionssajter. Om du är intresserad av att delta eller vill veta mer kan du skicka ett e-postmeddelande till [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) med en kort beskrivning av ditt användningsfall.

### Edge-autentisering för Edge Delivery Services (Beta-programmet) {#edge-authentication}

Med Edge Authentication kan du begränsa åtkomsten till Edge Delivery Services-sidor till endast de som har autentiserats hos din identitetsleverantör (IdP). Detta uppnås genom att distribuera en YAML-fil med OpenID Connect-konfiguration (OIDC).

Om du är intresserad kan du skicka ett e-postmeddelande till [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) med en kort beskrivning av ditt användningsfall och eventuella frågor du har.

<!--
### CDN Configuration for Edge Delivery Services (Beta Program) {#cdn-eds-beta}

The Adobe-Managed CDN offers flexible configuration options, as described in the [Config Pipeline article](/help/operations/config-pipeline.md#configurations). 

Now in beta, youcan deploy a config pipeline for features including CDN origin selectors, response and request transformations, CDN log forwarding and more. Please reach out to [aemcs-cdn-config-adopter@adobe.com](mailto:aemcs-cdn-config-adopter@adobe.com) with the details of your use case.

-->

### Kanarieproduktionsdistributioner till testkod innan Live-trafik godkänns (Beta-programmet) {#canary-beta}

Validera en produktionsbygge med intern testtrafik innan den visas för slutanvändarna. Leverera till produktion, dirigera endast kanarietrafik (med en särskild rubrik), övervaka beteendet och sedan antingen marknadsföra till livstrafik eller backa - utan att det påverkar kunderna.

Distribuera era kodreleaser till produktion, men begränsa den till enbart intern testtrafik innan du bestämmer dig för att acceptera direkttrafik eller återställa.

Skicka e-post till [aemcs-canary-deployments-beta@adobe.com](mailto:aemcs-canary-deployments-beta@adobe.com) för att begära åtkomst och dela feedback.

### Ögonblicksbilder för RDE (Alpha Program) {#rde-snapshot-program}

I alfa har Rapid Development Environment (RDE) nu stöd för en funktion som tar en ögonblicksbild av det aktuella kodläget och innehållet, som kan återställas vid ett senare tillfälle. Detta kan vara användbart när du synkroniserar kod som behöver återställas eller när du växlar mellan utveckling av olika funktioner. Det går också att återställa bara det ändringsbara innehållet som en känd startpunkt för testning.

Skicka ett e-postmeddelande till [aemcs-rde-support@adobe.com](mailto:aemcs-rde-support@adobe.com) om du är intresserad av att lämna feedback om funktionen.

### AEM Log-Forwarding to More Destinations (Beta Program) {#log-forwarding-beta}

Medan loggar kan hämtas från Cloud Manager tycker många att det är bra att strömma dessa loggar till ett önskat loggningsmål. AEM har redan stöd för AEM- och CDN-loggvidarebefordran till Azure Blob Storage, Datadog, HTTPS, Elasticsearch (och OpenSearch) och Splunk. Den här funktionen är konfigurerad på ett självbetjäningssätt och distribueras med Config Pipeline.

I betaversionen kan du nu vidarebefordra AEM-loggar till Amazon S3, Sumo Logic, Dynatrace och ditt eget New Relic-konto (inte till Adobe-kontot). Observera att AEM-loggar (inklusive Apache/Dispatcher) stöds för dessa loggningsmål, men inte CDN-loggar. E-post [aemcs-logforwarding-beta@adobe.com](mailto:aemcs-logforwarding-beta@adobe.com) för åtkomst.

Läs mer i [dokumentationen för vidarebefordran av loggfiler](/help/implementing/developing/introduction/log-forwarding.md).

### Utökad APM (Application Performance Monitoring) (Alpha-program) {#apm-alpha}

AEM Cloud-tjänsten har för närvarande stöd för [New Relic One](https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/user-access-new-relic) som tillhandahålls av Adobe och kundhanterade [Dynatrace](https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/dynatrace), vilket gör den observerbar. När vi utforskar stöd för ytterligare APM-alternativ kan du skicka ett e-postmeddelande till [aemcs-apm-beta@adobe.com](mailto:aemcs-apm-beta@adobe.com) med den leverantör eller teknik du föredrar, tillsammans med användningsexempel.


## [!DNL Experience Manager] stödlinjer {#guides}

Du hittar en fullständig lista över nya och förbättrade funktioner i den senaste utgåvan av Adobe Experience Manager Guides [här](https://experienceleague.adobe.com/sv/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

## Cloud Manager {#cloud-manager}

Du hittar en fullständig lista över månadsutgåvor av Cloud Manager [här](/help/implementing/cloud-manager/release-notes/current.md).

## Migreringsverktyg {#migration-tools}

Du hittar en fullständig lista över migreringsverktygen [här](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).

## Universal Editor {#universal-editor}

Du hittar en fullständig lista över universella redigeringsversioner [här](/help/release-notes/universal-editor/current.md).

## Generera variationer {#generate-variations}

Du hittar en fullständig lista över versioner av Generera variationer [här](/help/generative-ai/release-notes-generate-variations.md).

## Versionsinformation för Experience Cloud {#experience-cloud}

Du hittar information om releaser av andra Experience Cloud-program [här](https://experienceleague.adobe.com/sv/docs/release-notes/experience-cloud/current).

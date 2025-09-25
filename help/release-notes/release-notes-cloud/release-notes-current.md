---
title: Aktuell versionsinformation för  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Versionsinformation för  [!DNL Adobe Experience Manager] as a Cloud Service.
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: bdc0e7623592efed5270a3cb8322ef22e50cbad9
workflow-type: tm+mt
source-wordcount: '2066'
ht-degree: 0%

---

# Aktuell versionsinformation för [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

I följande avsnitt beskrivs versionsinformationen för den aktuella (senaste) versionen av [!DNL Experience Manager] as a Cloud Service.

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

>[!VIDEO](https://video.tv.adobe.com/v/3440924?quality=12&captions=swe)

-->

## [!DNL Experience Manager Sites] som en [!DNL Cloud Service] {#sites}

### Nya funktioner i Experience Manager Sites Prerelease {#prerelease-sites}

Innehållsmodellredigeraren för AEM Content Fragments har moderniserats för att passa ihop med andra React Spectrum-baserade gränssnitt i AEM. Implementeringen av användargränssnittet och utbyggbarhetsmodellen överensstämmer nu med Content Fragment Editor och Universal Editor. Den nya modellredigeraren är nu standard när den öppnas från det nya gränssnittet för innehållsmodelladministratör. Om du öppnar en innehållsmodell i Touch-gränssnittet öppnas Touch UI-redigeraren och den nya redigeraren erbjuds att testa.

## [!DNL Experience Manager Assets] som en [!DNL Cloud Service] {#assets}

### Nya funktioner i vyn Assets {#new-features-assets-view}

**Förbättrad textformatering med delsträngar i dynamiska mediamallar**

Du kan nu använda formatering på delsträngar i textlager i mallen Dynamic Media. Ett markerat ord eller en fras behandlas som ett separat lager så att du kan justera teckensnitt, teckenstorlek, färg med mera. Delsträngslagret parametriseras så att du kan uppdatera det i realtid med mallens leverans-URL

### Nya funktioner i Dynamic Media med OpenAPI-funktioner {#new-features-dynamic-media-with-openapi}

**SEO-vänlig DM med OpenAPI-URL:er**

Skapa Vanity-URL:er för leverans av resurser i DM med OpenAPI och ersätt långa systemgenererade UUID:n med korta, läsbara identifierare. Detta gör länkar till SEO-anpassade och bättre anpassade till ert varumärke eller era kampanjer. Vanity-URL:er löses automatiskt till det ursprungliga resurs-UUID:t vid körning utan att befintliga arbetsflöden avbryts.

>[!NOTE]
>
>Den här funktionen är tillgänglig som en begränsad tillgänglighetsfunktion. Du kan [skapa och skicka ett Adobe kundsupportärende](https://helpx.adobe.com/se/enterprise/using/support-for-experience-cloud.html) för att aktivera det för din distribution.

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

**Indatakomponent för datum och tid**

Det finns nu en [datum- och tidskomponent](https://experienceleague.adobe.com/sv/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/date-time-component) som gör att användare kan välja både datum och tid med hjälp av ett kalender- och klockgränssnitt, eller genom att ange värden manuellt i ett format som stöds.

**Utökad felhantering för filöverföringar**

Komponenten [Bifogad fil](https://experienceleague.adobe.com/sv/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/file-attachment#basic-tab) validerar nu automatiskt den överförda filtypen mot tillåtelselista. Om en användare överför en fil i ett format som inte stöds visas ett fel under överföringen. Komponenten kontrollerar också filinnehållet för att validera dess typ, vilket förbättrar formulärets övergripande säkerhet.

**Angivet felsvar för anpassad överföringsåtgärd**

När en [anpassad skicka-åtgärd](/help/forms/custom-submit-action-troubleshooting.md) påträffar ett ohanterat fel returneras felkoden 502. Detta hjälper till att identifiera att problemet är relaterat till den anpassade skicka-åtgärden, vilket gör felsökningen enklare.

**Utesluter dolda fält från postdokument**

En ny egenskap tillåter att dolda fält utesluts från [postdokumentet](/help/forms/generate-document-of-record-core-components.md#document-of-record-settings). Som standard är det här alternativet inte markerat och gäller för alla formulärfält.


### Pre-Release-funktioner i AEM Forms

**Generera och synkronisera AFP-återgivningar**

Du kan nu använda [AEM Forms Communication API](/help/forms/document-generation-afp-api.md) för att konvertera en XDP-fil till AFP-format. AFP är ett högpresterande format som används ofta vid storskalig trycksaksproduktion.

**Förbättringar i regelredigeraren**

* [Validera metod i funktionslista](/help/forms/rule-editor-enhancements-use-cases.md#validate-method-in-function-list): Metoderna validate och reset har nu stöd för körning på panelnivå, fält- och formulärnivå. Tidigare stöddes de endast på formulärnivå.
* [Modernt JavaScript-stöd](/help/forms/rule-editor-core-components-difference-tables.md): Stöd för ECMAScript 2019 och senare funktioner har lagts till för anpassade funktioner, vilket gör att du kan skriva mer effektiv, modulär och återanvändbar kod.
* [Ladda ned DoR-alternativ i regelredigeraren](/help/forms/rule-editor-enhancements-use-cases.md#downloaddor-as-ootb-fuction-in-rule-editor): En funktion för att hämta dokumentarkivfilen (DoR) har lagts till som ett OTB-alternativ (Out-of-Box) i regelredigeraren.

  ![Dokument-av-post](/help/forms/assets/document-of-record-rn.gif)

* [Dynamiska variabler i Regelredigeraren](/help/forms/rule-editor-enhancements-use-cases.md#support-for-dynamic-variables-in-rules): Du kan nu använda dynamiska (tillfälliga) variabler i Regelredigeraren för större flexibilitet när du definierar villkor och åtgärder. Dolda fält behövs inte längre för att lagra tillfälliga värden.
* [Stöd för anpassade händelsebaserade regler](/help/forms/rule-editor-enhancements-use-cases.md#custom-event-based-rules-support): Du kan nu definiera anpassade händelser och utlösarregler baserat på dessa händelser.
* [Kontextmedvetna upprepningsbara panelregler](/help/forms/rule-editor-enhancements-use-cases.md#context-based-rule-execution-for-repeatable-panels): I upprepningsbara paneler körs nu regler baserat på kontext, i stället för att bara tillämpas på den sista panelinstansen.
* [Regler som utlösts av parametrar](/help/forms/rule-editor-enhancements-use-cases.md#url-and-browser-parameter-based-rules-in-adaptive-forms): Regelredigeraren stöder nu regelkörning baserat på frågeparametrar, UTM-parametrar eller webbläsarparametrar.
* [Formulärspecifika anpassade funktioner](/help/edge/docs/forms/universal-editor/rule-editor-universal-editor.md#organizing-custom-functions-across-different-forms): Edge Delivery Services Forms har nu stöd för formulärspecifika anpassade funktionsskript, vilket ger större flexibilitet vid hantering av återanvändbar logik.
* [Statisk import för anpassade funktioner](/help/edge/docs/forms/universal-editor/rule-editor-universal-editor.md#static-imports-for-custom-functions): Regelredigeraren i Universal Editor har nu stöd för statiska importer, vilket gör att utvecklare kan ordna, dela och återanvända funktioner i flera formulär.

### Nya funktioner för tidig åtkomst i AEM Forms {#forms-new-early-access-features}

AEM Forms Early Access Program ger dig unika möjligheter att få exklusiv tillgång till de senaste innovationerna och hjälpa till att utforma deras utveckling.

I versionsinformationen visas de innovationer som levererats i den aktuella versionen. En fullständig lista över de innovationer som är tillgängliga under Tidig åtkomst-programmet finns i [AEM Forms Tidig åtkomst-programdokumentation](/help/forms/early-access-ea-features.md).

**Klottsignaturkomponent**

Du kan nu använda [Klottsigneringskomponenten](https://experienceleague.adobe.com/sv/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/scribble-signature) för att hjälpa användare att lägga till signaturer i ett formulär, till exempel i ett avtalsformulär. Med komponenten kan användare rita sin signatur direkt i formuläret med en mus, en styluspenna eller en pekskärm.

**Direkt API-integrering i regelredigeraren**

Adaptiv Forms har nu stöd för [direkt API-integrering](/help/forms/api-integration-in-rule-editor.md) i Visual Rule Editor utan någon formulärdatamodell. Författare kan konfigurera API:er med en URL- eller cURL-import, mappa in-/utdataparametrar och säkra anrop med autentisering.

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

Observera, separat från Edge Delivery Services, att tidigare i år har vi släppt en funktion för att konfigurera Open ID Connect [för AEM Cloud-tjänstens publiceringsskiktsprojekt](/help/security/open-id-connect-support-for-aem-as-a-cloud-service-on-publish-tier.md) för att skydda AEM-sidor.

<!--
### CDN Configuration for Edge Delivery Services (Beta Program) {#cdn-eds-beta}

The Adobe-Managed CDN offers flexible configuration options, as described in the [Config Pipeline article](/help/operations/config-pipeline.md#configurations). 

Now in beta, youcan deploy a config pipeline for features including CDN origin selectors, response and request transformations, CDN log forwarding and more. Please reach out to [aemcs-cdn-config-adopter@adobe.com](mailto:aemcs-cdn-config-adopter@adobe.com) with the details of your use case.

-->

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

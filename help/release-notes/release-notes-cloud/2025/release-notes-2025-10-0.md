---
title: Versionsinformation om 2025.10.0-utgåvan av  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Versionsinformation om 2025.10.0-utgåvan av  [!DNL Adobe Experience Manager] as a Cloud Service.
feature: Release Information
role: Admin
source-git-commit: c5918c887be60c5198b762d860fe72afd31df352
workflow-type: tm+mt
source-wordcount: '1894'
ht-degree: 0%

---

# Versionsinformation 2025.10.0 för [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

I följande avsnitt beskrivs versionsinformationen för funktionen för 2025.10.0-versionen av [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Härifrån kan du navigera till versionsinformation för tidigare versioner som 2023 eller 2024.
>
>Ta en titt på [Experience Manager Releases Roadmap](https://experienceleague.adobe.com/sv/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) om du vill veta mer om kommande funktionsaktiveringar för [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Om du vill få ett månatligt e-postmeddelande om uppdateringar av Experience Cloud versionsinformation prenumererar du på [Adobe Priority Product Update](https://www.adobe.com/subscription/priority-product-update.html).

## Releasedatum {#release-date}

Releasedatum för [!DNL Adobe Experience Manager] som [!DNL Cloud Service] aktuell funktionsversion (2025.10.0) är 30 oktober 2025. Nästa funktionsversion (2025.11.0) planeras bli 20 november 2025.

## Versionsinformation om underhåll {#maintenance}

Du hittar den senaste underhållsversionsinformationen [här](/help/release-notes/maintenance/latest.md).

<!-- 

## Release Video {#release-video}

Have a look at the July 2025 Release Overview video for a summary of the features added in the 2025.7.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3440924?captions=swe&quality=12)

-->

## [!DNL Experience Manager Sites] som en [!DNL Cloud Service] {#sites}

### Nya funktioner i Experience Manager Sites {#new-sites}

* [Startar för innehållsfragment](/help/sites-cloud/administering/content-fragments/launches-for-content-fragments.md): Innehållsförfattare kan nu skapa och schemalägga framtida varianter av strukturerat innehåll med hjälp av startfunktioner för innehållsfragment. Med den nya konsolen för innehållsfragment kan du skapa, redigera, hantera och schemalägga Content Fragment som grenar för framtida innehåll som kan synkroniseras med källgrenen. En ny Diff-vy ger en tydlig översikt över alla innehållsändringar innan du implementerar en Launch för framtida publicering.

* [Innehållsmodellredigeraren för AEM-innehållsfragment](/help/sites-cloud/administering/content-fragments/content-fragment-models.md) har moderniserats så att den justeras mot andra React Spectrum-baserade gränssnitt i AEM. Implementeringen av användargränssnittet och utbyggbarhetsmodellen överensstämmer nu med Content Fragment Editor och Universal Editor. Den nya modellredigeraren är nu standard när den öppnas från det nya gränssnittet för innehållsmodelladministratör. Om du öppnar en innehållsmodell i Touch-gränssnittet öppnas Touch UI-redigeraren och den nya redigeraren erbjuds att testa.

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

**Universell redigerare för adaptiva Forms och formulärfragment**

Universalredigeraren ger nu en enhetlig redigeringsfunktion för att skapa adaptiva Forms och återanvändbara formulärfragment. Man kan visuellt utforma blanketter i en intuitiv WYSIWYG-miljö med kraftfulla funktioner för tillägg och inlämning. Redigeraren integrerar reCAPTCHA-validering för förbättrad säkerhet, tillhandahåller förifyllda tjänster för att minska manuell inmatning och stöder responsiv design på alla enheter.

**Tillgängliga tillägg:**

* **Regelredigerare**: Med den visuella regelredigeraren kan formulärförfattare lägga till dynamiskt beteende i formulärfält utan kodning, stöd för händelsestyrda regler, omedelbar validering och felhantering.
* **Formuläregenskaper**: En guide som hjälper användare att konfigurera skicka-åtgärder, förifyllningstjänst, tackmeddelande och andra formulärrelaterade beteenden direkt i redigeraren.
* **Formulärdata Source och bind referens**: Med datakälltillägget kan formulärförfattare lägga till komponenter som är kopplade till en datamodell direkt i ett adaptivt formulär och välja en bindningsreferens från ett trädval för alla komponenter.

**Överföringsåtgärder som stöds:**

Den universella redigeraren har stöd för ett stort antal inskickningsarbetsflöden, inklusive Custom Submit Action, Submit to Microsoft SharePoint, Submit to Microsoft OneDrive, Submit to Azure Blob Storage, Submit to REST endpoint, Invoke an AEM Workflow, Invoke a Power Automate flow, Submit to Marketo Engage (AEP), Submit to Spreadsheet, Submit using using Form Data Model (FDM), Submit to Workfront Fusion och Send Email.

Fullständig information finns i dokumentationen för [Universal Editor för Edge Delivery Services för Forms](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md). Mer information om hur du konfigurerar skicka-åtgärder finns i [Åtgärden Skicka anpassat formulär](/help/edge/docs/forms/universal-editor/submit-action.md).

<!-- ### Pre-Release features in AEM Forms 

**Rule Editor Enhancements**

The Rule Editor now supports enhanced navigation and allows use of function and mathematical expressions in input parameters.

**Enhanced Navigation with Event Payload Support**
 
The `Navigate To` action in the Invoke Service handlers now supports `EVENT_PAYLOAD`, enabling form authors to configure follow-up actions based on event responses. This enhancement offers greater flexibility in designing post-submission workflows, ensuring smoother transitions and more personalized user experiences. For more information, see [Enhanced Navigation with Event Payload Support](/help/forms/invoke-service-enhancements-rule-editor.md#use-case-5-use-event-payload-in-navigate-to-action-in-invoke-service).

**Function and Mathematical Expression Support in Input Parameters**
 
Input parameters now support both function calls and mathematical expressions, enabling form authors to pass dynamically computed values directly. This enhancement streamlines rule configurations, eliminates the need for extra fields, and makes forms more adaptable to complex logic and calculation-driven scenarios. For more information, see [Function and Mathematical Expression Support in Input Parameters](/help/forms/rule-editor-core-components-user-interface.md#function-and-mathematical-expression-support-in-input-parameters). -->

### Nya funktioner för tidig åtkomst i AEM Forms {#forms-new-early-access-features}

AEM Forms Early Access Program ger dig unika möjligheter att få exklusiv tillgång till de senaste innovationerna och hjälpa till att utforma deras utveckling.

I versionsinformationen visas de innovationer som levererats i den aktuella versionen. En fullständig lista över de innovationer som är tillgängliga under Tidig åtkomst-programmet finns i [AEM Forms Tidig åtkomst-programdokumentation](/help/forms/early-access-ea-features.md).

#### Förbättringar av interaktiv kommunikation

##### Låsning av mallar

Lås innehåll och layoutelement i mallar för att bevara varumärkets integritet och förhindra obehöriga ändringar. Detta garanterar en enhetlig design i all kommunikation.

##### Stöd för innehållsspill

Nu finns alternativet&quot;Tillåt sidbrytningar i innehåll&quot; för flödade layouter. Den här förbättringen möjliggör smidig flersidig redigering och bättre texthantering för komplexa dokument.

##### XDP-filredigering

Interactive Communication editor now supports XDP editing, including fragment integration. Nu kan du redigera XDP-filer i en webbläsare i stället för i Forms Designer som endast kan köras i Microsoft Windows.

##### Dynamisk sidnumrering

Visa automatiskt&quot;Sidnummer av ##&quot; på mallsidor för tydlig och konsekvent sidnumrering över flersidiga dokument.

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
>Skicka ett e-postmeddelande till [aemcs-update-free@adobe.com](mailto:aemcs-update-free@adobe.com) om du vill aktivera det i dina program.

### AEM Log Forwarding to More Destinations {#log-forwarding}

Nu går det att vidarebefordra AEM-loggar till Amazon S3, Sumo Logic, Dynatrace och ditt eget New Relic-konto (inte till Adobe-kontot). Observera att AEM-loggar (inklusive Apache/Dispatcher) stöds för dessa loggningsmål, men inte CDN-loggar.

Se hela uppsättningen med [loggvidarebefordringsmål som stöds](/help/implementing/developing/introduction/log-forwarding.md).

### Konfigurera pipeline för Edge Delivery Services {#config-pipeline-eds}

Config Pipelines stöds nu för sajter som byggts med Edge Delivery Services, vilket ger fler möjligheter än bara publicering via AEM Author och AEM. Du kan använda Konfigurera pipelines för att hantera inställningar som CDN-konfiguration, inklusive trafikfilterregler och ursprungsväljare. Se [Konfigurationer som stöds](/help/operations/config-pipeline.md#configurations).

Edge Delivery config pipelines har också stöd för hemligheter via Cloud Manager pipeline-variabler.

Se [Lägg till Edge Delivery-pipeline](/help/implementing/cloud-manager/configuring-pipelines/configuring-edge-delivery-pipeline.md).

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

Adobe uppgraderade miljöerna **Stage** och **Production** till **Java 21-miljön** med högre prestanda den 14 oktober 2025. Från och med slutet av januari fungerar varken AEM Cloud Service SDK eller någon molnmiljö med Java 11 runtime.

>[!NOTE]
>
> För att kunna utnyttja de senaste prestandaoptimeringarna och språkförbättringarna rekommenderar vi att du bygger med Java 17 eller Java 21 (rekommenderas). Det finns fortfarande stöd för att bygga med Java 8 och Java 11, men det kommer att bli inaktuellt i en kommande version. Ett separat meddelande kommer att utfärdas innan den tas bort. Se avsnittet *Krav för byggtid* i [den här artikeln](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements).
>

### Tillämpning av konfigurationspolicy för AEM Java-loggar {#logconfig-policy}

Som framgår av versionsinformationen för april måste AEM Java-loggarna följa ett standardformat för att säkerställa tillförlitlig övervakning i alla kundmiljöer. Anpassade loggkonfigurationer, t.ex. ändringar i loggformatering, utdatafiler eller standardloggnivåer, stöds inte längre. Loggar måste vara dirigerade till standardfilerna och standardloggnivåerna för AEM-produktkoden måste bevaras. Mer information finns i artikeln [Loggning](/help/implementing/developing/introduction/logging.md#configuration-loggers).

Med början den **20 november** kommer alla anpassade loggningsåsidosättningar som inte stöds att ignoreras. Baserat på vår analys kommer de flesta kunder inte att påverkas och Adobe har kontaktat kunder vars nuvarande konfiguration kan påverkas.

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


### AI-svar - Smartare, sammanhangsberoende svar för AEM Sites (Beta-programmet) {#ai-answers-beta}

AI-svar introducerar ett nytt sätt för era besökare att interagera med ert innehåll. Den bygger på teknik från Retrieval-Augmented Generation (RAG) och använder data som hanteras av AEM för att leverera korrekta, varumärkeskonsekventa svar direkt i era digitala upplevelser.

Vi förbereder oss för att lansera Beta-programmet för AI-svar och bjuder nu in kunderna att registrera sina intressen. Eftersom betaversionen har mycket begränsad kapacitet kommer tidiga registreringar att få prioritet. Genom att delta i betaversionen kan du utforska AI-svar i AEM Cloud-tjänstmiljön, validera prestanda och precision och hjälpa till att utforma den framtida upplevelsen innan den blir allmänt tillgänglig.

Kontakta [feedback-ai-answers@adobe.com](mailto:feedback-ai-answers@adobe.com) om du vill begära deltagande eller få uppdateringar.


### Ögonblicksbilder för RDE (Alpha Program) {#rde-snapshot-program}

I alfa har Rapid Development Environment (RDE) nu stöd för en funktion som tar en ögonblicksbild av det aktuella kodläget och innehållet, som kan återställas vid ett senare tillfälle. Detta kan vara användbart när du synkroniserar kod som behöver återställas eller när du växlar mellan utveckling av olika funktioner. Det går också att återställa bara det ändringsbara innehållet som en känd startpunkt för testning.

Skicka ett e-postmeddelande till [aemcs-rde-support@adobe.com](mailto:aemcs-rde-support@adobe.com) om du är intresserad av att lämna feedback om funktionen.

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

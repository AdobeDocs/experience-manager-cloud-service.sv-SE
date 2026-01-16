---
title: Aktuell versionsinformation för  [!DNL Adobe Experience Manager] as a Cloud Service
description: Versionsinformation för  [!DNL Adobe Experience Manager] as a Cloud Service.
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: a1b860b4d691515f7f868e4e7e1a70bac0c20cbe
workflow-type: tm+mt
source-wordcount: '1944'
ht-degree: 0%

---

# Aktuell versionsinformation för [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

I följande avsnitt beskrivs versionsinformationen för den aktuella (senaste) versionen av [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Härifrån kan du navigera till versionsinformation för tidigare versioner som 2023 eller 2024.
>
>Ta en titt på [Experience Manager Releases Roadmap](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) om du vill veta mer om kommande funktionsaktiveringar för [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Om du vill få ett månatligt e-postmeddelande om uppdateringar av Experience Cloud versionsinformation prenumererar du på [Adobe Priority Product Update](https://www.adobe.com/subscription/priority-product-update.html).

## Releasedatum {#release-date}

Releasedatum för [!DNL Adobe Experience Manager] som [!DNL Cloud Service] aktuell funktionsversion (2025.12.0) är 11 december 2025. Nästa funktionsversion (2026.1.0) är planerad till 29 januari 2026.

## Versionsinformation om underhåll {#maintenance}

Du hittar den senaste underhållsversionsinformationen [här](/help/release-notes/maintenance/latest.md).

<!-- 

## Release Video {#release-video}

Have a look at the July 2025 Release Overview video for a summary of the features added in the 2025.7.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3440920?quality=12)

-->

## AEM Beta-program {#aem-beta-programs}

Adobe Experience Manager (AEM) betaprogram är ett sätt för kunderna att få tillgång till betaversionsfunktioner och -kod, ge feedback och vägleda framtiden för AEM.

>[!IMPORTANT]
>
>Beta-releaser kan innehålla defekter och tillhandahålls i befintligt skick utan någon garanti av något slag. Adobe har ingen skyldighet att upprätthålla, korrigera, uppdatera, ändra, modifiera eller på annat sätt ge support (via Adobe Support Services eller på annat sätt) för betaversioner. Adobe rekommenderar sina kunder att iaktta försiktighet och inte förlita sig på att betaversioner fungerar eller fungerar som de ska, eller på medföljande dokumentation eller material. Funktioner och API:er i betaversionen kan ändras utan föregående meddelande. Därför är all användning av betaversioner helt och hållet på kundens egen risk.

**Fördelar med att delta**
Genom att få tidig tillgång till funktioner som Adobe utvecklar kan kunder och partners ge feedback och utforma produktutvecklingen. Det hjälper dem också att förbereda sig för att införa nya funktioner före allmän tillgänglighet.

**Aktuella betaprogram**
I följande avsnitt visas aktiva betaprogram.

### Agenter i AEM (Beta-programmet) {#agents-in-aem-beta-program}

Få snabb tillgång till kraftfulla nya AEM-funktioner för produktion, styrning, optimering, upptäckt och utveckling. Din feedback är direkt till form för Adobe färdplan och slutfunktioner. Mer information finns i [Översikt över agenter i AEM](/help/ai-in-aem/agents/overview.md).

Programmet varar normalt 4-6 veckor, men kan anpassas så att det är flexibelt att du aktivt kan delta.

Om du vill anmäla dig till att delta i det här programmet skickar du ett e-postmeddelande till [aemagentsteam@adobe.com](mailto:aemagentsteam@adobe.com) med följande information så långt det är möjligt:

* Namn och Adobe ID på gruppmedlemmar som aktivt kommer att använda agenter.
* Visa en lista över specifika agenter som du eller ditt team vill använda. Eller säg bara &quot;Alla agenter&quot;.

### AEM Foundation (Beta-program) {#aem-foundation-beta-programs}

Se [betaprogram för AEM Foundation](#foundation-early-adopter).

### Cloud Manager (Beta-program) {#cloud-manager-beta-programs}

Se [Cloud Manager betaprogram](/help/implementing/cloud-manager/release-notes/current.md).


## [!DNL Experience Manager Assets] som en [!DNL Cloud Service] {#assets}

**Det finns en ny version av Figma Plugin för integrering med AEM Assets**

* Stöd för videofiler (MP4, MOV, WebM), animerade filer (GIF) och vektorfiler (SVG) när du importerar resurser från AEM-databasen till Figma-dokumentet.

* Stöd för att kontrollera om det finns några uppdateringar av resurserna som används i Figma-dokument jämfört med resurserna som finns i AEM-databasen och hämta den senaste versionen av resurserna om det finns några uppdateringar.

* Stöd för exportkonfigurationer vid export av PNG- (scale) och JPG-filformat (bildskala och kvalitet).

  ![Figma plugin](/help/assets/assets/figma-v2-plugin.png)

**Identifiering av skadlig kod för överförda resurser**

AEM Assets innehåller nu automatisk skanning av skadlig kod av överförda filer, vilket säkerställer att misstänkta tillgångar sätts i karantän innan de går in i DAM för att skydda databasen mot hot. Administratörer kan konfigurera skanningsinställningar och karantänkvarhållningsprinciper för smidiga säkerhetskontroller.

**AI-genererade metadata - behörighetsuppdatering**

AI-genererade metadata i AEM Assets kräver inte längre att GenAI Rider signeras för att aktiveras. Funktionen är nu tillgänglig för både kunder som har signerat GenAI Rider och kunder som ännu inte har validerats. Funktionen kommer även fortsättningsvis att vara inaktiverad för kunder som uttryckligen har valt att inte använda GenAI. Mer information om hur du hanterar funktionsaktiveringen på miljönivå finns i [Inaktivera AI-genererade metadata](/help/assets/enhance-content-discovery-with-ai-generated-metadata.md#disable-ai-generated-metadata). Den här ändringen görs för kunder i version 23482 eller senare.


## [!DNL Experience Manager Forms] som en [!DNL Cloud Service] {#forms}

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

### [!DNL Experience Manager] som [!DNL Cloud Service] Foundation New Features {#foundation-new}

#### Kommande Java API-borttagningar {#java-api-deprecation}

Flera inaktuella API:er markerades för borttagning den 31 augusti och bör därför inte längre refereras. Du får meddelanden från Åtgärdscenter om inaktuell API-användning upptäcks i koden, och efter den 29 januari visas meddelanden under Cloud Manager-byggen för att förstärka vikten av att ta bort användningen. Mer information finns i artikeln [som inte längre används](/help/release-notes/deprecated-removed-features.md#aem-apis), men dessa API:er finns i listan nedan för att underlätta:

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

#### Java 11 Runtime Deprecation {#java11-runtime-deprecation}

Adobe uppgraderade miljöerna **Stage** och **Production** till **Java 21-miljön** med högre prestanda den 14 oktober 2025. Från och med **9 februari** fungerar varken AEM Cloud-tjänsten SDK eller någon molnmiljö med Java 11-miljön.

>[!NOTE]
>
> För att kunna utnyttja de senaste prestandaoptimeringarna och språkförbättringarna rekommenderar vi att du bygger med Java 17 eller Java 21 (rekommenderas). Det finns fortfarande stöd för att bygga med Java 8 och Java 11, men det kommer att bli inaktuellt i en kommande version. Ett separat meddelande kommer att utfärdas innan den tas bort. Se avsnittet *Krav för byggtid* i [den här artikeln](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements).
>

#### Tillämpning av konfigurationspolicy för AEM Java-loggar {#logconfig-policy}

Som framgår av versionsinformationen för april måste AEM Java-loggarna följa ett standardformat för att säkerställa tillförlitlig övervakning i alla kundmiljöer. Anpassade loggkonfigurationer, t.ex. ändringar i loggformatering, utdatafiler eller standardloggnivåer, stöds inte längre. Loggar måste vara dirigerade till standardfilerna och standardloggnivåerna för AEM-produktkoden måste bevaras. Mer information finns i artikeln [Loggning](/help/implementing/developing/introduction/logging.md#configuration-loggers).

Med början den **29 januari** kommer alla anpassade loggningsåsidosättningar som inte stöds att ignoreras. Baserat på vår analys kommer de flesta kunder inte att påverkas och Adobe har kontaktat kunder vars nuvarande konfiguration kan påverkas.

Granska och uppdatera alla processer som är beroende av anpassat loggningsbeteende. Till exempel:

* Om ditt system för vidarebefordring av loggar förväntar sig ett anpassat loggformat kan du behöva justera dina regler för inmatning.
* Om du tidigare har minskat loggens utförlighet genom att ändra loggnivåerna bör du tänka på att en återställning till standardnivåerna kan öka loggvolymen.

### [!DNL Experience Manager] som en [!DNL Cloud Service] Foundation Tidiga Adobe-funktioner {#foundation-early-adopter}

#### Pausa automatiska underhållsuppdateringar {#pause-updates}

Dagar live, live event, toppförsäljning - dessa stunder kan inte brytas. [Våra nya självbetjäningsfunktioner](/help/implementing/deploying/quiet-hours-update-free-periods.md) avbryter automatiskt underhåll av uppdateringar när det behövs, så att era team kan fokusera.

* Tysta timmar: Blockera automatiskt underhåll under fasta tider varje dag. Idealiskt för arbetstider, nattkörningar eller morgonavslutningar.
* Uppdateringsfri period: Blockera automatiskt underhåll under en hel vecka. Använd den för lanseringar, kampanjer eller årsfrysningar.

>[!NOTE]
>
>Tillgänglig som begränsad tillgänglighet den 25 september.
>Skicka ett e-postmeddelande till [aemcs-update-free@adobe.com](mailto:aemcs-update-free@adobe.com) om du vill aktivera det i dina program.
>

#### Edge Computing (Beta Program)

Med Edge kan du köra JavaScript på CDN-lagret, vilket tar databearbetningen närmare slutanvändaren. Detta minskar latensen och möjliggör responsiva, dynamiska upplevelser i framkanten.

Exempel på vanliga användningsområden:

* Anpassa innehåll baserat på geografisk placering, enhetstyp eller användarattribut
* Fungerar som mellanvara mellan CDN och ditt ursprung
* Formatera om svar från tredjeparts-API:er (och kanske samla in flera API-svar) innan de skickas till webbläsaren
* Skapa och leverera serveråtergivna HTML i toppklass med material som sammanfogats från olika bakgrunder
* Exponera en MCP-server för LLM-program som ChatGPT och Claude för att få tillgång till anpassade verktyg

Vi har ett begränsat antal möjligheter, antingen för AEM Publish Delivery eller för Edge Delivery Services-projekt, för produktionssajter. Om du är intresserad av att delta eller vill veta mer kan du skicka ett e-postmeddelande till [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) med en kort beskrivning av ditt användningsfall.

#### Edge-autentisering för Edge Delivery Services (Beta-programmet) {#edge-authentication}

Med Edge Authentication kan du begränsa åtkomsten till Edge Delivery Services-sidor till endast de som har autentiserats hos din identitetsleverantör (IdP). Detta uppnås genom att distribuera en YAML-fil med OpenID Connect-konfiguration (OIDC).

Om du är intresserad kan du skicka ett e-postmeddelande till [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) med en kort beskrivning av ditt användningsfall och eventuella frågor du har.

#### Kanarieproduktionsdistributioner till testkod innan Live-trafik godkänns (Beta-programmet) {#canary-beta}

Validera en produktionsbygge med intern testtrafik innan den visas för slutanvändarna. Leverera till produktion, dirigera endast kanarietrafik (med en särskild rubrik), övervaka beteendet och sedan antingen marknadsföra till livstrafik eller backa - utan att det påverkar kunderna.

Distribuera era kodreleaser till produktion, men begränsa den till enbart intern testtrafik innan du bestämmer dig för att acceptera direkttrafik eller återställa.

Skicka e-post till [aemcs-canary-deployments-beta@adobe.com](mailto:aemcs-canary-deployments-beta@adobe.com) för att begära åtkomst och dela feedback.


#### AI-svar - Smartare, sammanhangsberoende svar för AEM Sites (Beta-programmet) {#ai-answers-beta}

AI-svar introducerar ett nytt sätt för era besökare att interagera med ert innehåll. Den bygger på teknik från Retrieval-Augmented Generation (RAG) och använder data som hanteras av AEM för att leverera korrekta, varumärkeskonsekventa svar direkt i era digitala upplevelser.

Vi förbereder oss för att lansera Beta-programmet för AI-svar och bjuder nu in kunderna att registrera sina intressen. Eftersom betaversionen har mycket begränsad kapacitet kommer tidiga registreringar att få prioritet. Genom att delta i betaversionen kan du utforska AI-svar i AEM Cloud-tjänstmiljön, validera prestanda och precision och hjälpa till att utforma den framtida upplevelsen innan den blir allmänt tillgänglig.

Kontakta [feedback-ai-answers@adobe.com](mailto:feedback-ai-answers@adobe.com) om du vill begära deltagande eller få uppdateringar.

#### Ögonblicksbilder för RDE (Beta Program) {#rde-snapshot-program}

I betaversionen stöder nu Rapid Development Environment (RDE) en funktion som tar en ögonblicksbild av det aktuella läget för kod och innehåll, som kan återställas vid ett senare tillfälle. Detta kan vara användbart när du synkroniserar kod som behöver återställas eller när du växlar mellan utveckling av olika funktioner. Det går också att återställa bara det ändringsbara innehållet som en känd startpunkt för testning.

Skicka ett e-postmeddelande till [aemcs-rde-support@adobe.com](mailto:aemcs-rde-support@adobe.com) om du är intresserad av att använda och ge feedback på den här funktionen.

#### Snabba upp AEM-utvecklingen med AI (Alpha-programmet) {#ai-dev-alpha}

AEM Java-stackteam använder i allt större utsträckning AI-assisterad utveckling i verktyg som Cursor, Claude Code, Visual Studio och IntelliJ för att snabba upp leverans av funktioner och förbättra kodkvaliteten. Vi samlar verkliga upplevelser som hjälper till att utforma framtida AI-funktioner som stöds av Adobe.

Dela vad som fungerar för ditt team - och vad du vill att Adobe ska tillhandahålla - genom att skicka ett e-postmeddelande till [aemcs-java-adopter@adobe.com](mailto:aemcs-java-adopter@adobe.com).

#### Utökad APM (Application Performance Monitoring) (Alpha-program) {#apm-alpha}

AEM Cloud-tjänsten har för närvarande stöd för [New Relic One](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/user-access-new-relic) som tillhandahålls av Adobe och kundhanterade [Dynatrace](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/dynatrace), vilket gör den observerbar. När vi utforskar stöd för ytterligare APM-alternativ kan du skicka ett e-postmeddelande till [aemcs-apm-beta@adobe.com](mailto:aemcs-apm-beta@adobe.com) med den leverantör eller teknik du föredrar, tillsammans med användningsexempel.

## [!DNL Experience Manager] stödlinjer {#guides}

Du hittar en fullständig lista över nya och förbättrade funktioner i den senaste utgåvan av Adobe Experience Manager Guides [här](https://experienceleague.adobe.com/en/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

## Cloud Manager {#cloud-manager}

Du hittar en fullständig lista över månadsutgåvor av Cloud Manager [här](/help/implementing/cloud-manager/release-notes/current.md).

## Migreringsverktyg {#migration-tools}

Du hittar en fullständig lista över migreringsverktygen [här](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).

## Universal Editor {#universal-editor}

Du hittar en fullständig lista över universella redigeringsversioner [här](/help/release-notes/universal-editor/current.md).

## Generera variationer {#generate-variations}

Du hittar en fullständig lista över versioner av Generera variationer [här](/help/generative-ai/release-notes-generate-variations.md).

## Versionsinformation för Experience Cloud {#experience-cloud}

Du hittar information om releaser av andra Experience Cloud-program [här](https://experienceleague.adobe.com/en/docs/release-notes/experience-cloud/current).

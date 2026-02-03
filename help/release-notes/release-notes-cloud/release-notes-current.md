---
title: Aktuell versionsinformation för  [!DNL Adobe Experience Manager] as a Cloud Service
description: Versionsinformation för  [!DNL Adobe Experience Manager] as a Cloud Service.
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: 1c5cbed1ea9e8beda14ed3c66f14a446941cd9cf
workflow-type: tm+mt
source-wordcount: '2011'
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

Releasedatum för [!DNL Adobe Experience Manager] som [!DNL Cloud Service] aktuell funktionsversion (2026.1.0) är 29 januari 2026. Nästa funktionsversion (2026.2.0) är planerad till den 26 februari 2026.

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
I följande avsnitt visas aktiva beta- och Utforskarprogram.

### Agenter i AEM (Utforskarprogrammet) {#agents-in-aem-beta-program}

Få snabb tillgång till kraftfulla nya AEM-funktioner för produktion, styrning, optimering, upptäckt och utveckling. Din feedback är direkt till form för Adobe färdplan och slutfunktioner. Mer information finns i [Översikt över agenter i AEM](/help/ai-in-aem/agents/overview.md).

Programmet varar normalt 4-6 veckor, men kan anpassas så att det är flexibelt att du aktivt kan delta.

Om du vill anmäla dig till att delta i det här programmet skickar du ett e-postmeddelande till [aemagentsteam@adobe.com](mailto:aemagentsteam@adobe.com) med följande information så långt det är möjligt:

* Namn och Adobe ID på gruppmedlemmar som aktivt kommer att använda agenter.
* Visa en lista över specifika agenter som du eller ditt team vill använda. Eller säg bara &quot;Alla agenter&quot;.

Kunder som valts ut att delta meddelas direkt av Adobe. Deltagandet är beroende av vad som gäller, inklusive kundlicenser och begränsad programkapacitet. Även om inte alla förfrågningar till att börja med kan hanteras, kan ytterligare kunder övervägas i framtida betaversioner.

### AEM Foundation (Beta-program) {#aem-foundation-beta-programs}

Se [betaprogram för AEM Foundation](#foundation-early-adopter).

### Cloud Manager (Beta-program) {#cloud-manager-beta-programs}

Se [Cloud Manager betaprogram](/help/implementing/cloud-manager/release-notes/current.md).

## [!DNL Experience Manager Sites] som en [!DNL Cloud Service] {#sites}

### Content MCP Server {#content-MCP}

AEM Cloud-tjänsten innehåller nu **Content MCP-servrar**, som är ett standardiserat sätt för AI-baserade upplevelser att arbeta med AEM-innehåll via MCP-kompatibla verktyg.

Utvecklare och avancerade användare som arbetar med chattappar och agentplattformar kan koppla AEM till anpassade kopior och automatiseringar, så att innehållsarbetet blir en del av kompletta arbetsflöden.

AEM har två servrar:

1. **Skrivskyddad innehålls-MCP-server** - för säker hämtning av innehåll
1. **MCP-servern för läs/skriv innehåll** - för att göra ändringar i innehållet

Dessa MCP-servrar innehåller verktyg för att arbeta med **sidor**, **innehållsfragment** och **Assets** och kan användas från följande MCP-klienter: **ChatGPT**, **Claude**, **Cursor** och **Microsoft Copilot Studio** .

Läs mer i [Använda MCP med AEM Cloud-tjänsten](/help/ai-in-aem/mcp-support/using-mcp-with-aem-as-a-cloud-service.md). Om du har frågor eller vill ha feedback skickar du ett e-postmeddelande till [aemcs-mcp-feedback@adobe.com](mailto:aemcs-mcp-feedback@adobe.com).

## [!DNL Experience Manager Assets] som en [!DNL Cloud Service] {#assets}

**AI-sökning**

Med AI Search introduceras en smart, sammanhangsberoende sökfunktion som går utöver traditionell nyckelordsmatchning genom att förstå innebörden och avsikten bakom användarfrågor. Med AI och maskininlärning får man exaktare resultat även när frågorna formuleras på olika sätt, innehåller felstavningar, använder synonymer eller skickas in på olika språk, vilket gör att man snabbare kan hitta relevant innehåll.

Mer information finns i AI-sökning i [Assets-vyn](/help/assets/search-assets-view.md#ai-search) och [administratörsvyn](/help/assets/search-assets.md#ai-search).

**Desktop App 3.0.1, version**

[Skrivbordsapp 3.0.1 (20 december 2025)](https://experienceleague.adobe.com/sv/docs/experience-manager-desktop-app/using/release-notes) förbättrar tillförlitlighet, prestanda och stabilitet i viktiga arbetsflöden. Den här versionen ger konsekvent namngivning av mappar genom att åtgärda synkroniseringsproblem med AEM Author, tillåter oavbruten användning av appen vid aktiva överföringar, förbättrar användargränssnittets svarstider genom asynkron bearbetning, optimerar stora filöverföringar med sidnumrering och löser stabilitetsproblem som Author server startar om och kraschar vid stora mappöverföringar och nedladdningar.

**Adobe Asset Link CEP 2026.01.0**

[Adobe Asset Link CEP 2026.01.0](https://helpx.adobe.com/se/enterprise/using/adobe-asset-link.html) introducerar ett nytt alternativ för länkar om saknade länkar i InDesign som automatiskt länkar om andra saknade resurser från samma AEM-mapp. Funktionen matchar resurser baserat på filnamn, vilket avsevärt minskar den manuella ansträngningen vid återställning av brutna länkar.


## [!DNL Experience Manager Forms] som en [!DNL Cloud Service] {#forms}

**Förbättringar av fotnotsplatshållaren i Adaptiv Forms (Foundation Components)**

* [Stöd för flera rader har lagts till med radbrytningar](/help/forms/footnotes-richtextsupport.md), vilket ger tydligare och mer uttrycksfull presentation av fotnotsinnehåll.
* Fotnoter är nu fortfarande synliga i fotnotsplatshållaren, oavsett vilka paneler som är kopplade till dem, vilket ger enhetlig åtkomst till viktig information.
  ![Fotnotsbeskrivning](/help/forms/assets/footnote-description.png){height=50%}

### Nya funktioner för tidig åtkomst i AEM Forms {#forms-new-early-access-features}

**Hämta värden från en JSON-array**

Utökade anpassade funktioner för att [extrahera värden från JSON-arrayer](/help/forms/invoke-service-enhancements-rule-editor.md#retrieve-property-values-from-a-json-array), ta emot via ett API-anrop och binda dem direkt till adaptiva formulärfält. Nu kan ni utveckla affärslogik och regler med minimal manuell datamappning.

**Kör det associerade användargränssnittet på en publiceringsinstans**

Nu kan du köra [Associate UI](/help/forms/interactive-communication/associate-ui-in-interactive-communication-editor.md) direkt på publiceringsinstanser. Detta gör att era agenter kan komma åt det tillhörande användargränssnittet och enkelt anpassa kommunikationen för era kunder.

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

### [!DNL Experience Manager] som [!DNL Cloud Service] Foundation Viktigt Notices {#foundation-notices}

#### Java API-borttagningar {#java-api-deprecation}

De borttagna API:erna med mål 2/26/2026 ska inte längre användas i koden. Om du vill förhindra distributionsblock tar du bort API-användning före 26 mars 2026. Viktiga datum:

* **Från och med 26 januari 2026**: Meddelanden från Åtgärdscenter skickas **veckovis per miljö** som en påminnelse om att ta bort användningen av dessa API:er.
* **26 februari 2026**: Cloud Manager-pipelines som innehåller kod som använder dessa API:er **pausas** under **kodkvalitet** -steget. Distributionshanteraren, projektledaren eller affärsägaren kan åsidosätta problemet så att pipeline kan fortsätta.
* **26 mars 2026**: Cloud Manager-pipelines som innehåller kod som använder dessa API:er **misslyckas** under **Kodkvalitet** -steget, **blockerar distributioner** av ny kod tills användningen har tagits bort.
* **30 april 2026**: Miljöer som fortfarande använder dessa API:er kan **inte längre få viktiga uppdateringar för Adobe-utgåvor**.

Mer information finns i artikeln [som inte längre används](/help/release-notes/deprecated-removed-features.md#aem-apis), men dessa API:er finns i listan nedan för att underlätta:

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

Adobe uppgraderade miljöerna **Stage** och **Production** till **Java 21-miljön** med högre prestanda den 14 oktober 2025. Från och med **9 februari** (gradvis utrullning till och med 11 februari) fungerar varken AEM Cloud-tjänsten SDK eller någon molnmiljö med Java 11 runtime.

>[!NOTE]
>
> För att kunna utnyttja de senaste prestandaoptimeringarna och språkförbättringarna rekommenderar vi att du bygger med Java 17 eller Java 21 (rekommenderas). Det finns fortfarande stöd för att bygga med Java 8 och Java 11, men det kommer att bli inaktuellt i en kommande version. Ett separat meddelande kommer att utfärdas innan den tas bort. Se avsnittet *Krav för byggtid* i [den här artikeln](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements).
>

#### Tillämpning av konfigurationspolicy för AEM Java-loggar {#logconfig-policy}

AEM Java-loggar måste följa ett standardformat för att säkerställa tillförlitlig övervakning i alla kundmiljöer. Anpassade loggkonfigurationer, t.ex. ändringar i loggformatering, utdatafiler eller standardloggnivåer, stöds inte längre. Loggar måste vara dirigerade till standardfilerna och standardloggnivåerna för AEM-produktkoden måste bevaras. Mer information finns i artikeln [Loggning](/help/implementing/developing/introduction/logging.md#configuration-loggers).

Alla anpassade loggningsåsidosättningar som inte stöds *ignoreras nu*. De flesta kunder påverkades inte och Adobe har kontaktat kunder vars aktuella konfiguration kan påverkas.

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

#### Funktioner i AEM Edge (Beta) {#edge-functions}

Med funktionerna i AEM Edge (som i tidigare versionsinformation kallades *Edge Computing*) kan du köra JavaScript i CDN-lagret, vilket tar databearbetningen närmare slutanvändaren. Detta minskar latensen och möjliggör responsiva, dynamiska upplevelser i framkanten.

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

#### Ögonblicksbilder för RDE (Beta Program) {#rde-snapshot-program}

I betaversionen stöder nu Rapid Development Environment (RDE) en funktion som tar en ögonblicksbild av det aktuella läget för kod och innehåll, som kan återställas vid ett senare tillfälle. Detta kan vara användbart när du synkroniserar kod som behöver återställas eller när du växlar mellan utveckling av olika funktioner. Det går också att återställa bara det ändringsbara innehållet som en känd startpunkt för testning.

Skicka ett e-postmeddelande till [aemcs-rde-support@adobe.com](mailto:aemcs-rde-support@adobe.com) om du är intresserad av att använda och ge feedback om den här funktionen.

#### AI-verktyg för IDE för AEM Java och Dispatcher Development (Beta Program) {#ai-dev-beta}

Java-stackteam använder i allt större utsträckning AI-assisterad utveckling i verktyg som Cursor, Claude Code, Visual Studio och IntelliJ för att snabba upp leverans av funktioner och förbättra kodkvaliteten. Gå med i betaversionen:

* Dela verkliga upplevelser för att utforma framtida AI-funktioner som stöds av Adobe
* Prova IDE-verktyg som kan användas av AI-agenter för att generera och felsöka AEM-kod och dispatcherkonfiguration

Mejla [aemcs-java-adopter@adobe.com](mailto:aemcs-java-adopter@adobe.com) för mer information.

#### Utökad APM (Application Performance Monitoring) (Alpha-program) {#apm-alpha}

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

---
title: Aktuell versionsinformation för  [!DNL Adobe Experience Manager] as a Cloud Service
description: Versionsinformation för  [!DNL Adobe Experience Manager] as a Cloud Service.
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: 0c2d61f05d8a6adea1116406b18aa1245ff701d1
workflow-type: tm+mt
source-wordcount: '2156'
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

Releasedatum för [!DNL Adobe Experience Manager] som [!DNL Cloud Service] aktuell funktionsversion (2026.3.0) är 26 mars 2026. Nästa funktionsversion (2026.4.0) är planerad till 30 april 2026.

## Versionsinformation om underhåll {#maintenance}

Du hittar den senaste underhållsversionsinformationen [här](/help/release-notes/maintenance/latest.md).

<!--  ## Release Video {#release-video}

Have a look at the March 2026 Release Overview video for a summary of the features added in the 2026.3.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3480403/?captions=swe&quality=12)

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

### Agenter i AEM {#agents-in-aem}

Om du vill utforska de nya kraftfulla AEM-funktionerna för produktion, styrning, optimering, identifiering och utveckling kan du [läsa mer om hur du kommer åt dem här.](/help/ai-in-aem/agents/overview.md)

<!--
### Agents in AEM (Explorer program) {#agents-in-aem-beta-program}

Gain early access to powerful, new AEM agentic capabilities across production, governance, optimization, discovery, and development. Your feedback directly shapes Adobe's roadmap and final features. See [Overview of Agents in AEM](/help/ai-in-aem/agents/overview.md) to learn more.

This program typically lasts 4-6 weeks, but can be tailored to be flexible around your ability to actively participate. 

To opt in to participate in this program, email [aemagentsteam@adobe.com](mailto:aemagentsteam@adobe.com) and include the following details to the extent possible:

* Names and Adobe ID's of team members who will actively use agents.
* List Specific agents that you or your team will want to use. Or simply say "All Agents."

Customers selected for participation will be notified directly by Adobe. Participation is subject to eligibility considerations, including customer licensing and limited program capacity. While not all requests can be accommodated initially, additional customers may be considered in future beta waves.
-->

### AEM Foundation (Beta-program) {#aem-foundation-beta-programs}

Se [betaprogram för AEM Foundation](#foundation-early-adopter).

### Cloud Manager (Beta-program) {#cloud-manager-beta-programs}

Se [Cloud Manager betaprogram](/help/implementing/cloud-manager/release-notes/current.md).

## [!DNL Experience Manager Sites] som en [!DNL Cloud Service] {#sites}

### Checka ut/in för innehållsfragment {#cf-checkout-in}

För att förbättra pariteten med AEM Touch-gränssnittet kan innehållsfragment nu checkas ut och checkas in igen med det nya gränssnittet för administration av innehållsfragment. Utcheckningsfunktionen är oförändrad och låser effektivt ett utcheckat innehållsfragment och förhindrar därmed att det redigeras av andra användare i Content Fragment Editor. Användare som äger ett innehållsfragment och administratörer kan checka ut och in fragmentet igen. Att checka ut ett fragment har ingen effekt på refererade underordnade fragment eller resurser.

### Panelen Innehållsfragment startar jobb {#cf-launches-jobs}

Asynkrona jobb för att starta innehållsfragment kan nu visas på egenskapspanelen för innehållsfragmentet när administratörsgränssnittet startas för att kontrollera status - om ett jobb fortfarande körs, har slutförts eller avbrutits, tillsammans med relevant detaljinformation om jobbet.

### Uppdatera till textredigeraren för innehållsfragmentredigeraren {#cf-rte-update}

RTF-redigeraren i Content Fragment Editor har flyttats från TinyMCE till TipTap. Den här förändringen medför ett antal fördelar.

* Nu använder den universella redigeraren och Content Fragment Editor samma RTE-teknologi.
   * Det innebär att båda redigerarna nu producerar samma HTML.
   * Tillägg kan nu återanvändas.
   * Samma funktioner och metoder är nu tillgängliga med båda redigeringsprogrammen (i headless-fall).
   * Det yttersta målet är att en konfiguration leder till en enhetlig upplevelse i båda redigeringsprogrammen.
* Innehållsredigeraren har nu ett nytt utseende och en ny känsla i Spectrum 2-stilen.
* Det finns nya funktioner i Content Fragment Editor, bland annat för att söka och ersätta och för att vara innehållsrådgivare.

## [!DNL Experience Manager Assets] som en [!DNL Cloud Service] {#assets}

**Innehållsrådgivare i AEM Sites**

Content Advisor är nu tillgängligt i AEM Sites och introducerar intelligent resursidentifiering från AEM Assets direkt. Det gör det möjligt för användare att enkelt upptäcka, söka efter och återanvända de mest relevanta resurserna direkt i arbetsflödet, vilket eliminerar behovet av att växla mellan olika sammanhang.

Content Advisor tillhandahåller intelligenta funktioner för resurser som kampanjkortsbaserade förslag, sammanhangsbaserade förslag, tillgång till dynamiska medierenderingar och detaljerade metadata för resurser.

Kommer snart - stöd för Content Advisor i Adobe Workfront- och AJO B2C-program, inklusive möjlighet att upptäcka innehållsfragment

### Nya funktioner i Dynamic Media {#dynamic-media-new-features}

#### Uppdateringar för Dynamic Media Template Editor {#dynamic-media-template-editor-updates}

**Lagerhanteringsförbättringar**

* Dra-och-släpp-ändring av lagerordning: Nu kan du ändra ordning på lager direkt på panelen Lager genom att dra, vilket ger ett snabbare och mer intuitivt sätt att ordna lagerstaplingsordningen utöver de befintliga åtgärderna Lägg över eller Lägg under.
* Kopiera, Klistra in och duplicera: Fullt stöd för kopiering, inklistring och duplicering av lager med kortkommandon (Cmd/Ctrl+C, V, D) eller snabbmenyn, med stöd för markeringar med flera lager.
* Knappen Separata lageregenskaper: Knappen Lageregenskaper har lagts till för enklare navigering till lageregenskaper, med stöd för dubbelklick på lager för snabb åtkomst.

**Textformateringsfunktioner**

* Kontroll av radavstånd: Nytt reglage för radavstånd ger exakt kontroll över radhöjden i textlager, med stöd för ångra/gör om i hela stycket samt för att spara/läsa in i mallar.
* Formatering av versaler: Textlager har nu stöd för formateringsalternativet Versaler i verktygsfältet Teckensnittsformat tillsammans med Fet, Kursiv och Understruken.
* Lodräta justeringsalternativ: Lagt till lodräta justeringskontroller för textlager, vilket ger mer exakt textplacering i textrutor.

**Storlek och Dimension-kontroller**

* Lås upp proportioner: Användare kan nu låsa upp proportioner när de justerar storleksegenskaper, vilket möjliggör oberoende bredd- och höjdjusteringar för mer flexibel lagerstorlek.
* Konfiguration av textpassningsrader: Stöd för `copyfitlines`- och `copyfitmaxlines`-inställningar i textpassningsegenskaper har lagts till, vilket ger bättre kontroll över textpassningsbeteendet.

**Visuell polsk**

* Uppdaterade ikoner för Timer- och Shape-lager med avancerade systemikoner för Spectrum 2 (S2).

## [!DNL Experience Manager Forms] som en [!DNL Cloud Service] {#forms}

### Tidiga åtkomstfunktioner i AEM Forms {#forms-early-access-features}

**Visa etiketter för flervalslistrutan i Skicka PDF**
Flervalskomponenter i listrutan Adaptive Forms återger nu de valda visningsetiketterna i den [genererade Submission PDF](/help/forms/generate-document-of-record-core-components.md) så att dokumentet korrekt återspeglar vad som visas i formuläret.

**Förbättrad tillgänglighet för kryssrutor, alternativknappar och panelkomponenter**
Med adaptiva Forms Core Components introduceras WCAG 2.2-kompatibel semantisk markering för [kryssrutegrupper(v2)](https://experienceleague.adobe.com/sv/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/checkbox-group), [alternativknappsgrupper(v2)](https://experienceleague.adobe.com/sv/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/radio-button) och [panelkomponenten](https://experienceleague.adobe.com/sv/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel) . De här komponenterna utnyttjar `<fieldset>`- och `<legend>` HTML-element för att skapa meningsfulla relationer mellan gruppetiketter och deras alternativ, vilket möjliggör korrekt tolkning av skärmläsare och andra hjälpmedelstekniker.

**Versionsstöd i Forms Manager**
Forms Manager har nu [&#x200B; stöd för versionshantering för adaptiva Forms (Core Components and Foundation Components) &#x200B;](/help/forms/manage-form-versions-forms-manager.md) , formulärfragment, teman, XDP-mallar och binära resurser. Skapa versioner, se hela versionshistoriken och återställ tidigare lägen för formulärresurserna direkt från Forms &amp; Documents-konsolen.

## [!DNL Experience Manager] som en [!DNL Cloud Service]-grund {#foundation}

### [!DNL Experience Manager] som [!DNL Cloud Service] Foundation New Features {#foundation-new}

#### Förenklad indexhantering {#simplified-index-management}

[Förenklad indexhantering](https://oak-indexing.github.io/oakTools/simplified.html) är ett enklare sätt att definiera anpassade index och anpassa OTB-index med en JSON-fil, utan att behöva kopiera fullständiga definitioner eller hantera versioner manuellt. Anpassningarna sammanfogas med det senaste OTB-indexet och en ny indexversion skapas vid behov.

#### Cloud Manager MCP Server {#cm-mcp-server}

>[!VIDEO](https://video.tv.adobe.com/v/3480346/?captions=swe&quality=12)

Moderna utvecklingsmiljöer använder MCP (Model Context Protocol) för att möjliggöra stora språkmodeller för att anropa verktyg som exponeras av MCP-servrar. I stället för att integrera direkt med lågnivå-API-specifikationer kan utvecklare beskriva sin avsikt på ett naturligt språk.

Med Cloud Manager MCP Server kan du interagera med Cloud Manager API:er direkt från din utvecklingsmiljö med hjälp av uppmaningar. Exempel på scenarier som stöds är att köra pipelines, kontrollera miljöstatus med mera.

Läs mer om [AEM MCP-servrar](/help/ai-in-aem/mcp-support/using-mcp-with-aem-as-a-cloud-service.md).

### [!DNL Experience Manager] som [!DNL Cloud Service] Foundation Viktigt Notices {#foundation-notices}

#### Java API-borttagningar {#java-api-deprecation}

De borttagna API:erna med mål 2/26/2026 ska inte längre användas i koden. Om du vill förhindra distributionsblock tar du bort API-användning före **30 mars 2026**. Viktiga datum:

* **Från och med 26 januari 2026**: Meddelanden från Åtgärdscenter skickas som en påminnelse om att ta bort användningen av dessa API:er.
* **26 februari 2026**: Cloud Manager-pipelines som innehåller kod som använder dessa API:er **pausas** under **kodkvalitet** -steget. Distributionshanteraren, projektledaren eller affärsägaren kan åsidosätta problemet så att pipeline kan fortsätta. *Det kan göra att du inte kan validera och släppa kodändringar.*
* **30 mars 2026**: Cloud Manager-pipelines som innehåller kod som använder dessa API:er **misslyckas** under steget **Kodkvalitet**. Distributioner blockeras tills den borttagna API-användningen tas bort. *Detta kan hindra dig från att släppa tidskänsliga uppdateringar och kan påverka dina affärsåtgärder.*
* **4 maj 2026**: Miljöer som fortfarande använder inaktuella API:er **kommer inte att få viktiga Adobe-uppdateringar** och omfattas inte av Adobe standardåtaganden om prestanda och tillgänglighet. Du får alltså inga nya funktioner eller felkorrigeringar, programmets stabilitet och drifttid kan påverkas negativt och säkerhetsriskerna kan öka ytterligare.

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
* `org.apache.jackrabbit.oak.plugins.memory`

+++

### [!DNL Experience Manager] som en [!DNL Cloud Service] Foundation Tidiga Adobe-funktioner {#foundation-early-adopter}

#### IDE AI-verktyg för AEM Java och Dispatcher Development (Public Beta Program) {#ai-dev-beta}

Java-stackteam använder i allt större utsträckning AI-assisterad utveckling i verktyg som Cursor, Claude Code, Visual Studio och IntelliJ för att snabba upp leverans av funktioner och förbättra kodkvaliteten.

Delta i betaversionen (ingen registrering krävs) för att testa IDE-verktyg som kan användas av kodningsagenter för att generera och felsöka AEM-kod och dispatcherkonfiguration.

Läs mer i betatestningsdokumentationen för [Local Development with AI Tools](/help/ai-in-aem/local-development-with-ai-tools.md) och i e-postmeddelandet [aemcs-ai-ide-tools-feedback@adobe.com](mailto:aemcs-ai-ide-tools-feedback@adobe.com) med frågor eller feedback.

#### Funktioner i AEM Edge (Beta) {#edge-functions}

Med AEM Edge Function kan du köra JavaScript i CDN-lagret, vilket tar databearbetningen närmare slutanvändaren. Detta minskar latensen och möjliggör responsiva, dynamiska upplevelser i framkanten.

Exempel på vanliga användningsområden:

* Anpassa innehåll baserat på geografisk placering, enhetstyp eller användarattribut
* Fungerar som mellanvara mellan CDN och ditt ursprung
* Formatera om svar från tredjeparts-API:er (och kanske samla in flera API-svar) innan de skickas till webbläsaren
* Skapa och leverera serveråtergivna HTML i toppklass med material som sammanfogats från olika bakgrunder
* Exponera en MCP-server för LLM-program som ChatGPT och Claude för att få tillgång till anpassade verktyg

Vi har ett begränsat antal möjligheter, antingen för AEM Publish Delivery eller för Edge Delivery Services-projekt, för produktionssajter. Om du är intresserad av att delta eller vill veta mer kan du skicka ett e-postmeddelande till [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) med en kort beskrivning av ditt användningsfall.

#### Felsökning av konfigurationsförlopp på webbnivå med utvecklingsagenten (Beta-programmet) {#devagent-webtier}

Utvecklingsagentens [pipeline-felsökning](/help/ai-in-aem/agents/brand-experience/development/development.md) hjälper utvecklare att effektivt diagnostisera och lösa problem i AEM as a Cloud Service-distributioner. Förutom att utvecklingsagenten har stöd för fullständiga stackrörledningar (driftsättnings- och kodkvalitet) har den nu även stöd för felsökning för **konfigurationspipelinen för webbnivån** som en del av ett betaprogram.

Om du vill begära åtkomst till betaversionen skickar du ett e-postmeddelande till [aem-devagent@adobe.com](mailto:aem-devagent@adobe.com). Åtkomst till agenter i AEM krävs.

#### IDE AI-verktyg för AEM 6.5 till AEM Cloud Service Migration (Alpha Program) {#cm-ide-migration}

Snabba upp migreringen från AEM 6.5 till AEM as a Cloud Service (Java stack) genom att använda IDE AI-verktygen för att följa rekommendationerna i [Best Practices Analyzer Report](/help/journey-migration/best-practices-analyzer/overview-best-practices-analyzer.md).

Mejla [aemcs-ai-ide-tools-feedback@adobe.com](mailto:aemcs-ai-ide-tools-feedback@adobe.com) för mer information.

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

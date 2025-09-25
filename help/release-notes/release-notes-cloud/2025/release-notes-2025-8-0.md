---
title: Versionsinformation om 2025.8.0-utgåvan av  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Versionsinformation om 2025.8.0-utgåvan av  [!DNL Adobe Experience Manager] as a Cloud Service.
feature: Release Information
role: Admin
source-git-commit: 4187f9bb08d8af214054b937a5426e95c1de748d
workflow-type: tm+mt
source-wordcount: '1910'
ht-degree: 0%

---

# Versionsinformation 2025.8.0 för [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

I följande avsnitt beskrivs versionsinformationen för funktionen för 2025.8.0-versionen av [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Härifrån kan du navigera till versionsinformation för tidigare versioner som 2023 eller 2024.
>
>Ta en titt på [Experience Manager Releases Roadmap](https://experienceleague.adobe.com/sv/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) om du vill veta mer om kommande funktionsaktiveringar för [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Om du vill få ett månatligt e-postmeddelande om uppdateringar av Experience Cloud versionsinformation prenumererar du på [Adobe Priority Product Update](https://www.adobe.com/subscription/priority-product-update.html).

## Releasedatum {#release-date}

Releasedatum för [!DNL Adobe Experience Manager] som [!DNL Cloud Service] aktuell funktionsversion (2025.8.0) är 28 augusti 2025. Nästa funktionsversion (2025.9.0) är planerad till 25 september 2025.

## Versionsinformation om underhåll {#maintenance}

Du hittar den senaste underhållsversionsinformationen [här](/help/release-notes/maintenance/latest.md).

<!-- 

## Release Video {#release-video}

Have a look at the July 2025 Release Overview video for a summary of the features added in the 2025.7.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3440920?quality=12)

-->

## Experience Hub {#experience-hub}

[Experience Hub](/help/experience-hub.md) är den centrala utgångspunkten för åtkomst till alla AEM-funktioner. Det är personaliserat baserat på din användarpersonlighet och de licenser som är tillgängliga för dig, så att varje användare kan uppnå sina resultat effektivt.

## AI Assistant i AEM {#AI-assistant}

[AI Assistant](/help/implementing/cloud-manager/ai-assistant-in-aem.md) för AEM har ett konversationsgränssnitt som ger dig snabba svar på dina produktrelaterade frågor om AEM (*som är tillgängliga för alla användare*) och automatisera skapandet av supportärenden (*som är tillgängliga för supportadministratörer*). Det är direkt inbäddat i AEM och tillgängligt från AEM Experience Hub, Cloud Manager och redigeringsgränssnittet.

## [!DNL Experience Manager Sites] som en [!DNL Cloud Service] {#sites}

### Nya funktioner i Experience Manager Sites {#enhancements-sites}

* I Administratörsgränssnittet för innehållsfragment kan du nu visa arbetsflödesstatusen för innehållsfragment, med detaljerad information om tidigare och pågående arbetsflöden för ett valt fragment.
* Prestandan för att öppna innehållsfragment i den nya redigeraren för innehållsfragment har ökat med 25 % i vanliga scenarier genom att öppna fragment via UUID i stället för via sökväg.
* När du kopierar innehållsfragment med refererade fragment lagras kopior av refererade fragment nu på samma plats som den överordnade fragmentkopian.
* Nu kan du konfigurera en anpassad arbetsyta i mappinställningarna för att exportera innehållsfragmenten till den konfigurerade arbetsytan i Adobe Target.

## [!DNL Experience Manager Assets] som en [!DNL Cloud Service] {#assets}

### Nya funktioner i Content Hub {#new-features-content-hub}

**Masssökning via filteregenskaper**

Content Hub gör det nu snabbare att upptäcka de resurser ni behöver. Med den nya funktionen för masssökning kan du ange flera värden för valfri filteregenskap, avgränsade med en avgränsare (till exempel flera SKU-ID:n), och omedelbart hämta alla matchande resurser med en enda sökning.

### Nya funktioner i Dynamic Media med OpenAPI-funktioner {#new-features-dynamic-media-with-openapi}

**SEO-vänlig DM med OpenAPI-URL:er**

Skapa Vanity-URL:er för leverans av resurser i DM med OpenAPI och ersätt långa systemgenererade UUID:n med korta, läsbara identifierare. Detta gör länkar till SEO-anpassade och bättre anpassade till ert varumärke eller era kampanjer. Vanity-URL:er löses automatiskt till det ursprungliga resurs-UUID:t vid körning utan att befintliga arbetsflöden avbryts.

>[!NOTE]
>
>Den här funktionen blir tillgänglig som en begränsad tillgänglighetsfunktion den 10 september. Du kan [skapa och skicka ett Adobe kundsupportärende](https://helpx.adobe.com/se/enterprise/using/support-for-experience-cloud.html) för att aktivera det för din distribution.

## [!DNL Experience Manager Forms] som en [!DNL Cloud Service] {#forms}

* [Indatakomponent för datum och tid](https://experienceleague.adobe.com/sv/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/date-time-component): Nu finns det en komponent för datum och tid som gör att användare kan välja både datum och tid med hjälp av ett kalender- och klockgränssnitt, eller genom att ange värden manuellt i ett format som stöds.
* [Förbättrad felhantering för filöverföringar](https://experienceleague.adobe.com/sv/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/file-attachment#basic-tab): Komponenten för bifogad fil validerar nu automatiskt den överförda filtypen mot tillåtelselista. Om en användare överför en fil i ett format som inte stöds visas ett fel under överföringen. Komponenten kontrollerar också filinnehållet för att validera dess typ, vilket förbättrar formulärets övergripande säkerhet.
* [Angivet felsvar för anpassad skickaåtgärd](/help/forms/custom-submit-action-troubleshooting.md): När en anpassad sändningsåtgärd påträffar ett ohanterat fel returneras felkod 502. Detta hjälper till att identifiera att problemet är relaterat till den anpassade skicka-åtgärden, vilket gör felsökningen enklare.
* [Utesluter dolda fält från postdokument](/help/forms/generate-document-of-record-core-components.md#document-of-record-settings): En ny egenskap har lagts till för att tillåta att dolda fält utesluts från postdokumentet. Som standard är det här alternativet inte markerat och gäller för alla formulärfält.

### Pre-Release-funktioner i AEM Forms

* [Generera och synkronisera AFP-återgivningar](/help/forms/document-generation-afp-api.md): Nu kan du använda AEM Forms Communication API för att konvertera en XDP-fil till AFP-format. AFP är ett högpresterande format som används ofta vid storskalig trycksaksproduktion.
* **Förbättringar i regelredigeraren**
   * [Validera metod i funktionslista](/help/forms/rule-editor-enhancements-use-cases.md#validate-method-in-function-list): Metoderna validate och reset har nu stöd för körning på panelnivå, fält- och formulärnivå. Tidigare stöddes de endast på formulärnivå.
   * [Modernt stöd för JavaScript](/help/forms/rule-editor-core-components-difference-tables.md): Stöd för ECMAScript 2019 och senare funktioner har lagts till för anpassade funktioner, vilket gör att du kan skriva mer effektiv, modulär och återanvändbar kod
   * [Ladda ned DoR-alternativ i regelredigeraren](/help/forms/rule-editor-enhancements-use-cases.md#downloaddor-as-ootb-fuction-in-rule-editor): En funktion för att hämta dokumentarkivfilen (DoR) har lagts till som ett OTB-alternativ (Out-of-Box) i regelredigeraren.
     ![Dokument-av-post](/help/forms/assets/document-of-record-rn.gif)
   * [Dynamiska variabler i Regelredigeraren](/help/forms/rule-editor-enhancements-use-cases.md#support-for-dynamic-variables-in-rules): Du kan nu använda dynamiska (tillfälliga) variabler i Regelredigeraren för större flexibilitet när du definierar villkor och åtgärder. Dolda fält behövs inte längre för att lagra tillfälliga värden.
   * [Stöd för anpassade händelsebaserade regler](/help/forms/rule-editor-enhancements-use-cases.md#custom-event-based-rules-support): Du kan nu definiera anpassade händelser och utlösarregler baserat på dessa händelser.
   * [Kontextmedvetna upprepningsbara panelregler](/help/forms/rule-editor-enhancements-use-cases.md#context-based-rule-execution-for-repeatable-panels): I upprepningsbara paneler körs nu regler baserat på kontext, i stället för att bara tillämpas på den sista panelinstansen.
   * [Regler som utlösts av parametrar](/help/forms/rule-editor-enhancements-use-cases.md#url-and-browser-parameter-based-rules-in-adaptive-forms): Regelredigeraren stöder nu regelkörning baserat på frågeparametrar, UTM-parametrar eller webbläsarparametrar.
   * [Formulärspecifika anpassade funktioner](/help/edge/docs/forms/universal-editor/rule-editor-universal-editor.md#organizing-custom-functions-across-different-forms): Edge Delivery Services Forms har nu stöd för formulärspecifika anpassade funktionsskript, vilket ger större flexibilitet vid hantering av återanvändbar logik.
   * [Statisk import för anpassade funktioner](/help/edge/docs/forms/universal-editor/rule-editor-universal-editor.md#static-imports-for-custom-functions): Regelredigeraren i Universal Editor har nu stöd för statiska importer, vilket gör att utvecklare kan ordna, dela och återanvända funktioner i flera formulär.

### Tidiga Adobe-funktioner i AEM Forms

* [Klottsigneringskomponent](https://experienceleague.adobe.com/sv/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/scribble-signature): Nu kan du använda komponenten Klottsignatur för att hjälpa användare att lägga till sina signaturer i ett formulär, till exempel i ett avtalsformulär. Med komponenten kan användare rita sin signatur direkt i formuläret med en mus, en styluspenna eller en pekskärm.
* [Direkt API-integrering i regelredigeraren](/help/forms/api-integration-in-rule-editor.md): Adaptiv Forms har nu stöd för direkt API-integrering i Visual Rule Editor utan att någon formulärdatamodell krävs. Författare kan konfigurera API:er med en URL- eller cURL-import, mappa in-/utdataparametrar och säkra anrop med autentisering.

<!--
**Forms Optimization opportunities**

Forms Optimization uses AI to analyze your forms and suggest improvements for better performance. It highlights forms with low engagement, flags accessibility issues, and generates AI-powered variations to help increase conversion rates and compliance with WCAG standards.

>[!VIDEO](https://video.tv.adobe.com/v/3469472/) 

Key optimization opportunities include:

* Increasing visibility for forms with low views
* Improving completion rates for forms with low conversions
* Addressing accessibility compliance issues
* Streamlining navigation to enhance user experience

With Forms Optimization, you get automated, data-driven recommendations and variations, making it easier to boost engagement and ensure your forms are effective and inclusive. -->

## [!DNL Experience Manager] som en [!DNL Cloud Service]-grund {#foundation}

### JavaScript Compilation Update {#javascript-compilation}

JavaScript-kompileringen för standardbiblioteket (clientlibs) har nu ECMASCRIPT_2018 som mål i stället för ECMASCRIPT5. Uppdateringen kan åsidosättas tidigare men ger prestandaförbättringar, modern JavaScript-syntax och funktioner som standard.

### Kommande Java API-borttagningar {#java-api-deprecation}

Flera inaktuella API:er är avsedda för borttagning den 31 augusti och bör därför inte längre refereras. I början av september kommer meddelanden från Åtgärdscenter att skickas om API-användning upptäcks, och efter den 25 september kommer meddelanden att visas under Cloud Manager byggen för att förstärka vikten av att ta bort användningen. Mer information finns i artikeln [som inte längre används](/help/release-notes/deprecated-removed-features.md#aem-apis), men dessa API:er finns i listan nedan för att underlätta:

<details>
  <summary>Expandera om du vill visa Java API-borttagningar</summary>

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
</details>

<!--
OSGi properties:

* `org.apache.sling.commons.log.LogManager` (all properties)
* `org.apache.sling.commons.log.LogManager.factory.config` (`org.apache.sling.commons.log.file`, `org.apache.sling.commons.log.pattern`)
* 

-->

### Java 11 Runtime Deprecation {#java11-runtime-deprecation}

*Java 11-miljön* är nu föråldrad och de flesta miljöer har redan uppgraderats till den mer prestandaanpassade **Java 21-miljön**.

Om din miljö inte kunde uppgraderas på grund av beroenden som inte stöds (se [Java 21-körningskrav](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements)), bör du ha fått ett e-postmeddelande från Adobe med specifika nästa steg. Kontrollera att alla nödvändiga uppdateringar är slutförda senast **1 oktober 2025** så att miljön kan uppgraderas utan avbrott.

Obs! Körningsversionen är en annan än den version koden har. Vi rekommenderar att du bygger med Java 21, men Java 11-byggen stöds fortfarande för tillfället. Ett separat meddelande om borttagning av Java 11-byggen kommer att delas i framtiden.

### Tillämpning av konfigurationspolicy för AEM Java-loggar {#logconfig-policy}

Som framgår av versionsinformationen för april måste AEM Java-loggarna följa ett standardformat för att säkerställa tillförlitlig övervakning i alla kundmiljöer. Anpassade loggkonfigurationer, t.ex. ändringar i loggformatering, utdatafiler eller standardloggnivåer, stöds inte längre. Loggar måste vara dirigerade till standardfilerna och standardloggnivåerna för AEM-produktkoden måste bevaras. Mer information finns i artikeln [Loggning](/help/implementing/developing/introduction/logging.md#configuration-loggers).

Med början den **25 september** kommer alla anpassade loggningsåsidosättningar som inte stöds att ignoreras. Baserat på vår analys kommer de flesta kunder inte att påverkas och Adobe har kontaktat kunder vars nuvarande konfiguration kan påverkas.

Granska och uppdatera alla processer som är beroende av anpassat loggningsbeteende. Till exempel:

* Om ditt system för vidarebefordring av loggar förväntar sig ett anpassat loggformat kan du behöva justera dina regler för inmatning.
* Om du tidigare har minskat loggens utförlighet genom att ändra loggnivåerna bör du tänka på att en återställning till standardnivåerna kan öka loggvolymen.

### Edge Computing (Beta Program) {#edge-computing}

Med Edge kan du köra JavaScript på CDN-lagret, vilket tar databearbetningen närmare slutanvändaren. Detta minskar latensen och möjliggör responsiva, dynamiska upplevelser i framkanten.

Exempel på vanliga användningsområden:

* Autentisera användare med en identitetsleverantör innan du beviljar åtkomst till innehåll
* Anpassa innehåll baserat på geografisk placering, enhetstyp eller användarattribut
* Fungerar som mellanvara mellan CDN och ditt ursprung
* Formatera om svar från tredjeparts-API:er (och kanske samla in flera API-svar) innan de skickas till webbläsaren
* Skapa och leverera serveråtergivna HTML i toppklass med material som sammanfogats från olika bakgrunder
* Exponera en MCP-server för LLM-program som ChatGPT och Claude för att få tillgång till anpassade verktyg

Vi har ett begränsat antal möjligheter, antingen för AEM Publish Delivery eller för Edge Delivery Services-projekt, för produktionssajter. Om du är intresserad av att delta eller vill veta mer kan du skicka ett e-postmeddelande till [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) med en kort beskrivning av ditt användningsfall.

### CDN-konfiguration för Edge Delivery Services (Beta-programmet) {#cdn-eds-beta}

Adobe-hanterad CDN erbjuder flexibla konfigurationsalternativ, vilket beskrivs i artikeln [Konfigurera pipeline](/help/operations/config-pipeline.md#configurations).

I betaversionen kan du nu distribuera en konfigurationsprocess för funktioner som väljare av CDN-ursprung, svar- och begärandeomvandlingar, CDN-loggvidarebefordran med mera. Kontakta [aemcs-cdn-config-adopter@adobe.com](mailto:aemcs-cdn-config-adopter@adobe.com) med information om ditt användningsfall.

### Ögonblicksbilder för RDE (Alpha Program) {#rde-snapshot-program}

I alfa har Rapid Development Environment (RDE) nu stöd för en funktion som tar en ögonblicksbild av det aktuella kodläget och innehållet, som kan återställas vid ett senare tillfälle. Detta kan vara användbart när du synkroniserar kod som behöver återställas eller när du växlar mellan utveckling av olika funktioner. Det går också att återställa bara det ändringsbara innehållet som en känd startpunkt för testning.

Skicka ett e-postmeddelande till [aemcs-rde-support@adobe.com](mailto:aemcs-rde-support@adobe.com) om du är intresserad av att lämna feedback om funktionen.

### AEM Log-Forwarding to More Destinations (Beta Program) {#log-forwarding-beta}

Medan loggar kan hämtas från Cloud Manager tycker många att det är bra att strömma dessa loggar till ett önskat loggningsmål. AEM har redan stöd för AEM- och CDN-loggvidarebefordran till Azure Blob Storage, Datadog, HTTPS, Elasticsearch (och OpenSearch) och Splunk. Den här funktionen är konfigurerad på ett självbetjäningssätt och distribueras med Config Pipeline.

I betaversionen kan du nu vidarebefordra AEM-loggar till Amazon S3, Sumo Logic, Dynatrace och ditt eget New Relic-konto (inte till Adobe-kontot). Observera att AEM-loggar (inklusive Apache/Dispatcher) stöds för dessa loggningsmål, men inte CDN-loggar. E-post [aemcs-logforwarding-beta@adobe.com](mailto:aemcs-logforwarding-beta@adobe.com) för åtkomst.

Läs mer i [dokumentationen för vidarebefordran av loggfiler](/help/implementing/developing/introduction/log-forwarding.md).

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

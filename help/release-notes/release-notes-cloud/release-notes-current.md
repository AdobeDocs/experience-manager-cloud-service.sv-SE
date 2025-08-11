---
title: Aktuell versionsinformation för  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Versionsinformation för  [!DNL Adobe Experience Manager] as a Cloud Service.
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: 401eaaaa0bb8dad054c7105533cbd4486964c484
workflow-type: tm+mt
source-wordcount: '2269'
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

Releasedatum för [!DNL Adobe Experience Manager] som [!DNL Cloud Service] aktuell funktionsversion (2025.7.0) är 7 augusti 2025. Nästa version (2025.8.0) är planerad till 28 augusti 2025.

## Versionsinformation om underhåll {#maintenance}

Du hittar den senaste underhållsversionsinformationen [här](/help/release-notes/maintenance/latest.md).

<!-- 

## Release Video {#release-video}

Have a look at the July 2025 Release Overview video for a summary of the features added in the 2025.7.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3440920?quality=12)

-->

## [!DNL Experience Manager Sites] som en [!DNL Cloud Service] {#sites}

### Nya funktioner i Experience Manager Sites {#enhancements-sites}

* Nu kan du kopiera innehållsfragment med refererade fragment (underordnade fragment) i en åtgärd. Detta gör att befintliga innehållsfragmentstrukturer kan återanvändas för att skapa nytt innehåll.
* I Administratörsgränssnittet för innehållsfragment kan du nu visa arbetsflödesstatusen för innehållsfragment, med detaljerad information om tidigare och pågående arbetsflöden för ett valt fragment.
* Om du byter namn på eller flyttar en källsida för live-kopia kommer det nu att utlösa en ompublicering av en sida med motsvarande namn eller flyttad live-kopia.

## [!DNL Experience Manager Assets] som en [!DNL Cloud Service] {#assets}

**Lägg till former i dynamiska mediamallar**

Du kan nu [lägga till formlager i dynamiska mediamallar](/help/assets/dynamic-media/dynamic-media-templates.md#add-shapes-to-the-canvas) i Experience Manager Assets. Precis som bild- och textlager har formlager stöd för parametrar för realtidsuppdateringar via mallens URL. Du kan även inkludera call-to-action-länkar (CTA) till former i dina mallar.

![Lägg till former i dynamiska mediamallar](/help/assets/assets/enable-uniform-radius-shape.png)

**Förbättringar av AI-genererade metadata**

Nu kan du [konfigurera visningen av resursrubriker i kortvyn eller listvyn](/help/assets/smart-tags.md#configure-ai-generated-titles) på sidan Resurssökning i AEM Assets. Du kan välja att visa resurstiteln som du har definierat, titeln som har genererats med AI, eller använda AI-genererad titel endast om det inte finns någon befintlig titel för resursen.

![Konfigurera AI-genererade titlar](/help/assets/assets/configure-title-ai-generated.png)

Du kan nu även välja att inaktivera AI-genererade metadata på mappnivå.

### Nya funktioner i Content Hub {#new-features-content-hub}

**Utökad flexibilitet för varumärken i Content Hub**

Tack vare de befintliga personaliseringsfunktionerna kan administratörer nu skräddarsy sin driftsättning ytterligare genom att lägga till anpassade logotypbilder. Stöd för filformatet TIFF har också lagts till för både banner- och logotypbilder, vilket ger större flexibilitet i designen.

**Smart delning med namngivna länkar**

Du kan nu lägga till en titel när du skapar en delad länk, oavsett om det är från vyn med tillgångsinformation eller efter att du har valt en eller flera resurser. Detta hjälper mottagarna att enkelt identifiera syftet med varje länk, särskilt när de tar emot flera delade resurser.

![privat och offentlig länk](/help/assets/assets/shared-link-for-assets.png)

**Förbättrad filternavigering**

Content Hub innehåller nu alternativet **Visa alla** i filter, vilket gör att användare kan visa alla tillgängliga aspekter tillsammans med resursantal från den aktuella begränsningen att endast visa upp till tio sidor. Förbättrade sök- och sorteringsfunktioner i varje filter gör det enklare att upptäcka och hantera resurser effektivare.

### AEM Desktop App version 3.0.0 {#desktop-app-release-3.0.0}

Få automatisk uppladdning av nya filer och mappar, förbättrad filhantering, smartare resursidentifiering och smidig integrering med AEM - vilket gör innehållshanteringen snabbare, tydligare och mer intuitiv.

En fullständig lista över funktioner finns i [Versionsinformation för skrivbordsapp](https://experienceleague.adobe.com/en/docs/experience-manager-desktop-app/using/release-notes).

### Nya funktioner i Dynamic Media med OpenAPI-funktioner {#new-features-dynamic-media-with-openapi}

**Förhandsgranska resurser före publicering**

[!DNL Dynamic Media with OpenAPI capabilities] tillåter nu att du förhandsgranskar resurser direkt på [!DNL AEM Sites]-författarsidor innan du gör dem tillgängliga för allmänheten. Dela förhandsgranskningssidor med intressenter för att samla in feedback om visuell kvalitet och kontextuell anpassning. Under granskningscykeln kan du skapa och hantera flera versioner av resurser innan du färdigställer dem för publicering.

**Förbättrad Smart Imaging för OpenAPI-bildbegäranden**

Alla OpenAPI-bildbegäranden utnyttjar nu Smart Imaging fullt ut med automatisk befordran och reservlogik. Den här förbättringen optimerar bilder baserat på enhets- och nätverksförhållanden, vilket ger snabbare sidinläsning och minskad bandbreddsanvändning samtidigt som den visuella kvaliteten bibehålls.


## [!DNL Experience Manager Forms] som en [!DNL Cloud Service] {#forms}

### Nya funktioner i AEM Forms {#forms-new-features}

**Universell redigerare för adaptiva Forms och formulärfragment**

[Universal Editor](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md) har nu stöd för att skapa både adaptiva Forms-filer och återanvändbara formulärfragment. Man kan visuellt skapa blanketter, konfigurera skicka-åtgärder och lägga in reCAPTCHA-validering i en förenklad WYSIWYG-miljö. Detta snabbar upp framtagningen av blanketter, ger bättre enhetlighet och förbättrar skyddet mot skräppost och automatiskt missbruk.

![Universell redigerare](/help/edge/docs/forms/universal-editor/assets/universal-editor.png){width=80%, align-center}


**Forms Submission Service för Edge Delivery Services Forms**

Se [Forms Submission Service](/help/forms/forms-submission-service.md). Med kan du smidigt lagra data från inskickade adaptiva formulär direkt i vanliga kalkylbladsplattformar som Google Sheets, Microsoft OneDrive eller SharePoint. Integreringen effektiviserar datahanteringen genom att möjliggöra direkt inlämning av formulärdata till det kalkylblad du valt, vilket eliminerar manuell dataöverföring och minskar antalet fel.

Några viktiga fördelar:

* **Direktintegrering:** Konfigurera formulären så att de skickar data direkt till ett angivet kalkylblad.
* **Anpassad datamappning:** Mappa formulärfält till motsvarande kalkylbladskolumner för organiserad lagring.
* **Åtkomstkontroll:** Utnyttja befintliga kalkylbladsbehörigheter för att hantera vilka som får åtkomst till eller ändra skickade data.

**Generera och synkronisera AFP-återgivningar från adaptiv Forms**

Med API:t [AFP Output Sync](/help/forms/document-generation-afp-api.md) kan administratörer och användare generera AFP-utdata (Advanced Function Presentation) från Adaptive Forms och synkronisera utdata med externa system eller lagringsplatser. AFP är ett högpresterande dokumentformat som är optimerat för utskrift och ofta används i storskaliga företagsmiljöer.

<!-- ### New pre-release features in AEM Forms {#forms-new-pre-release-features}

**Enhancements in Rule Editor**

* The `validate` method in the function list now supports validation at the panel, field, and form levels.
* Client-side custom function parsing now supports ES10+ JavaScript features and static imports.
* The button to download Document of Record (DoR) is now available as an out-of-the-box (OOTB) option in the rule editor.
* Rules now support the use of dynamic variables.
* Custom event-based rules are now supported.
* Repeatable panel rules are now executed based on context, rather than only on the last panel instance.
* Rules can now be triggered based on query parameters, UTM parameters, and browser parameters.
* Form-specific custom function scripts are now supported for Adaptive Forms in Edge Delivery Services.

 -->

### Nya funktioner för tidig åtkomst i AEM Forms {#forms-new-early-access-features}

AEM Forms Early Access Program ger dig unika möjligheter att få exklusiv tillgång till de senaste innovationerna och hjälpa till att utforma deras utveckling.

I versionsinformationen visas de innovationer som levererats i den aktuella versionen. En fullständig lista över de innovationer som är tillgängliga under Tidig åtkomst-programmet finns i [AEM Forms Tidig åtkomst-programdokumentation](/help/forms/early-access-ea-features.md).


<!-- **Forms Optimization opportunities**

Forms Optimization uses AI to analyze your forms and suggest improvements for better performance. It highlights forms with low engagement, flags accessibility issues, and generates AI-powered variations to help increase conversion rates and compliance with WCAG standards.

>[!VIDEO](https://video.tv.adobe.com/v/3469472/) 

Key optimization opportunities include:

* Increasing visibility for forms with low views
* Improving completion rates for forms with low conversions
* Addressing accessibility compliance issues
* Streamlining navigation to enhance user experience

With Forms Optimization, you get automated, data-driven recommendations and variations, making it easier to boost engagement and ensure your forms are effective and inclusive. -->

**Regelredigerare för interaktiv kommunikationsredigerare**

Bygg dynamiska, datadrivna funktionsmakron direkt i dokumenten med ett intuitivt musstyrt gränssnitt. Definiera enkelt villkorsstyrd logik, automatisera arbetsflöden och personalisera innehåll utan att behöva skriva kod.

**AEM Forms Scaffolder CLI för anpassade komponenter**

>[!VIDEO]&#x200B;(https://video.tv.adobe.com/v/3470514/aem-forms)

Snabba upp utvecklingen av AEM Forms Edge Delivery Services med detta CLI-verktyg. Generera kod och kablar som behövs för att snabbt komma igång med utvecklingen av anpassade komponenter - ingen boilerplate, inget trassel.

**API-integreringsverktyg för dynamiska formulärdata**

Med API Integration Tool kan man skapa dynamiska, intelligenta blanketter som automatiskt hämtar och fyller i data från externa REST API:er baserat på användarinteraktioner. Denna icke-kodsintegration omvandlar statiska formulär till responsiva datainsamlingsgränssnitt.

## [!DNL Experience Manager] som en [!DNL Cloud Service]-grund {#foundation}

### Nodvy för behörighetshantering {#node-view}

AEM introducerar behörighetshantering för nodvy. Huvudfunktionaliteten är densamma som det klassiska användargränssnittet, men är mer användarvänlig och effektiv. Mer information finns i den [dedikerade artikeln](/help/security/touch-ui-principal-view.md).

### Uppdaterad borttagningsprocess {#updated-deprecation-process}

Adobe granskar regelbundet funktioner, bibliotek, API:er och konfigurationer för att säkerställa att de uppfyller standarder för prestanda, säkerhet och värde. När funktioner inte längre uppfyller dessa standarder markeras de för borttagning och användningen måste stoppas med ett angivet borttagningsdatum. Adobe kommer fram till detta datum att påminna kunderna med e-postmeddelanden och åtgärder som måste vidtas i Cloud Manager innan nya byggen kan fortsätta eller distribueras. Om du inte vidtar nödvändiga åtgärder kan det leda till att du inte kan uppgradera till nya versioner av AEM, vilket kan påverka säkerheten, prestanda, tillförlitlighet och tillgänglighet.

Mer information finns i artikeln [som inte längre används](/help/release-notes/deprecated-removed-features.md).

#### Inaktuella Java-API:er och OSGi-konfigurationer närmar sig borttagningsdatum {#deprecated-near-removals}

Expandera listan nedan för att visa de inaktuella API:er och OSGi-konfigurationer som inte längre får användas. Mer information, inklusive tidslinjer för borttagning, finns i artikeln om borttagning.

<details>
  <summary>Expandera om du vill visa borttagningarna</summary>

Java-API:er:

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

OSGi-egenskaper:

* `org.apache.sling.commons.log.LogManager` (alla egenskaper)
* `org.apache.sling.commons.log.LogManager.factory.config` (`org.apache.sling.commons.log.file`, `org.apache.sling.commons.log.pattern`)

</details>

### Java 11 Runtime Deprecation {#java11-runtime-deprecation}

**Java 11-miljön*- är nu föråldrad och de flesta miljöer har redan uppgraderats till den mer avancerade **Java 21-miljön**.

Om din miljö inte kunde uppgraderas på grund av beroenden som inte stöds (se [Java 21-körningskrav](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements)), bör du ha fått ett e-postmeddelande från Adobe med specifika nästa steg. Kontrollera att alla nödvändiga uppdateringar är slutförda senast den **28 augusti 2025** så att miljön kan uppgraderas utan avbrott.

Obs! Körningsversionen är en annan än den version koden har. Vi rekommenderar att du bygger med Java 21, men Java 11-byggen stöds fortfarande för tillfället. Ett separat meddelande om borttagning av Java 11-byggen kommer att delas i framtiden.

### Tillämpning av konfigurationspolicy för AEM Java-loggar {#logconfig-policy}

Som framgår av versionsinformationen för april måste AEM Java-loggarna följa ett standardformat för att säkerställa tillförlitlig övervakning i alla kundmiljöer. Anpassade loggkonfigurationer, t.ex. ändringar i loggformatering, utdatafiler eller standardloggnivåer, stöds inte längre. Loggar måste vara dirigerade till standardfilerna och standardloggnivåerna för AEM-produktkoden måste bevaras. Mer information finns i artikeln [Loggning](/help/implementing/developing/introduction/logging.md#configuration-loggers).

Med början i **slutet av augusti** kommer alla anpassade loggningsåsidosättningar som inte stöds att ignoreras. Baserat på vår analys kommer de flesta kunder inte att påverkas och Adobe har kontaktat kunder vars nuvarande konfiguration kan påverkas.

Granska och uppdatera alla processer som är beroende av anpassat loggningsbeteende. Till exempel:

* Om ditt system för vidarebefordring av loggar förväntar sig ett anpassat loggformat kan du behöva justera dina regler för inmatning.
* Om du tidigare har minskat loggens utförlighet genom att ändra loggnivåerna bör du tänka på att en återställning till standardnivåerna kan öka loggvolymen.

### Standardrensning av äldre versioner och granskningsloggar {#mt-defaults}

För närvarande har innehållsversioner och granskningsloggar sina associerade *rensningsunderhållsaktiviteter - inaktiverade som standard och inga data tas bort om de inte uttryckligen konfigureras.

För att optimera databasprestanda kommer rensning att vara aktiverat som standard vid ett framtida meddelande, enligt följande riktlinjer:

#### Innehållsversioner {#mt-content}

* **Nya miljöer*- (skapas efter ett kommande datum (kommer att meddelas senare)
   * Versioner som är äldre än **30 dagar*- tas regelbundet bort.
   * De senaste fem versionerna under de senaste 30 dagarna bevaras tillsammans med den senaste versionen och den aktuella versionen, oavsett ålder.

* **Befintliga miljöer*- (skapades före detta kommande datum):
   * Versioner som är äldre än **7 år*- tas regelbundet bort.
   * Alla versioner under de senaste 7 åren bevaras.
   * Detta höga standardtröskelvärde förhindrar oavsiktlig borttagning av senaste data. Vi rekommenderar dock att du konfigurerar lägre värden för att optimera databasens prestanda.

* Du kan ändra dessa standardvärden med hjälp av YAML-konfigurationen, som distribueras med konfigurationsflödet.

#### Granskningslogg {#mt-auditlogs}

* **Nya miljöer*- (skapas efter ett kommande datum, som kommuniceras separat):
   * Replikerings-, DAM- och sidgranskningsloggar som är äldre än **7 dagar* - tas regelbundet bort.
   * Alla händelser loggas som standard.

* **Befintliga miljöer*- (skapades före detta kommande datum):
   * Replikerings-, DAM- och sidgranskningsloggar som är äldre än **7 år* - tas regelbundet bort.
   * Alla händelser loggas som standard.
   * Detta höga standardtröskelvärde förhindrar oavsiktlig borttagning av senaste data. Vi rekommenderar dock att du konfigurerar lägre värden för att optimera databasens prestanda.

* Du kan ändra dessa standardvärden med hjälp av YAML-konfigurationen, som distribueras med konfigurationsflödet.

Mer information finns i artikeln [Underhållsåtgärder](/help/operations/maintenance.md#defaults).

### Edge Computing (Alpha Program) {#edge-computing}

Med Edge kan du köra JavaScript på CDN-lagret, vilket tar databearbetningen närmare slutanvändaren. Detta minskar latensen och möjliggör responsiva, dynamiska upplevelser i framkanten.

Exempel på vanliga användningsområden:

* Autentisera användare med en identitetsleverantör innan du beviljar åtkomst till innehåll
* Anpassa innehåll baserat på geografisk placering, enhetstyp eller användarattribut
* Fungerar som mellanvara mellan CDN och ditt ursprung
* Formatera om svar från tredjeparts-API:er (och kanske samla in flera API:er) innan de skickas till webbläsaren
* Skapa och leverera serveråtergivna HTML i toppklass med material som sammanfogats från olika bakgrunder
* Exponera en MCP-server för LLM-program som ChatGPT och Claude för att få tillgång till anpassade verktyg

Vi har ett begränsat antal möjligheter, antingen för AEM Publish Delivery eller för Edge Delivery Services-projekt, för produktionssajter. Om du är intresserad av att delta eller vill veta mer kan du skicka ett e-postmeddelande till [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) med en kort beskrivning av ditt användningsfall.

### CDN-konfiguration för Edge Delivery Services (Beta-programmet) {#cdn-eds-beta}

Adobe-hanterad CDN erbjuder flexibla konfigurationsalternativ, vilket beskrivs i artikeln [Konfigurera pipeline](/help/operations/config-pipeline.md#configurations).

Distribuera nu i en betaversion en konfigurationsprocess för funktioner som väljare av CDN-ursprung, svar- och begäranomvandlingar, CDN-loggvidarebefordran med mera. Kontakta [aemcs-cdn-config-adopter@adobe.com](mailto:aemcs-cdn-config-adopter@adobe.com) med information om ditt användningsfall.

### Ögonblicksbilder för RDE (Alpha Program) {#rde-snapshot-beta}

I alfa har Rapid Development Environment (RDE) nu stöd för en funktion som tar en ögonblicksbild av det aktuella kodläget och innehållet, som kan återställas vid ett senare tillfälle. Detta kan vara användbart när du synkroniserar kod som behöver återställas eller när du växlar mellan utveckling av olika funktioner. Det går också att återställa bara det ändringsbara innehållet som en känd startpunkt för testning.

Skicka ett e-postmeddelande till [aemcs-rde-support@adobe.com](mailto:aemcs-rde-support@adobe.com) om du är intresserad av att lämna feedback om funktionen.

### AEM Log-Forwarding to More Destinations (Beta Program) {#log-forwarding-beta}

Medan loggar kan hämtas från Cloud Manager tycker många att det är bra att strömma dessa loggar till ett önskat loggningsmål. AEM har redan stöd för AEM- och CDN-loggvidarebefordran till Azure Blob Storage, Datadog, HTTPS, Elasticsearch (och OpenSearch) och Splunk. Den här funktionen är konfigurerad på ett självbetjäningssätt och distribueras med Config Pipeline.

I betaversionen kan du nu vidarebefordra AEM-loggar till Amazon S3, Sumo Logic, Dynatrace och ditt eget New Relic-konto (inte till Adobe-kontot). Observera att AEM-loggar (inklusive Apache/Dispatcher) stöds för dessa loggningsmål, men inte CDN-loggar. E-post [aemcs-logforwarding-beta@adobe.com](mailto:aemcs-logforwarding-beta@adobe.com) för åtkomst.

Läs mer i [dokumentationen för vidarebefordran av loggfiler](/help/implementing/developing/introduction/log-forwarding.md).

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

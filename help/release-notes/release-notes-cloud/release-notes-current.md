---
title: Aktuell versionsinformation för  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Versionsinformation för  [!DNL Adobe Experience Manager] as a Cloud Service.
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: b4aec70b13575366c1d40ccf935481580a1fb6d8
workflow-type: tm+mt
source-wordcount: '1810'
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

Releasedatum för [!DNL Adobe Experience Manager] som [!DNL Cloud Service] aktuell funktionsversion (2025.6.0) är 26 juni 2025. Nästa version (2025.7.0) är planerad till 7 augusti 2025.

## Versionsinformation om underhåll {#maintenance}

Du hittar den senaste underhållsversionsinformationen [här](/help/release-notes/maintenance/latest.md).

<!-- 

## Release Video {#release-video}

Have a look at the February 2025 Release Overview video for a summary of the features added in the 2025.2.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3440924?quality=12&captions=swe)

-->

## [!DNL Experience Manager Assets] som en [!DNL Cloud Service] {#assets}

**Förbättrad hantering av metadataformulär i Assets View**

Nu kan du importera metadataformulär från administrationsvyn direkt till Assets-vyn. Uppdateringar som görs i dessa formulär i Assets-vyn visas automatiskt i administrationsvyn, vilket ger en konsekvent upplevelse. Den här funktionen stöder en smidig övergång till den nya vyn i Assets samtidigt som kontinuiteten bibehålls i befintliga metadatakonfigurationer.

![AI genererade metadata](/help/assets/assets/import-metadata-forms-page.png)

### Nya funktioner i Content Hub {#new-features-content-hub}

**Samlingsstyrning**

I Content Hub kan du nu [styra åtkomsten till samlingar när du skapar, så att bara behöriga användare kan visa eller hantera grupperade resurser](/help/assets/collections-content-hub.md##create-collections). Det ger bättre säkerhet, bättre samarbete, organiserad resurshantering och förenklad styrning.

>[!VIDEO](https://video.tv.adobe.com/v/3463336)


## [!DNL Experience Manager Forms] som en [!DNL Cloud Service] {#forms}



### Funktioner för förhandsversioner

* [Universell redigerare för adaptiva Forms- och formulärfragment](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md): Den universella redigeraren har nu stöd för att skapa både adaptiva Forms och återanvändbara formulärfragment. Man kan visuellt skapa blanketter, konfigurera skicka-åtgärder och lägga in reCAPTCHA-validering i en förenklad WYSIWYG-miljö. Detta snabbar upp framtagningen av blanketter, ger bättre enhetlighet och förbättrar skyddet mot skräppost och automatiskt missbruk.

* [Generera och synkronisera AFP-återgivningar från adaptiv Forms](/help/forms/document-generation-afp-api.md): Med API:t för AFP-utdatasynkronisering kan administratörer och användare generera AFP-utdata (Advanced Function Presentation) från adaptiv Forms och synkronisera utdata med externa system eller lagringsplatser. AFP är ett högpresterande dokumentformat som är optimerat för utskrift och ofta används i storskaliga företagsmiljöer.

* [SharePoint-dokumentbibliotek - Spara bifogade filer med originalfilnamn](/help/forms/connect-forms-to-sharepoint-document-library.md#connect-an-adaptive-form-to-microsoft-sharepoint-document-library): Du kan nu välja att spara bifogade filer med sina ursprungliga filnamn när du lagrar dem i ett SharePoint-dokumentbibliotek. Den här förbättringen gör det enklare att identifiera och hantera överförda filer.

* **Regelredigeraren**:
   * [Binärt villkor med klickningshändelse i &quot;When&quot;-sats](/help/forms/rule-editor-core-components-events-operators.md#available-operator-types-and-events-in-rule-editor): Regelredigeraren tillåter nu att en knappklickningshändelse (_Är klickad_) kombineras med andra villkor i &quot;When&quot;-satsen. Detta ger mer exakt kontroll över regelkörningen baserat på användarinteraktion och andra faktorer. Obs! Om du använder flera villkor måste klickhändelsen vara det första villkoret som anges.
   * [Valideringsvillkor för fält och paneler](/help/forms/rule-editor-core-components-usecases.md): Regelredigeraren innehåller nu villkoren _IsValid_ och _IsNotValid_ . Med dessa kan du kontrollera valideringsstatusen för specifika fält eller hela paneler (inklusive layouter som Vågräta flikar, Lodräta flikar, Dragspel och Guider), vilket underlättar formulärnavigering och användarupplevelse baserat på valideringsresultat.
* [Förbättrad scopehantering för SharePoint-listor](/help/forms/connect-forms-to-sharepoint-list.md): SharePoint-webbplatser har nu stöd för alla hanterade sökvägar, till exempel /sites och /teams. Den här förbättringen möjliggör en bredare integrering över olika SharePoint webbplatsstrukturer, vilket ger större flexibilitet när det gäller att ansluta till organisationsinnehåll.
* [Stöd för att spara postdokument i SharePoint-lista](/help/forms/generate-document-of-record-core-components.md#bind-adaptive-form-components-with-template-fields): Forms som har skapats med en SharePoint listbaserad formulärdatamodell (FDM) kan nu spara postdokumentet (DoR) i SharePoint-listor genom att konfigurera fältegenskapen Dokumentreferens för postbindning. Den här förbättringen möjliggör smidig integrering av formulärdata och dokument som stöds med SharePoint-lagring.

### Tidiga åtkomstfunktioner i AEM Forms {#forms-new-early-access-features}

Programmet AEM Forms Early Access Program ger dig en unik möjlighet att få exklusiv tillgång till de senaste innovationerna och hjälper dig att utveckla dem.

Den här versionsinformationen innehåller en lista över de innovationer som levererats i den aktuella versionen. En fullständig lista över de innovationer som är tillgängliga under Tidig åtkomst-programmet finns i [AEM Forms Tidig åtkomst-programdokumentation](/help/forms/early-access-ea-features.md).

#### Adobe Experience Platform (AEP)-integrering med Forms

* [Integrering av AEM Forms med Adobe Experience Platform](/help/forms/aem-forms-aep-connector.md): AEM Forms till Adobe Experience Platform Connector möjliggör sömlös integrering mellan adaptiv Forms och Adobe Experience Platform. Med den här funktionen kan formulärdata mappas till XDM-scheman och skickas direkt till AEP i realtid. Det effektiviserar datainhämtningen för användning av personalisering och aktivering i olika Adobe Experience Cloud-lösningar.

## [!DNL Experience Manager] som en [!DNL Cloud Service]-grund {#foundation}

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

**Java 11-miljön** är nu föråldrad och de flesta miljöer har redan uppgraderats till den mer prestandaanpassade **Java 21-miljön**.

Om din miljö inte kunde uppgraderas på grund av beroenden som inte stöds (se [Java 21-körningskrav](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements)), bör du ha fått ett e-postmeddelande från Adobe med specifika nästa steg. Kontrollera att alla nödvändiga uppdateringar är slutförda senast den **28 augusti 2025** så att miljön kan uppgraderas utan avbrott.

Obs! Körningsversionen är en annan än den version koden har. Vi rekommenderar att du bygger med Java 21, men Java 11-byggen stöds fortfarande för tillfället. Ett separat meddelande om borttagning av Java 11-byggen kommer att delas i framtiden.

### Tillämpning av konfigurationspolicy för AEM Java-loggar {#logconfig-policy}

Som framgår av versionsinformationen för april måste AEM Java-loggarna följa ett standardformat för att säkerställa tillförlitlig övervakning i alla kundmiljöer. Anpassade loggkonfigurationer, t.ex. ändringar i loggformatering, utdatafiler eller standardloggnivåer, stöds inte längre. Loggar måste vara dirigerade till standardfilerna och standardloggnivåerna för AEM-produktkoden måste bevaras. Mer information finns i artikeln [Loggning](/help/implementing/developing/introduction/logging.md#configuration-loggers).

Med början i **slutet av augusti** kommer alla anpassade loggningsåsidosättningar som inte stöds att ignoreras. Baserat på vår analys kommer de flesta kunder inte att påverkas och Adobe har kontaktat kunder vars nuvarande konfiguration kan påverkas.

Granska och uppdatera alla processer som är beroende av anpassat loggningsbeteende. Till exempel:

* Om ditt system för vidarebefordring av loggar förväntar sig ett anpassat loggformat kan du behöva justera dina regler för inmatning.
* Om du tidigare har minskat loggens utförlighet genom att ändra loggnivåerna bör du tänka på att en återställning till standardnivåerna kan öka loggvolymen.

### Standardrensning av äldre versioner och granskningsloggar {#mt-defaults}

För närvarande har innehållsversioner och granskningsloggar associerade *rensningsunderhållsaktiviteter* inaktiverats som standard och inga data tas bort om de inte uttryckligen konfigureras.

Om du vill optimera databasprestanda från och med **början av juli 2025** aktiveras rensning som standard enligt följande riktlinjer:

#### Innehållsversioner {#mt-content}

* **Nya miljöer** (skapas efter ett kommande datum (kommer att meddelas senare)
   * Versioner som är äldre än **30 dagar** tas regelbundet bort.
   * De senaste fem versionerna under de senaste 30 dagarna bevaras tillsammans med den senaste versionen och den aktuella versionen, oavsett ålder.

* **Befintliga miljöer** (skapades före detta kommande datum):
   * Versioner som är äldre än **7 år** tas regelbundet bort.
   * Alla versioner under de senaste 7 åren bevaras.
   * Detta höga standardtröskelvärde förhindrar oavsiktlig borttagning av senaste data. Vi rekommenderar dock att du konfigurerar lägre värden för att optimera databasens prestanda.

* Du kan ändra dessa standardvärden med hjälp av YAML-konfigurationen, som distribueras med konfigurationsflödet.

#### Granskningslogg {#mt-auditlogs}

* **Nya miljöer** (skapas efter ett kommande datum, som kommuniceras separat):
   * Replikerings-, DAM- och sidgranskningsloggar som är äldre än **7 dagar** tas regelbundet bort.
   * Alla händelser loggas som standard.

* **Befintliga miljöer** (skapades före detta kommande datum):
   * Replikerings-, DAM- och sidgranskningsloggar som är äldre än **7 år** tas regelbundet bort.
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

Vi har ett begränsat antal möjligheter, antingen för AEM Publish Delivery eller för Edge Delivery Services-projekt, för produktionssajter. Om du är intresserad av att delta eller vill veta mer kan du skicka ett e-postmeddelande till [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) med en kort beskrivning av ditt användningsfall.

### CDN-konfiguration för Edge Delivery Services (Beta-programmet) {#cdn-eds-beta}

Adobe-hanterad CDN erbjuder flexibla konfigurationsalternativ, vilket beskrivs i artikeln [Konfigurera pipeline](/help/operations/config-pipeline.md#configurations).

Distribuera nu en konfigurationsprocess i en betaversion för funktioner som väljare av CDN-ursprung, svar- och begäranomvandlingar med mera. Kontakta [aemcs-cdn-config-adopter@adobe.com](mailto:aemcs-cdn-config-adopter@adobe.com) med information om ditt användningsfall.

### AEM Log-Forwarding to More Destinations (Beta Program) {#log-forwarding-beta}

Medan loggar kan hämtas från Cloud Manager tycker många att det är bra att strömma dessa loggar till ett önskat loggningsmål. AEM har redan stöd för AEM- och CDN-loggvidarebefordran till Azure Blob Storage, Datadog, HTTPS, Elasticsearch (och OpenSearch) och Splunk. Den här funktionen är konfigurerad på ett självbetjäningssätt och distribueras med Config Pipeline.

I betaversionen kan du nu vidarebefordra AEM-loggar till Amazon S3, Sumo Logic och ditt eget New Relic-konto (inte till Adobe-kontot). Observera att AEM-loggar (inklusive Apache/Dispatcher) stöds för dessa loggningsmål, men inte CDN-loggar. E-post [aemcs-logforwarding-beta@adobe.com](mailto:aemcs-logforwarding-beta@adobe.com) för åtkomst.

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

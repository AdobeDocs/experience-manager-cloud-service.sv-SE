---
title: Aktuell versionsinformation för  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Versionsinformation för  [!DNL Adobe Experience Manager] as a Cloud Service.
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: 31fac8e421e58146977222d699bac1c7cf3ee4e5
workflow-type: tm+mt
source-wordcount: '1713'
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

Releasedatum för [!DNL Adobe Experience Manager] som [!DNL Cloud Service] aktuell funktionsversion (2025.4.0) är 24 april 2025. Nästa version (2025.5.0) är planerad till 5 juni 2025.

## Versionsinformation om underhåll {#maintenance}

Du hittar den senaste underhållsversionsinformationen [här](/help/release-notes/maintenance/latest.md).

<!-- 

## Release Video {#release-video}

Have a look at the February 2025 Release Overview video for a summary of the features added in the 2025.2.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3440924?quality=12&captions=swe)

-->

## [!DNL Experience Manager Sites] som en [!DNL Cloud Service] {#sites}

### Nya funktioner i Experience Manager Sites {#enhancements-sites}

**Nytt gränssnitt för administratör för innehållsfragmentmodell**

När du sedan fyller i listan över nya användargränssnitt på klientsidan när du arbetar med AEM Content Fragments finns nu ett nytt administratörsgränssnitt tillgängligt för innehållsfragmentmodeller. Det nya användargränssnittet ger en ren och modern listvy som gör det möjligt att söka efter modeller med filter, och som visar modelltaggar och vilka innehållsfragment som finns och som baseras på en viss modell. Dokumentation finns [här](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md).

## [!DNL Experience Manager Assets] som en [!DNL Cloud Service] {#assets}

### Dynamiska media (Scene7) {#dynamic-media-scene7}

**Dynamiska media (Scene7) stöds inte i Förbättrade säkerhetsmiljöer**

Dynamic Media (Scene7) på AEM as a Cloud Service är inte HIPAA-klart och kan inte användas i AEM-miljöer där Förbättrat skydd är aktiverat.

Från och med AEM as a Cloud Service-versionen från april 2025 förhindrar en teknisk begränsning att Dynamic Media (Scene7) konfigureras i miljöer med förbättrat skydd. Därför är kortet **Dynamisk mediekonfiguration** under **Verktyg** > **Molntjänster** inte längre synligt i dessa miljöer.

Dessutom bör kunder som använder AEM 6.5 vara medvetna om att stacken Dynamic Media (Scene7) inte är HIPAA-klar.

### Dynamic Media Classic {#dynamic-media-classic}

**Rapportering**

Fliken Bandbredd i Dynamic Media Classic rapportkontrollpanel stöds inte längre från och med april 2025.

Se [Bandbredd och lagring, rapporttyper](https://experienceleague.adobe.com/sv/docs/dynamic-media-classic/using/setup/administration-setup#types-of-reports).


## Nya funktioner i Assets View {#new-features-assets-view}

**Resursrelationer**

Assets View har nu stöd för att visa och redigera resursrelationer på en förenklad resurspanel. Lägg enkelt in relationer som Source och Derivative i materialet så att användarna kan hitta relevant hjälteinnehåll effektivare.

![Exempel på Assets-relation](/help/assets/assets/asset-relations-example.png)

**Jämför versioner av en resurs**

Nu kan du snabbt välja och jämföra vilken version av en mediefil som helst med den senaste versionen i Assets-vyn.

![jämför versioner av resurs](/help/assets/assets/version-compare2.png)

## [!DNL Experience Manager Forms] som en [!DNL Cloud Service] {#forms}

### Funktioner för förhandsversioner

* [Universell redigerare - Formulärfragment](/help/edge/docs/forms/universal-editor/creating-form-fragments.md): Nu kan du skapa och återanvända formulärfragment för adaptiv Forms med den universella redigeraren. Dessa fragment är återanvändbara formuläravsnitt (t.ex. kontaktuppgifter, tillståndsfält) som kan byggas en gång och tillämpas på flera formulär. Den här funktionen effektiviserar formulärframtagningen, säkerställer enhetlighet och förbättrar redigeringseffektiviteten.

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

Integreringsfunktioner mellan Forms och AEP finns nu tillgängliga för användare som är tidiga.

## CIF Add-on {#cloud-services-cif}

### Förbättringar {#enhancements-cif}

* Lägga till val av produktvariant för CIF produktreferenstyp
* [Experimentell]: JSON+LD i CIF Core Components i PDP:er
* [Experimentell]: CIF möjlighet att rensa cache

### Felkorrigeringar {#bug-fixes-cif}

* Åtgärda sökproblem i produktfält
* Produkt-URL-formatet fungerar inte som förväntat för #variant_sku
* Det går inte att lägga till fler än 20 SKU:er i produktlistekomponenten

## [!DNL Experience Manager] som en [!DNL Cloud Service]-grund {#foundation}

### OpenAPI-baserade API:er {#open-apis}

Utvecklare kan integrera AEM som Cloud Service-funktioner i sina egna program och verktyg. Nya AEM as a Cloud Service-API:er följer OpenAPI-specifikationen och har som mål att vara konsekventa, väldokumenterade och användarvänliga. Autentiseringsuppgifter för slutpunkter som kräver autentisering genereras genom att skapa Adobe Developer Console-projekt och ha stöd för OAuth Server-to-Server, Web App och Single Page App (SPA).

[Se den fullständiga listan](https://developer.adobe.com/experience-cloud/experience-manager-apis/#openapi-based-apis) med OpenAPI-baserade API:er, [läs mer](/help/implementing/developing/open-api-based-apis.md) och prova en [heltäckande självstudiekurs](https://experienceleague.adobe.com/sv/docs/experience-manager-learn/cloud-service/aem-apis/openapis/invoke-api-using-oauth-s2s) som visar konfiguration och användning.

I den här videon får du lära dig hur du konfigurerar ett autentiserat API för senare användning:

>[!VIDEO](https://video.tv.adobe.com/v/3457510?quality=12&learn=on)

### CDN-konfigurationsrelaterade förbättringar {#cdn-enhancements}

Adobe-hanterad CDN erbjuder flexibla konfigurationsalternativ, vilket beskrivs i artikeln [Konfigurera pipeline](/help/operations/config-pipeline.md#configurations). Här är några nya funktioner:

#### Inkludera ytterligare egenskaper i CDN-loggar {#props-in-cdnlogs}

Detta är användbart för scenarier som felsökning och dataanalys. Du kan inkludera mer information i CDN-loggarna utöver standardegenskaperna genom att ange åtgärden `logProperty` i [begäran- och svarsomvandlingar](/help/implementing/dispatcher/cdn-configuring-traffic.md#request-transformations).

#### Region, Kontinent och Organisationsegenskaper som Matchningsvillkor {#matching-conditions}

CDN-reglerna kan nu matchas baserat på region, kontinent och organisation för användning som blockerar trafik och omdirigeringar. `clientRegion` och `clientContinent` utökar det `clientCountry` som redan stöds för att matcha baserat på geografi, medan `clientAsName` och `clientAsNumber` matchar autonoma system för att identifiera stora Internet-leverantörer, företag eller molnleverantörer. Läs mer om de här [nyexponerade begäranegenskaperna](/help/security/traffic-filter-rules-including-waf.md#condition-structure).

#### Ange cookie-värde {#cookie-attributes}

Du kan ange cookie-attribut i [svarsomvandlingar](/help/implementing/dispatcher/cdn-configuring-traffic.md#response-transformations).

### Stöd för Java 21 {#java21}

Från och med januariversionen kan du skapa kod med Java 21 och Java 17. Du får tillgång till nya funktioner som mönstermatchning, fasta klasser och olika prestandaförbättringar. Konfigurationssteg, inklusive uppdatering av projekt- och biblioteksversioner för Maven, finns i artikeln [Byggmiljö](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#using-java-support).

Den mer prestandaanpassade Java 21 **runtime** distribueras automatiskt när en Java 17- eller 21-version upptäcks. Adobe rekommenderar dock att du går med i Java 21-miljön för miljöer som byggts med Java 11 genom att skicka ett e-postmeddelande till [aemcs-java-adopter@adobe.com](mailto:aemcs-java-adopter@adobe.com). Läs mer om [Java 21-körningskrav](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements).

>[!IMPORTANT]
>
> Java 21 **runtime** distribuerades till dina dev/RDE-miljöer i februari. Den kommer att användas i dina scen-/produktionsmiljöer den 28 och 29 april **.** Observera att **byggkoden** med Java 21 (eller Java 17) är oberoende av Java 21-miljön - du måste vidta åtgärder explicit för att skapa kod med Java 21 (eller Java 17).

### Tillämpning av AEM konfigurationsprincip för loggning {#logconfig-policy}

För att säkerställa effektiv övervakning av kundmiljöer måste AEM Java-loggarna ha ett konsekvent format och bör inte åsidosättas av anpassade konfigurationer. Loggutdata måste vara dirigerade till standardfilerna. För AEM-produktkod måste standardloggnivåer bevaras. Du kan dock justera loggnivåerna för kundutvecklad kod.

Därför bör ändringar inte göras i följande OSGi-egenskaper:
* **Konfiguration av Apache Sling-logg** (PID: `org.apache.sling.commons.log.LogManager`) — *alla egenskaper*
* **Konfiguration av loggningsloggare för Apache Sling** (Factory PID: `org.apache.sling.commons.log.LogManager.factory.config`):
   * `org.apache.sling.commons.log.file`
   * `org.apache.sling.commons.log.pattern`

I mitten av maj kommer AEM att tillämpa en policy där anpassade ändringar av dessa egenskaper ignoreras. Granska och justera processerna i efterföljande led. Om du till exempel använder funktionen för vidarebefordran av loggar:
* Om loggningsmålet förväntar sig ett anpassat (icke-standard) loggformat, kan du behöva uppdatera dina regler för inmatning.
* Om ändringar i loggnivåer minskar loggens utförlighet bör du vara medveten om att standardloggnivåerna kan leda till en avsevärd ökning av loggvolymen.

### AEM Log Forwarding to More Destinations - Beta Program {#log-forwarding-earlyadopter}

I betaversionen kan du nu vidarebefordra AEM-loggar till New Relic (med HTTPS), Amazon S3 och Sumo Logic. Observera att AEM-loggar (inklusive Apache/Dispatcher) stöds, men inte CDN-loggar. E-post [aemcs-logforwarding-beta@adobe.com](mailto:aemcs-logforwarding-beta@adobe.com) för åtkomst.

Medan loggar kan hämtas från Cloud Manager tycker många att det är bra att strömma dessa loggar till ett önskat loggningsmål. AEM har redan stöd för (GA) AEM- och CDN-loggvidarebefordran till Azure Blob Storage, Datadog, HTTPS, Elasticsearch (och OpenSearch) och Splunk. Den här funktionen är konfigurerad på ett självbetjäningssätt och distribueras med Config Pipeline.

Läs mer i [dokumentationen för vidarebefordran av loggfiler](/help/implementing/developing/introduction/log-forwarding.md).

### Edge Computing - Request for Feedback! {#edge-computing-feedback}

Edge datoranvändning för databearbetning närmare webbläsaren, vilket har bl.a. kortare svarstider. Adobe vill gärna veta om du tycker att den här tekniken är användbar för AEM Publish Delivery och Edge Delivery Services. Dessutom kan du tala om för oss vad du tänkt dig när du använder den som indata i produktfärdplanen.

Några möjliga användningsexempel:

* Autentisering med en IdP för att ge åtkomst till innehåll
* Personalization genom att återge dynamiskt innehåll baserat på geopositionering, enhetstyp, användarattribut osv.
* Avancerad bildbehandling
* Mittprogram mellan CDN och ett ursprung
* Ett lager mellan webbläsaren och ett tredjeparts-API, kanske för att formatera om API-svaret
* Samla in data från flera källor för att göra det enklare för klientwebbläsaren att återge dem

Mejla [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) med frågor och kommentarer!

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

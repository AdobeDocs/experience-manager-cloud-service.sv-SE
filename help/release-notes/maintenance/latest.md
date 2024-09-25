---
title: Aktuell underhållsversionsinformation för  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Aktuell underhållsversionsinformation för  [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 22f8ffc3e3acec9846a2f868be48195ca62df88b
workflow-type: tm+mt
source-wordcount: '1343'
ht-degree: 0%

---


# Versionsinformation om underhåll {#maintenance-release-notes}

I följande avsnitt beskrivs de tekniska versionsinformationen för den aktuella underhållsutgåvan av Experience Manager as a Cloud Service.

## Utgåva 17964 {#release-17964}

Nedan sammanfattas de kontinuerliga förbättringarna av underhållsreleasen 17964, som offentliggjordes den 25 september 2024. Den tidigare underhållsversionen var version 17689.

Funktionsaktiveringen i 2024.10.0 kommer att innehålla alla funktioner som finns i den här underhållsversionen. Mer information finns i [Experience Manager Releases Roadmap](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

### Förbättringar {#enhancements-17964}

* ASSETS - 37750: [Prioritet 4] [GraphQL] Stöd för URL:er för DM-scener7: bildsmarta beskärningar.
* CQ - 4354583: [AEMaaCS] Skicka översättningsprocesshändelser via Adobe Pipeline.
* CQ - 4357642: Uppdatera MSFT-autentiseringsuppgifter i OOTB Connector.
* CQ - 4358217: Deserialisera begärandetexten från begärandeentiteten.
* CQ - 4358342: Registrera RequestProcessors på endast en HTTP-metod.
* FORMS - 10781: Förbättra regelredigeraren för att skapa regler för nästa/föregående objekt på en panel.
* FORMS - 14595: [Webbläsarlös funktion] Värden saknas i DoR när förfyllda data används för att beräkna DoR-återgivning utan webbläsare.
* FORMS - 15619: AEM Forms uppdaterade översättningsverktyg.
* FORMS - 16113: [Adobe Sign]Det går inte att uppdatera avtalsstatus för en annan användare.
* FORMS - 16155: [Regelredigeraren] Implementera asynkron funktion.
* GRANITE - 53872: Lägg till nya miljövariabler för IMS-klient-ID.
* SITES - 23738: Release Core Components 2.27.0.
* SITES - 16610: Content Fragments: Get launch details endpoint.
* SITES - 16614: Content Fragments: Rebase Launch endpoint.
* SITES - 16615: Content Fragments: Promote Launch endpoint.
* SITES - 24215: Content Fragments: Implementera slutpunkt för Get Launch sources.
* SITES - 20336: Content Fragments: Imimprove validation when when deleting a Content Fragment Model.
* SITES - 21090: Content Fragments: Add support for fractional min/max values for number fields
* SITES - 21658: Content Fragments: Upgrade to use UUID-references.
* SITES - 23054: Content Fragments: Copy Content Fragment Models.
* SITES - 23264: Content Fragments: Create a static schema of a model.
* SITES - 23265: Content Fragments: Expose the static schema of a model through the UI schema GET endpoint.
* SITES - 23266: Content Fragments: Ability to add constraints to Content Fragment Models.
* SITES - 23778: Content Fragments: Search Content Fragment Models should allow searching for models that has never been published.
* SITES - 23335: Content Fragments: Add support for external asset references.
* SITES - 24626: Content Fragments: RTC: Permissions for UUID migration: 2.
* SITES - 24786: Content Fragments: Enhancements for `referencesTree` endpoint.
* SITES - 24833: Content Fragments: Remove the validation of HTML input into mot a list of allowed HTML tags.
* SITES - 23380: GraphQL: använd rätt API för att läsa metadata för resurser.
* SITES - 22864: [Edge Delivery] Universal editor with new AEM content structure integration H2 2024.
* SITES - 23584: Foundation component tests failed on Java 17.
* SITES - 23662: Händelse: Användare som utlöser en publiceringsbegäran kan inte extraheras från JCR-loggsatser i serverloggar.
* SITES - 23301: Lägg till stöd för att starta ett nytt arbetsflöde för att skapa mappstrukturer när du skapar översättningar av innehållsfragment.
* SITES - 23336: Content Fragments: Add support for external asset references
* SITES - 24091: MSM-innehållspaketet har delats: master.
* SITES - 24114: isSourceRenderCondition: Reducera felloggmeddelande till DEBUG.
* SITES - 24166: Remote assets reduction for Touch-UI editor.
* SITES - 24409: Registrera alla begärande processorer på endast en HTTP-metod.
* SITES - 25008: Improved handling of PersistenceExceptions and permissions problems.
* SITES - 24821: [Xwalk] Använd aem.page / aem.live som standard.

### Åtgärdade problem {#fixed-issues-17964}

* CQ - 4356887: Inkonsekvens i översättningsprojektstatus för Akamai Technologies Inc.
* CQ - 4357878: Översättningsramverket anger inte feltillstånd vid översättning av leverantörsfel.
* CQ - 4358028: Det gick inte att skapa projektet om en miniatyrbild har överförts.
* CQ - 4358290: Målinställningen fungerar INTE på den publicerade sidan.
* FORMS - 13173: Justering av nedrullningsbar lista i Adaptiv form > Regelredigerare > Släpp objektfält.
* FORMS - 13873: AFv2: (&quot;-&quot;) i komponentens namn resulterar i att reglerna inte fungerar.
* FORMS - 14340: Fel vid instansiering av FormsAndDocumentOmniSearchHandler och CloudStorageSubmitActionInserter.
* FORMS - 15363: Visat namn i regelredigeraren.
* FORMS - 15381: Förbättring av användargränssnittet i Scope-meddelandet för auktorisering.
* FORMS - 15595: AEM TnC Component Consent Text line break issue.
* FORMS - 15623: AEMaaCS Forms - alternativ för att uppdatera flera tabeller i Dynamics med en POST.
* FORMS - 15682: AEM Forms - Det går inte att binda DOR till Dynamics FDM.
* FORMS - 15799: Adobe Sign GovCloud Signature page does note render in iframe.
* FORMS - 15835: Problem med att skriva om formulär-URL efter överföring.
* FORMS - 16091: Använder den omstrukturerade Binary.java.
* FORMS - 16096: Forms-användare har inte åtkomst till dialogrutan för brytpunkter.
* FORMS - 16139: Lägger till obligatorisk loggning för DoR i formulär för kärnkomponenter.
* FORMS - 6935: Den aktiva komponentens tillstånd saknar kontrastförhållande 3 till 1.
* FORMS - 7018: Tomt element får fokus.
* GRANITE - 53028: NPE i ExternalProcessPollingHandler.
* GRANITE - 53907: Det går inte att identifiera tjänstanvändaren som en superanvändare i arbetsflödet.
* SITES - 24405: Content Fragments: Extended Info for enums should be more resilient
* SITES - 23024: Content Fragments: Enumeration does not return locked: true in GET fragments.
* SITES - 23269: Content Fragments: Creating Content Fragments allows setting locked fields.
* SITES - 23337: Content Fragments: Batch endpoint with `body` failed with casting exception.
* SITES - 23474: Content Fragments: Pagination should exclude resources in Search Content Fragments.
* SITES - 23615: Content Fragments: Content Fragment copy AuthoringInfo is not updated
* SITES - 23668: Content Fragments: Patch live copy with multifield fails with 400
* SITES - 23695: Content Fragments: Tab description is not available in UiSchema
* SITES - 23704: Content Fragments: Multi-value enums not supported in _extendedInfo
* SITES - 23781: Content Fragments: Duplicate values not allowed in enumeration fields
* SITES - 24150: Content Fragments: Content Fragment Version Authoring data about creation is missing
* SITES - 24230: Content Fragments: Fix filtering after `modified` replication status in Search Content Fragment Models
* SITES - 24233: Content Fragments: Filtering med `publishedBy` kan innehålla opublicerade resurser i Search Content Fragment Models.
* SITES - 24355: Content Fragments: Live Relationship respekteras inte för mappskapade innehållsfragment
* SITES - 24816: Content Fragments: ValidationStatus messages order inconsistent.
* SITES - 23896: Eventing: More events are coming together with a Page Moved event
* SITES - 23899: Eventing: Page events are delay or not generated alls
* SITES - 23961: Eventing: Creating Content Fragment Models with references fails when configuration folder is present
* SITES - 23963: Eventing: Page deleted events (Händelser för borttagna sidor) kommer ibland inte
* SITES - 23443: GraphQL: GraphQL Cursor query inconsistent behavior.
* SITES - 10994: Ordningen för tangentbordsfokus är inte logisk.
* SITES - 16357: AEM: Button trunkeras på fliken Setup Analytics (Installationsanalys) på Sites-menyn.
* SITES - 19836: Ghost-komponenten i behållaren visas i publicerings- och förhandsvisningsinstanser.
* SITES - 22348: Sidan Översikt över Live-kopia läses inte in om de är över 100 aktiva kopior för ett projekt.
* SITES - 22960: Ostängd resurshanterare i ContentFragmentModelOmniSearchHandler.
* SITES - 23284: URL-kodning orsakar en tom dialogruta för sökvägsläsare.
* SITES - 23505: Components visar felaktiga URL:er när sidan flyttas till en annan plats.
* SITES - 23574: Det går inte att förhandsgranska/jämföra med aktuella versioner för många sidor
* SITES - 23585: Issue with Restoring Inheritance for components having cq:responsive node
* SITES - 23650: Discrecy in Incoming Links Count in AEM Author Environment
* SITES - 23659: Content Language Servlet regression orsakad av växlingen FT_* SITES - 9757
* SITES - 23759: Assets som lagts till i upplevelsefragment publiceras inte med Launches
* SITES - 24025: 302 dirigerar om AEM returnerar platshuvud med intern DNS i stället för offentlig DNS
* SITES - 24036: Investigation needed for AEM RTE Persisting Characters in ASCII Format
* SITES - 24317: Proxykonfigurationen fungerar inte med grundläggande autentisering
* SITES - 24918: [Xwalk] korrigerar 504 fel som returneras då och då när en dedikerad IP-utgång används.

### Kända fel {#known-issues-17964}

* FORMS - 15818: Komponentbeskrivningsposten `OSGI-INF/com.adobe.aemfd.docmanager.impl.*.xml` hittade inte programsatser i serverloggar. Det här är ofarliga loggsatser.

### Föråldrade funktioner och API:er {#deprecated-17964}

Observera att vi håller på att uppdatera `com.day.cq.wcm.api` och med den aktuella versionen har vi markerat `@Deprecated` som några av dess metoder och klasser. Dessa kommer att tas bort i framtida versioner, så överväg att byta till de föreslagna alternativen om du använder något av dem.

Inaktuella och borttagna funktioner och API:er i AEM as a Cloud Service beskrivs i dokumentet [Inaktuella och Borttagna funktioner och API:er](/help/release-notes/deprecated-removed-features.md).

### Säkerhetskorrigeringar {#security-17964}

AEM as a Cloud Service strävar efter att optimera säkerheten och prestandan för din plattform. Denna underhållsrelease åtgärdar 16 identifierade sårbarheter, vilket stärker vårt engagemang för robust systemskydd.

### Inbäddade tekniker {#embedded-tech-17964}

| Teknik | Version | Länk |
|---|---|---|
| AEM Oak | 1.68.0 | [Oak API 1.68.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.68.0/index.html) |
| AEM SLING API | 2.27.6 | [API:t för Apache Sling 2.27.6 ](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTML | 1.4.24-1.4.0 | [Språkspecifikation för HTML-mall](https://github.com/adobe/htl-spec) |
| Grundläggande komponenter i AEM | 2.27.0 | [AEM WCM-kärnkomponenter](https://github.com/adobe/aem-core-wcm-components) |

---
title: Aktuell underhållsversionsinformation för  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Aktuell underhållsversionsinformation för  [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 6fa6fc9015624bec9113a198285531a3bdd7e29c
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 0%

---


# Versionsinformation om underhåll {#maintenance-release-notes}

I följande avsnitt beskrivs de tekniska versionsinformationen för den aktuella underhållsutgåvan av Experience Manager as a Cloud Service.

## Utgåva 18175 {#release-18175}

Nedan sammanfattas de kontinuerliga förbättringarna av underhållsutgåvan 18175, som offentliggjordes den 10 oktober 2024. Den tidigare underhållsversionen var version 17964. Utgåva 18099 har gjorts privat på grund av ett problem.

Funktionsaktiveringen i 2024.10.0 kommer att innehålla alla funktioner som finns i den här underhållsversionen. Mer information finns i [Experience Manager Releases Roadmap](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

### Förbättringar {#enhancements-18175}

* ASSETS-38322: Aktivera händelsen http-begäran för AEM.
* ASSETS-41448: Uppdatera paketet auth.ims som stöd för FI till gruppmappningar.
* ASSETS-41684: Lägg till OOB OSGI-konfigurationer för att definiera FI för gruppmappning för Assets, Foundation, Sites och Forms.
* ASSETS-43015: Uppdatera till det senaste paketet med auth.ims.
* CQ-4356633: Lägg till extra tecken i verktygstipset Endast innehåll.
* GRANITE-50948: Integrera databastjänst i AEM Support för databastjänster.
* GRANITE-52454: Lägger till supporthjälpen 0.1.2.
* GRANITE-52454: Uppgraderar supporthjälpen GRANITE-52454 för uppgradering av supporthjälpen så att den använder den senaste versionen för AEMaaCS.
* GRANITE-53287: Uppdaterar testversionen av integrering av säkerhetsbehörighet.
* GRANITE-53485: Support Service Principal authentication for replication Azure Blob Storage.
* GRANITE-53514: Treeactivation updated to version 1.0.26.
* GRANITE-53870: Skapa en intern mekanism som hoppar över den maximala JVM-versionskontrollen för snabbstarten.
* GRANITE-53914: Åtgärda plattformstest med Java 17 Updated module version.
* GRANITE-53966: Använd en separat trådpool för innehållsdistribution.
* GRANITE-54006: update Jackson to 2.17.2.
* GRANITE-54038: Lägg till Creative Cloud Enterprise IMS-klienten i AEM IMS-klientens tillåtelselista.
* GRANITE-54054: Miljövariabel för com.adobe.granite.database.impl.SystemUserValidation warnOnly.
* GRANITE-54266: Search Suggestor-tjänsten saknas i Production SDK.
* GRANITE-54274: Acceptera Firefly IMS-klient.
* GRANITE-54300: Uppdatera Oak till den senaste offentliga versionen (1.70.0).
* GUIDES-19069: Add guidesPeerLinkIndex for aem guides add on.
* SITES-23584: Fix failed test for Foundation component on Java 17.
* SKYOPS-69768: SlingModels avserialiserar inte ResourceResolvers.
* SKYOPS-76378: Förbättra trådsäkerheten för registrering/avregistrering av ResourceBundle i i18n.
* SKYOPS-79285: Uppdatera Sling XSS till 2.4.2.
* SKYOPS-82383: Exponera konverterings-merge-analyze-resultatet för helm-values i kommandokörningsbeskrivningen.
* SKYOPS-84810: Hoppa över körning av&quot;40-initialize-publish.sh&quot; vid start för RDE.
* SKYOPS-84951: Korrigera genereringskod för kontrollsumma för muterbart innehåll.
* SKYOPS-85335: Uppdatera org.apache.sling.jcr.repoint till 1.1.52.
* SKYOPS-85336: Uppdatera Sling Commons Threads till 3.3.0.
* SKYOPS-86329: Uppdatera versioner av plattformstest för stöd för java 21 sdk.

### Åtgärdade problem {#fixed-issues-18175}

* CNTBF-298: Ta bort jcr:uid från CC-exporterade paket.
* SKYOPS-83910: Åtgärda problem med samtidighet i SKYOPS-82371.
* GRANITE-52876: Uppdatering till com.adobe.granite.ui.content 0.8.1448.
* GUIDES-14445: Generering av ursprungliga PDF misslyckas med ett fel som relaterar till hämtning av beroenden för Node.js.
* GUIDES-16961: Titeln med `<conref>` kan inte matchas på panelerna Baslinje och Översättning i webbredigeraren.
* GUIDES-17283: När du väljer alternativet **Använd metadata som lagts till i topicmeta** sprids inte metadataegenskaperna i dokumentägarna för utdata från Native PDF.
* GUIDES-17793: Det refererade PDF aktiveras inte från **Massaktiveringen av Publish Dashboard** under gruppaktiveringen av publicerat innehåll.

Mer information om de nya och förbättrade guiderefunktionerna och problemen som har åtgärdats i den här versionen finns i [Experience Manager Guides-lanseringens färdplan](https://experienceleague.adobe.com/en/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

### Kända fel {#known-issues-18175}

* FORMS-15818: Komponentbeskrivningsposten `OSGI-INF/com.adobe.aemfd.docmanager.impl.*.xml` hittade inte programsatser i serverloggar. Det här är ofarliga loggsatser.

### Föråldrade funktioner och API:er {#deprecated-18175}

Inaktuella och borttagna funktioner och API:er i AEM as a Cloud Service beskrivs i dokumentet [Inaktuella och Borttagna funktioner och API:er](/help/release-notes/deprecated-removed-features.md).

Här följer en sammanfattning av nyligen borttagna funktioner eller funktioner som håller på att tas bort.

#### JavaScript Use API {#javascript-use-api}

[API:t för JavaScript-användning](https://github.com/adobe/htl-spec/blob/master/SPECIFICATION.md#42-javascript-use-api) är officiellt föråldrat på grund av problem som användare har med att felsöka och underhålla kod som utnyttjar API:t samt prestandabegränsningar jämfört med Java-alternativet.

Du bör gå över till [Java Use API,](https://experienceleague.adobe.com/en/docs/experience-manager-htl/content/java-use-api), som ger bättre prestanda, enklare felsökning och mer långsiktigt stöd.

#### com.day.cq.wcm.api {#com-day-cq-wcm-api}

Observera att Adobe håller på att uppdatera `com.day.cq.wcm.api`. Vissa av dess metoder och klasser har markerats som `@Deprecated` i den aktuella versionen. Dessa kommer att tas bort i framtida versioner. Överväg att byta till de föreslagna alternativen.

#### org.apache.jackrabbit.oak.plugins.blob {#org.apache.jackrabbit.oak.plugins.blob}

* GRANITE-54165: Borttagen org.apache.jackrabbit.oak.plugins.blob i publikt API.

### Säkerhetskorrigeringar {#security-18175}

AEM as a Cloud Service strävar efter att optimera säkerheten och prestandan för din plattform. Denna underhållsrelease åtgärdar två identifierade sårbarheter, vilket stärker vårt engagemang för robust systemskydd.

### Inbäddade tekniker {#embedded-tech-18175}

| Teknik | Version | Länk |
|---|---|---|
| AEM Oak | 1.70.0 | [Oak API 1.70.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.70.0/index.html) |
| AEM SLING API | 2.27.6 | [API:t för Apache Sling 2.27.6 ](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTML | 1.4.24-1.4.0 | [Språkspecifikation för HTML-mall](https://github.com/adobe/htl-spec) |
| Grundläggande komponenter i AEM | 2.27.0 | [AEM WCM-kärnkomponenter](https://github.com/adobe/aem-core-wcm-components) |

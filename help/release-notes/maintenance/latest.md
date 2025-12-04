---
title: Aktuell information om underhållsversionen av  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Aktuell information om underhållsversionen av  [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 68444ac15513bad7c1eaee97c474e21d36992d49
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 1%

---


# Versionsinformation om underhåll {#maintenance-release-notes}

I följande avsnitt beskrivs den tekniska versionsinformationen för den aktuella underhållsversionen av Experience Manager as a Cloud Service.

## Version 23482 {#23482}

Nedan sammanfattas de kontinuerliga förbättringarna av underhållsutgåva 23482, som offentliggjordes den 3 december 2025. Den tidigare underhållsversionen var version 23385.

Funktionsaktiveringen i 2025.12.0 ger den fullständiga funktionsuppsättningen för den här underhållsversionen. Mer information finns i [Experience Manager Releases Roadmap](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).


### Förbättringar {#enhancements-23482}

* ASSETS-49770: Lägg till karantänmeddelanden för sökresultat efter skadlig kod.
* ASSETS-54079: Använd anpassade metadataformulär för karantänmapp.
* ASSETS-54083: Skapa schemalagd karantänrensningsmekanism.
* ASSETS-54278: Ta bort egenskapen `dam:avScanTime` från resurserna.
* ASSETS-57284: Begränsa filöverföringar till karantänmappen (inaktivera dra och släpp).
* ASSETS-57428: Dölj karantänmappen i Assets View-gränssnittet.
* ASSETS-57626: Förbättra återförsöksbeteendet för asynkrona resursjobb.
* ASSETS-57879: Lägg till sammanslagningsalternativ för asynkrona flytt-/kopieringsjobb.
* ASSETS-58099: Lägg till config för att inaktivera smarta taggar för hela miljön.
* ASSETS-58136: Implementera sidnumreringsfeedback i Search OpenAPI.
* ASSETS-59402: Lägg till asynkrona jobbslutpunkter för mappborttagnings-API: exportpaket till intern region.
* ASSETS-59966: Byt namn på gruppen Administratörer för skadlig kod till karantänadministratörer.
* ASSETS-60166: Använd VideoViewer.js i stället för iframe-baserade URL:er.
* GRANITE-61378: Felsökningsverktyget för behörigheter - API:t för ListPrincipals.
* GRANITE-63235: Fråga för att identifiera platser som använder egenskapen `cq:conf`, stöder identifiering av gamla sidor/versioner.
* SITES-30452: Innehålls-API med ASO - Titel- och beskrivningsförslag, XWalk-stöd, JSON-korrigeringsåtgärder, IMS-tjänstens huvudbindning.

### Åtgärdade problem {#fixed-issues-23482}

* ASSETS-57430: Korrigera förbearbetning av Assets View-överföring: exportera `repoapi.preprocessing`-paket, uppdatera RAPI till senaste.
* ASSETS-58190: Minska antalet gissningar som blir onödigt höga i användargränssnittet för samlingar.
* ASSETS-58866: Korrigera objektets titel/beskrivning/ID som returneras i OpenAPI-svar.
* ASSETS-58868: Korrigera sidnumrering vid sortering av fält som saknas i resurser.
* ASSETS-58920: Korrigera förbearbetning av bulkresurser som importeras.
* ASSETS-59168: Korrigera start-/sluttid för skanning med felaktig tidszon.
* ASSETS-59702: Korrigera händelseordning när resursstatusen är inställd på Ingen status.
* ASSETS-59830: asynkrona jobb som köats igen stoppades vid podavslutning.
* ASSETS-49757: Korrigeringar för händelser för sökning efter skadlig kod.
* GRANITE-61019: Korrigera `gcMonitor` som inte har meddelats vid första körningen efter att AEM startats om.
* GRANITE-62717: Korrigera lösenordshantering för `JSafe` med icke-ASCII-tecken.
* SITES-34331: Korrigera 503-timeout vid inläsning av övertäckning för utrullning för icke-adminanvändare (`cqLiveSyncCancelled index`).

### Kända fel {#known-issues-23482}

Ingen.

### Föråldrade funktioner och API:er {#deprecated-23482}

Inaktuella och borttagna funktioner och API:er i AEM as a Cloud Service beskrivs i dokumentet [Inaktuella och Borttagna funktioner och API:er](/help/release-notes/deprecated-removed-features.md).

### Säkerhetskorrigeringar {#security-23482}

AEM as a Cloud Service strävar efter att optimera säkerheten och prestandan för din plattform. Denna underhållsrelease åtgärdar fyra identifierade sårbarheter, vilket stärker vårt engagemang för robust systemskydd.

### Inbäddade tekniker {#embedded-tech-23482}

| Teknik | Version | Länk |
|---|---|---|
| AEM Oak | 1.88.0 | [Oak 1.8.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.88/index.html) |
| AEM SLING API | 2.27.6 | [API:t för Apache Sling 2.27.6 ](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [Språkspecifikation för HTML-mall](https://github.com/adobe/htl-spec) |
| Apache HTTP-server | 2.4.65 | [Apache HTTP 2.4.65](https://apache.googlesource.com/httpd/+/refs/tags/2.4.65/CHANGES) |
| Grundläggande komponenter i AEM | 2.30.2 | [AEM WCM Core Components](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14 (standard) | [Node.js-versioner som stöds](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |


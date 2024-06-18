---
title: Aktuell underhållsanvisning för [!DNL Adobe Experience Manager] as a Cloud Service.
description: Aktuell underhållsanvisning för [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: e0156c54b51eed0f729f2026c47eb93917143017
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 1%

---

# Versionsinformation om underhåll {#maintenance-release-notes}

I följande avsnitt beskrivs den tekniska versionsinformationen för den aktuella underhållsutgåvan av Experience Manager as a Cloud Service.

## Utgåva 16799 {#release-16799}

Nedan sammanfattas de kontinuerliga förbättringarna av underhållsutgåvan 16799, som offentliggjordes den 18 juni 2024. Den tidigare underhållsversionen var version 16544.

2024.6.0 Funktionsaktivering innehåller alla funktioner som finns i den här underhållsversionen. Se [Roadmap för lanseringar av Experience Manager](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) för mer information.

### Förbättringar {#enhancements-16799}

* ASSETS-31977: Förbättrade åtgärder för att flytta, kopiera och ta bort resurser.
* ASSETS-33618: Funktioner för automatisk transkription och översättning för videor i Dynamic Media.
* ASSETS-33618: Godkännandeåtgärd för ContentHub och DM och lägg till egenskaper i egenskaperna damAssetLucene.
* ASSETS-35533: Lägg till DRM- och CAI-egenskaper i index damAssetLucene.
* ASSETS-37280: Sekventiell jobbhantering för översättning när källunderrubriken (vtt) fortfarande bearbetas.
* ASSETS-37559: Förbättrad händelse för borttagning av resurser.
* ASSETS-37723: Implementera resurspublicerad händelse.
* ASSETS-37724: Implementera händelse för opublicerad resurs.
* ASSETS-38614: Förbättringar i användargränssnittet för Dela länk.
* ASSETS-39601: Tillämpa valideringsregex automatiskt på resursliveopynamnet.
* ASSETS-39454: Uppgradera till visningsprogram för 2024.5.0 i Quickstart.
* CNTBF-184: Supportsökvägar under `/conf` i innehållsomflödning.

### Åtgärdade problem {#fixed-issues-16799}

* ASSETS-37335: Redigering av sökpanel i filter avmarkerar alla rutor.
* ASSETS-38069: AEM DAM PDF Preview Issue on Timeline Filter Selection.
* ASSETS-38215: Adobe Stock-licensknappen är nedtonad i AEM as a Cloud Service for enterprise-prenumeration.
* ASSETS-38578: Felaktiga hyperlänkar i länkdelningsrapporten för resurser.
* ASSETS-38678: Visa inställningar som är brutna i Samlingsinformation.
* ASSETS-39071: Webboptimerad leverans kan generera ett undantag om den ursprungliga återgivningens mime-typ är null.
* ASSETS-39316: Sortering efter namn fungerar inte i samlingar.
* ASSETS-39377: Massimport från OneDrive kan misslyckas om du får ett baktryck från fjärr-API.
* ASSETS-39428: Renderingsproblem i gränssnittet för copyrighthantering.
* CQ-4357150: Guava i cq-content-sync bundle.
* SCRNS-4194: Ta bort beroendet av Google Guava API:er.
* SCRNS-4360: Knappen Hantera publikation och snabbpublicering saknas för icke-adminanvändare i innehållsleverantören för kanaler.
* SCRNS-4323: Hide/Disable launches from screens.html.

### Kända fel {#known-issues-16799}

Ingen.

### Ändringsmeddelande {#change-notice-16799}

* Den här versionen innehåller följande nya produktindexversioner:
   * **damAssetLucene-11**
   * **fragments-11**

  Anpassade versioner av tidigare indexversioner sammanfogas automatiskt med den nya produktindexversionen. Använd ytterligare anpassade uppdateringar för den sammanfogade versionen.

* Från och med september 2024 kommer AEM as a Cloud Service att inaktivera serialiseringen av Resurslösare via Sling Model Exporter-ramverket. Se [dokumentationen](/help/implementing/developing/hybrid/disallow-the-serialization-of-resourceresolvers-via-sling-model-exporter.md) för mer information.

### Föråldrade funktioner och API:er {#deprecated-16799}

Om du vill veta vad som är föråldrat eller borttaget i AEM as a Cloud Service kan du läsa [Föråldrade och borttagna funktioner och API:er](/help/release-notes/deprecated-removed-features.md).

### Inbäddade tekniker {#embedded-tech-16799}

| Teknik | Version | Länk |
|---|---|---|
| AEM Oak | 1.64.0 | [Oak API 1.64.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.64.0/index.html) |
| AEM SLING API | 2.27.2 | [API för Apache Sling 2.27.2](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTML | 1.4.22-1.4.0 | [HTML-mallens språkspecifikation](https://github.com/adobe/htl-spec) |
| Grundläggande komponenter i AEM | 2.25.4 | [AEM WCM-kärnkomponenter](https://github.com/adobe/aem-core-wcm-components) |

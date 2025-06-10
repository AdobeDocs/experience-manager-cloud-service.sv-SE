---
title: Aktuell information om underhållsversionen av  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Aktuell information om underhållsversionen av  [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: d3cdc3d69c0002c5b124150050f905123457331c
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 1%

---


# Versionsinformation om underhåll {#maintenance-release-notes}

I följande avsnitt beskrivs den tekniska versionsinformationen för den aktuella underhållsversionen av Experience Manager as a Cloud Service.

## Utgåva 21193 {#21193}

Nedan sammanfattas de kontinuerliga förbättringarna av underhållsutgåvan 21193, som offentliggjordes den 10 juni 2025. Den tidigare underhållsutgåvan släpptes 2005.

Funktionsaktiveringen i 2025.6.0 kommer att innehålla alla funktioner som finns i den här underhållsversionen. Mer information finns i [Experience Manager Releases Roadmap](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

### Förbättringar {#enhancements-21193}

* ASSETS-51245: Förbättrade prestanda för stora mapplistor i Touch-gränssnittet.
* ASSETS-51686: Förbättringar av massjobb, bland annat enklare jobbavbrott, förbättrad loggning och granskningsnedladdningar för större resultat.
* CQ-4360131: Förbättrat felsvar för OpenAPI-slutpunkter som gör att API-klienter kan få korrekt strukturerad felinformation.

### Åtgärdade problem {#fixed-issues-21193}

* ASSETS-41007: Borttagna resurser kan förbli synliga i Content Hub.
* ASSETS-50994: AemRequestEventFilter orsakar för hög Jetty-trådskonflikter.
* ASSETS-50155: Dubblerade metadataändringshändelser utlöstes.
* ASSETS-50716: Sortering efter titel i Assets listvy fungerar inte som förväntat.
* ASSETS-50820: Kontrollera att ogiltiga begäranden till API:t för resursrelationer avvisas korrekt med ett 400-fel.
* ASSETS-50562: API för överföring av resurser ska skapa version som standard vid namnkonflikt.
* ASSETS-50992: Assets API-slutpunkten initialUpload.json ska returnera innehållstypen för application/json.
* ASSETS-51322: Automatisk borttagning och förfallodatum för asynkrona barrikader som kvarstår oavbrutet efter ett misslyckat jobb.
* ASSETS-51809: CSV-redigeraren visade inte nyligen sparade ändringar på grund av webbläsarcachelagring.
* SITES-31678: Experience Fragments (XF) with context-aware references was not resolve the correct language root in XF Publishing API.


### Kända fel {#known-issues-21193}

Ingen.

### Föråldrade funktioner och API:er {#deprecated-21193}

Inaktuella och borttagna funktioner och API:er i AEM as a Cloud Service beskrivs i dokumentet [Inaktuella och Borttagna funktioner och API:er](/help/release-notes/deprecated-removed-features.md).

### Säkerhetskorrigeringar {#security-21193}

AEM as a Cloud Service strävar efter att optimera säkerheten och prestandan för din plattform. Denna underhållsrelease åtgärdar två identifierade sårbarheter, vilket stärker vårt engagemang för robust systemskydd.

### Inbäddade tekniker {#embedded-tech-21193}

| Teknik | Version | Länk |
|---|---|---|
| AEM Oak | 1.80.0 | [Oak API 1.80.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.80.0/index.html) |
| AEM SLING API | 2.27.6 | [API:t för Apache Sling 2.27.6 ](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [Språkspecifikation för HTML-mall](https://github.com/adobe/htl-spec) |
| Grundläggande komponenter i AEM | 2.29.0 | [AEM WCM Core Components](https://github.com/adobe/aem-core-wcm-components) |

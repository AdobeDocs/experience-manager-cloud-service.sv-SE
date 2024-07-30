---
title: Aktuell underhållsversionsinformation för  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Aktuell underhållsversionsinformation för  [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: dc7150c6ce971aa6f89fa24f7ca387cbb28db1f2
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 1%

---


# Versionsinformation om underhåll {#maintenance-release-notes}

I följande avsnitt beskrivs de tekniska versionsinformationen för den aktuella underhållsutgåvan av Experience Manager as a Cloud Service.

## Version 17258 {#release-17258}

Nedan sammanfattas de kontinuerliga förbättringarna av underhållsutgåvan 17258, som offentliggjordes den 30 juli 2024. Den tidigare underhållsversionen var version 17098.

Funktionsaktiveringen i 2024.8.0 kommer att innehålla alla funktioner som finns i den här underhållsversionen. Mer information finns i [Experience Manager Releases Roadmap](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

### Förbättringar {#enhancements-17258}

* ASSETS-31445 - Initiala Dynamic Media-mallfunktioner
* ASSETS-40399 - Uppdaterade köinställningar för automatisk DM-transkripering
* ASSETS-40873 - Tillåt att maximalt antal rader för metadataexport anges via OSGI-konfigurationen

### Åtgärdade problem {#fixed-issues-17258}

* ASSETS-30613 - Ersätt resurs tar inte bort och lägger inte till resurs i nytt leveransskikt
* ASSETS-31882 - Åtkomst till en manifestfil för direktuppspelning i författaren är förbjuden
* ASSETS-39598 - Massimport kan inte ta bort resurser med specialtecken i namnet från S3-serverdelen
* CNTBF-209 - Förbättringar av annullering av flödesjobb
* SCRNS-3762 - Förbättra playerLogger i Sequence-kanalen för att placera loggar på konsolen när du förhandsgranskar kanalen i webbläsaren
* SCRNS-4455 - Knappen Hantera publikation och Snabb Publish saknas för användare som inte är ADMIN i innehållsleverantören för kanaler
* SITES-22940 - Det går inte att visa innehållsfragment som arbetsflödets nyttolast

### Kända fel {#known-issues-17258}

Ingen

### Ändringsmeddelande {#change-notice-17258}

* Från och med september 2024 kommer AEM as a Cloud Service att inaktivera serialiseringen av resurslösare via Sling Model Exporter-ramverket. Mer information finns i [dokumentationen](/help/implementing/developing/hybrid/disallow-the-serialization-of-resourceresolvers-via-sling-model-exporter.md).

### Föråldrade funktioner och API:er {#deprecated-17258}

Inaktuella och borttagna funktioner och API:er i AEM as a Cloud Service beskrivs i dokumentet [Inaktuella och Borttagna funktioner och API:er](/help/release-notes/deprecated-removed-features.md).

### Inbäddade tekniker {#embedded-tech-17258}

| Teknik | Version | Länk |
|---|---|---|
| AEM Oak | 1.66.0 | [Oak API 1.6.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.66.0/index.html) |
| AEM SLING API | 2.27.2 | [API:t för Apache Sling 2.27.2 ](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTML | 1.4.24-1.4.0 | [Språkspecifikation för HTML-mall](https://github.com/adobe/htl-spec) |
| Grundläggande komponenter i AEM | 2.25.4 | [AEM WCM-kärnkomponenter](https://github.com/adobe/aem-core-wcm-components) |

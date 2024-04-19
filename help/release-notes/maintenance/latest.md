---
title: Aktuell underhållsanvisning för [!DNL Adobe Experience Manager] as a Cloud Service.
description: Aktuell underhållsanvisning för [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: f15b42e4012385c461b5440b92f53c4e58fb8ac2
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 2%

---

# Versionsinformation om underhåll {#maintenance-release-notes}

I följande avsnitt beskrivs den tekniska versionsinformationen för den aktuella underhållsutgåvan av Experience Manager as a Cloud Service.

## Utgåva 15977 {#release-15977}

Nedan sammanfattas de kontinuerliga förbättringarna av underhållsutgåvan 15977, som offentliggjordes den 19 april 2024. Den tidigare underhållsutgåvan släpptes 15939.

2024.4.0 Funktionsaktivering innehåller alla funktioner som finns i den här underhållsversionen. Se [Roadmap för lanseringar av Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html) för mer information.

### Förbättringar {#enhancements-15977}

* GRANITE-51335: Optimera AEM hälsokontroll för att öka instansstabiliteten.

### Åtgärdade problem {#fixed-issues-15977}

* CQ-4357226: Korrigera regression i IMS-konfigurationer som stöder OAuth-autentiseringsuppgifter.
* GRANITE-51335: Ratelimit upgrade to 5.0.4 Fixed Felix Health Check registrations.

### Kända fel {#known-issues-15977}

Ingen.

### Föråldrade funktioner och API:er {#deprecated-15977}

* [Borttagning av JWT-autentiseringsuppgifter i Adobe Developer Console](/help/security/jwt-credentials-deprecation-in-adobe-developer-console.md)

Titta på [Föråldrade och borttagna funktioner och API:er](/help/release-notes/deprecated-removed-features.md) för att veta vad som har tagits bort eller tagits bort på AEM as a Cloud Service.

### Inbäddade tekniker {#embedded-tech-15977}

| Teknik | Version | Länk |
|---|---|---|
| AEM | 1.62.0 | [API för Oak API 1.62.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.62.0/index.html) |
| AEM SLING API | 2.27.2 | [API för Apache Sling 2.27.2](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTML | 1.4.20-1.4.0 | [HTML-mallens språkspecifikation](https://github.com/adobe/htl-spec) |
| Grundläggande komponenter i AEM | 2.24.6 | [AEM WCM-kärnkomponenter](https://github.com/adobe/aem-core-wcm-components) |

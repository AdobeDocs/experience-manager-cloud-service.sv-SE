---
title: Aktuell underhållsanvisning för [!DNL Adobe Experience Manager] as a Cloud Service.
description: Aktuell underhållsanvisning för [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 39b2afda66e3bcb7db8ae63a2d0dcd27014ce377
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 3%

---

# Versionsinformation om underhåll {#maintenance-release-notes}

I följande avsnitt beskrivs den tekniska versionsinformationen för den aktuella underhållsutgåvan av Experience Manager as a Cloud Service.

## Utgåva 12790 {#release-12790}

Nedan sammanfattas de kontinuerliga förbättringarna av underhållsreleasen 12790, som offentliggjordes den 21 juli 2023. Den här underhållsversionen är en uppdatering från den tidigare underhållsversionen 12697.

2023.7.0 Funktionsaktivering innehåller alla funktioner som finns i den här underhållsversionen. Se [Roadmap för lansering av Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html) för mer information.

### Förbättringar {#enhancements-12790}

Ingen.

### Åtgärdade problem {#fixed-issues-112790}

- SLING-11974 - Korrigerad regression i SlingHttpServletRequest#getUserPrincipal för icke-autentiserade begäranden. Korrigeringen ser till att ett huvudnamn returneras även för oautentiserade begäranden.

### Kända fel {#known-issues-12790}

Ingen.

### Inbäddade tekniker {#embedded-tech-12790}

| Teknik | Version | Länk |
|---|---|---|
| AEM OAK | 1.52-T20230629133256-25c01b8 | [API för Oak API 1.52.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.52.0/index.html) |
| AEM SLING API | Version 2.27.2 | [API för Apache Sling 2.27.2](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTML | Version 1.4.20-1.4.0 | [HTML-mallens språkspecifikation](https://github.com/adobe/htl-spec) |
| Grundläggande komponenter i AEM | Version 2.23.0 | [AEM WCM-kärnkomponenter](https://github.com/adobe/aem-core-wcm-components) |

---
title: Aktuell underhållsanvisning för [!DNL Adobe Experience Manager] as a Cloud Service.
description: Aktuell underhållsanvisning för [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 558babc0124a8ee8c1337b91c5ef016ed238c935
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 1%

---

# Versionsinformation om underhåll {#maintenance-release-notes}

I följande avsnitt beskrivs den tekniska versionsinformationen för den aktuella underhållsutgåvan av Experience Manager as a Cloud Service.

## Version 16544 {#release-16544}

Nedan sammanfattas de kontinuerliga förbättringarna av underhållsutgåvan 16544, som offentliggjordes den 4 juni 2024. Den tidigare underhållsversionen var version 16461.

2024.6.0 Funktionsaktivering innehåller alla funktioner som finns i den här underhållsversionen. Se [Roadmap för lanseringar av Experience Manager](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) för mer information.

### Förbättringar {#enhancements-16544}

* GRANITE-41133: Stöd för Jakarta Servlet API 5 och OSGi Servlet Whiteboard API.
* GRANITE-51355: Deprecate org.slf4j.event.
* GRANITE-51565: AEM förlorar den lokala grupprelationen med den externa gruppen när den lokala gruppen publiceras från AEM.
* GRANITE-51707: Ange cookie saml_request_path under http-omdirigering för autentisering.
* GRANITE-52010: Uppdatera Jackrabbit-version till 2.20.16.
* GRANITE-52057: Uppdatera Filevault till 3.7.3-T20240514105118-694f6aea som korrigerar JCRVLT-745.
* SKYOPS-35998: Uppdatera Sling RepoInit-beroenden: Repoinit Parser 1.9.0, Repoinit JCR 1.1.46.

### Åtgärdade problem {#fixed-issues-16544}

* DXML-17171: AEM stödlinjer: Kopiering och inklistring av ämnen som överstiger 15 kB misslyckas med ett oväntat fel.
* DXML-17088: AEM stödlinjer: Funktionen som används för att ändra dokumentstatus från **Filegenskaper** panelen fungerar inte som den ska och ändringar i *Utkast* tillstånd.
* DXML-16931: AEM stödlinjer: Länkade bilder från ämnen visas inte i baslinjen när versionerna har skapats.
* DXML-16896: AEM stödlinjer: Återanvändbara innehållspaneler listar inte element när **Användarinställningar** är inställda på att visa filer efter **Filnamn**.
* GRANITE-51375: idp-sync returnerar NPE om ingen mellanliggande sökväg anges.

### Kända fel {#known-issues-16544}

Ingen.

### Föråldrade funktioner och API:er {#deprecated-16544}

Om du vill veta vad som är föråldrat eller borttaget i AEM as a Cloud Service kan du läsa [Föråldrade och borttagna funktioner och API:er](/help/release-notes/deprecated-removed-features.md).

### Inbäddade tekniker {#embedded-tech-16544}

| Teknik | Version | Länk |
|---|---|---|
| AEM Oak | 1.64.0 | [Oak API 1.64.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.64.0/index.html) |
| AEM SLING API | 2.27.2 | [API för Apache Sling 2.27.2](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTML | 1.4.22-1.4.0 | [HTML-mallens språkspecifikation](https://github.com/adobe/htl-spec) |
| Grundläggande komponenter i AEM | 2.25.4 | [AEM WCM-kärnkomponenter](https://github.com/adobe/aem-core-wcm-components) |

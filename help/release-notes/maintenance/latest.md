---
title: Aktuell underhållsanvisning för [!DNL Adobe Experience Manager] as a Cloud Service.
description: Aktuell underhållsanvisning för [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: eca0903050bb178f13d37073f8d65354f4bf36d3
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 2%

---

# Versionsinformation om underhåll {#maintenance-release-notes}

I följande avsnitt beskrivs den tekniska versionsinformationen för den aktuella underhållsutgåvan av Experience Manager as a Cloud Service.

## Utgåva 12697 {#release-12697}

Nedan sammanfattas de kontinuerliga förbättringarna av underhållsreleasen 12697, som offentliggjordes den 14 juli 2023. Den här underhållsversionen är en uppdatering från den tidigare underhållsversionen 12549. Underhållsutgåva 12697 ersätter 12585 för att åtgärda ett problem.

2023.7.0 Funktionsaktivering innehåller alla funktioner som finns i den här underhållsversionen. Se [Roadmap för lansering av Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html) för mer information.

### Förbättringar {#enhancements-12697}

- Allmänna förbättringar av RDE-stabiliteten (SKYOPS-61133, SKYOPS-55281, SKYOPS-61216 och SKYOPS-61401)
- DXML-12327: AEM stödlinjer: Stöd för språkvariabler i Native PDF
- DXML-11518: AEM stödlinjer: Förbättrat stöd för metadata vid publicering i Native PDF
- DXML-10093: AEM stödlinjer: Stöd för anslutning till externa datakällor och infogning av data i dataämnen
- DXML-10699: AEM stödlinjer: Stöd för XLIFF-format i översättning
- DXML-10141: AEM stödlinjer: Möjlighet att använda mikrotjänstbaserad publicering för förinställningstyperna PDF (Native &amp; DITA-OT), HTML och Custom
- SKYOPS-61385 - Uppdatera dispatchern så att libpcre2 används vid utvärdering av reguljära uttryck i Apache HTTPD

### Åtgärdade problem {#fixed-issues-12697}

- AEM stödlinjer: Förbättringar och stabilitetskorrigeringar för olika inbyggda PDF
- SKYOPS-53130: Förbättra stödet för AC-verktyg i RDE
- SKYOPS-57146: Åtgärda dödläge vid AEM
- SKYOPS-61646: Det senaste replikeringsdatumet uppdateras inte efter uppgradering till version 12585

### Kända fel {#known-issues-12697}

Ingen.

### Inbäddade tekniker {#embedded-tech-12697}

| Teknik | Version | Länk |
|---|---|---|
| AEM OAK | 1.52-T20230629133256-25c01b8 | [API för Oak API 1.52.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.52.0/index.html) |
| AEM SLING API | Version 2.27.2 | [API för Apache Sling 2.27.2](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTML | Version 1.4.20-1.4.0 | [HTML-mallens språkspecifikation](https://github.com/adobe/htl-spec) |
| Grundläggande komponenter i AEM | Version 2.23.0 | [AEM WCM-kärnkomponenter](https://github.com/adobe/aem-core-wcm-components) |

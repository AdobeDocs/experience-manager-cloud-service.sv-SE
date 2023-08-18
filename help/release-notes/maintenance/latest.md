---
title: Aktuell underhållsanvisning för [!DNL Adobe Experience Manager] as a Cloud Service.
description: Aktuell underhållsanvisning för [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: cf8b5d8b11452268b2839053c1e05cc2ec107a91
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 2%

---

# Versionsinformation om underhåll {#maintenance-release-notes}

I följande avsnitt beskrivs den tekniska versionsinformationen för den aktuella underhållsutgåvan av Experience Manager as a Cloud Service.

## Utgåva 13173 {#release-13173}

Nedan sammanfattas de kontinuerliga förbättringarna av underhållsutgåvan 13173, som offentliggjordes den 18 augusti 2023. Den här underhållsversionen är en uppdatering från den tidigare underhållsversionen 13099.

2023.8.0 Funktionsaktivering innehåller alla funktioner som finns i den här underhållsversionen. Se [Roadmap för lanseringar av Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html) för mer information.

### Förbättringar {#enhancements-13173}

Ingen.

### Åtgärdade problem {#fixed-issues-13173}

- SITES-15463: Sites Templates - Templates kan inte publiceras.

### Kända fel {#known-issues-13173}

- SITES-15359: Content Fragments - Variantnamnsmönstret matchar inte varianter som har ```'_'``` i sina resursnamn.
- FORMS-10444: Adaptiva Forms-mallar - mallar kan inte publiceras (tillfällig lösning: använd distributionskonsolen).
- CQ-4354191: Arbetsflöden - Anpassad startfunktion kan utlösas många gånger på grund av replikeringsmetadata som finns på nod:ostrukturerade noder (tillfällig lösning: startprogram för uppdatering som exkluderar egenskaper för replikeringsmetadata för att undvika överlappning).

### Inbäddade tekniker {#embedded-tech-13173}

| Teknik | Version | Länk |
|---|---|---|
| AEM | 1.52-T20230629133256-25c01b8 | [API för Oak API 1.52.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.52.0/index.html) |
| AEM SLING API | Version 2.27.2 | [API för Apache Sling 2.27.2](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTML | Version 1.4.20-1.4.0 | [HTML-mallens språkspecifikation](https://github.com/adobe/htl-spec) |
| Grundläggande komponenter i AEM | Version 2.23.2 | [AEM WCM-kärnkomponenter](https://github.com/adobe/aem-core-wcm-components) |

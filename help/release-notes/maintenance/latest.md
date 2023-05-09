---
title: Aktuell underhållsanvisning för [!DNL Adobe Experience Manager] as a Cloud Service.
description: Aktuell underhållsanvisning för [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: ea3a476f7f2d7d97a2428c6facf61b746dba7a23
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 2%

---

# Versionsinformation om underhåll {#maintenance-release-notes}

I följande avsnitt beskrivs den tekniska versionsinformationen för den aktuella underhållsutgåvan av Experience Manager as a Cloud Service.

## Utgåva 11873 {#release-11873}

Nedan sammanfattas de kontinuerliga förbättringarna av underhållsutgåvan 11873, som offentliggjordes den 3 maj 2023. Den här underhållsversionen är en uppdatering från den tidigare underhållsversionen 11835.

Funktionsaktiveringen för den här underhållsversionen ger dig den fullständiga funktionsuppsättningen. Se [aktuell versionsinformation](/help/release-notes/release-notes-cloud/release-notes-current.md) för fullständig information.

### Förbättringar {#enhancements}

- SITES-1200 - Förbättringar i sök-API med taggbaserad filtrering
- GRANITE-42939 - Lägg till borttagningsanteckningar och varningar i oauth-serverkod

### Kända fel {#known-issues-11873}

Ingen.

### Åtgärdade problem {#fixed-issues-11873}

- SKYSI-19884/SKYOPS-53745 - Korrigerat problem med PublishPageRenderingErrorsHigh
- GRANITE-4388 - Korrigerade dataflödesförsämring efter ett stort antal DAM-resursskrivningar på Mongo
- SITES-11922 - Korrigerat problem med avpublicering från förhandsgranskning som inte tog bort synkroniseringsstatus
- ASSETS-21648 - Korrigerat behörighetsproblem med tillgångsrelaterade funktioner

### Inbäddade tekniker {#embedded-tech-11873}

| Teknik | Version | Länk |
|---|---|---|
| AEM OAK | 1.44-T20221206170501-6d59064 | [API för Oak API 1.4.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.44.0/index.html) |
| AEM SLING API | Version 2.27.0 | [API för Apache Sling 2.27.0](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTML | Version 1.4.20-1.4.0 | [HTML-mallens språkspecifikation](https://github.com/adobe/htl-spec) |
| Grundläggande komponenter i AEM | Version 2.21.2 | [AEM WCM-kärnkomponenter](https://github.com/adobe/aem-core-wcm-components) |

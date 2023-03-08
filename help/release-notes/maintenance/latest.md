---
title: Senaste underhållsinformation [!DNL Adobe Experience Manager] as a Cloud Service.
description: Senaste underhållsinformation [!DNL Adobe Experience Manager] as a Cloud Service.
source-git-commit: edb8949b532b80a55106e706a49e2ada68722a67
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 2%

---


# Versionsinformation om underhåll {#maintenance-release-notes}

I följande avsnitt beskrivs de tekniska releasefoterna för den senaste underhållsutgåvan av Experience Manager as a Cloud Service.

## Utgåva 11289 {#release-11289}

Nedan sammanfattas de kontinuerliga förbättringarna av underhållsutgåvan 11289, som offentliggjordes den 7 mars 2023. Den här underhållsversionen är en uppdatering från den tidigare underhållsversionen 10912.

Funktionsaktiveringen för den här underhållsversionen ger dig den fullständiga funktionsuppsättningen. Se [aktuell versionsinformation](/help/release-notes/release-notes-cloud/release-notes-current.md) för fullständig information.

### Kända fel {#known-issues}

Uppgradera inte om du använder CORS. Ett problem som påverkar GraphQL innehållsleveransfunktion identifierades i den här versionen. En ändring i standardkonfigurationen AEM dispatcher vad gäller hur beständiga GraphQL-frågor cachelagras kan störa leveransen av GraphQL-innehåll i sådana frågor. Problemet kommer att åtgärdas i nästa underhållsrelease.

### Åtgärdade problem {#fixed-issues}

#### Sites {#sites-issues}

- SITES-11584 Korrigerat problem med Live-kopior som inte kunde skapas för sidor med anteckningar
- SITES-11683 Inaktiverade MSM Live-kopior med delvis brutet arv

#### Assets {#assets-issues}

- ASSETS-20879 Korrigerad regression som förhindrar att gränssnittet för tillgångsrapporter fungerar korrekt och resulterade i felaktiga resultat i genererade rapporter.
- ASSETS-21020 Åtgärdat problem med hämtning av brutna resurser - Bildprofilen finns inte efter att resursen har flyttats
- ASSETS-21023 Ett problem med bildåtergivningar i Dynamic Media som förhindrar åtkomst via API har korrigerats

#### Forms {#forms-issues}

- Inget

#### Plattform {#platform-issues}

- GRANITE-44467 - Korrigerat problem som medförde att importen misslyckades, när en befintlig nod uppdaterades, bevarade inte Filevault under vissa instanser blandningstyper och underordnade noder

### Inbäddade tekniker {#embedded-tech}

| Teknik | Version | Länk |
|---|---|---|
| AEM OAK | 1.44-T20221206170501-6d59064 | [API för Oak API 1.4.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.44.0/index.html) |
| AEM SLING API | Version 2.27.0 | [API för Apache Sling 2.27.0](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTML | Version 1.4.20-1.4.0 | [HTML-mallens språkspecifikation](https://github.com/adobe/htl-spec) |
| Grundläggande komponenter i AEM | Version 2.21.2 | [AEM WCM-kärnkomponenter](https://github.com/adobe/aem-core-wcm-components) |

---
title: Aktuell information om underhållsversionen av  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Aktuell information om underhållsversionen av  [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 30b5d5838087a35a457939cdbaa13c5735df144e
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 1%

---


# Versionsinformation om underhåll {#maintenance-release-notes}

I följande avsnitt beskrivs den tekniska versionsinformationen för den aktuella underhållsversionen av Experience Manager as a Cloud Service.

## Utgåva 19823 {#19823}

Nedan sammanfattas de kontinuerliga förbättringarna av underhållsreleasen 19823, som offentliggjordes den 4 mars 2025. Den tidigare underhållsutgåvan släpptes 19687.

Funktionsaktiveringen i 2025.3.0 kommer att innehålla alla funktioner som finns i den här underhållsversionen. Mer information finns i [Experience Manager Releases Roadmap](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

### Förbättringar {#enhancements-19823}

* ASSETS-46491: OSGI-händelsehanterare för statusändring för bearbetning av resurser.
* ASSETS-45613: Skicka avpubliceringshändelser när resurser tas bort eller flyttas.
* ASSETS-45131: Stöd för anpassade taggegenskaper i Content Hub.

### Åtgärdade problem {#fixed-issues-19823}

* ASSETS-20433: Dynamic Media-problem med lösenordsskyddade PDF-filer.
* ASSETS-24675: Bildbearbetningsalternativ visas inte för bilder med enbart färgrutor.
* ASSETS-41257: Versionsjämförelse återger resurs med felaktiga proportioner. Resursversioner visas i fel ordning på tidslinjen.
* ASSETS-44894: Det är inte säkert att bokmärken i Assets-vyn kan klickas.
* ASSETS-45015: Smart beskärningsbredd och -höjd har angetts som noll om det inte går att hitta resurshandtaget för smart beskärning.
* ASSETS-45192: Minska frekvensen för pulsförfrågningar.
* ASSETS-45724: Kontrollera att DM-överföringen görs om om överföringsjobbet inte har tilldelats.
* ASSETS-46425: Adobe Stock integreringssökningsproblem.
* ASSETS-27400: Generatorn för mappförhandsvisning kan försöka öppna originalet.
* CQ-4358722: Hantera olika språkkoder i Java 11 och Java 17.
* SITES-29369: Page Published/Unpublished Events triggered on Asset activation/deactivation.
* SITES-24074: Korrigera tangentbordstillgänglighet med ett enhetligt skal.
* SITES-28058: Assets-mapptiteln överförs inte till live-kopian.

### Kända fel {#known-issues-19823}

Ingen.

### Föråldrade funktioner och API:er {#deprecated-19823}

Inaktuella och borttagna funktioner och API:er i AEM as a Cloud Service beskrivs i dokumentet [Inaktuella och Borttagna funktioner och API:er](/help/release-notes/deprecated-removed-features.md).

### Säkerhetskorrigeringar {#security-19823}

AEM as a Cloud Service strävar efter att optimera säkerheten och prestandan för din plattform. Denna underhållsrelease åtgärdar sex identifierade sårbarheter, vilket stärker vårt engagemang för robust systemskydd.

### Inbäddade tekniker {#embedded-tech-19823}

| Teknik | Version | Länk |
|---|---|---|
| AEM Oak | 1.76.0 | [Oak API 1.76.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.76.0/index.html) |
| AEM SLING API | 2.27.6 | [API:t för Apache Sling 2.27.6 ](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.26-1.4.0 | [Språkspecifikation för HTML-mall](https://github.com/adobe/htl-spec) |
| Grundläggande komponenter i AEM | 2.27.0 | [AEM WCM Core Components](https://github.com/adobe/aem-core-wcm-components) |

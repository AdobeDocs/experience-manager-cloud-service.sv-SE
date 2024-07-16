---
title: Aktuell underhållsversionsinformation för  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Aktuell underhållsversionsinformation för  [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 573de431328650778b3ef0979a24190477382310
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 1%

---


# Versionsinformation om underhåll {#maintenance-release-notes}

I följande avsnitt beskrivs de tekniska versionsinformationen för den aktuella underhållsutgåvan av Experience Manager as a Cloud Service.

## Utgåva 17098 {#release-17098}

Nedan sammanfattas de kontinuerliga förbättringarna av underhållsutgåvan 17098, som offentliggjordes den 16 juli 2024. Den tidigare underhållsversionen var version 16971.

Funktionsaktiveringen i 2024.7.0 kommer att innehålla alla funktioner som finns i den här underhållsversionen. Mer information finns i [Experience Manager Releases Roadmap](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

### Förbättringar {#enhancements-17098}

- SKYOPS-79817: Aktivera aktiviteten Sling Feature Analyzer Task för Service User Mappings

### Åtgärdade problem {#fixed-issues-17098}

- ASSETS-39665: Synkronisering av smarta beskärningar fungerar inte efter migrering från 6.5 till AEMCS
- FORMS-14993: Forms API returnerar 500 för det tidigare fungerande materialet
- GRANITE-52120: CRXDE returnerar 500 när åtkomstkontrollsdata visas
- GRANITE-52573: Begäranden som returnerar 400 när // används i återskrivna URL:er
- GRANITE-52746: Alla nodtyper har inte lästs in i dialogrutan Skapa nod
- GRANITE-52777: Hantering av 404-talsfel när begäran paketeras
- GRANITE-52871: Kontrollera att publish-worker har synkroniserats med gyllene publicering och är klar före komprimering
- SKYOPS-79173: Replikatorn replikerar inte till flera agenter som matchar ett visst AgentIdFilter
- SKYOPS-80075: Problem med miljöförändringar i tillgångsnamn som orsakar blockering i publiceringskön (Mac)
- SKYOPS-81032: Filtrera ut loggar som genererats av begäranden för att hämta loggar när Förbättrad loggning används

### Kända fel {#known-issues-17098}

Ingen

### Ändringsmeddelande {#change-notice-17098}

- Från och med september 2024 kommer AEM as a Cloud Service att inaktivera serialiseringen av resurslösare via Sling Model Exporter-ramverket. Mer information finns i [dokumentationen](/help/implementing/developing/hybrid/disallow-the-serialization-of-resourceresolvers-via-sling-model-exporter.md).

### Föråldrade funktioner och API:er {#deprecated-17098}

Inaktuella och borttagna funktioner och API:er i AEM as a Cloud Service beskrivs i dokumentet [Inaktuella och Borttagna funktioner och API:er](/help/release-notes/deprecated-removed-features.md).

### Inbäddade tekniker {#embedded-tech-17098}

| Teknik | Version | Länk |
|---|---|---|
| AEM Oak | 1.66.0 | [Oak API 1.6.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.66.0/index.html) |
| AEM SLING API | 2.27.2 | [API:t för Apache Sling 2.27.2 ](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTML | 1.4.24-1.4.0 | [Språkspecifikation för HTML-mall](https://github.com/adobe/htl-spec) |
| Grundläggande komponenter i AEM | 2.25.4 | [AEM WCM-kärnkomponenter](https://github.com/adobe/aem-core-wcm-components) |

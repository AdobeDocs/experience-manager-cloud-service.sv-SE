---
title: Aktuell information om underhållsversionen av  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Aktuell information om underhållsversionen av  [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 33468de99a3e77539f4bdc9435324c9f52a45d9f
workflow-type: tm+mt
source-wordcount: '350'
ht-degree: 1%

---


# Versionsinformation om underhåll {#maintenance-release-notes}

I följande avsnitt beskrivs den tekniska versionsinformationen för den aktuella underhållsversionen av Experience Manager as a Cloud Service.

## Utgåva 22171 {#22171}

Nedan sammanfattas de kontinuerliga förbättringarna av underhållsutgåvan 22171, som offentliggjordes den 2 september 2025. Den tidigare underhållsversionen var version 21994.

Funktionsaktiveringen i 2025.9.0 kommer att innehålla alla funktioner som finns i den här underhållsversionen. Mer information finns i [Experience Manager Releases Roadmap](https://experienceleague.adobe.com/sv/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

### Nya funktioner  {#new-features-22171}

* ASSETS-53136: Stöd för Vanity ID i Dynamic Media med OpenAPI.

### Förbättringar {#enhancements-22171}

Ingen.

### Åtgärdade problem {#fixed-issues-22171}

* ASSETS-52510: Dubblettnamnsidentifiering misslyckas för filnamn som innehåller Unicode `U+202F`.
* ASSETS-53489: Borttagning av mappar från Assets-visningsgränssnittet godkänner inte alla resurser som ingår.
* ASSETS-54821: Intermittent serverfel i Asset Link.
* ASSETS-55024: Skadad bild i AEM Assets mall &quot;Download by Email&quot;.
* ASSETS-55325: Dynamiska medias statiska URL:er utelämnar filtillägget efter namnbytet.
* ASSETS-55334: Dialogrutan Länkdelning blinkar kort och försvinner eller visas aldrig.
* ASSETS-55382: Omstartade asynkrona resursjobb skapar en dubblett av målmappen.
* ASSETS-55472: Alternativet Hantera publikation,&quot;Inkludera endast redan publicerade sidor&quot;, ignorerades.
* SITES-31600: Contexthub js error break personalization.

Mer information om de nya och förbättrade funktionerna och problemen som har åtgärdats i den här versionen finns i [Experience Manager Guides-lanseringens färdplan](https://experienceleague.adobe.com/sv/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

### Kända fel {#known-issues-22171}

Ingen.

### Föråldrade funktioner och API:er {#deprecated-22171}

Inaktuella och borttagna funktioner och API:er i AEM as a Cloud Service beskrivs i dokumentet [Inaktuella och Borttagna funktioner och API:er](/help/release-notes/deprecated-removed-features.md).

### Säkerhetskorrigeringar {#security-22171}

AEM as a Cloud Service strävar efter att optimera säkerheten och prestandan för din plattform. Denna underhållsrelease åtgärdar 7 identifierade sårbarheter, vilket stärker vårt engagemang för robust systemskydd.

### Inbäddade tekniker {#embedded-tech-22171}

| Teknik | Version | Länk |
|---|---|---|
| AEM Oak | 1.84.0 | [Oak API 1.84.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.84/index.html) |
| AEM SLING API | 2.27.6 | [API:t för Apache Sling 2.27.6 ](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [Språkspecifikation för HTML-mall](https://github.com/adobe/htl-spec) |
| Apache HTTP-server | 2.4.65 | [Apache HTTP 2.4.65](https://apache.googlesource.com/httpd/+/refs/tags/2.4.65/CHANGES) |
| Grundläggande komponenter i AEM | 2.29.0 | [AEM WCM Core Components](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14 (standard) | [Node.js-versioner som stöds](https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |

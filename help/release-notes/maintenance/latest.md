---
title: Aktuell information om underhållsversionen av  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Aktuell information om underhållsversionen av  [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: c5152543550b5f81bf0b79741f288b0c16648584
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 1%

---


# Versionsinformation om underhåll {#maintenance-release-notes}

I följande avsnitt beskrivs den tekniska versionsinformationen för den aktuella underhållsversionen av Experience Manager as a Cloud Service.

## Utgåva 20476 {#20476}

Nedan sammanfattas de kontinuerliga förbättringarna av underhållsutgåvan 20476, som offentliggjordes den 15 april 2025. Den tidigare underhållsutgåvan släpptes 2013.

Funktionsaktiveringen i 2025.4.0 kommer att innehålla alla funktioner som finns i den här underhållsversionen. Mer information finns i [Experience Manager Releases Roadmap](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

### Förbättringar {#enhancements-20476}

* CNTBF-411: Lägg till möjlighet att ta bort sling-jobb om det släpps av JCR.
* CQ-4359813: AEM Translation Kit: 20 mars.
* CQ-4359811: Granite Translation Kit: 20 mars.
* GRANITE-57863: Uppdatera Fireworks till version 3.8.4.
* GRANITE-56154: Konfigurera exponentiella återförsök i eksegment-azure.
* GRANITE-55999: Förbättra prestanda för UserPropertiesService.
* GRANITE-55781: Undvik redundant omkonfigurering av användarmedlemskap.
* GRANITE-53956: Uppgradera Azure SDK V8 till V12 för eksegment-azure.
* GRANITE-50654: På fliken för huvudbehörigheter tar du bort inläsningen &quot;alla&quot; som standard på frontsidan.
* SKYOPS-103444: Uppdatera till Sling ResourceResolver 1.12.6.
* SKYOPS-101147: Konfig. av uppdatering.
* SKYOPS-97124: Lägg till analysvarningar för inaktuella versioner av SPIFly-paketet.
* SKYOPS-95826: Uppdatera Java-versioner för körning till 11.0.26 och 21.0.6.
* SKYOPS-53671: Använd kundinstallerade artefakter från funktionsmodeller i AEM (RDE).

### Åtgärdade problem {#fixed-issues-20476}

* ASSETS-49027: [Regression] AemRequestEventFilter bryter POST-begäranden till OSGI-webbkonsolen.
* ASSETS-44956: Det går inte att välja någon dynamisk medieåtergivning - skripttaggar ska läsas in i den översta komponenten.
* CNTBF-410: CheckJob getId null-pekare i ContentCopy Bundle.
* CNTBF-341: Index för ContentCopy-export ligger utanför gränserna.
* CQ-4355411: Verktygstips visas fortfarande på skärmen i dialogrutan Användarinställningar.
* GRANITE-57265: Värden för listrutemarkering markeras inte.
* GRANITE-57067 - Effektiva principer saknas för användargränssnittet.
* SITES-30727: Det går eventuellt inte att dra och släppa underkomponenter i AEM Editor.
* SKYOPS-90607: Sling-jobb körs i inaktiv distribution/inaktiverat innehåll.
* SKYOPS-95722: Ta bort storleken `MaxPermSize` från snabbstartflaggor i AEM-SDK.
* SKYOPS-103569: Vissa bilder kan inte läsas in med Java 21: `javax.imageio.IIOException: Cannot create Sun JPEGImageReader backend`.

### Kända fel {#known-issues-20476}

Ingen.

### Föråldrade funktioner och API:er {#deprecated-20476}

Inaktuella och borttagna funktioner och API:er i AEM as a Cloud Service beskrivs i dokumentet [Inaktuella och Borttagna funktioner och API:er](/help/release-notes/deprecated-removed-features.md).

### Säkerhetskorrigeringar {#security-20476}

AEM as a Cloud Service strävar efter att optimera säkerheten och prestandan för din plattform. Denna underhållsrelease åtgärdar 5 identifierade sårbarheter, vilket stärker vårt engagemang för robust systemskydd.

### Inbäddade tekniker {#embedded-tech-20476}

| Teknik | Version | Länk |
|---|---|---|
| AEM Oak | 1.78.0 | [Oak API 1.78.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.78.0/index.html) |
| AEM SLING API | 2.27.6 | [API:t för Apache Sling 2.27.6 ](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.26-1.4.0 | [Språkspecifikation för HTML-mall](https://github.com/adobe/htl-spec) |
| Grundläggande komponenter i AEM | 2.28.0 | [AEM WCM Core Components](https://github.com/adobe/aem-core-wcm-components) |

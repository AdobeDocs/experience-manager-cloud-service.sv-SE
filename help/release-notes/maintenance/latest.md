---
title: Aktuell information om underhållsversionen av  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Aktuell information om underhållsversionen av  [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 6884e33a922a7147e3a6a3f3ddb3dd3b2da85fbf
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 1%

---


# Versionsinformation om underhåll {#maintenance-release-notes}

I följande avsnitt beskrivs den tekniska versionsinformationen för den aktuella underhållsversionen av Experience Manager as a Cloud Service.

## Version 21005 {#21005}

Nedan sammanfattas de kontinuerliga förbättringarna av underhållsutgåvan 21005, som offentliggjordes den 27 maj 2025. Den tidigare underhållsutgåvan släpptes 20626.

Funktionsaktiveringen i 2025.5.0 kommer att innehålla alla funktioner som finns i den här underhållsversionen. Mer information finns i [Experience Manager Releases Roadmap](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

### Förbättringar {#enhancements-21005}

* GRANITE-58927: Förbättringar av växlingsfunktionen Semantic Search.
* GRANITE-58800: Uppdatera Apache Commons-samlingar till version 4.5.0.
* GRANITE-58866: Uppdatera Oak till 1.80.0.
* SKYOPS-106509: Förbättrad GSON-kompatibilitet via reflekterande åtkomst i Java 21.
* SKYOPS-107761: Uppdatering av Sling Models Jackson Exporter till 1.1.6.
* SKYOPS-107813: Uppdatera till Sling ResourceResolver 1.12.8.

### Åtgärdade problem {#fixed-issues-21005}

* CNTBF-443: Fast SearchSlingJob `EVENT_JOB_TOPIC`-egenskap.
* GRANITE-57853: Korrigerade nedrullningsjusteringsproblem i användargränssnittet.
* GRANITE-58107: Korrigerade 404 fel vid publicering genom att inaktivera användarbaserad pod-tillhörighet i OAuth-hanteraren.
* GRANITE-58276, SLING-12755: Åtgärdade OSGi-beroendecykler som kan förhindra att HTL Script Engine-fabriken startar korrekt, vilket kan orsaka intermittenta återgivningsfel på serversidan.
* SKYOPS-105151: Fast NPE vid åtkomst till paketlistan.
* SKYOPS-83910, SKYOPS-82371 - Korrigerade problem med samtidig JSP-kompilering.

#### AEM Guides {#guides}

* GUIDES-26919: När du öppnar en DITA-karta med det enhetliga skalet aktiverat uppdateras redigeraren regelbundet.
* GUIDES-26282: Om JCR-sessionsanslutningar inte kan stängas vid uppdatering eller skapande av ämnen resulterar detta i minnesläckor och driftavbrott.
* GUIDES-26434: Den inbyggda PDF-publiceringen fortsätter i oändlighet om DITA-innehållet har en webblänk utan omfång som `external`.
* GUIDES-26516: Publicering av inbyggda PDF-filer och AEM-webbplatser stoppas och köas om det finns fel i innehållet.

Mer information om de nya och förbättrade funktionerna och problemen som har åtgärdats i den här versionen finns i [Experience Manager Guides-lanseringens färdplan](https://experienceleague.adobe.com/en/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

### Kända fel {#known-issues-21005}

Ingen.

### Föråldrade funktioner och API:er {#deprecated-21005}

* GRANITE-54164: `org.apache.jackrabbit.oak.plugins.blob` har tagits bort från publikt API.
* GRANITE-54280: `org.apache.jackrabbit.oak.cache` har tagits bort från publikt API.
* GRANITE-58332: `org.apache.jackrabbit.oak.plugins.memory` har tagits bort i publikt API.
* YUI-kompressor för javascript har tagits bort.
* Funktionen [Experience Cloud Setup Automation](/help/sites-cloud/integrating/adobe-analytics-exc-setup-automation.md) har tagits bort.

Inaktuella och borttagna funktioner och API:er i AEM as a Cloud Service beskrivs i dokumentet [Inaktuella och Borttagna funktioner och API:er](/help/release-notes/deprecated-removed-features.md).

### Säkerhetskorrigeringar {#security-21005}

AEM as a Cloud Service strävar efter att optimera säkerheten och prestandan för din plattform. Denna underhållsrelease åtgärdar 5 identifierade sårbarheter, vilket stärker vårt engagemang för robust systemskydd.

### Ändringsmeddelande {#change-notice-21005}

* Den här versionen innehåller följande nya produktindexversioner:
   * **damAssetLucene-12**

Anpassade versioner av tidigare indexversioner sammanfogas automatiskt med den nya produktindexversionen. Använd ytterligare anpassade uppdateringar för den sammanfogade versionen.

#### Uppdatera aem-cloud-testing-clients {#update-aem-cloud-testing-clients-21005}

För kommande ändringar måste biblioteket [aem-cloud-testing-clients](https://github.com/adobe/aem-testing-clients) som används i dina anpassade funktionstester uppdateras till minst version **1.2.1** (Rekommenderas: senaste versionen 1.2.9)

Kontrollera att beroendet i `it.tests/pom.xml` har uppdaterats.

```xml
<dependency>
   <groupId>com.adobe.cq</groupId>
   <artifactId>aem-cloud-testing-clients</artifactId>
   <version>1.2.9</version>
</dependency>
```

Denna ändring måste utföras före den 15 juni 2025.
Om du inte uppdaterar beroendebiblioteket kommer det att uppstå ett pipeline-fel i steget&quot;Custom Functional Testing&quot;.

### Inbäddade tekniker {#embedded-tech-21005}

| Teknik | Version | Länk |
|---|---|---|
| AEM Oak | 1.80.0 | [Oak API 1.80.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.80.0/index.html) |
| AEM SLING API | 2.27.6 | [API:t för Apache Sling 2.27.6 ](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [Språkspecifikation för HTML-mall](https://github.com/adobe/htl-spec) |
| Grundläggande komponenter i AEM | 2.29.0 | [AEM WCM Core Components](https://github.com/adobe/aem-core-wcm-components) |

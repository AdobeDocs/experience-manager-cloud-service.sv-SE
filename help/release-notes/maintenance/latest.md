---
title: Aktuell underhållsanvisning för [!DNL Adobe Experience Manager] as a Cloud Service.
description: Aktuell underhållsanvisning för [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 1dd2eae9201c86d2cdac78ff99634eff8ca57a05
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 2%

---

# Versionsinformation om underhåll {#maintenance-release-notes}

I följande avsnitt beskrivs den tekniska versionsinformationen för den aktuella underhållsutgåvan av Experience Manager as a Cloud Service.

## Version 15860 {#release-15860}

Nedan sammanfattas de kontinuerliga förbättringarna av underhållsutgåvan 15860, som offentliggjordes den 10 april 2024. Den tidigare underhållsversionen var version 15787.

2024.3.0 Funktionsaktivering innehåller alla funktioner som finns i den här underhållsversionen. Se [Roadmap för lanseringar av Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html) för mer information.

### Förbättringar {#enhancements-15860}

Ingen.

### Åtgärdade problem {#fixed-issues-15860}

* Korrigerar regression för att visa startkonsolen när en start refererar till en borttagen eller flyttad sida.

### Kända fel {#known-issues-15860}

Ingen.

### Föråldrade funktioner och API:er {#deprecated-15860}

* [Borttagning av JWT-autentiseringsuppgifter i Adobe Developer Console](/help/security/jwt-credentials-deprecation-in-adobe-developer-console.md)

Titta på [Föråldrade och borttagna funktioner och API:er](/help/release-notes/deprecated-removed-features.md) för att veta vad som har tagits bort eller tagits bort på AEM as a Cloud Service.

### Ändringsmeddelande {#change-notice-15860}

**Åtgärder krävs**

#### Ange CM Java-versionen till 11 {#set-java-version-11}

Den nya versionen av aem-sdk-api innehåller klasser som kompilerats med ett Java 11-mål, vilket inte är kompatibelt med JDK version 1.8 som är standard i Creative Manager Build-miljön. Denna uppdatering kräver att Maven körs med JDK 11.

Vi rekommenderar att man lägger till en `.cloudmanager/java-version` till roten av Git-rapporten med innehållet: `11`. Se [Bygg miljö / Ställa in JDK-versionen av Maven](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#alternate-maven-jdk-version).


### Inbäddade tekniker {#embedded-tech-15860}

| Teknik | Version | Länk |
|---|---|---|
| AEM | 1.60-T20240131102219-0cde853 | [Oak API 1.60.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.60.0/index.html) |
| AEM SLING API | Version 2.27.2 | [API för Apache Sling 2.27.2](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTML | Version 1.4.20-1.4.0 | [HTML-mallens språkspecifikation](https://github.com/adobe/htl-spec) |
| Grundläggande komponenter i AEM | Version 2.24.4 | [AEM WCM-kärnkomponenter](https://github.com/adobe/aem-core-wcm-components) |

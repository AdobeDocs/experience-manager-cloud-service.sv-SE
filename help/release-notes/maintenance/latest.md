---
title: Aktuell underhållsanvisning för [!DNL Adobe Experience Manager] as a Cloud Service.
description: Aktuell underhållsanvisning för [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: dbdc63db9a9ac954ce6359d3643231d6e195fd53
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 1%

---

# Versionsinformation om underhåll {#maintenance-release-notes}

I följande avsnitt beskrivs den tekniska versionsinformationen för den aktuella underhållsutgåvan av Experience Manager as a Cloud Service.

## Utgåva 15575 {#release-15575}

Nedan sammanfattas de kontinuerliga förbättringarna av underhållsutgåvan 15575, som offentliggjordes den 19 mars 2024. Den tidigare underhållsversionen var version 15262.

2024.3.0 Funktionsaktivering innehåller alla funktioner som finns i den här underhållsversionen. Se [Roadmap för lanseringar av Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html) för mer information.

### Förbättringar {#enhancements-15575}

Ingen.

### Åtgärdade problem {#fixed-issues-15575}

* ASSETS-36358: Det går inte att återge överföringsrapporten.
* GRANITE-50774: GraniteContent bör använda deterministisk ordning för egenskapsvärden vid initieringstidpunkten.

### Kända fel {#known-issues-15575}

Ingen.

### Ändringsmeddelande {#change-notice-15575}

**Åtgärder krävs**

#### Ange CM Java-versionen till 11 {#set-java-version-11}

Den nya versionen av aem-sdk-api innehåller klasser som kompilerats med ett Java 11-mål, vilket inte är kompatibelt med JDK version 1.8 som är standard i Creative Manager Build-miljön. Denna uppdatering kräver att Maven körs med JDK 11.

Vi rekommenderar att man lägger till en `.cloudmanager/java-version` till roten av Git-rapporten med innehållet: `11`. Se [Bygg miljö / Ställa in JDK-versionen av Maven](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#alternate-maven-jdk-version).

#### Uppdatera aem-cloud-testing-clients till 1.2.1 {#update-aem-cloud-testing-clients}

Kommande ändringar kräver biblioteket [aem-cloud-testing-clients](https://github.com/adobe/aem-testing-clients) som används i dina anpassade funktionstester för att uppdateras till åtminstone en version **1.2.1**

Se till att ditt beroende `it.tests/pom.xml` har uppdaterats.

```xml
<dependency>
   <groupId>com.adobe.cq</groupId>
   <artifactId>aem-cloud-testing-clients</artifactId>
   <version>1.2.1</version>
</dependency>
```

Denna ändring måste utföras före 6 april 2024.

Om du inte uppdaterar beroendebiblioteket kommer det att uppstå ett pipeline-fel i steget&quot;Custom Functional Testing&quot;.

### Inbäddade tekniker {#embedded-tech-15575}

| Teknik | Version | Länk |
|---|---|---|
| AEM | 1.60-T20240131102219-0cde853 | [Oak API 1.60.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.60.0/index.html) |
| AEM SLING API | Version 2.27.2 | [API för Apache Sling 2.27.2](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTML | Version 1.4.20-1.4.0 | [HTML-mallens språkspecifikation](https://github.com/adobe/htl-spec) |
| Grundläggande komponenter i AEM | Version 2.23.4 | [AEM WCM-kärnkomponenter](https://github.com/adobe/aem-core-wcm-components) |

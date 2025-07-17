---
title: Aktuell information om underhållsversionen av  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Aktuell information om underhållsversionen av  [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 2e90e40a0fe439653987a23792a4c1ec612aafd6
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 2%

---


# Versionsinformation om underhåll {#maintenance-release-notes}

I följande avsnitt beskrivs den tekniska versionsinformationen för den aktuella underhållsversionen av Experience Manager as a Cloud Service.

## Utgåva 21570 {#21570}

Nedan sammanfattas de kontinuerliga förbättringarna av underhållsutgåva 21570, som offentliggjordes den 15 juli 2025. Den tidigare underhållsversionen var version 21484.

>[!NOTE]
>
>[Version 21484](/help/release-notes/maintenance/2025/2025-7-0.md#21484) har gjorts privat och ersatts av version 21570.

Funktionsaktiveringen i 2025.7.0 kommer att innehålla alla funktioner som finns i den här underhållsversionen. Mer information finns i [Experience Manager Releases Roadmap](https://experienceleague.adobe.com/sv/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

### Förbättringar {#enhancements-21570}

* Migrerad till Apache HTTP 2.4.63

### Åtgärdade problem {#fixed-issues-21570}

* SKYOPS-112722 - Korrigerat ett problem som medförde att URL-matchningen för vanity misslyckades

### Kända fel {#known-issues-21570}

* Den samhörande AEM SDK har ett annat versions-ID (21575) och är tillgänglig via portalen för distribution av programvara.
* Apache HTTP Server version 2.4.63 gav upphov till en brytande ändring i hur `mod_rewrite` hanterar frågetecken (`?`) i URL-adresser. Den här ändringen implementerades för att förhindra att flaggan `UnsafeAllow3F` används, vilket ansågs vara en säkerhetsrisk. Detta påverkar alla `RewriteRule`-direktiv som förlitar sig på frågeteckenidentifiering i URL-mönster.

### Föråldrade funktioner och API:er {#deprecated-21570}

Inaktuella och borttagna funktioner och API:er i AEM as a Cloud Service beskrivs i dokumentet [Inaktuella och Borttagna funktioner och API:er](/help/release-notes/deprecated-removed-features.md).

### Säkerhetskorrigeringar {#security-21570}

Ingen

### Inbäddade tekniker {#embedded-tech-21570}

| Teknik | Version | Länk |
|---|---|---|
| AEM Oak | 1.80.0 | [Oak API 1.80.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.80.0/index.html) |
| AEM SLING API | 2.27.6 | [API:t för Apache Sling 2.27.6 ](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [Språkspecifikation för HTML-mall](https://github.com/adobe/htl-spec) |
| Apache HTTP-server | 2.4.63 | [Apache HTTP 2.4.63](https://github.com/apache/httpd/blob/2.4.63/CHANGES) |
| Grundläggande komponenter i AEM | 2.29.0 | [AEM WCM Core Components](https://github.com/adobe/aem-core-wcm-components) |

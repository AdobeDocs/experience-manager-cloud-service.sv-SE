---
title: Aktuell underhållsanvisning för [!DNL Adobe Experience Manager] as a Cloud Service.
description: Aktuell underhållsanvisning för [!DNL Adobe Experience Manager] as a Cloud Service.
source-git-commit: 4aa4954f214545dcd768fdf955f1fc2f776da939
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 1%

---


# Versionsinformation om underhåll {#maintenance-release-notes}

I följande avsnitt beskrivs den tekniska versionsinformationen för den aktuella underhållsutgåvan av Experience Manager as a Cloud Service.

## Utgåva 11835 {#release-11835}

Nedan sammanfattas de kontinuerliga förbättringarna av underhållsutgåvan 11835, som offentliggjordes den 19 april 2023. Den här underhållsversionen är en uppdatering från den tidigare underhållsversionen 11382.

Funktionsaktiveringen för den här underhållsversionen ger dig den fullständiga funktionsuppsättningen. Se [aktuell versionsinformation](/help/release-notes/release-notes-cloud/release-notes-current.md) för fullständig information.

### Åtgärdade problem {#fixed-issues-11835}

- SITES-12573 - GraphQL-frågor som använder variabler i ett filter misslyckas om ingen variabel anges. Please do not update to this release shall you use GraphQL with AEM as a Cloud Service.
- SKYOPS-51970 - Identifierad regression för den FACT-version som används i buildImage-steget, vilket leder till att användarmappningen inte matchar.
- GRANITE-44542 - Problem har rapporterats för kunder som inte angav en paketnodtyp (genom att tillhandahålla en .content.xml med jcr:primaryType) för mappar som ingår i paketfiltret. Detta gjorde att mapparna behandlades som not:folder, vilket i olika fall orsakade problem.
- SKYOPS-56928 - Apache HTTPD-regression kan orsaka 404 fel. Om du får dessa problem av säkerhetsskäl bör du återställa till den tidigare versionen och undvika att rörledningar körs under den tidsperioden.

### Inbäddade tekniker {#embedded-tech-11835}

| Teknik | Version | Länk |
|---|---|---|
| AEM OAK | 1.44-T20221206170501-6d59064 | [API för Oak API 1.4.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.44.0/index.html) |
| AEM SLING API | Version 2.27.0 | [API för Apache Sling 2.27.0](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTML | Version 1.4.20-1.4.0 | [HTML-mallens språkspecifikation](https://github.com/adobe/htl-spec) |
| Grundläggande komponenter i AEM | Version 2.21.2 | [AEM WCM-kärnkomponenter](https://github.com/adobe/aem-core-wcm-components) |

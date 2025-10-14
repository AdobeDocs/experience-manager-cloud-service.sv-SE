---
title: Aktuell information om underhållsversionen av  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Aktuell information om underhållsversionen av  [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 1a1eeb3b9aec839677baadf9bea67993a22f9519
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 0%

---


# Versionsinformation om underhåll {#maintenance-release-notes}

I följande avsnitt beskrivs den tekniska versionsinformationen för den aktuella underhållsversionen av Experience Manager as a Cloud Service.

## Utgåva 22943 {#22943}

Nedan sammanfattas de kontinuerliga förbättringarna av underhållsreleasen 22943, som offentliggjordes den 14 oktober 2025. Den tidigare underhållsversionen var version 22758.

Funktionsaktiveringen i 2025.10.0 kommer att innehålla alla funktioner som finns i den här underhållsversionen. Mer information finns i [Experience Manager Releases Roadmap](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

### Förbättringar {#enhancements-22943}

* ASSETS-57809: Uppdatering av indexdefinition för damAssetLucene-13.
* ASSETS-36521: Förbättrat arbetsflöde för återinläsning av DM för att säkerställa konsekvent efterbearbetning.
* ASSETS-56400: Lagt till ny OTB Zoom PNG-rendering för resurser med genomskinlighet.
* ASSETS-55326: Aktiverad konfigurationsvy för AI-metadatamapp via HTTP-händelser.
* ASSETS-56905: Stöd för anslutning till InDesign via proxy.
* ASSETS-48286: Lägg till CAI-egenskaper i Algolia för GenStudio.
* ASSETS-48653: Använd den osynliga vattenstämpeln i förbearbetningsfasen.
* ASSETS-55874: Migrerar bildförinställning från scen7 till DMWithOpenapi.
* SITES-30452: Förbättringar av innehålls-API för ASO i slutpunkten /content/definition.

### Åtgärdade problem {#fixed-issues-22943}

* ASSETS-56301: Korrigerad export av selektiva metadata som inkluderar PredictedTags i CSV.
* ASSETS-55543: Återanvänd asynkron bearbetningslogik i ett återanvändbart paket.
* ASSETS-54789: Fast NPE i ACLPermissionsValidator när DM ACL är aktiverat.
* ASSETS-55888: Korrigerad rendering av skadlig kod som visas på panelen för gränssnittsåtergivningar.
* GRANITE-62236: Problem med lokalisering av nyckelord i sparade sökningar efter smarta samlingar har åtgärdats.
* GRANITE-61875: Ett hotfix för utvärdering av ogiltiga uttryck har korrigerats som förhindrar att innehållsfragment och hämtningar av resurser sparas.
* SITES-24074: Dold mobil navigering som får fokus under tangentbordsnavigering har åtgärdats.
* SITES-33611: Fixed Live Copy Overview issue for high-volume market.

#### AEM Guides {#guides-22943}

* GUIDES-31421: När flera DITA-kartor eller -ämnen är öppna och ett av avsnitten stängs, överlappas knappen **>>** som visar alla öppna flikar med de återstående öppna flikarna i flikfältet.
* GUIDES-33229: När PDF-filer genereras ignoreras filtreringsreglerna i en DITAVAL-fil om något egenskapsnamn innehåller en punkt.
* GUIDES-33720: När du zoomar i översättningsgränssnittet flyttas knappen Skicka för översättning under ellipsen och aktiveras även utan att någon resurs markeras.
* GUIDES-33590: När en granskare slutför en granskningsåtgärd eller initieraren uppdaterar en granskningsåtgärd utan att skriva några kommentarer, visar det skickade e-postmeddelandet den senaste föregående kommentaren.

Mer information om de nya och förbättrade funktionerna och problemen som har åtgärdats i den här versionen finns i [Experience Manager Guides-lanseringens färdplan](https://experienceleague.adobe.com/en/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

### Föråldrade funktioner och API:er {#deprecated-22943}

Inaktuella och borttagna funktioner och API:er i AEM as a Cloud Service beskrivs i dokumentet [Inaktuella och Borttagna funktioner och API:er](/help/release-notes/deprecated-removed-features.md).

### Säkerhetskorrigeringar {#security-22943}

AEM as a Cloud Service strävar efter att optimera säkerheten och prestandan för din plattform. Denna underhållsrelease åtgärdar 14 identifierade sårbarheter, vilket stärker vårt engagemang för robust systemskydd.

### Ändringsmeddelande

* Den här versionen innehåller följande nya produktindexversioner:
* **damAssetLucene-13**

### Inbäddade tekniker {#embedded-tech-22943}

| Teknik | Version | Länk |
|---|---|---|
| AEM Oak | 1.86.0 | [Oak 1.86.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.86/index.html) |
| AEM SLING API | 2.27.6 | [API:t för Apache Sling 2.27.6 &#x200B;](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [Språkspecifikation för HTML-mall](https://github.com/adobe/htl-spec) |
| Apache HTTP-server | 2.4.65 | [Apache HTTP 2.4.65](https://apache.googlesource.com/httpd/+/refs/tags/2.4.65/CHANGES) |
| Grundläggande komponenter i AEM | 2.30.2 | [AEM WCM Core Components](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14 (standard) | [Node.js-versioner som stöds](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |

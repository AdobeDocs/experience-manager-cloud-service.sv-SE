---
title: Aktuell underhållsversionsinformation för  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Aktuell underhållsversionsinformation för  [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: a3c414f9b5e575856a942e02661e8c70a7083495
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 1%

---


# Versionsinformation om underhåll {#maintenance-release-notes}

I följande avsnitt beskrivs de tekniska versionsinformationen för den aktuella underhållsutgåvan av Experience Manager as a Cloud Service.

## Utgåva 19149 {#19149}

Nedan sammanfattas de kontinuerliga förbättringarna av underhållsreleasen 19149, som offentliggjordes den 21 januari 2025. Den tidigare underhållsversionen var version 18751.

Funktionsaktiveringen i 2025.1.0 kommer att innehålla alla funktioner som finns i den här underhållsversionen. Mer information finns i [Experience Manager Releases Roadmap](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

### Förbättringar {#enhancements-19149}

* ASSETS-45286: Visa detaljerade förlopp för nedladdning av arkiveringsasynkront jobb.
* ASSETS-46296: Stöd för Dynamic Media-mallar i resursväljaren.
* ASSETS-44796: Starta Assets Events för asynkrona DAM-resursjobb.

### Åtgärdade problem {#fixed-issues-19149}

* GRANITE-55074: Kontrollera att CORS-svarshuvuden är inställda på felsvar.
* ASSETS-43755: Skalbarhetsförbättringar för att relatera till massresurser.
* ASSETS-45399: Dirigera om till Assets Console när du har skapat en live-copy för resurs.
* ASSETS-45462: Problem med webbläsarcachelagring med anpassade mappminiatyrer.
* ASSETS-46398: Dölj åtgärderna Hämta och bearbeta om för DM-mallar.
* ASSETS-44484: Problem med att spara om konfigurationen för anslutna Assets.
* ASSETS-44122: Jobbet Async copy assets ändrar inte namn på målmappen vid kopiering till den aktuella mappen.
* ASSETS-44463: Knappen Hämta CSV visas inte vid lyckad metadataexport.
* ASSETS-45134: Flyttjobb med måltitel åsidosätter alla mapptitlar.
* ASSETS-45137: Konflikter med massöverföring via Assets View.
* ASSETS-45758: Resursrelationer får en oändlig upptagnings-/inläsningsanimering efter att en relation har lagts till.
* ASSETS-44148: NODE_MOVED-händelse i AEM kan orsaka oönskad NPE i loggar.
* ASSETS-28607: JS-fel vid inställning av anpassad videominiatyr.
* GRANITE-55781: Förbättra gruppsynkroniseringen mellan Adobe Developer Console och AEM. Mer information finns i [Förändringar i användargruppen och produktprofilssynkroniseringen](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/security/changes-in-user-group-and-product-profile-synchronization).
* GRANITE-55754: Säkerställ att SDK startskript stöder Java 21.
* GRANITE-54248: Det går inte att bläddra igenom alla objekt i en stor resursmapp.
* SCRNS-4597: Förbättringar i sökresultatlistvyn.


### Kända fel {#known-issues-19149}

Ingen.

### Föråldrade funktioner och API:er {#deprecated-19149}

Inaktuella och borttagna funktioner och API:er i AEM as a Cloud Service beskrivs i dokumentet [Inaktuella och Borttagna funktioner och API:er](/help/release-notes/deprecated-removed-features.md).

#### Ändringar i synkronisering av användargrupp och produktprofil

När du använder Adobe Admin Console för behörighetshantering FÅR följande grupper INTE användas eftersom de inte längre kommer att synkroniseras med AEM:
* AEM som slutar med _GROUP_NAME_SUFFIX.
* Produktprofiler från andra miljöer, program eller produkter.

Mer information finns i [Ändringar i användargruppen och produktprofilssynkroniseringen](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/security/changes-in-user-group-and-product-profile-synchronization).

#### Borttagning av SPA {#deprecate-spa-editor}

[SPA redigerare](/help/implementing/developing/hybrid/introduction.md) har tagits bort för nya projekt från och med version 2025.1.0. SPA Editor stöds fortfarande för befintliga projekt, men bör inte användas för nya projekt.

De redigerare som rekommenderas för att hantera innehåll utan AEM är:

* [Den universella redigeraren](/help/edge/wysiwyg-authoring/authoring.md) för visuell redigering.
* [Innehållsfragmentsredigeraren](/help/assets/content-fragments/content-fragments-managing.md) för formulärbaserad redigering.

### Säkerhetskorrigeringar {#security-19149}

AEM as a Cloud Service strävar efter att optimera säkerheten och prestandan för din plattform. Denna underhållsrelease åtgärdar fyra identifierade sårbarheter, vilket stärker vårt engagemang för robust systemskydd.

### Inbäddade tekniker {#embedded-tech-19149}

| Teknik | Version | Länk |
|---|---|---|
| AEM Oak | 1.72.0 | [Oak API 1.72.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.72.0/index.html) |
| AEM SLING API | 2.27.6 | [API:t för Apache Sling 2.27.6 ](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTML | 1.4.24-1.4.0 | [Språkspecifikation för HTML-mall](https://github.com/adobe/htl-spec) |
| Grundläggande komponenter i AEM | 2.27.0 | [AEM WCM-kärnkomponenter](https://github.com/adobe/aem-core-wcm-components) |

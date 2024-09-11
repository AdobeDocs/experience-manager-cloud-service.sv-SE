---
title: Aktuell underhållsversionsinformation för  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Aktuell underhållsversionsinformation för  [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 9323464610b804ff407f5eedf404ab2cca93a8da
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 1%

---


# Versionsinformation om underhåll {#maintenance-release-notes}

I följande avsnitt beskrivs de tekniska versionsinformationen för den aktuella underhållsutgåvan av Experience Manager as a Cloud Service.

## Utgåva 17689 {#release-17689}

Nedan sammanfattas de kontinuerliga förbättringarna av underhållsutgåvan 17689, som offentliggjordes den 10 september 2024. Den tidigare underhållsversionen var version 17569.

Funktionsaktiveringen i 2024.9.0 kommer att innehålla alla funktioner som finns i den här underhållsversionen. Mer information finns i [Experience Manager Releases Roadmap](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

### Förbättringar {#enhancements-17689}

* ASSETS-41404: Ändringar som har stöd för DRM-förbättringar.
* ASSETS-41621: Uppdaterat asynkront kopieringsjobb.
* ASSETS-32166: Uppdaterat asynkront resursflyttningsjobb.
* ASSETS-41429: Stöd för bildförinställningar i DM OpenAPI.
* ASSETS-38968: Förbättra återgivningen av Content Fragments-referenser.
* ASSETS-41787, ASSETS-41183: Förbättringar för ramverket Assets Bulk Operations.
* GRANITE-52917: Optimeringar som förbättrar installationstiden för innehållskopia.
* SCRNS-3980: Identifiera gråskärm på spelare som har sekvenser utan schemalagda resurser.

### Åtgärdade problem {#fixed-issues-17689}

* ASSETS-40875: Icke-förstörande NPE loggad av AssetDeleteHandler.
* ASSETS-42422: Undvik att utlösa asynkrona jobb för flyttning av enstaka resurser.
* ASSETS-41234: Enhetligt gränssnitt - Global navigering kanske inte fungerar om den öppnas när sökfältet är öppet.
* ASSETS-42256: Enhetligt gränssnitt - Tagg/Badge-indikeringsmiljön fungerar bara då och då.
* ASSETS-41271: Förhindra att Assets publiceras på nytt i onödan under flyttningsåtgärder.
* ASSETS-38894: Begränsa återförsök genom att bearbeta övervakningsenheten.
* ASSETS-40815: Använd PDF-renderingen för förhandsgranskning för att visa PPT-filen i användargränssnittet för länkdelning.
* ASSETS-37123: Det går inte att läsa in förhandsgranskning av resurs i dialogrutan Länkdelning.
* CQ-4358156: Uppdaterar bakgrunder till taggen som tas bort.
* SCRNS-4495: Knappen Klistra in som åtgärdats fungerar inte korrekt för olika användargrupper.
* SCRNS-4512: Ta bort komponenter som är relaterade till enheten från AEMaaCS-skärmar.
* SCRNS-4466: Dölj - Visa manifest, generera offlineinnehåll, uppdatera manifestcache, visningspanel på panelen i Channel Dashboard.
* SCRNS-4513: Lägg till kolumnrubriker för sökresultatsidan i listvyn.

### Kända fel {#known-issues-17689}

* FORMS-14340: Fel vid instansiering av FormsAndDocumentOmniSearchHandler och CloudStorageSubmitActionInserter. Det här är ofarliga loggsatser.
* FORMS-15818: Komponentbeskrivningspost&quot;OSGI-INF/com.adobe.aemfd.docmanager.impl.*.xml kan inte hitta satser i serverloggar. Det här är ofarliga loggsatser.
* SITES-23662: Användare som utlöser en publicering kan inte extraheras från JCR-loggsatser i serverloggar. Det här är en funktion under utveckling som kan orsaka fel av typen&quot;Det går inte att hitta ett giltigt användar-ID i gruppen med OSGI-händelser&quot; i loggen.

### Ändringsmeddelande {#change-notice-17689}

* Från och med september 2024 kommer AEM as a Cloud Service att inaktivera serialiseringen av resurslösare via Sling Model Exporter-ramverket. Mer information finns i [dokumentationen](/help/implementing/developing/hybrid/disallow-the-serialization-of-resourceresolvers-via-sling-model-exporter.md).

### Föråldrade funktioner och API:er {#deprecated-17689}

Observera att vi håller på att uppdatera `com.day.cq.wcm.api` och med den aktuella versionen har vi markerat `@Deprecated` som några av dess metoder och klasser. Dessa kommer att tas bort i framtida versioner, så överväg att byta till de föreslagna alternativen om du använder något av dem.

Inaktuella och borttagna funktioner och API:er i AEM as a Cloud Service beskrivs i dokumentet [Inaktuella och Borttagna funktioner och API:er](/help/release-notes/deprecated-removed-features.md).

### Säkerhetskorrigeringar {#security-17689}

AEM as a Cloud Service strävar efter att optimera säkerheten och prestandan för din plattform. Denna underhållsrelease åtgärdar fyra identifierade sårbarheter, vilket stärker vårt engagemang för robust systemskydd.

### Inbäddade tekniker {#embedded-tech-17689}

| Teknik | Version | Länk |
|---|---|---|
| AEM Oak | 1.68.0 | [Oak API 1.68.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.68.0/index.html) |
| AEM SLING API | 2.27.6 | [API:t för Apache Sling 2.27.6 ](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTML | 1.4.24-1.4.0 | [Språkspecifikation för HTML-mall](https://github.com/adobe/htl-spec) |
| Grundläggande komponenter i AEM | 2.26.0 | [AEM WCM-kärnkomponenter](https://github.com/adobe/aem-core-wcm-components) |

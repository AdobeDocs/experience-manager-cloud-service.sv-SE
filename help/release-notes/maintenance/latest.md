---
title: Aktuell underhållsversionsinformation för  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Aktuell underhållsversionsinformation för  [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 9278ec9bb5bccd7b40cd65a120f296faba454b9c
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 1%

---


# Versionsinformation om underhåll {#maintenance-release-notes}

I följande avsnitt beskrivs de tekniska versionsinformationen för den aktuella underhållsutgåvan av Experience Manager as a Cloud Service.

## Utgåva 18311 {#18311}

Nedan sammanfattas de kontinuerliga förbättringarna av underhållsutgåvan 18311, som offentliggjordes den 22 oktober 2024. Den tidigare underhållsversionen var version 18175.

Funktionsaktiveringen i 2024.10.0 kommer att innehålla alla funktioner som finns i den här underhållsversionen. Mer information finns i [Experience Manager Releases Roadmap](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

### Förbättringar {#enhancements-18311}

* ASSETS-41820: Indexeringsförbättringar för bearbetning av watchdog.
* ASSETS-43720: Funktionsförbättringar för bearbetning av övervakningsenhet.
* ASSETS-42554: Prestandaförbättringar för stora mappar.
* SKYOPS-77603: Hantering av omdirigeringar av företagsanvändare.

### Åtgärdade problem {#fixed-issues-18311}

* ASSETS-37534: Ändringar i sökningen visar inte den egenskap som används för godkännandemålet.
* ASSETS-38322: Ta bort publiceringsvillkorsproviderkonfiguration Ta bort publiceringshändelsefunktion.
* ASSETS-40482: Problem med tillgänglighet vid uppspelning/paus och knappen Stäng av/slå på i Scene7 videospelare.
* ASSETS-40593: Felsidan visas när du klickar på knappen &quot;Egenskaper&quot; i Assets > Filer.
* ASSETS-40598: Synkronisera smarta beskärningar när osynkroniserad resurs flyttas till en mapp som är aktiverad för synkronisering.
* ASSETS-40743: Problem med att utlösa dialogrutan Ersätt resurs när vissa tecken finns i filnamnet.
* ASSETS-40825: Assets Search Facets försvinner när sökformuläret har redigerats.
* ASSETS-41007: Borttagning av AEM lämnar ibland Assets vid leveransen som föräldralöst.
* ASSETS-41172: Specialtecken för Dynamic Media-mallar tillåts inte i namn.
* ASSETS-41896: Assets som omnämns i cq:discarded property on the folder ska INTE publiceras till Brand Portal.
* ASSETS-42067: Dynamic Media-mallar - Nedladdning ger fel.
* ASSETS-42070: Dynamic Media-mallar - användare som inte är administratörer bör ha behörighet att skapa/redigera mallar.
* ASSETS-42344: Ansluten Assets-synkronisering är frånkopplad - Koppla upp och få kundråd.
* ASSETS-42620: Problem med förhandsvisningsalternativet för resursversioner - visar en tom förhandsvisning när vi öppnar resursen.
* ASSETS-42701: Web Optimized Image Delivery and Cropping Issue.
* ASSETS-42966: Async Barcade kan tas bort om flera jobb delar samma sökväg.
* ASSETS-43072: Dynamic Media-mallar - Sökningar efter mallreferenser i en ogiltig referens.
* ASSETS-43212: Internationaliseringsproblem i schemaredigeraren för metadata.
* ASSETS-43202: Korrigeringar för att välja anteckningar att skriva ut från tidslinjen.
* ASSETS-43502: Namnet på AEM befintliga bildförinställningen visas inte på redigeringssidan.
* ASSETS-43538: Jobbet Async copy assets använder en felaktig egenskap för källsökvägen.
* ASSETS-43798: Kontrollera målsökvägen innan du kopierar resurser.
* ASSETS-43945: Öka fördröjningen för nya försök till 20 min för jobbkön för asynkrona resurser.
* ASSETS-44025: Jobbet för asynkron borttagning av resurser misslyckas när enskilda resurser väljs.
* SITES-26128: Undantag för klassskiftning i CreateLiveCopyStep.
* SCRNS-4551: [SG Pools] Screens-kanal som innehåller videokomponenten visar &quot;General Page Error&quot; i webbläsarförhandsvisning och spelare

### Kända fel {#known-issues-18311}

* FORMS-15818: Komponentbeskrivningsposten `OSGI-INF/com.adobe.aemfd.docmanager.impl.*.xml` hittade inte programsatser i serverloggar. Det här är ofarliga loggsatser.

### Föråldrade funktioner och API:er {#deprecated-18311}

Inaktuella och borttagna funktioner och API:er i AEM as a Cloud Service beskrivs i dokumentet [Inaktuella och Borttagna funktioner och API:er](/help/release-notes/deprecated-removed-features.md).

### Säkerhetskorrigeringar {#security-18311}

AEM as a Cloud Service strävar efter att optimera säkerheten och prestandan för din plattform. Denna underhållsrelease åtgärdar tre identifierade sårbarheter, vilket stärker vårt engagemang för robust systemskydd.

### Inbäddade tekniker {#embedded-tech-18311}

| Teknik | Version | Länk |
|---|---|---|
| AEM Oak | 1.70.0 | [Oak API 1.70.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.70.0/index.html) |
| AEM SLING API | 2.27.6 | [API:t för Apache Sling 2.27.6 ](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTML | 1.4.24-1.4.0 | [Språkspecifikation för HTML-mall](https://github.com/adobe/htl-spec) |
| Grundläggande komponenter i AEM | 2.27.0 | [AEM WCM-kärnkomponenter](https://github.com/adobe/aem-core-wcm-components) |

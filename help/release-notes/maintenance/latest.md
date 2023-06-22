---
title: Aktuell underhållsanvisning för [!DNL Adobe Experience Manager] as a Cloud Service.
description: Aktuell underhållsanvisning för [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 46f0f8ba51b328bef1061d574b0d378a510fcf38
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 1%

---

# Versionsinformation om underhåll {#maintenance-release-notes}

I följande avsnitt beskrivs den tekniska versionsinformationen för den aktuella underhållsutgåvan av Experience Manager as a Cloud Service.

## Version 12255 {#release-12255}

Nedan sammanfattas de kontinuerliga förbättringarna av underhållsreleasen 12255, som offentliggjordes den 13 juni 2023. Den här underhållsversionen är en uppdatering från den tidigare underhållsversionen 12142.

Funktionsaktiveringen för den här underhållsversionen ger dig tillgång till alla funktioner som är aktiverade i 2023.6.0. Se [Roadmap för lansering av Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html) för mer information.

### Förbättringar {#enhancements-12255}

Ingen.

### Åtgärdade problem {#fixed-issues-12255}

- Olika tillgänglighetsrelaterade uppdateringar
- ASSETS-15116 - Alternativet &quot;Gå till plats&quot; är tillgängligt i resursens sökvy
- ASSETS-17453 - (Dynamic Media) Det går inte att välja en anpassad miniatyrbild för videoklipp
- ASSETS-19279 - Arkiv för hämtning av resurser för stora filer
- ASSETS-19544 - Senast ändrad av användaren för resursuppdateringar
- ASSETS-20146 - (Touch UI) Rapporter om misslyckade hämtningsrapporter på grund av valideringsfel visas alltid högst upp på listsidan för rapporter
- ASSETS-21056 - Optimera prestanda för resursreferens för att minimera skrivningar
- ASSETS-21909 - Det går inte att se videon med smart beskärning när videon inte kan hämtas
- ASSETS-22261 - Mappstrukturen för Linkshare-hämtningar är inkonsekvent med resursgränssnittets hämtningar
- ASSETS-22550 - sökfilterpanelen är nu öppen som standard
- ASSETS-22920 - Avpubliceringsmappen från Brand Portal markerar inte resurserna i som opublicerade
- ASSETS-22922 - Inaktiverade visningsprogramförinställningar visas i Dynamic Media-komponenten
- ASSETS-23461 - sökvyn Brand Portal Snabbpublicering från resurser
- ASSETS-23466 - Länkhantering som inte går att komma åt i InDesign Server kan inte matcha AAL-länkar som innehåller blanksteg
- ASSETS-23469 - Standardresursfilter kolliderade med anpassade filter
- ASSETS-23981 - Sorteringsfunktionen för titlar som inte fungerar i samlingslänkar
- ASSETS-24723 - Publicerade resurser bearbetades på nytt utan att användaren behövde göra något
- GRANITE-45385 - Migrera trädaktivering så att sling-jobb används i stället för arbetsflöde

### Kända fel {#known-issues-12255}

- ASSETS-25729 - Visa väljarmenyn är inaktiverad
- ASSETS-25728 - alternativet Bearbeta om resurs är inte tillgängligt i sökvyn
- ASSETS-22603 - Vissa kolumner för tillgångsrapport av hämtningstyp visar &quot;null&quot;-värden i användargränssnittet. Hämtningsbar CSV-fil påverkas inte.

### Inbäddade tekniker {#embedded-tech-12255}

| Teknik | Version | Länk |
|---|---|---|
| AEM OAK | 1.50-T20230405052634-f9df4aa | [Oak API 1.50.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.50.0/index.html) |
| AEM SLING API | Version 2.27.0 | [API för Apache Sling 2.27.0](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTML | Version 1.4.20-1.4.0 | [HTML-mallens språkspecifikation](https://github.com/adobe/htl-spec) |
| Grundläggande komponenter i AEM | Version 2.23.0 | [AEM WCM-kärnkomponenter](https://github.com/adobe/aem-core-wcm-components) |

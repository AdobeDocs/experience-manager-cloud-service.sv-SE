---
title: Testning av innehållsgranskning - Cloud Services
description: Testning av innehållsgranskning - Cloud Services
translation-type: tm+mt
source-git-commit: 27f9f4441a95964a4ae0db798577510c726133c5
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 0%

---


# Testning av innehållsgranskning {#content-audit-testing}

Content Audit är en funktion som finns i Cloud Manager Sites Production pipelines, ett verktyg med öppen källkod från Google. Den här funktionen är aktiverad i alla produktionspipelinjer för Cloud Manager.

Den validerar distributionsprocessen och säkerställer att ändringar som distribueras:

1. Uppfyll grundläggande standarder för prestanda, tillgänglighet, bästa praxis, SEO (Search Engine Optimization) och PWA (Progressive Web App).

1. Inkludera inte regressioner i dessa dimensioner.

Content Audit i Cloud Manager säkerställer att slutanvändarnas digitala upplevelse på webbplatsen kan underhållas enligt högsta standard. Resultaten är informativa och gör att användaren kan se poängen och ändringen mellan den aktuella och den tidigare poängen. Den här insikten är värdefull för att avgöra om det finns en regression som kommer att introduceras i den aktuella distributionen.

## Om granskningsresultat för innehåll {#understanding-content-audit-results}

Content Audit ger aggregerade och detaljerade testresultat på sidnivå via körningssidan för Production Pipeline.

* Mätvärden för aggregerad nivå mäter medelpoängen för de sidor som granskades.
* Enskilda sidnivåpoäng kan också göras via fördjupning.
* Det finns uppgifter om poängen för att se vilka resultat de enskilda testerna ger, tillsammans med vägledning om hur man åtgärdar eventuella problem som upptäcktes under innehållsgranskningen.
* En historik över testresultaten sparas i Cloud Manager så att kunderna kan se om de ändringar som införs i pipeline-körningen innehåller några regressioner från föregående körning.

### Sammanställd bakgrundsmusik {#aggregate-scores}

Det finns ett aggregerat nivåpoäng för varje testtyp (prestanda, hjälpmedel, SEO, bästa praxis och PWA).

Poängen för sammanställd nivå tar medelpoängen för de sidor som ingår i körningen. Ändringen på aggregeringsnivå representerar medelpoängen för sidorna i den aktuella körningen jämfört med medelvärdet för poängen från föregående körning, även om den sidsamling som konfigurerats att inkluderas har ändrats mellan körningar.

Värdet för Change-måttet kan vara något av följande:

* **Positivt värde** - sidan/sidorna har förbättrats på det valda testet sedan den senaste produktionskanalen kördes

* **Negativt värde** - sidan/sidorna har gått om på det valda testet sedan den senaste körningen av produktionsflödet

* **Ingen ändring** - sidan/sidorna har fått samma resultat sedan den senaste produktionspipeline-körningen

* **Ej tillämpligt** - det fanns ingen tidigare poäng att jämföra med

   ![](/help/implementing/developing/introduction/assets/content-audit-test1.png)

### Poäng på sidnivå {#page-level-scores}

Genom att gå in i något av testerna kan man se en mer detaljerad sidnivåbedömning. Användaren kommer att kunna se hur de enskilda sidorna sparades för det specifika testet tillsammans med ändringen från den föregående gången testet kördes.

Om du klickar på detaljerna för en enskild sida visas information om de element på sidan som har utvärderats och vägledning för att åtgärda problem om möjligheter till förbättring upptäcks. Detaljer om testerna och tillhörande vägledning tillhandahålls av Google Lighthuse.

![](/help/implementing/developing/introduction/assets/page-level-scores.png)


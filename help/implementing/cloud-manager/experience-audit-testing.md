---
title: Experience Audit Testing - Cloud Services
description: Experience Audit Testing - Cloud Services
translation-type: tm+mt
source-git-commit: 561345f58ce8e448176507e3bba114324dc18256
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 0%

---


# Testning av Experience Audit {#experience-audit-testing}

Experience Audit är en funktion som finns i Cloud Manager Sites Production pipelines, ett verktyg med öppen källkod från Google. Den här funktionen är aktiverad i alla produktionspipelinjer för Cloud Manager.

Den validerar distributionsprocessen och säkerställer att ändringar som distribueras:

1. Uppfyll grundläggande standarder för prestanda, tillgänglighet, bästa praxis, SEO (Search Engine Optimization) och PWA (Progressive Web App).

1. Inkludera inte regressioner i dessa dimensioner.

Experience Audit i Cloud Manager säkerställer att slutanvändarnas digitala upplevelse på webbplatsen kan upprätthållas enligt högsta standard. Resultaten är informativa och gör att användaren kan se poängen och ändringen mellan den aktuella och den tidigare poängen. Den här insikten är värdefull för att avgöra om det finns en regression som kommer att introduceras i den aktuella distributionen.

## Upplevelsegranskningsresultat {#understanding-experience-audit-results}

Experience Audit ger aggregerade och detaljerade testresultat på sidnivå via sidan för körning av produktionspipeline.

* Mätvärden för aggregerad nivå mäter medelpoängen på de sidor som granskats med avseende på prestanda, tillgänglighet, bästa praxis, SEO (sökmotoroptimering).
   >[!NOTE]
   >Progressive Web App-poäng (PWA) ingår inte i sammanfattningspoängen och visas endast på informationsskärmen på sidnivå.
* Enskilda sidnivåpoäng kan också göras via fördjupning.
* Det finns uppgifter om poängen för att se vilka resultat de enskilda testerna ger, tillsammans med vägledning om hur man åtgärdar eventuella problem som upptäcktes under innehållsgranskningen.
* En historik över testresultaten sparas i Cloud Manager så att kunderna kan se om de ändringar som införs i pipeline-körningen innehåller några regressioner från föregående körning.

### Sammanställd bakgrundsmusik {#aggregate-scores}

Det finns en sammanställd nivå för varje testtyp, som prestanda, tillgänglighet, SEO och bästa praxis.
>[!NOTE]
>Progressive Web App-poäng (PWA) ingår inte i sammanfattningspoängen och visas endast på informationsskärmen på sidnivå.

Poängen för sammanställd nivå tar medelpoängen för de sidor som ingår i körningen. Ändringen på aggregeringsnivå representerar medelpoängen för sidorna i den aktuella körningen jämfört med medelvärdet för poängen från föregående körning, även om den sidsamling som konfigurerats att inkluderas har ändrats mellan körningar.

Värdet för Change-måttet kan vara något av följande:

* **Positivt värde** - sidan/sidorna har förbättrats på det valda testet sedan den senaste produktionskanalen kördes

* **Negativt värde** - sidan/sidorna har gått om på det valda testet sedan den senaste körningen av produktionsflödet

* **Ingen ändring** - sidan/sidorna har fått samma resultat sedan den senaste produktionspipeline-körningen

* **Ej tillämpligt** - det fanns ingen tidigare poäng att jämföra med

   ![](/help/implementing/cloud-manager/assets/exp-audit-1.png)


### Poäng på sidnivå {#page-level-scores}

Genom att gå in i något av testerna kan man se en mer detaljerad sidnivåbedömning. Användaren kommer att kunna se hur de enskilda sidorna sparades för det specifika testet tillsammans med ändringen från den föregående gången testet kördes.

Om du klickar på detaljerna för en enskild sida visas information om de element på sidan som har utvärderats och vägledning för att åtgärda problem om möjligheter till förbättring upptäcks. Detaljer om testerna och tillhörande vägledning tillhandahålls av Google Lighthuse.

![](/help/implementing/cloud-manager/assets/exp-audit-2.png)


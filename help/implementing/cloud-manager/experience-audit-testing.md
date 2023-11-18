---
title: Testning av Experience Audit
description: Läs om hur Experience Audit validerar er distributionsprocess och ser till att de ändringar som driftsätts uppfyller grundläggande standarder för prestanda, tillgänglighet, bästa praxis och SEO.
exl-id: 8d31bc9c-d38d-4d5b-b2ae-b758e02b7073
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 0%

---


# Testning av Experience Audit {#experience-audit-testing}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_expaudittesting"
>title="Testning av Experience Audit"
>abstract="Läs om hur Experience Audit validerar er distributionsprocess och ser till att de ändringar som driftsätts uppfyller grundläggande standarder för prestanda, tillgänglighet, bästa praxis och SEO."

Läs om hur Experience Audit validerar er distributionsprocess och ser till att de ändringar som driftsätts uppfyller grundläggande standarder för prestanda, tillgänglighet, bästa praxis och SEO.

## Översikt {#overview}

Experience Audit är en funktion i Cloud Manager Sites Production pipelines som validerar distributionsprocessen och hjälper till att säkerställa att ändringar som distribueras:

1. Uppfyll grundläggande standarder för prestanda, tillgänglighet, bästa praxis, SEO (Search Engine Optimization) och PWA (Progressive Web App).

1. Inför inte regressioner.

Experience Audit i Cloud Manager säkerställer att slutanvändarens upplevelse på webbplatsen är av högsta standard.

Granskningsresultaten är informativa och gör det möjligt för distributionshanteraren att se poängen och ändringen mellan aktuella och tidigare poäng. Den här insikten är värdefull för att avgöra om det finns en regression som introducerades i den aktuella distributionen.

Experience Audit drivs av Google Lightroom, ett verktyg med öppen källkod från Google, och är aktiverat i alla produktionspipelines i Cloud Manager.

>[!INFO]
>
>Från och med 31 augusti 2023 kommer Experience Audit att gå över till att visa resultat som är specifika för den mobila plattformen. Observera att mobilprestandamätningar vanligtvis registrerar lägre värden än stationära datorer, så du bör förutse en förändring i rapporterade prestanda efter den här ändringen.

>[!TIP]
>
>Du konfigurerar vilka sidor som ska ingå i Experience Audit när du [konfigurera din pipeline](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#full-stack-code).

## Upplevelsegranskningsresultat {#understanding-experience-audit-results}

Experience Audit ger aggregerade och detaljerade testresultat på sidnivå via [körningssida för produktionsflöde](/help/implementing/cloud-manager/deploy-code.md).

* Sammanlagda mätvärden mäter medelpoängen på de sidor som granskats för prestanda, tillgänglighet, bästa praxis, SEO (sökmotoroptimering).
* Enskilda sidnivåpoäng kan också göras via fördjupning.
* Detaljerad information om poängen finns tillgänglig för att visa resultaten av de enskilda testerna tillsammans med vägledning om hur man åtgärdar eventuella problem som identifierats.
* En historik över testresultaten finns kvar i Cloud Manager för att avgöra om ändringar som införs i pipeline inkluderar eventuella regressioner från föregående körning.

### Sammanställd bakgrundsmusik {#aggregate-scores}

Poängen för sammanställd nivå tar medelpoängen för de sidor som ingår i körningen. Ändringen på aggregeringsnivå representerar medelpoängen för sidorna i den aktuella körningen jämfört med medelvärdet för poängen från föregående körning, även om den sidsamling som konfigurerats att inkluderas har ändrats mellan körningar.

Det finns en sammanställd nivå för varje testtyp, som prestanda, tillgänglighet, SEO och bästa praxis.

Ändringsmåttet kan ha något av följande värden.

* **Positivt värde** - Sidorna har förbättrats på det valda testet sedan den senaste produktionspipeline-körningen.

* **Negativt värde** - sidan/sidorna har gått om på det valda testet sedan den senaste produktionspipeline-körningen.

* **Ingen ändring** - Sidorna har fått samma resultat sedan den senaste produktionsflödet.

* **Ej tillämpligt** - Det fanns inga tidigare poäng att jämföra.

![Resultat av granskning](/help/implementing/cloud-manager/assets/exp-audit-1.png)

### Poäng på sidnivå {#page-level-scores}

Genom att gå igenom något av testerna blir det lättare att göra en mer detaljerad sidnivåbedömning. Du kan se hur de enskilda sidorna sparades för det specifika testet tillsammans med ändringen från föregående testkörning.

Om du klickar på detaljerna för en enskild sida får du information om vilka element på sidan som har utvärderats och vägledning för att åtgärda problem om möjligheter till förbättring upptäcks.

![Poäng på sidnivå](/help/implementing/cloud-manager/assets/exp-audit-2.png)

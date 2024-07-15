---
title: Testning av Experience Audit
description: Läs om hur Experience Audit validerar er distributionsprocess och ser till att de ändringar som driftsätts uppfyller grundläggande standarder för prestanda, tillgänglighet, bästa praxis och SEO.
exl-id: 8d31bc9c-d38d-4d5b-b2ae-b758e02b7073
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '890'
ht-degree: 0%

---


# Testning av Experience Audit {#experience-audit-testing}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_expaudittesting"
>title="Testning av Experience Audit"
>abstract="Läs om hur Experience Audit validerar er distributionsprocess och ser till att de ändringar som driftsätts uppfyller grundläggande standarder för prestanda, tillgänglighet, bästa praxis och SEO."

Läs om hur Experience Audit validerar er distributionsprocess och ser till att de ändringar som driftsätts uppfyller grundläggande standarder för prestanda, tillgänglighet, bästa praxis och SEO.

## Ökning {#overview}

Experience Audit är en funktion i Cloud Manager Sites Production pipelines som validerar driftsättningsprocessen och säkerställer att ändringar som distribueras:

1. Uppfyll grundläggande standarder för prestanda, tillgänglighet, bästa praxis, SEO (Search Engine Optimization) och PWA (Progressive Web App).

1. Inför inte regressioner.

Med Experience Audit i Cloud Manager säkerställs att användarens upplevelse på webbplatsen är av högsta standard.

Granskningsresultaten är informativa och gör det möjligt för distributionshanteraren att se poängen och ändringen mellan aktuella och tidigare poäng. Den här insikten är värdefull för att avgöra om det finns en regression som introducerades i den aktuella distributionen.

Experience Audit drivs av Google Lightroom, ett verktyg med öppen källkod från Google.

>[!INFO]
>
>Från och med 31 augusti 2023 kommer Experience Audit att gå över till att visa resultat som är specifika för den mobila plattformen. Mätvärden för mobila prestanda registrerar vanligtvis lägre än de för stationära datorer, så du bör förutse en förändring i rapporterade prestanda efter den här ändringen.

## Tillgänglighet {#availability}

Experience Audit finns för Cloud Manager:

* Sites production pipelines, som standard.
* Utvecklingsledningar för frontend, om du vill.

Mer information om hur du konfigurerar granskningen för de valfria miljöerna finns i avsnittet [Konfiguration](#configuration).

## Konfiguration {#configuration}

Experience Audit är tillgängligt som standard för produktionspipelines. Den kan även aktiveras för frontutvecklingspipelines. I samtliga fall måste du definiera vilka innehållssökvägar som utvärderas under pipeline-körningen.

Du konfigurerar vilka sidor som ska ingå i Experience Audit när du konfigurerar din pipeline.

1. Beroende på vilken typ av pipeline du vill konfigurera kan du följa anvisningarna för att:

   * Lägg till en ny [produktionspipeline,](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md), om du vill definiera sökvägarna som ska utvärderas av granskningen.
   * Lägg till en ny [icke-produktionspipeline](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md) om du vill aktivera granskningen för en frontendpipeline eller en fullständig utvecklingspipeline.
   * Du kan också [redigera en befintlig pipeline](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md) och uppdatera befintliga alternativ.

1. Om du lägger till eller redigerar ett icke-produktionsflöde som du vill använda Experience Audit för, måste du markera kryssrutan **Experience Audit** på fliken **Source Code**.

   ![Aktiverar Experience Audit](assets/experience-audit-enable.jpg)

   * Detta är endast nödvändigt för rörledningar som inte är avsedda för produktion.
   * Fliken **Experience Audit** visas när kryssrutan är markerad.

1. För pipelines för både produktion och icke-produktion definierar du sökvägarna som ska inkluderas i Experience Audit på fliken **Experience Audit** .

   * Sidsökvägarna måste börja med `/` och är relativa till din plats.
   * Om din webbplats till exempel är `wknd.site` och vill inkludera `https://wknd.site/us/en/about-us.html` i Experience Audit anger du sökvägen `/us/en/about-us.html`.

   ![Definiera en sökväg för Experience Audit](assets/experience-audit-add-page.png)

1. Tryck eller klicka på **Lägg till sida** så fylls sökvägen automatiskt i med adressen till din miljö och läggs till i sökvägstabellen.

   ![Sparar sökvägen till tabellen](assets/experience-audit-page-added.png)

1. Fortsätt att lägga till banor efter behov genom att upprepa de två föregående stegen.

   * Du kan lägga till högst 25 banor.
   * Om du inte definierar några sökvägar inkluderas webbplatsens hemsida som standard i Experience Audit.

1. Klicka på **Spara** för att spara din pipeline.

## Upplevelsegranskningsresultat {#understanding-experience-audit-results}

Experience Audit ger aggregerade och detaljerade testresultat på sidnivå via sidan [för körning av produktionspipeline](/help/implementing/cloud-manager/deploy-code.md).

* Sammanlagda mätvärden mäter medelpoängen på de sidor som granskats för prestanda, tillgänglighet, bästa praxis, SEO (sökmotoroptimering).
* Enskilda sidnivåpoäng kan också göras via fördjupning.
* Detaljerad information om poängen finns tillgänglig för att visa resultaten av de enskilda testerna tillsammans med vägledning om hur man åtgärdar eventuella problem som identifierats.
* En historik över testresultaten finns kvar i Cloud Manager för att avgöra om ändringar som införs i pipelinen innehåller regressioner från den föregående körningen.

### Sammanställd bakgrundsmusik {#aggregate-scores}

Poängen för sammanställd nivå tar medelpoängen för de sidor som ingår i körningen. Ändringen på aggregeringsnivå representerar medelpoängen för sidorna i den aktuella körningen jämfört med medelvärdet för poängen från föregående körning, även om den sidsamling som konfigurerats att inkluderas har ändrats mellan körningar.

Det finns en sammanställd nivå för varje testtyp, som prestanda, tillgänglighet, SEO och bästa praxis.

Ändringsmåttet kan ha något av följande värden.

* **Positivt värde** - Sidorna har förbättrats på det valda testet sedan den senaste körningen av produktionsflödet.

* **Negativt värde** - sidorna har gått om i det valda testet sedan den senaste körningen av produktionspipelinen.

* **Ingen ändring** - Sidorna har fått samma resultat sedan den senaste produktionspipeline-körningen.

* **N/A** - Det fanns inga tidigare poäng att jämföra.

![Upplev granskningsresultat](/help/implementing/cloud-manager/assets/exp-audit-1.png)

### Poäng på sidnivå {#page-level-scores}

Genom att gå igenom något av testerna blir det lättare att göra en mer detaljerad sidnivåbedömning. Du kan se hur de enskilda sidorna sparades för det specifika testet tillsammans med ändringen från föregående testkörning.

Om du klickar på detaljerna för en enskild sida får du information om vilka element på sidan som har utvärderats och vägledning för att åtgärda problem om möjligheter till förbättring upptäcks.

![Poäng på sidnivå](/help/implementing/cloud-manager/assets/exp-audit-2.png)

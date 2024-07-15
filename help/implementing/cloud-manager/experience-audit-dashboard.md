---
title: Kontrollpanelen för Experience Audit
description: Läs om hur Experience Audit validerar er distributionsprocess och ser till att de ändringar som driftsätts uppfyller grundläggande standarder för prestanda, tillgänglighet, bästa praxis och SEO via ett tydligt och informativt gränssnitt.
exl-id: 6d33c3c5-258c-4c9c-90c2-d566eaeb14c0
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '1958'
ht-degree: 0%

---


# Kontrollpanelen för Experience Audit {#experience-audit-dashboard}

Läs om hur Experience Audit validerar er distributionsprocess och ser till att de ändringar som driftsätts uppfyller grundläggande standarder för prestanda, tillgänglighet, bästa praxis och SEO via ett tydligt och informativt gränssnitt.

>[!NOTE]
>
>Den här funktionen är bara tillgänglig för [det tidiga adopterprogrammet.](/help/implementing/cloud-manager/release-notes/current.md#early-adoption)
>
>Mer information om den befintliga funktionen Experience Audit för AEM as a Cloud Service finns i dokumentet [Experience Audit Testing](/help/implementing/cloud-manager/experience-audit-testing.md)

## Ökning {#overview}

Experience Audit validerar distributionsprocessen och säkerställer att ändringarna som distribueras:

1. Uppfyll grundläggande standarder för prestanda, tillgänglighet, bästa praxis, SEO (Search Engine Optimization) och PWA (Progressive Web App).

1. Inför inte regressioner.

Med Experience Audit i Cloud Manager säkerställs att användarens upplevelse på webbplatsen är av högsta standard.

Granskningsresultaten är informativa och gör det möjligt för distributionshanteraren att se poängen och ändringen mellan aktuella och tidigare poäng. Den här insikten är värdefull för att avgöra om det finns en regression som introducerades i den aktuella distributionen.

Experience Audit drivs av [Google Lightroom](https://developer.chrome.com/docs/lighthouse/overview/), ett verktyg med öppen källkod från Google, och är aktiverat i alla Cloud Manager produktionspipelines.

## Tillgänglighet {#availability}

Experience Audit finns för Cloud Manager:

* Platser som producerar rörledningar, som standard
* Utveckla rörledningar i full hög, om du vill
* Utveckla rörledningar (front-end), om du vill

Mer information om hur du konfigurerar granskningen för de valfria miljöerna finns i avsnittet [Konfiguration](#configuration).

Granskningar körs som en del av pipeline. Granskningar kan också [köras på begäran](#on-demand) utanför pipelines.

## Konfiguration {#configuration}

Experience Audit är tillgängligt som standard för produktionspipelines. Den kan även aktiveras för utveckling av rörledningar i full stack och front-end. I samtliga fall måste du definiera vilka innehållssökvägar som utvärderas under pipeline-körningen.

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

## Resultat av granskning {#results}

Resultaten av Experience Audit presenteras i **fasen av testningen** i produktionsflödet via körningssidan för [produktionspipeline.](/help/implementing/cloud-manager/deploy-code.md)

![Kontrollpanel i pipeline](assets/experience-audit-dashboard.jpg)

Experience Audit tillhandahåller medianpoängen för Google Lighthuse för de [konfigurerade sidorna](#configuration) och skillnaden i poäng med den tidigare sökningen.

I den här sammanfattningsvyn i **scentestningsfasen** i pipeline finns två alternativ:

* **[Visa långsammaste sidor](#view-slowest-pages)**
* **[Visa fullständig rapport](#view-full-report)**

Förutom sammanfattningen som visas i informationen för en pipeline-körning kan du även få direkt åtkomst till det fullständiga resultatet av granskningen genom att använda fliken **Rapporter** på Cloud Manager kontrollpanel för att få tillgång till [den fullständiga rapporten](#view-full-report) direkt.

>[!TIP]
>
>I följande avsnitt beskrivs hur du visar resultaten av Experience Audit.
>
>* Om du vill ha mer information om hur granskningen fungerar läser du avsnittet [Information om Experience Audit Evaluation.](#details)
>* Om du vill veta hur du kör en upplevelsegranskning på begäran kan du läsa avsnittet [Granskningsrapporter på begäran.](#on-demand)
>* Om du får problem med granskningen kan du läsa avsnittet [Problem med Experience Audit Encounters.](#issues)
>* Allmänna tips om prestanda finns i avsnittet [Allmänna tips om prestanda.](#performance-tips)

### Visa långsammaste sidor {#view-slowest-pages}

Om du trycker eller klickar på **Visa långsammaste sidor** öppnas dialogrutan **Långsamt 5 sidor** som visar de fem sidor som har lägst prestanda och som du [har konfigurerat för granskning.](#configuration)

![Långsammast fem](assets/experience-audit-slowest-five.jpg)

Poängen delas upp efter **Prestanda**, **Tillgänglighet**, **God praxis** och **SEO** tillsammans med avvikelsen för varje mätvärde från den senaste granskningen.

Som standard öppnas dialogrutan med bakgrundsmusik för mobila enheter. Du kan ändra detta till skrivbordspoäng med hjälp av alternativet **Enheter** längst upp i dialogrutan.

Dialogrutan är avsedd för en snabb översikt. Tryck eller klicka på **Visa fullständig rapport** om du vill ha fullständig information.

### Visa fullständig rapport {#view-full-report}

Du kan visa den fullständiga Experience Audit-rapporten genom att:

* Tryck eller klicka på **Visa fullständig rapport** i dialogrutan **[Långaste 5 sidor](#view-slowest-pages)**.
* Tryck eller klicka på **Visa fullständig rapport** när du visar [körningen av en pipeline.](#results)
* Tryck eller klicka på fliken **Rapporter** i Cloud Manager.

Fliken **Rapporter** i Cloud Manager öppnas och **Experience Audit** visas.

![Upplev granskningsrapporter](assets/experience-audit-reports.png)

Rapporten är uppdelad i två områden:

* **[Sidpoäng - trend](#trend)**
* **[Upplev granskningsresultat](#results)**

#### Sidpoäng - trend {#trend}

Som standard är den valda vyn för **Sidpoäng - trend** **medianpoäng** för de **senaste sex månaderna**.

Använd listrutorna **Markera** och **Visa** längst upp och längst ned på diagramknappen för att välja sidspecifik information respektive olika tidsramar. Tryck eller klicka på knappen och knappen **Uppdatera trend** längst upp i diagrammet för att tillämpa markeringarna och uppdatera diagrammet.

När du flyttar musen över diagrammet visas ett verktygstips värdena för kategorierna Google Lightroom vid specifika tidpunkter.

![Trendinformation](assets/experience-audit-trend-details.png)

Om du trycker eller klickar på diagrammet vid en tidpunkt öppnas en pekare med detaljer om den skanningen. Tryck eller klicka på **Öppna Experience Audit Scan** för att läsa in de inläsningsresultaten till avsnittet **[Experience Audit Scan results](#scan-results)**.

![Välj en annan skanning](assets/experience-audit-open-scan.png)

#### Resultat av Experience Audit Scan {#scan-results}

Avsnittet **Resultat av granskningsgenomsökning** ger rekommendationer om hur du kan förbättra resultatet och information om alla inlästa sidor. Den är uppdelad i två delar:

* **[Recommendations](#recommendations)**
* **[Skannade sidor](#scanned-pages)**

##### Recommendations {#recommendations}

Avsnittet **Recommendations** visar en sammanställd uppsättning insikter. Rekommendationer för **prestanda** visas som standard. Använd listrutan bredvid rubriken **Recommendations** om du vill byta till en annan kategori.

![Recommendations](assets/experience-audit-recommendations.png)

Tryck eller klicka på avtryckaren om du vill visa information om den.

![Rekommendationsinformation](assets/experience-audit-recommendation-details.png)

När det är tillgängligt innehåller den utökade rekommendationsinformationen också procentandelen av rekommendationseffekten, vilket hjälper dig att fokusera på de mest effektiva ändringarna.

Tryck eller klicka på länken **visa sidor** i informationsvyn för att visa de sidor som rekommendationen gäller för.

![Sidor för rekommendationsinformationen](assets/experience-audit-details-pages.png)

##### Inlästa sidor {#scanned-pages}

Avsnittet **Skannade sidor** innehåller information om bakgrundsmusik för alla skannade sidor. Du kan använda knapparna **Föregående** och **Nästa** för att bläddra igenom resultaten och välja hur många som ska visas som sidnumrering.

![Skannade sidor](assets/experience-audit-scanned-pages.png)

Om du trycker eller klickar på länken för en viss sida uppdateras filtret **Välj** för [**Sidpoäng - trend** avsnitt](#trend) och fliken **Resultat och rekommendationer** för den valda sidan visas.

![Sidresultat](assets/experience-audit-page-results.png)

Fliken **Raw-rapporter** ger dig poäng för varje granskning av sidan. Tryck eller klicka på ikonen **Hämta** för att hämta en JSON-fil med rådata.

![Raw-rapport](assets/experience-audit-raw-reports.png)

Då öppnas en ny flik i webbläsaren som pekar på `https://googlechrome.github.io/lighthouse/viewer/` med en signerad URL-adress till JSON-rapporten (Lightroom Raw JavaScript Object Notation) för den markerade sidan, som öppnas automatiskt för detaljerad granskning

![Visa Raw-rapport](assets/experience-audit-view-raw-report.png)

## Granskningsrapporter på begäran {#on-demand}

Förutom att de körs under pipeline-körning kan Experience Audit-rapporter även genereras på begäran. Det här är en bra lösning för att snabbt skanna sidor utan att behöva köra en pipeline.

Om du vill köra en genomsökning på begäran går du till fliken **Rapporter** för att visa den fullständiga granskningsrapporten och trycker eller klickar på knappen **Kör genomsökning** .

![On demand-skanning](assets/experience-audit-on-demand.png)

On-demand-skanningar utlöser en Experience Audit för de senaste 25 [konfigurerade sidorna](#configuration) och avslutas normalt på några minuter.

När poängen är klara uppdateras poängdiagrammet automatiskt och du kan kontrollera resultaten exakt som vid en genomsökning av pipeline-körningar.

Du kan filtrera poängdiagrammet baserat på utlösartypen med hjälp av väljaren **Trigger**.

![Utlösarfilter](assets/experience-audit-on-demand-trigger.png)

>[!NOTE]
>
>En genomsökning på begäran kan bara startas om miljön inte tas bort och det inte finns några andra väntande genomsökningar i samma miljö.

## Problem med Experience Audit Encounters {#issues}

Om [sidorna som du konfigurerade](#configuration) att granskas inte var tillgängliga visas detta i Experience Audit.

Pipelinen visar ett utökningsbart felavsnitt som visar de relativa URL-sökvägar som den inte har åtkomst till.

![Problem som påträffades av Experience Audit](assets/experience-audit-issues.jpg)

Om du visar den fullständiga rapporten visas information i avsnittet **[Resultat av granskningssökning](#results)**.

![Fullständiga rapportproblem](assets/experience-audit-issues-reports.jpeg)

En del orsaker till att sidorna kanske inte är tillgängliga är:

* Konfigurationsblocken ger åtkomst.
* Sidan finns inte.
* Sidan omdirigeras som kräver annan autentisering än grundläggande.
* Ett internt fel har inträffat.
* osv.

>[!TIP]
>
>[Om du får åtkomst till rå-rapporter](#scanned-pages) för en sida kan du få information om varför det inte gick att granska sidan.

## Allmänna tips för prestanda {#performance-tips}

Två av de vanligaste effektproblemen som är enkla att åtgärda är CLS (Cumulative Layout Shifts) och LCP (Largest Contentful Paint).

Dessa kan förbättras genom att

* Det går inte att läsa in bilderna ovanför vecket (innehållet som visas i webbläsaren utan att behöva rulla nedåt).
* Att prioritera hur resurser läses in korrekt (t.ex. genom att läsa in bilderna asynkront under det veckade intervallet efter att dokumentet har lästs in).
* Förhämtning av JavaScript- och CSS-filer som används för att återge innehåll ovanför förgrunden (om de behövs).
* Reservera det lodräta utrymmet genom att tilldela en proportion till behållare som antingen läses in långsamt eller återges senare.
* Konverterar bilder till WebP-format för att minska deras storlek.
* Använder `<picture>` och bild `srcset` med olika bildstorlekar för olika visningsrutor (och ser till att storleksändringen fungerar).

## Utvärderingsinformation för Experience Audit {#details}

Följande information innehåller ytterligare information om hur Experience Audit utvärderar er webbplats. De är inte nödvändiga för allmän användning av funktionen och anges här för fullständighetens skull.

* Även om [konfigurerade sökvägar för sidan Experience Audit](#configuration) visar utgivarens `.com`-domän, söker granskningen igenom den ursprungliga domänen (`.net`) för att säkerställa att problem som uppstod under utvecklingen identifieras.
   * Domänen `.com` använder ett CDN och kan ge bättre resultat eller innehålla cachelagrade resultat.
* Mellanlagringsmiljön skannas in i rörledningar med full stapel i produktionen.
   * För att säkerställa att granskningen innehåller relevanta detaljer under granskningen bör mellanlagringsmiljöns innehåll vara så nära produktionsmiljön som möjligt.
* Sidorna som visas i listrutan **Välj** i [**Sidpoäng - trend** avsnitt](#trend) är alla kända sidor som tidigare har skannats in av Experience Audit.
* [En rekommendation](#recommendations) kan ha en potentiell ökning och en skillnad från den tidigare sökningen.
   * Experience Audit uppskattar den potentiella vinsten genom att bearbeta raw-rapporten för varje sida och korrelera de byte eller millisekunder som slöseri med en insikt som har en viktad effekt på resultatet.
   * Granskningen innehåller denna information (samt berörda sidor) för att hjälpa till att avgöra vilken rekommendation som ska följas.
   * Mer information finns i avsnittet [Allmänna prestandatester](#performance-tips)
* Med tanke på att en frontend-pipeline kan distribueras till en befintlig miljö (eller det kan finnas flera frontend-pipelines som är avsedda för samma miljö) och att skanningsresultaten sammanställs på en miljönivå, visas poängen, trenderna och rekommendationerna i samma valda miljö, oavsett vilken pipeline-körning som utlöste skanningen.

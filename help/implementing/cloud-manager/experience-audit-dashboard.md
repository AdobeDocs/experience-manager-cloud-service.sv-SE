---
title: Kontrollpanelen för Experience Audit
description: Upptäck hur Experience Audit validerar er driftsättningsprocess och ser till att ändringarna uppfyller grundläggande standarder för prestanda, tillgänglighet, bästa praxis och SEO. Den ger ett tydligt och informativt gränssnitt för att spåra mätvärdena.
exl-id: 6d33c3c5-258c-4c9c-90c2-d566eaeb14c0
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 72868ab808ebbd99c5e81805e7669083c5c754fb
workflow-type: tm+mt
source-wordcount: '1927'
ht-degree: 0%

---


# Kontrollpanel för Experience Audit {#experience-audit-dashboard}

Upptäck hur Experience Audit validerar er driftsättningsprocess och ser till att ändringarna uppfyller grundläggande standarder för prestanda, tillgänglighet, bästa praxis och SEO. Den ger ett tydligt och informativt gränssnitt för att spåra mätvärdena.

>[!NOTE]
>
>Den här funktionen är bara tillgänglig för [det tidiga adopterprogrammet](/help/implementing/cloud-manager/release-notes/current.md#early-adoption).
>
>Mer information om den befintliga funktionen Experience Audit för AEM as a Cloud Service finns i [Experience Audit Testing](/help/implementing/cloud-manager/experience-audit-testing.md).

## Ökning {#overview}

Experience Audit validerar distributionsprocessen och säkerställer att ändringarna distribueras:

1. Uppfyll grundläggande standarder för prestanda, tillgänglighet, bästa praxis, SEO (Search Engine Optimization) och PWA (Progressive Web App).

1. Inför inte regressioner.

Med Experience Audit i Cloud Manager säkerställs att användarens upplevelse på webbplatsen är av högsta standard.

Granskningsresultaten är informativa och gör det möjligt för distributionshanteraren att se poängen och ändringen mellan aktuella och tidigare poäng. Den här insikten är värdefull för att avgöra om det finns en regression som introducerades i den aktuella distributionen.

Experience Audit drivs av [Google Lightroom](https://developer.chrome.com/docs/lighthouse/overview/), ett verktyg med öppen källkod från Google, och är aktiverat i alla Cloud Manager produktionspipelines.

## Tillgänglighet {#availability}

Experience Audit finns för Cloud Manager:

* (Standard) Anläggningspipelines för produktion
* (Valfritt) Utveckling av rörledningar i full stapel
* (Valfritt) Utveckling av rörledningar

Mer information om hur du konfigurerar granskningen för de valfria miljöerna finns i avsnittet [Konfiguration](#configuration).

Granskningar körs som en del av pipeline. Granskningar kan också [köras på begäran](#on-demand) utanför pipelines.

## Konfiguration {#configuration}

Experience Audit är tillgängligt som standard för produktionspipelines. Den kan även aktiveras för utveckling av rörledningar i full hög och frontendspikar. I samtliga fall måste du definiera vilka innehållssökvägar som utvärderas under pipeline-körningen.

1. Beroende på vilken typ av pipeline du vill konfigurera kan du följa anvisningarna för att:

   * Lägg till en ny [produktionspipeline](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) för att definiera sökvägarna som du vill att granskningen ska utvärdera.
   * Lägg till en ny [icke-produktionspipeline](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md) om du vill aktivera granskningen för en frontendpipeline eller en fullständig utvecklingspipeline.
   * Du kan också [redigera en befintlig pipeline](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md) och uppdatera befintliga alternativ.

1. Om du vill använda Experience Audit när du lägger till eller redigerar en icke-produktionspipeline markerar du kryssrutan **Experience Audit** . Det här alternativet finns på fliken **Source-kod**.

   ![Aktiverar Experience Audit](assets/experience-audit-enable.jpg)

   * Krävs endast för rörledningar som inte är avsedda för produktion.
   * Fliken **Experience Audit** visas när kryssrutan är markerad.

1. För pipelines för både produktion och icke-produktion definierar du sökvägarna som ska inkluderas i Experience Audit på fliken **Experience Audit** .

   * Sidsökvägarna måste börja med `/` och är relativa till din plats.
   * Om din webbplats till exempel är `wknd.site` och vill inkludera `https://wknd.site/us/en/about-us.html` i Experience Audit anger du sökvägen `/us/en/about-us.html`.

   ![Definiera en sökväg för Experience Audit](assets/experience-audit-add-page.png)

1. Klicka på **Lägg till sida** så fylls sökvägen automatiskt i med adressen till din miljö och läggs till i sökvägstabellen.

   ![Sparar sökvägen till tabellen](assets/experience-audit-page-added.png)

1. Fortsätt att lägga till banor efter behov genom att upprepa de två föregående stegen.

   * Du kan lägga till högst 25 banor.
   * Om du inte definierar några sökvägar inkluderas webbplatsens hemsida som standard i Experience Audit.

1. Klicka på **Spara**.

## Resultat av granskning {#results}

Resultaten av Experience Audit presenteras i **fasen av testningen** i produktionsflödet via [sidan för körning av produktionspipeline](/help/implementing/cloud-manager/deploy-code.md).

![Kontrollpanel i pipeline](assets/experience-audit-dashboard.jpg)

Experience Audit tillhandahåller medianpoängen för Google Lighthuse för de [konfigurerade sidorna](#configuration) och skillnaden i poäng med den tidigare sökningen.

I den här sammanfattningsvyn i **scentestningsfasen** i pipeline finns två alternativ:

* **[Visa de långsammaste sidorna](#view-slowest-pages)**
* **[Visa den fullständiga rapporten](#view-full-report)**

Du får tillgång till det fullständiga granskningsresultatet genom att klicka på fliken **Rapporter** på Cloud Manager kontrollpanel. Förutom sammanfattningen som visas i pipeline-körningsinformationen kan du visa [den fullständiga rapporten](#view-full-report) direkt.

>[!TIP]
>
>I följande avsnitt beskrivs hur du visar resultaten av Experience Audit.
>
>* Mer information om hur granskningen fungerar finns i [Information om Experience Audit Evaluation](#details).
>* Mer information om hur du kör en Experience Audit on demand finns i [On-Demand Audit Reports](#on-demand).
>* Om du får problem med granskningen kan du läsa [Experience Audit Encounters Issues](#issues) (Problem med granskningsupptäckter).
>* Allmänna tips om prestanda finns i [Allmänna tips för prestanda](#performance-tips).

### Visa de långsammaste sidorna {#view-slowest-pages}

Klicka på **Visa långsammaste sidor** för att öppna dialogrutan **Långsammaste 5 sidor**. De fem sidor med lägst prestanda som du [har konfigurerat för granskning](#configuration) visas.

![Långsammast fem](assets/experience-audit-slowest-five.png)

Cloud Manager delar upp poängen med **Prestanda**, **Tillgänglighet**, **God praxis** och **SEO**, vilket visar avvikelsen för varje mätresultat från den tidigare granskningen.

Som standard öppnas dialogrutan med bakgrundsmusik för mobila enheter. Du kan se bakgrundsmusik med hjälp av växlingsknappen **Enheter** i dialogrutans övre del.

Dialogrutan ger dig en snabb översikt. Klicka på **Visa fullständig rapport** om du vill ha fullständig information.

### Visa hela rapporten {#view-full-report}

Du kan visa den fullständiga Experience Audit-rapporten genom att göra följande:

* Klicka på **`View full report`** i dialogrutan **[Långaste 5 sidor](#view-slowest-pages)**.
* Klicka på **`View full report`** när du visar [körningen av en pipeline](#results).
* Klicka på fliken **Rapporter** i Cloud Manager.

Fliken **Rapporter** i Cloud Manager öppnas och **Experience Audit** visas.

![Experience Audit-rapporter](assets/experience-audit-reports.png)

Rapporten är uppdelad i två områden:

* **[Sidpoäng - trend](#trend)**
* **[Upplev granskningsresultat](#results)**

#### Sidpoäng - trend {#trend}

Som standard är den valda vyn för **Sidpoäng — trend** **medianpoäng** för de **senaste sex månaderna**.

Använd listrutorna **Markera** och **Visa** längst upp och längst ned på diagramknappen för att välja sidspecifik information respektive olika tidsramar. Klicka på **uppdatera trenden** längst upp i diagrammet för att tillämpa markeringarna och uppdatera diagrammet.

När du flyttar musen över diagrammet visas ett verktygstips värdena för kategorierna Google Lightroom vid specifika tidpunkter.

![Trendinformation](assets/experience-audit-trend-details.png)

Om du klickar på diagrammet vid en tidpunkt öppnas en port med detaljer om den skanningen. Klicka på **Öppna Experience Audit-genomsökningen** för att läsa in dessa genomsökningsresultat i avsnittet **[Experience Audit-resultat](#scan-results)**.

![Välj en annan skanning](assets/experience-audit-open-scan.png)

#### Resultat av granskning av Experience Audit {#scan-results}

Avsnittet **Experience Audit results** ger rekommendationer om hur du kan förbättra poängen och detaljerna för alla inlästa sidor. Den är uppdelad i två delar:

* **[Recommendations](#recommendations)**
* **[Skannade sidor](#scanned-pages)**

##### Recommendations {#recommendations}

Avsnittet **Recommendations** visar en sammanställd uppsättning insikter. Rekommendationer för **prestanda** visas som standard. Använd listrutan bredvid rubriken **Recommendations** om du vill byta till en annan kategori.

![Recommendations](assets/experience-audit-recommendations.png)

Klicka på avfasningen om du vill visa information om den.

![Rekommendationsinformation](assets/experience-audit-recommendations-details.png)

När det är tillgängligt innehåller den utökade rekommendationsinformationen också procentandelen av rekommendationseffekten, vilket hjälper dig att fokusera på de mest effektiva ändringarna.

Klicka på länken **visa sidor** i informationsvyn för att visa de sidor som rekommendationen gäller för.

![Sidor för rekommendationsinformationen](assets/experience-audit-details-pages.png)

##### Inlästa sidor {#scanned-pages}

Avsnittet **Skannade sidor** innehåller information om bakgrundsmusik för alla skannade sidor. Använd knapparna **Föregående** och **Nästa** för att bläddra igenom resultaten och välj hur många som ska visas som sidnumrering.

![Skannade sidor](assets/experience-audit-scanned-pages.png)

Klicka på länken för en viss sida för att uppdatera filtret **Välj** för [**Sidresultat - trend** avsnitt](#trend) och visa fliken **Resultat och rekommendationer** för den valda sidan.

![Sidresultat](assets/experience-audit-page-results.png)

Fliken **Raw-rapporter** ger dig poäng för varje granskning av sidan. Klicka på rapportdatumet i kolumnen **Lightroom Report** för att hämta en JSON-fil med rådata.

![Raw-rapport](assets/experience-audit-raw-reports.png)

En ny flik öppnas i webbläsaren som dirigerar dig till `https://googlechrome.github.io/lighthouse/viewer/`. Den läser automatiskt in en signerad URL-adress som innehåller JSON-rapporten för Lightroom Raw för den valda sidan, vilket möjliggör detaljerad granskning.

![Visa Raw-rapport](assets/experience-audit-view-raw-report.png)

## Granskningsrapporter för behovsstyrd skanning {#on-demand}

Experience Audit-rapporter kan även genereras på begäran, utöver att de körs under pipeline-körning. Det här alternativet är en bra lösning för att skanna sidor snabbt utan att behöva köra en pipeline.

Om du vill köra en genomsökning på begäran går du till fliken **Rapporter** för att visa den fullständiga granskningsrapporten och klickar sedan på knappen **Kör genomsökning** .

![On demand-skanning](assets/experience-audit-on-demand.png)

Knappen **Kör skanning** blir inte tillgänglig och har en klockikon när en skanning på begäran redan körs.

![On demand-skanning körs](assets/experience-audit-on-demand-running.png)

On-demand-skanningar utlöser en Experience Audit för de senaste 25 [konfigurerade sidorna](#configuration) och avslutas normalt på några minuter.

När resultatet är klart uppdateras poängdiagrammet automatiskt och du kan kontrollera resultatet exakt som vid en genomsökning av pipeline-körningar.

Du kan filtrera poängdiagrammet baserat på utlösartypen med hjälp av väljaren **Trigger**.

![Utlösarfilter](assets/experience-audit-on-demand-trigger.png)

>[!NOTE]
>
>En genomsökning på begäran kan bara startas om miljön inte tas bort och det inte finns några andra väntande genomsökningar i samma miljö.

## Problem med Experience Audit Encounters {#issues}

Om [sidorna som du konfigurerade](#configuration) att granskas inte var tillgängliga eller om det fanns andra fel i granskningen, speglar Experience Audit detta faktum.

Pipelinen visar ett utökningsbart felavsnitt som visar de relativa URL-sökvägar som den inte har åtkomst till.

![Problem som påträffades av Experience Audit](assets/experience-audit-issues.jpg)

Om du visar den fullständiga rapporten visas information i avsnittet **[Experience Audit results](#results)** som också kan utökas.

![Fullständiga rapportproblem](assets/experience-audit-issues-report.png)

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

Du kan förbättra dessa områden genom att göra följande:

* Inte lat läsa in bilderna ovanför förvrängningen - det innehåll som syns i webbläsaren utan att behöva rulla nedåt.
* Prioritera hur resurserna läses in korrekt (t.ex. genom att läsa in bilderna asynkront under det veckade intervallet efter att dokumentet har lästs in).
* Förhämtning av JavaScript- och CSS-filer som används för att återge innehåll ovanför förgrunden (om de behövs).
* Reservera det lodräta utrymmet genom att tilldela en proportion till behållare som antingen läses in långsamt eller återges senare.
* Konverterar bilder till WebP-format för att minska deras storlek.
* Använder `<picture>` och bild `srcset` med olika bildstorlekar för olika visningsrutor (och ser till att storleksändringen fungerar).

## Utvärderingsinformation för Experience Audit {#details}

Följande information innehåller ytterligare information om hur Experience Audit utvärderar er webbplats. De är inte nödvändiga för allmän användning av funktionen och anges här för fullständighetens skull.

* Granskningen skannar ursprungsdomänen (`.com`) från de [konfigurerade sökvägarna på sidan Experience Audit](#configuration) för utgivaren för att simulera verkliga användarupplevelser, vilket hjälper dig att fatta bättre beslut om att hantera och optimera dina webbplatser.
* Mellanlagringsmiljön skannas in i rörledningar med full stapel i produktionen. För att säkerställa att granskningen innehåller relevanta detaljer under granskningen bör mellanlagringsmiljöns innehåll vara så nära produktionsmiljön som möjligt.
* Sidorna som visas i listrutan **Välj** i [**Sidpoäng - trend** avsnitt](#trend) är alla kända sidor som Experience Audit har skannat in tidigare.
* [En rekommendation](#recommendations) kan ha en potentiell ökning och en skillnad från den tidigare sökningen.
* Experience Audit uppskattar möjliga förbättringar genom att bearbeta raw-rapporten för varje sida. Den korrelerar slösade byte eller millisekunder med insikter, vilket ger en viktad effekt på prestandan. Granskningen innehåller denna information och de berörda sidorna som kan hjälpa till att avgöra vilken rekommendation som ska följas.
Mer information finns i avsnittet [Allmänna prestandatester](#performance-tips).
* En frontendpipeline kan distribueras till en befintlig miljö, och flera frontendpipelines kan ha samma miljö som mål. Eftersom inläsningsresultaten samlas på miljönivå är poängen, trenderna och rekommendationerna konsekventa. Dessa resultat visas i den valda miljön, oavsett vilken pipeline som utlöste sökningen.

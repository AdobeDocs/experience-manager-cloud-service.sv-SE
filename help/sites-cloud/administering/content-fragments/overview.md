---
title: Översikt över begrepp och bästa metoder för att arbeta med innehållsfragment
description: Lär dig hur du kan skapa och använda strukturerat innehåll med hjälp av innehållsfragment i Adobe Experience Manager (AEM) as a Cloud Service, vilket är idealiskt för rubrikfri leverans och sidredigering.
feature: Content Fragments
role: User, Developer
exl-id: ce9cb811-57d2-4a57-a360-f56e07df1b1a
solution: Experience Manager Sites
source-git-commit: 2449bc380268ed42b6c8d23ae4a4fecaf1736889
workflow-type: tm+mt
source-wordcount: '2357'
ht-degree: 1%

---

# Arbeta med innehållsfragment - begrepp och bästa praxis {#working-with-content-fragments-concepts-and-best-practices}

Med Adobe Experience Manager (AEM) as a Cloud Service kan du med Content Fragments utforma, skapa, strukturera och publicera sidoberoende innehåll. De gör att du kan förbereda innehåll som är klart för användning på flera platser och i flera kanaler, vilket är idealiskt för [headless delivery](/help/headless/what-is-headless.md) och [page authoring](/help/sites-cloud/authoring/fragments/content-fragments.md).

>[!IMPORTANT]
>
>Många funktioner som beskrivs i det här avsnittet är *endast* tillgängliga i [Unified Shell](/help/overview/aem-cloud-service-on-unified-shell.md); så *online* Adobe Experience Manager (AEM) as a Cloud Service, inte en lokal instans.

>[!IMPORTANT]
>
>Du kan komma åt innehållsfragment från två konsoler: **Innehållsfragment** och **Assets**.
>
>Det finns också två redigerare för att skapa innehållsfragment. Även om de grundläggande funktionerna är desamma finns det vissa skillnader. Båda redigerarna är tillgängliga från båda konsolerna.
>
>I det här avsnittet behandlas konsolen **Innehållsfragment** och den *nya* innehållsfragmentsredigeraren. Dessa har utvecklats för leverans av headless-innehåll (även om de kan användas för alla scenarier)
>
>Mer information finns i:
>
>* användning av **Assets**-konsolen för [hantering av innehållsfragment](/help/assets/content-fragments/content-fragments-managing.md)
>* användning av den [*ursprungliga* innehållsfragmentsredigeraren](/help/assets/content-fragments/content-fragments-variations.md),
>* använder [Innehållsfragment för sidredigering](/help/sites-cloud/authoring/fragments/content-fragments.md).


Innehållsfragment innehåller strukturerat innehåll:

* Varje fragment baseras på en [innehållsfragmentmodell](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md).
   * [Content Fragment Model definierar strukturen ](/help/sites-cloud/administering/content-fragments/content-fragment-models.md) för det resulterande fragmentet.
* Varje fragment består av:
   * **[Main](#main-and-variations)** - en integrerad del av fragmentet som innehåller kärninnehållet. Finns alltid, kan inte tas bort
   * **[Variationer](#main-and-variations)** - en eller flera permutationer av innehållet som skapats av författaren
* Strukturen kan variera mellan:
   * Grundläggande
      * Ett enda textfält med flera rader, till exempel.
      * Kan användas för att förbereda okomplicerat innehåll för sidredigering.
      * Kan även användas för leverans utan huvud till programmet.
   * Komplex
      * En kombination av många fält med olika datatyper, bland annat text, tal, booleskt värde samt datum och tid.
      * Kan användas antingen för att förbereda mer strukturerat innehåll för sidredigering eller för att skicka till programmet utan extra kostnad.
   * Kapslad
      * De tillgängliga referensdatatyperna gör att du kan kapsla ditt innehåll.
      * Tender som ska användas för headless-leverans till programmet.

Innehållsfragment kan också levereras i JSON-format med exportfunktionerna för Sling Model (JSON) i AEM kärnkomponenter. Leveranssätt:

* gör att du kan använda komponenten för att hantera vilka element i ett fragment som ska levereras
* tillåter massleverans, genom att lägga till flera [kärnkomponenter för innehållsfragment](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html) på sidan som används för API-leverans

Antalet kommunikationskanaler ökar årligen. Kanalerna avser vanligen leveransmekanismen, antingen som:

* Fysisk kanal, till exempel dator, mobil.
* Leveranssätt i en fysisk kanal, t.ex.&quot;produktinformationssida&quot;,&quot;produktkategorisida&quot; för dator eller&quot;mobilwebb&quot;,&quot;mobilapp&quot; för mobil.

Du (förmodligen) vill inte använda *exakt* samma innehåll för alla kanaler. Du måste optimera innehållet utifrån den specifika kanalen.

Med innehållsfragment kan du:

* Fundera på hur ni kan nå målgrupper effektivt i alla kanaler.
* Skapa och hantera kanalneutralt redaktionellt innehåll.
* Bygg innehållspooler för en rad olika kanaler.
* Utforma innehållsvarianter för specifika kanaler.
* Lägg till bilder i texten genom att infoga resurser.
* Skapa kapslat innehåll som återspeglar komplexiteten i era data.

Dessa innehållsfragment kan sedan monteras för att ge upplevelser över flera olika kanaler.

>[!NOTE]
>
>**Innehållsfragment** och **[Upplevelsefragment](/help/sites-cloud/authoring/fragments/content-fragments.md)** är olika funktioner i AEM:
>
>* **Innehållsfragment** är redaktionellt innehåll, med definition och struktur, men utan ytterligare visuell design och/eller layout. De kan användas för att komma åt strukturerade data, bland annat texter, siffror och datum.
>* **Upplevelsefragment** är helt utformat för innehåll, ett fragment av en webbsida.
>
>Upplevelsefragment kan innehålla innehåll i form av innehållsfragment, men inte tvärtom.
>
>Mer information finns i [Om innehållsfragment och upplevelsefragment i AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/content-fragments/understand-content-fragments-and-experience-fragments.html#content-fragments).

På den här och följande sidor beskrivs hur du skapar, konfigurerar, underhåller och använder innehållsfragment:

* [Aktivera funktionen för innehållsfragment för din instans](/help/sites-cloud/administering/content-fragments/setup.md)
* [Modeller för innehållsfragment](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md) - aktivera, skapa och [definiera](/help/sites-cloud/administering/content-fragments/content-fragment-models.md) dina modeller
* [Skapa dina innehållsfragment](/help/sites-cloud/administering/content-fragments/managing.md#creating-a-content-fragment) (med konsolen för innehållsfragment)

När fragmenten har skapats kan du:

* [Använd konsolen för innehållsfragment](/help/sites-cloud/administering/content-fragments/managing.md) - för att:
   * få tillgång till, publicera (för att förhandsgranska eller producera) och referera till dina fragment
* [Använd redigeraren för innehållsfragment](/help/sites-cloud/administering/content-fragments/authoring.md) - för att:
   * redigera, publicera (för att förhandsgranska eller producera) och referera till dina fragment
   * samarbeta med andra författare med hjälp av kommentarer
* [Analysera](/help/sites-cloud/administering/content-fragments/analysis.md) innehållsfragmentets struktur med hjälp av redigeraren
* [Få tillgång till dina fragment med GraphQL för headless-leverans till dina program](/help/sites-cloud/administering/content-fragments/content-delivery-with-graphql.md).
* [Integrera och använda dina innehållsfragment i Adobe Journey Optimizer](/help/sites-cloud/administering/content-fragments/content-fragments-with-journey-optimizer.md)
* Skapa, och hantera, [Startar innehållsfragment](/help/sites-cloud/administering/content-fragments/launches-for-content-fragments.md)
* [Eller använd fragmenten för att skapa sidor](/help/sites-cloud/authoring/fragments/content-fragments.md)

>[!NOTE]
>
>Dessa sidor kan läsas tillsammans med:
>
>* [Anpassa och utöka Content Fragments](/help/implementing/developing/extending/content-fragments-customizing.md)
>* [Content Fragments – konfigurera komponenter för återgivning](/help/implementing/developing/extending/content-fragments-configuring-components-rendering.md)
>* [Stöd för Content Fragments i AEM Assets HTTP API](/help/assets/content-fragments/assets-api-content-fragments.md)
>* [AEM GraphQL API för användning med innehållsfragment](/help/headless/graphql-api/content-fragments.md)
>* [Sidredigering med innehållsfragment](/help/sites-cloud/authoring/fragments/content-fragments.md).
>* OpenAPI:erna [Content Fragment och Content Fragment Model](/help/headless/content-fragment-openapis.md) är också tillgängliga.


## Huvud och variationer {#main-and-variations}

Variationer är en viktig egenskap i AEM innehållsfragment. Med dem kan du skapa och redigera kopior av **Main** -innehållet som ska användas i vissa kanaler och scenarier, vilket gör innehållsleverans utan rubrik och sidredigering ännu mer flexibelt.

* **Huvudsida**

   * **Main** är inte en sådan variation, utan är grunden för alla variationer.
   * En integrerad del av fragmentet

      * Varje innehållsfragment har en instans av **Main**.
      * Det går inte att ta bort **Main**.

   * **Huvudsida** är tillgänglig i fragmentredigeraren under **[Variationer](/help/sites-cloud/administering/content-fragments/authoring.md#variations)**.

  >[!NOTE]
  >
  >I redigeraren som är tillgänglig från **Assets**-konsolen heter **Main** **Master**.

* **Variationer**

   * Återgivning av fragmenttext som är specifik för redaktionella ändamål. Den kan vara relaterad till kanalen men är inte obligatorisk, men kan även användas för lokala ad hoc-ändringar.
   * Skapas som kopior av **Main**, men kan sedan redigeras efter behov. Innehållet överlappar ofta mellan själva variationerna.
   * Kan definieras under fragmentredigering från den vänstra panelen.
   * Lagras i fragmentet för att undvika spridning av innehållskopior.
   * Variationer kan [jämföras och synkroniseras](/help/sites-cloud/administering/content-fragments/authoring.md#compare-and-synchronize-rich-text) med **Main**.
  <!--
  * Can be [Summarized](/help/sites-cloud/administering/content-fragments/authoring.md#summarizing-text) to quickly truncate the text to a predefined length.
  -->

## Innehållsfragment och innehållstjänster {#content-fragments-and-content-services}

AEM Content Services är utformat för att generalisera beskrivningen och leveransen av innehåll i/från AEM utöver fokus på webbsidor.

De levererar innehåll till kanaler som inte är traditionella AEM webbsidor, med standardiserade metoder som kan användas av alla kunder. Dessa kanaler kan omfatta:

* Enkelsidiga program
* Inbyggda mobilprogram
* andra kanaler och kontaktpunkter utanför AEM

Leveransen görs i JSON-format med JSON-exporteraren.

AEM Content Fragments kan användas för att beskriva och hantera strukturerat innehåll. Strukturerat innehåll definieras i modeller som kan innehålla olika innehållstyper, bland annat text, numeriska data, booleska värden, datum och tid.

Tillsammans med JSON-exportfunktionerna i AEM kärnkomponenter kan detta strukturerade innehåll sedan användas för att leverera AEM-innehåll till andra kanaler än AEM-sidor.

>[!NOTE]
>
>Se [Headless och AEM](/help/headless/introduction.md) för en introduktion till Headless Development för AEM Sites as a Cloud Service.

>[!NOTE]
>
>AEM har också stöd för översättning av fragmentinnehåll. Mer information finns i [Översätta Assets](/help/assets/translate-assets.md).

## Innehållstyp {#content-type}

Innehållsfragmenten är:

* En **webbplatsfunktion**.

* Lagrat som **Assets**:

   * Innehållsfragment (och deras varianter) kan skapas och underhållas från konsolen [Innehållsfragment](#content-fragments-console).
   * Skapat och redigerat i [redigeraren för innehållsfragment](/help/sites-cloud/administering/content-fragments/authoring.md).

* Tillgängligt för innehållsleverans med [AEM GraphQL API](/help/headless/graphql-api/content-fragments.md).

* Tillgängligt i sidredigeraren [genom att använda komponenten Content Fragment](/help/sites-cloud/authoring/fragments/content-fragments.md) (refereringskomponent):

   * [Kärnkomponenten för innehållsfragment](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html) är tillgänglig för sidförfattare. De kan referera till, och leverera, önskat innehållsfragment i antingen HTML- eller JSON-format.

Innehållsfragment är en innehållsstruktur som:

* Är utan layout eller design (textformatering är möjlig för textfält).
* Är oberoende av leveransmekanismen (till exempel sidan eller kanalen).
* Innehåller en eller flera [beståndsdelar](#constituent-parts-of-a-content-fragment).
* Kan [innehålla eller vara ansluten till bilder](#fragments-with-visual-assets).

### Fragment med Visual Assets {#fragments-with-visual-assets}

För att ge författarna bättre kontroll över sitt innehåll kan bilder läggas till och/eller integreras med ett innehållsfragment.

Assets kan användas med ett innehållsfragment på flera sätt, vart och ett med sina egna fördelar:

* som en **innehållsreferens**
* i ett **textfält med flera rader**

### Komponentdelar i ett innehållsfragment {#constituent-parts-of-a-content-fragment}

Resurserna för innehållsfragment består av följande delar (antingen direkt eller indirekt):

* **Fragmentelement**

   * Elementen korrelerar till de datafält som innehåller innehåll.
   * Du använder en [innehållsfragmentmodell](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md) för att skapa innehållsfragmentet. Elementen (fälten) [ som anges i modellen definierar fragmentets struktur ](/help/sites-cloud/administering/content-fragments/content-fragment-models.md). Dessa element (fält) kan vara av olika datatyper.

* **Fragmentera stycken**

   * Textblock, ofta flerradiga, som avgränsas som enskilda enheter.

   * Aktivera innehållskontroll vid sidredigering.

* **Fragmentmetadata**

   * Använd [Assets-metadatamatcheman](/help/assets/metadata-schemas.md).
   * Taggar kan skapas när du:

      * Skapa och redigera fragmentet
      * Eller senare, när du [visar eller redigerar egenskaperna](/help/sites-cloud/administering/content-fragments/authoring.md#view-properties-tags) i fragmentredigeraren

  >[!CAUTION]
  >
  >Metadatabearbetningsprofiler gäller inte för innehållsfragment.

  >[!CAUTION]
  >
  >En innehållsfragmentmodell kan ofta definiera datafält med namnen **Title** och **Description**. Om de här två fälten finns är de användardefinierade och kan uppdateras i redigerarens innehållsområde.
  >
  >Innehållsfragmentet och dess varianter har också metadatafält (egenskap) som kallas **Titel** och **Beskrivning**. Dessa två metadatafält är en integrerad del av alla innehållsfragment, och variationer, och definieras ursprungligen när fragmentet skapas. De kan uppdateras under Egenskaper/metadata i redigeraren.

* **[Huvudsida](#main-and-variations)**
* **[Variationer](#main-and-variations)**

### Krävs av fragment {#required-by-fragments}

Om du vill skapa innehållsfragment behöver du:

* **Innehållsmodell**

   * Är [aktiverade med hjälp av Konfigurationsläsaren](/help/sites-cloud/administering/content-fragments/setup.md).
   * Skapas [med konsolen för innehållsfragment](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md#creating-a-content-fragment-model).
   * Krävs för att [skapa ett fragment](/help/sites-cloud/administering/content-fragments/managing.md#creating-content-fragments).
   * Definierar strukturen för ett fragment (rubrik, innehållselement, taggdefinitioner).
   * Definitioner av innehållsfragmentmodellen kräver en titel och ett dataelement. Allt annat är valfritt.
   * Modellen kan definiera standardinnehåll, om tillämpligt.
   * Författare kan inte ändra den definierade strukturen när de redigerar fragmentinnehåll, men de kan öppna modellredigeraren från fragmentredigeraren.
   * Ändringar som görs i en modell efter att beroende innehållsfragment har skapats kan påverka dessa innehållsfragment.

Om du vill använda dina innehållsfragment för leverans av headless-innehåll behöver du också:

* en [GraphQL-fråga](/help/headless/graphql-api/content-fragments.md) för att begära nödvändigt innehåll
* Innehållet kan sedan användas för att utveckla egna SPA för AEM. Mer information finns i följande dokument:

   * [SPA WKND - självstudiekurs](/help/implementing/developing/hybrid/wknd-tutorial.md)
   * [Komma igång med React](/help/implementing/developing/hybrid/getting-started-react.md)
   * [Komma igång med Angular](/help/implementing/developing/hybrid/getting-started-angular.md)

Om du vill använda dina innehållsfragment för att skapa sidor behöver du också:

* En **komponent för innehållsfragment**

   * Instrumentellt för att leverera fragmentet i HTML- och/eller JSON-format.
   * Krävs för att [referera till fragmentet på en sida](/help/sites-cloud/authoring/fragments/content-fragments.md).
   * Ansvarig för layout och leverans av ett fragment, t.ex. kanaler.
   * Fragment behöver en eller flera dedikerade komponenter för att definiera layout och leverera vissa eller alla element/varianter och tillhörande innehåll.
   * Om du drar ett fragment till en sida när du redigerar kopplas den nödvändiga komponenten automatiskt till.
   * Se [kärnkomponenten för innehållsfragment](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html).

## Konsolen Innehållsfragment {#content-fragments-console}

Konsolen för innehållsfragment är dedikerad för att hantera, söka efter och skapa [innehållsfragment](/help/sites-cloud/administering/content-fragments/managing.md), [modeller för innehållsfragment](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md) och [Assets](/help/sites-cloud/administering/content-fragments/assets-content-fragments-console.md). Den har optimerats för användning i ett Headless-sammanhang, men används även när du skapar innehållsfragment och modeller för innehållsfragment för användning vid sidredigering.

Konsolen kan nås direkt från den översta nivån i Global Navigation.

![Global navigering - konsolen för innehållsfragment](assets/cf-managing-global-navigation.png)

Du kan använda panelen längst till vänster för att välja resurstyp för att visa, bläddra och hantera:

![Konsolen för innehållsfragment - navigering](/help/sites-cloud/administering/content-fragments/assets/cf-console-assets-navigation.png)

Mer information finns i:

* [Innehållsfragment](/help/sites-cloud/administering/content-fragments/managing.md)
* [Modeller för innehållsfragment](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md)
* [Assets](/help/sites-cloud/administering/content-fragments/assets-content-fragments-console.md)

* Det finns ett urval av [kortkommandon](/help/sites-cloud/administering/content-fragments/keyboard-shortcuts.md) som kan användas i den här konsolen

>[!CAUTION]
>
>Konsolen är *endast* tillgänglig i Adobe Experience Manager (AEM) as a Cloud Service online.

>[!NOTE]
>
>Ditt projektteam kan anpassa konsolen och redigeraren om det behövs. Mer information finns i [Anpassa konsolen och redigeraren för innehållsfragment](/help/implementing/developing/extending/content-fragments-console-and-editor.md).

## Exempel på användning {#example-usage}

Ett fragment, med dess element och variationer, kan användas för att skapa sammanhängande innehåll för flera kanaler. När du utformar ditt fragment måste du tänka på vad som kommer att användas och var.

### WKND-exempel {#wknd-sample}

Proverna [WKND Site och WKND Shared](/help/implementing/developing/introduction/develop-wknd-tutorial.md) finns tillgängliga som hjälp att lära dig mer om AEM as a Cloud Service.

<!-- CHECK: which links can/should be used these days? -->

WKND-projektet innehåller:

* Content Fragment Models available under:

   * `.../libs/dam/cfm/models/console/content/models.html/conf/wknd`

   * `.../ui#/aem/libs/dam/cfm/models/console/content/models.html/conf/wknd-shared`

* Innehållsfragment (och annat innehåll) tillgängliga under:

   * `.../assets.html/content/dam/wknd/en`

## Bästa praxis {#best-practices}

Innehållsfragment kan användas för att skapa komplexa strukturer. Adobe ger rekommendationer för bästa praxis när det gäller att definiera och använda både modeller och fragment.

### Behåll det enkelt {#keep-it-simple}

När du utformar strukturerat innehåll i AEM ska du hålla innehållsstrukturerna så enkla som möjligt för att säkerställa starka systemprestanda och effektiv styrning.

### Antal modeller {#number-of-models}

Skapa så många innehållsmodeller som behövs, men inte mer.

För många modeller komplicerar styrningen och kan göra GraphQL-frågor långsammare. En liten uppsättning modeller, som är högst tio, är vanligtvis tillräckliga. Om du närmar dig de tiotals eller fler höga nivåerna bör du tänka om din modelleringsstrategi.

### Kapslingsmodeller och fragment (mycket viktigt) {#nesting-models-and-fragments}

Undvik djup eller överdriven kapsling av innehållsfragment med Content Fragment Reference, som gör att fragment kan referera till andra fragment, ibland på flera nivåer.

Omfattande användning av Content Fragment-referenser kan i hög grad påverka systemets prestanda, användargränssnittets svarstider och körningen av GraphQL-frågor. Målet är att inte kapsla mer än tio nivåer.

### Antal datafält och datatyper per per modell  {#number-of-data-fields-and-types-per-model}

Inkludera endast de datafält och datatyper som modellen verkligen behöver.

Överdrivet komplexa modeller leder till alltför komplexa fragment som kan göra redigeringen svår och minska redigeringsprestanda.

### RTF-fält {#rich-text-fields}

Använd RTF-fält (datatypen **Flera rader**) med hänsyn till detta.

Begränsa antalet RTF-fält per modell. Även mängden text som lagras i varje fragment och mängden HTML-formatering. Mycket stort RTF-innehåll kan påverka systemets prestanda negativt.

### Antal variationer {#number-of-variations}

Skapa så många fragmentvariationer som behövs, men inte mer.

Variationer lägger till bearbetningstid i ett innehållsfragment, i författarmiljön och även vid leverans. Vi rekommenderar att du håller antalet variationer till ett hanterbart minimum.

Ett tips är att inte överskrida tio varianter per innehållsfragment.

### Testa före produktion {#test-before-production}

När du är osäker kan du skapa prototyper för de avsedda innehållsstrukturerna innan du distribuerar dem till produktionen. Tidiga korrekturrundor och lämplig testning, både för tekniska frågor och för användaren, kan hjälpa dig att undvika problem senare när du måste klara deadlines i produktionen.
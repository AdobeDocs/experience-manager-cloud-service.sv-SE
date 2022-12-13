---
title: Arbeta med innehållsfragment
description: Lär dig hur innehållsfragment i Adobe Experience Manager (AEM) as a Cloud Service gör att du kan designa, skapa, strukturera och använda sidoberoende innehåll, idealiskt för sidredigering och rubrikfri leverans.
feature: Content Fragments
role: User
exl-id: d12b1dda-85ce-4665-b8b1-915b74231bb8
source-git-commit: 6204830f30c28daba3ff87ba60acd0150847b523
workflow-type: tm+mt
source-wordcount: '2070'
ht-degree: 3%

---

# Arbeta med innehållsfragment {#working-with-content-fragments}

Med Adobe Experience Manager (AEM) as a Cloud Service kan du skapa, strukturera och [publicera sidoberoende innehåll](/help/sites-cloud/authoring/fundamentals/content-fragments.md) Med dem kan du förbereda innehåll som är klart för användning på flera platser/i flera kanaler, idealiskt för sidredigering och headless-leverans.

Innehållsfragment innehåller strukturerat innehåll:

* De bygger på en [Content Fragment Model](/help/sites-cloud/administering/content-fragments/content-fragments-models.md), som fördefinierar en struktur för det resulterande fragmentet.
* Strukturen kan variera mellan:
   * Grundläggande
      * Ett textfält med flera rader, till exempel.
      * Kan användas för att förbereda okomplicerat innehåll för sidredigering.
   * Komplex
      * En kombination av många fält med olika datatyper, bland annat text, tal, boolesk information och tid.
      * Kan användas antingen för att förbereda mer strukturerat innehåll för redigering av sidor eller för leverans till programmet.
   * Kapslad
      * De tillgängliga referensdatatyperna gör att du kan kapsla ditt innehåll.
      * Tender som ska användas för leverans till ditt program.

Innehållsfragment kan också levereras i JSON-format med exportfunktionerna i Sling Model (JSON) AEM kärnkomponenterna. Leveranssätt:

* gör att du kan använda komponenten för att hantera vilka element i ett fragment som ska levereras
* tillåter massleverans genom att lägga till flera kärnkomponenter för innehållsfragment på sidan som används för API-leverans

På den här och följande sidor beskrivs hur du skapar, konfigurerar, underhåller och använder dina innehållsfragment:

* [Aktivera funktionen för innehållsfragment för din instans](/help/sites-cloud/administering/content-fragments/content-fragments-configuration-browser.md)
* [Modeller för innehållsfragment](/help/sites-cloud/administering/content-fragments/content-fragments-models.md) - aktivera, skapa och definiera dina modeller
* [Använda konsolen Innehållsfragment](/help/sites-cloud/administering/content-fragments/content-fragments-console.md) - för att få tillgång till, skapa, redigera, publicera och referera till dina fragment
* [Hantera innehållsfragment](/help/sites-cloud/administering/content-fragments/content-fragments-managing.md) - skapa era innehållsfragment; redigera, publicera och referera
* [Variationer - innehåll för redigeringsfragment](/help/sites-cloud/administering/content-fragments/content-fragments-variations.md) - skapa fragmentinnehållet och skapa varianter av det Överordnad
* [Markering](/help/sites-cloud/administering/content-fragments/content-fragments-markdown.md) - med markeringssyntax för ditt fragment
* [Använda associerat innehåll](/help/sites-cloud/administering/content-fragments/content-fragments-assoc-content.md) - lägga till associerat innehåll
* [Metadata - Fragmentegenskaper](/help/sites-cloud/administering/content-fragments/content-fragments-metadata.md) - visa och redigera fragmentegenskaperna
* Använd dina innehållsfragment:

   * [för att skapa sidor](/help/sites-cloud/authoring/fundamentals/content-fragments.md)
   * [tillsammans med GraphQL, för headless-leverans till programmen](/help/sites-cloud/administering/content-fragments/content-fragments-graphql.md).
Om du vill ha hjälp med det här kan du förhandsvisa [Strukturträd](/help/sites-cloud/administering/content-fragments/content-fragments-structure-tree.md) och [JSON-utdata](/help/sites-cloud/administering/content-fragments/content-fragments-json-preview.md).

>[!NOTE]
>
>Dessa sidor kan läsas tillsammans med:
>
>* [Sidredigering med innehållsfragment](/help/sites-cloud/authoring/fundamentals/content-fragments.md).
>* [Anpassa och utöka Content Fragments](/help/implementing/developing/extending/content-fragments-customizing.md)
>* [Content Fragments – konfigurera komponenter för återgivning](/help/implementing/developing/extending/content-fragments-configuring-components-rendering.md)
>* [Stöd för Content Fragments i AEM Assets HTTP API](/help/assets/content-fragments/assets-api-content-fragments.md)
>* [AEM GraphQL API för användning med innehållsfragment](/help/headless/graphql-api/content-fragments.md)


Antalet kommunikationskanaler ökar årligen. Kanalerna avser vanligen leveransmekanismen, antingen som

* Fysisk kanal. till exempel dator, mobil.
* Leveranssätt i fysisk kanal. till exempel&quot;produktinformationssida&quot;,&quot;produktkategorisida&quot; för datorer eller&quot;mobilwebben&quot;,&quot;mobilapp&quot; för mobiler.

Men du vill (förmodligen) inte använda exakt samma innehåll för alla kanaler - du måste optimera innehållet utifrån den specifika kanalen.

Med innehållsfragment kan du:

* Fundera på hur ni kan nå målgrupper effektivt i alla kanaler.
* Skapa och hantera kanalneutralt redaktionellt innehåll.
* Bygg innehållspooler för en rad olika kanaler.
* Utforma innehållsvarianter för specifika kanaler.
* Lägg till bilder i texten genom att infoga resurser (blandade mediefragment).
* Skapa kapslat innehåll som återspeglar komplexiteten i era data.

Dessa innehållsfragment kan sedan samlas ihop för att ge upplevelser över en mängd olika kanaler.

>[!NOTE]
>
>**Innehållsfragment** och **[Upplevelsefragment](/help/sites-cloud/authoring/fundamentals/experience-fragments.md)** har olika funktioner i AEM:
>* **Innehållsfragment** är redaktionellt innehåll som kan användas för att få tillgång till strukturerade data, bland annat texter, siffror och datum. De är rent innehåll, med definition och struktur, men utan ytterligare visuell design och/eller layout.
>* **Upplevelsefragment** är helt utformat, ett fragment av en webbsida.
>
>Upplevelsefragment kan innehålla innehåll i form av innehållsfragment, men inte tvärtom.
>
>Mer information finns även i [Förstå innehållsfragment och upplevelsefragment i AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/content-fragments/understand-content-fragments-and-experience-fragments.html#content-fragments).

## Innehållsfragment och innehållstjänster {#content-fragments-and-content-services}

AEM Content Services är utformat för att generera beskrivning och leverans av innehåll i/från AEM utöver fokus på webbsidor.

De levererar innehåll till kanaler som inte är traditionella AEM webbsidor, med standardiserade metoder som kan användas av alla kunder. Dessa kanaler kan omfatta:

* Enkelsidiga program
* Inbyggda mobilprogram
* andra kanaler och kontaktpunkter externt för AEM

Leveransen görs i JSON-format med JSON-exporteraren.

AEM kan användas för att beskriva och hantera strukturerat innehåll. Strukturerat innehåll definieras i modeller som kan innehålla olika innehållstyper. inklusive text, numeriska data, boolesk information, datum och tid med mera.

Tillsammans med JSON-exportfunktionerna i AEM kärnkomponenter kan detta strukturerade innehåll sedan användas för att leverera AEM till andra kanaler än AEM.

>[!NOTE]
>
>Se [Headless och AEM](/help/headless/introduction.md) för en introduktion till Headless Development för AEM Sites as a Cloud Service.

>[!NOTE]
>
>AEM har också stöd för översättning av fragmentinnehåll.

>[!NOTE]
>
>AEM har också stöd för översättning av fragmentinnehåll. Se [Översätta resurser](/help/assets/translate-assets.md) för ytterligare information.

## Innehållstyp {#content-type}

Innehållsfragmenten är:

* A **Webbplatser** -funktion.

* Lagrad som **Resurser**:

   * Innehållsfragment (och deras variationer) kan skapas och underhållas från båda **Innehållsfragment** konsolen och **Resurser** konsol.
   * Skapat och redigerat i Content Fragment Editor.

* Används i [sidredigeraren med komponenten Content Fragment](/help/sites-cloud/authoring/fundamentals/content-fragments.md) (refererande komponent):

   * The **Innehållsfragment** -komponenten är tillgänglig för sidförfattare. De kan referera till och leverera det nödvändiga innehållsfragmentet i antingen HTML- eller JSON-format.

* Tillgängligt med [AEM GraphQL API](/help/headless/graphql-api/content-fragments.md).

Innehållsfragment är en innehållsstruktur som:

* Är utan layout eller design (viss textformatering är möjlig i RTF-läge).
* Innehåller en eller flera [beståndsdelar](#constituent-parts-of-a-content-fragment).
* Kan [innehålla eller vara ansluten till bilder](#fragments-with-visual-assets).
* Kan använda [mellanliggande innehåll](#in-between-content-when-page-authoring-with-content-fragments) vid referens på en sida.

* Är oberoende av leveransmekanismen (dvs. sida, kanal).

### Fragment med visuella resurser {#fragments-with-visual-assets}

För att ge författarna bättre kontroll över sitt innehåll kan bilder läggas till och/eller integreras med ett innehållsfragment.

Resurser kan användas med ett innehållsfragment på flera sätt. var och en med sina egna fördelar:

* **Infoga resurs** till ett fragment (blandade mediefragment)

   * Är en integrerad del av fragmentet (se [Komponentdelar i ett innehållsfragment](#constituent-parts-of-a-content-fragment)).
   * Definiera tillgångens position.
   * Se [Infoga resurser i fragment](/help/sites-cloud/administering/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment) i fragmentredigeraren om du vill ha mer information.

   >[!NOTE]
   >
   >Visuella resurser som infogats i själva innehållsfragmentet kopplas till föregående stycke. När fragmentet läggs till på en sida flyttas dessa resurser i relation till det stycket när mellanliggande innehåll läggs till.

* **Associerat innehåll**

   * är anslutna till ett fragment, men inte en fast del av fragmentet (se [Komponentdelar i ett innehållsfragment](#constituent-parts-of-a-content-fragment)).
   * Möjliggör viss flexibilitet för placering.
   * Är enkelt tillgängliga för användning (som mellanliggande innehåll) när du använder fragmentet på en sida.
   * Se [Associerat innehåll](/help/sites-cloud/administering/content-fragments/content-fragments-assoc-content.md) för mer information.

* Resurser som är tillgängliga från **resursläsaren** i sidredigeraren

   * Möjliggör full flexibilitet för val av en resurs.
   * Möjliggör viss flexibilitet för placering.
   * Innebär inte att man kan godkänna ett visst fragment.
   * Se [Resursläsaren](/help/sites-cloud/authoring/fundamentals/environment-tools.md#assets-browser) för mer information.

### Komponentdelar i ett innehållsfragment {#constituent-parts-of-a-content-fragment}

Resurserna för innehållsfragmentet består av följande delar (antingen direkt eller indirekt):

* **Fragmentelement**

   * Elementen korrelerar till de datafält som innehåller innehåll.
   * Du använder en innehållsmodell för att skapa innehållsfragmentet. De element (fält) som anges i modellen definierar fragmentets struktur. Dessa element (fält) kan vara av olika datatyper.

* **Fragmentera stycken**

   * Textblock, ofta flerradiga, som avgränsas som enskilda enheter.

   * I lägena [RTF](/help/sites-cloud/administering/content-fragments/content-fragments-variations.md#rich-text) och [Markdown-kod](/help/sites-cloud/administering/content-fragments/content-fragments-variations.md#markdown) kan ett stycke formateras som en rubrik, och då utgör det och det efterföljande stycket en enhet.

   * Aktivera innehållskontroll vid sidredigering.

* **Resurser som infogats i ett fragment (blandade mediefragment)**

   * Resurser (bilder) infogade i det faktiska fragmentet och används som det interna innehållet i ett fragment.
   * Är inbäddade i fragmentets styckesystem.
   * Kan formateras när [fragment används/refereras på en sida](/help/sites-cloud/authoring/fundamentals/content-fragments.md).
   * Kan endast läggas till, tas bort från eller flyttas inom ett fragment med fragmentredigeraren. Dessa åtgärder kan inte utföras i sidredigeraren.
   * Kan endast läggas till, tas bort från eller flyttas inom ett fragment med [RTF-format i fragmentredigeraren](/help/sites-cloud/administering/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment).
   * Kan endast läggas till i flerradiga textelement (alla fragmenttyper).
   * Kopplas till föregående text (stycke).

      >[!CAUTION]
      >
      >Resurser kan tas bort (oavsiktligt) från ett fragment genom att växla till oformaterad text.

      >[!NOTE]
      >
      >Resurser kan också läggas till som [extra (mellanliggande) innehåll](/help/sites-cloud/authoring/fundamentals/content-fragments.md#using-associated-content) när ett fragment används på en sida, med antingen Associerat innehåll eller resurser från Resurser-webbläsaren.

* **Associerat innehåll**

   * Detta innehåll är externt, men med redaktionell relevans för, ett fragment. Vanligtvis bilder, videoklipp eller andra fragment.
   * De enskilda resurserna i samlingen är tillgängliga för användning med fragmentet i sidredigeraren när det läggs till på en sida. Det innebär att de är valfria, beroende på den specifika kanalens krav.
   * Resurserna är [kopplade till fragment via samlingar](/help/sites-cloud/administering/content-fragments/content-fragments-assoc-content.md); kopplade samlingar låter författaren bestämma vilka resurser som ska användas när de redigerar sidan.

      * Samlingar kan kopplas till fragment som standardinnehåll, eller av författare vid fragmentredigering.
      * [DAM-samlingar](/help/assets/manage-collections.md) är grunden för det associerade fragmentinnehållet.
   * Du kan också lägga till själva fragmentet i en samling för att underlätta spårningen.

* **Fragmentmetadata**

   * Använd [Resurser för metadatamodeller](/help/assets/metadata-schemas.md).
   * Taggar kan skapas när du:

      * Skapa och redigera fragmentet
      * Eller senare:

         * Genom att visa/redigera fragmentet **Egenskaper** från konsolen
         * Genom att redigera **Metadata** i fragmentredigeraren

   >[!CAUTION]
   >
   >Metadatabearbetningsprofiler gäller inte för innehållsfragment.

* **Överordnad**

   * En integrerad del av fragmentet

      * Alla innehållsfragment har en instans av Överordnad.
      * Överordnad kan inte tas bort.
   * Överordnad är tillgängligt i fragmentredigeraren under **[Variationer](/help/sites-cloud/administering/content-fragments/content-fragments-variations.md)**.
   * Överordnad är inte en variation i sig, utan är grunden för alla variationer.


* **Variationer**

   * Återgivning av fragmenttext som är specifik för redaktionella ändamål. kan vara relaterat till kanalen men inte obligatoriskt, kan också vara för lokala ad hoc-ändringar.
   * Skapas som kopior av **Överordnad**, men kan sedan redigeras efter behov; det ofta finns innehållsöverlappning mellan själva variationerna.
   * Kan definieras vid fragmentredigering.
   * Lagras i fragmentet för att undvika spridning av innehållskopior.
   * Variationer kan vara [synkroniserad](/help/sites-cloud/administering/content-fragments/content-fragments-variations.md#synchronizing-with-master) med Överordnad om det Överordnad innehållet har uppdaterats.
   * Kan [Sammanfattad](/help/sites-cloud/administering/content-fragments/content-fragments-variations.md#summarizing-text) för att snabbt korta av texten till en fördefinierad längd.
   * Tillgängligt under [Variationer](/help/sites-cloud/administering/content-fragments/content-fragments-variations.md) i fragmentredigeraren.

### Mellan innehåll vid sidredigering med innehållsfragment {#in-between-content-when-page-authoring-with-content-fragments}

Mellanliggande innehåll:

* Kan användas i sidredigeraren när du arbetar med innehållsfragment.
* Är [ytterligare innehåll som lagts till i flödet för ett fragment](/help/sites-cloud/authoring/fundamentals/content-fragments.md#adding-in-between-content) när det har använts eller refererats på en sida.
* Finns att använda i [Sidredigeraren när du arbetar med innehållsfragment](/help/sites-cloud/authoring/fundamentals/content-fragments.md).
* Mellanliggande innehåll kan läggas till i vilket fragment som helst, där bara ett element är synligt.
* Associerat innehåll kan användas, liksom resurser och/eller komponenter från lämplig webbläsare.

>[!CAUTION]
>
>Det mellanliggande innehållet är sidinnehåll. Den lagras inte i innehållsfragmentet.

### Krävs av fragment {#required-by-fragments}

Om du vill skapa innehållsfragment behöver du:

* **Innehållsmodell**

   * är [aktiveras med hjälp av Konfigurationsläsaren](/help/sites-cloud/administering/content-fragments/content-fragments-configuration-browser.md).
   * är [skapad med verktyg](/help/sites-cloud/administering/content-fragments/content-fragments-models.md).
   * Krävs för [skapa ett fragment](/help/sites-cloud/administering/content-fragments/content-fragments-managing.md#creating-content-fragments).
   * Definierar strukturen för ett fragment (rubrik, innehållselement, taggdefinitioner).
   * Innehållsmodelldefinitioner kräver en titel och ett dataelement. allt annat är valfritt.
   * Modellen kan definiera standardinnehåll, om tillämpligt.
   * Författare kan inte ändra den definierade strukturen när de redigerar fragmentinnehåll.
   * Ändringar som görs i en modell efter att beroende innehållsfragment har skapats kan påverka dessa innehållsfragment.

Om du vill använda dina innehållsfragment för att skapa sidor behöver du också:

* **Innehållsfragmentkomponent**

   * Instrumentellt för att leverera fragmentet i HTML- och/eller JSON-format.
   * Krävs för [referera till fragmentet på en sida](/help/sites-cloud/authoring/fundamentals/content-fragments.md).
   * Ansvarig för layout och leverans av ett fragment. dvs. kanaler.
   * Fragment behöver en eller flera dedikerade komponenter för att definiera layout och leverera vissa eller alla element/varianter och tillhörande innehåll.
   * Om du drar ett fragment till en sida när du redigerar kopplas den nödvändiga komponenten automatiskt till.

## Exempel på användning {#example-usage}

Ett fragment, med dess element och variationer, kan användas för att skapa sammanhängande innehåll för flera kanaler. När du utformar ditt fragment måste du tänka på vad som kommer att användas var.

### WKND-exempel {#wknd-sample}

The [WKND-plats](/help/implementing/developing/introduction/develop-wknd-tutorial.md) finns exempel som hjälper dig att lära dig mer om AEM as a Cloud Service.

WKND-projektet innehåller:

* Content Fragment Models available under:
   `http://<hostname>:<port>/libs/dam/cfm/models/console/content/models.html/conf/wknd`

* Innehållsfragment (och annat innehåll) tillgängliga under:
   `http://<hostname>:<port>/assets.html/content/dam/wknd/en`

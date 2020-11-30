---
title: Arbeta med innehållsfragment
description: Lär dig hur innehållsfragment i Adobe Experience Manager (AEM) som en Cloud Service gör att du kan utforma, skapa, strukturera och använda sidoberoende innehåll.
translation-type: tm+mt
source-git-commit: 85f47a417e73432d776c0ed4f5cdb7673ce41a70
workflow-type: tm+mt
source-wordcount: '1818'
ht-degree: 2%

---


# Arbeta med innehållsfragment{#working-with-content-fragments}

Med Adobe Experience Manager (AEM) som Cloud Service kan du utforma, skapa, strukturera och [publicera sidoberoende innehåll](/help/sites-cloud/authoring/fundamentals/content-fragments.md). Med dem kan du förbereda innehåll som är klart för användning på flera platser/i flera kanaler.

Innehållsfragment innehåller strukturerat innehåll:

* De baseras på en [innehållsfragmentmodell](/help/assets/content-fragments/content-fragments-models.md), som fördefinierar en struktur för det resulterande fragmentet.

Innehållsfragment kan också levereras i JSON-format med exportfunktionerna i Sling Model (JSON) AEM kärnkomponenterna. Leveranssätt:

* gör att du kan använda komponenten för att hantera vilka element i ett fragment som ska levereras
* tillåter massleverans genom att lägga till flera kärnkomponenter för innehållsfragment på sidan som används för API-leverans

På den här och följande sidor beskrivs hur du skapar, konfigurerar och underhåller dina innehållsfragment:

* [Hantera innehållsfragment](/help/assets/content-fragments/content-fragments-managing.md) - skapa dina innehållsfragment; redigera, publicera och referera
* [Content Fragment Models](/help/assets/content-fragments/content-fragments-models.md) - aktivera, skapa och definiera dina modeller
* [Variationer - Innehåll](/help/assets/content-fragments/content-fragments-variations.md) för redigeringsfragment - skapa fragmentinnehållet och skapa varianter av det Överordnad
* [Markering](/help/assets/content-fragments/content-fragments-markdown.md) - med markeringssyntax för ditt fragment
* [Använda associerat innehåll](/help/assets/content-fragments/content-fragments-assoc-content.md) - lägga till associerat innehåll
* [Metadata - Fragmentegenskaper](/help/assets/content-fragments/content-fragments-metadata.md) - visa och redigera fragmentegenskaperna

>[!NOTE]
>
>Dessa sidor ska läsas tillsammans med [Sidredigering och Innehållsfragment](/help/sites-cloud/authoring/fundamentals/content-fragments.md).

Antalet kommunikationskanaler ökar årligen. Kanalerna avser vanligen leveransmekanismen, antingen som

* Fysisk kanal. t.ex. dator, mobil.
* Leveranssätt i fysisk kanal. t.ex.&quot;produktinformationssida&quot;,&quot;produktkategorisida&quot; för datorer eller&quot;mobilwebben&quot;,&quot;mobilapp&quot; för mobiler.

Men du vill (förmodligen) inte använda exakt samma innehåll för alla kanaler - du måste optimera innehållet utifrån den specifika kanalen.

Med innehållsfragment kan du:

* Fundera på hur ni kan nå målgrupper effektivt i alla kanaler.
* Skapa och hantera kanalneutralt redaktionellt innehåll.
* Bygg innehållspooler för en rad olika kanaler.
* Utforma innehållsvarianter för specifika kanaler.
* Lägg till bilder i texten genom att infoga resurser (blandade mediefragment).

Dessa innehållsfragment kan sedan samlas ihop för att ge upplevelser över en mängd olika kanaler.

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
>**Content Fragments** and **[Experience Fragments](/help/sites-cloud/authoring/fundamentals/experience-fragments.md)** are different features within AEM:
>* **Innehållsfragment** är redaktionellt innehåll som kan användas för att komma åt strukturerade data, bland annat texter, siffror och datum. De är rent innehåll, med definition och struktur, men utan ytterligare visuell design och/eller layout.
>* **Experience Fragments** är helt utformat för innehåll, ett fragment av en webbsida.

>
>
Upplevelsefragment kan innehålla innehåll i form av innehållsfragment, men inte tvärtom.
>
>Mer information finns också i [Förstå innehållsfragment och Upplevelsefragment i AEM](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/content-fragments-experience-fragments-article-understand.html).

>[!NOTE]
>
>AEM har också stöd för översättning av fragmentinnehåll.

<!--
>[!NOTE]
>
>AEM also supports the translation of fragment content. See [Creating Translation Projects for Content Fragments](/help/assets/creating-translation-projects-for-content-fragments.md) for further information.
-->

## Innehållstyp {#content-type}

Innehållsfragmenten är:

* Lagrat som **resurser**:

   * Innehållsfragment (och deras varianter) kan skapas och underhållas från **Assets** Console.
   * Skapat och redigerat i Content Fragment Editor.

* Används i [sidredigeraren med komponenten](/help/sites-cloud/authoring/fundamentals/content-fragments.md) Content Fragment (refereringskomponent):

   * Komponenten **Innehållsfragment** är tillgänglig för sidförfattare. Det gör att de kan referera till och leverera det nödvändiga innehållsfragmentet i antingen HTML- eller JSON-format.

Innehållsfragment är en innehållsstruktur som:

* Är utan layout eller design (viss textformatering är möjlig i RTF-läge).
* Innehåller en eller flera [beståndsdelar](#constituent-parts-of-a-content-fragment).
* Kan [innehålla eller vara ansluten till bilder](#fragments-with-visual-assets).
* Kan använda [mellanliggande innehåll](#in-between-content-when-page-authoring-with-content-fragments) när det refereras till på en sida.

* Är oberoende av leveransmekanismen (dvs. sida, kanal).

### Fragment med visuella resurser {#fragments-with-visual-assets}

För att ge författarna bättre kontroll över sitt innehåll kan bilder läggas till och/eller integreras med ett innehållsfragment.

Resurser kan användas med ett innehållsfragment på flera sätt. var och en med sina egna fördelar:

* **Infoga resurs** i ett fragment (blandade mediefragment)

   * Är en integrerad del av fragmentet (se [Ingående delar i ett innehållsfragment](#constituent-parts-of-a-content-fragment)).
   * Definiera tillgångens position.
   * Mer information finns i [Infoga resurser i fragmentredigeraren](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment) .

   >[!NOTE]
   >
   >Visuella resurser som infogats i själva innehållsfragmentet kopplas till föregående stycke. När fragmentet läggs till på en sida flyttas dessa resurser i relation till det stycket när mellanliggande innehåll läggs till.

* **Associerat innehåll**

   * är anslutna till ett fragment, men inte en fast del av fragmentet (se [beståndsdelar i ett innehållsfragment](#constituent-parts-of-a-content-fragment)).
   * Möjliggör viss flexibilitet för placering.
   * Är enkelt tillgängliga för användning (som mellanliggande innehåll) när du använder fragmentet på en sida.
   * Mer information finns i [Associerat innehåll](/help/assets/content-fragments/content-fragments-assoc-content.md) .

* Resurser som är tillgängliga från **resursläsaren** i sidredigeraren

   * Möjliggör full flexibilitet för val av en resurs.
   * Möjliggör viss flexibilitet för placering.
   * Innebär inte att man kan godkänna ett visst fragment.
   * Mer information finns i [Resursläsaren](/help/sites-cloud/authoring/fundamentals/environment-tools.md#assets-browser) .

### Komponentdelar i ett innehållsfragment {#constituent-parts-of-a-content-fragment}

Resurserna för innehållsfragmentet består av följande delar (antingen direkt eller indirekt):

* **Fragmentelement**

   * Elementen korrelerar till de datafält som innehåller innehåll.
   * Du använder en innehållsmodell för att skapa innehållsfragmentet. De element (fält) som anges i modellen definierar fragmentets struktur. Dessa element (fält) kan vara av olika datatyper.

* **Fragmentera stycken**

   * Textblock, ofta flerradiga, som avgränsas som enskilda enheter.

   * I lägena [RTF](/help/assets/content-fragments/content-fragments-variations.md#rich-text) och [Markdown-kod](/help/assets/content-fragments/content-fragments-variations.md#markdown) kan ett stycke formateras som en rubrik, och då utgör det och det efterföljande stycket en enhet.

   * Aktivera innehållskontroll vid sidredigering.

* **Resurser som infogats i ett fragment (blandade mediefragment)**

   * Resurser (bilder) infogade i det faktiska fragmentet och används som det interna innehållet i ett fragment.
   * Är inbäddade i fragmentets styckesystem.
   * Kan formateras när [fragmentet används/refereras på en sida](/help/sites-cloud/authoring/fundamentals/content-fragments.md).
   * Kan endast läggas till, tas bort från eller flyttas inom ett fragment med fragmentredigeraren. Dessa åtgärder kan inte utföras i sidredigeraren.
   * Kan endast läggas till, tas bort från eller flyttas inom ett fragment med [RTF-format i fragmentredigeraren](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment).
   * Kan endast läggas till i flerradiga textelement (alla fragmenttyper).
   * Kopplas till föregående text (stycke).

   >[!CAUTION]
   >
   >Kan tas bort (oavsiktligt) från ett fragment genom att växla till oformaterad text.

   >[!NOTE]
   >
   >Resurser kan också läggas till som [extra (mellanliggande) innehåll](/help/sites-cloud/authoring/fundamentals/content-fragments.md#using-associated-content) när ett fragment används på en sida. med antingen Associerat innehåll eller resurser från Resurser-webbläsaren.

* **Associerat innehåll**

   * Detta innehåll är externt, men med redaktionell relevans för, ett fragment. Vanligtvis bilder, videoklipp eller andra fragment.
   * De enskilda resurserna i samlingen är tillgängliga för användning med fragmentet i sidredigeraren när det läggs till på en sida. Det innebär att de är valfria, beroende på den specifika kanalens krav.
   * Resurserna är [kopplade till fragment via samlingar](/help/assets/content-fragments/content-fragments-assoc-content.md). kopplade samlingar låter författaren bestämma vilka resurser som ska användas när de redigerar sidan.

      * Samlingar kan kopplas till fragment som standardinnehåll, eller av författare vid fragmentredigering.
      * [DAM-samlingar](/help/assets/manage-collections.md) är grunden för det associerade fragmentinnehållet.
   * Du kan också lägga till själva fragmentet i en samling för att underlätta spårningen.

* **Fragmentmetadata**

   * Använd metadatamatchningar för [resurser](/help/assets/metadata-schemas.md).
   * Taggar kan skapas när du:

      * Skapa och redigera fragmentet
      * Eller senare:

         * Genom att visa/redigera **fragmentegenskaperna** från konsolen
         * Genom att redigera **metadata** i fragmentredigeraren

   >[!CAUTION]
   >
   >Metadatabearbetningsprofiler gäller inte för innehållsfragment.

* **Överordnad**

   * En integrerad del av fragmentet

      * Alla innehållsfragment har en instans av Överordnad.
      * Överordnad kan inte tas bort.
   * Överordnad är tillgängligt i fragmentredigeraren under **[Variationer](/help/assets/content-fragments/content-fragments-variations.md)**.
   * Överordnad är inte en variation i sig, utan är grunden för alla variationer.


* **Variationer**

   * Återgivning av fragmenttext som är specifik för redaktionella ändamål. kan vara relaterat till kanalen men inte obligatoriskt, kan också vara för lokala ad hoc-ändringar.
   * skapas som kopior av **Överordnad**, men kan sedan redigeras efter behov, det ofta finns innehållsöverlappning mellan själva variationerna.
   * Kan definieras vid fragmentredigering.
   * Lagras i fragmentet för att undvika spridning av innehållskopior.
   * Variationer kan [synkroniseras](/help/assets/content-fragments/content-fragments-variations.md#synchronizing-with-master) med Överordnad om det Överordnad innehållet har uppdaterats.
   * Kan [sammanfattas](/help/assets/content-fragments/content-fragments-variations.md#summarizing-text) för att snabbt korta av texten till en fördefinierad längd.
   * Tillgängligt på fliken [Variationer](/help/assets/content-fragments/content-fragments-variations.md) i fragmentredigeraren.

### Mellan innehåll vid sidredigering med innehållsfragment {#in-between-content-when-page-authoring-with-content-fragments}

Mellanliggande innehåll:

* Kan användas i sidredigeraren när du arbetar med innehållsfragment.
* Läggs [ytterligare innehåll till i flödet för ett fragment](/help/sites-cloud/authoring/fundamentals/content-fragments.md#adding-in-between-content) när det har använts/refererats på en sida.
* Kan användas i [sidredigeraren när du arbetar med innehållsfragment](/help/sites-cloud/authoring/fundamentals/content-fragments.md).
* Mellanliggande innehåll kan läggas till i vilket fragment som helst, där bara ett element är synligt.
* Associerat innehåll kan användas, liksom resurser och/eller komponenter från lämplig webbläsare.

>[!CAUTION]
>
>Det mellanliggande innehållet är sidinnehåll. Den lagras inte i innehållsfragmentet.

### Krävs av fragment {#required-by-fragments}

Om du vill skapa, redigera och använda innehållsfragment behöver du också:

* **Innehållsmodell**

   * Är [aktiverade och skapas sedan med verktyg](/help/assets/content-fragments/content-fragments-models.md).
   * Krävs för att [skapa ett fragment](/help/assets/content-fragments/content-fragments-managing.md#creating-content-fragments).
   * Definierar strukturen för ett fragment (rubrik, innehållselement, taggdefinitioner).
   * Innehållsmodelldefinitioner kräver en titel och ett dataelement. allt annat är valfritt.
   * Modellen kan definiera standardinnehåll, om tillämpligt.
   * Författare kan inte ändra den definierade strukturen när de redigerar fragmentinnehåll.
   * Ändringar som görs i en modell efter att beroende innehållsfragment har skapats kan påverka dessa innehållsfragment.

* **Innehållsfragmentkomponent**

   * Instrumentellt för att leverera fragmentet i HTML- och/eller JSON-format.
   * Krävs för att [referera till fragmentet på en sida](/help/sites-cloud/authoring/fundamentals/content-fragments.md).
   * Ansvarig för layout och leverans av ett fragment. dvs. kanaler.
   * Fragment behöver en eller flera dedikerade komponenter för att definiera layout och leverera vissa eller alla element/varianter och tillhörande innehåll.
   * Om du drar ett fragment till en sida när du redigerar kopplas den nödvändiga komponenten automatiskt till.

## Exempel på användning {#example-usage}

Ett fragment, med dess element och variationer, kan användas för att skapa sammanhängande innehåll för flera kanaler. När du utformar ditt fragment måste du tänka på vad som kommer att användas var.

### WKND-exempel {#wknd-sample}

WKND- [webbplatsexemplen](/help/implementing/developing/introduction/develop-wknd-tutorial.md) är till för att du ska kunna lära dig mer om AEM som Cloud Service. Den innehåller exempelfragment som kan ses vid:

`hhttp://<host>:<port>/assets.html/content/dam/wknd/en/adventures`

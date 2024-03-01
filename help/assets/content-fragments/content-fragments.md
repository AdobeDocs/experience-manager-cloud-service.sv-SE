---
title: Arbeta med innehållsfragment (resurser - innehållsfragment)
description: Lär dig hur du med Content Fragments in Adobe Experience Manager (AEM) as a Cloud Service kan utforma, skapa, strukturera och använda sidoberoende innehåll, idealiskt för sidredigering och rubrikfri leverans. Hur de kan användas tillsammans med MSM.
exl-id: db17eff1-4252-48d5-bb67-5e476e93ef7e
source-git-commit: a213d94b6c5bd4eaaf78b8384b96e1d99104874d
workflow-type: tm+mt
source-wordcount: '2228'
ht-degree: 2%

---

# Arbeta med innehållsfragment {#working-with-content-fragments}

Med Adobe Experience Manager (AEM) as a Cloud Service kan du designa, skapa, välja och [publicera sidoberoende innehåll](/help/sites-cloud/authoring/fragments/content-fragments.md). Med dem kan du förbereda innehåll som är klart att användas på flera platser/över flera kanaler, vilket är perfekt för fjärradministrerad leverans. De kan också användas tillsammans med [Hantering av flera webbplatser för att du ska kunna återanvända ditt innehåll](#reusing-content-fragments-with-msm-assets).

Innehållsfragment innehåller strukturerat innehåll:

* De bygger på en [Content Fragment Model](/help/assets/content-fragments/content-fragments-models.md), som fördefinierar en struktur för det resulterande fragmentet.
* Strukturen kan variera mellan:
   * Grundläggande
      * Ett enda textfält med flera rader.
      * Den kan användas för att förbereda okomplicerat innehåll för sidredigering.
   * Komplex
      * En kombination av många fält med olika datatyper, bland annat text, tal, boolesk information och tid.
      * Den kan användas antingen för att förbereda mer strukturerat innehåll för redigering av sidor eller för leverans till programmet.
   * Kapslad
      * De tillgängliga referensdatatyperna gör att du kan kapsla ditt innehåll.
      * Tender som ska användas för leverans till ditt program.

Innehållsfragment kan också levereras i JSON-format med exportfunktionerna i Sling Model (JSON) AEM kärnkomponenterna. Leveranssätt:

* gör att du kan använda komponenten för att hantera vilka element i ett fragment som ska levereras
* tillåter massleverans genom att lägga till flera kärnkomponenter för innehållsfragment på sidan som används för API-leverans

>[!NOTE]
>
>Innehållsfragment är en webbplatsfunktion, men lagras som **Resurser**.
>
>De hanteras nu främst med **[Innehållsfragment](/help/sites-cloud/administering/content-fragments/managing.md#content-fragments-console)** konsolen, men de kan fortfarande hanteras från **Resurser** konsol. Detta avsnitt behandlar ledning från **Resurser** konsol.
>
>Det finns två redigeringsprogram för att skapa Content Fragments. I det här avsnittet beskrivs den ursprungliga redigeraren, som du i första hand kommer åt från **Resurser** konsol. Se webbplatsernas dokumentation, [Content Fragments - Authoring](/help/sites-cloud/administering/content-fragments/authoring.md), för information om den nya redaktören (främst tillgänglig via **Content Fragments** konsol). Båda redigerarna har en växlingsknapp i det övre verktygsfältet för att ge snabb åtkomst till den andra redigeraren.

På den här och följande sidor beskrivs hur du skapar, konfigurerar, underhåller och använder innehållsfragment:

* [Aktivera funktionen för innehållsfragment för din instans](/help/assets/content-fragments/content-fragments-configuration-browser.md)
* [Modeller för innehållsfragment](/help/assets/content-fragments/content-fragments-models.md) - aktivera, skapa och definiera dina modeller
* [Hantera innehållsfragment](/help/assets/content-fragments/content-fragments-managing.md) - skapa dina innehållsfragment och sedan redigera, publicera och referera
* [Variationer - innehåll för redigeringsfragment](/help/assets/content-fragments/content-fragments-variations.md) - skapa fragmentinnehållet och skapa varianter av mallsidan
* [Markdown](/help/assets/content-fragments/content-fragments-markdown.md) - använda markdown-syntax för ditt avsnitt
* [Använda associerat innehåll](/help/assets/content-fragments/content-fragments-assoc-content.md) - lägga till tillhörande innehåll
* [Metadata - Fragmentegenskaper](/help/assets/content-fragments/content-fragments-metadata.md) - visa och redigera fragmentegenskaperna
* Användning [Content Fragments, och GraphQL, så att du kan leverera innehåll](/help/assets/content-fragments/content-fragments-graphql.md) för användning i dina program. Du kan förhandsgranska om du vill ha hjälp [JSON-utdata](/help/assets/content-fragments/content-fragments-json-preview.md).
* [Återanvänd Content Fragments med hjälp av MSM for Assets](#reusing-content-fragments-with-msm-assets)

>[!NOTE]
>
>Dessa sidor kan läsas med:
>
>* [Sidredigering med innehållsfragment](/help/sites-cloud/authoring/fragments/content-fragments.md).
>* [Anpassa och utöka Content Fragments](/help/implementing/developing/extending/content-fragments-customizing.md)
>* [Content Fragments – konfigurera komponenter för återgivning](/help/implementing/developing/extending/content-fragments-configuring-components-rendering.md)
>* [Stöd för Content Fragments i AEM Assets HTTP API](/help/assets/content-fragments/assets-api-content-fragments.md)
>* [AEM GraphQL API för användning med Content Fragments](/help/headless/graphql-api/content-fragments.md)

Antalet kommunikationskanaler ökar årligen. Kanalerna avser vanligen leveransmekanismen, antingen som:

* Fysisk kanal, till exempel dator, mobil.
* Leveranssätt i en fysisk kanal, t.ex.&quot;produktinformationssida&quot;,&quot;produktkategorisida&quot; för dator eller&quot;mobilwebb&quot;,&quot;mobilapp&quot; för mobil.

Men du vill (förmodligen) inte använda samma innehåll för alla kanaler. Du måste optimera innehållet utifrån den specifika kanalen.

Med innehållsfragment kan du:

* Fundera på hur ni kan nå målgrupper effektivt i alla kanaler.
* Skapa och hantera kanalneutralt redaktionellt innehåll.
* Bygg innehållspooler för en rad olika kanaler.
* Utforma innehållsvarianter för specifika kanaler.
* Lägg till bilder i texten genom att infoga resurser (blandade mediefragment).
* Skapa kapslat innehåll så att ni speglar komplexiteten i era data.

Dessa innehållsfragment kan sedan sammanställas för att ge upplevelser över olika kanaler.

>[!NOTE]
>
>**Innehållsfragment** och **[Upplevelsefragment](/help/sites-cloud/authoring/fragments/content-fragments.md)** har olika funktioner i AEM:
>* **Innehållsfragment** är redaktionellt innehåll, med definition och struktur, men utan ytterligare visuell design och/eller layout. De kan användas för att komma åt strukturerade data, bland annat texter, siffror och datum.
>* **Upplevelsefragment** är helt utformat för innehåll, ett fragment av en webbsida.
>
>Upplevelsefragment kan innehålla innehåll i form av Content Fragments, men inte tvärtom.
>
>Mer information finns även i [Förstå innehållsfragment och upplevelsefragment i AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/content-fragments/understand-content-fragments-and-experience-fragments.html#content-fragments).

## Innehållsfragment och innehållstjänster {#content-fragments-and-content-services}

AEM Content Services är utformat för att generera beskrivning och leverans av innehåll i/från AEM utöver fokus på webbsidor.

De levererar innehåll till kanaler som inte är traditionella AEM webbsidor, med standardiserade metoder som kan användas av alla kunder. Dessa kanaler kan omfatta:

* Enkelsidiga program
* Inbyggda mobilappar
* andra kanaler och beröringspunkter än AEM

Leveransen görs i JSON-format med hjälp av JSON-exporteraren.

AEM Content Fragments kan användas för att beskriva och hantera strukturerat innehåll. Strukturerat innehåll definieras i modeller som kan innehålla olika innehållstyper, bland annat text, numeriska data, booleskt, datum och tid.

Tillsammans med JSON-exportfunktionerna i AEM kärnkomponenter kan detta strukturerade innehåll sedan användas för att leverera AEM till andra kanaler än AEM.

>[!NOTE]
>
>Se [Headless och AEM](/help/headless/introduction.md) för en introduktion till Headless Development för AEM Sites as a Cloud Service.

>[!NOTE]
>
>AEM har också stöd för översättning av fragmentinnehåll. Se [Översätta resurser](/help/assets/translate-assets.md) för ytterligare information.

## Innehållstyp {#content-type}

Innehållsfragmenten är:

* Lagrad som **Resurser**:

   * Innehållsfragment (och deras variationer) kan skapas och underhållas från **Resurser** konsol.
   * Skapat och redigerat i Content Fragment Editor.

* Används i [sidredigeraren av komponenten Content Fragment](/help/sites-cloud/authoring/fragments/content-fragments.md) (refererande komponent):

   * The **Innehållsfragment** -komponenten är tillgänglig för sidförfattare. De kan referera till och leverera det nödvändiga innehållsfragmentet i antingen HTML- eller JSON-format.

* Tillgängligt med [AEM GRAPHQL API](/help/headless/graphql-api/content-fragments.md).

Innehållsfragment är en innehållsstruktur som:

* Har ingen layout eller design (viss textformatering är möjlig i RTF-läge).
* Innehåller en eller flera [beståndsdelar](#constituent-parts-of-a-content-fragment).
* [Innehåller eller kan kopplas till bilder](#fragments-with-visual-assets).
* Används [mellanliggande innehåll](#in-between-content-when-page-authoring-with-content-fragments) när den refereras på en sida.
* De är oberoende av leveransmekanismen (d.v.s. sidan, kanalen).

### Fragment med visuella resurser {#fragments-with-visual-assets}

För att ge författarna bättre kontroll över sitt innehåll kan bilder läggas till och/eller integreras med ett innehållsfragment.

Resurser kan användas med ett innehållsfragment på flera sätt, vart och ett med sina egna fördelar:

* **Infoga resurs** till ett fragment (blandade mediefragment)

   * De är en del av fragmentet (se [Beståndsdelar i ett Content Fragment](#constituent-parts-of-a-content-fragment)).
   * Definiera mediefilens position.
   * Se [Infoga objekt i ett fragment](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment) i Fragment Editor om du vill ha mer information.

  >[!NOTE]
  >
  >Visuella resurser som infogas i själva innehållsfragmentet är kopplade till föregående stycke. När avsnittet läggs till på en sida flyttas resurserna i förhållande till stycket när det mellanliggande innehållet läggs till.

* **Associerat innehåll**

   * ansluten till ett fragment, men inte till en fast del av fragmentet (se [Beståndsdelar i ett Content Fragment](#constituent-parts-of-a-content-fragment)).
   * Har viss flexibilitet för placering.
   * Enkelt tillgängligt för användning (som mellanliggande innehåll) när du använder fragmentet på en sida.

  Se [Associerat innehåll](/help/assets/content-fragments/content-fragments-assoc-content.md) för mer information.

* Resurser som är tillgängliga från **resursläsaren** i sidredigeraren

   * Möjliggör full flexibilitet för val av en resurs.
   * Har viss flexibilitet för placering.
   * Innebär inte att man kan godkänna ett visst fragment.

  Se [Resursläsaren](/help/sites-cloud/authoring/page-editor/editor-side-panel.md#assets-browser) för mer information.

### Komponentdelar i ett innehållsfragment {#constituent-parts-of-a-content-fragment}

Resurserna för innehållsfragmentet består av följande delar (antingen direkt eller indirekt):

* **Fragmentelement**

   * Elementen korrelerar till de datafält som innehåller innehåll.
   * Du använder en innehållsmodell för att skapa innehållsfragmentet. Elementen (fälten) som anges i modellen definierar fragmentets struktur. Dessa element (fält) kan vara av olika datatyper.

* **Fragmentera stycken**

   * Textblock, ofta flerradiga, som avgränsas som enskilda enheter.

   * I lägena [RTF](/help/assets/content-fragments/content-fragments-variations.md#rich-text) och [Markdown-kod](/help/assets/content-fragments/content-fragments-variations.md#markdown) kan ett stycke formateras som en rubrik, och då utgör det och det efterföljande stycket en enhet.

   * Aktivera innehållskontroll vid sidredigering.

* **Resurser som infogats i ett fragment (blandade mediefragment)**

   * Resurser (bilder) infogade i det faktiska fragmentet och används som det interna innehållet i ett fragment.
   * Inbäddad i fragmentets styckesystem.
   * Kan formateras när [används/refereras till på en sida](/help/sites-cloud/authoring/fragments/content-fragments.md).
   * Kan endast läggas till, tas bort från eller flyttas inom ett fragment med fragmentredigeraren. Dessa åtgärder kan inte utföras i sidredigeraren.
   * Kan endast läggas till, tas bort från eller flyttas inom ett fragment med [RTF-format i fragmentredigeraren](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment).
   * Kan endast läggas till i flerradiga textelement (alla fragmenttyper).
   * Kopplas till föregående text (stycke).

     >[!CAUTION]
     >
     >Du kan ta bort resurser från ett fragment (av misstag) genom att växla till normalt textformat.

     >[!NOTE]
     >
     >Resurser kan också läggas till som ytterligare innehåll (däremellan) när du använder ett fragment på en sida. Använd antingen [Associerat innehåll](/help/assets/content-fragments/content-fragments-assoc-content.md) eller resurser från resurswebbläsaren.

* **Associerat innehåll**

   * Det här är innehåll som inte hör till, men har redaktionell relevans för, ett fragment. Normalt bilder, videor eller andra fragment.
   * De enskilda objekten i samlingen är tillgängliga för användning med avsnittet i sidredigeraren när det läggs till på en sida. Det innebär att de är valfria, beroende på kraven i den specifika kanalen.
   * Resurserna är [som är kopplade till fragment via samlingar](/help/assets/content-fragments/content-fragments-assoc-content.md); associerade samlingar låter författaren bestämma vilka resurser som ska användas när de redigerar sidan.

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

* **Master**

   * En del av fragmentet

      * Varje innehållsfragment har en instans av Master.
      * Master kan inte tas bort.

   * Mallen är tillgänglig i fragmentredigeraren under **[Variationer](/help/assets/content-fragments/content-fragments-variations.md)**.
   * Huvudet är inte en variation i sig, utan baserar alla variationer.

* **Variationer**

   * Återgivningar av fragmenttext som är specifik för ett redaktionellt syfte. Den kan vara relaterad till kanalen men är inte obligatorisk, men kan även användas för lokala ad hoc-ändringar.
   * Skapas som kopior av **Master**, men kan sedan redigeras efter behov. Innehållet överlappar själva variationerna.
   * Kan definieras vid fragmentredigering.
   * Lagras i fragmentet för att undvika spridning av innehållskopior.
   * Variationer kan vara [synkroniserad](/help/assets/content-fragments/content-fragments-variations.md#synchronizing-with-master) med Master om mallinnehållet har uppdaterats.
   * Kan [Sammanfattad](/help/assets/content-fragments/content-fragments-variations.md#summarizing-text) för att snabbt korta av texten till en fördefinierad längd.
   * Tillgängligt under [Variationer](/help/assets/content-fragments/content-fragments-variations.md) i fragmentredigeraren.

### Mellan innehåll vid sidredigering med innehållsfragment {#in-between-content-when-page-authoring-with-content-fragments}

Mellanliggande innehåll:

* Kan användas i sidredigeraren när du arbetar med innehållsfragment.
* [Ytterligare innehåll som läggs till i flödet i ett fragment](/help/sites-cloud/authoring/fragments/content-fragments.md#adding-in-between-content) efter att det har använts eller refererats på en sida.
* Finns att använda i [Sidredigeraren när du arbetar med innehållsfragment](/help/sites-cloud/authoring/fragments/content-fragments.md).
* Mellanliggande innehåll kan läggas till i vilket fragment som helst, där bara ett element är synligt.
* Associerat innehåll kan användas, liksom resurser och/eller komponenter från lämplig webbläsare.

>[!CAUTION]
>
>Det mellanliggande innehållet är sidinnehåll. Den lagras inte i innehållsfragmentet.

### Krävs av fragment {#required-by-fragments}

Om du vill skapa innehållsfragment måste du:

* **Innehållsmodell**

   * är [aktiveras med hjälp av Konfigurationsläsaren](/help/assets/content-fragments/content-fragments-configuration-browser.md).
   * är [skapad med verktyg](/help/assets/content-fragments/content-fragments-models.md).
   * Krävs för [skapa ett fragment](/help/assets/content-fragments/content-fragments-managing.md#creating-content-fragments).
   * Definierar strukturen för ett fragment (rubrik, innehållselement, taggdefinitioner).
   * Innehållsmodelldefinitioner kräver en titel och ett dataelement. Allt annat är valfritt.
   * Modellen kan definiera standardinnehåll, om tillämpligt.
   * Författare kan inte ändra den definierade strukturen när de redigerar fragmentinnehåll.
   * Ändringar som görs i en modell efter att beroende innehållsfragment har skapats kan påverka dessa innehållsfragment.

Om du vill använda dina innehållsfragment för att skapa sidor behöver du också:

* **Innehållsfragmentkomponent**

   * Instrumental för att leverera fragmentet i HTML-format, JSON-format eller båda.
   * Krävs för att [referera till avsnittet på en sida](/help/sites-cloud/authoring/fragments/content-fragments.md).
   * Ansvarig för layout och leverans av ett fragment, det vill säga kanaler.
   * Fragment behöver en eller flera dedikerade komponenter för att definiera layouten och leverera vissa eller alla element/varianter och tillhörande innehåll.
   * Om du drar ett fragment till en sida när du redigerar kopplas den nödvändiga komponenten automatiskt till.

## Återanvända innehållsfragment med MSM (för resurser) {#reusing-content-fragments-with-msm-assets}

Vid åtkomst via **Resurser** kan du använda MSM och skapa Live-kopior för dina fragment.

Mer information finns i:

* [Återanvänd Content Fragments med MSM (for Assets)](/help/assets/content-fragments/content-fragments-msm.md)
* [Återanvänd resurser med MSM for Assets](/help/assets/reuse-assets-using-msm.md).

Dessa aktivera [arv](/help/assets/content-fragments/content-fragments-variations.md#inheritance) för både variationer och enskilda fält i fragment.

>[!CAUTION]
>
>Om du vill använda MSM (som skapar kopior av Content Fragments), så **Unikt** begränsningar tas bort från alla datatyper som används i respektive [Modeller för innehållsfragment](/help/assets/content-fragments/content-fragments-models.md).

## Exempel på användning {#example-usage}

Ett fragment, med dess element och variationer, kan användas för att skapa sammanhängande innehåll för flera kanaler. När du utformar ditt fragment bör du tänka på vad som används och var det används.

### WKND-exempel {#wknd-sample}

The [WKND-plats](/help/implementing/developing/introduction/develop-wknd-tutorial.md) finns exempel som hjälper dig att lära dig mer om AEM as a Cloud Service.

WKND-projektet innehåller:

* Content Fragment Models available under:
  `http://<hostname>:<port>/libs/dam/cfm/models/console/content/models.html/conf/wknd`

* Innehållsfragment (och annat innehåll) tillgängliga under:
  `http://<hostname>:<port>/assets.html/content/dam/wknd/en`

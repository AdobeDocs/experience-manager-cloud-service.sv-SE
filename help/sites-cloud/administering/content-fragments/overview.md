---
title: En översikt över hur du arbetar med innehållsfragment
description: Lär dig hur innehållsfragment i AEM as a Cloud Service gör att du kan skapa och använda innehåll, idealiskt för rubrikfri leverans och sidredigering.
feature: Content Fragments
role: User, Developer, Architect
exl-id: ce9cb811-57d2-4a57-a360-f56e07df1b1a
source-git-commit: 19685cb952a890731bd7d75a2adf3cfd841a465f
workflow-type: tm+mt
source-wordcount: '1792'
ht-degree: 1%

---

# En översikt över hur du arbetar med innehållsfragment {#overview-working-with-content-fragments}

Med Adobe Experience Manager (AEM) as a Cloud Service kan du skapa, redigera och [publicera sidoberoende innehåll](/help/sites-cloud/authoring/fundamentals/content-fragments.md). Med dem kan du förbereda innehåll som är klart för användning på flera platser, och över flera kanaler, idealiskt för headless leverans, och skapa sidor.

>[!IMPORTANT]
>
>Du kan komma åt innehållsfragment från två konsoler: **Innehållsfragment** och **Resurser**.
>
>Det finns också två redigerare för innehållsfragment. (Båda redigerarna är tillgängliga från båda konsolerna.)
>
>Det här avsnittet handlar om **Innehållsfragment** konsolen och *new* Innehållsfragmentsredigerare. Dessa har utvecklats för leverans av headless-innehåll (även om de kan användas för alla scenarier)
>
>Mer information finns i:
>
>* användning av **Resurser** konsol för [hantera innehållsfragment](/help/assets/content-fragments/content-fragments-managing.md)
>* användning av [*original* Innehållsfragmentsredigerare](/help/assets/content-fragments/content-fragments-variations.md),
>* använda [Content Fragments for page-authoring](/help/sites-cloud/authoring/fundamentals/content-fragments.md).


Innehållsfragment innehåller strukturerat innehåll:

* Varje fragment baseras på en [Content Fragment Model](/help/sites-cloud/administering/content-fragments/content-fragment-models.md).
   * Content Fragment Model definierar strukturen för det resulterande fragmentet.
* Varje fragment består av:
   * **[Huvud](#main-and-variations)** - en integrerad del av det fragment som innehåller kärninnehållet, finns alltid, kan inte tas bort
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

Innehållsfragment kan också levereras i JSON-format med JSON-exportfunktionerna (Sling Model) AEM kärnkomponenterna. Leveranssätt:

* gör att du kan använda komponenten för att hantera vilka element i ett fragment som ska levereras
* tillåter massleverans, genom att lägga till flera [Kärnkomponenter för innehållsfragment](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html) på sidan som används för API-leverans

Antalet kommunikationskanaler ökar årligen. Kanalerna avser vanligen leveransmekanismen, antingen som:

* Fysisk kanal, till exempel dator, mobil.
* Leveranssätt i en fysisk kanal, t.ex.&quot;produktinformationssida&quot;,&quot;produktkategorisida&quot; för dator eller&quot;mobilwebb&quot;,&quot;mobilapp&quot; för mobil.

Du (förmodligen) inte vill använda *exakt* samma innehåll för alla kanaler - ni måste optimera innehållet utifrån den specifika kanalen.

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
>**Innehållsfragment** och **[Upplevelsefragment](/help/sites-cloud/authoring/fundamentals/experience-fragments.md)** har olika funktioner i AEM:
>* **Innehållsfragment** är redaktionellt innehåll, med definition och struktur, men utan ytterligare visuell design och/eller layout. De kan användas för att komma åt strukturerade data, bland annat texter, siffror och datum.
>* **Upplevelsefragment** är helt utformat för innehåll, ett fragment av en webbsida.
>
>Upplevelsefragment kan innehålla innehåll i form av innehållsfragment, men inte tvärtom.
>
>Mer information finns i [Förstå innehållsfragment och upplevelsefragment i AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/content-fragments/understand-content-fragments-and-experience-fragments.html#content-fragments).

På den här och följande sidor beskrivs hur du skapar, konfigurerar, underhåller och använder innehållsfragment:

* [Aktivera funktionen för innehållsfragment för din instans](/help/sites-cloud/administering/content-fragments/setup.md)
* [Modeller för innehållsfragment](/help/sites-cloud/administering/content-fragments/content-fragment-models.md) - aktivera, skapa och definiera dina modeller
* [Skapa dina innehållsfragment](/help/sites-cloud/administering/content-fragments/managing.md#creating-a-content-fragment) (med konsolen Innehållsfragment)

När fragmenten har skapats kan du:

* [Använda konsolen Innehållsfragment](/help/sites-cloud/administering/content-fragments/managing.md) - få tillgång till, publicera (för att förhandsgranska eller producera) och referera till dina fragment
* [Använda redigeraren för innehållsfragment](/help/sites-cloud/administering/content-fragments/authoring.md) - redigera, publicera (för att förhandsgranska eller producera) och referera till dina fragment
* [Analysera](/help/sites-cloud/administering/content-fragments/analysis.md)  strukturen för ditt innehållsfragment med hjälp av redigeraren
* [Få tillgång till dina fragment med GraphQL, för headlessleverans till dina applikationer](/help/sites-cloud/administering/content-fragments/content-delivery-with-graphql.md).
* [Eller använd fragmenten för att skapa sidor](/help/sites-cloud/authoring/fundamentals/content-fragments.md)

>[!NOTE]
>
>Dessa sidor kan läsas tillsammans med:
>
>* [Anpassa och utöka Content Fragments](/help/implementing/developing/extending/content-fragments-customizing.md)
>* [Content Fragments – konfigurera komponenter för återgivning](/help/implementing/developing/extending/content-fragments-configuring-components-rendering.md)
>* [Stöd för Content Fragments i AEM Assets HTTP API](/help/assets/content-fragments/assets-api-content-fragments.md)
>* [AEM GraphQL API för användning med innehållsfragment](/help/headless/graphql-api/content-fragments.md)
>* [Sidredigering med innehållsfragment](/help/sites-cloud/authoring/fundamentals/content-fragments.md).

## Huvud och variationer {#main-and-variations}

Variationer är en viktig egenskap i AEM innehållsfragment. De gör att du kan skapa och redigera kopior av **Huvud** innehåll som kan användas i specifika kanaler och scenarier, vilket gör innehållsleverans utan rubrik och sidredigering ännu mer flexibelt.

* **Huvud**

   * **Huvud** är inte en variation i sig, utan utgör grunden för alla ändringar.
   * En integrerad del av fragmentet

      * Varje innehållsfragment har en instans av **Huvud**.
      * **Huvud** kan inte tas bort.

   * **Huvud** är tillgängligt i fragmentredigeraren under **[Variationer](/help/sites-cloud/administering/content-fragments/authoring.md#variations)**.

  >[!NOTE]
  >
  >I redigeraren som finns på **Resurser** konsol, **Huvud** är märkt som **Master**.

* **Variationer**

   * Återgivning av fragmenttext som är specifik för redaktionella ändamål. Den kan vara relaterad till kanalen men är inte obligatorisk, men kan även användas för lokala ad hoc-ändringar.
   * Skapas som kopior av **Huvud**, men kan sedan redigeras efter behov. Innehållet överlappar ofta själva variationerna.
   * Kan definieras under fragmentredigering från den vänstra panelen.
   * Lagras i fragmentet för att undvika spridning av innehållskopior.
   * Variationer kan vara [jämförda och synkroniserade](/help/sites-cloud/administering/content-fragments/authoring.md#compare-and-synchronize-rich-text) med **Huvud**.
  <!--
  * Can be [Summarized](/help/sites-cloud/administering/content-fragments/authoring.md#summarizing-text) to quickly truncate the text to a predefined length.
  -->

## Innehållsfragment och innehållstjänster {#content-fragments-and-content-services}

AEM Content Services är utformat för att generera beskrivning och leverans av innehåll i/från AEM utöver fokus på webbsidor.

De levererar innehåll till kanaler som inte är traditionella AEM webbsidor, med standardiserade metoder som kan användas av alla kunder. Dessa kanaler kan omfatta:

* Enkelsidiga program
* Inbyggda mobilprogram
* andra kanaler och kontaktpunkter externt för AEM

Leveransen görs i JSON-format med JSON-exporteraren.

AEM kan användas för att beskriva och hantera strukturerat innehåll. Strukturerat innehåll definieras i modeller som kan innehålla olika innehållstyper, bland annat text, numeriska data, booleska värden, datum och tid.

Tillsammans med JSON-exportfunktionerna i AEM kärnkomponenter kan detta strukturerade innehåll sedan användas för att leverera AEM till andra kanaler än AEM.

>[!NOTE]
>
>Se [Headless och AEM](/help/headless/introduction.md) för en introduktion till Headless Development för AEM Sites as a Cloud Service.

>[!NOTE]
>
>AEM har också stöd för översättning av fragmentinnehåll. Se [Översätta resurser](/help/assets/translate-assets.md) för ytterligare information.

## Innehållstyp {#content-type}

Innehållsfragmenten är:

* A **Webbplatser** -funktion.

* Lagrad som **Resurser**:

   * Innehållsfragment (och deras variationer) kan skapas och underhållas från [Konsol för innehållsfragment](/help/sites-cloud/administering/content-fragments/managing.md#content-fragments-console).
   * Redigerad i [Innehållsfragmentsredigerare](/help/sites-cloud/administering/content-fragments/authoring.md).

* Tillgängligt för leverans av innehåll med [AEM GRAPHQL API](/help/headless/graphql-api/content-fragments.md).

* Finns i [sidredigeraren med komponenten Content Fragment](/help/sites-cloud/authoring/fundamentals/content-fragments.md) (refererande komponent):

   * The [Kärnkomponent för innehållsfragment](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html) är tillgängligt för sidförfattare. De kan referera till, och leverera, önskat innehållsfragment i antingen HTML- eller JSON-format.

Innehållsfragment är en innehållsstruktur som:

* Är utan layout eller design (textformatering är möjlig för textfält).
* Är oberoende av leveransmekanismen (till exempel sidan eller kanalen).
* Innehåller en eller flera [beståndsdelar](#constituent-parts-of-a-content-fragment).
* Kan [innehålla eller vara ansluten till bilder](#fragments-with-visual-assets).

### Fragment med visuella resurser {#fragments-with-visual-assets}

För att ge författarna bättre kontroll över sitt innehåll kan bilder läggas till och/eller integreras med ett innehållsfragment.

Resurser kan användas med ett innehållsfragment på flera sätt, vart och ett med sina egna fördelar:

* som **Innehållsreferens**
* inom en **Flerradstext** fält

### Komponentdelar i ett innehållsfragment {#constituent-parts-of-a-content-fragment}

Resurserna för innehållsfragment består av följande delar (antingen direkt eller indirekt):

* **Fragmentelement**

   * Elementen korrelerar till de datafält som innehåller innehåll.
   * Du använder en [Content Fragment Model](/help/sites-cloud/administering/content-fragments/content-fragment-models.md) för att skapa innehållsfragmentet. Elementen (fälten) som anges i modellen definierar fragmentets struktur. Dessa element (fält) kan vara av olika datatyper.

* **Fragmentera stycken**

   * Textblock, ofta flerradiga, som avgränsas som enskilda enheter.

   * Aktivera innehållskontroll vid sidredigering.

* **Fragmentmetadata**

   * Använd [Resurser för metadatamodeller](/help/assets/metadata-schemas.md).
   * Taggar kan skapas när du:

      * Skapa och redigera fragmentet
      * Eller senare, när du [visa eller redigera egenskaperna](/help/sites-cloud/administering/content-fragments/authoring.md#view-properties-tags) i fragmentredigeraren

  >[!CAUTION]
  >
  >Metadatabearbetningsprofiler gäller inte för innehållsfragment.

  >[!CAUTION]
  >
  >En innehållsfragmentmodell kan ofta definiera datafält med namnet **Titel** och **Beskrivning**. Om de här två fälten finns är de användardefinierade och kan uppdateras i redigerarens innehållsområde.
  >
  >Innehållsfragmentet och dess varianter har också metadatafält (egenskap) som kallas **Titel** och **Beskrivning**. Dessa två metadatafält är en integrerad del av alla innehållsfragment, och variationer, och definieras ursprungligen när fragmentet skapas. De kan uppdateras under Egenskaper/metadata i redigeraren.

* **[Huvud](#main-and-variations)**
* **[Variationer](#main-and-variations)**

### Krävs av fragment {#required-by-fragments}

Om du vill skapa innehållsfragment behöver du:

* **Innehållsmodell**

   * är [aktiveras med hjälp av Konfigurationsläsaren](/help/sites-cloud/administering/content-fragments/setup.md).
   * är [skapad med verktyg](/help/sites-cloud/administering/content-fragments/content-fragment-models.md).
   * Krävs för [skapa ett fragment](/help/sites-cloud/administering/content-fragments/managing.md#creating-content-fragments).
   * Definierar strukturen för ett fragment (rubrik, innehållselement, taggdefinitioner).
   * Definitioner av innehållsfragmentmodellen kräver en titel och ett dataelement. Allt annat är valfritt.
   * Modellen kan definiera standardinnehåll, om tillämpligt.
   * Författare kan inte ändra den definierade strukturen när de redigerar fragmentinnehåll, men de kan öppna modellredigeraren från fragmentredigeraren.
   * Ändringar som görs i en modell efter att beroende innehållsfragment har skapats kan påverka dessa innehållsfragment.

Om du vill använda dina innehållsfragment för leverans av headless-innehåll behöver du också:

* a [GraphQL query](/help/headless/graphql-api/content-fragments.md) för att begära nödvändigt innehåll
* det här innehållet kan sedan användas för att utveckla egna SPA för AEM. Mer information finns i följande dokument:

   * [SPA WKND - självstudiekurs](/help/implementing/developing/hybrid/wknd-tutorial.md)
   * [Komma igång med React](/help/implementing/developing/hybrid/getting-started-react.md)
   * [Komma igång med Angular](/help/implementing/developing/hybrid/getting-started-angular.md)

Om du vill använda dina innehållsfragment för att skapa sidor behöver du också:

* A **Innehållsfragmentkomponent**

   * Instrumentellt för att leverera fragmentet i HTML- och/eller JSON-format.
   * Krävs för [referera till fragmentet på en sida](/help/sites-cloud/authoring/fundamentals/content-fragments.md).
   * Ansvarig för layout och leverans av ett fragment, t.ex. kanaler.
   * Fragment behöver en eller flera dedikerade komponenter för att definiera layout och leverera vissa eller alla element/varianter och tillhörande innehåll.
   * Om du drar ett fragment till en sida när du redigerar kopplas den nödvändiga komponenten automatiskt till.
   * Se [Kärnkomponent för innehållsfragment](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html).

## Exempel på användning {#example-usage}

Ett fragment, med dess element och variationer, kan användas för att skapa sammanhängande innehåll för flera kanaler. När du utformar ditt fragment måste du tänka på vad som kommer att användas och var.

### WKND-exempel {#wknd-sample}

The [WKND-webbplats och WKND delad](/help/implementing/developing/introduction/develop-wknd-tutorial.md) finns exempel som hjälper dig att lära dig mer om AEM as a Cloud Service.

<!-- CHECK: which links can/should be used these days? -->

WKND-projektet innehåller:

* Content Fragment Models available under:

   * `.../libs/dam/cfm/models/console/content/models.html/conf/wknd`

   * `.../ui#/aem/libs/dam/cfm/models/console/content/models.html/conf/wknd-shared`

* Innehållsfragment (och annat innehåll) tillgängliga under:

   * `.../assets.html/content/dam/wknd/en`

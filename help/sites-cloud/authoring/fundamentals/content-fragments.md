---
title: Innehållsfragment
description: Med Adobe Experience Manager som Cloud Service Content Fragments kan du utforma, skapa, strukturera och använda sidoberoende innehåll
translation-type: tm+mt
source-git-commit: be65ba65fb6bbd7634da882ef8337565f1fce477
workflow-type: tm+mt
source-wordcount: '1165'
ht-degree: 3%

---


# Innehållsfragment {#content-fragments}

Innehållsfragment i Adobe Experience Manager (AEM) som en Cloud Service [skapas och hanteras som sidoberoende resurser](/help/assets/content-fragments/content-fragments.md).

Med dem kan du skapa kanalneutralt innehåll tillsammans med (eventuellt kanalspecifika) variationer. Du kan sedan använda dessa fragment och deras variationer när du redigerar innehållssidorna.

Tillsammans med den uppdaterade JSON-exporteraren kan strukturerade innehållsfragment även användas för att leverera AEM innehåll via Content Services till andra kanaler än AEM.

>[!NOTE]
>
>**Content Fragments** and **[Experience Fragments](/help/sites-cloud/authoring/fundamentals/experience-fragments.md)** are different features within AEM:
>
>* **Innehållsfragment** är redaktionellt innehåll, främst text och relaterade bilder. De är rent innehåll, utan design och layout.
>* **Upplevelsefragment** är helt utformat för innehåll och därmed delar av en webbsida.

>
>
Upplevelsefragment kan innehålla innehåll i form av innehållsfragment, men inte tvärtom.

>[!CAUTION]
>
>Den här sidan måste läsas tillsammans med [Arbeta med innehållsfragment](/help/assets/content-fragments/content-fragments.md) (och relaterade sidor) eftersom den innehåller grundläggande terminologi och koncept samt skapar och hanterar fragment.

Innehållsfragmenten aktiverar:

* **Marknadsförings- och kampanjstrategi**
   * Granska innehåll via centralt hanterade innehållsfragment.
* **Creative Pro**
   * Spåra kreativa resurser via samlingar som är kopplade till innehållsfragment.
* **Kopiera författare**
   * Skriv i AEM innehållsfragmentredigerare.
   * Kan skapa innehållsvariationer.
   * Kan associera relevant innehåll med innehållsfragmentet.
   * Kan använda versionshantering/arbetsflöde.
   * Kan dela innehållsfragment.
   * Kan hantera översättningar centralt.
* **Producenter och reseansvariga**
   * Välj bland fördefinierade fragment och variationer med redigering i AEM.
   * Kan förlita sig på att fragment och tillhörande innehåll alltid är uppdaterade när kopieringsförfattare och kreatörer uppdaterar centralt hanterade fragment och resurser.
   * Kan lita på att tillhörande medieinnehåll kurateras för relevans.
   * Kan skapa tillfälliga innehållsvariationer direkt samtidigt som dessa variationer förblir centralt hanterade i fragmentet.

## Lägga till ett innehållsfragment på sidan {#adding-a-content-fragment-to-your-page}

1. Öppna sidan för redigering.
2. Lägg till komponenten **Innehållsfragment** ; från antingen **komponentwebbläsaren** eller **Infoga ny komponent**.
3. Du kan antingen:
   * Öppna **resursläsaren** och filtrera efter **innehållsfragment** (standardvärdet är Bilder). Dra sedan det önskade fragmentet till komponentinstansen.
   * Markera innehållskomponenten och **Konfigurera** sedan i verktygsfältet. I dialogrutan kan du öppna urvalsdialogrutan för att bläddra och välja önskat **innehållsfragment**.

   >[!NOTE]
   >
   >Ett annat sätt är att dra ett visst innehållsfragment direkt till sidan. Då skapas automatiskt den associerade komponenten (innehållsfragment).

4. Inledningsvis visas innehållet från **Main** Element och **Överordnad** (variation). Du kan [markera andra element och/eller variationer](#selecting-the-element-or-variation) efter behov.

   ![Innehållsfragment i Resursläsaren](/help/sites-cloud/authoring/assets/content-fragments.png)

   >[!NOTE]
   >
   >Mer information om ytterligare redigeringsfunktioner finns även i:
   >
   >* [Responsiv layout](/help/sites-cloud/authoring/features/responsive-layout.md)
   >* [Redigera sidinnehåll](/help/sites-cloud/authoring/fundamentals/editing-content.md)


### Markera elementet eller variationen {#selecting-the-element-or-variation}

Öppna fragmentets dialogruta **Konfiguration** för att konfigurera fragmentet för användning på den aktuella sidan. Dialogrutan kan vara beroende av vilken komponent som används.

>[!NOTE]
>
>Se även [kärnkomponenter, komponenten Content Fragment](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/content-fragment-component.html)

I rätt konfigurationsdialogruta kan du välja tillgängliga parametrar, bland annat:

* **Innehållsfragment**
   * Ange det fragment som ska användas.
* **Visningsläge**:
   * **Enkelt textelement**
   * **Flera element**
* **Element**
   * En markering är tillgänglig beroende på vilken modell som används.

   >[!NOTE]
   >
   >Vilka element som är tillgängliga beror på vilken modell som används.

* **Variant**
   * **Standardmastern** är alltid tillgänglig.
   * En markering blir tillgänglig om variationer har skapats för fragmentet.

* **ID**

   * **HTML ID** -attribut som ska användas för komponenten.

### Snabb anslutning till Fragment Editor {#quick-connection-to-fragment-editor}

Du kan öppna fragmentkällan för redigering (resursen) med ikonen **Redigera** i komponentverktygsfältet. På så sätt kan du [redigera och hantera innehållsfragmentet](/help/assets/content-fragments/content-fragments.md).

>[!CAUTION]
>
>Som alltid kommer redigering av fragmentkällan att påverka alla sidor som refererar till det innehållsfragmentet.

### Lägga till mellaninnehåll {#adding-in-between-content}

När ett visst innehållsfragment läggs till på sidan finns det en **Drag-komponent här** som platshållare mellan varje HTML-stycke (och längst upp/längst ned) i fragmentet.

På så sätt kan du lägga till extra innehåll [däremellan (dvs. mellanliggande innehåll)](/help/assets/content-fragments/content-fragments.md#in-between-content-when-page-authoring-with-content-fragments) i fragmentinnehållet (vid någon av de tillgängliga punkterna) utan att behöva ändra rotfragmentet.

För mellanliggande innehåll kan du:

* Lägg till komponenter från [komponentwebbläsaren](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser).
* Lägg till resurser från [Resurser-webbläsaren](/help/sites-cloud/authoring/fundamentals/environment-tools.md#assets-browser).
* Använd [associerat innehåll](#using-associated-content) som källa för mellanliggande innehåll.

>[!CAUTION]
>
>Det mellanliggande innehållet är sidinnehåll. Den lagras inte i innehållsfragmentet.

![Infoga komponent](/help/sites-cloud/authoring/assets/content-fragments-insert.png)

>[!NOTE]
>
>Du kan också [infoga visuella resurser (bilder) i själva](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment)fragmentet.
>
>Visuella resurser som infogats i själva fragmentet kopplas till föregående stycke i fragmentet. Det innebär att du inte kan placera innehåll mellan en visuell resurs och föregående stycke. Om du behöver den här anslutningsnivån kan du lägga till bilden i fragmentet (som ett [blandat mediefragment](/help/assets/content-fragments/content-fragments.md#fragments-with-visual-assets)).

>[!CAUTION]
>
>När du har lagt till mellanliggande innehåll i ett innehållsfragment på sidan kan ändringar av strukturen för det underliggande innehållsfragmentet (dvs. i innehållsfragmentredigeraren) leda till felaktiga/oväntade resultat.
>
>När detta inträffar behålls det mellanliggande innehållet som det är:
>
>* Mellanliggande komponenter har en absolut position inom komponentsekvensen i fragmentflödet. Den här positionen ändras inte, även när innehållet i styckena i fragmentet ändras.
>
>  
Detta kan få det att se ut som om den relativa placeringen har ändrats, eftersom mellanliggande stycken inte har någon kontextuell relation till (fragmentet) stycken som de är placerade bredvid.
>* Om inte de två styckestrukturerna står i konflikt med varandra. I så fall visas inte det mellanliggande innehållet (även om det fortfarande finns internt).


### Använda associerat innehåll {#using-associated-content}

Om du har [associerat innehåll](/help/assets/content-fragments/content-fragments-assoc-content.md) med [innehållsfragmentet](/help/assets/content-fragments/content-fragments.md) är dessa resurser tillgängliga från sidopanelen (när du har placerat fragmentet på innehållssidan). Associated content is effectively a special source of content for [in-between content](/help/assets/content-fragments/content-fragments.md#in-between-content-when-page-authoring-with-content-fragments).

>[!NOTE]
>
>Det finns olika metoder för att lägga till [visuella resurser (t.ex. bilder)](/help/assets/content-fragments/content-fragments.md#fragments-with-visual-assets) till fragmentet och/eller sidan.

>[!NOTE]
>
>Om du har flera innehållsfragment på en sida visar fliken **Associerat innehåll** resurser som passar alla fragment.

När du har lagt till ett fragment med associerat innehåll på sidan öppnas en ny flik (**Associerat innehåll**) på sidopanelen.

Här kan du dra resurserna till önskad plats (antingen till en befintlig komponent eller till önskad plats där rätt komponent skapas):

![Infoga en bild](/help/sites-cloud/authoring/assets/content-fragments-image.png)

### Resurser som infogats i fragmentet {#assets-inserted-into-the-fragment}

Om resurser (t.ex. bilder) har infogats i själva fragmentet (som [blandade mediefragment](/help/assets/content-fragments/content-fragments.md#fragments-with-visual-assets)) är alternativen för att redigera dessa resurser i sidredigeraren begränsade.

För en bild kan du till exempel

* Beskär, rotera eller vänd bilden.
* Lägg till en titel eller alternativ text.
* Ange en storlek.
* Du kan också konfigurera layouten.

Andra ändringar, till exempel move, copy, delete, måste göras i fragmentredigeraren.

### Publicering {#publishing}

Fragment måste publiceras så att de kan användas på dina publicerade webbsidor:

* Ett fragment kan publiceras efter [att fragmentet har skapats i resurskonsolen](/help/assets/content-fragments/content-fragments-managing.md#publishing-and-referencing-a-fragment).
* Om ett *opublicerat fragment* används på en sida som publiceras kan fragmentet också publiceras just nu.

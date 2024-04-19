---
title: Innehållsfragment
description: Med Adobe Experience Manager as a Cloud Service Content Fragments kan du utforma, skapa, strukturera och använda sidoberoende innehåll
exl-id: 7a44fc4e-3793-4aa3-8c21-db0567c93244
source-git-commit: 0ad9f349c997c35862e4f571b4741ed4c0c947e2
workflow-type: tm+mt
source-wordcount: '1273'
ht-degree: 0%

---

# Innehållsfragment {#content-fragments}

Innehållsfragment i Adobe Experience Manager (AEM) as a Cloud Service är [skapat och hanterat som sidoberoende resurser](/help/sites-cloud/administering/content-fragments/overview.md).

Med dem kan du skapa kanalneutralt innehåll tillsammans med (eventuellt kanalspecifika) variationer. Du kan sedan använda dessa fragment och deras variationer när du redigerar innehållssidorna.

Tillsammans med den uppdaterade JSON-exporteraren kan strukturerade innehållsfragment även användas för att leverera AEM innehåll via Content Services till andra kanaler än AEM.

>[!NOTE]
>
>Innehållsfragment är en **Webbplatser** -funktionen, men lagras som **Resurser**.
>
>De hanteras nu främst med **[Innehållsfragment](/help/sites-cloud/administering/content-fragments/managing.md#content-fragments-console)** konsolen, men de kan fortfarande hanteras från **[Resurser](/help/assets/content-fragments/content-fragments-managing.md)** konsol.
>
>Det finns två redigerare för att skapa innehållsfragment:
>
>* Den nya redigeraren för [Content Fragments - Authoring](/help/sites-cloud/administering/content-fragments/authoring.md), kommer i första hand åt från **Innehållsfragment** konsol.
>* The [originalredigerare](/help/assets/content-fragments/content-fragments-variations.md) primärt hämtas från **Resurser** konsol.

>[!NOTE]
>
>**Innehållsfragment** och **[Upplevelsefragment](/help/sites-cloud/authoring/fundamentals/experience-fragments.md)** har olika funktioner i AEM:
>* **Innehållsfragment** är redaktionellt innehåll, med definition och struktur, men utan ytterligare visuell design och/eller layout. De kan användas för att få tillgång till strukturerade data, bland annat texter, siffror och datum.
>* **Upplevelsefragment** är helt utformat för innehåll, ett fragment av en webbsida.
>
>Upplevelsefragment kan innehålla innehåll i form av innehållsfragment, men inte tvärtom.
>
>Mer information finns i [Förstå innehållsfragment och upplevelsefragment i AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/content-fragments/understand-content-fragments-and-experience-fragments.html#content-fragments).

>[!CAUTION]
>
>Den här sidan måste läsas tillsammans med [Arbeta med innehållsfragment](/help/sites-cloud/administering/content-fragments/overview.md) (och relaterade sidor) eftersom det innehåller grundläggande terminologi och begrepp, tillsammans med att skapa och hantera fragment.

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
   * Välj bland fördefinierade fragment och variationer med AEM.
   * Kan förlita sig på att fragment och tillhörande innehåll alltid är uppdaterade när kopieringsförfattare och kreatörer uppdaterar centralt hanterade fragment och resurser.
   * Kan lita på att tillhörande medieinnehåll kurateras för relevans.
   * Kan skapa tillfälliga innehållsvariationer direkt samtidigt som dessa variationer förblir centralt hanterade i fragmentet.

## Lägga till ett innehållsfragment på sidan {#adding-a-content-fragment-to-your-page}

1. Öppna sidan för redigering.
2. Lägg till **Innehållsfragment** från någon av **Komponenter** webbläsare **Infoga ny komponent**.
3. Du kan antingen:
   * Öppna **Resurser** webbläsare och filter för **Innehållsfragment** (standard är Bilder). Dra sedan det önskade fragmentet till komponentinstansen.
   * Markera innehållets fragmentkomponent och sedan **Konfigurera** i verktygsfältet. I dialogrutan kan du öppna urvalsdialogrutan för att bläddra och välja önskat alternativ **Innehållsfragment**.

   >[!NOTE]
   >
   >Ett annat sätt är att dra ett visst innehållsfragment direkt till sidan. Då skapas automatiskt den associerade komponenten (innehållsfragment).

4. Till att börja med innehåller innehållet från **Huvud** Element och **Master** (variation) visas. Du kan [markera andra element och/eller variationer](#selecting-the-element-or-variation) efter behov.

   ![Innehållsfragment i Resursläsaren](/help/sites-cloud/authoring/assets/content-fragments.png)

   >[!NOTE]
   >
   >Mer information om ytterligare redigeringsfunktioner finns även i:
   >
   >* [Responsiv layout](/help/sites-cloud/authoring/features/responsive-layout.md)
   >* [Redigera sidinnehåll](/help/sites-cloud/authoring/fundamentals/editing-content.md)

### Markera elementet eller variationen {#selecting-the-element-or-variation}

Öppna fragmentets **Konfiguration** för att konfigurera fragmentet för användning på den aktuella sidan. Dialogrutan kan vara beroende av vilken komponent som används.

>[!NOTE]
>
>Se även [Kärnkomponenter, komponenten Innehållsfragment](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html)

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
   * Standardvärdet **Master** är alltid tillgängligt.
   * En markering är tillgänglig om variationer har skapats för fragmentet.

* **ID**

   * **HTML ID** -attribut som ska användas på komponenten.

### Snabb anslutning till Fragment Editor {#quick-connection-to-fragment-editor}

Du kan öppna fragmentkällan för redigering (resursen) med **Redigera** -ikonen i komponentens verktygsfält. Då kan du [redigera och hantera innehållsfragmentet](/help/sites-cloud/administering/content-fragments/overview.md).

>[!CAUTION]
>
>Som alltid kommer redigering av fragmentkällan att påverka alla sidor som refererar till det innehållsfragmentet.

### Lägga till mellaninnehåll {#adding-in-between-content}

När ett visst innehållsfragment läggs till på sidan finns det ett **Dra komponenter hit** platshållare mellan styckena HTML (och längst upp/längst ned) i fragmentet.

Detta gör att du kan lägga till extra innehåll [in-between (d.v.s. in-between content)](/help/assets/content-fragments/content-fragments.md#in-between-content-when-page-authoring-with-content-fragments) fragmentinnehållet (vid någon av de tillgängliga punkterna), utan att behöva ändra rotfragmentet.

För mellanliggande innehåll kan du:

* Lägg till komponenter från [Komponentwebbläsare](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser).
* Lägg till resurser från [Resursläsaren](/help/sites-cloud/authoring/fundamentals/environment-tools.md#assets-browser).
* Använd [Associerat innehåll](#using-associated-content) som en källa för mellanliggande innehåll.

>[!CAUTION]
>
>Det mellanliggande innehållet är sidinnehåll. Den lagras inte i innehållsfragmentet.

![Infoga komponent](/help/sites-cloud/authoring/assets/content-fragments-insert.png)

>[!NOTE]
>
>Du kan också [infoga visuella resurser (bilder) i själva fragmentet](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment).
>
>Visuella resurser som infogats i själva fragmentet kopplas till föregående stycke i fragmentet. Det innebär att du inte kan placera innehåll mellan en visuell resurs och föregående stycke. Om du behöver den här anslutningsnivån kan du lägga till bilden i fragmentet (som en [blandat mediefragment](/help/assets/content-fragments/content-fragments.md#fragments-with-visual-assets)).

>[!CAUTION]
>
>När du har lagt till mellanliggande innehåll i ett innehållsfragment på sidan kan en ändring av strukturen för det underliggande innehållsfragmentet (det vill säga i innehållsfragmentets redigerare) leda till felaktiga/oväntade resultat.
>
>När detta inträffar behålls det mellanliggande innehållet som det är:
>
>* Mellanliggande komponenter har en absolut position inom komponentsekvensen i fragmentflödet. Den här positionen ändras inte, även när innehållet i styckena i fragmentet ändras.
>
>  Detta kan få det att se ut som om den relativa placeringen har ändrats, eftersom mellanliggande stycken inte har någon kontextuell relation till (fragmentet) stycken som de är placerade bredvid.
>* Såvida inte de två styckestrukturerna står i konflikt med varandra, visas inte det mellanliggande innehållet (även om det fortfarande finns internt).

### Använda associerat innehåll {#using-associated-content}

Om du har [associerat innehåll](/help/assets/content-fragments/content-fragments-assoc-content.md) med [innehållsfragment](/help/assets/content-fragments/content-fragments.md) dessa resurser är tillgängliga från sidopanelen (när du har placerat fragmentet på innehållssidan). Associerat innehåll är i själva verket en särskild innehållskälla för [mellanliggande innehåll](/help/assets/content-fragments/content-fragments.md#in-between-content-when-page-authoring-with-content-fragments).

>[!NOTE]
>
>Det finns olika metoder att lägga till [visuella resurser (till exempel bilder)](/help/assets/content-fragments/content-fragments.md#fragments-with-visual-assets) till fragmentet och/eller sidan.

>[!NOTE]
>
>Om du har flera innehållsfragment på en sida **Associerat innehåll** -fliken visar resurser som passar alla fragment.

När du har lagt till ett fragment med associerat innehåll på sidan visas en ny flik (**Associerat innehåll**) öppnas på sidopanelen.

Här kan du dra resurserna till önskad plats (antingen till en befintlig komponent eller till önskad plats där rätt komponent skapas):

![Infoga en bild](/help/sites-cloud/authoring/assets/content-fragments-image.png)

### Resurser som infogats i fragmentet {#assets-inserted-into-the-fragment}

Om resurser (till exempel bilder) har infogats i själva fragmentet (som [blandade mediefragment](/help/assets/content-fragments/content-fragments.md#fragments-with-visual-assets)) är alternativen för att redigera dessa resurser i sidredigeraren begränsade.

För en bild kan du till exempel

* Beskär, rotera eller vänd bilden.
* Lägg till en titel eller alternativ text.
* Ange en storlek.
* Du kan också konfigurera layouten.

Andra ändringar, som att flytta, kopiera och ta bort, måste göras i fragmentredigeraren.

### Publicering {#publishing}

Fragment måste publiceras så att de kan användas på dina publicerade webbsidor:

* Ett fragment kan publiceras efter [skapa fragmentet i konsolen för innehållsfragment](/help/sites-cloud/administering/content-fragments/managing.md#publishing-and-previewing-a-fragment).
* Om en *opublicerat fragment* används på en sida som publiceras, kan fragmentet också publiceras just nu.

## Exportera innehållsfragment {#exporting-content-fragments}

Vid export till Adobe Target kan JSON användas för att leverera fragmentet. Se:

* [Integrera med Adobe Target](/help/sites-cloud/integrating/integrating-adobe-target.md)
* [Exportera innehållsfragment till Adobe Target](/help/sites-cloud/integrating/content-fragments-target.md)

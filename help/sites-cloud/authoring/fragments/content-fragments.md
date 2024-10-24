---
title: Innehållsfragment
description: Med Adobe Experience Manager as a Cloud Service Content Fragments kan du utforma, skapa, strukturera och använda kanaloberoende innehåll som också kan användas när du skapar sidor.
exl-id: 7a44fc4e-3793-4aa3-8c21-db0567c93244
solution: Experience Manager Sites
feature: Authoring, Content Fragments
role: User
source-git-commit: b2b38a3163925fdc2bd4c5f78aaddb44ae716601
workflow-type: tm+mt
source-wordcount: '1267'
ht-degree: 0%

---

# Innehållsfragment {#content-fragments}

Innehållsfragment i Adobe Experience Manager (AEM)-as a Cloud Service [skapas och hanteras som sidoberoende resurser](/help/sites-cloud/administering/content-fragments/overview.md), vilket gör att du kan skapa kanalneutralt innehåll tillsammans med (eventuellt kanalspecifika) varianter. Du kan använda dessa fragment och deras variationer när du redigerar innehållssidorna.

>[!CAUTION]
>
>Den här sidan måste läsas tillsammans med [Arbeta med innehållsfragment](/help/sites-cloud/administering/content-fragments/overview.md) (och relaterade sidor) eftersom den innehåller grundläggande terminologi och begrepp, tillsammans med information om hur du skapar och hanterar fragment och levererar strukturerade innehållsfragment till andra kanaler än AEM sidor.

>[!NOTE]
>
>Innehållsfragment är en **webbplatsfunktion**, men lagras som **Assets**.
>
>De hanteras nu primärt med konsolen **[Innehållsfragment](/help/sites-cloud/administering/content-fragments/managing.md#content-fragments-console)**, men de kan fortfarande hanteras från konsolen **[Assets](/help/assets/content-fragments/content-fragments-managing.md)**.
>
>Det finns två redigerare för att skapa innehållsfragment:
>
>* Den nya redigeraren för [innehållsfragment - redigering](/help/sites-cloud/administering/content-fragments/authoring.md), nås primärt från konsolen **Innehållsfragment**.
>* Den [ursprungliga redigeraren](/help/assets/content-fragments/content-fragments-variations.md) är primärt åtkomlig från **Assets**-konsolen.

>[!NOTE]
>
>**Innehållsfragment** och **[Upplevelsefragment](/help/sites-cloud/authoring/fragments/content-fragments.md)** är olika funktioner i AEM:
>* **Innehållsfragment** är redaktionellt innehåll, med definition och struktur, men utan ytterligare visuell design och/eller layout. De kan användas för att få tillgång till strukturerade data, bland annat texter, siffror och datum.
>* **Upplevelsefragment** är helt utformat för innehåll, ett fragment av en webbsida.
>
>Upplevelsefragment kan innehålla innehåll i form av innehållsfragment, men inte tvärtom.
>
>Mer information finns i [Om innehållsfragment och upplevelsefragment i AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/content-fragments/understand-content-fragments-and-experience-fragments.html#content-fragments).

Innehållsfragmenten aktiverar:

* **Marknadsföring och kampanjstrategi**
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
2. Lägg till komponenten **Innehållsfragment**, antingen från webbläsaren **Komponenter** eller från **Infoga ny komponent**.
3. Du kan antingen:
   * Öppna webbläsaren **Assets** och filtrera efter **Innehållsfragment** (standardvärdet är Bilder). Dra sedan det önskade fragmentet till komponentinstansen.
   * Markera innehållskomponenten och **Konfigurera** i verktygsfältet. I dialogrutan kan du öppna urvalsdialogrutan för att bläddra och välja önskat **innehållsfragment**.

   >[!NOTE]
   >
   >Ett annat sätt är att dra ett visst innehållsfragment direkt till sidan. Då skapas automatiskt den associerade komponenten (innehållsfragment).

4. Till att börja med visas innehållet från elementet **Main** och **Master** (variation). Du kan [markera andra element och/eller variationer](#selecting-the-element-or-variation) efter behov.

   ![Innehållsfragment i Assets-webbläsaren](/help/sites-cloud/authoring/assets/content-fragments.png)

   >[!NOTE]
   >
   >Mer information om ytterligare redigeringsfunktioner finns även i:
   >
   >* [Responsiv layout](/help/sites-cloud/authoring/page-editor/responsive-layout.md)
   >* [Redigera sidinnehåll](/help/sites-cloud/authoring/page-editor/edit-content.md)

### Markera elementet eller variationen {#selecting-the-element-or-variation}

Öppna fragmentets dialogruta **Konfiguration** för att konfigurera fragmentet för användning på den aktuella sidan. Dialogrutan kan vara beroende av vilken komponent som används.

>[!NOTE]
>
>Se även [kärnkomponenter, komponenten Content Fragment](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html)

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
   * Standardmallen **Master** är alltid tillgänglig.
   * En markering är tillgänglig om variationer har skapats för fragmentet.

* **ID**

   * **HTML ID**-attribut som ska användas för komponenten.

### Snabb anslutning till Fragment Editor {#quick-connection-to-fragment-editor}

Du kan öppna fragmentkällan för redigering (resursen) med ikonen **Redigera** i komponentverktygsfältet. På så sätt kan du [redigera och hantera innehållsfragmentet](/help/sites-cloud/administering/content-fragments/overview.md).

>[!CAUTION]
>
>Som alltid kommer redigering av fragmentkällan att påverka alla sidor som refererar till det innehållsfragmentet.

### Lägga till mellaninnehåll {#adding-in-between-content}

När ett visst innehållsfragment läggs till på sidan finns det en **Drag-komponent här** mellan varje HTML-stycke (och längst upp/längst ned) i fragmentet.

Detta gör att du kan lägga till extra innehåll [däremellan (det vill säga mellanliggande innehåll)](/help/assets/content-fragments/content-fragments.md#in-between-content-when-page-authoring-with-content-fragments) i fragmentinnehållet (vid någon av de tillgängliga punkterna), utan att behöva ändra rotfragmentet.

För mellanliggande innehåll kan du:

* Lägg till komponenter från [komponentwebbläsaren.](/help/sites-cloud/authoring/page-editor/editor-side-panel.md#components-browser)
* Lägg till resurser från webbläsaren [Assets.](/help/sites-cloud/authoring/page-editor/editor-side-panel.md#assets-browser)
* Använd [Associerat innehåll](#using-associated-content) som källa för mellanliggande innehåll.

>[!CAUTION]
>
>Det mellanliggande innehållet är sidinnehåll. Den lagras inte i innehållsfragmentet.

![Infoga komponent](/help/sites-cloud/authoring/assets/content-fragments-insert.png)

>[!NOTE]
>
>Du kan också [infoga visuella resurser (bilder) i själva fragmentet](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment).
>
>Visuella resurser som infogats i själva fragmentet kopplas till föregående stycke i fragmentet. Det innebär att du inte kan placera innehåll mellan en visuell resurs och föregående stycke. Om du behöver den här anslutningsnivån kan du lägga till bilden i fragmentet (som ett [blandat mediefragment](/help/assets/content-fragments/content-fragments.md#fragments-with-visual-assets)).

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

Om du har [associerat innehåll](/help/assets/content-fragments/content-fragments-assoc-content.md) med [innehållsfragmentet](/help/assets/content-fragments/content-fragments.md) är dessa resurser tillgängliga från sidopanelen (efter att du har placerat fragmentet på innehållssidan). Associerat innehåll är i själva verket en särskild innehållskälla för [det mellanliggande innehållet](/help/assets/content-fragments/content-fragments.md#in-between-content-when-page-authoring-with-content-fragments).

>[!NOTE]
>
>Det finns olika metoder för att lägga till [visuella resurser (till exempel bilder)](/help/assets/content-fragments/content-fragments.md#fragments-with-visual-assets) till avsnittet och/eller sidan.

>[!NOTE]
>
>Om du har flera innehållsfragment på en sida visar fliken **Associerat innehåll** resurser som passar alla fragment.

När du har lagt till ett fragment med associerat innehåll på sidan öppnas en ny flik (**Associerat innehåll**) på sidopanelen.

Här kan du dra resurserna till önskad plats (antingen till en befintlig komponent eller till önskad plats där rätt komponent skapas):

![Infoga en bild](/help/sites-cloud/authoring/assets/content-fragments-image.png)

### Assets infogat i fragmentet {#assets-inserted-into-the-fragment}

Om resurser (till exempel bilder) har infogats i själva fragmentet (som [blandade mediefragment](/help/assets/content-fragments/content-fragments.md#fragments-with-visual-assets)) är alternativen för att redigera dessa resurser i sidredigeraren begränsade.

För en bild kan du till exempel

* Beskär, rotera eller vänd bilden.
* Lägg till en titel eller alternativ text.
* Ange en storlek.
* Du kan också konfigurera layouten.

Andra ändringar, som att flytta, kopiera och ta bort, måste göras i fragmentredigeraren.

### Publicering {#publishing}

Fragment måste publiceras så att de kan användas på dina publicerade webbsidor:

* Ett fragment kan publiceras när [fragmentet har skapats i konsolen för innehållsfragment](/help/sites-cloud/administering/content-fragments/managing.md#publishing-and-previewing-a-fragment).
* Om ett *opublicerat fragment* används på en sida som publiceras, kan fragmentet även publiceras just nu.

## Exportera innehållsfragment {#exporting-content-fragments}

Vid export till Adobe Target kan JSON användas för att leverera fragmentet. Se:

* [Integrera med Adobe Target](/help/sites-cloud/integrating/integrating-adobe-target.md)
* [Exportera innehållsfragment till Adobe Target](/help/sites-cloud/integrating/content-fragments-target.md)

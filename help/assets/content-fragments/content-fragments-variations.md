---
title: Variationer - innehåll i redigeringsfragment (Assets - innehållsfragment)
description: Förstå hur varianter av innehållsfragment gör att du kan skapa innehåll för fragmentet och sedan skapa variationer av innehållet utifrån syfte, vilket ökar flexibiliteten.
exl-id: af05aae6-d535-4007-ba81-7f41213ff152
feature: Content Fragments
role: User
solution: Experience Manager Sites
source-git-commit: 8dc6874f3f8833ef67a4fa93d2a830fa8485b593
workflow-type: tm+mt
source-wordcount: '2530'
ht-degree: 4%

---

# Variationer - innehåll för redigeringsfragment{#variations-authoring-fragment-content}

[Variationer](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) är en viktig funktion i innehållsfragment i Adobe Experience Manager (AEM) as a Cloud Service. Detta beror på att du kan skapa och redigera kopior av **mallinnehållet** för användning i vissa kanaler och scenarier. Detta gör i synnerhet innehållsleverans utan motstycke ännu flexiblare.

>[!NOTE]
>
>Innehållsfragment är en webbplatsfunktion, men lagras som **Assets**.
>
>Det finns två redigerare för att skapa innehållsfragment - den nya redigeraren och den ursprungliga redigeraren. Den nya redigeraren är standard. Även om de grundläggande funktionerna är desamma finns det vissa skillnader.
>
>I det här avsnittet beskrivs den ursprungliga redigeraren. Det här är [öppnat via den nya redigeraren](/help/assets/content-fragments/content-fragments-managing.md#opening-the-fragment-editor).
>
>Mer information om den nya redigeraren finns i webbplatsdokumentationen [Innehållsfragment - redigering](/help/sites-cloud/administering/content-fragments/authoring.md).

På fliken **Variationer** kan du göra följande:

* [Ange innehållet](#authoring-your-content) för ditt fragment,
* [Skapa och hantera variationer](#managing-variations) av **mallinnehållet**,

Utför en mängd andra åtgärder beroende på vilken datatyp som redigeras, till exempel:

* [Infoga visuella resurser i fragmentet](#inserting-assets-into-your-fragment) (bilder)

* Välj mellan [RTF](#rich-text), [Oformaterad text](#plain-text) och [Markering](#markdown) för redigering

* [Överför innehåll](#uploading-content)

* [Visa nyckelstatistik](#viewing-key-statistics) (om flerradig text)

* [Sammanfatta text](#summarizing-text)

* [Synkronisera varianter med mallinnehåll](#synchronizing-with-master)

>[!CAUTION]
>
>När ett fragment har publicerats och/eller refererats visas en varning i AEM när en författare öppnar fragmentet för redigering igen. Detta för att varna för att ändringar i fragmentet även påverkar de refererade sidorna.

## Redigera ditt innehåll {#authoring-your-content}

När du öppnar ditt innehållsfragment för redigering i den ursprungliga redigeraren är fliken **Variationer** öppen som standard. Här kan du skapa innehållet, för mallsidor eller andra varianter som du har. Det strukturerade fragmentet innehåller fält med olika datatyper som har definierats i innehållsmodellen.

Till exempel:

![helskärmsredigerare](assets/cfm-variations-02.png)

Du kan:

* Redigera ditt innehåll direkt på fliken **Variationer**. Varje datatyp innehåller olika redigeringsalternativ, till exempel:

   * när den är konfigurerad (som flera) i modellen tillåter olika datatyper dig att **lägga till** instanser av det relevanta fältet

   * för **Flerradiga textfält** kan du även öppna [helskärmsredigeraren](#full-screen-editor) för att:

      * välj [Format](#formats)
      * se fler redigeringsalternativ (för formatet [RTF](#rich-text))
      * få åtkomst till ett intervall med [åtgärder](#actions)

   * För **fragmentreferensfält** kan alternativet [Redigera innehållsfragment](#fragment-references-edit-content-fragment) vara tillgängligt, beroende på modelldefinitionen.

* Tilldela **taggar** till den aktuella varianten. Du kan lägga till, uppdatera och ta bort taggarna.

   * [Taggar](/help/sites-cloud/authoring/sites-console/tags.md) är kraftfulla när du organiserar dina fragment eftersom de kan användas för innehållsklassificering och taxonomi. Taggar kan användas för att söka efter innehåll (efter taggar) och tillämpa gruppåtgärder.

      * Sökningar efter en tagg returnerar fragmentet, med taggvariationen markerad.
      * Variationstaggar kan också användas för att gruppera variationer för en viss CDN-profil (Content Delivery Network) (för CDN-cache) i stället för att använda variantnamnet.

     Du kan till exempel tagga relevanta fragment som&quot;Julstart&quot; så att du bara kan bläddra bland dem som en delmängd, eller kopiera dem för användning med en annan framtida start i en ny mapp.

  >[!NOTE]
  >
  >**Taggar** kan också läggas till (i varianten **Master**) som en del av [Metadata](/help/assets/content-fragments/content-fragments-metadata.md)

* [Skapa och hantera varianter](#managing-variations) av **mallinnehållet**.

>[!NOTE]
>
>Beroende på definitioner i den underliggande modellen kan fälten omfattas av vissa typer av [validering](/help/assets/content-fragments/content-fragments-models.md#validation).

### Helskärmsredigerare {#full-screen-editor}

När du redigerar ett textfält med flera rader kan du öppna redigeraren i helskärmsläge. Markera i själva texten och välj sedan följande åtgärdsikon:

![redigeringsikon för helskärm](assets/cfm-variations-03.png)

Då öppnas textredigeraren i helskärmsläge:

![helskärmsredigerare](assets/cfm-variations-fullscreentexteditor.png)

Textredigeraren i helskärmsläge innehåller följande:

* Åtkomst till olika [åtgärder](#actions)
* Beroende på [format](#formats) kan ytterligare formateringsalternativ användas ([RTF](#rich-text))

### Åtgärder {#actions}

Följande åtgärder är också tillgängliga (för alla [format](#formats)) när helskärmsredigeraren (d.v.s. flerradig text) är öppen:

* Välj [format](#formats) ([RTF](#rich-text), [Oformaterad text](#plain-text), [Markdown](#markdown))

* [Överför innehåll](#uploading-content)

* [Visa textstatistik](#viewing-key-statistics)

* [Synkronisera med mallsida](#synchronizing-with-master) (när du redigerar en variant)

* [Sammanfatta text](#summarizing-text)

### Format {#formats}

Vilka alternativ du kan använda för att redigera text med flera rader beror på vilket format du har valt:

* [RTF](#rich-text)
* [Oformaterad text](#plain-text)
* [Markering](#markdown)

Formatet kan väljas när helskärmsredigeraren används.

### RTF {#rich-text}

Med textredigering kan du formatera:

* Fet
* Kursiv
* Understruken
* Justering: vänster, mitten, höger
* Punktlista
* Numrerad lista
* Indrag: öka, minska
* Skapa/bryt hyperlänkar
* Klistra in text/text från Word
* Infoga en tabell
* Styckeformat: Stycke, Rubrik 1/2/3
* [Infoga resurs](#inserting-assets-into-your-fragment)
* Öppna helskärmsredigeraren, där följande formateringsalternativ är tillgängliga:
   * Sök
   * Sök/ersätt
   * Stavningskontroll
   * [Anteckningar](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment)
* [Infoga innehållsfragment](#inserting-content-fragment-into-your-fragment); tillgängligt när fältet **Flerradig text** har konfigurerats med **Tillåt fragmentreferens**.

[åtgärderna](#actions) är även tillgängliga från helskärmsredigeraren.

### Oformaterad text {#plain-text}

Med oformaterad text kan du snabbt lägga in innehåll utan formaterings- eller markeringsinformation. Du kan även öppna helskärmsredigeraren för ytterligare [åtgärder](#actions).

>[!CAUTION]
>
>Om du väljer **Oformaterad text** kan du förlora formatering, markeringar eller resurser som du infogat i antingen **RTF** eller **Markdown**.

### Markering {#markdown}

>[!NOTE]
>
>Mer information finns i dokumentationen för [Markdown](/help/assets/content-fragments/content-fragments-markdown.md).

På så sätt kan du formatera texten med hjälp av markeringar. Du kan definiera:

* Rubriker
* Stycken och radbrytningar
* Länkar
* Bilder
* Blockcitat
* Listor
* Betoning
* Kodblock
* Backslash Escapes

Du kan även öppna helskärmsredigeraren för ytterligare [åtgärder](#actions).

>[!CAUTION]
>
>Om du växlar mellan **RTF** och **Markdown-kod** kan du få oväntade effekter med Blockcitattecken och Kodblock, eftersom dessa båda format kan hanteras på olika sätt.

### Fragmentreferenser {#fragment-references}

Om innehållsfragmentmodellen innehåller fragmentreferenser kan fragmentförfattarna ha ytterligare alternativ:

* [Redigera innehållsfragment](#fragment-references-edit-content-fragment)
* [Nytt innehållsfragment](#fragment-references-new-content-fragment)

![Fragmentreferenser](assets/cfm-variations-12.png)

#### Redigera innehållsfragment {#fragment-references-edit-content-fragment}

Alternativet **Redigera innehållsfragment** öppnar det fragmentet på en ny redigeringsflik (på samma webbläsarflik).

Om du väljer den ursprungliga fliken igen (till exempel **Little Pony Inc.**) stängs den sekundära fliken (i det här fallet **Adam Smith**).

![Fragmentreferenser](assets/cfm-variations-editreference.png)

#### Nytt innehållsfragment {#fragment-references-new-content-fragment}

Med alternativet **Nytt innehållsfragment** kan du skapa ett fragment. För att uppnå detta öppnas en variant av guiden Skapa innehållsfragment i redigeraren.

**Så här skapar du ett innehållsfragment:**

1. Navigera till och markera önskad mapp.
1. Markerar **Nästa**.
1. Ange egenskaper, till exempel **Titel**.
1. Markerar **Skapa**.
1. Äntligen:
   1. **Klar**:
      * returnerar (till det ursprungliga fragmentet)
      * refererar till det nya fragmentet
   1. **Öppna**:
      * refererar till det nya fragmentet
      * öppnar det nya avsnittet för redigering på en ny flik i webbläsaren

### Visa nyckelstatistik {#viewing-key-statistics}

När helskärmsredigeraren är öppen visar åtgärden **Textstatistik** en rad information om texten.

Till exempel:

![statistik](assets/cfm-variations-04.png)

### Överför innehåll {#uploading-content}

Om du vill förenkla redigeringen av innehållsfragment kan du överföra text, som har förberetts i en extern redigerare och lägga till den direkt i fragmentet.

### Sammanfatta text {#summarizing-text}

Att sammanfatta text är utformat för att hjälpa användare att minska längden på texten till ett fördefinierat antal ord, samtidigt som man behåller huvudpunkterna och den övergripande innebörden.

>[!NOTE]
>
>På en mer teknisk nivå behåller systemet meningarna som det klassificerar som om de ger det *bästa förhållandet mellan informationstäthet och unikhet* enligt specifika algoritmer.

>[!CAUTION]
>
>Innehållsfragmentet måste ha en giltig språkmapp (ISO-kod) som överordnad. Detta används för att avgöra vilken språkmodell som ska användas.
>
>Till exempel `en/` som i följande sökväg:
>
>  `/content/dam/my-brand/en/path-down/my-content-fragment`

>[!CAUTION]
>
>Engelska finns i körklart skick.
>
>Andra språk är tillgängliga som språkmodellpaket från programvarudistribution:
>
>* [Franska (fr)](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-fr)
>* [Tyska (de)](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-de)
>* [Italienska (it)](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-it)
>* [Spanska (es)](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-es)
>

1. Välj **mallsida** eller önskad variant.
1. Öppna fullskärmsredigeraren.

1. Välj **Sammanfatta text** i verktygsfältet.

   ![sammanfattning](assets/cfm-variations-05.png)

1. Ange målantalet ord och välj **Start**:
1. Den ursprungliga texten visas sida vid sida med den föreslagna sammanfattningen:

   * Alla meningar som ska tas bort markeras med rött, med genomstrykning.
   * Klicka på en markerad mening så att du kan behålla den i det sammanfattande innehållet.
   * Klicka på en mening som inte är markerad så att den kan tas bort.

1. Markera **Sammanfatta** för att bekräfta ändringarna.

1. Den ursprungliga texten visas sida vid sida med den föreslagna sammanfattningen:

   * Alla meningar som ska tas bort markeras med rött, med genomstrykning.
   * Klicka på en markerad mening så att du kan behålla den i det sammanfattande innehållet.
   * Klicka på en mening som inte är markerad så att den kan tas bort.
   * Sammanfattningsstatistiken visas: **Faktiskt** och **Mål**-
   * Du kan **förhandsgranska** ändringarna.

   ![summeringsjämförelse](assets/cfm-variations-06.png)

### Anteckna ett innehållsfragment {#annotating-a-content-fragment}

Så här kommenterar du ett fragment:

1. Välj **mallsida** eller önskad variant.

1. Öppna fullskärmsredigeraren.

1. Ikonen **Anteckning** är tillgänglig i det övre verktygsfältet. Du kan markera text om det behövs.

   ![anteckna](assets/cfm-variations-07.png)

1. En dialogruta öppnas. Här kan du ange din anteckning.

   ![anteckna](assets/cfm-variations-07a.png)

1. Välj **Använd** i dialogrutan.

   ![anteckna](assets/cfm-variations-annotations-apply-icon.png)

   Om anteckningen tillämpades på den markerade texten förblir den texten markerad.

   ![anteckna](assets/cfm-variations-07b.png)

1. Stäng helskärmsredigeraren, anteckningarna är fortfarande markerade. Om du väljer det här alternativet öppnas en dialogruta så att du kan redigera anteckningen ytterligare.

1. Välj **Spara**.

1. Stäng helskärmsredigeraren, anteckningarna är fortfarande markerade. Om du väljer det här alternativet öppnas en dialogruta så att du kan redigera anteckningen ytterligare.

   ![anteckna](assets/cfm-variations-07c.png)

>[!NOTE]
>
>Anteckningsfunktionen visar inte kommentarer som har angetts i den nya [innehållsfragmentsredigeraren](/help/sites-cloud/administering/content-fragments/authoring.md#commenting-on-your-fragment).

### Visa, redigera, ta bort anteckningar {#viewing-editing-deleting-annotations}

Anteckningar:

* De indikeras av markeringen på texten, både i helskärmsläge och normalt läge i redigeraren. Du kan sedan visa, redigera och/eller ta bort all information i en anteckning genom att klicka på den markerade texten, som öppnar dialogrutan igen.

  >[!NOTE]
  >
  >En nedrullningsbar väljare tillhandahålls om flera anteckningar har tillämpats på ett textstycke.

* När du tar bort hela texten som kommentaren användes på tas även anteckningen bort.

* Den kan listas och tas bort genom att välja fliken **Anteckningar** i fragmentredigeraren.

  ![anteckningar](assets/cfm-variations-08.png)

* Den kan visas och tas bort på [tidslinjen](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments) för det valda fragmentet.

### Infoga Assets i fragment {#inserting-assets-into-your-fragment}

Om du vill skapa innehållsfragment enklare kan du lägga till [Assets](/help/assets/manage-digital-assets.md) (bilder) direkt i fragmentet.

De läggs till i fragmentets styckesekvens utan formatering. Formatering kan göras när [fragmentet används/refereras på en sida](/help/sites-cloud/authoring/fragments/content-fragments.md).

>[!CAUTION]
>
>Dessa resurser kan inte flyttas eller tas bort på en referenssida. Detta måste göras i fragmentredigeraren.
>
>Formatering av resursen (till exempel storlek) måste dock göras i [sidredigeraren](/help/sites-cloud/authoring/fragments/content-fragments.md). Representationen av resursen i fragmentredigeraren är endast avsedd för redigering av innehållsflödet.

>[!NOTE]
>
>Det finns olika metoder för att lägga till [bilder](/help/assets/content-fragments/content-fragments.md#fragments-with-visual-assets) i fragmentet och/eller på sidan.

1. Placera markören där du vill lägga till bilden.
1. Använd ikonen **Infoga resurs** för att öppna sökdialogrutan.

   ![Infoga resursikon](assets/cfm-variations-09.png)

1. I dialogrutan kan du antingen navigera till den önskade resursen i DAM eller söka efter resursen i DAM.

   Välj önskad resurs genom att klicka på miniatyrbilden.

1. Använd **Välj** för att lägga till resursen i innehållsfragmentets styckesystem på den aktuella platsen.

   >[!CAUTION]
   >
   >När du har lagt till en resurs, om du ändrar formatet till:
   >
   >* **Oformaterad text**: resursen förloras från fragmentet.
   >* **Markering**: Resursen är inte synlig, men finns fortfarande kvar när du återgår till **RTF**.

### Infoga ett innehållsfragment i fragmentet {#inserting-content-fragment-into-your-fragment}

Om du vill skapa innehållsfragment enklare kan du även lägga till ytterligare ett innehållsfragment i fragmentet.

De läggs till som en referens på den aktuella platsen i fragmentet.

>[!NOTE]
>
>Det här alternativet är tillgängligt när **Flerradig text** har konfigurerats med **Tillåt fragmentreferens**.

>[!CAUTION]
>
>Dessa resurser kan inte flyttas eller tas bort på en referenssida. Detta måste göras i fragmentredigeraren.
>
>Formatering av resursen (till exempel storlek) måste dock göras i [sidredigeraren](/help/sites-cloud/authoring/fragments/content-fragments.md). Representationen av resursen i fragmentredigeraren är endast avsedd för redigering av innehållsflödet.

>[!NOTE]
>
>Det finns olika metoder för att lägga till [bilder](/help/assets/content-fragments/content-fragments.md#fragments-with-visual-assets) i fragmentet och/eller på sidan.

1. Placera markören där du vill lägga till fragmentet.
1. Använd ikonen **Infoga innehållsfragment** för att öppna sökdialogrutan.

   ![ikonen Infoga innehållsfragment](assets/cfm-variations-13.png)

1. I dialogrutan kan du antingen navigera till det önskade fragmentet i Assets-mappen eller söka efter fragmentet.

   Välj önskat fragment när du är placerad genom att klicka på miniatyrbilden.

1. Använd **Välj** om du vill lägga till en referens till det markerade innehållsfragmentet i det aktuella innehållsfragmentet (på den aktuella platsen).

   >[!CAUTION]
   >
   >När du har lagt till en referens till ett annat fragment kan du ändra formatet till:
   >
   >* **Oformaterad text**: referensen förloras från fragmentet.
   >* **Markering**: referensen återstår.

## Arv {#inheritance}

Arv är den mekanism där innehåll automatiskt kan överföras från ett fragment till ett annat. Ärvda fält och varianter kan vara produkten av [Multi-Site Management](/help/assets/content-fragments/content-fragments-msm.md).

Du kan avbryta (och sedan återaktivera) arvet. Beroende på sammanhanget kan detta vara tillgängligt för en variation, eller ett enskilt fält, om fragmentet är en del av en live-kopia.

![Ett innehållsfragment som visar arvsrelation](/help/assets/content-fragments/assets/cfm-variations-inheritance.png)

Till exempel:

* Avbryt arv

  ![Knappen Avbryt arv](/help/assets/content-fragments/assets/editing-cancel-inheritance.png)

* Återaktivera arv (om arv redan har avbrutits)

  ![Återaktivera arvsknappen](/help/assets/content-fragments/assets/editing-reenable-inheritance.png)

<!--
* Rollout action is also available in Live Copy source

  ![Rollout button](/help/assets/content-fragments/assets/editing-rollout.png)
-->

## Hantera variationer {#managing-variations}

### Skapa en variant {#creating-a-variation}

Med variationer kan du ta **mallinnehållet** och ändra det efter syfte (om det behövs).

**Så här skapar du en variant:**

1. Öppna fragmentet och se till att sidopanelen är synlig.
1. Välj **Variationer** i ikonfältet på sidpanelen.
1. Välj **Skapa variant**.
1. En dialogruta öppnas så att du kan ange **Rubrik** och **Beskrivning** för den nya varianten.
1. Välj **Lägg till**. Fragmentet **Mallen** kopieras till den nya varianten som nu är öppen för [redigering](#editing-a-variation).

   >[!NOTE]
   >
   >När du skapar en variant är det alltid **mallsidan** som kopieras, inte varianten som är öppen.

   >[!NOTE]
   >
   >När du skapar en variant kopieras alla **taggar** som för närvarande är tilldelade **mallvarianten** till den nya varianten.

### Redigera en variant {#editing-a-variation}

Du kan ändra variantinnehållet efter antingen:

* [Skapar din variation](#creating-a-variation).
* Öppna ett befintligt fragment och välj sedan önskad variation på sidopanelen.

![redigera en variation](assets/cfm-variations-10.png)

### Byta namn på en variant {#renaming-a-variation}

1. Öppna fragmentet och välj **Variationer** på sidpanelen.
1. Välj önskad variant.
1. Välj **Byt namn** i listrutan **Åtgärder**.

1. Ange den nya **titeln** och/eller **beskrivningen** i dialogrutan som visas.

1. Bekräfta åtgärden **Byt namn**.

>[!NOTE]
>
>Detta påverkar bara variationen **Rubrik**.

### Ta bort en variant {#deleting-a-variation}

1. Öppna fragmentet och välj **Variationer** på sidpanelen.
1. Välj önskad variant.
1. Välj **Ta bort** i listrutan **Åtgärder**.

1. Bekräfta åtgärden **Ta bort** i dialogrutan.

>[!NOTE]
>
>Du kan inte ta bort **mallsida**.

### Synkroniserar med mallsida {#synchronizing-with-master}

**Master** är en del av ett innehållsfragment och, per definition, att det innehåller huvudkopian av innehållet. Variationer håller de individuella uppdaterade och skräddarsydda versionerna av det innehållet. När mallsidan uppdateras är det möjligt att dessa ändringar också är relevanta för variationerna och därför måste spridas till dem.

När du redigerar en variant har du tillgång till åtgärden för att synkronisera det aktuella elementet i variationen med mallsidan. På så sätt kan du automatiskt kopiera ändringar som gjorts i mallsidan till önskad variant.

>[!CAUTION]
>
>Synkronisering är bara tillgängligt för att kopiera ändringar *från **mastern**till varianten*.
>
>Endast varianternas aktuella element synkroniseras.
>
>Synkronisering fungerar bara för datatypen **Flerradig text**.
>
>Du kan inte överföra ändringar *från en variant till **mastern***.

1. Öppna ditt innehållsfragment i fragmentredigeraren. Kontrollera att **mallsidan** har redigerats.

1. Välj en specifik variant och sedan lämplig synkroniseringsåtgärd från antingen:

   * den nedrullningsbara menyn **Åtgärder** - **Synkronisera aktuellt element med mallsida**

     ![synkroniserar med mallsida](assets/cfm-variations-11a.png)

   * verktygsfältet i fullskärmsredigeraren - **Synkronisera med mallsida**

     ![synkroniserar med mallsida](assets/cfm-variations-11b.png)

1. Mallen och variationen visas sida vid sida:

   * grönt anger att innehållet har lagts till (i varianten)
   * rött anger att innehållet har tagits bort (från varianten)
   * blå anger ersatt text

   ![synkroniserar med mallsida](assets/cfm-variations-11c.png)

1. Välj **Synkronisera**. Variationen uppdateras och visas.

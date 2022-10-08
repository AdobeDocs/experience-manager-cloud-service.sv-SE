---
title: Variationer - innehåll i redigeringsfragment (resurser - innehållsfragment)
description: Förstå hur variationer kan göra ert headless-innehåll i AEM ännu mer flexibelt genom att du kan skapa innehåll för fragmentet och sedan skapa variationer av innehållet utifrån syfte.
exl-id: af05aae6-d535-4007-ba81-7f41213ff152
source-git-commit: d720d403cab4e51dd89a58aae5b4e29ca9da7f1c
workflow-type: tm+mt
source-wordcount: '2288'
ht-degree: 11%

---

# Variationer – redigera innehållsfragment{#variations-authoring-fragment-content}

[Variationer](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) är en viktig egenskap hos AEM innehållsfragment, eftersom de gör det möjligt att skapa och redigera kopior av det överordnad innehållet för användning i specifika kanaler och/eller scenarier, vilket gör headless content delivery ännu flexiblare.

Från **Variationer** -flik:

* [Ange innehållet](#authoring-your-content) för ditt fragment,
* [Skapa och hantera variationer](#managing-variations) i **Överordnad** innehåll,

Utför en rad andra åtgärder beroende på vilken datatyp som redigeras. till exempel:

* [Infoga visuella resurser i fragmentet](#inserting-assets-into-your-fragment) (bilder)

* Välj mellan [RTF](#rich-text), [Oformaterad text](#plain-text) och [Markering](#markdown) för redigering

* [Överför innehåll](#uploading-content)

* [Visa nyckelstatistik](#viewing-key-statistics) (om text med flera rader)

* [Sammanfatta text](#summarizing-text)

* [Synkronisera varianter med Överordnad innehåll](#synchronizing-with-master)

>[!CAUTION]
>
>När ett fragment har publicerats och/eller refererats visar AEM en varning när en författare öppnar fragmentet för redigering igen. Detta är för att varna för att ändringar i avsnittet även påverkar de refererade sidorna.

## Redigera ditt innehåll {#authoring-your-content}

När du öppnar ditt innehållsfragment för redigering visas **Variationer** som standard är fliken öppen. Här kan du skapa innehåll, för Överordnad eller andra varianter som du har. Det strukturerade fragmentet innehåller olika fält, av olika datatyper, som har definierats i innehållsmodellen.

Till exempel:

![helskärmsredigerare](assets/cfm-variations-02.png)
Du kan:

* gör redigeringar direkt i **Variationer** tab

   * varje datatyp har olika redigeringsalternativ

* for **Flerradstext** fält som du också kan öppna [helskärmsredigerare](#full-screen-editor) till:

   * välj [Format](#formats)
   * se fler redigeringsalternativ (för [RTF](#rich-text) format)
   * få tillgång till ett antal [funktionsmakron](#actions)

* För **Fragmentreferens** fälten **[Redigera innehållsfragment](#fragment-references-edit-content-fragment)** kan vara tillgängligt, beroende på modelldefinitionen.

### Helskärmsredigerare {#full-screen-editor}

När du redigerar ett textfält med flera rader kan du öppna redigeraren i helskärmsläge; tryck eller klicka i den faktiska texten och välj sedan följande åtgärdsikon:

![redigeringsikon för helskärm](assets/cfm-variations-03.png)

Då öppnas textredigeraren i helskärmsläge:

![helskärmsredigerare](assets/cfm-variations-fullscreentexteditor.png)

Textredigeraren i helskärmsläge innehåller:

* Åtkomst till olika [funktionsmakron](#actions)
* Beroende på [format](#formats), ytterligare formateringsalternativ ([RTF](#rich-text))

### Åtgärder {#actions}

Följande åtgärder är också tillgängliga (för alla [format](#formats)) när helskärmsredigeraren (d.v.s. text med flera rader) är öppen:

* Välj [format](#formats) ([RTF](#rich-text), [Oformaterad text,](#plain-text) [Markering](#markdown))

* [Överför innehåll](#uploading-content)

* [Visa textstatistik](#viewing-key-statistics)

* [Synkronisera med Överordnad](#synchronizing-with-master) (när du redigerar en variant)

* [Sammanfatta text](#summarizing-text)

### Format {#formats}

Vilka alternativ du kan använda för att redigera text med flera rader beror på vilket format du har valt:

* [RTF-text](#rich-text)
* [Oformaterad text](#plain-text)
* [Markdown](#markdown)

Formatet kan väljas när helskärmsredigeraren används.

### RTF-text {#rich-text}

Med textredigering kan du formatera:

* Fet
* Kursiv
* Understrykning
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
   * Sökning
   * Sök/ersätt
   * Stavningskontroll
   * [Anteckningar](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment)
* [Infoga innehållsfragment](#inserting-content-fragment-into-your-fragment); som är tillgängliga när **Flerradstext** fältet är konfigurerat med **Tillåt fragmentreferens**.

The [funktionsmakron](#actions) kan även användas i helskärmsredigeraren.

### Oformaterad text {#plain-text}

Med oformaterad text kan du snabbt lägga in innehåll utan formaterings- eller markeringsinformation. Du kan även öppna helskärmsredigeraren för ytterligare information [funktionsmakron](#actions).

>[!CAUTION]
>
>Om du väljer **Oformaterad text** kan du förlora formatering, markdown-kod och/eller resurser som du har infogat i **RTF** eller **Markdown-kod**.

### Markering {#markdown}

>[!NOTE]
>
>Mer information finns i [Markering](/help/assets/content-fragments/content-fragments-markdown.md) dokumentation.

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

Du kan även öppna helskärmsredigeraren för ytterligare information [funktionsmakron](#actions).

>[!CAUTION]
>
>Om du växlar mellan **RTF** och **Markdown-kod** kan du få oväntade effekter med Blockcitattecken och Kodblock, eftersom dessa båda format kan hanteras på olika sätt.

### Fragmentreferenser {#fragment-references}

Om innehållsfragmentmodellen innehåller fragmentreferenser kan fragmentförfattarna ha ytterligare alternativ:

* [Redigera innehållsfragment](#fragment-references-edit-content-fragment)
* [Nytt innehållsfragment](#fragment-references-new-content-fragment)

![Fragmentreferenser](assets/cfm-variations-12.png)

#### Redigera innehållsfragment {#fragment-references-edit-content-fragment}

Alternativet **Redigera innehållsfragment** öppnar fragmentet på en ny redigeringsflik (på samma webbläsarflik).

Markera den ursprungliga fliken igen (till exempel **Little Pony Inc.**) kommer att stänga den sekundära fliken (i det här fallet **Adam Smith**).

![Fragmentreferenser](assets/cfm-variations-editreference.png)

#### Nytt innehållsfragment {#fragment-references-new-content-fragment}

Alternativet **Nytt innehållsfragment** kan du skapa ett helt nytt fragment. För att uppnå detta öppnas en variant av guiden Skapa innehållsfragment i redigeraren.

Sedan kan du skapa ett nytt fragment genom att:

1. Navigera till och markera önskad mapp.
1. Markera **Nästa**.
1. Ange egenskaper. till exempel **Titel**.
1. Markera **Skapa**.
1. Äntligen:
   1. **Klar** återgår (till det ursprungliga fragmentet) och refererar till det nya fragmentet.
   1. **Öppna** refererar till det nya fragmentet samt öppnar det nya fragmentet, för redigering, på en ny flik i webbläsaren.

### Visa nyckelstatistik {#viewing-key-statistics}

När helskärmsredigeraren är öppen visar åtgärden **Textstatistik** information om texten.

Till exempel:

![statistik](assets/cfm-variations-04.png)

### Överför innehåll {#uploading-content}

För att underlätta redigeringen av innehållsfragment kan du överföra text, förberedd i en extern redigerare och lägga till den direkt i fragmentet.

### Sammanfatta text {#summarizing-text}

Att sammanfatta text är utformat för att hjälpa användare att minska längden på texten till ett fördefinierat antal ord, samtidigt som man behåller huvudpunkterna och den övergripande innebörden.

>[!NOTE]
>
>På en mer teknisk nivå håller systemet kvar de meningar som det bedömer som att det tillhandahåller *bästa förhållandet mellan informationstäthet och unikhet* enligt specifika algoritmer.

>[!CAUTION]
>
>Innehållsfragmentet måste ha en giltig språkmapp (ISO-kod) som överordnad. används för att fastställa vilken språkmodell som ska användas.
>
>Till exempel: `en/` som i följande sökväg:
>
>  `/content/dam/my-brand/en/path-down/my-content-fragment`

>[!CAUTION]
Engelska finns i körklart skick.
Andra språk är tillgängliga som språkmodellpaket från programvarudistribution:
* [Franska (fr)](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-fr)
* [German (de)](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-de)
* [Italienska (it)](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-it)
* [Spanska (es)](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-es)
>


1. Välj **Överordnad** eller den variation som krävs.
1. Öppna fullskärmsredigeraren.

1. Välj **Sammanfatta text** i verktygsfältet.

   ![sammanfattning](assets/cfm-variations-05.png)

1. Ange målantalet ord och markera **Starta**:
1. Den ursprungliga texten visas sida vid sida med den föreslagna sammanfattningen:

   * Alla meningar som ska tas bort markeras med rött, med genomstrykning.
   * Klicka på en markerad mening om du vill behålla den i det sammanfattande innehållet.
   * Klicka på en mening som inte är markerad för att ta bort den.

1. Välj **Sammanfatta** för att bekräfta ändringarna.

1. Den ursprungliga texten visas sida vid sida med den föreslagna sammanfattningen:

   * Alla meningar som ska tas bort markeras med rött, med genomstrykning.
   * Klicka på en markerad mening om du vill behålla den i det sammanfattande innehållet.
   * Klicka på en mening som inte är markerad för att ta bort den.
   * Sammanfattningsstatistiken visas: **Faktisk** och **Mål**-
   * Du kan **Förhandsgranska** ändringarna.

   ![summeringsjämförelse](assets/cfm-variations-06.png)

### Anteckna ett innehållsfragment {#annotating-a-content-fragment}

Så här kommenterar du ett fragment:

1. Välj **Överordnad** eller den variation som krävs.

1. Öppna fullskärmsredigeraren.

1. The **Anteckna** ikonen är tillgänglig i det övre verktygsfältet. Du kan markera text om det behövs.

   ![anteckna](assets/cfm-variations-07.png)

1. En dialogruta öppnas. Här kan du ange din anteckning.

   ![anteckna](assets/cfm-variations-07a.png)

1. Välj **Använd** i dialogrutan.

   ![anteckna](assets/cfm-variations-annotations-apply-icon.png)

   Om anteckningen tillämpades på den markerade texten förblir den texten markerad.

   ![anteckna](assets/cfm-variations-07b.png)

1. Stäng helskärmsredigeraren, anteckningarna är fortfarande markerade. Om du väljer det här alternativet öppnas en dialogruta där du kan redigera kommentaren ytterligare.

1. Välj **Spara**.

1. Stäng helskärmsredigeraren, anteckningarna är fortfarande markerade. Om du väljer det här alternativet öppnas en dialogruta där du kan redigera kommentaren ytterligare.

   ![anteckna](assets/cfm-variations-07c.png)

### Visa, redigera, ta bort anteckningar {#viewing-editing-deleting-annotations}

Anteckningar:

* Indikeras av markeringen på texten, både i helskärmsläge och i normalt läge i redigeraren. Du kan sedan visa, redigera och/eller ta bort all information i en anteckning genom att klicka på den markerade texten, som öppnar dialogrutan igen.

   >[!NOTE]
   En nedrullningsbar väljare tillhandahålls om flera anteckningar har tillämpats på ett textstycke.

* När du tar bort hela texten som kommentaren användes på tas även anteckningen bort.

* Kan listas och tas bort genom att välja **Anteckningar** i fragmentredigeraren.

   ![anteckningar](assets/cfm-variations-08.png)

* Kan visas, tas bort och visas i [Tidslinje](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments) för det valda fragmentet.

### Infoga resurser i fragment {#inserting-assets-into-your-fragment}

Du kan lägga till [Resurser](/help/assets/manage-digital-assets.md) (bilder) direkt till fragmentet.

De läggs till i fragmentets styckesekvens utan formatering. formatering kan göras när [fragment används/refereras på en sida](/help/sites-cloud/authoring/fundamentals/content-fragments.md).

>[!CAUTION]
Dessa resurser kan inte flyttas eller tas bort på en referenssida. Detta måste göras i fragmentredigeraren.
Formatering av resursen (till exempel storlek) måste dock göras i [sidredigerare](/help/sites-cloud/authoring/fundamentals/content-fragments.md). Representationen av resursen i fragmentredigeraren är endast till för att skapa innehållsflödet.

>[!NOTE]
Det finns olika metoder att lägga till [bilder](/help/assets/content-fragments/content-fragments.md#fragments-with-visual-assets) till fragmentet och/eller sidan.

1. Placera markören på den plats där du vill lägga till bilden.
1. Använd ikonen **Infoga resurs** för att öppna sökdialogrutan.

   ![infoga resursikon](assets/cfm-variations-09.png)

1. I dialogrutan kan du antingen:

   * navigera till den nödvändiga resursen i DAM
   * söka efter resursen i DAM

   Välj önskad resurs genom att klicka på miniatyrbilden.

1. Använd **Välj** för att lägga till resursen i innehållsfragmentets styckesystem på den aktuella platsen.

   >[!CAUTION]
   Om du efter att ha lagt till en resurs ändrar formatet till:
   * **Oformaterad text**: Resursen kommer att förloras helt från fragmentet.
   * **Markdown-kod**: Resursen visas inte, men finns fortfarande kvar när du återgår till **RTF**.


### Infoga ett innehållsfragment i fragmentet {#inserting-content-fragment-into-your-fragment}

Om du vill skapa innehållsfragment enklare kan du även lägga till ytterligare ett innehållsfragment i fragmentet.

De kommer att läggas till som en referens på din aktuella plats i fragmentet.

>[!NOTE]
Det här alternativet är tillgängligt när **Flerradstext** är konfigurerad med **Tillåt fragmentreferens**.

>[!CAUTION]
Dessa resurser kan inte flyttas eller tas bort på en referenssida. Detta måste göras i fragmentredigeraren.
Formatering av resursen (till exempel storlek) måste dock göras i [sidredigerare](/help/sites-cloud/authoring/fundamentals/content-fragments.md). Representationen av resursen i fragmentredigeraren är endast till för att skapa innehållsflödet.

>[!NOTE]
Det finns olika metoder att lägga till [bilder](/help/assets/content-fragments/content-fragments.md#fragments-with-visual-assets) till fragmentet och/eller sidan.

1. Placera markören på den plats där du vill lägga till fragmentet.
1. Använd **Infoga innehållsfragment** -ikonen för att öppna sökdialogrutan.

   ![ikonen Infoga innehållsfragment](assets/cfm-variations-13.png)

1. I dialogrutan kan du antingen:

   * navigera till det nödvändiga fragmentet i resursmappen
   * sök efter fragmentet

   När du har hittat fragmentet väljer du det genom att klicka på miniatyrbilden.

1. Använd **Välj** om du vill lägga till en referens till det markerade innehållsfragmentet i det aktuella innehållsfragmentet (på den aktuella platsen).

   >[!CAUTION]
   Om du efter att ha lagt till en referens till ett annat fragment ändrar formatet till:
   * **Oformaterad text**: referensen tas bort helt från fragmentet.
   * **Markering**: referensen kvarstår.


## Hantera variationer {#managing-variations}

### Skapa en variant {#creating-a-variation}

Med variationer kan du ta **Överordnad** innehållet och variera det beroende på syfte (om det behövs).

Så här skapar du en ny variant:

1. Öppna fragmentet och se till att sidopanelen är synlig.
1. Välj **Variationer** från ikonfältet på sidopanelen.
1. Välj **Skapa variant**.
1. En dialogruta öppnas där du anger **titel** och **beskrivning** för den nya varianten.
1. Välj **Lägg till**. **Fragmentmastern** kopieras till den nya varianten, som nu är öppen för [redigering](#editing-a-variation).

   >[!NOTE]
   När du skapar en ny variant är det alltid **Överordnad** som kopieras, inte varianten som är öppen.

### Redigera en variant {#editing-a-variation}

Du kan ändra variantinnehållet efter antingen:

* [Skapa en variant](#creating-a-variation).
* Öppna ett befintligt fragment och välj sedan önskad variation på sidopanelen.

![redigera en variant](assets/cfm-variations-10.png)

### Byta namn på en variant {#renaming-a-variation}

Så här byter du namn på en befintlig variant:

1. Öppna fragmentet och välj **Variationer** från sidopanelen.
1. Välj önskad variant.
1. Välj **Byt namn** från **Åtgärder** nedrullningsbar meny.

1. Ange den nya **titeln** och/eller **beskrivningen** i dialogrutan som visas.

1. Bekräfta **Byt namn** åtgärd.

>[!NOTE]
Detta påverkar bara variationen **Titel**.

### Ta bort en variant {#deleting-a-variation}

Så här tar du bort en befintlig variant:

1. Öppna fragmentet och välj **Variationer** från sidopanelen.
1. Välj önskad variant.
1. Välj **Ta bort** från **Åtgärder** nedrullningsbar meny.

1. Bekräfta **Ta bort** i dialogrutan.

>[!NOTE]
Du kan inte ta bort **Överordnad**.

### Synkroniserar med Överordnad {#synchronizing-with-master}

**Överordnad** är en integrerad del av ett innehållsfragment och innehåller per definition den överordnad kopian av innehållet, medan varianterna innehåller de individuella uppdaterade och anpassade versionerna av det innehållet. När Överordnad uppdateras är det möjligt att dessa ändringar också är relevanta för variationerna och därför måste spridas till dem.

När du redigerar en variant har du tillgång till åtgärden för att synkronisera det aktuella elementet i variationen med Överordnad. På så sätt kan du automatiskt kopiera ändringar som gjorts Överordnad till den önskade variationen.

>[!CAUTION]
Synkronisering är bara tillgängligt för att kopiera ändringar *från **mastern**till varianten*.
Endast det aktuella elementet i variationen kommer att synkroniseras.
Synkronisering fungerar bara på datatypen **Flerradig text**.
Du kan inte överföra ändringar *från en variant till **mastern***.

1. Öppna ditt innehållsfragment i fragmentredigeraren. Se till att **Överordnad** har redigerats.

1. Välj en specifik variant och sedan lämplig synkroniseringsåtgärd från antingen:

   * den **Åtgärder** nedrullningsbar väljare - **Synkronisera aktuellt element med överordnad**

      ![synkronisera med överordnad](assets/cfm-variations-11a.png)

   * verktygsfältet i fullskärmsredigeraren - **Synkronisera med överordnad**

      ![synkronisera med överordnad](assets/cfm-variations-11b.png)

1. Överordnad och variationen visas sida vid sida:

   * grönt anger innehåll som lagts till (i varianten)
   * rött anger att innehållet har tagits bort (från varianten)
   * blå anger ersatt text

   ![synkronisera med överordnad](assets/cfm-variations-11c.png)

1. Välj **Synkronisera** uppdateras och visas variationen.

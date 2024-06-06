---
title: Bästa tillvägagångssätt för att optimera bildkvaliteten
description: Lär dig de effektivaste strategierna som hjälper dig att optimera kvaliteten på dina bildresurser med Dynamic Media.
contentOwner: Rick Brough
feature: Asset Management
role: User
exl-id: 2efc4a27-01d7-427f-9701-393497314402
source-git-commit: 7820492f462d2b5824e408429332b5adf2e67aab
workflow-type: tm+mt
source-wordcount: '1629'
ht-degree: 0%

---

# Bästa tillvägagångssätt för att optimera bildkvaliteten {#best-practices-for-optimizing-the-quality-of-your-images}

Att optimera bildkvaliteten kan vara en tidskrävande process eftersom många faktorer bidrar till att återge godtagbara resultat. Resultatet är delvis subjektivt eftersom individer upplever olika bildkvalitet. Strukturerade experiment är avgörande.

Adobe Experience Manager innehåller över 100 Dynamic Media-kommandon för att justera och optimera bilder och återge resultat. Följande riktlinjer kan hjälpa dig att effektivisera processen och uppnå goda resultat snabbt med några viktiga kommandon och bästa metoder.

<!-- ADDED THE FOLLOWING TOPIC AS PER CQDOC-21594 -->

## Aktivera Smart Imaging i Dynamic Media {#bp-enable-smart-imaging}

**Smart bildbehandling:**

* Om du aktiverar Smart Imaging i Dynamic Media kan du automatiskt optimera bildformat, storlek och kvalitet baserat på webbläsarens funktioner.
Vill du veta mer? Gå till [Smart bildbehandling](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/dynamicmedia/imaging-faq).
* Den förbättrar bildens prestanda genom att dynamiskt justera dessa parametrar.
* Du kan utvärdera Smart bildbehandling med självutvärderingsverktyget [Ögonblicksbild](https://snapshot.scene7.com/).

**Bildformat:**

* Undvik att använda explicit `fmt=webp` eller `fmt=avif` -kommandon i en URL, såvida det inte är särskilt nödvändigt för ett användningsfall.
* Smart Imaging väljer automatiskt det bästa formatet, vilket ger optimala bandbreddsvinster.

**Standardbeteende:**

* Om inget formatkommando har angetts i URL:en och Smart Imaging inte har aktiverats används JPEG-formatet som standard för bildleverans i Dynamic Media.

Genom att göra välgrundade val i bildformat och aktivera Smart Imaging kan du påverka prestanda och användarupplevelser avsevärt.


<!-- ADDED THE FOLLOWING TOPIC AS PER CQDOC-21594 -->

## Bästa tillvägagångssätt för att välja källbild {#bp-select-source-image}

Viktiga överväganden när du arbetar med källbilder:

* **Källbildformat:**
   * Med förlustfria format som PNG, TIFF och PSD kan du vara säker på att bildkvaliteten förblir hög utan några komprimeringsartefakter.
   * Dessa format bevarar alla ursprungliga data, vilket gör dem idealiska för redigering och vidare bearbetning.
* **Storlek på källbild:**
   * Från och med en högupplöst bild får du mer detaljrikedom och flexibilitet.
   * När bilder måste visas i olika storlekar (till exempel på olika enheter eller skärmupplösningar) ger en större källbild bättre skalning.
   * För bilder som har stöd för zoomning (t.ex. produktfoton) bör du rikta in dig på dimensioner på minst 2 000 pixlar på den längsta sidan.
   * Logotyper och banderoller som inte kräver zoomning kan laddas upp i den största storlek som behövs för deras avsedda användning.

Genom att göra dessa noggranna val på källnivå kan du bidra avsevärt till den övergripande kvaliteten på det visuella innehållet.

<!-- REMOVED TOPIC AS PER CQDOC-21594
## Best practices for image format (`&fmt=`) {#best-practices-for-image-format-fmt}

* JPG or PNG are the best choices to deliver images in good quality and with manageable size and weight.
* If no format command is supplied in the URL, Dynamic Media Image Delivery defaults to JPG for delivery.
* JPG compresses at a ratio of 10:1 and usually produces smaller image file sizes. PNG compresses at a ratio of about 2:1, except when images contain a white background. Typically though, PNG file sizes are larger than JPG files.
* JPG uses lossy compression, meaning that picture elements (pixels) are dropped during compression. PNG on the other hand uses lossless compression.
* JPG often compresses photographic images with better fidelity than synthetic images with sharp edges and contrast.
* If your images contain transparency, use PNG because JPG does not support transparency.

As a best practice for image format, start with the most common setting `&fmt=JPG`. -->

## Bästa tillvägagångssätt för bildstorlek {#best-practices-for-image-size}

Att minska bildstorleken dynamiskt är en av de vanligaste uppgifterna. Det handlar om att ange storleken och, om så önskas, vilket nedsamplingsläge som används för att nedskala bilden.

* För bildstorlek är det bästa och enklaste sättet att använda `&wid=<value>` och `&hei=<value>,`eller bara `&hei=<value>`. Dessa parametrar ställer automatiskt in bildbredden i enlighet med proportionerna.
* `&resMode=<value>`styr den algoritm som används för nedsampling. Börja med `&resMode=sharp2`. Det här värdet ger den bästa bildkvaliteten. När nedsampling används `value =bilin` är snabbare, leder det ofta till aliasing av artefakter.

Ett tips om hur du kan ändra bildstorlek är att använda `&wid=<value>&hei=<value>&resMode=sharp2` eller `&hei=<value>&resMode=sharp2`

## Bästa tillvägagångssätt för bildskärpa {#best-practices-for-image-sharpening}

Bildskärpa är den mest komplicerade aspekten när det gäller att styra bilder på webbplatsen och var många misstag görs. Ta dig tid att lära dig mer om hur skärpa och oskarp maskning fungerar i Experience Manager genom att titta på följande resurser:

* Rapport om bästa praxis [Adobe Dynamic Media Classic bästa praxis för bildkvalitet och skärpa](/help/assets/dynamic-media/assets/sharpening_images.pdf) gäller även Experience Manager.

* Titta [Använd bildskärpa med Experience Manager - Dynamic Media](https://experienceleague.adobe.com/en/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-image-sharpening-feature-video-use#dynamic-media).

Med Experience Manager kan du öka skärpan i bilder vid intag, vid leverans eller både och. Normalt är det dock bäst att öka skärpan i bilder med bara en metod eller en annan, men inte med båda. Att skärpa bilderna vid leverans, på en URL-adress, ger oftast bäst resultat.

Det finns två metoder för bildskärpa:

* Enkel skärpa ( `&op_sharpen`) - Precis som det skärpefilter som används i Photoshop, tillämpar enkel skärpa den grundläggande skärpan på den slutliga vyn av bilden efter den dynamiska storleksändringen. Den här metoden kan dock inte konfigureras av användaren. Det bästa sättet är att undvika att använda `&op_sharpen` om det inte är nödvändigt.
* Oskarp maskering ( `&op_USM`) - Oskarp maskning är ett skärpefilter som är branschstandard. Det bästa sättet är att göra bilder skarpare med oskarp maskering enligt riktlinjerna nedan. Med Oskarp maskning kan du styra följande tre parametrar:

   * `&op_sharpen=`belopp,radie,tröskelvärde

      * **[!UICONTROL amount]** (0-5, effektens styrka.)
      * **[!UICONTROL radius]** (0-250, bredden på de&quot;skärpelinjer&quot; som ritas runt objektet med skärpa, mätt i pixlar.)

     Tänk på att parametrarnas radie och mängd fungerar mot varandra. Minskad radie kan kompenseras genom att öka beloppet. Med radie får du bättre kontroll eftersom ett lägre värde ökar skärpan endast för kantpixlarna, medan ett högre värde ökar skärpan för ett större antal pixlar.

      * **[!UICONTROL threshold]** (0-255, effektkänslighet.)

     Den här parametern avgör hur annorlunda de pixlar som ska göras skarpare måste vara från det omgivande området innan de betraktas som kantpixlar och filtret gör dem skarpare. The **[!UICONTROL threshold]** kan du undvika att använda för mycket skärpa i områden med liknande färger, som hudtoner. Ett tröskelvärde på 12 ignorerar till exempel små variationer i hudtonens ljusstyrka för att undvika att lägga till&quot;brus&quot;, samtidigt som kantkontrasten läggs till i områden med hög kontrast, till exempel där ögonfransarna möter huden.

     Mer information om hur du ställer in de här tre parametrarna, inklusive de bästa sätten att använda med filtret, finns i följande resurser:

      * Rapport om bästa praxis [Adobe Dynamic Media Classic bästa praxis för bildkvalitet och skärpa](/help/assets/dynamic-media/assets/sharpening_images.pdf) gäller även Experience Manager.

      * Titta [Använd bildskärpa med Experience Manager - Dynamic Media](https://experienceleague.adobe.com/en/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-image-sharpening-feature-video-use#dynamic-media).

      * Med Experience Manager kan du även styra en fjärde parameter: monokrom (0,1). Den här parametern avgör om oskarp maskning används separat på varje färgkomponent med värdet 0 eller på bildens intensitet/intensitet med värdet 1.

Ett tips är att börja med parametern unsharp mask radius. Radie-inställningar som du kan börja med är följande:

* **[!UICONTROL Website]**: 0,2-0,3 pixlar
* **[!UICONTROL Photographic printing (250-300 ppi)]**: 0,3-0,5 pixlar
* **[!UICONTROL Offset printing (266-300 ppi)]**: 0,7-1,0 pixlar
* **[!UICONTROL Canvas printing (150 ppi)]**: 1,5-2,0 pixlar

Öka mängden gradvis från 1,75 till 4. Om skärpan fortfarande inte är som du vill ha den ökar du radien med ett decimalkomma och kör mängden igen från 1,75 till 4. Upprepa vid behov.

Lämna den monokroma parameterinställningen på 0.

### Bästa tillvägagångssätt för JPEF-komprimering (`&qlt=`) {#best-practices-for-jpef-compression-qlt}

* Den här parametern styr kodningskvaliteten för JPG. Ett högre värde innebär en bild med högre kvalitet men en stor filstorlek. Ett lägre värde innebär en bild med lägre kvalitet men mindre filstorlek. Intervallet för parametern är 0-100.
* Om du vill optimera kvaliteten ska du inte ange parametervärdet 100. Skillnaden mellan en inställning på 90 eller 95 och 100 är nästan osynlig. Och ändå ökar 100 bildfilens storlek i onödan. Om du vill optimera kvaliteten men undvika att bildfilerna blir för stora anger du `qlt= value` till 90 eller 95.
* Om du vill optimera för en liten bildfilsstorlek men behålla bildkvaliteten på en godtagbar nivå anger du `qlt= value` till 80. Värden under 70 till 75 ger en signifikant försämring av bildkvaliteten.
* Det bästa sättet att vara i mitten är att ställa in `qlt= value` till 85 om du vill stanna i mitten.
* Använda chroma-flaggan i `qlt=`

   * The `qlt=` parametern har en andra inställning som gör att du kan aktivera nedsampling av färgvärden i RGB `,1` eller avaktivera med hjälp av värdet `,0`.
   * Börja med att stänga av nedsampling av kromaticitet i RGB (`,0`). Den här inställningen ger vanligtvis bättre bildkvalitet, särskilt för syntetiska bilder med många skarpa kanter och kontrast.

Ett tips för komprimering med JPG är att använda `&qlt=85,0`.

## Bästa tillvägagångssätt för storleksändring av JPEG (`&jpegSize=`) {#best-practices-for-jpeg-sizing-jpegsize}

Parametern `jpegSize` är användbart om du vill garantera att en bild inte överskrider en viss storlek för leverans till enheter som har begränsat minne.

* Den här parametern anges i kilobyte (`jpegSize=&lt;size_in_kilobytes&gt;`). Det definierar den största tillåtna storleken för bildleverans.
* `&jpegSize=` interagerar med komprimeringsparametern JPG `&qlt=`. Om JPG svarar med den angivna komprimeringsparametern JPG (`&qlt=`) överstiger inte ejpegSize-värdet, bilden returneras med `&qlt=` enligt definition. I annat fall `&qlt=` minskas gradvis tills bilden får plats i den tillåtna maxstorleken. Eller tills systemet avgör att det inte får plats och returnerar ett fel.

Som bästa praxis bör du ange `&jpegSize=` och lägg till parametern `&qlt=` om du levererar JPG-bilder till enheter med begränsat minne.

## Sammanfattning av bästa praxis {#best-practices-summary}

Det bästa sättet att uppnå hög bildkvalitet och liten filstorlek är att börja med följande kombination av parametrar:

`fmt=jpg&qlt=85,0&resMode=sharp2&op_usm=1.75,0.3,2,0`

Den här kombinationen av inställningar ger utmärkta resultat under de flesta omständigheter.

Om bilden behöver optimeras ytterligare finjusterar du stegvis skärpeparametrarna (oskarp maskning) genom att börja med radien 0,2 eller 0,3. Därefter ökar du mängden gradvis från 1,75 till maximalt 4 (vilket motsvarar 400 % i Photoshop). Kontrollera att resultatet är det önskade.

Om skärpeeffekten fortfarande inte är tillräcklig ökar du radien i decimalsteg. För varje decimalsteg startar du om beloppet vid 1,75 och ökar det gradvis till 4. Upprepa den här processen tills du uppnår önskat resultat. Värdena ovan är en metod som de kreativa studierna har validerat, men kom ihåg att du kan börja med andra värden och följa andra strategier. Oavsett om resultaten är tillfredsställande för dig eller inte är en subjektiv fråga, så är strukturerade experiment avgörande.

Följande allmänna förslag är användbara när du experimenterar för att optimera arbetsflödet:

* Testa olika parametrar i realtid direkt på en URL.
* Det är en god vana att gruppera Dynamic Media Image Serving-kommandon i en bildförinställning. En bildförinställning är i princip URL-kommandomakron med egna förinställningsnamn, som `$thumb_low$` och `&product_high$`. Det anpassade förinställningsnamnet i en URL-sökväg anropar de här förinställningarna. Den här funktionen hjälper dig att hantera kommandon och kvalitetsinställningar för olika användningsmönster för bilder på webbplatsen och förkortar den totala längden på URL-adresser.
* Experience Manager har också mer avancerade sätt att finjustera bildkvaliteten, t.ex. genom att använda skärpebilder vid intag. Om du vill justera och optimera återgivningsresultaten [Adobe Consulting Services](https://business.adobe.com/customers/consulting-services/main.html) kan hjälpa er med skräddarsydda insikter och bästa praxis.

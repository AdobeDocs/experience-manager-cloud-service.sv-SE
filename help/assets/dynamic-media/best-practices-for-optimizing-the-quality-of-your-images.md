---
title: Bästa tillvägagångssätt för att optimera bildkvaliteten
description: Lär dig de bästa sätten att optimera bildkvaliteten i Dynamic Media
translation-type: tm+mt
source-git-commit: 21b2541b6a3c5011b6eca7edf85299291c361147

---


# Bästa tillvägagångssätt för att optimera bildkvaliteten {#best-practices-for-optimizing-the-quality-of-your-images}

Att optimera bildkvaliteten kan vara en tidskrävande process eftersom många faktorer bidrar till att återge godtagbara resultat. Resultatet är delvis subjektivt eftersom individer upplever olika bildkvalitet. Strukturerade experiment är avgörande.

AEM innehåller över 100 kommandon för leverans av dynamiska media-bilder för justering och optimering av bilder och återgivning. Följande riktlinjer kan hjälpa dig att effektivisera processen och uppnå goda resultat snabbt med några viktiga kommandon och bästa metoder.

## Bästa tillvägagångssätt för bildformat (`&fmt=`) {#best-practices-for-image-format-fmt}

* JPG eller PNG är de bästa alternativen för att leverera bilder med god kvalitet och hanterbar storlek och vikt.
* Om inget formatkommando anges i URL:en används JPG som standard för leverans av dynamiska bilder.
* JPG komprimeras med förhållandet 10:1 och ger vanligtvis mindre bildfilsstorlekar. PNG komprimeras med ett förhållande på cirka 2:1, utom i vissa fall, till exempel när bilder innehåller en vit bakgrund. Vanligtvis är PNG-filernas storlek större än JPG-filer.
* JPG använder förstörande komprimering, vilket innebär att bildelement (pixlar) tas bort under komprimeringen. PNG använder däremot förlustfri komprimering.
* JPG komprimerar ofta fotografiska bilder med bättre återgivning än syntetiska bilder med skarpa kanter och kontrast.
* Om dina bilder innehåller genomskinlighet kan du använda PNG eftersom JPG inte har stöd för genomskinlighet.

Ett tips för bildformat är att börja med den vanligaste inställningen `&fmt=JPG`.

## Bästa tillvägagångssätt för bildstorlek {#best-practices-for-image-size}

Att minska bildstorleken dynamiskt är en av de vanligaste uppgifterna. Det handlar om att ange storleken och, om så önskas, vilket nedsamplingsläge som används för att nedskala bilden.

* För storleksändring av bilder är det bästa och enklaste sättet att använda `&wid=<value>` och `&hei=<value>,`eller bara `&hei=<value>`. Dessa parametrar ställer automatiskt in bildbredden i enlighet med proportionerna.
* `&resMode=<value>`styr den algoritm som används för nedsampling. Börja med `&resMode=sharp2`. Det här värdet ger den bästa bildkvaliteten. Nedsamplingen `value =bilin` går snabbare, men resulterar ofta i alias av artefakter.

Det bästa sättet att ändra storlek på bilder är att använda `&wid=<value>&hei=<value>&resMode=sharp2` eller `&hei=<value>&resMode=sharp2`

## Bästa tillvägagångssätt för bildskärpa {#best-practices-for-image-sharpening}

Bildskärpa är den mest komplicerade aspekten när det gäller att styra bilder på webbplatsen och var många misstag görs. Ta dig tid att lära dig mer om hur skärpa och oskarp maskning fungerar i AEM med hjälp av följande resurser:

De bästa sätten att arbeta med [informationsbilder i Adobe Scene7 Publishing System och i Image Server](/help/assets/dynamic-media/assets/s7_sharpening_images.pdf) gäller även för AEM.

På Adobe TV tittar du på [Skärpa på en bild med oskarp mask](https://helpx.adobe.com/photoshop/atv/cs6-tutorials/sharpening-an-image-with-unsharp-mask.html).

Med AEM kan du förbättra skärpan i bilder vid intag, vid leverans eller både och. I de flesta fall bör du emellertid skärpa upp bilder med endast en metod eller med en annan, men inte med båda metoderna. Att skärpa bilderna vid leverans, på en URL-adress, ger oftast bäst resultat.

Det finns två metoder för bildskärpa:

* Enkel skärpa ( `&op_sharpen`) - Precis som skärpefiltret som används i Photoshop, tillämpar enkel skärpa grundläggande skärpa på den slutliga vyn av bilden efter den dynamiska storleksändringen. Den här metoden kan dock inte konfigureras av användaren. Det bästa sättet är att inte använda &amp;op_sharpen om det inte behövs.
* Oskarp maskering ( `&op_USM`) - Oskarp maskning är ett skärpefilter som är branschstandard. Det bästa sättet är att göra bilder skarpare med oskarp maskering enligt riktlinjerna nedan. Med Oskarp maskning kan du styra följande tre parametrar:

   * `&op_sharpen=`belopp,radie,tröskelvärde

      * **[!UICONTROL mängd]** (0-5, effektens styrka).
      * **[!UICONTROL radie]** (0-250, bredden på de&quot;skärpelinjer&quot; som ritas runt det skarpa objektet, mätt i pixlar.)

         Tänk på att parametrarnas radie och mängd fungerar mot varandra. Reducerad radie kan kompenseras genom ett ökat belopp. Med radie får du bättre kontroll eftersom ett lägre värde ökar skärpan endast för kantpixlarna, medan ett högre värde ökar skärpan för ett större antal pixlar.

      * **[!UICONTROL tröskelvärde]** (0-255, effektkänslighet).

         Den här parametern avgör hur annorlunda de pixlar som ska göras skarpare måste vara från det omgivande området innan de betraktas som kantpixlar och filtret gör dem skarpare. Parametern **[!UICONTROL threshold]** undviker du för mycket skärpa i områden med liknande färger, som hudtoner. Ett tröskelvärde på 12 ignorerar till exempel små variationer i hudtonens ljusstyrka för att undvika att lägga till&quot;brus&quot;, medan kantkontrasten läggs till i områden med hög kontrast, till exempel där ögonfransarna möter huden.
      Mer information om hur du ställer in de här tre parametrarna, inklusive de bästa sätten att använda med filtret, finns i följande resurser:

      AEM Help topic on Sharpening an image.

      Best practices white paper [Sharpening images in Adobe Scene7 Publishing System and on Image Server](/help/assets/dynamic-media/assets/s7_sharpening_images.pdf).

   * Med AEM kan du även styra en fjärde parameter: monokrom (0,1). Den här parametern avgör om oskarp maskning används separat på varje färgkomponent med värdet 0 eller på bildens intensitet/intensitet med värdet 1.


Det bästa sättet är att börja med parametern oskarp maskradie. Radie-inställningar som du kan börja med är följande:

* **[!UICONTROL Webbplats]**: 0,2-0,3 pixlar
* **[!UICONTROL Fotografisk utskrift (250-300 ppi)]**: 0,3-0,5 pixlar
* **[!UICONTROL Offsettryck (266-300 ppi)]**: 0,7-1,0 pixlar
* **[!UICONTROL Arbetsyteutskrift (150 ppi)]**: 1,5-2,0 pixlar

Öka mängden gradvis från 1,75 till 4. Om skärpan fortfarande inte är som du vill ha den ökar du radien med ett decimalkomma och kör mängden igen från 1,75 till 4. Upprepa vid behov.

Lämna den monokroma parameterinställningen på 0.

### Bästa tillvägagångssätt för JPEF-komprimering (`&qlt=`) {#best-practices-for-jpef-compression-qlt}

* Den här parametern styr JPG-kodningskvaliteten. Ett högre värde innebär en bild av högre kvalitet men en stor filstorlek. Ett lägre värde innebär en bild med lägre kvalitet men mindre filstorlek. Intervallet för den här parametern är 0-100.
* Om du vill optimera kvaliteten ska du inte ställa in parametervärdet på 100. Skillnaden mellan en inställning på 90 eller 95 och 100 är nästan otydlig, men 100 ökar storleken på bildfilen i onödan. Om du vill optimera för kvalitet men undvika att bildfiler blir för stora anger du därför 90 eller 95 som `qlt= value` värde.
* Om du vill optimera för en liten bildfilsstorlek men behålla bildkvaliteten på en acceptabel nivå anger du värdet `qlt= value` 80. Värden under 70 till 75 ger en signifikant försämring av bildkvaliteten.
* Ett tips är att du bör behålla mitten genom att ställa in värdet `qlt= value` på 85 för att behålla mitten.
* Använda chroma-flaggan i `qlt=`

   * Parametern `qlt=` har en andra inställning som gör att du kan aktivera nedsampling av RGB-kromaticitet med hjälp av värdet `,1` eller inaktiverat med hjälp av värdet `,0`.
   * Börja med att stänga av nedsampling av RGB-kromaticitet (`,0`). Den här inställningen ger vanligtvis bättre bildkvalitet, särskilt för syntetiska bilder med många skarpa kanter och kontrast.

Ett tips för JPG-komprimering är att använda `&qlt=85,0`.

## Bästa tillvägagångssätt för JPEG-storleksändring (`&jpegSize=`) {#best-practices-for-jpeg-sizing-jpegsize}

jpegSize är en användbar parameter om du vill försäkra dig om att en bild inte överskrider en viss storlek för leverans till enheter som har begränsat minne.

* Den här parametern anges i kilobyte (`jpegSize=&lt;size_in_kilobytes&gt;`). Det definierar den största tillåtna storleken för bildleverans.
* `&jpegSize=` interagerar med JPG-komprimeringsparametern `&qlt=`. Om JPG-svaret med den angivna JPG-komprimeringsparametern (`&qlt=`) inte överskrider ejpegSize-värdet returneras bilden med `&qlt=` det definierade värdet. Annars `&qlt=` minskas bilden gradvis tills bilden får plats i den högsta tillåtna storleken, eller tills systemet fastställer att den inte får plats och returnerar ett fel.

Det bästa sättet är att ange `&jpegSize=` och lägga till parametern `&qlt=` om du levererar JPG-bilder till enheter med begränsat minne.

## Sammanfattning av bästa praxis {#best-practices-summary}

Det bästa sättet att uppnå en hög bildkvalitet och liten filstorlek är att börja med följande kombination av parametrar:

`fmt=jpg&qlt=85,0&resMode=sharp2&op_usm=1.75,0.3,2,0`

Den här kombinationen av inställningar ger utmärkta resultat under de flesta omständigheter.

Om bilden behöver optimeras ytterligare finjusterar du stegvis skärpeparametrarna (oskarp maskning) genom att börja med radien 0,2 eller 0,3. Öka sedan mängden gradvis från 1,75 till maximalt 4 (motsvarande 400 % i Photoshop). Kontrollera att resultatet är det önskade.

Om skärpeeffekten fortfarande inte är tillräcklig ökar du radien i decimalsteg. För varje decimalsteg startar du om beloppet vid 1,75 och ökar det gradvis till 4. Upprepa den här processen tills du uppnår önskat resultat. Värdena ovan är en metod som de kreativa studierna har validerat, men kom ihåg att du kan börja med andra värden och följa andra strategier. Oavsett om resultaten är tillfredsställande för dig eller inte är en subjektiv fråga, så är strukturerade experiment avgörande.

När du experimenterar kan du också hitta följande allmänna förslag som kan hjälpa dig att optimera arbetsflödet:

* Testa och testa olika parametrar i realtid, antingen direkt på en URL eller med Scene7 Publishing System bildjusteringsfunktion som ger förhandsgranskning i realtid för justeringsåtgärder.
* Det är en god vana att gruppera kommandona Dynamic Media Image Serving i en bildförinställning. En bildförinställning är i princip URL-kommandomakron med anpassade förinställningsnamn som `$thumb_low$` och `&product_high$`. Det anpassade förinställningsnamnet i en URL-sökväg gör att dessa förinställningar anropas. Den här funktionen hjälper dig att hantera kommandon och kvalitetsinställningar för olika användningsmönster för bilder på webbplatsen och förkortar den totala längden på URL-adresser.
* AEM erbjuder också mer avancerade sätt att finjustera bildkvaliteten, t.ex. att använda skärpebilder vid inhämtning. I avancerade fall där detta kan vara ett alternativ för att ytterligare finjustera och optimera återgivningsresultaten kan [Adobe Professional Services](https://www.adobe.com/experience-cloud/consulting-services.html) hjälpa dig med anpassade insikter och bästa metoder.


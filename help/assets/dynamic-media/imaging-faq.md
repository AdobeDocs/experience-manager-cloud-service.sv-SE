---
title: Smart bildbehandling
description: Smart bildbehandling utnyttjar varje användares unika visningsegenskaper för att automatiskt leverera rätt bilder som är optimerade för sin upplevelse, vilket ger bättre prestanda och engagemang.
translation-type: tm+mt
source-git-commit: 6224d193adfb87bd9b080f48937e0af1f03386d6

---


# Smart bildbehandling {#smart-imaging}

## Vad är smart bildbehandling? {#what-is-smart-imaging}

Smart bildbehandling utnyttjar varje användares unika visningsegenskaper för att automatiskt leverera rätt bilder som är optimerade för sin upplevelse, vilket ger bättre prestanda och engagemang. Smart bildbehandling fungerar med befintliga bildförinställningar och använder intelligens under de sista millisekunderna i leveransen för att ytterligare minska bildfilens storlek baserat på webbläsarens eller nätverkets anslutningshastighet.

Smarta bildbehandlingsfördelar tack vare den ökade prestandaförbättringen med att vara helt integrerad med den bästa CDN-tjänsten i klassen. Den här tjänsten hittar den optimala Internetvägen mellan servrar, nätverk och peering-punkter som har den lägsta latensen och/eller paketförlustfrekvensen än standardvägen på Internet.

## Vilka är de viktigaste fördelarna med smart bildbehandling? {#what-are-the-key-benefits-of-smart-imaging}

Smart bildbehandling ger bättre prestanda genom att bildfilens storlek automatiskt optimeras baserat på användarens egenskaper. Eftersom bilder utgör större delen av en sidas inläsningstid kan prestandaförbättringarna få en genomgripande effekt på nyckeltal som högre konverteringsgrad, tidsåtgång på webbplatsen, lägre avhoppsfrekvens på webbplatsen och så vidare. Adobe jämförde prestanda för standardbildleverans jämfört med smart bildbehandling i olika filformat, webbläsare och kvalitetsinställningar (QLT). På det hela taget kan du förvänta dig en prestandaförbättring på 22-47 % beroende på dina befintliga inställningar för bildförinställningar och specifika slutanvändaregenskaper.

![image2017-11-14_133226](/help/assets/dynamic-media/assets/image2017-11-14_133226.png)

## Kostar licensieringen för smart bildbehandling några? {#are-there-any-licensing-costs-associated-with-smart-imaging}

Nej. Smart bildbehandling ingår i din befintliga licens av antingen Dynamic Media Classic (Scene7) eller Dynamic Media. Det finns inga extra kostnader att dra nytta av den här nya funktionen.

## Hur fungerar smart bildbehandling? {#how-does-smart-imaging-work}

När en bild begärs för första gången av en konsument kontrollerar vi användaregenskaperna och konverterar till rätt bildformat baserat på webbläsare. Dessutom skapar vi samtidigt alla formatkonverteringar som sedan cachas vid CDN. När användare i olika webbläsare efterfrågar den bilden levereras det korrekta bildformatet automatiskt direkt från CDN-cachen. Dessa formatkonverteringar görs på ett förlustfritt sätt som inte försämrar den visuella återgivningen. Smart bildbehandling konverterar automatiskt bilder till olika format baserat på webbläsarkapacitet enligt följande:

* Konvertera automatiskt till förlustfri WebP för webbläsare som stöder WebP-format som Chrome, Android och Opera.
* Konvertera automatiskt till förlustfri JPEGXR för webbläsare som stöder JPEGXR-format, t.ex. Internet Explorer 9+.
* Konvertera automatiskt till förlustfri JPEG2000 för webbläsare som stöder JPEG2000-format, t.ex. Safari.
* För webbläsare som inte stöder dessa format används det bildformat som ursprungligen begärdes.

## Vilka bildformat stöds? {#what-image-formats-are-supported}

Följande bildformat stöds för smart bildbehandling:

* RGB JPEG
* RGB PNG
* RGB TIFF
* CMYK JPEG
* CMYK TIFF

## Hur fungerar smart bildbehandling med befintliga bildförinställningar som redan används? {#how-does-smart-imaging-work-with-our-existing-image-presets-that-are-already-in-use}

Smart bildbehandling fungerar med dina befintliga bildförinställningar och observerar praktiskt taget alla bildinställningar, som storlek, kvalitet, skärpa och så vidare. Det som kommer att ändras är bildformatet eller, vid långsam nätverksanslutningshastighet, kvalitetsinställningen. För formatkonvertering behåller vi fullständig visuell återgivning enligt inställningarna i bildförinställningen, men med en mindre filstorlek.

Anta att en bildförinställning har definierats med JPEG-format, storlek 500x500, kvalitet=85 och oskarp mask=0.1,1,5. När vi upptäcker att en användare använder webbläsaren Chrome konverteras bilden till ett icke-förstörande WebP-format med storleken 500x500, quality=85 och oskarp mask=0.1,1,5.

## Måste jag ändra URL:er, bildförinställningar eller driftsätta ny kod på min webbplats för smart bildbehandling? {#will-i-have-to-change-any-urls-image-presets-or-deploy-any-new-code-on-my-site-for-smart-imaging}

Nej. Smart bildbehandling fungerar sömlöst med befintliga bild-URL:er och bildförinställningar. Dessutom kräver smart bildbehandling inte att du lägger till kod på webbplatsen för att identifiera olika användaregenskaper (webbläsare, bandbredd, enhet osv.). Allt detta hanteras automatiskt av Adobe.

Den enda ändring som kan behövas är att uppdatera inställningen **[!UICONTROL TTL (Time To Live]** ). Den här inställningen definierar hur länge resurser cachas av CDN. För att maximera prestandaförbättringarna av smart bildbehandling rekommenderar Adobe att TTL-värdet ställs in på 24 timmar eller längre. Så här ändrar du den här inställningen:

* Om du använder Dynamic Media Classic trycker du på **[!UICONTROL Inställningar > Programinställningar > Publiceringsinställningar > Bildserver]**. Ange **[!UICONTROL standardvärdet för Klientcachetstid till Live]** till 24 eller längre.

* Om du använder Dynamic Media anger du värdet för **[!UICONTROL Förfallotid]** till 24 timmar eller längre.

>[!NOTE]
>
>Om du anger TTL &lt;= 1 timme fungerar inte smart bildbehandling.

## Fungerar smart bildbehandling med HTTPS? Vad sägs om HTTP/2? {#does-smart-imaging-working-with-https-how-about-http}

Smart bildbehandling fungerar med bilder som levereras via HTTP eller HTTPS. Dessutom fungerar det även över HTTP/2.

## Är jag berättigad att använda smart bildbehandling? {#am-i-eligible-to-use-smart-imaging}

För att kunna använda smart bildbehandling måste företagets konto för Dynamic Media Classic eller Dynamic Media på AEM uppfylla följande krav:

* Använd det Adobe-paketerade CDN (Content Delivery Network) som en del av din licens.
* Använd en dedikerad domän (d.v.s. `images.company.com` eller `mycompany.scene7.com`), inte en allmän domän (d.v.s. `s7d1.scene7.com`, `s7d2.scene7.com`eller `s7d13.scene7.com`).

   Om du vill hitta dina domäner loggar du in på ditt företagskonto eller dina företagskonton.

   Tryck på **[!UICONTROL Inställningar > Programinställningar > Allmänna inställningar]**. Leta efter fältet **[!UICONTROL Publicerat servernamn]**. Om du för närvarande använder en allmän domän kan du begära att du flyttar över till din egen anpassade domän som en del av den här övergången.

* Begär inte CMYK JPEG-bilder. Smart bildbehandling konverterar CMYK JPEG-bilder till RGB. Om du behöver hämta CMYK JPEG-bilder kan du inte använda smart bildbehandling.

## Hur aktiverar jag smart bildbehandling för mitt konto? {#what-is-the-process-for-enabling-smart-imaging-for-my-account}

Du måste initiera begäran om att använda smart bildåtergivning; den inte aktiveras automatiskt.

1. Initiera en begäran om teknisk support (e-post: s7support@adobe.com).
1. Ange följande information i din supportförfrågan:

   1. Primärt kontaktnamn, e-postadress, telefon.
   1. Alla domäner som ska aktiveras för smart bildbehandling (det vill säga images.company.com eller mycompany.scene7.com).

      Om du vill hitta dina domäner loggar du in på ditt företagskonto eller dina företagskonton.

      Klicka på **[!UICONTROL Inställningar > Programinställningar > Allmänna inställningar]**.

      Leta efter fältet **[!UICONTROL Publicerat servernamn]**.
   1. Kontrollera att du använder CDN via Adobe och inte hanteras med en direkt relation.
   1. Kontrollera att du använder en dedikerad domän som `images.company.com` eller `mycompany.scene7.com`och inte en allmän domän som `s7d1.scene7.com`, `s7d2.scene7.com`, `s7d13.scene7.com`.

      Om du vill hitta dina domäner loggar du in på ditt företagskonto eller dina företagskonton.

      Klicka på **[!UICONTROL Inställningar > Programinställningar > Allmänna inställningar]**.

      Leta efter fältet **[!UICONTROL Publicerat servernamn]**. Om du för närvarande använder en allmän Dynamic Media Classic-domän kan du begära att du flyttar över till din egen anpassade domän som en del av den här övergången.
   1. Ange om du även vill att detta ska fungera över HTTP/2

1. Teknisk support lägger till dig i väntelistan för smarta bilder baserat på i vilken ordning begäranden skickades.
1. När Adobe är redo att hantera din förfrågan kontaktar supporten dig för att koordinera och ange ett måldatum.
1.  Valfritt: Du kan testa smart bildåtergivning i mellanlagring innan Adobe publicerar den nya funktionen i produktion.
1. Du meddelas när du är klar via supporten.
1. För att maximera prestandaförbättringarna av smart bildbehandling rekommenderar Adobe att du anger TTL-värdet (Time To Live) till 24 timmar eller längre. TTL-värdet definierar hur länge resurser cachas av CDN. Så här ändrar du den här inställningen:

   1. Om du använder Dynamic Media Classic klickar du på **[!UICONTROL Inställningar > Programinställningar > Publiceringsinställningar > Bildserver]**. Ange **[!UICONTROL standardvärdet för Klientcachetstid till Live]** till 24 eller längre.
   1. Om du använder Dynamic Media anger du värdet för **[!UICONTROL Förfallotid]** 24 timmar eller längre.

## När kan jag förvänta mig att mitt konto ska aktiveras med smart bildbehandling? {#when-can-i-expect-my-account-to-be-enabled-with-smart-imaging}

Förfrågningar behandlas i den ordning som de tas emot av teknisk support, enligt väntelistan.

>[!NOTE]
Det kan finnas lång ledtid eftersom du måste rensa cacheminnet för att aktivera smart bildbehandling. Därför kan bara ett fåtal kundövergångar hanteras vid en viss tidpunkt.

## Vilka är riskerna med att byta till smart bildbehandling? {#what-are-the-risks-with-switching-over-to-use-smart-imaging}

Övergången till smart bildbehandling rensar bort cacheminnet vid CDN eftersom det handlar om att byta till en ny konfiguration av Dynamic Media Classic eller Dynamic Media i AEM.

Under den första övergången träffar de icke-cachelagrade bilderna direkt Adobes servrar tills cachen återskapas. På grund av detta planerar Adobe att hantera ett fåtal kundövergångar i taget så att godtagbara prestanda upprätthålls när vi drar in förfrågningar från vårt ursprung. För de flesta kunder är cacheminnet helt uppbyggt igen på CDN inom cirka 1 till 2 dagar.

## Hur kan jag verifiera om smart bildbehandling fungerar som väntat?  {#how-can-i-verify-whether-smart-imaging-is-working-as-expected}

1. När ditt konto har konfigurerats med smart bildåtergivning läser du in en URL-adress för bilden Dynamic Media Classic(S7)/Dynamic Media i webbläsaren.
1. Öppna panelen Chrome developer genom att klicka på **[!UICONTROL View > Developer > Developer Tools]** i webbläsaren. Eller välj vilket verktyg du vill.

1. Kontrollera att cache är inaktiverat när utvecklingsverktygen är öppna.

   1. I Windows går du till inställningarna i rutan för utvecklarverktyget och markerar kryssrutan **[!UICONTROL Inaktivera cache (när utvecklingsverktygen är öppna)]** .
   1. På Mac väljer du **[!UICONTROL inaktivera cache]** under fliken **[!UICONTROL Nätverk]** i utvecklarfönstret.

1. Bilden kommer inte att optimeras efter den första begäran. Det tar normalt cirka 15 minuter att returnera den optimerade bilden om den inte finns i CDN-cachen.
1. Observera att innehållstypen har omvandlats till lämpligt format. På följande skärmbild visas PNG-bilden som konverteras dynamiskt till WebP i Chrome.
1. Upprepa testet i olika webbläsare och under olika användarförhållanden.

>[!NOTE]
Alla bilder konverteras inte. Smart bildbehandling avgör om konverteringen behövs för att förbättra prestandan. I vissa fall, där det inte finns någon förväntad prestandaökning, konverteras bilden inte.

![image2017-11-14_15398](/help/assets/dynamic-media/assets/image2017-11-14_15398.png)


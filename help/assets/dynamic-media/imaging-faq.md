---
title: Smart bildbehandling
description: Smart bildbehandling utnyttjar varje användares unika visningsegenskaper för att automatiskt leverera rätt bilder som är optimerade för sin upplevelse, vilket ger bättre prestanda och engagemang.
translation-type: tm+mt
source-git-commit: d84a6692f2d0aae496bd2bd98ac99c2663f3fe52
workflow-type: tm+mt
source-wordcount: '1669'
ht-degree: 0%

---


# Smart bildbehandling {#smart-imaging}

## Vad är&quot;Smart Imaging&quot;? {#what-is-smart-imaging}

Smart Imaging-tekniken utnyttjar Adobe Senseis AI-funktioner och fungerar med befintliga&quot;bildförinställningar&quot; för att förbättra bildleveransen genom att automatiskt optimera bildformat, storlek och kvalitet baserat på webbläsarens kapacitet.

Smart Imaging får också bättre prestanda eftersom det är helt integrerat med Adobes förstklassiga CDN-tjänst. Den här tjänsten hittar den optimala Internetvägen mellan servrar, nätverk och peering-punkter som har den lägsta latensen och/eller paketförlustfrekvensen än standardvägen på Internet.

I följande bildresursexempel visas den nya optimeringen av smarta bilder:

| Bild<br>(URL) | Miniatyrbild | Storlek<br> (JPEG) | Storlek (WebP)<br> (med Smart Imaging) | % minskning |
|---|---|---|---|---|
| [Bild 1](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_6?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture1](/help/assets/assets-dm/picture1.png) | 73,75 kB | 45,92 kB | 38% |
| [Bild 2](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_3?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture2](/help/assets/assets-dm/picture2.png) | 191 kB | 70,66 kB | 63% |
| [Bild 3](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_2?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture3](/help/assets/assets-dm/picture3.png) | 96,64 kB | 39,44 kB | 59% |
| [Bild 4](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_1?hei=500&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture4](/help/assets/assets-dm/picture4.png) | 315,80 kB | 178,19 kB | 44% |
|  |  |  |  | Genomsnitt = 51 % |

På samma sätt som ovanstående testade Adobe även 7 009 URL:er från kundsajter och lyckades i genomsnitt optimera filstorleken 38 % ytterligare för JPEG och optimera filstorleken 31 % ytterligare för PNG med WebP-format, tack vare Smart Imaging.

## Vilka är de viktigaste fördelarna med den senaste Smart Imaging? {#what-are-the-key-benefits-of-smart-imaging}

Eftersom bilder utgör större delen av en sidas inläsningstid kan prestandaförbättringarna få en genomgripande effekt på nyckeltal som högre konvertering, tid på webbplatsen och lägre avhoppsfrekvens.

Förbättringar i den senaste versionen av Smart Imaging:

* Serverar optimerat innehåll direkt (vid körning).
* Använder Adobe Sensei-teknik för att konvertera enligt den kvalitet (qlt) som anges i bildbegäran.
* Smart Imaging kan inaktiveras med URL-parametern &quot;bfc&quot;.
* TTL-oberoende (Time To Live). Tidigare var en minsta TTL på 12 timmar obligatorisk för att Smart Imaging skulle fungera.
* Tidigare cachelagrades både original- och härledda bilder, och det var en tvåstegsprocess för att göra cacheminnet ogiltigt. I den senaste versionen av Smart Imaging cachelagras bara derivat, vilket möjliggör en cacheogiltigförklaring i ett enda steg.
* Kunder som använder anpassade rubriker i sina regeluppsättningar (till exempel&quot;Timing Allow Origin&quot;,&quot;X-Robot&quot; som föreslogs när ett anpassat rubrikvärde [lades till i bildsvar|Dynamic Media Classic](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/add-custom-header-val-image.html)) kommer att dra nytta av den senaste smarta bildhanteringen eftersom dessa rubriker inte blockeras, till skillnad från den tidigare versionen av Smart Imaging.

## Kostar licensieringen för smart bildbehandling några? {#are-there-any-licensing-costs-associated-with-smart-imaging}

Nej. Smart Imaging ingår i din befintliga licens av antingen Dynamic Media Classic (Scene7) eller AEM Dynamic Media (On Prem, AMS och AEM som en molntjänst).

>[!NOTE]
>
>Smart Imaging är inte tillgängligt för kunder med Dynamic Media - Hybrid.


## Hur fungerar smart bildbehandling? {#how-does-smart-imaging-work}

Smart Imaging använder Adobe Sensei för att automatiskt konvertera bilder till det optimala formatet, storleken och kvaliteten, baserat på webbläsarkapacitet:

* Konvertera automatiskt till WebP för webbläsare som Chrome, Firefox, Microsoft Edge, Android och Opera.
* Konvertera automatiskt till JPEG2000 för webbläsare som Safari.
* Konvertera automatiskt till JPEG för webbläsare som Internet Explorer 9+.
* För webbläsare som inte stöder dessa format används det bildformat som ursprungligen begärdes.

Om den ursprungliga bildstorleken är mindre än vad Smart Imaging skapar, behålls originalbilden.

## Vilka bildformat stöds? {#what-image-formats-are-supported}

Följande bildformat stöds för Smart Imaging:
* JPEG
* PNG

<!-- For any other format mentioned in a URL, you should explicity turn off Smart Imaging.  Append modifier `bfc=off` to the URL for file formats other than JPEG and PNG. You can accomplish this by using either one of the following methods:

* Use a ruleset if the `fmt` modifier is mentioned in the URL. 
* Append in URL modifiers field of the presets concerned.

Adobe is working on a permanent fix that does not require you to append `bfc=off` for `fmt !=JPEG` or `fmt !=PNG`. This topic will be updated after the fix is delivered. -->

## Hur fungerar Smart Imaging med befintliga bildförinställningar som redan används? {#how-does-smart-imaging-work-with-our-existing-image-presets-that-are-already-in-use}

Smart Imaging fungerar med dina befintliga &quot;bildförinställningar&quot; och alla bildinställningar kontrolleras, med undantag för kvalitet (qlt) och format (fmt) om det begärda filformatet är JPEG eller PNG. För formatkonvertering behåller vi fullständig visuell återgivning enligt inställningarna i bildförinställningen, men med en mindre filstorlek. Om den ursprungliga bildstorleken är mindre än vad Smart Imaging skapar, behålls originalbilden.

<!-- In addition, if your image presets are used to return `fmt !=JPEG` or `fmt !=PNG`, be sure append `bfc=off` in the preset modifier field to return the requested file format. -->

## Måste jag ändra URL:er, bildförinställningar eller driftsätta ny kod för Smart Imaging på min webbplats? {#will-i-have-to-change-any-urls-image-presets-or-deploy-any-new-code-on-my-site-for-smart-imaging}

Nej. Smart Imaging fungerar sömlöst med befintliga bild-URL:er och bildförinställningar. Dessutom kräver Smart Imaging inte att du lägger till kod på webbplatsen för att identifiera en användares webbläsare. Allt detta hanteras automatiskt.

<!-- As mentioned earlier, Smart Imaging supports only JPEG and PNG image formats. For other formats, you need to append the `bfc=off` modifier to the URL as described earlier. -->

Se även [Är jag berättigad att använda Smart Imaging?](#am-i-eligible-to-use-smart-imaging) för att förstå vad som krävs för smart bildbehandling.

## Fungerar Smart Imaging med HTTPS? Vad sägs om HTTP/2? {#does-smart-imaging-working-with-https-how-about-http}

Smart Imaging fungerar med bilder som levereras via HTTP eller HTTPS. Dessutom fungerar det även över HTTP/2.

## Är jag berättigad att använda smart bildbehandling? {#am-i-eligible-to-use-smart-imaging}

För att kunna använda Smart Imaging måste företagets konto för Dynamic Media Classic eller Dynamic Media på AEM uppfylla följande krav:

* Använd det Adobe-paketerade CDN (Content Delivery Network) som en del av din licens.
* Använd en dedikerad domän (till exempel `images.company.com` eller `mycompany.scene7.com`), inte en allmän domän (till exempel `s7d1.scene7.com`, `s7d2.scene7.com`eller `s7d13.scene7.com`).

Om du vill hitta dina domäner loggar du in på ditt företagskonto eller dina företagskonton.

Tryck på **[!UICONTROL Setup > Application Setup > General Settings]**. Leta efter fältet som är märkt **[!UICONTROL Published Server Name]**. Om du för närvarande använder en allmän domän kan du begära att du flyttar över till din egen anpassade domän som en del av den här övergången när du skickar in en teknisk supportanmälan.

Din första anpassade domän kostar inget extra med en Dynamic Media-licens.

## Hur aktiverar jag Smart Imaging för mitt konto? {#what-is-the-process-for-enabling-smart-imaging-for-my-account}

Du måste initiera begäran om att använda smart bildåtergivning; den inte aktiveras automatiskt.

1. Initiera en begäran om teknisk support (e-post: `s7support@adobe.com`).
1. Ange följande information i din supportförfrågan:

   1. Primärt kontaktnamn, e-postadress, telefon.
   1. Alla domäner som ska aktiveras för smart bildåtergivning (d.v.s. `images.company.com` eller `mycompany.scene7.com`).

      Om du vill hitta dina domäner loggar du in på ditt företagskonto eller dina företagskonton.

      Klicka på **[!UICONTROL Setup > Application Setup > General Settings]**.

      Leta efter fältet som är märkt **[!UICONTROL Published Server Name]**.
   1. Kontrollera att du använder CDN via Adobe och inte hanteras med en direkt relation.
   1. Kontrollera att du använder en dedikerad domän som `images.company.com` eller `mycompany.scene7.com`och inte en allmän domän som `s7d1.scene7.com`, `s7d2.scene7.com`, `s7d13.scene7.com`.

      Om du vill hitta dina domäner loggar du in på ditt företagskonto eller dina företagskonton.

      Klicka på **[!UICONTROL Setup > Application Setup > General Settings]**.

      Leta efter fältet som är märkt **[!UICONTROL Published Server Name]**. Om du för närvarande använder en allmän Dynamic Media Classic-domän kan du begära att du flyttar över till din egen anpassade domän som en del av den här övergången.
   1. Ange om du även vill att detta ska fungera över HTTP/2.

1. Den tekniska supporten lägger till dig i väntelistan för Smart Imaging-kunder baserat på i vilken ordning begäranden skickades.
1. När Adobe är redo att hantera din förfrågan kontaktar supporten dig för att koordinera och ange ett måldatum.
1. **Valfritt**: Du kan testa smart bildåtergivning i mellanlagring innan Adobe publicerar den nya funktionen i produktion.
1. Du meddelas när du är klar via supporten.
1. För att maximera prestandaförbättringarna av Smart Imaging rekommenderar Adobe att du anger TTL-värdet (Time To Live) till 24 timmar eller längre. TTL-värdet definierar hur länge resurser cachas av CDN. Så här ändrar du den här inställningen:

   1. Om du använder Dynamic Media Classic klickar du på **[!UICONTROL Setup > Application Setup > Publish Setup > Image Server]**. Ange **[!UICONTROL Default Client Cache Time To Live]** värdet 24 eller längre.
   1. Om du använder Dynamic Media följer du [dessa anvisningar](config-dm.md). Ange **[!UICONTROL Expiration]** värdet 24 timmar eller längre.

## När kan jag förvänta mig att mitt konto ska aktiveras med Smart Imaging? {#when-can-i-expect-my-account-to-be-enabled-with-smart-imaging}

Förfrågningar behandlas i den ordning som de tas emot av teknisk support, enligt väntelistan.

>[!NOTE]
Det kan ta lång tid eftersom Adobe måste rensa cachen för att kunna aktivera Smart Imaging. Därför kan bara ett fåtal kundövergångar hanteras vid en viss tidpunkt.

## Vilka är riskerna med att byta till Smart Imaging? {#what-are-the-risks-with-switching-over-to-use-smart-imaging}

Det finns ingen risk för kundens webbsida. Du bör dock vara medveten om att övergången till Smart Imaging rensar bort ditt cacheminne vid CDN eftersom det handlar om att byta till en ny konfiguration av Dynamic Media Classic eller Dynamic Media i AEM.

Under den första övergången träffar de icke-cachelagrade bilderna direkt Adobes servrar tills cachen återskapas. På grund av detta planerar Adobe att hantera ett fåtal kundövergångar i taget så att godtagbara prestanda upprätthålls när vi drar in förfrågningar från vårt ursprung. För de flesta kunder är cacheminnet helt uppbyggt igen på CDN inom cirka 1 till 2 dagar.

## Hur kan jag verifiera om smart bildbehandling fungerar som väntat?  {#how-can-i-verify-whether-smart-imaging-is-working-as-expected}

1. När ditt konto har konfigurerats med smart bildåtergivning läser du in en URL-adress för en bild i Dynamic Media Classic (Scene7)/Dynamic Media i webbläsaren.
1. Öppna Chrome-utvecklarfönstret genom att klicka **[!UICONTROL View > Developer > Developer Tools]** i webbläsaren. Eller välj ett valfritt verktyg för webbläsare.

1. Kontrollera att cache är inaktiverat när utvecklingsverktygen är öppna.

   * I Windows navigerar du till inställningarna i rutan för utvecklarverktyget och markerar sedan **[!UICONTROL Disable cache (while devtools is open)]** kryssrutan.
   * På Mac - i utvecklarrutan, under **[!UICONTROL Network]** fliken, väljer du **[!UICONTROL disable cache]** .

1. Observera att innehållstypen har omvandlats till lämpligt format. På följande skärmbild visas en PNG-bild som konverteras dynamiskt till WebP i Chrome.
1. Upprepa testet i olika webbläsare och under olika användarförhållanden.

>[!NOTE]
Alla bilder konverteras inte. Smart Imaging avgör om konverteringen behövs för att förbättra prestandan. I vissa fall, där det inte finns någon förväntad prestandaökning eller där formatet inte är JPEG eller PNG, konverteras inte bilden.

![image2017-11-14_15398](assets/image2017-11-14_15398.png)

## Kan Smart Imaging stängas av på begäran? {#turning-off-smart-imaging}

Ja. Du kan inaktivera Smart Imaging genom att lägga till modifieraren `bfc=off` i URL:en.

## Vilken &quot;justering&quot; är tillgänglig? Finns det några inställningar eller beteenden som kan definieras? (#tuning-settings)

För närvarande kan du välja att aktivera eller inaktivera Smart bildbehandling. Ingen annan justering är tillgänglig.

## Om Smart Imaging hanterar kvalitetsinställningarna, finns det några minimi- och maximumvärden vi kan ange? Kan du till exempel ange &quot;inte lägre än 60&quot; och &quot;inte större än 80&quot;? (#minimum-maximum)

Det finns ingen sådan provisioneringsmöjlighet i den aktuella funktionen för smart bildbehandling.

## I vissa fall returneras en JPEG-bild till Chrome i stället för till en WebP-bild. Varför händer det där? (#jpeg-webp)

Smart bildbehandling avgör om konverteringen är bra eller inte. Den nya bilden returneras bara om konverteringen resulterar i en mindre filstorlek med jämförbar kvalitet.

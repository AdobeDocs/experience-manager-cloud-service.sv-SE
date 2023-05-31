---
title: Smart bildbehandling
description: Läs om hur Smart Imaging med Adobe Sensei AI använder varje användares unika visningsegenskaper för att automatiskt leverera rätt bilder som är optimerade för sin upplevelse, vilket ger bättre prestanda och engagemang.
contentOwner: Rick Brough
feature: Asset Management,Renditions
role: User
mini-toc-levels: 2
exl-id: 863784d9-0c91-4deb-8edd-1354a21581c3
source-git-commit: 6f9ddcf31a1869bb8bebb566d05c371e996fe354
workflow-type: tm+mt
source-wordcount: '3482'
ht-degree: 0%

---

# Smart bildbehandling {#smart-imaging}

## Om Smart Imaging{#about-smart-imaging}

Smart Imaging-tekniken tillämpar Adobe Sensei AI-funktioner och fungerar med befintliga&quot;bildförinställningar&quot;. Det förbättrar bildleveransen genom att automatiskt optimera bildformat, storlek och kvalitet baserat på webbläsarens funktioner.

Och nu får du en bättre Google Core Web Vital-poäng för LCP (Störst Contentful Paint) med förbättrad Smart Imaging som nu har stöd för både AVIF och WebP.

>[!IMPORTANT]
>
>Smart Imaging kräver att du använder det färdiga CDN (Content Delivery Network) som medföljer Adobe Experience Manager - Dynamic Media. Eventuellt annat anpassat CDN stöds inte med den här funktionen.

>[!TIP]
>
>Prova och upptäck fördelarna med Dynamic Media bildmodifierare och Smart Imaging med Dynamic Media [_Ögonblicksbild_](https://snapshot.scene7.com/).
>
> Ögonblicksbild är ett visuellt demonstrationsverktyg som är utformat för att illustrera styrkan hos Dynamic Media för optimerad och dynamisk bildleverans. Experimentera med testbilder eller Dynamic Media-URL:er för att visuellt se resultatet av olika bildmodifierare i Dynamic Media och optimera smarta bilder för följande:
>* Filstorlek (med WebP- och AVIF-leverans)
>* Nätverksbandbredd
>* DPR (Device Pixel Ratio)
>
>Om du vill veta hur enkelt det är att använda Snapshot spelar du [Utbildningsvideo om ögonblicksbild](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-snapshot.html?lang=en) (3 minuter och 17 sekunder).

Smart Imaging drar nytta av den ökade prestandaförbättringen genom att vara helt integrerad med Adobe förstklassiga CDN-tjänst (Content Delivery Network). Den här tjänsten hittar den optimala Internet-vägen mellan servrar, nätverk och peering-punkter. Den hittar en väg som har lägst latens och lägst paketförlustfrekvens i stället för att använda standardvägen på Internet.

I följande bildresursexempel visas den nya optimeringen av smarta bilder:

| Bild (URL) | Miniatyrbild | Storlek (JPEG) | Storlek (WebP) med smart bildbehandling | Storlek (AVIF) med smart bildbehandling | % minskning med WebP | % minskning med AVIF |
|---|---|---|---|---|---|---|
| [Bild 1](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_6?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture1](/help/assets/assets-dm/picture1.png) | 145 kB | 106 kB | 90,2 kB | 26.89% | 37.79% |
| [Bild 2](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_3?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture2](/help/assets/assets-dm/picture2.png) | 412 kB | 346 kB | 113 kB | 16.01% | 72.57% |
| [Bild 3](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_2?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture3](/help/assets/assets-dm/picture3.png) | 221 kB | 189 kB | 87,1 kB | 14.47% | 60.58% |
| [Bild 4](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_1?hei=500&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture4](/help/assets/assets-dm/picture4.png) | 594 kB | 545 kB | 286 kB | 8.25% | 51.85% |

På samma sätt som ovan utförde Adobe också ett test med en större exempeluppsättning. Formatet AVIF gav 20 % extra storleksminskning jämfört med WebP, vilket gav en 27-procentig minskning jämfört med JPEG. Allt med samma visuella kvalitet. Totalt ger AVIF upp till 41 % genomsnittlig storleksminskning jämfört med JPEG.

Jämför WebP och AVIF med PNG, du kan se en storleksminskning på 84 % med WebP och 87 % med AVIF. Och eftersom både WebP- och AVIF-formaten stöder genomskinlighet och flera bildanimeringar är det en bra ersättning för genomskinliga PNG- och GIF-filer.

Se även [Bildoptimering med nästa generations bildformat (WebP och AVIF)](https://blog.developer.adobe.com/image-optimisation-with-next-gen-image-formats-webp-and-avif-248c75afacc4)

<!-- HIDDEN ON MAY 19, 2022 BASED ON CQDOC-19280 On the mobile web, the challenges are compounded by two factors:

* Large variety of devices with different form factors and high-resolution displays.
* Constrained network bandwidth.

In terms of images, the goal is to serve the best quality images as efficiently as possible. -->

**Fördelar med Smart Imaging**

Smart Imaging ger bättre prestanda vid bildleverans genom att automatiskt optimera bildfilens storlek baserat på vilken webbläsare som används, enhetens visning och nätverksförhållanden. Eftersom bilder utgör det mesta av en sidas laddningstid kan alla prestandaförbättringar ha en genomgripande effekt på nyckeltal som högre konverteringsgrader, tidsåtgång på en webbplats och lägre avhoppsfrekvens.

De senaste fördelarna med den senaste funktionen för smart bildbehandling är bland annat följande:

* Stöd för nästa generations AVIF-format.
* PNG till WebP och AVIF har nu stöd för förlustkonvertering. Eftersom PNG är ett icke-förstörande format levererades tidigare WebP och AVIF utan dataförlust.
* [Konvertering av webbläsarformat](#bfc)
* [Enhetens pixelproportioner](#dpr)
* [Nätverksbandbredd](#bandwidth)

### Om konvertering av webbläsarformat {#bfc}

Aktivera konvertering av webbläsarformat genom att lägga till `bfc=on` till bild-URL:en konverterar automatiskt JPEG och PNG till förstörande AVIF, förstörande WebP, förstörande JPEGXR, förstörande JPEG2000 för olika webbläsare. För webbläsare som inte stöder dessa format fortsätter Smart Imaging att fungera som JPEG eller PNG. Tillsammans med formatet beräknas kvaliteten på det nya formatet om med Smart Imaging.

Smart bildbehandling kan även stängas av genom att lägga till `bfc=off` till bildens URL.

Se även [bfc](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-bfc.html?lang=en) i Dynamic Media Image Serving and Rendering API.

### Om optimering av enhetspixelproportioner {#dpr}

Enhetens pixelproportioner (DPR) - även kallat CSS-pixelproportioner - är relationen mellan en enhets fysiska pixlar och logiska pixlar. I synnerhet med nya retinaskärmar växer pixelupplösningen i moderna mobilenheter i snabb takt.

Om du aktiverar optimering av enhetspixelproportioner återges bilden med skärmens ursprungliga upplösning, vilket gör den skarp.

För närvarande kommer pixeldensiteten för visningen från Akamai CDN-rubrikvärden.

| Tillåtna värden i en bilds URL | Beskrivning |
|---|---|
| `dpr=off` | Inaktivera DPR-optimering på URL-nivå för en enskild bild. |
| `dpr=on,dprValue` | Åsidosätt det DPR-värde som identifieras av Smart Imaging, med ett anpassat värde (som identifieras av någon klientlogik eller annan metod). Tillåtet värde för `dprValue` är ett tal som är större än 0. |

>[!NOTE]
>
>* Du kan använda `dpr=on,dprValue` även om företagets nivå DPR-inställning är avstängd.
>* På grund av DPR-optimering identifieras alltid MaxPix-bredden när den resulterande bilden är större än Dynamic Media-inställningen MaxPix genom att bildens proportioner behålls. —>


| Begärd bildstorlek | Enhetspixelproportioner (dpr), värde | Levererad bildstorlek |
|---|---|---|
| 816 x 500 | 1 | 816 x 500 |
| 816 x 500 | 2 | 1632 x 1000 |

Se även [När du arbetar med bilder](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md#when-working-with-images) och [När du arbetar med smart beskärning](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md#when-working-with-smart-crop).

### Om optimering av nätverksbandbredd {#bandwidth}

Om du aktiverar nätverksbandbredd justeras den bildkvalitet som hanteras automatiskt baserat på den faktiska nätverksbandbredden. För dålig nätverksbandbredd inaktiveras DPR-optimering (Device Pixel Ratio) automatiskt, även om den redan är aktiverad.

Om du vill kan ditt företag välja att inte optimera nätverksbandbredden på den enskilda bildnivån genom att lägga till `network=off` till bildens URL.

| Tillåtet värde i URL:en för en bild | Beskrivning |
|---|---|
| `network=off` | Stänger av nätverksoptimering på URL-nivå för en enskild bild. |

DPR- och nätverksbandbreddsvärdena baseras på de värden som identifierats på klientsidan för det paketerade CDN. Dessa värden är ibland felaktiga. Exempel: iPhone5 med DPR=2 och iPhone12 med `dpr=3`, båda visa `dpr=2`. För högupplösta enheter skickas ändå `dpr=2` är bättre än att skicka `dpr=1`. Det bästa sättet att överbrygga denna brist är dock att använda DPR på klientsidan för att ge er helt korrekta värden. Och det fungerar för alla enheter, oavsett om det är Apple eller någon annan enhet som startades. Se [Använd smart bildbehandling med enhetspixelproportioner på klientsidan](/help/assets/dynamic-media/client-side-dpr.md).

**Ytterligare viktiga fördelar med smart bildbehandling**

* Förbättrad Google SEO-rankning för webbsidor som använder den senaste Smart Imaging-funktionen.
* Serverar optimerat innehåll direkt (vid körning).
* Använder Adobe Sensei-teknik för att konvertera enligt kvalitet (`qlt`) som anges i bildbegäran.
* TTL-oberoende (Time To Live). Tidigare var en minsta TTL på 12 timmar obligatorisk för att Smart Imaging skulle fungera.
* Tidigare cachelagrades både original- och härledda bilder, och det var en tvåstegsprocess att göra cacheminnet ogiltigt. I den senaste versionen av Smart Imaging cachelagras bara derivat, vilket möjliggör en cacheogiltigförklaring i ett enda steg.
* Kunder som använder anpassade rubriker i sina regeluppsättningar kan dra nytta av den senaste smarta bildhanteringen eftersom dessa rubriker inte blockeras, till skillnad från den tidigare versionen av Smart Imaging. Exempel:&quot;Timing Allow Origin&quot;,&quot;X-Robot&quot; som föreslås i [Lägg till ett anpassat rubrikvärde i bildsvaren|Dynamic Media Classic](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/add-custom-header-val-image.html).

## Så fungerar Smart Imaging{#how-smart-imaging-works}

När en bild efterfrågas av en konsument kontrollerar Smart Imaging användarens egenskaper och konverterar den till rätt bildformat baserat på den webbläsare som används. Dessa formatkonverteringar görs på ett sätt som inte försämrar den visuella återgivningen. Smart bildbehandling konverterar automatiskt bilder till olika format baserat på webbläsarkapacitet på följande sätt.

* Konvertera automatiskt till AVIF om webbläsaren stöder formatet
* Konvertera automatiskt till WebP om AVIF-konverteringen inte var fördelaktig eller om webbläsaren inte stöder AVIF
* Konvertera automatiskt till JPEG2000 om Safari inte stöder WebP
* Konvertera automatiskt till JPEGXR för IE 9+ eller om Edge inte stöder WebP\
   | Bildformat | Webbläsare som stöds | |—|—| | AVIF | [https://caniuse.com/avif](https://caniuse.com/avif) | | WebP | [https://caniuse.com/webp](https://caniuse.com/webp) | | JPEG 2000 | [https://caniuse.com/jpeg2000](https://caniuse.com/jpeg2000) | | JPEGXR | [https://caniuse.com/jpegxr](https://caniuse.com/jpegxr) |
* För webbläsare som inte stöder dessa format används det bildformat som ursprungligen begärdes.

Om den ursprungliga bildstorleken är mindre än vad Smart Imaging skapar, behålls originalbilden.

## Stöd för bildformat i Smart Imaging{#image-format-support}

Följande bildformat stöds för Smart Imaging:

* JPEG
* PNG

För bildfilformatet JPEG beräknas kvaliteten på det nya formatet om med Smart Imaging.

För bildfilsformat som stöder genomskinlighet som PNG kan du konfigurera Smart Imaging så att AVIF och WebP blir förstörande. För konvertering av förlustgivande format använder Smart Imaging den kvalitet som anges i bildens URL, eller i annat fall den kvalitet som konfigurerats i Dynamic Media företagskonto.

## Stöd för kommandovisning i Smart Imaging{#imaging-serving-command-support}

Kommandona Bild `fmt` och `qlt` stöds inte, alla återstående kommandon stöds.

## Frågor och svar om Smart Imaging{#smart-imaging-faq}

+++**Kostar licensieringen av Smart Imaging?**

Nej. Smart Imaging ingår i din befintliga licens. Den här regeln gäller antingen Dynamic Media Classic eller Experience Manager - Dynamic Media (On-prem, AMS och Experience Manager as a Cloud Service).

>[!IMPORTANT]
>
>Smart Imaging är inte tillgängligt för Dynamic Media - Hybrid-kunder.

+++

+++**Kan Smart Imaging stängas av på begäran?**

Ja. Du kan inaktivera Smart bildbehandling genom att lägga till någon av följande modifierare:

* `bfc=off` om du vill inaktivera konvertering av webbläsarformat. Se även [Konvertering av webbläsarformat](#bfc).
* `dpr=off` för att inaktivera Device Pixel Ratio. Se även [Enhetens pixelproportioner](#dpr).
* `network=off` för att stänga av nätverksbandbredd. Se även [Nätverksbandbredd](#network).

+++

+++**Är det möjligt att&quot;justera&quot; Smart Imaging?**

Ja. Smart bildbehandling har tre alternativ som du kan aktivera eller inaktivera.

* [Konvertering av webbläsarformat](#bfc)
* [Enhetens pixelproportioner](#dpr)
* [Nätverksbandbredd](#network)

+++

+++**Fungerar Smart Imaging med mina befintliga bildförinställningar?**

Ja. Smart Imaging fungerar med dina befintliga bildförinställningar och alla bildinställningar registreras. Vilka ändringar som görs är bildformatet, kvalitetsinställningen eller båda. Vid formatkonvertering bevarar Smart Imaging den fullständiga visuella återgivningen enligt inställningarna för bildförinställningarna, men med en mindre filstorlek.

Anta till exempel att en bildförinställning har definierats med formatet JPEG, storleken 500 x 500, kvaliteten=85 och den oskarpa masken=0.1,1,5. När Smart Imaging upptäcker att en användare använder en Chrome-webbläsare konverteras bilden till WebP-format med storleken 500 x 500. Oskarp mask=0.1,1,5 är i WebP-kvalitet som överensstämmer med JPEG-kvaliteten på 85 så nära som möjligt. Den WebP-konverteringen tar stor plats jämfört med JPEG, och den mindre av båda returneras.

+++

+++**Måste jag ändra URL:er, bildförinställningar eller distribuera ny kod på min webbplats?**

Nej. Smart Imaging fungerar sömlöst med befintliga bild-URL:er och bildförinställningar. Smart Imaging kräver dessutom inte att du lägger till kod på webbplatsen för att identifiera en användares webbläsare. Alla dessa funktioner hanteras automatiskt.

<!-- Smart Imaging works seamlessly with your existing image URLs and image presets if you configure Smart Imaging on your existing custom domain. In addition, Smart Imaging does not require you to add any code on your website to detect a user's browser. It is all handled automatically.

In case you must configure a new custom domain to use Smart Imaging, the URLs must be updated to reflect this custom domain.

To understand pre-requisites for Smart Imaging, see [Am I eligible to use Smart Imaging?](#am-i-eligible-to-use-smart-imaging) -->

<!-- OLD As mentioned earlier, Smart Imaging supports only JPEG and PNG image formats. For other formats, you need to append the `bfc=off` modifier to the URL as described earlier. -->

+++

+++**Fungerar Smart Imaging med HTTPS? Vad sägs om HTTP/2?**

Ja, på båda frågorna. Smart Imaging fungerar med bilder som levereras via HTTP eller HTTPS. Dessutom fungerar det även över HTTP/2.

+++

+++**Är jag berättigad att använda Smart Imaging?**

Det beror på. Om du vill använda Smart Imaging måste ditt företags Dynamic Media Classic- eller Dynamic Media-konto på Experience Manager uppfylla följande krav:

* Använd det Adobe-paketerade CDN (Content Delivery Network) som en del av licensen.
* Använd en dedikerad domän (till exempel `images.company.com` eller `mycompany.scene7.com`), inte en allmän domän (till exempel `s7d1.scene7.com`, `s7d2.scene7.com`, eller `s7d13.scene7.com`).

Om du vill hitta dina domäner öppnar du [Dynamic Media Classic desktop application](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)och logga sedan in på ditt eller dina företagskonton.

Gå till **[!UICONTROL Setup]** > **[!UICONTROL Application Setup]** > **[!UICONTROL General Settings]**. Leta efter fältet med etiketten **[!UICONTROL Published Server Name]**. Om du för närvarande använder en allmän domän kan du begära att få gå över till din egen anpassade domän. Gör den här övergångsbegäran när du skickar in ett supportärende.

Din första anpassade domän kostar inget extra med en Dynamic Media-licens.

+++

+++**Kan jag aktivera Smart Imaging för mitt konto?**

Nej. Du startar en begäran om att använda Smart Imaging; den inte aktiveras automatiskt.

Skapa ett supportärende enligt beskrivningen nedan. I ditt supportfall ska du ange vilken av följande smarta bildredigeringsfunktioner (en eller flera) som du vill ska aktiveras för ditt konto:

* WebP
* AVIF
* Optimering av DPR och nätverksbandbredd
* PNG till AVIF-förstörande eller förstörande WebP

Om du redan har Smart Imaging aktiverat med WebP, men vill ha andra nya funktioner enligt ovan, måste du skapa ett supportärende.

**Så här skapar du ett supportärende för att aktivera Smart Imaging på ditt konto:**

1. [Använd Admin Console för att börja skapa ett nytt supportärende](https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html).
1. Ange följande information i ditt supportärende:

   * Primärt kontaktnamn, e-postadress, telefon.

   * Ange vilka av följande Smart Imaging-funktioner (en eller flera) du vill aktivera på ditt konto:
      * WebP
      * AVIF
      * Optimering av DPR och nätverksbandbredd
      * PNG till AVIF-förstörande eller förstörande WebP
   * Alla domäner som ska aktiveras för Smart Imaging (d.v.s. `images.company.com` eller `mycompany.scene7.com`).

      Om du vill hitta dina domäner öppnar du [Dynamic Media Classic desktop application](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)och logga sedan in på ditt eller dina företagskonton.

      Gå till **[!UICONTROL Setup]** > **[!UICONTROL Application Setup]** > **[!UICONTROL General Settings]**.

      Leta efter fältet med etiketten **[!UICONTROL Published Server Name]**.

   * Kontrollera att du använder CDN via Adobe och inte hanteras med en direkt relation.

   * Verifiera att du använder en dedikerad domän som `images.company.com` eller `mycompany.scene7.com`och inte en allmän domän, som `s7d1.scene7.com`, `s7d2.scene7.com`, `s7d13.scene7.com`.

      Om du vill hitta dina domäner öppnar du [Dynamic Media Classic desktop application](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)och logga sedan in på ditt eller dina företagskonton.

      Gå till **[!UICONTROL Setup]** > **[!UICONTROL Application Setup]** > **[!UICONTROL General Settings]**.

      Leta efter fältet med etiketten **[!UICONTROL Published Server Name]**. Om du för närvarande använder en allmän Dynamic Media Classic-domän kan du begära att du flyttar över till din egen anpassade domän som en del av den här övergången.

   * Ange om du vill att den ska fungera över HTTP/2.


1. Adobe kundsupport lägger till dig i kundväntelistan för Smart Imaging baserat på i vilken ordning begäranden skickas.
1. När Adobe är redo att hantera din begäran kontaktar kundsupporten dig för att koordinera och ange ett måldatum.
1. **Valfritt**: Om du vill kan du testa Smart Imaging i Förproduktion innan Adobe publicerar den nya funktionen.
1. Du meddelas när du är klar av kundsupporten.
1. För att maximera prestandaförbättringarna av Smart Imaging rekommenderar Adobe att TTL (Time To Live) ställs in på 24 timmar eller längre. TTL-värdet definierar hur länge resurser cachas av CDN. Så här ändrar du den här inställningen:

   1. Om du använder Dynamic Media Classic går du till **[!UICONTROL Setup]** > **[!UICONTROL Application Setup]** > **[!UICONTROL Publish Setup]** > **[!UICONTROL Image Server]**. Ange **[!UICONTROL Default Client Cache Time To Live]** värdet är 24 eller längre.
   1. Om du använder Dynamic Media, följ [dessa instruktioner](config-dm.md). Ange **[!UICONTROL Expiration]** 24 timmar eller längre.

+++

+++**När aktiveras mitt konto med Smart Imaging?**

Förfrågningar behandlas i den ordning som de tas emot av kundsupporten, enligt väntelistan.

>[!NOTE]
>
>Det kan ta lång tid att skapa eftersom du måste rensa cacheminnet genom att aktivera Smart Imaging. Därför kan bara ett fåtal kundövergångar hanteras vid en viss tidpunkt.

+++

+++**Finns det några risker med Smart Imaging?**

Det finns ingen risk för kundens webbsida. Övergången till Smart Imaging tar dock bort CDN-cachen. Den här åtgärden innebär att du måste gå till en ny konfiguration av Dynamic Media Classic eller Dynamic Media på Experience Manager.

Under den inledande övergången kommer de icke-cachelagrade bilderna direkt till Adobe origin-servrarna tills cachen återskapas. Adobe planerar därför att hantera ett fåtal kundövergångar i taget så att man behåller godtagbara prestanda när man drar in förfrågningar från ursprungsläget. För de flesta kunder är cacheminnet helt uppbyggt igen på CDN inom cirka en till två dagar.

+++

+++**Kan jag verifiera om Smart Imaging fungerar?**

Ja. Du kan göra följande:

1. När ditt konto har konfigurerats med Smart Imaging läser du in en bild-URL för Dynamic Media Classic eller Adobe Experience Manager - Dynamic Media i webbläsaren.
1. Öppna Chrome-utvecklarfönstret genom att gå till **[!UICONTROL View]** > **[!UICONTROL Developer]** > **[!UICONTROL Developer Tools]** i webbläsaren. Eller välj ett valfritt verktyg för webbläsare.

1. Kontrollera att cache är inaktiverat när utvecklingsverktygen är öppna.

   * I Windows® går du till inställningarna i rutan för utvecklarverktyget och väljer **[!UICONTROL Disable cache (while devtools is open)]** kryssruta.
   * På macOS, i utvecklarfönstret, under **[!UICONTROL Network]** flik, välja **[!UICONTROL disable cache]**.

1. Observera att innehållstypen har omvandlats till lämpligt format. På följande skärmbild visas en PNG-bild som konverteras dynamiskt till WebP i Chrome. Om din domän har AVIF aktiverat kan du även förvänta dig att se AVIF i innehållstypen.
1. Upprepa testet i olika webbläsare och under olika användarförhållanden.

>[!NOTE]
>
>Alla bilder konverteras inte. Smart Imaging avgör om konverteringen kan förbättra prestandan. Ibland konverteras bilden inte om det inte finns någon förväntad prestandaökning eller om formatet inte är JPEG eller PNG.

![image2017-11-14_15398](assets/image2017-11-14_15398.png)

+++

+++**Finns det något sätt att lära sig fördelarna med Smart bildbehandling?**

Ja. Huvudet Smart Imaging avgör fördelarna med Smart Imaging. När Smart Imaging är aktiverat, efter att du har begärt en bild, under **[!UICONTROL Response Headers]** rubrik, du kan se `-X-Adobe-Smart-Imaging` som i följande markerade exempel:

![Rubrik för smart bildbehandling](/help/assets/dynamic-media/assets/smartimagingheader.png)

Den här rubriken innehåller följande information:

* Smart Imaging fungerar för företaget.
* Ett positivt värde innebär att konverteringen lyckas. I det här fallet returneras en ny WebP-bild.
* Ett negativt värde innebär att konverteringen inte lyckas. I så fall returneras den ursprungliga begärda bilden (JPEG som standard, om inget anges).
* Ett positivt värde visar skillnaden i byte mellan den begärda bilden och den nya bilden. I exemplet ovan sparas de sparade byten `75048` eller ungefär 75 kB för en bild.
* Ett negativt värde innebär att den begärda bilden är mindre än den nya bilden. Den negativa storleksskillnaden visas, men bilden som visas är endast den ursprungliga begärda bilden.

>[!NOTE]
>
>**X-Adobe-Smart-Imaging = -1 när WebP levereras**
>
>Om värdet för `X-Adobe-Smart-Imaging` är -1 och WebP levereras fortfarande, vilket betyder att Smart Imaging fungerar, men storleksfördelarna har inte beräknats på grund av gammal cache. Du kan använda `cache=update` (endast en gång) i bildens URL för att åtgärda problemet.
>Ett exempel på hur du använder modifieraren:
>`https://smartimaging.scene7.com/is/image/SmartImaging/sample1?cache=update`
>Om du vill göra hela cachen ogiltig måste du skapa ett supportärende.

+++

+++**Kan jag inaktivera AVIF-optimering i Smart Imaging?**

Ja. Om du vill växla tillbaka till att använda WebP som standard skapar du ett supportärende för det. Som vanligt kan du inaktivera Smart Imaging genom att lägga till parametern `bfc=off` till bildens URL. Du kan dock inte välja WebP eller AVIF i URL-modifieraren för Smart Imaging. Den här möjligheten bibehålls på kontonivån.

+++

+++**Varför misslyckas min begäran när jag har en URL med fmt=tif i webbläsaren Chrome?**

Det här felet inträffar inte om Smart Imaging inte är aktiverat på ditt konto. Smart Imaging fungerar endast med JPEG eller PNG-format.

För att undvika det här felet kan du antingen:

* Ange JPEG eller PNG, eller
* Använd inte `fmt` modifierare alls, eller
* Använd ett webbläsarformat som definieras av Smart Imaging. Du kan till exempel använda WebP för webbläsaren Chrome.

+++

+++**Kan jag hämta en TIFF-bild från en bilds URL?**

Ja. Lägg till `fmt=tif` och `bfc=off` till bildens URL-sökväg.

+++

+++**Hanterar Smart Imaging bildformat och bildkvalitetsinställningar?**

Ja. Smart bildbehandling använder både format och kvalitet. Resten av parametrarna förblir desamma, om det krävs i bildens URL.

+++

+++**Kan jag ange en lägsta och högsta kvalitetsinställning?**

Nej. Det finns för närvarande ingen sådan etablering.

+++

+++**Justerar Smart Imaging inställningen för procentkvalitet?**

Ja. Smart Imaging justerar automatiskt kvalitetsprocenten. Kvalitetsprocenten bestäms med hjälp av en maskininlärningsalgoritm som utvecklats av Adobe. Den här procentandelen är inte intervallspecifik.

+++

+++**Ersätts endast JPEG och PNG med Smart Imaging?**

Ja. Den här funktionen fungerar endast för JPEG och PNG.

+++

+++**Varför återgår JPEG ibland till Chrome istället för till WebP?**

Smart bildbehandling avgör om konverteringen är bra eller inte. Den returnerar bara den nya bilden för konverteringen.

+++

+++**Varför fungerar inte Device Pixel Ratio (dpr) för sammansatta bilder?**

Om en sammansatt bild innehåller för många lager kan dpr-funktionen påverkas när du använder en positionsmodifierare. Problemet är känt och kommer att åtgärdas i framtida versioner av Smart Imaging. Om andra Smart Imaging-funktioner inte fungerar som förväntat kan du skapa ett supportärende för att rapportera problemet.

+++

+++**Varför konverteras Smart Imaging PNG till förlustfri WebP/AVIF?**

Eftersom PNG är ett icke-förstörande format har de tidigare WebP- och AVIF-versionerna som levererades blivit förlustfria, vilket är större än förväntat. Smart Imaging har nu stöd för förlustkonvertering. Du kan använda modifieraren `cache=update` (endast en gång) i en bildbegäran för att åtgärda problemet. Ett exempel på hur den här modifieraren används:

`https://smartimaging.scene7.com/is/image/SmartImaging/sample1?cache=update`

Om du vill göra hela cacheminnet ogiltigt måste du skapa ett supportärende och begära en sådan åtgärd.

+++

+++**Kan jag fortsätta använda PNG för förlustfri konvertering i Smart Imaging?**

Ja. Smart Imaging har nu stöd för förlustkonvertering baserat på kvalitetsnivån. Om du vill fortsätta använda förlustfri konvertering kan du använda 100-kvalitet som är inställd antingen enligt företagets inställning eller via bildens URL med `qlt=100` i banan.

+++



























<!-- ## If Smart Imaging manages the quality settings, are there minimums and maximums I can set? For example, is it possible to set "no lower than 60" and "no greater than 80 quality"? {#minimum-maximum}

There is no such provisioning ability in the current Smart Imaging. -->

<!-- ## Sometimes a JPEG image is returned to Chrome instead of a WebP image. Why does that change happen? {#jpeg-webp}

Smart Imaging determines if the conversion is beneficial or not. It returns the new image only if the conversion results in a smaller file size with comparable quality.

How does Smart Imaging DPR optimization work with Adobe Experience Manager Sites components and Dynamic Media viewers?

* Experience Manager Sites Core Components are configured by default for DPR optimization. To avoid oversized images owing to server-side Smart Imaging DPR optimization, `dpr=off` is always added to Experience Manager Sites Core Components Dynamic Media images.
* Given Dynamic Media Foundation Component is configured by default for DPR optimization, to avoid oversized images owing to server-side Smart Imaging DPR optimization, `dpr=off` is always added to Dynamic Media Foundation Component images. Even if customer deselects DPR optimization in DM Foundation Component, server-side Smart Imaging DPR does not kick in. In summary, in the DM Foundation Component, DPR optimization comes into effect based on DM Foundation Component level setting only.
* Any viewer side DPR optimization works in tandem with server-side Smart Imaging DPR optimization, and does not result in over-sized images. In other words, wherever DPR is handled by the viewer, such as the main view only in a zoom-enabled viewer, the server-side Smart Imaging DPR values are not triggered. Likewise, wherever viewer elements, such as swatches and thumbnails, do not have DPR handling, the server-side Smart Imaging DPR value is triggered.

See also [When working with images](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md#when-working-with-images) and [When working with Smart Crop](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md#when-working-with-smart-crop).

>[!MORELIKETHIS]
>
>* [Image optimization with next generation image formats WebP and AVIF.](https://medium.com/adobetech/image-optimisation-with-next-gen-image-formats-webp-and-avif-248c75afacc4) -->
>
---
title: Dynamic Media bildprofiler
description: Lär dig hur du skapar Dynamic Media-bildprofiler som innehåller inställningar för oskarp mask och smart beskärning eller smarta färgrutor, eller båda. Använd sedan profilen på en mapp med bildresurser.
contentOwner: Rick Brough
feature: Asset Management,Image Profiles,Renditions,Best Practices
role: User
exl-id: 0856f8a1-e0a9-4994-b338-14016d2d67bd
source-git-commit: 0ad506fc72cb73d3a6a8cdd9eee50f213b52665e
workflow-type: tm+mt
source-wordcount: '3372'
ht-degree: 0%

---

# Dynamic Media bildprofiler {#image-profiles}

När du överför bilder kan du beskära bilden automatiskt vid överföring genom att tillämpa en bildprofil på mappen.

>[!IMPORTANT]
>
>Bildprofiler kan inte användas för PDF-, animerade GIF- eller INDD-filer (Adobe InDesign).

## Oskarp mask, alternativ {#unsharp-mask}

När du skapar en bildprofil kan du använda alternativet **[!UICONTROL Unsharp mask]** för att finjustera en skärpefiltereffekt på den slutliga nedsamplade bilden. Du kan styra effektens intensitet, radie (mätt i pixlar) och ett tröskelvärde för kontrast som ignoreras. Den här effekten använder samma alternativ som Adobe Photoshop Oskarp mask-filter.

>[!NOTE]
>
>Den oskarpa masken används bara för nedskalade återgivningar i PTIFF (pyramidformade gånger) som nedsamplas till mer än 50 %. Den oskarpa masken påverkar inte de största återgivningarna i pixeln. Mindre renderingar, till exempel miniatyrbilder, ändras (och visar den oskarpa masken).

I **[!UICONTROL Unsharp Mask]** har du följande filtreringsalternativ:

<table>
 <tbody>
  <tr>
   <td><strong>Alternativ</strong></td>
   <td><strong>Beskrivning</strong></td>
  </tr>
  <tr>
   <td>Belopp</td>
   <td>Styr mängden kontrast som används på kantpixlar. Standardvärdet är 1,75. För högupplösta bilder kan du öka den till upp till 5. Tänk på Mängd som ett mått på filterintensiteten. Intervallet är 0-5.</td>
  </tr>
  <tr>
   <td>Radie</td>
   <td>Anger antalet pixlar runt kantpixlarna som påverkar skärpan. För högupplösta bilder anger du 1 till 2. Med ett lågt värde ökas skärpan endast för kantpixlarna. Med ett högt värde ökas skärpan för ett bredare intervall av pixlar. Vilket värde som är korrekt beror på bildens storlek. Standardvärdet är 0,2. Intervallet är 0-250.</td>
  </tr>
  <tr>
   <td>Tröskelvärde</td>
   <td><p>Anger det kontrastintervall som ska ignoreras när det oskarpa maskfiltret används. Det här alternativet styr hur olika pixlar med skärpa måste vara från omgivningen för att betraktas som kantpixlar. Endast pixlar som uppfyller det här tröskelvärdet skärps. Experimentera med värden mellan 0 och 255 för att undvika brus.</p> </td>
  </tr>
 </tbody>
</table>

Skärpa beskrivs i [Skärpa bilder](/help/assets/dynamic-media/assets/sharpening_images.pdf).

## Beskärningsalternativ {#crop-options}

När du implementerar smart beskärning på bilder rekommenderar Adobe följande bästa praxis och tillämpar följande gräns:

| Resurs - begränsningstyp | Bästa praxis | Begränsning har införts |
| --- | --- | --- |
| **Bild** - antal smarta beskärningar per bild | 5 | 100 |

Se även [Dynamic Media-begränsningar](/help/assets/dynamic-media/limitations.md).

<!-- CQDOC-16069 for the paragraph directly below -->

Smarta beskärningskoordinater är proportionella. För inställningarna för smart beskärning i en bildprofil skickas samma proportioner till Dynamic Media om proportionerna är desamma för de tillagda dimensionerna i bildprofilen. Adobe rekommenderar att du använder samma beskärningsområde. Om du gör det ser du till att de olika måtten som används i bildprofilen inte påverkas.

Varje smart beskärningsgenerering som du skapar kräver extra bearbetning. Om du till exempel lägger till mer än fem proportioner för smart beskärning kan det leda till en långsam intag av resurser. Det kan också ge ökad belastning på systemen. Eftersom smart beskärning kan användas på mappnivå rekommenderar Adobe att endast använda den för mappar där det behövs.

**Riktlinjer för att definiera smart beskärning i en bildprofil**
För att behålla kontrollen över användningen av Smart Crop och för att optimera bearbetningstiden och lagringen av beskärningar rekommenderar Adobe följande riktlinjer och tips:

* Bildresurser som ska ha en smart beskärning måste vara minst 50 x 50 pixlar eller större.
* Helst bör du ha 10-15 smarta beskärningar per bild som optimerar för skärmproportioner och bearbetningstid.
* Namnge smarta beskärningar baserat på beskärningsdimensioner, inte på slutanvändning. På så sätt kan du optimera för dubbletter där en enda dimension används på flera sidor.
* Skapa sidvisa/resurstypsvisa bildprofiler för specifika mappar och undermappar i stället för en gemensam smart beskärningsprofil som tillämpas på alla mappar eller alla resurser.
* En bildprofil som du tillämpar på undermappar åsidosätter en bildprofil som tillämpas på mappen.
* En bildprofil som innehåller duplicerade smarta beskärningsdimensioner tillåts inte.
* Det är inte tillåtet att duplicera namngivna bildprofiler med smarta beskärningsalternativ.

Du kan välja mellan två bildbeskärningsalternativ: pixelbeskärning och smart beskärning. Du kan också välja att automatisera skapandet av färg- och bildfärgrutor eller bevara beskärningsinnehållet i olika upplösningar.

>[!IMPORTANT]
>
>Adobe rekommenderar att du granskar alla genererade beskärningar och färgrutor för att se till att de är lämpliga och relevanta för ert varumärke och era värden.

| Alternativ | När ska du använda | Beskrivning |
| --- | --- | --- |
| **[!UICONTROL Pixel Crop]** | Beskär bilder i grupp endast baserat på dimensioner. | I listrutan **[!UICONTROL Cropping Options]** väljer du **[!UICONTROL Pixel Crop]**.<br>Om du vill beskära från sidorna av en bild anger du antalet pixlar som ska beskäras från valfri sida eller från varje sida av bilden. Hur mycket av bilden som beskärs beror på bildfilens ppi-inställning (pixlar per tum).<br>En bildprofils pixelbeskärning återges på följande sätt:<br> ・ är Överkant, Underkant, Vänster och Höger.<br> ・ uppe till vänster räknas som `0,0` och pixelbeskärningen beräknas därifrån.<br> ・ startpunkt för beskärning: Vänster är X och Överkant är Y<br> ・ Vågrät beräkning: vågrät pixelstorlek för originalbilden minus Vänster och sedan minus Höger.<br> ・ Lodrät beräkning: lodrät pixelhöjd minus Överkant och sedan minus Underkant.<br>Anta till exempel att du har en bild på 4 000 x 3 000 pixlar. Använd värden: Top=250, Bottom=500, Left=300, Right=700.<br>Från övre vänstra (300,250) beskär med fyllningsutrymmet (4000-300-700, 3000-250-500 eller 3000,2250). |
| **[!UICONTROL Smart Crop]** | Massbeskär bilder baserat på deras visuella fokalpunkt. | Smart Crop använder intelligensen i Adobe Sensei för att automatisera beskärningen av bilder snabbt och enkelt. Smart Crop identifierar och beskär automatiskt bilder till fokuspunkten i alla bilder för att uppnå den avsedda intressepunkten, oavsett skärmstorlek.<br>Välj **[!UICONTROL Smart Crop]** i listrutan **[!UICONTROL Cropping Options]** och aktivera sedan funktionen till höger om **[!UICONTROL Responsive Image Crop]**.<br>Standardbrytpunktsstorlekarna (**[!UICONTROL Large]**, **[!UICONTROL Medium]**, **[!UICONTROL Small]**) täcker alla storlekar som används i de flesta bilder på mobila enheter och surfplattor, datorer och banderoller. Om du vill kan du redigera standardnamnen Stora, Medium och Små.<br>Om du vill lägga till fler brytpunkter väljer du **[!UICONTROL Add Crop]**. Om du vill ta bort en beskärning väljer du ikonen Skräpburk. |
| **[!UICONTROL Color and Image Swatch]** | Med Massor genereras en färgruta för varje bild. | **Obs!**: Smarta färgrutor stöds inte i Dynamic Media Classic.<br>Hitta och generera högkvalitativa färgrutor automatiskt från produktbilder som visar färg eller struktur.<br>Välj **[!UICONTROL Smart Crop]** i listrutan **[!UICONTROL Cropping Options]**. Aktivera funktionen till höger om **[!UICONTROL Color and Image Swatch]**. Ange ett pixelvärde i textrutorna **[!UICONTROL Width]** och **[!UICONTROL Height]**.<br>Alla bildbeskärningar är tillgängliga från renderingslisten, men färgrutor används bara med funktionen **[!UICONTROL Copy URL]** . Använd en egen visningskomponent för att återge färgrutan på webbplatsen. Undantaget till den här regeln är Carousel banners. Dynamic Media tillhandahåller visningskomponenten för den färgruta som används i karusellbanderoller.<br><br>**Använda färgrutor för bilder**<br> URL:en för färgrutor för bilder är enkel:<br>`/is/image/company/&lt;asset_name&gt;:Swatch`<br>Där `:Swatch` läggs till i resursbegäran.<br><br>**Använda färgrutor**<br> Om du vill använda färgrutor gör du en `req=userdata`-förfrågan med följande:<br>`/is/image/&lt;company_name&gt;/&lt;swatch_asset_name&gt;:Swatch?req=userdata`<br><br>Följande är till exempel en färgruteresurs i Dynamic Media Classic:<br>`https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch`<br>Och här är färgruteresursens motsvarande `req=userdata` URL:<br>`https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch?req=userdata`<br>Svaret `req=userdata` är följande:<br>`SmartCropDef=Swatch`<br>`SmartCropHeight=200.0`<br>`SmartCropRect=0.421671,0.389815,0.0848564,0.0592593,200,200`<br>`SmartCropType=Swatch`<br>`SmartCropWidth=200.0`<br>`SmartSwatchColor=0xA56DB2`<br>Du kan även begära ett `req=userdata`-svar i antingen XML- eller JSON-format, som i följande: respektive URL-exempel:<br> ・`https://my.company.com</code>:8080/is/image/DemoCo/Sleek:Swatch?req=userdata,json`<br> ・`https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch?req=userdata,xml`<br><br>**Obs!** Du måste skapa en egen WCM-komponent för att begära en färgruta och tolka attributet `SmartSwatchColor` , som representeras av ett 24-bitars RGB hexadecimalt värde.<br>Se även [`userdata`](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/req/r-userdata) i referenshandboken för visningsprogram. |
| **[!UICONTROL Preserve crop content across target resolutions]** | Bevara beskärningsinnehåll i samma proportioner | Använd när du skapar en smart beskärningsprofil.<br>Om du vill generera nytt beskärningsinnehåll - samtidigt som fokalpunkten behålls - för en given proportion i olika upplösningar avmarkerar du det här alternativet <br>Om du avmarkerar den här rutan kontrollerar du att den ursprungliga bildupplösningen är högre än de upplösningar som du anger för den smarta beskärningsprofilen.<br><br>Anta att du har angett proportionerna 600 x 600 (stor), 400 x 400 (Medium) och 300 x 300 (liten).<br>När alternativet **[!UICONTROL Preserve crop content across target resolutions]** är *markerat* ser du samma beskärning i alla tre upplösningarna, som i följande exempelutdata för bilder (endast i illustrativa syften):<br>![Alternativet markerat](/help/assets/dynamic-media/assets/preserve-checked.png)<br><br>När alternativet **[!UICONTROL Preserve crop content across target resolutions]** är *avmarkerat* är beskärningsinnehållet nytt för alla tre upplösningarna, som i följande exempelutdata för bilder (endast i illustrativa syften):<br>![Alternativet avmarkerat ](/help/assets/dynamic-media/assets/preserve-unchecked.png) |

### Bildfilformat som stöds för Smart Beskärning och Färgrutor

Den maximala upplösningen för indatafilens storlek som stöds är 16 kB.

>[!NOTE]
>
>Upplösningen 16K är en skärmupplösning med ungefär 16 000 pixlar vågrätt. Den vanligaste 16K-upplösningen är 1 5360 × 8 640, vilket fördubblar pixelantalet för 8K UHD i varje dimension, vilket ger totalt fyra gånger så många pixlar. Upplösningen har 132,7 megapixlar, 16 gånger så många pixlar som upplösningen 4K och 64 gånger så många pixlar som upplösningen 1080p.

| Bildformat | Skiftlägesokänsligt filtillägg | MIME-typ | Färgrymd för indata som stöds | Största storlek på indatafil som stöds | Bildformat som stöds? |
| --- | --- | --- | --- | --- | --- |
| BMP | `.bmp` | image/bmp | sRGB | 4 GB | Ja |
| CMYK | | | | | Ja |
| EPS | | | | | Nej |
| GIF | `.gif` | image/gif | sRGB | 15 GB | Ja. Den första bildrutan i det animerade GIF används för återgivningen. Du kan inte konfigurera eller ändra den första bildrutan. |
| JPEG | `.jpg` och `.jpeg` | image/jpeg | sRGB | 15 GB | Ja |
| PNG | `.png` | bild/png | sRGB | 15 GB | Ja |
| PSD | `.psd` | image/vnd.adobe.photoshop | sRGB<br>CMYK | 2 GB | Ja |
| SVG | | | | | Nej |
| TIFF | `.tif` och `.tiff` | bild/tiff | sRGB<br>CMYK | 4 GB | Ja |
| WebP/Animerad WebP | | | | | Nej |

## Skapa Dynamic Media-bildprofiler {#creating-image-profiles}

Mer information om hur du definierar avancerade bearbetningsparametrar för andra resurstyper finns i [Konfigurera resursbearbetning](config-dm.md#configuring-asset-processing).

Se [Om Dynamic Media bildprofiler och videoprofiler](/help/assets/dynamic-media/about-image-video-profiles.md).

Se även [Bästa metoder för att ordna din digitala Assets för att använda Bearbeta profiler](/help/assets/organize-assets.md).

**Så här skapar du Dynamic Media-bildprofiler:**

1. Välj Adobe Experience Manager logotyp och gå till **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Image Profiles]**.
1. Om du vill lägga till en bildprofil väljer du **[!UICONTROL Create]**.
1. Ange ett profilnamn och värden för oskarp mask, beskärning eller färgruta, eller båda.

   >[!TIP]
   >
   >Använd ett profilnamn som är specifikt för dess avsedda syfte. Anta till exempel att du vill skapa en profil som bara genererar färgrutor. Smart beskärning är alltså inaktiverat (inaktiverat) och Färg och Bildruta är aktiverat (aktiverat). I så fall kan du använda profilnamnet&quot;Smart färgruta&quot;.

   Se även [Alternativ för smart beskärning och smarta färgrutor](#crop-options) och [Oskarp mask](#unsharp-mask).

   ![beskär](assets/crop.png)

1. Välj **[!UICONTROL Save]**. Den skapade profilen visas i listan med tillgängliga profiler.

## Redigera eller ta bort Dynamic Media bildprofiler {#editing-or-deleting-image-profiles}

1. Markera Experience Manager-logotypen och gå till **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Image Profiles]**.
1. Markera den bildprofil som du vill redigera eller ta bort. Om du vill redigera den väljer du **[!UICONTROL Edit Image Processing Profile]**. Om du vill ta bort den väljer du **[!UICONTROL Delete Image Processing Profile]**.

   ![chlimage_1-254](assets/chlimage_1-254.png)

1. Spara ändringarna om du redigerar dem. Bekräfta att du vill ta bort profilen om du tar bort den.

## Använd en Dynamic Media-bildprofil på mappar {#applying-an-image-profile-to-folders}

När du tilldelar en bildprofil till en mapp ärver alla undermappar automatiskt profilen från den överordnade mappen. Därför kan du bara tilldela en bildprofil till en mapp. Fundera därför noga över mappstrukturen för var du överför, lagrar, använder och arkiverar resurser.

Om du tilldelade en annan bildprofil till en mapp åsidosätter den nya profilen den tidigare profilen. De tidigare befintliga mappresurserna ändras inte. Den nya profilen används för resurser som läggs till i mappen senare.

Mappar med en tilldelad profil visar profilens namn på kortet.

<!-- When you add smart crop to an existing Image Profile, you need to re-trigger the [DAM Update Asset workflow](assets-workflow.md) if you want to generate crops for existing assets in your asset repository. -->

Du kan tillämpa bildprofiler på specifika mappar eller globalt på alla resurser.

Du kan bearbeta resurser i en mapp som redan har en befintlig bildprofil som du senare ändrade. Se [Bearbeta resurser i en mapp igen när du har redigerat dess bearbetningsprofil](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets).

### Använd Dynamic Media-bildprofiler på specifika mappar {#applying-image-profiles-to-specific-folders}

Du kan tillämpa en bildprofil på en mapp från menyn **[!UICONTROL Tools]** eller från **[!UICONTROL Properties]** om du är i mappen.

Mappar med en tilldelad profil visar profilens namn direkt under mappnamnet.

Du kan bearbeta resurser i en mapp som redan har en befintlig videoprofil som du senare ändrade. Se [Bearbeta resurser i en mapp igen när du har redigerat dess bearbetningsprofil](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets).

#### Använd Dynamic Media-bildprofiler på mappar från användargränssnittet för profiler {#applying-image-profiles-to-folders-from-profiles-user-interface}

1. Markera Experience Manager-logotypen och gå till **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Image Profiles]**.
1. Välj den bildprofil som du vill använda för en eller flera mappar.

   ![chlimage_1-255](assets/chlimage_1-255.png)

1. Markera **[!UICONTROL Apply Processing Profile to Folders]** och markera den eller de mappar som du vill använda för att ta emot de nyligen överförda resurserna och välj **[!UICONTROL Apply]**. Mappar med en tilldelad profil visar profilens namn direkt under mappnamnet.

#### Använd Dynamic Media-bildprofiler på mappar från Egenskaper {#applying-image-profiles-to-folders-from-properties}

1. Markera Experience Manager-logotypen och gå till **[!UICONTROL Assets]**.
1. Navigera till en *mapp* (inte en resurs) som du vill tillämpa en bildprofil på.
1. Beroende på vilken vy du befinner dig i gör du något av följande:
   * Håll pekaren över mappen i kortvyn och markera den sedan.
   * Markera kryssrutan till vänster om mappnamnet i kolumnvyn eller listvyn.
1. Välj **[!UICONTROL Properties]** i verktygsfältet.
1. Välj fliken **[!UICONTROL Dynamic Media Processing]**.
1. Under **[!UICONTROL Image Profile]** väljer du den profil som ska användas i listrutan **[!UICONTROL Profile Name]**.
1. Välj **[!UICONTROL Save & Close]** i sidans övre högra hörn. Mappar med en tilldelad profil visar profilens namn direkt under mappnamnet.

   ![chlimage_1-256](assets/chlimage_1-256.png)

### Använd en Dynamic Media-bildprofil globalt {#applying-an-image-profile-globally}

Förutom att tillämpa en profil på en mapp kan du även tillämpa en profil globalt. Den valda profilen används för allt innehåll som överförs till Experience Manager Assets i alla mappar.

Du kan bearbeta resurser i en mapp som redan har en befintlig videoprofil som du senare ändrade. Se [Bearbeta resurser i en mapp igen när du har redigerat dess bearbetningsprofil](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets).

**Så här använder du en Dynamic Media-bildprofil globalt:**

1. Gör något av följande:

   * Navigera till `https://&lt;AEM server&gt;/mnt/overlay/dam/gui/content/assets/foldersharewizard.html/content/dam` och använd rätt profil och välj **[!UICONTROL Save]**.

     ![chlimage_1-257](assets/chlimage_1-257.png)

   * Navigera till CRXDE Lite till följande nod: `/content/dam/jcr:content`.

     Lägg till egenskapen `imageProfile:/conf/global/settings/dam/adminui-extension/imageprofile/<name of image profile>` och välj **[!UICONTROL Save All]**.

     ![configure_image_profiles](assets/configure_image_profiles.png)

## Redigera smart beskärning eller smarta färgrutor för en enskild bild {#editing-the-smart-crop-or-smart-swatch-of-a-single-image}

>[!IMPORTANT]
>
>Adobe rekommenderar att du granskar alla genererade smarta beskärningar och smarta färgrutor för att se till att de är lämpliga och relevanta för ert varumärke och era värden.

Om du vill förfina fokalpunkten i en bild kan du justera justeringen eller ändra storlek på det smarta beskärningsfönstret manuellt.

När du har redigerat en smart beskärning och sparat sprids ändringen överallt där du använder beskärningen för de specifika bilderna.

>[!IMPORTANT]
>
>När du justerar det smarta beskärningsfönstret för en resurs sparas ändringarna. Dessa redigeringar förblir intakta även om du bearbetar om resursen senare. Om du däremot redigerar bredd, höjd eller både och i området **[!UICONTROL Responsive Image Crop]** i bildprofilen kan resursen bearbetas om.
>Se [Bearbeta Dynamic Media-resurser igen i en mapp](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets).

Kör om smart beskärning för att generera ytterligare beskärningar om det behövs.

Se även [Redigera den smarta beskärningen eller den smarta färgrutan för flera bilder](#editing-the-smart-crop-or-smart-swatch-of-multiple-images).

**Så här redigerar du den smarta beskärningen eller den smarta färgrutan för en enskild bild:**

1. Markera Experience Manager-logotypen och navigera till **[!UICONTROL Assets]** och sedan till den mapp där en smart beskärningsbildprofil eller en smart färgrutebildprofil används.
1. Markera mappen om du vill öppna dess innehåll.
1. Markera den bild vars smarta beskärning eller smarta färgruta du vill justera.
1. Välj **[!UICONTROL Smart Crop]** i verktygsfältet.

   >[!TIP]
   >
   >Använd snabbtangenten `s` för att redigera smarta beskärningar eller smarta färgrutor.

1. Gör något av följande:

   * I närheten av det övre högra hörnet av sidan drar du skjutreglaget åt vänster eller höger för att öka respektive minska visningen av bilden.
   * Dra i ett hörnhandtag på bilden för att justera storleken på det visningsbara området för beskärningen eller färgrutan.
   * Dra rutan/färgrutan till en ny plats på bilden. Du kan bara redigera färgrutor. Färgrutor är statiska.
   * I närheten av bildens övre högra hörn väljer du **[!UICONTROL Revert]** om du vill ångra alla redigeringar och återställa den ursprungliga beskärningen eller färgrutan.
   * Använd piltangenterna på tangentbordet för att beskära bildrutestorleken, flytta bilden eller båda.

1. I närheten av sidans övre högra hörn väljer du **[!UICONTROL Save]** och sedan **[!UICONTROL Close]** för att gå tillbaka till resursmappen.

## Redigera smart beskärning eller smart färgruta för flera bilder {#editing-the-smart-crop-or-smart-swatch-of-multiple-images}

>[!IMPORTANT]
>
>Adobe rekommenderar att du granskar alla genererade smarta beskärningar och smarta färgrutor för att se till att de är lämpliga och relevanta för ert varumärke och era värden.

När du har tillämpat en bildprofil, som innehåller smart beskärning, på en mapp tillämpas en beskärning på alla bilder i den mappen. Om det behövs kan du justera fokalpunkterna manuellt eller ändra storlek på det smarta beskärningsfönstret på flera bilder.

När du har redigerat en smart beskärning och sparat sprids ändringen överallt där du använder beskärningen för de specifika bilderna.

>[!IMPORTANT]
>
>När du manuellt justerar det smarta beskärningsfönstret för flera resurser sparas ändringarna. Dessa redigeringar förblir intakta även om du bearbetar om materialet senare. Om du däremot redigerar bredd, höjd eller både och i området **[!UICONTROL Responsive Image Crop]** i bildprofilen, bearbetas dessa resurser om.
>Se [Bearbeta Dynamic Media-resurser igen i en mapp](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets).

Kör om smart beskärning för att generera ytterligare beskärningar om det behövs.

**Så här redigerar du den smarta beskärningen eller den smarta färgrutan för flera bilder:**

1. Markera Experience Manager-logotypen och navigera till **[!UICONTROL Assets]** och sedan till en mapp där en smart beskärningsbildprofil eller en smart färgrutebildprofil används.
1. I mappen väljer du ikonen **[!UICONTROL More Actions]** (..) och sedan **[!UICONTROL Smart Crop]**.

1. Gör något av följande på sidan **[!UICONTROL Edit Smart Crops]**:

   * Justera visningsstorleken för bilder på sidan.

     Dra skjutreglaget åt vänster eller höger till höger om listrutan för brytpunktsnamn om du vill ändra storleken på den visningsbara bilden.

     ![edit_smart_crop-sliderbar](assets/edit_smart_crops-sliderbar.png)

   * Filtrera listan med visningsbara bilder baserat på brytpunktsnamn. I exemplet nedan filtreras bilderna efter brytpunktsnamnet&quot;Medium&quot;.

     I den nedrullningsbara listan i det övre högra hörnet av sidan väljer du ett brytpunktsnamn som du vill filtrera efter vilka bilder du ser. (Se bilden ovan.)

     ![edit_smart_crop-dropdownlist](assets/edit_smart_crops-dropdownlist.png)

   * Ändra storlek på den smarta beskärningsrutan. Gör något av följande:

      * Om bilden har en smart beskärning eller endast en smart färgruta drar du i beskärningsrutans hörnhandtag på bilden. Justera storleken på den visningsbara ytan för beskärningen.
      * Om bilden har både en smart beskärning och en smart färgruta drar du i beskärningsrutans hörnhandtag på bilden. Justera storleken på den visningsbara ytan för beskärningen. Du kan också markera den smarta färgrutan under bilden (färgrutorna är statiska) och sedan dra i beskärningsrutans hörnhandtag. Justera storleken på den visningsbara ytan för färgrutan.

     ![Ändra storlek på smart beskärning för en bild](assets/edit_smart_crops-resize.png).

   * Flytta den smarta beskärningsrutan. Gör något av följande:

      * Om bilden har en smart beskärning eller endast en smart färgruta drar du beskärningsrutan till en ny plats på bilden.
      * Om bilden har både en smart beskärning och en smart färgruta drar du den smarta beskärningsrutan till en ny plats på bilden. Du kan också markera den smarta färgrutan under bilden (färgrutorna är statiska) och sedan dra den smarta färgrutans beskärningsruta till en ny plats.

     ![edit_smart_crop-move](assets/edit_smart_crops-move.png)

   * Ångra alla redigeringar och återställ den ursprungliga smarta beskärningen eller den smarta färgrutan (gäller endast den aktuella redigeringssessionen).

     Välj **[!UICONTROL Revert]** ovanför bilden.

     ![edit_smart_crop-revert](assets/edit_smart_crops-revert.png)

1. I närheten av sidans övre högra hörn väljer du **[!UICONTROL Save]** och sedan **[!UICONTROL Close]** för att gå tillbaka till resursmappen.

## Ta bort en bildprofil från mappar {#removing-an-image-profile-from-folders}

När du tar bort en bildprofil från en mapp ärver alla undermappar automatiskt borttagningen av profilen från den överordnade mappen. All bearbetning av filer som har inträffat i mapparna förblir dock oförändrad.

Du kan ta bort en bildprofil från en mapp från menyn **[!UICONTROL Tools]** eller från **[!UICONTROL Properties]** om du är i mappen.

### Ta bort Dynamic Media Image Profiles från mappar via användargränssnittet Profiles {#removing-image-profiles-from-folders-via-profiles-user-interface}

1. Markera Experience Manager-logotypen och gå till **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Image Profiles]**.
1. Markera den bildprofil som du vill ta bort från en eller flera mappar.
1. Markera **[!UICONTROL Remove Processing Profile from Folders]** och markera den eller de mappar som du vill använda för att ta bort profilen från och välj **[!UICONTROL Remove]**.

   Du kan bekräfta att bildprofilen inte längre används för en mapp eftersom namnet inte längre visas under mappnamnet.

### Ta bort Dynamic Media-bildprofiler från mappar via Egenskaper {#removing-image-profiles-from-folders-via-properties}

1. Markera Experience Manager-logotypen, navigera till **[!UICONTROL Assets]** och sedan till den mapp som du vill ta bort en bildprofil från.
1. Markera kryssmarkeringen för att markera mappen i mappen och välj sedan **[!UICONTROL Properties]**.
1. Välj fliken **[!UICONTROL Image Profiles]**.
1. I listrutan **[!UICONTROL Profile Name]** väljer du **[!UICONTROL None]** och sedan **[!UICONTROL Save & Close]**.

   Mappar med en tilldelad profil visar profilens namn direkt under mappnamnet.

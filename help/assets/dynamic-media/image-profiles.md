---
title: Bildprofiler för Dynamic Media
description: Lär dig hur du skapar Dynamic Media-bildprofiler som innehåller inställningar för oskarp mask och smart beskärning eller smarta färgrutor, eller båda. Använd sedan profilen på en mapp med bildresurser.
feature: Asset Management,Image Profiles,Renditions
role: User
exl-id: 0856f8a1-e0a9-4994-b338-14016d2d67bd
source-git-commit: 8918f7fca967e9c5bd56d9dcbac8fc78648d1941
workflow-type: tm+mt
source-wordcount: '3087'
ht-degree: 5%

---

# Bildprofiler för Dynamic Media {#image-profiles}

När du överför bilder kan du beskära bilden automatiskt vid överföring genom att tillämpa en bildprofil på mappen.

>[!IMPORTANT]
>
>Bildprofiler kan inte användas för PDF-, animerade GIF- eller INDD-filer (Adobe InDesign).

## Oskarp mask, alternativ {#unsharp-mask}

När du skapar en bildprofil kan du använda **[!UICONTROL Unsharp mask]** om du vill finjustera en skärpefiltereffekt på den slutliga nedsamplade bilden. Du kan styra intensiteten för effekten, radien för effekten (mätt i pixlar) och ett tröskelvärde för kontrast som ignoreras. Effekten har samma alternativ som filtret Oskarp mask i Adobe Photoshop.

>[!NOTE]
>
>Oskarp mask används endast för nedskalade återgivningar i PTIFF (pyramidformade gånger) som nedsamplas till mer än 50 %. Det innebär att de största återgivningarna i bilden inte påverkas av oskarp mask. Mindre renderingar, till exempel miniatyrbilder, ändras (och visar den oskarpa masken).

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
   <td>Anger antalet pixlar runt kantpixlarna som påverkar skärpan. För högupplösta bilder anger du 1 till 2. Med ett lågt värde ökas endast kantpixlarna skärpan. ett högt värde ökar skärpan i ett större antal pixlar. Vilket värde som är korrekt beror på bildens storlek. Standardvärdet är 0,2. Intervallet är 0-250.</td>
  </tr>
  <tr>
   <td>Tröskelvärde</td>
   <td><p>Anger det kontrastintervall som ska ignoreras när det oskarpa maskfiltret används. Med andra ord, det här alternativet avgör hur olika de pixlar som ska göras skarpare måste vara från det omgivande området innan de betraktas som kantpixlar och blir skarpare. Experimentera med värden mellan 0 och 255 för att undvika brus.</p> </td>
  </tr>
 </tbody>
</table>

Skärpa beskrivs i [Skärpa bilder](/help/assets/dynamic-media/assets/sharpening_images.pdf).

## Beskärningsalternativ {#crop-options}

<!-- CQDOC-16069 for the paragraph directly below -->

Koordinaterna för smart beskärning är proportionella. För inställningarna för smart beskärning i en bildprofil skickas samma proportioner till Dynamic Media om proportionerna är desamma för de tillagda dimensionerna i bildprofilen. Adobe rekommenderar att du använder samma beskärningsområde. Om du gör det ser du till att de olika måtten som används i bildprofilen inte påverkas.

Varje generering av Smart Crop som du skapar kräver extra bearbetning. Om du till exempel lägger till fler än fem proportioner för smart beskärning kan det leda till en långsam intag av resurser. Det kan också ge ökad belastning på systemen. Eftersom du kan använda SmartCrop på mappnivå rekommenderar Adobe att du använder det på mappar *endast* där det behövs.

Du kan välja mellan två bildbeskärningsalternativ. Du kan också välja att automatisera skapandet av färg- och bildfärgrutor eller bevara beskärningsinnehållet i olika upplösningar.

>[!IMPORTANT]
>
>Adobe rekommenderar att du granskar alla genererade beskärningar och färgrutor för att se till att de är lämpliga och relevanta för ert varumärke och era värden.

| Alternativ | När ska användas | Beskrivning |
| --- | --- | --- |
| **[!UICONTROL Pixel Crop]** | Beskär bilder i grupp endast baserat på dimensioner. | I listrutan **[!UICONTROL Cropping Options]** väljer du **[!UICONTROL Pixel Crop]**.<br>Om du vill beskära från sidorna av en bild anger du antalet pixlar som ska beskäras från valfri sida eller från varje sida av bilden. Hur mycket av bilden som beskärs beror på bildfilens ppi-inställning (pixlar per tum).<br>Pixelbeskärning i en bildprofil återges på följande sätt:<br>・ Värdena är Överkant, Underkant, Vänster och Höger.<br>・ Övre vänster beaktas `0,0` och pixelbeskärningen beräknas därifrån.<br>・ Startpunkt för beskärning: Vänster är X och Överkant är Y<br>・ Vågrät beräkning: vågrät pixelstorlek för originalbilden minus vänster och sedan minus höger.<br>・ Lodrät beräkning: vertikal pixelhöjd minus överkant och sedan minus underkant.<br>Anta till exempel att du har en bild på 4 000 x 3 000 pixlar. Du använder värden: Top=250, Bottom=500, Left=300, Right=700.<br>Från övre vänstra (300,250) beskär med fyllningsutrymmet (4000-300-700, 3000-250-500 eller 3000,2250). |
| **[!UICONTROL Smart Crop]** | Massbeskär bilder baserat på deras visuella fokalpunkt. | Smart Crop använder intelligensen i Adobe Sensei för att snabbt automatisera beskärningen av bilder i bulk. Smart Crop identifierar och beskär automatiskt bilder till fokuspunkten i alla bilder för att uppnå den avsedda intressepunkten, oavsett skärmstorlek.<br>Från **[!UICONTROL Cropping Options]** nedrullningsbar lista, välja **[!UICONTROL Smart Crop]**, sedan till höger om **[!UICONTROL Responsive Image Crop]**, aktivera (aktivera) funktionen.<br>Standardbrytpunktsstorlekar (**[!UICONTROL Large]**, **[!UICONTROL Medium]**, **[!UICONTROL Small]**) täcker hela det spektrum av storlekar som de flesta bilder används för på mobiler och surfplattor, datorer och banners. Om du vill kan du redigera standardnamnen för Stor, Medel och Liten.<br>Om du vill lägga till fler brytpunkter väljer du **[!UICONTROL Add Crop]**; Om du vill ta bort en beskärning väljer du ikonen Skräpburk. |
| **[!UICONTROL Color and Image Swatch]** | Med Massor genereras en färgruta för varje bild. | **Anteckning**: Smarta färgrutor stöds inte i Dynamic Media Classic.<br>Hitta och generera högkvalitativa färgrutor automatiskt från produktbilder som visar färg eller textur.<br>I listrutan **[!UICONTROL Cropping Options]** väljer du **[!UICONTROL Smart Crop]**. Sedan till höger om **[!UICONTROL Color and Image Swatch]**, aktivera (aktivera) funktionen. Ange ett pixelvärde i dialogrutan **[!UICONTROL Width]** och **[!UICONTROL Height]** textrutor.<br>Alla bildbeskärningar är tillgängliga från renderingslisten, men färgrutor används bara via **[!UICONTROL Copy URL]** -funktion. Använd en egen visningskomponent för att återge färgrutan på webbplatsen. Undantaget till den här regeln är Carousel banners. Dynamic Media tillhandahåller visningskomponenten för den färgruta som används i karusellbanderoller.<br><br>**Använda färgrutor**<br> URL:en för färgrutor är enkel:<br>`/is/image/company/&lt;asset_name&gt;:Swatch`<br>Plats `:Swatch` läggs till i resursbegäran.<br><br>**Använda färgrutor**<br> Om du vill använda färgrutor skapar du en `req=userdata` begäran med följande:<br>`/is/image/&lt;company_name&gt;/&lt;swatch_asset_name&gt;:Swatch?req=userdata`<br><br>Följande är till exempel en färgruteresurs i Dynamic Media Classic:<br>`https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch`<br>Och här motsvarar färgruteresursen `req=userdata` URL:<br>`https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch?req=userdata`<br>The `req=userdata` Svaret är följande:<br>`SmartCropDef=Swatch`<br>`SmartCropHeight=200.0`<br>`SmartCropRect=0.421671,0.389815,0.0848564,0.0592593,200,200`<br>`SmartCropType=Swatch`<br>`SmartCropWidth=200.0`<br>`SmartSwatchColor=0xA56DB2`<br>Du kan också begära en `req=userdata` svar i antingen XML- eller JSON-format, som i följande URL-exempel:<br>・`https://my.company.com</code>:8080/is/image/DemoCo/Sleek:Swatch?req=userdata,json`<br>・`https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch?req=userdata,xml`<br><br>**Anteckning**: Du måste skapa en egen WCM-komponent för att begära en färgruta och tolka `SmartSwatchColor` -attribut, som representeras av ett 24-bitars RGB hexadecimalt värde.<br>Se även [`userdata`](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/req/r-userdata.html) i referenshandboken för visningsprogrammen. |
| **[!UICONTROL Preserve crop content across target resolutions]** | Bevara beskärningsinnehåll i samma proportioner | Använd när du skapar en smart beskärningsprofil.<br>Om du avmarkerar den här rutan genereras nytt beskärningsinnehåll, samtidigt som fokalpunkten behålls, för en given proportion i olika upplösningar.<br>Om du vill avmarkera den här rutan kontrollerar du att den ursprungliga bildupplösningen är högre än de upplösningar som du anger för profilen för smart beskärning.<br><br>Anta att du har angett proportionerna 600 x 600 (stor), 400 x 400 (medel) och 300 x 300 (liten). <br>Med **[!UICONTROL Preserve crop content across target resolutions]** option *checked* skulle du se samma beskärning i alla tre upplösningarna, vilket resulterar i följande exempelutdata av bilder (endast i illustrationssyfte):<br>![Alternativet är markerat](/help/assets/dynamic-media/assets/preserve-checked.png)<br><br>Med **[!UICONTROL Preserve crop content across target resolutions]** option *avmarkerad*, är beskärningsinnehållet nytt för alla tre upplösningar, vilket ger följande exempelutdata av bilder (endast i illustrationssyfte):<br>![Alternativet är avmarkerat](/help/assets/dynamic-media/assets/preserve-unchecked.png) |

### Bildfilformat som stöds för Smart Beskärning och Färgrutor

Den maximala upplösningen för indatafilens storlek som stöds är 16 kB.

| Bildformat | Skiftlägesokänsligt filtillägg | MIME-typ | Färgrymd för indata som stöds | Största tillåtna indatafilstorlek | Bildformat som stöds? |
| --- | --- | --- | --- | --- | --- |
| BMP | `.bmp` | image/bmp | sRGB | 4 GB | Ja |
| EPS |  |  |  |  | Nej |
| GIF | `.gif` | image/gif | sRGB | 15 GB | Ja, den första bildrutan i det animerade GIF används för återgivningen. Du kan inte konfigurera eller ändra den första bildrutan. |
| JPEG | `.jpg` and `.jpeg` | image/jpeg | sRGB | 15 GB | Ja |
| PNG | `.png` | bild/png | sRGB | 15 GB | Ja |
| PSD | `.psd` | image/vnd.adobe.photoshop | sRGB<br>CMYK | 2 GB | Ja |
| SVG |  |  |  |  | Nej |
| TIFF | `.tif` och `.tiff` | bild/tiff | sRGB<br>CMYK | 4 GB | Ja |
| WebP/Animerad WebP |  |  |  |  | Nej |

## Skapa Dynamic Media-bildprofiler {#creating-image-profiles}

Mer information om hur du definierar avancerade bearbetningsparametrar för andra resurstyper finns i [Konfigurerar resursbearbetning](config-dm.md#configuring-asset-processing).

Se [Om Dynamic Media bildprofiler och videoprofiler](/help/assets/dynamic-media/about-image-video-profiles.md).

Se även [Bästa metoderna för att ordna dina digitala resurser så att du kan använda Bearbeta profiler](/help/assets/organize-assets.md).

**Så här skapar du Dynamic Media-bildprofiler:**

1. Välj Adobe Experience Manager logotyp och navigera till **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Image Profiles]**.
1. Om du vill lägga till en bildprofil väljer du **[!UICONTROL Create]**.
1. Ange ett profilnamn och värden för oskarp mask, beskärning eller färgruta, eller båda.

   Tips: Använd ett profilnamn som är specifikt för dess avsedda syfte. Anta till exempel att du vill skapa en profil som bara genererar färgrutor. Smart beskärning är alltså inaktiverat (inaktiverat) och Färg och Bildruta är aktiverat (aktiverat). I så fall kan du använda profilnamnet&quot;Smarta färgrutor&quot;.

   Se även [Alternativ för smart beskärning och smarta färgrutor](#crop-options) och [Oskarp mask](#unsharp-mask).

   ![beskära](assets/crop.png)

1. Välj **[!UICONTROL Save]**. Den nya profilen visas i listan med tillgängliga profiler.

## Redigera eller ta bort Dynamic Media bildprofiler {#editing-or-deleting-image-profiles}

1. Markera logotypen för Experience Manager och navigera till **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Image Profiles]**.
1. Markera den bildprofil som du vill redigera eller ta bort. Om du vill redigera den väljer du **[!UICONTROL Edit Image Processing Profile]**. Om du vill ta bort den väljer du **[!UICONTROL Delete Image Processing Profile]**.

   ![chlimage_1-254](assets/chlimage_1-254.png)

1. Spara ändringarna om du redigerar dem. Bekräfta att du vill ta bort profilen om du tar bort den.

## Använd en Dynamic Media-bildprofil på mappar {#applying-an-image-profile-to-folders}

När du tilldelar en bildprofil till en mapp ärver alla undermappar automatiskt profilen från den överordnade mappen. Därför kan du bara tilldela en bildprofil till en mapp. Fundera därför noga över mappstrukturen för var du överför, lagrar, använder och arkiverar resurser.

Om du har tilldelat en annan bildprofil till en mapp åsidosätter den nya profilen den tidigare profilen. De tidigare befintliga mappresurserna ändras inte. Den nya profilen används för resurser som läggs till i mappen senare.

Mappar som har tilldelats en profil visas i användargränssnittet med namnet på profilen som visas på kortet.

<!-- When you add smart crop to an existing Image Profile, you need to re-trigger the [DAM Update Asset workflow](assets-workflow.md) if you want to generate crops for existing assets in your asset repository. -->

Du kan tillämpa bildprofiler på specifika mappar eller globalt på alla resurser.

Du kan bearbeta resurser i en mapp som redan har en befintlig bildprofil som du senare ändrade. Se [Bearbeta resurser i en mapp igen när du har redigerat dess bearbetningsprofil](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets).

### Använd Dynamic Media-bildprofiler på specifika mappar {#applying-image-profiles-to-specific-folders}

Du kan tillämpa en bildprofil på en mapp inifrån **[!UICONTROL Tools]** eller om du är i mappen, från **[!UICONTROL Properties]**.

För mappar som redan har tilldelats en profil visas profilens namn direkt under mappnamnet.

Du kan bearbeta resurser i en mapp som redan har en befintlig videoprofil som du senare ändrade. Se [Bearbeta resurser i en mapp igen när du har redigerat dess bearbetningsprofil](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets).

#### Använd Dynamic Media-bildprofiler på mappar från användargränssnittet för profiler {#applying-image-profiles-to-folders-from-profiles-user-interface}

1. Markera logotypen för Experience Manager och navigera till **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Image Profiles]**.
1. Välj den bildprofil som du vill använda för en eller flera mappar.

   ![chlimage_1-255](assets/chlimage_1-255.png)

1. Välj **[!UICONTROL Apply Processing Profile to Folders]** och markera den eller de mappar som du vill använda för att ta emot de nyligen överförda resurserna och markera **[!UICONTROL Apply]**. För mappar som redan har tilldelats en profil visas profilens namn direkt under mappnamnet.

#### Använd Dynamic Media-bildprofiler på mappar från Egenskaper {#applying-image-profiles-to-folders-from-properties}

1. Tryck på Experience Manager-logotypen och navigera till **[!UICONTROL Assets]**.
1. Navigera till en *mapp* (inte en resurs) som du vill använda en bildprofil på.
1. Beroende på vilken vy du befinner dig i gör du något av följande:
   * Håll pekaren över mappen i kortvyn och markera den sedan.
   * Markera kryssrutan till vänster om mappnamnet i kolumnvyn eller listvyn.
1. I verktygsfältet väljer du **[!UICONTROL Properties]**.
1. Välj **[!UICONTROL Dynamic Media Processing]** -fliken.
1. Under **[!UICONTROL Image Profile]**, från **[!UICONTROL Profile Name]** väljer du den profil som ska användas.
1. I sidans övre högra hörn väljer du **[!UICONTROL Save & Close]**. För mappar som redan har tilldelats en profil visas profilens namn direkt under mappnamnet.

   ![chlimage_1-256](assets/chlimage_1-256.png)

### Använd en Dynamic Media-bildprofil globalt {#applying-an-image-profile-globally}

Förutom att tillämpa en profil på en mapp kan du även tillämpa en profil globalt. Den valda profilen används för allt innehåll som överförs till Experience Manager Assets i alla mappar.

Du kan bearbeta resurser i en mapp som redan har en befintlig videoprofil som du senare ändrade. Se [Bearbeta resurser i en mapp igen när du har redigerat dess bearbetningsprofil](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets).

**Så här använder du en Dynamic Media-bildprofil globalt:**

1. Gör något av följande:

   * Navigera till `https://&lt;AEM server&gt;/mnt/overlay/dam/gui/content/assets/foldersharewizard.html/content/dam` och använda rätt profil och välja **[!UICONTROL Save]**.

      ![chlimage_1-257](assets/chlimage_1-257.png)

   * Navigera till CRXDE Lite till följande nod: `/content/dam/jcr:content`.

      Lägg till egenskapen `imageProfile:/conf/global/settings/dam/adminui-extension/imageprofile/<name of image profile>` och markera **[!UICONTROL Save All]**.

      ![configure_image_profiles](assets/configure_image_profiles.png)

## Redigera smart beskärning eller smarta färgrutor för en enskild bild {#editing-the-smart-crop-or-smart-swatch-of-a-single-image}

>[!IMPORTANT]
>
>Adobe rekommenderar att du granskar alla genererade smarta beskärningar och smarta färgrutor för att se till att de är lämpliga och relevanta för ert varumärke och era värden.

Du kan justera eller ändra storlek på bildens smarta beskärningsfönster manuellt för att ytterligare förfina fokalpunkten.

När du har redigerat en smart beskärning och sparat sprids ändringen överallt där du använder beskärningen för de specifika bilderna.

>[!IMPORTANT]
>
>När du manuellt justerar eller ändrar storlek på det smarta beskärningsfönstret för en resurs bevaras och bevaras redigeringen, även om du senare bestämmer dig för att bearbeta resursen. Om du däremot redigerar bredden, höjden eller både och i **[!UICONTROL Responsive Image Crop]** i bildprofilen. Resursen bearbetas.
>Se [Bearbeta Dynamic Media-resurser igen i en mapp](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets).

Du kan vid behov köra smart beskärning igen för att generera ytterligare beskärningar.

Se även [Redigera smart beskärning eller smart färgruta för flera bilder](#editing-the-smart-crop-or-smart-swatch-of-multiple-images).

**Så här redigerar du den smarta beskärningen eller smarta färgrutan för en enskild bild:**

1. Markera logotypen för Experience Manager och navigera till **[!UICONTROL Assets]** till den mapp där en smart beskärning eller en smart färgrutebildprofil används.
1. Markera mappen om du vill öppna dess innehåll.
1. Markera den bild vars smarta beskärning eller smarta färgruta du vill justera.
1. Välj **[!UICONTROL Smart Crop]**.

1. Gör något av följande:

   * I närheten av det övre högra hörnet av sidan drar du skjutreglaget åt vänster eller höger för att öka respektive minska visningen av bilden.
   * Dra i ett hörnhandtag på bilden för att justera storleken på det visningsbara området för beskärningen eller färgrutan.
   * Dra rutan/färgrutan till en ny plats på bilden. Du kan bara redigera färgrutor för bilder; färgrutor är statiska.
   * Markera ovanför bilden  **[!UICONTROL Revert]** om du vill ångra alla redigeringar och återställa den ursprungliga beskärningen eller färgrutan.
   * Använd piltangenterna på tangentbordet för att beskära bildrutestorleken, flytta bilden eller båda.

1. I sidans övre högra hörn väljer du **[!UICONTROL Save]** väljer **[!UICONTROL Close]** för att återgå till resursmappen.

## Redigera smart beskärning eller smart färgruta för flera bilder {#editing-the-smart-crop-or-smart-swatch-of-multiple-images}

När du har tillämpat en bildprofil - som innehåller smart beskärning - på en mapp tillämpas en beskärning på alla bilder i den mappen. Om du vill kan du *manuellt* justera om eller ändra storlek på det smarta beskärningsfönstret i flera bilder för att ytterligare förfina fokalpunkten.

När du har redigerat en smart beskärning och sparat sprids ändringen överallt där du använder beskärningen för de specifika bilderna.

>[!IMPORTANT]
>
>När du manuellt justerar om eller ändrar storlek på det smarta beskärningsfönstret för flera resurser bevaras och bevaras redigeringarna, även om du senare bestämmer dig för att bearbeta om dessa resurser. Om du däremot redigerar bredden, höjden eller både och i **[!UICONTROL Responsive Image Crop]** i bildprofilen, bearbetas dessa resurser.
>Se [Bearbeta Dynamic Media-resurser igen i en mapp](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets).

Du kan vid behov köra smart beskärning igen för att generera ytterligare beskärningar.

**Så här redigerar du den smarta beskärningen eller smarta färgrutan för flera bilder:**

1. Markera logotypen för Experience Manager och navigera till **[!UICONTROL Assets]** till en mapp där en bildprofil för en smart beskärning eller en smart färgruta används.
1. I mappen väljer du **[!UICONTROL More Actions]** (...), ikon och välj **[!UICONTROL Smart Crop]**.

1. På **[!UICONTROL Edit Smart Crops]** gör du något av följande:

   * Justera visningsstorleken för bilder på sidan.

      Dra skjutreglaget åt vänster eller höger till höger om listrutan för brytpunktsnamn för att ändra storleken på den visningsbara bilden.

      ![edit_smart_crop-sliderbar](assets/edit_smart_crops-sliderbar.png)

   * Filtrera listan med visningsbara bilder baserat på brytpunktsnamn. I exemplet nedan filtreras bilderna efter brytpunktsnamnet&quot;Medium&quot;.

      I den nedrullningsbara listan i det övre högra hörnet av sidan väljer du ett brytpunktsnamn som du vill filtrera efter vilka bilder du ser. (Se bilden ovan.)

      ![edit_smart_crop-dropdownlist](assets/edit_smart_crops-dropdownlist.png)

   * Ändra storlek på den smarta beskärningsrutan. Gör något av följande:

      * Om bilden har en smart beskärning eller endast en smart färgruta drar du i beskärningsrutans hörnhandtag på bilden. Justera storleken på den visningsbara ytan för beskärningen.
      * Om bilden har både en smart beskärning och en smart färgruta drar du i beskärningsrutans hörnhandtag på bilden. Justera storleken på den visningsbara ytan för beskärningen. Du kan också markera den smarta färgrutan under bilden (färgrutorna är statiska) och sedan dra i beskärningsrutans hörnhandtag. Justera storleken på den visningsbara ytan för färgrutan.

      ![Ändra storlek på smart beskärning i en bild](assets/edit_smart_crops-resize.png).

   * Flytta den smarta beskärningsrutan. Gör något av följande:

      * Om bilden har en smart beskärning eller endast en smart färgruta drar du beskärningsrutan till en ny plats på bilden.
      * Om bilden har både en smart beskärning och en smart färgruta drar du den smarta beskärningsrutan till en ny plats på bilden. Du kan också markera den smarta färgrutan under bilden (färgrutorna är statiska) och sedan dra den smarta färgrutans beskärningsruta till en ny plats.

      ![edit_smart_crop-move](assets/edit_smart_crops-move.png)

   * Ångra alla redigeringar och återställ den ursprungliga smarta beskärningen eller den smarta färgrutan (gäller endast den aktuella redigeringssessionen).

      Välj **[!UICONTROL Revert]** ovanför bilden.

      ![edit_smart_crop-revert](assets/edit_smart_crops-revert.png)



1. I sidans övre högra hörn väljer du **[!UICONTROL Save]** väljer **[!UICONTROL Close]** för att återgå till resursmappen.

## Ta bort en bildprofil från mappar {#removing-an-image-profile-from-folders}

När du tar bort en bildprofil från en mapp ärver alla undermappar automatiskt borttagningen av profilen från den överordnade mappen. All bearbetning av filer som har inträffat i mapparna förblir dock oförändrad.

Du kan ta bort en bildprofil från en mapp i **[!UICONTROL Tools]** eller om du är i mappen, från **[!UICONTROL Properties]**.

### Ta bort Dynamic Media Image Profiles från mappar via användargränssnittet Profiles {#removing-image-profiles-from-folders-via-profiles-user-interface}

1. Markera logotypen för Experience Manager och navigera till **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Image Profiles]**.
1. Markera den bildprofil som du vill ta bort från en eller flera mappar.
1. Välj **[!UICONTROL Remove Processing Profile from Folders]** och markera den eller de mappar som du vill använda för att ta bort profilen från och markera **[!UICONTROL Remove]**.

   Du kan bekräfta att bildprofilen inte längre används för en mapp eftersom namnet inte längre visas under mappnamnet.

### Ta bort Dynamic Media-bildprofiler från mappar via Egenskaper {#removing-image-profiles-from-folders-via-properties}

1. Markera Experience Manager-logotypen och navigera **[!UICONTROL Assets]** och sedan till mappen som du vill ta bort en bildprofil från.
1. Markera den markerade mappen genom att markera den och markera sedan **[!UICONTROL Properties]**.
1. Välj **[!UICONTROL Image Profiles]** -fliken.
1. Från **[!UICONTROL Profile Name]** nedrullningsbar lista, välja **[!UICONTROL None]** väljer **[!UICONTROL Save & Close]**.

   För mappar som redan har tilldelats en profil visas profilens namn direkt under mappnamnet.

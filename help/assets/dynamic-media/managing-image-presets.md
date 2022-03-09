---
title: Hantera bildförinställningar
description: Lär dig mer om bildförinställningar och hur du skapar, ändrar och hanterar bildförinställningar.
feature: Image Presets,Viewers,Renditions
role: User
exl-id: a53f40ab-0e27-45f8-9142-781c077a04cc
source-git-commit: 77f1b744dabd72fc26d3b0607db9561e6cb7fa66
workflow-type: tm+mt
source-wordcount: '3499'
ht-degree: 7%

---

# Hantera bildförinställningar{#managing-image-presets}

Med bildförinställningar kan Adobe Experience Manager Assets dynamiskt leverera bilder i olika storlekar, i olika format eller med andra bildegenskaper som genereras dynamiskt. Varje bildförinställning representerar en fördefinierad samling kommandon för storleksändring och formatering för visning av bilder. När du skapar en bildförinställning väljer du en storlek för bildleverans. Du kan också välja formateringskommandon så att bildens utseende optimeras när bilden levereras för visning.

Administratörer kan skapa förinställningar för att exportera resurser. Användarna kan välja en förinställning när de exporterar bilder, vilket även innebär att bilderna formateras om enligt de specifikationer som administratören anger.

Du kan också skapa bildförinställningar som är responsiva. Om du använder en responsiv bildförinställning på dina resurser ändras de beroende på vilken enhet eller skärmstorlek de visas på. Du kan konfigurera bildförinställningar så att de använder CMYK i färgmodellen, förutom RGB eller Grå.

I det här avsnittet beskrivs hur du skapar, ändrar och i allmänhet hanterar bildförinställningar. Du kan använda en bildförinställning på en bild när du vill förhandsvisa den. Se [Använd bildförinställningar](/help/assets/dynamic-media/image-presets.md).

>[!NOTE]
>
>Smart bildbehandling fungerar med befintliga bildförinställningar och använder intelligens under de sista millisekunderna i leveransen för att ytterligare minska bildfilens storlek baserat på webbläsarens eller nätverkets anslutningshastighet. Se [Smart bildbehandling](/help/assets/dynamic-media/imaging-faq.md) för mer information.

## Läs mer om bildförinställningar {#understanding-image-presets}

Precis som ett makro är en bildförinställning en fördefinierad samling kommandon för storleksändring och formatering som sparats under ett namn. Anta att webbplatsen kräver att varje produktbild visas i olika storlekar, olika format och komprimeringsgrader för datorer och mobila enheter för att du ska förstå hur bildförinställningar fungerar.

Du kan skapa två bildförinställningar: en med 500 x 500 pixlar för skrivbordsversionen och 150 x 150 pixlar för den mobila versionen. Du skapar två bildförinställningar, en som kallas `Enlarge` för att visa bilder med 500 x 500 pixlar och en som anropas `Thumbnail` om du vill visa bilder med 150 x 150 pixlar. Leverera bilder på `Enlarge` och `Thumbnail` storlek hittar Experience Manager definitionen av förinställningen Förstora bild och miniatyrbildens förinställning. Sedan genererar Experience Manager dynamiskt en bild med samma storlek och formateringsspecifikationer som varje bildförinställning.

Bilder som minskar i storlek när de levereras dynamiskt kan förlora i skärpa och detaljer. Därför innehåller varje bildförinställning formateringskontroller för optimering av en bild när den levereras i en viss storlek. Med dessa kontroller kan du vara säker på att dina bilder är skarpa och tydliga när de levereras till din webbplats eller ditt program.

Administratörer kan skapa bildförinställningar. Om du vill skapa en bildförinställning kan du börja från början eller så kan du börja från en befintlig förinställning och spara den under ett nytt namn.

## Hantera bildförinställningar {#managing-image-presets-1}

Du hanterar dina bildförinställningar i Experience Manager genom att välja Experience Manager-logotypen för att komma åt den globala navigeringskonsolen och sedan välja verktygsikonen och navigera till **[!UICONTROL Assets]** > **[!UICONTROL Image Presets]**.

![6_5_tools-assets-imageppresets](assets/6_5_tools-assets-imagepresets.png)

>[!NOTE]
>
>Alla bildförinställningar som du skapar är också tillgängliga som dynamiska återgivningar när du förhandsvisar eller levererar resurser.
>
>Det gör du *not* måste publicera bildförinställningar när bildförinställningar publiceras automatiskt.
>
>Se [Publicera bildförinställningar](#publishing-image-presets).

>[!NOTE]
>
>Systemet visar olika återgivningar när du väljer **[!UICONTROL Renditions]** i en tillgångs detaljvy. Du kan öka eller minska antalet bildförinställningar som visas. Se [Öka antalet bildförinställningar som visas](#increasing-or-decreasing-the-number-of-image-presets-that-display).

### Adobe Illustrator (AI), PostScript® (EPS) och PDF {#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats}

Om du tänker ge stöd för att lägga in AI-, EPS- och PDF-filer så att du kan generera dynamiska återgivningar av dessa filformat bör du granska följande information innan du skapar bildförinställningar.

Adobe Illustrator filformat är en variant av PDF. De största skillnaderna när det gäller Experience Manager Assets är följande:

* Adobe Illustrator-dokument består av en sida med flera lager. Varje lager extraheras som en PNG-delresurs under Illustrator huvudresurs.
* PDF-dokument består av en eller flera sidor. Varje sida extraheras som en enda PDF-delresurs under det huvudsakliga flersidiga PDF-dokumentet.

Delresurserna skapas av `Create Sub Asset process` -komponenten inom det övergripande `DAM Update Asset` arbetsflöde. Om du vill se den här processkomponenten i arbetsflödet går du till **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]** > **[!UICONTROL DAM Update Asset]** > **[!UICONTROL Edit]**.

<!-- See also [Viewing pages of a multi-page file](/help/assets/manage-linked-subassets.md#view-pages-of-a-multi-page-file). -->

Du kan visa delresurserna eller sidorna när du öppnar resursen, välja Innehåll-menyn och välja **[!UICONTROL Subassets]** eller **[!UICONTROL Pages]**. Deltillgångarna är verkliga tillgångar. PDF sidor extraheras med andra ord av `Create Sub Asset` arbetsflödeskomponent. De lagras sedan som `page1.pdf`, `page2.pdf`och så vidare, under huvudtillgången. När de är lagrade `DAM Update Asset` arbetsflödet behandlar dem.

Om du vill använda Dynamic Media för att förhandsgranska och generera dynamiska renderingar för AI-, EPS- eller PDF-filer måste du utföra följande steg:

1. I `DAM Update Asset` arbetsflöde, `Rasterize PDF/AI Image Preview Rendition` processkomponenten rastrerar den första sidan i den ursprungliga resursen - med den konfigurerade upplösningen - till en `cqdam.preview.png` återgivning.

1. The `cqdam.preview.png` återgivningen optimeras sedan till en PTIFF-fil med `Dynamic Media Process Image Assets` -processens komponent i arbetsflödet.

>[!NOTE]
>
>I arbetsflödet för DAM-uppdatering av resurser genererar steget **[!UICONTROL EPS thumbnails]** miniatyrer för EPS-filer.

#### PDF/AI/EPS-metadataegenskaper för objekt {#pdf-ai-eps-asset-metadata-properties}

| **Metadataegenskap** | **Beskrivning** |
|---|---|
| dam:Physicalwiddinins | Dokumentets bredd i tum. |
| dam:Physicalheightininches | Dokumenthöjd i tum. |

Du har åtkomst `Rasterize PDF/AI Image Preview Rendition` bearbeta komponentalternativ via `DAM Update Asset` arbetsflöde.

Välj Adobe Experience Manager i det övre vänstra hörnet, navigera till **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**. På sidan Arbetsflödesmodeller väljer du **[!UICONTROL DAM Update Asset]** väljer du **[!UICONTROL Edit]**. Dubbeltryck på arbetsflödessidan för DAM-uppdatering av resurser `Rasterize PDF/AI Image Preview Rendition` för att öppna dialogrutan Stegegenskaper.

#### Rastrera återgivningsalternativen PDF/AI Image Preview {#rasterize-pdf-ai-image-preview-rendition-options}

![Argument för att rastrera arbetsflödet för PDF eller AI](assets/rasterize_pdf_ai_image_preview.png)

Argument för att rastrera arbetsflödet för PDF eller AI

| Processargument | Standardinställning | Beskrivning |
|---|---|---|
| Mime-typer | application/pdf<br>application/postscript<br>program/illustrator | Lista över dokumentMIME-typer som anses vara PDF- eller Illustrator-dokument. |
| Maxbredd | 2048 | Maximal bredd i pixlar för den genererade förhandsvisningsåtergivningen. |
| Maxhöjd | 2048 | Maximal höjd för den genererade förhandsvisningsåtergivningen, i pixlar. |
| Upplösning | 72 | Upplösning för att rastrera den första sidan, i ppi (pixlar per tum). |

Med standardprocessargumenten rastreras den första sidan i ett PDF/AI-dokument med 72 ppi och den genererade förhandsvisningsbilden med storleken 2 048 x 2 048 pixlar. För en vanlig driftsättning kan du öka upplösningen till minst 150 ppi. Ett dokument med US-teckenstorlek på 300 ppi kräver t.ex. en maximal bredd och höjd på 2 550 x 3 300 pixlar.

Maximal bredd och Maximal höjd begränsar upplösningen som rastreras. Om maxvärdena t.ex. är oförändrade och upplösningen är 300 ppi rastreras ett US Letter-dokument med 186 ppi. Dokumentet är alltså 1 581 x 2 046 pixlar.

The `Rasterize PDF/AI Image Preview Rendition` processkomponenten har en definierad maxgräns för att säkerställa att den inte skapar för stora bilder i minnet. Sådana stora bilder kan flöda över minnet som Java™ Virtual Machine (Java™ Virtual Machine) har fått. Man måste se till att JVM får tillräckligt med minne för att hantera det konfigurerade antalet parallella arbetsflöden, där var och en har möjlighet att skapa en bild med den högsta konfigurerade storleken.

### InDesign (INDD), filformat {#indesign-indd-file-format}

Om du tänker ge stöd för inmatning av INDD-filer så att du kan generera en dynamisk återgivning av det här filformatet bör du granska följande information innan du skapar bildförinställningar.

För InDesign-filer extraheras underresurser endast om Adobe InDesign Server är integrerat med Experience Manager. Refererade resurser länkas baserat på deras metadata. InDesign Server krävs inte för länkning. De refererade resurserna måste dock finnas i Experience Manager innan InDesign-filerna bearbetas för de länkar som ska skapas mellan InDesign-filerna och de refererade resurserna.

<!-- See [Integrate Experience Manager Assets with InDesign Server](/help/assets/indesign.md). -->

Processkomponenten för medieextraheringsprocessen i `DAM Update Asset` arbetsflödet kör flera förkonfigurerade Extend Scripts för att bearbeta InDesign-filer.

![ExtendScript-sökvägarna i argumenten i medieextraheringsprocessen](/help/assets/dynamic-media/assets/6_5_mediaextractionprocess.png)

ExtendScript-sökvägarna i argumenten för processkomponenten Medieextrahering i arbetsflödet för DAM-uppdatering.

Följande skript används av Dynamic Media-integrering:


| ExtendScript name | Standard | Beskrivning |
|---|---|---|
| ThumbnailExport.jsx | Ja | Skapar en 300 PPI `thumbnail.jpg` återgivning som är optimerad och omvandlad till en PTIFF-återgivning med `Dynamic Media Process Image Assets` processkomponent. |
| JPEGPagesExport.jsx | Ja | Skapar en 300 PPI JPEG-underresurs för varje sida. Underresursen JPEG är en reell tillgång som lagras under resursen InDesign. Den är också optimerad och omvandlad till en PTIFF av `DAM Update Asset` arbetsflöde. |
| PDFPagesExport.jsx | Nej | Skapar en PDF-underresurs för varje sida. Underresursen PDF bearbetas enligt beskrivningen ovan. Eftersom PDF endast innehåller en sida genereras inga delresurser. |

### Konfigurera miniatyrstorlek för bild {#configuring-image-thumbnail-size}

Du kan konfigurera storleken på miniatyrbilder genom att konfigurera inställningarna i dialogrutan **[!UICONTROL DAM Update Asset]** arbetsflöde. I arbetsflödet finns två steg där du kan konfigurera miniatyrstorlek för bildresurser. Ett (**[!UICONTROL Dynamic Media Process Image Assets]**) används för dynamiska bildresurser. Den andra (**[!UICONTROL Process Thumbnails]**) används för att generera statiska miniatyrbilder eller när inga andra processer kan generera miniatyrbilder. Oavsett, *båda* måste ha samma inställningar.

I steget **[!UICONTROL Dynamic Media Process Image Assets]** genereras miniatyrbilder av bildservern och den här konfigurationen är oberoende av den konfiguration som används i steget **[!UICONTROL Process Thumbnails]**. Att skapa miniatyrbilder med steget **[!UICONTROL Process Thumbnails]** är det långsammaste och mest minneskrävande sättet att skapa miniatyrbilder.

Storleksändring för miniatyrbilder definieras i följande format: **[!UICONTROL width:height:center]**, till exempel `80:80:false`. Bredden och höjden bestämmer storleken i pixlar på miniatyrbilden. Mittvärdet är antingen false eller true. Om värdet är true innebär det att miniatyrbilden har exakt den storlek som anges i konfigurationen. Om den storleksändrade bilden är mindre centreras den i miniatyrbilden.

>[!NOTE]
>
>* Miniatyrstorlekar för EPS-filer konfigureras i **[!UICONTROL EPS thumbnails]** steg, i **[!UICONTROL Arguments]** under Miniatyrbilder.
>
>* Miniatyrbildsstorlekar för videoklipp konfigureras i **[!UICONTROL FFmpeg thumbnails]** steg, i **[!UICONTROL Process]** flik under **[!UICONTROL Arguments]**.
>


**Så här konfigurerar du miniatyrbildens storlek:**

1. Navigera till **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]** > **[!UICONTROL DAM Update Asset]** > **[!UICONTROL Edit]**.
1. Välj **[!UICONTROL Dynamic Media Process Image Assets]** steg och välj **[!UICONTROL Thumbnails]** -fliken. Ändra miniatyrstorleken efter behov och välj sedan **[!UICONTROL OK]**.

   ![6_5_dynamicmediaprocessimageassets-thumbnailstab](assets/6_5_dynamicmediaprocessimageassets-thumbnailstab.png)

1. Välj **[!UICONTROL Process Thumbnails]** väljer du **[!UICONTROL Thumbnails]** -fliken. Ändra miniatyrstorleken efter behov och välj sedan **[!UICONTROL OK]**.

   >[!NOTE]
   >
   >Värdena i thumbnails-argumentet i steget **[!UICONTROL Process Thumbnails]** måste matcha thumbnails-argumentet i steget **[!UICONTROL Dynamic Media Process Image Assets]**.

1. Välj **[!UICONTROL Save]** för att spara ändringarna i arbetsflödet.

### Öka eller minska antalet bildförinställningar som visas {#increasing-or-decreasing-the-number-of-image-presets-that-display}

De bildförinställningar du skapar är tillgängliga som dynamiska återgivningar när du förhandsgranskar resurser. Experience Manager visar olika dynamiska återgivningar när en resurs från **[!UICONTROL Detail View > Renditions]**. Du kan öka eller minska gränsen för de återgivningar som visas.

**Så här ökar eller minskar du antalet bildförinställningar som visas:**

1. Navigera till CRXDE Lite ([https://localhost:4502/crx/de](https://localhost:4502/crx/de)).
1. Navigera till noden med bildförinställningar på `/libs/dam/gui/coral/content/commons/sidepanels/imagepresetsdetail/imgagepresetslist`

   ![ökning_minskningEnumberofimagepresetsthatdisplay](assets/increase_decreasethenumberofimagepresetsthatdisplay.png)

1. I egenskapen **[!UICONTROL limit]** ändrar du **[!UICONTROL Value]**, som är inställt på 15 som standard, till önskat tal.
1. Navigera till bildförinställningens datakälla på `/libs/dam/gui/coral/content/commons/sidepanels/imagepresetsdetail/imgagepresetslist/datasource`

   ![chlimage_1-495](assets/chlimage_1-495.png)

1. I egenskapen limit ändrar du talet till önskat tal, till exempel `{empty requestPathInfo.selectors[1] ? "20" : requestPathInfo.selectors[1]}`
1. Välj **[!UICONTROL Save All]**.

### Skapa bildförinställningar {#creating-image-presets}

Skapa bildförinställningar så att du kan använda samma inställningar på alla bilder när du förhandsgranskar eller publicerar.

>[!NOTE]
>
>Om du använder Internet Explorer 9 visas inte den förinställning du har skapat i förinställningslistan direkt när du har sparat. Du kan lösa problemet genom att inaktivera cacheminnet för IE9.

Om du tänker ge stöd för att lägga in AI-, PDF- och EPS-filer så att du kan generera en dynamisk återgivning av dessa filformat bör du granska följande information innan du skapar bildförinställningar.

Se [Adobe Illustrator (AI), PostScript® (EPS) och PDF](#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats).

Om du tänker ge stöd för inmatning av INDD-filer så att du kan generera en dynamisk återgivning av det här filformatet bör du granska följande information innan du skapar bildförinställningar.

Se [InDesign (INDD), filformat](#indesign-indd-file-format).

**Så här skapar du bildförinställningar:**

1. I Experience Manager väljer du Experience Manager logotypen för att komma åt den globala navigeringskonsolen och går sedan till **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Image Presets]**.
1. Välj **[!UICONTROL Create]**.

   ![chlimage_1-496](assets/chlimage_1-496.png)

   >[!NOTE]
   >
   >Om du vill att den här bildförinställningen ska vara responsiv raderar du värdena i fälten **[!UICONTROL width]** och **[!UICONTROL height]** och lämnar dem tomma.

1. I **[!UICONTROL Edit Image Preset]** fönster, ange värden i **[!UICONTROL Basic]** och **[!UICONTROL Advanced]** tabbar, inklusive ett namn. Alternativen beskrivs i [Alternativ för bildförinställningar](#image-preset-options). Förinställningarna visas i den vänstra rutan och kan användas direkt tillsammans med andra resurser.

   ![6_5_imagepreset-edit](assets/6_5_imagepreset-edit.png)

1. Välj **[!UICONTROL Save]**.

### Skapa en responsiv bildförinställning {#creating-a-responsive-image-preset}

Om du vill skapa en responsiv bildförinställning utför du stegen i [Skapa bildförinställningar](#creating-image-presets). När du anger höjd och bredd i **[!UICONTROL Edit Image Preset]** radera värdena och lämna dem tomma.

Om du lämnar dem tomma visas information för Experience Manager om att den här bildförinställningen är responsiv. Du kan justera de andra värdena efter behov.

>[!NOTE]
>
>Om du vill visa knapparna **[!UICONTROL URL]** och **[!UICONTROL RESS]** när du använder en bildförinställning på en resurs måste resursen publiceras.
>
>![chlimage_1-79](assets/chlimage_1-498.png)
>
>Bildförinställningar och bildresurser publiceras automatiskt.

### Alternativ för bildförinställningar {#image-preset-options}

När du skapar eller redigerar bildförinställningar finns alternativen som beskrivs i det här avsnittet. Adobe rekommenderar dessutom att du börjar med följande alternativ:

* **[!UICONTROL Format]** (**[!UICONTROL Basic]** tab) - Select **[!UICONTROL JPEG]** eller något annat format som uppfyller dina krav. Alla webbläsare har stöd för JPEG-bildformatet. Det ger en bra balans mellan små filstorlekar och bildkvalitet. I bilder med JPEG-format används dock förstörande komprimering, som kan ge upphov till oönskade bildartefakter om komprimeringsinställningen är för låg. Därför rekommenderar Adobe att du ställer in komprimeringskvaliteten på 75. Den här inställningen ger en bra balans mellan bildkvalitet och liten filstorlek.

* **[!UICONTROL Enable Simple Sharpening]** – Markera inte **[!UICONTROL Enable Simple Sharpening]** (det här skärpefiltret ger mindre kontroll än inställningarna för Oskarp mask).

* **[!UICONTROL Sharpening: Resampling Mode]** - Välj **[!UICONTROL Bi-Cubic]**.

#### Alternativ på fliken Grundläggande {#basic-tab-options}

| Fält | Beskrivning |
| --- | --- |
| **Namn** | Ange ett beskrivande namn utan blanksteg. Om du vill hjälpa användare att identifiera den här bildförinställningen tar du med bildstorleksspecifikationen i namnet. |
| **Bredd och höjd** | Ange bildstorleken i pixlar. Bredd och höjd måste vara större än 0 pixlar. Om något av värdena är 0 skapas ingen förinställning. Om båda värdena är tomma skapas en responsiv bildförinställning. |
| **Format** | Välj ett format på menyn.<br>Välja **JPEG** erbjuder följande andra alternativ:<br>・ **Kvalitet** - Kvalitetsskalan JPEG är 1-100. Skalan visas när du drar i skjutreglaget.<br>・ **Aktivera nedsampling av JPG krominans** - Eftersom ögat är mindre känsligt för högfrekvent färginformation än högfrekvent luminans delas bildinformationen i JPEG i luminans och färgkomponenter. När en JPEG-bild komprimeras lämnas luminanskomponenten i full upplösning, medan färgkomponenterna nedsamplas genom att medelvärdet av alla pixelgrupper ökas. Nedsampling minskar datavolymen med en halv eller en tredjedel utan att det påverkar den upplevda kvaliteten. Nedsampling kan inte användas för gråskalebilder. Den här tekniken minskar mängden komprimering som är användbar för bilder med hög kontrast (till exempel bilder med överlagrad text).<br><br>Välja **GIF** eller **GIF med alfa** innehåller ytterligare **Färgkvantifiering för GIF** alternativ:<br>・ **Typ** - Välj **Adaptiv** (standard), **Webb**, eller **Macintosh**. Om du väljer **GIF med alfa**&#x200B;är alternativet Macintosh inte tillgängligt.<br>・ **Gitter** - Välj **Diffusera** eller **Av**.<br>・ **Antal färger** - Ange ett tal mellan 2 och 256.<br>・ **Färglista** - Ange en kommaavgränsad lista. För vitt, grått och svart anger du `000000,888888,ffffff`.<br><br>Välja **PDF**, **TIFF**, eller **TIFF med alfa** innehåller ytterligare alternativ:<br>・ **Komprimering** - Välj en komprimeringsalgoritm. Algoritmalternativ för PDF är **Ingen**, **Postnummer** och **Jpeg**; för TIFF är de **Ingen**, **LZW**, **Jpeg** och **Postnummer**; och TIFF med alfa är **Ingen**, **LZW** och **Postnummer**.<br><br>Välja **PNG**, **PNG med alfa**, eller **EPS** innehåller inga ytterligare alternativ. |
| **Skärpa** | Välj **Aktivera enkel skärpa** om du vill använda ett grundläggande skärpefilter på bilden efter att all skalförändring har gjorts. Skärpa kan kompensera för oskärpa som kan uppstå när du visar en bild i en annan storlek. |

#### Avancerade flikalternativ {#advanced-tab-options}

<table>
 <tbody>
  <tr>
   <td><strong>Fält</strong></td>
   <td><strong>Beskrivning</strong></td>
  </tr>
  <tr>
   <td><strong>Färgmodell</strong></td>
   <td>Välj <strong>RGB, CMYK,</strong> eller <strong>Gråskala</strong> för färgrymden.</td>
  </tr>
  <tr>
   <td><strong>Färgprofil</strong></td>
   <td>Välj den utdatafärgrymdsprofil som du vill att resursen ska konverteras till om den inte är densamma som arbetsprofilen.</td>
  </tr>
  <tr>
   <td><strong>Återgivningsmetod</strong></td>
   <td>Du kan åsidosätta standardåtergivningsmetoden. Återgivningsmetoden bestämmer vad som händer med färger som inte kan återges i målfärgprofilen (ej tryckbart). Återgivningsmetoden ignoreras om den inte är kompatibel med ICC-profilen.
    <ul>
     <li>Välj <strong>Perceptuell</strong> om du vill komprimera det totala färgomfånget från en färgrymd till en annan när en eller flera färger i den ursprungliga bilden är utanför färgomfånget för målfärgrymden.</li>
     <li>Välj <strong>Relativa färgvärden</strong> när en färg i den aktuella färgrymden inte är tryckbar i målfärgrymden. Och du vill mappa den till närmaste möjliga färg inom färgomfånget för målfärgrymden utan att påverka några andra färger. </li>
     <li>Välj <strong>Mättnad</strong> om du vill återge den ursprungliga bildens färgmättnad när du konverterar till målfärgrymden. </li>
     <li>Välj <strong>Absoluta färgvärden</strong> om du vill matcha färgerna exakt utan justering för vitpunkt eller svartpunkt som skulle ändra bildens intensitet.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Svartpunktskompensation</strong></td>
   <td>Välj det här alternativet om utdataprofilen har stöd för den här funktionen. Svartpunktskompensation ignoreras om den inte är kompatibel med den angivna ICC-profilen.</td>
  </tr>
  <tr>
   <td><strong>Gitter</strong></td>
   <td>Välj det här alternativet om du vill undvika eller minska färgränder. </td>
  </tr>
  <tr>
   <td><strong>Skärpetyp</strong></td>
   <td><p>Välj <strong>Ingen</strong>, <strong>Skärpa</strong>, eller <strong>Oskarp mask</strong>. </p>
    <ul>
     <li>Välj <strong>Ingen</strong> om du vill inaktivera skärpa.</li>
     <li>Välj <strong>Skärpa </strong>om du vill använda ett grundläggande skärpefilter på bilden efter att all skalförändring har gjorts. Skärpa kan kompensera för oskärpa som kan uppstå när du visar en bild i en annan storlek. </li>
     <li>Välj<strong> Oskarp mask</strong> om du vill finjustera en skärpefiltereffekt på den slutliga nedsamplade bilden. Du kan styra intensiteten för effekten, radien för effekten (mätt i pixlar) och ett kontrasttröskelvärde som ignoreras. Effekten har samma alternativ som filtret Oskarp mask i Photoshop.</li>
    </ul> <p>I <strong>Oskarp mask</strong>har du följande alternativ:</p>
    <ul>
     <li><strong>Belopp</strong> - Styr mängden kontrast som används på kantpixlar. Standardvärdet för reella tal är 1,0. För högupplösta bilder kan du öka den till upp till 5.0. Tänk på Mängd som ett mått på filterintensiteten.</li>
     <li><strong>Radie</strong> - Anger antalet pixlar runt kantpixlarna som påverkar skärpan. För högupplösta bilder anger du ett reellt tal mellan 1 och 2. Med ett lågt värde ökas endast kantpixlarna skärpan. ett högt värde ökar skärpan i ett större antal pixlar. Vilket värde som är korrekt beror på bildens storlek.</li>
     <li><strong>Tröskelvärde</strong> - Anger det kontrastintervall som ska ignoreras när det oskarpa maskfiltret används. Med andra ord, det här alternativet avgör hur olika de pixlar som ska göras skarpare måste vara från det omgivande området innan de betraktas som kantpixlar och blir skarpare. Experimentera med heltalsvärden mellan 2 och 20 för att undvika brus. </li>
     <li><strong>Använd på</strong> - Avgör om den oskarpa inställningen ska gälla för varje färg eller intensitet.</li>
    </ul>
    <div>
      Skärpa beskrivs i
     <a href="https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-image-sharpening-feature-video-use.html#dynamic-media">Använda bildskärpa med Experience Manager Dynamic Media</a> video, in <a href="https://experienceleague.adobe.com/docs/dynamic-media-classic/using/master-files/sharpening-image.html#master-files">Öka skärpan i en bild</a> onlinehjälpavsnitt och i <a href="https://experienceleague.adobe.com/docs/dynamic-media-classic/assets/s7_sharpening_images.pdf">Bästa tillvägagångssätt för att skärpa bilder i Dynamic Media Classic</a> nedladdningsbar PDF.
    </div> </td>
  </tr>
  <tr>
   <td><strong>Omsamplingsläge</strong></td>
   <td>Välj en <strong>Omsamplingsläge</strong> alternativ. Dessa alternativ gör bilden skarpare när den nedsamplas:
    <ul>
     <li><strong>Dubbellinjär</strong> - Den snabbaste omsamplingsmetoden. Vissa aliaseringsartefakter är märkbara.</li>
     <li><strong>Bi-Cubic</strong> - Ökar CPU-användningen men ger skarpare bilder med mindre märkbara aliaseringsartefakter.</li>
     <li><strong>Sharp2</strong> - Kan ge något skarpare resultat än bikubik, men till en ännu högre CPU-kostnad.</li>
     <li><strong>Bi-Sharp</strong> - Väljer Photoshop standardomsampling för att minska bildstorleken, vilket kallas <strong>bikubisk skarpare</strong> i Adobe Photoshop.</li>
     <li><strong>Varje färg</strong> och <strong>Intensitet</strong> - varje metod kan baseras på färg eller intensitet. Som standard <strong>Varje färg</strong> är markerat.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Utskriftsupplösning</strong></td>
   <td>Välj en upplösning för utskrift av den här bilden; 72 pixlar är standard.</td>
  </tr>
  <tr>
   <td><strong>Bildmodifierare</strong></td>
   <td><p>Förutom de vanliga bildinställningarna i användargränssnittet har Dynamic Media stöd för många avancerade bildändringar som du kan ange i <strong>Bildmodifierare</strong> fält. Dessa parametrar definieras i <a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/syntax-and-features/image-serving-http/c-command-overview.html">Kommandoreferens för Image Server-protokoll</a>.</p> <p>Viktigt: Följande funktioner i API:t stöds inte:</p>
    <ul>
     <li>Grundläggande kommandon för mallar och textåtergivning: <code>text= textAngle= textAttr= textFlowPath= textFlowXPath= textPath=</code> och <code>textPs=</code></li>
     <li>Lokaliseringskommandon: <code>locale=</code> och <code>req=xlate</code></li>
     <li><code>req=set</code> är inte tillgängligt för allmän användning.</li>
     <li><code>req=mbrset</code></li>
     <li><code>req=saveToFile</code></li>
     <li><code>req=targets</code></li>
     <li><code>template=</code></li>
     <li>Icke-kärntjänster från Dynamic Media: SVG, bildåtergivning och webb-till-tryck</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### Definiera förinställningsalternativ för bilder med bildmodifierare {#defining-image-preset-options-with-image-modifiers}

Förutom alternativen på flikarna Grundläggande och Avancerat kan du definiera bildmodifierare som ger dig fler alternativ när du definierar bildförinställningar. Bildåtergivning bygger på Dynamic Media API för bildåtergivning och definieras i detalj i [HTTP-protokollreferens](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-rendering-api/http-protocol-reference/c-ir-introduction.html#image-rendering-api).

Nedan följer några grundläggande exempel på vad du kan göra med bildmodifierare.

>[!NOTE]
>
>Vissa bildmodifierare [kan inte användas i Experience Manager](#advanced-tab-options).

* [op_invert](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-op-invert.html) - Inverterar varje färgkomponent för en negativ bildeffekt.

   ```xml {.line-numbers}
   &op_invert=1
   ```

   ![6_5_imagepreset-edit-invert](assets/6_5_imagepreset-edit-invert.png)

* [op_blur](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-op-blur.html) - Använder ett oskärpefilter på bilden.

   ```xml {.line-numbers}
   &op_blur=7
   ```

   ![6_5_imagepreset-edit-blur](assets/6_5_imagepreset-edit-blur.png)

* Kombinerade kommandon - op_blur och op-invert

   ```xml {.line-numbers}
   &op_invert=1&op_blur=7
   ```

   ![chlimage_1-80](assets/chlimage_1-501.png)

* [op_brightness](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-op-brightness.html) - Minskar eller ökar intensiteten.

   ```xml {.line-numbers}
   &op_brightness=58
   ```

   ![6_5_imagepreset-edit-brightness](assets/6_5_imagepreset-edit-brightness.png)

* [opac](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-opac.html) - Justerar bildens opacitet. Du kan minska förgrundens opacitet.

   ```xml {.line-numbers}
   opac=29
   ```

   ![6_5_imagepreset-edit-opacity](assets/6_5_imagepreset-edit-opacity.png)

### Redigera bildförinställningar {#modifying-image-presets}

1. I Experience Manager väljer du Experience Manager logotypen för att komma åt den globala navigeringskonsolen och går sedan till **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Image Presets]**.

   ![6_5_imagepreset-editpreset](assets/6_5_imagepreset-editpreset.png)

1. Markera en förinställning och välj sedan **[!UICONTROL Edit]**. The **[!UICONTROL Edit Image Preset]** öppnas.
1. Gör ändringar och markera **[!UICONTROL Save]** för att spara dina ändringar eller **[!UICONTROL Cancel]** om du vill avbryta ändringarna.

### Publicera bildförinställningar {#publishing-image-presets}

Bildförinställningar publiceras automatiskt åt dig.

### Ta bort bildförinställningar {#deleting-image-presets}

1. I Experience Manager väljer du Experience Manager logotypen för att komma åt den globala navigeringskonsolen och väljer verktygsikonen.
1. Navigera till **[!UICONTROL Assets]** > **[!UICONTROL Image Presets]**.
1. Välj en förinställning och välj sedan **[!UICONTROL Delete]**. Dynamic Media bekräftar att du vill ta bort den. Välj **[!UICONTROL Delete]** ta bort eller markera **[!UICONTROL Cancel]** för att återgå till bildförinställningar.

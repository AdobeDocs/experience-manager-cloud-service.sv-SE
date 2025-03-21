---
title: Hantera bildförinställningar
description: Lär dig mer om bildförinställningar och hur du skapar, ändrar och hanterar dem.
contentOwner: Rick Brough
feature: Image Presets,Viewers,Renditions
role: User
exl-id: a53f40ab-0e27-45f8-9142-781c077a04cc
source-git-commit: c82f84fe99d8a196adebe504fef78ed8f0b747a9
workflow-type: tm+mt
source-wordcount: '3466'
ht-degree: 5%

---

# Hantera bildförinställningar{#managing-image-presets}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime och Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM Assets-integrering med Edge Delivery Services</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>UI-utökningsbarhet</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Aktivera Dynamic Media Prime och Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>Sök efter bästa praxis</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>Metadata - bästa praxis</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Content Hub</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>Dynamiska media med OpenAPI-funktioner</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>AEM Assets-dokumentation för utvecklare</b></a>
        </td>
    </tr>
</table>

Med bildförinställningar kan Adobe Experience Manager Assets leverera bilder dynamiskt i olika storlekar, i olika format eller med andra bildegenskaper som genereras dynamiskt. Varje bildförinställning representerar en fördefinierad samling kommandon för storleksändring och formatering för visning av bilder. När du skapar en bildförinställning väljer du en storlek för bildleverans. Du kan också välja formateringskommandon så att bildens utseende optimeras när bilden levereras för visning.

Administratörer kan skapa förinställningar för att exportera resurser. Användarna kan välja en förinställning när de exporterar bilder, vilket även innebär att bilderna formateras om enligt de specifikationer som administratören anger.

Du kan också skapa bildförinställningar som är responsiva. Om du använder en responsiv bildförinställning på dina resurser ändras de beroende på vilken enhet eller skärmstorlek de visas på. Du kan konfigurera bildförinställningar så att de använder CMYK i färgmodellen, förutom RGB och Grå.

I det här avsnittet beskrivs hur du skapar, ändrar och i allmänhet hanterar bildförinställningar. Du kan använda en bildförinställning på en bild när du vill förhandsvisa den. Se [Använda bildförinställningar](/help/assets/dynamic-media/image-presets.md).

>[!NOTE]
>
>Smart bildbehandling fungerar med befintliga bildförinställningar och använder intelligens under de sista millisekunderna av leveransen för att minska bildfilens storlek ytterligare baserat på webbläsarens eller nätverkets anslutningshastighet. Mer information finns i [Smart bildbehandling](/help/assets/dynamic-media/imaging-faq.md).

## Läs mer om bildförinställningar {#understanding-image-presets}

Precis som ett makro är en bildförinställning en fördefinierad samling kommandon för storleksändring och formatering som sparats under ett namn. Anta att webbplatsen kräver att varje produktbild visas i olika storlekar, olika format och komprimeringsgrader för datorer och mobila enheter för att du ska kunna förstå hur bildförinställningar fungerar.

Du kan skapa två bildförinställningar: 500 x 500 pixlar för skrivbordet och 150 x 150 pixlar för mobilen. Du skapar två bildförinställningar, en med namnet `Enlarge` om du vill visa bilder med 500 x 500 pixlar och en med namnet `Thumbnail` om du vill visa bilder med 150 x 150 pixlar. För att leverera bilder i storleken `Enlarge` och `Thumbnail` hittar Experience Manager definitionen av `Enlarge Image Preset` och `Thumbnail Image Preset`. Sedan genererar Experience Manager dynamiskt en bild med samma storlek och formateringsspecifikationer som varje bildförinställning.

Bilder som minskar i storlek när de levereras dynamiskt kan förlora i skärpa och detaljer. Därför innehåller varje bildförinställning formateringskontroller för optimering av en bild när den levereras i en viss storlek. Med dessa kontroller kan du vara säker på att dina bilder är skarpa och tydliga när de levereras till din webbplats eller ditt program.

Administratörer kan skapa bildförinställningar. Om du vill skapa en bildförinställning kan du börja från början eller så kan du börja från en befintlig och spara den under ett nytt namn.

## Hantera bildförinställningar {#managing-image-presets-1}

Du hanterar dina bildförinställningar i Experience Manager genom att välja Experience Manager logotyp för att komma åt den globala navigeringskonsolen och sedan välja ikonen Verktyg och navigera till **[!UICONTROL Assets]** > **[!UICONTROL Image Presets]**.

![6_5_tools-assets-imagepresets](assets/6_5_tools-assets-imagepresets.png)

>[!NOTE]
>
>Alla bildförinställningar som du skapar är också tillgängliga som dynamiska återgivningar när du förhandsvisar eller levererar resurser.
>
>Du behöver *inte* publicera bildförinställningar eftersom bildförinställningar publiceras automatiskt.
>
>Se [Publicera bildförinställningar](#publishing-image-presets).

>[!NOTE]
>
>I systemet visas olika återgivningar när du väljer **[!UICONTROL Renditions]** i en tillgångs detaljvy. Du kan öka eller minska antalet bildförinställningar som visas. Se [Öka antalet bildförinställningar som visas](#increasing-or-decreasing-the-number-of-image-presets-that-display).

### Adobe Illustrator (AI), PostScript® (EPS) och PDF {#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats}

Om du tänker ge stöd för att lägga in AI-, EPS- och PDF-filer så att du kan generera dynamiska återgivningar av dessa filformat bör du granska följande information innan du skapar bildförinställningar.

Adobe Illustrator filformat är en sorts PDF. De största skillnaderna i Experience Manager Assets är följande:

* Adobe Illustrator-dokument består av en sida med flera lager. Varje lager extraheras som en PNG-delresurs under Illustrator huvudresurs.
* PDF-dokument består av en eller flera sidor. Varje sida extraheras som en PDF-delresurs på en sida under PDF-huvuddokumentet med flera sidor.

Komponenten `Create Sub Asset process` skapar delresurserna i det övergripande `DAM Update Asset`-arbetsflödet. Om du vill visa den här processkomponenten i arbetsflödet går du till **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]** > **[!UICONTROL DAM Update Asset]** > **[!UICONTROL Edit]**.

<!-- See also [Viewing pages of a multi-page file](/help/assets/manage-linked-subassets.md#view-pages-of-a-multi-page-file). -->

Du kan visa delresurserna eller sidorna när du öppnar resursen, välja Innehåll-menyn och välja **[!UICONTROL Subassets]** eller **[!UICONTROL Pages]**. Deltillgångarna är verkliga tillgångar. Arbetsflödeskomponenten `Create Sub Asset` extraherar PDF-sidorna. De lagras sedan som `page1.pdf`, `page2.pdf` och så vidare, under huvudresursen. När de har lagrats bearbetar arbetsflödet `DAM Update Asset` dem.

Om du vill använda Dynamic Media för att förhandsgranska och generera dynamiska renderingar för AI-, EPS- eller PDF-filer måste du utföra följande steg:

1. I arbetsflödet `DAM Update Asset` rastrerar processkomponenten `Rasterize PDF/AI Image Preview Rendition` den första sidan i den ursprungliga resursen - med den konfigurerade upplösningen - till en `cqdam.preview.png`-rendering.

1. Processkomponenten `Dynamic Media Process Image Assets` i arbetsflödet optimerar återgivningen av `cqdam.preview.png` till en PTIFF.

>[!NOTE]
>
>I arbetsflödet för DAM-uppdatering av resurser genererar steget **[!UICONTROL EPS thumbnails]** miniatyrer för EPS-filer.

#### PDF/AI/EPS-metadataegenskaper {#pdf-ai-eps-asset-metadata-properties}

| **Metadataegenskap** | **Beskrivning** |
|---|---|
| `dam:Physicalwidthininches` | Dokumentets bredd i tum. |
| `dam:Physicalheightininches` | Dokumenthöjd i tum. |

Du kommer åt alternativen för processkomponenten `Rasterize PDF/AI Image Preview Rendition` via arbetsflödet `DAM Update Asset`.

Välj Adobe Experience Manager i det övre vänstra hörnet och klicka på **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**. På sidan Arbetsflödesmodeller väljer du **[!UICONTROL DAM Update Asset]** och sedan **[!UICONTROL Edit]** i verktygsfältet. Dubbelmarkera processkomponenten `Rasterize PDF/AI Image Preview Rendition` på arbetsflödessidan DAM Update Asset för att öppna dialogrutan Step Properties.

#### Rastrera återgivningsalternativen PDF/AI Image Preview {#rasterize-pdf-ai-image-preview-rendition-options}

![Argument för rastrering av PDF- eller AI-arbetsflöde](assets/rasterize_pdf_ai_image_preview.png)

Argument för att rastrera arbetsflödet i PDF eller AI

| Processargument | Standardinställning | Beskrivning |
|---|---|---|
| Mime-typer | application/pdf<br>application/postscript<br>application/illustrator | Lista över dokumentMIME-typer som anses vara PDF- eller Illustrator-dokument. |
| Maximal bredd | 2048 | Maximal bredd i pixlar för den genererade förhandsvisningsåtergivningen. |
| Maximal höjd | 2048 | Maximal höjd för den genererade förhandsvisningsåtergivningen, i pixlar. |
| Upplösning | 72 | Upplösning för att rastrera den första sidan, i ppi (pixlar per tum). |

Med standardprocessargumenten rastreras den första sidan i ett PDF/AI-dokument med 72 ppi och den genererade förhandsvisningsbilden med storleken 2 048 x 2 048 pixlar. För en vanlig driftsättning kan du öka upplösningen till minst 150 ppi. Ett dokument med US-teckenstorlek på 300 ppi kräver t.ex. en maximal bredd och höjd på 2 550 x 3 300 pixlar.

Maximal bredd och Maximal höjd begränsar upplösningen som rastreras. Om maxvärdena t.ex. är oförändrade och upplösningen är 300 ppi rastreras ett US Letter-dokument med 186 ppi. Dokumentet är alltså 1 581 x 2 046 pixlar.

Processkomponenten `Rasterize PDF/AI Image Preview Rendition` har en definierad maxgräns för att säkerställa att den inte skapar för stora bilder i minnet. Sådana stora bilder kan flöda över minnet som Java™ Virtual Machine (Java™ Virtual Machine) har fått. Man måste se till att JVM får tillräckligt med minne för att hantera det konfigurerade antalet parallella arbetsflöden, där var och en har möjlighet att skapa en bild med den högsta konfigurerade storleken.

### InDesign (INDD), filformat {#indesign-indd-file-format}

Om du tänker ge stöd för inmatning av INDD-filer så att du kan generera en dynamisk återgivning av det här filformatet bör du granska följande information innan du skapar bildförinställningar.

För InDesign-filer extraheras underresurser endast om Adobe InDesign Server är integrerat med Experience Manager. Refererade resurser länkas baserat på deras metadata. InDesign Server krävs inte för länkning. De refererade resurserna måste dock finnas i Experience Manager innan InDesign-filerna bearbetas för att länkarna ska skapas mellan InDesign-filerna och de refererade resurserna.

<!-- See [Integrate Experience Manager Assets with InDesign Server](/help/assets/indesign.md). -->

Processkomponenten för medieextrahering i arbetsflödet `DAM Update Asset` kör flera förkonfigurerade Extend Scripts för att bearbeta InDesign-filer.

![ExtendScript-sökvägarna i argumenten i medieextraheringsprocessen](/help/assets/dynamic-media/assets/6_5_mediaextractionprocess.png)

ExtendScript-sökvägarna i argumenten för processkomponenten Medieextrahering i arbetsflödet för DAM-uppdatering av resurser.

Följande skript används av integreringen med Dynamic Media:


| ExtendScript name | Standard | Beskrivning |
|---|---|---|
| ThumbnailExport.jsx | Ja | Skapar en 300 PPI `thumbnail.jpg`-rendering som är optimerad och omvandlad till en PTIFF-rendering av `Dynamic Media Process Image Assets`-processkomponenten. |
| JPEGPagesExport.jsx | Ja | Skapar en 300 PPI JPEG-underresurs för varje sida. Underresursen JPEG är en verklig tillgång som lagras under InDesign-resursen. Arbetsflödet `DAM Update Asset` optimerar och konverterar det till en PTIFF. |
| PDFPagesExport.jsx | Nej | Skapar en PDF-underresurs för varje sida. PDF underresurs bearbetas enligt beskrivningen ovan. Eftersom PDF endast innehåller en sida genereras inga underresurser. |

### Konfigurera miniatyrbildens storlek {#configuring-image-thumbnail-size}

Du kan konfigurera storleken på miniatyrbilder genom att konfigurera inställningarna i arbetsflödet för **[!UICONTROL DAM Update Asset]**. I arbetsflödet finns två steg där du kan konfigurera miniatyrstorlek för bildresurser. En (**[!UICONTROL Dynamic Media Process Image Assets]**) används för dynamiska bildresurser. Den andra (**[!UICONTROL Process Thumbnails]**) används för att generera statiska miniatyrbilder eller när inga andra processer kan generera miniatyrbilder. Oavsett vilket måste *båda* ha samma inställningar.

I steget **[!UICONTROL Dynamic Media Process Image Assets]** används bildservern för att generera miniatyrbilder, oberoende av konfigurationen som används i steget **[!UICONTROL Process Thumbnails]**. Att skapa miniatyrbilder med steget **[!UICONTROL Process Thumbnails]** är det långsammaste och mest minneskrävande sättet att skapa miniatyrbilder.

Storleksändring för miniatyrbilder har definierats i följande format: **[!UICONTROL width:height:center]**, till exempel `80:80:false`. Bredden och höjden bestämmer storleken i pixlar på miniatyrbilden. Mittvärdet är antingen false eller true. Om värdet är true innebär det att miniatyrbilden har exakt den storlek som anges i konfigurationen. Om den storleksändrade bilden är mindre centreras den i miniatyrbilden.

>[!NOTE]
>
>* Miniatyrbildsstorlekar för EPS-filer konfigureras i steget **[!UICONTROL EPS thumbnails]** på fliken **[!UICONTROL Arguments]** under Miniatyrbilder.
>
>* Miniatyrstorlekar för videoklipp konfigureras i steget **[!UICONTROL FFmpeg thumbnails]** på fliken **[!UICONTROL Process]** under **[!UICONTROL Arguments]**.
>

**Så här konfigurerar du bildens miniatyrstorlek:**

1. Navigera till **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]** > **[!UICONTROL DAM Update Asset]** > **[!UICONTROL Edit]**.
1. Välj steget **[!UICONTROL Dynamic Media Process Image Assets]** och välj fliken **[!UICONTROL Thumbnails]**. Ändra miniatyrstorleken efter behov och välj sedan **[!UICONTROL OK]**.

   ![6_5_dynamicmediaprocessimageassets-thumbnailstab](assets/6_5_dynamicmediaprocessimageassets-thumbnailstab.png)

1. Markera steget **[!UICONTROL Process Thumbnails]** och välj sedan fliken **[!UICONTROL Thumbnails]**. Ändra miniatyrstorleken efter behov och välj sedan **[!UICONTROL OK]**.

   >[!NOTE]
   >
   >Värdena i thumbnails-argumentet i steget **[!UICONTROL Process Thumbnails]** måste matcha thumbnails-argumentet i steget **[!UICONTROL Dynamic Media Process Image Assets]**.

1. Välj **[!UICONTROL Save]** om du vill spara ändringarna i arbetsflödet.

### Öka eller minska antalet bildförinställningar som visas {#increasing-or-decreasing-the-number-of-image-presets-that-display}

De bildförinställningar du skapar är tillgängliga som dynamiska återgivningar när du förhandsgranskar resurser. Experience Manager visar olika dynamiska återgivningar när en resurs från **[!UICONTROL Detail View > Renditions]** visas. Du kan öka eller minska gränsen för de återgivningar som visas.

**Om du vill öka eller minska antalet bildförinställningar som visas:**

1. Gå till CRXDE Lite ([https://localhost:4502/crx/de](https://localhost:4502/crx/de)).
1. Navigera till noden med bildförinställningar på `/libs/dam/gui/coral/content/commons/sidepanels/imagepresetsdetail/imgagepresetslist`

   ![increase_decasethenumberofimagepresetsthatdisplay](assets/increase_decreasethenumberofimagepresetsthatdisplay.png)

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

Se [Adobe Illustrator (AI), PostScript® (EPS) och PDF ](#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats).

Om du tänker ge stöd för inmatning av INDD-filer så att du kan generera en dynamisk återgivning av det här filformatet bör du granska följande information innan du skapar bildförinställningar.

Se [InDesign-filformat (INDD)](#indesign-indd-file-format).

**Så här skapar du bildförinställningar:**

1. I Experience Manager väljer du Experience Manager logotyp för att komma åt den globala navigeringskonsolen och går sedan till **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Image Presets]**.
1. Välj **[!UICONTROL Create]**.

   ![chlimage_1-496](assets/chlimage_1-496.png)

   >[!NOTE]
   >
   >Om du vill göra den här bildförinställningen responsiv raderar du värdena i fälten **[!UICONTROL width]** och **[!UICONTROL height]** och lämnar dem tomma.

1. I fönstret **[!UICONTROL Edit Image Preset]** anger du värden på flikarna **[!UICONTROL Basic]** och **[!UICONTROL Advanced]**, inklusive ett namn. Alternativen beskrivs i [Alternativ för bildförinställningar](#image-preset-options). Förinställningarna visas i den vänstra rutan och kan användas direkt tillsammans med andra resurser.

   ![6_5_imagepreset-edit](assets/6_5_imagepreset-edit.png)

1. Välj **[!UICONTROL Save]**.

### Skapa en responsiv bildförinställning {#creating-a-responsive-image-preset}

Om du vill skapa en responsiv bildförinställning utför du stegen i [Skapa bildförinställningar](#creating-image-presets). När du anger höjd och bredd i fönstret **[!UICONTROL Edit Image Preset]** raderar du värdena och låter dem vara tomma.

Om du lämnar dem tomma visas information om för Experience Manager att den här bildförinställningen är responsiv. Du kan justera de andra värdena efter behov.

>[!NOTE]
>
>Om du vill visa knapparna **[!UICONTROL URL]** och **[!UICONTROL RESS]** när du använder en bildförinställning på en resurs måste resursen publiceras.
>
>![chlimage_1-79](assets/chlimage_1-498.png)
>
>Bildförinställningar och bildresurser publiceras automatiskt.

### Alternativ för bildförinställning {#image-preset-options}

När du skapar eller redigerar bildförinställningar finns alternativen som beskrivs i det här avsnittet. Dessutom rekommenderar Adobe att du börjar med följande alternativ:

* **[!UICONTROL Format]** (**[!UICONTROL Basic]** tab) - Välj **[!UICONTROL JPEG]** eller ett annat format som uppfyller dina krav. Alla webbläsare har stöd för JPEG-bildformatet. Det ger en bra balans mellan små filstorlekar och bildkvalitet. I bilder med JPEG-format används dock förstörande komprimering, som kan ge upphov till oönskade bildartefakter om komprimeringsinställningen är för låg. Därför rekommenderar Adobe att du ställer in komprimeringskvaliteten på 75. Den här inställningen ger en bra balans mellan bildkvalitet och liten filstorlek.

* **[!UICONTROL Enable Simple Sharpening]** – Markera inte **[!UICONTROL Enable Simple Sharpening]** (det här skärpefiltret ger mindre kontroll än inställningarna för Oskarp mask).

* **[!UICONTROL Sharpening: Resampling Mode]** - Välj **[!UICONTROL Sharp2]**.

#### Alternativ på fliken Grundläggande {#basic-tab-options}

| Fält | Beskrivning |
| --- | --- |
| **Namn** | Ange ett beskrivande namn utan blanksteg. Om du vill hjälpa användare att identifiera den här bildförinställningen tar du med bildstorleksspecifikationen i namnet. |
| **Bredd och höjd** | Ange bildstorleken i pixlar. Bredd och höjd måste vara större än 0 pixlar. Om något av värdena är 0 skapas ingen förinställning. Om båda värdena är tomma skapas en responsiv bildförinställning. |
| **Format** | Välj ett format på menyn.<br>Om du väljer **JPEG** får du tillgång till följande alternativ:<br> ・ **Kvalitet** - JPEG kvalitetsskala är 1-100. Skalan visas när du drar skjutreglaget.<br> ・ **Aktivera nedsampling av färgåtergivning i JPG** - Eftersom ögat är mindre känsligt för högfrekvent färginformation än högfrekvent luminans delas bildinformationen upp i JPEG-bilder i luminans- och färgkomponenter. När en JPEG-bild komprimeras lämnas luminanskomponenten i full upplösning, medan färgkomponenterna nedsamplas genom att medelvärdet av grupper med pixlar ökas. Nedsampling minskar datavolymen till hälften eller en tredjedel med minimal inverkan på den upplevda kvaliteten. Nedsampling kan inte användas för gråskalebilder. Den här tekniken minskar mängden komprimering som är användbar för bilder med hög kontrast (till exempel bilder med överlagrad text).<br><br>Om du väljer **GIF** eller **GIF med alfa** finns följande ytterligare alternativ för **GIF-färgkvantifiering**:<br> ・ **Typ** - Välj **Adaptiv** (standard), **Webb** eller **Macintosh**. Om du väljer **GIF med Alpha** är Macintosh-alternativet inte tillgängligt.<br> ・ **Gitter** - Välj **Diffusera** eller **Av**.<br> ・ **Antal färger** - Ange en siffra mellan 2 och 256.<br> ・ **Färglista** - Ange en kommaavgränsad lista. Ange till exempel `000000,888888,ffffff` för vitt, grått och svart.<br><br>Om du väljer **PDF**, **TIFF** eller **TIFF med alfa** får du följande alternativ:<br> ・ **Komprimering** - Välj en komprimeringsalgoritm. Algoritmalternativen för PDF är **Ingen**, **Zip** och **Jpeg**. För TIFF är de **Ingen**, **LZW**, **Jpeg** och **Zip** och för TIFF med Alpha är de **Inga** , **LZW** och **Zip** .<br><br>Om du väljer **PNG**, **PNG med Alpha** eller **EPS** finns inga ytterligare alternativ. |
| **Skärpa** | Välj **Aktivera enkel skärpa** om du vill använda ett grundläggande skärpefilter på bilden när all skalning har gjorts. Skärpa kan kompensera för oskärpa som kan uppstå när du visar en bild i en annan storlek. |

#### Avancerade flikalternativ {#advanced-tab-options}

<table>
 <tbody>
  <tr>
   <td><strong>Fält</strong></td>
   <td><strong>Beskrivning</strong></td>
  </tr>
  <tr>
   <td><strong>Färgmodell</strong></td>
   <td>Välj <strong>RGB, CMYK,</strong> eller <strong>Gråskala</strong> som färgrymd.</td>
  </tr>
  <tr>
   <td><strong>Färgprofil</strong></td>
   <td>Välj den utdatafärgrymdsprofil som du vill att resursen ska konverteras till om den inte är densamma som arbetsprofilen.</td>
  </tr>
  <tr>
   <td><strong>Återgivningsmetod</strong></td>
   <td>Du kan åsidosätta standardåtergivningsmetoden. Återgivningsmetoden avgör vad som händer med färger som inte kan återges i målfärgprofilen (ej tryckbart). Återgivningsmetoden ignoreras om den inte är kompatibel med ICC-profilen.
    <ul>
     <li>Välj <strong>Perceptuell</strong> om du vill komprimera det totala färgomfånget från en färgrymd till en annan när en eller flera färger i den ursprungliga bilden är utanför färgomfånget för målfärgrymden.</li>
     <li>Välj <strong>Relativa färgvärden</strong> när en färg i den aktuella färgrymden inte är tryckbar i målfärgrymden. Och du vill mappa den till närmaste målfärgomfång utan att ändra andra färger. </li>
     <li>Välj <strong>Mättnad</strong> om du vill återge den ursprungliga bildens färgmättnad när du konverterar till målfärgrymden. </li>
     <li>Välj <strong>Absolut färgvärde</strong> om du vill matcha färgerna exakt utan justering för vitpunkt eller svartpunkt som skulle ändra bildens intensitet.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Svartpunktskompensation</strong></td>
   <td>Välj det här alternativet om utdataprofilen har stöd för den här funktionen. Svartpunktskompensation ignoreras om den inte är kompatibel med den angivna ICC-profilen.</td>
  </tr>
  <tr>
   <td><strong>Gitter</strong></td>
   <td>Välj det här alternativet om du vill undvika eller minska eventuella färgränder. </td>
  </tr>
  <tr>
   <td><strong>Skärpetyp</strong></td>
   <td><p>Välj <strong>Ingen</strong>, <strong>Skärpa</strong> eller <strong>Oskarp mask</strong>. </p>
    <ul>
     <li>Välj <strong>Inget</strong> om du vill inaktivera skärpa.</li>
     <li>Välj <strong>Öka skärpan </strong> om du vill använda ett grundläggande skärpefilter på bilden när all skalning har gjorts. Skärpa kan kompensera för oskärpa som kan uppstå när du visar en bild i en annan storlek. </li>
     <li>Välj <strong> Oskarp mask </strong> om du vill finjustera en skärpefiltereffekt på den slutliga nedsamplade bilden. Du kan styra effektens intensitet, radie (mätt i pixlar) och ett tröskelvärde för kontrast som ignoreras. Den här effekten använder samma alternativ som Photoshop Oskarp mask-filter.</li>
    </ul> <p>I <strong>Oskarp mask</strong> har du följande alternativ:</p>
    <ul>
     <li><strong>Mängd</strong> - Anger mängden kontrast som används på kantpixlar. Standardvärdet för reella tal är 1,0. För högupplösta bilder kan du öka den till upp till 5.0. Tänk på Mängd som ett mått på filterintensiteten.</li>
     <li><strong>Radie</strong> - Anger antalet pixlar runt kantpixlarna som påverkar skärpan. För högupplösta bilder anger du ett reellt tal mellan 1 och 2. Med ett lågt värde ökas skärpan endast för kantpixlarna. Med ett högt värde ökas skärpan för ett bredare intervall av pixlar. Vilket värde som är korrekt beror på bildens storlek.</li>
     <li><strong>Tröskelvärde</strong> - Anger det kontrastintervall som ska ignoreras när filtret Oskarp mask används. Med andra ord definierar det här alternativet hur mycket skärpa som måste skilja sig från det omgivande området för att betraktas som kantpixlar och som skärpa. Experimentera med heltalsvärden mellan 2 och 20 för att undvika brus. </li>
     <li><strong>Gäller för </strong> - Avgör om den oskarpa inställningen gäller för varje färg eller intensitet.</li>
    </ul>
    <div>
      Skärpa beskrivs i
     <a href="https://experienceleague.adobe.com/en/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-image-sharpening-feature-video-use#dynamic-media">Använda bildskärpa med Experience Manager Dynamic Media</a> -video, i <a href="https://experienceleague.adobe.com/en/docs/dynamic-media-classic/using/master-files/sharpening-image#master-files">Skärpa en bild</a> onlinehjälpavsnitt och i <a href="https://experienceleague.adobe.com/docs/dynamic-media-classic/assets/s7_sharpening_images.pdf">Bästa tillvägagångssätt för skärpa i bilder i Dynamic Media Classic</a> hämtningsbar PDF.
    </div> </td>
  </tr>
  <tr>
   <td><strong>Omsamplingsläge</strong></td>
   <td>Välj ett <strong>omsamplingsläge</strong> -alternativ. Dessa alternativ gör bilden skarpare när den nedsamplas:
    <ul>
     <li><strong>Dubbellinjär</strong> - den snabbaste omsamplingsmetoden. Vissa aliaseringsartefakter är märkbara.</li>
     <li><strong>Bi-Cubic</strong> - Ökar CPU-användningen men ger skarpare bilder med mindre framträdande aliasartefakter.</li>
     <li><strong>Sharp2</strong> - Kan ge något tydligare resultat än bikubisk, men till en ännu högre CPU-kostnad.</li>
     <li><strong>Bi-Sharp</strong> - Väljer Photoshop standardomsampling för att minska bildstorleken, som kallas <strong>bikubisk skarpare</strong> i Adobe Photoshop.</li>
     <li><strong>Varje färg</strong> och <strong>Intensitet</strong> - varje metod kan baseras på färg eller intensitet. Som standard är <strong>Varje färg</strong> markerad.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Utskriftsupplösning</strong></td>
   <td>Välj en upplösning för utskrift av den här bilden. 72 pixlar är standard.</td>
  </tr>
  <tr>
   <td><strong>Bildmodifierare</strong></td>
   <td><p>Förutom de vanliga bildinställningarna i användargränssnittet har Dynamic Media stöd för många avancerade bildändringar som du kan ange i fältet <strong>Bildmodifierare</strong>. De här parametrarna definieras i <a href="https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/syntax-and-features/image-serving-http/c-command-overview">Image Server Protocol-kommandoreferensen</a>.</p> <p>Viktigt: Följande funktioner i API:t stöds inte:</p>
    <ul>
     <li>Grundläggande kommandon för mallar och textåtergivning: <code>text= textAngle= textAttr= textFlowPath= textFlowXPath= textPath=</code> och <code>textPs=</code></li>
     <li>Localization commands: <code>locale=</code> och <code>req=xlate</code></li>
     <li><code>req=set</code> är inte tillgängligt för allmän användning.</li>
     <li><code>req=mbrset</code></li>
     <li><code>req=saveToFile</code></li>
     <li><code>req=targets</code></li>
     <li><code>template=</code></li>
     <li>Icke-kärnbaserade dynamiska medietjänster: SVG, bildåtergivning och web-to-Print</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### Definiera förinställningsalternativ för bilder med bildmodifierare {#defining-image-preset-options-with-image-modifiers}

Förutom alternativen på flikarna Grundläggande och Avancerat kan du definiera bildmodifierare som ger dig fler alternativ när du definierar bildförinställningar. Bildåtergivning är beroende av API:t för bildåtergivning för dynamiska media och definieras i detalj i [HTTP-protokollreferensen](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-rendering-api/http-protocol-reference/c-ir-introduction#image-rendering-api).

Nedan följer några grundläggande exempel på vad du kan göra med bildmodifierare.

>[!NOTE]
>
>Vissa bildmodifierare [kan inte användas i Experience Manager](#advanced-tab-options).

* [op_invert](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-op-invert) - Inverterar varje färgkomponent för en negativ bildeffekt.

  ```xml {.line-numbers}
  &op_invert=1
  ```

  ![6_5_imagepreset-edit-invert](assets/6_5_imagepreset-edit-invert.png)

* [op_blur](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-op-blur) - Använder ett oskärpefilter på bilden.

  ```xml {.line-numbers}
  &op_blur=7
  ```

  ![6_5_imagepreset-edit-blur](assets/6_5_imagepreset-edit-blur.png)

* Kombinerade kommandon - op_blur och op-invert

  ```xml {.line-numbers}
  &op_invert=1&op_blur=7
  ```

  ![chlimage_1-80](assets/chlimage_1-501.png)

* [op_brightness](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-op-brightness) - Minskar eller ökar intensiteten.

  ```xml {.line-numbers}
  &op_brightness=58
  ```

  ![6_5_imagepreset-edit-brightness](assets/6_5_imagepreset-edit-brightness.png)

* [opac](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-opac) - Justerar bildens opacitet. Du kan minska förgrundens opacitet.

  ```xml {.line-numbers}
  opac=29
  ```

  ![6_5_imagepreset-edit-opacity](assets/6_5_imagepreset-edit-opacity.png)

### Redigera bildförinställningar {#modifying-image-presets}

1. I Experience Manager väljer du Experience Manager logotyp för att komma åt den globala navigeringskonsolen och går sedan till **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Image Presets]**.

   ![6_5_imagepreset-editpreset](assets/6_5_imagepreset-editpreset.png)

1. Välj en förinställning och välj sedan **[!UICONTROL Edit]**. Fönstret **[!UICONTROL Edit Image Preset]** öppnas.
1. Gör ändringar och välj **[!UICONTROL Save]** om du vill spara ändringarna eller **[!UICONTROL Cancel]** om du vill avbryta ändringarna.

### Publicera bildförinställningar {#publishing-image-presets}

Bildförinställningar publiceras automatiskt åt dig.

### Ta bort bildförinställningar {#deleting-image-presets}

1. I Experience Manager väljer du Experience Manager logotyp för att öppna den globala navigeringskonsolen och väljer verktygsikonen.
1. Navigera till **[!UICONTROL Assets]** > **[!UICONTROL Image Presets]**.
1. Välj en förinställning och välj sedan **[!UICONTROL Delete]**. Dynamic Media bekräftar att du vill ta bort det. Välj **[!UICONTROL Delete]** om du vill ta bort eller välj **[!UICONTROL Cancel]** om du vill återgå till bildförinställningar.

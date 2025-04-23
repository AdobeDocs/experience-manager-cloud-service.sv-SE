---
title: Hur hanterar jag  [!DNL Dynamic Media] mallar?
description: Lär dig hur du skapar  [!DNL Dynamic Media] mallar med en WYSIWYG-mallredigerare och inkluderar flera bilder och textlager för att snabbt skapa banners och flygblad och använda dem i program längre fram i kedjan.
hide: true
role: User
exl-id: 07de648e-4ae2-4524-8e05-3cf10bb6006d
source-git-commit: 5bdbd0c7273a1e8a650a87a7d0b0c9749f5e1030
workflow-type: tm+mt
source-wordcount: '3026'
ht-degree: 0%

---

# [!DNL Dynamic Media] mallar{#dynamic-media-templates}

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

Skapa anpassningsbara mallar i realtid för banners och flygblad med hjälp av [!DNL Dynamic Media]-mallar, en WYSIWYG-mallredigerare. Publicera din [!DNL Dynamic Media]-mall och använd den i program längre fram i kedjan. En [!DNL Dynamic Media]-mall innehåller bild- och textlager. Lägg till parametrar i bild- och textlagren i mallen och använd [[!DNL Dynamic Media] URL:er](https://experienceleague.adobe.com/en/docs/commerce-admin/content-design/wysiwyg/storage/catalog-urls-dynamic-media) för att flytta och ändra storlek på lagret och uppdatera innehållet i realtid.

Några av de viktigaste funktionerna:

* **[!DNL Dynamic Media]WYSIWYG mallredigerare:** Skapa anpassningsbara banners med bild- och textlager.
* **Lagerparameterisering:** Definiera dynamiska nyckelvärdepar för lager för att aktivera realtidsuppdateringar.
* **[!DNL Dynamic Media]URL-stöd:** Använd [!DNL Dynamic Media] URL:er för mallar och integrera anpassade värden från första eller tredje part-program.
* **Kontroll av lagersynlighet:** Dölj eller visa lager dynamiskt efter behov.
* **Smart storleksändring av text:** Justera automatiskt textstorleken så att den passar de angivna områdena.

Några av de största fördelarna med mallar i [!DNL Dynamic Media] är:

* **Optimera 1:1 Personalization:** Anpassa innehåll efter kundsignaler i realtid.
* **Minska den manuella ansträngningen:** Automatisera och snabba upp skapandet och hanteringen av innehåll.
* **Säkerställ enhetliga flerkanalsupplevelser:** Bevara varumärkets enhetlighet över alla kanaler.
* **Återanvänd innehåll effektivt:** Undvik engångsinnehåll och skalning med dynamiska, parametriserade mallar.
* **Minska riskerna:** Uppdatera priser, rabatter och länkar i realtid.
* **Förbättra kundengagemanget:** Skapa interaktiva, sammanhangsberoende upplevelser.

>[!NOTE]
>
>Kunder som prenumererar på SKU:n Förbättrade skyddsinställningar kan inte använda några [!DNL Dynamic Media]-funktioner, inklusive [!DNL Dynamic Media]-mallar, i det molntjänstprogrammet.

## Innan du börjar{#prerequisites-for-dynamic-media-wysiwyg-template}

Uppfyll följande krav för att skapa en [!DNL Dynamic Media]-mall och generera dess leverans-URL:

1. Åtkomst till [!DNL Dynamic Media].
1. På startsidan för [!DNL Assets View] har du en mapp i **[!UICONTROL Dynamic Media Assets]** där du kan spara mallen. [Skapa en mapp](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/assets-view/add-delete-assets-view) i ![Assets ](/help/assets/assets/Asset-icon.svg)**[!UICONTROL Assets]**för att replikera den mappen i **[!UICONTROL Dynamic Media Assets]**.
1. [Synkronisera bilderna som är tillgängliga i din [!DNL AEM Assets] instans med [!DNL Dynamic Media] för att använda dem för att skapa mallen](/help/assets/dynamic-media/config-dm.md).
1. Publicera bilderna som ska användas när mallen skapas för att generera leverans-URL:en för mallen när den har skapats. Leverans-URL:en kan användas i program längre fram i kedjan.
1. Om du vill använda ett annat teckensnitt än standardteckensnittet [!UICONTROL Adobe Sans F2] i mallens textlager [överför och publicerar du teckensnittsfilen till AEM och Dynamic Media samtidigt](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/assets-view/publish-assets-to-aem-and-dm?lang=en#dynamic-media-publish-mode-set-to-upon-activation). [De teckensnittsfilformat som stöds är: AFM, OTF, PFB, PFM, PhotoFont, TTC, TTF](https://experienceleague.adobe.com/en/docs/dynamic-media-classic/using/upload-publish/uploading-files#supported-asset-file-formats). Se även till att [bearbeta om](/help/assets/reprocessing-assets-view.md) befintliga teckensnitt för att använda dem. Mer information finns i [Teckensnitt](https://experienceleague.adobe.com/en/docs/dynamic-media-classic/using/support-files/fonts).<!--(On [!DNL Assets View] home page, click ![Assets](/help/assets/assets/Asset-icon.svg)**[!UICONTROL Assets]**, navigate to the font file location, select the font file one at a time and click ![Reprocess](/help/assets/assets/Refresh-docs.svg)**[!UICONTROL Reprocess]**)-->
1. verifiera följande i Touch-gränssnittet:
   * **[!UICONTROL [!DNL Dynamic Media] sync mode]** som är inställd på **[!UICONTROL Disabled by default]** på **[!UICONTROL Edit [!DNL Dynamic Media] Configuration page]** används inte på alla AEM-mappar (**[!UICONTROL Sync all content]** är avmarkerad). Mer information finns i [Konfigurera Dynamic Media Cloud Service](/help/assets/dynamic-media/config-dm.md).
   * **[!UICONTROL [!DNL Dynamic Media] sync mode]** är inställt på **[!UICONTROL Enable for subfolders]** för målmappen eller undermappen där du vill spara mallen när den har skapats. Mer information finns i [Konfigurera [!DNL Dynamic Media] Cloud Service](/help/assets/dynamic-media/config-dm.md).

## Skapa mallen [!DNL Dynamic Media]{#how-to-create-dynamic-media-template}

Utför följande steg för att skapa en [!DNL Dynamic Media]-mall:
<!--
1. Navigate to your [!DNL Assets View] and [create a folder](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/assets-view/add-delete-assets-view) in ![Assets](/help/assets/assets/Asset-icon.svg)**[!UICONTROL Assets]**. The folder tree in ![Assets](/help/assets/assets/Asset-icon.svg)**[!UICONTROL Assets]** replicates in **[!UICONTROL Dynamic Media Assets]**. Save your [!DNL Dynamic Media] template in this [!UICONTROL Dynamic Media Assets] folder.
1. Select ![Assets](/help/assets/assets/Asset-icon.svg)**[!UICONTROL Assets]** and [upload and publish your images to [!DNL AEM] and [!DNL Dynamic Media] simultaneously](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/assets-view/publish-assets-to-aem-and-dm#dynamic-media-publish-mode-set-to-upon-activation) to use them in creating the template. Publishing images is required to generate the template's delivery URL, after creating the template. The delivery URL can be used in downstream applications.
1. [Execute these asset uploading and publishing steps](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/assets-view/publish-assets-to-aem-and-dm?lang=en#dynamic-media-publish-mode-set-to-upon-activation) to upload and publish a font file to AEM and Dynamic Media simultaneously to use it in creating the template. [!UICONTROL Adobe Sans F2] is the only default font available in the text layer. [The supported font file formats are, AFM, OTF, PFB, PFM, PhotoFont, TTC, TTF](https://experienceleague.adobe.com/en/docs/dynamic-media-classic/using/upload-publish/uploading-files#supported-asset-file-formats). Ensure to [reprocess](/help/assets/reprocessing-assets-view.md) the existing fonts to use them in creating the template (On [!DNL Assets View] home page, click ![Assets](/help/assets/assets/Asset-icon.svg)**[!UICONTROL Assets]**, navigate to the font file location, select the font file one at a time and click ![Reprocess](/help/assets/assets/Refresh-docs.svg)**[!UICONTROL Reprocess]**). See [Fonts](https://experienceleague.adobe.com/en/docs/dynamic-media-classic/using/support-files/fonts) to know more about fonts.
-->
1. [Skapa en tom arbetsyta](#create-a-canvas)
1. [Lägga till bilder på arbetsytan](#add-images-to-the-canvas)
1. [Lägga till textlager på arbetsytan](#add-text-to-the-canvas)
1. [Redigera eller ta bort ett lager](#edit-or-delete-a-layer)
1. [Parameterlager](#parameterise-a-layer)

### Skapa en tom arbetsyta{#create-a-canvas}

Så här skapar du en tom arbetsyta:

1. Navigera till [!DNL Assets View], markera **[!UICONTROL Dynamic Media Assets]** i den vänstra panelen och navigera till din mapp för att spara mallen i den mappen.

   ![Dynamiska mediamallar](/help/assets/assets/DM-Assets1.png)

1. Välj **[!UICONTROL Create Template]**. Dialogrutan **[!UICONTROL New Template]** visas.
   ![Så här skapar du dynamiska mallar som kan anpassas i realtid](/help/assets/assets/new-template.png)
   >[!NOTE]
   >
   >  Mallen sparas på den plats där du skapar den. På startsidan för [!DNL Assets View] väljer du **[!UICONTROL Dynamic Media Assets]** och klickar på **[!UICONTROL Create Template]** för att spara mallen i rotmappen för **[!UICONTROL Dynamic Media Assets]**.

1. Ange ett mallnamn, definiera arbetsytans bredd och höjd och klicka på **[!UICONTROL Create]**. En tom arbetsyta visas med menyalternativ på båda sidor som du kan använda för att skapa mallen. Håll muspekaren över menyalternativen för att se deras verktygstips.
   ![anpassningsbar mall i realtid](/help/assets/assets/blank-canvas-page.png)

   >[!NOTE]
   >
   > Tillåtet intervall för bredd och höjd är mellan 50 och 5000.

**Menyalternativ i den högra rutan:** Använd dessa alternativ för att lägga till nödvändiga bilder och textlager på arbetsytan.

* ![DM-mallar](/help/assets/assets/add-image.svg): Klicka för att lägga till bilder på arbetsytan.
* ![anpassningsbara mallar](/help/assets/assets/add-text.svg): Klicka för att lägga till text på arbetsytan.
* ![anpassningsbara mallar](/help/assets/assets/show-layers-list.svg): Klicka för att visa listan över alla lager (bild och text) på arbetsytan. Alla bilder och all text som läggs till på arbetsytan representeras som separata lager.

**Menyalternativ i den vänstra rutan:** Använd dessa alternativ för följande vanliga redigeringsåtgärder.

* ![DM-mallar](/help/assets/assets/layer-selector.svg): Välj ![DM-mallar](/help/assets/assets/layer-selector.svg) och klicka på ett lager på arbetsytan för att markera det.
* ![mallar som stöder anpassning](/help/assets/assets/bring-forward.svg): Klicka på ![mallar som stöder anpassning](/help/assets/assets/bring-forward.svg) eller använd kortkommando, **Ctrl** + **]** (Windows) eller **Cmd** + **]** (Mac) för att föra ett markerat lager framåt.
* ![Så här skapar du en mall som enkelt kan anpassas](/help/assets/assets/send-backward.svg): Klicka på ![Skapa en mall som enkelt kan anpassas](/help/assets/assets/send-backward.svg) eller använd kortkommando, **Ctrl** + **[** (Windows) eller **Cmd** + **[** (Mac) för att skicka ett markerat lager bakåt.
* ![skapa en mall som kan anpassas direkt](/help/assets/assets/undo.svg): Klicka på ![skapa en mall som kan anpassas direkt](/help/assets/assets/undo.svg) eller använd kortkommando, **Ctrl** + **Z** (Windows) eller **Cmd** + **Z** (Mac) för att ångra den senaste åtgärden.
* ![mall för att skapa banners snabbt](/help/assets/assets/redo.svg): Klicka på mallen ![om du vill skapa banners snabbt](/help/assets/assets/redo.svg) eller använd kortkommando, **Ctrl** + **Y** (Windows) eller **Cmd** + **Y** (Mac) om du vill göra om den senaste åtgärden.
* ![mall för att snabbt skapa flygblad](/help/assets/assets/zoom-in.svg): Klicka på mallen ![om du vill skapa flygblad snabbt](/help/assets/assets/zoom-in.svg) eller använd kortkommando, **Ctrl** + **+** (Windows) eller **Cmd** + **+** (Mac) om du vill zooma in arbetsytan.
* ![mall för att skapa banners snabbt](/help/assets/assets/Zoom-out.svg): Klicka på mallen ![ om du vill skapa banners snabbt](/help/assets/assets/Zoom-out.svg) eller använd kortkommando, **Ctrl** + **-** (Windows) eller **Cmd** + **-** (Mac) om du vill zooma ut arbetsytan.
* Tryck på **Backsteg** eller **delete** för att ta bort det markerade lagret om ingen text eller egenskap redigeras.

Klicka på mallen ![om du vill skapa flygblad snabbt](/help/assets/assets/show-layers-list.svg) och välja fler alternativ (![](/help/assets/assets/three-dots.svg)) på lagret Canvas om du vill redigera arbetsytans dimensioner när du skapar mallen.
![](/help/assets/assets/edit-canvas1.png)

>[!NOTE]
>
> Mallar tillåter högst 20 lager, inklusive arbetsytan.

### Lägga till bilder på arbetsytan{#add-images-to-the-canvas}

Gör så här för att lägga till bilder på arbetsytan:

1. Klicka på ![skapa en banderoll på nolltid](/help/assets/assets/add-image.svg) för att öppna panelen [Resursväljare](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/manage/asset-selector/overview-asset-selector). På panelen visas de bilder i din AEM Assets-instans som synkroniseras med [!DNL Dynamic Media].
1. Bläddra i panelen eller använd nyckelord i sökfältet för att hitta en viss bild.
1. Dra och släpp en bild på arbetsytan för att använda den. Se [**[!UICONTROL Properties Panel]**](#reposition-resize-delete-a-layer) för att ändra storlek på eller flytta ett lager på arbetsytan.
   ![skapa en banderoll inom några sekunder](/help/assets/assets/add-image-to-canvas.png)

### Lägga till textlager på arbetsytan{#add-text-to-the-canvas}

Gör så här för att lägga till textlager på arbetsytan:

1. Klicka på ![skapa nya banderoller snabbt](/help/assets/assets/add-text.svg) för att lägga till ett textlager på arbetsytan och öppna panelen Egenskaper.
1. Markera lagret och klicka på texten för att uppdatera den.
1. Välj **[!UICONTROL Smart Text Resize]** på egenskapspanelen om du automatiskt vill justera textlängden och teckenstorleken så att den passar i det angivna området.
   ![bästa anpassningsbara banners](/help/assets/assets/add-text-layer.png)

Se [**[!UICONTROL Properties Panel]**](#reposition-resize-delete-a-layer) för att flytta, ändra storlek på, rotera eller ta bort lagret. Formatera texten till önskat teckensnitt, önskad storlek, färg, stil, justering (i lagret) genom att ändra deras värden i respektive fält under **[!UICONTROL Text]**-delen av panelen. Fältet **[!UICONTROL Font Family]** innehåller [!UICONTROL Adobe Sans F2] standardteckensnitt, de ombearbetade befintliga teckensnitten samt de nyligen överförda och publicerade teckensnitten. Mer information finns i punkt 5 i avsnittet [Innan du börjar](#prerequisites-for-dynamic-media-wysiwyg-template) ovan.

### Redigera eller ta bort ett lager {#edit-or-delete-a-layer}

Så här redigerar eller tar du bort ett lager på arbetsytan:

1. Klicka på ![mallar med stöd för dynamiska uppdateringar](/help/assets/assets/show-layers-list.svg) och markera lagret antingen på arbetsytan eller i listan Lager.
1. Klicka på **[!UICONTROL more options]** (![mallar med stöd för realtidsuppdateringar](/help/assets/assets/three-dots.svg)) om du vill redigera eller ta bort lagret.
1. Klicka på **[!UICONTROL Delete]** för att ta bort lagret.
1. Klicka på **[!UICONTROL Edit]** om du vill redigera lagret med [**[!UICONTROL Properties Panel]**](#reposition-resize-delete-a-layer).
   ![skapa banner snabbt](/help/assets/assets/dm-templates/edit-delete-layer.png)

### Egenskapspanelen{#properties-panel}

Navigera till ett lagers egenskapspanel:

1. Klicka på ![Skapa snabbt innehåll](/help/assets/assets/show-layers-list.svg).
1. Markera lagret i listan.

På den här panelen visas positionen för lagrets mittpunkt på arbetsytans plan (X- och Y-värden) och lagrets mått (bredd och höjd) tillsammans med textformateringsalternativ.

![skapa snabbt innehåll](/help/assets/assets/properties-panel.png)

Gå till egenskapspanelen för ett lager och markera ett annat lager på arbetsytan för att navigera till egenskapspanelen.


#### Flytta, ändra storlek på, rotera eller ta bort ett lager{#reposition-resize-delete-a-layer}

Se de här vanliga redigeringsåtgärderna för lager när du vill redigera text eller ett bildlager:

* **Flytta lagret:** Dra lagret så att det flyttas var som helst på arbetsytan. Den här åtgärden uppdaterar X- och Y-värdena på egenskapspanelen.
* **Ändra storlek på lagret:** Markera lagret och dra i dess kanthandtag för att ändra storlek på det. Den här åtgärden uppdaterar värdena för B (bredd) och H (höjd) på egenskapspanelen.
* **Rotera lagret:** Dra det fyrkantiga handtaget som är placerat lodrätt ovanför lagret för att rotera det runt dess mitt. Den här åtgärden uppdaterar vinkelvärdena på egenskapspanelen.
* **Ta bort lagret:** Tryck på **Backsteg** eller **delete** och klicka sedan på **[!UICONTROL Confirm]** för att ta bort ett markerat lager.

#### Textformateringsalternativ{#text-formatting-options-on-properties-panel}

Formatera texten till önskat teckensnitt, önskad storlek, färg, stil, justering (i lagret) genom att ändra deras värden i respektive fält under avsnittet **[!UICONTROL Text]** på panelen.
Inkludera **[!UICONTROL Smart Text Resize]**. [!UICONTROL Smart Text Resize] fungerar med algoritmen [Textpassning](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/text-formatting/r-copy-fitting) för att fylla texten optimalt i textområdet och förhindrar textspill och minimerar extra utrymme längst ned i texten.

![Skapa innehåll på nolltid](/help/assets/assets/smart-text-resize.png)

### Parameterlager {#parameterise-a-layer}

När du har skapat en mall med flera lager med bilder och texter, parametriseras de markerade lagren. När ett lager eller dess egenskap är parametriserad, hämtas ett nyckelvärdepar (kallas även parameter). Den här parametern kan inkluderas i mallens URL för att uppdatera lagrets position, storlek eller innehåll i realtid, vilket resulterar i att mallen anpassas på nolltid.

Så här parameteriserar du ett lager:

1. klicka på ![Skapa innehåll direkt](/help/assets/assets/show-layers-list.svg), markera ett lager och klicka på **[!UICONTROL Parameters]**. Panelen **[!UICONTROL Parameters]** visas.
1. Växla **[!UICONTROL Include Parameter]** för att parameterisera en egenskap. Se [Alternativ på panelen Parametrar](#parameterisation-options-or-allowed-parameters) om du vill veta hur egenskapen fungerar efter parametrisering.
1. **Valfritt:** Byt namn på parametern. Ett parameternamn har ett lagernamn följt av ett suffix. Alla parametriserade egenskaper för ett markerat lager delar samma lagernamn följt av ett varierande suffix. Byt namn på lagret genom att följa den semantiska namnkonventionen, så att när du tar med parametern i URL:en, förklarar parameternamnet själva lagrets innehåll eller dess syfte.
1. Klicka på **[!UICONTROL Save]**.
   ![skapa innehåll direkt](/help/assets/assets/parameterise-a-layer.png)
Om du vill växla mellan parameterpanelen för ett bild- och textlager markerar du lagret på arbetsytan och klickar på **[!UICONTROL Parameters]** .

#### Alternativet Parameterpanel {#parameterisation-options-or-allowed-parameters}

Parameteriserade egenskaper kan inkluderas som URL-parametrar i mallens URL för att redigera mallen i realtid med URL:en.

**Bildparametrar:**

**[!UICONTROL X]:** Inkludera om du vill flytta lagret vågrätt längs dess mittlinje, parallellt med mallplanets X-axel, genom att ändra parameterns värde i URL:en.
**[!UICONTROL Y]:** Inkludera om du vill flytta lagret lodrätt längs dess mittlinje, parallellt med mallplanets Y-axel, genom att ändra parameterns värde i URL:en.
**[!UICONTROL Width]:** Inkludera om du vill justera lagrets bredd genom att ändra parameterns värde i URL:en.
**[!UICONTROL Height]:** Inkludera om du vill justera lagrets höjd genom att ändra parameterns värde i URL:en.
**[!UICONTROL Hide]:** Inkludera om du vill dölja eller visa lagret i mallen med 0 (visa) och 1 (dölj).
**[!UICONTROL Source]:** Inkludera om du vill ersätta lagrets bild med en ny bild genom att ändra bildsökvägen i parameterns värde i URL:en.

**Textformateringsparametrar:**

Ta med parametrarna nedan om du vill redigera texten, teckensnittet, färgen och storleken från URL:en genom att uppdatera parametervärdena i URL:en.

**[!UICONTROL Text]:** Inkludera om du vill uppdatera text från URL:en.
**[!UICONTROL Font Family]:** Inkludera om du vill uppdatera textens teckensnitt från URL:en.
**[!UICONTROL Font Size]:** Inkludera om du vill uppdatera textens teckenstorlek från URL:en.
**[!UICONTROL Text color]:** Inkludera om du vill uppdatera textens teckenfärg från URL:en.

### Gruppera lager för att styra synligheten samtidigt{#group-layers}

Ett annat sätt att göra mallarna flexibla är att använda ett enda parameternamn för att styra flera lager. Den här strategin är användbar för parametern visibility (hide or show layers) för att uppdatera designen eller grafiken från en enda mall.

Följ de här stegen för att tilldela samma namn till parametrarna för att dölja (![skapa snabbt innehåll](/help/assets/assets/Visibility-icon.svg)) för flera lager, så att du kan dölja eller visa dem samtidigt.

1. Navigera till [**[!UICONTROL Properties Panel]**](#parameterise-a-layer) för ett lager.
1. Växla parametern **[!UICONTROL Hide]** om den inte är parameteriserad tidigare.
1. **Valfritt:** Byt namn på parametern **[!UICONTROL Hide]**.
1. Kopiera parametern **[!UICONTROL Hide]**.
1. Gå till panelen Parameter för andra lager genom att markera dem på arbetsytan och växla deras **[!UICONTROL Hide]**-parameter om de inte är parameteriserade.
1. Ersätt deras **[!UICONTROL Hide parameter]**-namn med det kopierade namnet.
1. Klicka på **[!UICONTROL Save]** om du vill gruppera lagren.
1. Utför steg 3 och sedan 4 i avsnittet [**[!UICONTROL Preview and Publish]**](#preview-and-publish-template-and-copy-template-deliver-url) för att se ändringarna.

## Förhandsgranska och publicera mallen för att kopiera leverans-URL:en{#preview-and-publish-template-and-copy-template-deliver-url}

Utför dessa steg för att förhandsgranska och publicera mallen och kopiera leverans-URL:en:

1. Klicka på **[!UICONTROL Preview]** på arbetsytans sida. Du kan också navigera till **[!UICONTROL Assets View]** **>** **[!UICONTROL Dynamic Media Assets]** **>** och välja mallen **>**, klicka **[!UICONTROL Edit Template]** **>** och klicka **[!UICONTROL Preview]**. Förhandsgranskningssidan visar mallen, dess parametrar (parametriserade lager och egenskaper), publiceringsstatus och alternativet **[!UICONTROL Publish]**.
1. Välj parametrar på panelen **[!UICONTROL Template Parameters]** om du vill redigera deras värden och omedelbart uppdatera innehåll, storlek, position eller textformatering för motsvarande mallager i förhandsgranskningen. Till exempel:
   1. Markera ett textlager och redigera texten eller
   1. Markera ett bildlager, klicka på ![skapa innehåll när du vill](/help/assets/assets/add-image.svg), markera en bild i resursväljaren och klicka på **[!UICONTROL Refresh]**.

   Mallen uppdateras omedelbart, visar den redigerade texten och ersätter den tidigare bilden med den nya. Dessutom återspeglar bildparametervärdet den nya bildsökvägen. På samma sätt kan du ändra storlek på ett lager genom att justera dess värden, och ändringarna tillämpas på mallen i realtid.
1. Välj parametern **[!UICONTROL Hide]** för [grupperade lager](#group-layers) i listan om du vill visa eller dölja dem tillsammans i mallen.
1. **Valfritt:** Ändra parametervärdet **[!UICONTROL Hide]** mellan 0 och 1 och klicka på **[!UICONTROL Refresh]** för att se ändringarna. Lager med samma **[!UICONTROL Hide]**-parameter döljs eller visas tillsammans. På samma sätt kan du styra lagrens synlighet från URL-adressen.

   ![skapar innehåll i farten](/help/assets/assets/dm-templates-publish-status.png)
Du kan också växla **[!UICONTROL Include all parameters]** för att redigera alla parametervärden som visas och se uppdateringarna i mallförhandsvisningen.
   <br>
1. Om du vill publicera mallen från förhandsgranskningssidan klickar du på **[!UICONTROL Publish]** och bekräftar att du vill publicera. Ett **[!UICONTROL Publish Complete]**-meddelande visas och publiceringsstatusen uppdateras till **[!UICONTROL Published]**.

### Kopiera leverans-URL

De valda parametrarna på sidan **[!UICONTROL Preview]** blir URL-parametrar i mall-URL:en.

Kontrollera att bilderna i mallen redan har publicerats till AEM och Dynamic Media för att generera mallens leverans-URL.

Utför följande steg för att kopiera mallens leverans-URL:

1. Klicka på **[!UICONTROL Copy URL]**. Dialogrutan **[!UICONTROL Copy URL]** visas. Markera och kopiera den URL som visas. Den första parametern i URL:en startar efter ett frågetecken **([!UICONTROL ?])** och ett nyckelvärdepar börjar med **[!UICONTROL $]** och slutar med **[!UICONTROL &]**. Nyckeln och värdet avgränsas med ett likhetstecken **([!UICONTROL =])**, med tangenten till vänster och värdet till höger.
1. Klistra in den här URL-adressen på webbläsarfliken och se den aktiva mallen. Anpassa mallen i realtid genom att uppdatera den obligatoriska parameterns värde (Key-värdet) i URL:en direkt, vilket visas i [steg 2](#preview-and-publish-template-and-copy-template-deliver-url) i avsnittet **Förhandsgranska och publicera** .
1. Använd den här URL:en för snabb försäljning av produkter och tjänster. Du kan dela den här URL:en med dina kunder eller integrera den på din webbplats eller i ett tredjepartsprogram för att visa banderollen och göra uppdateringar i realtid för den så att den speglar de pågående erbjudandena.

Lär dig att skapa en [!DNL Dynamic Media]-mall steg för steg i den här videon.
>[!VIDEO](https://video.tv.adobe.com/v/3443281)

## Uppdatera mallen i realtid från URL:en{#update-the-template-from-the-url}

Det kan vara tidsödande att redigera parametrar direkt i URL:en. Förenkla:

1. Kopiera URL-adressen och klistra in den i en anteckningsruta.
1. Använd Cmd+F (Mac) eller Ctrl+F (Windows) för att hitta och redigera parametervärdena. Till exempel:
   * Sök och ersätt bildbanor för bildlager.
   * Hitta lagrets [parametriserade](#parameterise-a-layer)-koordinater, bredd och höjd för att justera deras värden.
   * Redigera text, teckensnitt, färg, storlek eller justering för textlager.
   * Ändra synlighetsvärden mellan 0 och 1.

Klistra in den uppdaterade URL-adressen i webbläsaren för att visa ändringarna.

## Redigera mallen{#edit-the-template}

Redigera mallen genom att följa de här stegen:

1. Klicka på **[!UICONTROL Dynamic Media Assets]** på [!DNL Assets view].
2. Navigera till mallplatsen.
3. Markera mallen.
4. Klicka på **[!UICONTROL Edit Template]**. Mallens arbetsyta visar mallen och listan över alla dess lager på panelen Lager. Börja redigera mallen efter dina behov.

## Lägg till länken Call to Action (CTA) i mallagret{#add-CTA-in-dynamic-media-templates}

Omvandla en bild eller ett textlager i mallen [!DNL Dynamic Media] till en hyperlänk genom att lägga till en CTA-länk som dirigerar användarna till en målsida.

Så här lägger du till en CTA-länk till ett lager:

1. Navigera till mallplatsen, markera mallen och klicka på ![redigera](/help/assets/assets/edit-pen-icon.svg) **[!UICONTROL Edit Template]**. Mallen visas på arbetsytan.
1. Markera mallagret och [navigera till egenskapspanelen](#edit-or-delete-a-layer) för att lägga till en CTA-länk till det.
1. Välj **[!UICONTROL Add CTA]** på egenskapspanelen, ange mål-URL:en i fältet **[!UICONTROL URL]** och klicka på **[!UICONTROL Save]**.

   ![lägg till CTA](/help/assets/assets/add-cta.png)

1. Klicka på **[!UICONTROL Preview]** om du vill förhandsgranska mallen och se de definierade parametrarna.
1. Klicka på **[!UICONTROL Publish]** och välj **[!UICONTROL Yes]** för att publicera mallen, om den inte har publicerats tidigare.
1. Navigera till mappen där mallen sparas, markera den här mallen och klicka på ![informationssidan](/help/assets/assets/details-page-icon.svg) **[!UICONTROL Details]**.
1. Klicka på **[!UICONTROL Copy Options]** och välj **[!UICONTROL Copy Embed Code]**. Se till att publicera mallbilderna på [!DNL AEM and Dynamic Media] för att kopiera inbäddningskoden.

   ![kopiera inbäddningskod](/help/assets/assets/copy-options1.png)

   Här följer ett exempel på den inbäddade koden:

   ```json
    <div class="adobe-dynamicmedia-template-embed-container">
    <img id="<Image ID>>" src="<Image Source>>" alt="adobe dynamicmedia template" usemap="#adobe-dynamicmedia-template-map" width="800" height="300">
    <map name="adobe-dynamicmedia-template-map">
    <area shape="rect" coords="417,-60,817,340" href="https://business.adobe.com/products.html" alt="Layer with CTA" title="https://business.adobe.com/products.html" target="_blank">
    <area shape="rect" coords="6,206.57,129,231.43" href="https://business.adobe.com/products.html" alt="Layer with CTA" title="https://business.adobe.com/products.html" target="_blank">
    </map>
    </div>
   ```

1. Lägg till den kopierade inbäddningskoden i webbplatsens HTML-fil och kör den i webbläsaren för att visa mallen.

Klicka på CTA-elementet i mallen för att navigera till målsidan.

I den här stegvideon lär du dig hur du lägger till en CTA-länk i ett mallager.

>[!VIDEO](https://video.tv.adobe.com/v/3457616)

## Viktiga punkter att notera {#important-points-to-note}

* När du har skapat en mall med parametriserade bildlager för dynamiska uppdateringar måste du se till att de bilder som är avsedda för framtida uppdateringar har samma dimensioner som de parametriserade bilderna. Detta garanterar att bilderna passar perfekt i lagren utan att de flödar över eller lämnar tomma utrymmen. Mallen stöder för närvarande inte automatiska dimensionsjusteringar för att passa in bilder i lagren.
* Det finns inget stöd för delsträngar i ett textlager. Användaren kan inte använda olika teckensnittsegenskaper på delsträngar i ett textlager.
* Stöd för flera [!DNL Dynamic Media]-företag är för närvarande inte tillgängligt med [!DNL Dynamic Media]-mallar.
* Om du kopierar eller flyttar, visar målväljaren alla mappar (inklusive mappar som inte är synkroniserade [!DNL Dynamic Media]). För närvarande visas inte heller mallresurserna [!DNL Dynamic Media] (båda är begränsningar för målväljaren).
* Alla uppdateringsåtgärder för en mapp (till exempel Publicera eller Ta bort) från Assets-avsnittet påverkar de [!DNL Dynamic Media]-mallar som är tillgängliga i den mappen.
* Papperskorgen fungerar inte för [!DNL Dynamic Media]-mallar. Om en resurs flyttas till papperskorgen och sedan återställs, återställs resursen i AEM men inte på [!DNL Dynamic Media]. Samma sak gäller för [!DNL Dynamic Media]-mallar.

## Se även

1. Utforska [[!DNL Dynamic Media] och dess funktioner](/help/assets/dynamic-media/dynamic-media.md)
1. Utforska [[!DNL Dynamic Media] med OpenAPI-funktioner](/help/assets/dynamic-media-open-apis-overview.md)
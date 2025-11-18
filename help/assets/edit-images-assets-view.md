---
title: Redigera bilder
description: Redigera bilder med [!DNL Adobe Express] aktiverade alternativ och spara uppdaterade bilder som versioner.
role: User
exl-id: cfc4c7b7-da8c-4902-9935-0e3d4388b975
feature: Best Practices, Interactive Images, Smart Crop, Smart Imaging
source-git-commit: 744c76f29a37610313835074f2f13fdd8f098465
workflow-type: tm+mt
source-wordcount: '1128'
ht-degree: 0%

---

# Redigera bilder i [!DNL Assets view] {#edit-images-in-assets-view}

Assets-vyns gränssnitt möjliggör grundläggande bildredigering som drivs av Adobe Express, integrerat i UI:t. Denna redigering inkluderar storleksanpassning, bakgrundsborttagning, beskärning och konvertering mellan JPEG- och PNG-format. Dessutom möjliggör det avancerad redigering via Adobe Express-gränssnittet som är inbäddat i Assets-vyns gränssnitt.

Efter att ha redigerat en bild kan du spara den nya bilden som en ny version. Versionshantering hjälper dig att återgå till den ursprungliga tillgången senare om det behövs. För att redigera en bild, [öppna dess förhandsvisning](https://experienceleague.adobe.com/en/docs/experience-manager-assets-essentials/help/navigate-view#preview-assets) och klicka på **Redigera bild**.

>[!NOTE]
>
>Du kan redigera bilder av PNG- och JPEG-filtyper med hjälp av [!DNL Adobe Express].

<!--The editing actions that are available are Spot healing, Crop and straighten, Resize image, and Adjust image.-->

## Redigera bild {#edit-image}

Gå till Assets view UI, använd länken - [Assets View](https://experience.adobe.com/#/assets) och välj rätt arkiv. För att få tillgång, kontakta din organisations administratör.
För ytterligare referensinformation, se - [Kom igång med Adobe Experience Manager Assets View](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/assets-view/get-started-assets-view), [Förstå användargränssnittet](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/assets-view/navigate-assets-view#understand-interface-navigation) för Assets View och [Assets View användningsfall](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/assets-view/get-started-assets-view#use-cases).
<!--
>[!CONTEXTUALHELP]
>id="assets_express_integration"
>title="Adobe Express Integration"
>abstract="Easy and intuitive image-editing tools powered by Adobe Express available directly within AEM Assets to increase content reuse and accelerate content velocity."-->

### Redigera bild i tillgångsvyn med Adobe Express {#edit-image-on-assets-view-using-adobe-express}

Efter att ha navigerat till Assets View, klicka på **Assets**, välj en bild och klicka sedan på **Redigera** från den övre skenan. Den nya skärmen visar de tillgängliga redigeringsalternativen som drivs av Adobe Express, vilka inkluderar storleksanpassning, bakgrundsborttagning, beskärning och konvertering mellan JPEG- och PNG-format.

#### Ändra storlek på bilden {#resize-image-using-express}

Att ändra storlek på en bild till en specifik storlek är ett populärt användningsområde. Assets View låter dig snabbt ändra storlek på bilder för att passa de vanliga fotostorlekarna genom att tillhandahålla förberäknade nya upplösningar för specifika fotostorlekar. För att ändra storlek på bilden med Assets View, följ stegen nedan:

1. Klicka på **Ändra storlek på bilden** från vänstra rutan. En dialogruta visar bildändringarna som drivs av Adobe Express.
1. Välj rätt sociala medieplattform från listan för Storleksändring och välj bildstorleken från de alternativ som visas.
1. Skala bilden om det behövs med hjälp av **fältet Bildskalan** .
1. Klicka **[!UICONTROL Apply]** för att göra dina ändringar.
   ![Bildredigering med Adobe Express](assets/adobe-express-resize-image.png)

   Din redigerade bild finns tillgänglig för nedladdning. Du kan antingen spara den redigerade tillgången som en ny version av samma tillgång eller spara den som en ny tillgång.
   ![Spara bild med Adobe Express](assets/adobe-express-resize-save.png)

#### Ta bort bakgrund {#remove-background-using-express}

Du kan ta bort bakgrund från en bild genom att följa stegen nedan:

1. Klicka på **Ta bort bakgrund** från vänstra rutan. Experience Manager Assets visar bilden utan bakgrund.
1. Klicka **[!UICONTROL Apply]** för att göra dina ändringar.
   ![Spara bild med Adobe Express](assets/adobe-express-remove-background.png)

   Din redigerade bild finns tillgänglig för nedladdning. Du kan antingen spara den redigerade tillgången som en ny version av samma tillgång eller spara den som en ny tillgång.

#### Beskär bild {#crop-image-using-express}

Att omvandla en bild till perfekt storlek är enkelt med inbäddade [!DNL Adobe Express] snabba åtgärder.

1. Klicka **[!UICONTROL Crop Image]** från vänstra rutan.
2. Dra handtagen i hörnen av bilden för att skapa önskad beskärning.
3. Klicka på **[!UICONTROL Apply]**.
   ![Spara bild med Adobe Express](assets/adobe-express-crop-image.png)
Den beskurna bilden finns tillgänglig för nedladdning. Du kan antingen spara den redigerade tillgången som en ny version av samma tillgång eller spara den som en ny tillgång.

#### Konvertera JPEG till PNG {#convert-image-types-using-express}

Du kan snabbt konvertera mellan JPEG- och PNG-bildformat med Adobe Express. Utför följande steg:

1. Klicka på **JPEG till PNG** eller **PNG till JPEG** från vänstra rutan.
   <!--![Convert to PNG with Adobe Express](/help/using/assets/adobe-express-convert-image.png)-->
1. Klicka på **[!UICONTROL Download]**.

#### Begränsningar {#limitations-adobe-express}

* Stödd bildupplösning: Minimum - 50 pixlar, Maximum - 6000 pixlar per dimension.
* Maximal filstorlek som stöds: 17 MB.

### Redigera bilder i Adobe Express inbyggda redigerare {#edit-images-in-adobe-express-embedded-editor}

Användare med Express-behörighet kan använda den inbyggda Express-redigeraren från Assets View för att enkelt redigera innehåll och skapa nytt innehåll med GenAI från Adobe Firefly. Denna funktion förbättrar återanvändning av innehåll och ökar innehållets hastighet. Du kan också använda fördefinierade element för att få din asset att se fantastisk ut eller utföra snabba åtgärder för att redigera din bild med bara några klick.

![uttryck i Essentials UI](/help/assets/assets/express-in-essentials-ui.jpg)
För att redigera bilder med inbäddad [!DNL Adobe Express] redigerare, följ stegen nedan:

1. Gå till AEM Assets View via länken - [AEM Assets View](https://experience.adobe.com/#/assets) och välj rätt arkiv.
1. Klicka på **Tillgångar**, öppna en mapp och välj en bild.
1. Klicka på Öppna **i Adobe Express**. Bilden öppnas på en expressduk.
1. Gör de nödvändiga ändringarna i bilden.
1. Om ditt projekt kräver att du lägger till fler sidor, klicka **på Lägg till**, välj tillgångar, gå in i en mapp, välj en bild att ta till canvas-sidan och utför sedan de nödvändiga redigeringarna av bilden.
1. För att spara en eller flera tillgångar, klicka på **Spara**. Spardialogrutan visar sparalternativen. För att välja mellan sparalternativen, följ en av instruktionerna nedan som stämmer överens med dina behov:
   1. För att spara en enda sida, klicka på **Spara som version** för att exportera bilden som en ny version (behåll originalformatet), och spara den i samma mapp.

   1. För att spara en enda sida, klicka på **Spara som en ny tillgång** för att exportera tillgången till ett annat format och spara den i valfri mapp som en ny tillgång.

   1. För att spara en enda sida från flera sidor, klicka på **Spara som version** för att spara tillgången i dess ursprungliga format och plats.

   1. För att spara flera sidor eller en enda sida bland flera sidor, klicka på **Spara som ny tillgång**. Denna åtgärd exporterar enskilda eller flera tillgångar till valfri mapp och sparar dem som nya tillgångar eller tillgångar i originalet eller ett annat format.

1. I dialogrutan Spara:
   1. Ange ett namn på filen i **fältet Spara som** .
   1. Välj en destinationsmapp.
   1. Valfritt: Ange detaljer som projekt- eller kampanjnamn, nyckelord, kanaler, tidsram och region.
1. Klicka på **Spara som version** eller **Spara som ny tillgång** för att spara tillgången/tillgångarna.

#### Begränsningar med att redigera bilder i Express Editor {#limitations-of-editing-images-in-the-express-editor}

* Stödd filtyp: JPEG eller PNG.
* Maximal filstorlek som stöds: 40 MB.
* Stödd bredd och höjd: 65MP (till exempel 8K x 8K eller 16K x 4K).
* Ladda om sidan för att se den senaste sparade nya tillgången i källmappen.

### Skapa nya tillgångar med Adobe Express {#create-new-embedded-editor}

[!DNL Assets view] Gör det möjligt att skapa en ny mall från grunden med en [!DNL Adobe Express] inbäddad editor. För att skapa en ny tillgång med , [!DNL Adobe Express]utför följande steg:

1. Gå till **[!UICONTROL My Workspace]** och klicka **[!UICONTROL Create]** inom Adobe Express-bannern som visas högst upp. [!DNL Adobe Express] Tom duk visas i användargränssnittet [!DNL Assets view] .
1. Skapa ditt innehåll med hjälp av [mallar](https://helpx.adobe.com/in/express/using/work-with-templates.html). Annars, navigera till **[!UICONTROL Your Stuff]** för att ändra befintligt innehåll.
1. När du är klar med redigeringen, klicka på **[!UICONTROL Save]**.
1. Ange destinationsväg för den skapade tillgången och klicka **[!UICONTROL Save as new asset]** på .

#### Begränsningar {#limitations}

* Du kan bara ändra bilder och `JPEG` `PNG` formattyper.
* Tillgångsstorleken måste vara mindre än 80 MB för stationära enheter och 40 MB för mobila enheter.
* Stödd bredd- och höjdintervall är mellan 50 och 8000 pixlar.
* Du kan spara en bild i `PDF`, `JPEG`, eller `PNG` format.

<!--
## Edit images using [!DNL Adobe Photoshop Express] {#edit-using-photoshop-express}

<!--
After editing an image, you can save the new image as a new version. Versioning helps you to revert to the original asset later, if needed. To edit an image, [open its preview](navigate-assets-view.md#preview-assets) and click **[!UICONTROL Edit Image]** ![edit icon](assets/do-not-localize/edit-icon.png) from the rail on the right.

![Options to edit an image](assets/edit-image2.png)

*Figure: The options to edit images are powered by [!DNL Adobe Photoshop Express].*
-->
<!--
### Touch up images {#spot-heal-images-using-photoshop-express}

If there are minor spots or small objects on an image, you can edit and remove the spots using the spot healing feature provided by Adobe Photoshop.

The brush samples the retouched area and makes the repaired pixels blend seamlessly into the rest of the image. Use a brush size that is only slightly larger than the spot you want to fix.

![Spot healing edit option](assets/edit-spot-healing.png)

<!-- 
TBD: See if we should give backlinks to PS docs for these concepts.
For more information about how Spot Healing works in Photoshop, see [retouching and repairing photos](https://helpx.adobe.com/photoshop/using/retouching-repairing-images.html). 
-->
<!-- 
### Crop and straighten images {#crop-straighten-images-using-photoshop-express}

Using the crop and straighten option that you can do basic cropping, rotate image, flip it horizontally or vertically, and crop it to dimensions suitable for popular social media websites.

To save your edits, click **[!UICONTROL Crop Image]**. After editing, you can save the new image as a version.

![Option to crop and straighten](assets/edit-crop-straighten.png)

Many default options let you crop your image to the best proportions that fit various social media profiles and posts.

### Resize image {#resize-image-using-photoshop-express}

You can view the common photo sizes in centimeters or inches to know the dimensions. By default, the resizing method retains the aspect ratio. To manually override the aspect ratio, click ![](assets/do-not-localize/lock-closed-icon.png).

Enter the dimensions and click **[!UICONTROL Resize Image]** to resize the image. Before you save the changes as a version, you can either undo all the changes done before saving by clicking [!UICONTROL Undo] or you can change the specific step in the editing process by clicking [!UICONTROL Revert].

![Options when resizing an image](assets/resize-image.png)

### Adjust image {#adjust-image-using-photoshop-express}

[!DNL Assets view] lets you adjust the color, tone, contrast, and more, with just a few clicks. Click **[!UICONTROL Adjust image]** in the edit window. The following options are available in the right sidebar:

* **Popular**: [!UICONTROL High Contrast & Detail], [!UICONTROL Desaturated Contrast], [!UICONTROL Aged Photo], [!UICONTROL B&W Soft], and [!UICONTROL B&W Sepia Tone].
* **Color**: [!UICONTROL Natural], [!UICONTROL Bright], [!UICONTROL High Contrast], [!UICONTROL High Contrast & Detail], [!UICONTROL Vivid], and [!UICONTROL Matte].
* **Creative**: [!UICONTROL Desaturated Contrast], [!UICONTROL Cool Light], [!UICONTROL Turquoise & Red], [!UICONTROL Soft Mist], [!UICONTROL Vintage Instant], [!UICONTROL Warm Contrast], [!UICONTROL Flat & Green], [!UICONTROL Red Lift Matte], [!UICONTROL Warm Shadows], and [!UICONTROL Aged Photo].
* **B&W**: [!UICONTROL B&W Landscape], [!UICONTROL B&W High Contrast], [!UICONTROL B&W Punch], [!UICONTROL B&W Low Contrast], [!UICONTROL B&W Flat], [!UICONTROL B&W Soft], [!UICONTROL B&W Infrared], [!UICONTROL B&W Selenium Tone], [!UICONTROL B&W Sepia Tone], and [!UICONTROL B&W Split Tone].
* **Vignetting**: [!UICONTROL None], [!UICONTROL Light], [!UICONTROL Medium], and [!UICONTROL Heavy].

![Adjust image by editing](assets/adjust-image.png)

<!--
TBD: Insert a video of the available social media options.
-->

### Nästa steg {#next-steps}

* Ge produktfeedback via [!UICONTROL Feedback] alternativet som finns i användargränssnittet för tillgångsvy.

* Ge dokumentationsfeedback genom att [!UICONTROL Edit this page] ![redigera sidan](assets/do-not-localize/edit-page.png) eller [!UICONTROL Log an issue] ![skapa ett GitHub-nummer](assets/do-not-localize/github-issue.png) tillgängligt i högra sidofältet.

* Kontakta [kundtjänst](https://experienceleague.adobe.com/?support-solution=General#support)

>[!MORELIKETHIS]
>
>* [Snabba åtgärder i Adobe Express](https://helpx.adobe.com/in/express/using/resize-image.html)
>* [Visa versionshistorik för en tillgång](navigate-assets-view.md)

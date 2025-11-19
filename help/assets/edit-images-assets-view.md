---
title: Redigera bilder
description: Redigera bilder med  [!DNL Adobe Express] aktiverade alternativ och spara uppdaterade bilder som versioner.
role: User
exl-id: cfc4c7b7-da8c-4902-9935-0e3d4388b975
feature: Best Practices, Interactive Images, Smart Crop, Smart Imaging
source-git-commit: cbda4b0735190f0fcaaa1c573e4fc327ab903de1
workflow-type: tm+mt
source-wordcount: '1133'
ht-degree: 0%

---

# Redigera bilder i [!DNL Assets view] {#edit-images-in-assets-view}

Assets vygränssnitt möjliggör grundläggande bildredigering med Adobe Express i botten, integrerad i användargränssnittet. Den här redigeringen inkluderar storleksändring, borttagning av bakgrund, beskärning och konvertering mellan JPEG- och PNG-format. Dessutom går det att redigera i Adobe Express-gränssnittet Inbäddat i Assets-visningsgränssnittet.

När du har redigerat en bild kan du spara den nya bilden som en ny version. Versionshantering hjälper dig att återgå till den ursprungliga resursen senare om det behövs. Om du vill redigera en bild [öppnar du förhandsvisningen](https://experienceleague.adobe.com/en/docs/experience-manager-assets-essentials/help/navigate-view#preview-assets) och klickar på **Redigera bild**.

>[!NOTE]
>
>Du kan redigera bilder av filtyperna PNG och JPEG med [!DNL Adobe Express].

<!--The editing actions that are available are Spot healing, Crop and straighten, Resize image, and Adjust image.-->

## Redigera bild {#edit-image}

Gå till användargränssnittet för Assets-vyn med hjälp av länken [Assets-vy](https://experience.adobe.com/#/assets) och välja rätt databas. Kontakta organisationens administratör för att få åtkomst.
Ytterligare referensinformation finns i - [Kom igång med Adobe Experience Manager Assets View](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/assets-view/get-started-assets-view), [Förstå användargränssnittet i Assets-vyn](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/assets-view/navigate-assets-view#understand-interface-navigation) och [Assets View-användningsexempel](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/assets-view/get-started-assets-view#use-cases).
<!--
>[!CONTEXTUALHELP]
>id="assets_express_integration"
>title="Adobe Express Integration"
>abstract="Easy and intuitive image-editing tools powered by Adobe Express available directly within AEM Assets to increase content reuse and accelerate content velocity."-->

### Redigera bild i Assets View med Adobe Express {#edit-image-on-assets-view-using-adobe-express}

Klicka på **Assets**, markera en bild och sedan på **Redigera** i den övre listen när du har navigerat till Assets-vyn. På den nya skärmen visas de tillgängliga redigeringsalternativen som bygger på Adobe Express, bland annat storleksändring, borttagning av bakgrund, beskärning och konvertering mellan JPEG- och PNG-format.

#### Ändra bildstorlek {#resize-image-using-express}

Att ändra storlek på en bild till en viss storlek är ett vanligt användningsexempel. I Assets View kan du snabbt ändra storlek på bilder så att de passar de vanliga fotostorlekarna genom att tillhandahålla förberäknade nya upplösningar för specifika fotostorlekar. Följ stegen nedan om du vill ändra storlek på bilden med Assets View:

1. Klicka på **Ändra storlek på bild** i den vänstra rutan. I en dialogruta visas hur du ändrar storlek på bilder med Adobe Express.
1. Välj lämplig plattform för sociala medier i listrutan Ändra storlek och välj bildstorlek bland de alternativ som visas.
1. Skala bilden, om det behövs, med fältet **Bildskala**.
1. Klicka på **[!UICONTROL Apply]** för att tillämpa ändringarna.
   ![Bildredigering med Adobe Express](assets/adobe-express-resize-image.png)

   Den redigerade bilden kan hämtas. Du kan antingen spara den redigerade resursen som en ny version av samma resurs eller spara den som en ny resurs.
   ![Spara bild med Adobe Express](assets/adobe-express-resize-save.png)

#### Ta bort bakgrund {#remove-background-using-express}

Du kan ta bort bakgrunden från en bild genom att följa stegen nedan:

1. Klicka på **Ta bort bakgrund** i den vänstra rutan. Experience Manager Assets visar bilden utan bakgrund.
1. Klicka på **[!UICONTROL Apply]** för att tillämpa ändringarna.
   ![Spara bild med Adobe Express](assets/adobe-express-remove-background.png)

   Den redigerade bilden kan hämtas. Du kan antingen spara den redigerade resursen som en ny version av samma resurs eller spara den som en ny resurs.

#### Beskär bild {#crop-image-using-express}

Det är enkelt att omvandla en bild till en perfekt storlek med inbäddade [!DNL Adobe Express] snabbåtgärder.

1. Klicka på **[!UICONTROL Crop Image]** i den vänstra rutan.
2. Dra handtagen i hörnen av bilden för att skapa den önskade beskärningen.
3. Klicka på **[!UICONTROL Apply]**.
   ![Spara bild med Adobe Express](assets/adobe-express-crop-image.png)
Den beskurna bilden kan hämtas. Du kan antingen spara den redigerade resursen som en ny version av samma resurs eller spara den som en ny resurs.

#### Konvertera JPEG till PNG {#convert-image-types-using-express}

Du kan snabbt konvertera mellan JPEG- och PNG-bildformat med Adobe Express. Utför följande steg:

1. Klicka på **JPEG till PNG** eller **PNG till JPEG** i den vänstra rutan.
   <!--![Convert to PNG with Adobe Express](/help/using/assets/adobe-express-convert-image.png)-->
1. Klicka på **[!UICONTROL Download]**.

#### Begränsningar {#limitations-adobe-express}

* Bildupplösning som stöds: Minimal - 50 pixlar, Maximal - 6 000 pixlar per dimension.
* Största filstorlek som stöds: 17 MB.

### Redigera bilder i Adobe Express inbäddade redigerare {#edit-images-in-adobe-express-embedded-editor}

Användare med Express-berättigande kan använda den inbäddade Express-redigeraren inifrån Assets View för att enkelt redigera innehåll och skapa nytt innehåll med GenAI från Adobe Firefly. Den här funktionen förbättrar återanvändning av innehåll och snabbar upp innehållets hastighet. Du kan också använda fördefinierade element för att få dina resurser att se fantastiska ut eller utföra snabba åtgärder för att redigera bilden med bara några klick.

![express i grundläggande gränssnitt](/help/assets/assets/express-in-essentials-ui.jpg)
Följ stegen nedan om du vill redigera bilder med den inbäddade [!DNL Adobe Express] redigeraren:

1. Gå till AEM Assets View med länken - [AEM Assets View](https://experience.adobe.com/#/assets) och välj rätt databas.
1. Klicka på **Assets**, ange en mapp och markera en bild.
1. Klicka på **Öppna i Adobe Express**. Bilden öppnas på en snabbarbetsyta.
1. Gör de ändringar du vill i bilden.
1. Om ditt projekt kräver att du lägger till fler sidor klickar du på **Lägg till**, väljer resurser, anger en mapp, väljer en bild som ska läggas till på arbetsytesidan och utför sedan de redigeringar som krävs på bilden.
1. Om du vill spara en eller flera resurser klickar du på **Spara**. I dialogrutan Spara visas alternativen för att spara. Om du vill välja mellan alternativen för att spara följer du någon av instruktionerna nedan som passar dina krav:
   1. Om du vill spara en sida klickar du på **Spara som version** för att exportera bilden som en ny version (med originalformatet) och spara den i samma mapp.

   1. Om du vill spara en enstaka sida klickar du på **Spara som ny resurs** för att exportera resursen till ett annat format och spara den i en mapp som en ny resurs.

   1. Om du vill spara en sida från flera sidor klickar du på **Spara som version** för att spara resursen i dess ursprungliga format och på dess ursprungliga plats.

   1. Om du vill spara flera sidor eller en sida mellan flera sidor klickar du på **Spara som ny resurs**. Den här åtgärden exporterar en eller flera resurser till valfri mapp och sparar dem som nya resurser i det ursprungliga eller ett annat format.

1. I dialogrutan Spara:
   1. Ange ett namn för filen i fältet **Spara som**.
   1. Välj en målmapp.
   1. Valfritt: Ange information som projekt- eller kampanjnamn, nyckelord, kanaler, tidsram och region.
1. Klicka på **Spara som version** eller **Spara som ny resurs** för att spara resursen/resurserna.

#### Begränsningar för redigering av bilder i Express Editor {#limitations-of-editing-images-in-the-express-editor}

* Filtyp som stöds: JPEG eller PNG.
* Största filstorlek som stöds: 40 MB.
* Bredd- och höjdintervall som stöds: 65 MP (t.ex. 8K x 8K eller 16K x 4K).
* Läs in sidan igen för att se den senaste sparade nya resursen i källmappen.

### Skapa nya resurser med Adobe Express {#create-new-embedded-editor}

Med [!DNL Assets view] kan du skapa en ny mall från grunden med den inbäddade [!DNL Adobe Express]-redigeraren. Så här skapar du en ny resurs med [!DNL Adobe Express]:

1. Navigera till **[!UICONTROL My Workspace]** och klicka på **[!UICONTROL Create]** i den Adobe Express-banderoll som visas högst upp. [!DNL Adobe Express] tom arbetsyta visas i användargränssnittet för [!DNL Assets view].
1. Skapa ditt innehåll med [Mallar](https://helpx.adobe.com/in/express/using/work-with-templates.html). I annat fall går du till **[!UICONTROL Your Stuff]** för att ändra befintligt innehåll.
1. Klicka på **[!UICONTROL Save]** när du är klar med redigeringen.
1. Ange målsökväg för den skapade resursen och klicka på **[!UICONTROL Save as new asset]**.

#### Begränsningar {#limitations}

* Du kan bara ändra bilder av formaten `JPEG` och `PNG`.
* Resursens storlek måste vara mindre än 80 MB för stationära enheter och 40 MB för mobila enheter.
* Bredd- och höjdintervall som stöds är 65 MP (till exempel 8K x 8K eller 16K x 4K).
* Du kan spara en bild i formaten `PDF`, `JPEG` eller `PNG`.

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

* Ge produktfeedback med alternativet [!UICONTROL Feedback] som finns i användargränssnittet i Assets-vyn.

* Ge feedback genom att [!UICONTROL Edit this page] ![redigera sidan](assets/do-not-localize/edit-page.png) eller [!UICONTROL Log an issue] ![skapa ett GitHub-problem](assets/do-not-localize/github-issue.png) som är tillgängligt på den högra sidopanelen.

* Kontakta [kundtjänst](https://experienceleague.adobe.com/?support-solution=General#support)

>[!MORELIKETHIS]
>
>* [Snabbåtgärder i Adobe Express](https://helpx.adobe.com/in/express/using/resize-image.html)
>* [Visa versionshistorik för en resurs](navigate-assets-view.md)

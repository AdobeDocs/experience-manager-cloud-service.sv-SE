---
title: Redigera bilder
description: Redigera bilder med [!DNL Adobe Express] och spara uppdaterade bilder som versioner.
role: User
exl-id: cfc4c7b7-da8c-4902-9935-0e3d4388b975
feature: Best Practices, Interactive Images, Smart Crop, Smart Imaging
source-git-commit: ab2cf8007546f538ce54ff3e0b92bb0ef399c758
workflow-type: tm+mt
source-wordcount: '836'
ht-degree: 0%

---

# Redigera bilder i [!DNL Assets view] {#edit-images}

[!DNL Assets view] innehåller användarvänliga redigeringsalternativ som bygger på [!DNL Adobe Express]. De redigeringsåtgärder som är tillgängliga med [!DNL Adobe Express] är Ändra storlek på bild, Ta bort bakgrund, Beskär bild och Konvertera JPEG till PNG eller vice versa.

När du har redigerat en bild kan du spara den nya bilden som en ny version. Versionshantering hjälper dig att vid behov återställa den ursprungliga resursen senare. Dessutom är versionshantering endast tillgänglig för PNG-filtyperna, vilket innebär att JPG konverteras automatiskt till PNG när du försöker ta bort bakgrund från en JPG-filtyp. Om du vill redigera en bild [öppna förhandsgranskningen](navigate-assets-view.md) och klicka **[!UICONTROL Edit Image]**.

>[!NOTE]
>
>Du kan redigera bilder av filtyperna PNG och JPEG med [!DNL Adobe Express].

<!--The editing actions that are available are Spot healing, Crop and straighten, Resize image, and Adjust image.-->

## Redigera bilder med Adobe Express {#edit-using-express}

>[!CONTEXTUALHELP]
>id="assets_express_integration"
>title="Integrering av Adobe Expresser"
>abstract="Enkla och intuitiva bildredigeringsverktyg med Adobe Express som är tillgängliga direkt i AEM Assets för att öka återanvändningen och snabba upp innehållets hastighet."

### Ändra bildstorlek {#resize-image-using-express}

Att ändra storlek på en bild till en viss storlek är ett vanligt användningsexempel. [!DNL Assets view] Med kan du snabbt ändra storlek på bilden så att den passar de vanliga fotostorlekarna genom att tillhandahålla förberäknade nya upplösningar för specifika fotostorlekar. Ändra storlek på bilden med [!DNL Assets view]följer du stegen nedan:

1. Välj en bild från [!DNL Experience Manager] Resurskatalogen och klicka på **Redigera**.
2. Klicka **[!UICONTROL Resize Image]** från de snabbåtgärder som är tillgängliga i den vänstra rutan.
3. Välj lämplig plattform för sociala medier från **[!UICONTROL Resize for]** och välj bildstorlek bland de alternativ som visas.
4. Skalförändra bilden, om det behövs, med **[!UICONTROL Image Scale]** fält.
5. Klicka **[!UICONTROL Apply]** för att tillämpa ändringarna.
   ![Bildredigering med Adobe Express](assets/adobe-express-resize-image.png)

   Den redigerade bilden kan hämtas. Du kan antingen spara den redigerade resursen som en ny version av samma resurs eller spara den som en ny resurs.
   ![Spara bild med Adobe Express](assets/adobe-express-resize-save.png)

### Ta bort bakgrund {#remove-background-using-express}

Du kan ta bort bakgrunden från en bild med några enkla steg enligt nedan:

1. Välj en bild från [!DNL Experience Manager] Resurskatalogen och klicka på **Redigera**.
2. Klicka **[!UICONTROL Remove Background]** från de snabbåtgärder som är tillgängliga i den vänstra rutan. Experience Manager Assets visar bilden utan bakgrund.
3. Klicka **[!UICONTROL Apply]** för att tillämpa ändringarna.
   ![Spara bild med Adobe Express](assets/adobe-express-remove-background.png)

### Beskär bild {#crop-image-using-express}

Det är enkelt att omvandla en bild till en perfekt storlek med hjälp av inbäddade [!DNL Adobe Express] snabba åtgärder.

1. Välj en bild från [!DNL Experience Manager] Resurskatalogen och klicka på **Redigera**.
2. Klicka **[!UICONTROL Crop Image]** från de snabbåtgärder som är tillgängliga i den vänstra rutan.
3. Dra handtagen i hörnen av bilden för att skapa den önskade beskärningen.
4. Klicka på **[!UICONTROL Apply]**.
   ![Spara bild med Adobe Express](assets/adobe-express-crop-image.png)
Den beskurna bilden kan hämtas. Du kan antingen spara den redigerade resursen som en ny version av samma resurs eller spara den som en ny resurs.

### Konvertera JPEG till PNG {#convert-jpeg-to-png-using-express}

Du kan snabbt konvertera en JPEG-bild till ett PNG-format med Adobe Express. Utför följande steg:

1. Välj en bild från [!DNL Experience Manager] Resurskatalogen och klicka på **Redigera**.
2. Klicka **[!UICONTROL Convert to PNG]** från de snabbåtgärder som är tillgängliga i den vänstra rutan.
   <!--![Convert to PNG with Adobe Express](/help/using/assets/adobe-express-convert-image.png)-->
3. Klicka på **[!UICONTROL Apply]**.
4. Navigera till **[!UICONTROL Save as on the top right]** och klicka **[!UICONTROL Save as new asset]**.

### Konvertera PNG till JPEG {#convert-png-to-jpeg-using-express}

Du kan snabbt konvertera en PNG-bild till ett JPEG-format med Adobe Express. Utför följande steg:

1. Välj en bild från [!DNL Experience Manager] Resurskatalogen och klicka på **Redigera**.
2. Klicka **[!UICONTROL Convert to JPEG]** från de snabbåtgärder som är tillgängliga i den vänstra rutan.
3. Klicka på **[!UICONTROL Apply]**.
4. Navigera till **[!UICONTROL Save as on the top right]** och klicka **[!UICONTROL Save as new asset]**.

### Begränsningar {#limitations-adobe-express}

* Bildupplösning som stöds: Minimal - 50 pixlar, Maximal - 6 000 pixlar per dimension.

* Största filstorlek som stöds: 17 MB.

## Redigera bilder med Adobe Expressens inbäddade redigerare {#edit-using-embedded-editor}

Organisationer med tillgång till Adobe Express kan använda integrerade bildredigerings- och redigeringsverktyg från Adobe Express och Adobe Firefly som är tillgängliga direkt i resursvyn för att förbättra återanvändningen av innehåll och snabba upp innehållets hastighet. Du kan också använda fördefinierade element för att få dina resurser att se fantastiska ut eller utföra snabba åtgärder för att redigera bilden med bara några klick.

Redigera bilder med [!DNL Adobe Express] följer du stegen nedan:

1. Välj en bild från [!DNL Experience Manager] Resurskatalog.
1. Klicka på **[!UICONTROL Open in Adobe Express]**.

   ![Adobe Expressens inbäddade redigerare](assets/embedded-editor.png)

   Du kan utnyttja funktionerna i [!DNL Adobe Express] för att utföra alla bildredigeringsrelaterade åtgärder, som [ändra storlek på bild](https://helpx.adobe.com/in/express/using/resize-image.html), [ta bort eller ändra bakgrundsfärg](https://helpx.adobe.com/in/express/using/remove-background.html), [beskära bild](https://helpx.adobe.com/in/express/using/crop-image.html)och mycket annat.

1. När du är klar med bildredigeringen kan du hämta en resurs som en ny resurs eller spara resursen som en ny version.

## Skapa nya resurser med Adobe Express {#create-new-embedded-editor}

[!DNL Assets view] gör att du kan skapa en ny mall från grunden med [!DNL Adobe Express] inbäddad redigerare Skapa en ny resurs med [!DNL Adobe Express]utför du följande steg:

1. Navigera till **[!UICONTROL My Workspace]** och klicka **[!UICONTROL Create]** i Adobe Expressens banderoll som visas högst upp. [!DNL Adobe Express] tom arbetsyta visas i [!DNL Assets view] användargränssnitt.
1. Skapa innehåll med [Mallar](https://helpx.adobe.com/in/express/using/work-with-templates.html). I annat fall går du till **[!UICONTROL Your Stuff]** för att ändra befintligt innehåll.
1. När du är klar klickar du **[!UICONTROL Save as new asset]**.
1. Ange målsökväg för den skapade resursen och klicka på **[!UICONTROL Save]**.

>[!NOTE]
>
>* Du kan bara ändra bilder på `JPEG` och `PNG` formattyper.
>* Resursens storlek måste vara mindre än 17 MB.
>* Du kan spara en bild i `PDF`, `JPEG`, eller `PNG` format. Om det finns flera sidor kan du spara dem som `PDF`.

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

* Ge produktfeedback med [!UICONTROL Feedback] alternativ som finns i användargränssnittet i resursvyn

* Ge feedback på dokumentationen med [!UICONTROL Edit this page] ![redigera sidan](assets/do-not-localize/edit-page.png) eller [!UICONTROL Log an issue] ![skapa ett GitHub-problem](assets/do-not-localize/github-issue.png) som finns till höger

* Kontakt [Kundtjänst](https://experienceleague.adobe.com/?support-solution=General#support)

>[!MORELIKETHIS]
>
>* [Snabbåtgärder i Adobe Expressen](https://helpx.adobe.com/in/express/using/resize-image.html)
>* [Visa versionshistorik för en resurs](navigate-assets-view.md)

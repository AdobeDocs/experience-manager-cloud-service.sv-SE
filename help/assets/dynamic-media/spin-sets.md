---
title: Snurrande uppsättningar
description: Lär dig hur du arbetar med snurruppsättningar i Dynamic Media
translation-type: tm+mt
source-git-commit: df0374c58150780c373780051aeb7dda0c111e45
workflow-type: tm+mt
source-wordcount: '1740'
ht-degree: 13%

---


# Snurrande uppsättningar{#spin-sets}

Med en snurra uppsättning kan du simulera hur det ser ut när du vrider ett objekt för att undersöka det. Med snurra uppsättningar kan du visa objekt från vilken vinkel som helst och få fram de viktigaste visuella detaljerna från vilken vinkel som helst.

Med en snurra uppsättning simuleras en 360-graders visningsupplevelse. Dynamic Media har en enda axelsnurra där tittarna kan rotera ett objekt. Dessutom kan man zooma och panorera med några enkla musklick. På så sätt kan användare undersöka ett objekt närmare från en viss betraktningsvinkel.

Spin Sets are designated by a banner with the word **[!UICONTROL SPINSET]**. In addition, if the Spin Set is published, then the publish date, indicated by the **[!UICONTROL World]** icon is on the banner along with the last modification date, indicated by the **[!UICONTROL Pencil]** icon displays.

![chlimage_1-](assets/chlimage_1-380.png)

>[!NOTE]
>
>Mer information om användargränssnittet Resurser finns i [Hantera resurser med Touch-gränssnittet](/help/assets/manage-digital-assets.md).

## Snabbstart: Snurra uppsättningar {#quick-start-spin-sets}

Så här kommer du igång snabbt med Spin Sets:

1. [Ladda upp bilderna för flera vyer.](#uploading-assets-for-spin-sets)

   Du behöver minst 8-12 tagningar av ett objekt för en endimensionell snurra och 16-24 för en tvådimensionell snurra uppsättning. Fotografierna måste tas med jämna mellanrum för att ge intryck av att objektet roteras och vändas. Om en endimensionell snurra t.ex. innehåller 12 tagningar roterar du objektet 30 grader (360/12) för varje tagning.

1. [Skapa snurruppsättningar.](#creating-spin-sets)

   Om du vill skapa en snurruppsättning markerar du **[!UICONTROL Create > Spin Set]** och namnger uppsättningen, väljer resurser och väljer den ordning bilderna ska visas.

   See [Working with Selectors](/help/assets/dynamic-media/working-with-selectors.md).

   >[!NOTE]
   >
   >Du kan också skapa rotationsuppsättningar automatiskt med hjälp av [förinställningar för gruppuppsättningar](/help/assets/dynamic-media/config-dm.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets). **Viktigt!** Gruppuppsättningar skapas av IPS (Image Production System) som en del av resurshämtningen.

1. Ställ in [förinställningar](/help/assets/dynamic-media/managing-viewer-presets.md)för Snurra Ställ in visningsprogram efter behov.

   Administratörer kan skapa eller ändra visningsförinställningar för rotationsuppsättningar. Om du vill visa rotationsuppsättningen med en visningsförinställning markerar du rotationsuppsättningen och väljer **Visningsprogram** i listrutan till vänster.

   Se **[!UICONTROL Tools > Assets > Viewer Presets]** för att skapa eller redigera visningsförinställningar.

   Se [Lägga till och redigera visningsförinställningar.](/help/assets/dynamic-media/managing-viewer-presets.md)

   Du kan visa och komma åt uppsättningar som skapats med förinställningar för gruppuppsättningar på tre olika sätt. (Uppsättningar som skapats med gruppuppsättningsförinställningar visas *inte* i användargränssnittet.)

1. [Förhandsgranska snurra uppsättningar.](/help/assets/dynamic-media/previewing-assets.md)

   Markera rotationsuppsättningen så kan du förhandsgranska den. Rotera snurrsuppsättningen. Du kan välja olika visningsprogram på **[!UICONTROL Viewers]** menyn, som finns i den vänstra listrutan.

1. [Publicera snurruppsättningar.](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)

   När du publicerar en snurruppsättning aktiveras URL-adressen och strängen Embed. Dessutom måste du [publicera visningsförinställningen](/help/assets/dynamic-media/managing-viewer-presets.md).

1. [Länka URL:er till webbprogrammet](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md) eller [bädda in video- eller bildvisningsprogrammet](/help/assets/dynamic-media/embed-code.md).

   AEM Assets skapar URL-anrop för Spin-uppsättningar och aktiverar dem när du har publicerat rotationsuppsättningarna. Du kan kopiera dessa URL:er när du förhandsgranskar resurser. Du kan även bädda in dem på din webbplats.

   Markera rotationsuppsättningen och välj sedan **[!UICONTROL Viewers]** i listrutan till vänster.

   Läs [Länka en rotationsuppsättning till en webbsida](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md) och [Bädda in video- eller bildvisningsprogrammet](/help/assets/dynamic-media/embed-code.md).

Om du behöver kan du [redigera snurra uppsättningar](#editing-spin-sets). Dessutom kan du visa och ändra egenskaperna [för](/help/assets/manage-digital-assets.md#editing-properties)rotationsuppsättningen.

## Överför resurser för snurpuppsättningar {#uploading-assets-for-spin-sets}

Du behöver minst 8-12 tagningar av ett objekt för en endimensionell snurra och 16-24 för en tvådimensionell snurra uppsättning. Fotografierna måste tas med jämna mellanrum för att ge intryck av att objektet roteras och vändas. Om en endimensionell snurra t.ex. innehåller 12 tagningar roterar du objektet 30 grader (360/12) för varje tagning.

Du kan överföra bilder för snurra uppsättningar på samma sätt som du [överför andra resurser i AEM Assets](/help/assets/manage-digital-assets.md).

### Riktlinjer för hämtning av bilder för din snurruppsättning {#guidelines-for-shooting-spin-set-images}

Nedan följer några tips om hur du använder snurra uppsättningsbilder. Ju fler bilder du har i en snurrfunktion, desto bättre blir effekten av att snurra. Om du inkluderar många bilder i uppsättningen ökar dock tiden det tar för bilderna att läsas in. AEM rekommenderar följande riktlinjer för att ta bilder för användning i snurra uppsättningar:

* Använd minst 8-12 bilder i en endimensionell snurra och 16-24 bilder i en tvådimensionell snurra. Minst 8 bilder krävs för att kunna vridas 360 grader. Endimensionella snurruppsättningar är vanligare eftersom tvådimensionella snurvuppsättningar är arbetsintensiva.
* Använd ett förlustfritt format, TIFF och PNG rekommenderas.
* Maskera alla bilder så att objektet visas på en helt vit eller annan bakgrund med hög kontrast. Du kan också lägga till skuggor.
* Se till att produktinformationen är väl belyst och i fokus.
* Ta snurra bilder till modekläder med mannequin eller modell. Ofta är mannequin antingen helt maskerat (med hjälp av en glasmannequin) eller en stiliserad mannequin/form visas i bilden. Du kan skapa en omformningsrotation genom att definiera antalet vinklar. Markera varje vinkel med band på golvet för att vägleda modellen till steg och titta i riktningen för varje tagning.

## Skapa snurruppsättningar {#creating-spin-sets}

I det här avsnittet beskrivs hur du skapar snurruppsättningar.

>[!NOTE]
>
>Du kan också skapa rotationsuppsättningar automatiskt med hjälp av [förinställningar för gruppuppsättningar](/help/assets/dynamic-media/config-dm.md). **Viktigt!** Gruppuppsättningar skapas av IPS (Image Production System) som en del av resurshämtningen.
>
>Se&quot;Skapa gruppuppsättningsförinställningar för automatisk generering av bilduppsättningar och snurruppsättningar&quot; i [Konfigurera dynamiska media](/help/assets/dynamic-media/config-dm.md).

>[!NOTE]
>
>Den ordning i vilken bilderna visas i en snurrfunktion. Se till att ordna dem så att snurret blir en jämn 360-gradersvy.

**Skapa snurruppsättningar**

1. I Assets navigerar du till den plats där du vill skapa en rotationsuppsättning, klickar sedan på **[!UICONTROL Create]** och väljer **[!UICONTROL Spin Set]**. Du kan också skapa uppsättningen inifrån en mapp som innehåller resurserna. Redigeraren för rotationsuppsättningar visas.

   ![6_5_spinset-createpulldownmenu](assets/6_5_spinset-createpulldownmenu.png)

1. Ange ett namn för rotationsuppsättningen i **[!UICONTROL Title]** fältet i rotationsredigeraren. Namnet visas i banderollen över snurruppsättningen. Du kan också ange en beskrivning.

   ![6_5_spinset-spinseteditortitle](assets/6_5_spinset-spinseteditortitle.png)

   >[!NOTE]
   >
   >När du skapar rotationsuppsättningen kan du ändra miniatyrbilden för rotationsuppsättningen eller låta AEM välja miniatyrbilden automatiskt baserat på resurserna i rotationsuppsättningen. Om du vill välja en miniatyrbild klickar du på **[!UICONTROL Change thumbnail]** och väljer en bild (du kan navigera till andra mappar för att hitta bilder också). If you have selected a thumbnail and then decide that you want AEM to generate one from the spin set, select **[!UICONTROL Switch to Automatic thumbnail]**.

1. Gör något av följande:

   * Tryck på i det övre vänstra hörnet på sidan för redigeraren för uppsättningar **[!UICONTROL Add Asset]**.

   * I mitten av sidan för redigeraren för snurra uppsättning trycker du på **[!UICONTROL Tap to open Asset Selector]**.
   Tryck för att välja resurser som du vill inkludera i din snurruppsättning. De markerade resurserna visas med en bock. When you are finished, near the upper-right corner of the page, tap **[!UICONTROL Select]**.

   Med resursväljaren kan du söka efter resurser genom att skriva ett nyckelord och trycka på **[!UICONTROL Return]**. Du kan också använda filter för att förfina sökresultatet. Du kan filtrera efter sökväg, samling, filtyp och tagg. Markera filtret och tryck sedan på ikonen **[!UICONTROL Filter]** i verktygsfältet. Ändra vyn genom att trycka på ikonen Visa och sedan välja **[!UICONTROL Column View]**, **[!UICONTROL Card View]** eller **[!UICONTROL List View]**.

   See [Working with Selectors](/help/assets/dynamic-media/working-with-selectors.md).

   ![chlimage_1-383](assets/chlimage_1-383.png)

1. När du lägger till resurser i uppsättningen läggs de automatiskt till i alfanumerisk ordning. Du kan sortera om eller sortera resurser manuellt när du har lagt till dem.

   Om det behövs kan du dra en resurs sorteringsikon till höger om resursens filnamn för att ordna om bilderna uppåt eller nedåt i uppsättningslistan.

   ![Ändra ordning på bildruta 11 i rotationsrutan genom att dra den till en ny plats.](assets/6_5_spinset-reorderassets.png)

   Ändra ordning på bildruta 11 i rotationsrutan genom att dra den till en ny plats.

1. (Valfritt) Gör något av följande:

   * Om du vill ta bort en bild markerar du bilden och trycker på **[!UICONTROL Delete Asset]**.

   * To apply a preset, near the upper-right corner of the page, tap **[!UICONTROL Preset]**, then select a preset to apply to all the assets at once.

1. Klicka på **[!UICONTROL Save]**. Den nyligen skapade rotationsuppsättningen visas i den mapp du skapade den i.

## Visa snurruppsättningar {#viewing-spin-sets}

Du kan skapa snurruppsättningar antingen i användargränssnittet eller automatiskt med hjälp av [gruppuppsättningsförinställningar](/help/assets/dynamic-media/config-dm.md). Uppsättningar som skapats med gruppuppsättningsförinställningar visas *inte* i användargränssnittet. Du kan få åtkomst till uppsättningar som skapats med gruppuppsättningsförinställningar på tre olika sätt. (Dessa metoder är tillgängliga även om du har skapat rotationsuppsättningarna i användargränssnittet).

>[!NOTE]
>
>Du kan också visa uppsättningar via användargränssnittet enligt beskrivningen i [Redigera snurruppsättningar](#editing-spin-sets).

**Så här visar du snurruppsättningar**

1. När egenskaperna för en enskild resurs öppnas. Egenskaper anger vad som ställer in den valda resursen som medlem av (under **[!UICONTROL Member of Sets]**). Klicka på uppsättningens namn för att se hela uppsättningen.

   ![chlimage_1-156](assets/chlimage_1-384.png)

1. Från en medlemsbild i en uppsättning. Select the **[!UICONTROL Sets]** menu to display the sets that the asset is a member of.

   ![chlimage_1-157](assets/chlimage_1-385.png)

1. I sökningen kan du välja **[!UICONTROL Filters]** och sedan expandera **[!UICONTROL Dynamic Media]** och markera **[!UICONTROL Sets]**.

   Sökningen returnerar matchande uppsättningar som skapats manuellt i användargränssnittet eller automatiskt skapats med gruppuppsättningsförinställningar. För automatiska uppsättningar utförs sökfrågan med hjälp av `Starts with` sökvillkor som skiljer sig från AEM som baseras på `Contains` sökvillkor. Det enda sättet att söka efter automatiska uppsättningar är att ställa in filtret på **[!UICONTROL Sets]** .

   ![chlimage_1-158](assets/chlimage_1-386.png)

## Redigera snurruppsättningar {#editing-spin-sets}

Du kan utföra en mängd redigeringsåtgärder på snurra uppsättningar, till exempel:

* Lägg till bilder i rotationsrutan.
* Ändra ordning på bilderna i rotationsrutan.
* Ta bort resurser i rotationsuppsättningen.
* Använd förinställningar för visningsprogram.
* Ta bort rotationsrutan.

**Redigera en snurruppsättning**

1. Gör något av följande:

   * Håll pekaren över en resurs i en snurruppsättning och tryck sedan på **[!UICONTROL Edit]** (pennikon).
   * Håll muspekaren över en resurs i en snurruppsättning, tryck **[!UICONTROL Select]** (bockmarkeringsikon) och tryck sedan **[!UICONTROL Edit]** på verktygsfältet.

   * Tryck på en snurra uppsättningsresurs och tryck sedan på **[!UICONTROL Edit]** (pennikon) i verktygsfältet.

1. Gör något av följande om du vill redigera rotationsuppsättningen:

   * Om du vill ändra ordning på bilderna drar du en bild till en ny plats (markera ikonen för att ändra ordning för att flytta objekt).
   * Om du vill sortera objekt i stigande eller fallande ordning klickar du på kolumnrubriken.
   * Om du vill lägga till en resurs eller uppdatera en befintlig resurs klickar du på **[!UICONTROL Add Asset]**. Navigera till en resurs, markera den och tryck sedan **[!UICONTROL Select]** i det övre högra hörnet.
Om du tar bort den bild som AEM använder som miniatyrbild genom att ersätta den med en annan bild, visas fortfarande originalresursen.
   * Om du vill ta bort en resurs markerar du den och klickar eller trycker **[!UICONTROL Delete Asset]**.
   * Om du vill använda en förinställning trycker eller klickar du på förinställningsikonen och väljer en förinställning.
   * Om du vill ta bort en hel snurruppsättning går du till snurra-uppsättningen, markerar den och markerar den **[!UICONTROL Delete]**

   >[!NOTE]
   >
   >You can edit the images in a Spin Set by navigating to the set, tap **[!UICONTROL Set Members]** in the left rail, and then tap the Pencil icon on an individual asset to open the editing window.

1. Klicka **[!UICONTROL Save]** när du är klar med redigeringen.

## Förhandsgranska snurra uppsättningar {#previewing-spin-sets}

Se [Förhandsgranska resurser](/help/assets/dynamic-media/previewing-assets.md).

## Publicera snurruppsättningar {#publishing-spin-sets}

Se [Publicera resurser](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).
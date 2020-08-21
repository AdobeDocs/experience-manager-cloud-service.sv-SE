---
title: Blandade medieuppsättningar
description: Lär dig hur du arbetar med blandade medieuppsättningar i Dynamic Media
translation-type: tm+mt
source-git-commit: c240f9aa465b019fa77cc471f865db1f4ab45532
workflow-type: tm+mt
source-wordcount: '1395'
ht-degree: 28%

---


# Blandade medieuppsättningar{#mixed-media-sets}

Med blandade medieuppsättningar kan du kombinera bilder, bilduppsättningar, snurruppsättningar och videoklipp i en presentation.

Blandade medieuppsättningar definieras av en banderoll med ordet **[!UICONTROL MixedMediaSet]**. Om uppsättningen med blandade medier publiceras visas dessutom det publiceringsdatum som anges av ikonen **[!UICONTROL World]** på banderollen tillsammans med det senaste ändringsdatumet, som anges av ikonen **[!UICONTROL Pencil]**.

![chlimage_1-137](assets/chlimage_1-348.png)

>[!NOTE]
>
>Mer information om användargränssnittet Resurser finns i [Hantera resurser med Touch-gränssnittet](/help/assets/manage-digital-assets.md).

## Snabbstart: Blandade medieuppsättningar {#quick-start-mixed-media-sets}

Följ de här stegen för att komma igång snabbt med blandade medieuppsättningar:

1. [Överför dina resurser](#uploading-assets).

   Börja med att ladda upp bilder och videoklipp för uppsättningarna med blandade medier. Om det behövs kan du skapa [bilduppsättningar](/help/assets/dynamic-media/image-sets.md) och [rotationsuppsättningar](/help/assets/dynamic-media/spin-sets.md). Eftersom användare kan zooma in bilder i visningsprogrammet för uppsättningen med blandade medier bör du ta hänsyn till zoomningen när du väljer bilder. Se till att bilderna har minst 2 000 pixlar i den största dimensionen.

1. [Skapa blandade medieuppsättningar.](#creating-mixed-media-sets)

   Om du vill skapa en uppsättning med blandade medier trycker du på **[!UICONTROL Create > Mixed Media Set]** på resurssidan och ger sedan uppsättningen ett namn, väljer resurser och väljer i vilken ordning bilderna ska visas.

   See [Working with Selectors.](/help/assets/dynamic-media/working-with-selectors.md)

1. Ställ in förinställningar [för](/help/assets/dynamic-media/managing-viewer-presets.md)blandad Media Viewer efter behov.

   Administratörer kan skapa eller ändra visningsförinställningar för blandade medieuppsättningar. Om du vill visa de blandade medierna med en visningsförinställning väljer du uppsättningen med blandade medier och väljer sedan **[!UICONTROL Viewers]** i listrutan till vänster.

   Se **[!UICONTROL Tools > Assets > Viewer Presets]** för att skapa eller redigera visningsförinställningar.

   Se [Lägga till och redigera visningsförinställningar.](/help/assets/dynamic-media/managing-viewer-presets.md)

1. [Förhandsgranska blandade medieuppsättningar.](#previewing-mixed-media-sets)

   Markera den blandade medieuppsättningen och du kan förhandsgranska den. Klicka på miniatyrbildikonerna för att undersöka den blandade medieuppsättningen i det valda visningsprogrammet. Du kan välja olika visningsprogram på **[!UICONTROL Viewers]** menyn, som finns i den vänstra listrutan.

1. [Publicera blandade medieuppsättningar.](#publishing-mixed-media-sets)

   När du publicerar en blandad medieuppsättning aktiveras URL-adressen och strängen Embed. Dessutom måste du [publicera visningsförinställningen](/help/assets/dynamic-media/managing-viewer-presets.md#publishing-viewer-presets).

1. [Länka URL:er till webbprogrammet](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md) eller [bädda in video- eller bildvisningsprogrammet](/help/assets/dynamic-media/embed-code.md).

   AEM Assets skapar URL-anrop för blandade medieuppsättningar och aktiverar dem när du har publicerat de blandade medieuppsättningarna. Du kan kopiera dessa URL:er när du förhandsgranskar resurser. Du kan även bädda in dem på din webbplats.

   Select the Mixed Media Set, then in the left rail drop-down menu, select **[!UICONTROL Viewers]**.

   Se [Länka en uppsättning med blandade medier till en webbsida](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md) och [Bädda in video- eller bildvisningsprogrammet](/help/assets/dynamic-media/embed-code.md).

Om du behöver kan du redigera [blandade medieuppsättningar](#editing-mixed-media-sets). Dessutom kan du visa och ändra egenskaperna [för](/help/assets/manage-digital-assets.md#editing-properties)den blandade medieuppsättningen.

>[!NOTE]
>
>Om du har problem med att skapa uppsättningar kan du läsa [Felsöka dynamiska media](/help/assets/dynamic-media/troubleshoot-dm.md).

## Överför resurser {#uploading-assets}

Börja med att ladda upp bilder och videoklipp för uppsättningarna med blandade medier. Eftersom användare kan zooma in bilder i visningsprogrammet för den blandade medieuppsättningen måste du ta hänsyn till zoomningen när du väljer bilder. Se till att bilderna har minst 2 000 pixlar i den största dimensionen.

Om du dessutom vill lägga till snurrsuppsättningar eller bilduppsättningar i den blandade medieuppsättningen skapar du även dem.

## Skapa blandade medieuppsättningar {#creating-mixed-media-sets}

Du kan lägga till bilder, bilduppsättningar, snurruppsättningar och videoklipp i din uppsättning med blandade media. Se till att dina filer, bilduppsättningar och snurruppsättningar är klara att publiceras innan du lägger till dem i den blandade medieuppsättningen.

När du lägger till resurser i uppsättningen läggs de automatiskt till i alfanumerisk ordning. Du kan ändra ordning på eller sortera resurser manuellt när de har lagts till.

**Skapa en blandad medieuppsättning**

1. Navigera till den plats där du vill skapa en blandad medieuppsättning i Assets, klicka på **[!UICONTROL Create]** och välj **[!UICONTROL Mixed Media Set]**. Du kan också skapa uppsättningen inifrån en mapp som innehåller resurserna. Redigeraren för uppsättningar med blandade medier visas.

   ![chlimage_1-138](assets/chlimage_1-349.png)

1. I redigeraren för den blandade medieuppsättningen **[!UICONTROL Title]** anger du ett namn för den blandade medieuppsättningen. Namnet visas i banderollen över den blandade medieuppsättningen. Du kan också ange en beskrivning.

   ![chlimage_1-139](assets/chlimage_1-350.png)

   >[!NOTE]
   >
   >När du skapar den blandade medieuppsättningen kan du ändra miniatyrbilden för den blandade medieuppsättningen eller låta AEM välja miniatyrbilden automatiskt baserat på resurserna i den blandade medieuppsättningen. Om du vill välja en miniatyrbild klickar du på **[!UICONTROL Change thumbnail]** och väljer en bild (du kan navigera till andra mappar för att hitta bilder också). If you have selected a thumbnail and then decide that you want AEM to generate one from the mixed media set, select **[!UICONTROL Switch to Automatic thumbnail]**.

1. Tryck på resursväljaren för att välja resurser som du vill inkludera i den blandade medieuppsättningen. Select them and click **[!UICONTROL Select]**.

   Med resursväljaren kan du söka efter resurser genom att skriva ett nyckelord och trycka på **[!UICONTROL Return]**. Du kan också använda filter för att förfina sökresultatet. Du kan filtrera efter sökväg, samling, filtyp och tagg. Markera filtret och tryck sedan på ikonen **[!UICONTROL Filter]** i verktygsfältet. Ändra vyn genom att markera ikonen **[!UICONTROL View]** och markera **[!UICONTROL List View]**, **[!UICONTROL Column View]** eller **[!UICONTROL Card View]**.

   See [Working with Selectors](/help/assets/dynamic-media/working-with-selectors.md).

   ![chlimage_1-140](assets/chlimage_1-351.png)

1. Ändra ordning på resurserna genom att dra dem uppåt eller nedåt i listan (du måste markera **[!UICONTROL Reorder]** ikonen) efter behov.

   ![chlimage_1-141](assets/chlimage_1-352.png)

   Om du vill lägga till miniatyrbilder klickar du på ikonen **+** **[!UICONTROL thumbnail]** bredvid bilden och går till den miniatyrbild du vill använda. När du har markerat alla miniatyrbilderna klickar du på **[!UICONTROL Save]**.

   >[!NOTE]
   >
   >Tryck på **[!UICONTROL Add Asset]** om du vill lägga till resurser.

1. Om du vill ta bort en resurs markerar du motsvarande kryssruta och trycker på **[!UICONTROL Delete Asset]**.
1. Om du vill använda en förinställning trycker du **[!UICONTROL Preset]** i det övre högra hörnet och väljer en förinställning som ska användas på resurserna.
1. Klicka på **[!UICONTROL Save]**. Den nya blandade medieuppsättningen visas i den mapp du skapade den i.

## Redigera blandade medieuppsättningar {#editing-mixed-media-sets}

Du kan utföra en mängd redigeringsåtgärder för resurser i blandade medieuppsättningar direkt i användargränssnittet, [precis som för andra resurser i Resurser](/help/assets/manage-digital-assets.md). Du kan även utföra följande åtgärder i Blandade medieuppsättningar:

* Lägg till resurser i den blandade medieuppsättningen.
* Ändra ordning på resurser i den blandade medieuppsättningen.
* Ta bort resurser i den blandade medieuppsättningen.
* Använd förinställningar för visningsprogram.
* Ändra standardminiatyrbilden.

**Redigera en blandad medieuppsättning**

1. Gör något av följande:

   * Håll pekaren över en resurs i en blandad medieuppsättning och tryck sedan på **[!UICONTROL Edit]** (pennikon).
   * Håll pekaren över en resurs i en blandad medieuppsättning, tryck **[!UICONTROL Select]** (bockmarkeringsikon) och tryck sedan **[!UICONTROL Edit]** på verktygsfältet.

   * Tryck på en resurs i en blandad medieuppsättning och tryck sedan på **[!UICONTROL Edit]** (pennikon) i verktygsfältet.

1. Gör något av följande i redigeraren för den blandade medieuppsättningen:

   * Om du vill ändra ordning på resurser trycker du på **[!UICONTROL Assets]** (bildikon) och drar en resurs till en ny plats.
   * Om du vill lägga till resurser trycker du på **[!UICONTROL Add Asset]**. Navigera till resurserna. För varje resurs som du vill lägga till håller du pekaren över resursens bild (inte resursens namn) och trycker sedan på bockmarkeringsikonen. Tryck på i det övre högra hörnet **[!UICONTROL Select]**.

   * Om du vill ta bort en resurs trycker du på **[!UICONTROL Assets]** (bildikon) i den vänstra panelen och väljer sedan resursen. Tryck på i verktygsfältet **[!UICONTROL Delete Asset]**.

   * Om du vill sortera resurser efter namn i stigande eller fallande ordning trycker du på **[!UICONTROL Assets]** (bildikon) i den vänstra panelen. Till höger om **[!UICONTROL Assets]** rubriken: tryck på upp- eller nedknappsikonerna.

      >[!NOTE]
      >
      >* To delete an entire Mixed Media Set, from any viewing mode (such as **[!UICONTROL Card View]** or **[!UICONTROL Column View]**) navigate to the Mixed Media Set. Håll pekaren över resursen och tryck på bocken för att markera den. Tryck **[!UICONTROL Backspace]** på tangentbordet eller klicka på **[!UICONTROL More]** (tre punkter) i verktygsfältet och tryck sedan på **[!UICONTROL Delete]**.
         >
         >
      * You can edit the assets in a Mixed Media Set by navigating to the set, clicking **[Set Members]** in the left rail, and then tapping the **[!UICONTROL Pencil]** icon on an individual asset to open the editing window.


1. Tryck **[!UICONTROL Save]** när du är klar med redigeringen.

   >[!NOTE]
   >
   >* Om du vill redigera resurserna i en uppsättning med blandade medier navigerar du till den blandade medieuppsättningen. Tryck på (markera inte) uppsättningen för att öppna den på AEM-sidan för förhandsgranskning. In the left rail, click the down caret to open the drop-down list, then tap **[!UICONTROL Set Members]**. In the Set Members page, hover on an asset, then tap **[!UICONTROL Edit]** (pencil icon) to open the editing page.
      >
      >
   * Om du vill ta bort en hel uppsättning med blandade medier – I valfritt visningsläge (som kortvyn eller kolumnvyn) går du till uppsättningen med blandade medier. Hover on the set, then tap **[Select]** (checkmark icon). Tryck **[!UICONTROL Backspace]** på tangentbordet eller tryck **[!UICONTROL More]** (rad om tre punkter) och tryck sedan på **[!UICONTROL Delete]**.


## Förhandsgranska blandade medieuppsättningar {#previewing-mixed-media-sets}

Mer information om hur du förhandsgranskar blandade medieuppsättningar finns i [Förhandsgranska resurser](/help/assets/dynamic-media/previewing-assets.md) .

## Publicera blandade medieuppsättningar {#publishing-mixed-media-sets}

Mer information om hur du publicerar blandade medieuppsättningar finns i [Publicera resurser](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md) .

>[!NOTE]
>
>Om den blandade medieuppsättningen inte hamnar helt i leveranstjänsten första gången du publicerar den kanske du måste publicera den blandade medieuppsättningen en andra gång.


---
title: Hantera digitala resurser
description: Läs om olika metoder för resurshantering och redigering
contentOwner: AG
mini-toc-levels: 1
feature: Asset Management,Publishing,Collaboration,Asset Processing
role: User,Architect,Admin
exl-id: 51a26764-ac2b-4225-8d27-42a7fd906183
source-git-commit: 764ddc2621d8da3323af4eb037ec5b92e1214503
workflow-type: tm+mt
source-wordcount: '4137'
ht-degree: 10%

---

# Hantera resurser {#manage-assets}

I den här artikeln beskrivs hur du hanterar och redigerar resurser i [!DNL Adobe Experience Manager Assets]. Att hantera [!DNL Content Fragments], se [[!DNL Content Fragments]](content-fragments/content-fragments.md) resurser.

## Skapa mappar {#creating-folders}

När du organiserar en samling resurser, till exempel, alla `Nature` kan du skapa mappar som håller ihop dem. Du kan använda mappar för att kategorisera och ordna dina resurser. [!DNL Experience Manager Assets] kräver inte att du ordnar resurser i mappar för att fungera bättre.

>[!NOTE]
>
>* Sharing an Assets folder of the type `sling:OrderedFolder`, is not supported when sharing to Marketing Cloud. If you want to share a folder, do not select [!UICONTROL Ordered] when creating a folder.
>* Experience Manager does not allow using `subassets` word as the name of a folder. It is a keyword reserved for node that contain subassets for compound assets


1. Navigate to the place in your digital assets folder where you want to create a new folder. Klicka på **[!UICONTROL Create]**. Välj **[!UICONTROL New Folder]**.
1. I **[!UICONTROL Title]** anger du ett mappnamn. Som standard använder DAM den titel som du angav som mappnamn. Once the folder is created, you can override the default and specify another folder name.
1. Klicka på **[!UICONTROL Create]**. Your folder is displayed in the digital assets folder.

The following (space-separated list of) characters are not supported:

* Namnet på en resursfil får inte innehålla något av följande tecken: `* / : [ \\ ] | # % { } ? &`
* Namnet på en resursmapp får inte innehålla något av följande tecken: `* / : [ \\ ] | # % { } ? \" . ^ ; + & \t`

## Överför resurser {#uploading-assets}

Se [lägga till digitala resurser i Experience Manager](add-assets.md).

## Identifiera duplicerade resurser {#detect-duplicate-assets}

<!-- TBD: This feature may not work as documented. See CQ-4283718. Get PM review done. -->

Om en DAM-användare överför en eller flera resurser som redan finns i databasen, [!DNL Experience Manager] identifierar dupliceringen och meddelar användaren. Dubblettidentifiering är inaktiverat som standard eftersom det kan påverka prestanda beroende på databasens storlek och antalet överförda resurser. Aktivera funktionen genom att konfigurera [!UICONTROL Adobe AEM Cloud Asset Duplication Detector]. Se [Så här gör du OSGi-konfigurationer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html). Dubblettidentifieringen baseras på den unika `dam:sha1` värde lagrat på `jcr:content/metadata/dam:sha1`. Det innebär att duplicerade resurser identifieras även om filnamnen är olika.

Du kan lägga till konfigurationsfilen `/apps/example/config.author/com.adobe.cq.assetcompute.impl.assetprocessor.AssetDuplicationDetector.cfg.json` i egen kod och filen kan innehålla följande:

```json
{
  "enabled":true,
  "detectMetadataField":"dam:sha1"
}
```

När den är aktiverad skickar Experience Manager meddelanden om duplicerade resurser till Inkorgen Experience Manager. Det är ett aggregerat resultat för flera dubbletter. Användarna kan välja att ta bort resurserna baserat på resultatet.

![Inkorgsmeddelande för duplicerade resurser](assets/duplicate-detect-inbox-notification.png)

>[!NOTE]
>
>När du överför resurser till databasen upptäcker Experience Manager duplicering och meddelar dig om de första 100 duplicerade resurserna.

## Förhandsgranska resurser {#previewing-assets}

Följ de här stegen för att förhandsgranska en resurs.

1. Navigera från användargränssnittet Resurser till platsen för den resurs som du vill förhandsgranska.
1. Tryck på önskad resurs för att öppna den.

1. I förhandsgranskningsläget finns zoomalternativ för [bildtyper som stöds](/help/assets/file-format-support.md) (med interaktiv redigering).

   Om du vill zooma in på en resurs trycker/klickar du `+` (eller tryck/klicka på förstoringsglaset på resursen). Om du vill zooma ut trycker du/klickar `-`. När du zoomar in kan du titta närmare på alla delar av bilden genom att panorera. Med den återställda zoompilen återgår du till den ursprungliga vyn.

   Tryck **[!UICONTROL Reset]** om du vill återställa vyn till den ursprungliga storleken.

## Redigera egenskaper {#editing-properties}

1. Navigera till platsen för resursen vars metadata du vill redigera.

1. Markera resursen och tryck/klicka på **[!UICONTROL Properties]** i verktygsfältet för att visa resursegenskaper. Du kan också välja **[!UICONTROL Properties]** Snabba åtgärder på tillgångskortet.

   ![properties_quickaction](assets/properties_quickaction.png)

1. I [!UICONTROL Properties] redigerar du metadataegenskaperna på olika flikar. Till exempel, under **[!UICONTROL Basic]** kan du redigera titeln, beskrivningen och så vidare.

   >[!NOTE]
   >
   >Layouten för [!UICONTROL Properties] vilken sida och vilka metadataegenskaper som är tillgängliga beror på det underliggande metadataschemat. Så här ändrar du layouten för [!UICONTROL Properties] sida, se [Metadata-scheman](/help/assets/metadata-schemas.md).

1. Om du vill schemalägga ett visst datum/tid för att aktivera resursen använder du datumväljaren bredvid fältet **[!UICONTROL On Time]**.

   ![chlimage_1-217](assets/chlimage_1-217.png)

1. Om du vill inaktivera tillgången efter en viss tid väljer du datum/tid för inaktiveringen i datumväljaren bredvid **[!UICONTROL Off Time]** fält. Inaktiveringsdatumet ska vara senare än aktiveringsdatumet för en tillgång. Efter [!UICONTROL Off Time], är en resurs och dess återgivningar inte tillgängliga via webbgränssnittet Resurser eller via HTTP-API:t.

   ![chlimage_1-218](assets/chlimage_1-218.png)

1. I **[!UICONTROL Tags]** markerar du en eller flera taggar. Om du vill lägga till en egen tagg skriver du namnet på taggen i rutan och markerar `Enter` nyckel. Den nya taggen sparas i [!DNL Experience Manager].

   YouTube kräver att taggar ska publiceras och ha en länk till YouTube (om en lämplig länk finns).

   >[!NOTE]
   >
   >Om du vill skapa taggar måste du ha skrivbehörighet på `/content/cq:tags/default` sökväg i CRX-databasen.

1. Tryck/klicka på **[!UICONTROL Save & Close]**.

1. Navigera till användargränssnittet Resurser. De redigerade metadataegenskaperna, inklusive rubrik, beskrivning och taggar, visas på resurskortet i kortvyn och under relevanta kolumner i listvyn.

<!-- TBD: Uncomment after verification for Dec release.

## View asset usage and references {#usage-and-references}

[!DNL Experience Manager] lets you track statistics about usage of a digital asset. The usage statistics include the following:

    * Number of times the asset was viewed or downloaded
    * Channels/devices through which the asset was used
    * Creative solutions where the asset was recently used

To view usage statistics for an asset, in the [!UICONTROL Properties] page, click the **[!UICONTROL Insights]** tab. For more details, see [Assets Insights](assets-insights.md).

[!DNL Experience Manager] also lets you check all the incoming references to an asset, that is, the usage of an asset in remote [!DNL Sites] and in compound assets. Authors of webpages on [!DNL Experience Manager Sites] deployment can use an asset on a remote [!DNL Assets] deployment using the Connected Assets functionality. The [!UICONTROL References] tab in an asset's [!UICONTROL Properties] page lists the local and remote references of the asset. That is, the use of assets in compound assets in [!DNL Assets] and its use in remote [!DNL Sites] pages.

-->

## Kopiera resurser {#copying-assets}

När du kopierar en resurs eller en mapp kopieras hela resursen eller mappen tillsammans med dess innehållsstruktur. En kopierad resurs eller en mapp dupliceras på målplatsen. Resursen på källplatsen ändras inte.

Några attribut som är unika för en viss kopia av en tillgång överförs inte. Några exempel är:

* Tillgångs-ID, datum och tid när de skapades samt versioner och versionshistorik. Vissa av dessa egenskaper indikeras av egenskaperna `jcr:uuid`, `jcr:created`och `cq:name`.

* Skapandetid och refererade sökvägar är unika för varje resurs och för varje återgivning.

Övriga egenskaper och metadatainformation behålls. Ingen del av kopian skapas när en resurs kopieras.

1. Välj en eller flera resurser i resursgränssnittet och tryck/klicka sedan på **[!UICONTROL Copy]** -ikonen i verktygsfältet. Du kan även välja **[!UICONTROL Copy]** ![copy_icon](assets/copy_icon.png) snabbåtgärd från tillgångskortet.

   >[!NOTE]
   >
   >If you use the [!UICONTROL Copy] quick action, you can only copy one asset at a time.

1. Navigera till den plats där du vill kopiera resurserna.

   >[!NOTE]
   >
   >Om du kopierar en resurs på samma plats, [!DNL Experience Manager] genererar automatiskt en variant av namnet. Om du till exempel kopierar en resurs med namnet `Square`, [!DNL Experience Manager] genererar automatiskt titeln för kopian som `Square1`.

1. Klicka på **[!UICONTROL Paste]** resursikon i verktygsfältet. Resurser kopieras till den här platsen.

   ![chlimage_1-219](assets/chlimage_1-219.png)

   >[!NOTE]
   >
   >The **[!UICONTROL Paste]** icon is available in the toolbar until the paste operation is completed.

### Move or rename assets {#moving-or-renaming-assets}

1. Navigate to the location of the asset you want to move.

1. Markera resursen och tryck/klicka på **[!UICONTROL Move]** icon ![move_icon](assets/move_icon.png) i verktygsfältet.

1. Gör något av följande i guiden Flytta resurser:

   * Ange namnet på resursen när den har flyttats. Tryck sedan på/klicka **[!UICONTROL Next]** för att fortsätta.

   * Tryck/klicka **[!UICONTROL Cancel]** för att stoppa processen.
   >[!NOTE]
   >
   >* Du kan ange samma namn för resursen om det inte finns någon resurs med det namnet på den nya platsen. Du bör emellertid använda ett annat namn om du flyttar resursen till en plats där det finns en resurs med samma namn. Om du använder samma namn genereras automatiskt en variant av namnet. Om resursen till exempel har namnet Fyrkant, genereras namnet Fyrkant1 för kopian.
   >* När namnet ändras tillåts inte tomt utrymme i filnamnet.


1. På **[!UICONTROL Select Destination]** gör du något av följande:

   * Navigera till resursernas nya plats och tryck/klicka sedan på **[!UICONTROL Next]** för att fortsätta.

   * Tryck/klicka **[!UICONTROL Back]** för att gå tillbaka till **[!UICONTROL Rename]** skärm.

1. Om de resurser som flyttas har några referenssidor, resurser eller samlingar, **[!UICONTROL Adjust References]** visas bredvid **[!UICONTROL Select Destination]** -fliken.

   Gör något av följande i dialogrutan **[!UICONTROL Adjust References]** skärm:

   * Ange vilka referenser som ska justeras baserat på de nya detaljerna och tryck/klicka sedan på **[!UICONTROL Move]** för att fortsätta.

   * Från **[!UICONTROL Adjust]** markerar/avmarkerar du referenser till resurserna.
   * Tryck/klicka **[!UICONTROL Back]** för att gå tillbaka till **[!UICONTROL Select Destination]** skärm.

   * Tryck/klicka **[!UICONTROL Cancel]** för att stoppa flyttåtgärden.

   Om du inte uppdaterar referenser fortsätter de att peka på resursens tidigare sökväg. Om du justerar referenserna uppdateras de till den nya resurssökvägen.

### Hantera återgivningar {#managing-renditions}

1. Du kan lägga till eller ta bort återgivningar för en resurs, förutom originalet. Navigera till platsen för resursen som du vill lägga till eller ta bort återgivningar för.

1. Tryck/klicka på resursen för att öppna sidan för resursen.

   ![chlimage_1-220](assets/chlimage_1-220.png)

1. Tryck/klicka på ikonen GlobalNav och välj **[!UICONTROL Renditions]** från listan.

   ![renditions_menu](assets/renditions_menu.png)

1. I **[!UICONTROL Renditions]** visa en lista över återgivningar som genererats för resursen.

   ![renditions_panel](assets/renditions_panel.png)

   >[!NOTE]
   >
   >Som standard [!DNL Experience Manager Assets] visar inte den ursprungliga återgivningen av resursen i förhandsgranskningsläget. Om du är administratör kan du använda övertäckningar för att konfigurera [!DNL Assets] om du vill visa de ursprungliga återgivningarna i förhandsvisningsläget.

1. Välj en återgivning om du vill visa eller ta bort återgivningen.

   **Ta bort en återgivning**

   Välj en återgivning på menyn **[!UICONTROL Renditions]** och sedan trycka/klicka på **[!UICONTROL Delete Rendition]** -ikonen i verktygsfältet. Det går inte att ta bort återgivningar gruppvis när resursbearbetningen är slutförd. För enskilda resurser kan du ta bort återgivningar manuellt från användargränssnittet. För flera resurser kan du anpassa [!DNL Experience Manager] om du vill ta bort en viss återgivning eller ta bort resurserna och överföra de borttagna resurserna igen.

   ![delete_renderingicon](assets/delete_renditionicon.png)

   **Överföra en ny återgivning**

   Navigera till sidan med resursinformation för resursen och tryck/klicka på ikonen **[!UICONTROL Add Rendition]** i verktygsfältet för att överföra en ny återgivning för resursen.

   ![chlimage_1-221](assets/chlimage_1-221.png)

   >[!NOTE]
   >
   >Om du väljer en återgivning på panelen **[!UICONTROL Renditions]** ändras sammanhanget för verktygsfältet och endast de åtgärder som är relevanta visas. Alternativ som ikonen Överför återgivning visas inte. Om du vill visa de här alternativen i verktygsfältet går du till informationssidan för resursen.

   Du kan konfigurera dimensionerna för den återgivning som du vill ska visas på informationssidan för en bild- eller videoresurs. Baserat på de dimensioner du anger visar Resurser återgivningen med de exakta eller närmaste dimensionerna.

   Om du vill konfigurera återgivningsdimensionerna för en bild på resursdetaljnivån överlagrar du noden `renditionpicker` (`libs/dam/gui/content/assets/assetpage/jcr:content/body/content/content/items/assetdetail/items/col1/items/assetview/renditionpicker`) och konfigurera värdet för breddegenskapen (width). Konfigurera egenskapen **[!UICONTROL size (Long) in KB]** i stället för bredden för att anpassa återgivningen på resursdetaljsidan utifrån bildstorleken. För storleksbaserad anpassning prioriterar egenskapen `preferOriginal` originalet om storleken på den matchade återgivningen är större än originalet.

   På samma sätt kan du anpassa anteckningssidans bild genom att lägga över `libs/dam/gui/content/assets/annotate/jcr:content/body/content/content/items/content/renditionpicker`.

   ![chlimage_1-222](assets/chlimage_1-222.png)

   Om du vill konfigurera återgivningsdimensioner för en videoresurs går du till `videopicker` nod i CRX-databasen på platsen `/libs/dam/gui/content/assets/assetpage/jcr:content/body/content/content/items/assetdetail/items/col1/items/assetview/videopicker`, lägg över noden och redigera sedan lämplig egenskap.

   >[!NOTE]
   >
   >Videoanteckningar stöds bara i webbläsare med HTML5-kompatibla videoformat. Beroende på webbläsaren stöds dessutom olika videoformat.

## Ta bort resurser {#delete-assets}

Om du vill lösa eller ta bort inkommande referenser från andra sidor uppdaterar du de relevanta referenserna innan du tar bort en resurs.

Du kan även inaktivera Tvinga borttagningsknappen med hjälp av en övertäckning, så att användare inte kan ta bort refererade resurser och lämna brutna länkar.

1. Navigera till platsen för de resurser som du vill ta bort.

1. Markera resursen och klicka på **[!UICONTROL Delete]** ![delete_icon](assets/do-not-localize/delete-icon.png) i verktygsfältet.

1. I bekräftelsedialogrutan klickar du på:

   * **[!UICONTROL Cancel]** för att stoppa åtgärden
   * **[!UICONTROL Delete]** för att bekräfta åtgärden:

      * If the asset has no references, the asset is deleted.
      * If the asset has references, an error-message informs you that **[!UICONTROL One or more assets are referenced]**. Du kan välja **[!UICONTROL Force Delete]** eller **[!UICONTROL Cancel]**.

   >[!NOTE]
   >
   >Du måste ha behörighet att ta bort en resurs för att den ska kunna tas bort. Om du bara har ändringsbehörighet kan du bara redigera metadata för resursen och lägga till anteckningar till resursen. However, you cannot delete the asset or its metadata.

   >[!NOTE]
   >
   >Om du vill lösa eller ta bort inkommande referenser från andra sidor uppdaterar du de relevanta referenserna innan du tar bort en resurs. You can disallow deletion of referenced assets as it causes broken links. Inaktivera Tvinga borttagningsknappen med hjälp av en övertäckning.

## Download assets {#download-assets}

Se [hämta resurser från [!DNL Experience Manager]](/help/assets/download-assets-from-aem.md).

## Publicera eller avpublicera resurser {#publish-assets}

1. Navigera till platsen för resursen eller resursmappen som du vill publicera eller som du vill ta bort från publiceringsmiljön (avpublicera).

1. Markera resursen eller mappen som ska publiceras eller avpubliceras och välj **[!UICONTROL Manage Publication]** ![hantera publikationsalternativ](assets/do-not-localize/globe-publication.png) i verktygsfältet. Om du snabbt vill publicera väljer du **[!UICONTROL Quick Publish]** i verktygsfältet. Om mappen som du vill publicera innehåller en tom mapp publiceras inte den tomma mappen.

1. Välj **[!UICONTROL Publish]** eller **[!UICONTROL Unpublish]** efter behov.

   ![Avpubliceringsåtgärd](assets/unpublish_action.png)
   *Bild: Alternativ för publicering och avpublicering samt schemaläggning.*

1. Välj **[!UICONTROL Now]** för att agera på resursen direkt eller välja **[!UICONTROL Later]** för att schemalägga åtgärden. Välj ett datum och en tid om du väljer **[!UICONTROL Later]** alternativ. Klicka på **[!UICONTROL Next]**.

1. Om en resurs refererar till andra resurser vid publicering visas dess referenser i guiden. Endast de referenser som inte har publicerats eller ändrats sedan den senaste publiceringen visas. Välj de referenser som du vill publicera.

1. Om en resurs refererar till andra resurser vid avpublicering väljer du de referenser som du vill avpublicera. Klicka på **[!UICONTROL Unpublish]**. Klicka på **[!UICONTROL Cancel]** för att stoppa funktionsmakrot eller klicka **[!UICONTROL Unpublish]** för att bekräfta att resurserna ska avpubliceras vid det angivna datumet.

Förstå följande begränsningar och tips för publicering eller avpublicering av resurser och mappar:

* Alternativet att [!UICONTROL Manage Publication] är bara tillgängligt för användarkonton som har replikeringsbehörigheter.
* När du avpublicerar en komplex resurs avpublicerar du bara resursen. Undvik att avpublicera referenserna eftersom andra publicerade resurser kan referera till dem.
* Tomma mappar publiceras inte.
* Om du publicerar ett material som bearbetas publiceras bara det ursprungliga innehållet. Återgivningarna saknas. Antingen väntar du på att bearbetningen ska slutföras och publicerar eller publicerar om resursen när bearbetningen är klar.

## Stängd användargrupp {#closed-user-group}

En stängd användargrupp (CUG) används för att begränsa åtkomsten till specifika resursmappar som publiceras från [!DNL Experience Manager]. Om du skapar en CUG-fil för en mapp är åtkomsten till mappen (inklusive mappresurser och undermappar) begränsad till endast tilldelade medlemmar eller grupper. För att få åtkomst till mappen måste de logga in med sina inloggningsuppgifter.

CUG är ett extra sätt att begränsa åtkomsten till dina resurser. Du kan också konfigurera en inloggningssida för mappen.

1. Välj en mapp i resursgränssnittet och visa egenskapssidan genom att trycka/klicka på egenskapsikonen i verktygsfältet.
1. Från **[!UICONTROL Permissions]** flik, lägga till medlemmar eller grupper under **[!UICONTROL Closed User Group]**.

   ![add_user](assets/add_user.png)

1. Om du vill visa en inloggningsskärm när användare öppnar mappen väljer du **[!UICONTROL Enable]** alternativ. Välj sedan sökvägen till en inloggningssida i [!DNL Experience Manager]och spara ändringarna.

   ![login_page](assets/login_page.png)

   >[!NOTE]
   >
   >Om du inte anger sökvägen till en inloggningssida [!DNL Experience Manager] visar standardinloggningssidan i publiceringsinstansen.

1. Publicera mappen och försök sedan komma åt den från publiceringsinstansen. En inloggningsskärm visas.
1. Om du är CUG-medlem anger du dina säkerhetsuppgifter. Mappen visas efter [!DNL Experience Manager] autentiserar dig.

## Söka efter resurser {#search-assets}

Att söka resurser är centralt för användningen av ett digitalt resurshanteringssystem - oavsett om det är avsett för kreativa användare, för robust hantering av resurser av företagsanvändare och marknadsförare eller för administration av DAM-administratörer.

Mer information om enkla, avancerade och anpassade sökningar för att hitta och använda de lämpligaste resurserna finns i [söka efter resurser i [!DNL Experience Manager]](/help/assets/search-assets.md).

## Snabbåtgärder {#quick-actions}

Snabbåtgärdsikoner är tillgängliga för en enskild resurs i taget. Beroende på vilken enhet du använder utför du följande åtgärder för att visa snabbåtgärdsikonerna:

* Pekskärmar: Peka och håll. På en iPad kan du till exempel trycka och hålla ned en resurs så att snabbåtgärderna visas.
* Ej pekskärmar: Hovringspekare. På en stationär enhet visas t.ex. snabbåtgärdsfältet om du håller pekaren över miniatyrbilden för resursen.

<!-- Hiding this topic via cqdoc-18707

## Edit images {#editing-images}

The editing tools in the [!DNL Experience Manager Assets] interface let you perform small editing jobs on image assets. You can crop, rotate, flip, and perform other editing jobs on images. You can also add image maps to assets.

>[!NOTE]
>
>For some components, the Full Screen mode has additional options available.

1. Do one of the following to open an asset in edit mode:

    * Select the asset and then click/tap the **[!UICONTROL Edit]** icon in the toolbar.
    * Tap/click the **[!UICONTROL Edit]** icon that appears on an asset in the Card view.
    * In the asset page, tap/click the **[!UICONTROL Edit]** icon in the toolbar.

   ![edit_icon](assets/edit_icon.png)

1. To crop the image, tap/click the **Crop** icon.

   ![chlimage_1-226](assets/chlimage_1-226.png)

1. Select the desired option from the list. The crop area appears on the image based on the option you choose. The **Free Hand** option lets you crop the image without any aspect ratio restrictions.

   ![chlimage_1-227](assets/chlimage_1-227.png)

1. Select the area to be cropped, and resize or reposition it on the image.
1. Use the **Finish** icon (top right corner) to crop the image. Clicking the **Finish** icon also triggers the regeneration of renditions.

   ![chlimage_1-228](assets/chlimage_1-228.png)

1. Use the **Undo** and **Redo** icons on the top right to revert to the uncropped image or retain the cropped image, respectively.

   ![chlimage_1-229](assets/chlimage_1-229.png)

1. Tap/click the appropriate Rotate icon to rotate the image clockwise or anti-clockwise.

   ![chlimage_1-230](assets/chlimage_1-230.png)

1. Tap/click the appropriate Flip icon to flip the image horizontally or vertically.

   ![chlimage_1-231](assets/chlimage_1-231.png)

1. Tap/click the **Finish** icon to save the changes.

   ![chlimage_1-232](assets/chlimage_1-232.png)

>[!NOTE]
>
>Image editing is supported for BMP, GIF, PNG, and JPEG files formats.

>[!NOTE]
>
>To edit a TXT file, set **Day CQ Link Externalizer** from Configuration Manager.
-->

## Tidslinje {#timeline}

På tidslinjen kan du visa olika händelser för ett markerat objekt, t.ex. aktiva arbetsflöden för en resurs, kommentarer/anteckningar, aktivitetsloggar och versioner.

![Sortera tidslinjeposter för en resurs](assets/sort_timeline.gif)
*Bild: Sortera tidslinjeposter för en resurs*

>[!NOTE]
>
>I [Samlingskonsol](/help/assets/manage-collections.md#navigate-the-collections-console), **[!UICONTROL Show All]** finns det alternativ för att endast visa kommentarer och arbetsflöden. Dessutom visas tidslinjen bara för samlingar på den översta nivån som visas i konsolen. Den visas inte om du navigerar i någon av samlingarna.

>[!NOTE]
>
>Tidslinjen innehåller flera [alternativ som är specifika för innehållsfragment](content-fragments/content-fragments.md).

## Annotate assets {#annotating}

Annotations are comments or explanatory notes added to images or videos. Annotations provide marketers the ability to collaborate and leave feedback about assets.

Video annotations are only supported on browsers with HTML5-compatible video formats. Videoformat som Assets stöder beror på webbläsaren.

>[!NOTE]
>
>För innehållsfragment, [anteckningar skapas i fragmentredigeraren](content-fragments/content-fragments.md).

1. Navigera till platsen för resursen som du vill lägga till anteckningar i.
1. Tryck/klicka på **[!UICONTROL Annotate]** ikoner från något av följande:

   * [Snabbåtgärder](#quick-actions)
   * Från verktygsfältet när du har valt resursen eller navigerat till resurssidan

   ![chlimage_1-233](assets/chlimage_1-233.png)

1. Lägg till en kommentar i rutan **[!UICONTROL Comment]** längst ned på tidslinjen. Du kan också markera ett område i bilden och lägga till en anteckning i dialogrutan **[!UICONTROL Add Annotation]**.

   ![chlimage_1-234](assets/chlimage_1-234.png)

<!--
1. To notify a user about an annotation, specify the email address of the user and add the comment. For example, to notify Aaron MacDonald about an annotation, enter @aa. Hints for all matching users is displayed in a list. Select Aaron's email address from the list to tag her with the comment. Similarly, you can tag more users anywhere within the annotation or before or after it.
-->

>[!NOTE]
>
>För användare som inte är administratörer visas endast förslag om användaren har läsbehörighet på `/home` i CRXDE.

![chlimage_1-235](assets/chlimage_1-235.png)

1. När du har lagt till anteckningen klickar du på **[!UICONTROL Add]** för att spara den. Ett meddelande om anteckningen skickas till Aaron.

   ![chlimage_1-236](assets/chlimage_1-236.png)

   >[!NOTE]
   >
   >Du kan lägga till flera anteckningar innan du sparar dem.

1. Tryck/klicka **[!UICONTROL Close]** om du vill avsluta anteckningsläget.
1. Om du vill visa meddelandet loggar du in på Assets med Aaron MacDonalds inloggningsuppgifter och klickar på knappen **[!UICONTROL Notifications]** om du vill visa meddelandet.

   >[!NOTE]
   >
   >Anteckningar kan också läggas till i videomaterialet. När du kommenterar videoklipp pausas spelaren så att du kan anteckna i en bildruta. Mer information finns i [hantera videomaterial](manage-video-assets.md).

1. Om du vill välja en annan färg så att du kan skilja på användarna klickar/trycker du på profilikonen och klickar/trycker **[!UICONTROL My Preferences]**.

   ![chlimage_1-237](assets/chlimage_1-237.png)

   Ange önskad färg i rutan **[!UICONTROL Annotation Color]** och klicka/tryck sedan på **[!UICONTROL Accept]**.

   ![chlimage_1-238](assets/chlimage_1-238.png)

>[!NOTE]
>
>Du kan också lägga till anteckningar i en samling. Men om en samling innehåller underordnade samlingar kan du bara lägga till anteckningar/kommentarer i den överordnade samlingen. Alternativet Anteckning är inte tillgängligt för underordnade samlingar.

### Visa sparade anteckningar {#viewing-saved-annotations}

Du kan bara visa en anteckning åt gången.

>[!NOTE]
>
>Om du markerar flera anteckningar visas den senaste anteckningen i användargränssnittet.
>
>Flerval stöds bara för utskrift av kommenterade objekt som PDF.

1. Om du vill visa sparade anteckningar för en resurs går du till resursens plats och öppnar resurssidan för resursen.

1. Tryck/klicka på ikonen GlobalNav och välj **[!UICONTROL Timeline]** från listan.

   ![chlimage_1-239](assets/chlimage_1-239.png)

1. I listan **[!UICONTROL Show All]** på tidslinjen väljer du **[!UICONTROL Comments]** för att filtrera resultatet baserat på kommentarer.

   ![chlimage_1-240](assets/chlimage_1-240.png)

   Tryck/klicka på en kommentar i **[!UICONTROL Timeline]** för att visa motsvarande anteckning i bilden.

   ![chlimage_1-241](assets/chlimage_1-241.png)

   Tryck/klicka **[!UICONTROL Delete]**, om du vill ta bort en viss kommentar.

### Skriv ut anteckningar {#printing-annotations}

Om en resurs har anteckningar eller har genomgått ett granskningsarbetsflöde kan du skriva ut resursen tillsammans med anteckningar och granskningsstatus som en PDF-fil för offlinegranskning.

Du kan också välja att bara skriva ut anteckningarna eller granskningsstatusen.

>[!NOTE]
>
>Du kan markera flera anteckningar när du skriver ut den kommenterade resursen som PDF.

Tryck/klicka på knappen **[!UICONTROL Print]** och följ instruktionerna i guiden. The **[!UICONTROL Print]** visas bara i verktygsfältet när resursen har tilldelats minst en antecknings- eller granskningsstatus.

1. Öppna förhandsgranskningssidan för en resurs i resursgränssnittet.
1. Gör något av följande:

   * Om du vill skriva ut alla anteckningar och granskningsstatus hoppar du över steg 3 och går direkt till steg 4.
   * Om du vill skriva ut särskilda anteckningar och granskningsstatus öppnar du [tidslinje](/help/assets/manage-digital-assets.md#timeline) och sedan gå till steg 3.

1. Om du vill skriva ut särskilda anteckningar väljer du anteckningarna på tidslinjen.

   ![chlimage_1-242](assets/chlimage_1-242.png)

   Om du bara vill skriva ut granskningsstatusen markerar du den på tidslinjen.

   ![chlimage_1-243](assets/chlimage_1-243.png)

1. Tryck/klicka på ikonen **[!UICONTROL Print]** i verktygsfältet.

   ![chlimage_1-244](assets/chlimage_1-244.png)

1. I dialogrutan Skriv ut väljer du den position du vill att anteckningarna/granskningsstatusen ska visas på PDF. Om du till exempel vill att anteckningarna/statusen ska skrivas ut längst upp till höger på sidan som innehåller den utskrivna bilden använder du **Övre vänster** inställning. Det är markerat som standard.

   ![chlimage_1-245](assets/chlimage_1-245.png)

   Du kan välja andra inställningar beroende på var du vill att anteckningarna/statusen ska visas i den utskrivna PDF-filen. Om du vill att anteckningarna/statusen ska visas på en sida som är skild från den utskrivna resursen väljer du **[!UICONTROL Next Page]**.

1. Klicka på **[!UICONTROL Print]**. Beroende på vilket alternativ du väljer i steg 2 visar den genererade PDF-filen anteckningarna/statusen vid den angivna positionen. Om du till exempel väljer att skriva ut både anteckningar och granskningsstatus med inställningen **Överst till vänster** liknar genererade utdata den PDF-fil som återges här.

   ![chlimage_1-246](assets/chlimage_1-246.png)

1. Hämta eller skriv ut PDF med alternativen längst upp till höger.

   ![chlimage_1-247](assets/chlimage_1-247.png)

   Om du vill ändra utseendet på den återgivna PDF-filen, t.ex. teckensnittsfärg, storlek och format, bakgrundsfärg för kommentarer och statusvärden, öppnar du **[!UICONTROL Annotation PDF configuration]** från Configuration Manager och ändra önskade alternativ. Om du till exempel vill ändra visningsfärgen för den godkända statusen ändrar du färgkoden i motsvarande fält. Mer information om hur du ändrar teckenfärg för anteckningar finns i [Anteckningar](/help/assets/manage-digital-assets.md#annotating).

   Återgå till den återgivna PDF-filen och uppdatera den. Det uppdaterade PDF återspeglar de ändringar du gjorde.

## Resursversionshantering {#asset-versioning}

Versionshantering skapar en ögonblicksbild av digitala resurser vid en viss tidpunkt. Versionshantering hjälper till att återställa resurser till ett tidigare läge vid ett senare tillfälle. Om du till exempel vill ångra en ändring som du har gjort i en resurs återställer du den oredigerade versionen av resursen.

Här följer exempel där du skapar versioner:

* Du ändrar en bild i ett annat program och överför den till Assets. En version av bilden skapas så att originalbilden inte skrivs över.
* Du redigerar metadata för en resurs.
* Du använder [!DNL Experience Manager] för att checka ut en befintlig resurs och spara dina ändringar. En ny version skapas varje gång resursen sparas.

Du kan även aktivera automatisk versionshantering via ett arbetsflöde. När du skapar en version för en resurs sparas metadata och återgivningar tillsammans med versionen. Återgivningar är renderingsalternativ för samma bilder, till exempel en PNG-återgivning av en överförd JPEG-fil.

Versionsfunktionen gör följande:

* Skapa en version av en resurs.
* Visa aktuell revision för en tillgång.
* Återställ resursen till en tidigare version.

1. Navigera till platsen för resursen som du vill skapa en version för och öppna resursens sida genom att trycka/klicka på den.

1. Tryck/klicka på ikonen GlobalNav och välj **[!UICONTROL Timeline]** på menyn.

   ![tidslinje](assets/timeline.png)

1. Tryck/klicka på **[!UICONTROL Actions]** (pil) längst ned för att visa de tillgängliga åtgärder du kan utföra på resursen.

   ![chlimage_1-249](assets/chlimage_1-249.png)

1. Tryck/klicka **[!UICONTROL Save as Version]** för att skapa en version för resursen.

   ![chlimage_1-250](assets/chlimage_1-250.png)

1. Lägg till en etikett och kommentar och klicka sedan på **[!UICONTROL Create]** för att skapa en version. Du kan också trycka/klicka **Avbryt** för att avsluta åtgärden.

   ![chlimage_1-251](assets/chlimage_1-251.png)

1. Om du vill visa den nya versionen öppnar du listan **[!UICONTROL Show All]** på tidslinjen från sidan med resursinformation eller från Assets-gränssnittet och väljer **[!UICONTROL Versions]**. Alla versioner som skapas för en resurs visas på fliken Tidslinje. Du kan filtrera listan så att olika versioner visas genom att klicka på listrutepilen och välja **[!UICONTROL Versions]** i listan.

   ![versions_option](assets/versions_option.png)

1. Välj en specifik version för resursen om du vill förhandsgranska den eller aktivera den för visning i resursgränssnittet.

   ![select_version](assets/select_version.png)

1. Lägg till en etikett och kommentar för versionen som ska återställas till den aktuella versionen i resursgränssnittet.

   ![save_version](assets/save_version.png)

1. Om du vill generera en förhandsgranskning för versionen trycker/klickar du på **[!UICONTROL Preview Version]**.
1. Om du vill visa den här versionen i resursgränssnittet väljer du **[!UICONTROL Revert to this Version]**.
1. Om du vill jämföra två versioner går du till resursens tillgångssida och trycker/klickar på den version som ska jämföras med den aktuella versionen.

   ![select_version_tocompare](assets/select_version_tocompare.png)

1. Välj den version du vill jämföra på tidslinjen och dra reglaget åt vänster för att lägga den här versionen ovanpå den aktuella versionen och jämföra.

   ![compare_versions](assets/compare_versions.png)

### Starta ett arbetsflöde för en resurs {#starting-a-workflow-on-an-asset}

1. Navigera till platsen för resursen som du vill starta ett arbetsflöde för och tryck/klicka på resursen för att öppna resurssidan.
1. Tryck/klicka på ikonen GlobalNav och välj **[!UICONTROL Timeline]** på menyn för att visa tidslinjen.

   ![tidslinje-1](assets/timeline-1.png)

1. Tryck/klicka på **[!UICONTROL Actions]** (pil) längst ned för att öppna en lista med tillgängliga åtgärder för resursen.

   ![chlimage_1-252](assets/chlimage_1-252.png)

1. Tryck/klicka **[!UICONTROL Start Workflow]** från listan.

   ![chlimage_1-253](assets/chlimage_1-253.png)

1. I **[!UICONTROL Start Workflow]** väljer du en arbetsflödesmodell i listan.

   ![chlimage_1-254](assets/chlimage_1-254.png)

1. (Valfritt) Ange en rubrik för arbetsflödet som kan användas som referens för arbetsflödesinstansen.

   ![chlimage_1-255](assets/chlimage_1-255.png)

1. Tryck/klicka på **[!UICONTROL Start]** och sedan på **[!UICONTROL Proceed]** i dialogrutan för att bekräfta. Varje steg i arbetsflödet visas på tidslinjen som en händelse.

   ![chlimage_1-256](assets/chlimage_1-256.png)

## Samlingar {#collections}

En samling är en ordnad uppsättning med resurser. Använd samlingar för att dela resurser mellan användare.

* En samling kan innehålla resurser från olika platser eftersom de bara innehåller referenser till dessa resurser. Varje samling bevarar materialens referensintegritet.
* Du kan dela samlingar med flera användare med olika behörighetsnivåer, inklusive redigering, visning och så vidare.

Mer information om hantering av samlingar finns i [hantera samlingar](/help/assets/manage-collections.md).

## Dölj utgångna resurser när du visar resurser i skrivbordsappen eller Adobe Asset Link {#hide-expired-assets-via-acp-api}

[!DNL Experience Manager] datorprogrammet ger åtkomst till DAM-databasen från Windows eller Mac. Adobe Asset Link ger åtkomst till resurser inifrån det stöd [!DNL Creative Cloud] datorprogram.

När du bläddrar bland resurser inifrån [!DNL Experience Manager] de utgångna resurserna visas inte i användargränssnittet. Administratörer kan göra följande konfiguration för att förhindra att resurser som har gått ut visas, söks och hämtas när de bläddrar bland resurser från skrivbordsappen och Asset Link. Konfigurationen fungerar för alla användare, oavsett administratörsbehörighet.

Kör följande CURL-kommando. Säkerställ läsåtkomst på `/conf/global/settings/dam/acpapi/` för de användare som har åtkomst till resurser. Användare som är en del av `dam-user` gruppen har behörigheten som standard.

```curl
curl -v -u admin:admin --location --request POST 'http://localhost:4502/conf/global/settings/dam/acpapi/configuration/_jcr_content' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'jcr:title=acpapiconfig' \
--data-urlencode 'hideExpiredAssets=true' \
--data-urlencode 'hideExpiredAssets@TypeHint=Boolean' \
--data-urlencode 'jcr:primaryType=nt:unstructured' \
--data-urlencode '../../jcr:primaryType=sling:Folder'
```

Om du vill veta mer kan du se hur [bläddra bland DAM-resurser med datorprogrammet](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#browse-search-preview-assets) och [Så här använder du Adobe Asset Link](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/manage-assets-using-adobe-asset-link.ug.html).

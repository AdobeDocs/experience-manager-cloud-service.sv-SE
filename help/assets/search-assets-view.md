---
title: Lär dig hur du söker efter och identifierar resurser i  [!DNL Assets view]?
description: Läs om hur du söker efter och identifierar resurser i AEM Assets-vyn. Med de kraftfulla sökfunktionerna kan du snabbt hitta rätt resurs och hjälpa dig att förbättra innehållets hastighet.
role: User
exl-id: abfe6a91-1699-436f-8bf4-0d0bf2369f46
feature: Asset Management, Publishing, Collaboration, Asset Processing
source-git-commit: f83324be68bdab65e5c76ef336eb7e4a2e318dd1
workflow-type: tm+mt
source-wordcount: '1566'
ht-degree: 0%

---

# Sök efter resurser i [!DNL Assets view] {#search-assets}

>[!CONTEXTUALHELP]
>id="assets_search"
>title="Sök i Assets"
>abstract="Sök efter resurser genom att ange ett nyckelord i sökfältet eller genom att filtrera resurser baserat på status, filtyp, MIME-typ, storlek, skapande, ändring och förfallodatum. Du kan också använda egna filter förutom standardfiltren. Du kan spara de filtrerade resultaten som en sparad sökning eller som en smart samling."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-assets-essentials/help/manage-collections.html?lang=sv-SE#manage-smart-collection" text="Skapa smarta samlingar"

[!DNL Assets view] innehåller en effektiv sökning som bara fungerar som standard. Sökningen är omfattande eftersom den är en fulltextsökning. Med de kraftfulla sökfunktionerna kan du snabbt hitta rätt resurs och hjälpa dig att förbättra innehållets hastighet. [!DNL Assets view] innehåller fulltextsökning och även sökningar via metadata som smarta taggar, titel, skapad den och copyright.

Så här söker du efter resurser:

* Klicka i sökrutan högst upp på sidan. Som standard söker programmet i den mapp som du just nu bläddrar i. Gör något av följande:

  ![sökruta](assets/search-box.png)

   * Sök med ett nyckelord och ändra mappen om du vill. Tryck på Retur.

   * Börja arbeta med en nyligen visad resurs genom att söka direkt efter den. Klicka i sökrutan och välj en nyligen visade resurs bland förslagen.

## Filtrera sökresultaten {#refine-search-results}

Du kan förfina sökresultaten för att hitta relevanta resurser genom att använda flera filter. Dessa filter, som konfigureras av en administratör, baseras på filer, mappar och samlingar. Se [Anpassa sökfilter](custom-search-filters.md).

![Sökfilter](assets/filters-panel.gif)

Du kan filtrera sökresultaten baserat på följande parametrar.

* Resursstatus: Filtrera sökresultaten med en `Approved`-, `Rejected`- eller `No Status`-resursstatus.
* Filtyp: Filtrera sökresultaten efter de filtyper som stöds, `Images`, `Documents` och `Videos`.
* MIME-typ: Filtrera efter ett eller flera av de filformat som stöds. <!-- TBD:  [supported file formats](/help/using/supported-file-formats.md). -->
* Bildstorlek: Ange en av flera av de minsta och högsta måtten för att filtrera bilder. Storleken anges i pixeldimensioner och är inte bildens filstorlek.
* Skapad: Datum när resursen skapades enligt metadatan. Standarddatumformatet som används är `yyyy-mm-dd`.
* Ändrad: Senaste ändringsdatum för resurserna. Standarddatumformatet som används är `yyyy-mm-dd`.
* Förfallodatum: Filtrera sökresultaten baserat på en `Expired`-resursstatus. Du kan dessutom ange ett förfallodatumintervall för resurser för att ytterligare filtrera sökresultaten.
* Egna filter: [Lägg till anpassade filter](#custom-filters) i användargränssnittet i vyn Assets. Använd de anpassade filtren utöver standardfiltren för att förfina sökresultaten.

Du kan sortera de sökda resurserna i stigande eller fallande ordning `Name`, `Relevance`, `Size`, `Modified` och `Created`. De sökda resurserna sorteras som standard baserat på `Relevance`.

<!--
  
## Manage custom filters {#custom-filters}

**Permissions required:**  `Can Edit`, `Owner`, or Administrator.

Assets view also enable you to add custom filters to the user interface. You can then apply those custom filters in addition to the [standard filters](#refine-search-results) to refine your search results.

Assets view provides the following custom filters:

<table>
    <tbody>
     <tr>
      <th><strong>Custom filter name</strong></th>
      <th><strong>Description</strong></th>
     </tr>
     <tr>
      <td>Title</td>
      <td>Filter assets using the asset title. The title that you specify in the case-sensitive search criteria must match the exact title of the asset to display in the results.</td>
     </tr>
     <tr>
      <td>Name</td>
      <td>Filter assets using the asset file name. The name that you specify in the case-sensitive search criteria must match the exact file name of the asset to display in the results.</td>
     </tr>
     <tr>
      <td>Asset Size</td>
      <td>Filter assets by defining a size range, in bytes, in the search criteria for an asset to display in the results.</td>
     </tr>
     <tr>
      <td>Predicted Tags</td>
      <td>Filter assets using the asset smart tag. The smart tag name that you specify in the case-sensitive search criteria must match the exact smart tag name of the asset to display in the results. You cannot specify multiple smart tags in search criteria.</td>
     </tr>    
    </tbody>
   </table>

   <!--
   You can use a wildcard operator (*) to enable Assets view to display assets in the results that partially match the search criteria. For example, if you define <b>ma*</b> as the search criteria, Assets view displays assets with title, such as, market, marketing, man, manchester, and so on in the results.

   You can use a wildcard operator (*) to enable Assets view to display assets in the results that partially match the search criteria.

   You can use a wildcard operator (*) to enable Assets view to display assets in the results that partially match the search criteria. You can specify multiple smart tags separated by a comma in the search criteria.

   

### Add custom filters {#add-custom-filters}

To add custom filters:

1. Click **[!UICONTROL Filters]**. 

1. In the **[!UICONTROL Custom Filters]** section, click **[!UICONTROL Edit]** or **[!UICONTROL Add Filters]**.

   ![Add custom filters](assets/add-custom-filters.png)

1. On the **[!UICONTROL Custom filters management]** dialog box, select the filters that you need to add to the existing list of filters. Select **[!UICONTROL Custom Filters]** to select all filters.

1. Click **[!UICONTROL Confirm]** to add the filters to the user interface.

### Remove custom filters {#remove-custom-filters}

To remove custom filters:

1. Click **[!UICONTROL Filters]**. 

1. In the **[!UICONTROL Custom Filters]** section, click **[!UICONTROL Edit]**.

1. On the **[!UICONTROL Custom filters management]** dialog box, deselect the filters that you need to remove from the existing list of filters.

1. Click **[!UICONTROL Confirm]** to remove the filters from the user interface.

-->

## AI-sökning {#ai-search}

AI-sökning är en avancerad sökfunktion som förstår innebörden och avsikten bakom en användarfråga i stället för att förlita sig på exakta nyckelordsmatchningar. Det använder artificiell intelligens (AI) och maskininlärning för att leverera mer korrekta och kontextmedvetna resultat.

Till skillnad från traditionell nyckelordsbaserad sökning, som söker efter exakta termer, tolkas relationerna mellan ord, begrepp och användarmetod i AI Search. Detta gör att användarna hittar det de söker efter, även om deras fråga är formulerad på ett annat sätt, innehåller stavfel eller är på ett annat språk.

Några av fördelarna med den:

* **Flerspråksstöd**: Sök på flera språk utan att exakta översättningar krävs. Användarna kan hitta relevant innehåll oavsett frågespråk.

* **Hanterar felstavningar**: Tolkar stavfel och typografiska stavfel, vilket ger korrekta resultat även om indata är felaktiga.

* **Förstå synonymer**: Ger resultat för relaterade termer och fraser, så användarna behöver inte gissa rätt nyckelord.

* **Kontextmedveten sökning**: Identifierar avsikten bakom en fråga, inte bara de exakta orden.

### Exempel på AI-sökning {#examples-ai-search}

**Exempelfråga**: *Kvinna som dricker kaffe*

Den traditionella nyckelordsbaserade sökningen söker efter exakta matchningar av metadata för resurser, som `Woman`, `drinking`, `Coffee`, och returnerar resurser som innehåller alla dessa termer i metadata.

AI-sökning matchar emellertid liknande ord som `Girl`, `Lady` i fallet `Woman` och `Cappuccino` och `Latte` i fallet `Coffee`.

På samma sätt kan du ange den här uppmaningen på spanska eller felstava `Woman` som `Wman` och ändå få samma resultat.

![Semantisk sökning i Assets-vyn](assets/semantic-search.png)

### Aktivera eller inaktivera AI-sökning i Assets-vyn {#enable-disable-ai-search}

Gör så här för att aktivera eller inaktivera AI-sökning:

1. Navigera till **[!UICONTROL Settings]** >> **[!UICONTROL General Settings]** och välj fliken **[!UICONTROL Search]**.

1. I avsnittet **[!UICONTROL Search]** väljer du **[!UICONTROL AI Search]** för att aktivera AI-sökning eller **[!UICONTROL Keyword]** för att inaktivera den.

   ![Semantisk sökning i Assets-vyn](/help/assets/assets/enable-disable-ai-search.png)

1. Klicka på **[!UICONTROL Save]**.


## Sök efter resurser med [!DNL Adobe Firefly] {#search-firefly}

Du kan söka efter en resurs som inte är tillgänglig i någon av resursmapparna genom att använda sökfunktionen [!DNL Adobe Firefly] i [!DNL Experience Manager Assets]. På så sätt kan du effektivt generera resurser i realtid som inte lagras i resursmapparna.

### Innan du börjar {#search-assets-firefly-prereqs}

Du måste ha en aktiv [!DNL Adobe Express]-prenumeration.

### Generera resurser {#generate-assets-firefly}

Så här skapar du nya resurser med [!DNL Adobe Firefly]:

1. Navigera till arbetsytan [!DNL AEM Assets].

1. Skriv resursnamnet i sökfältet. Du kan till exempel söka efter en resurs med nyckelordet `Bugatti Type 57`. När du söker efter resursen hittas inga resultat eftersom resursen inte finns i någon av resursmapparna. Klicka på **[!UICONTROL Generate with Firefly]** om du vill generera resurser med hjälp av AI. Skärmen [!DNL Adobe Firefly] visas.

   ![Integrering med Firefly](assets/firefly-integration.png)

   De nya resurserna har genererats. Du kan dessutom ändra bildbeskrivningen genom att skriva den nya textrutan i beskrivningsrutan. [Lär dig hur du skriver en bra AI-uppmaning för att generera extraordinärt och relevant innehåll](https://helpx.adobe.com/in/firefly/using/tips-and-tricks.html). Du kan även [redigera bilden med olika andra funktioner, som att ändra format, bilddimensioner och mer](https://helpx.adobe.com/in/firefly/using/text-to-image.html).

   ![Integrering med Firefly](assets/bugatti-type-57.png)

1. Markera en bild som du vill spara. Klicka på **[!UICONTROL Save]** om du vill spara resurserna i den mapp du föredrar så att du enkelt kommer åt dem.

1. Formuläret Spara resurs visas. Ange följande fält:

   * Ange ett namn för filen i fältet **Spara som**.
   * Välj en målmapp.
   * Ange detaljer som projektnamn eller kampanjnamn, nyckelord, kanaler, tidsram och region.

   ![Integrering med Firefly](assets/save-generated-asset.png)

1. Klicka på **Spara som ny resurs** för att spara resursen/resurserna.

<!--

### Upload assets {#upload-assets-firefly}

To upload the generated asset to the assets repository:

1. Click **[!UICONTROL Upload]**.
1. Select the asset folder to which you need to upload the asset and click **[!UICONTROL Select Folder]**.
 ![Upload asset](assets/upload-asset-firefly.jpg)

 -->

## Sparade sökningar {#saved-search}

Sökfunktionen är ganska enkel att använda i [!DNL Assets view]. I sökrutan kan du inte bara skriva ett nyckelord och trycka på Retur för att se resultatet. Du kan också snabbt söka igen efter dina nyligen sökta nyckelord med ett enda klick.

Du kan också filtrera sökresultaten baserat på specifika villkor runt metadata och resurstyp. För filter som används ofta kan du spara sökparametrarna i [!DNL Assets view] för att förbättra sökupplevelsen. Du kan sedan markera den sparade sökningen och använda filtret med bara ett klick.

Om du vill skapa en sparad sökning söker du efter en resurs, använder ett eller flera filter och klickar på **[!UICONTROL Save as]** > **[!UICONTROL Saved Search]** på panelen [!UICONTROL Filters]. Du kan också klicka på **[!UICONTROL Save as]** och välja **[!UICONTROL Smart Collection]** för att spara resultatet som en smart samling. Mer information finns i [Skapa en smart samling](manage-collections.md#create-a-smart-collection).

![Skapa smart samling](assets/create-smart-collection.png)

<!-- TBD: Search behavior. Full-text search. Ranking and rank boosts. Hidden assets.
Report poor UX that users can only save a filtered search and not a simple search.
.
Are other supported files fully indexed and support full-text search? Eg. audio/videos files can at best have metadata indexed.
Anything about ranking of assets displayed in search results?

What about temporarily hiding an asset (suspending search on it) from the search results? If an asset is undergoing review collaboration, should it be used by others? Should it be hidden in search?

When userA is searching and userB add an asset that matches search results, will the asset display in search as soon as userA refreshes the page? Assuming indexing is near real-time. May not be so for bulk uploads.
-->

## Arbeta med sökresultat {#work-with-search-results}

Du kan markera de resurser som visas i sökresultaten och göra följande:

* **Hitta liknande bild**: Hitta en liknande bildresurs i Assets-gränssnittet baserat på metadata och smarta taggar.

* **Information**: Visa och redigera resursegenskaper.

* **Hämta**: Hämta en resurs.

* **Lägg till i samling**: Lägg till den valda resursen i en samling.

* **Fäst i snabbåtkomst**: [Fäst en resurs](my-workspace-assets-view.md) för snabbare åtkomst när du behöver den senare. Alla fästa objekt visas i avsnittet **Snabbåtkomst** i Min Workspace.

* **Öppna i Adobe Express**: Redigera en bild i den integrerade Adobe Express-bilden från Experience Manager Assets-skärmen.

* **Redigera**: Redigera bilden med Adobe Express.

* **Dela länk**: [Dela länkar](share-links-for-assets-view.md) för en resurs med andra användare så att de kan komma åt och hämta den.

* **Ta bort**: Ta bort en resurs.

* **Kopiera**: Kopiera en resurs till en annan mapplats.

* **Flytta**: Flytta en resurs till en annan mapplats.

* **Byt namn på**: Byt namn på en resurs.

* **Kopiera till bibliotek**: Lägg till en resurs i biblioteket.

* **Tilldela uppgifter**: Tilldela uppgifter till användare för en resurs.

* **Titta**: [Övervaka de åtgärder](https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-service/content/assets/manage/search-assets) som utförs på en resurs.

## Konfigurera den första startsidan för sökning {#configuring-search-first-homepage}

I Assets-vyn kan du välja standardlandningssida för din organisation. När du använder Sök först som startsida har du också möjlighet att anpassa sidans varumärke genom att konfigurera bakgrunds- och logotypbilderna så att de passar ert varumärke.

Så här konfigurerar du den första startsidan för sökningen:

1. Navigera till **[!UICONTROL Settings]** > **[!UICONTROL General Settings]**.
1. Välj **[!UICONTROL Search first]**. Sökningskonfigurationen öppnas sedan. Du kan ange [justering](#setting-alignment-search-bar) eller [ange bakgrunds- och logotypbilden](#setting-background-image-and-logo) för din hemsida.

### Ange justering för sökfältet {#setting-alignment-search-bar}

Med [!DNL Assets view] kan du ändra justeringen av sökfältet. Du kan ange att sökfältet ska visas antingen i mitten eller högst upp. Välj lämplig justering och klicka på **[!UICONTROL Save]**.

![Sök efter justering för första hemsida](assets/search-first-alignment.png)

### Ställa in bakgrunds- och logotypbild för hemsidan {#setting-background-image-and-logo}

Du kan lägga till en logotyp och en bakgrundsbild på din första söksida. Utför följande steg:

1. Navigera till avsnittet **[!UICONTROL Background and Logo image]** under **[!UICONTROL Homepage]**.
1. Klicka på **[!UICONTROL Replace]** om du vill bläddra bland bilder från den befintliga resurskatalogen.
1. Klicka på **[!UICONTROL Save]**. [Förhandsgranska](#preview-configured-homepage) ändringarna för att granska ändringarna.

### Förgranska konfigurerad startsida {#preview-configured-homepage}

Du kan förhandsgranska om du vill kontrollera layout och formatering för den första söksidan. Med hjälp av **[!UICONTROL Preview]** kan du korrigera layouten eller göra ändringar efter behov. Om du vill förhandsgranska den konfigurerade startsidan följer du stegen nedan:

1. Klicka på **[!UICONTROL General Settings]** och välj **[!UICONTROL Search first]**.
1. Navigera till **[!UICONTROL Customize search first homepage]** och klicka på **[!UICONTROL Preview]**. Växla genom knappen **[!UICONTROL Dark theme]** om du vill förhandsgranska hemsidan i mörkt eller ljust tema.
1. Klicka på **[!UICONTROL Close]** för att stänga förhandsgranskningsskärmen.

   ![Sök i förhandsvisning av första hemsidan](/help/assets/assets/search-first-preview.gif)


<!--

## Contextual Search {#contextual-search}

You can also search assets available in the repository by defining text prompts. Experience Manager Assets automatically transforms those text prompts to search filters and displays the search results. You can view and modify automatic filters using the Filters Pane to further narrow down the search results.

### Access Contextual Search {#access-contextual-search}

To access Contextual Search in Experience Manager Assets:

1. Click **[!UICONTROL Search]** in the left pane.

   ![Contextual Search](assets/access-contextual-search.png)

1. Define the text prompt in the Search text box and click **[!UICONTROL Contextual Search]**.

   ![Contextual Search text prompt](/help/assets/assets/wknd-contextual-search.png)

   [!DNL Experience Manager Assets] displays the search results.

### Supported filters {#supported-filters}

Contextual Search supports the following filters out-of-the-box. Base your text prompts on these filters to view appropriate search results.

* Image height

* Image width

* File type: image, document, video, or folder.

* MIME type: JPG, PNG, TIFF, GIF, MP4, PDF, PPTX, DOCX or XLSX

* Created date

* Modified date

* Expiration date

* Asset status: Approved, Rejected, or all

* Expired assets

### Examples for the text prompts {#text-prompts-examples}

**Example 1**

**Text Prompt**: Images created this month.

[!DNL Experience Manager Assets] applies the following filters automatically and displays the search results:

![Contextual Search Example 1](assets/contextual-search-example1.png)

**Example 2**

**Text prompt**: Images at least 200px tall and 100px wide with beach and clear sky.

[!DNL Experience Manager Assets] applies the following filters automatically and displays the search results:

![Contextual Search Example 2](assets/contextual-search-example2.png)

**Example 3**

**Text prompt**: I need images of blue sky that are 1500 and 2500 pixel height and created in the past month that is not expired and approved.

[!DNL Experience Manager Assets] applies the following filters automatically and displays the search results:

![Contextual Search Example 3](assets/contextual-search-example3.png)

The following video illustrates the end-to-end process from accessing the Contextual Search User Interface to defining text prompts, and viewing the search results.

>[!VIDEO](https://video.tv.adobe.com/v/3428407)

### Disable Contextual Search {#disable-contextual-search}

Administrators also have the option to disable Contextual Search for users in your organization. To do so, execute the following steps:

1. Navigate to **[!UICONTROL Settings]** > **[!UICONTROL General Settings]**.

1. In the [!UICONTROL Contextual Search] section, turn off the **[!UICONTROL Enable Contextual Search for your organization]** toggle to disable the Contextual Search feature for all users in your organization.  

### Contextual Search feedback {#contextual-search-feedback}

If you need to provide feedback on the Contextual Search feature, click ![Contextual Search icon](assets/do-not-localize/Smock_Help_18_N.svg)  and click the Feedback icon. Select the feedback type, specify the subject and description, and click **[!UICONTROL Submit]**.

![Contextual Search feedback](assets/contextual-search-feedback.png)

-->

## Nästa steg {#next-steps}

* [Titta på en video om du vill söka efter resurser i Assets-vyn](https://experienceleague.adobe.com/docs/experience-manager-learn/assets-essentials/basics/using.html?lang=sv-SE)

* Ge produktfeedback med alternativet [!UICONTROL Feedback] som finns i användargränssnittet i Assets-vyn

* Ge feedback genom att [!UICONTROL Edit this page] ![redigera sidan](assets/do-not-localize/edit-page.png) eller [!UICONTROL Log an issue] ![skapa ett GitHub-problem](assets/do-not-localize/github-issue.png) som är tillgängligt på den högra sidopanelen.

* Kontakta [kundtjänst](https://experienceleague.adobe.com/sv?support-solution=General#support)




---
title: Söka efter resurser i Content Hub
description: Lär dig söka efter resurser i  [!DNL Content Hub]
role: User
source-git-commit: 5a968440c8841abe7af2c81c4af12258b7e4547f
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 0%

---


# Sök i Assets i [!DNL Content Hub] {#search-assets}

![Dela banderollbild för resurser](assets/search.png)

När du har ett stort antal resurser i din databas är det tidskrävande att söka efter rätt resurs. [!DNL The Content Hub]-sökningen ger dig möjlighet att söka efter godkända resurser så att du kan utföra ytterligare åtgärder på dem, till exempel hämta, dela eller skapa samlingar. Du kan använda olika funktioner för att begränsa sökresultaten, till exempel textbaserad sökning, filter, taggar eller smart taggspecifik sökning, sökning efter ett visst filformat och så vidare.

## Förutsättningar {#prerequisites}

[Content Hub-användare](deploy-content-hub.md#onboard-content-hub-users) kan utföra åtgärder som nämns i den här artikeln.

## Vad du kan söka efter  {#what-you-can-search}

[!DNL Content Hub]-sökningen ger resultat baserat på:

* **Matchande text:** Med [!DNL Content Hub]-sökningen kan du söka efter en resurs med hjälp av dess namn eller beskrivning. Du kan utföra nyckelordsbaserad sökning, som jämför nyckelordet med texten som finns i egenskaperna för en resurs.

* **Matchande kontext:** [!DNL Content Hub] sökresultatlistan innehåller ungefärliga resultat för resurser som du får baserat på matchande kontext. Om du till exempel skriver `cool` i sökfältet visas resurserna som är relaterade till `winter`, `snow`, `cold surroundings` i söklistan.

* **Resursinformation (titel, taggar eller smarta taggar):** [!DNL Content Hub] använder algoritmen för smart sökning för att rangordna sökresultaten korrekt och så relevant som möjligt. [Metadata](#asset-properties.md) är samlingen av alla data som är tillgängliga för en resurs, men det är inte säkert att de finns i resursen. [Det hjälper dig att kategorisera resurser ytterligare och är till hjälp när mängden digital information växer.](/help/assets/configure-content-hub-ui-options.md##configure-metadata-search-content-hub)

* **Senast ändrat:** Resurserna som nyligen ändrades visas högst upp i sökresultatlistan. Du kan även filtrera datumintervallet efter dina behov.

* **Användning:** De resurser som används ofta visas högst upp i söklistan.

* **Sökhistorik:** Klicka i sökrutan utan att skriva ett tecken för att få tillgång till sökhistoriken. Du kan också ta bort ett visst nyckelord från historiken. Sökhistoriken sparas i cacheminnet för en webbläsare, vilket innebär att du inte kan visa sökhistoriken längre om du öppnar sökningen i [!DNL Content Hub] i en annan webbläsare eller om du rensar cacheminnet för webbläsaren.

* **Sökning medan du skriver:** [!DNL Content Hub] Sökningen förbättrar sökupplevelsen genom att ge förslag som fylls i automatiskt när du börjar skriva.

## Grundläggande sökning {#basic-search}

Om du vill utföra grundläggande sökning på [!DNL the Content Hub] går du till sökfältet och anger det nyckelord som du behöver söka efter. Navigera till de filter som finns i den vänstra rutan och använd dem för att begränsa sökresultaten.

Du kan till exempel söka efter alla **[!UICONTROL JPEG]**-bilder med nyckelordet `architect` som har ändrats under det senaste året. Så här kör du det här scenariot:

1. Ange `architect` som söknyckelord.

1. Navigera till filterpanelen > **[!UICONTROL Format]** > markera **[!UICONTROL JPEG]**.

1. Navigera till **[!UICONTROL Modified]** > ange datumintervall.

   ![Grundläggande sökning](assets/basic-search.png)

## Begränsa sökresultaten med filter {#narrow-down-search-results}

Använd panelen Filter om du vill söka efter resurser baserat på metadata. Du kan filtrera sökresultat baserat på olika sökpredikt. Du kan välja alla lämpliga predikat för att minimera eller begränsa sökresultaten. När du väljer flera alternativ i ett filter visas de resurser som matchar något av de alternativ som är markerade i ett filter. När du väljer flera alternativ för olika filter visas endast de resurser som matchar alla alternativ som har valts för olika filter för att begränsa sökresultaten.

Standardfiltren innehåller filformat, godkänt av, godkänt, förfallet och inte förfallet samt förfallodatum. Administratörer kan också konfigurera de filter som visas i filterlistan. Mer information finns i [Konfigurera Content Hub användargränssnitt](configure-content-hub-ui-options.md#configure-filters-content-hub).

<!--

<table>
    <tbody>
     <tr>
      <th><strong>Search Predicate</strong></th>
      <th><strong>Description</strong></th>
      <th><strong>Properties</strong></th>
     </tr>
     <tr>
      <td> Campaigns </td>
      <td> Allows you to search using planned activity performed to take any particular action. For example, advertisement campaign run on Ferrari to know the understand the interests of people using number of clicks people perform.</td>
      <td>NA</td>
     </tr>
     <tr>
      <td> Channels </td>
      <td> Helps you to understand the path from where the asset is coming from. For example, web, social media, books, catalog, etc.</td>
      <td>NA</td>
     </tr>
     <tr>
      <td> Region </td>
      <td> Helps you to understand the location where the asset is created. For example, Japan, EMEA, Worldwide, etc.</td>
      <td>NA</td>
     </tr>
     <tr>
      <td> Keywords </td>
      <td> Keyword helps you search using terms or the words that you enter based on the topic. For example, images, low-resolution, etc.</td>
      <td>NA</td>
     </tr>
     <tr>
      <td> Timeframe </td>
      <td> Helps you search assets using timeline. For example, search by year 2024, Q3 2023, etc.</td>
      <td>NA</td>
     </tr>
     <tr>
      <td>File format</td>
      <td>Composition of an asset. The supported assets include image, document, video, printable media, and so on.</td>
      <td>
        <ul>
            <li>[!UICONTROL JPEG]</li> 
            <li>[!UICONTROL Quicktime]</li> 
            <li>[!UICONTROL PNG]</li> 
            <li>[!UICONTROL WebP]</li> 
            <li>[!UICONTROL MP4]</li> 
            <li>[!UICONTROL Plain]</li> 
            <li>[!UICONTROL PDF]</li>
            <li>[!UICONTROL SVG + XML]</li>
        </ul>
      </td>
     </tr>
     <tr>
      <td>Tags</td>
      <td>Tags help you categorize assets that can be browsed and searched more efficiently based on hierarchical taxonomies.</td>
      <td>
        <ul>
            <li>Field label</li>
            <li>Property name</li>
            <li>Path</li>
            <li>Description</li>
        </ul>
      </td>
     </tr>
     <!--<tr>
      <td>Subject</td>
      <td>Classification of assets based on their theme. For example, colorful, hiking, outdoors.</td>
      <td>NA</td>
     </tr>
          <tr>
      <td>Last modified</td>
      <td>Search assets based on their last modification. Specify the date range using the Start date and End date fields.</td>
      <td>
        <ul>
            <li>Range text (From)</li> 
            <li>Range text (To) </li>
        </ul>
      </td>
     </tr>    
     <!--<tr>
      <td>Asset ID</td>
      <td>Unique number that identifies the asset.</td>
      <td>NA</td>
     </tr>
     <tr>
      <td> Colors </td>
      <td> Helps you search assets using colors that are automatically identified in an asset using Adobe's Sensei AI capabilities.</td>
      <td>NA</td>
     </tr>  
    </tbody>
   </table>

-->

## Gör mer med sökningar {#do-more-with-search}

[!DNL The Content Hub] är inte begränsat till sökning, utan låter dig utföra ytterligare åtgärder, som [download](download-assets-content-hub.md), [share](share-assets-content-hub.md) och [lägga till resurser i samlingen](collections-content-hub.md), direkt från sök- eller förhandsgranskningsgränssnittet. Markera resurserna på sökresultatsidan för att visa dessa alternativ.

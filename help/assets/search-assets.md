---
title: Hur söker AEM resurser?
description: Lär dig hur du söker efter resurser i AEM med hjälp av panelen Filter och hur du använder resultaten som visas vid resurssökning.
contentOwner: AG
mini-toc-levels: 1
feature: Search,Metadata,Asset Distribution
role: User,Admin
exl-id: 68bdaf25-cbd4-47b3-8e19-547c32555730
source-git-commit: f7f60036088a2332644ce87f4a1be9bae3af1c5e
workflow-type: tm+mt
source-wordcount: '5434'
ht-degree: 3%

---

# Sök efter resurser i AEM {#search-assets-in-aem}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/search-assets.html) |
| AEM as a Cloud Service | Den här artikeln |

[!DNL Adobe Experience Manager Assets] har robusta metoder för resurssökning som hjälper dig att få högre innehållshastighet. Teamen kan korta time-to-market med smidig och intelligent sökfunktion med hjälp av färdiga funktioner och anpassade metoder. Funktionen för att söka resurser är central för användningen av ett digitalt resurshanteringssystem - vare sig det är till för kreativa användare, för robust hantering av resurser av företagsanvändare och marknadsförare eller för administration av DAM-administratörer. Enkla, avancerade och anpassade sökningar som du kan utföra via [!DNL Assets] användargränssnittet eller andra appar och ytor hjälper till att uppfylla dessa användningsexempel.

Resurssökning i AEM stöder följande användningsfall och den här artikeln beskriver användning, begrepp, konfigurationer, begränsningar och felsökning för dessa användningsfall.

| Sök resurser | Konfigurera och administrera sökfunktioner | Arbeta med resurssökningsresultat |
|---|---|---|
| [Grundläggande sökningar](#searchbasics) | [Sökindex](#searchindex) | [Sortera resultat](#sort) |
| [Förstå sökgränssnittet](#searchui) | [Textextrahering](#extracttextupload) | [Kontrollera egenskaper och metadata för en resurs](#checkinfo) |
| [Sökförslag](#searchsuggestions) | [Obligatoriska metadata](#mandatorymetadata) | [Ladda ned](#download) |
| [Förstå sökresultat och beteenden](#searchbehavior) | [Ändra sökfaktorer](#searchfacets) | [Massmetadatauppdateringar](#metadata-updates) |
| [Sökrankning och förstärkning](#searchrank) | [Anpassade predikat](#custompredicates) | [Smarta samlingar](#collections) |
| [Avancerad sökning: filtrering och sökningens omfattning](#scope) | | [Förstå och felsöka oväntade resultat](#unexpected-results) |
| [Sök bland andra lösningar och appar](#search-assets-other-surfaces):<ul><li>[Adobe Asset Link](#aal)</li><li>[Brand Portal](#brand-portal)</li><li>[Experience Manager datorprogram](#desktop-app)</li><li>[Adobe Stock-bilder](#adobe-stock)</li><li>[Dynamic Media-resurser](#search-dynamic-media-assets)</li></ul> | | |
| [Resursväljare](#asset-picker) | | |
| [Begränsningar](#limitations) och [Tips](#tips) | | |
| [Illustrationer](#samples) | | |

Söka efter resurser med hjälp av omsökningsfältet högst upp i [!DNL Experience Manager] webbgränssnitt. Gå till **[!UICONTROL Assets]** > **[!UICONTROL Files]** in [!DNL Experience Manager], klicka ![search_icon](assets/do-not-localize/search_icon.png) i det övre fältet anger du söknyckelord och väljer `Return`. Du kan även använda kortkommandot för nyckelord `/` (snedstreck) för att öppna Omnissearch-fältet. `Location:Assets` är förvalt för att begränsa sökningarna till DAM-resurser. `Path:/content/dam` visas även när du utför sökningar på rotnivå i **[!UICONTROL Files]** mapp. Om du navigerar till en annan mapp `Path:/content/dam/<folder name>` visas i Omnissearch-fältet för att begränsa sökningen till den aktuella mappen. [!DNL Experience Manager] ger förslag när du börjar skriva ett söknyckelord.

Använd **[!UICONTROL Filters]** för att söka efter resurser, mappar, taggar och metadata. Du kan filtrera sökresultaten baserat på de olika alternativen (predikaten), t.ex. filtyp, filstorlek, datum då filen senast ändrades, status för resursen, information om insikter och Adobe Stock-licensiering. Du kan anpassa panelen Filter och lägga till eller ta bort sökpredikatorn med [sökfack](/help/assets/search-facets.md). The [!UICONTROL File Type] filtret i [!UICONTROL Filters] panelen har kryssrutor för blandat läge. Om du inte markerar alla kapslade predikat (eller format) markeras därför kryssrutorna på första nivån delvis.

[!DNL Experience Manager] sökfunktionen stöder sökning efter samlingar och sökning efter resurser i en samling. Se [söksamlingar](/help/assets/manage-collections.md).

## Förstå gränssnittet för resurssökning {#searchui}

Bekanta dig med gränssnittet för resurssökning och de tillgängliga åtgärderna.
<!--
![Understand Experience Manager Assets search results interface](assets/aem_search_results.png)
-->
![Förstå Experience Manager Assets sökresultatgränssnitt](assets/aem-search-interface.png)
*Bild: Förstå [!DNL Experience Manager Assets] sökresultatgränssnitt.*

**S.** Spara sökningen som en smart samling.
**B.** Filter eller predikat som begränsar sökresultaten.
**C.** Visa filer, mappar eller båda.
**D.** Sökplatsen är DAM.
**E.** Få åtkomst till sparade sökningar.
**F.** Klicka på Filter för att öppna eller stänga den vänstra listen.
**G.** Visar resurser som standardsökning.
**H.** Sökplatsen är DAM.
**Jag.** Omsökningsfält med användardefinierat söknyckelord.
**J.** Välj inlästa sökresultat.
**K.** Sortera efter Skapad, Ändrad, Namn, Ingen.
**L.** Sortera efter stigande eller fallande ordning.
**M.** Antal visade sökresultat av totalt antal sökresultat. **N.** Stäng sökningen.
**O.** Växla mellan kortvyn och listvyn.

### Dynamiska sökfaktorer {#dynamicfacets}

Du kan identifiera önskade resurser snabbare från sökresultatsidan med det dynamiskt uppdaterade antalet förväntade sökresultat i sökmetoderna. Det förväntade antalet resurser uppdateras även innan sökfiltret används. Genom att se det förväntade antalet mot filtret kan du snabbt och effektivt navigera bland sökresultaten.

![Se det ungefärliga antalet resurser utan att filtrera sökresultaten i sökfaktorer.](assets/asset_search_results_in_facets_filters.png)

*Bild: Se det ungefärliga antalet resurser utan att filtrera sökresultaten i sökfaktorer.*

Experience Manager Assets visar antalet fasetter för två egenskaper som standard:

* Resurstyp (jcr:content/metadata/dc:format)

* Godkännandestatus (jcr:content/metadata/dam:status)

Från och med augusti 2023 innehåller Experience Manager Assets en ny version 9 av `damAssetLucene` index. Tidigare versioner, `damAssetLucene-8` och nedan använder du `statistical` läge för att kontrollera åtkomstkontroll för ett urval av objekt för varje antal sökfaktorer.

`damAssetLucene-9` ändrar beteendet för Oak Query facet-inventering så att åtkomstkontrollen inte längre utvärderas för antalet facet som returneras av det underliggande sökindexet, vilket ger snabbare svarstider vid sökning. Detta kan leda till att användarna får se värden för antal ansikten, som innehåller resurser som de inte har tillgång till. Dessa användare kan inte komma åt, hämta eller läsa någon annan information om dessa resurser, inklusive sökvägar, eller få mer information om dem.

Om du behöver växla till föregående beteende (`statistical` läge), se [Innehållssökning och indexering](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/indexing.html) skapa en anpassad version av `damAssetLucene-9` index. Adobe rekommenderar inte att du byter till `secure` läge på grund av påverkan på svarstider vid sökning med stora resultatuppsättningar.

Mer information om Oaks ansiktsfunktioner, inklusive en detaljerad beskrivning av dessa lägen, finns i [den här artikeln](https://jackrabbit.apache.org/oak/docs/query/lucene.html#facets).

## Sök efter förslag medan du skriver {#searchsuggestions}

När du börjar skriva ett nyckelord föreslår Experience Manager möjliga söknyckelord eller fraser. Förslagen baseras på resurserna i Experience Manager. Experience Manager indexerar alla metadatafält som ska vara till hjälp vid sökning. Systemet använder värdena från följande metadatafält för att ge sökförslag. Om du vill ge sökförslag bör du överväga att fylla i följande fält med lämpliga nyckelord:

* Resurstaggar. (mappar till `jcr:content/metadata/cq:tags`)
* Resursrubrik. (mappar till `jcr:content/metadata/dc:title`)
* Resursbeskrivning. (mappar till `jcr:content/metadata/dc:description`)
* Titel i JCR-databasen. Värdet kan mappas till Resursrubrik. (mappar till `jcr:content/jcr:title`)
* Beskrivning i JCR-databasen. Värdet kan mappas till tillgångsbeskrivningen. (mappar till `jcr:content/jcr:description`)

## Förstå sökresultat och beteenden {#searchbehavior}

### Grundläggande söktermer och sökresultat {#searchbasics}

Du kan köra nyckelordssökningar från OmniSearch-fältet. Nyckelordssökningen är inte skiftlägeskänslig och är en fulltextsökning (i alla vanliga metadatafält). Om mer än ett nyckelord används, `AND` är standardoperatorn mellan nyckelorden.

Resultatet sorteras efter relevans, med början med närmast matchande. För flera nyckelord är mer relevanta resultat de resurser som innehåller båda termerna i sina metadata. I metadata rangordnas nyckelord som visas som smarta taggar högre än nyckelord som visas i andra metadatafält. [!DNL Experience Manager] ger en viss sökterm högre vikt. Det går även att [öka rankningen](#searchrank) av ett antal målinriktade resurser för specifika söktermer.

För att snabbt hitta relevanta resurser innehåller det avancerade gränssnittet funktioner för filtrering, sortering och markering. Du kan filtrera resultat baserat på flera villkor och se antalet sökningar efter olika filter. Du kan också köra sökningen igen genom att ändra frågan i fältet Omnissearch. När du ändrar söktermer eller filter används de andra filtren för att bevara sökkontexten.

När resultatet är många resurser [!DNL Experience Manager] visar de första 100 i kortvyn och 200 i listvyn. När användare rullar läses fler resurser in. Detta för att förbättra prestandan. Se en videodemonstration av [antal resurser som visas](https://www.youtube.com/watch?v=LcrGPDLDf4o).

Ibland kan du se oväntade resurser i sökresultaten. Mer information finns på [oväntade resultat](#unexpected-results).

[!DNL Experience Manager] kan söka i många filformat och sökfiltren kan anpassas efter dina behov. Kontakta administratören för att få veta vilka sökalternativ som är tillgängliga för DAM-databasen och vilka begränsningar ditt konto har.

<!-- 
### Results with and without enhanced Smart Tags {#withsmarttags}

By default, [!DNL Experience Manager] search combines the search terms with an AND clause. For example, consider searching for keywords woman running. Only the assets with both woman and running keywords in the metadata appear in the search results by default. The same behavior is retained when special characters (periods, underscores, or dashes) are used with the keywords. The following search queries return the same results:

* `woman running`
* `woman.running`
* `woman-running`

However, the query `woman -running` returns assets without `running` in their metadata.
Using Smart Tags adds an extra `OR` clause to find any of the search terms as the applied smart tags. An asset tagged with either `woman` or `running` using Smart Tags also appear in such a search query. So the search results are a combination of,

* Assets with `woman` and `running` keywords in the metadata (default behavior).

* Assets smart tagged with either of the keywords (Smart Tags behavior).
-->

### Sök efter rankning och förstärkning {#searchrank}

Sökresultaten som matchar alla söktermer i metadatafält visas först, följt av sökresultaten som matchar någon av söktermerna i de smarta taggarna. I ovanstående exempel är den ungefärliga visningsordningen för sökresultat:

1. Matchar med `woman running` i de olika metadatafälten.
1. Matchar med `woman running` i smarta taggar.
1. Matchar med `woman` eller `running` i smarta taggar.

Du kan förbättra nyckelordens relevans för vissa resurser för att öka sökningen baserat på nyckelorden. Det innebär att de bilder som du befordrar särskilda nyckelord för visas högst upp i sökresultatet när du söker baserat på dessa nyckelord.

1. Från [!DNL Assets] öppnar du egenskapssidan för resursen. Klicka **[!UICONTROL Advanced]** och klicka **[!UICONTROL Add]** under **[!UICONTROL Elevate for search keywords]**.
1. I **[!UICONTROL Search Promote]** anger du ett nyckelord som du vill göra sökningen efter bilden snabbare och klickar sedan på **[!UICONTROL Add]**. Du kan ange flera nyckelord på samma sätt.
1. Klicka på **[!UICONTROL Save & Close]**. Den resurs som du befordrade för det här nyckelordet visas bland de översta sökresultaten.

Du kan använda detta till din fördel genom att öka rankningen för vissa resurser i sökresultaten för nyckelordet target. Se exempelvideon nedan. Mer information finns på [sök i [!DNL Experience Manager]](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/search-and-discovery/search-boost.html).

>[!VIDEO](https://video.tv.adobe.com/v/16766/?quality=6)

*Video: Förstå hur sökresultaten rangordnas och hur rangordningen kan påverkas.*

## Konfigurera batchstorlek för resurs för att visa sökresultat {#configure-asset-batch-size}

Administratörer kan nu konfigurera batchstorleken för resurser som visas när du utför en sökning. Resurssökresultaten visas i multipler av det konfigurerade batchstorleksnumret när du rullar nedåt för att läsa in resultaten. Du kan välja mellan de tillgängliga gruppstorlekarna 200, 500 och 1 000 resurser. Om du anger ett lägre batchstorleksnummer blir sökningen snabbare.

Om du till exempel anger gränsen för antal resultat till en batchstorlek på 200 resurser, visas en batchstorlek på 200 resurser i sökresultaten när du börjar utföra sökningen i Experience Manager Assets. När du bläddrar nedåt för att navigera bland sökresultaten visas nästa grupp med 200 resurser. Processen fortsätter tills alla resurser som matchar sökfrågan visas.

Så här konfigurerar du batchstorleken för resursen:

1. Navigera till **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Assets Configurations]** > **[!UICONTROL Assets Omnisearch Configuration]**.

1. Markera gränsen för antal resultat och klicka på **[!UICONTROL Save]**.

   ![Konfiguration av batchstorlek för resurser](/help/release-notes/assets/assets-batch-size-configuration.png)

## Avancerad sökning {#scope}

[!DNL Experience Manager] I finns olika metoder, till exempel filter som används för de sökda resurserna, för att du snabbare ska kunna hitta de önskade resurserna. Nedan beskrivs några vanliga metoder. Några [exempel](#samples) delas nedan.

**Sök efter filer eller mappar**: I sökresultaten ska du läsa antingen filer, mappar eller både och. Från **[!UICONTROL Filters]** kan du välja rätt alternativ. Se [sökgränssnitt](#searchui).

**Söka efter resurser i en mapp**: Du kan begränsa sökningen till en viss mapp. I **[!UICONTROL Filters]** lägger du till en mappsökväg. Du kan bara markera en mapp i taget.

![Begränsa sökresultaten till en mapp genom att lägga till en mappsökväg i panelen Filter](assets/limiting-search.gif)
<!--
![Limit search results to a folder by adding a folder path in Filters panel](assets/search_folder_select.gif)
-->

*Bild: Begränsa sökresultaten till en mapp genom att lägga till en mappsökväg på panelen Filter.*

### Söka efter liknande bilder {#visualsearch}

Om du vill söka efter bilder som visuellt liknar en användarvald bild klickar du på alternativet **[!UICONTROL Find Similar]** i kortvyn för en bild eller i verktygsfältet. [!DNL Experience Manager] I visas smarta taggade bilder från DAM-databasen som liknar den bild som användaren har valt.

![Söka efter liknande bilder med hjälp av alternativet i kortvyn](assets/search_find_similar.png)

*Bild: Hitta liknande bilder med hjälp av alternativet i kortvyn.*

### Adobe Stock-bilder {#adobe-stock}

Från [!DNL Experience Manager] användargränssnitt, användare kan söka [Adobe Stock-resurser](/help/assets/aem-assets-adobe-stock.md) och licensiera de mediefiler som behövs. Lägg till `Location: Adobe Stock` i Omnissearch bar. Du kan också använda panelen Filter för att hitta alla licensierade eller olicensierade mediefiler eller söka efter en viss mediefil med hjälp av Adobe Stock filnummer.

### Dynamic Media-resurser {#dmassets}

Du kan filtrera efter dynamiska mediebilder genom att välja **[!UICONTROL Dynamic Media]** > **[!UICONTROL Sets]** på panelen **[!UICONTROL Filters]**. Den filtrerar och visar resurser som bilduppsättningar, karuseller, blandade medieuppsättningar och snurruppsättningar.

### GQL-sökning med specifika värden i metadatafält {#gql-search}

Du kan söka efter resurser baserat på exakta värden för metadatafält, som titel, beskrivning och skapare. Funktionen för fulltextsökning i GQL hämtar endast resurser vars metadatavärde exakt matchar din sökfråga. Namnen på egenskaperna (Skapare, Titel och så vidare) och värdena är skiftlägeskänsliga.

| Metadatafält | Fasettvärde och -användning |
|---|---|
| Titel | title:John |
| Skapare | skapare:John |
| Plats | plats:NA |
| Beskrivning | description:&quot;Sample Image&quot; |
| Skapare | creatortool:&quot;Adobe Photoshop&quot; |
| Copyright-ägare | copyrightowner:&quot;Adobe Systems&quot; |
| Medarbetare | medarbetare:John |
| Användningsvillkor | usageterms:&quot;CopyRights Reserved&quot; |
| Skapad | skapad:YYY-MM-DDTHH |
| Utgångsdatum | förfaller:ÅÅÅ-MM-DDTHH |
| I tid | ontime:YYY-MM-DDTHH |
| Fråntid | offtime:YYY-MM-DDTHH |
| Tidsintervall (förfaller dateontime, offtime) | facet field : lowerbound..upperbound |
| Bana | /content/dam/&lt;folder name=&quot;&quot;> |
| PDF | pdftitle:&quot;Adobe-dokument&quot; |
| Ämne | ämne: Utbildning |
| Taggar | taggar:&quot;Plats och resa&quot; |
| Typ | type:&quot;image\png&quot; |
| Bildens bredd | width:lowerbound..upperbound |
| Bildens höjd | height:lowerbound..upperbound |
| Person | person:John |

Egenskaperna `path`, `limit`, `size`och `orderby` kan inte kombineras med `OR` -operatorn med någon annan egenskap.

<!-- TBD: Where are the limit, size, orderby properties defined?
-->

Nyckelordet för en användargenererad egenskap är dess fältetikett i egenskapsredigeraren i gemener, med borttagna blanksteg.

Här är några exempel på sökformat för komplexa frågor:

* Så här visar du alla resurser med flera facets-fält (till exempel: title=John Doe och creator-verktyget = Adobe Photoshop): `title:"John Doe" creatortool:Adobe*`
* Så här visar du alla resurser när ansiktsvärdet inte är ett enda ord utan en mening (till exempel: title=Scott Reynolds): `title:"Scott Reynolds"`
* Så här visar du resurser med flera värden för en enda egenskap (till exempel: title=Scott Reynolds eller John Doe): `title:"Scott Reynolds" OR "John Doe"`
* Så här visar du resurser med egenskapsvärden som börjar med en viss sträng (till exempel: titeln är Scott Reynolds): `title:Scott*`
* Så här visar du resurser med egenskapsvärden som slutar med en viss sträng (till exempel: title är Scott Reynolds): `title:*Reynolds`
* Så här visar du resurser med ett egenskapsvärde som innehåller en specifik sträng (till exempel: title = Basel Meeting Room): `title:*Meeting*`
* Så här visar du resurser som innehåller en viss sträng och har ett specifikt egenskapsvärde (till exempel: sök efter strängen Adobe i resurser som har title=John Doe): `*Adobe* title:"John Doe"`

## Söka efter resurser från andra [!DNL Experience Manager] erbjudanden eller gränssnitt {#search-assets-other-surfaces}

[!DNL Adobe Experience Manager] kopplar DAM-databasen till andra [!DNL Experience Manager] lösningar som ger snabbare tillgång till digitalt material och effektiviserar de kreativa arbetsflödena. Alla resursidentifieringar börjar med bläddring eller sökning. Sökfunktionen är i stort sett densamma på alla olika ytor och lösningar. Vissa sökmetoder ändras när målgruppen, användningsexemplen och användargränssnittet varierar mellan olika målgrupper [!DNL Experience Manager] lösningar. De specifika metoderna beskrivs för de enskilda lösningarna på länkarna nedan. De universellt tillämpliga tipsen och beteendena beskrivs i den här artikeln.

### Söka efter resurser från panelen Resurslänk i Adobe {#aal}

Med Adobe Asset Link kan formgivarna nu komma åt material som lagrats i [!DNL Experience Manager Assets]utan att lämna de Adobe Creative Cloud-program som stöds. Med hjälp av panelen i appen på panelen kan du smidigt söka efter, checka ut och checka in resurser [!DNL Adobe Creative Cloud] appar: [!DNL Adobe Photoshop], [!DNL Adobe Illustrator]och [!DNL Adobe InDesign]. Med Asset Link kan du också söka visuellt liknande resultat. Visuella sökresultat bygger på Adobe Sensei maskininlärningsalgoritmer och hjälper användarna att hitta estetiskt liknande bilder. Se [söka efter och bläddra bland resurser](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html#UseAdobeAssetLink) med Adobe Asset Link.

### Sök efter resurser i [!DNL Experience Manager] datorprogram {#desktop-app}

Kreatörer använder datorprogrammet för att skapa [!DNL Experience Manager Assets] enkelt sökbara och tillgängliga lokalt (Win eller Mac). Creative Cloud kan enkelt visa de önskade resurserna i Mac Finder eller Utforskaren i Windows, som öppnats i skrivbordsprogram och ändrats lokalt - ändringarna sparas sedan i [!DNL Experience Manager] med en ny version som skapats i databasen. Programmet stöder enkla sökningar med ett eller flera nyckelord, `*` och `?` jokertecken, och `AND` -operator. Se [bläddra bland, söka efter och förhandsgranska resurser](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#browse-search-preview-assets) i datorprogrammet.

### Sök efter resurser i [!DNL Brand Portal] {#brand-portal}

Affärsanvändare och marknadsförare använder Brand Portal för att effektivt och säkert dela godkända digitala resurser med interna team, partners och återförsäljare. Se [sökresurser på Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/search-capabilities/brand-portal-searching.html).

### Sök [!DNL Adobe Stock] bilder {#adobe-stock1}

Från [!DNL Experience Manager] -användargränssnittet kan användare söka efter Adobe Stock-resurser och licensiera de nödvändiga resurserna. Lägg till `Location: Adobe Stock` i Omnissearch-fältet. Du kan också använda **[!UICONTROL Filters]** för att hitta alla licensierade eller olicensierade mediefiler eller söka efter en viss mediefil med hjälp av Adobe Stock filnummer. Se [hantera [!DNL Adobe Stock] bilder i [!DNL Experience Manager]](/help/assets/aem-assets-adobe-stock.md#usemanage).

### Sök [!DNL Dynamic Media] resurser {#search-dynamic-media-assets}

Du kan filtrera efter dynamiska mediebilder genom att välja **[!UICONTROL Dynamic Media]** > **[!UICONTROL Sets]** på panelen **[!UICONTROL Filters]**. Den filtrerar och visar resurser som bilduppsättningar, karuseller, blandade medieuppsättningar och rotationsuppsättningar. När författarna redigerar webbsidor kan de söka efter uppsättningar inifrån Content Finder. Det finns ett filter för uppsättningar på en snabbmeny.

### Söka efter resurser i Content Finder vid redigering av webbsidor {#content-finder}

Författare kan använda Content Finder för att söka i DAM-databasen efter relevanta resurser och använda resurserna på de webbsidor de skapar. Författare kan också använda funktionen Anslutna resurser för att söka efter resurser som är tillgängliga på en fjärrdator [!DNL Experience Manager] distribution. Författare kan sedan använda dessa resurser på webbsidor på en lokal [!DNL Experience Manager] distribution. Se [använda fjärrresurser](/help/assets/use-assets-across-connected-assets-instances.md#use-remote-assets).

### Sök i samlingar {#collections}

[!DNL Experience Manager] sökfunktionen stöder sökning efter samlingar och sökning efter resurser i en samling. Se [söksamlingar](/help/assets/manage-collections.md).

## Resursväljare {#asset-picker}

Resursväljare (kallas tillgångsväljare i tidigare versioner av [!DNL Adobe Experience Manager]) kan du söka efter, filtrera och bläddra bland DAM-resurser på ett speciellt sätt. Resursväljaren finns på `https://[aem_server]:[port]/aem/assetpicker.html`. Du kan hämta metadata för resurser som du väljer med resursväljaren. Du kan starta det med begärandeparametrar som stöds, till exempel resurstyp (bild, video, text) och markeringsläge (enstaka eller flera markeringar). De här parametrarna anger kontexten för resursväljaren för en viss sökinstans och förblir intakta genom hela markeringen.

Resursväljaren använder HTML 5 `Window.postMessage` meddelande som skickar data för den valda resursen till mottagaren. Det fungerar bara i bläddringsläget och endast med omsökningsresultatsidan.

Skicka följande frågeparametrar i en URL för att starta resursväljaren i en viss kontext:

| Namn | Värden | Exempel | Syfte |
|---|---|---|---|
| resurssuffix (B) | Mappsökväg som resurssuffix i URL: [https://localhost:4502/aem/assetpicker.html/&lt;folder_path>](https://localhost:4502/aem/assetpicker.html) | Så här startar du resursväljaren med en viss mapp markerad, till exempel med mappen `/content/dam/we-retail/en/activities` markerat ska URL:en ha följande format: `https://localhost:4502/aem/assetpicker.html/content/dam/we-retail/en/activities?assettype=images` | Om du vill att en viss mapp ska väljas när resursväljaren startas, skickar du den som ett resurssuffix. |
| `mode` | en, flera | <ul><li>`https://localhost:4502/aem/assetpicker.html?mode=single`</li><li>`https://localhost:4502/aem/assetpicker.html?mode=multiple`</li></ul> | I flera lägen kan du markera flera resurser samtidigt med resursväljaren. |
| `dialog` | true, false | [https://localhost:4502/aem/assetpicker.html?dialog=true](https://localhost:4502/aem/assetpicker.html?dialog=true) | Använd de här parametrarna för att öppna resursväljaren som Granite-dialogrutan. Det här alternativet kan bara användas när du startar resursväljaren via fältet Bevilja sökväg och konfigurerar den som URL för pickerSrc. |
| `root` | &lt;folder_path> | `https://localhost:4502/aem/assetpicker.html?assettype=images&root=/content/dam/we-retail/en/activities` | Använd det här alternativet om du vill ange rotmappen för resursväljaren. I det här fallet kan du bara välja underordnade resurser (direkt/indirekt) under rotmappen med resursväljaren. |
| `viewmode` | sök | | Så här startar du resursväljaren i sökningsläge, med `assettype` och `mimetype` parametrar. |
| `assettype` | Bilder, dokument, multimedia, arkiv. | <ul><li>`https://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=images`</li><li> `https://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=documents` </li><li> `https://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=multimedia` </li><li> `https://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=archives` </li></ul> | Använd alternativet för att filtrera resurstyper baserat på angivet värde. |
| `mimetype` | MIME-typ (`/jcr:content/metadata/dc:format`) av en resurs (jokertecken stöds också). | <ul><li>`https://localhost:4502/aem/assetpicker.html?mimetype=image/png`</li><li>`https://localhost:4502/aem/assetpicker.html?mimetype=*png`</li><li>`https://localhost:4502/aem/assetpicker.html?mimetype=*presentation`</li><li>`https://localhost:4502/aem/assetpicker.html?mimetype=*presentation&mimetype=*png`</li></ul> | Använd det för att filtrera resurser baserat på MIME-typ. |

Om du vill komma åt resursväljargränssnittet går du till `https://[aem_server]:[port]/aem/assetpicker`. Navigera till önskad mapp och markera en eller flera resurser. Du kan också söka efter den önskade resursen i rutan Sök, tillämpa det filter som behövs och sedan markera den.

![Bläddra och markera resurs i resursväljaren](assets/select-asset.png)

<!--![Browse and select asset in the asset selector](assets/assetpicker.png)-->

*Bild: Bläddra och markera resurs i resursväljaren.*

## Begränsningar {#limitations}

Sökfunktionen i [!DNL Experience Manager Assets] har följande begränsningar:

* Ange inget radavståndsutrymme i sökfrågan, annars fungerar inte sökningen.
* [!DNL Experience Manager] kan fortsätta att visa söktermen efter att du har valt egenskaper för en resurs bland sökresultaten och sedan avbryta sökningen. <!-- (CQ-4273540) -->
* När du söker efter mappar, filer och mappar kan sökresultaten inte sorteras efter någon parameter.
* Om du väljer `Return` utan att skriva i Omnisearch-fältet, [!DNL Experience Manager] returnerar en lista med endast filer och inte mappar. Om du söker efter mappar utan att använda ett nyckelord [!DNL Experience Manager] returnerar inga resultat.
* Du kan utföra fulltextsökning på mappar. Ange ett sökord som sökningen ska fungera med.

Visuell sökning eller likhetssökning har följande begränsningar:

* Visuell sökning fungerar bäst med en stor databas. Även om det inte finns något minsta antal bilder som krävs för bra resultat är kvaliteten på matchningar med ett fåtal bilder inte lika bra som matchningar från en stor databas.
* Du kan inte ändra modell eller tåg [!DNL Experience Manager] för att hitta liknande bilder. Modellen ändras inte om du till exempel lägger till eller tar bort smarta taggar för ett fåtal resurser. Resurserna tas inte med i de visuellt liknande sökresultaten.

Sökfunktionen kan ha prestandabegränsningar i följande scenarier:

* Kortvyn har en snabbare inläsningstid jämfört med listvyn för att visa sökresultaten.

## Söktips {#tips}

* När du övervakar granskningsstatusen för resurser ska du använda lämpligt alternativ för att hitta vilka resurser som är godkända eller vilka resurser som väntar på godkännande.
* Använd Insights-predikatet för att söka efter resurser som stöds baserat på användningsstatistik från olika Creative-program. Användningsdata grupperas under Användningspoäng, Impressions, Clicks och Media-kanaler där resurserna visas i kategorier.
* Använd **[!UICONTROL Select All]** om du vill välja de sökbara resurserna. [!DNL Experience Manager] visar först 100 resurser i kortvyn och 200 resurser i listvyn. Fler resurser läses in när du bläddrar i sökresultaten. Du kan välja fler resurser än de inlästa resurserna. Antalet markerade resurser visas i det övre högra hörnet på sökresultatsidan. Du kan arbeta med markeringen, till exempel hämta de markerade resurserna, uppdatera metadataegenskaperna i grupp för de markerade resurserna eller lägga till de markerade resurserna i en samling. När fler resurser är markerade än vad som visas tillämpas en åtgärd antingen på alla markerade resurser eller så visas antalet resurser som åtgärden används på i en dialogruta. Om du vill använda en åtgärd på de resurser som inte lästes in kontrollerar du att alla resurser är uttryckligen markerade.
* Om du vill söka efter resurser som inte innehåller obligatoriska metadata går du till [obligatoriska metadata](#mandatorymetadata).
* Alla metadatafält används för sökningen. En allmän sökning, som att söka efter 12, ger vanligtvis många resultat. Du får bättre resultat om du använder dubbla (inte enkla) citattecken eller ser till att talet ligger intill ett ord utan specialtecken (till exempel `shoe12`).
* Fulltextsökning stöder operatorer som `-` och `^`. Om du vill söka efter de här bokstäverna som stränglitteraler omger du sökuttrycket med citattecken. Använd till exempel `"Notebook - Beauty"` i stället för `Notebook - Beauty`.
* Om sökresultaten är för många bör du begränsa [sökområde](#scope) till noll-i för de önskade resurserna. Det fungerar bäst om du har en aning om hur du ska söka efter de önskade resurserna, till exempel en viss filtyp, en viss plats, specifika metadata och så vidare.

* **Taggning**: Taggar hjälper dig att kategorisera resurser som kan bläddras och sökas effektivare. Taggning hjälper till att sprida rätt taxonomi till andra användare och arbetsflöden. [!DNL Experience Manager] erbjuder metoder för att automatiskt tagga resurser med hjälp av Adobe Sensei artificiellt intelligenta tjänster som hela tiden blir bättre på att tagga materialet med användning och utbildning. När du söker efter resurser är de smarta taggarna inkapslade. Det fungerar tillsammans med de inbyggda sökfunktionerna. Se [sökbeteende](#searchbehavior). Om du vill optimera den ordning i vilken sökresultaten visas kan du [öka rankningen](#searchrank) av några utvalda resurser.

* **Indexering**: Endast indexerade metadata och resurser returneras i sökresultatet. För bättre täckning och prestanda bör du se till att indexeringen är korrekt och följa bästa praxis. Se [indexering](#searchindex).

## Några exempel som illustrerar sökning {#samples}

Använd citattecken runt nyckelord för att hitta resurser som innehåller den exakta frasen i exakt den ordning som anges av användaren.

![Sökbeteende med och utan citattecken](assets/search_with_quotes.gif)

*Bild: Sökbeteende med och utan citattecken.*

**Sök med asterisk som jokertecken**: Om du vill bredda sökningen använder du en asterisk före eller efter sökordet för att matcha ett valfritt antal tecken. Om du till exempel söker efter en körning utan asterisk returneras inga resurser som innehåller någon variant av ordet (inklusive i metadata). En asterisk ersätter ett valfritt antal tecken. Exempel:

* `run` returnerar resurser med nyckelordet exakt run
* `run*` returnerar resurser med `running`, `run`, `runaway`och så vidare.
* `*run` returnerar resurser med `outrun`, `rerun`och så vidare.
* `*run*` returnerar alla möjliga kombinationer.

![Illustration use asterisk wildcard in asset search using a example](assets/search_with_asterisk_run.gif)

*Bild: Illustration use of asterisk wildcard in Asset search using an example.*

**Söka med frågetecken - jokertecken**: Om du vill bredda sökningen använder du en eller flera ? tecken som matchar det exakta antalet tecken. I följande bild:

* `run???` frågan matchar inte någon resurs.

* `run????` frågan matchar ordet `running` med fyra tecken efter `run`.

* `??run` frågan matchar ordet `rerun` med två tecken före `run`.

![Illustration use of question mark wildcard in Asset search using a example](assets/search_with_questionmark_run.gif)

*Bild: Illustration av användningen av frågetecknet jokertecken i resurssökning med hjälp av ett exempel.*

**Uteslut ett nyckelord**: Använd streck för att söka efter resurser som inte innehåller något nyckelord. Till exempel: `running -shoe` frågan returnerar resurser som innehåller `running`, men inte `shoe`. På samma sätt `camp -night` frågan returnerar resurser som innehåller `camp` men inte `night`. Frågan `camp-night` returnerar resurser som innehåller båda `camp` och `night`.

![Användning av bindestreck för att söka efter resurser som inte innehåller ett exkluderat nyckelord](assets/search_dash_exclude_keyword.gif)

*Bild: Användning av bindestreck för att söka efter resurser som inte innehåller ett exkluderat nyckelord.*

<!--
## Configuration and administration tasks related to search functionality {#configadmin}

### Search index configurations {#searchindex}

Asset discovery relies on indexing of DAM contents, including the metadata. Faster and accurate asset discovery relies on optimized indexing and appropriate configurations. See [indexing](/help/operations/indexing.md).
-->

<!--
### Visual or similarity search {#configvisualsearch}

Visual search uses Smart Tags. After configuring smart tagging functionality, follow these steps.

1. In [!DNL Experience Manager] CRXDE, in `/oak:index/lucene` node, add the following properties and values and save the changes.

    * `costPerEntry` property of type `Double` with the value `10`.

    * `costPerExecution` property of type `Double` with the value `2`.

    * `refresh` property of type `Boolean` with the value `true`.

   This configuration allows searches from the appropriate index.

1. To create Lucene index, in CRXDE, at `/oak:index/damAssetLucene/indexRules/dam:Asset/properties`, create node named `imageFeatures` of type `nt-unstructured`. In `imageFeatures` node,

    * Add `name` property of type `String` with the value `jcr:content/metadata/imageFeatures/haystack0`.

    * Add `nodeScopeIndex` property of type `Boolean` with the value of `true`.

    * Add `propertyIndex` property of type `Boolean` with the value of `true`.

    * Add `useInSimilarity` property of type `Boolean` with the value `true`.

   Save the changes.

1. Access `/oak:index/damAssetLucene/indexRules/dam:Asset/properties/predictedTags` and add `similarityTags` property of type `Boolean` with the value of `true`.
1. Apply Smart Tags to the assets in your [!DNL Experience Manager] repository. See [how to configure smart tags](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/configuring/tagging.html#configuring).
1. In CRXDE, in `/oak-index/damAssetLucene` node, set the `reindex` property to `true`. Save the changes.
1. (Optional) If you have customized search form then copy the `/libs/settings/dam/search/facets/assets/jcr%3Acontent/items/similaritysearch` node to `/conf/global/settings/dam/search/facets/assets/jcr:content/items`. Save the changes.

For related information, see [understand smart tags in Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/metadata/image-smart-tags.html) and [how to manage smart tags](/help/assets/smart-tags.md).
-->

<!--
### Mandatory metadata {#mandatorymetadata}

Business users, administrators, or DAM librarians can define some metadata as mandatory metadata that is a must for the business processes to work. For various reasons, some assets may be missing this metadata, such as legacy assets or assets migrated in bulk. Assets with missing or invalid metadata are detected and reported based on the indexed metadata property. To configure it, see [mandatory metadata](/help/assets/metadata-schemas.md#defining-mandatory-metadata).

### Modify search facets {#searchfacets}

To improve the speed of discovery, [!DNL Experience Manager Assets] offers search facets using which you can filter the search results. The Filters panel includes a few standard facets by default. Administrators can customize the Filters panel to modify the default facets using the in-built predicates. [!DNL Experience Manager] provides a good collection of in-built predicates and an editor to customize the facets. See [search facets](/help/assets/search-facets.md).

### Extract text when uploading assets {#extracttextupload}

You can configure [!DNL Experience Manager] to extract the text from the assets when users upload assets, such as PSD or PDF files. [!DNL Experience Manager] indexes the extracted text and helps users search these assets based on the extracted text. See [upload assets](/help/assets/manage-digital-assets.md#uploading-assets).
-->

### Anpassade predikat för att filtrera sökresultat {#custompredicates}

Predikat används för att skapa ansikten. Administratörer kan anpassa sökmetoderna på panelen Filter med förkonfigurerade predikat. Dessa predikat kan anpassas med hjälp av övertäckningar. Se [skapa anpassade predikat](/help/assets/search-facets.md).

Du kan söka efter digitala resurser baserat på en eller flera av följande egenskaper. Filter som gäller för vissa av dessa egenskaper är som standard tillgängliga och vissa andra filter kan skapas för att användas på andra egenskaper.

| Sökfält | Sök egenskapsvärden |
|-----------------|----------------------------------------------------------------------------------------------------------------------------------------|
| MIME-typer | Bilder, Dokument, Multimedia, Arkiv eller Annat. |
| Senast ändrad | Timme, dag, vecka, månad eller år. |
| Filstorlek | Liten, Medel eller Stor. |
| Publiceringsstatus | Publicerad eller opublicerad. |
| Godkänd status | Godkänd eller Avvisad. |
| Orientering | Vågrät, Lodrät eller Fyrkant. |
| Stil | Färg eller Svartvitt. |
| Videohöjd | Anges som lägsta och högsta värde. Värdet lagras endast i metadata för videoåtergivningar. |
| Videobredd | Anges som lägsta och högsta värde. Värdet lagras endast i metadata för videoåtergivningar. |
| Videoformat | DVI, Flash, MPEG4, MPEG, OGG Theora, QuickTime, Windows Media. Värdet lagras i källvideons metadata och eventuella återgivningar. |
| Videokodek | x264. Värdet lagras endast i metadata för videoåtergivningar. |
| Videobithastighet | Anges som lägsta och högsta värde. Värdet lagras endast i metadata för videoåtergivningar. |
| Ljudkodek | Libvorbis, Lame MP3, AAC-kodning. Värdet lagras endast i metadata för videoåtergivningar. |
| Bithastighet för ljud | Anges som lägsta och högsta värde. Värdet lagras endast i metadata för videoåtergivningar. |

## Arbeta med resurssökningsresultat {#aftersearch}

Du kan göra följande med de resurser du har sökt i [!DNL Experience Manager]:

* Visa metadataegenskaper och annan information.
* Hämta en eller flera resurser.
* Använd Skrivbordsåtgärder för att öppna resurserna i skrivbordsappen.
* Skapa smarta samlingar.
* Skapa en version
* Starta ett arbetsflöde
* Relatera eller inte relatera tillgångar
* Använd filter på panelen Filter som visas automatiskt när du har gjort sökningen för att begränsa sökresultaten.
* Navigera till resursplatsen

### Sortera sökresultat {#sort}

Sortera sökresultaten för att hitta de resurser som behövs snabbare. Du kan sortera sökresultaten i listvyn och endast när du väljer **[[!UICONTROL Files]](#searchui)** från **[!UICONTROL Filters]** -panelen. [!DNL Assets] använder sortering på serversidan för att snabbt sortera alla resurser (oavsett hur många) i en mapp eller resultaten av en sökfråga. Sortering på serversidan ger snabbare och exaktare resultat än sortering på klientsidan.

I listvyn kan du sortera sökresultaten på samma sätt som du kan sortera resurser i valfri mapp. Sortering fungerar för de här kolumnerna - Namn, Titel, Status, Dimensioner, Storlek, Klassificering, Användning, Skapat (Datum), Ändrat (Datum), Publicerat (Datum), Arbetsflöde och Utcheckat.

Information om begränsningar för sorteringsfunktioner finns i [begränsningar](#limitations).

### Kontrollera detaljerad information om en resurs {#checkinfo}

Du kan kontrollera detaljerad information om en sökresurs från sökresultatsidan.

Om du vill visa alla metadata för en resurs markerar du resursen och klickar på **[!UICONTROL properties]** i verktygsfältet.

Om du vill kontrollera kommentarerna för en resurs eller versionshistoriken för en resurs klickar du på resursen för att öppna en stor förhandsvisning. Öppna tidslinjen i den vänstra rutan och välj **[!UICONTROL Comments]** eller **[!UICONTROL Versions]**. Du kan också sortera tidslinjeaktiviteter, som kommentarer eller versioner, i kronologisk ordning.

![Sortera tidslinjeposter för en sökresurs](assets/sort_timeline_search_results.gif)

*Bild: Sortera tidslinjeposter för en sökresurs.*

### Hämta sökbara resurser {#download}

Du kan hämta de sökda resurserna och deras återgivningar på samma sätt som du hämtar vanliga resurser från mappar. Välj en eller flera resurser från sökresultaten och klicka på **[!UICONTROL Download]** i verktygsfältet.

### Uppdatera metadataegenskaper gruppvis {#metadata-updates}

Det går att göra satsvisa uppdateringar av de gemensamma metadatafälten för flera resurser. Välj en eller flera resurser från sökresultaten. Klicka **[!UICONTROL Properties]** i verktygsfältet och uppdatera metadata efter behov. Klicka **[!UICONTROL Save and Close]** när det är klart. De befintliga metadata i de uppdaterade fälten skrivs över.

För resurser som är tillgängliga i en enda mapp eller samling är det enklare att [uppdatera flera metadata samtidigt](/help/assets/manage-metadata.md#manage-assets-metadata) utan att använda sökfunktionen. För resurser som är tillgängliga i olika mappar eller matchar ett gemensamt villkor är det snabbare att uppdatera metadata i grupp via sökning.

### Smarta samlingar {#smart-collections}

En samling är en ordnad uppsättning resurser som kan innehålla resurser från olika platser, eftersom samlingar bara innehåller referenser till dessa resurser. Samlingar är av följande två typer:

* En statisk referenslista med resurser, mappar och andra samlingar.
* En dynamisk lista (smart samling) som fyller i resurser i samlingen baserat på sökvillkor.

Du kan skapa smarta samlingar baserat på sökvillkoren. På panelen **[!UICONTROL Filters]** väljer du **[!UICONTROL Files]** och klickar på **[!UICONTROL Save Smart Collection]**. Läs mer i [Hantera samlingar](/help/assets/manage-collections.md).

### Skapa en version {#create-version}

Skapa en version för resurserna som visas i sökresultaten. Markera resursen och klicka på **[!UICONTROL Create]** > **[!UICONTROL Version]**. Lägg till en valfri etikett eller kommentar och klicka på **[!UICONTROL Create]**. Du kan också välja flera resurser och skapa versioner för dem samtidigt.

### Skapa ett arbetsflöde {#create-workflow}

På samma sätt som när du skapar en version kan du också skapa ett arbetsflöde för resurserna som visas i sökresultaten. Markera resurserna och klicka på **[!UICONTROL Create]** > **[!UICONTROL Workflow]**. Välj arbetsflödesmodell, ange en rubrik för arbetsflödet och klicka på **[!UICONTROL Start]**.

### Relatera och inte relatera tillgångar {#relate-unrelate-assets}

Relatera och dela upp resurser som visas i sökresultaten. Markera resurserna och klicka på **[!UICONTROL Relate]** eller **[!UICONTROL Unrelate]**.

### Navigera till resursmappens plats {#navigate-asset-folder-location}

Navigera till mapplatsen för resurser som visas i sökresultaten. Markera resursen och klicka på **[!UICONTROL Show File Location]**.

## Oväntade sökresultat och problem {#unexpected-results}

<!--
**Partially related or unrelated search results**: Experience Manager may display seemingly partially related or unrelated assets, alongside the desired assets in the search results. If you enable Enhanced Smart Tags, the search behavior changes slightly. See how it changes [after smart tagging](#withsmarttags).
-->

| Fel, problem, symtom | Möjlig orsak | Möjlig korrigering eller förståelse för problemet |
|---|---|---|
| Felaktiga resultat vid sökning efter resurser som saknar metadata. | När du söker efter resurser som saknar obligatoriska metadata, [!DNL Experience Manager] kan visa vissa resurser som har giltiga metadata. Resultatet baseras på indexerad metadataegenskap. | När metadata har uppdaterats krävs omindexering för att resursens metadata ska visas korrekt. Se [obligatoriska metadata](metadata-schemas.md#define-mandatory-metadata). |
| För många sökresultat. | En stor sökparameter. | Begränsa [sökområde](#scope). Smarta taggar kan ge fler sökresultat än du förväntade dig. Se [sökbeteende med smarta taggar](#withsmarttags). |
| Orelaterade eller delvis relaterade sökresultat. | Sökbeteendet ändras med smart taggning. | Förstå [hur sökningen ändras efter smart taggning](#withsmarttags). |
| Inga förslag för resurser som fylls i automatiskt. | Nyligen överförda resurser har ännu inte indexerats. Metadata är inte omedelbart tillgängliga som förslag när du börjar skriva ett söknyckelord i omsökningsfältet. | [!DNL Experience Manager] Väntar till utgången av en timeout-period (en timme som standard) innan ett bakgrundsjobb körs för att indexera metadata för alla nyligen överförda eller uppdaterade resurser och lägger sedan till metadata i listan med förslag. |
| Inga sökresultat. | <ul><li>Resurser som matchar din fråga finns inte. </li><li> Blanksteg har lagts till före sökfrågan. </li><li> Det metadatafält som inte stöds innehåller nyckelordet som du sökte efter.</li><li> Sökningar som görs när en resurs är ledig. </li></ul> | <ul><li>Sök med ett annat nyckelord. Du kan också använda smart taggning eller likhetssökning för att förbättra sökresultaten. </li><li>[Känd begränsning](#limitations).</li><li>Alla metadatafält används inte för sökningar. Se [omfång](#scope).</li><li>Sök senare eller ändra i tid och offline för att hitta de resurser som behövs.</li></ul> |
| Sökfilter eller predikat är inte tillgängligt. | <ul><li>Sökfiltret är inte konfigurerat.</li><li>Den är inte tillgänglig för din inloggning.</li><li>(Sannolikheten är mindre) Sökalternativen är inte anpassade efter den distribution du använder.</li></ul> | <ul><li>Kontakta administratören för att kontrollera om sökanpassningarna är tillgängliga eller inte.</li><li>Kontakta administratören för att kontrollera om ditt konto har behörighet att använda anpassningen.</li><li>Kontakta administratören och kontrollera tillgängliga anpassningar för [!DNL Assets] distribution du använder.</li></ul> |
| När du söker efter visuellt liknande bilder saknas en förväntad bild. | <ul><li>Bilden är inte tillgänglig i [!DNL Experience Manager].</li><li>Bilden är inte indexerad. Vanligtvis när den nyligen har överförts.</li><li>Bilden är inte smart taggad.</li></ul> | <ul><li>Lägg till bilden i [!DNL Assets].</li><li>Kontakta administratören om du vill indexera om databasen. Se även till att du använder rätt index.</li><li>Kontakta administratören om du vill tagga de relevanta resurserna på ett smart sätt.</li></ul> |
| När du söker efter visuellt liknande bilder visas en irrelevant bild. | Visuell sökfunktion. | [!DNL Experience Manager] visar så många potentiellt relevanta tillgångar som möjligt. Mindre relevanta bilder, om sådana finns, läggs till i resultatet men med en lägre sökrankning. Kvaliteten på matchningarna och relevansen hos de sökda resurserna minskar när du bläddrar nedåt i sökresultaten. |
| När du väljer och arbetar med sökresultat utförs inte alla sökbara resurser. | The [!UICONTROL Select All] väljer bara de första 100 sökresultaten i kortvyn och de första 200 sökresultaten i listvyn. | |

**Se även**

* [Sök efter bästa praxis](search-best-practices.md)
* [Översätt resurser](translate-assets.md)
* [Resurser för HTTP API](mac-api-assets.md)
* [Resurser som stöds i filformat](file-format-support.md)
* [Anslutna resurser](use-assets-across-connected-assets-instances.md)
* [Resursrapporter](asset-reports.md)
* [Metadata-scheman](metadata-schemas.md)
* [Hämta resurser](download-assets-from-aem.md)
* [Hantera metadata](manage-metadata.md)
* [Sök efter ansikten](search-facets.md)
* [Hantera samlingar](manage-collections.md)
* [Import av massmetadata](metadata-import-export.md)
* [Publicera resurser till AEM och Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] guide för sökimplementering](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/developing/search-tutorial-develop.html)
>* [Avancerad konfiguration som förbättrar sökresultaten](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/search-and-discovery/search-boost.html)
>* [Konfigurera smart översättningssökning](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/translation/smart-translation-search-technical-video-setup.html)

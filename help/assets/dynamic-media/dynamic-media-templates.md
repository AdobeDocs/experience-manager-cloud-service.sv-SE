---
title: Hur hanterar jag dynamiska mediamallar?
description: Lär dig hur du skapar dynamiska mediamallar med hjälp av en WYSIWYG mallredigerare och hur du inkluderar flera bilder och textlager för att snabbt skapa banners och flygblad och använda dem i program längre fram i kedjan.
hide: true
role: User
exl-id: 07de648e-4ae2-4524-8e05-3cf10bb6006d
source-git-commit: 2fcbcaf5fe4794d8ea52386583dc592c0c1983d5
workflow-type: tm+mt
source-wordcount: '2696'
ht-degree: 0%

---

# Dynamiska mediamallar{#dynamic-media-templates}

| [Sök efter bästa praxis](/help/assets/search-best-practices.md) | [Metadata - bästa praxis](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [AEM Assets-dokumentation för utvecklare](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|-----|

Skapa dynamiska mediamallar med en WYSIWYG malleditor och lägg in flera bilder och textlager för att snabbt skapa banners och flygblad och använda dem i program längre fram i kedjan. Du kan också lägga till parametrar till de bilder och textlager som ingår i mallen och använda [dynamiska medie-URL:er](https://experienceleague.adobe.com/en/docs/commerce-admin/content-design/wysiwyg/storage/catalog-urls-dynamic-media) för att uppdatera värdena för dessa lager i realtid.

Några av de viktigaste funktionerna:

* **Dynamic Media WYSIWYG Template Editor:** Skapa anpassningsbara banners med bild- och textlager.
* **Lagerparameterisering:** Definiera dynamiska nyckelvärdepar för lager för att aktivera realtidsuppdateringar.
* **Stöd för dynamiska medie-URL:er:** Använd dynamiska medie-URL:er för mallar och integrera personaliserade värden från första eller tredje parts program.
* **Kontroll av lagersynlighet:** Dölj eller visa lager dynamiskt efter behov.
* **Smart storleksändring av text:** Justera automatiskt textstorleken så att den passar de angivna områdena.

Några av fördelarna med Dynamic Media-mallar:

* **Optimera 1:1 Personalization:** Anpassa innehåll efter kundsignaler i realtid.
* **Minska den manuella ansträngningen:** Automatisera och snabba upp skapandet och hanteringen av innehåll.
* **Säkerställ enhetliga flerkanalsupplevelser:** Bevara varumärkets enhetlighet över alla kanaler.
* **Återanvänd innehåll effektivt:** Undvik engångsinnehåll och skalning med dynamiska, parametriserade mallar.
* **Minska riskerna:** Uppdatera priser, rabatter och länkar i realtid.
* **Förbättra kundengagemanget:** Skapa interaktiva, sammanhangsberoende upplevelser.

>[!NOTE]
>
>Kunder som prenumererar på Enhanced Security SKU kan inte använda några Dynamic Media-funktioner, inklusive Dynamic Media Templates, i det Cloud Services-programmet.

## Innan du börjar{#prerequisites-for-dynamic-media-wysiwyg-template}

Om du vill skapa en mall för dynamiska media måste du ha:

1. Tillgång till Dynamic Media.
1. [Synkroniserade bilderna som är tillgängliga i din AEM Assets-instans med Dynamic Media för att använda dem för att skapa mallen](/help/assets/dynamic-media/config-dm.md).
1. har verifierat följande i Touch-gränssnittet:
   * **[!UICONTROL Dynamic Media sync mode]** som är inställd på **[!UICONTROL Disabled by default]** på **[!UICONTROL Edit Dynamic Media Configuration page]** används inte på alla AEM-mappar (**[!UICONTROL Sync all content]** är avmarkerad). Mer information finns i [Konfigurera Dynamic Media Cloud Service](/help/assets/dynamic-media/config-dm.md).
   * **[!UICONTROL Dynamic Media sync mode]** är inställt på **[!UICONTROL Enable for subfolders]** för målmappen eller undermappen där du vill spara mallen när den har skapats. Mer information finns i [Konfigurera Dynamic Media Cloud Service](/help/assets/dynamic-media/config-dm.md).

## Skapa Dynamic Media WYSIWYG-mall{#how-to-create-dynamic-media-wysiwyg-template}

Så här skapar du en DM-mall:

1. [Skapa en tom arbetsyta](#create-a-canvas)
1. [Lägga till bilder på arbetsytan](#add-images-to-the-canvas)
1. [Lägga till textlager på arbetsytan](#add-text-to-the-canvas)
1. [Redigera eller ta bort ett lager](#edit-or-delete-a-layer)
1. [Parameterlager](#parameterise-a-layer)

### Skapa en tom arbetsyta{#create-a-canvas}

Så här skapar du en tom arbetsyta:

1. Navigera till Assets-vyn och klicka på **[!UICONTROL Dynamic Media Assets]** i den vänstra panelen.

   ![Dynamiska mediamallar](/help/assets/assets/DM-Assets1.png)

1. Klicka på **[!UICONTROL Create Template]** om du vill spara mallen under Dynamic Media Assets eller navigera till en mapp och klicka på **[!UICONTROL Create Template]** om du vill spara mallen i den mappen. Dialogrutan **[!UICONTROL New Template]** visas.
   ![Så här skapar du dynamiska mallar som kan anpassas i realtid](/help/assets/assets/new-template.png)
Om du vill [ skapa en mapp ](/help/assets/add-delete-assets-view.md) under **[!UICONTROL Dynamic Media Assets]** skapar du en mapp under **[!UICONTROL Assets]** . Mappträdet under **[!UICONTROL Assets]** replikeras under **[!UICONTROL Dynamic Media Assets]**.
1. Ange ett mallnamn, definiera arbetsytans bredd och höjd och klicka på **[!UICONTROL Create]**. En tom arbetsyta visas med menyalternativ på båda sidor som du kan använda för att skapa mallen. Håll muspekaren över menyalternativen för att se deras verktygstips.
   ![anpassningsbar mall i realtid](/help/assets/assets/blank-canvas-page.png)

>[!NOTE]
>
> Tillåtet intervall för bredd och höjd är mellan 50 och 5000.

**Menyalternativ i den högra rutan:** Använd dessa alternativ för att lägga till nödvändiga bilder och textlager på arbetsytan.

* ![DM-mallar](/help/assets/assets/add-image.svg): Klicka för att lägga till bilder på arbetsytan.
* ![anpassningsbara mallar](/help/assets/assets/add-text.svg): Klicka för att lägga till text på arbetsytan.
* ![anpassningsbara mallar](/help/assets/assets/show-layers-list.svg): Klicka för att visa listan över alla lager (bild och text) på arbetsytan. Alla bilder och all text som läggs till på arbetsytan representeras som separata lager.

**Menyalternativ i den vänstra rutan:** Använd dessa alternativ för vanliga redigeringsåtgärder som anges nedan.

* ![DM-mallar](/help/assets/assets/layer-selector.svg): Välj ett lager.
* ![mallar som stöder anpassning](/help/assets/assets/bring-forward.svg): Klicka för att föra ett markerat lager framåt eller tryck på **Ctrl** + **]** (Windows) eller **Cmd** + **]** (Mac).
* ![Så här skapar du en mall som enkelt kan anpassas](/help/assets/assets/send-backward.svg): Klicka för att skicka ett markerat lager bakåt eller tryck på **Ctrl** + **[** (Windows) eller **Cmd** + **[** (Mac).
* ![skapa en mall som kan anpassas direkt](/help/assets/assets/undo.svg): Klicka för att ångra den senaste åtgärden eller tryck på **Ctrl** + **Z** (Windows) eller **Cmd** + **Z** (Mac).
* ![mall för att skapa banners snabbt](/help/assets/assets/redo.svg): Klicka för att göra om den senaste åtgärden eller tryck på **Ctrl** + **Y** (Windows) eller **Cmd** + **Y** (Mac).
* ![mall för att snabbt skapa flygblad](/help/assets/assets/zoom-in.svg): Klicka för att zooma in arbetsytan eller tryck på **Ctrl** + **+** (Windows) eller Cmd + **+** (Mac).
* ![mall för att skapa banners snabbt](/help/assets/assets/Zoom-out.svg): Klicka för att zooma ut arbetsytan eller tryck på **Ctrl** + **-** (Windows) eller **Cmd** + **-** (Mac).
* Tryck på **Backsteg** eller **delete** för att ta bort det markerade lagret om ingen text eller egenskap redigeras.

Klicka på mallen ![om du vill skapa flygblad snabbt](/help/assets/assets/show-layers-list.svg) **>** fler alternativ (![](/help/assets/assets/three-dots.svg)) på lagret Canvas om du vill redigera arbetsytans dimensioner när du skapar mallen.
![](/help/assets/assets/edit-canvas1.png)

>[!NOTE]
>
> Mallar tillåter högst 20 lager, inklusive arbetsytan.

### Lägga till bilder på arbetsytan{#add-images-to-the-canvas}

Gör så här för att lägga till bilder på arbetsytan:

1. Klicka på ![skapa en banderoll på nolltid](/help/assets/assets/add-image.svg) för att visa panelen [Resursväljare](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/manage/asset-selector/overview-asset-selector). På panelen visas de bilder i din AEM Assets-instans som synkroniseras med Dynamic Media.
1. Bläddra i panelen eller använd nyckelord i sökfältet för att hitta en viss bild.
1. Dra och släpp en bild på arbetsytan för att använda den. Se [**[!UICONTROL Properties Panel]**](#reposition-resize-delete-a-layer) för att ändra storlek på eller flytta ett lager på arbetsytan.
   ![skapa en banderoll inom några sekunder](/help/assets/assets/add-image-to-canvas.png)

### Lägga till textlager på arbetsytan{#add-text-to-the-canvas}

Gör så här för att lägga till textlager på arbetsytan:

1. Klicka på ![skapa nya banderoller snabbt](/help/assets/assets/add-text.svg) för att lägga till ett textlager på arbetsytan och öppna panelen Egenskaper.
1. Markera lagret och klicka på texten för att uppdatera den.
1. Aktivera **[!UICONTROL Smart Text Resize]** på egenskapspanelen om du vill justera textlängden och teckensnittsstorleken automatiskt så att de passar i det avsedda området optimalt.
   ![bästa anpassningsbara banners](/help/assets/assets/add-text-layer.png)

Se [**[!UICONTROL Properties Panel]**](#reposition-resize-delete-a-layer) för att flytta, ändra storlek på, rotera eller ta bort lagret. Formatera texten till önskat teckensnitt, önskad storlek, färg, stil, justering (i lagret) genom att ändra deras värden i respektive fält under **[!UICONTROL Text]**-delen av panelen.

>[!NOTE]
>
> Om du vill använda ett annat teckensnitt än standardteckensnittsfamiljen Adobe Sans F2 måste du överföra och publicera teckensnittsfilen till AEM Assets och Dynamic Media. Om du har några gamla teckensnitt i din instans måste du [bearbeta om](/help/assets/reprocessing-assets-view.md) för att kunna visa dem i mallredigeraren.

### Redigera eller ta bort ett lager {#edit-or-delete-a-layer}

Så här redigerar eller tar du bort ett lager på arbetsytan:

1. Klicka på ![mallar med stöd för dynamiska uppdateringar](/help/assets/assets/show-layers-list.svg) och markera lagret antingen på arbetsytan eller i listan Lager.
1. Klicka på **fler alternativ** (![mallar med stöd för realtidsuppdateringar](/help/assets/assets/three-dots.svg)) om du vill redigera eller ta bort lagret.
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

Formatera texten till önskat teckensnitt, önskad storlek, färg, stil, justering (i lagret) genom att ändra deras värden i respektive fält under **[!UICONTROL Text]**-delen av panelen.

**[!UICONTROL Smart Text Resize]** Se till att inkludera **[!UICONTROL Smart Text Resize]** ([Textpassning](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/text-formatting/r-copy-fitting)) så att all text i det avsedda området passar optimalt genom att justera teckensnittsstorleken och längden smart. Den här funktionen förhindrar att texten flödar över eller minimerar extra blanksteg längst ned i texten.
![Skapa innehåll på nolltid](/help/assets/assets/smart-text-resize.png)

### Parameterlager {#parameterise-a-layer}

När du har skapat en mall med flera lager med bilder och texter, parametriseras de markerade lagren. När ett lager eller dess egenskap är parametriserad, hämtas ett nyckelvärdepar (kallas även parameter). Den här parametern kan inkluderas i mallens URL för att uppdatera lagrets position, storlek eller innehåll i realtid, vilket resulterar i att mallen anpassas på nolltid.

Så här parameteriserar du ett lager:

1. klicka på ![Skapa innehåll direkt](/help/assets/assets/show-layers-list.svg), markera ett lager och klicka på **[!UICONTROL Parameters]**. Panelen **[!UICONTROL Parameters]** visas.
1. Växla **[!UICONTROL Include Parameter]** för att parameterisera en egenskap. Mer information om egenskapens beteende efter parametrisering finns i [this](#parameterisation-options-or-allowed-parameters).
1. **Valfritt:** Byt namn på parametern. Ett parameternamn har ett lagernamn följt av ett suffix. Alla parametriserade egenskaper för ett markerat lager delar samma lagernamn följt av ett varierande suffix. Byt namn på lagret genom att följa den semantiska namnkonventionen, så att när du tar med parametern i URL:en, förklarar parameternamnet själva lagrets innehåll eller dess syfte.
1. Klicka på **[!UICONTROL Save]**.
   ![skapa innehåll direkt](/help/assets/assets/parameterise-a-layer.png)
Om du vill växla mellan parameterpanelen för ett bild- och textlager markerar du lagret på arbetsytan och klickar på **[!UICONTROL Parameters]** .

#### Alternativet Parameterpanel {#parameterisation-options-or-allowed-parameters}

Parameteriserade egenskaper kan inkluderas som URL-parametrar i mallens URL för att redigera mallen i realtid med URL:en.

**Bildparametrar:**

**X:** Inkludera om du vill flytta lagret vågrätt längs dess mittlinje, parallellt med mallplanets X-axel, genom att ändra parameterns värde i URL:en.
**Y:** Inkludera om du vill flytta lagret lodrätt längs dess mittlinje, parallellt med mallplanets Y-axel, genom att ändra parameterns värde i URL:en.
**Bredd:** Inkludera om du vill justera lagrets bredd genom att ändra parameterns värde i URL:en.
**Höjd:** Inkludera om du vill justera lagrets höjd genom att ändra parameterns värde i URL:en.
**Dölj:** Inkludera om du vill dölja eller visa lagret i mallen med 0 (visa) och 1 (dölj).
**Source:** Inkludera om du vill ersätta lagrets bild med en ny bild genom att ändra bildsökvägen i parameterns värde i URL:en.

**Textformateringsparametrar:**

Ta med parametrarna nedan om du vill redigera texten, teckensnittet, färgen och storleken från URL:en genom att uppdatera parametervärdena i URL:en.

**Text:** Inkludera om du vill uppdatera text från URL:en.
**Teckensnittsfamilj:** Inkludera om du vill uppdatera teckensnittet för texten från URL:en.
**Teckenstorlek:** Inkludera om du vill uppdatera textens teckenstorlek från URL:en.
**Textfärg:** Inkludera om du vill uppdatera textens teckenfärg från URL:en.

### Gruppera lager för att styra synligheten samtidigt{#group-layers}

Ett annat sätt att göra mallarna flexibla är att använda ett enda parameternamn för att styra flera lager. Den här strategin är användbar för parametern visibility (hide or show layers) för att uppdatera designen eller grafiken från en enda mall.

Följ de här stegen för att tilldela samma namn till parametrarna för att dölja (![skapa snabbt innehåll](/help/assets/assets/Visibility-icon.svg)) för flera lager, så att du kan dölja eller visa dem samtidigt.

1. Navigera till [**[!UICONTROL Properties Panel]**](#parameterise-a-layer) för ett lager.
1. Växla parametern **[!UICONTROL Hide]** om den inte är parameteriserad tidigare.
1. **Valfritt:** Byt namn på parametern Dölj.
1. Kopiera Dölj parameternamn.
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
1. Välj parametern hide för [grupperade lager](#group-layers) i listan om du vill visa eller dölja dem tillsammans i mallen.
1. **Valfritt:** Ändra parametervärdet **[!UICONTROL Hide]** mellan 0 och 1 och klicka på **[!UICONTROL Refresh]** för att se ändringarna. Lager med samma dolda parameter döljs eller visas tillsammans. På samma sätt kan du styra lagrens synlighet från URL-adressen.

   ![skapar innehåll i farten](/help/assets/assets/dm-templates-publish-status.png)
Du kan också växla **[!UICONTROL Include all parameters]** för att redigera alla parametervärden som visas och se uppdateringarna i mallförhandsvisningen.
   <br>
1. Om du vill publicera mallen på förhandsgranskningssidan klickar du på **[!UICONTROL Publish]** och bekräftar att du vill publicera. Meddelandet Publicera färdigt visas och publiceringsstatusen uppdateras till Publicerat.

>[!NOTE]
>
>När du publicerar mallen måste mallbilderna publiceras först.

### Kopiera leverans-URL

De valda parametrarna på sidan **[!UICONTROL Preview]** blir URL-parametrar i mall-URL:en.

Så här kopierar du URL:en för den publicerade mallen som visas i förhandsgranskningen:

1. Klicka på **[!UICONTROL Copy URL]**. Dialogrutan **[!UICONTROL Copy URL]** visas. Markera och kopiera den URL som visas. Observera att den första parametern i URL:en börjar efter frågetecknet **(?)** och ett nyckelvärdepar börjar med **$** och slutar med **&amp;**. Nyckeln och värdet avgränsas med ett likhetstecken **(=)**, med tangenten till vänster och värdet till höger.
1. Klistra in den här URL-adressen på webbläsarfliken och se den aktiva mallen. Anpassa mallen i realtid genom att uppdatera den obligatoriska parameterns värde (Key-värdet) i URL:en direkt, vilket visas i [steg 2](#preview-and-publish-template-and-copy-template-deliver-url) i avsnittet **Förhandsgranska och publicera** .
1. Använd den här URL:en för snabb försäljning av produkter och tjänster. Du kan dela den här URL:en med dina kunder eller integrera den på din webbplats eller i ett tredjepartsprogram för att visa banderollen och göra uppdateringar i realtid för den så att den speglar de pågående erbjudandena.

Lär dig skapa en mall för dynamiska media steg för steg i den här videon.
>[!VIDEO](https://video.tv.adobe.com/v/3443281)

## Uppdatera mallen i realtid från URL:en{#update-the-template-from-the-url}

Det kan vara tidsödande att redigera parametrar direkt i URL:en. Förenkla:

1. Kopiera URL-adressen och klistra in den i en anteckningsruta.
1. Använd Cmd+F (Mac) eller Ctrl+F (Windows) för att hitta och redigera parametervärdena. Till exempel:
   * Ersätt bildbanor för bildlager.
   * Justera lagerdimensioner och lagerpositioner (om [är parametriserad](#parameterise-a-layer)).
   * Redigera text, teckensnitt, färg, storlek eller justering för textlager.
   * Ändra synlighetsvärden mellan 0 och 1.

Klistra in den uppdaterade URL-adressen i webbläsaren för att visa ändringarna.

## Redigera mallen{#edit-the-template}

Redigera mallen genom att följa de här stegen:

1. Klicka på **[!UICONTROL Dynamic Media Assets]** i vyn Assets.
2. Navigera till mallplatsen.
3. Markera mallen.
4. Klicka på **[!UICONTROL Edit Template]**. Mallens arbetsyta visar mallen och listan över alla dess lager på panelen Lager. Börja redigera mallen efter dina behov.

## Viktiga punkter att notera {#important-points-to-note}

* När du har skapat en mall med parametriserade bildlager för dynamiska uppdateringar måste du se till att de bilder som är avsedda för framtida uppdateringar har samma dimensioner som de parametriserade bilderna. Detta garanterar att bilderna passar perfekt i lagren utan att de flödar över eller lämnar tomma utrymmen. Mallen stöder för närvarande inte automatiska dimensionsjusteringar för att passa in bilder i lagren.
* Det finns inget stöd för delsträngar i ett textlager. Användaren kan inte använda olika teckensnittsegenskaper på delsträngar i ett textlager.
* Stöd för flera Dynamic Media-företag finns för närvarande inte med Dynamic Media Templates.
* Om du kopierar eller flyttar, visar målväljaren alla mappar (inklusive icke-dynamiska mediasynkroniserade mappar). För närvarande visas inte heller resurserna för dynamiska mediamallar (båda är begränsningar för målväljaren).
* Alla uppdateringsåtgärder för en mapp (till exempel Publicera eller Ta bort) från Assets-avsnittet påverkar de dynamiska mediamallar som finns i den mappen.
* Det går inte att använda papperskorgen för dynamiska mediamallar. Om en resurs flyttas till papperskorgen och sedan återställs, återställs resursen i AEM men inte i Dynamic Media. Samma sak gäller för dynamiska mediamallar.

## Se även

1. Utforska [Dynamiska media och dess funktioner](/help/assets/dynamic-media/dynamic-media.md)
1. Utforska [Dynamiska media med OpenAPI-funktioner](/help/assets/dynamic-media-open-apis-overview.md)

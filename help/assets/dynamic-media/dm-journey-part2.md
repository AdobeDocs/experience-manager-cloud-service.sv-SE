---
title: Resa till Dynamic Media, del II
description: Dynamic Media Journey beskriver grunderna i Dynamic Media, hur det fungerar, vad det kan göra för dig och vilket värde det ger både ditt arbete och dina kunder.
contentOwner: Rick Brough
products: Experience Manager as a Cloud Service
topic-tags: introduction,administering
content-type: reference
feature: Image Profiles,Best Practices
role: User, Admin
mini-toc-levels: 4
hide: false
hidefromtoc: false
exl-id: cdca41ad-a2cd-4f68-aaa4-5eec33c30f0b
source-git-commit: 879af9e3168a1ab993eff930355c4bd200879c71
workflow-type: tm+mt
source-wordcount: '2591'
ht-degree: 0%

---

# Dynamic Media Journey: The Basics, del II  {#dm-journey-part2}

{{work-with-dynamic-media}}

Välkommen till Dynamic Media Journey: The Basics, Part II, där du kan förvänta dig följande:

* Anatomi av en Dynamic Media-URL och hur Dynamic Media levererar innehåll
* Grundläggande om att skapa bildförinställningar för att återge resurser
* Bilduppsättningar, snurpuppsättningar och blandade medieuppsättningar

Se även [Dynamic Media Journey; The Basics, Part I](/help/assets/dynamic-media/dm-journey-part1.md).

>[!TIP]
>
>För bästa resultat rekommenderar Adobe att du läser och visar den här Dynamic Media-resan på en stationär dator.

## Anatomi av en Dynamic Media-URL och hur Dynamic Media levererar innehåll {#dm-journey-d}

När dina Dynamic Media-resurser har överförts och publicerats kan du kopiera resursens genererade URL och klistra in den i webbläsaren för att se hur resursen kommer att se ut för kunden. Följande kopierade URL-adress för en bevakad bild bryts ned efter färg så att den blir lättare att läsa och förstå.

![Anatomi en Dynamic Media URL](/help/assets/dynamic-media/assets/dm-colored-url.png)
_Anatomi av en Dynamic Media-URL._

Den första delen av URL:en i rött refererar till själva serverdomänen. I det här fallet körs Dynamic Media på en allmän serverdomän, som är `https://s7d1.scene7.com/is/image/`. Det är enkelt att ta en titt på en uppsättning bilder och förstå om de hanteras av Dynamic Media bara genom att titta på serverdomänen. URL:en kommer att vara ganska konsekvent. Det finns dock vissa Dynamic Media-kunder som har bytt till en dedikerad serverdomän där den kan vara `name-of-your-company.scene7.com`. En dedikerad serverdomän krävs för Smart Imaging.

Kontonamnet är delen i lila. I det här fallet kallas kontot `jpearldemo`.

Resurs-ID:t eller namnet `AdobeStock_28563982` är grönt. Observera att resursen har filtillägget _no_ som `.png` eller `.jpg`. När resurser hämtas till Dynamic Media tas filtillägget bort och en annan typ av fil skapas: en pyramid-TIFF-fil. Med Pyramic-TIFF kan Dynamic Media snabbt skapa renderingar direkt.

Slutligen finns det några bildbehandlingsparametrar, `?wid=1000&fmt=jpeg&qlt=85`, som visas i gult på slutet.

Hela URL-sökvägen är aktiv. [Prova](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock_28563982?wid=1000&amp;fmt=jpeg&amp;qlt=85){target="_blank"}.

Låt webbläsarfönstret fortfarande vara öppet för Dynamic Media URL och den bevakade bilden. Vi tittar närmare på hur du kan skapa återgivningar av bilden bara genom att ändra URL:en.

### Återge den bevakade bilden via URL:en

Börja med att manuellt ta bort endast bildbearbetningsreglerna i URL-sökvägen. Lämna servernamnet, kontonamnet och resurs-ID:t eller bildnamnet. [Prova](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock_28563982){target="_blank"}.

Lägg nu till en bildbehandlingsparameter i slutet av URL:en. I URL-fältet skriver du `?wid=500` till höger om bildnamnet och trycker sedan på **[!UICONTROL Enter]**. [Prova](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock%5F28563982?wid=500){target="_blank"}.

Observera att en ny återgivning av bevakningen genereras. En viktig fördel med detta enkla arbete med att ändra bildens bredd är att bilden som visas genereras 100 % dynamiskt.

Ändra nu breddvärdet för `500` pixlar till `1000` pixlar och tryck sedan på **[!UICONTROL Enter]**. [Prova](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock%5F28563982?wid=1000){target="_blank}.
När du trycker på **[!UICONTROL Enter]** återgår webbläsaren till Dynamic Media Image Server. Den genererar en helt ny återgivning av klockan, baserat på det nya breddvärdet du just angav, skickar sedan tillbaka den nya bilden till webbläsaren och cachelagrar den.

Dynamic Media har många bildbehandlingsparametrar som du kan använda för att finjustera bildresurser på webbsidor. Du kan [se en lista över dem här](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html?lang=en).

Prova att lägga till en rotationsparameter till den bevakade bilden. Och slutet på URL-sökvägen, omedelbart efter `wid=1000`, skriv `&rotate=90` och tryck sedan på **[!UICONTROL Enter]**. [Prova](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock%5F28563982?wid=1000&amp;rotate=90){target="_blank"}.

Klockan är fortfarande något skev till vänster. Ändra rotationsvärdet för `90` till `92` och tryck sedan på **[!UICONTROL Enter]**. [Prova](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock%5F28563982?wid=1000&amp;rotate=9){target="_blank"}.

När du trycker på **[!UICONTROL Enter]** genereras en ny återgivning av klockan nästan omedelbart. Du kan se vilken typ av prestanda du får, vilket förklarar varför Dynamic Media kan leverera fler än 800 000 bildbegäranden, _per sekund_, under en hektisk helg eller en stor semester.

Även om det går att ändra bildbehandlingsparametrar i en URL-adress bild för bild är det inte en effektiv metod, särskilt om du har tiotusentals bilder som utgör webbplatsen. Ett mycket bättre sätt är att använda bildförinställningar.

## Grundläggande om att skapa bildförinställningar för att återge resurser {#dm-journey-e}

Det finns flera sätt och platser där du vill skapa en bild eller ha en bild tillgänglig. Traditionellt sett går en Creative-användare in i Adobe Photoshop och sparar alla dessa olika renderingar som statiska bilder.

![Statiska bilder](/help/assets/dynamic-media/assets/dm-static-images.png)
_Bra: statiska bilder som skapats manuellt._

Nu kan du föreställa dig att Creative Director tittar på bilderna och säger:

_&quot;Jag ville verkligen ha den här bilden så att den stora handen pekar på de fyra, och den lilla handen pekar på den första för att göra det lättare att se den.&quot;_

Alla nya statiska bilder måste fotograferas igen.

Men om du har olika bildförinställningar i Dynamic Media kan du använda dessa bilder var du vill. Bildförinställningarna följer standarder.

![Primär filhantering](/help/assets/dynamic-media/assets/dm-onefile.png)
_Bäst: en fil med flera återgivningar skapade i farten med hjälp av bildförinställningar, som `Search_Grid` och `Thumbnail` ._

| **Varför använda bildförinställningar?** | |
|---|---|
| Standarder | Bildförinställningar tillämpar en standardbehandling för bildbearbetning på alla bilder som de efterfrågas med. |
| Ändringshantering | Om du måste ändra bildbearbetningen redigerar du bara parametern för den befintliga bildförinställningen. Den uppdaterade definitionen sprids automatiskt till alla begäranden. |

Alla ställen där du behöver en viss typ av bild, till exempel

* en produktinformationssida,
* sökstödraster,
* miniatyrbild,
* shoppingkort, eller
* hjältebild

Du vill att den bilden ska levereras med samma parametrar oavsett var de kommer att användas.

Låt oss nu titta på hur en bildförinställning skapas i Dynamic Media.

![Skapa en bildförinställning med början på fliken Grundläggande](/help/assets/dynamic-media/assets/dm-image-preset-basictab.png)
_Skapa en bildförinställning som börjar med fliken Grundläggande._

I exemplet ovan ser du att en ny bildförinställning skapades med namnet _Medium_. Dynamic Media använder ett exempel, en färdig bild - ryggsäcken - som hjälper dig att se egenskaper för bildförinställningen när du skapar den.

Bildförinställningen _Medium_ har en bredd på 500 pixlar och en höjd på 800 pixlar. I del I av den här resan läser du om hur du levererar resurser i olika format. I listrutan **[!UICONTROL Format]** kan du välja att leverera resurser i JPEG, PNG, TIFF eller flera andra format. Här har du flexibilitet.

Om du väljer fliken **[!UICONTROL Advanced]** får du alternativ för resursens färgrymd. Beroende på vilket format du valde på fliken **[!UICONTROL Basic]** - i exemplet ovan markerades JPEG - kan du leverera resurser i RGB, gråskala eller CMYK. I listrutan **[!UICONTROL Color Profile]** kan du välja hur en CMYK-bildresurs ska levereras för utskrift. Observera också att det finns ytterligare parametrar som du kan använda för att göra bilderna skarpare. I det här fallet tillämpades **[!UICONTROL Unsharp Mask]**.

![Skapa en bildförinställning genom att välja alternativ på fliken Avancerat](/help/assets/dynamic-media/assets/dm-image-preset-advancedtab.png)
_Skapa en bildförinställning genom att välja alternativ på fliken Avancerat._

Du kommer ihåg i [Anatomi av en Dynamic Media URL](#dm-journey-d) tidigare att du läste om Dynamic Media URL och hur den skapades. I textrutan **[!UICONTROL Image Modifier]** kan du ange ytterligare bildbehandlingsparametrar som du vill använda. Parametrarna tas med i förinställningsnamnet för URL:en när bilderna levereras med hjälp av förinställningen. I skärmbilden ovan lades parametern `bgc=451B15` till. Det vill säga, en mörkbrun bakgrundsfärg lades till.

Du kan tänka dig en bildförinställning som ett recept för dina bilder. Den kommer att leverera alla bilder som använder förinställningen, konsekvent, varje gång; den kommer att vara densamma. Parametern `&op_brightness=+10` lades också till för att öka intensiteten något.

När du är klar sparar du förinställningen och nu är den tillgänglig för alla bilder som du har. I det här fallet vill du använda bildförinställningen _Medium_ på en bild av en skål flytande choklad.

![Använda bildförinställningen *Medium* för att generera en återgivning av en bild](/help/assets/dynamic-media/assets/dm-medium-image-preset.png)
_Använda bildförinställningen Medium för att generera en återgivning av en bild._

Du kopierar URL-adressen och klistrar sedan in den i webbläsaren för att kontrollera bildens utseende. [Prova](http://s7d1.scene7.com/is/image/jpearldemo/AdobeStock_74043302?$Medium$){target="_blank"}.

Lägg märke till namnet på bildförinställningen _Medium_ i den fullständiga URL-sökvägen i webbläsaren.

Du kan se vilken typ av skärpa som visas i bilden. Kvaliteten beror delvis på hur chokladskålen filmades. Dessutom beror det delvis på att du med Dynamic Media kan lagra större bilder än vad som levereras till de digitala kanalerna.

Om allt ser bra ut för chokladskålen, klistrar du in URL-adressen på webbsidorna där du vill att bilden ska visas på webbplatsen.

Om du tittar igen på den bevakade bilden nedan kan du se att det finns en `Cart`-bildförinställning, en `Grid`-förinställning, en `Large`-förinställning, en `PDP-page`-förinställning (produktinformationssida) och flera andra.

![Statiska och dynamiska bildförinställningar](/help/assets/dynamic-media/assets/dm-image-presets.png)
_Statiska och dynamiska bildförinställningar. Den bevakade bilden återgavs med bildförinställningen `PDP-page`._

Men tänk om du måste ändra en bild på din webbplats? Anta till exempel att du har utfört några tester och funnit att bilden på 120 x 120 (bildförinställningen `Cart`) inte tas emot som du trodde. Du måste göra bilden större genom att öka bredden till 175 pixlar och öka höjden till 175 pixlar. Traditionellt sett måste du bege dig till Adobe Photoshop och återskapa alla kundvagnsbilderna. Men med Dynamic Media redigerar du bara bildförinställningen genom att uppdatera värdena för Bredd och Höjd till 175 och spara förinställningen enligt exemplet nedan.

![Redigera en bildförinställning](/help/assets/dynamic-media/assets/dm-edit-image-preset.png)
_Redigera bredd och höjd för bildförinställningen i `Cart` ._

När du har ändrat bildförinställningen och tömt cacheminnet uppdateras alla bilder och alla URL:er som används med den förinställningen _ändras inte_ någonstans. Det innebär att inga brutna länkar och att inga omdirigeringar av webbsidor behövs.

## Bilduppsättningar, snurra uppsättningar och blandade medieuppsättningar {#dm-journey-f}

En del av de vanligaste användningsområdena för Dynamic Media är möjligheten att skapa bilduppsättningar, snurra och blandade medieuppsättningar.

Bilduppsättningar består vanligtvis av en serie bildresurser som presenteras som en enda enhet. Den här typen av uppsättningar ger användarna en integrerad visningsupplevelse, där användarna kan se olika vyer av ett objekt genom att klicka på en miniatyrbild. Med bilduppsättningar kan du presentera alternativa vyer av något och visningsprogrammet har zoomverktyg som gör att du kan granska bilder noggrant. [Visa en bilduppsättning med namnet&quot;Körs&quot; som använder visningsprogrammet ](https://s7d1.scene7.com/s7viewers/html5/FlyoutViewer.html?asset=jpearldemo/Running).

Här i Dynamic Media ser du flera bilder på skor. Det är en produktserie som försäljning och marknadsföring vill att kunderna ska se som en enda presentation, en Image-uppsättning.

![Skapa en bilduppsättning](/help/assets/dynamic-media/assets/dm-create-image-set.png)
_Början av att skapa en bilduppsättning._

Om du vill skapa bilduppsättningen väljer du **[!UICONTROL Image Set]** i den nedrullningsbara menyn **[!UICONTROL Create]**. Observera på menyn att det också finns alternativ för att skapa en **[!UICONTROL Mixed Media Set]**, en **[!UICONTROL Spin Set]** och en **[!UICONTROL Carousel Set]**. Du skapar uppsättningarna på ungefär samma sätt som en bilduppsättning.

En uppsättning med blandade media kan innehålla bilder, färgruteuppsättningar, snurruppsättningar, videor och adaptiva videouppsättningar. [Prova](https://s7d9.scene7.com/s7viewers/html5/MixedMediaViewer.html?asset=Scene7SharedAssets/Mixed_Media_Set_Sample). En snurra simulerar hur det verkliga händer att ett objekt testas. Med snurruppsättningar kan du visa viktiga visuella detaljer från alla vinklar. [Prova](https://s7d9.scene7.com/s7viewers/html5/SpinViewer.html?asset=Scene7SharedAssets/SpinSet_Sample&amp;stagesize=500,400){target="_blank"}.

Det är enkelt att skapa en bilduppsättning. Du lägger bara till de bildresurser som du vill inkludera i uppsättningen.

![Skapa en bilduppsättning](/help/assets/dynamic-media/assets/dm-create-image-set-add-assets.png)
_Med bilduppsättningsredigeraren kan du lägga till bildresurser och ändra ordningen på deras utseende i uppsättningen._

Du måste ge uppsättningen ett namn. Välj namnet noggrant eftersom du inte kan redigera det senare! I exemplet ovan kallas uppsättningen `Running`. När du är klar sparar du uppsättningen.

Här är `Running`-bilden i Experience Manager Assets.

![Den bild som körs i Experience Manager Assets, kortvyn](/help/assets/dynamic-media/assets/dm-image-set.png)
_`Running` Bilduppsättningen i Experience Manager Assets, kortvyn._

Vare sig du har skapat en uppsättning med bilder, en uppsättning med blandade media, en snurra eller något annat interaktivt medium vill du se hur den ser ut och fungerar för en kund när du har skapat den. Dynamic Media har många inbyggda visningsprogram som du kan använda för att göra just det.

Du börjar med att välja den inbyggda bilduppsättningen för att öppna den i en förhandsvisning som i följande exempel.

![Den bild som körs i förhandsvisning med alternativet Visare markerat](/help/assets/dynamic-media/assets/dm-image-set-viewer.png)
_Alternativet `Running` Bilduppsättningen i förhandsvisning med visningsprogram är markerat._

Observera i förhandsgranskningen att du kan välja de körbara färgrutorna och zooma in och ut på skorna. Om du vill använda ett visningsprogram för uppsättningen väljer du **[!UICONTROL Viewers]** i listrutan.

![Den bild som körs när visningsprogrammet för utfällbara bilder används](/help/assets/dynamic-media/assets/dm-image-set-flyout-viewer.png)
_`Running` Bilden med visningsprogrammet för utfällbara bilder._

I det här fallet har visningsprogrammet `Flyout` valts. Nu kan du förhandsvisa bilduppsättningen i visningsprogrammet. Men det är bäst att se det i webbläsaren, precis som kunden ser det. Du väljer **[!UICONTROL URL]** i det nedre vänstra hörnet, kopierar URL-adressen och klistrar in den i webbläsaren. [Prova](https://s7d1.scene7.com/s7viewers/html5/FlyoutViewer.html?asset=jpearldemo/Running&amp;config=jpearldemo/Flyout){target="_blank"}.

Med den enda URL:en kan du använda bilduppsättningen och visningsprogrammet där du behöver dem på webbplatsen. I det föregående exemplet kan du ha lagt märke till att **[!UICONTROL Embed]** är till höger om URL-knappen. Genom att välja **[!UICONTROL Embed]** kan du kopiera koden för den här bilduppsättningen/visningsprogrammet och lägga till den på en webbsida eller i en Experience Manager Sites-komponent.

Utfällbara visningsprogram är ett standardvisningsprogram som inte kan öppnas och vars egenskaper du kan redigera. Eller, precis som när du skapar en bildförinställning, kan du skapa ett eget anpassat visningsprogram.

Anta att ert sälj- och marknadsföringsteam inte gillar visningsprogrammet. De gillar zoomfunktionen men vill att kunderna ska se zoomeffekten direkt över skorna. I så fall tillämpar du bara InlineZoom-visningsprogrammet på bilduppsättningen och kopierar och klistrar in URL-adressen i webbläsaren för att se hur den fungerar. [Prova](https://s7d1.scene7.com/s7viewers/html5/FlyoutViewer.html?asset=jpearldemo/Running&amp;config=jpearldemo/InlineZoom){target="_blank"}.

När du flyttar muspekaren över skon zoomar du in i den bilden och du ser fler detaljer när du flyttar pekaren. Orsaken till det är bara storleken på bilden som ursprungligen överfördes till Dynamic Media.

När du funderar på att bo som konsument eller arbeta i din dagliga roll och när du besöker olika webbplatser ser du saker som detta. Fundera på hur det går till och hur du kan använda Dynamic Media i ditt eget arbete och på företagets webbplats.

Du läser bara om bilduppsättningar och visningsprogram. Låt oss titta på ett par andra tittare och testa dem på enstaka resurser. Om du vill återställa visningsprogrammet klickar du på knappen **[!UICONTROL Refresh]** i det nedre vänstra hörnet.

<!-- LEAVE THIS HIDDEN PATH IN THE DOCUMENTATION FOR DEMO PURPOSES [Flyout viewer with image set](http://www.partycity.com/girls-little-old-lady-costume-P750948.html) -->

* Visningsprogrammet `ZoomVertical_dark` används för en bildresurs. [Prova](https://s7d1.scene7.com/s7viewers/html5/ZoomVerticalViewer.html?asset=jpearldemo/AdobeStock_96311480&amp;config=jpearldemo/ZoomVertical_dark){target="_blank"}.
* Visningsprogrammet `Zoom_light` används på en bild. [Prova](https://s7d1.scene7.com/s7viewers/html5/BasicZoomViewer.html?asset=jpearldemo/AdobeStock_38827423&amp;config=jpearldemo/Zoom_light){target="_blank"}.

## Valfritt - Läs mer

Om du vill veta mer om vad du just läste kan du använda materialet nedan för att utforska koncept i detalj. Annars är din Dynamic Media Journey klar!

{{see-also-dm}}

<!--
_Dynamic Media Help topics_

* [How to create image presets](/help/assets/dynamic-media/image-presets.md)
* A list of [image processing parameters](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html) that you can use in the Image Modifier field when you create an image preset
* [How to preview assets](/help/assets/dynamic-media/previewing-assets.md)
* [How to preview 3D assets](/help/assets/dynamic-media/previewing-3d-assets.md)
* [How to create Image sets](/help/assets/dynamic-media/image-sets.md)
* [How to create Spin sets](/help/assets/dynamic-media/spin-sets.md)
* [How to create Mixed Media sets](/help/assets/dynamic-media/mixed-media-sets.md) -->

_Dynamic Media självstudiekurser_

* [Använd Dynamic Media med Experience Manager Assets](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-overview-feature-video-use.html)
* [Adobe Experience Manager innehållsbibliotek](https://experienceleague.adobe.com/?lang=en#recommended/solutions/experience-manager) (sök på _Dynamic Media_)

_Dynamic Media-visningsprogram_

* [Live-demonstrationer](https://landing.adobe.com/en/na/dynamic-media/ctir-2755/live-demos.html) för varje visningsprogram

<!-- Live as of April 28 2022. LEAVE IN HERE https://landing.adobe.com/en/na/dynamic-media/ctir-2755/index.html -->
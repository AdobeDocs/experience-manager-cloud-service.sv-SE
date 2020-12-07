---
title: Grundläggande hantering
description: Bekanta dig med navigering i AEM och dess grundläggande användning
translation-type: tm+mt
source-git-commit: 305f584d89bc92f89b3ddaa49bb5da2f10e567db
workflow-type: tm+mt
source-wordcount: '2864'
ht-degree: 4%

---


# Grundläggande hantering {#basic-handling}

Dokumentet är utformat för att ge en översikt över grundläggande hantering när du använder AEM redigeringsmiljö. Konsolen **Platser** används som bas.

>[!NOTE]
>
>* Vissa funktioner är inte tillgängliga i alla konsoler, och i vissa konsoler kan ytterligare funktioner vara tillgängliga. Specifik information om de enskilda konsolerna och deras tillhörande funktioner beskrivs mer ingående på andra sidor.
>* Kortkommandon är tillgängliga i hela AEM. Speciellt när [du använder konsoler](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md) och [redigerar sidor](/help/sites-cloud/authoring/fundamentals/keyboard-shortcuts.md).


## Ett touchaktiverat gränssnitt {#a-touch-enabled-ui}

AEM användargränssnitt har aktiverats för beröring. Med ett pekaktiverat gränssnitt kan du använda touchfunktioner för att interagera med programvaran med gester som att trycka, hålla ned och dra. Eftersom användargränssnittet för AEM är pekaktiverat kan du använda pekgester på enheter med pekskärm som mobiltelefonen eller surfplattan. Det finns dock även musåtgärder på en traditionell stationär enhet, vilket ger dig flexibilitet när det gäller hur du väljer att skapa ditt innehåll.

## Steg {#first-steps}

Omedelbart efter inloggningen kommer du till navigeringspanelen [](#navigation-panel). Om du väljer något av alternativen öppnas respektive konsol.

![Navigeringspanelen](/help/sites-cloud/authoring/assets/navigation.png)

För att få en god förståelse för hur AEM används är det här dokumentet baserat på konsolen **Platser**. Klicka på eller tryck på **Platser** för att komma igång.

## Produktnavigering {#product-navigation}

När en användare först kommer åt en konsol startas en produktnavigeringssjälvstudiekurs. Klicka eller tryck en minut för att få en bra överblick över den grundläggande hanteringen av AEM.

![Navigering, genomgång](/help/sites-cloud/authoring/assets/tutorial.png)

Klicka eller tryck på **Nästa** för att gå vidare till nästa sida i översikten. Klicka eller tryck på **Stäng** eller klicka eller tryck utanför översiktsdialogrutan för att stänga.

Översikten startas om nästa gång du öppnar en konsol, såvida du inte antingen visar alla bilder eller markerar alternativet **Visa inte detta igen**.

## Global navigering {#global-navigation}

Du kan navigera mellan konsolerna med den globala navigeringspanelen. Detta aktiveras som en listruta i helskärmsläge när du klickar eller trycker på länken Adobe Experience Manager längst upp till vänster på skärmen.

Du kan stänga den globala navigeringspanelen genom att klicka eller trycka på **Stäng** för att gå tillbaka till föregående plats.

![Navigeringspanelens övre fält](/help/sites-cloud/authoring/assets/navigation-bar.png)

Global navigering har två paneler, som representeras av ikoner i skärmens vänstra marginal:

* **[Navigering](#navigation-panel)**  - Representeras av en kompass och standardpanelen när du loggar in på AEM
* **[Verktyg](#tools-panel)**  - motsvaras av en hammare

De alternativ som är tillgängliga på dessa paneler beskrivs nedan.

### Navigeringspanel {#navigation-panel}

Navigeringspanelen:

![Navigeringspanelen](/help/sites-cloud/authoring/assets/navigation.png)

Titeln på webbläsarfliken uppdateras för att återspegla din position när du navigerar genom konsolerna och innehållet.

Följande konsoler finns i Navigation:

| Konsol | Syfte |
|---|---|
| Projekt | Med projektkonsolen får du direktåtkomst till dina projekt. [Projekt är virtuella ](/help/sites-cloud/authoring/projects/overview.md) kontrollpaneler som kan användas för att skapa ett team. Sedan kan ni ge teamet tillgång till resurser, arbetsflöden och uppgifter och på så sätt låta andra arbeta mot ett gemensamt mål. |
| Sites | Med platskonsolerna kan du [skapa, visa och hantera platser](/help/sites-cloud/authoring/fundamentals/organizing-pages.md) som körs på din AEM. Med den här konsolen kan du skapa, redigera, kopiera, flytta och ta bort sidor, starta arbetsflöden och publicera sidor. |
| Experience Fragments | En [Experience Fragment](/help/sites-cloud/authoring/fundamentals/experience-fragments.md) är en fristående upplevelse som kan återanvändas i alla kanaler och som har variationer, vilket sparar problem med att kopiera och klistra in upplevelser eller delar av upplevelser upprepade gånger. |
| Assets | Med Resurskonsolen kan du importera och hantera digitala resurser som bilder, videoklipp, dokument och ljudfiler. Dessa resurser kan sedan användas av alla webbplatser som körs på samma AEM.<!--add some kind of assets link--> |
| Personanpassning | Den här konsolen innehåller ett ramverk med verktyg för att [skapa riktat innehåll och presentera personaliserade upplevelser.](/help/sites-cloud/authoring/personalization/overview.md) |

## Panelen Verktyg {#tools-panel}

På verktygspanelen finns en sidopanel som innehåller en rad kategorier som grupperar liknande verktygskonsoler. Verktygskonsolerna ger tillgång till ett antal specialiserade verktyg och konsoler som hjälper dig att administrera dina webbplatser, digitala resurser och andra aspekter av ditt innehållslager. <!--The [Tools consoles](/help/sites-administering/tools-consoles.md) provide access to a number of specialized tools and consoles that help you administer your websites, digital assets, and other aspects of your content repository.-->

![Verktygspanelen](/help/sites-cloud/authoring/assets/tools-panel.png)

## Sidhuvudet {#the-header}

Rubriken visas alltid längst upp på skärmen. De flesta alternativen i huvudet är desamma oavsett var du befinner dig i systemet, men vissa är sammanhangsspecifika.

![Navigeringsrubrik](/help/sites-cloud/authoring/assets/navigation-bar.png)

* [Global navigering](#global-navigation)

   Klicka på länken **Adobe Experience Manager** för att navigera mellan konsoler.

   ![Global navigering](/help/sites-cloud/authoring/assets/global-navigation.png)

* [Sökning](/help/sites-cloud/authoring/getting-started/search.md)

   ![Ikonen Sök](/help/sites-cloud/authoring/assets/search-icon.png)

   Du kan också använda kortkommandot [](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md) `/` (snedstreck) för att starta sökning från en konsol.

* [Lösningar](https://www.adobe.com/experience-cloud.html)

   ![Knappen Lösningar](/help/sites-cloud/authoring/assets/solutions.png)

* [Hjälp](#accessing-help)

   ![Hjälp-knapp](/help/sites-cloud/authoring/assets/help.png)

* [Meddelanden](/help/sites-cloud/authoring/getting-started/inbox.md)

   ![Knappen Meddelanden](/help/sites-cloud/authoring/assets/notifications.png)

   Den här ikonen kommer att märkas med antalet för närvarande tilldelade ofullständiga meddelanden.

* [Användaregenskaper](/help/sites-cloud/authoring/getting-started/account-environment.md)

   ![Knappen Användaregenskaper](/help/sites-cloud/authoring/assets/user-properties.png)

* [Järnvägsväljare](#rail-selector)

   ![Knapp för att välja tåg](/help/sites-cloud/authoring/assets/rail-selector.png)

   Vilka alternativ som visas beror på den aktuella konsolen. I **Platser** kan du t.ex. markera endast innehåll (standardvärdet), tidslinjen, referenser eller panelen på filtersidan.

   ![Exempel på järnvägsväljare](/help/sites-cloud/authoring/assets/rail-selector-example.png)

* Breadcrumbs

   ![Bläddringar i navigeringsfältet](/help/sites-cloud/authoring/assets/breadcrumbs-navigation.png)

   I mitten av spåret, och alltid med beskrivningen av det markerade objektet, kan du navigera i en viss konsol med hjälp av de synliga kolumnerna. I konsolen **Platser** kan du navigera på webbplatsens nivåer.

   Klicka bara på den breda texten för att visa en listruta med hierarkinivåerna för det markerade objektet. Klicka på en post för att hoppa till den platsen.

   ![Exempel på expanderade vägbeskrivningar](/help/sites-cloud/authoring/assets/breadcrumbs-example.png)

* **Knappen** Skapa

   ![Knappen Skapa](/help/sites-cloud/authoring/assets/create.png)

   När du klickar på det här alternativet lämpar sig de alternativ som visas för konsolen/kontexten.

* [Vyer](#viewing-and-selecting-resources)

   Vyikonen finns längst till höger i verktygsfältet AEM. Eftersom den aktuella vyn också visas ändras den. I standardvyn, **Kolumnvy**, visas till exempel:

   ![Knappen Vyer](/help/sites-cloud/authoring/assets/views-button.png)

   Du kan växla mellan kolumnvy, kortvy och listvy. I listvyn visas även visningsinställningarna.

   ![Vyer](/help/sites-cloud/authoring/assets/view.png)

   >[!NOTE]
   >
   >Alternativet **Visa inställningar** är bara tillgängligt i **listvyn**.

* Tangentbordsnavigering

   Du kan bara navigera på en webbplats med hjälp av tangentbordet. Detta använder standardwebbläsarfunktionerna i **TAB**-tangenten (eller **OPT+TAB**) för att flytta dig mellan element på sidan som är fokuserbara.

   I konsolen **Platser** finns det ett alternativ för att **Hoppa till huvudinnehåll**. Detta blir synligt när du bläddrar mellan rubrikalternativen och snabbar upp navigeringen genom att du kan hoppa över standardelementen i verktygsfältet (produkten) och ta dig direkt till huvudinnehållet.

   ![Hoppa till huvudinnehåll](/help/sites-cloud/authoring/assets/skip-to-main-content.png)

## Få hjälp {#accessing-help}

Det finns olika hjälpresurser:

* **Verktygsfältet Konsol**

   Beroende på var du befinner dig kommer ikonen **Hjälp** att öppna rätt resurser:

   ![Hjälpikon](/help/sites-cloud/authoring/assets/help-console.png)

* **Navigering**

   Första gången du navigerar i systemet [innehåller en serie bilder AEM navigering](#product-navigation).

   ![Självstudiekurs](/help/sites-cloud/authoring/assets/tutorial.png)

* **Page Editor**

   Första gången du redigerar en sida innehåller en serie bilder en sidredigerare.

   ![Redigerare, genomgång](/help/sites-cloud/authoring/assets/editor-tutorial.png)

   Navigera i den här översikten på samma sätt som du gör med [produktnavigeringsöversikten](#product-navigation) när du för första gången använder en konsol.

   På menyn [**Sidinformation** kan du när som helst välja **Hjälp**](/help/sites-cloud/authoring/fundamentals/environment-tools.md#accessing-help) om du vill visa detta igen.

* **Verktygskonsol**

   Från konsolen **Verktyg** kan du även komma åt de externa **resurserna**:

   * **Dokumentation**  - Se dokumentationen för Web Experience Management
   * **Resurser**  för utvecklare - Resurser och nedladdningar för utvecklare

   >[!NOTE]
   >
   >Du kan när som helst få tillgång till en översikt över kortkommandon med snabbtangenten `?` (frågetecken) i en konsol.
   >
   >En översikt över alla kortkommandon finns i följande dokumentation:
   >
   >* [Kortkommandon för att redigera sidor](/help/sites-cloud/authoring/fundamentals/keyboard-shortcuts.md)
   >* [Kortkommandon för konsoler](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md)


## Verktygsfältet Åtgärder {#actions-toolbar}

När en resurs är markerad (t.ex. en sida eller en resurs) visas olika åtgärder med ikoner med förklarande text i verktygsfältet. Dessa åtgärder är beroende av:

* Aktuell konsol
* Aktuellt sammanhang
* Om du är i [markeringsläge](#viewing-and-selecting-resources)

Den åtgärd som är tillgänglig i verktygsfältet ändras så att den återspeglar de åtgärder du kan vidta för de valda objekten.

Hur du [väljer en resurs](#viewing-and-selecting-resources) beror på vyn.

På grund av utrymmesbegränsningar i vissa fönster kan verktygsfältet snabbt bli längre än det tillgängliga utrymmet. När detta inträffar visas ytterligare alternativ. Om du klickar eller trycker på ellipsen (de tre punkterna eller **...**) öppnas en listruta med alla återstående åtgärder. När du till exempel har valt en sida i **Sites**-konsolen:

![Ytterligare alternativ](/help/sites-cloud/authoring/assets/additional-options.png)

>[!NOTE]
>
>De enskilda ikonerna som är tillgängliga dokumenteras i relation till rätt konsol/funktion/scenario.

## Snabbåtgärder {#quick-actions}

I [kortvyn](#card-view) är vissa åtgärder tillgängliga som snabbåtgärdsikoner och som finns i verktygsfältet. Snabbåtgärdsikoner är tillgängliga för ett enskilt objekt i taget och eliminerar behovet av att välja i förväg.

Snabbåtgärderna visas när du för musen över ett resurskort (en stationär enhet). Vilka snabbåtgärder som är tillgängliga beror på konsolen och sammanhanget. Här följer till exempel snabbåtgärderna för en sida i konsolen **Platser**:

![Ytterligare alternativ](/help/sites-cloud/authoring/assets/quick-actions.png)

## Visa och välja resurser {#viewing-and-selecting-resources}

Visning, navigering och markering är lika begreppsmässigt för alla vyer, men har små variationer i hantering, beroende på vilken vy du använder.

Du kan visa, navigera i och välja (för ytterligare åtgärder) dina resurser med någon av de tillgängliga vyerna, som du kan markera med ikonen längst upp till höger:

* [Kolumnvy](#column-view)
* [Kortvy](#card-view)
* [Listvy](#list-view)

>[!NOTE]
>
>Som standard visas inte de ursprungliga återgivningarna av resurser i användargränssnittet som miniatyrbilder i någon av vyerna i AEM Assets. Om du är administratör kan du använda övertäckningar för att konfigurera AEM Assets så att ursprungliga återgivningar visas som miniatyrbilder.

### Välja resurser {#selecting-resources}

Välja en specifik resurs beror på en kombination av vyn och enheten:

| Visa | Välj Touch | Välj skrivbord | Avmarkera Touch | Avmarkera skrivbord |
|---|---|---|---|---|
| Kolumn | Tryck på miniatyrbilden | Klicka på miniatyrbilden | Tryck på miniatyrbilden | Klicka på miniatyrbilden |
| Kort | Tryck och håll på kortet | Muspekaren använder sedan snabbåtgärden för bockmarkering | Tryck på kortet | Klicka på kortet |
| Lista | Tryck på miniatyrbilden | Klicka på miniatyrbilden | Tryck på miniatyrbilden | Klicka på miniatyrbilden |

#### Markera alla {#select-all}

Du kan markera alla objekt i valfri vy genom att klicka på alternativet **Markera alla** längst upp till höger på konsolen.

* I **kortvyn** är alla kort markerade.
* I **listvyn** markeras alla objekt i listan.
* I **Kolumnvy** markeras alla objekt i kolumnen längst till vänster.

![Markera alla](/help/sites-cloud/authoring/assets/select-all.png)

#### Avmarkera alla {#deselecting-all}

När du markerar objekt visas antalet markerade objekt längst upp till höger i verktygsfältet.

Du kan avmarkera alla objekt och avsluta markeringsläget genom att:

* Klicka eller tryck på **X** bredvid antalet
* Använda **escape**-tangenten

![Avmarkera alla](/help/sites-cloud/authoring/assets/deselect-all.png)

I alla vyer kan du avmarkera alla objekt genom att trycka på Esc på tangentbordet om du använder en stationär enhet.

#### Välja exempel {#selecting-example}

1. I kortvyn:

   ![Vyn Kort](/help/sites-cloud/authoring/assets/card-view-select.png)

1. När du har valt en resurs täcks den översta rubriken av verktygsfältet [Åtgärder](#actions-toolbar) som ger åtkomst till åtgärder som för närvarande gäller för den valda resursen.

   Om du vill avsluta markeringsläget väljer du **X** längst upp till höger eller använder **escape**.

### Kolumnvy {#column-view}

![Kolumnvy](/help/sites-cloud/authoring/assets/column-view.png)

I kolumnvyn kan du visuellt navigera i ett innehållsträd genom en serie överlappande kolumner. I den här vyn kan du visualisera och gå igenom webbplatsens trädstruktur.

Om du väljer en resurs i kolumnen längst till vänster visas de underordnade resurserna i en kolumn till höger. Om du väljer en resurs i den högra kolumnen visas de underordnade resurserna i en annan kolumn till höger och så vidare.

* Du kan navigera uppåt och nedåt i trädet genom att trycka eller klicka på resursnamnet eller nedåt till höger om resursnamnet.

   * Resursnamnet och förvrängningen markeras när användaren knackar på eller klickar på den.
   * De underordnade resurserna för den resurs som användaren klickar på/trycker på visas i kolumnen till höger om den resurs som användaren klickar på/trycker på.
   * Om du trycker eller klickar på ett resursnamn som inte har några underordnade objekt visas informationen i den sista kolumnen.

* Om du trycker eller klickar på miniatyrbilden markeras resursen.

   * När du väljer det här alternativet kommer en bock att läggas över miniatyrbilden och resursnamnet kommer också att markeras.
   * Information om den valda resursen visas i den sista kolumnen.
   * Verktygsfältet för funktionsmakron blir tillgängligt.

   När en sida är markerad i kolumnvyn visas den markerade sidan i den sista kolumnen tillsammans med följande information:

   * Sidtitel
   * Sidnamn (del av sidans URL)
   * Mall som sidan baseras på
   * Ändringsinformation
   * Sidspråk
   * Publikationsinformation


### Kortvy {#card-view}

![Kortvy](/help/sites-cloud/authoring/assets/card-view.png)

* I kortvyn visas informationskort för varje objekt på den aktuella nivån. Dessa innehåller information som:

   * En visuell representation av sidinnehållet
   * Sidans titel
   * Viktiga datum (t.ex. senast redigerade och publicerade)
   * Om sidan är låst, dold eller ingår i en livecopy
   * Om det är lämpligt, när du måste vidta åtgärder som en del av ett arbetsflöde
      * Markörer som anger nödvändiga åtgärder kan vara relaterade till poster i din [inkorg](/help/sites-cloud/authoring/getting-started/inbox.md).

* [Snabbåtgärder ](#quick-actions) är också tillgängliga i den här vyn, t.ex. markering och vanliga åtgärder som redigering.

   ![Snabbåtgärder](/help/sites-cloud/authoring/assets/quick-actions.png)

* Du kan navigera nedåt i trädet genom att trycka/klicka på kort (var noga med att undvika snabbåtgärderna) eller uppåt igen genom att använda [vägbeskrivningar i rubriken](#the-header).

### Listvy {#list-view}

![Listvy](/help/sites-cloud/authoring/assets/list-view.png)

* I listvyn visas information om varje resurs på den aktuella nivån.
* Du kan navigera nedåt i trädet genom att trycka/klicka på resursnamnet och sedan säkerhetskopiera genom att använda [vägbeskrivningarna i rubriken](#the-header).
* Om du enkelt vill markera alla objekt i listan använder du kryssrutan längst upp till vänster i listan.

   ![Markera alla i listvyn](/help/sites-cloud/authoring/assets/list-view-select-all.png)

   * När alla objekt i listan är markerade visas den här kryssrutan markerad.

      * Avmarkera alla genom att klicka eller trycka på kryssrutan.
   * När bara vissa objekt är markerade visas det med ett minustecken.

      * Markera alla genom att klicka eller trycka på kryssrutan.
      * Klicka eller tryck på kryssrutan igen för att avmarkera alla.


* Markera de kolumner som ska visas med alternativet **Visa inställningar** under knappen Vyer. Följande kolumner är tillgängliga för visning:

   * **Namn**  - Sidnamn, som kan vara användbart i en flerspråkig redigeringsmiljö eftersom det är en del av sidans URL och inte ändras oavsett språk
   * **Ändrad**  - Senast ändrat den och senast ändrat av användaren
   * **Publicerad**  - Publiceringsstatus
   * **Mall**  - Mall som sidan baseras på
   * **Arbetsflöde**  - Arbetsflöde som används på sidan. Mer information finns när du för musen över eller öppnar tidslinjen.
   * **Sidanalys**
   * **Unika besökare**
   * **Tid på sidan**

      ![Markera kolumner](/help/sites-cloud/authoring/assets/select-columns.png)
   Som standard visas kolumnen **Namn**, som utgör en del av sidans URL. I vissa fall kan författaren behöva komma åt sidor på ett annat språk och det kan vara bra att se sidans namn (som vanligtvis inte ändras) om författaren inte kan sidans språk.

* Ändra objektens ordning med hjälp av den prickade lodräta listen längst till höger om varje objekt i listan.

   >[!NOTE]
   >
   >Det går bara att ändra ordningen i en ordnad mapp som har `jcr:primaryType`-värdet `sling:OrderedFolder`.

   ![Kolumnordning](/help/sites-cloud/authoring/assets/column-order.png)

   Klicka eller tryck på det lodräta markeringsfältet och dra objektet till en ny plats i listan.

   ![Orderlista](/help/sites-cloud/authoring/assets/order-list.png)

## Järnvägsväljare {#rail-selector}

**Rälsväljaren** är tillgänglig längst upp till vänster i fönstret och visar alternativ beroende på de aktuella konsolerna.

![Rälsväljaren expanderad](/help/sites-cloud/authoring/assets/rail-selector-expanded.png)

I **Platser** kan du t.ex. markera endast innehåll (standard), innehållsträdet, tidslinjen, referenser eller panelen på filtersidan.

Om du bara väljer innehåll visas bara ikonen för skenor. När något annat alternativ är markerat visas alternativnamnet bredvid ikonen för skenor.

>[!NOTE]
>
>[Det finns ](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md) kortkommandon som du kan använda för att snabbt växla mellan olika visningsalternativ.

### Innehållsträd {#content-tree}

Innehållsträdet kan användas för att snabbt navigera i platshierarkin på sidopanelen och visa mycket information om sidorna i den aktuella mappen.

Med innehållsträdets sidopanel i kombination med en listvy eller kortvy kan användarna enkelt se projektets hierarkiska struktur och enkelt navigera i innehållsstrukturen med innehållsträdets sidopanel, samt visa detaljerad sidinformation i listvyn.

![Innehållsträd](/help/sites-cloud/authoring/assets/content-tree.png)

>[!NOTE]
>
>När du har markerat en post i hierarkin kan du använda piltangenterna för att snabbt navigera i hierarkin.
>
>Mer information finns i [kortkommandona](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md).

### Tidslinje {#timeline}

Tidslinjen kan användas för att visa och/eller initiera händelser som har inträffat i den valda resursen. Om du vill öppna tidslinjekolumnen använder du järnvägsväljaren:

![Tidslinjeträd](/help/sites-cloud/authoring/assets/timeline.png)

I tidslinjekolumnen kan du:

* Visa olika händelser för ett valt objekt.

   * Händelsetyperna kan väljas i listrutan:

      * Kommentarer
      * [Anteckningar](/help/sites-cloud/authoring/fundamentals/annotations.md)
      * [Verksamhet](/help/sites-cloud/authoring/personalization/activities.md)
      * [Launches](/help/sites-cloud/authoring/launches/overview.md)
      * [Versioner](/help/sites-cloud/authoring/features/page-versions.md)
      * [Arbetsflöden](/help/sites-cloud/authoring/workflows/overview.md)
         * Med undantag för tillfälliga arbetsflöden eftersom ingen historikinformation sparas för dessa <!--With the exception of [transient workflows](/help/sites-developing/workflows.md#transient-workflows) as no history information is saved for these-->
      * Visa alla

* Lägg till/visa kommentarer om det markerade objektet. Rutan **Kommentar** visas längst ned i händelselistan. Om du skriver en kommentar följt av Retur registreras kommentaren. Den visas när **Kommentarer** eller **Visa alla** markeras.

* Specifika konsoler har ytterligare funktioner. I Platskonsolen kan du till exempel:

   * [Spara en version](/help/sites-cloud/authoring/features/page-versions.md)
   * [Starta ett arbetsflöde](/help/sites-cloud/authoring/workflows/applying.md)

Dessa alternativ är tillgängliga via markeringen bredvid **Kommentar**-fältet.

![Kommentarsfält](/help/sites-cloud/authoring/assets/comments.png)

### Referenser {#references}

**** Referenser visar alla anslutningar till den valda resursen. I konsolen **Platser** [referenser](/help/sites-cloud/authoring/fundamentals/environment-tools.md#references) för sidor visas till exempel:

* [Startar](/help/sites-cloud/authoring/launches/overview.md#launches-in-references-sites-console)
* Live-kopior<!--[Live copies](/help/sites-administering/msm-livecopy-overview.md#openingthelivecopyoverviewfromreferences)-->
* Språkkopior<!--[Language copies](/help/sites-administering/tc-prep.md#seeing-the-status-of-language-roots)-->
* Innehållsreferenser:

   * Länkar från andra sidor till den markerade sidan
   * Innehåll som lånats från och/eller lånats ut till den valda sidan av referenskomponenten

![Exempel på referenser](/help/sites-cloud/authoring/assets/references-example.png)

### Filter {#filter}

Då öppnas en panel som liknar [sök](/help/sites-cloud/authoring/getting-started/search.md) med rätt platsfilter inställda så att du kan filtrera innehållet ytterligare.

![Exempel på filter](/help/sites-cloud/authoring/assets/filter.png)

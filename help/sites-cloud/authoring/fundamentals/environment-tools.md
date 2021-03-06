---
title: Redigeringsmiljö och -verktyg
description: I redigeringsmiljön i AEM finns olika sätt att ordna och redigera ditt innehåll
exl-id: cc3bd4cf-93bd-429d-9a2a-4a02a7b42f7c
source-git-commit: f9a122f27ab1e2dc8ba429ce9048e3eab0509db9
workflow-type: tm+mt
source-wordcount: '2154'
ht-degree: 12%

---

# Redigeringsmiljö och -verktyg {#authoring-the-environment-and-tools}

I redigeringsmiljön i AEM finns olika sätt att ordna och redigera ditt innehåll. Verktygen som tillhandahålls är tillgängliga från olika konsoler och sidredigerare.

## Hantera din webbplats {#managing-your-site}

Med **Sites**-konsolen kan du navigera och hantera webbplatsen med hjälp av sidhuvudsfältet, verktygsfältet, åtgärdsikonerna (som gäller för den valda resursen), vägbeskrivningar och, om det är valt, sekundära rutor (till exempel tidslinje och referenser).

Till exempel kolumnvy:

![Kolumnvy](/help/sites-cloud/authoring/assets/column-view.png)

## Redigera sidinnehåll {#editing-page-content}

Du kan redigera en sida med sidredigeraren. Till exempel:

`http://<host>:<port>/editor.html/content/wknd/en/sports/la-skateparks.html`

![Page Editor](/help/sites-cloud/authoring/assets/page-editor.png)

>[!NOTE]
>
>Första gången du öppnar en sida för redigering visas en serie bilder med en genomgång av funktionerna.
>
>Du kan när som helst hoppa över genomgången och upprepa den genom att välja **Sidinformation** -menyn.

## Få hjälp {#accessing-help}

När du redigerar en sida **Hjälp** kan nås från:

* The [**Sidinformation**](/help/sites-cloud/authoring/fundamentals/page-properties.md#page-properties) väljaren som visar introduktionsbilderna (som visas första gången du öppnar redigeraren)
* The [konfiguration](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-toolbar) för specifika komponenter (med ? ikonen i dialogrutans verktygsfält), som visar sammanhangsberoende hjälp

Ytterligare [hjälprelaterade resurser är tillgängliga från konsoler](/help/sites-cloud/authoring/getting-started/basic-handling.md#accessing-help).

## Komponentbläddraren {#components-browser}

Komponenterna utgör byggstenarna i AEM. Du placerar flera komponenter på en sida och konfigurerar deras alternativ för att skapa din innehållssida med AEM.

Komponentwebbläsaren visar alla komponenter som är tillgängliga för användning på den aktuella sidan. Dessa kan dras till rätt plats och sedan redigeras för att lägga till ditt innehåll.

Komponentläsaren är en flik i sidopanelen (tillsammans med [resursläsaren](#assets-browser) och [innehållsträdet](#content-tree)). Om du vill öppna (eller stänga) sidopanelen använder du ikonen längst upp till vänster i verktygsfältet:

![Växla sida](/help/sites-cloud/authoring/assets/side-panel-toggle.png)

När du öppnar sidopanelen öppnas den från vänster sida (välj **Komponenter** tabb om det behövs). När du är öppen kan du bläddra igenom alla komponenter som är tillgängliga för sidan.

Det faktiska utseendet och hanteringen beror på vilken enhetstyp du använder:

* **Mobil enhet (t.ex. iPad)**

   Komponentwebbläsaren täcker hela sidan som redigeras.

   Om du vill lägga till en komponent på sidan trycker du på och håller ned den nödvändiga komponenten och flyttar den åt höger. Komponentwebbläsaren stängs och sidan visas igen, där du kan placera komponenten.

   ![Komponentbläddraren på mobilen](/help/sites-cloud/authoring/assets/component-browser-mobile.png)

* **Skrivbordsenhet**

   Komponentwebbläsaren öppnas till vänster i fönstret.

   Om du vill lägga till en komponent på sidan klickar du på den önskade komponenten och drar den till önskad plats.

   ![Komponentbläddraren på skrivbordet](/help/sites-cloud/authoring/assets/component-browser-desktop.png)

   Komponenterna representeras av

   * Komponentnamn
   * Komponentgrupp (i grått)
   * Ikon eller förkortning
      * Standardkomponentens ikoner är monokroma.
      * Förkortningar är alltid de två första tecknen i komponentnamnet.

   I det övre verktygsfältet i **Komponenter** webbläsare:

   * Filtrera komponenter efter namn.
   * Begränsa visningen till en viss grupp med listrutan.

   Om du vill ha en mer detaljerad beskrivning av komponenten kan du klicka eller trycka på informationsikonen bredvid komponenten i **komponentläsaren** (om den är tillgänglig). För **Innehållsfragment**:

   ![Information om komponentwebbläsare](/help/sites-cloud/authoring/assets/component-browser-information.png)

   Mer information om de komponenter som finns tillgängliga finns i [Komponentkonsol](/help/sites-cloud/authoring/features/components-console.md).

>[!NOTE]
>
>En mobil enhet identifieras när bredden är mindre än 1 024 pixlar. Detta kan också vara fallet för ett litet skrivbordsfönster.

## Resursläsaren {#assets-browser}

Resursläsaren visar alla [resurser](/help/assets/home.md) som är tillgängliga för direkt användning på den aktuella sidan.

Resursläsaren är en flik i sidopanelen tillsammans med [komponentläsaren](#components-browser) och [innehållsträdet](#content-tree). Om du vill öppna eller stänga sidopanelen använder du ikonen längst upp till vänster i verktygsfältet:

![Växla sida](/help/sites-cloud/authoring/assets/side-panel-toggle.png)

När du öppnar sidopanelen öppnas den från vänster sida. Välj **Resurser** tabba vid behov.

![Knappen Resursläsare](/help/sites-cloud/authoring/assets/assets-browser-button.png)

När resursläsaren är öppen kan du bläddra bland alla resurser som är tillgängliga för sidan. Oändlig rullning används för att expandera listan vid behov.

![Resursläsaren](/help/sites-cloud/authoring/assets/assets-browser.png)

Om du vill lägga till en resurs på sidan markerar och drar du den till önskad plats. Detta kan vara:

* En befintlig komponent av lämplig typ.
   * Du kan till exempel dra en resurs av typen bild till en bildkomponent.
* A [platshållare](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-placeholder) i styckesystemet för att skapa en ny komponent av lämplig typ.
   * Du kan till exempel dra en resurs av typen bild till styckesystemet för att skapa en bildkomponent.

>[!NOTE]
>
>Detta är tillgängligt för specifika resurser och komponenttyper. Se [Infoga en komponent med Resursläsaren](/help/sites-cloud/authoring/fundamentals/editing-content.md#inserting-a-component-using-the-assets-browser) för mer information.

I det övre verktygsfältet i resursläsaren kan du filtrera resurserna efter:

* Namn
* Bana
* Resurstyp som bilder, videoklipp, dokument, stycken, innehållsfragment och Experience Fragments
* Resursegenskaper som orientering och stil
   * Endast tillgängligt för vissa tillgångstyper

Det faktiska utseendet och hanteringen beror på vilken enhetstyp du använder:

* **Mobil enhet**

   Resursläsaren täcker hela sidan som redigeras.

   Om du vill lägga till en resurs på sidan håller du pekaren över den resurs du behöver och sedan flyttar den åt höger. Resursläsaren stängs och sidan visas igen, där du kan lägga till resursen i den nödvändiga komponenten.

   ![Resursläsaren på mobilen](/help/sites-cloud/authoring/assets/assets-browser-mobile.png)

* **Skrivbordsenhet**

   Resursläsaren öppnas till vänster i fönstret.

   Om du vill lägga till en resurs på sidan klickar du på den önskade resursen och drar den till önskad komponent eller plats.

   ![Resursläsaren på skrivbordet](/help/sites-cloud/authoring/assets/assets-browser-desktop.png)

>[!NOTE]
>
>En mobil enhet upptäcks när bredden är mindre än 1024px. dvs. även i ett litet skrivbordsfönster.

Om du snabbt behöver göra en ändring i en resurs kan du starta [tillgångsredigerare](/help/assets/manage-digital-assets.md) direkt från resursläsaren genom att klicka på redigeringsikonen som visas bredvid resursens namn.

![Knappen Resursredigering](/help/sites-cloud/authoring/assets/asset-edit-button.png)

## Innehållsträd {#content-tree}

The **Innehållsträd** ger en översikt över alla komponenter på sidan i en hierarki så att du snabbt kan se hur sidan är uppbyggd.

Innehållsträdet är en flik i sidopanelen (tillsammans med komponenterna och resursläsaren). Om du vill öppna (eller stänga) sidopanelen använder du ikonen längst upp till vänster i verktygsfältet:

![Knappen Innehållsträd](/help/sites-cloud/authoring/assets/content-tree-button.png)

När du öppnar sidopanelen öppnas den (från vänster sida). Välj **Innehållsträd** tabba vid behov. När den är öppen kan du se en trädvyrepresentation av sidan eller mallen, så att det blir lättare att förstå hur innehållet är hierarkiskt strukturerat. På en komplex sida är det dessutom enklare att växla mellan sidans komponenter.

![Innehållsträd](/help/sites-cloud/authoring/assets/content-tree-editor.png)

En sida kan enkelt bestå av många av samma typ av komponenter, så innehållsträdet (komponentträdet) visar beskrivande text (i grått) efter komponenttypens namn (i svart). Den beskrivande texten kommer från vanliga egenskaper för komponenten, t.ex. rubrik eller text.

Komponenttyper visas på användarspråket, medan komponentbeskrivningstexten kommer från sidspråket.

Om du klickar på markören bredvid en komponent kommer den nivån att komprimeras eller utökas.

![Utökning av Content Tree Chevron](/help/sites-cloud/authoring/assets/content-tree-chevron.png)

Om du klickar på komponenten markeras komponenten i sidredigeraren. Vilka åtgärder som är tillgängliga beror på sidstatus:

* En grundsida:

   ![Innehållsträdet markerat](/help/sites-cloud/authoring/assets/content-tree-highlighted.png)

   Komponenterna på en bassida har de vanliga alternativen.

   Om komponenten som du klickar på i trädet är redigerbar visas en skiftnyckelsikon till höger om namnet. Om du klickar på den här ikonen öppnas redigeringsdialogrutan för komponenten.

   ![Redigeringsknapp för innehållsträd](/help/sites-cloud/authoring/assets/content-tree-edit.png)

* En sida som är en del av en [livecopy](/help/sites-cloud/administering/msm/overview.md), där komponenter ärvs från en annan sida.

>[!NOTE]
>
>Innehållsträdet är inte tillgängligt om du redigerar en sida på en mobil enhet (om webbläsarbredden är mindre än 1024px).

## Fragment - Associerad innehållsläsare {#fragments-associated-content-browser}

Om sidan innehåller innehållsfragment får du även åtkomst till [webbläsare för associerat innehåll](/help/sites-cloud/authoring/fundamentals/content-fragments.md#using-associated-content).

## Referenser {#references}

**Referenser** visar anslutningar till den valda sidan:

* Ritningar
* Launches
* Live-kopior
* Språkversioner
* Inkommande länkar
* Användning av referenskomponenten: lånat och lånat innehåll

Öppna den nödvändiga konsolen, navigera till den nödvändiga resursen och öppna **Referenser** med:

![Alternativet Referenser](/help/sites-cloud/authoring/assets/references.png)

[Välj önskad resurs](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources) om du vill visa en lista över referenstyper som är relevanta för den resursen:

![Referensinformation](/help/sites-cloud/authoring/assets/references-detail.png)

Välj lämplig referenstyp för mer information. I vissa situationer är ytterligare åtgärder tillgängliga när du väljer en specifik referens, bland annat:

* **Inkommande länkar**, innehåller en lista med sidor som refererar till sidan, tillsammans med direktåtkomst till **Redigera** en av dessa sidor när du väljer en specifik länk
* Förekomster av lånat och lånat innehåll med **Referens** -komponent, härifrån kan du navigera till den refererande/refererade sidan
* [Startar](/help/sites-cloud/authoring/launches/overview.md), ger åtkomst till relaterade starter
* [Live-kopior](/help/sites-cloud/administering/msm/overview.md) visar sökvägarna för alla live-kopior som baseras på den valda resursen.
* [Blueprint](/help/sites-cloud/administering/msm/best-practices.md), innehåller information och olika åtgärder
* [Språkkopior](/help/sites-cloud/administering/translation/managing-projects.md#creating-translation-projects-using-the-references-panel), innehåller information och olika åtgärder

## Händelser - Tidslinje {#events-timeline}

För lämpliga resurser (t.ex. sidor från **Webbplatser** konsol, eller resurser från **Resurser** konsolen) [tidslinjen kan användas för att visa den senaste aktiviteten för markerade objekt](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline).

Öppna den nödvändiga konsolen, navigera till den nödvändiga resursen och öppna **Tidslinje**, med:

![Tidslinje, alternativ](/help/sites-cloud/authoring/assets/timeline.png)

[Välj önskad resurs](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)sedan antingen **Visa alla** eller **Verksamhet** om du vill visa alla senaste åtgärder för de valda resurserna:

![Information om tidslinjen](/help/sites-cloud/authoring/assets/timeline-detail.png)

## Sidinformation {#page-information}

Sidinformation (equalizer-ikonen) öppnar en meny som även innehåller information om den senaste redigeringen och det senaste dokumentet. Beroende på sidans egenskaper, dess plats och din instans kan det finnas fler eller färre alternativ:

![Sidinformation, alternativ](/help/sites-cloud/authoring/assets/page-information.png)

* [Öppna egenskaper](/help/sites-cloud/authoring/fundamentals/page-properties.md)
* [Utrullningssida](/help/sites-cloud/administering/msm/overview.md#msm-from-the-ui)
* [Starta arbetsflöde](/help/sites-cloud/authoring/workflows/applying.md#starting-a-workflow-from-the-page-editor)
* [Lås sida](/help/sites-cloud/authoring/fundamentals/editing-content.md#locking-a-page)
* [Publicera sida](/help/sites-cloud/authoring/fundamentals/publishing-pages.md#publishing-pages-1)
* [Avpublicera sida](/help/sites-cloud/authoring/fundamentals/publishing-pages.md#unpublishing-pages)
* [Redigera mall](/help/sites-cloud/authoring/features/templates.md)
* [Visa som publicerad](/help/sites-cloud/authoring/fundamentals/editing-content.md#view-as-published)
* [Visa i Admin](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)
* [Hjälp](/help/sites-cloud/authoring/getting-started/basic-handling.md#accessing-help)
* [Promote Launch](/help/sites-cloud/authoring/launches/promoting.md) (endast om sidan är en startsida)

Dessutom **Sidinformation** kan ge tillgång till analyser och rekommendationer, när så är lämpligt.

## Sidlägen {#page-modes}

Det finns olika lägen när du redigerar en sida som tillåter olika åtgärder:

* [Redigera](/help/sites-cloud/authoring/fundamentals/editing-content.md) - det läge som ska användas när sidinnehållet redigeras.
* [Layout](/help/sites-cloud/authoring/features/responsive-layout.md) - gör att du kan skapa och redigera din responsiva layout beroende på enhet (om sidan är baserad på en layoutbehållare)
* [Målinriktning](/help/sites-cloud/authoring/personalization/targeted-content.md) - öka innehållets relevans genom målinriktning och mätning i alla kanaler.
* [Timewarp](/help/sites-cloud/authoring/features/page-versions.md#timewarp) - gör att du kan visa ett sidläge vid en viss tidpunkt.
* [Live Copy-status](/help/sites-cloud/authoring/fundamentals/editing-content.md#live-copy-status) - ger dig en snabb översikt över live-kopians status och vilka komponenter som ärvs/inte ärvs.
* [Utvecklarläge](/help/implementing/developing/tools/developer-mode.md)
* [Förhandsgranska](/help/sites-cloud/authoring/fundamentals/editing-content.md#previewing-pages) - används för att visa sidan så som den kommer att visas i publiceringsmiljön, eller navigera med hjälp av länkar i innehållet.
* [Anteckna](/help/sites-cloud/authoring/fundamentals/annotations.md) - används för att lägga till eller visa anteckningar på sidan.

Du kommer åt dem med hjälp av ikonerna i det övre högra hörnet. Den faktiska ikonen ändras för att återspegla det läge som du använder för närvarande:

![Sidlägen](/help/sites-cloud/authoring/assets/page-modes.png)

>[!NOTE]
>
>* Beroende på sidans egenskaper kanske vissa lägen inte är tillgängliga.
>* Åtkomst till vissa lägen kräver lämplig behörighet/behörighet.
>* Utvecklarläget är inte tillgängligt på mobila enheter på grund av utrymmesbegränsningar.
>* Det finns ett [kortkommando](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md) (`Ctrl-Shift-M`) som du kan använda för att växla mellan **förhandsvisning** och det aktuella läget (t.ex. **Redigera** eller **Layout**).
>


## Banmarkering {#path-selection}

När du redigerar är det ofta nödvändigt att välja en annan resurs, till exempel när du definierar en länk till en annan sida eller resurs eller markerar en bild. Markera en bana enkelt genom att [sökvägsfält](#path-fields) erbjuder automatisk komplettering och [sökvägsläsare](#path-browser) ger mer robust markering.

### Sökvägsfält {#path-fields}

Det exempel som används här för att illustrera är bildkomponenten. Mer information om hur du använder och redigerar komponenter finns i [Komponenter för sidredigering](/help/sites-cloud/authoring/fundamentals/components.md).

Sökvägsfält har automatisk komplettering och framåtblickande funktioner som gör det enklare att hitta en resurs.

Klicka på **Öppna dialogrutan Markering** knappen i sökvägsfältet öppnar [sökvägsläsare](#path-browser) för mer detaljerade markeringsalternativ.

![Öppna dialogrutan Markering, knapp](/help/sites-cloud/authoring/assets/open-selection-dialog-button.png)

Du kan också börja skriva i sökvägsfältet och AEM erbjuder matchande sökvägar när du skriver.

![Öppna dialogrutan Markering, knapp](/help/sites-cloud/authoring/assets/path-selection-completion.png)

### Sökvägsläsaren {#path-browser}

Sökvägsläsaren är ordnad som [kolumnvy](/help/sites-cloud/authoring/getting-started/basic-handling.md#column-view) av webbplatskonsolen, vilket ger ett mer detaljerat urval av resurser.

![Sökvägsläsaren](/help/sites-cloud/authoring/assets/path-browser.png)

* När en resurs har valts **Välj** knappen längst upp till höger i dialogrutan aktiveras. Klicka eller tryck för att bekräfta markeringen eller **Avbryt** för att avbryta.
* Om det går att välja flera resurser aktiveras även knappen **Välj** när du väljer en resurs och antalet valda resurser läggs till i det övre högra hörnet fönstret. Klicka på **X** bredvid talet för att avmarkera alla.
* När du navigerar genom trädet visas platsen i de synliga kolumnerna högst upp i dialogrutan. Dessa vägbeskrivningar kan också användas för att snabbt hoppa in i resurshierarkin.
* Du kan när som helst använda sökfältet högst upp i dialogrutan. Klicka på **X** i sökfältet för att rensa sökningen.
* Om du vill begränsa sökningen kan du visa filteralternativen och filtrera resultaten baserat på en viss bana.

   ![Alternativet Filter](/help/sites-cloud/authoring/assets/filters-option.png)

## Kortkommandon {#keyboard-shortcuts}

Olika [kortkommandon](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md) är tillgängliga.

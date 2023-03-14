---
title: Snabbstartsguide till redigering av sidor
description: En snabb guide på hög nivå som hjälper dig att komma igång med att skapa sidinnehåll
exl-id: d37c9b61-7382-4bf6-8b90-59726b871264
source-git-commit: 07702fbebc768ee877d68219eff5551b09c7ff3e
workflow-type: tm+mt
source-wordcount: '1585'
ht-degree: 4%

---

# Snabbstartsguide till redigering av sidor {#quick-guide-to-authoring-pages}

Det här dokumentet är avsett som en snabbstartguide på hög nivå för de viktigaste redigeringsåtgärderna för sidor i AEM. Det här dokumentet:

* Är inte avsedd som omfattande täckning.
* Tillhandahåller länkar till detaljerad dokumentation.

Mer information om redigering med AEM finns i:

* [Designbegrepp](/help/sites-cloud/authoring/getting-started/concepts.md)
* [Grundläggande hantering](/help/sites-cloud/authoring/getting-started/basic-handling.md)

## Några snabba tips {#a-few-quick-hints}

Innan du börjar med snabbstartsguiden finns det en liten samling allmänna tips och tips som du bör tänka på, som är uppdelade i olika delar av redigeringssystemet.

### I platskonsolen {#sites-console}

* Skapa-knapp

   * Den här knappen är tillgänglig i många konsoler - de alternativ som visas är sammanhangsberoende så att de kan variera beroende på scenario.

* Ordna om sidor

   * Detta kan göras i [Listvy](/help/sites-cloud/authoring/getting-started/basic-handling.md#list-view). Ändringarna används och visas i andra vyer.

### Sidredigering {#page-authoring}

* Navigera i länkar

   * **Länkar är inte tillgängliga för navigering** när du är **Redigera** läge. Om du vill navigera med länkar måste du [förhandsgranska sidan](/help/sites-cloud/authoring/fundamentals/editing-content.md#previewing-pages) med antingen

      * [Förhandsgranskningsläge](/help/sites-cloud/authoring/fundamentals/editing-content.md#preview-mode)
      * [Visa som publicerad](/help/sites-cloud/authoring/fundamentals/editing-content.md#view-as-published)

* Versioner startas/skapas inte från sidredigeraren. Detta görs nu från **Webbplatser** konsol (via **Skapa** eller [Tidslinje](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline) för en vald resurs).

>[!NOTE]
>
>Det finns ett antal kortkommandon som kan underlätta redigeringen.
>
>* [Kortkommandon vid sidredigering](/help/sites-cloud/authoring/fundamentals/keyboard-shortcuts.md)
>* [Kortkommandon för konsoler](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md)


### Hitta din sida {#finding-your-page}

Det finns olika aspekter av att hitta en sida. kan du navigera och/eller söka:

1. Öppna **Webbplatser** konsol (med **Webbplatser** i [Global navigering](/help/sites-cloud/authoring/getting-started/basic-handling.md#global-navigation) - den här utlöses (nedrullningsbar) när du väljer länken Adobe Experience Manager (överst till vänster).

1. Navigera nedåt i trädet genom att trycka/klicka på lämplig sida. Hur sidresurserna visas beror på vilken vy du använder - [Kort, lista eller kolumn](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources):

   ![Visa listrutan för val](/help/sites-cloud/authoring/assets/views.png)

1. Navigera uppåt i trädet med [sidhuvudet](/help/sites-cloud/authoring/getting-started/basic-handling.md#the-header)som gör att du kan gå tillbaka till den valda platsen:

   ![Breadcrumb-listruta](/help/sites-cloud/authoring/assets/breadcrumb.png)

1. Du kan också [Sök](/help/sites-cloud/authoring/getting-started/search.md) för en sida. Du kan välja din sida bland de resultat som visas.

   ![Sökfält](/help/sites-cloud/authoring/assets/search.png)

### Skapa en ny sida {#creating-a-new-page}

Till [skapa en ny sida](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#creating-a-new-page):

1. [Navigera till platsen](#finding-your-page) där du vill skapa den nya sidan.
1. Använd **Skapa** ikon och sedan markera **Sida** från listan:

   ![Knappen Skapa](/help/sites-cloud/authoring/assets/create.png)

1. Då öppnas guiden som vägleder dig genom att samla in den information som behövs när [skapa en ny sida](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#creating-a-new-page). Följ instruktionerna på skärmen.

### Välja sida för ytterligare åtgärd {#selecting-your-page-for-further-action}

Du kan markera en sida så att du kan utföra en åtgärd på den. När du väljer en sida uppdateras verktygsfältet automatiskt så att de åtgärder som är relevanta för resursen visas.

Hur du väljer en sida beror på vilken vy du använder i konsolen:

1. Kolumnvy:

   * Tryck/klicka på miniatyrbilden för resursen - miniatyrbilden kommer att överlappas med en bock för att visa att den har markerats.

1. Listvy:

   * Tryck/klicka på miniatyrbilden för resursen - miniatyrbilden kommer att överlappas med en bock för att visa att den har markerats.

1. Kortvy:

   * Ange markeringsläge med [välja nödvändig resurs](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources). Hur du gör detta beror på din enhet:

      * På en mobil enhet: tryck och håll ned kortet
      * På en stationär enhet: använder [snabbåtgärd](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions) som representeras av tickningsikonen:
   * Kortet kommer att förses med en bock som visar att sidan har valts.

   ![Exempelkort](/help/sites-cloud/authoring/assets/card.png)

### Snabbåtgärder (endast kortvyn/skrivbordet) {#quick-actions-card-view-desktop-only}

[Snabbåtgärder](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions) är tillgängliga:

1. [Navigera till sidan](#finding-your-page) du vill vidta åtgärder för.
1. Håll muspekaren över kortet som representerar den resurs du behöver. Snabbåtgärderna visas:

   ![Kortåtgärder](/help/sites-cloud/authoring/assets/card-actions.png)

### Redigera sidinnehåll {#editing-your-page-content}

Så här redigerar du sidan:

1. [Navigera till sidan](#finding-your-page) du vill redigera.
1. [Öppna sidan för redigering](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#opening-a-page-for-editing) med ikonen Redigera (penna):

   ![Knappen Redigera](/help/sites-cloud/authoring/assets/edit.png)

   Du kommer åt detta från antingen:

   * [Snabbåtgärder (endast kortvyn/skrivbordet)](#quick-actions-card-view-desktop-only) för lämplig resurs.
   * Verktygsfältet när [sidan har valts](#selecting-your-page-for-further-action).

1. När redigeraren öppnas kan du:

   * [Lägga till en ny komponent på sidan](/help/sites-cloud/authoring/fundamentals/editing-content.md#inserting-a-component) av:

      * Öppna sidpanelen
      * Välja fliken Komponenter (på [komponentwebbläsare](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser))
      * Dra den önskade komponenten till sidan.

      Sidpanelen kan öppnas (och stängas) med:

      ![Växlingsknapp för sidopanelen](/help/sites-cloud/authoring/assets/side-panel-toggle.png)

   * [Redigera innehållet i en befintlig komponent](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-toolbar) på sidan:

      * Öppna komponentens verktygsfält genom att trycka eller klicka. Använd **Redigera** (penna) för att öppna dialogrutan.
      * Öppna komponentens direktredigerare genom att trycka och hålla ned eller dubbelklicka. De tillgängliga åtgärderna visas (för vissa komponenter är detta ett begränsat urval).
      * Om du vill visa alla tillgängliga åtgärder går du till helskärmsläge med:

         ![Helskärmsknapp](/help/sites-cloud/authoring/assets/full-screen.png)
   * [Konfigurera egenskaperna för en befintlig komponent](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-edit-dialog)

      * Öppna komponentens verktygsfält genom att trycka eller klicka. Använd **Konfigurera** (skiftnyckel) för att öppna dialogrutan.
   * [Flytta en komponent](/help/sites-cloud/authoring/fundamentals/editing-content.md#moving-a-component) antingen:

      * Dra den önskade komponenten till dess nya plats.
      * Öppna komponentens verktygsfält genom att trycka eller klicka. Använd **Klipp ut** sedan **Klistra in** ikoner där det behövs.
   * [Kopiera (och klistra in)](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-toolbar) en komponent:

      * Öppna komponentens verktygsfält genom att trycka eller klicka. Använd **Kopiera** sedan **Klistra in** ikoner efter behov.
   >[!NOTE]
   >
   >Du kan **Klistra in** -komponenter till antingen samma sida eller en annan sida. Om du klistrar in på en annan sida som redan var öppen före klipp ut/kopiera-åtgärden, måste sidan uppdateras.

   * [Ta bort](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-toolbar) en komponent:

      * Öppna komponentens verktygsfält med tryck eller klicka och använd sedan **Ta bort** ikon.
   * [Lägg till anteckningar](/help/sites-cloud/authoring/fundamentals/annotations.md#annotations) till sidan:

      * Välj **Anteckna** läge (pratbubblarikon). Lägg till anteckningar med **Lägg till anteckning** (plus) ikon. Avsluta anteckningsläget med X överst till höger.

         ![Anteckningsknapp](/help/sites-cloud/authoring/assets/annotations.png)
   * [Förhandsgranska en sida](/help/sites-cloud/authoring/fundamentals/editing-content.md#preview-mode) (för att se hur det kommer att se ut i publiceringsmiljön)

      * Välj **Förhandsgranska** i verktygsfältet.
   * Återgå till redigeringsläget (eller välj ett annat läge) med **Redigera** nedrullningsbar väljare.

   >[!NOTE]
   >
   >Navigera med hjälp av länkar i innehållet som du måste använda [Förhandsgranskningsläge](/help/sites-cloud/authoring/fundamentals/editing-content.md#preview-mode).

### Redigera sidegenskaperna {#editing-the-page-properties}

Det finns två (huvudsakliga) metoder för [redigera sidegenskaper](/help/sites-cloud/authoring/fundamentals/page-properties.md):

* Från **Webbplatser** konsol:

   1. [Navigera till sidan](#finding-your-page) du vill publicera.
   1. Välj **Egenskaper** ikon från antingen

      * [Snabbåtgärder (endast kortvyn/skrivbordet)](#quick-actions-card-view-desktop-only) för lämplig resurs.
      * Verktygsfältet när [sidan har valts](#selecting-your-page-for-further-action).

      ![Egenskapsknapp](/help/sites-cloud/authoring/assets/properties.png)

   1. Sidegenskaperna visas. Du kan göra nödvändiga uppdateringar och sedan använda Spara för att behålla dessa


* När [redigera sidan](#editing-your-page-content):

   1. Öppna **Sidinformation** -menyn.
   1. Välj **Öppna egenskaper** för att öppna dialogrutan för redigering av egenskaperna.

      ![Sidinformation, knapp](/help/sites-cloud/authoring/assets/page-information.png)

### Publicera din sida (eller avpublicera) {#publishing-your-page-or-unpublishing}

Det finns två huvudmetoder för [publicera din sida](/help/sites-cloud/authoring/fundamentals/publishing-pages.md) (och även avpublicering):

* Från **Webbplatser** konsol:

   1. [Navigera till sidan](#finding-your-page) du vill publicera.
   1. Välj **Snabbpublicering** ikon från antingen

      * [Snabbåtgärder (endast kortvyn/skrivbordet)](#quick-actions-card-view-desktop-only) för lämplig resurs.
      * Verktygsfältet när [sidan har valts](#selecting-your-page-for-further-action) (ger även tillgång till [Publicera senare](/help/sites-cloud/authoring/fundamentals/publishing-pages.md)).

      ![Knappen Snabbpublicering](/help/sites-cloud/authoring/assets/quick-publish.png)


* När [redigera sidan](#editing-your-page-content):

   1. Öppna **Sidinformation** -menyn.
   1. Välj **Publicera sida**.

* Du kan bara avpublicera en sida från konsolen via alternativet **Hantera publikation**, som bara är tillgängligt i verktygsfältet (inte via snabbåtgärderna).

   ![Knappen Hantera publikation](/help/sites-cloud/authoring/assets/manage-publication.png)

   The **Avpublicera sida** är fortfarande tillgängligt via **Sidinformation** i redigeraren.

   Se [Publicera sidor](/help/sites-cloud/authoring/fundamentals/publishing-pages.md#unpublishing-pages) för mer information.

### Flytta, kopiera och klistra in eller ta bort sidan {#move-copy-and-paste-or-delete-your-page}

Alla dessa åtgärder kan utlösas av:

1. [Navigera till sidan](#finding-your-page) du vill flytta, kopiera och klistra in eller ta bort.
1. Välj ikonen för kopiera (och sedan klistra in), flytta eller ta bort efter behov på något av följande sätt:

   * [Snabbåtgärder (endast kortvyn/skrivbordet)](#quick-actions-card-view-desktop-only) för den resurs som krävs.
   * Verktygsfältet när [sidan har valts](#selecting-your-page-for-further-action).

   Sedan, beroende på vad du gör:

   * [Kopiera](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#copying-and-pasting-a-page):

      * Du måste sedan navigera till den nya platsen och klistra in.
   * [Flytta](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#moving-or-renaming-a-page):

      * Guiden öppnas och samlar in den information som behövs för att flytta sidan. Följ instruktionerna på skärmen.
   * [Ta bort](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#deleting-a-page):

      * Du ombeds bekräfta åtgärden.
   >[!NOTE]
   >
   >Borttagning är inte tillgängligt som snabbåtgärd.

### Låser sidan (låser upp) {#locking-your-page-then-unlocking}

[När du låser en sida](/help/sites-cloud/authoring/fundamentals/editing-content.md#locking-a-page) kan andra författare inte arbeta med den. Ikonen/knappen Lås (och Lås upp) finns:

* Verktygsfältet när [sidan har valts](#selecting-your-page-for-further-action).
* The [Listruta för sidinformation](#editing-the-page-properties) när du redigerar en sida.
* Sidans verktygsfält när du redigerar en sida (när sidan är låst)

Låsikonen ser till exempel ut så här:

![Knappen Lås](/help/sites-cloud/authoring/assets/lock.png)

### Åtkomst till sidreferenser {#accessing-page-references}

[Snabb åtkomst till referenser](/help/sites-cloud/authoring/fundamentals/environment-tools.md#references) till/från en sida är tillgänglig i Reference Rail.

1. Välj **Referenser** med verktygsfältsikonen (antingen före eller efter [markera sidan](#selecting-your-page-for-further-action)):

   ![Alternativ för vyn Referenser](/help/sites-cloud/authoring/assets/references.png)

   En lista över referenstyper visas:

   ![Referensvy](/help/sites-cloud/authoring/assets/references-list.png)

1. Tryck/klicka på den typ av referens som krävs för att visa mer information och (vid behov) vidta ytterligare åtgärder.

### Skapa en version av din sida {#creating-a-version-of-your-page}

Skapa en [version](/help/sites-cloud/authoring/features/page-versions.md) på sidan:

1. Om du vill öppna tidslinjen markerar du **[Tidslinje](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline)** med verktygsfältsikonen (antingen före eller efter [markera sidan](#selecting-your-page-for-further-action)):

   ![Vyalternativ för tidslinje](/help/sites-cloud/authoring/assets/timeline.png)

1. Tryck/klicka på ellipsen längst ned till höger i kolumnen Tidslinje för att visa extra knappar, inklusive **Spara som version**.

   ![Tidslinjevy](/help/sites-cloud/authoring/assets/timeline-view.png)

1. Välj **Spara som version** sedan **Skapa**.

### Återställa/jämföra en version av sidan {#restoring-comparing-a-version-of-your-page}

Samma grundläggande funktion används när du återställer och/eller jämför versioner av sidan:

1. Välj **[Tidslinje](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline)** med verktygsfältsikonen (antingen före eller efter [markera sidan](#selecting-your-page-for-further-action)):

   ![Vyalternativ för tidslinje](/help/sites-cloud/authoring/assets/timeline.png)

   Om en version av sidan redan har sparats visas den i tidslinjen.

1. Tryck/klicka på den version som du vill återställa - då visas ytterligare åtgärdsknappar:

   * **Återgå till den här versionen**

      * Versionen återställs.
   * **Visa skillnader**

      * Sidan öppnas med skillnader (mellan de två versionerna) markerade.

---
title: Snabbstartsguide till framtagning av sidor
description: En snabb guide på hög nivå som hjälper dig att komma igång med att skapa sidinnehåll
exl-id: d37c9b61-7382-4bf6-8b90-59726b871264
source-git-commit: 0ad9f349c997c35862e4f571b4741ed4c0c947e2
workflow-type: tm+mt
source-wordcount: '1541'
ht-degree: 4%

---


# Snabbstartsguide till framtagning av sidor {#quick-guide-to-authoring-pages}

Det här dokumentet är avsett som en snabbstartguide på hög nivå för de viktigaste redigeringsåtgärderna för sidor i AEM. Det här dokumentet:

* Är inte avsedd som omfattande täckning.
* Tillhandahåller länkar till detaljerad dokumentation.

Mer information om redigering med AEM finns i:

* [Designbegrepp](/help/sites-cloud/authoring/getting-started/concepts.md)
* [Grundläggande hantering](/help/sites-cloud/authoring/getting-started/basic-handling.md)

{{edge-delivery-authoring}}

## Några snabba tips {#a-few-quick-hints}

Innan du börjar med snabbstartsguiden finns det en liten samling allmänna tips och tips som du bör tänka på, som är uppdelade i olika delar av redigeringssystemet.

### I platskonsolen {#sites-console}

* Skapa-knapp

   * Den här knappen är tillgänglig i många konsoler - de alternativ som visas är sammanhangsberoende så att de kan variera beroende på scenario.

* Ordna om sidor

   * Detta kan du göra i [listvyn](/help/sites-cloud/authoring/getting-started/basic-handling.md#list-view). Ändringarna används och visas i andra vyer.

### Sidredigering {#page-authoring}

* Navigera i länkar

   * **Länkar är inte tillgängliga för navigering** när du är i läget **Redigera**. Om du vill navigera med länkar måste du [förhandsgranska sidan](/help/sites-cloud/authoring/fundamentals/editing-content.md#previewing-pages) med hjälp av:

      * [Förhandsgranskningsläge](/help/sites-cloud/authoring/fundamentals/editing-content.md#preview-mode)
      * [Visa som publicerad](/help/sites-cloud/authoring/fundamentals/editing-content.md#view-as-published)

* Versioner startas/skapas inte från sidredigeraren. Detta görs nu från konsolen **Platser** (via **Skapa** eller [Tidslinje](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline) för en vald resurs).

>[!NOTE]
>
>Det finns flera kortkommandon som kan underlätta redigeringen.
>
>* [Kortkommandon vid sidredigering](/help/sites-cloud/authoring/fundamentals/keyboard-shortcuts.md)
>* [Kortkommandon för konsoler](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md)

### Hitta din sida {#finding-your-page}

Det finns olika aspekter av att hitta en sida. Du kan navigera och/eller söka efter:

1. Öppna konsolen **Platser** (med alternativet **Platser** i [Global navigering](/help/sites-cloud/authoring/getting-started/basic-handling.md#global-navigation) - detta aktiveras (nedrullningsbar) när du väljer länken Adobe Experience Manager (överst till vänster).

1. Navigera nedåt i trädet genom att trycka/klicka på lämplig sida. Hur sidresurserna visas beror på vilken vy du använder - [Kort, Lista eller Kolumn](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources):

   ![Listrutan Visa markering](/help/sites-cloud/authoring/assets/views.png)

1. Navigera uppåt i trädet med hjälp av [den synliga sökvägen i huvudet](/help/sites-cloud/authoring/getting-started/basic-handling.md#the-header), som gör att du kan gå tillbaka till den valda platsen:

   ![Listrutan Breadcrumb](/help/sites-cloud/authoring/assets/breadcrumb.png)

1. Du kan också [söka](/help/sites-cloud/authoring/getting-started/search.md) efter en sida. Du kan välja din sida bland de resultat som visas.

   ![Sökfält](/help/sites-cloud/authoring/assets/search.png)

### Skapa en ny sida {#creating-a-new-page}

Så här [skapar du en sida](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#creating-a-new-page):

1. [Navigera till platsen](#finding-your-page) där du vill skapa den nya sidan.
1. Använd ikonen **Skapa** och välj sedan **Sida** i listan:

   ![Knappen Skapa](/help/sites-cloud/authoring/assets/create.png)

1. Guiden som vägleder dig genom att samla in den information som behövs när [du skapar den nya sidan](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#creating-a-new-page) öppnas. Följ instruktionerna på skärmen.

### Välja sida för ytterligare åtgärd {#selecting-your-page-for-further-action}

Du kan markera en sida så att du kan agera på den. När du väljer en sida uppdateras verktygsfältet automatiskt så att de åtgärder som är relevanta för resursen visas.

Hur du väljer en sida beror på vilken vy du använder i konsolen:

1. Kolumnvy:

   * Markera miniatyrbilden för den resurs som du vill använda - miniatyrbilden överlappas med en bock som visar att den har markerats.

1. Listvy:

   * Markera miniatyrbilden för den resurs som du vill använda - miniatyrbilden överlappas med en bock som visar att den har markerats.

1. Kortvy:

   * Ange markeringsläge genom att [välja den nödvändiga resursen](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources). Hur du gör detta beror på din enhet:

      * På en mobil enhet: välj och håll ned kortet
      * Använd [snabbåtgärden](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions) som representeras av tickningsikonen på en stationär enhet:

   * Kortet är dolt med en bock som visar att sidan har valts.

   ![Exempelkort](/help/sites-cloud/authoring/assets/card.png)

### Snabbåtgärder (endast kortvyn/skrivbordet) {#quick-actions-card-view-desktop-only}

[Snabbåtgärder](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions) är tillgängliga:

1. [Navigera till sidan](#finding-your-page) som du vill arbeta med.
1. Håll muspekaren över kortet som representerar den resurs du behöver. Snabbåtgärderna visas:

   ![Kortåtgärder](/help/sites-cloud/authoring/assets/card-actions.png)

### Redigera sidinnehåll {#editing-your-page-content}

Så här redigerar du sidan:

1. [Navigera till sidan](#finding-your-page) som du vill redigera.
1. [Öppna sidan för redigering](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#opening-a-page-for-editing) med ikonen Redigera (penna):

   ![Knappen Redigera](/help/sites-cloud/authoring/assets/edit.png)

   Du kan komma åt detta från antingen:

   * [Snabbåtgärder (endast kortvyn/skrivbordet)](#quick-actions-card-view-desktop-only) för lämplig resurs.
   * Verktygsfältet när [sidan har valts](#selecting-your-page-for-further-action).

1. När redigeraren öppnas kan du:

   * [Lägg till en ny komponent på sidan](/help/sites-cloud/authoring/fundamentals/editing-content.md#inserting-a-component) genom att:

      * Öppna sidpanelen
      * Välja komponentfliken ([komponentwebbläsaren](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser))
      * Dra den önskade komponenten till sidan.

     Sidpanelen kan öppnas (och stängas) med:

     ![Växlingsknapp för sidopanelen](/help/sites-cloud/authoring/assets/side-panel-toggle.png)

   * [Redigera innehållet i en befintlig komponent](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-toolbar) på sidan:

      * Öppna komponentverktygsfältet med någon av markeringarna. Använd ikonen **Redigera** (penna) för att öppna dialogrutan.
      * Öppna komponentens in-place-redigerare genom att markera och hålla ned eller dubbelklicka. De tillgängliga åtgärderna visas (för vissa komponenter är det ett begränsat urval).
      * Om du vill visa alla tillgängliga åtgärder går du till helskärmsläge med:

        ![Helskärmsknapp](/help/sites-cloud/authoring/assets/full-screen.png)

   * [Konfigurera egenskaperna för en befintlig komponent](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-edit-dialog)

      * Öppna komponentverktygsfältet med någon av markeringarna. Använd ikonen **Konfigurera** (skiftnyckel) för att öppna dialogrutan.

   * [Flytta en komponent](/help/sites-cloud/authoring/fundamentals/editing-content.md#moving-a-component) antingen:

      * Dra den önskade komponenten till dess nya plats.
      * Öppna komponentverktygsfältet med någon av markeringarna. Använd ikonerna **Klipp ut** och **Klistra in** där det behövs.

   * [Kopiera (och klistra in)](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-toolbar) en komponent:

      * Öppna komponentverktygsfältet med någon av markeringarna. Använd ikonerna **Kopiera** och sedan **Klistra in** efter behov.

   >[!NOTE]
   >
   >Du kan **klistra in** komponenter på samma sida eller på en annan sida. Om du klistrar in på en annan sida som redan var öppen före klipp ut/kopiera-åtgärden, måste sidan uppdateras.

   * [Ta bort](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-toolbar) en komponent:

      * Öppna komponentens verktygsfält med antingen markering och använd sedan ikonen **Ta bort** .

   * [Lägg till anteckningar](/help/sites-cloud/authoring/fundamentals/annotations.md#annotations) på sidan:

      * Välj läget **Anteckning** (ikonen för pratbubbla). Lägg till anteckningar med ikonen **Lägg till anteckning** (plus). Avsluta anteckningsläget med X överst till höger.

        ![Anteckningsknapp](/help/sites-cloud/authoring/assets/annotations.png)

   * [Förhandsgranska en sida](/help/sites-cloud/authoring/fundamentals/editing-content.md#preview-mode) (för att se hur den kommer att se ut i publiceringsmiljön)

      * Välj **Förhandsgranska** i verktygsfältet.

   * Återgå till redigeringsläget (eller välj ett annat läge) med den nedrullningsbara väljaren **Redigera**.

   >[!NOTE]
   >
   >Om du vill navigera med hjälp av länkar i innehållet måste du använda [förhandsgranskningsläget](/help/sites-cloud/authoring/fundamentals/editing-content.md#preview-mode).

### Redigera sidegenskaperna {#editing-the-page-properties}

Det finns två (huvudmetoder) metoder för att [redigera sidegenskaper](/help/sites-cloud/authoring/fundamentals/page-properties.md):

* Från konsolen **Platser**:

   1. [Navigera till sidan](#finding-your-page) som du vill publicera.
   1. Välj ikonen **Egenskaper** från antingen:

      * [Snabbåtgärder (endast kortvyn/skrivbordet)](#quick-actions-card-view-desktop-only) för lämplig resurs.
      * Verktygsfältet när [sidan har valts](#selecting-your-page-for-further-action).

      ![Knappen Egenskaper](/help/sites-cloud/authoring/assets/properties.png)

   1. Sidegenskaperna visas. Du kan göra nödvändiga uppdateringar och sedan använda Spara för att behålla dessa

* När du [redigerar sidan](#editing-your-page-content):

   1. Öppna menyn **Sidinformation**.
   1. Välj **Öppna egenskaper** för att öppna dialogrutan för redigering av egenskaperna.

      ![Knappen Sidinformation](/help/sites-cloud/authoring/assets/page-information.png)

### Publicera din sida (eller avpublicera) {#publishing-your-page-or-unpublishing}

Det finns två huvudmetoder för att [publicera sidan](/help/sites-cloud/authoring/fundamentals/publishing-pages.md) (och även för att avpublicera):

* Från konsolen **Platser**:

   1. [Navigera till sidan](#finding-your-page) som du vill publicera.
   1. Välj ikonen **Snabb Publish** på något av följande sätt:

      * [Snabbåtgärder (endast kortvyn/skrivbordet)](#quick-actions-card-view-desktop-only) för lämplig resurs.
      * Verktygsfältet när [sidan har valts](#selecting-your-page-for-further-action) (ger även åtkomst till [Publish SENARE](/help/sites-cloud/authoring/fundamentals/publishing-pages.md)).

      ![Knappen Snabb Publish](/help/sites-cloud/authoring/assets/quick-publish.png)

* När du [redigerar sidan](#editing-your-page-content):

   1. Öppna menyn **Sidinformation**.
   1. Välj **Publish Page**.

* Du kan bara avpublicera en sida från konsolen via alternativet **Hantera publikation**, som bara är tillgängligt i verktygsfältet (inte via snabbåtgärderna).

  ![Knappen Hantera publikation](/help/sites-cloud/authoring/assets/manage-publication.png)

  Alternativet **Avpublicera sida** är fortfarande tillgängligt via menyn **Sidinformation** i redigeraren.

  Mer information finns i [Publicera sidor](/help/sites-cloud/authoring/fundamentals/publishing-pages.md#unpublishing-pages).

### Flytta, kopiera och klistra in eller ta bort sidan {#move-copy-and-paste-or-delete-your-page}

Alla dessa åtgärder kan utlösas av:

1. [Navigera till sidan](#finding-your-page) som du vill flytta, kopiera och klistra in eller ta bort.
1. Välj ikonen för kopiera (och sedan klistra in), flytta eller ta bort efter behov på något av följande sätt:

   * [Snabbåtgärder (endast kortvyn/skrivbordet)](#quick-actions-card-view-desktop-only) för den nödvändiga resursen.
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
* Listrutan [Sidinformation](#editing-the-page-properties) när du redigerar en sida.
* Sidans verktygsfält när du redigerar en sida (när sidan är låst)

Låsikonen ser till exempel ut så här:

![Lås-knapp](/help/sites-cloud/authoring/assets/lock.png)

### Åtkomst till sidreferenser {#accessing-page-references}

[Snabb åtkomst till referenser](/help/sites-cloud/authoring/fundamentals/environment-tools.md#references) till/från en sida finns i Reference Rail.

1. Välj **Referenser** med verktygsfältsikonen (antingen före eller efter [att du har valt sidan](#selecting-your-page-for-further-action)):

   ![Visningsalternativ för referenser](/help/sites-cloud/authoring/assets/references.png)

   En lista över referenstyper visas:

   ![Referensvy](/help/sites-cloud/authoring/assets/references-list.png)

1. Välj önskad typ av referens om du vill visa mer information och (när det är lämpligt) vidta ytterligare åtgärder.

### Skapa en version av din sida {#creating-a-version-of-your-page}

Så här skapar du en [version](/help/sites-cloud/authoring/features/page-versions.md) av sidan:

1. Om du vill öppna tidslinjen väljer du **[Tidslinje](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline)** med verktygsfältsikonen (antingen före eller efter [att du har valt sidan](#selecting-your-page-for-further-action)):

   ![Visningsalternativ för tidslinje](/help/sites-cloud/authoring/assets/timeline.png)

1. Markera ellipsen längst ned till höger i kolumnen Tidslinje om du vill visa extra knappar, inklusive **Spara som version**.

   ![Tidslinjevy](/help/sites-cloud/authoring/assets/timeline-view.png)

1. Välj **Spara som version** och sedan **Skapa**.

### Återställa/jämföra en version av sidan {#restoring-comparing-a-version-of-your-page}

Samma grundläggande funktion används när du återställer och/eller jämför versioner av sidan:

1. Välj **[Tidslinje](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline)** med verktygsfältsikonen (antingen före eller efter [att du har valt sidan](#selecting-your-page-for-further-action)):

   ![Visningsalternativ för tidslinje](/help/sites-cloud/authoring/assets/timeline.png)

   Om en version av sidan redan har sparats visas den på tidslinjen.

1. Välj den version som du vill återställa. Då visas ytterligare åtgärdsknappar:

   * **Återgå till den här versionen**

      * Versionen har återställts.

   * **Visa skillnader**

      * Sidan öppnas med skillnader (mellan de två versionerna) markerade.

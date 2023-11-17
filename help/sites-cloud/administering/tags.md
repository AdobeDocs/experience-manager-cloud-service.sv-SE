---
title: Administrera taggar
description: Lär dig hur du administrerar taggar i AEM för att ordna ditt innehåll.
exl-id: 42480699-b7a7-4678-a763-569a9b7573e2
source-git-commit: e2505c0fec1da8395930f131bfc55e1e2ce05881
workflow-type: tm+mt
source-wordcount: '2265'
ht-degree: 0%

---

# Administrera taggar {#administering-tags}

Taggar är ett intuitivt sätt att klassificera innehåll. De kan ses som nyckelord eller etiketter (metadata) som gör att innehållet kan hittas snabbare.

I Adobe Experience Manager (AEM) kan en -tagg vara en egenskap för:

* En innehållsnod för en sida
   * Se dokumentet [Använda taggar](/help/sites-cloud/authoring/features/tags.md) för mer information.
* En metadatanod för en resurs
   * Se dokumentet [Hantera metadata för digitala resurser](/help/assets/manage-metadata.md) för mer information.

>[!TIP]
>
>Det är bäst att minimera antalet taggar som relaterar till samma idéer. Om du till exempel hanterar innehåll för en butik utomhus behöver du förmodligen inte ha någon tagg för båda **skodon** och **skor**.

## Märkordsfunktioner {#tag-features}

Taggar har robusta funktioner för att ordna och hantera innehåll.

* Taggar kan grupperas i olika namnutrymmen.
   * Namnutrymmen kan tolkas som hierarkier som tillåter att taxonomier skapas.
   * Dessa taxonomier är globala i hela AEM.
* Taggar kan användas av författare och av webbplatsbesökare.
* Oavsett vem som skapat dem blir alla typer av taggar tillgängliga för markering, både när du tilldelar till en sida och när du söker.
* Taggar används av [List-komponent](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/list.html) om du vill generera dynamiska listor baserat på de markerade taggarna.

## Märkordskrav {#requirements}

Det finns några tekniska detaljer att tänka på när du skapar och hanterar taggar.

* Taggar måste vara unika inom ett specifikt namnutrymme.
* Namnet på en tagg får inte innehålla taggavgränsare:
   * Kolon (`:`) - Avgränsar namnutrymmestaggen
   * Snedstreck (`/`) - Definierar undertaggar
* Om en taggs titel innehåller taggavgränsare kommer de inte att visas i användargränssnittet.
* Taggar kan skapas och deras taxonomi kan ändras av medlemmar i `tag-administrators` grupp och medlemmar som har ändringsrättigheter till `/content/cq:tags`.
   * En tagg som innehåller underordnade taggar kallas behållartagg.
   * En tagg som inte är en behållartagg kallas för en lövtagg.
   * Ett taggnamnutrymme kan vara antingen en lövtagg eller en behållartagg.

Mer teknisk information om hur märkord fungerar finns i dokumentet [AEM Tagging Framework.](/help/implementing/developing/introduction/tagging-framework.md)

## Taggningskonsolen {#tagging-console}

Taggningskonsolen används för att skapa och hantera taggar och deras taxonomier. Du kan använda taggningskonsolen för att hantera dina taggar genom att:

* Gruppera dem i namnutrymmen.
* Granska användningen av befintliga taggar innan du skapar nya.
* Organisera om taggarna utan att koppla bort taggen från det aktuella innehållet.

Så här kommer du åt taggningskonsolen:

1. Logga in i en redigeringsmiljö med administratörsbehörighet.
1. Välj **`Tools`** -> **`General`** ->
   **`Tagging`**.

![Taggningskonsolen i AEM](/help/sites-cloud/administering/assets/tagging-console.png)

## Skapa nya taggar {#creating-new-tags}

Det finns ett antal steg för att skapa och använda taggar för att ordna ditt innehåll.

1. [Skapa ett namnutrymme för dina taggar](#creating-namespaces) (eller välj en befintlig som ska återanvändas).
1. [Skapa en ny tagg.](#creating-tags)
1. [Publicera taggen.](#publishing-tags)

### Skapa namnutrymmen {#creating-namespaces}

Ett namnutrymme används för att ordna andra taggar. Den kan ses som den lägsta nivån av taggen och används vanligtvis för att gruppera andra taggar.

1. Öppna dialogrutan [taggningskonsol](#tagging-console) och trycka eller klicka på **Skapa** i verktygsfältet och sedan **Skapa namnutrymme**.

   ![Dialogrutan Lägg till namnutrymme](/help/sites-cloud/administering/assets/add-namespace.png)

1. Tillhandahåll nödvändig information.

   * **Titel** - En rubrik för namnutrymmet som visas för användaren i användargränssnittet (valfritt)
   * **Namn** - Om inget namn anges skapas ett giltigt nodnamn från **Titel**. Se dokumentet [AEM Taggningsramverk](/help/implementing/developing/introduction/tagging-framework.md#tagid) för mer information.
   * **Beskrivning** - En beskrivning av namnutrymmet (valfritt)

1. När du angett den obligatoriska informationen trycker du eller klickar **Skapa**.

Namnutrymmet skapas. Observera att i taggningskonsolen är namnutrymmena på den lägsta nivån (längst till vänster i konsolen) och representeras av mappikoner, som visar deras natur som en&quot;behållare&quot; eller gruppering av andra taggar.

Nu kan du [skapa nya taggar](#creating-tags) i detta namnutrymme eller [hantera befintliga taggar.](#managing-tags)

Ett namnutrymme får inte innehålla några undertaggar. Eftersom ett namnutrymme i sig är en tagg kan det användas för att ordna ditt innehåll som vilken annan tagg som helst. Om du vill fortsätta att skapa en strukturerad taggningsstruktur kan du [skapa undertaggar](#creating-tags) i det namnutrymmet baserat på dina projektkrav.

### Skapa taggar {#creating-tags}

Taggar läggs vanligtvis till i namnutrymmen.

1. Öppna [taggningskonsol.](#tagging-console)

1. Välj det namnutrymme där du vill skapa taggen. Du kan också markera en annan tagg och skapa en undertagg under den.

1. Tryck eller klicka på **Skapa** i verktygsfältet och sedan **Skapa tagg**.

1. The **Skapa tagg** öppnas. Ange nödvändig information för den nya taggen.

   * **Titel** - En visningsrubrik för taggen (krävs)
   * **Namn** - Ett namn för taggen (obligatoriskt). Om inget anges skapas ett giltigt nodnamn från **Titel**. Se [TaggID](/help/implementing/developing/introduction/tagging-framework.md#tagid).
   * **Beskrivning** - En beskrivning av taggen
   * **Taggsökväg** - Standardvärdet är det namnutrymme (eller den tagg) som du valde i taggningskonsolen. Du kan uppdatera detta manuellt genom att trycka eller klicka på banväljarikonen.

   ![Dialogrutan Skapa tagg](assets/create-tag.png)

1. Tryck eller klicka **Skicka**.

Taggen skapas och konsolen uppdateras för att visa den nya taggen.

Taggar gör det möjligt att skapa en egen taxonomi som är anpassad efter organisationens behov.

* Du kan skapa underordnade taggar för befintliga taggar genom att markera den överordnade taggen i konsolen innan du skapar den nya taggen.
* Om du skapar en tagg utan att markera ett namnutrymme eller en annan tagg, skapar du effektivt ett namnutrymme.

### Publiceringstaggar {#publishing-tags}

Precis som när du skapar annat innehåll i AEM finns det bara i redigeringsmiljön när du har skapat en tagg (eller namnutrymme). För att dina taggar ska vara tillgängliga för användarna måste du publicera taggarna.

1. Öppna [taggningskonsol.](#tagging-console)

1. Markera den eller de taggar du vill publicera och välj sedan **Publicera**.

   ![Välja taggar i konsolen](assets/select-tags.png)

1. The **Publicera tagg** uppmanas du att bekräfta publiceringen av de markerade taggarna. Tryck eller klicka **Publicera**.

   ![Bekräftelsemodal publiceringstagg](assets/publish-tag.png)

1. Publiceringsåtgärden bekräftas med en **Lyckades** -dialogrutan.

   ![Dialogrutan Publicera taggar](assets/publish-tag-success.png)

De markerade taggarna står i kö för publicering. Precis som sidinnehåll publiceras bara de markerade taggarna, oavsett om de har undertaggar eller inte.

Om du vill publicera en hel taxonomi (ett namnutrymme och undertaggar) bör du skapa en [package](/help/implementing/developing/tools/package-manager.md) namnutrymmet (se [Taxonomirotnod](/help/implementing/developing/introduction/tagging-framework.md#taxonomy-root-node)).

<!--
Be sure to [apply permissions](#setting-tag-permissions) to the namespace before creating the package.
-->

## Hantera taggar {#managing-tags}

Det finns ett antal åtgärder som du kan vidta för befintliga taggar och namnutrymmen för att hantera och ordna dem. Markera bara en tagg eller ett namnutrymme i dialogrutan [taggningskonsol](#tagging-console) för att visa tillgängliga åtgärder i verktygsfältet.

* [Visa egenskaper](#viewing-tag-properties)
* [Redigera](#editing-tags)
* [Avpublicera](#unpublishing-tags)
* [Referenser](#viewing-tag-references)
* [Flytta](#moving-tags)
* [Sammanfoga](#merging-tags)
* [Ta bort](#deleting-tags)

Observera att när det finns tillräckligt med utrymme i verktygsfältet finns det ytterligare alternativ bakom ellipsikonen.

### Visa taggegenskaper {#viewing-tag-properties}

När en enskild tagg, ett namnutrymme eller en annan tagg markeras i taggningskonsolen visas grundläggande information om den markerade taggen, t.ex. tidpunkten för den senaste redigeringen och det senaste dokumentet i kolumnen till vänster om taggkolumnen.

![Kolumn med tagginformation](assets/tag-details-column.png)

Du kan visa mer information om taggen, inklusive vem som senast publicerade den och när genom att växla konsolen till **Egenskaper** vy.

1. Öppna [taggningskonsol.](#tagging-console)

1. Markera taggen vars egenskaper du vill visa och markera i den vänstra listen **Egenskaper**.

   ![Välja egenskapsvy](assets/view-tag-properties.png)

1. De detaljerade egenskaperna för den markerade taggen visas i den vänstra listen.

   ![Visa taggegenskaper](assets/tag-properties.png)

Mer information om hur du väljer visningsläge och räl finns i dokumentet [Grundläggande hantering.](/help/sites-cloud/authoring/getting-started/basic-handling.md#rail-selector)

### Redigera taggar {#editing-tags}

Taggar och namnutrymmen kan redigeras när de har skapats.

1. Öppna [taggningskonsol.](#tagging-console)

1. Markera taggen som du vill redigera och välj **Redigera**.

1. Gör önskade ändringar. Det går att ändra följande:

   * **Titel**
   * **Beskrivning**
   * [**Lokalisering**](#managing-tags-in-different-languages)

1. När redigeringarna är klara trycker eller klickar du **Skicka**.

Mer information om hur du lägger till språköversättningar finns i avsnittet om [Hantera taggar på olika språk](#managing-tags-in-different-languages).

Om de ändringar du har gjort är en redan publicerad tagg kanske du vill [publicera den igen.](#publishing-tags)

### Avpublicerar taggar {#unpublishing-tags}

Om du vill inaktivera taggen på författarinstansen och ta bort den från publiceringsinstansen kan du avpublicera den.

1. Om du vill avpublicera en tagg öppnar du [taggningskonsol.](#tagging-console)

1. Markera den eller de taggar du vill avpublicera och välj sedan **Avpublicera**.

   ![Välja taggar i konsolen](assets/select-tags.png)

1. The **Avpublicera tagg** uppmanas du att bekräfta publiceringen av de markerade taggarna. Tryck eller klicka **Publicera**.

   ![Bekräftelsemodal publiceringstagg](assets/unpublish-tag.png)

1. Avpubliceringsåtgärden bekräftas med en **Lyckades** -dialogrutan.

   ![Dialogrutan Publicera taggar](assets/unpublish-tag-success.png)

De markerade taggarna är köade för borttagning av publicering. Om den markerade taggen är en behållartagg inaktiveras alla dess underordnade taggar i redigeringsmiljön och tas bort från publiceringsmiljön.

### Visa taggreferenser {#viewing-tag-references}

Det kan vara praktiskt att se vilket innehåll en viss tagg används på. Du kan göra detta med **Referenser** i taggningskonsolen.

1. Öppna dialogrutan [taggningskonsol.](#tagging-console)

1. Markera taggen vars referenser du vill visa och markera i den vänstra listen **Referenser**.

   ![Välja egenskapsvy](assets/view-tag-references.png)

1. Det totala antalet referenser för den markerade taggen visas i den vänstra listen.

   ![Visa taggreferenser](assets/tag-references.png)

1. Tryck eller klicka på antalet taggreferenser för att visa den detaljerade listan med innehåll som är tilldelat taggen.

   ![Visa detaljerna i taggens referenser](assets/tag-references-detail.png)

Hovra musen eller tryck på ett refererande innehåll i listan för att visa innehållets fullständiga sökväg.

Mer information om hur du väljer visningsläge och räl finns i dokumentet [Grundläggande hantering.](/help/sites-cloud/authoring/getting-started/basic-handling.md#rail-selector)

### Flytta taggar {#moving-tags}

Du kan behöva rensa upp eller på annat sätt ordna om taggningen genom att flytta en tagg till en ny plats eller byta namn på den.

>[!TIP]
>
>Det är god praxis att endast administratörer får flytta och byta namn på taggar.

1. Öppna [taggningskonsol.](#tagging-console)

1. Markera taggen som du vill flytta eller byta namn på och tryck eller klicka på **Flytta** i verktygsfältet.

1. I **Flytta tagg** anger du vilken egenskap du vill ändra.

   * **Byt namn till** - Det nya namn som du vill ge taggen
      * Det här fältet är förifyllt med taggens aktuella namn.
      * Ändra inte om du bara vill flytta taggen och inte byta namn på den.
   * **Flytta till** - Var du vill flytta taggen
      * Det här fältet är förifyllt med taggens aktuella plats.
      * Ändra inte om du bara vill byta namn på taggen och inte flytta den.

   ![Flytta tagg](assets/move-tag.png)

1. Tryck eller klicka **Skicka**.

Taggens namn ändras och/eller flyttas till den nya platsen. När den markerade taggen är en behållartagg flyttas även alla underordnade taggar om du flyttar taggen.

### Sammanfoga taggar {#merging-tags}

Om taggningstaxonomin innehåller dubbletter eller liknande taggar kan det vara bra att sammanfoga de taggarna. När tagg `A` sammanfogas med taggen `B`, alla sidor taggade med tagg `A` blir taggade med tagg `B` och-tagg `A` är inte längre tillgängligt för författare.

1. Om du vill sammanfoga två taggar öppnar du [taggningskonsol.](#tagging-console)

1. Markera taggen som du vill sammanfoga med en annan tagg och tryck eller klicka sedan på **Sammanfoga** i verktygsfältet.

1. I **Sammanfoga tagg** trycker du på eller klickar på **Bläddra** ikonen för **Sammanfoga i** fält som anger i vilken tagg du vill sammanfoga den markerade taggen.

   ![Dialogrutan Sammanfoga tagg](assets/merge-tag.png)

1. Tryck eller klicka **Skicka**.

Den tagg som valts i konsolen sammanfogas med taggen som anges i dialogrutan. När en refererad tagg flyttas eller sammanfogas tas taggen inte bort fysiskt så att det går att behålla referenser. Se dokumentet [AEM Taggningsramverk](/help/implementing/developing/introduction/tagging-framework.md#moving-and-merging-tags) för mer information.

### Ta bort taggar {#deleting-tags}

Om taxonomin för taggning ändras och en tagg eller ett namnutrymme inte behövs kan den tas bort.

1. Öppna [taggningskonsol.](#tagging-console)

1. Markera taggen som du vill ta bort och tryck eller klicka sedan på **Ta bort** i verktygsfältet.

1. The **Ta bort tagg** uppmanas du att bekräfta borttagningen av de markerade taggarna. Tryck eller klicka **Ta bort**.

   ![Bekräftelsen Ta bort tagg modal](assets/delete-tag.png)

1. AEM kontrollerar att taggen inte refereras.

   1. Om inga referenser hittas ber AEM om en slutgiltig bekräftelse att radera. Tryck eller klicka **Ta bort**

      ![Inga referenser hittades](assets/no-references-found.png)

   1. Om referenser hittas visas de i AEM och en slutgiltig bekräftelse om att de ska tas bort.

      ![Referenser hittades](assets/references-found.png)

De markerade taggarna tas bort permanent från redigeringsmiljön. Om taggen publicerades tas den även bort från publiceringsmiljön. Om den markerade taggen är en behållartagg tas även alla dess underordnade taggar bort.

<!--

## Setting Tag Permissions {#setting-tag-permissions}

Tag permissions are ['secure (by default)'](/help/sites-administering/production-ready.md); a best practice for the publish environment that requires read permission to be explicitly allowed for tags. Bascially, this is done by creating a package of the Tag Namespace after permissions have been set on author, and installing the package on all publish instances.

* on author instance

    * sign in with administrative privileges
    * access the [Security Console](/help/sites-administering/security.md#accessing-user-administration-with-the-security-console),

        * for example, browse to http://localhost:4502/useradmin

    * in the left pane, select the group (or user) for which [read permission](/help/sites-administering/security.md#permissions) is to be granted
    * in the right pane, locate the **Path **to the Tag Namespace

        * for example, `/content/cq:tags/mycommunity`

    * select the `checkbox`in the **Read** column
    * select **Save**

![chlimage_1-204](assets/chlimage_1-204.png)

* ensure all publish instances have same permissions

    * one approach is to [create a package](/help/sites-administering/package-manager.md#package-manager) of the namespace on author

        * on `Advanced` tab, for `AC Handling` select `Overwrite`

    * replicate the package

        * choose `Replicate` from package manager

-->

## Hantera taggar på olika språk {#managing-tags-in-different-languages}

The `title` -egenskapen för en tagg kan översättas till flera språk. När taggtiteln har översatts kan den visas enligt användar- eller innehållsspråk.

Låt oss anta att vi har en tagg som heter `Animals` som vi vill översätta till tyska och franska.

1. Öppna [taggningskonsol.](#tagging-console)

1. Markera taggen som du vill översätta och tryck eller klicka sedan på **Redigera** i verktygsfältet.

1. I **Redigera tagg** i dialogrutan **Lokalisering** väljer du målspråk, till exempel tyska.

1. I **Tyska** anger du den översatta titeln.

1. Upprepa de två föregående stegen för franska.

   ![Översätta taggretitlar](assets/translate-tag.png)

1. Tryck eller klicka **Skicka**.

För innehållssidor hämtas det språk som valts för taggen från sidspråket, om tillgängligt.

I redigeringsmiljön använder AEM dock språkinställningen för användaren. Så i taggningskonsolen, för `Animals` tagg, `Animaux` visas för en användare som anger språket till franska i sina användaregenskaper.

Information om hur du lägger till ett nytt språk i dialogrutan finns i dokumentet [Bygga in märkord i AEM](/help/implementing/developing/introduction/tagging-applications.md#adding-a-new-language-to-the-edit-tag-dialog)

>[!TIP]
>
>Om du vill veta mer om AEM lokaliseringsfunktioner kan du läsa dokumentet [Översätta ditt innehåll för flerspråkiga webbplatser.](/help/sites-cloud/administering/translation/overview.md)

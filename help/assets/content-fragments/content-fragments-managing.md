---
title: Hantera innehållsfragment (resurser - innehållsfragment)
description: Lär dig hur du använder Resurskonsolen för att hantera AEM innehållsfragment, som utgör grunden för ditt headless-innehåll.
exl-id: 333ad877-db2f-454a-a3e5-59a936455932
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '1876'
ht-degree: 5%

---

# Hantera innehållsfragment {#managing-content-fragments}

Lär dig hur du använder Resurskonsolen för att hantera AEM innehållsfragment, som utgör grunden för ditt headless-innehåll.

När du har definierat [Modeller för innehållsfragment](#creating-a-content-model) kan du använda dessa för [skapa dina innehållsfragment](#creating-a-content-fragment).

The [Innehållsfragmentsredigerare](#opening-the-fragment-editor) innehåller olika [lägen](#modes-in-the-content-fragment-editor) för att göra det möjligt att

* [Redigera innehållet](#editing-the-content-of-your-fragment) och [hantera variationer](#creating-and-managing-variations-within-your-fragment)
* [Anteckna ditt fragment](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment)
* [Associera innehåll med fragment](#associating-content-with-your-fragment)
* [Konfigurera metadata](#viewing-and-editing-the-metadata-properties-of-your-fragment)
* [Visa strukturträdet](/help/assets/content-fragments/content-fragments-structure-tree.md)
* [Förhandsgranska JSON-representationen](/help/assets/content-fragments/content-fragments-json-preview.md)


>[!NOTE]
>
>Innehållsfragment kan användas:
>
>* när du redigerar sidor, se [Sidredigering med innehållsfragment](/help/sites-cloud/authoring/fundamentals/content-fragments.md).
>* for [Headless Content Delivery using Content Fragments with GraphQL](/help/assets/content-fragments/content-fragments-graphql.md).

>[!NOTE]
>
>Innehållsfragment är en webbplatsfunktion, men lagras som **Resurser**.
>
>De hanteras nu främst med **[Innehållsfragment](/help/sites-cloud/administering/content-fragments/managing.md#content-fragments-console)** konsolen, men de kan fortfarande hanteras från **Resurser** konsol. Detta avsnitt behandlar ledning från **Resurser** konsol.
>
>Det finns två redigerare för att skapa innehållsfragment. I det här avsnittet beskrivs den ursprungliga redigeraren, som du i första hand kommer åt från **Resurser** konsol. Se dokumentationen för Sites, [Content Fragments - Authoring](/help/sites-cloud/administering/content-fragments/authoring.md), om du vill ha information om den nya redigeraren (finns huvudsakligen i **Innehållsfragment** konsol). Båda redigerarna har en växlingsknapp i det övre verktygsfältet som ger snabb åtkomst till den andra redigeraren.

## Skapa innehållsfragment {#creating-content-fragments}

### Skapa en innehållsmodell {#creating-a-content-model}

[Modeller för innehållsfragment](/help/assets/content-fragments/content-fragments-models.md) kan aktiveras och skapas innan du skapar innehållsfragment med strukturerat innehåll.

### Skapa ett innehållsfragment {#creating-a-content-fragment}

Metoden för att skapa ett innehållsfragment är:

1. Navigera till mappen **Resurser** där du vill skapa fragmentet.
1. Välj **Skapa** och sedan **Innehållsfragment** för att öppna guiden.
1. I det första steget i guiden måste du ange grunden för det nya fragmentet.

   * [Modell](/help/assets/content-fragments/content-fragments-models.md) - används för att skapa ett fragment som kräver strukturerat innehåll, till exempel **Adventure** modell

      * Alla tillgängliga modeller visas.

   Efter markeringen kan du använda **Nästa** för att fortsätta.

   ![Välj innehållsfragmentmodell](assets/cfm-managing-01.png)

1. Ange följande i steget **Egenskaper**:

   * **Grundläggande**

      * **Titel**

        Fragmenttiteln.

        Obligatoriskt.

      * **Beskrivning**

      * **Taggar**

   * **Avancerat**

      * **Namn**

        Namnet; används för att skapa URL:en.

        Obligatoriskt; hämtas automatiskt från titeln, men kan uppdateras.

1. Välj **Skapa** för att slutföra åtgärden och **Öppna** sedan fragmentet för redigering eller gå tillbaka till konsolen med **Klar**.

   >[!NOTE]
   >I **Lista** läge för konsolen som du kan uppdatera **Visa inställningar** för att aktivera **Content Fragment Model** kolumn.

## Åtgärder för ett innehållsfragment i resurskonsolen {#actions-for-a-content-fragment-assets-console}

I **Resurser** konsol en rad åtgärder är tillgängliga för dina innehållsfragment, antingen:

* Från verktygsfältet: när du har valt fragmentet är alla lämpliga åtgärder tillgängliga.
* Som [snabbåtgärder](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions); en delmängd av åtgärder som är tillgängliga för de enskilda fragmentkorten.

![Åtgärder i verktygsfältet](assets/cfm-managing-02.png)

Markera fragmentet för att visa verktygsfältet med tillämpliga åtgärder:

* **Bearbeta resurser igen**
* **Skapa**
* **Ladda ned**

   * Spara fragmentet som en ZIP-fil. Du kan ange om du vill ta med Elements, Variationer eller Metadata.

* **Utcheckning**
* **Egenskaper**

   * Gör att du kan visa, redigera, eller båda, fragmentets metadata.

* **Redigera**

   * Låter dig [öppna fragmentet för att redigera innehåll](/help/assets/content-fragments/content-fragments-variations.md) tillsammans med dess element, variationer, tillhörande innehåll och metadata.

* **Snabbpublicering**
* **Hantera publikation**
* **Hantera taggar**
* **Till samling**
* **Kopiera** (och **Klistra in**)
* **Flytta**
* **Ta bort**

>[!NOTE]
>
>Många av dessa är [standardåtgärder för Assets](/help/assets/manage-digital-assets.md) och/eller [AEM](https://helpx.adobe.com/experience-manager/desktop-app/aem-desktop-app.html).

## Öppna fragmentredigeraren {#opening-the-fragment-editor}

Så här öppnar du fragmentet för redigering:

>[!CAUTION]
>
>Om du vill redigera ett innehållsfragment behöver du [lämpliga behörigheter](/help/implementing/developing/extending/content-fragments-customizing.md#asset-permissions). Kontakta systemadministratören om du har problem.

1. Använd **Resurser** för att navigera till platsen för ditt innehållsfragment.
1. Öppna fragmentet för redigering, antingen genom att:

   * Klicka/tryck på fragment- eller fragment-länken (detta beror på konsolvyn).
   * Markera fragmentet och sedan **Redigera** i verktygsfältet.

1. Fragmentredigeraren öppnas. Gör önskade ändringar:

   ![Fragmentredigerare](assets/cfm-managing-03.png)

1. När du har gjort ändringar använder du **Spara**, **Spara och stäng** eller **Stäng** efter behov.

   >[!NOTE]
   >
   >**Spara och stäng** är tillgängligt via **Spara** listruta.

   >[!NOTE]
   >
   >Båda **Spara och stäng** och **Stäng** kommer att avsluta redigeraren - se [Spara, stäng och versioner](#save-close-and-versions) för fullständig information om hur de olika alternativen fungerar för innehållsfragment.

## Lägen och åtgärder i Content Fragment Editor {#modes-actions-content-fragment-editor}

Det finns olika lägen och åtgärder tillgängliga från Content Fragment Editor.

### Lägen i Content Fragment Editor {#modes-in-the-content-fragment-editor}

Navigera genom de olika lägena med hjälp av ikonerna på sidopanelen:

* Variationer: [Redigera innehållet](#editing-the-content-of-your-fragment) och [Hantera dina variationer](#creating-and-managing-variations-within-your-fragment)

* [Anteckningar](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment)
* [Associerat innehåll](#associating-content-with-your-fragment)
* [Metadata](#viewing-and-editing-the-metadata-properties-of-your-fragment)
* [Strukturträd](/help/assets/content-fragments/content-fragments-structure-tree.md)
* [Förhandsgranska](/help/assets/content-fragments/content-fragments-json-preview.md)

![Lägen i redigeraren för innehållsfragment](assets/cfm-managing-04.png)

### Verktygsfältsåtgärder i redigeraren för innehållsfragment {#toolbar-actions-in-the-content-fragment-editor}

Vissa funktioner i det övre verktygsfältet finns i flera lägen:

![Verktygsfältsåtgärder som är tillgängliga i olika lägen](assets/cfm-managing-top-toolbar.png)

* Ett meddelande visas när fragmentet redan refereras på en innehållssida. Du kan **Stäng** meddelandet.

* Sidpanelen kan döljas/visas med **Växla sidopanel** -ikon.

* Under fragmentnamnet kan du se namnet på [Content Fragment Model](/help/assets/content-fragments/content-fragments-models.md) används för att skapa det aktuella fragmentet:

   * Namnet är också en länk som öppnar modellredigeraren.

* Se fragmentets status, till exempel information om när det skapades, ändrades eller publicerades. Statusen är även färgkodad:

   * **Nytt**: grå
   * **Utkast**: blue
   * **Publicerad**: grön
   * **Ändrad**: orange
   * **Inaktiverad**: röd

* Med en knapp **Prova den nya redigeraren** genom att öppna *new* [Innehållsfragmentsredigerare](/help/sites-cloud/administering/content-fragments/authoring.md) som är tillgängliga via [Konsol för innehållsfragment](/help/sites-cloud/administering/content-fragments/managing.md#content-fragments-console).

  >[!WARNING]
  >
  >Den nya redigeraren öppnas på samma flik. Vi rekommenderar inte att båda redigerarna är öppna samtidigt.

* **Spara** ger åtkomst till **Spara och stäng** alternativ.

* De tre punkterna (**...**) ger åtkomst till ytterligare åtgärder:
   * **Uppdatera sidreferenser**
      * Detta uppdaterar eventuella sidreferenser.
   * **[Snabbpublicering](#publishing-and-referencing-a-fragment)**
   * **[Hantera publikation](#publishing-and-referencing-a-fragment)**

<!--
This updates any page references and ensures that the Dispatcher is flushed as required. -->

## Spara, stäng och versioner {#save-close-and-versions}

>[!NOTE]
>
>Versioner kan också [har skapats, jämförts och återställts från tidslinjen](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments).

Redigeraren har olika alternativ:

* **Spara** och **Spara och stäng**

   * **Spara** sparar de senaste ändringarna och finns kvar i redigeraren.
   * **Spara och stäng** sparar de senaste ändringarna och avslutar redigeraren.

  >[!CAUTION]
  >
  >Om du vill redigera ett innehållsfragment behöver du [lämpliga behörigheter](/help/implementing/developing/extending/content-fragments-customizing.md#asset-permissions). Kontakta systemadministratören om du har problem.

  >[!NOTE]
  >
  >Du kan vara kvar i redigeraren och göra en serie ändringar innan du sparar.

  >[!CAUTION]
  >
  >Förutom att bara spara ändringarna uppdaterar åtgärderna alla referenser och ser till att Dispatcher rensas efter behov. Dessa ändringar kan ta tid att bearbeta. På grund av detta kan prestandan påverkas på ett stort/komplext/tungt laddat system.
  >
  >Tänk på detta när du använder **Spara och stäng** och sedan snabbt ange fragmentredigeraren igen för att göra och spara fler ändringar.

* **Stäng**

  Avslutar redigeraren utan att spara de senaste ändringarna (d.v.s. gjorda sedan den senaste **Spara**).

När du redigerar ditt innehållsfragment skapar AEM automatiskt versioner för att säkerställa att tidigare innehåll kan återställas om du avbryter ändringarna (med **Stäng** utan att spara):

1. När ett innehållsfragment öppnas för redigering AEM söker efter den cookie-baserade token som anger om en *redigeringssession* finns:

   1. Om token hittas betraktas fragmentet som en del av den befintliga redigeringssessionen.
   2. Om token är *not* är tillgängligt och användaren börjar redigera innehåll, en version skapas och en token för den nya redigeringssessionen skickas till klienten, där den sparas i en cookie.

2. Medan det finns en *aktiv* redigeringssession sparas det innehåll som redigeras automatiskt var 600:e sekund (standard).

   >[!NOTE]
   >
   >Intervallet för att spara automatiskt kan konfigureras med `/conf` mekanism.
   >
   >Standardvärde, se:
   >  `/libs/settings/dam/cfm/jcr:content/autoSaveInterval`

3. Om användaren avbryter redigeringen återställs den version som skapades i början av redigeringssessionen och token tas bort för att avsluta redigeringssessionen.
4. Om användaren väljer **Spara** redigeringarna, de uppdaterade elementen/varianterna bevaras och token tas bort för att avsluta redigeringssessionen.

## Redigera innehållet i fragmentet {#editing-the-content-of-your-fragment}

När du har öppnat fragmentet kan du använda [Variationer](/help/assets/content-fragments/content-fragments-variations.md) för att skapa ditt innehåll.

## Skapa och hantera variationer i fragment {#creating-and-managing-variations-within-your-fragment}

När du har skapat mallinnehållet kan du skapa och hantera [Variationer](/help/assets/content-fragments/content-fragments-variations.md) av det innehållet.

## Koppla innehåll till fragment {#associating-content-with-your-fragment}

Du kan också [associera innehåll](/help/assets/content-fragments/content-fragments-assoc-content.md) med ett fragment. Detta ger en anslutning så att resurser (dvs. bilder) kan användas (valfritt) med fragmentet när det läggs till på en innehållssida.

## Visa och redigera metadata (egenskaper) för fragmentet {#viewing-and-editing-the-metadata-properties-of-your-fragment}

Du kan visa och redigera egenskaperna för ett fragment med [Metadata](/help/assets/content-fragments/content-fragments-metadata.md) -fliken.

## Tidslinje för innehållsfragment {#timeline-for-content-fragments}

Förutom standardalternativen [Tidslinje](/help/assets/manage-digital-assets.md#timeline) innehåller både information och åtgärder som är specifika för innehållsfragment:

* Visa information om versioner, kommentarer och anteckningar
* Åtgärder för versioner

   * **[Återgå till den här versionen](#reverting-to-a-version)** (välj ett befintligt fragment och sedan en specifik version)

   * **[Jämför med aktuell](#comparing-fragment-versions)** (välj ett befintligt fragment och sedan en specifik version)

   * Lägg till en **Etikett** och/eller **Kommentar** (välj ett befintligt fragment och sedan en specifik version)

   * **Spara som version** (markera ett befintligt fragment och sedan uppilen längst ned på tidslinjen)

* Åtgärder för anteckningar

   * **Ta bort**

>[!NOTE]
>
Kommentarerna är:
>
* Standardfunktionalitet för alla resurser
* Skapat i tidslinjen
* Relaterat till fragmentresursen
>
Anteckningar (för innehållsfragment) är:
>
* Anges i fragmentredigeraren
* Specifik för ett markerat textsegment i fragmentet
>

Till exempel:

![Tidslinje](assets/cfm-managing-05.png)

## Jämföra fragmentversioner {#comparing-fragment-versions}

The **Jämför med aktuell** finns tillgänglig från [Tidslinje](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments) när du har valt en viss version.

Den öppnas:

* den **Aktuell** (senaste) version (vänster)

* den valda versionen **v&lt;*x.y*>** (höger)

De visas sida vid sida, där:

* Eventuella skillnader markeras

   * Borttagen text - röd
   * Infogad text - grön
   * Ersatt text - blå

* Med helskärmsikonen kan du öppna båda versionerna separat och sedan växla tillbaka till den parallella vyn
* Du kan **Återställ** till den specifika versionen
* **Klar** kommer du tillbaka till konsolen

>[!NOTE]
>
Du kan inte redigera fragmentinnehållet när du jämför fragment.

![Jämföra variationer](assets/cfm-managing-06.png)

## Återställa till en version  {#reverting-to-a-version}

Du kan återgå till en viss version av fragmentet:

* Direkt från [Tidslinje](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments).

  Välj önskad version och sedan **Återgå till den här versionen** åtgärd.

* while [jämföra en version med den aktuella versionen](/help/assets/content-fragments/content-fragments-managing.md#comparing-fragment-versions) du kan **Återställ** till den valda versionen.

## Publicera och referera till ett fragment {#publishing-and-referencing-a-fragment}

>[!CAUTION]
>
Om fragmentet är baserat på en modell bör du se till att [modellen har publicerats](/help/assets/content-fragments/content-fragments-models.md#publishing-a-content-fragment-model).
>
Om du publicerar ett innehållsfragment för vilket modellen ännu inte har publicerats, visas detta i en urvalslista och modellen publiceras med fragmentet.

Innehållsfragment måste publiceras för användning i publiceringsmiljön. Detta görs med standardfunktionaliteten Resurser:

* [Snabbpublicering](/help/assets/manage-publication.md#quick-publish)
* [Hantera publikation](/help/assets/manage-publication.md#manage-publication)

Du kan få åtkomst till detta:

* efter skapande; använda [åtgärder som är tillgängliga i resurskonsolen](#actions-for-a-content-fragment-assets-console).
* Från [Innehållsfragmentsredigerare](#toolbar-actions-in-the-content-fragment-editor).

Dessutom när du [publicera en sida som använder fragmentet](/help/sites-cloud/authoring/fundamentals/content-fragments.md#publishing); fragmentet visas i sidreferenserna.

>[!CAUTION]
>
När ett fragment har publicerats och/eller refererats visar AEM en varning när en författare öppnar fragmentet för redigering igen. Detta är för att varna för att ändringar i fragmentet även påverkar de refererade sidorna.

## Ta bort ett fragment {#deleting-a-fragment}

Ta bort ett fragment:

1. I **Resurser** konsolen navigerar till platsen för innehållsfragmentet.
2. Markera fragmentet.

   >[!NOTE]
   >
   The **Ta bort** åtgärden är inte tillgänglig som en snabbåtgärd.

3. Välj **Ta bort** i verktygsfältet.
4. Bekräfta **Ta bort** åtgärd.

   >[!CAUTION]
   >
   Om fragmentet redan finns på en sida visas ett varningsmeddelande och du måste bekräfta att du vill fortsätta med **Tvinga borttagning**. Fragmentet, tillsammans med dess innehållskomponent fragment, tas bort från alla innehållssidor.

---
title: Hantera innehållsfragment (Assets - innehållsfragment)
description: Lär dig hur du använder Assets-konsolen för att hantera AEM innehållsfragment, antingen som grund för ditt headless-innehåll eller för att skapa sidor.
exl-id: 333ad877-db2f-454a-a3e5-59a936455932
feature: Content Fragments
role: User, Admin
solution: Experience Manager Sites
source-git-commit: b018c1948d479c78e1ef25b2248f3674ec1fcf92
workflow-type: tm+mt
source-wordcount: '1907'
ht-degree: 4%

---

# Hantera innehållsfragment {#managing-content-fragments}

Lär dig hur du använder Assets-konsolen för att hantera AEM innehållsfragment, antingen som grund för ditt headless-innehåll eller för att skapa sidor.

När du har definierat dina [modeller för innehållsfragment](#creating-a-content-model) kan du använda dessa för att [skapa dina innehållsfragment](#creating-a-content-fragment).

[Innehållsfragmentredigeraren](#opening-the-fragment-editor) innehåller olika [lägen](#modes-in-the-content-fragment-editor) som du kan använda för att:

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
>* när du redigerar sidor, se [Sidredigering med innehållsfragment](/help/sites-cloud/authoring/fragments/content-fragments.md).
>* för [Headless Content Delivery med Content Fragments with GraphQL](/help/assets/content-fragments/content-fragments-graphql.md).

>[!NOTE]
>
>Innehållsfragment är en webbplatsfunktion, men lagras som **Assets**.
>
>De hanteras nu primärt med konsolen **[Innehållsfragment](/help/sites-cloud/administering/content-fragments/managing.md#content-fragments-console)**, men de kan fortfarande hanteras från konsolen **Assets**. I det här avsnittet beskrivs hantering från **Assets**-konsolen.
>
>Det finns två redigerare för att skapa innehållsfragment. Även om de grundläggande funktionerna är desamma finns det vissa skillnader. I det här avsnittet beskrivs den ursprungliga redigeraren, som huvudsakligen nås från **Assets**-konsolen. Mer information om den nya redigeraren finns i webbplatsdokumentationen, [Innehållsfragment - redigering](/help/sites-cloud/administering/content-fragments/authoring.md) (som huvudsakligen nås från konsolen **Innehållsfragment**). Båda redigerarna har en växlingsknapp i det övre verktygsfältet som ger snabb åtkomst till den andra redigeraren.

## Skapa innehållsfragment {#creating-content-fragments}

### Skapa en innehållsmodell {#creating-a-content-model}

[Modeller för innehållsfragment](/help/assets/content-fragments/content-fragments-models.md) kan aktiveras och skapas innan du skapar innehållsfragment med strukturerat innehåll.

### Skapa ett innehållsfragment {#creating-a-content-fragment}

Metoden för att skapa ett innehållsfragment är:

1. Navigera till mappen **Resurser** där du vill skapa fragmentet.
1. Välj **Skapa** och sedan **Innehållsfragment** för att öppna guiden.
1. I det första steget i guiden måste du ange grunden för det nya fragmentet.

   * [Modell](/help/assets/content-fragments/content-fragments-models.md) - används för att skapa ett fragment som kräver strukturerat innehåll, till exempel modellen **Adventure**

      * Alla tillgängliga modeller visas.

   Efter markeringen använder du **Nästa** för att fortsätta.

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
   >I konsolens **listläge** kan du uppdatera **visningsinställningarna** och aktivera kolumnen **Content Fragment Model**.

## Åtgärder för ett innehållsfragment i Assets Console {#actions-for-a-content-fragment-assets-console}

I **Assets**-konsolen finns ett antal åtgärder tillgängliga för dina innehållsfragment, antingen:

* Från verktygsfältet: när du har valt fragmentet är alla lämpliga åtgärder tillgängliga.
* Som [snabbåtgärder](/help/sites-cloud/authoring/basic-handling.md#quick-actions); en deluppsättning av åtgärder tillgängliga för de enskilda fragmentkorten.

![Åtgärder i verktygsfältet](assets/cfm-managing-02.png)

Markera fragmentet för att visa verktygsfältet med tillämpliga åtgärder:

* **Bearbeta Assets igen**
* **Skapa**
* **Hämta**

   * Spara fragmentet som en ZIP-fil. Du kan ange om du vill ta med Elements, Variationer eller Metadata.

* **Utcheckning**
* **Egenskaper**

   * Gör att du kan visa, redigera, eller båda, fragmentets metadata.

* **Redigera**

   * Gör att du kan [öppna fragmentet för redigering av innehåll](/help/assets/content-fragments/content-fragments-variations.md) tillsammans med dess element, variationer, tillhörande innehåll och metadata.

* **Snabb Publish**
* **Hantera publikation**
* **Hantera taggar**
* **Till samling**
* **Kopiera** (och **Klistra in**)
* **Flytta**
* **Ta bort**

>[!NOTE]
>
>Många av dessa är [standardåtgärder för Assets](/help/assets/manage-digital-assets.md) och/eller [AEM skrivbordsappen](https://helpx.adobe.com/experience-manager/desktop-app/aem-desktop-app.html).

## Öppna fragmentredigeraren {#opening-the-fragment-editor}

Så här öppnar du fragmentet för redigering:

>[!CAUTION]
>
>Du behöver [lämplig behörighet](/help/implementing/developing/extending/content-fragments-customizing.md#asset-permissions) för att kunna redigera ett innehållsfragment. Kontakta systemadministratören om du har problem.

1. Använd **Assets**-konsolen för att navigera till platsen för ditt innehållsfragment.
1. Öppna fragmentet för redigering, antingen genom att:

   * Klicka/tryck på fragment- eller fragment-länken (detta beror på konsolvyn).
   * Markera fragmentet och **Redigera** i verktygsfältet.

1. Fragmentredigeraren öppnas. Gör önskade ändringar:

   ![Fragmentredigerare](assets/cfm-managing-03.png)

1. När du har gjort ändringarna använder du **Spara**, **Spara och stäng** eller **Stäng** efter behov.

   >[!NOTE]
   >
   >**Spara och stäng** är tillgängligt i listrutan **Spara**.

   >[!NOTE]
   >
   >Både **Spara och stäng** och **Stäng** avslutar redigeraren. Mer information om hur de olika alternativen fungerar för innehållsfragment finns i [Spara, stäng och versioner](#save-close-and-versions).

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

![Verktygsfältsåtgärder är tillgängliga i olika lägen](assets/cfm-managing-top-toolbar.png)

* Ett meddelande visas när fragmentet redan refereras på en innehållssida. Du kan **Stäng** meddelandet.

* Sidpanelen kan döljas/visas med ikonen **Växla sidpanel** .

* Under fragmentnamnet kan du se namnet på [Content Fragment Model](/help/assets/content-fragments/content-fragments-models.md) som används för att skapa det aktuella fragmentet:

   * Namnet är också en länk som öppnar modellredigeraren.

* Se fragmentets status, till exempel information om när det skapades, ändrades eller publicerades. Statusen är även färgkodad:

   * **Nytt**: grått
   * **Utkast**: blått
   * **Publicerad**: grön
   * **Ändrad**: orange
   * **Inaktiverad**: röd

* Med en knapp kan du **Prova ny redigerare** genom att öppna den *nya* [redigeraren för innehållsfragment](/help/sites-cloud/administering/content-fragments/authoring.md) som är tillgänglig via konsolen [Innehållsfragment](/help/sites-cloud/administering/content-fragments/managing.md#content-fragments-console) direkt.

  >[!WARNING]
  >
  >Den nya redigeraren öppnas på samma flik. Vi rekommenderar inte att båda redigerarna är öppna samtidigt.

* **Spara** ger åtkomst till alternativet **Spara och stäng**.

* Listrutan med tre punkter (**..**) ger åtkomst till ytterligare åtgärder:
   * **Uppdatera sidreferenser**
      * Detta uppdaterar eventuella sidreferenser.
   * **[Snabbpublicering](#publishing-and-referencing-a-fragment)**
   * **[Hantera publikation](#publishing-and-referencing-a-fragment)**

<!--
This updates any page references and ensures that the Dispatcher is flushed as required. -->

## Spara, stäng och versioner {#save-close-and-versions}

>[!NOTE]
>
>Versioner kan också [skapas, jämföras och återställas från tidslinjen](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments).

Redigeraren har olika alternativ:

* **Spara** och **Spara och stäng**

   * **Spara** sparar de senaste ändringarna och finns kvar i redigeraren.
   * **Spara och stäng** sparar de senaste ändringarna och avslutar redigeraren.

  >[!CAUTION]
  >
  >Du behöver [lämplig behörighet](/help/implementing/developing/extending/content-fragments-customizing.md#asset-permissions) för att kunna redigera ett innehållsfragment. Kontakta systemadministratören om du har problem.

  >[!NOTE]
  >
  >Du kan vara kvar i redigeraren och göra en serie ändringar innan du sparar.

  >[!CAUTION]
  >
  >Förutom att bara spara ändringarna uppdaterar åtgärderna även alla referenser och ser till att Dispatcher rensas efter behov. Dessa ändringar kan ta tid att bearbeta. På grund av detta kan prestandan påverkas på ett stort/komplext/tungt laddat system.
  >
  >Tänk på den här processen när du använder **Spara och stäng** och sedan snabbt anger om fragmentredigeraren för att göra och spara fler ändringar.

* **Stäng**

  Avslutar redigeraren utan att spara de senaste ändringarna (d.v.s. gjorda sedan den senaste **Spara**).

När du redigerar ditt innehållsfragment skapar AEM automatiskt versioner för att säkerställa att tidigare innehåll kan återställas om du avbryter dina ändringar (med **Stäng** utan att spara):

1. När ett innehållsfragment öppnas för redigering AEM söker efter den cookie-baserade token som anger om det finns en *redigeringssession*:

   1. Om token hittas betraktas fragmentet som en del av den befintliga redigeringssessionen.
   2. Om token är *inte* tillgänglig och användaren börjar redigera innehåll, skapas en version och en token för den nya redigeringssessionen skickas till klienten, där den sparas i en cookie.

2. När det finns en *aktiv*-redigeringssession sparas innehållet som redigeras automatiskt var 600:e sekund (standard).

   >[!NOTE]
   >
   >Intervallet för att spara automatiskt kan konfigureras med `/conf`-mekanismen.
   >
   >Standardvärde, se:
   >  `/libs/settings/dam/cfm/jcr:content/autoSaveInterval`

3. Om användaren avbryter redigeringen återställs den version som skapades i början av redigeringssessionen och token tas bort för att avsluta redigeringssessionen.
4. Om användaren väljer att **spara** redigeringarna behålls de uppdaterade elementen/varianterna och token tas bort för att avsluta redigeringssessionen.

## Redigera innehållet i fragmentet {#editing-the-content-of-your-fragment}

När du har öppnat fragmentet kan du använda fliken [Variationer](/help/assets/content-fragments/content-fragments-variations.md) för att skapa innehållet.

## Skapa och hantera variationer i fragment {#creating-and-managing-variations-within-your-fragment}

När du har skapat huvudinnehållet kan du skapa och hantera [Variationer](/help/assets/content-fragments/content-fragments-variations.md) av det innehållet.

## Koppla innehåll till fragment {#associating-content-with-your-fragment}

Du kan också [associera innehåll](/help/assets/content-fragments/content-fragments-assoc-content.md) med ett fragment. Detta ger en anslutning så att resurser (dvs. bilder) kan användas (valfritt) med fragmentet när det läggs till på en innehållssida.

## Visa och redigera metadata (egenskaper) för fragmentet {#viewing-and-editing-the-metadata-properties-of-your-fragment}

Du kan visa och redigera egenskaperna för ett fragment på fliken [Metadata](/help/assets/content-fragments/content-fragments-metadata.md) .

## Tidslinje för innehållsfragment {#timeline-for-content-fragments}

Utöver standardalternativen innehåller [tidslinjen](/help/assets/manage-digital-assets.md#timeline) både information och åtgärder som är specifika för innehållsfragment:

* Visa information om versioner, kommentarer och anteckningar
* Åtgärder för versioner

   * **[Återgå till den här versionen](#reverting-to-a-version)** (välj ett befintligt fragment och sedan en specifik version)

   * **[Jämför med aktuell](#comparing-fragment-versions)** (välj ett befintligt fragment och sedan en specifik version)

   * Lägg till en **etikett** och/eller **kommentar** (välj ett befintligt fragment och sedan en specifik version)

   * **Spara som version** (markera ett befintligt fragment och sedan uppilen längst ned på tidslinjen)

* Åtgärder för anteckningar

   * **Ta bort**

>[!NOTE]
>
>Kommentarerna är:
>
>* Standardfunktionalitet för alla resurser
>* Skapat i tidslinjen
>* Relaterat till fragmentresursen
>
>Anteckningar (för innehållsfragment) är:
>
>* Anges i fragmentredigeraren
>* Specifik för ett markerat textsegment i fragmentet
>
>Ingendera av kommentarerna i den nya [redigeraren för innehållsfragment](/help/sites-cloud/administering/content-fragments/authoring.md#commenting-on-your-fragment) visas.

Till exempel:

![Tidslinje](assets/cfm-managing-05.png)

## Jämföra fragmentversioner {#comparing-fragment-versions}

Åtgärden **Jämför med aktuell** är tillgänglig från [tidslinjen](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments) när du har valt en viss version.

Den öppnas:

* den **aktuella** (senaste) versionen (vänster)

* den markerade versionen **v&lt;*x.y*>** (höger)

De visas sida vid sida, där:

* Eventuella skillnader markeras

   * Borttagen text - röd
   * Infogad text - grön
   * Ersatt text - blå

* Med helskärmsikonen kan du öppna båda versionerna separat och sedan växla tillbaka till den parallella vyn
* Du kan **återställa** till den specifika versionen
* **Klar** kommer att returnera dig till konsolen

>[!NOTE]
>
>Du kan inte redigera fragmentinnehållet när du jämför fragment.

![Jämför variationer](assets/cfm-managing-06.png)

## Återställa till en version  {#reverting-to-a-version}

Du kan återgå till en viss version av fragmentet:

* Direkt från [tidslinjen](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments).

  Välj önskad version och sedan åtgärden **Återgå till denna version**.

* När du [jämför en version med den aktuella versionen](/help/assets/content-fragments/content-fragments-managing.md#comparing-fragment-versions) kan du **Återgå** till den valda versionen.

## Publicera och referera till ett fragment {#publishing-and-referencing-a-fragment}

>[!CAUTION]
>
>Om fragmentet är baserat på en modell bör du kontrollera att modellen [har publicerats](/help/assets/content-fragments/content-fragments-models.md#publishing-a-content-fragment-model).
>
>Om du publicerar ett innehållsfragment för vilket modellen ännu inte har publicerats, visas detta i en urvalslista och modellen publiceras med fragmentet.

Innehållsfragment måste publiceras för användning i publiceringsmiljön. Detta görs med Assets standardfunktioner:

* [Snabb Publish](/help/assets/manage-publication.md#quick-publish)
* [Hantera publikation](/help/assets/manage-publication.md#manage-publication)

Du kan få åtkomst till detta:

* Efter skapande; använder [åtgärder som är tillgängliga i Assets-konsolen](#actions-for-a-content-fragment-assets-console).
* Från [redigeraren för innehållsfragment](#toolbar-actions-in-the-content-fragment-editor).

När du [publicerar en sida som använder fragmentet ](/help/sites-cloud/authoring/fragments/content-fragments.md#publishing) visas dessutom fragmentet i sidreferenserna.

>[!CAUTION]
>
>När ett fragment har publicerats och/eller refererats visar AEM en varning när en författare öppnar fragmentet för redigering igen. Detta är för att varna för att ändringar i fragmentet även påverkar de refererade sidorna.

## Ta bort ett fragment {#deleting-a-fragment}

Ta bort ett fragment:

1. Gå till platsen för innehållsfragmentet i **Assets**-konsolen.
2. Markera fragmentet.

   >[!NOTE]
   >
   >Åtgärden **Ta bort** är inte tillgänglig som en snabbåtgärd.

3. Välj **Ta bort** i verktygsfältet.
4. Bekräfta åtgärden **Ta bort**.

   >[!CAUTION]
   >
   >Om fragmentet redan finns på en sida visas ett varningsmeddelande och du måste bekräfta att du vill fortsätta med **Tvinga borttagning**. Fragmentet, tillsammans med dess innehållskomponent fragment, tas bort från alla innehållssidor.

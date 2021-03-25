---
title: Hantera innehållsfragment
description: Innehållsfragment lagras som resurser, så hanteras främst från resurskonsolen.
translation-type: tm+mt
source-git-commit: 243b7509661cbb9da670bdc15b68378db43b423a
workflow-type: tm+mt
source-wordcount: '1616'
ht-degree: 7%

---


# Hantera innehållsfragment{#managing-content-fragments}

Innehållsfragment lagras som **Resurser**, så hanteras primärt från konsolen **Resurser**.

>[!NOTE]
>
>Innehållsfragment kan användas:
>
>* vid framtagning av sidor, se [Sidredigering med innehållsfragment](/help/sites-cloud/authoring/fundamentals/content-fragments.md).
>* for [Headless Content Delivery using Content Fragments with GraphQL](/help/assets/content-fragments/content-fragments-graphql.md).


## Skapa innehållsfragment {#creating-content-fragments}

### Skapa en innehållsmodell {#creating-a-content-model}

[Modellskanning ](/help/assets/content-fragments/content-fragments-models.md) av innehållsfragment kan aktiveras och skapas innan innehållsfragment med strukturerat innehåll skapas.

### Skapa ett innehållsfragment {#creating-a-content-fragment}

Metoden för att skapa ett innehållsfragment är:

1. Navigera till mappen **Resurser** där du vill skapa fragmentet.
1. Välj **Skapa** och sedan **Innehållsfragment** för att öppna guiden.
1. I det första steget i guiden måste du ange grunden för det nya fragmentet.

   * [Modell](/help/assets/content-fragments/content-fragments-models.md)  - använd för att skapa ett fragment som kräver strukturerat innehåll. till exempel  **** Adventuremodel

      * Alla tillgängliga modeller visas.

   Efter markeringen använder du **Nästa** för att fortsätta.

   ![fragmentbas](assets/cfm-managing-01.png)

1. Ange följande i steget **Egenskaper**:

   * **Grundläggande**

      * **Titel**

         Fragmenttiteln.

         Obligatorisk.

      * **Beskrivning**

      * **Taggar**
   * **Avancerat**

      * **Namn**

         Namnet; används för att skapa URL:en.

         Obligatoriskt. hämtas automatiskt från titeln, men kan uppdateras.


1. Välj **Skapa** för att slutföra åtgärden och **Öppna** sedan fragmentet för redigering eller gå tillbaka till konsolen med **Klar**.

   >[!NOTE]
   >I **listläge** för konsolen kan du uppdatera **Visa inställningar** för att aktivera kolumnen **Content Fragment Model**.

## Åtgärder för ett innehållsfragment i resurskonsolen {#actions-for-a-content-fragment-assets-console}

I konsolen **Resurser** finns en rad åtgärder tillgängliga för dina innehållsfragment, antingen:

* Från verktygsfältet; när du har valt fragmentet är alla lämpliga åtgärder tillgängliga.
* Som [snabbåtgärder](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions); en delmängd av åtgärder som är tillgängliga för de enskilda fragmentkorten.

![funktionsmakron](assets/cfm-managing-02.png)

Markera fragmentet för att visa verktygsfältet med tillämpliga åtgärder:

* **Bearbeta resurser igen**
* **Skapa**
* **Hämta**

   * Spara fragmentet som en ZIP-fil; du kan definiera om element, variationer och metadata ska inkluderas.

* **Utcheckning**
* **Egenskaper**

   * Gör att du kan visa och/eller redigera fragmentets metadata.

* **Redigera**

   * Gör att du kan [öppna fragmentet för redigering av innehåll](/help/assets/content-fragments/content-fragments-variations.md) tillsammans med dess element, variationer, tillhörande innehåll och metadata.

* **Snabbpublicering**
* **Hantera publikation**
* **Hantera taggar**
* **Till samling**
* **Kopiera**  (och  **klistra in**)
* **Flytta**
* **Ta bort**

>[!NOTE]
>
>Många av dessa är [standardåtgärder för Assets](/help/assets/manage-digital-assets.md) och/eller [AEM skrivbordsappen](https://helpx.adobe.com/experience-manager/desktop-app/aem-desktop-app.html).

## Öppna fragmentredigeraren {#opening-the-fragment-editor}

Så här öppnar du fragmentet för redigering:

>[!CAUTION]
>
>Om du vill redigera ett innehållsfragment behöver du [de behörigheter som krävs](/help/implementing/developing/extending/content-fragments-customizing.md#asset-permissions). Kontakta systemadministratören om du har problem.

>[!CAUTION]
>
>Om du vill redigera ett innehållsfragment måste du ha rätt behörighet. Kontakta systemadministratören om du har problem.

1. Använd konsolen **Resurser** för att navigera till platsen för ditt innehållsfragment.
1. Öppna fragmentet för redigering, antingen genom att:

   * Klicka/tryck på fragment- eller fragment-länken (detta beror på konsolvyn).
   * Markera fragmentet och **Redigera** i verktygsfältet.

1. Fragmentredigeraren öppnas. Gör önskade ändringar:

   ![fragmentredigerare](assets/cfm-managing-03.png)

1. När du har gjort ändringarna använder du **Spara och stäng** eller **Avbryt** efter behov.

   >[!NOTE]
   >
   >Både **Spara och stäng** och **Avbryt** kommer att avsluta redigeraren. Mer information om hur båda alternativen fungerar för innehållsfragment finns i [Spara, Avbryt och Versioner](#save-cancel-and-versions).

## Lägen och åtgärder i Content Fragment Editor {#modes-actions-content-fragment-editor}

Det finns olika lägen och åtgärder tillgängliga från Content Fragment Editor.

### Lägen i Content Fragment Editor {#modes-in-the-content-fragment-editor}

Navigera genom de olika lägena med ikonerna på sidopanelen:

* Variationer: [Redigera innehållet](#editing-the-content-of-your-fragment) och [Hantera dina variationer](#creating-and-managing-variations-within-your-fragment)

* [Anteckningar](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment)
* [Associerat innehåll](#associating-content-with-your-fragment)
* [Metadata](#viewing-and-editing-the-metadata-properties-of-your-fragment)
* [Strukturträd](/help/assets/content-fragments/content-fragments-structure-tree.md)
* [Förhandsgranska](/help/assets/content-fragments/content-fragments-json-preview.md)

![lägen](assets/cfm-managing-04.png)

### Verktygsfältsåtgärder i redigeraren för innehållsfragment {#toolbar-actions-in-the-content-fragment-editor}

Vissa funktioner i det övre verktygsfältet finns i flera lägen:

![lägen](assets/cfm-managing-top-toolbar.png)

* Ett meddelande visas när fragmentet redan refereras på en innehållssida. Du kan **stänga** meddelandet.

* Sidpanelen kan döljas/visas med ikonen **Växla sidpanel**.

* Under fragmentnamnet kan du se namnet på den [modell för innehållsfragment](/help/assets/content-fragments/content-fragments-models.md) som används för att skapa det aktuella fragmentet:

   * Namnet är också en länk som öppnar modellredigeraren.

* Se fragmentets status. information om när den skapades, ändrades eller publicerades. Statusen är även färgkodad:

   * **Nytt**: grå
   * **Utkast**: blå
   * **Publicerat**: grön
   * **Ändrad**: orange
   * **Inaktiverad**: röd

* De tre punkterna (**)..**) ger åtkomst till ytterligare åtgärder:
   * **[Snabbpublicering](#publishing-and-referencing-a-fragment)**
   * **[Hantera publikation](#publishing-and-referencing-a-fragment)**

## Spara, Avbryt och Versioner {#save-cancel-and-versions}

>[!NOTE]
>
>Versioner kan också [skapas, jämföras och återställas från tidslinjen](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments).

Redigeraren har två alternativ:

* **Spara**

   Sparar de senaste ändringarna och avslutar redigeraren.

   >[!CAUTION]
   >
   >Om du vill redigera ett innehållsfragment behöver du [de behörigheter som krävs](/help/implementing/developing/extending/content-fragments-customizing.md#asset-permissions). Kontakta systemadministratören om du har problem.

   >[!NOTE]
   >
   >Det går att vara kvar i redigeraren och göra en serie ändringar innan du väljer **Spara**.

   >[!CAUTION]
   >
   >Förutom att bara spara ändringarna uppdaterar **Spara** alla referenser och ser till att Dispatcher rensas efter behov. Dessa ändringar kan ta tid att bearbeta. På grund av detta kan prestandan påverkas på ett stort/komplext/tungt belastat system.
   >
   >
   >Tänk på detta när du använder **Spara** och ange sedan snabbt fragmentredigeraren igen för att göra och spara ytterligare ändringar.

* **Avbryt**

   Redigeraren avslutas utan att de senaste ändringarna sparas.

När du redigerar ditt innehållsfragment skapar AEM automatiskt versioner för att säkerställa att tidigare innehåll kan återställas om du **avbryter** dina ändringar:

1. När ett innehållsfragment öppnas för redigering AEM söker efter den cookie-baserade token som anger om det finns en *redigeringssession*:

   1. Om token hittas betraktas fragmentet som en del av den befintliga redigeringssessionen.
   2. Om token är *inte* tillgänglig och användaren börjar redigera innehåll, skapas en version och en token för den nya redigeringssessionen skickas till klienten, där den sparas i en cookie.

2. När det finns en *aktiv* redigeringssession sparas innehållet som redigeras automatiskt var 600:e sekund (standard).

   >[!NOTE]
   >
   >Intervallet för att spara automatiskt kan konfigureras med hjälp av mekanismen `/conf`.
   >
   >Standardvärde, se:
   >  `/libs/settings/dam/cfm/jcr:content/autoSaveInterval`

3. Om användaren väljer att **avbryta** redigeringen återställs den version som skapades i början av redigeringssessionen och token tas bort för att avsluta redigeringssessionen.
4. Om användaren väljer att **spara** redigeringarna sparas de uppdaterade elementen/varianterna och token tas bort för att avsluta redigeringssessionen.

## Redigera innehållet i fragmentet {#editing-the-content-of-your-fragment}

När du har öppnat fragmentet kan du använda fliken [Variationer](/help/assets/content-fragments/content-fragments-variations.md) för att skapa innehållet.

## Skapa och hantera variationer i fragment {#creating-and-managing-variations-within-your-fragment}

När du har skapat det Överordnad innehållet kan du skapa och hantera [Variationer](/help/assets/content-fragments/content-fragments-variations.md) av det innehållet.

## Koppla innehåll till fragment {#associating-content-with-your-fragment}

Du kan även [associera innehåll](/help/assets/content-fragments/content-fragments-assoc-content.md) med ett fragment. Detta ger en anslutning så att resurser (t.ex. bilder) kan användas (valfritt) med fragmentet när det läggs till på en innehållssida.

## Visa och redigera metadata (egenskaper) för fragmentet {#viewing-and-editing-the-metadata-properties-of-your-fragment}

Du kan visa och redigera egenskaperna för ett fragment på fliken [Metadata](/help/assets/content-fragments/content-fragments-metadata.md).

## Tidslinje för innehållsfragment {#timeline-for-content-fragments}

Förutom standardalternativen innehåller [Tidslinjen](/help/assets/manage-digital-assets.md#timeline) både information och åtgärder som är specifika för innehållsfragment:

* Visa information om versioner, kommentarer och anteckningar
* Åtgärder för versioner

   * **[Återgå till den här versionen](#reverting-to-a-version)**  (välj ett befintligt fragment, sedan en specifik version)

   * **[Jämför med aktuell](#comparing-fragment-versions)**  (välj ett befintligt fragment och sedan en specifik version)

   * Lägg till en **etikett** och/eller **Kommentar** (välj ett befintligt fragment och sedan en specifik version)

   * **Spara som version**  (markera ett befintligt fragment och sedan uppilen längst ned på tidslinjen)

* Åtgärder för anteckningar

   * **Ta bort**

>[!NOTE]
Kommentarerna är:
* Standardfunktionalitet för alla resurser
* Skapat i tidslinjen
* Relaterat till fragmentresursen

Anteckningar (för innehållsfragment) är:
* Anges i fragmentredigeraren
* Specifik för ett markerat textsegment i fragmentet



Till exempel:

![tidslinje](assets/cfm-managing-05.png)

## Jämföra fragmentversioner {#comparing-fragment-versions}

Åtgärden **Jämför med aktuell** är tillgänglig från [tidslinjen](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments) när du har valt en specifik version.

Detta öppnas:

* **Aktuell** (senaste) version (vänster)

* den valda versionen **v&lt;*x.y*>** (höger)

De visas sida vid sida, där:

* Eventuella skillnader markeras

   * Borttagen text - röd
   * Infogad text - grön
   * Ersatt text - blå

* Med helskärmsikonen kan du öppna båda versionerna separat; växla sedan tillbaka till den parallella vyn
* Du kan **återställa** till den specifika versionen
* **** Donewill return you to the console

>[!NOTE]
Du kan inte redigera fragmentinnehållet när du jämför fragment.

![jämföra](assets/cfm-managing-06.png)

## Återställer till version {#reverting-to-a-version}

Du kan återgå till en viss version av fragmentet:

* Direkt från [tidslinjen](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments).

   Välj önskad version och sedan åtgärden **Återställ till denna version**.

* När du jämför en version med den aktuella versionen](/help/assets/content-fragments/content-fragments-managing.md#comparing-fragment-versions) kan du **återställa** till den valda versionen.[

## Publicera och referera till ett fragment {#publishing-and-referencing-a-fragment}

>[!CAUTION]
Om fragmentet är baserat på en modell bör du kontrollera att [modellen har publicerats](/help/assets/content-fragments/content-fragments-models.md#publishing-a-content-fragment-model).
Om du publicerar ett innehållsfragment för vilket modellen ännu inte har publicerats, visas detta i en urvalslista och modellen publiceras med fragmentet.

Innehållsfragment måste publiceras för användning i publiceringsmiljön. De kan publiceras:

* Efter skapande; med [åtgärder som är tillgängliga i resurskonsolen](#actions-for-a-content-fragment-assets-console).
* Från [redigeraren för innehållsfragment](#toolbar-actions-in-the-content-fragment-editor).
* När du [publicerar en sida som använder fragmentet](/help/sites-cloud/authoring/fundamentals/content-fragments.md#publishing); fragmentet kommer att listas i sidreferenserna.

>[!CAUTION]
När ett fragment har publicerats och/eller refererats visar AEM en varning när en författare öppnar fragmentet för redigering igen. Detta är för att varna för att ändringar i avsnittet även påverkar de refererade sidorna.

## Ta bort ett fragment {#deleting-a-fragment}

Så här tar du bort ett fragment:

1. I konsolen **Resurser** navigerar du till platsen för innehållsfragmentet.
2. Markera fragmentet.

   >[!NOTE]
   Åtgärden **Ta bort** är inte tillgänglig som en snabbåtgärd.

3. Välj **Ta bort** från verktygsfältet.
4. Bekräfta åtgärden **Ta bort**.

   >[!CAUTION]
   Om fragmentet redan finns på en sida visas ett varningsmeddelande och du måste bekräfta att du vill fortsätta med **Tvinga borttagning**. Fragmentet, tillsammans med dess innehållskomponentfragment, tas bort från alla innehållssidor.

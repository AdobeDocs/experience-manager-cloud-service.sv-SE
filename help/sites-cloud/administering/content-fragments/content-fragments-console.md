---
title: Konsol för innehållsfragment
description: Lär dig hur du hanterar innehållsfragment från konsolen Innehållsfragment.
landing-page-description: Lär dig hur du hanterar innehållsfragment från konsolen Innehållsfragment som fokuserar på användningen av innehållsfragment i stora volymer för rubrikfria användningsfall, men som även används vid redigering av sidor.
feature: Content Fragments
role: User
exl-id: 0e6e3b61-a0ca-44b8-914d-336e29761579
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '1103'
ht-degree: 0%

---

# Konsol för innehållsfragment  {#content-fragments-console}

Lär dig hur konsolen Innehållsfragment optimerar åtkomsten till dina innehållsfragment så att du kan skapa, söka efter och hantera dem genom att vidta administrativa åtgärder som publicera, avpublicera, kopiera.

Konsolen Innehållsfragment är avsedd för hantering, sökning och skapande av innehållsfragment. Den har optimerats för användning i ett Headless-sammanhang, men används även när innehållsfragment skapas för att användas vid sidredigering.

>[!NOTE]
>
>Den här konsolen visar bara innehållsfragment. Den visar inte andra resurstyper, t.ex. bilder och videoklipp.

>[!NOTE]
>
>Du kan få åtkomst till dina innehållsfragment via:
>
>* this **Innehållsfragment** konsol
>* den **Resurser** konsol - se [Hantera innehållsfragment](/help/assets/content-fragments/content-fragments-managing.md)

>[!NOTE]
>
>Ett urval av [kortkommandon är tillgängliga för användning i den här konsolen](/help/sites-cloud/administering/content-fragments/content-fragments-console-keyboard-shortcuts.md).

>[!NOTE]
>
>Ditt projektteam kan anpassa konsolen om det behövs. Se [Anpassa konsolen för innehållsfragment](/help/implementing/developing/extending/content-fragment-console-customizing.md) för mer information.

Konsolen för innehållsfragment kan nås direkt från den översta nivån i Global Navigation:

![Global navigering - konsol för innehållsfragment](assets/cfc-global-navigation.png)

## Konsolens grundläggande struktur och hantering {#basic-structure-handling-content-fragments-console}

Markera **Innehållsfragment** öppnar konsolen på en ny flik.

![Konsol för innehållsfragment - översikt](assets/cfc-console-overview.png)

Här ser du att det finns tre huvudområden:

* Det övre verktygsfältet
   * Tillhandahåller AEM
   * Visar även din IMS-organisation
* Den vänstra panelen
   * Här kan du dölja, eller visa, mappträdet
   * Du kan välja en viss gren av trädet
   * Storleken kan ändras så att kapslade mappar visas
* Panelen main/right - härifrån kan du:
   * Se listan med alla innehållsfragment i den markerade grenen i trädet:
      * Platsen anges av vägbeskrivningarna. dessa kan också användas för att ändra platsen
      * Innehållsfragment från den valda mappen och alla underordnade mappar visas:
         * [Olika informationsområden](#selectuse-available-columns) om ett innehållsfragment som innehåller länkar, Beroende på vilket fält det gäller kan dessa:
            * Öppna rätt fragment i redigeraren
            * Visa information om referenser
            * Visa information om språkversioner av fragmentet
      * Genom att använda musen på kolumnrubrikerna visas en listruta med åtgärdsväljare och breddreglage. Med dessa kan du göra följande:
         * Sortera - välj lämplig åtgärd för antingen stigande eller fallande Detta sorterar hela tabellen efter den kolumnen. Sortering är bara tillgängligt för lämpliga kolumner.
         * Ändra storlek på kolumnen med antingen funktionsmakrot eller breddreglagen

## Åtgärder {#actions}

I konsolen finns ett antal åtgärder som du kan använda, antingen direkt eller efter att du har valt ett visst fragment:

* Olika åtgärder är direkt [tillgänglig från konsolen](#available-actions)
* Du kan [markera ett eller flera innehållsfragment för att visa lämpliga åtgärder](#actions-selected-content-fragment)

### Åtgärder (omarkerade) {#actions-unselected}

Vissa åtgärder är tillgängliga från konsolen - utan att du behöver välja ett visst innehållsfragment:

* **[Skapa](/help/sites-cloud/administering/content-fragments/content-fragments-managing.md#creating-a-content-fragment)** ett nytt innehållsfragment
* [Filter](#filtering-fragments) innehållsfragment enligt ett urval predikatmallar och spara filtret för framtida bruk
* [Sök](#searching-fragments) innehållsfragment
* [Anpassa tabellvyn så att markerade informationskolumner visas](#select-available-columns)
* Använd **Öppna i resurser** om du vill öppna den aktuella platsen direkt i **Resurser** konsol

  >[!NOTE]
  >
  >The **Resurser** konsolen används för att komma åt resurser, som bilder, videor osv.  Konsolen kan nås:
  >
  >* med **Öppna i resurser** link (in the Content Fragments console)
  >* direkt från den globala navigeringsrutan

### Åtgärder för ett (markerat) innehållsfragment {#actions-selected-content-fragment}

Om du väljer ett visst fragment öppnas ett verktygsfält som fokuserar på de åtgärder som är tillgängliga för det fragmentet. Du kan också markera flera fragment - markeringen av funktionsmakron justeras därefter.

![Konsol för innehållsfragment - verktygsfält för ett valt fragment](assets/cfc-fragment-toolbar.png)

* **Öppna**
* **[Publicera](/help/sites-cloud/administering/content-fragments/content-fragments-managing.md#publishing-and-previewing-a-fragment)** (och **[Avpublicera](/help/sites-cloud/administering/content-fragments/content-fragments-managing.md#unpublishing-a-fragment)**)
* **Kopiera**
* **Flytta**
* **Byt namn**
* **[Ta bort](/help/sites-cloud/administering/content-fragments/content-fragments-managing.md#deleting-a-fragment)**

>[!NOTE]
>
>Åtgärder som Publicera, Avpublicera, Ta bort, Flytta, Byt namn, Kopiera, utlöser ett asynkront jobb. Jobbets förlopp kan övervakas via gränssnittet AEM asynkrona jobb.

## Information om dina innehållsfragment {#information-content-fragments}

Huvudpanelen/den högra panelen (tabellvyn) i konsolen innehåller en rad information om dina innehållsfragment. Vissa objekt har också direkta länkar till ytterligare åtgärder och/eller information:

* **Namn**
   * Tillhandahåller en länk för att öppna fragmentet i redigeraren.
* **Modell**
   * Tillhandahåller en länk för att öppna fragmentet i redigeraren.
* **Mapp**
   * Tillhandahåller en länk för att öppna mappen i konsolen.
Vid hovring över mappnamnet visas JCR-sökvägen.
* **Status**
   * Endast information
* **Förhandsgranska**
   * Endast information:
      * **Synkroniserad**: Innehållsfragmentet är synkroniserat på **Upphovsman** och **Förhandsgranska** tjänster.
      * **Slut på synkronisering**: Innehållsfragmentet är inte synkroniserat på **Upphovsman** och **Förhandsgranska** tjänster. Du måste **Publicera** till **Förhandsgranska** för att säkerställa att de två instanserna återgår till att vara synkroniserade.
      * blank: Innehållsfragmentet finns inte på **Förhandsgranska** service.
* **Ändrad**
   * Endast information
* **Ändrad av**
   * Endast information
* **Publicerad den**
   * Endast information
* **Publicerat av**
   * Endast information
* **Refererad av**

   * Tillhandahåller en länk som öppnar en dialogruta med alla överordnade referenser till det fragmentet. inklusive referenser till innehållsfragment, upplevelsefragment och sidor. Om du vill öppna en viss referens klickar du på **Titel** i dialogrutan.

     ![Konsolen Innehållsfragment - dialogrutan Referenser](assets/cfc-console-references-dialog.png)

* **Språk**

   * Anger språket för innehållsfragmentet tillsammans med det totala antalet språk/språkkopior som är associerade med innehållsfragmentet.

     ![Konsol för innehållsfragment - språkindikator](assets/cfc-console-language-indicator.png)

      * Klicka/tryck på antalet för att öppna en dialogruta som visar alla språkkopior. Om du vill öppna en viss språkkopia klickar du på **Titel** i dialogrutan.

        ![Konsol för innehållsfragment - språkdialogruta](assets/cfc-console-languages-dialog.png)

## Välj tillgängliga kolumner {#select-available-columns}

Precis som med andra konsoler kan du konfigurera de kolumner som är synliga och tillgängliga för åtgärder:

![Konsol för innehållsfragment - kolumnkonfiguration](assets/cfc-console-column-icon.png)

Här visas en lista med kolumner som du kan dölja eller visa:

![Konsol för innehållsfragment - kolumnkonfiguration](assets/cfc-console-column-selection.png)

## Filtrera fragment {#filtering-fragments}

På panelen Filter finns:

* Ett urval av prediater. ett eller flera predikat kan markeras och kombineras för att skapa filtret
* möjlighet att **Spara** din konfiguration
* alternativet att hämta ett sparat sökfilter för återanvändning

![Konsol för innehållsfragment - filtrering](assets/cfc-console-filter.png)

### Snabb filtrering {#fast-filtering}

Du kan också välja ett predikat genom att klicka på ett visst kolumnvärde i listan. Du kan välja ett eller flera värden för att kombinera predikat.

Välj till exempel **Publicerad** i **Status** kolumn:

>[!NOTE]
>
>Snabb filtrering stöds bara för **Modell**, **Status**, **Ändrad av** och **Publicerat av** kolumner.

![Konsol för innehållsfragment - filtrering](assets/cfc-console-fast-filter-01.png)

Efter markeringen visas den som ett filterpredikat och listan filtreras därefter:

![Konsol för innehållsfragment - filtrering](assets/cfc-console-fast-filter-02.png)

## Söka efter fragment {#searching-fragments}

I sökrutan går det att söka i heltext. Ange dina söktermer i sökrutan:

![Konsolen Innehållsfragment - Sökning](assets/cfc-console-search-01.png)

Ger de valda resultaten:

![Konsol för innehållsfragment - sökresultat](assets/cfc-console-search-02.png)

I sökrutan kan du även snabbt komma åt **Senaste innehållsfragment** och **Sparade sökningar**:

![Konsol för innehållsfragment - senaste och sparade](assets/cfc-console-search-03.png)

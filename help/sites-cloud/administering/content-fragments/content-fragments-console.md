---
title: Konsol för innehållsfragment
description: Lär dig hur du hanterar innehållsfragment från konsolen Innehållsfragment.
landing-page-description: Lär dig hur du hanterar innehållsfragment från konsolen Innehållsfragment som fokuserar på användning av innehållsfragment i stora volymer för Headless-fall, men som även används vid redigering av sidor.
source-git-commit: 8c44ecf0237c7a3660ef9fa97f46cc400e4bd30f
workflow-type: tm+mt
source-wordcount: '551'
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


Konsolen för innehållsfragment kan nås direkt från den översta nivån i Global Navigation:

![Global navigering - konsol för innehållsfragment](assets/cfc-global-navigation.png)

Markera **Innehållsfragment** öppnar konsolen på en ny flik.

![Konsol för innehållsfragment - översikt](assets/cfc-console-overview.png)

Här ser du att det finns tre huvudområden:

* Det övre verktygsfältet
   * Tillhandahåller AEM
   * Visar även din IMS-organisation
* Den vänstra panelen
   * Här kan du dölja, eller visa, mappträdet
   * Du kan välja en viss gren av trädet
* Panelen main/right - härifrån kan du:
   * Se listan med alla innehållsfragment i den markerade grenen i trädet
      * Platsen anges av vägbeskrivningarna. dessa kan också användas för att ändra platsen
      * Innehållsfragment från den markerade mappen och alla underordnade mappar visas
         * Olika informationsområden om ett innehållsfragment innehåller länkar. kan dessa öppna rätt fragment i redigeraren
      * Du kan välja en kolumnrubrik för att sortera tabellen efter den kolumnen; välj igen för att växla mellan stigande och fallande
   * **[Skapa](#creating-new-content-fragment)** ett nytt innehållsfragment
   * [Filter](#filtering-fragments) innehållsfragment enligt ett urval predikatmallar och spara filtret för framtida bruk
   * [Sök](#searching-fragments) innehållsfragment
   * Anpassa tabellvyn så att markerade informationskolumner visas
   * Använd **Öppna i resurser** om du vill öppna den aktuella platsen direkt i **Resurser** konsol.

      >[!NOTE]
      >
      >The **Resurser** konsolen används för att komma åt resurser, som bilder, videor osv.  Konsolen kan nås:
      >
      >* med **Öppna i resurser** link (in the Content Fragments console)
      >* direkt från den globala navigeringsrutan


Om du väljer ett visst fragment öppnas ett verktygsfält som fokuserar på de åtgärder som är tillgängliga för det fragmentet. Du kan också markera flera fragment. Markeringen av funktionsmakron justeras därefter.

![Konsol för innehållsfragment - verktygsfält för ett valt fragment](assets/cfc-fragment-toolbar.png)

## Skapa ett nytt innehållsfragment {#creating-new-content-fragment}

Markera **Skapa** öppnar komprimeringen **Nytt innehållsfragment** dialog:

![Konsol för innehållsfragment - Skapa ett nytt fragment](assets/cfc-console-create.png)

## Filtrera fragment {#filtering-fragments}

På panelen Filter finns:

* ett urval av predikat som kan markeras och kombineras
* möjlighet att **Spara** din konfiguration
* alternativet att hämta ett sparat sökfilter för återanvändning

![Konsol för innehållsfragment - filtrering](assets/cfc-console-filter.png)

## Söka efter fragment {#searching-fragments}

I sökrutan går det att söka i heltext. Ange dina söktermer i sökrutan:

![Konsolen Innehållsfragment - Sökning](assets/cfc-console-search-01.png)

Ger de valda resultaten:

![Konsol för innehållsfragment - sökresultat](assets/cfc-console-search-02.png)

I sökrutan kan du även snabbt komma åt **Senaste innehållsfragment** och **Sparade sökningar**:

![Konsol för innehållsfragment - senaste och sparade](assets/cfc-console-search-03.png)

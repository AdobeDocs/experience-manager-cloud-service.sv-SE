---
title: Din inkorg
description: Hantera dina uppgifter med inkorgen
translation-type: tm+mt
source-git-commit: 672f1483c017d791365173c91b0bee5c44c33535
workflow-type: tm+mt
source-wordcount: '913'
ht-degree: 15%

---


# Din inkorg {#your-inbox}

Du kan få meddelanden från olika AEM, inklusive arbetsflöden och projekt. Du kan till exempel få meddelanden om:

* Uppgifter:
   * Dessa kan också skapas vid olika punkter i AEM, t.ex. under **Projekt**.
   * Dessa kan ha sitt ursprung i arbetsflödessteget **Skapa uppgift** eller **Skapa projektuppgift**.
* Arbetsflöden:
   * Arbetsobjekt som representerar åtgärder som du behöver utföra på sidinnehåll
      * Detta är produkten av arbetsflödets **deltagarsteg** .
   * Misslyckade objekt, så att administratörer kan försöka igen

Du får dessa meddelanden i din egen Inkorg där du kan visa dem och vidta åtgärder.

>[!NOTE]
>
>Mer information om objekttyperna finns även i:
>
>* [Projekt](/help/sites-cloud/authoring/projects/overview.md)
>* [Projekt - arbeta med uppgifter](/help/sites-cloud/authoring/projects/tasks.md)
>* [Arbetsflöden](/help/sites-cloud/authoring/workflows/overview.md)


## Inkorgen i sidhuvudet {#inbox-in-the-header}

Från någon av konsolerna visas det aktuella antalet objekt i din inkorg i sidhuvudet. Indikatorn kan också öppnas för att ge snabb åtkomst till sidan/sidorna som kräver åtgärder eller åtkomst till inkorgen:

![Översikt över Inkorgen i rubriken](/help/sites-cloud/authoring/assets/inbox-header.png)

>[!NOTE]
>
>Vissa åtgärder visas även i [kortvyn för den aktuella resursen](/help/sites-cloud/authoring/getting-started/basic-handling.md#card-view).

## Öppna Inkorgen {#opening-the-inbox}

Så här öppnar du AEM inkorg:

1. Klicka/tryck på indikatorn i verktygsfältet.

1. Välj **Visa alla**. **AEM -inkorgen** öppnas. I inkorgen visas objekt från arbetsflöden, projekt och uppgifter.
1. Standardvyn är [Listvy](#inbox-list-view), men du kan även växla till [Kalendervy](#inbox-calendar-view). Detta görs med vyväljaren (verktygsfält, överst till höger).

   För båda vyerna kan du även definiera [visningsinställningar](#inbox-view-settings). Vilka alternativ som är tillgängliga beror på den aktuella vyn.

   ![Inställningar för Inkorgsvy](/help/sites-cloud/authoring/assets/inbox-view-settings.png)

>[!NOTE]
>
>Inkorgen fungerar som en konsol, och du kan använda [Global navigering](/help/sites-cloud/authoring/getting-started/basic-handling.md#global-navigation) eller [Sök](/help/sites-cloud/authoring/getting-started/search.md) för att navigera till en annan plats när du är klar.

### Inkorg - listvy {#inbox-list-view}

I den här vyn visas alla objekt tillsammans med relevant information:

![Listvy i Inkorgen](/help/sites-cloud/authoring/assets/inbox-list-view.png)

### Inkorg - kalendervy {#inbox-calendar-view}

I den här vyn visas objekt efter deras placering i kalendern:

![Kalendervy för inkorg](/help/sites-cloud/authoring/assets/inbox-calendar-view.png)

Du kan:

* Välj en specifik vy: **Tidslinje**, **kolumn**, **lista**
* Ange de uppgifter som ska visas enligt **Schema**: **Alla**, **Planerade**, **Pågående**, **Förfaller snart**, **Förfallna**
* Detaljerad information om ett objekt
* Välj ett datumintervall som vyn ska fokuseras i:

![Inkorgskalenderns datumintervall](/help/sites-cloud/authoring/assets/inbox-calendar-range.png)

### Inkorg - Visa inställningar {#inbox-view-settings}

För båda vyerna (List och Calendar) kan du definiera inställningar:

* **Kalendervy**

   I **kalendervyn** kan du konfigurera:

   * **Gruppera efter**
   * **Schema** eller **Ingen**
   * **Kortstorlek**

   ![Visningsinställningar för inkorgskalender](/help/sites-cloud/authoring/assets/inbox-calendar-settings.png)

* **Listvy**

   I **listvyn** kan du konfigurera sorteringsmekanismen:

   * **Sortera efter**
   * **Sorteringsordning**

   ![Visningsinställningar för inkorgslista](/help/sites-cloud/authoring/assets/inbox-list-settings.png)

   Du kan även delegera din kalender till andra användare samt begära delegering från andra användare och hantera dina delegeringar.

   ![Visningsdelegeringsinställningar för inkorgslista](/help/sites-cloud/authoring/assets/inbox-delegation.png)

## Vidta åtgärder för ett objekt {#taking-action-on-an-item}

>[!NOTE]
>
>Även om det går att markera mer än ett objekt, kan åtgärder bara vidtas för ett objekt i taget.

1. Om du vill utföra en åtgärd för ett objekt markerar du miniatyrbilden för det aktuella objektet. Ikoner för de åtgärder som är tillämpliga på det objektet visas i verktygsfältet:

   ![Markera inkorgsobjekt](/help/sites-cloud/authoring/assets/inbox-select-item.png)

   Åtgärderna är lämpliga för objektet och omfattar:

   * **Fullständig** åtgärd
   * **Delegera** ett objekt
   * **Öppna** ett objekt, beroende på objekttyp kan den här åtgärden:

      * Visa objektegenskaper
      * Öppna en lämplig kontrollpanel eller guide för ytterligare åtgärder
      * Öppna relaterad dokumentation
   * **Gå tillbaka** till föregående steg
   * Visa nyttolasten för ett arbetsflöde
   * Skapa ett projekt från artikeln

   >[!NOTE]
   >
   >Mer information finns i:
   >
   >* Arbetsflödesobjekt - [delta i arbetsflöden](/help/sites-cloud/authoring/workflows/participating.md)


2. Beroende på vilket objekt som är markerat startas en åtgärd, till exempel:

   * En dialogruta som är lämplig för åtgärden öppnas
   * En åtgärdsguide startas
   * En dokumentationssida öppnas

   En dialogruta öppnas t.ex. av **Delegera** :

   ![Delegera inkorgsaktivitet](/help/sites-cloud/authoring/assets/inbox-assign-task.png)

   Beroende på om en dialogruta, guide, dokumentationssida har öppnats kan du:

   * Bekräfta lämplig åtgärd, t.ex. omtilldelning.
   * Avbryt åtgärden
   * Välj bakåtpilen för att återgå till inkorgen, t.ex. om en åtgärdsguide eller dokumentationssida har öppnats, kan du gå tillbaka till Inkorgen.


## Skapa en uppgift {#creating-a-task}

I inkorgen kan du skapa uppgifter:

1. Välj **Skapa** och sedan **Aktivitet**.
1. Fyll i de nödvändiga fälten på flikarna **Grundläggande** och **Avancerat** (endast **Titel** är obligatoriskt, alla andra är valfria):

   * **Grundläggande**:

      * **Titel**
      * **Projekt**
      * **Tilldelad**
      * **Innehåll**, ungefär som nyttolast, är en referens från aktiviteten till en plats i databasen
      * **Beskrivning**
      * **Aktivitetsprioritet**
      * **Startdatum**
      * **Förfallodatum**

   ![Lägg till uppgift i Inkorgen](/help/sites-cloud/authoring/assets/inbox-create-task.png)

   * **Avancerat**

      * **Namn**: Detta används för att skapa URL:en och om det är tomt baseras det på **titeln**.

   ![Inkorgen lägger till avancerade alternativ för uppgifter](/help/sites-cloud/authoring/assets/inbox-add-task-advanced.png)

1. Välj **Skicka**.

## Skapa ett projekt {#creating-a-project}

För vissa uppgifter kan du skapa ett [projekt](/help/sites-cloud/authoring/projects/overview.md) baserat på den uppgiften:

1. Välj lämplig åtgärd genom att trycka/klicka på miniatyrbilden.

   >[!NOTE]
   >
   >Endast uppgifter som skapats med alternativet **Skapa** i **Inkorgen** kan användas för att skapa ett projekt.
   >
   >Arbetsobjekt (från ett arbetsflöde) kan inte användas för att skapa ett projekt.

1. Välj **Skapa projekt** i verktygsfältet för att öppna guiden.
1. Select the appropriate template, then **Next**.
1. Ange de nödvändiga egenskaperna:

   * **Grundläggande**

      * **Titel**
      * **Beskrivning**
      * **Startdatum**
      * **Förfallodatum**
      * **Användare** och roll
   * **Avancerat**

      * **Namn**
   >[!NOTE]
   >
   >Mer information finns i [Skapa ett projekt](/help/sites-cloud/authoring/projects/managing.md#creating-a-project) .

1. Bekräfta åtgärden genom att välja **Skapa** .

## Filtrera objekt i AEM {#filtering-items-in-the-aem-inbox}

Du kan filtrera objekten i listan:

1. Öppna **AEM**.

1. Öppna filterväljaren:

   ![Inkorgssökning](/help/sites-cloud/authoring/assets/inbox-search.png)

1. Du kan filtrera de listade objekten enligt ett intervall med villkor, varav många kan förfinas. Till exempel:

   ![Inkorgssökfilter](/help/sites-cloud/authoring/assets/inbox-search-filter.png)

   >[!NOTE]
   >
   >Med [visningsinställningar](#inbox-view-settings) kan du även konfigurera sorteringsordningen när du använder [listvyn](#inbox-list-view).

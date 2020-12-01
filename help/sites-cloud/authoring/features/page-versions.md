---
title: Arbeta med sidversioner
description: Skapa, jämföra och återställa versioner av en sida
translation-type: tm+mt
source-git-commit: 83c6301cd804ea1bb41204cf68d9a8de0b373678
workflow-type: tm+mt
source-wordcount: '1521'
ht-degree: 4%

---


# Arbeta med sidversioner {#working-with-page-versions}

Versionshantering skapar en ögonblicksbild av en sida vid en viss tidpunkt. Med versionshantering kan du utföra följande åtgärder:

* Skapa en version av en sida.
* Återskapa en tidigare version av en eller flera sidor till:
   * Ångra ändringar som gjorts på sidorna.
   * Återställ sidor som har tagits bort.
   * Återställ ett träd (som angivet datum och tid).
* Förhandsgranska en version.
* Jämför den aktuella versionen av en sida med en tidigare version.
   * Skillnader i text och bilder markeras.
* Timewarp använder sidversionerna för att avgöra publiceringsmiljöns tillstånd.

## Skapa en ny version {#creating-a-new-version}

Du kan skapa en version av resursen från:

* [Tidslinjen](#creating-a-new-version-timeline)
* Alternativet [Skapa](#creating-a-new-version-create-with-a-selected-resource) (när en resurs har valts)

### Skapar en ny version - Tidslinje {#creating-a-new-version-timeline}

1. Navigera till sidan som du vill skapa en version för.
1. Markera sidan i [markeringsläge](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources).
1. Öppna **tidslinjen**.
1. Klicka/tryck på ellipsen i kommentarfältet för att visa alternativen:

   ![Versioner i tidslinjen](/help/sites-cloud/authoring/assets/versions-timeline-rail.png)

1. Välj **Spara som version**.
1. Ange en **etikett** och **Kommentar** om det behövs.

   ![Lägg till etikett för en version](/help/sites-cloud/authoring/assets/versions-add-label.png)

1. Bekräfta den nya versionen med **Skapa**.

   Informationen i tidslinjen uppdateras för att ange den nya versionen.

### Skapa en ny version - Skapa med en markerad resurs {#creating-a-new-version-create-with-a-selected-resource}

1. Navigera till sidan som du vill skapa en version för.
1. Markera sidan i [markeringsläge](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources).
1. Välj alternativet **Skapa** i verktygsfältet.
1. Samma dialogruta öppnas. Du kan ange en **etikett** och en **kommentar** om det behövs.
1. Bekräfta den nya versionen med **Skapa**.

Tidslinjen öppnas och informationen uppdateras för att ange den nya versionen.

## Återställer versioner {#reinstating-versions}

När du har skapat en version av sidan finns det olika metoder för att återställa en tidigare version:

* alternativet **Återställ till denna version** från [tidslinjen](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline)

   Återskapa en tidigare version av en markerad sida.

* **Återställ**-alternativen i det övre [verktygsfältet Åtgärder](/help/sites-cloud/authoring/getting-started/basic-handling.md#actions-toolbar)

   * **Återställ version**

      Återställa versioner av angivna sidor i den markerade mappen; detta kan även omfatta återställning av sidor som tidigare har tagits bort.

   * **Återställ träd**

      återinför en version av ett helt träd vid ett angivet datum och en viss tidpunkt, kan innehålla sidor som tidigare har tagits bort.

>[!NOTE]
>
>När du återställer en sida blir den skapade versionen en del av en ny gren.
>
>Så här illustrerar du:
>
>1. Skapa versioner av valfri sida.
>1. De inledande etiketterna och versionsnodnamnen är 1.0, 1.1, 1.2 och så vidare.
>1. återställ den första versionen, dvs. 1.0.
>1. Skapa nya versioner igen.
>1. De genererade etiketterna och nodnamnen blir nu 1.0.0, 1.0.1, 1.0.2 osv.


### Återgå till version {#revert-to-a-version}

Om du vill **återställa** den markerade sidan till en tidigare version:

1. Navigera till sidan som du vill återställa till en tidigare version.
1. Markera sidan i [markeringsläge](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources).
1. Öppna kolumnen **Tidslinje** och välj antingen **Visa alla** eller **Versioner**. Sidversionerna för den valda sidan visas.
1. Välj den version som du vill återställa till. Möjliga alternativ visas:

   ![Återgå till den här versionen](/help/sites-cloud/authoring/assets/versions-revert.png)

1. Välj **Återställ till denna version**. Den valda versionen återställs och informationen på tidslinjen uppdateras.

### Återställ version {#restore-version}

Denna metod kan användas för att återställa versioner av angivna sidor i den aktuella mappen; Detta kan även omfatta återställning av sidor som tidigare har tagits bort:

1. Navigera till och [markera](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources) den obligatoriska mappen.

1. Välj **Återställ** och sedan **Återställ version** i det övre verktygsfältet för [åtgärder](/help/sites-cloud/authoring/getting-started/basic-handling.md#actions-toolbar).

   >[!NOTE]
   >
   >Om:
   >* du har valt en sida som aldrig har haft några underordnade sidor,
   >* eller ingen av sidorna i mappen har versioner,

   >
   >Då är visningen tom eftersom det inte finns några tillämpliga versioner.

1. De tillgängliga versionerna visas:

   ![Återställ version - Lista över alla sidor i mappen](/help/sites-cloud/authoring/assets/versions-restore-version-01.png)

1. Använd listruteväljaren under **ÅTERSTÄLL TILL VERSION** för att välja önskad version för en viss sida.

   ![Återställ version - Välj version](/help/sites-cloud/authoring/assets/versions-restore-version-02.png)

1. Markera den sida som ska återställas i huvudskärmen:

   ![Återställ version - Välj sida](/help/sites-cloud/authoring/assets/versions-restore-version-03.png)

1. Välj **Återställ** för den valda versionen av den valda sidan som ska återställas som den aktuella versionen.

>[!NOTE]
>
>Den ordning i vilken du väljer en obligatorisk sida och den relaterade versionen är utbytbara.

### Återställ träd {#restore-tree}

Den här metoden kan användas för att återställa en version av ett träd vid ett angivet datum och en viss tidpunkt. detta kan omfatta sidor som tidigare har tagits bort:

1. Navigera till och [markera](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources) den obligatoriska mappen.

1. Välj **Återställ** och **Återställ träd** i det övre verktygsfältet för [åtgärder](/help/sites-cloud/authoring/getting-started/basic-handling.md#actions-toolbar). Trädets senaste version visas:

   ![Återställ träd](/help/sites-cloud/authoring/assets/versions-restore-tree-01.png)

1. Använd datum- och tidsväljaren på **Senaste versioner på Date** för att välja en annan version av trädet - den som ska återställas.

1. Ange flaggan **Bevarade icke-versionshanterade sidor** efter behov:

   * Om den är aktiv (markerad) bevaras alla sidor som inte är versionshanterade och påverkas inte av återställningen.

   * Om alternativet är inaktivt (omarkerat) tas alla sidor som inte är versionshanterade bort eftersom de inte fanns i versionsträdet.

1. Välj **Återställ** för den valda versionen av trädet som ska återställas som den *aktuella* versionen.

## Förhandsgranska version {#previewing-a-version}

Du kan förhandsgranska en viss version:

1. Navigera till den sida som du vill jämföra.
1. Markera sidan i [markeringsläge](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources).
1. Öppna kolumnen **Tidslinje** och välj antingen **Visa alla** eller **Versioner**.
1. Sidversionerna visas. Markera den version som du vill förhandsgranska:

   ![Förhandsgranska version](/help/sites-cloud/authoring/assets/versions-revert.png)

1. Välj **Förhandsgranska**. Sidan visas på en ny flik.

   >[!CAUTION]
   >
   >Om en sida har flyttats kan du inte längre förhandsgranska versioner som gjorts före flyttningen.
   >
   >Om du får problem med en förhandsgranskning kan du kontrollera [tidslinjen](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline) för sidan för att se om sidan har flyttats.

## Jämföra en version med den aktuella sidan {#comparing-a-version-with-current-page}

Så här jämför du en tidigare version med den aktuella sidan:

1. Navigera till den sida som du vill jämföra.
1. Markera sidan i [markeringsläge](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources).
1. Öppna kolumnen **Tidslinje** och välj antingen **Visa alla** eller **Versioner**.
1. Sidversionerna visas. Välj den version du vill jämföra:

   ![Jämför versioner](/help/sites-cloud/authoring/assets/versions-revert.png)

1. Välj **Jämför med aktuell**. Skillnaden mellan [sidorna](/help/sites-cloud/authoring/features/page-diff.md) öppnas och visas.

## Timewarp {#timewarp}

Timewarp är en funktion som är utformad för att simulera *publicerat*-läge för en sida vid en viss tidpunkt.

>[!NOTE]
>
>[Timewarp kan även användas med Launches för att förhandsgranska framtiden](/help/sites-cloud/authoring/launches/preview.md).

Eftersom framtagning av innehåll är en pågående och samarbetsorienterad process är syftet med Timewarp att tillåta författare att spåra den publicerade webbplatsen över tid för att förstå hur innehållet har ändrats. Den här funktionen använder sidversionerna för att avgöra publiceringsmiljöns tillstånd.

Så här gör du:

* Systemet söker efter den sidversion som var aktiv vid den valda tidpunkten.
* Det innebär att den visade versionen skapades/aktiverades *före* den tidpunkt som valdes i Timewarp.
* När du navigerar till en sida som har tagits bort återges den också, så länge som de gamla versionerna av sidan fortfarande är tillgängliga i databasen.
* Om ingen publicerad version hittas återgår Timewarp till sidans aktuella status i redigeringsmiljön (detta för att förhindra ett fel/404-sida, vilket skulle förhindra bläddring).

### Använda Timewarp {#using-timewarp}

Timewarp är ett [läge](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes) för sidredigeraren. Du startar det genom att helt enkelt växla det på samma sätt som andra lägen.

1. Starta redigeraren för sidan där du vill starta Timewarp och välj sedan **Timewarp** i lägesvalet.

   ![Timewarp, läge](/help/sites-cloud/authoring/assets/versions-timewarp-mode.png)

1. Ange ett måldatum och en måltid i dialogrutan och klicka eller tryck på **Ange datum**. Om du inte väljer någon tid används den aktuella tiden som standard.

   ![Måldatum för tidstänjning](/help/sites-cloud/authoring/assets/versions-timewarp-target.png)

1. Sidan visas baserat på det angivna datumet. Timewarp-läget indikeras via det blå statusfältet högst upp i fönstret. Använd länkarna i statusfältet för att välja ett nytt måldatum eller avsluta Timewarp-läget.

   ![I läget Timewarp](/help/sites-cloud/authoring/assets/versions-timewarp.png)

### Begränsningar för tidsförvrängning {#timewarp-limitations}

Med Timewarp kan du göra ett bra försök att återskapa en sida vid en viss tidpunkt. På grund av komplexiteten i den kontinuerliga redigeringen av innehåll i AEM är detta dock inte alltid möjligt. Dessa begränsningar bör beaktas när du använder Timewarp.

* **Timewarp fungerar baserat på publicerade sidor**  - Timewarp fungerar bara helt om du tidigare har publicerat sidan. I annat fall visas den aktuella sidan i författarmiljön.
* **Vid tidsförvrängning används sidversioner** - Om du navigerar till en sida som har tagits bort/tagits bort från databasen kommer den att återges korrekt om gamla versioner av sidan fortfarande är tillgängliga i databasen.
* **Borttagna versioner påverkar Timewarp** - Om versioner tas bort från databasen kan inte Timewarp visa rätt vy.
* **Timewarp är skrivskyddat**  - Du kan inte redigera den gamla versionen av sidan. Det är bara tillgängligt för visning. Om du vill återställa den äldre versionen måste du göra det manuellt med [restore](#revert-to-a-version).
* **Timewarp baseras bara på sidinnehåll**  - Om element (som kod, css, resurser/bilder osv.) för återgivning av webbplatsen har ändrats, skiljer sig vyn från den ursprungliga vyn eftersom objekten inte har versionsindelats i databasen.

>[!CAUTION]
>
>Timewarp är ett verktyg som hjälper författare att förstå och skapa sitt innehåll. Den är inte avsedd som en revisionslogg eller för juridiska ändamål.

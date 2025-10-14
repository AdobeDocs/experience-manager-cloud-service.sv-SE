---
title: Arbeta med sidversioner
description: Lär dig hur du skapar, jämför och återställer versioner av dina sidor i AEM.
exl-id: 33d8e43c-594d-4bba-9631-b2c42a1e910f
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: ebbf38563be65c28384276f7a0baa100f9f384b2
workflow-type: tm+mt
source-wordcount: '1620'
ht-degree: 2%

---

# Arbeta med sidversioner {#working-with-page-versions}

Versionshantering skapar en ögonblicksbild av en sida vid en viss tidpunkt. Med versionshantering kan du utföra följande åtgärder:

* Skapa en sidversion.
* Återskapa en tidigare version av en eller flera sidor till:
   * Ångra ändringar som gjorts på sidorna.
   * Återställ sidor som har tagits bort.
   * Återställ ett träd (som angivet datum och tid).
* Förhandsgranska en version.
* Jämför den aktuella versionen av en sida med en tidigare version.
   * Skillnader i text och bilder markeras.
* Timewarp använder sidversionerna för att avgöra publiceringsmiljöns tillstånd.

>[!NOTE]
>
>Endast innehåll versionshanteras i AEM-databasen. Dynamiska resurser som kod, CSS och JavaScript är inte versionshanterade.
>
>* När du visar versioner visas innehållet med den aktuella koden, CSS och JavaScript för databasen.
>* När du återställer versioner återställs endast innehållet och den aktuella koden, CSS och JavaScript för databasen tillämpas på det.

## Skapa en ny version {#creating-a-new-version}

Du kan skapa en version av resursen från:

* [Tidslinjerska](#creating-a-new-version-timeline)
* Alternativet [Skapa](#creating-a-new-version-create-with-a-selected-resource) (när en resurs har valts)

### Skapa en ny version - Tidslinje {#creating-a-new-version-timeline}

1. Navigera till sidan som du vill skapa en version för.
1. Markera sidan i [markeringsläge](/help/sites-cloud/authoring/basic-handling.md#viewing-and-selecting-resources).
1. Öppna **tidslinjen**.
1. Markera ellipsen i kommentarfältet för att visa alternativen:

   ![Versioner på tidslinjen](/help/sites-cloud/authoring/assets/versions-timeline-rail.png)

1. Välj **Spara som version**.
1. Ange en **etikett** och **kommentar** om det behövs.

   ![Lägg till etikett för en version](/help/sites-cloud/authoring/assets/versions-add-label.png)

1. Bekräfta den nya versionen med **Create**.

   Informationen i tidslinjen uppdateras för att ange den nya versionen.

### Skapa en ny version - Skapa med en markerad resurs {#creating-a-new-version-create-with-a-selected-resource}

1. Navigera till sidan som du vill skapa en version för.
1. Markera sidan i [markeringsläge](/help/sites-cloud/authoring/basic-handling.md#viewing-and-selecting-resources).
1. Välj alternativet **Skapa** i verktygsfältet.
1. Samma dialogruta öppnas. Om det behövs kan du ange en **etikett** och en **kommentar**.
1. Bekräfta den nya versionen med **Create**.

Tidslinjen öppnas med informationen uppdaterad för att ange den nya versionen.

## Återställer versioner {#reinstating-versions}

När du har skapat en version av sidan finns det olika metoder för att återställa en tidigare version:

* alternativet **Återgå till den här versionen** från [tidslinjen](/help/sites-cloud/authoring/basic-handling.md#timeline)

  Återskapa en tidigare version av en markerad sida.

* **Återställ**-alternativen i det övre verktygsfältet för [åtgärder](/help/sites-cloud/authoring/basic-handling.md#actions-toolbar)

   * **Återställ version**

     Återställ versioner av angivna sidor i den markerade mappen. Det kan även omfatta återställning av sidor som tidigare har tagits bort.

   * **Återställ träd**

     Återskapa en version av ett helt träd vid ett angivet datum och en angiven tid. Den kan även innehålla sidor som tidigare har tagits bort.

>[!NOTE]
>
>När du återställer en sida är den skapade versionen en del av en ny gren.
>
>Så här illustrerar du:
>
>1. Skapa versioner av valfri sida.
>1. De inledande etiketterna och versionsnodnamnen är 1.0, 1.1, 1.2 och så vidare.
>1. Återställ den första versionen, d.v.s. 1.0.
>1. Skapa versioner igen.
>1. De genererade etiketterna och nodnamnen är nu 1.0.0, 1.0.1, 1.0.2 och så vidare.

### Återgå till en version {#revert-to-a-version}

Så här **återställer du** den markerade sidan till en tidigare version:

1. Navigera till sidan som du vill återställa till en tidigare version.
1. Markera sidan i [markeringsläge](/help/sites-cloud/authoring/basic-handling.md#viewing-and-selecting-resources).
1. Öppna kolumnen **Tidslinje** och välj antingen **Visa alla** eller **Versioner**. Sidversionerna för den valda sidan visas.
1. Välj den version som du vill återställa till. Möjliga alternativ visas:

   ![Återgå till den här versionen](/help/sites-cloud/authoring/assets/versions-revert.png)

1. Välj **Återgå till den här versionen**. Den valda versionen återställs och informationen på tidslinjen uppdateras.

### Återställ version {#restore-version}

Den här metoden kan användas för att återställa versioner av angivna sidor i den aktuella mappen. Den kan även omfatta återställning av sidor som tidigare har tagits bort:

1. Navigera till och [markera](/help/sites-cloud/authoring/basic-handling.md#viewing-and-selecting-resources) den obligatoriska mappen.

1. Välj **Återställ** och sedan **Återställ version** i det övre verktygsfältet [Åtgärder](/help/sites-cloud/authoring/basic-handling.md#actions-toolbar).

   >[!NOTE]
   >
   >Om du har:
   >
   >* har markerat en enda sida som aldrig har haft några underordnade sidor,
   >* eller ingen av sidorna i mappen har versioner,
   >
   >Visningen blir tom eftersom det inte finns några tillämpliga versioner.

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

Den här metoden kan användas för att återställa en version av ett träd vid ett angivet datum och en angiven tid. Den kan innehålla sidor som tidigare har tagits bort:

1. Navigera till och [markera](/help/sites-cloud/authoring/basic-handling.md#viewing-and-selecting-resources) den obligatoriska mappen.

1. Välj **Återställ** och sedan **Återställ träd** i det övre verktygsfältet [Åtgärder](/help/sites-cloud/authoring/basic-handling.md#actions-toolbar). Trädets senaste version visas:

   ![Återställ träd](/help/sites-cloud/authoring/assets/versions-restore-tree-01.png)

1. Använd datum- och tidsväljaren vid **Senaste versioner vid datum** så att du kan välja en annan version av trädet, den som ska återställas.

1. Ange flaggan **Bevarade icke-versionshanterade sidor** efter behov:

   * Om den är aktiv (markerad) bevaras alla sidor som inte är versionshanterade och påverkas inte av återställningen.

   * Om sidan är inaktiv (omarkerad) tas alla sidor som inte är versionshanterade bort eftersom de inte fanns i versionsträdet.

1. Välj **Återställ** för den valda versionen av trädet som ska återställas som den *aktuella* versionen.

## Förhandsgranska en version {#previewing-a-version}

Du kan förhandsgranska en viss version:

1. Navigera till sidan som du vill jämföra.
1. Markera sidan i [markeringsläge](/help/sites-cloud/authoring/basic-handling.md#viewing-and-selecting-resources).
1. Öppna kolumnen **Tidslinje** och välj antingen **Visa alla** eller **Versioner**.
1. Sidversionerna visas. Välj den version som du vill förhandsgranska:

   ![Förhandsgranska version](/help/sites-cloud/authoring/assets/versions-revert.png)

1. Välj **Förhandsgranska**. Sidan visas på en ny flik.

   >[!CAUTION]
   >
   >Om en sida har flyttats kan du inte längre förhandsgranska versioner som gjorts före flyttningen.
   >
   >Om du får problem med en förhandsgranskning kan du kontrollera [tidslinjen](/help/sites-cloud/authoring/basic-handling.md#timeline) för sidan för att se om sidan har flyttats.

## Jämföra en version med den aktuella sidan {#comparing-a-version-with-current-page}

Så här jämför du en tidigare version med den aktuella sidan:

1. Navigera till sidan som du vill jämföra.
1. Markera sidan i [markeringsläge](/help/sites-cloud/authoring/basic-handling.md#viewing-and-selecting-resources).
1. Öppna kolumnen **Tidslinje** och välj antingen **Visa alla** eller **Versioner**.
1. Sidversionerna visas. Välj den version som du vill jämföra:

   ![Jämför versioner](/help/sites-cloud/authoring/assets/versions-revert.png)

1. Välj **Jämför med aktuell**. [Sidskillnaden &#x200B;](/help/sites-cloud/authoring/sites-console/page-diff.md) öppnas och skillnaderna visas.

## Timewarp {#timewarp}

Timewarp är en funktion som har utformats för att simulera en sidas *publicerade*-läge vid en viss tidpunkt.

Eftersom framtagning av innehåll är en pågående och samarbetsorienterad process är syftet med Timewarp att tillåta författare att spåra den publicerade webbplatsen över tid så att de kan förstå hur innehållet har ändrats. Den här funktionen använder sidversionerna för att avgöra publiceringsmiljöns tillstånd.

Så här använder du funktionen:

* Systemet söker efter den sidversion som var aktiv vid den valda tidpunkten.
* Det betyder att den visade versionen skapades/aktiverades *före* den tidpunkt som valdes i Timewarp.
* När du navigerar till en sida som har tagits bort återges den också, så länge som de gamla versionerna av sidan fortfarande är tillgängliga i databasen.
* Om ingen publicerad version hittas återgår Timewarp till det aktuella läget för sidan i författarmiljön (orsaken är att förhindra ett fel/404-sida, vilket skulle förhindra bläddring).

>[!NOTE]
>
>Timewarp fungerar och är avsett att användas för AEM-sidor - versioner för historik och starter för framtida innehållslägen.
>
>Det fungerar inte för kapslade starter eller när upplevelsefragment används.

>[!TIP]
>
>[Timewarp kan också användas med Launches (Starta) för att förhandsgranska framtiden](/help/sites-cloud/authoring/launches/preview.md).

### Använda Timewarp {#using-timewarp}

Timewarp är ett [läge](/help/sites-cloud/authoring/page-editor/introduction.md#page-modes) i sidredigeraren. Du startar det genom att helt enkelt växla det på samma sätt som andra lägen.

1. Starta redigeraren för sidan där du vill starta Timewarp och välj sedan **Timewarp** i lägesvalet.

   ![Timewarp-läge](/help/sites-cloud/authoring/assets/versions-timewarp-mode.png)

1. Ange ett måldatum och en måltid i dialogrutan och klicka på **Ange datum**. Om du inte väljer en tid används den aktuella tiden som standard.

   ![Måldatum för Timewarp](/help/sites-cloud/authoring/assets/versions-timewarp-target.png)

1. Sidan visas baserat på det angivna datumet. Timewarp-läget indikeras med det blå statusfältet högst upp i fönstret. Använd länkarna i statusfältet så att du kan välja ett nytt måldatum eller avsluta Timewarp-läget.

   ![I Timewarp-läge](/help/sites-cloud/authoring/assets/versions-timewarp.png)

### Begränsningar för Timewarp {#timewarp-limitations}

Med Timewarp kan du göra ett bra försök att återskapa en sida vid en viss tidpunkt. På grund av komplexiteten i det kontinuerliga skapandet av innehåll i AEM är dock detta inte alltid möjligt. Tänk på dessa begränsningar när du använder Timewarp.

* **Timewarp fungerar baserat på publicerade sidor** - Timewarp fungerar bara helt om du tidigare har publicerat sidan. Om inte, visar Timewarp den aktuella sidan i författarmiljön.
* **Timewarp använder sidversioner** - Om du navigerar till en sida som har tagits bort/tagits bort från databasen återges den korrekt om gamla versioner av sidan fortfarande är tillgängliga i databasen.
* **Borttagna versioner påverkar Timewarp** - Om versioner tas bort från databasen kan inte Timewarp visa rätt vy.
* **Timewarp är skrivskyddat** - du kan inte redigera den gamla versionen av sidan. Det är bara tillgängligt för visning. Om du vill återställa den äldre versionen måste du göra det manuellt med [restore](#revert-to-a-version).
* **Timewarp baseras på sidinnehåll** - Om element för återgivning av webbplatsen ändras, till exempel kod, CSS och resurser, skiljer sig vyn från den ursprungliga vyn. De objekten versionshanteras inte i databasen.
* Timewarp fungerar inte för kapslade starter eller när upplevelsefragment används.

>[!CAUTION]
>
>Timewarp är ett verktyg som hjälper författare att förstå och skapa sitt innehåll. Den är inte avsedd som en revisionslogg eller för juridiska ändamål.

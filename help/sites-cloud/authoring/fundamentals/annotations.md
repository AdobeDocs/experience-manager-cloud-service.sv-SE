---
title: Lägga till sidanteckningar
description: Använd anteckningsläget för att lämna anteckningar och skisser på sidor på samma sätt som du använder anteckningar för att underlätta granskning av innehåll
exl-id: a9cb9745-8140-4795-a5f9-fb3a1a299bd8
source-git-commit: 5d533354a29237aeafc00e5570ede3ab00b721fd
workflow-type: tm+mt
source-wordcount: '700'
ht-degree: 0%

---

# Lägga till sidanteckningar {#adding-page-annotations}

Att skapa innehåll för den digitala upplevelsen kräver ofta diskussion och feedback före publiceringen. För att underlätta den här feedbackprocessen kan du AEM lägga till kommentarer i ditt innehåll.

En anteckning placerar en enkel skiss eller anteckning (tänk riktig anteckning) på sidan. Med anteckningen kan du lämna kommentarer eller frågor till andra författare och granskare.

>[!TIP]
>
>Glöm inte att [kommentarer](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline) också är tillgängliga för att ge feedback på en sida.

Ett särskilt [läge](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes) används för att skapa och visa anteckningar.

>[!TIP]
>
>Beroende på dina behov kan du även utveckla ett [arbetsflöde](/help/sites-cloud/authoring/workflows/overview.md) för att skicka meddelanden när anteckningar läggs till, uppdateras eller tas bort.

## Anteckningsindikator {#annotation-indicator}

Anteckningar visas inte i redigeringsläge, men märket längst upp till höger i verktygsfältet visar hur många anteckningar som finns för den aktuella sidan. Märket ersätter standardikonen för anteckningar, men fungerar fortfarande som en snabblänk som växlar till/från anteckningsläget:

![Anteckningsindikator](/help/sites-cloud/authoring/assets/annotation-indicator.png)

## Anteckningsläge {#annotate-mode}

Anteckningar visas bara i anteckningsläget.

1. Du aktiverar läget Anteckning med ikonen i verktygsfältet (längst upp till höger) när du redigerar en sida:

   ![Anteckningsknapp](/help/sites-cloud/authoring/assets/annotations.png)

   Nu kan du visa alla befintliga anteckningar.

   ![Exempel på anteckningar](/help/sites-cloud/authoring/assets/annotation-sketches.png)

1. Klicka eller tryck på anteckningen för att öppna anteckningsdialogrutan och visa information om den.

   ![Anteckningsinformation](/help/sites-cloud/authoring/assets/annotation-sketches.png)

1. Om du vill avsluta anteckningsläget och återgå till det tidigare använda läget trycker/klickar du på x-knappen till höger om det övre verktygsfältet.

## Lägga till och redigera anteckningar {#annotating-a-component}

Förutom att visa anteckningarna kan du i anteckningsläget skapa, redigera, flytta eller ta bort anteckningar i innehållet

1. [Starta anteckningsläget ](#annotate-mode) på sidan.

1. Klicka eller tryck på ikonen Lägg till anteckning (plus symbol till vänster i verktygsfältet) för att börja lägga till anteckningar.

1. Klicka eller tryck på den nödvändiga komponenten (komponenter som kan kommenteras markeras med en blå ram) för att lägga till anteckningen och öppna dialogrutan:

   ![Lägga till en anteckning](/help/sites-cloud/authoring/assets/annotation-adding.png)

   Här kan du använda rätt fält och/eller ikon för att:

   * Ange anteckningstexten.
   * Skapa en skiss (linjer och former) för att markera ett område i komponenten.

      ![Anteckningsknapp](/help/sites-cloud/authoring/assets/annotation-sketch.png)

      Markören ändras till ett hårkors när du skapar en skiss. Du kan rita flera distinkta linjer. Skisslinjen återspeglar anteckningsfärgen och kan vara en pil, cirkel eller oval.

   * Välj eller ändra färg:

      ![Färgruteknapp för anteckningsfärg](/help/sites-cloud/authoring/assets/annotation-color-swatch.png)

1. Du kan stänga anteckningsdialogrutan genom att klicka eller trycka utanför dialogrutan. En trunkerad vy av anteckningen tillsammans med eventuella skisser visas:

   ![Anteckningskisser](/help/sites-cloud/authoring/assets/annotation-sketches.png)

1. När du är klar med redigeringen av en viss anteckning kan du:

   * Klicka eller tryck på textmarkören för att öppna anteckningen. När du har öppnat den fullständiga texten kan du göra ändringar eller [ta bort anteckningen.](#deleting-annotations)
   * Flytta textmarkören.
   * Klicka eller tryck på en skisslinje för att markera skissen och dra den till önskad plats.
   * Flytta eller kopiera en komponent
      * Alla relaterade anteckningar och skisser av dem flyttas eller kopieras också, men deras placering i förhållande till stycket förblir densamma.


>[!NOTE]
>
>Anteckningar kan inte läggas till på en sida som har låsts av en annan användare.

>[!NOTE]
>
>Definitionen av en enskild komponenttyp avgör om det är möjligt att lägga till en anteckning (eller inte) i instanser av den komponenten.

## Tar bort anteckning och skisser {#deleting-annotations}

Anteckningar och tillhörande skisser kan tas bort.

1. [Starta anteckningsläget ](#annotate-mode) på sidan.

1. Klicka/tryck på textmarkören för att öppna anteckningen.

1. Klicka på eller tryck på ikonen Ta bort.

   ![Ta bort anteckning](/help/sites-cloud/authoring/assets/annotation-delete.png)

1. Anteckningen och alla tillhörande skisser tas bort.

>[!NOTE]
>
>Om du tar bort en komponent tas alla anteckningar och skisser som är kopplade till den resursen bort, oavsett deras positioner på sidan som helhet.

## Tar endast bort skisser {#deleting-sketches}

Du kan bara ta bort vissa skisser i stället för hela anteckningen med alla associerade skisser.

1. [Starta anteckningsläget ](#annotate-mode) på sidan.

1. Klicka eller tryck på skissen. AEM markerar den med en mörkare blå ruta.

   ![Välj skiss för borttagning](/help/sites-cloud/authoring/assets/annotation-sketch-delete.png)

1. Tryck på Delete-tangenten på tangentbordet.

1. Skissen tas bort, men anteckningen finns kvar.

## Antecknar andra resurser {#annotating-other-resources}

Förutom komponenter kan du lägga till kommentarer i en mängd olika resurser:

* Anteckna resurser [Anteckna resurser](/help/assets/manage-digital-assets.md#annotating)
* Kommentera videoresurser [Anteckna videoresurser](/help/assets/manage-video-assets.md#annotate-video-assets)

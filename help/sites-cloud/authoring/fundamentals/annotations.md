---
title: Lägga till sidanteckningar
description: Många komponenter som är direkt relaterade till innehåll gör att du kan lägga till en anteckning
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 1%

---


# Lägga till sidanteckningar {#adding-page-annotations}

Om du lägger till innehåll på webbplatsens sidor kan det ofta bli aktuellt med diskussioner innan det faktiskt publiceras. För att underlätta detta kan du lägga till en anteckning i många komponenter som är direkt relaterade till innehåll (till skillnad från till exempel layout).

En anteckning placerar en färgad skiss eller anteckning på sidan. Med anteckningen kan du (eller andra användare) lämna kommentarer och/eller frågor till andra författare/granskare.

>[!NOTE]
>
>Glöm inte att [kommentarer](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline) också är tillgängliga för att ge feedback på en sida.

## Anteckningar {#annotations}

Ett särskilt [läge](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes) används för att skapa och visa anteckningar.

>[!CAUTION]
>
>Om du tar bort en resurs (t.ex. en komponent) tas alla anteckningar och skisser som är kopplade till den resursen bort, oavsett deras position på sidan som helhet.

>[!NOTE]
>
>Beroende på dina behov kan du även utveckla ett arbetsflöde för att skicka meddelanden när anteckningar läggs till, uppdateras eller tas bort.

### Kommenterar en komponent {#annotating-a-component}

I anteckningsläget kan du skapa, redigera, flytta eller ta bort anteckningar i ditt innehåll:

1. Du kan öppna anteckningsläget med ikonen i verktygsfältet (längst upp till höger) när du redigerar en sida:

   ![Anteckningsknapp](/help/sites-cloud/authoring/assets/annotations.png)

   Nu kan du visa alla befintliga anteckningar.

   >[!NOTE]
   >
   >Om du vill avsluta anteckningsläget trycker/klickar du på ikonen Anteckning (x-symbolen) till höger om det övre verktygsfältet.

1. Klicka/tryck på ikonen Lägg till anteckning (plus symbol till vänster i verktygsfältet) för att börja lägga till anteckningar.

   >[!NOTE]
   >
   >Om du vill sluta lägga till anteckningar (och återgå till att visa) trycker/klickar du på ikonen Avbryt (x-symbolen i en vit cirkel) till vänster om det övre verktygsfältet.

1. Klicka/tryck på den nödvändiga komponenten (komponenter som kan kommenteras markeras med en blå ram) för att lägga till anteckningen och öppna dialogrutan:

   ![Lägga till en anteckning](/help/sites-cloud/authoring/assets/annotation-adding.png)

   Här kan du använda rätt fält och/eller ikon för att:

   * Ange anteckningstexten.
   * Skapa en skiss (linjer och former) för att markera ett område i komponenten.

      ![Anteckningsknapp](/help/sites-cloud/authoring/assets/annotation-sketch.png)

      Markören ändras till ett hårkors när du skapar en skiss. Du kan rita flera distinkta linjer. Skisslinjen återspeglar anteckningsfärgen och kan vara en pil, cirkel eller oval.

   * Välj/ändra färg:

      ![Färgruteknapp för anteckningsfärg](/help/sites-cloud/authoring/assets/annotation-color-swatch.png)

   * Ta bort anteckningen.

      ![Knappen Ta bort anteckning](/help/sites-cloud/authoring/assets/annotation-delete.png)

1. Du kan stänga anteckningsdialogrutan genom att klicka/trycka utanför dialogrutan. En trunkerad vy (det första ordet) av anteckningen, tillsammans med eventuella skisser, visas:

   ![Anteckningskisser](/help/sites-cloud/authoring/assets/annotation-sketches.png)

1. När du är klar med redigeringen av en viss anteckning kan du:

   * Klicka/tryck på textmarkören för att öppna anteckningen. När du har öppnat hela texten kan du göra ändringar eller ta bort anteckningen.

      * Skisser kan inte tas bort oberoende av anteckningen.
   * Flytta textmarkören.
   * Klicka/tryck på en skisslinje för att markera skissen och dra den till önskad plats.
   * Flytta, eller kopiera, en komponent

      * Alla relaterade anteckningar och skisser av dem flyttas eller kopieras också, och deras placering i förhållande till stycket förblir densamma.


1. Om du vill avsluta anteckningsläget och återgå till det tidigare använda läget trycker/klickar du på ikonen Anteckning (x-symbol) till höger i det övre verktygsfältet.

>[!NOTE]
>
>Anteckningar kan inte läggas till på en sida som har låsts av en annan användare.

>[!NOTE]
>
>Definitionen av en enskild komponenttyp avgör om det är möjligt att lägga till en anteckning (eller inte) i instanser av den komponenten.

## Anteckningsindikator {#annotation-indicator}

Anteckningar visas inte i redigeringsläge, men märket längst upp till höger i verktygsfältet visar hur många anteckningar som finns för den aktuella sidan. Märket ersätter standardikonen för anteckningar, men fungerar fortfarande som en snabblänk som växlar till/från anteckningsläget:

![Anteckningsindikator](/help/sites-cloud/authoring/assets/annotation-indicator.png)

## Antecknar andra resurser {#annotating-other-resources}

Förutom komponenter kan du lägga till kommentarer i en mängd olika resurser:

* Anteckna resurser [Anteckna resurser](/help/assets/manage-digital-assets.md#annotating)
* Kommentera videoresurser [Anteckna videoresurser](/help/assets/manage-video-assets.md#annotate-video-assets)

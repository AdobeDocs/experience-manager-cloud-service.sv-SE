---
title: Developing and Page Diff
description: Förstå hur funktionen för sidskillnader fungerar och hur den kan påverka en utvecklare
exl-id: 03c08616-2203-4b90-bed6-4836266e2507
source-git-commit: 2d4ffd5518d671a55e45a1ab6f1fc41ac021fd80
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 0%

---

# Developing and Page Diff {#developing-and-page-diff}

## Översikt över funktioner {#feature-overview}

Att skapa innehåll är en repetitiv process. Effektiv redigering kräver att man kan se vad som har ändrats från en iteration till en annan. Om du visar den ena sidversionen och den andra är ineffektiv och felbenägen kan uppstå. En författare vill kunna jämföra den aktuella sidan med en tidigare version sida vid sida med skillnaderna markerade.

Med sidskillnaden kan användaren jämföra den aktuella sidan med startsidor, tidigare versioner osv. Mer information om den här användarfunktionen finns i [Sidskillnader](/help/sites-cloud/authoring/features/page-diff.md).

## Operationsinformation {#operation-details}

När du jämför versioner av en sida skapas den tidigare versionen som användaren vill jämföra av AEM i bakgrunden för att underlätta skillnaderna. Den här tidigare versionen är nödvändig för att återge innehållet [för jämförelse sida vid sida](/help/sites-cloud/authoring/features/page-diff.md).

Denna rekreationsåtgärd görs internt av AEM och är transparent för användaren och kräver ingen åtgärd. En administratör som visar databasen, till exempel i CRXDE Lite, skulle kunna se dessa återskapade versioner i innehållsstrukturen.

När innehållet jämförs återskapas hela trädet fram till sidan som ska jämföras på följande plats:

`/tmp/versionhistory/`

En rensningsåtgärd körs automatiskt för att rensa upp det tillfälliga innehållet.

## Begränsningar {#limitations}

Skillnaden sker på klientsidan genom DOM-jämförelse, vilket gör diff-processen enkel. Det finns dock flera begränsningar som måste beaktas av utvecklaren.

* Den här funktionen använder CSS-klasser som inte har något namn som AEM Produkten. Om andra anpassade CSS-klasser eller CSS-klasser från tredje part med samma namn inkluderas på sidan kan visningen av skillnaderna påverkas.

   * `html-added`
   * `html-removed`
   * `cq-component-added`
   * `cq-component-removed`
   * `cq-component-moved`
   * `cq-component-changed`

* Eftersom differensen är klientsidan och körs vid sidinläsning, räknas inga justeringar av DOM efter att diff-tjänsten på klientsidan har körts. Detta kan påverka följande:

   * Komponenter som använder AJAX för att inkludera innehåll
   * Enkelsidiga program
   * JavaScript-baserade komponenter som ändrar DOM när användaren interagerar.

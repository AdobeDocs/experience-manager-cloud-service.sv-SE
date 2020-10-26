---
title: Developing and Page Diff
description: Förstå hur funktionen för sidskillnader fungerar och hur den kan påverka en utvecklare
translation-type: tm+mt
source-git-commit: 57a9026dd944547196e53fecb1cf1213ed793af7
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 0%

---


# Developing and Page Diff {#developing-and-page-diff}

## Funktionsöversikt {#feature-overview}

Att skapa innehåll är en repetitiv process. Effektiv redigering kräver att man kan se vad som har ändrats från en iteration till en annan. Om du visar den ena sidversionen och den andra är ineffektiv och felbenägen kan uppstå. En författare vill kunna jämföra den aktuella sidan med en tidigare version sida vid sida med skillnaderna markerade.

Med sidskillnader kan en användare jämföra den aktuella sidan med startsidor, tidigare versioner osv. Mer information om den här användarfunktionen finns i [Sidskillnad](/help/sites-cloud/authoring/features/page-diff.md).

## Operationsinformation {#operation-details}

När du jämför versioner av en sida skapas den tidigare versionen som användaren vill jämföra av AEM i bakgrunden för att underlätta skillnaderna. Detta behövs för att kunna återge innehållet [för jämförelse](/help/sites-cloud/authoring/features/page-diff.md)sida vid sida.

Denna rekreationsåtgärd görs internt av AEM och är transparent för användaren och kräver ingen åtgärd. En administratör som visar databasen, till exempel i CRX DE Lite, skulle dock se dessa återskapade versioner i innehållsstrukturen.

När innehållet jämförs återskapas hela trädet fram till sidan som ska jämföras på följande plats:

`/tmp/versionhistory/`

En rensningsåtgärd körs automatiskt för att rensa upp det tillfälliga innehållet.

## Begränsningar {#limitations}

Skillnaden uppstår på klientsidan via DOM-jämförelsen, vilket gör diff-processen enkel, men det finns ett antal begränsningar som måste beaktas av utvecklaren.

* Den här funktionen använder CSS-klasser som inte har något namnutrymme för AEM. Om andra anpassade CSS-klasser eller CSS-klasser från tredje part med samma namn inkluderas på sidan kan visningen av skillnaderna påverkas.

   * `html-added`
   * `html-removed`
   * `cq-component-added`
   * `cq-component-removed`
   * `cq-component-moved`
   * `cq-component-changed`

* Eftersom differensen är klientsidan och körs vid sidinläsning, kommer eventuella justeringar av DOM efter att klientsidans diff-tjänst har körts inte att beaktas. Detta kan påverka

   * Komponenter som använder AJAX för att inkludera innehåll
   * Enkelsidiga program
   * Javascript-baserade komponenter som manipulerar DOM när användaren interagerar.

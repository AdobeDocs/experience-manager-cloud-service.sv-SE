---
title: Använda sidmallar med den universella redigeraren
description: Lär dig hur du skapar och använder sidmallar med den universella redigeraren.
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 773ce75975f4dcc2c5310422bcc377b487ebec25
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 0%

---


# Använda sidmallar med den universella redigeraren {#page-templates}

Lär dig hur du skapar och använder sidmallar med den universella redigeraren.

>[!NOTE]
>
>Den här funktionen kommer att finnas i en kommande version av AEM as a Cloud Service.

## Vad är sidmallar? {#what-are}

Riktlinjer för varumärken och marknadsföring styr ofta särskilda layouter för dina innehållssidor. Det är också ofta en praktisk verklighet att många av dina sidor har samma struktur och layout. Om du vill spara tid för innehållsförfattarna kan du skapa sidor från mallar.

Sidmallar fungerar som mallkopior av sidlayouterna. När du skapar en sida från en mall kopieras innehållet i mallen till den nya sidan, vilket hjälper till att fördefiniera sidans layout och ursprungliga innehåll för innehållsförfattaren, vilket sparar tid.

## Skapa en sidmall {#creating}

Du kan skapa en sidmall genom att skapa en ny sida eller genom att använda en befintlig sida som mall. I båda fallen använder du konsolen [**Platser**.](/help/sites-cloud/authoring/sites-console/introduction.md)

### Skapa en ny mall {#create-new}

1. Använd konsolen **Platser** för att navigera till den plats där du vill skapa den nya sidan som fungerar som mall och [skapa sidan precis som andra.](/help/sites-cloud/authoring/sites-console/creating-pages.md)

1. När sidan har skapats och du återgår till konsolen markerar du sidan och trycker eller klickar på ikonen [**Egenskaper** ](/help/sites-cloud/authoring/sites-console/page-properties.md) i verktygsfältet.

1. På fliken **Avancerat** i egenskapsdialogrutan under avsnittet **Mallinställningar** väljer du alternativet **Använd som mall**.

1. Ange ett beskrivande namn i fältet **Mallnamn**.

   * Det här är namnet som kommer att visa när nya innehållssidor skapas och du väljer en mall som den nya sidan ska baseras på.

1. Tryck eller klicka på **Spara och stäng**.

Den nya sidan kan nu användas som mall när nya sidor skapas.

### Använda en befintlig sida som mall {#existing-page}

1. Använd konsolen **Platser** för att [navigera till platsen för sidan](/help/sites-cloud/authoring/sites-console/introduction.md#selecting-resources) som du vill använda som mall.

1. Markera sidan och tryck eller klicka sedan på ikonen [**Egenskaper** ](/help/sites-cloud/authoring/sites-console/page-properties.md) i verktygsfältet.

1. På fliken **Avancerat** i egenskapsdialogrutan under avsnittet **Mallinställningar** väljer du alternativet **Använd som mall**.

1. Ange ett beskrivande namn i fältet **Mallnamn**.

   * Det här är namnet som kommer att visa när nya innehållssidor skapas och du väljer en mall som den nya sidan ska baseras på.

1. Tryck eller klicka på **Spara och stäng**.

Den valda sidan kan nu användas som mall när nya sidor skapas.

## Skapa en sida från en mall {#creating-from-template}

Att skapa en sida från en mall som ska användas med den universella redigeraren är samma arbetsflöde som när du [skapar sidan på samma sätt som andra.](/help/sites-cloud/authoring/sites-console/creating-pages.md)

1. Använd konsolen **Platser** för att [navigera till platsen](/help/sites-cloud/authoring/sites-console/introduction.md#selecting-resources) där du vill skapa den nya sidan.

1. Tryck eller klicka på **Skapa** -> **Sida**.

1. På fliken **Mall** i guiden **Skapa sida** kan du välja vilken mall du vill basera den nya sidan på. Tryck eller klicka på önskad mall för att markera den och tryck eller klicka sedan på **Nästa**.

Slutför guiden på samma sätt som du gör för andra sidor och du har skapat den nya sidan baserat på den valda mallen.

## Universal Editor och Page Editor {#page-vs-universal}

Sidmallar för den universella redigeraren löser samma problem som [sidmallar för den AEM sidredigeraren ](/help/sites-cloud/authoring/page-editor/templates.md) om du vill kunna återanvända innehåll för att snabbt skapa sidor baserat på en uppsättning fördefinierade layouter. De löser dock problemet på mycket olika sätt. Om du använder sidredigeraren bör du vara medveten om dessa skillnader.

* Sidor som skapas från sidmallar för den universella redigeraren är oberoende kopior av mallen.
* Om mallen ändras ändras därför inte de resulterande sidorna.
* Innehållsförfattaren kan ändra och uppdatera innehållet på den slutliga sidan efter behov utan begränsningar från mallen.

---
title: Vad är en avgränsningskomponent i Adaptive Forms?
description: Separatorkomponenten i Adaptive Forms hjälper till att segmentera ett formulär visuellt.
uuid: f8d2aed3-52aa-437f-bfe3-0c8779e7986c
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
docset: aem65
source-git-commit: 2d4ffd5518d671a55e45a1ab6f1fc41ac021fd80
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 0%

---


# Separatorkomponent i Adaptiv Forms{#separator-component-in-adaptive-forms}

Du kan använda avgränsarkomponenten för att dela upp paneler i ett formulär visuellt. Du kan definiera det övergripande utseendet och formatet för en avgränsningskomponent genom att ange följande egenskaper för avgränsningskomponenten:

* **Elementnamn:** Anger komponentens namn. SOM-uttrycken adresserar komponenten med ett värde angivet i fältet Elementnamn.
* **Tjocklek:** Anger tjockleken på avgränsningskomponenten i pixlar.

* **CSS-klass:** Anger den anpassade CSS-klassen för avgränsarkomponenten

* **Textbundna format:** Med [!DNL AEM Forms]kan du nu använda infogade CSS-format på enskilda adaptiva formulärkomponenter och förhandsgranska ändringarna i realtid.

Du kan använda layoutläget för att definiera antalet kolumner som avgränsningskomponenten sträcker sig till. Mer information finns i [Använd layoutläget för att ändra storlek på komponenter](resize-using-layout-mode.md).

Så här anger du egenskaper för en avgränsningskomponent:

1. Markera en avgränsningskomponent och markera ![cmppr](assets/cmppr.png). Egenskaperna öppnas i sidofältet.
1. Klicka på en flik i avsnittet Infoga CSS-egenskaper så att du kan ange CSS-egenskaper. Exempel: a. Klicka på fliken Fält **Lägg till objekt**. En rad med två fält läggs till.
1. I det första fältet från vänster anger du den CSS3-egenskap som du vill använda. Till exempel: **border**. Du kan också välja en egenskap genom att klicka på nedpilsknappen. Listrutan är inte fullständig och du kan ange ett CSS3-egenskapsnamn som stöds i det här fältet.
1. Ange ett giltigt värde för den angivna CSS3-egenskapen i det intilliggande fältet. Till exempel: **3 pixlar solid black**.
1. Klicka **Lägg till objekt** för att ange en annan egenskap och dess värde.
1. Klicka **Förhandsgranska** så att du kan se ändringarna i formuläret.
1. Gör något av följande:
   * Bekräfta ändringarna genom att klicka **OK**
   * Avsluta dialogrutan utan ändringar genom att klicka på **Avbryt**.


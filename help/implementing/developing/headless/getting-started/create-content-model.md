---
title: Skapa innehållsfragmentmodeller Headless Quick Start Guide
description: Content Fragment Models definierar strukturen för det innehåll du skapar och fungerar med AEM headless-funktioner.
translation-type: tm+mt
source-git-commit: 712a99095494ab333cf0ebb2ac9fffe3f5945f3b
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 0%

---


# Skapa innehållsfragmentmodeller Headless Quick Start Guide {#creating-content-fragment-models}

Content Fragment Models definierar strukturen för det innehåll du skapar och fungerar med AEM headless-funktioner.

## Vad är Content Fragment Models? {#what-are-content-fragment-models}

[Nu när du har skapat en konfiguration kan ](create-configuration.md) du använda den för att skapa modeller för innehållsfragment.

Modeller för innehållsfragment definierar strukturen för data och innehåll som du skapar och hanterar i AEM. De fungerar som en sorts ställningar för ert innehåll. När du väljer att skapa innehåll väljer författarna bland de modeller för innehållsfragment som du definierar, som vägleder dem när de skapar innehåll.

## Så här skapar du en innehållsfragmentmodell {#how-to-create-a-content-fragment-model}

En informationsarkitekt skulle utföra dessa uppgifter endast sporadiskt när nya modeller behövs. I den här guiden behöver vi bara skapa en modell.

1. Logga in AEM som Cloud Service och välj **Verktyg -> Resurser -> Content Fragment Models** på huvudmenyn.
1. Tryck eller klicka på mappen som skapades när du skapade konfigurationen.

   ![Mappen Modeller](../assets/models-folder.png)
1. Tryck eller klicka på **Skapa**.
1. Ange en **modelltitel** och **Beskrivning**.

   ![Skapa en modell](../assets/models-create.png)
1. Tryck eller klicka på **Öppna** i bekräftelsefönstret för att konfigurera modellen.

   ![Bekräftelsefönstret](../assets/models-confirmation.png)
1. Använd **Modellredigeraren för innehållsfragment** och bygg din modell för innehållsfragment genom att dra och släppa fält från kolumnen **Datatyper**.

   ![Dra och släppa fält](../assets/models-drag-and-drop.png)

1. När du har placerat ett fält måste du konfigurera dess egenskaper. Redigeraren växlar automatiskt till fliken **Egenskaper** för det tillagda fältet där du kan ange de obligatoriska fälten.

   ![Konfigurera egenskaper](../assets/models-configure-properties.png)
1. När du är klar med att skapa modellen trycker eller klickar du på **Spara**. Den nyskapade modellen sparas i läget **Utkast**.

   ![Modell i utkastläge](../assets/models-draft.png)
1. Modellen måste aktiveras för att den ska kunna användas. Markera den modell du just skapade och tryck eller klicka på **Aktivera**.

   ![Aktivera modellen](../assets/models-enable.png)
1. Bekräfta aktiveringen av modellen genom att trycka eller klicka på **Aktivera** i bekräftelsedialogrutan.

   ![Aktivera bekräftelsedialogrutan](../assets/models-enabling.png)
1. Modellen är nu aktiverad och klar att användas.

   ![Modellen är aktiverad](../assets/models-enabled.png)

**Modellredigeraren för innehållsfragment** stöder många olika datatyper, till exempel enkla textfält, resursreferenser, referenser till andra modeller och JSON-data.

Du kan skapa flera modeller. Modeller kan referera till andra innehållsfragment. Använd [konfigurationer](create-configuration.md) för att ordna dina modeller.

## Nästa steg {#next-steps}

Nu när du har definierat strukturerna för dina innehållsfragment genom att skapa modeller kan du gå vidare till den tredje delen av guiden Komma igång och [skapa mappar där du lagrar fragmenten själva.](create-assets-folder.md)

>!![TIP]
Fullständig information om modeller för innehållsfragment finns i [dokumentationen för modeller för innehållsfragment](/help/assets/content-fragments/content-fragments-models.md)

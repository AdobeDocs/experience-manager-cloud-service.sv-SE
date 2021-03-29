---
title: Skapa en startguide för en resursmapp utan rubrik
description: Använd AEM Content Fragment Models för att definiera strukturen för Content Fragments, som är grunden för ditt headless-innehåll.
translation-type: tm+mt
source-git-commit: e7ca6dc841ba777384be74021a27d523d530a956
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 0%

---


# Skapa en startguide för resursmapp utan rubrik {#creating-an-assets-folder}

Använd AEM Content Fragment Models för att definiera strukturen för Content Fragments, som är grunden för ditt headless-innehåll. Innehållsfragment lagras sedan i resursmappar.

##  Vad är en resursmapp? {#what-is-an-assets-folder}

[Nu när du har skapat ](create-content-model.md) modeller för innehållsfragment som definierar den struktur som du vill ha för framtida innehållsfragment, är du antagligen redo att skapa några fragment.

Du måste dock först skapa en resursmapp där du lagrar dem.

Resursmappar används för att [organisera traditionella innehållsresurser](/help/assets/manage-digital-assets.md) som bilder, video och innehållsfragment.

## Så här skapar du en resursmapp {#how-to-create-an-assets-folder}

En administratör behöver bara skapa mappar då och då för att ordna innehållet när det skapas. I den här guiden behöver vi bara skapa en mapp.

1. Logga in AEM som Cloud Service och välj **Navigation -> Assets -> Files** på huvudmenyn.
1. Tryck eller klicka på **Skapa -> Mapp**.
1. Ange en **titel** och ett **namn** för mappen.
   * **Titeln** ska vara beskrivande.
   * **Namnet** blir nodnamnet i databasen.
      * Den genereras automatiskt baserat på titeln och justeras enligt [AEM namnkonventioner.](/help/implementing/developing/introduction/naming-conventions.md)
      * Den kan vid behov justeras.

   ![Skapa mapp](../assets/assets-folder-create.png)
1. Markera mappen som du just skapade och välj sedan **Egenskaper** i verktygsfältet (eller använd kortkommandot `p` [.](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md))
1. I fönstret **Egenskaper** väljer du fliken **Cloud Services**.
1. För **molnkonfigurationen** Välj den [konfiguration du skapade tidigare.](create-configuration.md)

   ![Konfigurera resursmapp](../assets/assets-folder-configure.png)
1. Tryck eller klicka på **Spara och stäng**.
1. Tryck eller klicka på **OK** i bekräftelsefönstret.

   ![Bekräftelsefönstret](../assets/assets-folder-confirmation.png)

Du kan skapa ytterligare undermappar i den mapp du just skapade. Undermapparna ärver **molnkonfigurationen** för den överordnade mappen. Detta kan dock åsidosättas om du vill använda modeller från en annan konfiguration.

Om du använder en lokaliserad platsstruktur kan du [skapa en språkrot](/help/assets/translate-assets.md) under den nya mappen.

## Nästa steg {#next-steps}

Nu när du har skapat en mapp för dina innehållsfragment kan du gå vidare till den fjärde delen av guiden Komma igång och [skapa innehållsfragment.](create-content-fragment.md)

>[!TIP]
>
>Fullständig information om hur du hanterar innehållsfragment finns i [dokumentationen för innehållsfragment](/help/assets/content-fragments/content-fragments.md)

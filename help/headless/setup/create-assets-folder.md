---
title: Skapa en Assets-mapp - Headless-installation
description: Använd AEM Content Fragment Models för att definiera strukturen för Content Fragments, som är grunden för ditt headless-innehåll.
exl-id: 9a156a17-8403-40fc-9bd0-dd82fb7b2235
feature: Headless, Content Fragments,GraphQL API
role: Admin, Developer
source-git-commit: bdf3e0896eee1b3aa6edfc481011f50407835014
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 0%

---

# Skapa en Assets-mapp - Headless-installation {#creating-an-assets-folder}

Använd AEM Content Fragment Models för att definiera strukturen för Content Fragments, som är grunden för ditt headless-innehåll. Innehållsfragment lagras sedan i resursmappar.

## Vad är en Assets-mapp? {#what-is-an-assets-folder}

[Nu när du har skapat modeller för innehållsfragment](create-content-model.md) som definierar den struktur som du vill ha för framtida innehållsfragment, är du antagligen redo att skapa några fragment.

Du måste dock först skapa en resursmapp där du lagrar dem.

Assets-mappar används för att [ordna traditionella innehållsresurser](/help/assets/manage-digital-assets.md), till exempel bilder och videoklipp, tillsammans med innehållsfragment.

## Så här skapar du en Assets-mapp {#how-to-create-an-assets-folder}

En administratör behöver bara skapa mappar då och då för att ordna innehållet när det skapas. I den här guiden behöver vi bara skapa en mapp.

1. Logga in i AEM as a Cloud Service och välj **Navigering > Assets > Filer** på huvudmenyn.
1. Välj **Skapa > Mapp**.
1. Ange en **titel** och ett **namn** för din mapp.
   * **Rubriken** ska vara beskrivande.
   * **Namn** blir nodnamnet i databasen.
      * Den genereras automatiskt baserat på titeln och justeras enligt [AEM namnkonventioner](/help/implementing/developing/introduction/naming-conventions.md).
      * Den kan vid behov justeras.

   ![Skapa mapp](../assets/assets-folder-create.png)
1. Markera mappen som du skapade genom att hålla markeringen nedtryckt och trycka på den. Välj sedan **Egenskaper** i verktygsfältet (eller använd `p` [kortkommandot](/help/sites-cloud/authoring/sites-console/keyboard-shortcuts.md)).
1. I fönstret **Egenskaper** väljer du fliken **Cloud Service** .
1. För **molnkonfigurationen** väljer du den [konfiguration du skapade tidigare.](create-configuration.md)
   ![Konfigurera resursmappen](../assets/assets-folder-configure.png)
1. Välj **Spara och stäng**.
1. Välj **OK** i bekräftelsefönstret.

   ![Bekräftelsefönstret](../assets/assets-folder-confirmation.png)

Du kan skapa ytterligare undermappar i den mapp du skapade. Undermapparna ärver den överordnade mappens **molnkonfiguration**. Detta kan åsidosättas om du vill använda modeller från en annan konfiguration.

Om du använder en lokaliserad platsstruktur kan du [skapa en språkrot](/help/assets/translate-assets.md) under den nya mappen.

## Nästa steg {#next-steps}

Nu när du har skapat en mapp för dina innehållsfragment kan du gå vidare till den fjärde delen av guiden Komma igång och [skapa innehållsfragment](create-content-fragment.md).

>[!TIP]
>
>Fullständig information om hur du hanterar innehållsfragment finns i [dokumentationen för innehållsfragment](/help/sites-cloud/administering/content-fragments/overview.md)

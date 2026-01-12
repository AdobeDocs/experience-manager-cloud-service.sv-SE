---
title: Skapa en Assets-mapp - Headless-installation
description: Använd AEM Content Fragment Models för att definiera strukturen för Content Fragments, som är grunden för ditt headless-innehåll.
exl-id: 9a156a17-8403-40fc-9bd0-dd82fb7b2235
feature: Headless, Content Fragments,GraphQL API
role: Admin, Developer
source-git-commit: 95624ebf1a77dac1f535e199b660096c8efdfa76
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 0%

---

# Skapa en Assets-mapp - Headless-installation {#creating-an-assets-folder}

Använd AEM Content Fragment Models för att definiera strukturen för Content Fragments, som är grunden för ditt headless-innehåll. Innehållsfragment lagras sedan i resursmappar.

## Vad är en Assets-mapp? {#what-is-an-assets-folder}

[Nu när du har skapat modeller för innehållsfragment](create-content-model.md) som definierar den struktur som du vill ha för framtida innehållsfragment, är du antagligen redo att skapa några fragment.

Du måste dock först skapa en resursmapp där du lagrar dem.

Assets-mappar används för att [ordna traditionella innehållsresurser](/help/assets/manage-digital-assets.md), till exempel bilder och videoklipp, tillsammans med innehållsfragment.

## Skapa och konfigurera en Assets-mapp {#create-and-configure-an-assets-folder}

En administratör behöver bara skapa mappar då och då för att ordna innehållet när det skapas. Använd Assets Console för att skapa en ny mapp.

När du har skapat filen måste du tillämpa din [konfiguration](/help/headless/setup/create-configuration.md) på mappen. Mer information finns i [Använda konfigurationen i din mapp](/help/sites-cloud/administering/content-fragments/setup.md#apply-the-configuration-to-your-folder).

Du kan skapa ytterligare undermappar i den mapp du skapade. Undermapparna ärver den överordnade mappens **molnkonfiguration**. Detta kan åsidosättas om du vill använda modeller från en annan konfiguration.

Om du använder en lokaliserad platsstruktur kan du [skapa en språkrot](/help/assets/translate-assets.md) under den nya mappen.

## Nästa steg {#next-steps}

Nu när du har skapat en mapp för dina innehållsfragment kan du gå vidare till den fjärde delen av guiden Komma igång och [skapa innehållsfragment](create-content-fragment.md).

>[!TIP]
>
>Fullständig information om hur du hanterar innehållsfragment finns i [dokumentationen för innehållsfragment](/help/sites-cloud/administering/content-fragments/overview.md)

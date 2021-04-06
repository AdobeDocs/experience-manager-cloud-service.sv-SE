---
title: Skapa innehållsfragment Headless Quick Start Guide
description: Lär dig använda AEM innehållsfragment för att utforma, skapa, strukturera och använda sidoberoende innehåll för rubrikfri leverans.
exl-id: a227ae2c-f710-4968-8a00-bfe48aa66145
translation-type: tm+mt
source-git-commit: 088fa5c90d549c52ca2832bd026be4fcddb31b78
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 0%

---

# Skapa innehållsfragment Headless Quick Start Guide {#creating-content-fragments}

Lär dig använda AEM innehållsfragment för att utforma, skapa, strukturera och använda sidoberoende innehåll för rubrikfri leverans.

## Vad är innehållsfragment? {#what-are-content-fragments}

[Nu när du har skapat en ](create-assets-folder.md) resursmapp där du kan lagra dina innehållsfragment kan du nu skapa fragmenten!

Med Content Fragments kan du utforma, skapa, strukturera och publicera sidoberoende innehåll. Med dem kan du förbereda innehåll som är klart för användning på flera platser och i flera kanaler.

Innehållsfragment innehåller strukturerat innehåll och kan levereras i JSON-format.

## Så här skapar du ett innehållsfragment {#how-to-create-a-content-fragment}

Innehållsförfattare skapar valfritt antal innehållsfragment som representerar det innehåll de skapar. Detta kommer att vara deras huvuduppgift i AEM. I den här guiden behöver vi bara skapa en.

1. Logga in AEM som Cloud Service och välj **Navigation -> Assets** på huvudmenyn.
1. Tryck eller klicka på mappen [som du skapade tidigare.](create-assets-folder.md)
1. Tryck eller klicka på **Skapa -> Innehållsfragment**.
1. Skapandet av ett innehållsfragment presenteras som en guide i två steg. Välj först vilken modell du vill använda för att skapa ditt innehållsfragment och tryck eller klicka på **Nästa**.
   * Vilka modeller som är tillgängliga beror på den [**molnkonfiguration** du definierade för resursmappen](create-assets-folder.md) som du skapar innehållsfragmentet i.
   * Om du får meddelandet `We could not find any models` kontrollerar du konfigurationen för din resursmapp.

   ![Välj innehållsfragmentmodell](../assets/content-fragment-model-select.png)
1. Ange en **titel**, **Beskrivning** och **taggar** efter behov och tryck eller klicka på **Skapa**.

   ![Skapa innehållsfragment](../assets/content-fragment-create.png)
1. Tryck eller klicka på **Öppna** i bekräftelsefönstret.

   ![Bekräftelse på att innehållsfragment har skapats](../assets/content-fragment-confirmation.png)
1. Ange information om innehållsfragmentet i Content Fragment Editor.

   ![Innehållsfragmentsredigerare](../assets/content-fragment-edit.png)
1. Tryck eller klicka på **Spara** eller **Spara och stäng**.

Innehållsfragment kan referera till andra innehållsfragment, vilket möjliggör en kapslad innehållsstruktur om det behövs.

Innehållsfragment kan också referera till andra resurser i AEM. [Dessa resurser måste lagras i ](/help/assets/manage-digital-assets.md) AEM innan du skapar ett referensinnehållsfragment.

## Nästa steg {#next-steps}

Nu när du har skapat ett innehållsfragment kan du gå vidare till den sista delen av guiden Komma igång och [skapa API-begäranden för att komma åt och leverera innehållsfragment.](create-api-request.md)

>[!TIP]
>
>Fullständig information om hur du hanterar innehållsfragment finns i [dokumentationen för innehållsfragment](/help/assets/content-fragments/content-fragments.md)

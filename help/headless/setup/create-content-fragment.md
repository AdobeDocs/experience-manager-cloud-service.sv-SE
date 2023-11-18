---
title: Skapa innehållsfragment - Headless-inställningar
description: Lär dig använda AEM innehållsfragment för att utforma, skapa, strukturera och använda sidoberoende innehåll för rubrikfri leverans.
exl-id: a227ae2c-f710-4968-8a00-bfe48aa66145
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 0%

---

# Skapa innehållsfragment - Headless-inställningar {#creating-content-fragments}

Lär dig använda AEM innehållsfragment för att utforma, skapa, strukturera och använda sidoberoende innehåll för rubrikfri leverans.

## Vad är innehållsfragment? {#what-are-content-fragments}

[Nu när du har skapat en resursmapp](create-assets-folder.md) där du kan lagra dina innehållsfragment kan du nu skapa fragmenten!

Med Content Fragments kan du utforma, skapa, strukturera och publicera sidoberoende innehåll. Med dem kan du förbereda innehåll som är klart för användning på flera platser och i flera kanaler.

Innehållsfragment innehåller strukturerat innehåll och kan levereras i JSON-format.

## Så här skapar du ett innehållsfragment {#how-to-create-a-content-fragment}

Innehållsförfattare skapar valfritt antal innehållsfragment som representerar det innehåll de skapar. Detta är deras huvuduppgift i AEM. I den här guiden behöver vi bara skapa en.

1. Logga in AEM as a Cloud Service och välj **Navigering** > **Innehållsfragment**.

1. Välj [mapp som du skapade tidigare.](create-assets-folder.md)
1. Välj **Skapa**.
1. Skapandet av ett innehållsfragment visas som en dialogruta.
Välj den plats och modell som du vill använda för att skapa ditt innehållsfragment.

   * Vilka modeller som är tillgängliga beror på [**Molnkonfiguration** du har definierat för resursmappen](create-assets-folder.md) där du skapar innehållsfragmentet.
   * Om modellen inte är tillgänglig kontrollerar du konfigurationen för resursmappen.

   Lägg till titel, namn och, om det behövs, beskrivning.

   ![Dialogrutan Skapa nytt innehållsfragment](/help/sites-cloud/administering/content-fragments/assets/cfc-console-create.png)

1. Välj **Skapa** eller  **Skapa och öppna**.

Innehållsfragment kan referera till andra innehållsfragment, vilket möjliggör en kapslad innehållsstruktur om det behövs.

Innehållsfragment kan också referera till andra resurser i AEM. [Dessa resurser måste lagras i AEM](/help/assets/manage-digital-assets.md) innan du skapar ett referensinnehållsfragment.

## Nästa steg {#next-steps}

Nu när du har skapat ett innehållsfragment kan du gå vidare till den sista delen av guiden Komma igång och [skapa API-förfrågningar för åtkomst och leverans av innehållsfragment.](create-api-request.md)

>[!TIP]
>
>Fullständig information om hur du hanterar innehållsfragment finns i [Dokumentation för innehållsfragment](/help/sites-cloud/administering/content-fragments/overview.md)

---
title: Anpassa vyer av Sidegenskaper
description: Lär dig hur du visar och redigerar sidegenskaper av författare.
exl-id: 363b3c2d-f965-485f-bdae-2ea5b4cecb83
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 0%

---

# Anpassa vyer av Sidegenskaper{#customizing-views-of-page-properties}

Varje sida har en uppsättning [egenskaper](/help/sites-cloud/authoring/fundamentals/page-properties.md) som kan visas och redigeras av användare. En del krävs när du skapar sidan (skapar vy), andra kan visas och redigeras (redigeringsvy) i ett senare skede. Dessa sidegenskaper definieras och görs tillgängliga i dialogrutan (`cq:dialog`) för rätt sidkomponent.

Standardläget för varje sidegenskap är:

* Dolt i vyn Skapa (till exempel **Skapa sida** guide)

* Finns i redigeringsvyn (till exempel **Visa egenskaper**)

Fälten måste vara specifikt konfigurerade om någon ändring krävs. Detta görs med lämpliga nodegenskaper:

* Page-egenskap som ska vara tillgänglig i vyn create (till exempel **Skapa sida** guide):

   * Namn: `cq:showOnCreate`
   * Typ: `Boolean`

* Page-egenskap som ska vara tillgänglig i redigeringsvyn, till exempel **Visa**/**Redigera**  **Egenskaper** alternativ:

   * Namn: `cq:hideOnEdit`
   * Typ: `Boolean`

>[!TIP]
>
>Se [Utöka Sidegenskaper, genomgång](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/developing/page-properties-technical-video-develop.html) för att få hjälp med att anpassa sidegenskaper.

## Konfigurera dina sidegenskaper {#configuring-your-page-properties}

Du kan också konfigurera fälten som är tillgängliga genom att konfigurera dialogrutan för sidkomponenten och använda lämpliga nodegenskaper.

Som standard är [**Skapa sida** guide](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#creating-a-new-page) visar fält grupperade under **Fler rubriker och beskrivning**. Så här döljer du dessa konfigurationer:

1. Skapa sidkomponenten under `/apps`.
1. Skapa en åsidosättning (med *dialogruta* tillhandahålls av [Samla resurser](/help/implementing/developing/introduction/sling-resource-merger.md)) för `basic` del av sidkomponenten, till exempel:

   ```xml
   <your-page-component>/cq:dialog/content/items/tabs/items/basic
   ```

1. Ange `path` egenskap på `basic` för att peka på åsidosättningen av den grundläggande fliken (se även nästa steg). Till exempel:

   ```xml
   /apps/demos/components/page/tabs/basic
   ```

1. Skapa en åsidosättning av `basic` - `moretitles` i motsvarande sökväg, till exempel:

   ```xml
   /apps/demos/components/page/tabs/basic/items/column/items/moretitles
   ```

1. Använd lämplig nodegenskap:

   * **Namn**: `cq:showOnCreate`
   * **Typ**: `Boolean`
   * **Värde**: `false`

   The **Fler rubriker och beskrivning** -avsnittet visas inte längre i **Skapa sida** guide.

>[!NOTE]
>
>Information om hur du konfigurerar sidegenskaper för användning med live-kopior finns i [Utöka Multi Site Manager](/help/implementing/developing/extending/msm.md#configuring-msm-locks-on-page-properties) för mer information.

## Exempelkonfiguration av sidegenskaper {#sample-configuration-of-page-properties}

I det här exemplet visas tekniken för dialogrutor i [Samla resurser](/help/implementing/developing/introduction/sling-resource-merger.md) inklusive användning av [`sling:orderBefore`](/help/implementing/developing/introduction/sling-resource-merger.md#properties). Det visar också hur man använder båda `cq:showOnCreate` och `cq:hideOnEdit`.

Koden för den här sidan finns på [GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-page-dialog).

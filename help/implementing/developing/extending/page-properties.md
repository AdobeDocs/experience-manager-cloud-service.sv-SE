---
title: Anpassa vyer av Sidegenskaper
description: Lär dig hur du visar och redigerar sidegenskaper av författare.
exl-id: 363b3c2d-f965-485f-bdae-2ea5b4cecb83
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 0%

---

# Anpassa vyer av Sidegenskaper{#customizing-views-of-page-properties}

Varje sida har en uppsättning [egenskaper](/help/sites-cloud/authoring/sites-console/page-properties.md) som kan visas och redigeras av användare. En del krävs när du skapar sidan (skapar vy), andra kan visas och redigeras (redigeringsvy) i ett senare skede. Dessa sidegenskaper definieras och görs tillgängliga i dialogrutan (`cq:dialog`) för rätt sidkomponent.

Standardläget för varje sidegenskap är:

* Dold i vyn Skapa (t.ex. guiden **Skapa sida**)

* Finns i redigeringsvyn (till exempel **Visa egenskaper**)

Fälten måste vara specifikt konfigurerade om någon ändring krävs. Detta görs med lämpliga nodegenskaper:

* Sidegenskap som ska vara tillgänglig i skapandevyn (t.ex. guiden **Skapa sida**):

   * Namn: `cq:showOnCreate`
   * Typ: `Boolean`

* Sidegenskapen ska vara tillgänglig i redigeringsvyn, till exempel alternativet **Visa**/**Redigera** **Egenskaper** :

   * Namn: `cq:hideOnEdit`
   * Typ: `Boolean`

>[!TIP]
>
>I självstudiekursen [Utöka sidegenskaper](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/developing/page-properties-technical-video-develop.html) finns en guide om hur du anpassar sidegenskaper.

## Konfigurera dina sidegenskaper {#configuring-your-page-properties}

Du kan också konfigurera fälten som är tillgängliga genom att konfigurera dialogrutan för sidkomponenten och använda lämpliga nodegenskaper.

Som standard visar guiden **](/help/sites-cloud/authoring/sites-console/creating-pages.md#creating-a-new-page)[** Skapa sida de fält som är grupperade under **Fler rubriker och beskrivning**. Så här döljer du dessa konfigurationer:

1. Skapa sidkomponenten under `/apps`.
1. Skapa en åsidosättning (med *dialog diff* från [Sling Resource Merger](/help/implementing/developing/introduction/sling-resource-merger.md)) för `basic`-delen av sidkomponenten, till exempel:

   ```xml
   <your-page-component>/cq:dialog/content/items/tabs/items/basic
   ```

1. Ställ in egenskapen `path` för `basic` så att den pekar på åsidosättningen av grundfliken (se även nästa steg). Till exempel:

   ```xml
   /apps/demos/components/page/tabs/basic
   ```

1. Skapa en åsidosättning av avsnittet `basic` - `moretitles` vid motsvarande sökväg, till exempel:

   ```xml
   /apps/demos/components/page/tabs/basic/items/column/items/moretitles
   ```

1. Använd lämplig nodegenskap:

   * **Namn**: `cq:showOnCreate`
   * **Typ**: `Boolean`
   * **Värde**: `false`

   Avsnittet **Fler rubriker och beskrivning** visas inte längre i guiden **Skapa sida**.

>[!NOTE]
>
>Mer information finns i [Utöka Multi Site Manager](/help/implementing/developing/extending/msm.md#configuring-msm-locks-on-page-properties) när du konfigurerar sidegenskaper för användning med live-kopior.

## Exempelkonfiguration av sidegenskaper {#sample-configuration-of-page-properties}

I det här exemplet visas dialogtekniken för [Sling Resource Merger](/help/implementing/developing/introduction/sling-resource-merger.md), inklusive användningen av [`sling:orderBefore`](/help/implementing/developing/introduction/sling-resource-merger.md#properties). Det visar också hur både `cq:showOnCreate` och `cq:hideOnEdit` används.

Du hittar koden för den här sidan på [GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-page-dialog).

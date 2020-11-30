---
title: Komponentkonsol
description: Med komponentkonsolen kan du bläddra igenom alla komponenter som definierats för din instans
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 17%

---


# Komponentkonsol {#components-console}

Med komponentkonsolen kan du bläddra igenom alla komponenter som definierats för instansen och visa nyckelinformation för varje komponent.

Den finns under **Verktyg ->** **Allmänt ->** **Komponenter**. Eftersom det inte finns någon trädstruktur för komponenter är endast listvyn tillgänglig.

![Komponentkonsolen](/help/sites-cloud/authoring/assets/components-console.png)

>[!NOTE]
>
>Komponentkonsolen visar alla komponenter i systemet. I [komponentwebbläsaren](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser) visas komponenter som är tillgängliga för författare och alla komponentgrupper som börjar med en punkt ( `.`) döljs.

## Sökning {#search-field}

Med ikonen **Endast innehåll** (överst till vänster) kan du öppna **sökpanelen** och söka efter och/eller filtrera komponenterna:

![Söka i komponentkonsolen](/help/sites-cloud/authoring/assets/components-console-search.png)

### Komponentinformation {#component-details}

Om du vill visa information om en viss komponent trycker/klickar du på den nödvändiga resursen. Tre flikar innehåller:

* **Egenskaper**

   ![Egenskaper för komponentkonsolen](/help/sites-cloud/authoring/assets/components-console-properties.png)

   På fliken Egenskaper kan du:

   * Visa komponentens allmänna egenskaper.
      * Visa hur ikonen eller förkortningen har definierats för komponenten. <!-- View how the [icon or abbreviation has been defined](/help/sites-developing/components-basics.md#component-icon-in-touch-ui) for the component.-->
      * Om du klickar på ikonens källa kommer du till den komponenten.
   * Visa komponentens **resurstyp** och **resurssupertyp** (om den är definierad).
      * Om du klickar på Resurssupertypen kommer du till den komponenten.

   >[!NOTE]
   >
   >Eftersom `/apps` inte kan redigeras under körning är komponentkonsolen skrivskyddad.

* **Profiler**

   ![Principer för komponentkonsolen](/help/sites-cloud/authoring/assets/components-console-policies.png)

* **Live-användning**

   ![Live-användning av komponenter](/help/sites-cloud/authoring/assets/components-console-live-usage.png)

   >[!CAUTION]
   >
   >På grund av den typ av information som samlas in för den här vyn kan det ta en stund att sortera/visa informationen.

* **Dokumentation**

   Om utvecklaren har tillhandahållit dokumentation för komponenten visas den på fliken **Dokumentation** . Om det inte finns någon tillgänglig dokumentation visas inte fliken **Dokumentation** . <!-- If the developer has provided [documentation for the component](/help/sites-developing/developing-components.md#documenting-your-component), it will appear on the **Documentation** tab. If there is no documentation available, the **Documentation** tab will not be shown.-->

   ![Komponentdokumentation](/help/sites-cloud/authoring/assets/components-console-documentation.png)

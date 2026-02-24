---
title: Komponentkonsol
description: Med komponentkonsolen kan du bläddra igenom alla komponenter som definierats för din instans
badgeSaas: label="AEM Sites" type="Positive" tooltip="Gäller AEM Sites)."
exl-id: f4949331-5302-46d3-a004-b813bb95ec2f
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 98c0c9b6adbc3d7997bc68311575b1bb766872a6
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 11%

---

# Komponentkonsol {#components-console}

Med komponentkonsolen kan du bläddra igenom alla komponenter som definierats för instansen och visa nyckelinformation för varje komponent.

Den kan nås via **Verktyg >** **Allmänt >** **Komponenter**. Eftersom det inte finns någon trädstruktur för komponenter är endast listvyn tillgänglig.

![Komponentkonsolen](/help/sites-cloud/authoring/assets/components-console.png)

>[!NOTE]
>
>Komponentkonsolen visar alla komponenter i systemet. [Komponentbläddraren](/help/sites-cloud/authoring/page-editor/editor-side-panel.md#components-browser) visar komponenter som är tillgängliga för författare och döljer komponentgrupper som börjar med en punkt ( `.`).

## Sök {#search-field}

Med ikonen **Endast innehåll** (överst till vänster) kan du öppna **sökpanelen** och söka efter och/eller filtrera komponenterna:

![Söker i komponentkonsolen](/help/sites-cloud/authoring/assets/components-console-search.png)

### Komponentinformation {#component-details}

Om du vill visa information om en viss komponent väljer du önskad resurs. Tre flikar innehåller:

* **Egenskaper**

  ![Egenskaper för komponentkonsolen](/help/sites-cloud/authoring/assets/components-console-properties.png)

  På fliken Egenskaper kan du:

   * Visa komponentens allmänna egenskaper.
      * Visa hur ikonen eller förkortningen har definierats för komponenten. <!-- View how the [icon or abbreviation has been defined](/help/sites-developing/components-basics.md#component-icon-in-touch-ui) for the component.-->
      * Om du klickar på ikonens källa kommer du till den komponenten.
   * Visa komponentens **Resurstyp** och **Resurssupertyp** (om den är definierad).
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

  Om utvecklaren har tillhandahållit dokumentation för komponenten visas den på fliken **Dokumentation**. Om det inte finns någon tillgänglig dokumentation visas inte fliken **Dokumentation**. <!-- If the developer has provided [documentation for the component](/help/sites-developing/developing-components.md#documenting-your-component), it will appear on the **Documentation** tab. If there is no documentation available, the **Documentation** tab will not be shown.-->

  ![Komponentdokumentation](/help/sites-cloud/authoring/assets/components-console-documentation.png)

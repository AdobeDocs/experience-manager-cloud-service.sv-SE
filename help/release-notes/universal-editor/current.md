---
title: Versionsinformation om Universal Editor 2025.02.17
description: Detta är versionsinformationen för version 2025.02.17 av Universal Editor.
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: c88aa13c6bc75c8f9cd624d00ef768290981c840
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---


# Versionsinformation om Universal Editor 2025.02.17 {#release-notes}

Det här är versionsinformationen för den 17 februari 2025-versionen av Universal Editor.

>[!TIP]
>
>Den aktuella versionsinformationen för Adobe Experience Manager as a Cloud Service finns på [den här sidan](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Nyheter {#what-is-new}

* **Publicera för förhandsgranskning** - [När du publicerar (eller avpublicerar) ditt innehåll](/help/sites-cloud/authoring/universal-editor/publishing.md) med den universella redigeraren kan du nu välja om du vill publicera i [förhandsvisningsmiljön](/help/sites-cloud/authoring/sites-console/previewing-content.md) utöver publiceringsmiljön
   * På så sätt kan du granska innehållet före publicering.
* **Modell och filter kan definieras i komponentdefinitionen** - Nu kan du definiera vilken modell och vilket filter en komponent använder [ i komponentdefinitionen.](/help/implementing/universal-editor/component-definition.md#template)
   * Denna information kan behållas centralt i definitionen och behöver inte anges för instrumenteringen.
   * På så sätt kan du flytta komponenter mellan behållare.
* **Underordnade element i behållare betraktas implicit som komponenter** - Om [ ett objekt med `data-aue-resource`](/help/implementing/universal-editor/attributes-types.md#data-properties) placeras som direkt underordnat element i en behållare betraktas det som en komponent och kan flyttas utan att du behöver ange `data-aue-behavior="component"`.

## Andra förbättringar {#other-improvements}

* **AEM 6.5 Resursväljare** - 6.5-resursväljaren öppnas nu korrekt när [den universella redigeraren körs med AEM 6.5.](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/implementing/developing/headless/universal-editor/introduction)

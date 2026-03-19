---
title: Versionsinformation om Universal Editor 2026.03.19
description: Detta är versionsinformationen för version 2026.03.19 av Universal Editor.
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: 8d9d162ec5bba99afb1ae86252a49a9880be4e68
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 1%

---


# Versionsinformation om Universal Editor 2026.03.19 {#release-notes}

Detta är versionsinformationen för den 19 mars 2026-utgåvan av Universal Editor.

>[!TIP]
>
>Om du vill testa de **kommande** funktionerna i den universella redigeraren innan de släpps, se [Versionsinformationen om den universella redigeraren.](/help/release-notes/universal-editor/preview.md)

>[!TIP]
>
>Den aktuella versionsinformationen för Adobe Experience Manager as a Cloud Service finns på [den här sidan](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Nyheter {#what-is-new}

* Objekten i egenskaperna är nu komprimerade när du går tillbaka till [hemskärmen.](/help/sites-cloud/authoring/universal-editor/navigation.md#home-button)
* [Resursväljaren](/help/implementing/universal-editor/configure-assets-selector.md) har nu stöd för [filterdefinitioner.](/help/implementing/universal-editor/filtering.md)
* Om det inte finns några tillgängliga åtgärder för det markerade objektet visar [inte längre snabbmenyn](/help/sites-cloud/authoring/universal-editor/authoring.md#context-menu) en förvrängning för att komma åt åtgärder.

## Andra förbättringar {#other-improvements}

* Om det finns en modell-/filter-/komponentdefinition uppdateras den när du växlar från ett program till ett annat i redigeraren.
* När du tar bort en bild lämnas inte längre tomma bildtaggar när du använder DA som back end.
* Klasser i block hanteras nu korrekt när DA används som back end-komponent.
* Open API sparar nu fjärrresurser som objekt.

## Brytningsändring {#breaking-change}

* Alla tillägg bör uppdateras till `@adobe/uix-guest` >= `1.1.7` för att förbättra stabiliteten.

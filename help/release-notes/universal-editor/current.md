---
title: Versionsinformation om Universal Editor 2025.03.10
description: Det här är versionsinformationen för version 2025.03.10 av Universal Editor.
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: b3c98f5e41dbc5e1714d0ed418a317199c735b73
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 1%

---


# Versionsinformation om Universal Editor 2025.03.10 {#release-notes}

Detta är versionsinformationen för den 10 mars 2025-utgåvan av Universal Editor.

>[!TIP]
>
>Den aktuella versionsinformationen för Adobe Experience Manager as a Cloud Service finns på [den här sidan](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Nyheter {#what-is-new}

* **Flytta komponenter:** [Om du flyttar komponenter mellan behållare](/help/sites-cloud/authoring/universal-editor/authoring.md#reordering-components) observeras nu komponentfiltret för målbehållaren.  
   * Det finns inte längre något krav på att ha samma [filterdefinition](/help/implementing/universal-editor/filtering.md) för både mål- och målbehållare för att komponenten ska kunna flyttas mellan behållarna.
* **Låsta sidor:** Universal Editor-tjänsten observerar [låsstatusen för en sida](/help/sites-cloud/authoring/sites-console/managing-pages.md#locking-a-page) och skriver bara till sidor som inte är låsta eller som är låsta av användaren.

## Andra förbättringar {#other-improvements}

* Korrigeringar gjordes för att korrigera valideringen för arbetsytan utan huvud.

## Föråldring {#deprecation}

* Biblioteket `universal-editor-cors` som tillhandahålls via npm eller `https://unviersal-editor-service.experiencecloud.live/corslib/*` ska inte längre användas.
   * En skripttagg som pekar på `https://universal-editor-service.adobe.io/cors.js` ska användas i stället.
   * Se [Universal Editor Overview for AEM Developers](/help/implementing/universal-editor/developer-overview.md) för mer information om hur du kan mäta upp sidan för användning med Universal Editor.
   * Användarna ser ett borttagningsmeddelande en gång om dagen om fel metod används.

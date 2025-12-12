---
title: Versionsinformation om Universal Editor 2025.12.12
description: Detta är versionsinformationen för version 2025.12.11 av Universal Editor.
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: 577bc81c35ad052a96b85ed4de13b21f06e385aa
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 0%

---


# Versionsinformation om Universal Editor 2025.12.12 {#release-notes}

Det här är versionsinformationen för den 12 december 2025-versionen av Universal Editor.

>[!TIP]
>
>Om du vill testa de **kommande** funktionerna i den universella redigeraren innan de släpps, se [Versionsinformationen om den universella redigeraren.](/help/release-notes/universal-editor/preview.md)

>[!TIP]
>
>Den aktuella versionsinformationen för Adobe Experience Manager as a Cloud Service finns på [den här sidan](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Nyheter {#what-is-new}

* Stöd har lagts till i befintliga tabeller i [RTF-redigeraren.](/help/sites-cloud/authoring/universal-editor/authoring.md#formatting-options)
* Tabbtangenten har aktiverats för kapslade listor i [RTF-redigeraren.](/help/sites-cloud/authoring/universal-editor/authoring.md#formatting-options)
* Inloggningsfunktionen för utvecklare kan nu inaktiveras via [meta-taggen `dev-login`.](/help/implementing/universal-editor/customizing.md#meta-tags)
* En högerklickning i övertäckningssektionen visar nu en [snabbalternativmeny.](/help/sites-cloud/authoring/universal-editor/authoring.md#context-options)
* [Omfångsindrag](/help/implementing/universal-editor/configure-rte.md#indentation) stöds nu i [RTF-redigeraren.](/help/sites-cloud/authoring/universal-editor/authoring.md#formatting-options)

## Funktioner för tidig användning {#early-adopter}

Om du är intresserad av att testa de kommande funktionerna som listas nedan och dela med dig av dina synpunkter skickar du ett e-postmeddelande till din Adobe Customer Success Manager från den e-postadress som är kopplad till din Adobe ID.

* Grund kopia har implementerats för innehållsfragment.

## Andra förbättringar {#other-improvements}

* Egenskapsfältet synkroniseras nu när flera fält ändras i sitt sammanhang.
* Innehållsfragmentväljaren öppnas nu som väntat i AEM 6.5-instanser.
* Esc-tangenten stänger nu dialogrutor i RTF-redigeraren.
* Åtgärden **Ta bort komponent** är nu bara tillgänglig när en komponent är markerad.
* Den korrekta (gamla eller nya) redigeraren för innehållsfragment öppnas nu baserat på den använda instansen (om värdnamnet är AEM as a Cloud Service-mönstret använder du den nya redigeraren, annars använder du den äldre redigeraren).
* Filtervalidering läggs till i dubblettåtgärden.
* Långa titlar trunkeras nu i egenskapsfältet.
* Matriser för hantering av flera webbplatser med fler än 10 värden hanteras nu korrekt.
* Konfliktfel vid skapande av flera komponenter med samma namn hanteras nu korrekt.
* Matrishantering för flera platser med värden >10 lades till.

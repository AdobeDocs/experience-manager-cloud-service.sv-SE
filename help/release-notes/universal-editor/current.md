---
title: Versionsinformation om Universal Editor 2026.02.19
description: Detta är versionsinformationen för version 2026.02.19 av Universal Editor.
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: 39137052e9fa409f7f5494be53fa7693aaa60b17
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 0%

---


# Versionsinformation om Universal Editor 2026.02.19 {#release-notes}

Det här är versionsinformationen för den 19 februari 2026-versionen av Universal Editor.

>[!TIP]
>
>Om du vill testa de **kommande** funktionerna i den universella redigeraren innan de släpps, se [Versionsinformationen om den universella redigeraren.](/help/release-notes/universal-editor/preview.md)

>[!TIP]
>
>Den aktuella versionsinformationen för Adobe Experience Manager as a Cloud Service finns på [den här sidan](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Nyheter {#what-is-new}

* RTE har förbättrats.
   * [Det finns nu stöd för att dölja verktygsfältsobjekt i kontext-RTE](/help/implementing/universal-editor/configure-rte.md#common-action-options).
   * [Det finns nu stöd för figursättning av text i tabeller med stycken ](/help/implementing/universal-editor/configure-rte.md#table-actions).
   * [HTML-taggar](/help/implementing/universal-editor/configure-rte.md#unsupported-html) som inte stöds kan nu bevaras av RTE.
   * RTE-logik används nu från en separat fil.
   * [Tabeller kan nu skapas](/help/sites-cloud/authoring/universal-editor/authoring.md#formatting-options) och redigeras med RTE.
* Om ingen etikett anges används komponentens rubrik från komponentdefinitionen.
* `setEditorMode` är nu tillgängligt via tillägg.

## Funktioner för tidig användning {#early-adopter}

Om du är intresserad av att testa de kommande funktionerna som listas nedan och dela med dig av dina synpunkter skickar du ett e-postmeddelande till din Adobe Customer Success Manager från den e-postadress som är kopplad till din Adobe ID.

* Grund kopia har implementerats för innehållsfragment.

## Andra förbättringar {#other-improvements}

* RTE-slutpunkter används nu för redigeraren på plats.
* När du redigerar kapslade fält skrivs peer-poster från dessa strukturer inte längre över.
* Obligatoriska RTE-fält kan inte längre sparas som tomma.
* Formatering på plats används inte längre felaktigt när länkar läggs till efter formatering.

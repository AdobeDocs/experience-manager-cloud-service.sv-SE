---
title: Versionsinformation om förhandsvisning i Universal Editor
description: Det här är versionsinformationen för förhandsversionen av Universal Editor.
feature: Release Information
role: Admin
exl-id: e8d031aa-4676-4e45-977b-e5dffcc404c4
source-git-commit: 374c8045043f67f06d4ae68aef499bb594f1c08c
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%

---

# Versionsinformation om förhandsvisning i Universal Editor {#preview}

Det här är versionsinformationen för **förhandsvisningsversionen** av den universella redigeraren. De här funktionerna är för närvarande tillgängliga i den universella redigerarens **förhandsvisningsmiljö**. Dessa funktioner är planerade att släppas allmänt tillgängliga den 19 februari 2026.

Versionsinformationen **preview** är praktisk så att du vet vilka ändringar som kommer att göras i den universella redigeraren och kan testa dem genom att [växla till förhandsvisningsversionen.](/help/sites-cloud/authoring/universal-editor/navigation.md#user-properties)

>[!TIP]
>
>Information om **aktuell versionsinformation** för den universella redigeraren finns i dokumentet [Universal Editor Release Notes.](/help/release-notes/universal-editor/current.md)

>[!NOTE]
>
>Innehållet i den faktiska versionen samt releasedatumet kan komma att ändras.

## Kommande nya funktioner {#what-is-new}

* RTE har förbättrats.
   * Nu finns stöd för att dölja verktygsfältsobjekt i kontext-RTE.
   * Nu finns stöd för radbrytning av text i tabeller med stycken.
   * RTE-taggar som inte stöds bevaras nu.
   * RTE-logik används nu från en separat fil.
   * Tabeller kan nu skapas och redigeras med RTE.
* Om ingen etikett anges används komponentens rubrik från komponentdefinitionen.
* `setEditorMode` är nu tillgängligt via tillägg.

## Kommande förbättringar {#other-improvements}

* Funktionen Kopiera och klistra in mellan sidor har åtgärdats.
* `universal-editor-extensibility` har flyttats till `universal-editor`.
* Antalet begäranden till tilläggsslutpunkten har reducerats.
* RemoteApp-avmonteringar har reducerats från tre till ett.
* RTE-slutpunkter används nu för redigeraren på plats.
* När du redigerar kapslade fält skrivs peer-poster från dessa strukturer inte längre över.
* Obligatoriska RTE-fält kan inte längre sparas som tomma.
* Formatering på plats används inte längre felaktigt när länkar läggs till efter formatering.

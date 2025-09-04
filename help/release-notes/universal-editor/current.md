---
title: Versionsinformation om Universal Editor 2025.09.04
description: Detta är versionsinformationen för version 2025.09.04 av Universal Editor.
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: 0c380e0faca1db0966d22d056dd1f824a731a7bc
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---


# Versionsinformation om Universal Editor 2025.09.04 {#release-notes}

Det här är versionsinformationen för den 4 september 2025-versionen av Universal Editor.

>[!TIP]
>
>Den aktuella versionsinformationen för Adobe Experience Manager as a Cloud Service finns på [den här sidan](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Nyheter {#what-is-new}

* Kopiera och klistra in är tillgängligt för [tidiga användare](#copy-paste)

### Ångra/Gör om {#undo-redo}

Ångra och gör om är nu tillgängligt för innehållsförfattare i Universal Editor.

* Detta inkluderar redigeringar som görs i sitt sammanhang, redigeringar som görs via panelen Egenskaper samt tillägg (eller duplicering), flytt och borttagning av block.
* Ångra och gör om är begränsat till den aktuella webbläsarsessionen.

## Funktioner för tidig användning {#early-adopter}

Om du är intresserad av att testa dessa kommande funktioner och dela med dig av dina synpunkter skickar du ett e-postmeddelande till din Adobe Customer Success Manager från den e-postadress som är kopplad till din Adobe ID.

### Ny RTE {#new-rte}

Den nya ProseMirror RTE med en sidväljare i länkdialogrutan är nu tillgänglig på den högra panelen.

### Kopiera/klistra in {#copy-paste}

Kopiera och klistra in komponenter på samma sida är nu tillgängligt för innehållsförfattare.

## Andra förbättringar {#other-improvements}

* Utformningen av redigeringsverktygsfältet har uppdaterats för att bättre överensstämma med den kommande nya textredigeringsfunktionen.
* Filtren i resursväljarens dialogruta har återställts.

## Undertryckningar {#deprecations}

* Komponenterna `text-input` och `text-area` togs officiellt bort med [release 2025.07.09.](/help/release-notes/universal-editor/2025/2025-07-09.md)
   * I `model-definition.json` använder du textkomponenten för att skapa textinmatningar för egenskapspanelen.

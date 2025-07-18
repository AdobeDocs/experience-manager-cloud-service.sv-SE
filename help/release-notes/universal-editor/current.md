---
title: Versionsinformation om Universal Editor 2025.07.09
description: Det här är versionsinformationen för version 2025.07.09 av Universal Editor.
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: 199ee7e11f6706773bd426c3d27236d6ea791a6c
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 0%

---


# Versionsinformation om Universal Editor 2025.07.09 {#release-notes}

Detta är versionsinformationen för den 9 juli 2025-versionen av Universal Editor.

>[!TIP]
>
>Den aktuella versionsinformationen för Adobe Experience Manager as a Cloud Service finns på [den här sidan](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Nyheter {#what-is-new}

* [Om bara en komponenttyp tillåts när du klickar på verktygsfältsknappen **Lägg till** på behållare, ](/help/sites-cloud/authoring/universal-editor/authoring.md#adding-components) infogas den omedelbart utan att du behöver välja någon från den nedrullningsbara menyn.
* [Verktygsfältsalternativet ](/help/sites-cloud/authoring/universal-editor/navigation.md#autentication-settings) för autentiseringshuvudet har placerats bakom en funktionsväxling, eftersom det inte är användbart i de flesta fall.
* [Eftersom behållarkapsling inte tillåts för flera fält på egenskapspanelen ](/help/implementing/universal-editor/field-types.md#fields) filtrerar återgivningsrutinen nu bort kapslade behållare från fältlistan för att förhindra ogiltig kapsling.

## Funktioner för tidig användning {#early-adopter}

Om du är intresserad av att testa dessa kommande funktioner och dela med dig av dina synpunkter skickar du ett e-postmeddelande till din Adobe Customer Success Manager från den e-postadress som är kopplad till din Adobe ID.

### Ny RTE {#new-rte}

Den nya ProseMirror RTE med en sidväljare i länkdialogrutan är nu tillgänglig på den högra panelen.

### Ångra/Gör om {#undo-redo}

Ångra och gör om är nu tillgängligt för innehållsförfattare i Universal Editor.

* Detta inkluderar redigeringar som görs i sitt sammanhang, redigeringar som görs via panelen Egenskaper samt tillägg (eller duplicering), flytt och borttagning av block.
* Ångra och gör om är begränsat till den aktuella webbläsarsessionen.

## Andra förbättringar {#other-improvements}

* Ett problem har korrigerats där borttagning av en enda resursreferens inte var möjlig vid redigering via egenskapsfältet.
* Ett problem har korrigerats där egenskapspanelen lästes in oavbrutet eftersom resursreferenser automatiskt konverterades till arrayer, vilket orsakade ett oändligt inläsningstillstånd.
   * Resursreferensvärden lagras nu som de är, utan automatisk konvertering till arrayer.
* Ett problem har korrigerats där egenskapspanelen inte visade fält när en modell definierades men inte innehöll något innehåll.
   * Detta orsakade ett oändligt inläsningsläge för egenskapspanelen för tomma detaljsvar, som tomma innehållsfragment.
* ESLint-konfigurationen har omarbetats för kompatibilitet med version 9, inklusive uppdaterade regler och stöd för plugin-program.

## Undertryckningar {#deprecations}

* Komponenten `text-input` är nu officiellt föråldrad.
   * I `model-definition.json` använder du textkomponenten för att skapa textinmatningar för egenskapspanelen.

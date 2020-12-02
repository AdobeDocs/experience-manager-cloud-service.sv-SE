---
title: Förhandsgranska sidor med ContextHub-data
description: Verktygsfältet ContextHub visar data från ContextHub-butiker och gör att du kan ändra lagringsdata. Det är användbart för förhandsgranskning av innehåll
translation-type: tm+mt
source-git-commit: e361f24b943eff68982a37ac0dc2597f92450026
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 2%

---


# Förhandsgranska sidor med ContextHub-data  {#previewing-pages-using-contexthub-data}

Verktygsfältet ContextHub visar data från ContextHub-arkiv och gör att du kan ändra lagringsdata. Verktygsfältet ContextHub är användbart när du vill förhandsgranska innehåll som bestäms av data i ett ContextHub-lager.

Verktygsfältet består av en serie användargränssnittslägen som innehåller en eller flera användargränssnittsmoduler.

* Gränssnittslägen är ikoner som visas till vänster i verktygsfältet. När du klickar på eller trycker på en ikon visas de gränssnittsmoduler som finns i verktygsfältet.
* Gränssnittsmoduler visar data från en eller flera ContextHub-butiker. Vissa gränssnittsmoduler gör det även möjligt för dig att ändra lagrade data.

ContextHub installerar flera gränssnittslägen och gränssnittsmoduler. Din administratör kan ha [konfigurerat ContextHub](/help/implementing/developing/personalization/configuring-contexthub.md) för att visa olika.

## Visar ContextHub-verktygsfältet {#revealing-the-contexthub-toolbar}

Verktygsfältet ContextHub är tillgängligt i förhandsgranskningsläget. Verktygsfältet är bara tillgängligt på författarinstanser och endast när administratören har aktiverat det.

![Verktygsfältet ContextHub](/help/sites-cloud/authoring/assets/contexthub-toolbar.png)

1. Öppna sidan för redigering, klicka eller tryck på Förhandsgranska i verktygsfältet.

   ![Knappen Förhandsgranska](/help/sites-cloud/authoring/assets/contexthub-preview-button.png)

1. Visa verktygsfältet genom att klicka på eller trycka på ikonen ContextHub.

   ![Knappen ContextHub](/help/sites-cloud/authoring/assets/contexthub-button.png)

## Funktioner för användargränssnittsmodul {#ui-module-features}

Varje gränssnittsmodul innehåller olika uppsättningar funktioner, men följande typer av funktioner är vanliga. Eftersom gränssnittsmodulerna kan utökas kan utvecklaren implementera andra funktioner efter behov.

### Verktygsfältsinnehåll {#toolbar-content}

Gränssnittsmoduler kan visa data från en eller flera ContextHub-butiker i verktygsfältet. I gränssnittsmoduler används en ikon och en titel för att identifiera sig själva.

![ContextHub-profiler](/help/sites-cloud/authoring/assets/contexthub-persona-button.png)

### Popup-innehåll {#popup-content}

Vissa gränssnittsmoduler visar en popup-övertäckning när de klickas eller trycks på. Vanligtvis innehåller popup-fönstret mer information än vad som visas i verktygsfältet.

![Profilinformation för ContextHub](/help/sites-cloud/authoring/assets/contexthub-profile.png)

### Popup Forms {#popup-forms}

Popup-överlägget för en modul kan innehålla formulärelement som gör att du kan ändra data i ContextHub-arkivet. Om sidinnehållet bestäms av lagringsdata kan du använda formuläret och observera ändringar i sidinnehållet.

### Helskärmsläge {#fullscreen-mode}

Popup-övertäckningar kan innehålla en ikon som du klickar på eller trycker på för att expandera popup-innehållet så att det täcker hela webbläsarfönstret eller skärmen.

![Helskärmsknapp](/help/sites-cloud/authoring/assets/contexthub-fullscreen.png)

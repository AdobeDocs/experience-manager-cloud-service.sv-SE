---
title: Publicera innehåll med den universella redigeraren
description: Lär dig hur den universella redigeraren publicerar innehåll och hur dina appar kan hantera det publicerade innehållet.
exl-id: aee34469-37c2-4571-806b-06c439a7524a
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 3288edacba909335f8109eee7e1e793abe5a8343
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 0%

---


# Publicera innehåll med den universella redigeraren {#publishing}

Lär dig hur den universella redigeraren publicerar innehåll och hur dina appar kan hantera det publicerade innehållet.

>[!TIP]
>
>Den publiceringsprocess som beskrivs här är standardfunktionen i den universella redigeraren.
>
>Den universella redigeraren har också stöd för [tillägg och UI-utökningsmöjligheter](/help/implementing/universal-editor/extending.md) så att arbetsflöden kan stödja publiceringsprocessen, vilket kan ge olika publiceringsflöden.

## Publicera innehåll från den universella redigeraren {#publishing-content}

När du som innehållsförfattare är redo att publicera ditt innehåll behöver du bara trycka eller klicka på ikonen **Publicera** i den universella redigerarens verktygsfält.

![Publicerar sidor](assets/publish-menu.png)

1. Tryck eller klicka på ikonen **Publicera** i den universella redigerarens verktygsfält.](/help/sites-cloud/authoring/universal-editor/navigation.md#publish)[
1. Om du har en [förhandsgranskningstjänst](/help/sites-cloud/authoring/sites-console/previewing-content.md) tillgänglig kan du välja var du vill publicera ditt innehåll, antingen till **[Förhandsgranska](/help/sites-cloud/authoring/sites-console/previewing-content.md)** (om den är tillgänglig) eller **Publicera**.
1. I avsnittet **Objekt** visas innehållet som ingår i publikationen, inklusive:
   * **Nya** objekt som ännu inte har publicerats.
   * **Ändrat** innehåll som har publicerats, men ändrats sedan den senaste publikationen.
   * **Publicerat** innehåll som har publicerats och inte ändrats sedan den publiceringen.

   Tryck eller klicka på kryssrutorna bredvid dessa objekt för att inkludera/exkludera dem från publiceringen efter behov. Tryck eller klicka på **Utöka** om du vill visa enskilda objekt som ingår i summorna för de tre kategorierna och kunna in/exkludera dem individuellt.

   ![Publicera objekt](assets/publish-items.png)

   Tryck eller klicka på bakåtpilen bredvid rubriken **Items** för att återgå till översikten.

1. Tryck eller klicka på **Publicera** för att publicera eller **Avbryt** för att avbryta.

>[!NOTE]
>
>Alternativet att publicera till förhandsgranskning [kan inaktiveras](/help/implementing/universal-editor/customizing.md#publish-preview) och kanske inte visas i redigeraren.

## Avpublicera innehåll från den universella redigeraren {#unpublishing-content}

Att avpublicera innehåll fungerar på ungefär samma sätt som att publicera innehåll. När du som innehållsförfattare är redo att ta bort innehåll från publikationen trycker eller klickar du på ellipsikonen i den universella redigerarens verktygsfält och sedan **Avpublicera**.

Du har sedan samma alternativ för att avpublicera innehåll som du gjorde när du publicerade [innehåll.](#publishing-content) inkluderar avpublicering från en förhandsgranskningsinstans om sådan finns och vilka objekt som ska tas med i avpubliceringen.

## Publicera och avpublicera från Sites Console {#publishing-sites-console}

Du kan också publicera [ från webbplatskonsolen ](/help/sites-cloud/authoring/sites-console/publishing-pages.md) som kan vara användbar när du vill publicera flera sidor med innehåll eller schemalägga publicering eller avpublicering.

## Ytterligare resurser {#additional-resources}

Läs det här dokumentet om du vill lära dig hur du skapar innehåll med den universella redigeraren.

* [Skapa innehåll med den universella redigeraren](authoring.md) - Lär dig hur enkelt och intuitivt det är för innehållsförfattare att skapa innehåll med den universella redigeraren.

Mer information om de tekniska detaljerna i Universal Editor finns i dessa utvecklardokument.

* [Introduktion till universell redigering](/help/implementing/universal-editor/introduction.md) - Lär dig hur den universella redigeraren kan redigera alla delar av innehåll i alla implementeringar så att du kan leverera enastående upplevelser, öka innehållets hastighet och skapa en toppmodern utvecklarupplevelse.
* [Komma igång med den universella redigeraren i AEM](/help/implementing/universal-editor/getting-started.md) - Lär dig hur du får tillgång till den universella redigeraren och hur du börjar använda den i ditt första AEM-program.
* [Universell redigeringsarkitektur](/help/implementing/universal-editor/architecture.md) - Lär dig mer om arkitekturen för den universella redigeraren och hur data flödar mellan dess tjänster och lager.
* [Attribut och typer](/help/implementing/universal-editor/attributes-types.md) - Lär dig mer om de dataattribut och datatyper som krävs för den universella redigeraren.
* [Autentisering av universell redigerare](/help/implementing/universal-editor/authentication.md) - Lär dig hur den universella redigeraren autentiseras.

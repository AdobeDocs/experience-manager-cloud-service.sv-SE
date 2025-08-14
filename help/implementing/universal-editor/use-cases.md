---
title: Användningsexempel och inlärningssökvägar i Universal Editor
description: Lär dig mer om de viktigaste användningsexemplen i Universal Editor och hur du bäst lär dig mer om hur det används och hur du implementerar det i dina egna projekt.
exl-id: 398ad0e2-c299-4c49-9784-05c84c67bec2
feature: Developing
role: Admin, Architect, Developer
source-git-commit: bb149cd43158bfd1ceb43b04cc536c8c8291f968
workflow-type: tm+mt
source-wordcount: '882'
ht-degree: 0%

---

# Användningsexempel och inlärningssökvägar i Universal Editor {#use-cases-learning-paths}

Lär dig mer om de viktigaste användningsexemplen i Universal Editor och hur du bäst lär dig mer om hur det används och hur du implementerar det i dina egna projekt.

## Ökning {#overview}

Universal Editor är en mångsidig visuell editor som ingår i Adobe Experience Manager Sites. Man kan redigera det man redan gjort i WYSIWYG utan att behöva ta del av en massa rubriker.

I det här dokumentet förklaras dessa två användningsområden i detalj och du får lära dig mer om dem så att du kan implementera den universella redigeraren i ditt eget projekt.

>[!TIP]
>
>Om du inte redan gjort det kan du läsa dokumentet [Universal Editor Introduction](/help/implementing/universal-editor/introduction.md) för att få en fullständig översikt över och ett värde för Universal Editor.

## Användningsexempel {#use-cases}

Den universella redigeraren är en bekväm och intuitiv visuell redigerare för alla som skapar innehållet. De två huvudsakliga användningsområdena är:

* [WYSIWYG Authoring](#wysiwyg-authoring) - Använd AEM Sites-konsolen för att hantera innehåll och författarsidor i AEM med den universella redigeraren
* [Headless Authoring](#headless-authoring) - Skapa innehåll i ditt eget headless-program med Universal Editor.

### WYSIWYG Authoring {#wysiwyg-authoring}

Om du redan känner till AEM kan du använda webbplatskonsolen för att skapa och hantera dina sidor och sedan redigera dem med den universella redigeraren.

På så sätt kan du dra nytta av de verktyg som finns i Sites-konsolen, till exempel sidhantering (kopiera, klistra in, flytta) och arbetsflöden, men du kan också utnyttja den moderna universella redigeraren.

Om det är ditt sätt att arbeta kan du i nästa steg få en komplett översikt över hur du kommer igång med Universal Editor i AEM.

1. [Guiden Komma igång för utvecklare för WYSIWYG-redigering med Edge Delivery Services](https://www.aem.live/developer/ue-tutorial) - Kom igång med ditt första Universal Editor-projekt i AEM
1. [Skapar block som är instrumenterade för användning med den universella redigeraren](https://www.aem.live/developer/universal-editor-blocks) - Lär dig hur du gör instrumentblock för att göra ditt innehåll redigerbart i den universella redigeraren
1. [Innehållsmodellering för WYSIWYG-redigering med Edge Delivery Services Projects](https://www.aem.live/developer/component-model-definitions) - Lär dig mer om hur block är strukturerade för att effektivt modellera ditt innehåll för användning med den universella redigeraren.

När du har läst dessa dokument kan du gå tillbaka till den här sidan för att lära dig mer om hur du använder utan rubrik och hur den universella redigeraren fungerar i allmänhet.

### Headless Authoring {#headless-authoring}

Om du redan har en headless-app kan du använda den universella redigeraren för att skapa innehåll för appen och behålla dess innehåll som innehållsfragment i AEM. Det enda kravet är att programmet är instrumenterat för att tillåta användning av den universella redigeraren.

Om detta är ditt sätt att arbeta kan du i nästa steg se följande dokument som ett exempel på en headless-app som har instrument för att använda Universal Editor.

* [SecurBank-exempelapp för Universal Editor](/help/implementing/universal-editor/securbank.md)

När du har läst det dokumentet kan du gå tillbaka till den här sidan för att lära dig mer om WYSIWYG redigeringsprogram och hur den universella redigeraren fungerar i allmänhet.

{{ue-headless-auth}}

## How the Universal Editor Works {#how-ue-works}

Den universella redigerarens styrka är möjligheten att skapa allt innehåll på plats, vilket ger innehållsförfattaren ett helt intuitivt och enhetligt användargränssnitt oavsett vilket innehåll det gäller.

Universal Editor fungerar på följande sätt.

1. En utvecklare instrumenterar programmet eller sidan för att använda den universella redigeraren. Den här instrumenteringen talar om för redigeraren vilket innehåll som kan redigeras och hur det ska bevaras.
   * Om du följer [Developer Getting Started Guide for WYSIWYG Authoring with Edge Delivery Services](https://www.aem.live/developer/ue-tutorial) -dokumentationen, så används sidorna automatiskt.
   * För headless-redigering är det enkelt att instrumentera appen.
1. Innehållsförfattaren läser in Universal Editor, som i sin tur läser in sidan för redigering. Eftersom den är instrumenterad vet den vilket innehåll som är redigerbart och hur det ska återges och bevaras.
1. Innehållsförfattaren redigerar sidinnehållet i ett intuitivt WYSIWYG-gränssnitt och redigerar det på plats.
1. Den universella redigeraren återställer automatiskt ändringarna till datakällan.

Om du vill veta mer om arkitekturen för den universella redigeraren kan du läsa dokumentet [Universal Editor Architecture](/help/implementing/universal-editor/architecture.md).

## Universal Editor Concepts {#concepts}

För att en sida eller ett program ska kunna redigeras av den universella redigeraren måste den vara korrekt instrumenterad.

* [Attribut och typer](/help/implementing/universal-editor/attributes-types.md) - För att ett program eller en sida ska kunna redigeras av den universella redigeraren måste det vara korrekt instrumenterat. Detta inkluderar rätt metadata så att redigeraren kan redigera innehållet i programmet.
* [Modelldefinitioner, fält och komponenttyper](/help/implementing/universal-editor/field-types.md) - När metadata finns för att aktivera redigering av en komponent definierar du vilka fält och komponenttyper som de kan ändra på egenskapspanelen i redigeraren.
* [Universella redigeringshändelser](/help/implementing/universal-editor/events.md) - Du kan anpassa appen ytterligare genom att förbättra redigeringsupplevelsen i appen genom att använda händelser som den universella redigeraren genererar på innehåll eller gränssnittsinteraktioner.

Den universella redigeraren kan också anpassas efter dina projektbehov.

* [Anpassa den universella redigeraren](/help/implementing/universal-editor/customizing.md) - Du kan anpassa funktionen för den universella redigeraren genom att filtrera olika delar av redigeraren eller genom att utöka redigerarens funktioner.
* [Utöka den universella redigeraren](/help/implementing/universal-editor/extending.md) - Gränssnittet i den universella redigeraren kan utökas för att utöka dess funktioner så att det passar dina projektbehov.

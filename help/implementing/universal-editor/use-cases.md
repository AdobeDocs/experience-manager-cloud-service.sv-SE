---
title: Användningsexempel och inlärningssökvägar i Universal Editor
description: Lär dig mer om de viktigaste användningsexemplen i Universal Editor och hur du bäst lär dig mer om hur det används och hur du implementerar det i dina egna projekt.
exl-id: 398ad0e2-c299-4c49-9784-05c84c67bec2
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 7ad9a959592f1e8cebbcad9a67d280d5b2119866
workflow-type: tm+mt
source-wordcount: '863'
ht-degree: 0%

---

# Användningsexempel och inlärningssökvägar i Universal Editor {#use-cases-learning-paths}

Lär dig mer om de viktigaste användningsexemplen i Universal Editor och hur du bäst lär dig mer om hur det används och hur du implementerar det i dina egna projekt.

## Ökning {#overview}

Universal Editor är en mångsidig visuell editor som ingår i Adobe Experience Manager Sites. Med det kan författare redigera vad-du-se-is-what-you-get (WYSIWYG) oavsett headless eller headful experience.

I det här dokumentet förklaras dessa två användningsområden i detalj och du får lära dig mer om dem så att du kan implementera den universella redigeraren i ditt eget projekt.

>[!TIP]
>
>Om du inte redan gjort det kan du läsa dokumentet [Universal Editor Introduction](/help/implementing/universal-editor/introduction.md) för att få en fullständig översikt över och ett värde för Universal Editor.

## Användningsexempel {#use-cases}

Den universella redigeraren är en bekväm och intuitiv visuell redigerare för alla som skapar innehållet. De två huvudsakliga användningsområdena är:

* [WYSIWYG-redigering](#wysiwyg-authoring) - Använd AEM Sites-konsolen för att hantera ditt innehåll och författarsidor i AEM med den universella redigeraren
* [Headless Authoring](#headless-authoring) - Skapa innehåll i ditt eget headless-program med Universal Editor.

### WYSIWYG-redigering {#wysiwyg-authoring}

Om du redan känner till AEM kan du använda konsolen Platser för att skapa och hantera dina sidor och sedan redigera dem med den universella redigeraren.

På så sätt kan du dra nytta av de verktyg som finns i Sites-konsolen, till exempel sidhantering (kopiera, klistra in, flytta) och arbetsflöden, men du kan också utnyttja den moderna universella redigeraren.

Om det är ditt sätt att arbeta kan du i nästa steg få en fullständig översikt över hur du kommer igång med den universella redigeraren i AEM.

1. [Guiden Komma igång för utvecklare för WYSIWYG-redigering med Edge Delivery Services](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md) - Kom igång med ditt första Universal Editor-projekt i AEM
1. [Skapar block som är instrumenterade för användning med den universella redigeraren](/help/edge/wysiwyg-authoring/create-block.md) - Lär dig hur du gör instrumentblock för att göra ditt innehåll redigerbart i den universella redigeraren
1. [Innehållsmodellering för WYSIWYG-redigering med Edge Delivery Services Projects](/help/edge/wysiwyg-authoring/content-modeling.md) - Lär dig mer om hur block är strukturerade för att effektivt modellera ditt innehåll för användning med den universella redigeraren.

När du har läst dessa dokument kan du gå tillbaka till den här sidan för att lära dig mer om hur du använder utan rubrik och hur den universella redigeraren fungerar i allmänhet.

### Headless Authoring {#headless-authoring}

Om du redan har ett headless-program kan du använda den universella redigeraren för att skapa innehåll för programmet och behålla innehållet som innehållsfragment i AEM. Det enda kravet är att programmet är instrumenterat för att tillåta användning av den universella redigeraren.

Om detta är ditt sätt att arbeta kan du i nästa steg se följande dokument som ett exempel på en headless-app som har instrument för att använda Universal Editor.

* [SecurBank-exempelapp för Universal Editor](/help/implementing/universal-editor/securbank.md)

När du har läst dokumentet kan du gå tillbaka till den här sidan för att lära dig mer om WYSIWYG-redigeringsverktyget och hur den universella redigeraren fungerar i allmänhet.

## How the Universal Editor Works {#how-ue-works}

Den universella redigerarens styrka är möjligheten att skapa allt innehåll på plats, vilket ger innehållsförfattaren ett helt intuitivt och enhetligt användargränssnitt oavsett vilket innehåll det gäller.

Universal Editor fungerar på följande sätt.

1. En utvecklare instrumenterar programmet eller sidan för att använda den universella redigeraren. Den här instrumenteringen talar om för redigeraren vilket innehåll som kan redigeras och hur det ska bevaras.
   * För WYSIWYG-redigering instrumenteras sidor som skapas med mallmallen automatiskt.
   * För headless-redigering är det enkelt att instrumentera appen.
1. Innehållsförfattaren läser in Universal Editor, som i sin tur läser in sidan för redigering. Eftersom den är instrumenterad vet den vilket innehåll som är redigerbart och hur det ska återges och bevaras.
1. Innehållsförfattaren redigerar sidinnehållet i ett intuitivt WYSIWYG-gränssnitt och redigerar på plats.
1. Den universella redigeraren återställer automatiskt ändringarna till AEM.

Om du vill veta mer om arkitekturen för Universal Editor kan du läsa dokumentet [Universal Editor Architecture.](/help/implementing/universal-editor/architecture.md)

## Universal Editor Concepts {#concepts}

För att en sida eller ett program ska kunna redigeras av den universella redigeraren måste den vara korrekt instrumenterad. När den har instrumenterats kan den anpassas ytterligare efter dina projektbehov.

* [Attribut och typer](/help/implementing/universal-editor/attributes-types.md) - För att ett program eller en sida ska kunna redigeras av den universella redigeraren måste det vara korrekt instrumenterat. Detta inkluderar rätt metadata så att redigeraren kan redigera innehållet i programmet.
* [Modelldefinitioner, fält och komponenttyper](/help/implementing/universal-editor/field-types.md) - När metadata finns för att aktivera redigering av en komponent definierar du vilka fält och komponenttyper som de kan ändra i egenskapsfältet i redigeraren. Det gör du genom att skapa en modell och länka till den från komponenten.
* [Anpassa redigeringsupplevelsen för den universella redigeraren](/help/implementing/universal-editor/customizing.md) - När appen eller sidan är helt instrumenterad kan redigerarupplevelsen för den universella redigeraren anpassas ytterligare genom att de tillgängliga komponenterna filtreras eller genom att redigerarens funktionalitet utökas.
* [Universella redigeringshändelser](/help/implementing/universal-editor/events.md) - Du kan anpassa appen ytterligare genom att reagera på standardhändelser som universella skickar vid ändringar av innehållet och användargränssnittet.

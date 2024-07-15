---
title: Universal Editor Architecture
description: Läs mer om arkitekturen i den universella redigeraren och hur data flödar mellan tjänster och lager.
exl-id: e6f40743-0f21-4fb6-bf23-76426ee174be
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 0%

---


# Universal Editor Architecture {#architecture}

Läs mer om arkitekturen i den universella redigeraren och hur data flödar mellan tjänster och lager.

## Byggblock för arkitektur {#building-blocks}

Den universella redigeraren består av fyra viktiga byggblock som interagerar så att skribenterna kan redigera alla delar av innehållet i alla implementeringar, så att ni kan leverera enastående upplevelser, öka innehållets hastighet och skapa en toppmodern utvecklarupplevelse.

1. [Redigerare](#editors)
1. [Remote App](#remote-app)
1. [API-lager](#api-layer)
1. [Beständigt lager](#persistence-layer)

I det här dokumentet beskrivs dessa byggstenar och hur de utbyter data.

![Arkitektur för Universal Editor](assets/architecture.png)

>[!TIP]
>
>Om du vill se hur den universella redigeraren och dess arkitektur fungerar ska du läsa [Komma igång med den universella redigeraren i AEM](getting-started.md) för att lära dig hur du får tillgång till den universella redigeraren och hur du börjar använda den AEM första appen.

### Redigerare {#editors}

* **Universell redigerare** - Universell redigerare använder en instrumenterad DOM för att tillåta redigering av innehåll på plats. Mer information om nödvändiga metadata finns i [Attribut och typer](attributes-types.md). I dokumentet [Komma igång med den universella redigeraren i AEM](getting-started.md) finns ett exempel på instrumenteringen i AEM.
* **Egenskapsspår** - Vissa egenskaper i komponenter kan inte redigeras i sitt sammanhang, till exempel kan en karusells rotationstid eller vilken dragspelsflik alltid ska öppnas eller stängas. För att sådan komponentinformation ska kunna redigeras finns en formulärbaserad redigerare i sidlisten i redigeraren.

### Remote App {#remote-app}

DOM måste vara instrumenterad för att ett program ska kunna redigeras i sitt sammanhang i den universella redigeraren. Fjärrprogrammet måste återge vissa attribut i DOM. Mer information om nödvändiga metadata finns i [Attribut och typer](attributes-types.md). I dokumentet [Komma igång med den universella redigeraren i AEM](getting-started.md) finns ett exempel på instrumenteringen i AEM.

Den universella redigeraren strävar efter ett minimum av SDK, och därför är det implementeringen av fjärrappen som ansvarar för instrumenteringen.

### API-lager {#api-layer}

* **Innehållsdata** - För den universella redigeraren är varken källsystemen för innehållsdata eller hur de konsumeras viktiga. Det är bara viktigt att definiera och tillhandahålla de attribut som krävs med kontextredigerbara data.
* **Beständiga data** - För varje redigerbar data finns det en URN-identifierare. Denna URN används för att dirigera beständigheten till rätt system och resurs.

### Beständigt lager {#persistence-layer}

* **Modell för innehållsfragment** - För att stöda fältet för redigering av egenskaper för innehållsfragment, redigeraren för innehållsfragment och formulärbaserade redigerare krävs modeller per komponent och innehållsfragment.
* **Innehåll** - Innehåll kan lagras var som helst, t.ex. i AEM, Magento.

![Persistence-lager](assets/persistence-layer.png)

## Universal Editor Service och Backend System Dispatch {#service}

Universal Editor skickar alla innehållsändringar till en central tjänst som kallas Universal Editor Service. Den här tjänsten, som körs på Adobe I/O Runtime, läser in plugin-program som är tillgängliga i tilläggsregistret baserat på angiven URN. Plugin-programmet ansvarar för att kommunicera med serverdelen och returnera ett enhetligt svar.

![Universell redigeringstjänst](assets/universal-editor-service.png)

## Renderar pipelines {#rendering-pipelines}

### Återgivning på serversidan {#server-side}

![Återgivning på serversidan](assets/server-side.png)

### Skapa statisk plats {#static-generation}

![Statisk webbplatsgenerering](assets/static-generation.png)

### Återgivning på klientsidan {#client-side}

![Återgivning på klientsidan](assets/client-side.png)

---
title: Filtrera komponenter
description: Lär dig hur du kan begränsa vilka komponenter som tillåts per behållare i Universal Editor med hjälp av komponentfilter.
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 48c1a109c060db4ce19bf645723357008d51c572
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 0%

---


# Filtrera komponenter {#filtering-components}

Lär dig hur du kan begränsa vilka komponenter som tillåts per behållare i Universal Editor med hjälp av komponentfilter.

## Filter {#filters}

När du använder Universal Editor kan du begränsa vilka komponenter som tillåts per behållarkomponent. För att göra detta måste du infoga ytterligare en script-tagg som pekar på filterdefinitionen.

```html
<script type="application/vnd.adobe.aue.filter+json" src="/static/filter-definition.json"></script>
```

En filterdefinition kan se ut så här, vilket begränsar en behållare så att bara text och bilder kan läggas till.

```json
[
  {
    "id": "container-filter",
     "components": ["text", "image"]
   }
]
```

Sedan kan du referera till filterdefinitionen från behållarkomponenten genom att lägga till egenskapen `data-aue-filter` och skicka ID:t för filtret som du definierade tidigare.

```html
data-aue-filter="container-filter"
```

Om attributet `components` i en filterdefinition anges till `null` tillåts alla komponenter, som om det inte fanns något filter.

```json
[
  {
    "id": "another-container-filter",
     "components": null
   }
]
```

>[!TIP]
>
>Lär dig mer om andra anpassnings- och tilläggsalternativ som är tillgängliga för den universella redigeraren i dokumentet [Anpassa och utöka den universella redigeraren.](/help/implementing/universal-editor/customizing.md)

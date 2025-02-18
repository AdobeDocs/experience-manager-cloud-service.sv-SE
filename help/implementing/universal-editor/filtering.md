---
title: Filtrera komponenter
description: Lär dig hur du kan begränsa vilka komponenter som tillåts per behållare i Universal Editor med hjälp av komponentfilter.
feature: Developing
role: Admin, Architect, Developer
exl-id: eeae8d7c-c563-4d9b-8c54-1098a4e98c18
source-git-commit: cdad4954b13f5582bebfd604220da90529231ccd
workflow-type: tm+mt
source-wordcount: '153'
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
>Läs mer om andra anpassnings- och tilläggsalternativ som finns för den universella redigeraren i dokumenten:
>
>* [Anpassa den universella redigeraren](/help/implementing/universal-editor/customizing.md)
>* [Utöka den universella redigeraren](/help/implementing/universal-editor/extending.md)

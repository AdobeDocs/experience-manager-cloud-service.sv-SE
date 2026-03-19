---
title: Filter
description: Lär dig hur du kan definiera filter för att begränsa vilka alternativ som är tillgängliga i redigeraren, till exempel tillgängliga komponenter, textredigeringsalternativ och resursval.
feature: Developing
role: Admin, Developer
exl-id: eeae8d7c-c563-4d9b-8c54-1098a4e98c18
source-git-commit: 8d9d162ec5bba99afb1ae86252a49a9880be4e68
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 0%

---


# Filter {#filters}

Lär dig hur du kan definiera filter för att begränsa vilka alternativ som är tillgängliga i redigeraren, till exempel tillgängliga komponenter, textredigeringsalternativ och resursval.

## Konfigurera filter {#configuring-filters}

När du använder den universella redigeraren kan du begränsa vilka alternativ som tillåts för vissa funktioner genom att definiera ett filter. Ett filter är en lista med objekt eller åtgärder som är tillgängliga för det specifika sammanhanget. Du kan till exempel filtrera de komponenter som är tillgängliga för infogning i en behållare, [filtrera de alternativ som är tillgängliga i textredigeraren](/help/implementing/universal-editor/configure-rte.md) och [filtrera de tillgängliga resurserna](/help/implementing/universal-editor/configure-assets-selector.md) i resursväljaren.

Alla filter måste definieras på samma sätt.

1. [Lägg till script-tagg till punkt för filterdefinition](#add-tag)
1. [Definiera filtret](#define-filter)
1. [Referera till filtret](#reference-filter)

Låt oss ta ett exempel på filtrering av komponenter per behållarkomponent.

## Referensfilterdefinition {#add-tag}

Lägg först in ytterligare en script-tagg som pekar på filterdefinitionen.

Om du till exempel vill filtrera tillåtna komponenter per behållare kan taggen se ut ungefär så här.

```html
<script type="application/vnd.adobe.aue.filter+json" src="/static/filter-definition.json"></script>
```

## Definiera filtret {#define-filter}

En filterdefinition innehåller JSON med ett ID som är unikt för filtret och filtervillkoren.

Exempel: för att filtrera tillåtna komponenter per behållare kan det se ut så här, vilket begränsar en behållare så att bara text och bilder kan läggas till.

```json
[
  {
    "id": "container-filter",
    "components": ["text", "image"]
   }
]
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

## Referera till filtret {#reference-filter}

Om du vill använda filtret måste du referera till filterdefinitionen. Du kan göra detta genom att:

* Refererar filtret från behållarkomponenten genom att lägga till egenskapen `data-aue-filter` och skicka filtrets ID.

  ```html
  data-aue-filter="container-filter"
  ```

* Refererar till filtret från din [komponentdefinition,](/help/implementing/universal-editor/component-definition.md) skickar filtrets ID.

  ```json
  {
     "title":"My Container",
     "id":"my-container",
     "model": "my-model",
     "filter": "container-filter",
     ...
  }
  ```

## Ytterligare resurser {#additional-resources}

Läs mer om andra anpassnings- och tilläggsalternativ som finns för den universella redigeraren i dokumenten:

* [Konfigurera RTE för Universal Editor](/help/implementing/universal-editor/configure-rte.md)
* [Konfigurera filter för Assets-väljaren](/help/implementing/universal-editor/configure-assets-selector.md)
* [Anpassa den universella redigeraren](/help/implementing/universal-editor/customizing.md)
* [Utöka den universella redigeraren](/help/implementing/universal-editor/extending.md)

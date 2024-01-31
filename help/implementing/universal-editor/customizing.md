---
title: Anpassa användargränssnittet
description: Lär dig mer om de olika tilläggspunkterna som gör att du kan anpassa gränssnittet i den universella redigeraren efter innehållsförfattarnas behov.
exl-id: 8d6523c8-b266-4341-b301-316d5ec224d7
source-git-commit: 1bc65e65e6ce074a050e21137ce538b5c086665f
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 0%

---


# Anpassa användargränssnittet {#customizing-ui}

Lär dig mer om de olika tilläggspunkterna som gör att du kan anpassa gränssnittet i den universella redigeraren efter innehållsförfattarnas behov.

## Inaktiverar publicering {#disable-publish}

Vissa redigeringsarbetsflöden kräver att innehållet granskas innan det publiceras. I sådana fall bör alternativet att publicera inte vara tillgängligt för någon författare.

The **Publicera** kan därför inaktiveras helt i en app genom att följande metadata läggs till.

```html
<meta name="urn:adobe:aue:config:disable" content="publish"/>
```

## Filtrera komponenter {#filtering-components}

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

Sedan kan du referera till filterdefinitionen från behållarkomponenten genom att lägga till egenskapen `data-aue-filter`, skickar ID:t för filtret som du definierade tidigare.

```html
data-aue-filter="container-filter"
```

Ange `components` attribut i en filterdefinition till `null` tillåter alla komponenter, som om det inte fanns något filter.

```json
[
  {
    "id": "another-container-filter",
     "components": null
   }
]
```

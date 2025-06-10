---
title: Anpassa den universella redigeraren
description: Lär dig mer om de olika alternativen för att anpassa den universella redigeraren så att den passar dina innehållsförfattares behov.
exl-id: 8d6523c8-b266-4341-b301-316d5ec224d7
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 6976f0c9926fb4cb64b0b2d7f8d2daf004c6b936
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 0%

---


# Anpassa den universella redigeraren {#customizing}

Lär dig mer om de olika alternativen för att anpassa den universella redigeraren så att den passar dina innehållsförfattares behov.

>[!TIP]
>
>Den universella redigeraren erbjuder även många [tilläggspunkter](/help/implementing/universal-editor/extending.md) som gör att du kan utöka funktionaliteten efter dina projektbehov.

## Inaktiverar publicering {#disable-publish}

Vissa redigeringsarbetsflöden kräver att innehållet granskas innan det publiceras. I sådana fall bör alternativet att publicera inte vara tillgängligt för någon författare.

Knappen **Publicera** kan därför ignoreras helt i ett program genom att följande metadata läggs till.

```html
<meta name="urn:adobe:aue:config:disable" content="publish"/>
```

## Inaktiverar publicering till förhandsgranskning {#publish-preview}

Vissa redigeringsarbetsflöden kan utesluta publiceringen till [förhandsgranskningstjänsten](/help/sites-cloud/authoring/sites-console/previewing-content.md) (om den är tillgänglig).

Alternativet **Förhandsgranska** i publiceringsfönstret kan därför ignoreras helt i ett program genom att följande metadata läggs till.

```html
<meta name="urn:adobe:aue:config:disable" content="publish-preview"/>
```

## Inaktiverar Öppna sida {#open-page}

Knappen **Öppna sida** kan inaktiveras helt i ett program genom att följande metadata läggs till.

```html
<meta name="urn:adobe:aue:config:disable" content="header-open-page" />
```

## Filtrera komponenter {#filtering-components}

Du kan begränsa vilka komponenter som tillåts per behållare i den universella redigeraren med hjälp av komponentfilter. Mer information finns i dokumentet [Filtrera komponenter](/help/implementing/universal-editor/filtering.md).

## Visa och dölj komponenter villkorligt på egenskapspanelen {#conditionally-hide}

Även om en eller flera komponenter i allmänhet är tillgängliga för författarna, kan det finnas situationer där det inte passar. I så fall kan du dölja komponenter på egenskapspanelen genom att lägga till ett `condition`-attribut i [fälten i komponentmodellen](/help/implementing/universal-editor/field-types.md#fields).

Villkoren kan definieras med [JsonLogic-schema](https://jsonlogic.com/). Om villkoret är true visas fältet. Om villkoret är falskt döljs fältet.

>[!BEGINTABS]

>[!TAB Exempelmodell]

```json
 {
    "id": "conditionally-revealed-component",
    "fields": [
      {
        "component": "boolean",
        "label": "Shall the text field be revealed?",
        "name": "reveal",
        "valueType": "boolean"
      },
      {
        "component": "text-input",
        "label": "Hidden text field",
        "name": "hidden-text",
        "valueType": "string",
        "condition": { "===": [{"var" : "reveal"}, true] }
      }
    ]
 }
```

>[!TAB Villkorsfel]

![Dolt textfält](assets/hidden.png)

>[!TAB Sant villkor]

![Visar textfält](assets/shown.png)

>[!ENDTABS]

## URL för anpassad förhandsvisning {#custom-preview-urls}

Du kan ange en anpassad URL för förhandsgranskning via en `urn:adobe:aue:config:preview`-metakonfiguration, som öppnas när du klickar på knappen **Öppna sida** i [redigerarens övre högra verktygsfält](/help/sites-cloud/authoring/universal-editor/navigation.md#universal-editor-toolbar).

Detta är särskilt användbart för program med särskilda förhandsgranskningskrav, till exempel de [som använder Edge Delivery Services med WYSIWYG ](/help/edge/wysiwyg-authoring/authoring.md).

Det gör du genom att helt enkelt ta med önskad URL för förhandsgranskning i en meta-tagg för det instrumenterade programmet, som i följande exempel.

```html
<meta name="urn:adobe:aue:config:preview" content="https://wknd.site"/>
```

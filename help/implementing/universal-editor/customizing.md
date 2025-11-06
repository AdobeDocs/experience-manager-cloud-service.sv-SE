---
title: Anpassa den universella redigeraren
description: Lär dig mer om de olika alternativen för att anpassa den universella redigeraren så att den passar dina innehållsförfattares behov.
exl-id: 8d6523c8-b266-4341-b301-316d5ec224d7
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---


# Anpassa den universella redigeraren {#customizing}

Lär dig mer om de olika alternativen för att anpassa den universella redigeraren så att den passar dina innehållsförfattares behov.

>[!TIP]
>
>Den universella redigeraren erbjuder även många [tilläggspunkter](/help/implementing/universal-editor/extending.md) som gör att du kan utöka funktionaliteten efter dina projektbehov.

## Använda Meta Config-taggar {#meta-tags}

Vissa redigeringsarbetsflöden kan kräva att vissa funktioner i den universella redigeraren används, inte andra. För att stödja sådana olika fall finns metataggar tillgängliga för att konfigurera eller inaktivera vissa funktioner eller knappar i redigeraren.

Använd den här taggen i avsnittet `<head>` på sidan om du vill inaktivera en eller flera funktioner:

```html
<meta name="urn:adobe:aue:config:disable" content="..." />
```

Om du vill inaktivera flera funktioner anger du en kommaavgränsad lista med värden.

Följande värden stöds för `content`, d.v.s. de funktioner som kan inaktiveras med metataggar.

| Innehållsvärde | Beskrivning |
|---|---|
| `publish` | Inaktivera alla [publicerings](/help/sites-cloud/authoring/universal-editor/publishing.md)-funktioner, dvs. [publiceringsknappen](/help/sites-cloud/authoring/universal-editor/navigation.md#publish) och [avpubliceringsknappen](/help/sites-cloud/authoring/universal-editor/navigation.md#ellipsis) |
| `publish-live` | Inaktivera [publicering](/help/sites-cloud/authoring/universal-editor/publishing.md) live |
| `publish-preview` | Inaktivera förhandsgranskning (om [förhandsgranskningstjänsten](/help/sites-cloud/authoring/sites-console/previewing-content.md) är tillgänglig) |
| `unpublish` | Inaktivera knappen [unpublish](/help/sites-cloud/authoring/universal-editor/publishing.md#unpublishing-content) |
| `copy` | Inaktiverar knapparna [Kopiera och Klistra in](/help/sites-cloud/authoring/universal-editor/authoring.md#copy-paste) |
| `duplicate` | Inaktiverar knappen [Duplicera](/help/sites-cloud/authoring/universal-editor/navigation.md#duplicate) |
| `header-open-page` | Inaktiverar knappen [Öppna sida](/help/sites-cloud/authoring/universal-editor/navigation.md#open-page) |

## Ändra slutpunkten {#custom-endpoint}

Om du inte vill använda den universella redigeringstjänsten, som hanteras av Adobe, men din egen värdversion, kan du ange detta i en metatagg. Mer information finns i dokumentet [Komma igång med den universella redigeraren i AEM](/help/implementing/universal-editor/getting-started.md##configuration-settings).

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

Det gör du genom att helt enkelt ta med önskad URL för förhandsgranskning i en meta-tagg för det instrumenterade programmet, som i följande exempel.

```html
<meta name="urn:adobe:aue:config:preview" content="https://wknd.site"/>
```

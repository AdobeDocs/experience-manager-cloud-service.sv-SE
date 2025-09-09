---
title: Komponentdefinition
description: Förstå JSON-kontraktet mellan komponentdefinitionen och den universella redigeraren i detalj.
feature: Developing
role: Admin, Architect, Developer
exl-id: e1bb1a54-50c0-412a-a8fd-8167c6f47d2b
source-git-commit: b4e61ec6abcaf73119f8963d72317759b2bd7c76
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 0%

---

# Komponentdefinition {#component-definition}

Förstå JSON-kontraktet mellan komponentdefinitionen och den universella redigeraren i detalj.

## Ökning {#overview}

Filen `component-definition.json` definierar de komponenter som är tillgängliga för de som skapar ditt innehåll för projektet. I det här dokumentet förklaras i detalj syftet med filen och hur den används av den universella redigeraren för att ge författarna tillgång till komponenter för sidredigering.

>[!TIP]
>
>En översikt över innehållsmodelleringsprocessen finns i dokumentet [Innehållsmodellering för WYSIWYG-redigering med Edge Delivery Services-projekt.](https://www.aem.live/developer/component-model-definitions)

>[!TIP]
>
>Du behöver inte skapa en egen `component-definition.json`-fil från grunden. Projektmallen som du använder för att [bootstrap ditt projekt](https://www.aem.live/developer/ue-tutorial) innehåller en [fullt fungerande `component-definition.json` fil ](https://github.com/adobe-rnd/aem-boilerplate-xwalk/blob/main/component-definition.json) som du kan anpassa efter dina behov.

## Exempel på komponentdefinition {#example}

Följande är ett fullständigt, men enkelt `component-definition.json` som exempel.

```json
{
  "groups":[
    {
      "title":"General Components",
      "id":"general",
      "components":[
        {
          "title":"Text",
          "id":"text",
          "model": "text",
          "filter": "texts",
          "plugins":{
            "aem":{
              "page":{
                "resourceType":"wknd/components/text",
                "template":{
                  "text":"Default Text",
                  "name":"Text"
                }
              }
            },
            "aem65":{
              "page":{
                "resourceType":"wknd/components/text",
                "template":{
                  "text":"Default Text",
                  "name":"Text"
                }
              }
            }
          }
        }
      ]
    }
  ]
}
```

## `groups` {#groups}

`groups` definierar de grupper av komponenter som författaren ser i den universella redigeraren när han klickar på ikonen **Lägg till** på egenskapspanelen i redigeraren för att [lägga till en ny komponent på en sida](/help/sites-cloud/authoring/universal-editor/authoring.md#adding-components). Med grupper kan du ordna komponenterna. Vanliga grupper kan vara **Allmänna komponenter** och **Avancerade komponenter**.

* `title` definierar den textbeskrivning av gruppen som visas i redigerarens användargränssnitt.
* `id` identifierar gruppen unikt.

## `components` {#components}

`components` definierar vilka komponenter som tillhör en grupp.

* `title` definierar textbeskrivningen för komponenten som visas i användargränssnittet.
* `id` identifierar komponenten unikt.
   * [komponentmodellen](/help/implementing/universal-editor/field-types.md#model-structure) för samma `id` definierar komponentens fält.
   * Eftersom den är unik kan den till exempel användas i en [filterdefinition](/help/implementing/universal-editor/filtering.md) för att avgöra vilka komponenter som kan läggas till i en behållare.
* `model` definierar vilken [modell](/help/implementing/universal-editor/field-types.md#model-structure) som används med komponenten.
   * Modellen underhålls därför centralt i komponentdefinitionen och behöver inte vara [specificerad i instrumenteringen.](/help/implementing/universal-editor/field-types.md#instrumentation)
   * På så sätt kan du flytta komponenter mellan behållare.
* `filter` definierar vilket [filter](/help/implementing/universal-editor/filtering.md) som ska användas med komponenten.

## `plugins` {#plugins}

`plugins` definierar vilket plugin-program som ansvarar för att komponenten behålls. Vanliga plugin-program:

* `aem` för [AEM as a Cloud Service.](https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-service)
* `aem65` för [AEM 6.5.](https://experienceleague.adobe.com/sv/docs/experience-manager-65) och [AEM 6.5 LTS](https://experienceleague.adobe.com/sv/docs/experience-manager-65-lts)
* `xwalk` för [Redigering med AEM Sites för Edge Delivery Services.](https://www.aem.live/developer/ue-tutorial)

## `page` eller `cf` {#page-cf}

När `plugin` har definierats måste du ange om den är sidrelaterad eller fragmentrelaterad.

* `page` anger att komponenten är innehåll på den aktuella sidan.
* `cf` anger att komponenten är relaterad till innehåll i ett [innehållsfragment](/help/assets/content-fragments/content-fragments.md).

### `page` {#page}

Om komponenten är innehåll på sidan kan du ange följande information.

* `resourceType` definierar [Sling](/help/implementing/developing/introduction/sling-cheatsheet.md) `resourceType` som används för återgivning av komponenten.
* `template` definierar valfria nycklar/värden som ska skrivas automatiskt till den nyskapade komponenten och definierar vilket filter och/eller vilken modell som ska användas på komponenten.
   * Användbart för förklarande text, exempeltext eller platshållartext.

#### `template` {#template}

Genom att tillhandahålla valfria nyckel-/värdepar kan `template` automatiskt skriva dessa till den nya komponenten. Dessutom kan följande valfria värden anges.

### `cf` {#cf}

Om komponenten är relaterad till innehåll i ett innehållsfragment kan du ange följande information.

* `name` definierar ett valfritt namn som har sparats i JCR för den nyskapade komponenten.
   * Endast informativ och visas vanligtvis inte i användargränssnittet som `title` är.
* `cfModel` definierar [ Content Fragment ](/help/assets/content-fragments/content-fragments-models.md)-modellen för den nyskapade komponenten.
* `cfFolder` definierar i vilken mapp innehållsfragmentet ska skapas.
* `title` definierar titeln på det nya innehållsfragmentet.
* `description` definierar en beskrivning av det nya innehållsfragmentet.
* `template` definierar valfria nycklar/värden som automatiskt ska skrivas till det nyligen skapade innehållsfragmentet.
   * Användbart för förklarande text, exempeltext eller platshållartext.

### `cf` kan vara underförstådd {#cf-implied}

Om sidan är [instrumenterad](/help/implementing/universal-editor/getting-started.md#instrument-page) för att peka på ett referensfält antas `cf`.

```html
<div data-aue-resource="urn:aem:/content" data-aue-type="container" data-aue-prop="field"></div>
```

I så fall antas `cf` eftersom `data-aue-prop` pekar på ett referensfält. Utan `data-aue-prop` får den universella redigeraren `page` eftersom komponenterna i så fall inte är länkade via ett referensfält.

```html
<div data-aue-resource="urn:aem:/content" data-aue-type="container"></div>
```

Komponenterna är helt enkelt delnoder under resursen.

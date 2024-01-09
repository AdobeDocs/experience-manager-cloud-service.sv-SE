---
title: Fälttyper
description: Lär dig mer om de olika typer av fält som den universella redigeraren kan redigera i komponentfältet med exempel på hur du kan mäta din egen app.
source-git-commit: 44073e27ce7eb35bc0d71cb963c1bd0f14183f00
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 0%

---


# Fälttyper {#field-types}

Lär dig mer om de olika typer av fält som den universella redigeraren kan redigera i komponentfältet med exempel på hur du kan mäta din egen app.

{{universal-editor-status}}

## Ökning {#overview}

När du anpassar dina egna program för användning med den universella redigeraren måste du mäta komponenterna och definiera vilka datatyper som de kan hantera i redigerarens komponentspår.

Det här dokumentet innehåller en översikt över de fälttyper som är tillgängliga för dig tillsammans med exempelkonfigurationer.

>[!TIP]
>
>Om du inte känner till hur du kan mäta din app för den universella redigeraren kan du läsa dokumentet [Universell redigeringsöversikt för AEM.](/help/implementing/universal-editor/developer-overview.md)

## Boolean {#boolean}

Ett booleskt fält lagrar ett enkelt true/false-värde som återges som en kryssruta.

### Exempel {#sample-boolean}

```json
{
  "fields": [   
   {
      "component": "boolean",
      "valueType": "boolean",
      "name": "field1",
      "label": "Boolean Field",
      "description": "This is a boolean field.",
      "required": true,
      "placeholder": null,
      "validation": {
        "customErrorMsg": "This is an error."
      }
    }
  ]
}
```

## Kryssrutegrupp {#checkbox-group}

På samma sätt som för ett booleskt värde kan du använda en kryssrutegrupp för att välja flera sant/falskt-objekt.

### Exempel {#sample-checkbox-group}

```json
{
  "fields": [   
   {
      "component": "checkbox-group",
      "valueType": "string-array",
      "name": "field1",
      "label": "Checkbox Group",
      "description": "This is a checkbox group.",
      "required": true,
      "placeholder": null,
      "options": [
        { "name": "First option", "value": "one" },
        { "name": "Second option", "value": "two" },
        { "name": "Third option", "value": "three" }
      ]
    }
  ]
}
```

## Datum och tid {#date-time}

Ett datum-/tidsfält tillåter att ett datum eller en tid eller en kombination av dessa anges.

### Exempel {#sample-date-time}

```json
{
  "fields": [   
      {
      "component": "date-time",
      "valueType": "date-time",
      "name": "field1",
      "label": "Date Time",
      "description": "This is a date time field that stores both date and time.",
      "required": true,
      "placeholder": "YYYY-MM-DD HH:mm:ss",
      "displayFormat": null,
      "valueFormat": null,
      "validation": {
        "customErrorMsg": "Marty! You have to come back with me!"
      }
    },
    {
      "component": "date-time",
      "valueType": "date",
      "name": "field2",
      "label": "Another Date Time",
      "description": "This is another date time field that only stores the date.",
      "required": true,
      "placeholder": "YYYY-MM-DD",
      "displayFormat": null,
      "valueFormat": null,
      "validation": {
        "customErrorMsg": "Back to the future!"
      }
    },
    {
      "component": "date-time",
      "valueType": "time",
      "name": "field3",
      "label": "Yet Another Date Time",
      "description": "This is another date time field that only stores the time.",
      "required": true,
      "placeholder": "HH:mm:ss",
      "displayFormat": null,
      "valueFormat": null,
      "validation": {
        "customErrorMsg": "Great Scott!"
      }
    }
  ]
}
```

## Nummer {#number}

Ett nummerfält tillåter inmatning av ett tal.

### Exempel {#sample-number}

```json
{
  "fields": [   
   {
      "component": "number",
      "valueType": "number",
      "name": "field1",
      "label": "Number Field",
      "description": "This is a number field.",
      "required": true,
      "placeholder": null,
      "validation": {
        "numberMin": null,
        "numberMax": null,
        "customErrorMsg": "Please don't do that."
      }
    }
  ]
}
```

## Alternativgrupp {#radio-group}

En alternativknappsgrupp tillåter ett ömsesidigt uteslutande urval av flera alternativ som återges som en grupp som liknar en kryssrutegrupp.

### Exempel {#sample-radio-group}

```json
{
  "fields": [   
   {
      "component": "radio-group",
      "valueType": "string",
      "name": "field1",
      "label": "Radio Group",
      "description": "This is a radio group.",
      "required": true,
      "placeholder": null,
      "options": [
        { "name": "Option One", "value": "one" },
        { "name": "Option Two", "value": "two" },
        { "name": "Option Three", "value": "three" }
      ]
    }
  ]
}
```

## Referens {#reference}

En referens tillåter att ett annat dataobjekt specificeras som en referens från det aktuella objektet.

## Välj {#select}

Ett val gör att du kan välja ett eller flera fördefinierade alternativ i en nedrullningsbar meny.

### Exempel {#sample-select}

```json
{
  "fields": [   
   {
      "component": "select",
      "valueType": "string",
      "name": "field1",
      "label": "Select",
      "description": "This is a select.",
      "required": true,
      "placeholder": null,
      "options": [
        { "name": "Option One", "value": "one" },
        { "name": "Option Two", "value": "two" },
        { "name": "Option Three", "value": "three" }
      ],
      "emptyOption": true
    }
  ]
}
```

## Textområde {#text-area}

Ett textområde tillåter textinmatning med flera rader.

### Exempel {#sample-text-area}

```json
{
  "fields": [   
   {
      "component": "text-area",
      "valueType": "string",
      "name": "field1",
      "label": "Text Area",
      "description": "This is a text area.",
      "required": true,
      "multi": true,
      "placeholder": null,
      "mimeType": "text/x-markdown"
    }
  ]
}
```

## Textindata {#text-input}

En textinmatning tillåter en enda rad med textinmatning.

### Exempel {#sample-text-input}

```json
{
  "fields": [   
   {
      "component": "text-input",
      "valueType": "string",
      "name": "field1",
      "label": "Text Input",
      "description": "This is a text input.",
      "required": true,
      "multi": true,
      "placeholder": null
    },
    {
      "component": "text-input",
      "valueType": "string",
      "name": "field2",
      "label": "Another Text Input",
      "description": "This is a text input with validation.",
      "required": true,
      "multi": true,
      "placeholder": null,
      "validation": {
        "minLength": 5,
        "maxLength": 10,
        "regExp": "^foo:.*",
        "customErrorMsg": "I'm sorry, Dave. I can't do that."
      }
    }
  ]
}
```

## Tabb {#tab}

På en flik kan du gruppera andra inmatningsfält på flera flikar för att förbättra layoutordningen för författarna.

A `tab` kan betraktas som en avgränsare i arrayen med `fields`. Allt som kommer efter en `tab` placeras på den fliken tills en ny `tab` påträffas, där följande objekt placeras på den nya fliken.

Om du vill att objekt ska visas ovanför alla flikar måste de definieras före alla tabbar.

### Exempel {#sample-tab}

```json
{
  "id": "title",
  "fields": [
    {
      "component": "tab",
      "label": "Tab",
      "name": "tab1"
    },
    {
      "component": "text-input",
      "name": "tab-response",
      "value": "",
      "placeholder": "Tab? I can't give you a tab unless you order something.",
      "label": "Lou",
      "valueType": "string"
    },
    {
      "component": "tab",
      "label": "Pepsi Free",
      "name": "tab2"
    },
    {
      "component": "text-input",
      "name": "pepsi-free-response",
      "value": "",
      "placeholder": "You want a Pepsi, pal, you're gonna pay for it.",
      "label": "Mr. Carruthers",
      "valueType": "string"
    },
    {
      "component": "select",
      "name": "without-sugar",
      "value": "coffee",
      "label": "Something without sugar",
      "valueType": "string",
      "options": [
        { "name": "Coffee", "value": "coffee" },
        { "name": "Hot Coffee", "value": "hot-coffee" },
        { "name": "Hotter Coffee", "value": "hotter-coffee" }
      ]
    }
  ]
}
```

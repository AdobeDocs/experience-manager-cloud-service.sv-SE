---
title: Universella redigeringshändelser
description: Lär dig mer om de olika händelser som den universella redigeraren skickar och som du kan använda för att reagera på innehåll eller användargränssnittsändringar i din fjärrapp.
source-git-commit: e92a0be2213e3d5793fd077bd1968852336cc98b
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 0%

---


# Universella redigeringshändelser {#events}

Lär dig mer om de olika händelser som den universella redigeraren skickar och som du kan använda för att reagera på innehåll eller användargränssnittsändringar i din fjärrapp.

## Introduktion {#introduction}

Program kan ha olika krav för sid- och komponentuppdateringar. Därför skickar den universella redigeraren definierade händelser till fjärrprogram. Om fjärrprogrammet inte har någon anpassad händelseavlyssnare för den skickade händelsen kan en [händelseavlyssnare för fallback](#fallback-listeners) tillhandahålls av `universal-editor-cors` paketet körs.

Alla händelser anropas på det DOM-element som påverkas på fjärrsidan. Händelser bubblar upp till `BODY` element där standardhändelseavlyssnaren tillhandahålls av `universal-editor-cors` paketet är registrerat. Det finns händelser för innehållet och händelserna för användargränssnittet.

Alla händelser följer en namngivningskonvention.

* `aue:<content-or-ui>-<event-name>`

Till exempel: `aue:content-update` och `aue:ui-select`

Händelser inkluderar nyttolasten för begäran och svaret och aktiveras när motsvarande anrop lyckas. Mer information om samtal och exempel på deras nyttolaster finns i dokumentet [Universella redigeringsanrop.](/help/implementing/universal-editor/calls.md)

## Händelser för innehållsuppdatering {#content-events}

### aue:content-add {#content-add}

The `aue:content-add` -händelsen utlöses när en ny komponent läggs till i en behållare.

Nyttolasten är innehåll från Universal Editor, med reservinnehåll från komponentdefinitionen.

```json
{
    details: {
        request: request payload;   // what is sent to the service
        response: {                 // what is returned by the service
            resource: string;       // newly created content resource
            updates: [{
                resource: string;   // resource to update
                type: string;       // type of instrumentation
                content?: string;   // content to replace
            }]
        }
    }
}
```

### aue:content-details {#content-details}

The `aue:content-details` -händelsen utlöses när en komponent läses in i egenskapsfältet.

Nyttolasten är komponentens innehåll och eventuellt dess schema.

```json
{
    details: {
        content: object             // content object
        model: [object]             // model object
        request: request payload;   // what is sent to the service
        response: response payload; // what is returned by the service
    }
}
```

### aue:content-move {#content-move}

The `aue:content-move` -händelsen utlöses när en komponent flyttas.

Nyttolasten är komponenten, källbehållaren och målbehållaren.

```json
{
    details: {
        from: string;                   // container we move the component from
        component: string;              // component we move
        to: string;                     // container we move the component to
        before: string;                    // before which component shall we place the component
        request: request payload;       // what is sent to the service
        response: response payload;     // what is returned by the service
    }
}
```

### aue:content-patch {#content-patch}

The `aue:content-patch` -händelsen utlöses när en komponents data uppdateras i egenskapsfältet.

Nyttolasten är en JSON-korrigering av de uppdaterade egenskaperna.

```json
{
    details: {
        patch: {
            name: string;               // attribute which is updated
            value: string;              // new value which is stored to the attribute
        },
        request: request payload;       // what is sent to the service
        response: response payload;     // what is returned by the service
    }
}
```

### ljud:content-remove {#content-remove}

The `aue:content-remove` -händelsen utlöses när en komponent tas bort från en behållare.

Nyttolasten är objekt-ID för den borttagna komponenten.

```json
{
    details: {
        resource: string;               // the resource which got removed
        request: request payload;       // what is sent to the service
        response: response payload;     // what is returned by the service
    }
}
```

### aue:content-update {#content-update}

The `aue:content-update` -händelsen utlöses när egenskaperna för en komponent uppdateras i sitt sammanhang.

Nyttolasten är det uppdaterade värdet.

```json
{
    details: {
        value: string;                  // updated value
        request: request payload;       // what is sent to the service
        response: response payload;     // what is returned by the service 
    }
}
```

### Passing Payloads {#passing-payloads}

För alla innehållsuppdateringshändelser skickas den begärda nyttolasten samt svarsnyttolasten till händelsen. Till exempel för ett uppdateringssamtal:

Begär nyttolast:

```json
{
  "connections": [
    {
      "name": "aemconnection",
      "protocol": "aem",
      "uri": "https://author-p7452-e12433.adobeaemcloud.com"
    }
  ],
  "target": {
    "resource": "urn:aemconnection:/content/dam/wknd-shared/en/magazine/arctic-surfing/aloha-spirits-in-northern-norway/jcr:content/data/master",
    "type": "text",
    "prop": "title"
  },
  "value": "Alhoa Spirit Northern Norway!"
}
```

Svarsnyttolast

```json
{
    "updates": [
        {
            "resource": "urn:aemconnection:/content/dam/wknd-shared/en/magazine/arctic-surfing/aloha-spirits-in-northern-norway/jcr:content/data/master",
            "prop": "title",
            "type": "text"
        }
    ]
}
```

## UI-händelser {#ui-events}

### aue:ui-publish {#ui-publish}

The `aue:ui-publish` -händelsen utlöses när innehållet publiceras (med anrop på `BODY` nivå).

Nyttolasten är en lista över artikel-ID:n och deras publiceringsstatus.

### aue:ui-select {#ui-select}

The `aue:ui-select` -händelsen utlöses när en komponent markeras.

Nyttolasten är objekt-ID, objektegenskaper och objekttyp för den valda komponenten.

```json
{
    details: {
        resource: string;       // resource of the selected
        prop: string;           // prop of the selected
        type: string;           // type of the selected
        selected: boolean;      // was selected or unselected
    }
}
```

### aue:ui-preview {#ui-preview}

The `aue:ui-preview` -händelsen aktiveras när sidans redigeringsläge ändras till **Förhandsgranska**.

Nyttolasten är tom för den här händelsen.

```json
{
    details: {}
}
```

### aue:ui-edit {#ui-edit}

The `aue:ui-edit` -händelsen aktiveras när sidans redigeringsläge ändras till **Redigera**.

Nyttolasten är tom för den här händelsen.

```json
{
    details: {}
}
```

### aue:ui-viewport-change {#ui-viewport-change}

The `aue:ui-viewport-change` -händelsen utlöses när visningsrutans storlek ändras.

Nyttolasten är vyportens dimensioner.

```json
{
    details: {
        height: number?;        // height of the viewport. Undefined when fullscreen
        width: number?;         // width of the viewport. Undefined when fullscreen
    }
}
```

### aue:initierad {#initialized}

The `aue:initialized` -händelsen aktiveras för att fjärrsidan ska få veta att den har lästs in i Universell redigerare.

Nyttolasten är tom för den här händelsen.

```json
{
    details: {}
}
```

## Händelseavlyssnare för reserv {#fallback-listeners}

### Innehållsuppdateringar {#content-update-fallbacks}

| Händelse | Beteende |
|---|---|
| `aue:content-add` | Sidinläsning |
| `aue:content-details` | Gör ingenting |
| `aue:content-move` | Flytta komponentens innehåll/struktur till målområdet |
| `aue:content-patch` | Sidinläsning |
| `aue:content-remove` | Ta bort DOM-elementet |
| `aue:content-update` | Uppdatera `innerHTML` med nyttolasten |

### UI-händelser {#ui-event-fallbacks}

| Händelse | Beteende |
|---|---|
| `aue:ui-publish` | Gör ingenting |
| `aue:ui-select` | Bläddra till det markerade elementet |
| `aue:ui-preview` | Lägg till `class="adobe-ue-preview"` till taggen HTML |
| `aue:ui-edit` | Lägg till `class=adobe-ue-edit"` till taggen HTML |
| `aue:ui-viewport-change` | Gör ingenting |
| `aue:initialized` | Gör ingenting |

## Ytterligare resurser {#additional-resources}

* [Universella redigeringsanrop](/help/implementing/universal-editor/calls.md)

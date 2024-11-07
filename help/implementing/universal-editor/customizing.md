---
title: Anpassa och utöka den universella redigeraren
description: Lär dig mer om de olika tilläggspunkterna och andra funktioner som gör att du kan anpassa gränssnittet i den universella redigeraren så att det passar de behov som finns hos de som skapar innehållet.
exl-id: 8d6523c8-b266-4341-b301-316d5ec224d7
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 732b0648e7114594cb8d35df03f83b842d62736e
workflow-type: tm+mt
source-wordcount: '646'
ht-degree: 0%

---


# Anpassa och utöka den universella redigeraren {#customizing-extending}

Lär dig mer om de olika tilläggspunkterna och andra funktioner som gör att du kan anpassa redigeringsmiljön i den universella redigeraren så att den passar de behov som finns hos skribenterna.

## Ökning {#overview}

Med Universell redigerare kan du anpassa två typer av projekt efter dina behov.

* [Anpassa den universella redigeraren](#customizing) - Standardfunktionerna i den universella redigeraren kan anpassas via flera anpassningskonfigurationer.
* [Utöka gränssnittet för den universella redigeraren](#extending) - Gränssnittet i den universella redigeraren kan även utökas med App Builder för att uppfylla dina projektbehov.

Båda typerna beskrivs i följande avsnitt.

## Anpassa den universella redigeraren {#customizing}

Den universella redigeraren har flera inbyggda alternativ för att anpassa funktionaliteten.

### Inaktiverar publicering {#disable-publish}

Vissa redigeringsarbetsflöden kräver att innehållet granskas innan det publiceras. I sådana fall bör alternativet att publicera inte vara tillgängligt för någon författare.

Knappen **Publish** kan därför undertryckas helt i ett program genom att följande metadata läggs till.

```html
<meta name="urn:adobe:aue:config:disable" content="publish"/>
```

### Filtrera komponenter {#filtering-components}

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

### Visa och dölj komponenter villkorligt på egenskapspanelen {#conditionally-hide}

Även om en eller flera komponenter i allmänhet är tillgängliga för författarna, kan det finnas situationer där det inte passar. I så fall kan du dölja komponenter på egenskapspanelen genom att lägga till ett `condition`-attribut i [fälten i komponentmodellen.](/help/implementing/universal-editor/field-types.md#fields)

Villkoren kan definieras med hjälp av [JsonLogic-schema.](https://jsonlogic.com/) Om villkoret är sant visas fältet. Om villkoret är falskt döljs fältet.

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

### URL för anpassad förhandsvisning {#custom-preview-urls}

Du kan ange en anpassad URL för förhandsgranskning via en `urn:adobe:aue:config:preview`-metakonfiguration, som öppnas när du klickar på knappen **Öppna sida** i [redigerarens övre högra verktygsfält.](/help/sites-cloud/authoring/universal-editor/navigation.md#universal-editor-toolbar)

Detta är särskilt användbart för program med särskilda förhandsgranskningskrav, till exempel de [som använder Edge Delivery Services med WYSIWYG-redigering.](/help/edge/wysiwyg-authoring/authoring.md)

Det gör du genom att helt enkelt ta med önskad URL för förhandsgranskning i en meta-tagg för det instrumenterade programmet, som i följande exempel.

```html
<meta name="urn:adobe:aue:config:preview" content="https://wknd.site"/>
```

## Utöka gränssnittet för Universal Editor {#extending}

Som Adobe Experience Cloud-tjänst kan du utöka UI för den universella redigeraren med App Builder och Experience Manager.

Gränssnittstillägg är JavaScript-program som skapats med Adobe App Builder och som kan bäddas in i UI-program som körs med Adobe Experience Cloud enhetliga gränssnitt, till exempel Universal Editor. Du kan lägga till egna knappar och åtgärder på rubrikmenyn och egenskapspanelen samt skapa egna händelser för den universella redigeraren.

Om du vill utforska de här möjligheterna kan du läsa följande resurser:

1. [UI-utökningsbarhet](https://developer.adobe.com/uix/docs/) - Det här är utvecklardokumentationen för UI-tillägg.
1. [Guider för användargränssnittstillägg](https://developer.adobe.com/uix/docs/guides/) - stegvisa instruktioner för hur du utvecklar egna tillägg
1. [Extension Points för Universal Editor](https://developer.adobe.com/uix/docs/services/aem-universal-editor/) - Universell redigeringsspecifik dokumentation för tilläggspunkter

>[!TIP]
>
>Om du föredrar att lära dig som exempel kan du läsa självstudiekursen [AEM UI extensibility.](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/developing/extensibility/ui/overview) Även om den fokuserar på att utöka konsolen för innehållsfragment är begreppen för implementering av ett UI-tillägg i den universella redigeraren desamma.

[Med Extension Manager i AEM Sites](https://developer.adobe.com/uix/docs/extension-manager/) kan du aktivera eller inaktivera tillägg per instans, få åtkomst till tillägg från första Adobe, inklusive tillägg för den universella redigeraren, och mycket annat.

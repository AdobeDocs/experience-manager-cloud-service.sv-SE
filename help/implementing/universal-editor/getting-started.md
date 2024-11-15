---
title: Komma igång med Universal Editor i AEM
description: Lär dig hur du får tillgång till den universella redigeraren och hur du börjar använda den i ditt första AEM.
exl-id: 9091a29e-2deb-4de7-97ea-53ad29c7c44d
feature: Developing
role: Admin, Architect, Developer
source-git-commit: edef86c67becf3b8094196d39baa9e69d6c81777
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 0%

---


# Komma igång med Universal Editor i AEM {#getting-started}

Lär dig hur du får tillgång till den universella redigeraren och hur du börjar använda den i ditt första AEM.

>[!TIP]
>
>Om du hellre vill dyka rakt in i ett exempel kan du granska [Universal Editor-exempelappen på GitHub.](https://github.com/adobe/universal-editor-sample-editable-app)

Även om den universella redigeraren kan redigera innehåll från valfri källa, kommer det här dokumentet att använda ett AEM program som exempel. Det här dokumentet vägleder dig genom de här stegen.

## Instrument för sidan {#instrument-page}

Tjänsten Universal Editor kräver ett [enhetligt resursnamn (URN)](https://en.wikipedia.org/wiki/Uniform_Resource_Name) för att identifiera och använda rätt serverdelssystem för innehållet i appen som redigeras. Därför krävs ett URN-schema för att mappa tillbaka innehåll till innehållsresurser.

### Skapa anslutningar {#connections}

Anslutningar som används i appen lagras som `<meta>` taggar i sidans `<head>`.

```html
<meta name="urn:adobe:aue:<category>:<referenceName>" content="<protocol>:<url>">
```

* `<category>` - Det här är en klassificering av anslutningen med två alternativ.
   * `system` - För anslutningsslutpunkter
   * `config` - För [att definiera valfria konfigurationsinställningar](#configuration-settings)
* `<referenceName>` - Det här är ett kort namn som återanvänds i dokumentet för att identifiera anslutningen. T.ex. `aemconnection`
* `<protocol>` - Detta anger vilket beständighets-plugin-program för den universella redigerarens beständighetstjänst som ska användas. T.ex. `aem`
* `<url>` - Det här är URL:en till systemet där ändringarna ska sparas. T.ex. `http://localhost:4502`

Identifieraren `urn:adobe:aue:system` representerar anslutningen för Adobe Universal Editor.

`data-aue-resource` använder prefixet `urn` för att korta ned identifieraren.

```html
data-aue-resource="urn:<referenceName>:<resource>"
```

* `<referenceName>` - Det här är den namngivna referensen som nämns i `<meta>` -taggen. T.ex. `aemconnection`
* `<resource>` - Detta är en pekare till resursen i målsystemet. Till exempel en AEM innehållssökväg som `/content/page/jcr:content`

>[!TIP]
>
>I dokumentet [Attribut och typer](attributes-types.md) finns mer information om de dataattribut och datatyper som krävs för den universella redigeraren.

### Exempelanslutning {#example}

```html
<meta name="urn:adobe:aue:system:<referenceName>" content="<protocol>:<url>">

<html>
<head>
    <meta name="urn:adobe:aue:system:aemconnection" content="aem:https://localhost:4502">
    <meta name="urn:adobe:aue:system:fcsconnection" content="fcs:https://example.franklin.adobe.com/345fcdd">
</head>
<body>
        <aside>
          <ul data-aue-resource="urn:aemconnection:/content/example/list" data-aue-type="container">
            <li data-aue-resource="urn:aemconnection:/content/example/listitem" data-aue-type="component">
              <p data-aue-prop="name" data-aue-type="text">Jane Doe</p>
              <p data-aue-prop="title" data-aue-type="text">Journalist</p>
              <img data-aue-prop="avatar" src="https://www.adobe.com/content/dam/cc/icons/Adobe_Corporate_Horizontal_Red_HEX.svg" data-aue-type="image" alt="avatar"/>
            </li>

...

            <li data-aue-resource="urn:fcsconnection:/documents/mytext" data-aue-type="component">
              <p data-aue-prop="name" data-aue-type="text">John Smith</p>
              <p data-aue-resource="urn:aemconnection:/content/example/another-source" data-aue-prop="title" data-aue-type="text">Photographer</p>
              <img data-aue-prop="avatar" src="https://www.adobe.com/content/dam/cc/icons/Adobe_Corporate_Horizontal_Red_HEX.svg" data-aue-type="image" alt="avatar"/>
            </li>
          </ul>
        </aside>
</body>
</html>
```

### Konfigurationsinställningar {#configuration-settings}

Du kan använda prefixet `config` i anslutnings-URN för att ange tjänste- och tilläggsslutpunkter om det behövs.

Om du inte vill använda Universal Editor, som hanteras av Adobe, men din egen värdversion, kan du ange detta i en metatagg. Om du vill skriva över standardtjänstslutpunkten som tillhandahålls av Universal Editor anger du en egen tjänstslutpunkt:

* Meta name - `urn:adobe:aue:config:service`
* Metainnehåll - `content="https://adobe.com"` (exempel)

```html
<meta name="urn:adobe:aue:config:service" content="<url>">
```

Om du bara vill aktivera vissa tillägg för en sida kan du ange detta i en metatagg. Om du vill hämta tillägg anger du slutpunkterna för tillägget:

* Metanamn: `urn:adobe:aue:config:extensions`
* Metainnehåll: `content="https://adobe.com,https://anotherone.com,https://onemore.com"` (exempel)

```html
<meta name="urn:adobe:aue:config:extensions" content="<url>,<url>,<url>">
```

## Du är redo att använda den universella redigeraren {#youre-ready}

Din app är nu instrumenterad för att använda den universella redigeraren!

Se [Skapa innehåll med den universella redigeraren](/help/sites-cloud/authoring/universal-editor/authoring.md) för att lära dig hur enkelt och intuitivt det är för innehållsförfattare att skapa innehåll med den universella redigeraren.

## Ytterligare resurser {#additional-resources}

Mer information om Universal Editor finns i de här dokumenten.

* [Introduktion till universell redigering](introduction.md) - Lär dig hur den universella redigeraren kan redigera alla delar av innehåll i alla implementeringar så att du kan leverera enastående upplevelser, öka innehållets hastighet och skapa en toppmodern utvecklarupplevelse.
* [Skapa innehåll med den universella redigeraren](/help/sites-cloud/authoring/universal-editor/authoring.md) - Lär dig hur enkelt och intuitivt det är för innehållsförfattare att skapa innehåll med den universella redigeraren.
* [Publicera innehåll med den universella redigeraren](/help/sites-cloud/authoring/universal-editor/publishing.md) - Lär dig hur den universella redigeraren publicerar innehåll och hur dina appar kan hantera det publicerade innehållet.
* [Universell redigeringsarkitektur](architecture.md) - Lär dig mer om arkitekturen för den universella redigeraren och hur data flödar mellan dess tjänster och lager.
* [Attribut och typer](attributes-types.md) - Lär dig mer om de dataattribut och datatyper som krävs för den universella redigeraren.
* [Autentisering av universell redigerare](authentication.md) - Lär dig hur den universella redigeraren autentiseras.


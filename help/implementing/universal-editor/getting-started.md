---
title: Komma igång med Universal Editor i AEM
description: Lär dig hur du får tillgång till den universella redigeraren och hur du börjar använda den i ditt första AEM.
source-git-commit: acafa752c354781e41b11e46ac31a59feb8d94e7
workflow-type: tm+mt
source-wordcount: '881'
ht-degree: 0%

---


# Komma igång med Universal Editor i AEM {#getting-started}

Lär dig hur du får tillgång till den universella redigeraren och hur du börjar använda den i ditt första AEM.

>[!TIP]
>
>Om du hellre vill dyka rakt in i ett exempel kan du läsa [Universal Editor Sample App på GitHub.](https://github.com/adobe/universal-editor-sample-editable-app)

## Inledande steg {#onboarding}

Även om den universella redigeraren kan redigera innehåll från valfri källa, kommer det här dokumentet att använda ett AEM program som exempel.

Det finns ett antal steg för att komma igång med AEM och instrumentera den så att den kan använda den universella redigeraren.

1. [Begär åtkomst till Universal Editor.](#request-access)
1. [Inkludera grundbiblioteket för Universal Editor.](#core-library)
1. [Lägg till nödvändig OSGi-konfiguration.](#osgi-configurations)
1. [Instrumentera sidan.](#instrument-page)

Det här dokumentet vägleder dig genom dessa steg.

## Begär åtkomst till den universella redigeraren {#request-access}

Du måste först begära åtkomst till Universal Editor. Gå till [https://experience.adobe.com/#/aem/editor](https://experience.adobe.com/#/aem/editor) och validera om du har tillgång till den universella redigeraren.

Om du inte har åtkomst kan du begära det via ett formulär som är länkat på samma sida.

## Include the Universal Editor Core Library {#core-library}

Innan ditt program kan instrumenteras för användning med den universella redigeraren måste det innehålla följande beroenden.

```javascript
@adobe/universal-editor-cors
```

Om du vill aktivera instrumenteringen måste följande import läggas till i `index.js`.

```javascript
import "@adobe/universal-editor-cors";
```

### Alternativ för appar som inte kan reagera {#alternative}

Om du inte implementerar ett React-program och/eller kräver serveråtergivning och alternativ metod är att inkludera följande i dokumentets brödtext.

```html
<script src="https://cdn.jsdelivr.net/gh/adobe/universal-editor-cors/dist/universal-editor-embedded.js" async></script>
```

## Lägg till nödvändiga OSGi-konfigurationer {#osgi-configurations}

För att kunna redigera AEM med din app med Universal Editor måste CORS och cookie-inställningarna göras i AEM.

Följande [OSGi-konfigurationer måste anges för AEM.](/help/implementing/deploying/configuring-osgi.md)

* `SameSite Cookies = None` in `com.day.crx.security.token.impl.impl.TokenAuthenticationHandler`
* Ta bort X-FRAME-OPTIONS: SAMEORIGIN Header in `org.apache.sling.engine.impl.SlingMainServlet`

### com.day.crx.security.token.impl.impl.TokenAuthenticationHandler {#samesite-cookies}

Inloggningstokens cookie måste skickas till AEM som en tredjepartsdomän. Därför måste cookie-filen för samma plats anges explicit till `None`.

Den här egenskapen måste anges i `com.day.crx.security.token.impl.impl.TokenAuthenticationHandler` OSGi-konfiguration.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0"
          xmlns:jcr="http://www.jcp.org/jcr/1.0" jcr:primaryType="sling:OsgiConfig"
          token.samesite.cookie.attr="None" />
```

### org.apache.sling.engine.impl.SlingMainServlet {#sameorigin}

X-frame-options: SAMEORIGIN förhindrar återgivning AEM sidor i en iframe. Om du tar bort sidhuvudet kan sidorna läsas in.

Den här egenskapen måste anges i `org.apache.sling.engine.impl.SlingMainServlet` OSGi-konfiguration.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0"
          xmlns:jcr="http://www.jcp.org/jcr/1.0"
          jcr:primaryType="sling:OsgiConfig"
          sling.additional.response.headers="[X-Content-Type-Options=nosniff]"/>
```

## Instrument för sidan {#instrument-page}

Tjänsten Universal Editor kräver en [enhetligt resursnamn (URN)](https://en.wikipedia.org/wiki/Uniform_Resource_Name) för att identifiera och använda rätt serverdelssystem för innehållet i den app som redigeras. Därför krävs ett URN-schema för att mappa tillbaka innehåll till innehållsresurser.

De instrumentattribut som läggs till på sidan består huvudsakligen av [HTML Microdata,](https://developer.mozilla.org/en-US/docs/Web/HTML/Microdata) en branschstandard som också kan användas för att göra HTML mer semantiskt, göra HTML-dokument indexerbara osv.

### Skapa anslutningar {#connections}

Anslutningar som används i appen lagras som `<meta>` taggar på sidans `<head>`.

```html
<meta name="urn:auecon:<referenceName>" content="<protocol>:<url>">
```

* `<referenceName>` - Det här är ett kort namn som återanvänds i dokumentet för att identifiera anslutningen. T.ex. `aemconnection`
* `<protocol>` - Detta anger vilket beständighets-plugin-program för Universal Editor Persistence Service som ska användas. T.ex. `aem`
* `<url>` - Detta är URL:en till det system där ändringarna ska kvarstå. T.ex. `http://localhost:4502`

Den korta identifieraren `auecon` står för Adobe Universal Editor Connection.

`itemid`s kommer att använda `urn` för att förkorta identifieraren.

```html
itemid="urn:<referenceName>:<resource>"
```

* `<referenceName>` - Detta är den namngivna referens som omnämns i `<meta>` -tagg. T.ex. `aemconnection`
* `<resource>` - Detta är en pekare till resursen i målsystemet. t.ex. en AEM innehållssökväg som `/content/page/jcr:content`

>[!TIP]
>
>Se dokumentet [Attribut och typer](attributes-types.md) om du vill ha mer information om de dataattribut och datatyper som krävs för den universella redigeraren.

### Exempelanslutning {#example}

```html
<html>
<head>
    <meta name="urn:auecon:aemconnection" content="aem:https://localhost:4502">
    <meta name="urn:auecon:fcsconnection" content="fcs:https://example.franklin.adobe.com/345fcdd">
</head>
<body>
        <aside>
          <ul itemscope itemid="urn:aemconnection:/content/example/list" itemtype="container">
            <li itemscope itemid="urn:aemconnection/content/example/listitem" itemtype="component">
              <p itemprop="name" itemtype="text">Jane Doe</p>
              <p itemprop="title" itemtype="text">Journalist</p>
              <img itemprop="avatar" src="https://www.adobe.com/content/dam/cc/icons/Adobe_Corporate_Horizontal_Red_HEX.svg" itemtype="image" alt="avatar"/>
            </li>
 
...
 
            <li itemscope itemid="urn:fcsconnection:/documents/mytext" itemtype="component">
              <p itemprop="name" itemtype="text">John Smith</p>
              <p itemid="urn:aemconnection/content/example/another-source" itemprop="title" itemtype="text">Photographer</p>
              <img itemprop="avatar" src="https://www.adobe.com/content/dam/cc/icons/Adobe_Corporate_Horizontal_Red_HEX.svg" itemtype="image" alt="avatar"/>
            </li>
          </ul>
        </aside>
</body>
</html>
```

### Översättningstjänst för Universal Editor {#translation}

Den universella redigeraren utför översättning baserat på instrumenteringens metadata.

#### Grundläggande översättningsprincip {#principle}

Titta på följande markering från föregående exempel.

```html
<meta name="urn:auecon:aemconnection" content="aem:https://localhost:4502">
<ul itemscope itemid="urn:aemconnection:/content/example/list" itemtype="urn:fcs:type/list">
```

Redigeraren utför ersättningar och internt `itemid` kommer att skrivas om till följande:

```html
itemid="urn:aem:https://localhost:4502/content/example/list"
```

Detta resulterar i termen `aemconnection` ersätts med innehållet i `<meta>` -tagg.

#### Frågeväljare {#query-selector}

Ersättningen resulterar i följande frågesträng för John Smith.

```html
<ul itemscope itemid="urn:aemconnection:/content/example/list" itemtype="urn:fcs:type/list">
  <li itemscope itemid="urn:fcsconnection:/documents/mytext" itemtype="urn:fcs:type/fragment">.  
    <p itemprop="name" itemtype="text">John Smith</p>
    <p itemid="urn:aemconnection/content/example/another-source" itemprop="title" itemtype="text">Photographer</p>
    <img itemprop="avatar" src="urn:fcs:missing" itemtype="image" alt="avatar"/>
  </li>
```

`[itemid="urn:fcs:https://example.franklin.adobe.com/345fcdd/content/example/list][itemprop="name"]`

Om du vill ändra panelen med Sven Svensson är väljaren följande.

`[itemid="urn:aem:https://localhost:4502/content/example/another-source"][itemprop="title"]`

Istället för arv av `itemid`Universal Editor arbetar med omfång och resurser. Ett omfång kan definieras på en nodnivå och ärvas av hela understrukturen.

Om ett annat omfång krävs för en understruktur inom strukturen eller en definierad ledighet, ska en annan `itemid` kan definieras.

## Du är redo att använda den universella redigeraren {#youre-ready}

Din app är nu instrumenterad för att använda den universella redigeraren!

Se dokumentet [Skapa innehåll med den universella redigeraren](authoring.md) om du vill lära dig hur enkelt och intuitivt det är för skribenter att skapa innehåll med den universella redigeraren.

## Ytterligare resurser {#additional-resources}

Mer information om Universal Editor finns i de här dokumenten.

* [Introduktion till Universal Editor](introduction.md) - Lär dig hur den universella redigeraren möjliggör redigering av alla aspekter av innehåll i alla implementeringar för att leverera enastående upplevelser, öka innehållets hastighet och leverera en toppmodern utvecklarupplevelse.
* [Skapa innehåll med den universella redigeraren](authoring.md) - Lär dig hur enkelt och intuitivt det är för skribenter att skapa innehåll med den universella redigeraren.
* [Universal Editor Architecture](architecture.md) - Lär dig mer om arkitekturen i den universella redigeraren och hur data flödar mellan tjänster och lager.
* [Attribut och typer](attributes-types.md) - Läs mer om de dataattribut och datatyper som krävs för den universella redigeraren.
* [Autentisering av universell redigerare](authentication.md) - Lär dig hur den universella redigeraren autentiseras.

---
title: Komma igång med SPA i AEM med React
description: I den här artikeln visas ett exempel SPA programmet, hur det sätts ihop och hur du snabbt kommer igång med ditt eget SPA med React Framework.
exl-id: 13998526-65e7-4d1b-bd47-452bad3780a2
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '1143'
ht-degree: 0%

---

# Komma igång med SPA i AEM med React {#getting-started-with-spas-in-aem-using-react}

Single page applications (SPA) can offer compelling experiences for website users. Utvecklare vill kunna skapa webbplatser med SPA ramverk och författare vill smidigt redigera innehåll i AEM för en webbplats som byggts med SPA ramverk.

SPA innehåller en omfattande lösning för SPA inom AEM. I den här artikeln presenteras en förenklad SPA om React-ramverket, som förklarar hur det sätts ihop så att du snabbt kan komma igång med din egen SPA.

>[!NOTE]
>
>Artikeln bygger på React Framework. Motsvarande dokument för ramverket Angular finns i [Komma igång med SPA i AEM - Angular](getting-started-angular.md).

## Introduktion {#introduction}

I den här artikeln sammanfattas grundläggande funktioner för en enkel SPA och det minimum du behöver känna till för att få igång ditt arbete.

Mer information om hur SPA fungerar i AEM finns i följande dokument:

* [SPA introduktion och genomgång](introduction.md)
* [SPA](editor-overview.md)
* [SPA Blueprint](blueprint.md)

>[!NOTE]
>
>För att kunna skapa innehåll i en SPA måste innehållet lagras i AEM och kunna visas av innehållsmodellen.
>
>En SPA som utvecklats utanför AEM är inte författande om den inte följer innehållsmodellkontraktet.

Det här dokumentet kommer att gå igenom strukturen i en förenklad SPA som skapats med React-ramverket och illustrera hur det fungerar så att du kan tillämpa den här förståelsen på din egen SPA.

## Beroenden, konfiguration och byggnad {#dependencies-configuration-and-building}

Förutom det förväntade React-beroendet kan SPA utnyttja ytterligare bibliotek för att göra det enklare att skapa SPA.

### Beroenden {#dependencies}

Filen `package.json` definierar kraven för det övergripande SPA. Här listas de minsta AEM beroendena för en fungerande SPA.

```
  "dependencies": {
    "@adobe/aem-react-editable-components": "~1.0.4",
    "@adobe/aem-spa-component-mapping": "~1.0.5",
    "@adobe/aem-spa-page-model-manager": "~1.0.3"
  }
```

Eftersom det här exemplet baseras på React-ramverket finns det två React-specifika beroenden som är obligatoriska i `package.json`-filen:

```
 react
 react-dom
```

`aem-clientlib-generator` används för att skapa klientbibliotek automatiskt som en del av byggprocessen.

`"aem-clientlib-generator": "^1.4.1",`

Mer information om den finns [på GitHub här](https://github.com/wcm-io-frontend/aem-clientlib-generator).

`aem-clientlib-generator` är konfigurerat i `clientlib.config.js`-filen enligt följande.

```
module.exports = {
    // default working directory (can be changed per 'cwd' in every asset option)
    context: __dirname,

    // path to the clientlib root folder (output)
    clientLibRoot: "./../content/jcr_root/apps/my-react-app/clientlibs",

    libs: {
        name: "my-react-app",
        allowProxy: true,
        categories: ["my-react-app"],
        embed: ["my-react-app.responsivegrid"],
        jsProcessor: ["min:gcc"],
        serializationFormat: "xml",
        assets: {
            js: [
                "dist/**/*.js"
            ],
            css: [
                "dist/**/*.css"
            ]
        }
    }
};
```

### Byggnad {#building}

Att bygga appen utnyttjar [Webpack](https://webpack.js.org/) för implementering utöver aem-clientlib-generator för att automatiskt skapa klientbibliotek. Därför påminner kommandot build om:

`"build": "webpack && clientlib --verbose"`

När paketet har skapats kan det överföras till en AEM.

### AEM Project Archetype {#aem-project-archetype}

Alla AEM ska utnyttja den AEM projekttypen [som stöder SPA projekt med React eller Angular och använder SPA SDK.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)

## Programstruktur {#application-structure}

Om du tar med beroenden och bygger din app enligt beskrivningen ovan får du ett fungerande SPA som du kan överföra till din AEM.

I nästa avsnitt av det här dokumentet får du information om hur en SPA i AEM är strukturerad, vilka filer som är viktiga för programmet och hur de fungerar tillsammans.

En förenklad bildkomponent används som exempel, men alla komponenter i programmet är baserade på samma koncept.

### index.js {#index-js}

Startpunkten i SPA är förstås den `index.js`-fil som visas här förenklad för att fokusera på det viktiga innehållet.

```
import ReactDOM from 'react-dom';
import App from './App';
import { ModelManager, Constants } from "@adobe/aem-spa-page-model-manager";

...

ModelManager.initialize().then((pageModel) => {
ReactDOM.render(
    <App cqChildren={pageModel[Constants.CHILDREN_PROP]} cqItems={pageModel[Constants.ITEMS_PROP]} cqItemsOrder={pageModel[Constants.ITEMS_ORDER_PROP]} cqPath={ModelManager.rootPath} locationPathname={ window.location.pathname }/>
, document.getElementById('page'));

});
```

Huvudfunktionen i `index.js` är att använda funktionen `ReactDOM.render` för att avgöra var i DOM som programmet ska injiceras.

Det här är en standardanvändning av den här funktionen, som inte är unik för det här exempelprogrammet.

#### Statisk instansiering {#static-instantiation}

När komponenten instansieras statiskt med komponentmallen (t.ex. JSX), måste värdet skickas från modellen till komponentens egenskaper.

### App.js {#app-js}

Genom att återge programmet anropar `index.js` `App.js`, som visas här i en förenklad version för att fokusera på det viktiga innehållet.

```
import {Page, withModel } from '@adobe/aem-react-editable-components';

...

class App extends Page {
...
}

export default withModel(App);
```

`App.js` används främst för att kapsla in rotkomponenterna som appen består av. Startpunkten för alla program är sidan.

### Page.js {#page-js}

Genom att återge sidan anropar `App.js` `Page.js` som listas här i en förenklad version.

```
import {Page, MapTo, withComponentMappingContext } from "@adobe/aem-react-editable-components";

...

class AppPage extends Page {
...
}

MapTo('my-react-app/components/structure/page')(withComponentMappingContext(AppPage));
```

I det här exemplet utökar klassen `AppPage` `Page`, som innehåller de interna innehållsmetoderna som sedan kan användas.

Med `Page` importeras JSON-representationen av sidmodellen och innehållet bearbetas för att kapsla in/dekorera varje element på sidan. Mer information om `Page` finns i dokumentet [SPA Blueprint.](blueprint.md)

### Image.js {#image-js}

När sidan återges kan komponenter som `Image.js` som visas här återges.

```
import React, {Component} from 'react';
import {MapTo} from '@adobe/aem-react-editable-components';

require('./Image.css');

const ImageEditConfig = {

    emptyLabel: 'Image',

    isEmpty: function() {
        return !this.props || !this.props.src || this.props.src.trim().length < 1;
    }
};

class Image extends Component {

    render() {
        return (<img src={this.props.src}>);
    }
}

MapTo('my-react-app/components/content/image')(Image, ImageEditConfig);
```

Det centrala SPA i AEM är att mappa SPA komponenter till AEM och uppdatera komponenten när innehållet ändras (och vice versa). I dokumentet [SPA Editor Overview](editor-overview.md) finns en sammanfattning av den här kommunikationsmodellen.

`MapTo('my-react-app/components/content/image')(Image, ImageEditConfig);`

Metoden `MapTo` mappar SPA till AEM. Det stöder användningen av en enda sträng eller en array med strängar.

`ImageEditConfig` är ett konfigurationsobjekt som bidrar till att aktivera en komponents redigeringsfunktioner genom att tillhandahålla de metadata som behövs för att redigeraren ska kunna generera platshållare

Om det inte finns något innehåll visas etiketter som platshållare för det tomma innehållet.

#### Egenskaper som skickas dynamiskt {#dynamically-passed-properties}

Data som kommer från modellen skickas dynamiskt som egenskaper för komponenten.

## Exporterar redigerbart innehåll {#exporting-editable-content}

Du kan exportera en komponent och göra den redigerbar.

```
import React, { Component } from 'react';
import { MapTo } from '@adobe/aem-react-editable-components';

...

const EditConfig = {...}

class PageClass extends Component {...};

...

export default MapTo('my-react-app/react/components/structure/page')(PageClass, EditConfig);
```

Funktionen `MapTo` returnerar `Component` som är resultatet av en komposition som utökar den angivna `PageClass` med klassnamnen och attributen som aktiverar redigeringen. Den här komponenten kan exporteras för att senare instansieras i koden för programmet.

När den exporteras med funktionerna `MapTo` eller `withModel` kapslas komponenten `Page` in med en `ModelProvider`-komponent som ger standardkomponenter tillgång till den senaste versionen av sidmodellen eller en exakt plats i den sidmodellen.

Mer information finns i [SPAutkast](blueprint.md).

>[!NOTE]
>
>Som standard tar du emot hela komponentmodellen när du använder funktionen `withModel`.

## Dela information mellan SPA {#sharing-information-between-spa-components}

Det är regelbundet nödvändigt att komponenter i ett ensidigt program delar information. Det finns flera rekommenderade sätt att göra detta, som anges nedan i ökande komplexitetsordning.

* **Alternativ 1:** Centralisera logiken och sända till nödvändiga komponenter, till exempel med React Context.
* **Alternativ 2:** Dela komponentlägen med hjälp av ett tillståndsbibliotek som Redux.
* **Alternativ 3:** Utnyttja objekthierarkin genom att anpassa och utöka behållarkomponenten.

## Nästa steg {#next-steps}

* [Getting Started with SPA in AEM using ](getting-started-angular.md) Angularshows how a basic SPA is built to work with the SPA Editor in AEM using Angular.
* [SPA ](editor-overview.md) översiktsredigeraren går in mer på kommunikationsmodellen mellan AEM och SPA.
* [WKND SPA ](wknd-tutorial.md) Projects är en stegvis självstudiekurs som implementerar ett enkelt SPA i AEM.
* [Dynamisk mappning av modell till komponent för ](model-to-component-mapping.md) SPAsexkluderar den dynamiska mappningen av modell till komponent och hur den fungerar i SPA i AEM.
* [SPA ](blueprint.md) Blueprintger en djupdykning i hur SPA SDK for AEM fungerar om du vill implementera SPA i AEM för ett annat ramverk än React eller Angular eller bara vill ha en djupare förståelse.

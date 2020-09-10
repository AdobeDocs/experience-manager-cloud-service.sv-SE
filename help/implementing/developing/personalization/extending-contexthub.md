---
title: Utökar ContextHub
description: Definiera nya typer av ContextHub-butiker och moduler när de angivna lagren inte uppfyller dina lösningskrav
translation-type: tm+mt
source-git-commit: ddfdcf74977adf00bc0ab01b0b1a669781f0d730
workflow-type: tm+mt
source-wordcount: '624'
ht-degree: 0%

---


# Utökar ContextHub {#extending-contexthub}

Definiera nya typer av ContextHub-butiker och moduler när de angivna lagren inte uppfyller dina lösningskrav.

## Skapa anpassade butikskandidater {#creating-custom-store-candidates}

ContextHub-butiker skapas från registrerade butikskandidater. Om du vill skapa en anpassad butik måste du skapa och registrera en butikskandidater.

<!--The javascript file that includes the code that creates and registers the store candidate must be included in a [client library folder](/help/sites-developing/clientlibs.md#creating-client-library-folders). The category of the folder must match the following pattern:-->

Den javascript-fil som innehåller koden som skapar och registrerar lagringskandidaten måste inkluderas i en klientbiblioteksmapp. Mappens kategori måste matcha följande mönster:

```xml
contexthub.store.[storeType]
```

Delen i kategorin är den `storeType` del `storeType` som butikskandidaten registreras med. (Se [Registrera en ContextHub Store-kandidat](#registering-a-contexthub-store-candidate).) För till exempel storeType för `contexthub.mystore`måste kategorin för klientbiblioteksmappen vara `contexthub.store.contexthub.mystore`.

### Skapa en ContextHub Store-kandidat {#creating-a-contexthub-store-candidate}

Om du vill skapa en butikskandidat använder du funktionen för att utöka en av basbutikerna: [`ContextHub.Utils.inheritance.inherit`](contexthub-api.md#inherit-child-parent)

* [`ContextHub.Store.PersistedStore`](contexthub-api.md#contexthub-store-persistedstore)
* [`ContextHub.Store.SessionStore`](contexthub-api.md#contexthub-store-sessionstore)
* [`ContextHub.Store.JSONPStore`](contexthub-api.md#contexthub-store-jsonpstore)
* [`ContextHub.Store.PersistedJSONPStore`](contexthub-api.md#contexthub-store-persistedjsonpstore)

Observera att varje basbutik utökar [`ContextHub.Store.Core`](contexthub-api.md#contexthub-store-core) butiken.

I följande exempel skapas det enklaste tillägget för `ContextHub.Store.PersistedStore` butikskandidaten:

```javascript
myStoreCandidate = function(){};
ContextHub.Utils.inheritance.inherit(myStoreCandidate,ContextHub.Store.PersistedStore);
```

I realiteten definierar dina anpassade butikskandidater ytterligare funktioner eller åsidosätter butikens ursprungliga konfiguration. Flera [exempel på arkivkandidater](sample-stores.md) installeras i databasen nedan `/libs/granite/contexthub/components/stores`.

### Registrerar en ContextHub Store-kandidat {#registering-a-contexthub-store-candidate}

Registrera en butikskandidat för att integrera den med ContextHub-ramverket så att butiker kan skapas utifrån det. Om du vill registrera en butikskandidater använder du [`registerStoreCandidate`](contexthub-api.md#registerstorecandidate-store-storetype-priority-applies) funktionen för `ContextHub.Utils.storeCandidates` klassen.

När du registrerar en butikskandidat anger du ett namn för butikstypen. När du skapar en butik från kandidaten använder du butikstypen för att identifiera den kandidat som den baseras på.

När du registrerar en butikskandidat anger du dess prioritet. När en butikskandidat registreras med samma butikstyp som en redan registrerad butikskandidat, används den som har den högre prioriteten. Därför kan du åsidosätta befintliga butikskandidater med nya implementeringar.

```javascript
ContextHub.Utils.storeCandidates.registerStoreCandidate(myStoreCandidate,
                                'contexthub.mystorecandidate', 0);
```

I de flesta fall behövs bara en kandidat och prioriteten kan anges till `0`, men om du är intresserad kan du lära dig mer om [mer avancerade registreringar,](contexthub-api.md#registerstorecandidate-store-storetype-priority-applies) som gör att en av få butiksimplementationer kan väljas baserat på javascript-villkor (`applies`) och kandidatprioritet.

## Skapar gränssnittsmodultyper för ContextHub {#creating-contexthub-ui-module-types}

Skapa anpassade gränssnittsmodultyper när de som är [installerade med ContextHub](sample-modules.md) inte uppfyller dina krav. Om du vill skapa en gränssnittsmodultyp skapar du en ny gränssnittsmodulrenderare genom att utöka `ContextHub.UI.BaseModuleRenderer` klassen och sedan registrera den med `ContextHub.UI`.

Om du vill skapa en gränssnittsmodulrenderare skapar du ett `Class` objekt som innehåller logiken som återger gränssnittsmodulen. Klassen måste minst utföra följande åtgärder:

* Utöka `ContextHub.UI.BaseModuleRenderer` klassen. Den här klassen är den grundläggande implementeringen för alla UI-modulrenderare. Objektet definierar `Class` en egenskap med namnet `extend` som du använder för att namnge den här klassen som den som utökas.
* Ange en standardkonfiguration. Skapa en `defaultConfig` egenskap. Den här egenskapen är ett objekt som innehåller de egenskaper som har definierats för [`contexthub.base`](sample-modules.md#contexthub-base-ui-module-type) gränssnittsmodulen och alla andra egenskaper som du behöver.

Källan för `ContextHub.UI.BaseModuleRenderer` finns på `/libs/granite/contexthub/code/ui/container/js/ContextHub.UI.BaseModuleRenderer.js`.  Om du vill registrera återgivaren använder du metoden [`registerRenderer`](contexthub-api.md#registerrenderer-moduletype-renderer-dontrender) för `ContextHub.UI` klassen. Du måste ange ett namn för modultypen. När administratörer skapar en gränssnittsmodul som baseras på den här renderaren anger de det här namnet.

Skapa och registrera återgivningsklassen i en anonym funktion som körs automatiskt. Följande exempel baseras på källkoden för `contexthub.browserinfo` gränssnittsmodulen. Den här gränssnittsmodulen är ett enkelt tillägg till `ContextHub.UI.BaseModuleRenderer` klassen.

```javascript
;(function() {

    var SurferinfoRenderer = new Class({
        extend: ContextHub.UI.BaseModuleRenderer,

        defaultConfig: {
            icon: 'coral-Icon--globe',
            title: 'Browser/OS Information',

            storeMapping: {
                surferinfo: 'surferinfo'
            },

            template:
                '<p>{{surferinfo.browser.family}} {{surferinfo.browser.version}}</p>' +
                '<p>{{surferinfo.os.name}} {{surferinfo.os.version}}</p>'
        }
    });

    ContextHub.UI.registerRenderer('contexthub.browserinfo', new SurferinfoRenderer());

}());
```

<!--The javascript file that includes the code that creates and registers the renderer must be included in a [client library folder](/help/sites-developing/clientlibs.md#creating-client-library-folders). The category of the folder must match the following pattern:-->

Den javascript-fil som innehåller koden som skapar och registrerar återgivaren måste inkluderas i en klientbiblioteksmapp. Mappens kategori måste matcha följande mönster:

```javascript
contexthub.module.[moduleType]
```

Delen i kategorin är den `[moduleType]` del `moduleType` som modulåtergivaren registreras med. Till exempel måste kategorin för klientbiblioteksmappen vara `moduleType` av `contexthub.browserinfo`typen `contexthub.module.contexthub.browserinfo`.

---
title: Utökar ContextHub
description: Definiera nya typer av ContextHub-butiker och moduler när de angivna lagren inte uppfyller dina lösningskrav
exl-id: ba817c18-f8bd-485d-b043-87593a6a93b5
feature: Developing, Personalization
role: Admin, Architect, Developer
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 0%

---

# Utökar ContextHub {#extending-contexthub}

Definiera nya typer av ContextHub-butiker och moduler när de angivna inte uppfyller dina lösningskrav.

## Skapa anpassade butikskandidater {#creating-custom-store-candidates}

ContextHub-butiker skapas från registrerade butikskandidater. Om du vill skapa en anpassad butik måste du skapa och registrera en butikskandidater.

Den javascript-fil som innehåller koden som skapar och registrerar arkivkandidaten måste inkluderas i en [klientbiblioteksmapp](/help/implementing/developing/introduction/clientlibs.md). Mappens kategori måste matcha följande mönster:

```xml
contexthub.store.[storeType]
```

Delen `storeType` i kategorin är den `storeType` som butikskandidaten är registrerad med. (Se [Registrera ett ContextHub Store-förslag](#registering-a-contexthub-store-candidate)). För till exempel storeType för `contexthub.mystore` måste kategorin för klientbiblioteksmappen vara `contexthub.store.contexthub.mystore`.

### Skapa en ContextHub Store-kandidat {#creating-a-contexthub-store-candidate}

Om du vill skapa en butikskandidat använder du funktionen [`ContextHub.Utils.inheritance.inherit`](contexthub-api.md#inherit-child-parent) för att utöka en av basbutikerna:

* [`ContextHub.Store.PersistedStore`](contexthub-api.md#contexthub-store-persistedstore)
* [`ContextHub.Store.SessionStore`](contexthub-api.md#contexthub-store-sessionstore)
* [`ContextHub.Store.JSONPStore`](contexthub-api.md#contexthub-store-jsonpstore)
* [`ContextHub.Store.PersistedJSONPStore`](contexthub-api.md#contexthub-store-persistedjsonpstore)

Varje basbutik utökar butiken [`ContextHub.Store.Core`](contexthub-api.md#contexthub-store-core).

I följande exempel skapas det enklaste tillägget för arkivkandidaten `ContextHub.Store.PersistedStore`:

```javascript
myStoreCandidate = function(){};
ContextHub.Utils.inheritance.inherit(myStoreCandidate,ContextHub.Store.PersistedStore);
```

I realiteten definierar dina anpassade butikskandidater ytterligare funktioner eller åsidosätter butikens ursprungliga konfiguration. Flera [exempel på arkivkandidater](sample-stores.md) har installerats i databasen nedan `/libs/granite/contexthub/components/stores`.

### Registrerar en ContextHub Store-kandidat {#registering-a-contexthub-store-candidate}

Registrera en butikskandidat för att integrera den med ContextHub-ramverket så att butiker kan skapas utifrån det. Om du vill registrera en butikskandidater använder du funktionen [`registerStoreCandidate`](contexthub-api.md#registerstorecandidate-store-storetype-priority-applies) i klassen `ContextHub.Utils.storeCandidates`.

När du registrerar en butikskandidat anger du ett namn för butikstypen. När du skapar en butik från kandidaten använder du butikstypen för att identifiera den kandidat som den baseras på.

När du registrerar en butikskandidat anger du dess prioritet. När en butikskandidat registreras med samma butikstyp som en redan registrerad butikskandidat, används den som har den högre prioriteten. Därför kan du åsidosätta befintliga butikskandidater med nya implementeringar.

```javascript
ContextHub.Utils.storeCandidates.registerStoreCandidate(myStoreCandidate,
                                'contexthub.mystorecandidate', 0);
```

I de flesta fall är bara en kandidat nödvändig och prioriteten kan anges till `0`, men om du är intresserad kan du lära dig mer om [mer avancerade registreringar](contexthub-api.md#registerstorecandidate-store-storetype-priority-applies), som gör att en av få butiksimplementeringar kan väljas baserat på javascript-villkor (`applies`) och kandidatprioritet.

## Skapar gränssnittsmodultyper för ContextHub {#creating-contexthub-ui-module-types}

Skapa anpassade gränssnittsmodultyper när de som är [installerade med ContextHub](sample-modules.md) inte uppfyller dina krav. Om du vill skapa en gränssnittsmodultyp skapar du en gränssnittsmodulrenderare genom att utöka klassen `ContextHub.UI.BaseModuleRenderer` och sedan registrera den med `ContextHub.UI`.

Skapa ett `Class`-objekt som innehåller den logik som återger gränssnittsmodulen om du vill skapa en renderare i användargränssnittsmodulen. Klassen måste minst utföra följande åtgärder:

* Utöka klassen `ContextHub.UI.BaseModuleRenderer`. Den här klassen är den grundläggande implementeringen för alla UI-modulrenderare. Objektet `Class` definierar egenskapen `extend` som du använder för att namnge den här klassen som den som utökas.
* Ange en standardkonfiguration. Skapa en `defaultConfig`-egenskap. Den här egenskapen är ett objekt som innehåller de egenskaper som har definierats för användargränssnittsmodulen [`contexthub.base`](sample-modules.md#contexthub-base-ui-module-type) och alla andra egenskaper som du behöver.

Källan för `ContextHub.UI.BaseModuleRenderer` finns på `/libs/granite/contexthub/code/ui/container/js/ContextHub.UI.BaseModuleRenderer.js`.  Om du vill registrera återgivaren använder du metoden [`registerRenderer`](contexthub-api.md#registerrenderer-moduletype-renderer-dontrender) i klassen `ContextHub.UI`. Du måste ange ett namn för modultypen. När administratörer skapar en gränssnittsmodul som baseras på den här renderaren anger de det här namnet.

Skapa och registrera återgivningsklassen i en anonym funktion som körs automatiskt. Följande exempel baseras på källkoden för användargränssnittsmodulen `contexthub.browserinfo`. Den här gränssnittsmodulen är ett enkelt tillägg till klassen `ContextHub.UI.BaseModuleRenderer`.

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

JavaScript-filen som innehåller koden som skapar och registrerar återgivaren måste inkluderas i en [klientbiblioteksmapp](/help/implementing/developing/introduction/clientlibs.md). Mappens kategori måste matcha följande mönster:

```javascript
contexthub.module.[moduleType]
```

Delen `[moduleType]` i kategorin är den `moduleType` som modulåtergivaren är registrerad med. För `moduleType` av `contexthub.browserinfo` måste till exempel kategorin för klientbiblioteksmappen vara `contexthub.module.contexthub.browserinfo`.

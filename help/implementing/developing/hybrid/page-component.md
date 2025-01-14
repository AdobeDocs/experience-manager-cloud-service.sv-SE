---
title: SPA sidkomponent
description: I en SPA tillhandahåller inte sidkomponenten elementen HTML i de underordnade komponenterna, utan delegerar i stället detta till det SPA ramverket. Det här dokumentet förklarar hur det gör sidkomponenten i ett SPA unik.
exl-id: 41b56a60-ebb8-499d-a0ab-a2e920f26227
feature: Developing
role: Admin, Architect, Developer
source-git-commit: e06766160009eaa1bbc41bbf7cfad967a5195e71
workflow-type: tm+mt
source-wordcount: '602'
ht-degree: 0%

---

# SPA sidkomponent {#spa-page-component}

Sidkomponenten för en SPA tillhandahåller inte HTML-elementen för dess underordnade komponenter via en JSP- eller HTL-fil och resursobjekt. Den här åtgärden har delegerats till SPA ramverk. Representationen av underordnade komponenter hämtas som en JSON-datastruktur (d.v.s. modellen). De SPA komponenterna läggs sedan till på sidan enligt den angivna JSON-modellen. Det innebär att sidkomponentens ursprungliga brödkomposition skiljer sig från de förrenderade motsvarigheterna i HTML.

{{ue-over-spa}}

## Sidmodellshantering {#page-model-management}

Sidmodellens upplösning och hantering har delegerats till en angiven [`PageModelManager`](blueprint.md#pagemodelmanager)-modul. SPA måste interagera med modulen `PageModelManager` när den initieras för att hämta den första sidmodellen och registrera sig för modelluppdateringar - oftast när författaren redigerar sidan via sidredigeraren. `PageModelManager` är tillgängligt för SPA som ett nPM-paket. Som tolk mellan AEM och SPA ska `PageModelManager` åtfölja SPA.

Om du vill tillåta att sidan kan redigeras måste ett klientbibliotek med namnet `cq.authoring.pagemodel.messaging` läggas till för att tillhandahålla en kommunikationskanal mellan SPA och sidredigeraren. Om den SPA sidkomponenten ärver från sidans wcm/core-komponent finns det följande alternativ för att göra klientbibliotekskategorin `cq.authoring.pagemodel.messaging` tillgänglig:

* Om mallen är redigerbar lägger du till klientbibliotekskategorin i sidprincipen.
* Lägg till klientbibliotekskategorin med hjälp av sidkomponentens `customfooterlibs.html`.

Glöm inte att begränsa inkludering av kategorin `cq.authoring.pagemodel.messaging` till kontexten för sidredigeraren.

## Kommunikationsdatatyp {#communication-data-type}

Kommunikationsdatatypen anges som ett HTML-element inuti AEM Page-komponenten med attributet `data-cq-datatype`. När kommunikationsdatatypen är JSON, når GET-förfrågningarna en komponents Sling Model-slutpunkter. När en uppdatering har gjorts i sidredigeraren skickas JSON-representationen av den uppdaterade komponenten till sidmodellsbiblioteket. Sidmodellbiblioteket varnar sedan SPA om uppdateringar.

**SPA sidkomponent -`body.html`**

```
<div id="page"></div>
```

Förutom att vara god praxis att inte fördröja DOM-genereringen kräver SPA att skripten läggs till i slutet av brödtexten.

**SPA sidkomponent -`customfooterlibs.html`**

```
<sly data-sly-use.clientLib="${'/libs/granite/sightly/templates/clientlib.html'}"></sly>
<sly data-sly-test="${wcmmode.edit || wcmmode.preview}"
     data-sly-call="${clientLib.js @ categories='cq.authoring.pagemodel.messaging'}"></sly>
<sly data-sly-call="${clientLib.js @ categories='we-retail-journal-react'}"></sly>
```

Meta-resursegenskaperna som beskriver SPA innehåll:

**SPA sidkomponent -`customheaderlibs.html`**

```
<meta property="cq:datatype" data-sly-test="${wcmmode.edit || wcmmode.preview}" content="JSON"/>
<meta property="cq:wcmmode" data-sly-test="${wcmmode.edit}" content="edit"/>
<meta property="cq:wcmmode" data-sly-test="${wcmmode.preview}" content="preview"/>
<meta property="cq:pagemodel_root_url" data-sly-use.page="com.adobe.cq.sample.spa.journal.models.AppPage" content="${page.rootUrl}"/>
<sly data-sly-use.clientlib="/libs/granite/sightly/templates/clientlib.html">
    <sly data-sly-call="${clientlib.css @ categories='we-retail-journal-react'}"/>
</sly>
```

>[!NOTE]
>
>Standardmodellväljaren anges statiskt när Sling Model-representationen av en komponent begärs.

## Metaegenskaper {#meta-properties}

* `cq:wcmmode`: Redigerarnas WCM-läge (till exempel sida, mall)
* `cq:pagemodel_root_url`: URL för appens rotmodell. Viktigt vid direkt åtkomst till en underordnad sida eftersom den underordnade sidmodellen är ett fragment av appens rotmodell. `PageModelManager` komponerar sedan systematiskt om den inledande programmodellen när programmet anges från dess rotstartpunkt.
* `cq:pagemodel_router`: Aktivera eller inaktivera [`ModelRouter`](routing.md) för biblioteket `PageModelManager`
* `cq:pagemodel_route_filters`: Kommaseparerad lista eller reguljära uttryck för att tillhandahålla vägar som [`ModelRouter`](routing.md) måste ignorera.

## Synkronisering av sidredigeringsövertäckning {#page-editor-overlay-synchronization}

Synkroniseringen av övertäckningarna garanteras av exakt samma Mutation Observer som tillhandahålls av kategorin `cq.authoring.page`.

## Sling Model JSON Exported Structure Configuration {#sling-model-json-exported-structure-configuration}

När routningsfunktionerna är aktiverade antas att JSON-exporten av SPA innehåller olika vägar för programmet tack vare JSON-exporten av den AEM navigeringskomponenten. JSON-utdata för den AEM navigeringskomponenten kan konfigureras i innehållsprincipen för SPA genom följande två egenskaper:

* `structureDepth`: Nummer som motsvarar djupet i det exporterade trädet
* `structurePatterns`: Regex för en matris med regex som motsvarar den sida som ska exporteras

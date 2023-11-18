---
title: Anpassa sidredigering
description: Lär dig mer om de mekanismer som AEM as a Cloud Service har för att anpassa sidredigeringsfunktionerna.
exl-id: 98d3c7ab-46d2-4e8d-b0da-5c8a7b398135
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '969'
ht-degree: 0%

---

# Anpassa sidredigering {#customizing-page-authoring}

Adobe Experience Manager as a Cloud Service innehåller mekanismer som gör att du kan anpassa sidredigeringsfunktionerna (och [konsoler](/help/implementing/developing/extending/consoles.md)) i din redigeringsinstans.

## Clientlibs {#clientlibs}

Med Clientlibs kan du utöka standardimplementeringen för att aktivera nya funktioner, samtidigt som du återanvänder standardfunktioner, objekt och standardmetoder.

När du anpassar kan du skapa en egen klientlib under `/apps.` Den nya klientlib måste:

* Beroende på hur klientlib skapas `cq.authoring.editor.sites.page`.
* Bli en del av `cq.authoring.editor.sites.page.hook` kategori.

Se [Använda bibliotek på klientsidan på AEM as a Cloud Service](/help/implementing/developing/introduction/clientlibs.md).

## Övertäckningar {#overlays}

Övertäckningar baseras på noddefinitioner och gör att du kan täcka över standardfunktionerna i `/libs` med egna skräddarsydda funktioner i `/apps`.

När du skapar en övertäckning behövs ingen 1:1-kopia av originalet, eftersom [sammanslagning av säljresurser](/help/implementing/developing/introduction/sling-resource-merger.md) tillåter arv.

Mer information finns i [JS-dokumentationsuppsättning](https://developer.adobe.com/experience-manager/reference-materials/6-5/jsdoc/ui-touch/editor-core/index.html).

Mer information om övertäckningar finns i [Övertäckningar för Adobe Experience Manager as a Cloud Service](/help/implementing/developing/introduction/overlays.md).

## Lägg till nytt lager (läge) {#add-new-layer-mode}

När du redigerar en sida finns det olika [lägen](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes) tillgängliga. Dessa lägen implementeras med [lager](/help/implementing/developing/introduction/ui-structure.md#layer). Dessa ger åtkomst till olika typer av funktioner för samma sidinnehåll. Standardlägen AEM bland annat Redigera, Layout, Utvecklare, Timewarp, Live-kopieringsstatus och Målinriktning.

### Exempel på lager: Live Copy-status {#layer-example-live-copy-status}

En AEM standardinstans innehåller MSM-lagret. Detta ger åtkomst till data relaterade till [hantering av flera webbplatser](/help/sites-cloud/administering/msm/overview.md) och markerar det i lagret.

Om du vill se hur det fungerar kan du redigera en språkkopia i [WKND-exempelinnehåll](/help/implementing/developing/introduction/develop-wknd-tutorial.md) och väljer **Live Copy-status** läge.

MSM-lagerdefinitionen (som referens) finns i:

`/libs/wcm/msm/content/touch-ui/authoring/editor/js/msm.Layer.js`

### Kodexempel {#code-sample}

Detta är ett exempelpaket som visar hur du skapar ett lager (läge) för MSM-vyn.

Koden för den här sidan finns på [GitHub.](https://github.com/Adobe-Marketing-Cloud/aem-authoring-new-layer-mode)

## Lägg till ny markeringskategori i resursläsaren {#add-new-selection-category-to-asset-browser}

Resursläsaren visar resurser av olika typer/kategorier (till exempel bilder och dokument). Resurserna kan också filtreras efter dessa tillgångskategorier.

### Kodexempel {#code-sample-1}

`aem-authoring-extension-assetfinder-flickr` är ett exempelpaket som visar hur du lägger till en grupp i tillgångssökaren. Det här exemplet ansluter till [Flickr](https://www.flickr.com)Det offentliga flödet och visar dem på sidopanelen.

Koden för den här sidan finns på [GitHub.](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-assetfinder-flickr)

## Filtreringsresurser {#filtering-resources}

När användaren redigerar sidor måste han eller hon ofta välja bland resurser i en lista.

För att hålla listan i en rimlig storlek och även relevant för användningsfallet kan ett filter implementeras i form av ett anpassat predikat. Om `pathbrowser` Om du använder en Granite-komponent för att användaren ska kunna välja sökvägen till en viss resurs kan sökvägarna som visas filtreras på följande sätt:

* Implementera det anpassade predikatet genom att implementera [`com.day.cq.commons.predicate.AbstractNodePredicate`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/commons/predicate/package-summary.html) gränssnitt.
* Ange ett namn för predikatet och referera det namnet när du använder `pathbrowser`.

Mer information om hur du skapar ett anpassat predikat finns i [den här artikeln.](/help/implementing/developing/introduction/query-builder-custom-predicate.md)

## Lägg till ny åtgärd i ett komponentverktygsfält {#add-new-action-to-a-component-toolbar}

Varje komponent har vanligtvis ett verktygsfält som ger tillgång till en rad åtgärder som kan vidtas för den komponenten.

### Kodexempel {#code-sample-2}

`aem-authoring-extension-toolbar-screenshot` är ett exempelpaket som visar hur du skapar en anpassad verktygsfältåtgärd för att återge komponenter.

Koden för den här sidan finns på [GitHub.](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-toolbar-screenshot)

## Lägg till ny lokal redigerare {#add-new-in-place-editor}

### Standardredigerare på plats {#standard-in-place-editor}

I en vanlig AEM-installation:

1. `/libs/cq/gui/components/authoring/editors/clientlibs/core/js/editors/editorExample.js` innehåller definitioner av de olika redigeringsprogrammen.

1. Det finns en anslutning mellan redigeraren och varje resurstyp (som i komponenten) som kan använda den:

   * `cq:inplaceEditing`

     till exempel:

      * `/libs/foundation/components/text/cq:editConfig`
      * `/libs/foundation/components/image/cq:editConfig`

         * egenskap: `editorType`

           Definierar den typ av infogad redigerare som används när redigeringen på plats aktiveras för den komponenten, till exempel `text`, `textimage`, `image`, `title`.

1. Ytterligare konfigurationsinformation om redigeraren kan konfigureras med en `config` nod som innehåller konfigurationer och en `plugin` nod som innehåller information om nödvändig plugin-konfiguration.


Följande är ett exempel på hur du definierar bildproportioner för bildbeskärningsplugin-programmet för bildkomponenten.

```xml
   <cq:inplaceEditing
           jcr:primaryType="cq:InplaceEditingConfig"
           active="{Boolean}true"
           editorType="image">
           <config jcr:primaryType="nt:unstructured">
               <plugins jcr:primaryType="nt:unstructured">
                   <crop jcr:primaryType="nt:unstructured">
                       <aspectRatios jcr:primaryType="nt:unstructured">
                           <_x0031_6-10
                               jcr:primaryType="nt:unstructured"
                               name="16 : 10"
                               ratio="0.625"/>
                       </aspectRatios>
                   </crop>
               </plugins>
           </config>
   </cq:inplaceEditing>
```

>[!NOTE]
>
>AEM beskärningsproportioner, enligt inställningen i `ratio` egenskap, definieras som **höjd/bredd**. Detta skiljer sig från den vanliga definitionen av bredd/höjd och görs av bakåtkompatibilitetsskäl. Redigeringsanvändarna kommer inte att vara medvetna om några skillnader förutsatt att du definierar `name` egenskapen tydligt eftersom detta är vad som visas i användargränssnittet.

#### Skapa en ny lokal redigerare {#creating-a-new-in-place-editor}

Så här implementerar du en ny redigerare på plats (i klientlib):

1. Implementera:

   * `setUp`
   * `tearDown`

1. Registrera redigeraren (inkluderar konstruktorn):

   * `editor.register`

1. Ange anslutningen mellan redigeraren och alla resurstyper (som i komponenten) som kan använda den.

#### Kodexempel för att skapa en ny lokal redigerare {#code-sample-for-creating-a-new-in-place-editor}

`aem-authoring-extension-inplace-editor` är ett exempelpaket som visar hur du skapar en redigerare på plats i AEM.

Koden för den här sidan finns på [GitHub.](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-inplace-editor)

## Lägg till en ny sidåtgärd {#add-a-new-page-action}

Lägga till en ny sidåtgärd i verktygsfältet, till exempel en **Tillbaka till platser** (konsol).

### Kodexempel {#code-sample-3}

`aem-authoring-extension-header-backtosites` är ett exempelpaket som visar hur du skapar en anpassad åtgärd i sidhuvudsfältet för att hoppa tillbaka till webbplatskonsolen.

Koden för den här sidan finns på [GitHub.](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-header-backtosites)

## Anpassa arbetsflödet för begäran om aktivering {#customizing-the-request-for-activation-workflow}

färdiga arbetsflöden, **Ansökan om aktivering**:

* Visas automatiskt på rätt meny när en innehållsförfattare **har inte** rätt replikeringsrättigheter, men **har** medlemskap för DAM-användare och författare.

* I annat fall visas ingenting eftersom replikeringsrättigheter har tagits bort.

Om du vill ha ett anpassat beteende för en sådan aktivering kan du täcka över **Ansökan om aktivering** arbetsflöde:

1. I `/apps` överlägg **Webbplatser** guide `/libs/wcm/core/content/common/managepublicationwizard`

   * Detta i sig åsidosätter den vanliga förekomsten av `/libs/cq/gui/content/common/managepublicationwizard`.

1. Uppdatera arbetsflödesmodellen och relaterade konfigurationer/skript efter behov.
1. Ta bort höger till `replicate` åtgärd från alla lämpliga användare för alla relevanta sidor. Om du vill att det här arbetsflödet ska utlösas som en standardåtgärd när någon av användarna gör det, försöker du publicera (eller replikera) en sida.

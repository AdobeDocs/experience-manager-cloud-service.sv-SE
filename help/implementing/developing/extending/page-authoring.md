---
title: Anpassa sidredigering
description: Läs mer om de mekanismer som AEM as a Cloud Service har för att anpassa funktionerna för att skapa sidor.
exl-id: 98d3c7ab-46d2-4e8d-b0da-5c8a7b398135
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '937'
ht-degree: 0%

---

# Anpassa sidredigering {#customizing-page-authoring}

I Adobe Experience Manager as a Cloud Service finns mekanismer som du kan använda för att anpassa sidredigeringsfunktionen (och [konsolerna](/help/implementing/developing/extending/consoles.md)) för din redigeringsinstans.

## Clientlibs {#clientlibs}

Med Clientlibs kan du utöka standardimplementeringen för att aktivera nya funktioner, samtidigt som du återanvänder standardfunktioner, objekt och standardmetoder.

När du anpassar kan du skapa en egen klientlib under `/apps.` Den nya klienten måste:

* Beroende på redigeringsklienten `cq.authoring.editor.sites.page`.
* Bli en del av rätt `cq.authoring.editor.sites.page.hook`-kategori.

Se [Använda bibliotek på klientsidan i AEM as a Cloud Service](/help/implementing/developing/introduction/clientlibs.md).

## Övertäckningar {#overlays}

Övertäckningar är baserade på noddefinitioner och gör att du kan täcka över standardfunktionerna i `/libs` med dina egna anpassade funktioner i `/apps`.

När du skapar en övertäckning krävs ingen 1:1-kopia av originalet, eftersom [sling-resurskonfusion](/help/implementing/developing/introduction/sling-resource-merger.md) tillåter arv.

Mer information finns i [JS-dokumentationsuppsättningen](https://developer.adobe.com/experience-manager/reference-materials/6-5/jsdoc/ui-touch/editor-core/index.html).

Mer information om övertäckningar finns i [Övertäckningar för Adobe Experience Manager as a Cloud Service](/help/implementing/developing/introduction/overlays.md).

## Lägg till nytt lager (läge) {#add-new-layer-mode}

När du redigerar en sida finns det olika [lägen](/help/sites-cloud/authoring/page-editor/introduction.md#page-modes) tillgängliga. Dessa lägen implementeras med [lager](/help/implementing/developing/introduction/ui-structure.md#layer). Dessa ger åtkomst till olika typer av funktioner för samma sidinnehåll. Standardlägen AEM bland annat Redigera, Layout, Utvecklare, Timewarp, Live-kopieringsstatus och Målinriktning.

### Exempel på lager: Live Copy-status {#layer-example-live-copy-status}

En AEM standardinstans innehåller MSM-lagret. Detta ger åtkomst till data relaterade till [hantering av flera webbplatser](/help/sites-cloud/administering/msm/overview.md) och markerar dem i lagret.

Om du vill se hur det fungerar kan du redigera en språkkopia i [WKND-exempelinnehållet](/help/implementing/developing/introduction/develop-wknd-tutorial.md) och välja **Live Copy-status** .

MSM-lagerdefinitionen (som referens) finns i:

`/libs/wcm/msm/content/touch-ui/authoring/editor/js/msm.Layer.js`

### Kodexempel {#code-sample}

Detta är ett exempelpaket som visar hur du skapar ett lager (läge) för MSM-vyn.

Du hittar koden för den här sidan på [GitHub.](https://github.com/Adobe-Marketing-Cloud/aem-authoring-new-layer-mode)

## Lägg till ny markeringskategori i resursläsaren {#add-new-selection-category-to-asset-browser}

Resursläsaren visar resurser av olika typer/kategorier (till exempel bilder och dokument). Resurserna kan också filtreras efter dessa tillgångskategorier.

### Kodexempel {#code-sample-1}

`aem-authoring-extension-assetfinder-flickr` är ett exempelpaket som visar hur du lägger till en grupp i tillgångssökaren. Det här exemplet ansluter till [Flickr](https://www.flickr.com)s allmänna ström och visar dem på sidopanelen.

Du hittar koden för den här sidan på [GitHub.](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-assetfinder-flickr)

## Filtreringsresurser {#filtering-resources}

När användaren redigerar sidor måste han eller hon ofta välja bland resurser i en lista.

För att hålla listan i en rimlig storlek och även relevant för användningsfallet kan ett filter implementeras i form av ett anpassat predikat. Om du till exempel använder komponenten `pathbrowser` Granite för att användaren ska kunna välja sökvägen till en viss resurs, kan sökvägarna som visas filtreras på följande sätt:

* Implementera det anpassade predikatet genom att implementera gränssnittet [`com.day.cq.commons.predicate.AbstractNodePredicate`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/commons/predicate/package-summary.html).
* Ange ett namn för predikatet och referera det namnet när du använder `pathbrowser`.

Mer information om hur du skapar ett anpassat predikat finns i [den här artikeln.](/help/implementing/developing/introduction/query-builder-custom-predicate.md)

## Lägg till ny åtgärd i ett komponentverktygsfält {#add-new-action-to-a-component-toolbar}

Varje komponent har vanligtvis ett verktygsfält som ger tillgång till en rad åtgärder som kan vidtas för den komponenten.

### Kodexempel {#code-sample-2}

`aem-authoring-extension-toolbar-screenshot` är ett exempelpaket som visar hur du skapar en anpassad verktygsfältåtgärd för att återge komponenter.

Du hittar koden för den här sidan på [GitHub.](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-toolbar-screenshot)

## Lägg till ny lokal redigerare {#add-new-in-place-editor}

### Standardredigerare på plats {#standard-in-place-editor}

I en vanlig AEM-installation:

1. `/libs/cq/gui/components/authoring/editors/clientlibs/core/js/editors/editorExample.js` innehåller definitioner av de olika redigerarna.

1. Det finns en anslutning mellan redigeraren och varje resurstyp (som i komponenten) som kan använda den:

   * `cq:inplaceEditing`

     till exempel:

      * `/libs/foundation/components/text/cq:editConfig`
      * `/libs/foundation/components/image/cq:editConfig`

         * egenskap: `editorType`

           Definierar den typ av infogad redigerare som används när redigering på plats aktiveras för den komponenten, till exempel `text`, `textimage`, `image`, `title`.

1. Ytterligare konfigurationsinformation om redigeraren kan konfigureras med en `config`-nod som innehåller konfigurationer och en `plugin`-nod som innehåller nödvändig konfigurationsinformation för plugin-programmet.


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
>AEM beskärningsproportioner, som anges av egenskapen `ratio`, definieras som **height/width**. Detta skiljer sig från den vanliga definitionen av bredd/höjd och görs av bakåtkompatibilitetsskäl. Redigeringsanvändarna kommer inte att vara medvetna om några skillnader förutsatt att du definierar egenskapen `name` tydligt eftersom det är det som visas i gränssnittet.

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

Du hittar koden för den här sidan på [GitHub.](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-inplace-editor)

## Lägg till en ny sidåtgärd {#add-a-new-page-action}

Om du vill lägga till en ny sidåtgärd i sidverktygsfältet, till exempel en **Tillbaka till platser** (konsol)-åtgärd.

### Kodexempel {#code-sample-3}

`aem-authoring-extension-header-backtosites` är ett exempelpaket som visar hur du skapar en anpassad huvudfältåtgärd för att hoppa tillbaka till webbplatskonsolen.

Du hittar koden för den här sidan på [GitHub.](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-header-backtosites)

## Anpassa arbetsflödet för begäran om aktivering {#customizing-the-request-for-activation-workflow}

Det färdiga arbetsflödet, **Begär aktivering**:

* Visas automatiskt på rätt meny när innehållsförfattaren **inte har** rätt replikeringsbehörighet, men **inte har** medlemskap i DAM-användare och författare.

* I annat fall visas ingenting eftersom replikeringsrättigheter har tagits bort.

Om du vill ha ett anpassat beteende för en sådan aktivering kan du täcka över arbetsflödet **Begär aktivering**:

1. I `/apps`-övertäckningen **Platser**-guiden `/libs/wcm/core/content/common/managepublicationwizard`

   * Detta åsidosätter den gemensamma instansen av `/libs/cq/gui/content/common/managepublicationwizard`.

1. Uppdatera arbetsflödesmodellen och relaterade konfigurationer/skript efter behov.
1. Ta bort rättigheten till åtgärden `replicate` från alla lämpliga användare för alla relevanta sidor. Om du vill att det här arbetsflödet ska utlösas som en standardåtgärd när någon av användarna gör det, försöker du publicera (eller replikera) en sida.

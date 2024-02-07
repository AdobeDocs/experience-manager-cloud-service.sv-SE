---
title: Innehållsmodellering för AEM med Edge Delivery Services Projects
description: Lär dig hur innehållsmodellering fungerar AEM redigering med projekt för Edge Delivery Services och hur du modellerar eget innehåll.
source-git-commit: 8f3c7524ae8ee642a9aee5989e03e6584a664eba
workflow-type: tm+mt
source-wordcount: '1940'
ht-degree: 0%

---


# Innehållsmodellering för AEM med Edge Delivery Services Projects {#content-modeling}

Lär dig hur innehållsmodellering fungerar AEM redigering med projekt för Edge Delivery Services och hur du modellerar eget innehåll.

{{aem-authoring-edge-early-access}}

## Förutsättningar {#prerequisites}

Projekt som använder AEM med Edge Delivery Services ärver större delen av mekanismerna i andra Edge Delivery Services, oberoende av innehållskällan eller [redigeringsmetod.](/help/edge/authoring.md)

Innan du börjar modellera innehåll för projektet bör du först läsa följande dokumentation.

* [Komma igång - självstudiekurs för utvecklare](/help/edge/developer/tutorial.md)
* [Markeringar, avsnitt, block och automatisk blockering](/help/edge/developer/markup-sections-blocks.md)
* [Blockera samling](/help/edge/developer/block-collection.md)

Det är viktigt att förstå dessa koncept för att komma fram till en övertygande innehållsmodell som fungerar på ett innehållskällagnostikt sätt. Det här dokumentet innehåller information om de mekanismer som implementerats specifikt för AEM.

## Standardinnehåll {#default-content}

**Standardinnehåll** är innehåll som en författare intuitivt lägger upp på en sida utan att lägga till någon extra semantik. Detta inkluderar text, rubriker, länkar och bilder. Sådant innehåll är självförklarande när det gäller funktion och syfte.

I AEM implementeras det här innehållet som komponenter med mycket enkla, fördefinierade modeller, som innehåller allt som kan serialiseras i Markdown och HTML.

* **Text**: RTF (inklusive listelement och kraftig eller kursiv text)
* **Titel**: Text, typ (h1-h6)
* **Bild**: Källa, beskrivning
* **Knapp**: Text, titel, url, typ (standard, primär, sekundär)

Modellen för dessa komponenter är en del av [Mallen AEM redigering med Edge Delivery Services.](https://github.com/adobe-rnd/aem-boilerplate-xwalk/blob/main/component-models.json#L2-L112)

## Block {#blocks}

Block används för att skapa mer avancerat innehåll med specifika format och funktioner. I motsats till standardinnehåll kräver block ytterligare semantik. Block kan liknas vid [-komponenter i AEM.](/help/implementing/developing/components/overview.md)

Block är huvudsakligen innehållsdelar som dekorerats av JavaScript och formaterats med en formatmall.

### Blockmodellsdefinition {#model-definition}

När du använder AEM redigering med Edge Delivery Services måste innehållet i blocken utformas explicit för att författaren ska kunna använda gränssnittet för att skapa innehåll. Du måste i princip skapa en modell så att författargränssnittet vet vilka alternativ som ska visas för författaren baserat på blocket.

The [`component-models.json`](https://github.com/adobe-rnd/aem-boilerplate-xwalk/blob/main/component-models.json) -filen definierar blockmodellen. De fält som definieras i komponentmodellen bevaras som egenskaper i AEM och återges som celler i tabellen som utgör ett block.

```json
{
  "id": "hero",
  "fields": [
    {
      "component": "reference",
      "valueType": "string",
      "name": "image",
      "label": "Image",
      "multi": false
    },
    {
      "component": "text-input",
      "valueType": "string",
      "name": "imageAlt",
      "label": "Alt",
      "value": ""
    },
    {
      "component": "text-area",
      "name": "text",
      "value": "",
      "label": "Text",
      "valueType": "string"
    }
  ]
}
```

Observera att inte alla block måste ha en modell. Vissa block är bara [behållare](#container) för en lista med underordnade, där varje underordnad har sin egen modell.

Det är också nödvändigt att definiera vilka block som finns och som kan läggas till på en sida med den universella redigeraren. The [`component-definitions.json`](https://github.com/adobe-rnd/aem-boilerplate-xwalk/blob/main/component-definition.json) -filen listar komponenterna när de görs tillgängliga av den universella redigeraren.

```json
{
  "title": "Hero",
  "id": "hero",
  "plugins": {
    "xwalk": {
      "page": {
        "resourceType": "core/franklin/components/block/v1/block",
        "template": {
          "name": "Hero",
          "model": "hero"
        }
      }
    }
  }
}
```

Det går att använda en modell för många block. Vissa block kan till exempel dela en modell som definierar text och bild.

För varje block gäller följande:

* Måste använda `core/franklin/components/block/v1/block` resurstyp, den allmänna implementeringen av blocklogiken i AEM.
* Blocknamnet måste definieras, som ska återges i blockets tabellrubrik.
* Kan definiera en [modell-ID.](/help/implementing/universal-editor/field-types.md#model-structure)
* Kan definiera en [filter-ID.](/help/implementing/universal-editor/customizing.md#filtering-components)

All den här informationen lagras i AEM när ett block läggs till på en sida.

>[!WARNING]
>
>Det är inte nödvändigt att implementera anpassade AEM. Komponenterna för Edge Delivery Services som tillhandahålls av AEM är tillräckliga och erbjuder vissa skyddsräcken för att underlätta utvecklingen.
>
>Därför rekommenderar Adobe inte att du använder anpassade AEM-resurstyper.

### Blockstruktur {#block-structure}

Egenskaperna för blocken är [som definieras i komponentmodellerna](#model-definition) och beständig som sådan i AEM. Egenskaper återges som celler i blockets tabellliknande struktur.

#### Enkla block {#simple}

I den enklaste formen återger ett block varje egenskap i en enda rad/kolumn i den ordning som egenskaperna definieras i modellen.

I följande exempel definieras bilden först i modellen och sedan i textsekunden. De återges alltså med bilden först och sedan med texten sekund.

##### Data {#data-simple}

```json
{
  "name": "Hero",
  "model": "hero",
  "image": "/content/dam/image.png",
  "imageAlt": "Helix - a shape like a corkscrew",
  "text": "<h1>Welcome to AEM</h1>"
}
```

##### Markering {#markup-simple}

```html
<div class="hero">
  <div>
    <div>
      <picture>
        <img src="/content/dam/image.png" alt="Helix - a shape like a corkscrew">
      </picture>
    </div>
  </div>
  <div>
    <div>
      <h1>Welcome to AEM</h1>
    </div>
  </div>
</div>
```

Du kan lägga märke till att vissa typer av värden tillåter semikolonisering i markeringen, och egenskaper kombineras i enskilda celler. Detta beteende beskrivs i avsnittet [Texthärledning.](#type-inference)

#### Nyckelvärdesblock {#key-value}

I många fall rekommenderar vi att du dekorerar den renderade semantiska koden, lägger till CSS-klassnamn, lägger till nya noder eller flyttar dem i DOM och använder format.

I andra fall läses dock blocket som en konfiguration som påminner om nyckelvärdepar.

Ett exempel på detta är [metadata för avsnitt.](/help/edge/developer/markup-sections-blocks.md#sections) I det här fallet kan blocket konfigureras att återges som nyckelvärdepar-tabell. Se avsnittet [Avsnittsmetadata](#sections-metadata) för mer information.

##### Data {#data-key-value}

```json
{
  "name": "Featured Articles",
  "model": "spreadsheet-input",
  "key-value": true,
  "source": "/content/site/articles.json",
  "keywords": ['Developer','Courses'],
  "limit": 4
}
```

##### Markering {#markup-key-value}

```html
<div class="featured-articles">
  <div>
    <div>source</div>
    <div><a href="/content/site/articles.json">/content/site/articles.json</a></div>
  </div>
  <div>
    <div>keywords</div>
    <div>Developer,Courses</div>
  <div>
  <div>
    <div>limit</div>
    <div>4</div>
  </div>
</div>
```

#### Behållarblock {#container}

Båda de tidigare strukturerna har en enda dimension: listan med egenskaper. Behållarblock gör att du kan lägga till underordnade (vanligtvis av samma typ eller modell) och därför är tvådimensionella. Dessa block har fortfarande stöd för sina egna egenskaper som återges som rader med en enda kolumn först. Men de tillåter också att du lägger till underordnade objekt, för vilka varje objekt återges som rad och varje egenskap som kolumn i den raden.

I följande exempel accepterar ett block en lista med länkade ikoner som underordnade, där varje länkad ikon har en bild och en länk. Lägg märke till [filter-ID](/help/implementing/universal-editor/customizing.md#filtering-components) anges i blockets data för att referera till filterkonfigurationen.

##### Data {#data-container}

```json
{
  "name": "Our Partners",
  "model": "text-only",
  "filter": "our-partners",
  "text": "<p>Our community of partners is ...</p>",
  "item_0": {
    "model": "linked-icon",
    "image": "/content/dam/partners/foo.png",
    "imageAlt": "Icon of Foo",
    "link": "https://foo.com/"
  },
  "item_1": {
    "model": "linked-icon"
    "image": "/content/dam/partners/bar.png",
    "imageAlt": "Icon of Bar",
    "link": "https://bar.com"
  }
}
```

##### Markering {#markup-container}

```html
<div class="our-partners">
  <div>
    <div>
        Our community of partners is ...
    </div>
  </div>
  <div>
    <div>
      <picture>
         <img src="/content/dam/partners/foo.png" alt="Icon of Foo">
      </picture>
    </div>
    <div>
      <a href="https://foo.com">https://foo.com</a>
    </div>
  </div>
  <div>
    <div>
      <picture>
         <img src="/content/dam/partners/bar.png" alt="Icon of Bar">
      </picture>
    </div>
    <div>
      <a href="https://bar.com">https://bar.com</a>
    </div>
  </div>
</div>
```

### Skapa semantiska innehållsmodeller för block {#creating-content-models}

Med [Förklaring av blockstrukturens mekanik.](#block-structure) Det går att skapa en innehållsmodell som mappar innehåll som bevaras i AEM en till en till leveransnivån.

Tidigt i varje projekt måste man tänka på en innehållsmodell för varje block. Den måste vara agnostisk mot innehållskällan och redigeringsmiljön för att författare ska kunna växla eller kombinera dem när blockimplementeringar och format återanvänds. Mer information och allmänna riktlinjer finns i [David&#39;s Model (ta 2).](https://www.aem.live/docs/davidsmodel) Mer specifikt finns i [blocksamling](/help/edge/developer/block-collection.md) innehåller en omfattande uppsättning innehållsmodeller för specifika användningsområden för vanliga användargränssnittsmönster.

När AEM skapar med Edge Delivery Services ställer det här en fråga om hur en övertygande semantisk innehållsmodell ska användas när informationen skrivs med formulär som består av flera fält istället för att man redigerar semantiska markeringar i sitt sammanhang som RTF.

För att lösa det här problemet finns det tre metoder som gör det enklare att skapa en övertygande innehållsmodell:

* [Textpåverkan](#type-inference)
* [Dölj fält](#field-collapse)
* [Elementgruppering](#element-grouping)

>[!NOTE]
>
>Blockimplementeringar kan dekonstruera innehållet och ersätta blocket med en DOM som renderas på klientsidan. Även om detta är möjligt och intuitivt för en utvecklare är det inte bästa sättet för Edge Delivery Services.

#### Textpåverkan {#type-inference}

För vissa värden kan den semantiska innebörden härledas från själva värdena. Sådana värden är:

* **Bilder** - Om en referens till en resurs i AEM är en resurs med en MIME-typ som börjar med `image/`återges referensen som `<picture><img src="${reference}"></picture>`.
* **Länkar** - Om det finns en referens i AEM och inte är en bild, eller om värdet börjar med `https?://`  eller `#`återges referensen som `<a href="${reference}">${reference}</a>` .
* **RTF** - Om ett trimmat värde börjar med ett stycke (`p`, `ul`, `ol`, `h1`-`h6`, osv.) återges värdet som RTF.
* **Klassnamn** - `classes` egenskapen behandlas som blockalternativ och återges i tabellrubriken för [enkla block,](#simple) eller som värdelista för objekt i en [behållarblock](#container)
* **Värdelistor** - Om ett värde är en flervärdesegenskap och det första värdet inte är något av föregående, sammanfogas alla värden som kommaavgränsade listor.

Allt annat återges som oformaterad text.

#### Dölj fält {#field-collapse}

Fältkomprimering är den mekanism som används för att kombinera flera fältvärden till ett enda semantiskt element baserat på en namnkonvention med suffix `Title`, `Type`, `Alt`och `Text` (alla skiftlägeskänsliga). Egenskaper som slutar med något av dessa suffix betraktas inte som ett värde, utan som ett attribut för en annan egenskap.

##### Bilder {#image-collapse}

###### Data {#data-image}

```json
{
  "image": "/content/dam/red-car.png",
  "imageAlt: "A red card on a road"
}
```

###### Markering {#markup-image}

```html
<picture>
  <img src="/content/dam/red-car.png" alt="A red car on a road">
</picture>
```

##### Länkar och knappar {#links-buttons-collapse}

###### Data {#data-links-buttons}

```json
{
  "link": "https://www.adobe.com",
  "linkTitle": "Navigate to adobe.com",
  "linkText": "adobe.com",
  "linkType": "primary"
}
```

###### Markering {#markup-links-buttons}

Nej `linkType`, eller `linkType=default`

```html
<a href="https://www.adobe.com" title="Navigate to adobe.com">adobe.com</a>
```

`linkType=primary`

```html
<strong>
  <a href="https://www.adobe.com" title="Navigate to adobe.com">adobe.com</a>
</strong>
```

`linkType=secondary`

```html
<em>
  <a href="https://www.adobe.com" title="Navigate to adobe.com">adobe.com</a>
</em>
```

##### Rubriker {#headings-collapse}

###### Data {#data-headings}

```json
{
  "heading": "Getting started",
  "headingType": "h2"
}
```

###### Markering {#markup-headings}

```html
<h2>Getting started</h2>
```

#### Elementgruppering {#element-grouping}

while [fältkomprimering](#field-collapse) Om du vill kombinera flera egenskaper till ett enda semantiskt element, handlar elementgruppering om att sammanfoga flera semantiska element till en enda cell. Detta är särskilt användbart när det gäller användningsfall där författaren bör begränsas i den typ och det antal element som de kan skapa.

Författaren bör till exempel bara skapa en underrubrik, rubrik och en enda styckebeskrivning kombinerat med högst två knappar för att ringa in. När du grupperar dessa element tillsammans skapas en semantisk kod som kan formateras utan ytterligare åtgärd.

##### Data {#data-grouping}

```json
{
  "name": "teaser",
  "model": "teaser",
  "image": "/content/dam/teaser-background.png",
  "imageAlt": "A group of people sitting on a stage",
  "teaserText_subtitle": "Adobe Experience Cloud"
  "teaserText_title": "Meet the Experts"
  "teaserText_titleType": "h2"
  "teaserText_description": "<p>Join us in this ask me everything session...</p>"
  "teaserText_cta1": "https://link.to/more-details",
  "teaserText_cta1Text": "More Details"
  "teaserText_cta2": "https://link.to/sign-up",
  "teaserText_cta2Text": "RSVP",
  "teaserText_cta2Type": "primary"
}
```

##### Markering {#markup-grouping}

```html
<div class="teaser">
  <div>
    <div>
      <picture>
        <img src="/content/dam/teaser-background.png" alt="A group of people sitting on a stage">
      </picture>
    </div>
  </div>
  <div>
    <div>
      <p>Adobe Experience Cloud</p>
      <h2>Meet the Experts</h2>
      <p>Join us in this ask me everything session ...</p>
      <p><a href="https://link.to/more-details">More Details</a></p>
      <p><strong><a href="https://link.to/sign-up">RSVP</a></strong></p>
    </div>
  </div>
</div>
```

## Avsnittsmetadata {#sections-metadata}

På samma sätt som en utvecklare kan definiera och modellera flera [block,](#blocks) de kan definiera olika avsnitt.

Innehållsmodellen för Edge Delivery Services tillåter avsiktligt bara en enda kapslingsnivå, vilket är vilket standardinnehåll eller -block som finns i ett avsnitt. Detta innebär att om du vill ha mer komplexa visuella komponenter som kan innehålla andra komponenter måste de modelleras som sektioner och kombineras med hjälp av en autoblockerande klientsida. Typiska exempel på detta är tabbar och komprimerbara avsnitt som dragspelspaneler.

Ett avsnitt kan definieras på samma sätt som ett block, men med resurstypen för `core/franklin/components/section/v1/section`. Avsnitt kan ha ett namn och en [filter-ID,](/help/implementing/universal-editor/customizing.md#filtering-components) som används av [Universal Editor](/help/implementing/universal-editor/introduction.md) bara, samt [modell-ID,](/help/implementing/universal-editor/field-types.md#model-structure) som används för att återge avsnittets metadata. Modellen är på det här sättet modellen för avsnittets metadatablocket, som automatiskt läggs till i ett avsnitt som nyckelvärdesblock om det inte är tomt.

The [modell-ID](/help/implementing/universal-editor/field-types.md#model-structure) och [filter-ID](/help/implementing/universal-editor/customizing.md#filtering-components) standardavsnittet är `section`. Den kan användas för att ändra standardavsnittets beteende. I följande exempel läggs vissa format och en bakgrundsbild till i avsnittets metadatamodell.

```json
{
  "id": "section",
  "fields": [
    {
      "component": "multiselect",
      "name": "style",
      "value": "",
      "label": "Style",
      "valueType": "string",
      "options": [
        {
          "name": "Fade in Background",
          "value": "fade-in"
        },
        {
          "name": "Highlight",
          "value": "highlight"
        }
      ]
    },
    {
      "component": "reference",
      "valueType": "string",
      "name": "background",
      "label": "Image",
      "multi": false
    }
  ]
}
```

I följande exempel definieras ett tabbavsnitt, som kan användas för att skapa ett tabbblock genom att kombinera efterföljande avsnitt med ett tabbrubriksdataattribut till ett tabbblock under automatisk blockering.

```json
{
  "title": "Tab",
  "id": "tab",
  "plugins": {
    "xwalk": {
      "page": {
        "resourceType": "core/franklin/components/section/v1/section",
        "template": {
          "name": "Tab",
          "model": "tab",
          "filter": "section"
        }
      }
    }
  }
}
```

## Sidmetadata {#page-metadata}

Dokument kan ha en sida [metadatablockering,](/help/edge/authoring.md#metadata--seo) som används för att definiera vilka `<meta>` element återges i `<head>` på en sida. Sidegenskaperna för sidor i AEM as a Cloud Service mappas till de som är tillgängliga direkt för Edge Delivery Services, som `title`, `description`, `keywords`, osv.

Innan du kan utforska hur du definierar egna metadata bör du läsa följande dokument för att först förstå begreppet sidmetadata.

* [Metadata](https://www.aem.live/developer/block-collection/metadata)
* [Massmetadata](/help/edge/docs/bulk-metadata.md)

Det går också att definiera ytterligare sidmetadata på två sätt.

### Kalkylblad för metadata {#metadata-spreadsheets}

Det går att definiera metadata per bana eller per bana på ett tabellliknande sätt AEM as a Cloud Service. Det finns ett redigeringsgränssnitt för tabellliknande data som liknar Excel- och Google-ark.

Om du vill skapa en sådan tabell skapar du en sida och använder metadatamallen i webbplatskonsolen.

>[!NOTE]
>
>När du redigerar metadatakalkylbladet ska du se till att växla till **Förhandsgranska** eftersom redigeringen görs på själva sidan, inte i redigeraren.

I kalkylbladets sidegenskaper definierar du de metadatafält som du behöver tillsammans med URL:en. Lägg sedan till metadata per sidsökväg eller sidsökvägsmönster, där URL-fältet relaterar till mappade, offentliga sökvägar och inte innehållssökvägen i AEM.

Kontrollera att kalkylbladet läggs till i sökvägsmappningen innan du publicerar det.

```text
mappings:
  - /content/site/:/
  - /content/site/metadata:/metadata.json
```

### Sidegenskaper {#page-properties}

Du kan också definiera en komponentmodell för sidmetadata, som kommer att vara tillgänglig för författaren som en flik i dialogrutan AEM Sites sidegenskaper.

Om du vill göra det skapar du en komponentmodell med ID:t `page-metadata`.

```json
{
  "id": "page-metadata",
  "fields": [
    {
      "component": "text-input",
      "name": "theme",
      "label": "Theme"
    }
  ]
}
```

Det finns ett fåtal fältnamn som har en speciell betydelse och som kommer att hoppas över när redigeringsgränssnittet visas:

* **`cq:tags`** - Som standard `cq:tags` läggs inte till i metadata. Lägga till dem i `page-metadata` modellen lägger till tagg-ID:n som en kommaseparerad lista som en `tags` meta-tagg till huvudet.
* **`cq:lastModified`** - `cq:lastModified` lägger till data som `last-modified` till huvudet.

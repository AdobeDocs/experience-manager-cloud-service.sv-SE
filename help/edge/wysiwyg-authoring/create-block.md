---
title: Skapa block som är instrumenterade för användning med den universella redigeraren
description: Lär dig hur du skapar block som är instrumenterade för användning med den universella redigeraren i WYSIWYG-redigering med Edge Delivery Services.
exl-id: 65a5600a-8d16-4943-b3cd-fe2eee1b4abf
feature: Edge Delivery Services
role: Admin, Architect, Developer
source-git-commit: 364acc6a76261a725a46fe3e1ef173bc03b5a289
workflow-type: tm+mt
source-wordcount: '1401'
ht-degree: 0%

---


# Skapa block som är instrumenterade för användning med den universella redigeraren {#create-block}

Lär dig hur du skapar block som är instrumenterade för användning med den universella redigeraren i WYSIWYG-redigering med Edge Delivery Services.

## Förutsättningar {#prerequisites}

Den här guiden innehåller stegvisa instruktioner för hur du skapar block som är instrumenterade för den universella redigeraren i WYSIWYG-redigering med Edge Delivery Services-projekt. Det handlar om att lägga till komponenter, läsa in komponentdefinitioner i den universella redigeraren, publicera sidor, implementera blockdekoration och format, göra ändringar i produktionen och verifiera dem. När du är klar med den här guiden kan du skapa och distribuera ett nytt block för ditt eget projekt.

Den här guiden kräver kunskaper om WYSIWYG-redigering med Edge Delivery Services och den universella redigeraren. Innan du börjar den här guiden bör du ha tillgång till Edge Delivery Services och känna till grunderna i den:

* Du har slutfört [Självstudiekurs om Edge Delivery Service.](/help/edge/developer/tutorial.md)
* Du har tillgång till en [AEM Cloud Service sandlåda.](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md)
* Du har [har aktiverat den universella redigeraren i samma sandlådemiljö.](/help/implementing/universal-editor/getting-started.md)
* Du har slutfört [Utvecklarhandbok för att komma igång med WYSIWYG-redigering med Edge Delivery Services](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md) guide.

Den här guiden bygger vidare på det arbete som gjorts i [Utvecklarhandbok för att komma igång med WYSIWYG-redigering med Edge Delivery Services](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md) guide.

## Lägga till ett nytt block i projektet {#add-block}

I den här guiden skapar du ett block som återger ett minnesvärt citat på sidan.

För att förenkla det här exemplet görs alla ändringar i `main` gren av projektdatabasen. Självklart för ditt projekt, [du bör följa bästa praxis för utveckling](https://www.aem.live/docs/dev-collab-and-good-practices) genom att utveckla på en annan gren och granska alla ändringar via pull-begäran innan de sammanfogas med `main`.

Adobe rekommenderar att du utvecklar block i tre faser:

1. Skapa definitionen och modellen för blocket, granska det och ta det till produktion.
1. Skapa innehåll med det nya blocket.
1. Implementera dekoration och stilar för det nya blocket.

Följande exempel på offertblock följer den här metoden.

### Skapa blockdefinition och modell {#create-block-model}

1&amp;period; klona GitHub-projektet lokalt som du skapade i [Utvecklarhandbok för att komma igång med WYSIWYG-redigering med Edge Delivery Services](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md) och öppna den i valfri redigerare.

* Microsoft Code används här för illustrativa ändamål.

![Klona projektet](assets/create-block/clone.png)

2&amp;punkt; Redigera `component-definition.json` filen i projektets rot och lägg till följande definition för det nya offertblocket och spara filen.

>[!BEGINTABS]

>[!TAB JSON-exempel]

```json
{
  "title": "Quote",
  "id": "quote",
  "plugins": {
    "xwalk": {
      "page": {
        "resourceType": "core/franklin/components/block/v1/block",
        "template": {
          "name": "Quote",
          "model": "quote",
          "quote": "<p>Think, McFly! Think!</p>",
          "author": "Biff Tannen"
        }
      }
    }
  }
}
```

>[!TAB Skärmbild]

![Redigera filen component-definitions.json för att definiera offertblocket](assets/create-block/component-definitions.png)

>[!ENDTABS]

3&amp;punkt; Redigera `component-models.json` filen i projektets rot och lägg till följande [modelldefinition](/help/implementing/universal-editor/field-types.md#model-structure) för det nya offertblocket och spara filen.

* Se dokumentet [Innehållsmodellering för WYSIWYG-redigering med Edge Delivery Services Projects](/help/edge/wysiwyg-authoring/content-modeling.md) för mer information om vad som är viktigt att tänka på när du skapar innehållsmodeller.

>[!BEGINTABS]

>[!TAB JSON-exempel]

```json
{
  "id": "quote",
  "fields": [
     {
       "component": "text-area",
       "name": "quote",
       "value": "",
       "label": "Quote",
       "valueType": "string"
     },
     {
       "component": "text-input",
       "valueType": "string",
       "name": "author",
       "label": "Author",
       "value": ""
     }
   ]
}
```

>[!TAB Skärmbild]

![Redigera filen component-models.json för att definiera modellen för offertblocket](assets/create-block/component-models.png)

>[!ENDTABS]

4&amp;punkt; Redigera `component-filters.json` filen i projektets rot och lägg till offertblocket i [filterdefinition](/help/implementing/universal-editor/customizing.md#filtering-components) så att blocket kan läggas till i valfritt avsnitt och spara filen.

>[!BEGINTABS]

>[!TAB JSON-exempel]

```json
{
  "id": "section",
  "components": [
    "text",
    "image",
    "button",
    "title",
    "hero",
    "cards",
    "columns",
    "quote"
   ]
}
```

>[!TAB Skärmbild]

![Redigera filen component-filters.json för att definiera filter för offertblocket](assets/create-block/component-filters.png)

>[!ENDTABS]

5&amp;period; med Git implementerar du dessa ändringar i `main` gren.

* Bekräftar till `main` är endast till för illustrativa ändamål. [Följ vedertagna standarder](https://www.aem.live/docs/dev-collab-and-good-practices) och använda en pull-begäran för faktiskt projektarbete.

### Skapa innehåll med blocket {#create-content}

Nu när det grundläggande offertblocket är definierat och implementerat i exempelprojektet kan du lägga till ett offertblock på en befintlig sida.

1. Logga in AEM as a Cloud Service i en webbläsare. [Med Sites-konsolen](/help/sites-cloud/authoring/basic-handling.md) navigera till webbplatsen som du skapade i [Utvecklarhandbok för att komma igång med WYSIWYG-redigering med Edge Delivery Services](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md) och markera en sida.

   * I detta fall `index` används för illustrativa ändamål.

   ![Välja indexsida i webbplatskonsolen](assets/create-block/sites-console.png)

1. Tryck eller klicka **Redigera** i konsolens verktygsfält och Universal Editor öppnas.

   * Om du vill läsa in sidan kan du behöva trycka eller klicka **Logga in med Adobe** för att autentisera till AEM i Universal Editor.

1. Markera ett avsnitt i Universella redigeringsprogram. Tryck eller klicka på **Lägg till** ikonen och välj sedan din nya **Citat** på menyn.

   * The **Lägg till** är en plustecken.
   * Du vet att du har markerat ett avsnitt om den blå konturen för det markerade objektet har en tabb med etiketten **Avsnitt**.
   * I det här exemplet trycker eller klickar du något ovanför **Lorem Ipsum** heading markerar ett avsnitt som innehåller rubriken och lorem ipsum text.

   ![Markera ett avsnitt i den universella redigeraren](assets/create-block/add-quote-block.png)

1. Sidan läses in igen och offertblocket läggs till längst ned i det markerade avsnittet med standardinnehållet som anges i `component-definitions.json` -fil.

   * Citatteckenblocket kan markeras och redigeras som vilket annat block som helst, antingen på plats eller i egenskapsfältet.
   * Formateringen görs i ett steg till.

   ![Sidan med det nya offertblocket i det markerade avsnittet](assets/create-block/quote-added.png)

1. När du är nöjd med offertens innehåll kan du publicera sidan genom att trycka på eller klicka på **Publicera** i verktygsfältet i Universal Editor.

1. Kontrollera att innehållet har publicerats genom att gå till den publicerade sidan. Länken påminner om `https://<branch>--<repo>--<owner>.hlx.page`

   ![Den publicerade offerten](assets/create-block/quote-published.png)

### Formatera blocket {#style-block}

Nu när du har ett fungerande offertblock kan du formatera det.

1&amp;period; återgå till redigeraren för ditt projekt.

2&amp;period; Skapa en `quote` mappen under `blocks` mapp.

![Skapa en offertmapp](assets/create-block/new-folder.png)

3&amp;punkt; I ny `quote` mapp, lägga till `quote.js` -fil som ska implementera blockdekoration genom att lägga till följande JavaScript och spara filen.

>[!BEGINTABS]

>[!TAB JavaScript-exempel]

```javascript
export default function decorate(block) {
  const [quoteWrapper] = block.children;
 
  const blockquote = document.createElement('blockquote');
  blockquote.textContent = quoteWrapper.textContent.trim();
  quoteWrapper.replaceChildren(blockquote);
}
```

>[!TAB Skärmbild]

![Lägga till JavaScript för att dekorera blocket](assets/create-block/quote-js.png)

>[!ENDTABS]

4&amp;punkt; i `quote` mapp, lägga till `quote.css` -fil för att definiera blockets format genom att lägga till följande CSS-kod och spara filen.

>[!BEGINTABS]

>[!TAB CSS-exempel]

```css
.block.quote {
    background-color: #ccc;
    padding: 0 0 24px;
    display: flex;
    flex-direction: column;
    margin: 1rem 0;
}
 
.block.quote blockquote {
    margin: 16px;
    text-indent: 0;
}
 
.block.quote > div:last-child > div {
    margin: 0 16px;
    font-size: small;
    font-style: italic;
    position: relative;
}
 
.block.quote > div:last-child > div::after {
    content: "";
    display: block;
    position: absolute;
    left: 0;
    bottom: -8px;
    height: 5px;
    width: 30px;
    background-color: darkgray;
}
```

>[!TAB Skärmbild]

![Lägga till CSS för att definiera blockformateringen](assets/create-block/quote-css.png)

>[!ENDTABS]

5&amp;period; med Git implementerar du dessa ändringar i `main` gren.

* Bekräftar till `main` är endast till för illustrativa ändamål. [Följ vedertagna standarder](https://www.aem.live/docs/dev-collab-and-good-practices) och använda en pull-begäran för faktiskt projektarbete.

6&amp;period; återgå till webbläsarfliken i Universal Editor där du redigerade sidan i ditt projekt och läsa in sidan igen för att visa det formaterade blocket.

7&amp;punkt; se det nu formaterade citattecknet på sidan.

![Det formaterade citattecknet i Universell redigerare](assets/create-block/quote-styled.png)

8&amp;period; Verifiera att ändringarna flyttades till produktion genom att navigera till den publicerade sidan. Länken påminner om `https://<branch>--<repo>--<owner>.hlx.page`

![Det publicerade och formaterade citatteckenblocket](assets/create-block/quote-styled-published.png)

Grattis! Du har nu ett fullt fungerande och formaterat citattecken. Du kan använda det här exemplet som bas för att utforma egna projektspecifika block.

### Blockalternativ {#block-options}

Om du behöver ett block som ska se ut eller bete dig lite annorlunda beroende på vissa omständigheter, men inte tillräckligt annorlunda för att bli ett nytt block i sig, kan du låta författarna välja mellan [blockalternativ.](content-modeling.md#type-inference)

Genom att lägga till `classes` -egenskap till blocket, den egenskap som återges i tabellhuvudet för enkla block eller som värdelista för objekt i ett behållarblock.

```json
{
  "id": "simpleMarquee",
  "fields": [
    {
      "component": "text",
      "valueType": "string",
      "name": "marqueeText",
      "value": "",
      "label": "Marquee text",
      "description": "The text you want shown in your marquee"
    },
    {
      "component": "select",
      "name": "classes",
      "value": "",
      "label": "Background Color",
      "description": "The marquee background color",
      "valueType": "string",
      "options": [
        {
          "name": "Red",
          "value": "bg-red"
        },
        {
          "name": "Green",
          "value": "bg-green"
        },
        {
          "name": "Blue",
          "value": "bg-blue"
        }
      ]
    }
  ]
}
```

## Använda andra arbetsgrenar {#other-branches}

Den här guiden gav dig en direkt bindning till `main` för enkelhetens skull. Detta är vanligtvis inte något problem vid försök i en exempeldatabas. För verkligt projektarbete, [du bör följa bästa praxis för utveckling](https://www.aem.live/docs/dev-collab-and-good-practices) genom att utveckla på en annan gren och granska alla ändringar via pull-begäran innan de sammanfogas med `main`.

När du inte utvecklar på `main` gren, du kan lägga till `?ref=<branch>` i fältet Universal Editor för att läsa in sidan från din gren. `<branch>` är filialnamnet som det skulle användas för projektets förhandsgransknings- eller direktadresser, t.ex. `https://<branch>--<repo>--<owner>.hlx.page`.

Publicering av innehåll med en ny modell stöds bara när modellen sammanfogas med `main` gren.

## Nästa steg {#next-steps}

Nu när du vet hur man skapar block är det viktigt att förstå hur man modellerar innehåll på ett semantiskt sätt för att uppnå en smidig utvecklarupplevelse.

Se dokumentet [Innehållsmodellering för WYSIWYG-redigering med Edge Delivery Services Projects](/help/edge/wysiwyg-authoring/content-modeling.md) om du vill veta hur innehållsmodellering fungerar för WYSIWYG-redigering med Edge Delivery Services.

>[!TIP]
>
>Om du vill få en genomgång av hur du skapar ett projekt för nya Edge Delivery Services som är aktiverat för WYSIWYG-redigering med AEM as a Cloud Service som innehållskälla kan du titta på [det här AEM GEMs webbinarium.](https://experienceleague.adobe.com/en/docs/events/experience-manager-gems-recordings/gems2024/aem-authoring-and-edge-delivery)


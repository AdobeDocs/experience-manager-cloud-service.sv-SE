---
title: Skapa block som är instrumenterade för användning med den universella redigeraren
description: Lär dig hur du skapar block som är instrumenterade för användning med Universal Editor i WYSIWYG-redigering med Edge Delivery Services-projekt.
exl-id: 65a5600a-8d16-4943-b3cd-fe2eee1b4abf
feature: Edge Delivery Services
role: Admin, Architect, Developer
source-git-commit: fb7da1530f916ec63d5993446fd0c328af09ae7c
workflow-type: tm+mt
source-wordcount: '1415'
ht-degree: 0%

---


# Skapa block som är instrumenterade för användning med den universella redigeraren {#create-block}

Lär dig hur du skapar block som är instrumenterade för användning med Universal Editor i WYSIWYG-redigering med Edge Delivery Services-projekt.

## Förutsättningar {#prerequisites}

Den här guiden innehåller stegvisa instruktioner för hur du skapar block som är avsedda för den universella redigeraren i WYSIWYG-redigering med Edge Delivery Services-projekt. Det handlar om att lägga till komponenter, läsa in komponentdefinitioner i den universella redigeraren, publicera sidor, implementera blockdekoration och format, göra ändringar i produktionen och verifiera dem. När du är klar med den här guiden kan du skapa och distribuera ett nytt block för ditt eget projekt.

Den här guiden kräver kunskaper om WYSIWYG framtagning av Edge Delivery Services och den universella redigeraren. Innan du börjar den här guiden bör du ha tillgång till Edge Delivery Services och känna till grunderna i den:

* Du har slutfört självstudiekursen [Edge Delivery Service.](/help/edge/developer/tutorial.md)
* Du har åtkomst till en [AEM Cloud Service-sandlåda.](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md)
* Du har [aktiverat den universella redigeraren i samma sandlådemiljö.](/help/implementing/universal-editor/getting-started.md)
* Du har slutfört guiden [Komma igång för utvecklare för WYSIWYG med Edge Delivery Services](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md).

Den här guiden bygger vidare på det arbete som gjorts i guiden [Komma igång för utvecklare för WYSIWYG med Edge Delivery Services](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md) .

## Lägga till ett nytt block i projektet {#add-block}

I den här guiden skapar du ett block som återger ett minnesvärt citat på sidan.

För att förenkla det här exemplet görs alla ändringar i `main`-grenen i projektdatabasen. Självfallet för ditt faktiska projekt [bör du följa vedertagna utvecklingsmetoder](https://www.aem.live/docs/dev-collab-and-good-practices) genom att utveckla på en annan gren och granska alla ändringar via pull-begäran innan du sammanfogar till `main`.

Adobe rekommenderar att du utvecklar block i tre faser:

1. Skapa definitionen och modellen för blocket, granska det och ta det till produktion.
1. Skapa innehåll med det nya blocket.
1. Implementera dekoration och stilar för det nya blocket.

Följande exempel på offertblock följer den här metoden.

### Skapa blockdefinition och modell {#create-block-model}

1\. Klona GitHub-projektet lokalt som du skapade i guiden [Komma igång för WYSIWYG med Edge Delivery Services](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md) och öppna det i en valfri redigerare.

* Microsoft Code används här för illustrativa ändamål.

![Klonar projektet](assets/create-block/clone.png)

2\. Redigera filen `component-definition.json` i projektets rot och lägg till följande definition för det nya offertblocket och spara filen.

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

3\. Redigera filen `component-models.json` i projektets rot och lägg till följande [modelldefinition](/help/implementing/universal-editor/field-types.md#model-structure) för det nya offertblocket och spara filen.

* Mer information om vad som är viktigt att tänka på när du skapar innehållsmodeller finns i dokumentet [Innehållsmodellering för WYSIWYG-redigering med Edge Delivery Services ](/help/edge/wysiwyg-authoring/content-modeling.md) .

>[!BEGINTABS]

>[!TAB JSON-exempel]

```json
{
  "id": "quote",
  "fields": [
     {
       "component": "richtext",
       "name": "quote",
       "value": "",
       "label": "Quote",
       "valueType": "string"
     },
     {
       "component": "text",
       "valueType": "string",
       "name": "author",
       "label": "Author",
       "value": ""
     }
   ]
}
```

>[!TAB Skärmbild]

![Redigera filen component-models.json för att definiera modellen för citattecknet](assets/create-block/component-models.png)

>[!ENDTABS]

4\. Redigera filen `component-filters.json` i projektets rot och lägg till offertblocket i [filterdefinitionen](/help/implementing/universal-editor/customizing.md#filtering-components) så att det kan läggas till i valfritt avsnitt och spara filen.

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

![Redigera filen component-filters.json för att definiera filtren för citatblocket](assets/create-block/component-filters.png)

>[!ENDTABS]

5\. Använd Git för att implementera de här ändringarna i din `main`-gren.

* Att implementera på `main` är bara för illustrativa syften. [Följ bästa praxis](https://www.aem.live/docs/dev-collab-and-good-practices) och använd en pull-begäran för faktiskt projektarbete.

### Skapa innehåll med blocket {#create-content}

Nu när det grundläggande offertblocket är definierat och implementerat i exempelprojektet kan du lägga till ett offertblock på en befintlig sida.

1. Logga in på AEM as a Cloud Service i en webbläsare. [Använd webbplatskonsolen och](/help/sites-cloud/authoring/basic-handling.md) navigera till webbplatsen som du skapade i [Utvecklarhandboken Komma igång för WYSIWYG-redigering med Edge Delivery Services](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md) och markera en sida.

   * I det här fallet används `index` för illustrativa syften.

   ![Markera indexsidan i webbplatskonsolen](assets/create-block/sites-console.png)

1. Tryck eller klicka på **Redigera** i verktygsfältet på konsolen så öppnas Universell redigerare.

   * Om du vill läsa in sidan kan du behöva trycka på eller klicka på **Logga in med Adobe** för att autentisera AEM i Universella redigeraren.

1. Markera ett avsnitt i Universella redigeringsprogram. I egenskapspanelen trycker eller klickar du på ikonen **Lägg till** och väljer sedan det nya **offert**-blocket på menyn.

   * Ikonen **Lägg till** är en plustecken.
   * Du vet att du har markerat ett avsnitt om det markerade objektets blå kontur har en flik med namnet **Avsnitt**.
   * Om du i det här exemplet trycker eller klickar något ovanför rubriken **Lorem Ipsum** markeras ett avsnitt som innehåller rubriken och lorem ipsum-texten.

   ![Markera ett avsnitt i den universella redigeraren](assets/create-block/add-quote-block.png)

1. Sidan läses in igen och offertblocket läggs till längst ned i det markerade avsnittet med det standardinnehåll som anges i filen `component-definitions.json`.

   * Citatteckenblocket kan markeras och redigeras som vilket annat block som helst, antingen på plats eller på egenskapspanelen.
   * Formateringen görs i ett steg till.

   ![Sidan med det nya offertblocket i det markerade avsnittet](assets/create-block/quote-added.png)

1. När du är nöjd med offertens innehåll kan du publicera sidan genom att trycka på eller klicka på knappen **Publish** i verktygsfältet i den universella redigeraren.

1. Kontrollera att innehållet har publicerats genom att gå till den publicerade sidan. Länken liknar `https://<branch>--<repo>--<owner>.aem.page`

   ![Publicerad offert](assets/create-block/quote-published.png)

### Formatera blocket {#style-block}

Nu när du har ett fungerande offertblock kan du formatera det.

1\. Gå tillbaka till redigeraren för ditt projekt.

2\. Skapa en `quote`-mapp under mappen `blocks`.

![Skapa en offertmapp](assets/create-block/new-folder.png)

3\. I den nya mappen `quote` lägger du till en `quote.js`-fil som implementerar blockdekoration genom att lägga till följande JavaScript och spara filen.

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

![Lägger till JavaScript för att dekorera blocket](assets/create-block/quote-js.png)

>[!ENDTABS]

4\. I mappen `quote` lägger du till en `quote.css`-fil för att definiera blockets format genom att lägga till följande CSS-kod och spara filen.

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

![Lägger till CSS för att definiera blockformateringen](assets/create-block/quote-css.png)

>[!ENDTABS]

5\. Använd Git för att implementera de här ändringarna i din `main`-gren.

* Att implementera på `main` är bara för illustrativa syften. [Följ bästa praxis](https://www.aem.live/docs/dev-collab-and-good-practices) och använd en pull-begäran för faktiskt projektarbete.

6\. Gå tillbaka till webbläsarfliken i Universal Editor där du redigerade sidan i ditt projekt och läs in sidan igen för att visa det formaterade blocket.

7\. Se det nu formaterade citattecknet på sidan.

![Det formaterade citatteckenblocket i den universella redigeraren](assets/create-block/quote-styled.png)

8\. Kontrollera att ändringarna har flyttats till produktion genom att navigera till den publicerade sidan. Länken liknar `https://<branch>--<repo>--<owner>.aem.page`

![Det publicerade och formaterade citatteckenblocket](assets/create-block/quote-styled-published.png)

Grattis! Du har nu ett fullt fungerande och formaterat citattecken. Du kan använda det här exemplet som bas för att utforma egna projektspecifika block.

### Blockalternativ {#block-options}

Om du behöver ett block som ska se ut eller bete dig lite annorlunda baserat på vissa omständigheter, men inte tillräckligt annorlunda för att bli ett nytt block i sig, kan du låta författarna välja mellan [blockalternativen.](content-modeling.md#type-inference)

Genom att lägga till en `classes`-egenskap i blocket återges egenskapen i tabellhuvudet för enkla block eller som värdelista för objekt i ett behållarblock.

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

Den här guiden gjorde att du kunde binda dig direkt till grenen `main` för enkelhetens skull. Detta är vanligtvis inte något problem vid försök i en exempeldatabas. För verkligt projektarbete bör [du följa bästa praxis för utveckling](https://www.aem.live/docs/dev-collab-and-good-practices) genom att utveckla på en annan gren och granska alla ändringar via pull-begäran innan du sammanfogar till `main`.

När du inte utvecklar i grenen `main` kan du lägga till `?ref=<branch>` i fältet Universal Editor för att läsa in sidan från din gren. `<branch>` är filialnamnet som det skulle användas för ditt projekts förhandsgransknings- eller direktwebbadresser, t.ex. `https://<branch>--<repo>--<owner>.aem.page`.

## Återanvända era block för dokumentbaserad redigering {#reusing-blocks}

Du kan använda de block du skapar för WYSIWYG-redigering med den universella redigeraren för dokumentbaserad redigering om du följer samma innehållsmodell.

Mer information finns i dokumentet [Block för WYSIWYG och dokumentbaserad redigering](/help/edge/wysiwyg-authoring/wysiwyg-doc-blocks.md).

## Nästa steg {#next-steps}

Nu när du vet hur man skapar block är det viktigt att förstå hur man modellerar innehåll på ett semantiskt sätt för att uppnå en smidig utvecklarupplevelse.

Läs dokumentet [Innehållsmodellering för WYSIWYG-redigering med Edge Delivery Services ](/help/edge/wysiwyg-authoring/content-modeling.md) om du vill veta hur innehållsmodellering fungerar för WYSIWYG-redigering med Edge Delivery Services.

>[!TIP]
>
>En genomgång av hur du skapar ett projekt för nya Edge Delivery Services som är aktiverat för WYSIWYG-redigering med AEM as a Cloud Service som innehållskälla finns i [det här webbinariet för AEM.](https://experienceleague.adobe.com/en/docs/events/experience-manager-gems-recordings/gems2024/aem-authoring-and-edge-delivery)

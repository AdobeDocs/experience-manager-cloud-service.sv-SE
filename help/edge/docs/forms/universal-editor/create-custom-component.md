---
title: Skapa anpassade komponenter för ett EDS-formulär
description: Skapa anpassade komponenter för ett EDS-formulär
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 2bbe3f95-d5d0-4dc7-a983-7a20c93e2906
source-git-commit: 9ef4c5638c2275052ce69406f54dda3ea188b0ef
workflow-type: tm+mt
source-wordcount: '1804'
ht-degree: 0%

---

# Skapa anpassad komponent i WYSIWYG Authoring

<span class="preview"> Det här är en förhandsversion som är tillgänglig via vår <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=sv-SE#new-features">förhandsversion </a>. </span>


Edge Delivery Services Forms erbjuder anpassning så att gränssnittsutvecklare kan skapa skräddarsydda blankettkomponenter. Dessa anpassade komponenter integreras smidigt i WYSIWYG redigeringsmiljö, vilket gör det enkelt för formulärförfattare att lägga till, konfigurera och hantera dem i formulärredigeraren. Med anpassade komponenter kan man förbättra funktionaliteten samtidigt som man får en smidig och intuitiv redigeringsprocess.

I det här dokumentet beskrivs de olika stegen för att skapa anpassade komponenter genom att formatera de inbyggda HTML-formulärkomponenterna för att förbättra användarupplevelsen och göra formuläret snyggare.

## Krav

Innan du börjar skapa en anpassad komponent bör du:

* Lär dig grundläggande kunskaper om [inbyggda HTML-komponenter](/help/edge/docs/forms/form-components.md).
* Lär dig hur du [formaterar formulärfält baserat på fälttyp med CSS-väljarna](/help/edge/docs/forms/style-theme-forms.md)

## Skapa en anpassad komponent

Att lägga till en anpassad komponent i den universella redigeraren innebär att göra en ny komponent tillgänglig för formulärförfattare som kan använda när de utformar formulär. Detta innebär att registrera komponenten, definiera dess egenskaper och konfigurera var den kan användas. Stegen för att skapa anpassade komponenter är:

[1. Lägger till struktur för den nya anpassade komponenten ](#1-adding-structure-for-new-custom-component)
[ 2. Definiera egenskaperna för den anpassade komponenten för redigering av ](#2-defining-the-properties-of-your-custom-component-for-authoring)
[ 3.  Göra den anpassade komponenten synlig i WYSIWYG-komponentlistan ](#3-making-your-custom-component-visible-in-the-wysiwyg-component-list)
[ 4. Registrerar den anpassade komponenten ](#4-registering-your-custom-component)
[5. Lägger till körningsbeteendet för den anpassade komponenten ](#5-adding-the-runtime-behaviour-for-your-custom-component)

Låt oss ta ett exempel på hur du skapar en ny anpassad komponent med namnet **range**. Intervallkomponenten visas som en rak linje och visar värden som minimum, maximum eller selected.

![En visuell representation av en intervallkomponent som visar ett reglage med minimi- och maximivärden samt en markerad värdeindikator](/help/edge/docs/forms/universal-editor/assets/custom-component-range-style.png)

I slutet av den här artikeln lär du dig att skapa anpassade komponenter från grunden.

### &#x200B;1. Lägga till struktur för ny anpassad komponent

Innan en anpassad komponent kan användas måste den registreras så att Universal Editor identifierar den som ett tillgängligt alternativ. Detta uppnås genom en komponentdefinition, som innehåller en unik identifierare, standardegenskaper och komponentens struktur. Utför följande steg för att göra den anpassade komponenten tillgänglig för formulärutveckling:

1. **Lägg till ny mapp och nya filer**
Lägg till nya mappar och filer för den nya anpassade komponenten i AEM Project.
   1. Öppna ditt AEM-projekt och gå till `../blocks/form/components/`.
   1. Lägg till en ny mapp för din anpassade komponent på `../blocks/form/components/<component_name>`. I det här exemplet skapar vi en mapp med namnet `range`.
   1. Navigera till den nyligen skapade mappen på `../blocks/form/components/<component_name>`. Navigera till `../blocks/form/components/range` och lägg till följande filer:
      * `/blocks/form/components/range/_range.json`: Innehåller definitionen för den anpassade komponenten.
      * `../blocks/form/components/range/range.css`: Definierar formateringen för den anpassade komponenten.
      * `../blocks/form/components/range/range.js`: Anpassar den anpassade komponenten vid körning.

        ![Lägger till den anpassade komponenten för redigering](/help/edge/docs/forms/universal-editor/assets/adding-custom-component.png)

        >[!NOTE]
        >
        > Kontrollera att json-filen innehåller ett understreck (_) som prefix i filnamnet.

1. Navigera till filen `/blocks/form/components/range/_range.json` och lägg till komponentdefinitionen för den anpassade komponenten.

1. **Lägg till komponentdefinitionen**

   För att lägga till definitionen måste fälten läggas till i filen `_range.json`:

   * **title**: Titeln på komponenten som visas i den universella redigeraren.
   * **id**: En unik identifierare för komponenten.
   * **fieldType**: Forms stöder olika **fieldType** för att hämta specifika typer av användarindata. Du hittar den [stödda fieldType i avsnittet Extra Byte](#supported-fieldtypes).
   * **resourceType**: Varje anpassad komponent har en associerad resurstyp baserat på dess fieldType. Du hittar den [stödda resourceType i avsnittet Extra Byte](#supported-resourcetype).
   * **jcr:title**: Den liknar en titel, men den lagras i komponentens struktur.
   * **fd:viewType**: Den representerar namnet på den anpassade komponenten. Det är den unika identifieraren för komponenten. Du måste skapa en anpassad vy för komponenten.

`_range.json`-filen är följande när du har lagt till komponentdefinitionen:

```javascript
{
  "definitions": [
    {
      "title": "Range",
      "id": "range",
      "plugins": {
        "xwalk": {
          "page": {
            "resourceType": "core/fd/components/form/numberinput/v1/numberinput",
            "template": {
              "jcr:title": "Range",
              "fieldType": "number-input",
              "fd:viewType": "range",
              "enabled": true,
              "visible": true
            }
          }
        }
      }
    }
  ]
}
```

>[!NOTE]
>
> Alla formulärrelaterade komponenter följer samma tillvägagångssätt som webbplatser när de lägger till block i den universella redigeraren. Mer information finns i artikeln [Creating Blocks Instrumented for use with the Universal Editor](https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-service/content/edge-delivery/wysiwyg-authoring/create-block).

### &#x200B;2. Definiera egenskaperna för den anpassade komponenten för redigering

Den anpassade komponenten innehåller en komponentmodell som anger vilka egenskaper som kan konfigureras av formulärförfattaren. De här egenskaperna visas i dialogrutan **Egenskaper** i den universella redigeraren, vilket gör att författare kan justera inställningar som etiketter, valideringsregler, format och andra attribut. Så här definierar du egenskaper:

1. Navigera till filen `/blocks/form/components/range/_range.json` och lägg till komponentmodellen för den anpassade komponenten.

1. **Lägg till komponentmodellen**

   Om du vill definiera komponentmodellen för den anpassade komponenten måste du lägga till relevanta fält i filen `_range.json`.

   1. **Skapa ny modell**

      * Lägg till ett nytt objekt i modellarrayen och ställ in `id` för komponentmodellen så att den matchar egenskapen `fd:viewType` som konfigurerats tidigare i komponentdefinitionen.
      * Inkludera en fältarray i det här objektet.

   2. **Definiera fält för egenskapsdialogrutan**

      * Varje objekt i fältarrayen ska vara en behållartypskomponent, vilket gör att det kan visas som en flik i dialogrutan **Egenskap** .
      * Vissa fält kan referera till återanvändbara egenskaper i `models/form-common`.

   3. **Använd en befintlig komponentmodell som referens**

      * Du kan kopiera innehållet i en befintlig komponentmodell som motsvarar din valda `fieldType` och ändra den efter behov. Komponenten `number-input` utökas till att skapa en **range** -komponent, så vi kan använda modellarrayen från `models/form-components/_number-input.json` som referens.

   `_range.json`-filen är följande när du har lagt till komponentmodellen:

   ```javascript
   "models": [
   {
     "id": "range",
     "fields": [
       {
         "component": "container",
         "name": "basic",
         "label": "Basic",
         "collapsible": false,
         "...": "../../../../models/form-common/_basic-input-fields.json"
       },
       {
         "...": "../../../../models/form-common/_help-container.json"
       },
       {
         "component": "container",
         "name": "validation",
         "label": "Validation",
         "collapsible": true,
         "...": "../../../../models/form-common/_number-validation-fields.json"
       }
     ]
   }
   ]
   ```

   >[!NOTE]
   >
   > Om du vill lägga till ett nytt fält i dialogrutan **Egenskap** för en anpassad komponent följer du det [definierade schemat](https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/field-types#loading-model).

   Du kan också [lägga till anpassade egenskaper](#adding-custom-properties-for-your-custom-component) i en anpassad komponent för att utöka dess funktioner.

#### Lägga till anpassade egenskaper för den anpassade komponenten

Med anpassade egenskaper kan du definiera specifika beteenden baserat på värden som har angetts i egenskapsdialogrutan för en komponent. Detta gör att komponentens funktionalitet och anpassningsalternativ utökas.

I det här exemplet lägger vi till Stegvärde som en anpassad egenskap i intervallkomponenten.

![Egen egenskap för stegvärde](/help/edge/docs/forms/universal-editor/assets/customcomponent-stepvalue.png)

Lägg till den anpassade egenskapen Stegvärde genom att lägga till komponentmodellen med följande kodrader i filen ` _<component>.json`:

```javascript
      {
      "component": "number",
      "name": "stepValue",
      "label": "Step Value",
      "valueType": "number"
      }
```

JSON-fragmentet definierar en anpassad egenskap med namnet **Stegvärde** för en **Intervall** -komponent. Nedan visas en beskrivning av varje fält:

* **komponent**: Anger typen av indatafält som används i egenskapsdialogrutan. I det här fallet anger `number` att numeriska värden accepteras i fältet.
* **name**: Identifieraren för egenskapen, som används för att referera till den i komponentens logik. Här representerar `stepValue` stegvärdesinställningen för intervallet.
* **label**: Egenskapens visningsnamn som det visas i egenskapsdialogrutan.
* **valueType**: Definierar den datatyp som förväntas för egenskapen. `number` säkerställer att endast numeriska indata tillåts.

Du kan nu använda `stepValue` som en anpassad egenskap i JSON-egenskaperna för `range.js` och implementera dynamiskt beteende baserat på dess värde vid körning.

Därför är den sista `_range.json`-filen, efter att du har lagt till komponentdefinitionen, komponentmodellen och anpassade egenskaper, följande:

```javascript
 {
  "definitions": [
    {
      "title": "Range",
      "id": "range",
      "plugins": {
        "xwalk": {
          "page": {
            "resourceType": "core/fd/components/form/numberinput/v1/numberinput",
            "template": {
              "jcr:title": "Range",
              "fieldType": "number-input",
              "fd:viewType": "range",
              "enabled": true,
              "visible": true
            }
          }
        }
      }
    }
  ],
  "models": [
    {
      "id": "range",
      "fields": [
        {
          "component": "container",
          "name": "basic",
          "label": "Basic",
          "collapsible": false,
          "...": "../../../../models/form-common/_basic-input-fields.json"
         {
           "component": "number",
           "name": "stepValue",
            "label": "Step Value",
             "valueType": "number"
}
        },
        {
          "...": "../../../../models/form-common/_help-container.json"
        },
        {
          "component": "container",
          "name": "validation",
          "label": "Validation",
          "collapsible": true,
          "...": "../../../../models/form-common/_number-validation-fields.json"
        }
      ]
    }
  ]
}
```

![komponentdefinition och modell](/help/edge/docs/forms/universal-editor/assets/custom-component-json-file.png)


### &#x200B;3. Göra den anpassade komponenten synlig i komponentlistan i WYSIWYG

Ett filter definierar i vilket avsnitt den anpassade komponenten kan användas i Universellt redigeringsprogram. Detta garanterar att komponenten bara kan användas i lämpliga avsnitt, vilket bevarar strukturen och användbarheten.

Så här ser du till att den anpassade komponenten visas i listan med tillgängliga komponenter vid formulärutveckling i WYSIWYG:

1. Navigera till filen `/blocks/form/_form.json`.
1. Leta reda på komponentarrayen i objektet som har `id="form"`.
1. Lägg till värdet `fd:viewType` från `definitions[]` i komponentarrayen för objektet med `id="form"`.

```javascript
 "filters": [
    {
      "id": "form",
      "components": [
        "captcha",
        "checkbox",
        "checkbox-group",
        "date-input",
        "drop-down",
        "email",
        "file-input",
        "form-accordion",
        "form-button",
        "form-fragment",
        "form-image",
        "form-modal",
        "form-reset-button",
        "form-submit-button",
        "number-input",
        "panel",
        "plain-text",
        "radio-group",
        "rating",
        "telephone-input",
        "text-input",
        "tnc",
        "wizard",
        "range"
      ]
    }
  ]
```

![komponentfilter](/help/edge/docs/forms/universal-editor/assets/custom-component-form-file.png)

### &#x200B;4. Registrera din anpassade komponent

Om du vill att formulärblocket ska känna igen den anpassade komponenten och läsa in dess egenskaper som definierats i komponentmodellen vid formulärredigeringen, lägger du till värdet `fd:viewType` från komponentdefinitionen i filen `mappings.js`.
Så här registrerar du en komponent:
1. Navigera till filen `/blocks/form/mappings.js`.
1. Leta reda på `customComponents[]`-arrayen.
1. Lägg till värdet `fd:viewType` från arrayen `definitions[]` i arrayen `customComponents[]`.

```javascript
let customComponents = ["range"];
const OOTBComponentDecorators = ['file-input',
                                 'wizard', 
                                 'modal', 'tnc',
                                'toggleable-link',
                                'rating',
                                'datetime',
                                'list',
                                'location',
                                'accordion'];
```

![komponentmappning](/help/edge/docs/forms/universal-editor/assets/custom-component-mapping-file.png)

När du har slutfört stegen ovan visas den anpassade komponenten i formulärets komponentlista i Universalläsaren. Du kan sedan dra och släppa det i formuläravsnittet.

![Skärmbild av komponentpaletten Universal Editor som visar den anpassade intervallkomponenten som är tillgänglig för dra och släpp i formulär](/help/edge/docs/forms/universal-editor/assets/custom-component-range.png)

Skärmbilden nedan visar egenskaperna för komponenten `range` som lagts till i komponentmodellen, som anger egenskaperna som formulärförfattaren kan konfigurera:

![Skärmbild på egenskapspanelen för den universella redigeraren med konfigurerbara inställningar för intervallkomponenten inklusive grundläggande egenskaper, verifieringsregler och formateringsalternativ](/help/edge/docs/forms/universal-editor/assets/range-properties.png)

Nu kan du definiera runtime-beteendet för den anpassade komponenten genom att lägga till format och funktioner.

### &#x200B;5. Lägga till körningsbeteende för den anpassade komponenten

Du kan ändra anpassade komponenter med fördefinierad kod, vilket förklaras i [Formateringen av formulärfält](/help/edge/docs/forms/style-theme-forms.md). Detta kan du göra med anpassad CSS (Cascading Style Sheets) och anpassad kod för att förbättra komponentens utseende. Så här lägger du till körningsbeteendet för komponenten:

1. Om du vill lägga till formatet går du till filen `/blocks/form/components/range/range.css` och lägger till följande kodrad:

   ```javascript
   /** Styling for range */
   main .form .range-widget-wrapper.decorated input[type="range"] {
   margin: unset;
   padding: unset;
   appearance: none;
   height: 5px;
   border-radius: 5px;
   border: none;
   background-image: linear-gradient(to right, #ADD8E6 calc(100% * var(--current-steps)/var(--total-steps)), #C5C5C5 calc(100% * var(--current-steps)/var(--total-steps)));
   }
   
   main .form .range-widget-wrapper.decorated input[type="range"]:focus {
   outline: none;
   }
   
   .range-widget-wrapper.decorated input[type="range"]::-webkit-slider-thumb {
   appearance: none;
   width: 25px;
   height: 25px;
   border-radius: 50%;
   background: #00008B; /* Dark Blue */
   border: 3px solid #00008B; /* Dark Blue */
   cursor: pointer;
   outline: 3px solid #fff;
   }
   
   .range-widget-wrapper.decorated input[type="range"]:focus::-webkit-slider-thumb {
   border-color: #00008B; /* Dark Blue */
   }
   
   .range-widget-wrapper.decorated .range-bubble {
   color: #00008B; /* Dark Blue */
   font-size: 20px;
   line-height: 28px;
   position: relative;
   display: inline-block;
   padding-bottom: 12px;
   font-weight: bold;
   }
   
   .range-widget-wrapper.decorated .range-min,
   .range-widget-wrapper.decorated .range-max {
   font-size: 14px;
   line-height: 22px;
   color: #494f50;
   margin-top: 16px;
   display: inline-block;
   }
   
   .range-widget-wrapper.decorated .range-max {
   float: right;
   }
   ```

   Koden hjälper dig att definiera den anpassade komponentens format och visuella utseende.

1. Om du vill lägga till funktionen går du till filen `/blocks/form/components/range/range.js` och lägger till följande kodrad:

   ```javascript
   function updateBubble(input, element) {
   const step = input.step || 1;
   const max = input.max || 0;
   const min = input.min || 1;
   const value = input.value || 1;
   const current = Math.ceil((value - min) / step);
   const total = Math.ceil((max - min) / step);
   const bubble = element.querySelector('.range-bubble');
   // during initial render the width is 0. Hence using a default here.
   const bubbleWidth = bubble.getBoundingClientRect().width || 31;
   const left = `${(current / total) * 100}% - ${(current / total) * bubbleWidth}px`;
   bubble.innerText = `${value}`;
   const steps = {
       '--total-steps': Math.ceil((max - min) / step),
       '--current-steps': Math.ceil((value - min) / step),
   };
   const style = Object.entries(steps).map(([varName, varValue]) => `${varName}:${varValue}`).join(';');
   bubble.style.left = `calc(${left})`;
   element.setAttribute('style', style);
   }
   
   export default async function decorate(fieldDiv, fieldJson) {
   console.log('RANGE DIV: ', fieldDiv);
   console.log('RANGE JSON: fieldJson', fieldJson);
    const input = fieldDiv.querySelector('input');
   // modify the type in case it is not range.
   input.type = 'range';
   input.min = input.min || 10;
   input.max = input.max || 1000;
   // create a wrapper div to provide the min/max and current value
   const div = document.createElement('div');
   div.className = 'range-widget-wrapper decorated';
   input.after(div);
   const hover = document.createElement('span');
   hover.className = 'range-bubble';
   const rangeMinEl = document.createElement('span');
   rangeMinEl.className = 'range-min';
   const rangeMaxEl = document.createElement('span');
   rangeMaxEl.className = 'range-max';
   rangeMinEl.innerText = `${input.min || 1}`;
   rangeMaxEl.innerText = `${input.max}`;
   div.appendChild(hover);
   // move the input element within the wrapper div
   div.appendChild(input);
   div.appendChild(rangeMinEl);
   div.appendChild(rangeMaxEl);
   input.addEventListener('input', (e) => {
   updateBubble(e.target, div);
   });
   updateBubble(input, div);
   return fieldDiv;
   }
   ```

   Den styr hur den anpassade komponenten interagerar med användarens indata, bearbetar data och integreras med formulärblocket i den universella redigeraren.

   När du har infogat anpassade format och funktioner förbättras intervallkomponentens utseende och beteende. Den uppdaterade designen återspeglar de format som används, medan den nya funktionen ger en mer dynamisk och interaktiv användarupplevelse.
Skärmbilden nedan visar den uppdaterade intervallkomponenten.

![Den sista omfångskomponenten som fungerar visar ett reglage med värdebubblor och interaktiva funktioner i Universell redigerare](/help/edge/docs/forms/universal-editor/assets/custom-component-range-1.png)

## Frågor och svar

* **Om jag lägger till en stil i både component.css och forms.css, vilket prioriterar jag?**
När format definieras i både `component.css` och **forms.css** prioriteras `component.css` . Detta beror på att format på komponentnivå är mer specifika och åsidosätter globala format från `forms.css`.

* **Min anpassade komponent visas inte i listan över tillgängliga komponenter i Universal Editor. Hur kan jag åtgärda det här?**
Om din anpassade komponent inte visas kontrollerar du följande filer för att säkerställa att komponenten är korrekt registrerad:
   * **component-definition.json**: Verifiera att komponenten är korrekt definierad.
   * **component-filters.json**: Kontrollera att komponenten tillåts i rätt avsnitt.
   * **component-models.json**: Bekräfta att komponentmodellen är korrekt konfigurerad.

## Bästa praxis

* Vi rekommenderar att du [konfigurerar en lokal AEM-utvecklingsmiljö](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#set-up-local-aem-development-environment) för att utveckla anpassade format och komponenter lokalt.


## Extra byte

### ResourceType som stöds

| Fälttyp | Resurstyp |
|--------------|------------------------------------------------------------------|
| text-input | core/fd/components/form/textinput/v1/textinput |
| tal-input | core/fd/components/form/numberinput/v1/numberinput |
| date-input | core/fd/components/form/datepicker/v1/datepicker |
| panel | core/fd/components/form/panel/v1/panelContainer |
| kryssruta | core/fd/components/form/checkbox/v1/checkbox |
| nedrullningsbar | core/fd/components/form/dropdown/v1/dropdown |
| alternativgrupp | core/fd/components/form/radiobutton/v1/radiobutton |
| normal text | core/fd/components/form/text/v1/text |
| file-input | core/fd/components/form/fileinput/v2/fileinput |
| e-post | core/fd/components/form/emailinput/v1/emailinput |
| image | core/fd/components/form/image/v1/image |
| knapp | core/fd/components/form/button/v1/button |

### FieldTypes som stöds

FieldTypes som stöds för formulär är:
* text-input
* tal-input
* date-input
* panel
* kryssruta
* nedrullningsbar
* alternativgrupp
* normal text
* file-input
* e-post
* image
* knapp

## Se även

{{universal-editor-see-also}}

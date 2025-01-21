---
title: Skapa anpassade komponenter för ett EDS-formulär
description: Skapa anpassade komponenter för ett EDS-formulär
feature: Edge Delivery Services
hide: true
hidefromtoc: true
exl-id: 77e90657-38db-4a49-9aac-3f3774b62624
role: Admin, Architect, Developer
source-git-commit: 812b1e41b460783d3fa220bd24ecfcfd4208a5df
workflow-type: tm+mt
source-wordcount: '665'
ht-degree: 1%

---

# Skapa anpassade komponenter

Med Edge Delivery Services för AEM Forms kan du anpassa [systemspecifika HTML-formulärkomponenter](/help/edge/docs/forms/form-components.md) och skapa användarvänliga och interaktiva formulär. Det gör att du kan ändra formulärkomponenterna med fördefinierad kod, vilket förklaras i [Formateringen av formulärfält](/help/edge/docs/forms/style-theme-forms.md) med anpassad CSS (Cascading Style Sheets) och anpassad kod för att dekorera komponenten, vilket förbättrar utseendet på formulärfält i ett adaptivt Forms-block.

![Egen komponent](/help/edge/assets/custom-component-image.png)

I det här dokumentet beskrivs de olika stegen för att skapa anpassade komponenter genom att formatera de inbyggda HTML-formulärkomponenterna för att förbättra användarupplevelsen och göra formuläret snyggare.

Låt oss ta ett exempel på en `range`-komponent som visar `Estimated trip cost` i ett formulär. Komponenten `range` visas som en rak linje utan att visa värden som minimum, maximum eller selected.

![Intern intervallkomponent](/help/edge/assets/native-range-component.png)

Låt oss börja anpassa fältet `range` för att visa minsta, högsta och valda värden på raden genom att lägga till format med CSS och lägga till en anpassad funktion för att dekorera en komponent.

![Anpassad intervallkomponent](/help/edge/assets/custom-range-component.png)

I slutet av den här artikeln lär du dig att skapa anpassade komponenter genom att lägga till format i CSS-filen och den anpassade funktionen.

## Krav

Innan du börjar skapa en anpassad komponent bör du:

* Lär dig grundläggande kunskaper om [inbyggda HTML-komponenter](/help/edge/docs/forms/form-components.md).
* Lär dig hur du [formaterar formulärfält baserat på fälttyp med CSS-väljarna](/help/edge/docs/forms/style-theme-forms.md)


## Skapa en anpassad komponent


![steg för att skapa en anpassad komponent](/help/edge/docs/forms/assets/steps-to-create-custom-component.png)

Låt oss nu förstå varje steg i detalj.

Gå till [frågekalkylbladet](/help/edge/docs/forms/assets/enquiry.xlsx) om du vill anpassa komponenten `range` genom att följa stegen som beskrivs nedan.

### Lägga till en anpassad funktion för att dekorera komponenten

Den anpassade funktion som lagts till i `[../Form Block/components]` består av:

* **Funktionsdeklaration**: Definiera funktionsnamnet och dess parametrar.
* **Logikimplementering**: Skriv logiken för att lägga till det anpassade beteendet för komponenten.
* **Funktionsexport**: Gör funktionen tillgänglig i `[Form Block]`.

Låt oss skapa en JavaScript-fil med namnet `range.js` för att formatera intervallkomponenten. Så här lägger du till en anpassad funktion:

1. Gå till AEM projektmapp på Google Drive eller SharePoint.
1. Navigera till `[../Form Block/components]`.
1. Lägg till en ny fil med namnet `range.js`.
1. Lägg till följande kodrad:

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
   '--total-steps': Math.ceil((max - min) /    step),
   '--current-steps': Math.ceil((value - min) / step),
   };
   const style = Object.entries(steps).map(([varName, varValue]) => `${varName}:${varValue}`).join(';');
   bubble.style.left = `calc(${left})`;
   element.setAttribute('style', style);
   }
   // eslint-disable-next-line no-unused-vars
   export default function decorateRange(fieldDiv, field) {
   loadCSS('/blocks/form/components/range/range.css');
   const input = fieldDiv.querySelector('input');
   // modify the type in case it is not range.
   input.type = 'range';
   input.min = input.min || 1;
   // create a wrapper div to provide the min/max and current value
   const div = document.createElement('div');
   div.className = 'range-widget-wrapper';
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
   // as a best practice add a custom css class to apply custom styling
   fieldDiv.classList.add('decorated');
   return fieldDiv;    
   }
   ```

1. Spara ändringarna.

### Mata in dekoratorn i formulärblocket

`[Form Block]` använder semantiskt HTML för att återge formulärfält, inklusive inmatningsfält, etiketter och hjälptext, med standardattribut för tillgänglighet. Om du vill att `[Form Block]` ska använda en anpassad dekorator för en angiven komponent definierar du den i filen `mappings.js`. Filen `mappings.js` importerar en funktion som returnerar modulen som ansvarar för att dekorera en viss komponent. Funktionen tar fältegenskaperna och returnerar en dekoratorfunktion för formulärfältet.

I det här fallet kontrollerar funktionen egenskapen `fieldType` för fältet och returnerar den anpassade intervalldekoratorn från filen `range.js` i `[../Form Block/components]`.

Så här injicerar du dekoratorn i formulärblocket:

1. Gå till `[../Form Block/]` och öppna `mapping.js`.
1. Lägg till följande kodrad:

   ```javascript
   export default async function componentDecorator(fd) {
   const { ':type': type = '', fieldType } = fd;
   .... existing code ....
   if (fieldType === 'range') {
   const module = await import('./components/range.js');
   return module.default(element,fd);;
   }
    return null; // null should be returned to use the original markup
   }
   ```

1. Spara ändringarna.

### Lägga till format för komponenten i CSS-filen

Du kan ändra utseendet på formulärfält baserat på fälttyp och fältnamn med hjälp av CSS-väljare, vilket ger en konsekvent eller unik formatering baserat på krav. Om du vill formatera komponenten lägger du till kod i filen `form.css` för att ändra utseendet och känslan för formulärets komponent.

Om du vill anpassa formatet för komponenten `range` inkluderar du ett CSS-kodfragment som formaterar ett `range` -indataelement och dess associerade komponenter i ett formulär. Detta förutsätter en strukturerad HTML-layout med klasser som `.form` och `.range-wrapper`.

Så här lägger du till format för en komponent i CSS-filen:
1. Gå till `[../Form Block/]` och öppna `form.css`.
1. Lägg till följande kodrad:

   ```javascript
       /** styling for range */
   main .form .range-wrapper.decorated input[type="range"] {
   margin: unset;
   padding: unset;
   appearance: none;
   height: 5px;
   border-radius: 5px;
   border: none;
   background-image: linear-gradient(to right, var(--button-primary-color) calc(100% * var(--current-steps)/var(--total-steps)), #C5C5C5 calc(100% * var(--current-steps)/var(--total-steps)));
   }
   
   main .form .range-wrapper.decorated input[type="range"]:focus {
   outline: none;
   }
   
   .range-wrapper.decorated input[type="range"]::-webkit-slider-thumb {
   appearance: none;
   width: 25px;
   height: 25px;
   border-radius: 50%;
   background: #fff;
   border: 3px solid var(--button-primary-color);
   cursor: pointer;
   outline: 3px solid #fff;
   }
   
   .range-wrapper.decorated input[type="range"]:focus::-webkit-slider-thumb {
   border-color: var(--button-primary-color);
   }
   
   .range-wrapper.decorated .range-bubble {
   color: #17252e;
   font-size: 20px;
   line-height: 28px;
   position: relative;
   display: inline-block;
   padding-bottom: 12px;
   }
   
   .range-wrapper.decorated .range-min,
   .range-wrapper.decorated .range-max {
   font-size: 14px;
   line-height: 22px;
   color: #494f50;
   margin-top: 16px;
   display: inline-block;
   }
   
   .range-wrapper.decorated .range-max {
   float: right;
   }
   ```
1. Spara ändringarna.

### Distribuera filerna och bygg projektet

Distribuera de uppdaterade `range.js`-, `mapping.css`- och `form.css`-filerna till ditt GitHub-projekt och verifiera en lyckad version.

### Förhandsgranska formuläret med AEM

Använd [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) om du vill förhandsgranska formuläret med den nyligen implementerade funktionen som formaterar komponenten `range`.

![Anpassat komponentformulär](/help/edge/assets/custom-componet-form.png)

Den nya formateringen för komponenten `range` visar lägsta, högsta och valda värden på raden genom att lägga till format med CSS och en anpassad funktion som innehåller en dekorator för komponenten.


## Se även

{{see-more-forms-eds}}




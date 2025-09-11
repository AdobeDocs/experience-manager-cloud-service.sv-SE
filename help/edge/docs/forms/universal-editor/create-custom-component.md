---
title: Skapa anpassade komponenter för ett EDS-formulär
description: Skapa anpassade komponenter för ett EDS-formulär
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 2bbe3f95-d5d0-4dc7-a983-7a20c93e2906
source-git-commit: 6a63b4f839516a2ebc1eec641eb36315efca6dd5
workflow-type: tm+mt
source-wordcount: '2120'
ht-degree: 0%

---


# Skapa anpassad formulärkomponent i anpassat formulärblock

Edge Delivery Services Forms erbjuder anpassning så att gränssnittsutvecklare kan skapa skräddarsydda blankettkomponenter. Dessa anpassade komponenter integreras smidigt i WYSIWYG redigeringsmiljö, vilket gör det enkelt för formulärförfattare att lägga till, konfigurera och hantera dem i formulärredigeraren. Med anpassade komponenter kan man förbättra funktionaliteten samtidigt som man får en smidig och intuitiv redigeringsprocess.

I det här dokumentet beskrivs de olika stegen för att skapa anpassade komponenter genom att formatera de inbyggda HTML-formulärkomponenterna för att förbättra användarupplevelsen och göra formuläret snyggare.

## Arkitektur - översikt

En anpassad komponent för Forms-blocket följer ett **MVC-arkitekturmönster (Model-View-Controller)**:

### Modell

- Definieras av JSON-schemat för varje `field/component`.

- Redigerbara egenskaper anges i motsvarande JSON-fil (se block/form/models/form-components).

- Dessa egenskaper är tillgängliga för författare i formulärbyggaren och skickas till komponenten som en del av fältdefinitionen (fd).

### Visa

- HTML-strukturen för varje fälttyp beskrivs i formulärfälttyper.

- Det här är grundstrukturen för komponenten som kan utökas eller ändras.

- HTML grundstruktur för varje OOTB-komponent dokumenteras i formulärfälttyper.

### Styrenhets-/komponentlogik

- Implementeras i JavaScript, antingen som OTB (färdiga) eller anpassade komponenter.  - Finns i `blocks/form/components` för anpassade komponenter.

## OTB-komponenter

**OTB-komponenter (färdiga)** utgör grunden för anpassad utveckling:

- OTB-komponenter finns i `blocks/form/models/form-components`.

- Varje OTB-komponent har en JSON-fil som definierar dess redigerbara egenskaper (till exempel ` _text-input.json`,`_drop-down.json`).

- Dessa egenskaper är tillgängliga för författare i formulärbyggaren och skickas till komponenten som en del av fältdefinitionen (fd).

- HTML grundstruktur för varje OOTB-komponent dokumenteras i formulärfälttyper.

Genom att utöka en befintlig OOTB-komponent kan du återanvända dess grundstruktur, beteende och egenskaper samtidigt som du anpassar den efter dina behov.

- Anpassade komponenter måste omfatta en fördefinierad uppsättning OTB-komponenter.

- Systemet identifierar vilken OTB-komponent som ska utökas baserat på egenskapen `viewType` i fältets JSON.

- Systemet underhåller ett register med tillåtna anpassade komponentvarianter. Endast varianter som anges i det här registret kan användas, till exempel `customComponents[]` i `mappings.js`.

- När ett formulär återges kontrolleras variantegenskapen eller `:type/fd:viewType`. Om den matchar en registrerad anpassad komponent läses motsvarande JS- och CSS-filer in från mappen `blocks/form/components`.

- Den anpassade komponenten tillämpas sedan på OTB-komponentens bas-HTML-struktur, vilket gör att du kan förbättra eller åsidosätta dess beteende och utseende.

## Struktur för anpassad komponent

Om du vill skapa anpassade komponenter kan du använda **SCaffolder CLI** för att konfigurera de filer och mappar som krävs för komponenten och sedan lägga till kod för den anpassade komponenten.

- Anpassade komponenter finns i mappen `blocks/form/components`.

- Varje anpassad komponent måste placeras i sin egen mapp, med namnet efter komponenten, till exempel kort. I mappen ska följande filer vara:

   - **_cards.json** - JSON-fil som utökar komponentdefinitionen för en OTB-komponent, definierar dess redigerbara egenskaper (modeller []) och innehållsstruktur vid inläsning (definitioner []).
   - **cards.js** - Den JavaScript-fil som innehåller huvudlogiken.
   - **cards.css** - valfritt, för format.

- Namnet på mappen och JS/CSS-filerna måste matcha.

### Återanvända och utöka fält i anpassade komponenter

När du definierar fält i den anpassade komponentens JSON (för alla fältgrupper, grundläggande fält, validering, hjälp osv.) följer du de här bästa sätten för underhåll och konsekvens:

- Återanvänd standardfält/delade fält genom att referera till befintliga delade behållare eller fältdefinitioner (t.ex. `../form-common/_basic-input-placeholder-fields.json#/fields`, `../form-common/_basic- validation-fields.json#/fields`). Detta garanterar att du ärver alla standardalternativ utan att duplicera dem.

- Lägg bara till nya eller anpassade fält explicit i behållaren. Detta håller ditt schema DRY och fokuserat.

- Ta bort eller undvik att duplicera fält som redan finns i referenser. Definiera bara fält som är unika för komponentens logik.

- Referera till hjälpbehållare och annat delat innehåll (t.ex. `../form-common/_help-container.json`) efter behov för konsekvens och underhåll.

>[!TIP]
>
> - Det här mönstret gör det enkelt att uppdatera eller utöka logiken i framtiden och ser till att dina anpassade komponenter är konsekventa med resten av formulärsystemet.
> - Kontrollera alltid om det finns befintliga delade behållare eller fältdefinitioner innan du lägger till nya.

### Definiera nya egenskaper för anpassade komponenter

- Om du behöver hämta nya egenskaper för den anpassade komponenten från författare kan du göra det genom att definiera ett fält i komponentens `fields[]`-array i komponentens JSON-komponent.

- Den anpassade komponenten identifieras med egenskapen :type som kan anges som `fd:viewType` i JSON-filen (t.ex. `fd:viewType: cards`). Detta gör att systemet kan känna igen och läsa in rätt anpassad komponent och därför är detta obligatoriskt för anpassade komponenter

- Alla nya egenskaper som läggs till i JSON-definitionen är tillgängliga som egenskaper i fältdefinitionen. `<propertyName>` i din komponents JS-logik

## JavaScript API för anpassad komponent

JavaScript-API:t för den anpassade komponenten definierar hur du styr beteendet, utseendet och reaktiviteten för den anpassade formulärkomponenten.

### Dekorera funktion

Funktionen **decorate** är startpunkten för den anpassade komponenten. Komponenten initieras, länkas till dess JSON-definition och gör att du kan ändra dess HTML-struktur och -beteende.

>[!NOTE]
>
> Den anpassade komponentens JavaScript-fil måste exportera en standardfunktion som dekorate:

#### Funktionssignatur:

```javascript
export default function decorate(element, fieldJson, container, formId) {
// element: The HTML structure of the OOTB component you are extending
// fieldJson: The JSON field definition (all authorable properties)
// container: The parent element (fieldset or form)
// formId: The id of the form
// ... your logic here ...
}
```

Den kan:

- **Ändra elementet**: Lägg till händelseavlyssnare, uppdatera attribut eller mata in ytterligare kod.

- **Åtkomst till JSON-egenskaper**: Använd `fd.properties.<propertyName>` för att läsa värden som definierats i JSON-schemat och tillämpa dem i komponentlogiken.

## Prenumerationsfunktion

Funktionen **subscribe** gör att komponenten kan reagera på ändringar i fältvärden eller anpassade händelser. Detta garanterar att komponenten är synkroniserad med formulärets datamodell och kan uppdatera användargränssnittet dynamiskt.

### Funktionssignatur:

```JavaScript
import { subscribe } from '../../rules/index.js';

export default function decorate(fieldDiv, fieldJson, container, formId) {
// Access custom properties defined in the JSON
const { initialText, finalText, time } = fieldJson?.properties;
// ... setup logic ...
subscribe(fieldDiv, formId, (_fieldDiv, fieldModel) => { fieldModel.subscribe(() => {
// React to custom event (e.g., resetCardOption)
// ... logic ...
}, 'resetCardOption');
});
}
```

Den kan:

- **Registrera ett återanrop**: Anrop av **subscribe(element, formId, callback)** registrerar ditt återanrop så att det körs när fältdata ändras. Använd två återanropsparametrar:
   - **element**: Det HTML-element som representerar fältet.
   - **fieldModel**: Det objekt som representerar fältets läges- och händelse-API:er.

- **Lyssna efter ändringar eller händelser**: Använd `fieldModel.subscribe((event) => { ... }, 'eventName')` för att köra logik när ett värde ändras eller en anpassad händelse aktiveras. Händelseobjektet innehåller information om vad som ändrats.

## Skapa en anpassad komponent

I det här avsnittet får du lära dig hur du skapar en anpassad **kortkomponent** genom att utöka alternativknappskomponenten OTB.

![Anpassad kortkomponent](/help/edge/docs/forms/universal-editor/assets/cc-ue-card-component.png)

### &#x200B;1. Kodinställningar

#### 1.1 Filer och mappar

Det första steget är att ställa in de nödvändiga filerna för den anpassade komponenten och koppla den upp till koden i databasen. Den här processen utförs automatiskt av **AEM Forms Scaffolder CLI**, vilket gör det snabbare att ställa in och snurra nödvändiga filer.

>[!VIDEO](https://video.tv.adobe.com/v/3474752)

1. Öppna terminalen och navigera till roten i formulärprojektet.
2. Kör följande kommandon:

```bash
npm install
npm run create:custom-component
```

![Skaffelmapp CLI](/help/edge/docs/forms/universal-editor/assets/scaffolder-cli.png)

Den kommer att

- **Uppmana dig att namnge** den nya komponenten. Använd i det här fallet kort.
- **Be dig välja** en baskomponent (markera alternativknappar)

Då skapas alla mappar och filer som behövs, inklusive:

```
blocks/form/
└── components/
  └── cards/
    ├── cards.js
    └── cards.css
    └── _cards.json
```

Och knyter ihop den med resten av koden i databasen, så som visas i CLI-utdata.
Följande funktioner utförs automatiskt:

- Lägger till kort i filtren så att de kan läggas till i det adaptiva formulärblocket.
- Uppdaterar tillåtelselista till `mappings.js` för att inkludera den nya kortkomponenten.
- Registrerar definitionen av kortkomponenten under listan **Anpassade komponenter** i Universalläsaren.

>[!NOTE]
>
> Du kan också skapa en anpassad komponent med den manuella (äldre) metoden. Mer information finns i avsnittet [Manuell eller Äldre metod](#manual-or-legacy-method-to-create-custom-component) för att skapa anpassade komponenter.

#### 1.2 Använda komponent i universell redigerare

1. **Uppdatera den universella redigeraren**: Öppna formuläret i den universella redigeraren och uppdatera sidan så att den senaste koden från databasen läses in.

2. **Lägg till den anpassade komponenten**

   1. Klicka på knappen **Lägg till (+)** på formulärets arbetsyta.
   2. Bläddra till sektionen Egna komponenter.
   3. Välj den nyligen skapade **kortkomponenten** för att infoga den i formuläret.

      ![Välj anpassad komponent](/help/edge/docs/forms/universal-editor/assets/select-custom-component.png)

Eftersom det inte finns någon kod i `cards.js` återges den anpassade komponenten som en alternativknappsgrupp.

#### 1.3 Förhandsgranska och testa lokalt

Nu när formuläret innehåller den anpassade komponenten kan du proxygranska formuläret och göra ändringar i det lokalt och se ändringarna:

1. Gå till terminalen och kör `aem up`.

2. Öppna proxyservern som startades `http://localhost:3000/{path-to-your-form}` (sökvägsexempel: `/content/forms/af/custom-component-form`)


### &#x200B;2. Implementera anpassat beteende för din anpassade komponent

#### 2.1 Formatera den anpassade komponenten

Låt oss lägga till klassen **card** i komponenten för formatering och lägga till en bild för varje radio. Använd koden nedan för detta.

**Formatera den anpassade komponenten med dekorationsfunktionen i cards.js**

```javascript
import { createOptimizedPicture } from '../../../../scripts/aem.js';

export default function decorate(element, fieldJson, container, formId) { element.classList.add('card');
element.querySelectorAll('.radio-wrapper').forEach((radioWrapper) => { const image = createOptimizedPicture('https://main--afb--
jalagari.hlx.live/lab/images/card.png', 'card-image'); radioWrapper.appendChild(image);
});
return element;
}
```

**Lägg till körningsbeteende för den anpassade komponenten i cards.css**

```javascript
.card .radio-wrapper { min-width: 320px;
/* or whatever width fits your design */ max-width: 340px;
background: #fff;
border-radius: 16px;
box-shadow: 0 2px 8px rgba(0, 0, 0, 0.08);
flex: 0 0 auto;
scroll-snap-align: start; padding: 24px 16px;
margin-bottom: 0;
position: relative;
transition: box-shadow 0.2s; display: flex;
align-items: flex-start; gap: 12px;
}
```

Nu ser kortkomponenten ut så här:

![lägg till css och js-kort](/help/edge/docs/forms/universal-editor/assets/add-card-css.png)

#### 2.2 Lägga till dynamiskt beteende med prenumerationsfunktion

När listrutan ändras hämtas korten och ställs in i uppräkningen för alternativgruppen. Men för närvarande hanterar inte vyn det här. Det återges så som visas nedan:

![prenumerationsfunktion](/help/edge/docs/forms/universal-editor/assets/card-subscribe.png)

När API anropas anges fältmodellen och ändringarna måste avlyssnas och vyn återges. Detta uppnås med funktionen **subscribe**.

Låt oss konvertera visningskoden i föregående steg till en funktion och anropa den inuti prenumerationsfunktionen i `cards.js` enligt nedan:

```javascript
import { createOptimizedPicture } from '../../../../scripts/aem.js';  

import { subscribe } from '../../rules/index.js';  
function createCard(element, enums) {  

  element.querySelectorAll('.radio-wrapper').forEach((radioWrapper, index) => {  

    if (enums[index]?.name) {  

      let label = radioWrapper.querySelector('label');  

      if (!label) {  

        label = document.createElement('label');  

        radioWrapper.appendChild(label);  

      }  

      label.textContent = enums[index]?.name;  

    }  

    const image = createOptimizedPicture(enums[index].image || 'https://main--afb--jalagari.hlx.page/lab/images/card.png', 'card-image');  

   radioWrapper.appendChild(image);  

  });  

}  
export default function decorate(element, fieldJson, container, formId) {  

    element.classList.add('card');  

    createCard(element, fieldJson.enum);  

    subscribe(element, formId, (fieldDiv, fieldModel) => {  

        fieldModel.subscribe((e) => {  

            const { payload } = e;  

            payload?.changes?.forEach((change) => {  

                if (change?.propertyName === 'enum') {  

                    createCard(element, change.currentValue);  

                }  

            });  

        });  

    });  
    return element;  

} 
```

**Använd prenumerationsfunktionen för att lyssna efter händelseändringar i cards.js**

När du ändrar listrutan fylls korten i enligt nedan:

![prenumerationsfunktion](/help/edge/docs/forms/universal-editor/assets/card-subscribe-final.png)

#### 2.3 Synkronisera vyuppdateringar med fältmodell

Om du vill synkronisera vyändringarna till fältmodellen måste du ange värdet för det valda kortet. Lägg därför till följande ändringshändelseavlyssnare i cards.js enligt nedan:

**Använda API för fältmodell i cards.js**

```javascript
 

import { createOptimizedPicture } from '../../../../scripts/aem.js';  

import { subscribe } from '../../rules/index.js';  

  

  

function createCard(element, enums) {  

  element.querySelectorAll('.radio-wrapper').forEach((radioWrapper, index) => {  

    if (enums[index]?.name) {  

      let label = radioWrapper.querySelector('label');  

      if (!label) {  

        label = document.createElement('label');  

        radioWrapper.appendChild(label);  

      }  

      label.textContent = enums[index]?.name;  

    }  

    radioWrapper.querySelector('input').dataset.index = index;  

    const image = createOptimizedPicture(enums[index].image || 'https://main--afb--jalagari.hlx.page/lab/images/card.png', 'card-image');  

   radioWrapper.appendChild(image);  

  });  

}  
export default function decorate(element, fieldJson, container, formId) {  

    element.classList.add('card');  
    createCard(element, fieldJson.enum);  

    subscribe(element, formId, (fieldDiv, fieldModel) => {  

        fieldModel.subscribe((e) => {  

            const { payload } = e;  

            payload?.changes?.forEach((change) => {  

                if (change?.propertyName === 'enum') {  

                    createCard(element, change.currentValue);  

                }  

            });  

        });  
        element.addEventListener('change', (e) => {  

            e.stopPropagation();  

            const value = fieldModel.enum?.[parseInt(e.target.dataset.index, 10)];  

            fieldModel.value = value.name;  

        });  

    });  

    return element;  
} 
```

Nu visas den anpassade kortkomponenten enligt nedan:

![Anpassad kortkomponent](/help/edge/docs/forms/universal-editor/assets/cc-ue-card-component.png)

## Verkställ och skicka ändringar

När du har implementerat JavaScript och CSS för den anpassade komponenten och verifierat den lokalt implementerar och skickar du ändringarna till din Git-databas.

```bash
git add . && git commit -m "Add card custom component" && git push
```

Du har skapat en komplex, anpassad kortmarkeringskomponent i några enkla steg.

## Manuell eller äldre metod för att skapa anpassad komponent

Det äldre sättet att göra detta är att manuellt följa stegen som beskrivs nedan:

1. **Välj en OOTB-komponent** att utöka (t.ex. knapp, listruta, textinmatning osv.). I det här fallet utökar du radiokomponenten.

2. **Skapa en mapp** i `blocks/form/components` med din komponents namn (kort i det här fallet).

3. **Lägg till en JS-fil** med samma namn:
   - `blocks/form/components/cards/cards.js`.

4. (Valfritt) **Lägg till en CSS-fil** för anpassade format:
   - `blocks/form/components/cards/cards.css.`

5. **Definiera en ny JSON-fil** (t.ex. ` _cards.json`) i samma mapp som din **komponent-JS-fil** (`blocks/form/components/cards/_cards.json`). Denna JSON bör utöka en befintlig komponent och i sina definitioner ange `fd:viewType` till din komponents namn (kort i det här fallet):

   - Lägg till anpassade fält explicit för alla fältgrupper (grundläggande, validering, hjälp osv.).

6. **Implementera logiken för JS och CSS:**
   - Exportera en standardfunktion enligt beskrivningen ovan.
   - Använd parametern **element** för att ändra HTML grundstruktur.
   - Använd parametern **fieldJson** om det behövs för standardfältdata.
   - Använd funktionen **subscribe** för att lyssna på fältändringar eller anpassade händelser om det behövs.

     >[!NOTE]
     >
     >Implementera JS- och CSS-logiken för den anpassade komponenten enligt beskrivningen ovan.

7. Registrera komponenten som en variant i formulärbyggaren och ange variantegenskapen eller
   `fd:viewType/:type` i JSON till din komponents namn, till exempel, lägg till värdet `fd:viewType` från `definitions[]` som kort i komponentarrayen för objektet med `id="form`.

   ```javascript
   {
   "definitions": [
   {
   "title": "Cards",
   "id": "cards", "plugins": {
   "xwalk": {
   "page": {
   "resourceType":
   "core/fd/components/form/radiobutton/v1/radiobutton", "template": {
   "jcr:title": "Cards",
   "fieldType": "radio-button", "fd:viewType": "cards",
   "enabled": true, "visible": true}
   }
   } }
   }
   ]}
   ```

8. **Uppdatera mappings.js**: Lägg till komponentens namn i listan **OOTBComponentDecorators** (för OTB-formatkomponenter) eller **customComponents** så att den känns igen och läses in av systemet.

   ```javascript
   let customComponents = ["cards"];
   const OOTBComponentDecorators = [];
   ```

9. **Uppdatera_form.json**: Lägg till komponentens namn i arrayen `filters.components` så att den kan tas bort i redigeringsgränssnittet.

   ```javascript
   "filters": [
   {
       "id": "form",
       "components": [ "cards"]}
       ]
   ```

10. **Uppdatera _component-definition.json**: I `models/_component-definition.json` uppdaterar du arrayen i gruppen med `id custom-components` med ett objekt på följande sätt:

   ```javascript
   {
   "...":"../blocks/form/components/cards/_cards.json#/definitions"
   }
   ```

   Detta är för att ge referens till den nya kortkomponenten som ska byggas med resten av komponenterna

11. **Kör build:json script**: Kör `npm run build:json` för att kompilera och sammanfoga alla komponent-JSON-definitioner till en enda fil som ska hanteras från servern. Detta garanterar att den nya komponentens schema inkluderas i de sammanfogade utdata.

12. Implementera och skicka dina ändringar till din Git-databas.

Nu kan du lägga till den anpassade komponenten i formuläret.

## Skapa en sammansatt komponent

En sammansatt komponent skapas genom att flera komponenter kombineras.
En sammansatt villkorskomponent består till exempel av en överordnad panel som innehåller:

- Ett oformaterat textfält för att visa villkoren

- En kryssruta för att hämta användarens avtal

Kompositionsstrukturen definieras som en mall inuti respektive komponents JSON-fil. I följande exempel visas hur du definierar en mall för en villkorskomponent:

```javascript
{ 

  "definitions": [ 

    { 

      "title": "Terms and conditions", 

      "id": "tnc", 

      "plugins": { 

        "xwalk": { 

          "page": { 

            "resourceType": "core/fd/components/form/termsandconditions/v1/termsandconditions", 

            "template": { 

              "jcr:title": "Terms and conditions", 

              "fieldType": "panel", 

              "fd:viewType": "tnc", 

              "text": { 

                "value": "Text related to the terms and conditions come here.", 

                "sling:resourceType": "core/fd/components/form/text/v1/text", 

                "fieldType": "plain-text", 

                "textIsRich": true 

              }, 

              "approvalcheckbox": { 

                "name": "approvalcheckbox", 

                "jcr:title": "I agree to the terms & conditions.", 

                "sling:resourceType": "core/fd/components/form/checkbox/v1/checkbox", 

                "fieldType": "checkbox", 

                "required": true, 

                "type": "string", 

                "enum": [ 

                  "true" 

                ] 

              } 

            } 

          } 

        } 

      } 

    } 

  ], 

  ... 

} 
```

## Bästa praxis

Tänk på följande innan du skapar en egen anpassad komponent:

- **Behåll fokuseringen på komponentlogiken**: Lägg endast till/åsidosätt det som är nödvändigt för ditt anpassade beteende

- **Utnyttja grundstrukturen**: Använd OTB HTML som startpunkt

- **Använd redigerbara egenskaper:** Visa konfigurerbara alternativ via JSON-schemat

- **Namnge din CSS**: Undvik formatkonflikter genom att använda unika klassnamn

## Referenser

- formulärfälttyper: Grundläggande HTML-strukturer och -egenskaper för alla fälttyper. [Klicka här](/help/edge/docs/forms/eds-form-field-properties) om du vill visa detaljerade formulärfältsstrukturer och egenskaper.

- **block/form/models/form-components**: OTB och anpassade egenskapsdefinitioner för komponenter.

- **block/form/components**: Placera dina anpassade komponenter. Exempel: `blocks/form/components/countdown-timer/_countdown-timer.json` visar hur du utökar en baskomponent och lägger till nya egenskaper.

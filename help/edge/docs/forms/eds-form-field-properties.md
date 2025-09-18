---
title: Lagra egenskaper för anpassat Forms-blockfält
description: Skapa kraftfulla blanketter snabbare med kalkylblad och anpassningsbara Forms Block Field Properties! I den här guiden visas alla egenskaper som stöds av EDS Forms Block.
feature: Edge Delivery Services
source-git-commit: ccc6439f68d8199154d4cd664b9cdb6428460a64
workflow-type: tm+mt
source-wordcount: '930'
ht-degree: 0%

---


# Egenskaper för anpassat Forms-blockfält

Det här dokumentet sammanfattar hur JSON-scheman mappar till återgiven HTML i `blocks/form/form.js`, med fokus på hur fält identifieras och återges, vanliga mönster och fältspecifika skillnader.

## Hur fält (`fieldType`) identifieras?

Varje fält i JSON-schemat har en `fieldType`-egenskap som avgör hur det återges. `fieldType` kan vara:

- **En specialtyp**\
  Exempel: `drop-down`, `radio-group`, `checkbox-group`, `panel`, `plain-text`, `image`, `heading` osv.
- **En giltig HTML-indatatyp**\
  Exempel: `text`, `number`, `email`, `date`, `password`, `tel`, `range`, `file` osv.
- **En typ med ett `-input` suffix**\
  Exempel: `text-input`, `number-input` osv. (normaliserat till bastypen som `text`, `number`).

Om `fieldType` matchar en specialtyp används en **anpassad renderare** . Annars behandlas den som en **standardindatatyp**.

Se avsnitten nedan för den [fullständiga HTML-strukturen och egenskaperna](#common-html-structure) för varje fälttyp.

## Vanliga egenskaper som används av fält

Nedan visas de egenskaper som används i de flesta fält:

- `id`: Anger element-ID:t och stöder hjälpmedel.
- `name`: Definierar attributet `name` för indata-, select- eller fältuppsättningselement.
- `label.value`, `label.richText`, `label.visible`: Anger etikettexten/förklaringstexten, HTML-innehåll och synlighet.
- `value`: Representerar fältets aktuella värde.
- `required`: Lägger till attributet `required` eller valideringsdata.
- `readOnly`, `enabled`: Kontrollerar om fältet är redigerbart eller inaktiverat.
- `description`: Visar hjälptext under fältet.
- `tooltip`: Anger attributet `title` för indata.
- `constraintMessages`: Tillhandahåller anpassade felmeddelanden som dataattribut.

## Vanlig HTML-struktur

De flesta fält återges i en wrapper som innehåller en etikett och valfri hjälptext. I följande utdrag visas strukturen:

```html
<div class="<fieldType>-wrapper field-wrapper field-<name>" data-id="<id>">
<label for="<id>" class="field-label">Label</label>
<!-- Field-specific input/element here -->
<div class="field-description" id="<id>-description">Description or error
message</div>
</div>
```

För grupper (radio/kryssruta) och paneler används en `<fieldset>` med en `<legend>` i stället för en `<div>/<label>`. Hjälptexten <div> finns bara om beskrivning har angetts.

## Felmeddelandevisning

Felmeddelanden visas i samma `.field-description`-element som används för hjälptexten, som uppdateras dynamiskt.

**När ett fält är ogiltigt**:

- Radbrytaren (t.ex. `.field-wrapper`) tilldelas klassen `.field-invalid`.
- Innehållet i `.field-description` har ersatts med motsvarande felmeddelande.

**När fältet blir giltigt**:

- Klassen `.field-invalid` har tagits bort.
- `.field-description` återställs till den ursprungliga hjälptexten (om den är tillgänglig) eller tas bort om det inte finns någon.

Anpassade felmeddelanden kan definieras med egenskapen `constraintMessages` i JSON.\
De läggs till som `data-<constraint>ErrorMessage`-attribut i wrapper (till exempel `data-requiredErrorMessage`).

## Standardindatatyper (HTML Input eller `*-input`)

Om `fieldType` inte är en specialtyp behandlas den som en HTML-standardindatatyp eller som `<type>-input`, till exempel `text`, `number`, `email`, `date`, `text-input`, `number-input`.

- Suffixet `-input` tas bort och bastypen används som indatans `type`-attribut.
- De här typerna hanteras som standard i `renderField()`.
Vanliga standardindatatyper är `text`, `number`, `email`, `date`, `password`, `tel`, `range`, `file` osv.  De accepterar också `text-input`, `number-input` osv., som normaliseras till bastypen.

## Begränsningar för standardindatatyper

Begränsningar läggs till som attribut i indataelementet baserat på JSON-egenskaper.

| JSON-egenskap | HTML Attribute | Gäller för |
|--------------|---------------|------------|
| maxLength | maxlength | text, e-post, lösenord, tel |
| minLength | minlength | text, e-post, lösenord, tel |
| mönster | mönster | text, e-post, lösenord, tel |
| maximum | max | tal, intervall, datum |
| minimum | min | tal, intervall, datum |
| steg | steg | tal, intervall, datum |
| acceptera | acceptera | fil |
| flera | flera | fil |
| maxOccur | data-max | panel |
| minOccur | data-min | panel |

>[!NOTE]
>
> `multiple` är en boolesk egenskap. Om värdet är true läggs attributet `multiple` till.

Dessa attribut anges automatiskt av formuläråtergivaren baserat på fältets JSON-definition.

## Exempel: HTML Structure med Constraints

I följande exempel visas hur ett nummerfält återges med valideringsbegränsningar och felhanteringsattribut.

```html
<div class="number-wrapper field-wrapper field-age" data-id="age"
data-required="true"
data-minimumErrorMessage="Too small" data-maximumErrorMessage="Too large">
<label for="age" class="field-label">Age</label>
<input type="number"
id="age" name="age"
value="30" required min="18"
max="99" step="1"
placeholder="Enter your age" />
<div class="field-description" id="age-description"> Description or error message
</div>
</div>
```

Varje del av HTML-strukturen spelar en roll när det gäller databindning, validering och visning av hjälp- och felmeddelanden.

## Fältspecifika egenskaper och deras HTML-strukturer

### Nedrullningsbar meny

**Extra egenskaper:**

- `enum` / `enumNames`: Definiera alternativvärden och deras visningsetiketter för listrutan.
- `type`: Aktiverar flera markeringar om värdet är `array`.
- `placeholder`: Lägger till ett inaktiverat platshållaralternativ som vägleder användarna före markeringen.

Exempel:

```html
<div class="drop-down-wrapper field-wrapper field-<name>" data-id="<id>"
data-required="true"
data-requiredErrorMessage="This field is required">
<label for="<id>" class="field-label">Label</label>
<select id="<id>" name="<name>" required title="Tooltip" multiple>
<option disabled selected value="">Placeholder</option>
<option value="opt1">Option 1</option>
<option value="opt2">Option 2</option>
</select>
<div class="field-description" id="<id>-description"> Description or error message
</div>
</div>
```

### Oformaterad text

**Extra egenskaper**:

- `richText`: Om true återges HTML i stycket.

Exempel:

```html
<div class="plain-text-wrapper field-wrapper field-<name>" data-id="<id>">
<label for="<id>" class="field-label">Label</label>
<p>Text or <a href="..." target="_blank">link</a></p>
</div>
```

### Kryssruta

**Extra egenskaper**:

- `enum`: Definierar värdena för kryssrutans markerade och omarkerade lägen.
- `properties.variant / properties.alignment`: Anger den visuella stilen och justeringen för kryssrutor i switchstil.

Exempel:

```html
<div class="checkbox-wrapper field-wrapper field-<name>" data-id="<id>"
data-required="true"
data-requiredErrorMessage="Please check this box">
<label for="<id>" class="field-label">Label</label>
<input type="checkbox"
id="<id>"
name="<name>" value="on"
required
data-unchecked-value="off" />
<div class="field-description" id="<id>-description"> Description or error message
</div>
</div>
```

### Knapp

**Extra egenskaper**:

- `buttonType`: Anger knappens beteende genom att ange dess typ (knapp, skicka eller återställ).

Exempel:

```html
<div class="button-wrapper field-wrapper field-<name>" data-id="<id>">
<button id="<id>" name="<name>" type="submit" class="button"> Label
</button>
</div>
```

### Flera rader

**Extra egenskaper**:

- `minLength`: Anger det minsta antalet tecken som tillåts i text- eller textområdesindata.
- `maxLength`: Anger det maximala antalet tecken som tillåts i text- eller textområdesindata.
- `pattern`: Definierar ett reguljärt uttryck som indatavärdet måste matcha för att betraktas som giltigt.
- `placeholder`: Visar platshållartext i indata eller textområdet tills ett värde anges.

Exempel:

```html
<div class="multiline-wrapper field-wrapper field-<name>" data-id="<id>"
data-minLengthErrorMessage="Too short" data-maxLengthErrorMessage="Too long">
<label for="<id>" class="field-label">Label</label>
<textarea id="<id>"
name="<name>" required
minlength="2"
maxlength="100"
pattern="[A-Za-z]+"
placeholder="Type here..."></textarea>
<div class="field-description" id="<id>-description"> Description or error message
</div>
</div>
```

### Panel

**Extra egenskaper**:

- `repeatable`: Anger om panelen kan upprepas dynamiskt.
- `minOccur`: Anger det minsta antalet panelinstanser som krävs.   maxOccur: Anger maximalt antal tillåtna panelinstanser.
- `properties.variant`: Definierar panelens visuella stil eller variant.
- `properties.colspan`: Anger hur många kolumner panelen spänner över i en stödrasterlayout.
- `index`: Anger panelens position i dess överordnade behållare.
- `fieldset`: Grupperar relaterade fält under ett `<fieldset>`-element med en teckenförklaring eller etikett.

Exempel:

```html
<fieldset class="panel-wrapper field-wrapper field-<name>" data-id="<id>"
name="<name>"
data-repeatable="true" data-index="0">
<legend class="field-label">Label</legend>
<!-- Nested fields here -->
<button type="button" class="add">Add</button>
<button type="button" class="remove">Remove</button>
<div class="field-description" id="<id>-description"> Description or error message
</div>
</fieldset>
```

### Radio

**Extra egenskaper**:

- `enum`: Definierar uppsättningen tillåtna värden för alternativfältet, som används som värdeattribut för varje alternativknappsalternativ.

Exempel:

```html
<div class="radio-wrapper field-wrapper field-<name>" data-id="<id>"
data-required="true">
<label for="<id>" class="field-label">Label</label>
<input type="radio" id="<id>" name="<name>" value="opt1" required />
<div class="field-description" id="<id>-description"> Description or error message
</div>
</div>
```

### Alternativgrupp

**Extra egenskaper**:

- `enum`: Definierar listan med alternativvärden för alternativgruppen, som används som varje alternativknapps värde.
- `enumNames`: Tillhandahåller visningsetiketter för alternativknapparna, som matchar uppräkningsordningen.

Exempel:

```html
<fieldset class="radio-group-wrapper field-wrapper field-<name>" data-id="<id>"
data-required="true">
<legend class="field-label">Label</legend>
<div>
<input type="radio" id="<id>-0" name="<name>" value="opt1" required />
<label for="<id>-0">Option 1</label>
</div>
<div>
<input type="radio" id="<id>-1" name="<name>" value="opt2" />
<label for="<id>-1">Option 2</label>
</div>
<div class="field-description" id="<id>-description"> Description or error message
</div>
</fieldset>
```

### **Kryssrutegrupp**

**Extra egenskaper**:

- `enum`: Definierar listan med alternativvärden för kryssrutegruppen, som används som varje kryssrutas värde.
- `enumNames`: Tillhandahåller visningsetiketter för kryssrutorna, enligt uppräkningsordningen.
- `minItems`: Anger det minsta antalet kryssrutor som måste markeras för att vara giltiga.
- `maxItems`: Anger det maximala antalet kryssrutor som kan markeras innan ett fel utlöses.

Exempel:

```html
<fieldset class="checkbox-group-wrapper field-wrapper field-<name>" data-id="<id>"
data-required="true" data-minItems="1"
data-maxItems="3">
<legend class="field-label">Label</legend>
<div>
<input type="checkbox" id="<id>-0" name="<name>" value="opt1" required />
<label for="<id>-0">Option 1</label>
</div>
<div>
<input type="checkbox" id="<id>-1" name="<name>" value="opt2" />
<label for="<id>-1">Option 2</label>
</div>
<div class="field-description" id="<id>-description"> Description or error message
</div>
</fieldset>
```

### Bild

**Extra egenskaper**:

- `value / properties['fd:repoPath']`: Definierar sökvägen till bildkällan eller databassökvägen för återgivning av bilden.
- `altText`: Tillhandahåller alternativ text för bilden (alt-attribut) för att förbättra tillgängligheten.

Exempel:

```html
<div class="image-wrapper field-wrapper field-<name>" data-id="<id>">
<picture>
<img src="..." alt="..." />
<!-- Optimized sources -->
</picture>
</div>
```

### Rubrik

**Extra egenskaper**:

- `value`: Anger det textinnehåll som ska visas i rubrikelementet (t.ex. `<h2>`).

Exempel:

```html
<div class="heading-wrapper field-wrapper field-<name>" data-id="<id>">
<h2 id="<id>">Heading Text</h2>
</div>
```

Mer information finns i implementeringen i `blocks/form/form.js` och `blocks/form/util.js`.


<!--Each form field is represented as a dedicated row in the spreadsheet, analogous to fields in a database table. The column headers act as labels for the various properties supported by the form field block.

Think of your form as a table in a spreadsheet, where each line represents a different question or piece of information you want to collect. The table headings tell you what kind of answers you can expect for each section.

The below table lists all the properties that are supported by the Adaptive Forms Block.

**Master Your Forms with These Adaptive Forms Block Field Properties:**

This table details all the properties you can use to customize your Adaptive Forms Block fields:

| Property | Description | Example |
|---|---|---|
| **Type** | [HTML input type](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#input_types) (text, email, number, etc.), [textarea](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea), [select](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select), [fieldset](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset) | `text`, `email`, `radio`, `select` |
| **Name** | This defines the unique identifier for submitted data (e.g., 'email' for an email address field).  Choose a clear and unique name for each field, as the name serves as internal field identifier used for data mapping during submission. | `user_name`, `email_address` |
| **Label** | User-friendly field label | `"Full Name"`, `"Choose your country"` |
| **Value** | Default value displayed | `"John Doe"`, `"United States"` |
| **Placeholder** | Hint text within the field | `"Enter your email address"` |
| **Description** | Help text for users | `"Please enter a valid email address"` |
| **Visible** | Show/hide the field initially | `true`, `false` |
| **Mandatory** | Require a value from the user | `true`, `false` |
| **Min/Max** | Set minimum/maximum values (number, date, text length) | `18` (age), `2025-12-31` (date) |
| **Accept** | Allowed file types for file upload | `"image/jpeg,image/png"` |
| **Multiple** | Allow multiple file selections | `true`, `false` |
| **Options** | Comma-separated list for dropdown menus | `"Option 1, Option 2, Option 3"` |
| **Checked** | Default-selected radio button/checkbox | `true`, `false` |
| **Fieldset** | Group fields together | Fieldset name (e.g., `"Personal Information"`) |-->


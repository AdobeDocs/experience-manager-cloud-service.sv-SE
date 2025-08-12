---
title: Anpassa tema och stil för en Edge Delivery Services for AEM Forms
description: Anpassa temat och formatet för AEM Forms som levereras via Edge Delivery Services på ett effektivt sätt och skapa en sammanhängande och varumärkesanpassad användarupplevelse.
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: ac780399-34fe-457d-aaf4-b675656c024d
source-git-commit: edfefb163e2d48dc9f9ad90fa68809484ce6abb0
workflow-type: tm+mt
source-wordcount: '2493'
ht-degree: 0%

---

# Anpassa utseendet på formulären

Formulärformatering i Edge Delivery Services för AEM Forms kräver en sofistikerad förståelse för CSS-anpassade egenskaper, blockbaserad arkitektur och komponentspecifika strategier för målinriktning. Till skillnad från traditionella metoder för blankettformatering implementerar Adaptive Forms Block ett systematiskt designtokensystem som möjliggör enhetlig hantering samtidigt som man bibehåller Edge Delivery Services prestanda- och tillgänglighetsfördelar.

Den adaptiva Forms Block-arkitekturen genererar standardiserade HTML-strukturer för alla formulärkomponenter, vilket skapar förutsägbara mönster för CSS-målinriktning och anpassning. Tack vare den här enhetligheten kan utvecklare implementera omfattande formateringssystem som kan byggas ut över komplexa formulärimplementeringar samtidigt som de blockbaserade prestandaoptimeringarna som gör Edge Delivery Services exceptionellt snabba bevaras.

Denna omfattande handbok beskriver de tekniska grunderna för formulärformatering i Edge Delivery Services ekosystem, inklusive anpassade CSS-egenskapssystem, HTML-komponentstrukturmönster och avancerade formateringstekniker. Dokumentationen ger både teoretisk förståelse och praktisk implementeringsvägledning för att skapa avancerade varumärkesanpassade formulärupplevelser.

## Det du kommer att behärska

**CSS Custom Properties Mastery**: Förstå hela variabelsystemet som styr formulärutseendet, inklusive färgscheman, typografiskalor, mellanrumssystem och layoutparametrar. Lär dig hur du åsidosätter och utökar dessa egenskaper för att implementera omfattande varumärkesteman.

**Komponentarkitektur Förstå**: Få djupa kunskaper om de HTML-strukturmönster som används av varje formulärkomponenttyp, vilket möjliggör exakt CSS-målinriktning och anpassning utan att de underliggande funktionerna eller tillgänglighetsfunktionerna förstörs.

**Avancerade formateringstekniker**: Implementera sofistikerade formateringsmönster, inklusive lägesbaserad formatering, responsiv designintegrering och prestandaoptimerade anpassningsstrategier som bevarar de snabbladdande egenskaperna hos Edge Delivery Services.

**Professionella implementeringsstrategier**: Lär dig branschledande metoder för formulärformatering, inklusive integrering av designsystem, bibehållbar CSS-arkitektur och felsökningstekniker för komplexa formateringsscenarier.

## Förstå formulärfältstyper

Innan vi börjar dyka upp i en formatmall ska vi granska den gemensamma formulärtypen [fälttyper](/help/edge/docs/forms/universal-editor/create-custom-component.md#supported-fieldtypes) som stöds av det adaptiva Forms-blocket:

- Indatafält: Dessa innehåller textinmatningar, e-postinmatningar, lösenordsinmatningar med mera.
- Kryssrutegrupper: Används för att välja flera alternativ.
- Alternativgrupper: Används för att endast välja ett alternativ från en grupp.
- Listrutor: Kallas även urvalsrutor, som används för att välja ett alternativ i en lista.
- Paneler/behållare: Används för att gruppera relaterade formulärelement.

## Grundläggande formatprinciper

Att förstå [grundläggande CSS-koncept](https://www.w3schools.com/css/css_intro.asp) är avgörande innan du formaterar specifika formulärfält:

- [Väljare](https://www.w3schools.com/css/css_selectors.asp): Med CSS-väljare kan du ange specifika HTML-element som mål för formateringen. Du kan använda elementväljare, klassväljare eller ID-väljare.
- [Egenskaper](https://www.w3schools.com/css/css_syntax.asp): CSS-egenskaper definierar elementens visuella utseende. Vanliga egenskaper för formatformulärfält är bland annat färg, bakgrundsfärg, kant, utfyllnad, marginal.
- [Rutmodell](https://www.w3schools.com/css/css_boxmodel.asp): CSS-rutmodellen beskriver strukturen för HTML-element som ett innehållsområde omgivet av utfyllnad, kanter och marginaler.
- Flexbox/Grid: CSS [Flexbox](https://www.w3schools.com/css/css3_flexbox.asp) och [Grid layouts](https://www.w3schools.com/css/css_grid.asp) är kraftfulla verktyg för att skapa responsiva och flexibla designer.




## Omfattande formulärformatering med CSS-anpassade egenskaper

Det adaptiva Forms-blocket använder en sofistikerad CSS-arkitektur som bygger på anpassade egenskaper (CSS-variabler) som möjliggör systematisk tema och enhetlig formatering för alla formulärkomponenter. Att förstå denna struktur är nödvändigt för effektiv anpassning och varumärkesanpassning av formulär.

### Formulär.css-arkitekturen - introduktion

Standardformulärformaten finns i projektdatabasen på `/blocks/form/form.css` och följer en strukturerad metod som prioriterar underhållsbarhet, konsekvens och anpassningsflexibilitet. Arkitekturen består av flera viktiga komponenter:

**Anpassad CSS-egenskapsgrund**: Formateringssystemet bygger på anpassade CSS-egenskaper som definierats på `:root` -nivå, vilket ger ett centraliserat temasystem som överlappar alla formulärkomponenter. Dessa variabler används för att skapa designvariabler för färg-, typografi-, mellanrums- och layoutegenskaper.

**Blockbaserad CSS-struktur**: Edge Delivery Services använder en blockbaserad arkitektur där klassen `.form` fungerar som det primära namnutrymmet för alla formulärrelaterade format, vilket säkerställer korrekt omfångsisolering och förhindrar CSS-konflikter med andra sidkomponenter.

**Komponentspecifik formatering**: Individuella formulärkomponenter formateras med konsekventa brytningsmönster (`.{Type}-wrapper`) som ger förutsägbar målanpassning för olika fälttyper samtidigt som den övergripande designsystemintegriteten bevaras.

### Anpassad CSS-referens för egenskaper

Formulärformatsystemet innehåller över 50 anpassade CSS-egenskaper som styr alla aspekter av formulärens utseende och beteende. Genom att förstå dessa egenskaper kan du göra omfattande anpassningar samtidigt som du bibehåller designens enhetlighet.

+++ Färg- och temavariabler

Färgsystemet lägger grunden till en komplett visuell grund för blanketter med hjälp av välstrukturerade anpassade egenskaper:

```css
:root {
    /* Primary color system */
    --background-color-primary: #fff;
    --label-color: #666;
    --border-color: #818a91;
    --form-error-color: #ff5f3f;
    
    /* Button color system */
    --button-primary-color: #5F8DDA;
    --button-secondary-color: #666;
    --button-primary-hover-color: #035fe6;
    
    /* Form-specific color applications */
    --form-background-color: var(--background-color-primary);
    --form-input-border-color: var(--border-color);
    --form-invalid-border-color: #ff5f3f;
    --form-label-color: var(--label-color);
}
```

**Exempel på praktisk anpassning**: Om du vill implementera ett mörkt tema för dina formulär åsidosätter du basfärgsvariablerna:

```css
:root {
    --background-color-primary: #1a1a1a;
    --label-color: #e0e0e0;
    --border-color: #404040;
    --form-error-color: #ff6b6b;
    --button-primary-color: #4a9eff;
}
```

Den här enskilda ändringen sprids genom alla formulärkomponenter eftersom systemet använder variabelreferenser i stället för hårdkodade värden.

+++

+++ Typografi- och mellanrumsvariabler

Variabler för typografi och mellanrum ger omfattande kontroll över textpresentation och layout:

```css
:root {
    /* Font size system */
    --form-font-size-m: 22px;
    --form-font-size-s: 18px;
    --form-font-size-xs: 16px;
    
    /* Component-specific typography */
    --form-label-font-size: var(--form-font-size-s);
    --form-label-font-weight: 400;
    --form-title-font-weight: 600;
    --form-input-font-size: 1rem;
    
    /* Spacing system */
    --form-field-horz-gap: 40px;
    --form-field-vert-gap: 20px;
    --form-input-padding: 0.75rem 0.6rem;
    --form-padding: 0 10px;
}
```

**Exempel på praktisk anpassning**: Så här skapar du en mer kompakt formulärlayout med mindre typografi:

```css
:root {
    --form-font-size-m: 18px;
    --form-font-size-s: 14px;
    --form-font-size-xs: 12px;
    --form-field-horz-gap: 20px;
    --form-field-vert-gap: 15px;
    --form-input-padding: 0.5rem 0.4rem;
}
```

+++

+++ Layout- och strukturvariabler

Layoutvariabler styr formulärdimensioner, stödrasterbeteende och komponentdisposition:

```css
:root {
    /* Form layout */
    --form-width: 100%;
    --form-columns: 12;
    --form-submit-width: 100%;
    
    /* Card-based components */
    --form-card-border-radius: 4px;
    --form-card-padding: 0.6rem 0.8rem;
    --form-card-shadow: 0 1px 2px rgb(0 0 0 / 3%);
    --form-card-hover-shadow: 0 2px 4px rgb(0 0 0 / 6%);
    
    /* Wizard-specific layout */
    --form-wizard-padding: 0px;
    --form-wizard-padding-bottom: 160px;
    --form-wizard-step-legend-padding: 10px;
}
```

**Exempel på praktisk anpassning**: Så här skapar du ett kortliknande formulär med utökat visuellt djup:

```css
:root {
    --form-card-border-radius: 12px;
    --form-card-padding: 1.5rem 2rem;
    --form-card-shadow: 0 4px 12px rgb(0 0 0 / 8%);
    --form-card-hover-shadow: 0 8px 24px rgb(0 0 0 / 12%);
    --form-background-color: #f8f9fa;
}

.form {
    background: var(--form-background-color);
    border-radius: var(--form-card-border-radius);
    box-shadow: var(--form-card-shadow);
    padding: var(--form-card-padding);
    max-width: 600px;
    margin: 2rem auto;
}
```

+++

### CSS-formateringsmönster och bästa praxis

Det adaptiva Forms-blocket följer specifika CSS-mönster som säkerställer att alla komponenter har bibehållna, prestanda och enhetlig formatering.

+++ Primära formateringsmönster

**Formulärbehållare på blocknivå**: Använd den primära formulärbehållaren som mål för övergripande layout- och bakgrundsformat:

```css
.form {
    /* Form-wide styles */
    max-width: 800px;
    margin: 0 auto;
    background-color: var(--form-background-color);
    padding: var(--form-padding);
    border-radius: var(--form-card-border-radius);
}
```

**Komponentomslutningsmönster**: Målspecifika fälttyper som använder konsekventa omslutningsklasser:

```css
/* Text input fields */
.form .text-wrapper input {
    padding: var(--form-input-padding);
    border: var(--form-input-border-size) solid var(--form-input-border-color);
    font-size: var(--form-input-font-size);
    border-radius: 4px;
    width: 100%;
}

/* Email input fields */
.form .email-wrapper input {
    padding: var(--form-input-padding);
    border: var(--form-input-border-size) solid var(--form-input-border-color);
    font-size: var(--form-input-font-size);
}

/* Button styling */
.form .button-wrapper button {
    background-color: var(--form-button-background-color);
    color: var(--form-button-color);
    padding: var(--form-button-padding);
    border: var(--form-button-border);
    font-size: var(--form-button-font-size);
    border-radius: 4px;
    cursor: pointer;
    transition: background-color 0.2s ease;
}

.form .button-wrapper button:hover {
    background-color: var(--form-button-background-hover-color);
}
```

+++

+++ Avancerade anpassningsmönster

**Fältspecifik målgruppsanpassning**: Ange enskilda fält efter namn för unika formateringskrav:

```css
/* Style specific fields */
.form .field-email input {
    background-image: url('data:image/svg+xml;...'); /* Email icon */
    background-repeat: no-repeat;
    background-position: right 12px center;
    padding-right: 40px;
}

.form .field-phone input {
    text-align: center;
    letter-spacing: 1px;
    font-family: monospace;
}
```

**Statusbaserad formatering**: Implementera validering och interaktionstillstånd:

```css
/* Validation states */
.form .field-wrapper[data-valid="false"] input {
    border-color: var(--form-error-color);
    box-shadow: 0 0 0 2px rgba(255, 95, 63, 0.1);
}

.form .field-wrapper[data-valid="true"] input {
    border-color: #28a745;
    box-shadow: 0 0 0 2px rgba(40, 167, 69, 0.1);
}

/* Focus states */
.form .text-wrapper input:focus,
.form .email-wrapper input:focus {
    outline: none;
    border-color: var(--button-primary-color);
    box-shadow: 0 0 0 2px rgba(95, 141, 218, 0.2);
}
```

+++


## Komponentstruktur

Det adaptiva Forms-blocket erbjuder en enhetlig HTML-struktur för olika formulärelement, vilket gör det enklare att formatera och hantera. Du kan ändra komponenterna med CSS i formateringssyfte.

+++ Allmänna komponenter (utom listrutor, alternativknappar och kryssrutegrupper):

Alla formulärfält, utom listrutor, alternativgrupper och kryssrutegrupper, har följande HTML-struktur:

#### HTML-struktur för allmänna komponenter

```HTML
  <div class="{Type}-wrapper field-{Name}   field-wrapper" data-required={Required}>
     <label for="{FieldId}" class="field-label">First   Name</label>
     <input type="{Type}" placeholder="{Placeholder}"   maxlength="{Max}" id={FieldId}" name="{Name}"   aria-describedby="{FieldId}-description">
     <div class="field-description" aria-live="polite"  id="{FieldId}-description">
      Hint - First name should be minimum 3 characters  and a maximum of 10 characters.
     </div>
  </div>
```

- Klasser: div-elementet har flera klasser för att rikta specifika element och format. Du kräver att klasserna `{Type}-wrapper` eller `field-{Name}` utvecklar en CSS-väljare för att formatera ett formulärfält:
- {Type}: Identifierar komponenten efter fälttyp. Exempel: text (text-wrapper), tal (number-wrapper), datum (date-wrapper).
- {Name}: Identifierar komponenten efter namn. Fältets namn kan bara innehålla alfanumeriska tecken, de flera på varandra följande strecken i namnet ersätts med ett enda streck `(-)` och inledande och avslutande streck i ett fältnamn tas bort. Förnamn (field-first-name field-wrapper).
- {FieldId}: Det är en unik identifierare för fältet, som genereras automatiskt.
- {Required}: Det är ett booleskt värde som anger om fältet är obligatoriskt.
- Etikett: Elementet `label` innehåller en beskrivande text för fältet och associerar det med indataelementet med attributet `for`.
- Indata: Elementet `input` definierar vilken typ av data som ska anges. Till exempel text, tal, e-post.
- Beskrivning (valfritt): `div` med klassen `field-description` innehåller ytterligare information eller instruktioner för användaren.

**Exempel på HTML-struktur**

```HTML
<div class="text-wrapper field-first-name field-wrapper" data-required="true">
  <label for="firstName" class="field-label">First Name</label>
  <input type="text" placeholder="Enter your first name" maxlength="50" id="firstName" name="firstName" aria-describedby="firstName-description">
  <div class="field-description" aria-live="polite" id="firstName-description">
    Please enter your legal first name.
  </div>
</div>
```

#### CSS-väljare för allmänna komponenter

```css
/* Primary Pattern: Target field wrapper by type */
.form .{Type}-wrapper {
    /* Container styling for specific field types */
    margin-bottom: 1rem;
    border-radius: 4px;
}

/* Primary Pattern: Target input fields within wrapper */
.form .{Type}-wrapper input {
    /* Input field styling using CSS custom properties */
    border: var(--form-input-border-size) solid var(--form-input-border-color);
    padding: var(--form-input-padding);
    border-radius: 4px;
    width: 100%;
    font-size: var(--form-input-font-size);
}

/* Context-specific: Target element by field name when higher specificity needed */
.form .field-{Name} input {
    /* Field-specific customizations */
    /* Use this pattern for unique styling requirements */
}
```

- `.form .{Type}-wrapper`: Målar fältelementet baserat på fälttypen. `.form .text-wrapper` har till exempel alla textfältbehållare som mål.
- `.form .{Type}-wrapper input`: Målar de faktiska indataelementen i wrapper. Det här är det rekommenderade mönstret för att formatera formulärindata.
- `.form .field-{Name}`: Målelement baserat på det specifika fältnamnet. `.form .field-first-name` anger till exempel fältbehållaren Förnamn som mål. Använd `.form .field-{Name} input` för att ange indataelementet som mål specifikt.
- **Undvik**: `main .form form .{Type}-wrapper` - Detta skapar onödig CSS-specificitet och är svårare att underhålla.

**Exempel på CSS-väljare för allmänna komponenter**

```css
/* Primary Pattern: Target all text input fields */
.form .text-wrapper input {
    border: var(--form-input-border-size) solid var(--form-input-border-color);
    padding: var(--form-input-padding);
    border-radius: 4px;
    width: 100%;
    font-size: var(--form-input-font-size);
    background-color: var(--form-input-background-color);
}

/* Context-specific: Target field by name when higher specificity needed */
.form .field-first-name input {
    text-transform: capitalize;
    border-color: var(--button-primary-color);
}

/* Alternative with main context if needed */
main .form .text-wrapper input {
    /* Use only when you need higher specificity */
    color: var(--form-label-color);
}
```

+++

+++ Listrutekomponent

I listrutor används elementet `select` i stället för ett `input`-element:

#### HTML-struktur för nedrullningskomponent

```HTML
<div class="{Type}-wrapper field-{Name} field-wrapper" data-required={Required}>
   <label for="{FieldId}" class="field-label">First Name</label>
   <input type="{Type}" placeholder="{Placeholder}" maxlength="{Max}" id={FieldId}" name="{Name}" aria-describedby="{FieldId}-description">
   <div class="field-description" aria-live="polite" id="{FieldId}-description">
    Hint - First name should be minimum 3 characters and a maximum of 10 characters.
   </div>
</div>
```

**Exempel på HTML-struktur**

```HTML
<div class="drop-down-wrapper field-country field-wrapper" data-required="true">
  <label for="country" class="field-label">Country</label>
  <select id="country" name="country">
    <option value="">Select Country</option>
    <option value="US">United States</option>
    <option value="CA">Canada</option>
  </select>
  <div class="field-description" aria-live="polite" id="country-description">
    Please select your country of residence.
  </div>
</div>
```

#### CSS-väljare för nedrullningskomponent

Följande CSS visar några exempel på CSS-väljare för nedrullningsbara komponenter.

```css
/* Primary Pattern: Target the dropdown wrapper */
.form .drop-down-wrapper {
    /* Container layout using flexbox */
    display: flex;
    flex-direction: column;
    margin-bottom: var(--form-field-vert-gap);
}

/* Target the select element */
.form .drop-down-wrapper select {
    border: var(--form-input-border-size) solid var(--form-input-border-color);
    padding: var(--form-input-padding);
    border-radius: 4px;
    background-color: var(--form-input-background-color);
    font-size: var(--form-input-font-size);
    color: var(--form-label-color);
}

/* Style the label */
.form .drop-down-wrapper .field-label {
    margin-bottom: 5px;
    font-weight: var(--form-label-font-weight);
    color: var(--form-label-color);
    font-size: var(--form-label-font-size);
}
```

- Ange som mål för wrapper: Den första väljaren (`.drop-down-wrapper`) anger det yttre wrapper-elementet som mål, vilket garanterar att formaten tillämpas på hela listrutekomponenten.
- Flexbox Layout: Flexbox ordnar etiketten, listrutan och beskrivningen lodrätt för en ren layout.
- Etikettformatering: Etiketten sticker ut med en större teckensnittsvikt och en liten marginal.
- Formatering i listrutor: Elementet `select` får en kantlinje, utfyllnad och rundade hörn för en elegant look.
- Bakgrundsfärg: En konsekvent bakgrundsfärg ställs in för visuell harmoni.
- Anpassning av pilar: Valfria format döljer den nedrullningsbara standardpilen och skapar en anpassad pil med Unicode-tecken och placering.

+++

+++ Alternativgrupper

Ungdomsgrupper har en egen HTML-struktur och CSS-struktur, precis som komponenter i listrutor:

#### HTML Structure of Radio Group

```HTML
<fieldset class="radio-group-wrapper field-{Name} field-wrapper" id="{FieldId}" name="{Name}" data-required="{Required}">
   <legend for="{FieldId}" class="field-label">....</legend>
   <% for each radio in Group %>
   <div class="radio-wrapper field-{Name}">
      <input type="radio" value="" id="{UniqueId}" data-field-type="radio-group" name="{FieldId}">
      <label for="{UniqueId}" class="field-label">...</label>
   </div>
   <% end for %>
</fieldset>
```

**Exempel på HTML-struktur**

```HTML
<fieldset class="radio-group-wrapper field-color field-wrapper" id="color_preference" name="color_preference" data-required="true">
  <legend for="color_preference" class="field-label">Favorite Color:</legend>
  <% for each radio in Group %>
    <div class="radio-wrapper field-color">
      <input type="radio" value="red" id="color_red" data-field-type="radio-group" name="color_preference">
      <label for="color_red" class="field-label">Red</label>
    </div>
    <div class="radio-wrapper field-color">
      <input type="radio" value="green" id="color_green" data-field-type="radio-group" name="color_preference">
      <label for="color_green" class="field-label">Green</label>
    </div>
    <div class="radio-wrapper field-color">
      <input type="radio" value="blue" id="color_blue" data-field-type="radio-group" name="color_preference">
      <label for="color_blue" class="field-label">Blue</label>
    </div>
  <% end for %>
</fieldset>
```

#### CSS-väljare för alternativknappar

- Ange fältuppsättningen

```css
/* Target radio group container */
.form .radio-group-wrapper {
    border: var(--form-input-border-size) solid var(--form-input-border-color);
    padding: var(--form-input-padding);
    border-radius: 4px;
    margin-bottom: var(--form-field-vert-gap);
}
```

Den här väljaren anger alla fältuppsättningar med klassen Radio-Group-wrapper som mål. Det är användbart om du vill använda allmänna format på hela alternativgruppen.

- Egenskaper för alternativknappar

```css
/* Target radio button labels */
.form .radio-wrapper label {
    font-weight: var(--form-label-font-weight);
    margin-right: 10px;
    color: var(--form-label-color);
    font-size: var(--form-label-font-size);
    cursor: pointer;
}
```

- Ange alla alternativknappsetiketter för ett specifikt fält baserat på dess namn

```css
/* Target all radio button labels within a specific fieldset based on its name */
.form .field-color .radio-wrapper label {
    /* Field-specific radio label customizations */
    /* Add your custom styles here */
}
```

+++

+++ Kryssrutegrupper

#### HTML Structure of Checkbox Group

```HTML
<fieldset class="checkbox-group-wrapper field-{Name} field-wrapper" id="{FieldId}" name="{Name}" data-required="{Required}">
   <legend for="{FieldId}" class="field-label">....</legend>
   <% for each radio in Group %>
   <div class="checkbox-wrapper field-{Name}">
      <input type="checkbox" value="" id="{UniqueId}" data-field-type="checkbox-group" name="{FieldId}">
      <label for="{UniqueId}" class="field-label">...</label>
   </div>
   <% end for %>
</fieldset>
```

**Exempel på HTML-struktur**

```HTML
<fieldset class="checkbox-group-wrapper field-topping field-wrapper" id="topping_preference" name="topping_preference" data-required="false">
  <legend for="topping_preference" class="field-label">Pizza Toppings:</legend>
  <div class="checkbox-wrapper field-topping">
    <input type="checkbox" value="pepperoni" id="topping_pepperoni" data-field-type="checkbox-group" name="topping_preference">
    <label for="topping_pepperoni" class="field-label">Pepperoni</label>
  </div>
  <div class="checkbox-wrapper field-topping">
    <input type="checkbox" value="mushrooms" id="topping_mushrooms" data-field-type="checkbox-group" name="topping_preference">
    <label for="topping_mushrooms" class="field-label">Mushrooms</label>
  </div>
  <div class="checkbox-wrapper field-topping">
    <input type="checkbox" value="onions" id="topping_onions" data-field-type="checkbox-group" name="topping_preference">
    <label for="topping_onions" class="field-label">Onions</label>
  </div>
</fieldset>
```

#### CSS-väljare för kryssrutegrupper

- Ange som mål för den yttre omslutningen: Dessa väljare har de yttre behållarna för både alternativknappar och kryssrutegrupper som mål, vilket gör att du kan använda allmänna format för hela gruppstrukturen. Det här är användbart när du vill ange avstånd, justering eller andra layoutrelaterade egenskaper.

```css
/* Primary Pattern: Targets radio group wrappers */
.form .radio-group-wrapper {
    margin-bottom: var(--form-field-vert-gap); /* Adds space between radio groups */
    display: flex;
    flex-direction: column;
    border: var(--form-fieldset-border);
    padding: var(--form-input-padding);
}

/* Primary Pattern: Targets checkbox group wrappers */
.form .checkbox-group-wrapper {
    margin-bottom: var(--form-field-vert-gap); /* Adds space between checkbox groups */
    display: flex;
    flex-direction: column;
    border: var(--form-fieldset-border);
    padding: var(--form-input-padding);
}
```

- Målgruppsetiketter: Den här väljaren anger elementet `.field-label` som mål i gruppomslutningar för både alternativknappar och kryssrutor. På så sätt kan du formatera etiketterna specifikt för dessa grupper, vilket kan få dem att sticka ut mer.

```css
/* Primary Pattern: Target group labels */
.form .radio-group-wrapper legend,
.form .checkbox-group-wrapper legend {
    font-weight: var(--form-title-font-weight); /* Makes the group label bold */
    margin-bottom: 0.5rem;
    font-size: var(--form-fieldset-legend-font-size);
    color: var(--form-fieldset-legend-color);
    padding: var(--form-fieldset-legend-padding);
    border: var(--form-fieldset-legend-border);
}
```

- Indata och etiketter för enskilda användare: Dessa väljare ger mer exakt kontroll över enskilda alternativknappar, kryssrutor och tillhörande etiketter. Du kan använda dessa för att justera storlek, avstånd eller använda mer distinkta visuella format.

```css
/* Primary Pattern: Styling radio buttons */
.form .radio-group-wrapper input[type="radio"] {
    margin-right: 8px; /* Adds space between the input and its label */
    margin-bottom: 4px;
    cursor: pointer;
}

/* Primary Pattern: Styling radio button labels */
.form .radio-group-wrapper label {
    font-size: var(--form-label-font-size); /* Changes the label font size */
    color: var(--form-label-color);
    font-weight: var(--form-label-font-weight);
    display: flex;
    align-items: center;
    cursor: pointer;
}

/* Primary Pattern: Styling checkboxes */
.form .checkbox-group-wrapper input[type="checkbox"] {
    margin-right: 8px; /* Adds space between the input and its label */
    margin-bottom: 4px;
    cursor: pointer;
}

/* Primary Pattern: Styling checkbox labels */
.form .checkbox-group-wrapper label {
    font-size: var(--form-label-font-size); /* Changes the label font size */
    color: var(--form-label-color);
    font-weight: var(--form-label-font-weight);
    display: flex;
    align-items: center;
    cursor: pointer;
}
```

- Anpassa utseendet på alternativknappar och kryssrutor: Den här tekniken döljer standardindata och använder `:before` och `:after` pseudoelement för att skapa anpassade bilder som ändrar utseende baserat på markerat läge.

```css
/* Hide the default radio button or checkbox */
.form .radio-group-wrapper input[type="radio"],
.form .checkbox-group-wrapper input[type="checkbox"] {
    opacity: 0;
    position: absolute;
    width: 1px;
    height: 1px;
}

/* Create a custom radio button */
.form .radio-group-wrapper input[type="radio"] + label::before {
    content: '';
    display: inline-block;
    width: 16px;
    height: 16px;
    border: 2px solid var(--form-input-border-color);
    border-radius: 50%;
    margin-right: 8px;
    background-color: var(--form-input-background-color);
    transition: all 0.2s ease;
}

.form .radio-group-wrapper input[type="radio"]:checked + label::before {
    background-color: var(--button-primary-color);
    border-color: var(--button-primary-color);
    box-shadow: inset 0 0 0 3px var(--form-input-background-color);
}

/* Create a custom checkbox */
.form .checkbox-group-wrapper input[type="checkbox"] + label::before {
    content: '';
    display: inline-block;
    width: 16px;
    height: 16px;
    border: 2px solid var(--form-input-border-color);
    border-radius: 2px;
    margin-right: 8px;
    background-color: var(--form-input-background-color);
    transition: all 0.2s ease;
}

.form .checkbox-group-wrapper input[type="checkbox"]:checked + label::before {
    background-color: var(--button-primary-color);
    border-color: var(--button-primary-color);
    background-image: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 16 16"><path fill="white" d="M13.854 3.646a.5.5 0 0 1 0 .708l-7 7a.5.5 0 0 1-.708 0l-3.5-3.5a.5.5 0 1 1 .708-.708L6.5 10.293l6.646-6.647a.5.5 0 0 1 .708 0z"/></svg>');
    background-repeat: no-repeat;
    background-position: center;
}
```

+++

+++ Panel-/behållarkomponenter

#### HTML-struktur för paneler/behållarkomponenter

```HTML
<fieldset class="panel-wrapper field-{PanelName} field-wrapper">
  <legend for="{id}" class="field-label" data-visible="false">bannerComponent</legend>
  <div class="{Type}-wrapper field-{Name} field-wrapper">
    <label for="{FieldId}" class="field-label">First Name</label>
    <input type="{Type}" placeholder="{Placeholder}" maxlength="{Max}" id={FieldId}" name="{Name}">
    <div class="field-description" aria-live="polite" id="{FieldId}-description">
      Hint - First name should be minimum 3 characters and a maximum of 10 characters.
    </div>
  </div>
</fieldset>
```

**Exempel på HTML-struktur**

```HTML
<fieldset class="panel-wrapper field-login field-wrapper">
  <legend for="login" class="field-label" data-visible="false">Login Information</legend>
  <div class="text-wrapper field-username field-wrapper">
    <label for="username" class="field-label">Username</label>
    <input type="text" placeholder="Enter your username" maxlength="50" id="username" name="username">
    <div class="field-description" aria-live="polite" id="username-description">
      Please enter your username or email address.
    </div>
  </div>
  <div class="password-wrapper field-password field-wrapper">
    <label for="password" class="field-label">Password</label>
    <input type="password" placeholder="Enter your password" maxlength="20" id="password" name="password">
    <div class="field-description" aria-live="polite" id="password-description">
      Your password must be at least 8 characters long.
    </div>
  </div>
</fieldset>
```

- Fältuppsättningselementet fungerar som panelbehållare med klassens panelwrapper och ytterligare klasser för formatering baserat på panelnamnet (fältinloggning).
- Förklaringselementet (`<legend>`) fungerar som panelrubrik med texten Inloggningsinformation och klassfältets etikett. Attributet data-visible=&quot;false&quot; kan användas med JavaScript för att styra visningen av titeln.
- I fältuppsättningen, multipel.{Type}-wrapper-element (.text-wrapper och .password-wrapper i det här fallet) representerar enskilda formulärfält på panelen.
- Varje wrapper innehåller en etikett, ett inmatningsfält och en beskrivning, som liknar de föregående exemplen.


#### Exempel på CSS-väljare för panel-/behållarkomponenter

1. Panelen:

```CSS
  /- Target the entire panel container */
  main .form form .panel-wrapper {
    /- Add your styles here (e.g., border, padding, background color) */
    border: 1px solid #ccc;
    padding: 15px;
    border-radius: 4px;
    margin-bottom: 20px;
 }
```

- `.panel-wrapper`-väljaren formaterar alla element med klassens panelwrapper, vilket ger ett konsekvent utseende för alla paneler.

1. Ange paneltiteln som mål:

```CSS
  /- Target the legend element (panel title) */
  .panel-wrapper legend {
    /- Add your styles here (e.g., font-weight, font-size) */
    font-weight: bold;
    font-size: 16px;
    padding-bottom: 5px;
    margin-bottom: 10px;
    border-bottom: 1px solid #ddd; /- Optional: create a separation line */
  }
```

- `.panel-wrapper legend`-väljaren formaterar förklaringselementet på panelen, så att titeln sticker ut visuellt.


1. Ange enskilda fält som mål på panelen:

```CSS
/- Target all form field wrappers within a panel */
main .form form .panel-wrapper .{Type}-wrapper {
  /- Add your styles here (e.g., margin) */
  margin-bottom: 10px;
}
```

- `.panel-wrapper .{Type}-wrapper`-väljaren anger alla omslutningar med klassen `.{Type}-wrapper` på panelen som mål, vilket gör att du kan formatera mellanrummet mellan formulärfält.

1. Målspecifika fält (valfritt):

```CSS
  /- Target the username field wrapper */
  main .form form .panel-wrapper .text-wrapper.field-username {
    /- Add your styles here (specific to username field) */
  }

  /- Target the password field wrapper */
  main .form form .panel-wrapper .password-wrapper.field-password {
    /- Add your styles here (specific to password field) */
  }
```

- Dessa väljare gör att du kan rikta in dig på specifika fältbrytningar på panelen för unik formatering, t.ex. markera användarnamnsfältet.


+++

+++ Repeterbar panel

#### HTML-struktur för en upprepningsbar panel

```HTML
<fieldset class="panel-wrapper field-{PanelName} field-wrapper">
  <legend for="{id}" class="field-label" data-visible="false">bannerComponent</legend>
  <div class="{Type}-wrapper field-{Name} field-wrapper">
    <label for="{FieldId}" class="field-label">First Name</label>
    <input type="{Type}" placeholder="{Placeholder}" maxlength="{Max}" id={FieldId}" name="{Name}">
    <div class="field-description" aria-live="polite" id="{FieldId}-description">
      Hint - First name should be minimum 3 characters and a maximum of 10 characters.
    </div>
</fieldset>
```

**Exempel på HTML-struktur**

```HTML
<fieldset class="panel-wrapper field-contact field-wrapper" data-repeatable="true">
  <legend for="contact-1" class="field-label" data-visible="false">Contact Information</legend>
  <div class="text-wrapper field-name field-wrapper">
    <label for="name-1" class="field-label">Name</label>
    <input type="text" placeholder="Enter your name" maxlength="50" id="name-1" name="contacts[0].name">
    <div class="field-description" aria-live="polite" id="name-1-description">
      Please enter your full name.
    </div>
  </div>
  <div class="email-wrapper field-email field-wrapper">
    <label for="email-1" class="field-label">Email</label>
    <input type="email" placeholder="Enter your email address" maxlength="100" id="email-1" name="contacts[0].email">
    <div class="field-description" aria-live="polite" id="email-1-description">
      Please enter a valid email address.
    </div>
  </div>
</fieldset>

<fieldset class="panel-wrapper field-contact field-wrapper" data-repeatable="true">
  <legend for="contact-2" class="field-label" data-visible="false">Contact Information</legend>
  <div class="text-wrapper field-name field-wrapper">
    <label for="name-2" class="field-label">Name</label>
    <input type="text" placeholder="Enter your name" maxlength="50" id="name-2" name="contacts[1].name">
    <div class="field-description" aria-live="polite" id="name-2-description">
      Please enter your full name.
    </div>
  </div>
  <div class="email-wrapper field-email field-wrapper">
    <label for="email-2" class="field-label">Email</label>
    <input type="email" placeholder="Enter your email address" maxlength="100" id="email-2" name="contacts[1].email">
    <div class="field-description" aria-live="polite" id="email-2-description">
      Please enter a valid email address.
    </div>
  </div>
</fieldset>
```

Varje panel har samma struktur som exemplet med en panel, med ytterligare attribut:

- data-repetable=&quot;true&quot;: Det här attributet anger att panelen kan upprepas dynamiskt med JavaScript eller ett ramverk.

- Unika ID:n och namn: Varje element i panelen har ett unikt ID (till exempel name-1, email-1) och name-attribut baserat på panelens indexvärde (till exempel name=&quot;contact[0].name&quot;). Detta gör att data kan samlas in korrekt när flera paneler skickas.


#### CSS-väljare för en upprepningsbar panel

- Alla upprepningsbara paneler som mål:

```CSS
  /- Target all panels with the repeatable attribute */
 main .form form .panel-wrapper[data-repeatable="true"] {
    /- Add your styles here (e.g., border, margin) */
    border: 1px solid #ccc;
    padding: 15px;
    border-radius: 4px;
    margin-bottom: 20px;
  }
```

Väljaren formaterar alla paneler som kan upprepas, vilket ger ett konsekvent utseende och känsla.


- Ange enskilda fält som mål på en panel:

```CSS
/- Target all form field wrappers within a repeatable panel */
main .form form .panel-wrapper[data-repeatable="true"] .{Type}-wrapper {
  /- Add your styles here (e.g., margin) */
  margin-bottom: 10px;
}
```

Den här väljaren formaterar alla fältomslutningar på en repeterbar panel, vilket ger ett konsekvent avstånd mellan fälten.

- Ange specifika fält som mål (inom en panel):

```CSS
/- Target the name field wrapper within the first panel */
main .form form .panel-wrapper[data-repeatable="true"][data-index="0"] .text-wrapper.field-name {
  /- Add your styles here (specific to first name field) */
}

/- Target all
```


+++


+++ Bifogad fil

#### HTML-struktur för bifogad fil

```HTML
<div class="file-wrapper field-{FileName} field-wrapper">
  <legend for="{id}" class="field-label" data-visible="false"> File Attachment </legend>
  <div class="file-drag-area">
    <div class="file-dragIcon"></div>
    <div class="file-dragText">Drag and Drop To Upload</div>
    <button class="file-attachButton" type="button">Attach</button>
    <input type="file" accept="audio/*, video/*, image/*, text/*, application/pdf" id="{id}" name="{FileName}" autocomplete="off" multiple="" required="required">
  </div>
  <div class="files-list">
    <div data-index="0" class="file-description">
      <span class="file-description-name">ClaimForm.pdf</span>
      <span class="file-description-size">26 kb</span>
      <button class="file-description-remove" type="button"></button>
    </div>
  </div>
</div>
```

**Exempel på HTML-struktur**


```HTML
<div class="file-wrapper field-claim_form field-wrapper">
  <legend for="claim_form" class="field-label" data-visible="false">File Attachment</legend>
  <div class="file-drag-area">
    <div class="file-dragIcon"></div>
    <div class="file-dragText">Drag and Drop To Upload</div>
    <button class="file-attachButton" type="button">Attach</button>
  </div>
  <input type="file" accept="audio/*, video/*, image/*, text/*, application/pdf" id="claim_form"
         name="claim_form" autocomplete="off" multiple="" required="required" data-max-file-size="2MB">
  <div class="files-list">
    </div>
</div>
```

- Klassattributet använder det angivna namnet för den bifogade filen (claim_form).
- Attributen id och name för indataelementet matchar namnet på den bifogade filen (claim_form).
- Avsnittet med fillistan är inledningsvis tomt. Den fylls i dynamiskt med JavaScript när filer överförs.


#### CSS-väljare för komponenten Bifogad fil

- Målkomponenten för hela den bifogade filen:

```CSS
/- Target the entire file attachment component */
main .form form .file-wrapper {
  /- Add your styles here (e.g., border, padding) */
  border: 1px solid #ccc;
  padding: 15px;
  border-radius: 4px;
  margin-bottom: 20px;
}
```

Den här väljaren formaterar hela den bifogade filkomponenten, inklusive teckenförklaringen, dragningsområdet, inmatningsfältet och listan.

- Målinriktade specifika element:

```CSS
/- Target the drag and drop area */
main .form form .file-wrapper .file-drag-area {
  /- Add your styles here (e.g., background color, border) */
  background-color: #f0f0f0;
  border: 1px dashed #ddd;
  padding: 10px;
  text-align: center;
}

/- Target the file input element */
main .form form .file-wrapper input[type="file"] {
  /- Add your styles here (e.g., hide the default input) */
  display: none;
}

/- Target individual file descriptions within the list (populated dynamically) */
main .form form .file-wrapper .files-list .file-description {
  /- Add your styles here (e.g., margin, display) */
  display: flex;
  justify-content: space-between;
  margin-bottom: 5px;
}

/- Target the file name within the description */
main .form form .file-wrapper .files-list .file-description .file-description-name {
  /- Add your styles here (e.g., font-weight) */
  font-weight: bold;
}
```

Dessa väljare gör att du kan formatera olika delar av den bifogade filkomponenten individuellt. Du kan justera formaten så att de matchar dina designinställningar.

+++



## Formatkomponenter

Du kan formatera formulärfält baserat på deras specifika typ (`{Type}-wrapper`) eller enskilda namn (`field-{Name}`). På så sätt får du bättre kontroll över och anpassning av formulärets utseende.

+++ Formatering baserad på fälttyp

Du kan använda CSS-väljare för att ange specifika fälttyper och använda format på ett konsekvent sätt.

#### HTML Structure

```HTML
<div class="{Type}-wrapper field-{Name} field-wrapper" data-required={Required}>
   <label for="{FieldId}" class="field-label">First Name</label>
   <input type="{Type}" placeholder="{Placeholder}" maxlength="{Max}" id={FieldId}" name="{Name}" aria-describedby="{FieldId}-description">
   <div class="field-description" aria-live="polite" id="{FieldId}-description">
    Hint - First name should be minimum 3 characters and a maximum of 10 characters.
   </div>
</div>
```

**Exempel på HTML-struktur**

```HTML
<div class="text-wrapper field-name field-wrapper" data-required="true">
  <label for="name" class="field-label">Name</label>
  <input type="text" placeholder="Enter your name" maxlength="50" id="name" name="name">
</div>

<div class="number-wrapper field-age field-wrapper" data-required="true">
  <label for="age" class="field-label">Age</label>
  <input type="number" placeholder="Enter your age" id="age" name="age">
</div>

<div class="email-wrapper field-email field-wrapper" data-required="true">
  <label for="email" class="field-label">Email Address</label>
  <input type="email" placeholder="Enter your email" id="email" name="email">
</div>
```

- Varje fält kapslas i ett `div`-element med flera klasser:
   - `{Type}-wrapper`: Identifierar fälttypen. Exempel: `form-text-wrapper`, `form-number-wrapper`, `form-email-wrapper`.
   - `field-{Name}`: Identifierar fältet med dess namn. Till exempel `form-name`, `form-age`, `form-email`.
   - `field-wrapper`: En generisk klass för alla fältbrytare.
- Attributet `data-required` anger om fältet är obligatoriskt eller valfritt.
- Varje fält har en motsvarande etikett, indataelement och eventuella ytterligare element som platshållare och beskrivningar.




#### Exempel på CSS-väljare

```CSS
/- Primary Pattern: Target all text input fields */
.form .text-wrapper input {
  /- Add your styles here */
  width: 100%;
  padding: var(--form-input-padding);
}

/- Primary Pattern: Target all number input fields */
.form .number-wrapper input {
  /- Add your styles here */
  letter-spacing: 2px; /- Example for adding letter spacing to all number fields */
  text-align: center;
}
```
+++

+++ Formatering baserad på fältnamn

Du kan också ange enskilda fält som mål efter namn för att använda unika format.

#### HTML Structure

```HTML
<div class="{Type}-wrapper field-{Name} field-wrapper" data-required={Required}>
   <label for="{FieldId}" class="field-label">First Name</label>
   <input type="{Type}" placeholder="{Placeholder}" maxlength="{Max}" id="{FieldId}" name="{Name}" aria-describedby="{FieldId}-description">
   <div class="field-description" aria-live="polite" id="{FieldId}-description">
    Hint - Enter the 6 digit number sent to your mobile number.
   </div>
</div>
```

**Exempel på HTML-struktur**

```HTML
<div class="number-wrapper field-otp field-wrapper" data-required="true">
  <label for="otp" class="field-label">OTP</label>
  <input type="number" placeholder="Enter your OTP" maxlength="6" id="otp" name="otp" aria-describedby="otp-description">
  <div class="field-description" aria-live="polite" id="otp-description">
    Hint - Enter the 6 digit number sent to your mobile number.
   </div>
</div>
```


#### Exempel på CSS-väljare

```CSS
/- Primary Pattern: Target specific field by name */
.form .field-otp input {
   letter-spacing: 2px;
   text-align: center;
   font-family: monospace;
}

/- Context-specific: Use higher specificity when needed */
main .form .field-otp input {
   /- Use only when you need to override other styles */
   font-weight: bold;
}
```

Den här CSS-koden har alla indataelement som finns i ett element som har klassen `field-otp` som mål. Edge Delivery Services formulärstruktur följer de adaptiva blockkonventionerna för Forms, där behållare är markerade med fältspecifika klasser som &quot;field-otp&quot; för fält med namnet &quot;otp&quot;.


## CSS-filstruktur och implementering

### **Referensimplementering**

Den fullständiga formulärformatsreferensen finns i AEM Forms-databasen för mallar:

```
https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/blocks/form/form.css
```

Den här filen fungerar som en kanonisk implementering av det anpassade CSS-egenskapssystemet och utgör grunden för all formulärformatering. Den innehåller omfattande definitioner för alla CSS-variabler, komponentformateringsmönster och implementeringar av responsiv design.

+++

+++ Projektintegrering

I ditt Edge Delivery Services-projekt kan du implementera formulärformat på följande strukturerade sätt:

```
/blocks/form/form.css          // Core form block styles (copied from boilerplate)
/styles/styles.css             // Global site styles and CSS variable overrides
/styles/lazy-styles.css        // Additional component enhancements
```

+++

+++ Genomförandestrategi

**Åsidosätter anpassade CSS-egenskaper**: Åsidosätt formulärvariabler i globala format för att implementera varumärkesspecifik tema:

```css
/* In /styles/styles.css */
:root {
    /* Brand-specific overrides */
    --button-primary-color: #your-brand-color;
    --form-background-color: #your-background;
    --label-color: #your-text-color;
}
```

**Komponentspecifika anpassningar**:
Lägg till komponentspecifik formatering med bibehållet CSS-variabelsystem:

```css
/* Enhanced component styling */
.form .text-wrapper input {
    border-radius: var(--form-card-border-radius);
    transition: all 0.2s ease;
}

.form .text-wrapper input:focus {
    transform: translateY(-1px);
    box-shadow: 0 0 0 3px rgba(var(--button-primary-color), 0.1);
}
```

**Responsiv designintegrering**: Använd anpassade CSS-egenskaper i mediefrågor för konsekvent responsivt beteende:

```css
@media (max-width: 768px) {
    :root {
        --form-input-padding: 0.875rem;
        --form-field-vert-gap: 1rem;
        --form-padding: 1rem;
    }
}
```

+++

### Exempel på komplett formatimplementering

I det här avsnittet visas hur du skapar ett modernt, varumärkesprofilerat formulär med anpassade CSS-egenskaper. Implementeringen är uppdelad i tydliga underavsnitt för enklare förståelse och navigering.



+++ &#x200B;1. Variabler för varumärkestema

Definiera varumärkets färgpalett, mellanrum och typografi med hjälp av anpassade CSS-egenskaper.

```css
/* Custom brand theme */
:root {
  /* Brand color system */
  --brand-primary: #2563eb;
  --brand-secondary: #64748b;
  --brand-success: #059669;
  --brand-error: #dc2626;
  --brand-background: #f8fafc;
  
  /* Override form variables */
  --background-color-primary: #ffffff;
  --button-primary-color: var(--brand-primary);
  --button-primary-hover-color: #1d4ed8;
  --form-error-color: var(--brand-error);
  --form-background-color: var(--brand-background);
  --label-color: var(--brand-secondary);
  --border-color: #d1d5db;
  
  /* Enhanced spacing */
  --form-input-padding: 1rem;
  --form-field-vert-gap: 1.5rem;
  --form-padding: 2rem;
  
  /* Modern typography */
  --form-font-size-s: 16px;
  --form-label-font-weight: 500;
}
```


+++

+++ &#x200B;2. Formulärbehållarformatering

Använd en modern bakgrund, kantradie och skugga i formulärbehållaren för en visuellt tilltalande layout.


```css
/* Enhanced form container */
.form {
    background: linear-gradient(135deg, #f8fafc 0%, #f1f5f9 100%);
    border-radius: 12px;
    box-shadow: 0 10px 25px rgba(0, 0, 0, 0.05);
    max-width: 600px;
    margin: 2rem auto;
    overflow: hidden;
}
```




+++

+++ &#x200B;3. Formatering av inmatningsfält

Formatera text-, e-post- och nummerinmatningsfält för ett rent, modernt utseende.


```css
/* Modern input styling */
.form .text-wrapper input,
.form .email-wrapper input,
.form .number-wrapper input {
    background: white;
    border: 2px solid var(--border-color);
    border-radius: 8px;
    padding: var(--form-input-padding);
    font-size: 16px;
    transition: all 0.2s ease;
    width: 100%;
}
```


+++

+++ &#x200B;4. Ytterligare anpassning

Du kan utöka formulärformateringen ytterligare genom att rikta in dig på specifika fält, lägen eller komponenter efter behov. Mer information om avancerade mönster finns i tidigare avsnitt.

```css
/* Custom brand theme */
:root {
    /* Brand color system */
    --brand-primary: #2563eb;
    --brand-secondary: #64748b;
    --brand-success: #059669;
    --brand-error: #dc2626;
    --brand-background: #f8fafc;
    
    /* Override form variables */
    --background-color-primary: #ffffff;
    --button-primary-color: var(--brand-primary);
    --button-primary-hover-color: #1d4ed8;
    --form-error-color: var(--brand-error);
    --form-background-color: var(--brand-background);
    --label-color: var(--brand-secondary);
    --border-color: #d1d5db;
    
    /* Enhanced spacing */
    --form-input-padding: 1rem;
    --form-field-vert-gap: 1.5rem;
    --form-padding: 2rem;
    
    /* Modern typography */
    --form-font-size-s: 16px;
    --form-label-font-weight: 500;
}

/* Enhanced form container */
.form {
    background: linear-gradient(135deg, #f8fafc 0%, #f1f5f9 100%);
    border-radius: 12px;
    box-shadow: 0 10px 25px rgba(0, 0, 0, 0.05);
    max-width: 600px;
    margin: 2rem auto;
    overflow: hidden;
}

/* Modern input styling */
.form .text-wrapper input,
.form .email-wrapper input,
.form .number-wrapper input {
    background: white;
    border: 2px solid var(--border-color);
    border-radius: 8px;
    padding: var(--form-input-padding);
    font-size: 16px;
    transition: all 0.2s ease;
    width: 100%;
}

.form .text-wrapper input:focus,
.form .email-wrapper input:focus,
.form .number-wrapper input:focus {
    border-color: var(--brand-primary);
    box-shadow: 0 0 0 3px rgba(37, 99, 235, 0.1);
    transform: translateY(-1px);
}

/* Enhanced button styling */
.form .button-wrapper button[type="submit"] {
    background: linear-gradient(135deg, var(--brand-primary) 0%, #1d4ed8 100%);
    color: white;
    border: none;
    border-radius: 8px;
    padding: 1rem 2rem;
    font-size: 16px;
    font-weight: 600;
    cursor: pointer;
    transition: all 0.2s ease;
    width: 100%;
    box-shadow: 0 4px 12px rgba(37, 99, 235, 0.3);
}

.form .button-wrapper button[type="submit"]:hover {
    transform: translateY(-2px);
    box-shadow: 0 6px 20px rgba(37, 99, 235, 0.4);
}
```

Denna omfattande metod visar hur anpassade CSS-egenskaper möjliggör avancerad kodning samtidigt som de strukturella integritets- och tillgänglighetsfunktionerna i det adaptiva Forms-blocksystemet bibehålls.

+++

## Felsöka CSS-problem

+++ Specifika CSS-problem

```css
/- ❌ Problem: Styles not applying */
.text-wrapper input {
  color: red;
}

/- ✅ Solution: Match or exceed existing specificity */
.form .text-wrapper input {
  color: red;
}

/- ✅ Alternative: Use higher specificity when needed */
main .form .text-wrapper input {
  color: red;
}
```

+++

+++ CSS-variabelåsidosättningsproblem

```css
/- ❌ Problem: Variables not working */
.form {
  --form-border-color: blue; /- Local scope only */
}

/- ✅ Solution: Define in root scope */
:root {
  --form-border-color: blue; /- Global scope */
}
```

+++

+++ Formulärtillståndsformat

```css
/- Validation states */
.form .field-wrapper.error input {
  border-color: var(--form-error-color);
}

.form .field-wrapper.success input {
  border-color: var(--form-success-color);
}

/- Loading state */
.form[data-submitting="true"] {
  opacity: 0.7;
  pointer-events: none;
}

/- Disabled state */
.form input:disabled {
  background-color: var(--form-input-disabled-background);
  cursor: not-allowed;
}
```

+++

+++ Vanliga väljarfel

```css
/- ❌ Incorrect: Assumes direct nesting */
.form form input {
  /- This might miss inputs in wrappers */
}

/- ✅ Correct: Target actual structure */
.form .text-wrapper input {
  /- Targets actual HTML structure */
}

/- ❌ Avoid: Unnecessary specificity */
main .form form .text-wrapper input {
  /- Too specific, harder to override */
}

/- ✅ Preferred: Balanced specificity */
.form .text-wrapper input {
  /- Easier to maintain and override */
}
```

+++



### **Komponentspecifika metodtips**


+++ Knappformat

```css
/- Primary buttons */
.form .button-wrapper button[type="submit"] {
  background-color: var(--form-focus-color);
  color: white;
  border: none;
  padding: var(--form-input-padding);
  border-radius: var(--form-border-radius);
}

/- Secondary buttons */
.form .button-wrapper button[type="reset"] {
  background-color: transparent;
  color: var(--form-text-color);
  border: 1px solid var(--form-border-color);
}
```

+++

+++ Responsiv formulärdesign

```css
/- Mobile-first approach */
.form {
  width: 100%;
  padding: 1rem;
}

/- Tablet and up */
@media (min-width: 768px) {
  .form {
    max-width: var(--form-max-width);
    padding: var(--form-padding);
  }
}
```

+++

## Sammanfattning av bästa praxis

1. **Använd anpassade CSS-egenskaper**: Utnyttja variabler för konsekventa teman
2. **Följ blockbaserad arkitektur**: Använd `.form` som primär blockväljare
3. **Undvik överspecificitet**: Använd inte `main .form form` om det inte behövs
4. **Målwrappers**: Använd `.{Type}-wrapper`-mönster för komponentmål
5. **Bevara konsekvens**: Använd samma väljarmönster i hela projektet
6. **Testa på olika enheter**: Säkerställ att formulär fungerar bra på mobiler, surfplattor och datorer
7. **Verifiera hjälpmedel**: Kontrollera att formaten inte stör skärmläsare eller tangentbordsnavigering



---
title: Anpassa tema och stil för ett AEM Forms Edge Delivery Service-formulär
description: Anpassa tema och stil för ett AEM Forms Edge Delivery Service-formulär
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: 4a3ebcf7985253ebca24e90ab57ae7eaf3e924e9
workflow-type: tm+mt
source-wordcount: '1285'
ht-degree: 0%

---


# Formatera formulärfält

Forms är avgörande för användarinteraktion på webbplatser, så att de kan mata in data. Den här handboken behandlar grunderna i hur du formaterar olika formulärfält i dialogrutan [Formulärblock](/help/edge/docs/forms/create-forms.md)som hjälper dig att skapa visuellt tilltalande och användarvänliga formulär.

## Förstå formulärfältstyper

Innan vi börjar använda en formatmall ska vi granska de vanliga formulärfälttyperna som stöds av formulärblocket:

* Indatafält: Dessa innehåller textinmatningar, e-postinmatningar, lösenordsinmatningar med mera.
* Kryssrutegrupper: Används för att välja flera alternativ.
* Alternativgrupper: Används för att endast välja ett alternativ från en grupp.
* Listrutor: Kallas även urvalsrutor, som används för att välja ett alternativ i en lista.
* Paneler/behållare: Används för att gruppera relaterade formulärelement.

## Grundläggande formatprinciper

Att förstå grundläggande CSS-koncept är avgörande innan du formaterar specifika formulärfält:

* Väljare: Med CSS-väljare kan du ange specifika HTML-element för formatering som mål. Du kan använda elementväljare, klassväljare eller ID-väljare.
* Egenskaper: CSS-egenskaper definierar elementens visuella utseende. Vanliga egenskaper för formatformulärfält är bland annat färg, bakgrundsfärg, kant, utfyllnad, marginal.
* Rutmodell: CSS-rutmodellen beskriver strukturen för element i HTML som ett innehållsområde omgivet av utfyllnad, kanter och marginaler.
* Flexbox/Grid: CSS Flexbox och stödrasterlayouter är kraftfulla verktyg för att skapa responsiv och flexibel design.

## Formatera ett formulär för formulärblock

Formulärblocket har en standardiserad HTML-struktur som förenklar processen att markera och formatera formulärkomponenter:

* **Uppdatera standardformat**: Du kan ändra standardformaten för ett formulär genom att redigera `/blocks/form/form.css file`. Den här filen innehåller omfattande formatering för ett formulär med stöd för guideformulär i flera steg. Det är viktigt att du använder anpassade CSS-variabler för enkel anpassning, underhåll och enhetlig formatering i olika formulär. Instruktioner om hur du lägger till formulärblocket i projektet finns i [skapa ett formulär](/help/edge/docs/forms/create-forms.md).

* **Anpassning**: Använd standardvärdet `forms.css` som en bas och anpassa den för att ändra utseendet och känslan hos dina formulärkomponenter, vilket gör den visuellt tilltalande och användarvänlig. Filens struktur uppmuntrar organisationen och bevarar format för formulär, vilket ger en enhetlig design på hela webbplatsen.

## Uppdelning av forms.css struktur

* **Globala variabler:** Definieras på `:root` level, dessa variabler (`--variable-name`) lagra värden som används i hela formatmallen för att underlätta konsekvensen och uppdateringarna. Dessa variabler definierar färger, teckenstorlekar, utfyllnad och andra egenskaper. Du kan deklarera dina egna globala variabler eller ändra befintliga variabler för att ändra formulärets format.

* **Universella väljarformat:** The `*` väljaren matchar alla element i formuläret, vilket säkerställer att format används på alla komponenter som standard, inklusive inställning av `box-sizing` egenskap till `border-box`.

* **Formulärformat:** I det här avsnittet fokuseras på att formatera formulärkomponenter med hjälp av väljare för att ange specifika HTML-element. Här definieras format för inmatningsfält, textområden, kryssrutor, alternativknappar, filinmatningar, formuläretiketter och beskrivningar.

* **Ställa in guiden (om tillämpligt):** Det här avsnittet är avsett för att utforma guidelayouten, ett flerstegsformulär där varje steg visas ett i taget. Den definierar format för guidebehållaren, fältuppsättningar, teckenförklaringar, navigeringsknappar och responsiva layouter.

* **Mediefrågor:** Dessa innehåller format för olika skärmstorlekar och justerar layouten och formateringen utifrån detta.

* **Övrig formatering:**: I det här avsnittet beskrivs format för lyckade eller felmeddelanden, områden för filöverföring och andra element som du kan stöta på i ett formulär.


## Komponentstruktur

Formulärblocket har en enhetlig HTML-struktur för olika formulärelement, vilket gör det enklare att formatera och hantera. Du kan ändra komponenterna med CSS i formateringssyfte.

### Allmänna komponenter (utom listrutor, alternativknappar och kryssrutegrupper):

Alla formulärfält, utom listrutor, alternativgrupper och kryssrutegrupper, har följande HTML-struktur:

#### HTML struktur

```HTML
<div class="form-{Type}-wrapper form-{Name} field-wrapper" data-required={Required}>
  <label for="{FieldId}" class="field-label">Field Label</label>
  <input type="{Type}" placeholder="{Placeholder}" maxlength="{Max}" id="{FieldId}" name="{Name}" aria-describedby="{FieldId}-description">
  <div class="field-description" aria-live="polite" id="{FieldId}-description">
    Hint - Description of the field.
  </div>
</div>
```

* Klasser: div-elementet har flera klasser för att rikta specifika element och format. Du behöver `form-{Type}-wrapper` eller `form-{Name}` klasser för att utveckla en CSS-väljare för att formatera ett formulärfält:
   * {Type}: Identifierar komponenten efter fälttyp. Exempel: text (form-text-wrapper), tal (form-number-wrapper), datum (form-date-wrapper).
   * {Name}: Identifierar komponenten efter namn. Fältets namn kan bara innehålla alfanumeriska tecken. De flera på varandra följande strecken i namnet ersätts med ett enda streck `(-)`och inledande och avslutande streck i ett fältnamn tas bort. Förnamn (form-first-name field-wrapper).
   * {FieldId}: Det är en unik identifierare för fältet, som genereras automatiskt.
   * {Required}: Det är ett booleskt värde som anger om fältet är obligatoriskt.
* Etikett: `label` -elementet innehåller en beskrivande text för fältet och associerar det med indataelementet med `for` -attribut.
* Indata: `input` -element definierar vilken typ av data som ska anges. Till exempel text, tal, e-post.
* Beskrivning (valfritt): `div` med klass `field-description` innehåller ytterligare information eller instruktioner för användaren.

**Exempel**

```HTML
<div class="form-text-wrapper form-first-name field-wrapper" data-required="true">
  <label for="firstName" class="field-label">First Name</label>
  <input type="text" placeholder="Enter your first name" maxlength="50" id="firstName" name="firstName" aria-describedby="firstName-description">
  <div class="field-description" aria-live="polite" id="firstName-description">
    Please enter your legal first name.
  </div>
</div>
```

#### CSS-väljare för allmänna komponenter

```CSS
.form-{Type}-wrapper input {
  /* Add your styles here */
  border: 1px solid #ccc;
  padding: 8px;
  border-radius: 4px;
}


.form-{Name} input {
  /* Add your styles here */
  border: 1px solid #ccc;
  padding: 8px;
  border-radius: 4px;
}
```

* `.form-{Type}-wrapper`: Målar det yttre `div` -element baserat på fälttypen. Till exempel: `.form-text-wrapper` anger alla textinmatningsfält som mål.
* `.form-{Name}`: Markerar elementet ytterligare baserat på det specifika fältnamnet. Till exempel: `.form-first-name` anger textfältet&quot;Förnamn&quot; som mål.

**Exempel:**

```CSS
/*Target all text input fields */

.form-text-wrapper input {
  border: 1px solid #ccc;
  padding: 8px;
  border-radius: 4px;
}

/*Target all fields with name first-name*/

.form-first-name input {
  border: 1px solid #ccc;
  padding: 8px;
  border-radius: 4px;
}
```


### Listrutekomponent

I listrutor visas `select` -element används i stället för ett `input` element:


#### HTML struktur

```HTML
<div class="form-drop-down-wrapper form-{Name} field-wrapper" data-required={required}>
  <label for="{FieldId}" class="field-label">First Name</label>
  <select id="{FieldId}" name="{Name}"><option></option><option></option></select>
  <div class="field-description" aria-live="polite" id="{FieldId}-description">
    Hint - First name should be minimum 3 characters and a maximum of 10 characters.
  </div>
</div>
```

**Exempel**

```HTML
    <div class="form-drop-down-wrapper form-country field-wrapper" data-required="true">
      <label for="country" class="field-label">Country</label>
      <select id="country" name="country">
         <option value="">Select Country</option>
         <option value="US">United States</option>
         <option value="CA">Canada</option>
    </select>
   <div class="field-description" aria-live="polite" id="country-description">Please select your country of residence.</div>
   </div>
```

#### CSS-väljare för nedrullningskomponent

```CSS
/* Target the outer wrapper */
.form-drop-down-wrapper {
  /* Add your styles here */
  display: flex;
  flex-direction: column;
  margin-bottom: 15px;
}

/* Style the label */
.form-drop-down-wrapper .field-label {
  margin-bottom: 5px;
  font-weight: bold;
}

/* Style the dropdown itself */
.form-drop-down-wrapper select {
  border: 1px solid #ccc;
  padding: 8px;
  border-radius: 4px;
  background-color: white; /* Ensure a consistent background */
  /* Adjust arrow appearance as needed */
  -webkit-appearance: none;
  -moz-appearance: none;
  appearance: none;
}

/* Optional: Style the dropdown arrow */
.form-drop-down-wrapper select::-ms-expand {
  display: none; /* Hide the default arrow for IE11 */
}

.form-drop-down-wrapper select::after {
  content: "\25BC";
  font-size: 12px;
  color: #ccc;
  /* Adjust positioning as needed */
  position: absolute;
  right: 10px;
  top: 50%;
  transform: translateY(-50%);
}
```

* Ange som mål för wrapper: Den första väljaren (`.form-drop-down-wrapper`) anger det yttre wrapper-elementet som mål, vilket säkerställer att formaten tillämpas på hela den nedrullningsbara komponenten.
* Flexbox Layout: Flexbox ordnar etiketten, listrutan och beskrivningen lodrätt för en ren layout.
* Etikettformatering: Etiketten sticker ut med en större teckensnittsvikt och en liten marginal.
* Formatering i listruta: Det markerade elementet får en kantlinje, utfyllnad och rundade hörn för en elegant look.
* Bakgrundsfärg: En konsekvent bakgrundsfärg ställs in för visuell harmoni.
* Anpassning av pilar: Valfria format döljer den nedrullningsbara standardpilen och skapar en anpassad pil med Unicode-tecken och placering.

### Grupper av alternativknappar och kryssrutor

Precis som för komponenter i listrutor har alternativknappar och kryssrutegrupper sin egen HTML-struktur och CSS-överväganden:

#### Struktur för Radio Group HTML

```HTML
<div class="form-checkbox-group-wrapper form-{Name} field-wrapper" data-required={required}>
  <label class="field-label">{Label Text}</label>
  <div class="checkbox-group">
    <input type="checkbox" id="{FieldId}-1" name="{Name}" value="{Value1}">
    <label for="{FieldId}-1">{Option 1 Text}</label>
    <input type="checkbox" id="{FieldId}-2" name="{Name}" value="{Value2}">
    <label for="{FieldId}-2">{Option 2 Text}</label>
    </div>
  <div class="field-description" aria-live="polite" id="{FieldId}-description">
    Hint - Select multiple options (if applicable).
  </div>
</div>
```


#### Struktur för Radio Group HTML

```HTML
<div class="form-checkbox-group-wrapper form-{Name} field-wrapper" data-required={required}>
  <label class="field-label">{Label Text}</label>
  <div class="checkbox-group">
    <input type="checkbox" id="{FieldId}-1" name="{Name}" value="{Value1}">
    <label for="{FieldId}-1">{Option 1 Text}</label>
    <input type="checkbox" id="{FieldId}-2" name="{Name}" value="{Value2}">
    <label for="{FieldId}-2">{Option 2 Text}</label>
    </div>
  <div class="field-description" aria-live="polite" id="{FieldId}-description">
    Hint - Select multiple options (if applicable).
  </div>
</div>
```

#### CSS-väljare för alternativknappar och kryssrutegrupper

**Inriktning mot ytterhöljet**


```CSS
   /* Targets all radio group wrappers */
.form-radio-group-wrapper {
  margin-bottom: 20px; /* Adds space between radio groups */
}

/* Targets all checkbox group wrappers */
.form-checkbox-group-wrapper {
  margin-bottom: 20px; /* Adds space between checkbox groups */
}
```

Dessa väljare är avsedda för de yttre behållarna för grupper med både alternativknappar och kryssrutor, vilket gör att du kan använda allmänna format för hela gruppstrukturen. Det här är användbart när du vill ange avstånd, justering eller andra layoutrelaterade egenskaper.

**Målgruppsetiketter**

```CSS
.form-radio-group-wrapper .field-label,
.form-checkbox-group-wrapper .field-label {
 font-weight: bold; /* Makes the group label bold */
}
```

Den här väljaren anger målet för `.field-label` -element i gruppomslutningar för både alternativknappar och kryssrutor. På så sätt kan du formatera etiketterna specifikt för dessa grupper, vilket kan få dem att sticka ut mer.

**Målinrikta enskilda indata och etiketter**

```CSS
/* Styling radio buttons */
.form-radio-group-wrapper input[type="radio"] {
  margin-right: 5px; /* Adds space between the input and its label */
} 

/* Styling radio button labels */
.form-radio-group-wrapper label {
  font-size: 15px; /* Changes the label font size */
}

/* Styling checkboxes */
.form-checkbox-group-wrapper input[type="checkbox"] {
  margin-right: 5px;  /* Adds space between the input and its label */ 
}

/* Styling checkbox labels */
.form-checkbox-group-wrapper label {
  font-size: 15px; /* Changes the label font size */
}
```

Dessa väljare ger mer exakt kontroll över enskilda alternativknappar, kryssrutor och tillhörande etiketter. Du kan använda dessa för att justera storlek, avstånd eller använda mer distinkta visuella format.


**Anpassa utseende på alternativknappar och kryssrutor**

```CSS
/* Hide the default radio button or checkbox */
.form-radio-group-wrapper input[type="radio"],
.form-checkbox-group-wrapper input[type="checkbox"] {
  opacity: 0; 
  position: absolute; 
}

/* Create a custom radio button */
.form-radio-group-wrapper input[type="radio"] + label::before { 
  content: "";
  display: inline-block;
  width: 16px; 
  height: 16px; 
  border: 2px solid #ccc; 
  border-radius: 50%;
  margin-right: 5px;
}

.form-radio-group-wrapper input[type="radio"]:checked + label::before {
  background-color: #007bff; 
}

/* Create a custom checkbox */
/* Similar styling as above, with adjustments for a square shape */
```

Den här tekniken döljer standardindata och använder :before och :after-pseudoelement för att skapa anpassade bilder som ändrar utseende baserat på läget &#39;checked&#39;.


## Formateringsfält

Förutom de allmänna formateringstekniker som beskrivs ovan kan du även formatera formulärfält baserat på deras specifika typ eller enskilda namn. På så sätt får du bättre kontroll över och anpassning av formulärets utseende.

### Formatering baserad på fälttyp

Du kan använda CSS-väljare för att ange specifika fälttyper och använda format på ett konsekvent sätt.

**Exempel på HTML-struktur**

```HTML
<div class="form-text-wrapper form-name field-wrapper" data-required="true">
  <label for="name" class="field-label">Name</label>
  <input type="text" placeholder="Enter your name" maxlength="50" id="name" name="name">
</div>

<div class="form-number-wrapper form-age field-wrapper" data-required="true">
  <label for="age" class="field-label">Age</label>
  <input type="number" placeholder="Enter your age" id="age" name="age">
</div>

<div class="form-email-wrapper form-email field-wrapper" data-required="true">
  <label for="email" class="field-label">Email Address</label>
  <input type="email" placeholder="Enter your email" id="email" name="email">
</div>
```

* Varje fält radbryts i en `div` element med flera klasser:
   * `form-{Type}-wrapper`: Identifierar fälttypen. Till exempel: `form-text-wrapper`, `form-number-wrapper`, `form-email-wrapper`.
   * `form-{Name}`: Identifierar fältet med dess namn. Till exempel `form-name`, `form-age`, `form-email`.
   * `field-wrapper`: En generisk klass för alla fältbrytare.
* The `data-required` anger om fältet är obligatoriskt eller valfritt.
* Varje fält har en motsvarande etikett, indataelement och eventuella ytterligare element som platshållare och beskrivningar.

Till exempel:

```CSS
/* Target all text input fields */
.form-text-wrapper input {
  /* Add your styles here */
}

/* Target all number input fields */
.form-number-wrapper input {
  /* Add your styles here */
  letter-spacing: 2px; /* Example for adding letter spacing to all number fields */
}
```

### Formatera specifika fälttyper

Du kan också ange enskilda fält som mål efter namn för att använda unika format.

**Exempel på HTML-struktur**

```HTML
<div class="form-number-wrapper form-otp field-wrapper" data-required="true">
  <label for="otp" class="field-label">OTP</label>
  <input type="number" placeholder="Enter your OTP" maxlength="6" id="otp" name="otp">
</div>
```

**CSS-väljare**

```CSS
.form-otp input {
   letter-spacing: 2px
}
```

* Väljare: Den här CSS-koden riktar in alla indataelement som finns i ett element som har klassen `form-otp`. Din HTML-struktur följer konventionerna för formulärblocket, vilket innebär att det finns en behållare som är markerad med klassen &quot;form-otp&quot; som innehåller fältet med namnet &quot;otp&quot;.

* Egenskap och värde: koden gäller `letter-spacing: 2px`. Den här CSS-egenskapen styr mellanrummet mellan enskilda bokstäver i textinnehållet i inmatningsfältet.
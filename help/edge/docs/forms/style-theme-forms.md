---
title: Anpassa teman och format för Edge Delivery Services för AEM Forms
description: Anpassa teman och format för Edge Delivery Services för AEM Forms
feature: Edge Delivery Services
exl-id: c214711c-979b-4833-9541-8e35b2aa8e09
role: Admin, Architect, Developer
source-git-commit: babddee34b486960536ce7075684bbe660b6e120
workflow-type: tm+mt
source-wordcount: '1909'
ht-degree: 0%

---


# Anpassa utseendet på formulären

Forms är avgörande för användarinteraktion på webbplatser, så att de kan mata in data. Du kan använda CSS (Cascading Style Sheets) för att formatera formulärfält, förbättra den visuella presentationen av formulären och förbättra användarupplevelsen.

Det adaptiva Forms-blocket ger en konsekvent struktur för alla formulärfält. Denna enhetliga struktur gör det enklare att utveckla CSS-väljare för att markera och formatera formulärfält baserat på fälttyp och fältnamn.

I det här dokumentet beskrivs HTML-strukturen för olika formulärkomponenter och du kan skapa en förståelse för hur du skapar CSS-väljare för olika formulärfält för att formatera formulärfält i ett adaptivt Forms-block.

När artikeln är slut ska du:

* Bygg en förståelse för strukturen i standardfilen för CSS som ingår i det adaptiva Forms-blocket
* Bygg en förståelse för HTML-strukturen för de formulärkomponenter som ingår i det adaptiva Forms-blocket, inklusive allmänna komponenter och specifika komponenter som listrutor, alternativgrupper och kryssrutegrupper
* Lär dig att formatera formulärfält baserat på fälttyp och fältnamn med CSS-väljare, vilket ger en konsekvent eller unik formatering baserat på krav


## Förstå formulärfältstyper

Innan vi börjar dyka upp i en formatmall ska vi granska den gemensamma formulärtypen [fälttyper](/help/edge/docs/forms/form-components.md) som stöds av det adaptiva Forms-blocket:

* Indatafält: Dessa innehåller textinmatningar, e-postinmatningar, lösenordsinmatningar med mera
* Kryssrutegrupper: Används för att välja flera alternativ
* Alternativgrupper: Används för att endast välja ett alternativ från en grupp
* Listrutor: Kallas även urvalsrutor, som används för att välja ett alternativ i en lista
* Paneler/behållare: Används för att gruppera relaterade formulärelement

## Grundläggande formatprinciper

Att förstå [grundläggande CSS-koncept](https://www.w3schools.com/css/css_intro.asp) är avgörande innan du formaterar specifika formulärfält:

* [Väljare](https://www.w3schools.com/css/css_selectors.asp): Med CSS-väljare kan du ange specifika HTML-element som mål för formateringen. Du kan använda elementväljare, klassväljare eller ID-väljare
* [Egenskaper](https://www.w3schools.com/css/css_syntax.asp): CSS-egenskaper definierar elementens visuella utseende. Vanliga egenskaper för formatformulärfält är bland annat färg, bakgrundsfärg, kant, utfyllnad, marginal
* [Rutmodell](https://www.w3schools.com/css/css_boxmodel.asp): CSS-rutmodellen beskriver strukturen för HTML-element som ett innehållsområde omgivet av utfyllnad, kanter och marginaler
* Flexbox/Grid: CSS [Flexbox](https://www.w3schools.com/css/css3_flexbox.asp) och [Grid layouts](https://www.w3schools.com/css/css_grid.asp) är kraftfulla verktyg för att skapa responsiva och flexibla designer

## Formatera ett formulär för Adaptive Forms Block

Adaptive Forms Block har en standardiserad HTML-struktur som förenklar processen att välja ut och formatera formulärkomponenter:

* **Uppdatera standardformat**: Du kan ändra standardformaten för ett formulär genom att redigera `/blocks/form/form.css`-filen. Den här filen innehåller omfattande formatering för ett formulär med stöd för guideformulär i flera steg. Det är viktigt att du använder anpassade CSS-variabler för enkel anpassning, underhåll och enhetlig formatering i olika formulär. Instruktioner om hur du lägger till det adaptiva Forms-blocket i ditt projekt finns i [Skapa ett formulär](/help/edge/docs/forms/create-forms.md).

* **Anpassning**: Använd standardvärdet `forms.css` som bas och anpassa det för att ändra utseendet och känslan hos dina formulärkomponenter, så att de blir visuellt tilltalande och användarvänliga. Filens struktur uppmuntrar organisationen och bevarar format för formulär, vilket ger en enhetlig design på hela webbplatsen.

## Uppdelning av form.css-struktur

* **Globala variabler:** Dessa variabler (`--variable-name`) är definierade på `:root`-nivå och lagrar värden som används i hela formatmallen för att vara konsekventa och för att underlätta uppdateringar. Dessa variabler definierar färger, teckenstorlekar, utfyllnad och andra egenskaper. Du kan deklarera dina egna globala variabler eller ändra befintliga variabler för att ändra formulärets format.

* **Universella väljarformat:** `*` Väljaren matchar alla element i formuläret och ser till att format tillämpas på alla komponenter som standard, inklusive inställning av egenskapen `box-sizing` till `border-box`.

* **Formulärformat:** Det här avsnittet fokuserar på att formatera formulärkomponenter med väljare för att ange specifika HTML-element som mål. Här definieras format för inmatningsfält, textområden, kryssrutor, alternativknappar, filinmatningar, formuläretiketter och beskrivningar.

* **Ställning av guiden (om tillämpligt):** Det här avsnittet används för att utforma guidelayouten, ett flerstegsformulär där varje steg visas ett i taget. Den definierar format för guidebehållaren, fältuppsättningar, teckenförklaringar, navigeringsknappar och responsiva layouter.

* **Mediefrågor:** Dessa innehåller format för olika skärmstorlekar och justerar layout och format utifrån detta.

* **Diverse formatering:** I det här avsnittet beskrivs formatmallar för slutförda eller felmeddelanden, områden för filöverföring och andra element som du kan stöta på i ett formulär.


## Komponentstruktur

Det adaptiva Forms-blocket erbjuder en enhetlig HTML-struktur för olika formulärelement, vilket gör det enklare att formatera och hantera. Du kan ändra komponenterna med CSS i formateringssyfte.

### Allmänna komponenter (utom listrutor, alternativknappar och kryssrutegrupper):

Alla formulärfält, utom listrutor, alternativgrupper och kryssrutegrupper, har följande HTML-struktur:

+++ HTML-struktur för allmänna komponenter

```HTML
<div class="{Type}-wrapper field-{Name} field-wrapper" data-required={Required}>
   <label for="{FieldId}" class="field-label">First Name</label>
   <input type="{Type}" placeholder="{Placeholder}" maxlength="{Max}" id="{FieldId}" name="{Name}" aria-describedby="{FieldId}-description">
   <div class="field-description" aria-live="polite" id="{FieldId}-description">
    Hint - First name should be a minimum of 3 characters and a maximum of 10 characters.
   </div>
</div>
```

* Klasser: div-elementet har flera klasser för att rikta specifika element och format. Du kräver att klasserna `{Type}-wrapper` eller `field-{Name}` utvecklar en CSS-väljare för att formatera ett formulärfält:
   * {Type}: Identifierar komponenten efter fälttyp. Till exempel text (text-wrapper), tal (number-wrapper), datum (date-wrapper)
   * {Name}: Identifierar komponenten efter namn. Fältets namn kan bara innehålla alfanumeriska tecken. Flera bindestreck i följd i namnet ersätts med ett bindestreck `(-)` och inledande och avslutande bindestreck i ett fältnamn tas bort. Förnamn (field-first-name field-wrapper)
   * {FieldId}: Det är en unik identifierare för fältet, som genereras automatiskt
   * {Required}: Det är ett booleskt värde som anger om fältet är obligatoriskt
* Etikett: Elementet `label` innehåller beskrivande text för fältet och associerar det med indataelementet med attributet `for`
* Indata: Elementet `input` definierar vilken typ av data som ska anges. Till exempel text, tal, e-post
* Beskrivning (valfritt): `div` med klassen `field-description` innehåller ytterligare information eller instruktioner för användaren

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

+++

+++ CSS-väljare för allmänna komponenter

```CSS
/* Target all input fields within any .{Type}-wrapper */
.{Type}-wrapper {
  /* Add your styles here */
  border: 1px solid #ccc;
  padding: 8px;
  border-radius: 4px;
}

/* Target all input fields within any .{Type}-wrapper */
.{Type}-wrapper input {
  /* Add your styles here */
  border: 1px solid #ccc;
  padding: 8px;
  border-radius: 4px;
}

/* Target any element with the class field-{Name} */
.field-{Name} {
  /* Add your styles here */
  /* This could be used for styles specific to all elements with field-{Name} class, not just inputs */
}
```

* `.{Type}-wrapper`: Målar det yttre `div`-elementet baserat på fälttypen. `.text-wrapper` har till exempel alla textfält som mål
* `.field-{Name}`: Markerar elementet ytterligare baserat på det specifika fältnamnet. `.field-first-name` anger till exempel textfältet Förnamn som mål. Även om den här väljaren kan användas för att rikta element med klassen field-{Name} är det viktigt att vara försiktig. I det här specifika fallet skulle det inte vara användbart för formaterade inmatningsfält eftersom det skulle vara avsett inte bara för själva inmatningen utan även för etikett- och beskrivningselementen. Vi rekommenderar att du använder mer specifika väljare, som de du har för textinmatningsfält (.text-wrapper input)

**Exempel på CSS-väljare för allmänna komponenter**

```CSS
/* Target all text input fields */
.text-wrapper input {
  border: 1px solid #ccc;
  padding: 8px;
  border-radius: 4px;
}

/* Target all fields with name first-name */
.field-first-name input {
  border: 1px solid #ccc;
  padding: 8px;
  border-radius: 4px;
}
```

+++

### Listrutekomponent

I listrutor används elementet `select` i stället för ett `input`-element:

+++ HTML-struktur för nedrullningskomponent

```HTML
<div class="{Type}-wrapper field-{Name} field-wrapper" data-required={Required}>
   <label for="{FieldId}" class="field-label">Country</label>
   <select id="{FieldId}" name="{Name}"><option></option><option></option></select>
   <div class="field-description" aria-live="polite" id="{FieldId}-description">
    Please select your country from the list.
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

+++

+++ CSS-väljare för nedrullningskomponent

```CSS
/* Target the outer wrapper */
.drop-down-wrapper {
  /* Add your styles here */
  display: flex;
  flex-direction: column;
  margin-bottom: 15px;
}

/* Style the label */
.drop-down-wrapper .field-label {
  margin-bottom: 5px;
  font-weight: bold;
}

/* Style the dropdown itself */
.drop-down-wrapper select {
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
.drop-down-wrapper select::-ms-expand {
  display: none; /* Hide the default arrow for IE11 */
}

.drop-down-wrapper select::after {
  content: "\25BC";
}
```

+++

### Alternativgrupper

Ungdomsgrupper har en egen HTML-struktur och CSS-struktur, precis som komponenter i listrutor:

+++ HTML Structure of Radio Group

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

#### Exempel på HTML-struktur

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

+++

+++ CSS-väljare för alternativknappar

* Ange fältuppsättningen

```CSS
  .radio-group-wrapper {
    border: 1px solid #ccc;
    padding: 10px;
  }
```

Den här väljaren anger alla fältuppsättningar med klassen Radio-Group-wrapper som mål. Det är användbart om du vill använda allmänna format på hela alternativgruppen.

* Egenskaper för alternativknappar

```CSS
.radio-wrapper label {
    font-weight: normal;
    margin-right: 10px;
  }
```

* Ange alla alternativknappsetiketter för ett specifikt fält baserat på dess namn

```CSS
.field-color .radio-wrapper label {
  /* Your styles here */
}
```

+++

### Kryssrutegrupper

+++ HTML Structure of Checkbox Group

```HTML
<fieldset class="checkbox-group-wrapper field-{Name} field-wrapper" id="{FieldId}" name="{Name}" data-required="{Required}">
   <legend for="{FieldId}" class="field-label">....</legend>
   <% for each radio in Group %>
   <div class="radio-wrapper field-{Name}">
      <input type="checkbox" value="" id="{UniqueId}" data-field-type="checkbox-group" name="{FieldId}">
      <label for="{UniqueId}" class="field-label">...</label>
   </div>
   <% end for %>
</fieldset>
```

#### Exempel på HTML-struktur

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

+++

+++ CSS-väljare för kryssrutegrupper

* Inriktning för ytteromslutningen: Dessa väljare är avsedda för de yttre behållarna för både alternativknappar och kryssrutegrupper, vilket gör att du kan använda allmänna format för hela gruppstrukturen. Det här är användbart när du vill ange avstånd, justering eller andra layoutrelaterade egenskaper.


  ```CSS
     /* Targets radio group wrappers */
       .radio-group-wrapper {
       margin-bottom: 20px; /* Adds space between radio groups */  
     }
  
     /* Targets checkbox group wrappers */
     .checkbox-group-wrapper {
     margin-bottom: 20px; /* Adds space between checkbox groups */
     }
  ```


* Målgruppsetiketter: Den här väljaren anger elementet `.field-label` som mål i gruppomslutningar för både alternativknappar och kryssrutor. På så sätt kan du formatera etiketterna specifikt för dessa grupper, vilket kan få dem att sticka ut mer.

  ```CSS
   .radio-group-wrapper legend,
   .checkbox-group-wrapper legend {
     font-weight: bold; /* Makes the group label bold */
   }
  ```



* Indata och etiketter för enskilda användare: Dessa väljare ger mer exakt kontroll över enskilda alternativknappar, kryssrutor och tillhörande etiketter. Du kan använda dessa för att justera storlek, avstånd eller använda mer distinkta visuella format.

  ```CSS
  /* Styling radio buttons */
   .radio-group-wrapper input[type="radio"] {
     margin-right: 5px; /* Adds space between the input and its label */
   }
  
   /* Styling radio button labels */
   .radio-group-wrapper label {
     font-size: 15px; /* Changes the label font size */
   }
  
  /* Styling checkboxes */
   .checkbox-group-wrapper input[type="checkbox"] {
     margin-right: 5px; /* Adds space between the input and its label */
   }
  
   /* Styling checkbox labels */
   .checkbox-group-wrapper label {
     font-size: 15px; /* Changes the label font size */
   }
  ```




* Anpassa utseendet på alternativknappar och kryssrutor: Den här tekniken döljer standardindata och använder `:before` och `:after` pseudoelement för att skapa anpassade bilder som ändrar utseende baserat på markerat läge.

  ```CSS
  /* Hide the default radio button or checkbox */
     .radio-group-wrapper input[type="radio"],
     .checkbox-group-wrapper input[type="checkbox"] {
       opacity: 0;
       position: absolute;
     }
  
     /* Create a custom radio button */
     .radio-group-wrapper input[type="radio"] + label::before {
       /* ... styles for custom radio button ... */
     }
  
     .radio-group-wrapper input[type="radio"]:checked + label::before {
       /* ... styles for checked radio button ... */
     }
  
     /* Create a custom checkbox */
     /* Similar styling as above, with adjustments for a square shape  */
     .checkbox-group-wrapper input[type="checkbox"] + label::before {
       /* ... styles for custom checkbox ... */
     }
  
     .checkbox-group-wrapper input[type="checkbox"]:checked + label::before {
       /* ... styles for checked checkbox ... */
     }
  ```

+++

### Panel-/behållarkomponenter

+++ HTML-struktur för paneler/behållarkomponenter

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

* Fältuppsättningselementet fungerar som panelbehållare med klassens panelwrapper och ytterligare klasser för formatering baserat på panelnamnet (fältinloggning).
* Förklaringselementet (&lt;legend>) fungerar som panelrubrik med texten&quot;Inloggningsinformation&quot; och klassens fältetikett. Attributet data-visible=&quot;false&quot; kan användas med JavaScript för att styra visningen av titeln.
* I fältuppsättningen, multipel .{Type}-wrapper-element (.text-wrapper och .password-wrapper i det här fallet) representerar enskilda formulärfält på panelen.
* Varje wrapper innehåller en etikett, ett inmatningsfält och en beskrivning, som liknar de föregående exemplen.

+++

+++ Exempel på CSS-väljare för panel-/behållarkomponenter

1. Panelen:

```CSS
  /* Target the entire panel container */
  .panel-wrapper {
    /* Add your styles here (e.g., border, padding, background color) */
    border: 1px solid #ccc;
    padding: 15px;
    border-radius: 4px;
    margin-bottom: 20px;
 }
```

* `.panel-wrapper`-väljaren formaterar alla element med klassens panelwrapper, vilket ger ett konsekvent utseende för alla paneler.

1. Ange paneltiteln som mål:

```CSS
  /* Target the legend element (panel title) */
  .panel-wrapper legend {
    /* Add your styles here (e.g., font-weight, font-size) */
    font-weight: bold;
    font-size: 16px;
    padding-bottom: 5px;
    margin-bottom: 10px;
    border-bottom: 1px solid #ddd; /* Optional: create a separation line */
  }
```

* `.panel-wrapper legend`-väljaren formaterar förklaringselementet på panelen, så att titeln sticker ut visuellt.


1. Ange enskilda fält som mål på panelen:

```CSS
/* Target all form field wrappers within a panel */
.panel-wrapper .{Type}-wrapper {
  /* Add your styles here (e.g., margin) */
  margin-bottom: 10px;
}
```

* `.panel-wrapper .{Type}-wrapper`-väljaren anger alla omslutningar med klassen `.{Type}-wrapper` på panelen som mål, vilket gör att du kan formatera mellanrummet mellan formulärfält.

1. Målspecifika fält (valfritt):

```CSS
  /* Target the username field wrapper */
  .panel-wrapper .text-wrapper.field-username {
    /* Add your styles here (specific to username field) */
  }

  /* Target the password field wrapper */
  .panel-wrapper .password-wrapper.field-password {
    /* Add your styles here (specific to password field) */
  }
```

* Dessa väljare gör att du kan rikta in dig på specifika fältbrytningar på panelen för unik formatering, t.ex. markera användarnamnsfältet.

+++

### Repeterbar panel

+++ HTML-struktur för en upprepningsbar panel

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

* data-repetable=&quot;true&quot;: Det här attributet anger att panelen kan upprepas dynamiskt med JavaScript eller ett ramverk.

* Unika ID:n och namn: Varje element i panelen har ett unikt ID (till exempel name-1, email-1) och name-attribut baserat på panelens indexvärde (till exempel name=&quot;contact[0].name&quot;). Detta gör att data kan samlas in korrekt när flera paneler skickas.

+++

+++ CSS-väljare för en upprepningsbar panel

* Alla upprepningsbara paneler som mål:

```CSS
  /* Target all panels with the repeatable attribute */
  .panel-wrapper[data-repeatable="true"] {
    /* Add your styles here (e.g., border, margin) */
    border: 1px solid #ccc;
    padding: 15px;
    border-radius: 4px;
    margin-bottom: 20px;
  }
```

Väljaren formaterar alla paneler som kan upprepas, vilket ger ett konsekvent utseende och känsla.


* Ange enskilda fält som mål på en panel:

```CSS
/* Target all form field wrappers within a repeatable panel */
.panel-wrapper[data-repeatable="true"] .{Type}-wrapper {
  /* Add your styles here (e.g., margin) */
  margin-bottom: 10px;
}
```

Den här väljaren formaterar alla fältomslutningar på en repeterbar panel, vilket ger ett konsekvent avstånd mellan fälten.

* Ange specifika fält som mål (inom en panel):

```CSS
/* Target the name field wrapper within the first panel */
.panel-wrapper[data-repeatable="true"][data-index="0"] .text-wrapper.field-name {
  /* Add your styles here (specific to first name field) */
}

/* Target all
```

+++

### Bifogad fil

+++ HTML-struktur för bifogad fil

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

* Klassattributet använder det angivna namnet för den bifogade filen (claim_form).
* Attributen id och name för indataelementet matchar namnet på den bifogade filen (claim_form).
* Avsnittet med fillistan är inledningsvis tomt. Den fylls i dynamiskt med JavaScript när filer överförs.

+++

+++ CSS-väljare för komponenten Bifogad fil

* Målkomponenten för hela den bifogade filen:

```CSS
/* Target the entire file attachment component */
.file-wrapper {
  /* Add your styles here (e.g., border, padding) */
  border: 1px solid #ccc;
  padding: 15px;
  border-radius: 4px;
  margin-bottom: 20px;
}
```

Den här väljaren formaterar hela den bifogade filkomponenten, inklusive teckenförklaringen, dragningsområdet, inmatningsfältet och listan.

* Målinriktade specifika element:

```CSS
/* Target the drag and drop area */
.file-wrapper .file-drag-area {
  /* Add your styles here (e.g., background color, border) */
  background-color: #f0f0f0;
  border: 1px dashed #ddd;
  padding: 10px;
  text-align: center;
}

/* Target the file input element */
.file-wrapper input[type="file"] {
  /* Add your styles here (e.g., hide the default input) */
  display: none;
}

/* Target individual file descriptions within the list (populated dynamically) */
.file-wrapper .files-list .file-description {
  /* Add your styles here (e.g., margin, display) */
  display: flex;
  justify-content: space-between;
  margin-bottom: 5px;
}

/* Target the file name within the description */
.file-wrapper .files-list .file-description .file-description-name {
  /* Add your styles here (e.g., font-weight) */
  font-weight: bold;
}

/* Target the file size within the description */
.file-wrapper .files-list .file-description .file-description-size {
  /* Add your styles here (e.g., font-size) */
  font-size: 0.8em;
}

/* Target the remove button within the description */
.file-wrapper .files-list .file-description .file-description-remove {
  /* Add your styles here (e.g., background color, hover effect) */
  background-color: transparent;
  border: none;
  cursor: pointer;
}
```

Dessa väljare gör att du kan formatera olika delar av den bifogade filkomponenten individuellt. Du kan justera formaten så att de matchar dina designinställningar.

+++


## Formatkomponenter

Du kan formatera formulärfält baserat på deras specifika typ (`{Type}-wrapper`) eller enskilda namn (`field-{Name}`). På så sätt får du bättre kontroll över och anpassning av formulärets utseende.

### Formatering baserad på fälttyp

Du kan använda CSS-väljare för att ange specifika fälttyper och använda format på ett konsekvent sätt.

+++ HTML Structure

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

* Varje fält kapslas i ett `div`-element med flera klasser:
   * `{Type}-wrapper`: Identifierar fälttypen. Exempel: `form-text-wrapper`, `form-number-wrapper`, `form-email-wrapper`.
   * `field-{Name}`: Identifierar fältet med dess namn. Till exempel `form-name`, `form-age`, `form-email`.
   * `field-wrapper`: En generisk klass för alla fältbrytare.
* Attributet `data-required` anger om fältet är obligatoriskt eller valfritt.
* Varje fält har en motsvarande etikett, indataelement och eventuella ytterligare element som platshållare och beskrivningar.


+++


+++ Exempel på CSS-väljare

```CSS
/* Target all text input fields */
.text-wrapper input {
  /* Add your styles here */
}

/* Target all number input fields */
.number-wrapper input {
  /* Add your styles here */
  letter-spacing: 2px; /* Example for adding letter spacing to all number fields */
}
```

+++

### Formatering baserad på fältnamn

Du kan också ange enskilda fält som mål efter namn för att använda unika format.

+++ HTML Structure

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

+++

+++ Exempel på CSS-väljare

```CSS
.field-otp input {
   letter-spacing: 2px
}
```



Den här CSS-koden har alla indataelement som finns i ett element som har klassen `field-otp` som mål. Formulärets HTML-struktur följer konventionerna i det adaptiva Forms-blocket, vilket innebär att det finns en behållare som är markerad med klassen&quot;field-out&quot; som innehåller fältet med namnet&quot;otp&quot;.

+++

## Se även

{{see-more-forms-eds}}
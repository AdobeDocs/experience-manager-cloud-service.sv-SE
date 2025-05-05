---
title: Anpassa tema och stil för en Edge Delivery Services for AEM Forms
description: Anpassa temat och formatet för AEM Forms som levereras via Edge Delivery Services på ett effektivt sätt och skapa en sammanhängande och varumärkesanpassad användarupplevelse.
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: ac780399-34fe-457d-aaf4-b675656c024d
source-git-commit: 9127c58a72dc4942312907f9e8f0cdcc8de9aa4b
workflow-type: tm+mt
source-wordcount: '1876'
ht-degree: 0%

---

# Anpassa utseendet på formulären

<span class="preview"> Den här funktionen är tillgänglig via programmet för tidig åtkomst. Om du vill begära åtkomst skickar du ett e-postmeddelande med ditt GitHub-organisationsnamn och databasnamn från din officiella adress till <a href="mailto:aem-forms-ea@adobe.com">aem-forms-ea@adobe.com</a> . Om databas-URL:en till exempel är https://github.com/adobe/abc är organisationsnamnet adobe och databasnamnet abc.</span>


Forms är avgörande för användarinteraktion på webbplatser, så att de kan mata in data. Du kan använda CSS (Cascading Style Sheets) för att formatera fält i ett formulär, förbättra den visuella presentationen av formulären och förbättra användarupplevelsen.

Det adaptiva Forms-blocket ger en konsekvent struktur för alla formulärfält. Den konsekventa strukturen gör det enklare att utveckla CSS-väljare för att markera och formatera formulärfält baserat på fälttyp och fältnamn.

I det här dokumentet beskrivs HTML-strukturen för olika formulärkomponenter, så att du kan skapa en förståelse för hur du skapar CSS-väljare för olika formulärfält för att formatera formulärfält i ett adaptivt Forms-block.

I slutet av artikeln:

* Du bygger upp en förståelse för strukturen i standardfilen för CSS som ingår i det adaptiva Forms-blocket.
* Du bygger upp en förståelse för HTML-strukturen för de formulärkomponenter som tillhandahålls av det adaptiva Forms-blocket, inklusive allmänna komponenter och specifika komponenter som listrutor, alternativgrupper och kryssrutegrupper.
* Du lär dig att formatera formulärfält baserat på fälttyp och fältnamn med hjälp av CSS-väljare, vilket ger en konsekvent eller unik formatering baserat på krav.

## Förstå formulärfältstyper

Innan vi börjar dyka upp i en formatmall ska vi granska den gemensamma formulärtypen [fälttyper](/help/edge/docs/forms/universal-editor/create-custom-component.md#supported-fieldtypes) som stöds av det adaptiva Forms-blocket:

* Indatafält: Dessa innehåller textinmatningar, e-postinmatningar, lösenordsinmatningar med mera.
* Kryssrutegrupper: Används för att välja flera alternativ.
* Alternativgrupper: Används för att endast välja ett alternativ från en grupp.
* Listrutor: Kallas även urvalsrutor, som används för att välja ett alternativ i en lista.
* Paneler/behållare: Används för att gruppera relaterade formulärelement.

## Grundläggande formatprinciper

Att förstå [grundläggande CSS-koncept](https://www.w3schools.com/css/css_intro.asp) är avgörande innan du formaterar specifika formulärfält:

* [Väljare](https://www.w3schools.com/css/css_selectors.asp): Med CSS-väljare kan du ange specifika HTML-element som mål för formateringen. Du kan använda elementväljare, klassväljare eller ID-väljare.
* [Egenskaper](https://www.w3schools.com/css/css_syntax.asp): CSS-egenskaper definierar elementens visuella utseende. Vanliga egenskaper för formatformulärfält är bland annat färg, bakgrundsfärg, kant, utfyllnad, marginal.
* [Rutmodell](https://www.w3schools.com/css/css_boxmodel.asp): CSS-rutmodellen beskriver strukturen för HTML-element som ett innehållsområde omgivet av utfyllnad, kanter och marginaler.
* Flexbox/Grid: CSS [Flexbox](https://www.w3schools.com/css/css3_flexbox.asp) och [Grid layouts](https://www.w3schools.com/css/css_grid.asp) är kraftfulla verktyg för att skapa responsiva och flexibla designer.


## Formatera ett formulär för Adaptive Forms Block

Adaptive Forms Block har en standardiserad HTML-struktur som förenklar processen att välja ut och formatera formulärkomponenter:

* **Uppdatera standardformat**: Du kan ändra standardformaten för ett formulär genom att redigera `/blocks/form/form.css file`. Den här filen innehåller omfattande formatering för ett formulär med stöd för guideformulär i flera steg. Det är viktigt att du använder anpassade CSS-variabler för enkel anpassning, underhåll och enhetlig formatering i olika formulär.

* **CSS-format för Forms**: Om du vill vara säker på att dina format används på rätt sätt kapslar du in din formulärspecifika CSS i `main .form form` -väljaren. På så sätt kan du vara säker på att formaten bara är avsedda för formulärelementen i huvudinnehållsområdet, vilket förhindrar konflikter med andra delar av webbplatsen.
Exempel:

  ```css
    main .form form input {
        /* Add styles specific to input fields inside the form */
    }
  
    main .form form button {
        /* Add styles specific to buttons inside the form */
    }
  
    main .form form label {
        /* Add styles specific to labels inside the form */
    }
  
## Komponentstruktur

Det adaptiva Forms-blocket erbjuder en enhetlig HTML-struktur för olika formulärelement, vilket gör det enklare att formatera och hantera. Du kan ändra komponenterna med CSS i formateringssyfte.

### Allmänna komponenter (utom listrutor, alternativknappar och kryssrutegrupper):

Alla formulärfält, utom listrutor, alternativgrupper och kryssrutegrupper, har följande HTML-struktur:

+++ HTML-struktur för allmänna komponenter

```HTML

  <div class="{Type}-wrapper field-{Name}   field-wrapper" data-required={Required}>
     &lt;label for="{FieldId}" class="field-label">First   Name&lt;/label>
     &lt;input type="{Type}" placeholder="{Placeholder}"   maxlength="{Max}" id={FieldId}" name="{Name}"   aria-describedby="{FieldId}-description">
     <div class="field-description" aria-live="polite"  id="{FieldId}-description">
      Hint - First name should be minimum 3 characters  and a maximum of 10 characters.
     </div>
  </div>

```

* Klasser: div-elementet har flera klasser för att rikta specifika element och format. Du kräver att klasserna `{Type}-wrapper` eller `field-{Name}` utvecklar en CSS-väljare för att formatera ett formulärfält:
* {Type}: Identifierar komponenten efter fälttyp. Exempel: text (text-wrapper), tal (number-wrapper), datum (date-wrapper).
* {Name}: Identifierar komponenten efter namn. Fältets namn kan bara innehålla alfanumeriska tecken, de flera på varandra följande strecken i namnet ersätts med ett enda streck `(-)` och inledande och avslutande streck i ett fältnamn tas bort. Förnamn (field-first-name field-wrapper).
* {FieldId}: Det är en unik identifierare för fältet, som genereras automatiskt.
* {Required}: Det är ett booleskt värde som anger om fältet är obligatoriskt.
* Etikett: Elementet `label` innehåller en beskrivande text för fältet och associerar det med indataelementet med attributet `for`.
* Indata: Elementet `input` definierar vilken typ av data som ska anges. Till exempel text, tal, e-post.
* Beskrivning (valfritt): `div` med klassen `field-description` innehåller ytterligare information eller instruktioner för användaren.

**Exempel på HTML-struktur**

```HTML

<div class="text-wrapper field-first-name field-wrapper" data-required="true">
  &lt;label for="firstName" class="field-label">First Name&lt;/label>
  &lt;input type="text" placeholder="Enter your first name" maxlength="50" id="firstName" name="firstName" aria-describedby="firstName-description">
  <div class="field-description" aria-live="polite" id="firstName-description">
    Please enter your legal first name.
  </div>
</div>

```

+++

+++ CSS-väljare för allmänna komponenter

```CSS

  
  /* Target all input fields within any .{Type}-wrapper  */
  main .form form .{Type}-wrapper  &lbrace;
    /* Add your styles here */
    border: 1px solid #ccc;
    padding: 8px;
    border-radius: 4px;
  &rbrace;
  
  /* Target all input fields within any .{Type}-wrapper  */
  main .form form .{Type}-wrapper input &lbrace;
    /* Add your styles here */
    border: 1px solid #ccc;
    padding: 8px;
    border-radius: 4px;
  &rbrace;
  
  /* Target any element with the class field-{Name}  */
  main .form form .field-{Name} &lbrace;
    /* Add your styles here */
    /* This could be used for styles specific to all elements with   field-{Name} class, not just inputs */
  &rbrace;
  
```
* `.{Type}-wrapper`: Målar det yttre `div`-elementet baserat på    fälttypen. `.text-wrapper` anger till exempel all text som mål    fält.
* `.field-{Name}`: Markerar elementet ytterligare baserat på det specifika fältnamnet. `.field-first-name` anger till exempel textfältet Förnamn som mål. Även om den här väljaren kan användas för att rikta element med klassen field-{Name} är det viktigt att vara försiktig. I det här specifika fallet skulle det inte vara användbart för formaterade inmatningsfält eftersom det skulle vara avsett inte bara för själva inmatningen utan även för etikett- och beskrivningselementen. Vi rekommenderar att du använder mer specifika väljare, som de du har för textinmatningsfält (.text-wrapper input).

**Exempel på CSS-väljare för allmänna komponenter**

```CSS

/*Target all text input fields */
main .form form .text-wrapper input &lbrace;
  border: 1px solid #ccc;
  padding: 8px;
  border-radius: 4px;
  color: red;
&rbrace;

/*Target all fields with name first-name*/
main .form form .field-first-name input &lbrace;
  border: 1px solid #ccc;
  padding: 8px;
  border-radius: 4px;
&rbrace;

```

+++

### Listrutekomponent

I listrutor används elementet `select` i stället för ett `input`-element:

+++ HTML-struktur för nedrullningskomponent

```HTML

<div class="{Type}-wrapper field-{Name} field-wrapper" data-required={Required}>
   &lt;label for="{FieldId}" class="field-label">First Name&lt;/label>
   &lt;input type="{Type}" placeholder="{Placeholder}" maxlength="{Max}" id={FieldId}" name="{Name}" aria-describedby="{FieldId}-description">
   <div class="field-description" aria-live="polite" id="{FieldId}-description">
    Hint - First name should be minimum 3 characters and a maximum of 10 characters.
   </div>
</div>

```

**Exempel på HTML-struktur**

```HTML

<div class="drop-down-wrapper field-country field-wrapper" data-required="true">
  &lt;label for="country" class="field-label">Country&lt;/label>
  &lt;select id="country" name="country">
    &lt;option value="">Select Country&lt;/option>
    &lt;option value="US">United States&lt;/option>
    &lt;option value="CA">Canada&lt;/option>
  &lt;/select>
  <div class="field-description" aria-live="polite" id="country-description">
    Please select your country of residence.
  </div>
</div>

```

+++

+++ CSS-väljare för nedrullningskomponent

Följande CSS visar några exempel på CSS-väljare för nedrullningsbara komponenter.

```CSS

/* Target the outer wrapper */
main .form form .drop-down-wrapper &lbrace;
  /* Add your styles here */
  display: flex;
  flex-direction: column;
  margin-bottom: 15px;
&rbrace;

/* Style the label */
main .form form .drop-down-wrapper .field-label &lbrace;
  margin-bottom: 5px;
  font-weight: bold;
&rbrace;

```
* Ange som mål för wrapper: Den första väljaren (`.drop-down-wrapper`) anger det yttre wrapper-elementet som mål, vilket garanterar att formaten tillämpas på hela listrutekomponenten.
* Flexbox Layout: Flexbox ordnar etiketten, listrutan och beskrivningen lodrätt för en ren layout.
* Etikettformatering: Etiketten sticker ut med en större teckensnittsvikt och en liten marginal.
* Formatering i listrutor: Elementet `select` får en kantlinje, utfyllnad och rundade hörn för en elegant look.
* Bakgrundsfärg: En konsekvent bakgrundsfärg ställs in för visuell harmoni.
* Anpassning av pilar: Valfria format döljer den nedrullningsbara standardpilen och skapar en anpassad pil med Unicode-tecken och placering.

+++

---

### Alternativgrupper

Ungdomsgrupper har en egen HTML-struktur och CSS-struktur, precis som komponenter i listrutor:

+++ HTML Structure of Radio Group

```HTML

&lt;fieldset class="radio-group-wrapper field-{Name} field-wrapper" id="{FieldId}" name="{Name}" data-required="{Required}">
   &lt;legend for="{FieldId}" class="field-label">....&lt;/legend>
   <% for each radio in Group %>
   <div class="radio-wrapper field-{Name}">
      &lt;input type="radio" value="" id="{UniqueId}" data-field-type="radio-group" name="{FieldId}">
      &lt;label for="{UniqueId}" class="field-label">...&lt;/label>
   </div>
   <% end for %>
&lt;/fieldset>

```

**Exempel på HTML-struktur**

```HTML

&lt;fieldset class="radio-group-wrapper field-color field-wrapper" id="color_preference" name="color_preference" data-required="true">
  &lt;legend for="color_preference" class="field-label">Favorite Color:&lt;/legend>
  <% for each radio in Group %>
    <div class="radio-wrapper field-color">
      &lt;input type="radio" value="red" id="color_red" data-field-type="radio-group" name="color_preference">
      &lt;label for="color_red" class="field-label">Red&lt;/label>
    </div>
    <div class="radio-wrapper field-color">
      &lt;input type="radio" value="green" id="color_green" data-field-type="radio-group" name="color_preference">
      &lt;label for="color_green" class="field-label">Green&lt;/label>
    </div>
    <div class="radio-wrapper field-color">
      &lt;input type="radio" value="blue" id="color_blue" data-field-type="radio-group" name="color_preference">
      &lt;label for="color_blue" class="field-label">Blue&lt;/label>
    </div>
  <% end for %>
&lt;/fieldset>

```

+++

+++ CSS-väljare för alternativknappar

* Ange fältuppsättningen

```CSS

  main .form form .radio-group-wrapper &lbrace;
    border: 1px solid #ccc;
    padding: 10px;
  &rbrace;

```
Den här väljaren anger alla fältuppsättningar med klassen Radio-Group-wrapper som mål. Det är användbart om du vill använda allmänna format på hela alternativgruppen.

* Egenskaper för alternativknappar

```CSS

main .form form .radio-wrapper label &lbrace;
    font-weight: normal;
    margin-right: 10px;
  &rbrace;

```

* Ange alla alternativknappsetiketter för ett specifikt fält baserat på dess namn

```CSS

main .form form .field-color .radio-wrapper label &lbrace;
  /* Your styles here */
&rbrace;

```

+++

### Kryssrutegrupper

+++ HTML Structure of Checkbox Group

```HTML

&lt;fieldset class="checkbox-group-wrapper field-{Name} field-wrapper" id="{FieldId}" name="{Name}" data-required="{Required}">
   &lt;legend for="{FieldId}" class="field-label">....&lt;/legend>
   <% for each radio in Group %>
   <div class="radio-wrapper field-{Name}">
      &lt;input type="checkbox" value="" id="{UniqueId}" data-field-type="checkbox-group" name="{FieldId}">
      &lt;label for="{UniqueId}" class="field-label">...&lt;/label>
   </div>
   <% end for %>
&lt;/fieldset>

```

**Exempel på HTML-struktur**

```HTML

&lt;fieldset class="checkbox-group-wrapper field-topping field-wrapper" id="topping_preference" name="topping_preference" data-required="false">
  &lt;legend for="topping_preference" class="field-label">Pizza Toppings:&lt;/legend>
  <div class="checkbox-wrapper field-topping">
    &lt;input type="checkbox" value="pepperoni" id="topping_pepperoni" data-field-type="checkbox-group" name="topping_preference">
    &lt;label for="topping_pepperoni" class="field-label">Pepperoni&lt;/label>
  </div>
  <div class="checkbox-wrapper field-topping">
    &lt;input type="checkbox" value="mushrooms" id="topping_mushrooms" data-field-type="checkbox-group" name="topping_preference">
    &lt;label for="topping_mushrooms" class="field-label">Mushrooms&lt;/label>
  </div>
  <div class="checkbox-wrapper field-topping">
    &lt;input type="checkbox" value="onions" id="topping_onions" data-field-type="checkbox-group" name="topping_preference">
    &lt;label for="topping_onions" class="field-label">Onions&lt;/label>
  </div>
&lt;/fieldset>

```

+++

+++ CSS-väljare för kryssrutegrupper

* Ange som mål för den yttre omslutningen: Dessa väljare har de yttre behållarna för både alternativknappar och kryssrutegrupper som mål, vilket gör att du kan använda allmänna format för hela gruppstrukturen. Det här är användbart när du vill ange avstånd, justering eller andra layoutrelaterade egenskaper.

```CSS

  
  /* Targets radio group wrappers */
  main .form form .radio-group-wrapper &lbrace;
    margin-bottom: 20px; /* Adds space between radio groups */  
  &rbrace;

  /* Targets checkbox group wrappers */
  main .form form .checkbox-group-wrapper &lbrace;
    margin-bottom: 20px; /* Adds space between checkbox groups */
  &rbrace;

```

* Målgruppsetiketter: Den här väljaren anger elementet `.field-label` som mål i gruppomslutningar för både alternativknappar och kryssrutor. På så sätt kan du formatera etiketterna specifikt för dessa grupper, vilket kan få dem att sticka ut mer.

```CSS

main .form form .radio-group-wrapper legend,
main .form form .checkbox-group-wrapper legend &lbrace;
  font-weight: bold; /* Makes the group label bold */
&rbrace;

```

* Indata och etiketter för enskilda användare: Dessa väljare ger mer exakt kontroll över enskilda alternativknappar, kryssrutor och tillhörande etiketter. Du kan använda dessa för att justera storlek, avstånd eller använda mer distinkta visuella format.

```CSS

/* Styling radio buttons */
main .form form .radio-group-wrapper input[type="radio"] &lbrace;
  margin-right: 5px; /* Adds space between the input and its label */
&rbrace;

/* Styling radio button labels */
main .form form .radio-group-wrapper label &lbrace;
  font-size: 15px; /* Changes the label font size */
&rbrace;

/* Styling checkboxes */
main .form form .checkbox-group-wrapper input[type="checkbox"] &lbrace;
  margin-right: 5px; /* Adds space between the input and its label */
&rbrace;

/* Styling checkbox labels */
main .form form .checkbox-group-wrapper label &lbrace;
  font-size: 15px; /* Changes the label font size */
&rbrace;

```

* Anpassa utseendet på alternativknappar och kryssrutor: Den här tekniken döljer standardindata och använder `:before` och `:after` pseudoelement för att skapa anpassade bilder som ändrar utseende baserat på markerat läge.

```CSS

/* Hide the default radio button or checkbox */
main .form form .radio-group-wrapper input[type="radio"],
main .form form .checkbox-group-wrapper input[type="checkbox"] &lbrace;
  opacity: 0;
  position: absolute;
&rbrace;

/* Create a custom radio button */
main .form form .radio-group-wrapper input[type="radio"] + label::before &lbrace;
  /* ... styles for custom radio button ... */
&rbrace;

main .form form .radio-group-wrapper input[type="radio"]:checked + label::before &lbrace;
  /* ... styles for checked radio button ... */
&rbrace;

/* Create a custom checkbox */
main .form form .checkbox-group-wrapper input[type="checkbox"] + label::before &lbrace;
  /* ... styles for custom checkbox ... */
&rbrace;

main .form form .checkbox-group-wrapper input[type="checkbox"]:checked + label::before &lbrace;
  /* ... styles for checked checkbox ... */
&rbrace;

```

+++

### Panel-/behållarkomponenter

+++ HTML-struktur för paneler/behållarkomponenter

```HTML

&lt;fieldset class="panel-wrapper field-{PanelName} field-wrapper">
  &lt;legend for="{id}" class="field-label" data-visible="false">bannerComponent&lt;/legend>
  <div class="{Type}-wrapper field-{Name} field-wrapper">
    &lt;label for="{FieldId}" class="field-label">First Name&lt;/label>
    &lt;input type="{Type}" placeholder="{Placeholder}" maxlength="{Max}" id={FieldId}" name="{Name}">
    <div class="field-description" aria-live="polite" id="{FieldId}-description">
      Hint - First name should be minimum 3 characters and a maximum of 10 characters.
    </div>
  </div>
&lt;/fieldset>

```

**Exempel på HTML-struktur**

```HTML

&lt;fieldset class="panel-wrapper field-login field-wrapper">
  &lt;legend for="login" class="field-label" data-visible="false">Login Information&lt;/legend>
  <div class="text-wrapper field-username field-wrapper">
    &lt;label for="username" class="field-label">Username&lt;/label>
    &lt;input type="text" placeholder="Enter your username" maxlength="50" id="username" name="username">
    <div class="field-description" aria-live="polite" id="username-description">
      Please enter your username or email address.
    </div>
  </div>
  <div class="password-wrapper field-password field-wrapper">
    &lt;label for="password" class="field-label">Password&lt;/label>
    &lt;input type="password" placeholder="Enter your password" maxlength="20" id="password" name="password">
    <div class="field-description" aria-live="polite" id="password-description">
      Your password must be at least 8 characters long.
    </div>
  </div>
&lt;/fieldset>

```

* Fältuppsättningselementet fungerar som panelbehållare med klassens panelwrapper och ytterligare klasser för formatering baserat på panelnamnet (fältinloggning).
* Förklaringselementet (<legend>) fungerar som panelrubrik med texten&quot;Inloggningsinformation&quot; och klassens fältetikett. Attributet data-visible=&quot;false&quot; kan användas med JavaScript för att styra visningen av titeln.
* I fältuppsättningen, multipel.{Type}-wrapper-element (.text-wrapper och .password-wrapper i det här fallet) representerar enskilda formulärfält på panelen.
* Varje wrapper innehåller en etikett, ett inmatningsfält och en beskrivning, som liknar de föregående exemplen.

+++

+++ Exempel på CSS-väljare för panel-/behållarkomponenter

1. Panelen:

```CSS

  /* Target the entire panel container */
  main .form form .panel-wrapper &lbrace;
    /* Add your styles here (e.g., border, padding, background color) */
    border: 1px solid #ccc;
    padding: 15px;
    border-radius: 4px;
    margin-bottom: 20px;
 &rbrace;

```

* `.panel-wrapper`-väljaren formaterar alla element med klassens panelwrapper, vilket ger ett konsekvent utseende för alla paneler.

1. Ange paneltiteln som mål:

```CSS

  /* Target the legend element (panel title) */
  .panel-wrapper legend &lbrace;
    /* Add your styles here (e.g., font-weight, font-size) */
    font-weight: bold;
    font-size: 16px;
    padding-bottom: 5px;
    margin-bottom: 10px;
    border-bottom: 1px solid #ddd; /* Optional: create a separation line */
  &rbrace;

```

* `.panel-wrapper legend`-väljaren formaterar förklaringselementet på panelen, så att titeln sticker ut visuellt.


1. Ange enskilda fält som mål på panelen:

```CSS

/* Target all form field wrappers within a panel */
main .form form .panel-wrapper .{Type}-wrapper &lbrace;
  /* Add your styles here (e.g., margin) */
  margin-bottom: 10px;
&rbrace;

```

* `.panel-wrapper .{Type}-wrapper`-väljaren anger alla omslutningar med klassen `.{Type}-wrapper` på panelen som mål, vilket gör att du kan formatera mellanrummet mellan formulärfält.

1. Målspecifika fält (valfritt):

```CSS

  /* Target the username field wrapper */
  main .form form .panel-wrapper .text-wrapper.field-username &lbrace;
    /* Add your styles here (specific to username field) */
  &rbrace;

  /* Target the password field wrapper */
  main .form form .panel-wrapper .password-wrapper.field-password &lbrace;
    /* Add your styles here (specific to password field) */
  &rbrace;

```

* Dessa väljare gör att du kan rikta in dig på specifika fältbrytningar på panelen för unik formatering, t.ex. markera användarnamnsfältet.

+++

### Repeterbar panel

+++ HTML-struktur för en upprepningsbar panel

```HTML

&lt;fieldset class="panel-wrapper field-{PanelName} field-wrapper">
  &lt;legend for="{id}" class="field-label" data-visible="false">bannerComponent&lt;/legend>
  <div class="{Type}-wrapper field-{Name} field-wrapper">
    &lt;label for="{FieldId}" class="field-label">First Name&lt;/label>
    &lt;input type="{Type}" placeholder="{Placeholder}" maxlength="{Max}" id={FieldId}" name="{Name}">
    <div class="field-description" aria-live="polite" id="{FieldId}-description">
      Hint - First name should be minimum 3 characters and a maximum of 10 characters.
    </div>
&lt;/fieldset>

```

**Exempel på HTML-struktur**

```HTML

&lt;fieldset class="panel-wrapper field-contact field-wrapper" data-repeatable="true">
  &lt;legend for="contact-1" class="field-label" data-visible="false">Contact Information&lt;/legend>
  <div class="text-wrapper field-name field-wrapper">
    &lt;label for="name-1" class="field-label">Name&lt;/label>
    &lt;input type="text" placeholder="Enter your name" maxlength="50" id="name-1" name="contacts[0].name">
    <div class="field-description" aria-live="polite" id="name-1-description">
      Please enter your full name.
    </div>
  </div>
  <div class="email-wrapper field-email field-wrapper">
    &lt;label for="email-1" class="field-label">Email&lt;/label>
    &lt;input type="email" placeholder="Enter your email address" maxlength="100" id="email-1" name="contacts[0].email">
    <div class="field-description" aria-live="polite" id="email-1-description">
      Please enter a valid email address.
    </div>
  </div>
&lt;/fieldset>

&lt;fieldset class="panel-wrapper field-contact field-wrapper" data-repeatable="true">
  &lt;legend for="contact-2" class="field-label" data-visible="false">Contact Information&lt;/legend>
  <div class="text-wrapper field-name field-wrapper">
    &lt;label for="name-2" class="field-label">Name&lt;/label>
    &lt;input type="text" placeholder="Enter your name" maxlength="50" id="name-2" name="contacts[1].name">
    <div class="field-description" aria-live="polite" id="name-2-description">
      Please enter your full name.
    </div>
  </div>
  <div class="email-wrapper field-email field-wrapper">
    &lt;label for="email-2" class="field-label">Email&lt;/label>
    &lt;input type="email" placeholder="Enter your email address" maxlength="100" id="email-2" name="contacts[1].email">
    <div class="field-description" aria-live="polite" id="email-2-description">
      Please enter a valid email address.
    </div>
  </div>
&lt;/fieldset>

```

Varje panel har samma struktur som exemplet med en panel, med ytterligare attribut:

* data-repetable=&quot;true&quot;: Det här attributet anger att panelen kan upprepas dynamiskt med JavaScript eller ett ramverk.

* Unika ID:n och namn: Varje element i panelen har ett unikt ID (till exempel name-1, email-1) och name-attribut baserat på panelens indexvärde (till exempel name=&quot;contact[0].name&quot;). Detta gör att data kan samlas in korrekt när flera paneler skickas.

+++

+++ CSS-väljare för en upprepningsbar panel

* Alla upprepningsbara paneler som mål:

```CSS

  /* Target all panels with the repeatable attribute */
 main .form form .panel-wrapper[data-repeatable="true"] &lbrace;
    /* Add your styles here (e.g., border, margin) */
    border: 1px solid #ccc;
    padding: 15px;
    border-radius: 4px;
    margin-bottom: 20px;
  &rbrace;

```

Väljaren formaterar alla paneler som kan upprepas, vilket ger ett konsekvent utseende och känsla.


* Ange enskilda fält som mål på en panel:

```CSS

/* Target all form field wrappers within a repeatable panel */
main .form form .panel-wrapper[data-repeatable="true"] .{Type}-wrapper &lbrace;
  /* Add your styles here (e.g., margin) */
  margin-bottom: 10px;
&rbrace;

```
Den här väljaren formaterar alla fältomslutningar på en repeterbar panel, vilket ger ett konsekvent avstånd mellan fälten.

* Ange specifika fält som mål (inom en panel):

```CSS

/* Target the name field wrapper within the first panel */
main .form form .panel-wrapper[data-repeatable="true"][data-index="0"] .text-wrapper.field-name &lbrace;
  /* Add your styles here (specific to first name field) */
&rbrace;

/* Target all

```

+++

### Bifogad fil

+++ HTML-struktur för bifogad fil

```HTML

<div class="file-wrapper field-{FileName} field-wrapper">
  &lt;legend for="{id}" class="field-label" data-visible="false"> File Attachment &lt;/legend>
  <div class="file-drag-area">
    <div class="file-dragIcon"></div>
    <div class="file-dragText">Drag and Drop To Upload</div>
    &lt;button class="file-attachButton" type="button">Attach&lt;/button>
    &lt;input type="file" accept="audio/*, video/*, image/*, text/*, application/pdf" id="{id}" name="{FileName}" autocomplete="off" multiple="" required="required">
  </div>
  <div class="files-list">
    <div data-index="0" class="file-description">
      <span class="file-description-name">ClaimForm.pdf</span>
      <span class="file-description-size">26 kb</span>
      &lt;button class="file-description-remove" type="button">&lt;/button>
    </div>
  </div>
</div>

```

**Exempel på HTML-struktur**


```HTML

<div class="file-wrapper field-claim_form field-wrapper">
  &lt;legend for="claim_form" class="field-label" data-visible="false">File Attachment&lt;/legend>
  <div class="file-drag-area">
    <div class="file-dragIcon"></div>
    <div class="file-dragText">Drag and Drop To Upload</div>
    &lt;button class="file-attachButton" type="button">Attach&lt;/button>
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
main .form form .file-wrapper &lbrace;
  /* Add your styles here (e.g., border, padding) */
  border: 1px solid #ccc;
  padding: 15px;
  border-radius: 4px;
  margin-bottom: 20px;
&rbrace;

```

Den här väljaren formaterar hela den bifogade filkomponenten, inklusive teckenförklaringen, dragningsområdet, inmatningsfältet och listan.

* Målinriktade specifika element:

```CSS

/* Target the drag and drop area */
main .form form .file-wrapper .file-drag-area &lbrace;
  /* Add your styles here (e.g., background color, border) */
  background-color: #f0f0f0;
  border: 1px dashed #ddd;
  padding: 10px;
  text-align: center;
&rbrace;

/* Target the file input element */
main .form form .file-wrapper input[type="file"] &lbrace;
  /* Add your styles here (e.g., hide the default input) */
  display: none;
&rbrace;

/* Target individual file descriptions within the list (populated dynamically) */
main .form form .file-wrapper .files-list .file-description &lbrace;
  /* Add your styles here (e.g., margin, display) */
  display: flex;
  justify-content: space-between;
  margin-bottom: 5px;
&rbrace;

/* Target the file name within the description */
main .form form .file-wrapper .files-list .file-description .file-description-name &lbrace;
  /* Add your styles here (e.g., font-weight) */
  font-weight: bold;
&rbrace;

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
   &lt;label for="{FieldId}" class="field-label">First Name&lt;/label>
   &lt;input type="{Type}" placeholder="{Placeholder}" maxlength="{Max}" id={FieldId}" name="{Name}" aria-describedby="{FieldId}-description">
   <div class="field-description" aria-live="polite" id="{FieldId}-description">
    Hint - First name should be minimum 3 characters and a maximum of 10 characters.
   </div>
</div>

```

**Exempel på HTML-struktur**

```HTML

<div class="text-wrapper field-name field-wrapper" data-required="true">
  &lt;label for="name" class="field-label">Name&lt;/label>
  &lt;input type="text" placeholder="Enter your name" maxlength="50" id="name" name="name">
</div>

<div class="number-wrapper field-age field-wrapper" data-required="true">
  &lt;label for="age" class="field-label">Age&lt;/label>
  &lt;input type="number" placeholder="Enter your age" id="age" name="age">
</div>

<div class="email-wrapper field-email field-wrapper" data-required="true">
  &lt;label for="email" class="field-label">Email Address&lt;/label>
  &lt;input type="email" placeholder="Enter your email" id="email" name="email">
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
main .form form .text-wrapper input &lbrace;
  /* Add your styles here */
&rbrace;

/* Target all number input fields */
main .form form .number-wrapper input &lbrace;
  /* Add your styles here */
  letter-spacing: 2px; /* Example for adding letter spacing to all number fields */
&rbrace;

```

+++

### Formatering baserad på fältnamn

Du kan också ange enskilda fält som mål efter namn för att använda unika format.

+++ HTML Structure

```HTML

<div class="{Type}-wrapper field-{Name} field-wrapper" data-required={Required}>
   &lt;label for="{FieldId}" class="field-label">First Name&lt;/label>
   &lt;input type="{Type}" placeholder="{Placeholder}" maxlength="{Max}" id="{FieldId}" name="{Name}" aria-describedby="{FieldId}-description">
   <div class="field-description" aria-live="polite" id="{FieldId}-description">
    Hint - Enter the 6 digit number sent to your mobile number.
   </div>
</div>

```

**Exempel på HTML-struktur**

```HTML

<div class="number-wrapper field-otp field-wrapper" data-required="true">
  &lt;label for="otp" class="field-label">OTP&lt;/label>
  &lt;input type="number" placeholder="Enter your OTP" maxlength="6" id="otp" name="otp" aria-describedby="otp-description">
  <div class="field-description" aria-live="polite" id="otp-description">
    Hint - Enter the 6 digit number sent to your mobile number.
   </div>
</div>

```

+++

+++ Exempel på CSS-väljare

```CSS

main .form form .field-otp input &lbrace;
   letter-spacing: 2px
&rbrace;

```

Den här CSS-koden har alla indataelement som finns i ett element som har klassen `field-otp` som mål. Formulärets HTML-struktur följer konventionerna i det adaptiva Forms-blocket, vilket innebär att det finns en behållare som är markerad med klassen&quot;field-out&quot; som innehåller fältet med namnet&quot;otp&quot;.

+++




## Se även

{{universal-editor-see-also}}

---
title: AEM Forms Edge Delivery Service
description: AEM Forms Edge Delivery Service har tagits fram för bästa prestanda och ger er möjlighet att förutse framtiden för smidig datainsamling och användarengagemang. I artikeln listas alla formulärkomponenter som är tillgängliga i rutan för EDD-formulär.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: 3b24d0cd4099e0b8eb48c977f460b25c168af220
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 0%

---




# Formulärkomponenter

Med formulärblocket kan du enkelt skapa formulär för att hämta in och lagra inhämtade data. Den har stöd för komponenter som baseras på HTML5 [indatatyper](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#input_types) som text, e-post, nummer, datum och många andra. Den har även stöd för [textområde](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea), [välj](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select)och [fältuppsättning](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset) och innehåller indatavalideringsfunktioner som är inbyggda i HTML5.

Formulärblocket genererar en enhetlig HTML-struktur för alla fälttyper och behållare (paneler) för att säkerställa konsekvens. Denna enhetliga struktur gör det enklare att [formatera ett formulär](/help/edge/docs/forms/style-theme-forms.md).


## Komponentegenskaper

Följande egenskaper stöds för formulärkomponenter i formulärblocket:

<table>
 <tbody>
  <tr>
   <td><b>Egenskap</b> </td>
   <td><b>Formulärkomponenter (indatatyp)</b> </td>
   <td><b>Information</b></td>
  </tr>
  <tr>
   <td>Namn</td>
   <td>Alla komponenter</td>
   <td> En sträng som anger ett namn för komponenten. Komponentens data skickas mot det här namnet.
   </td>
  </tr>
  <tr>
   <td>Etikett</td>
   <td>Alla komponenter</td>
   <td> Etiketten fungerar som bildtext för fältet.
   </td>
  </tr>
  <tr>
   <td>Värde</td>
   <td>Alla komponenter</td>
   <td> Kontrollens startvärde. För alternativknappar och kryssrutekomponenter är detta det värde/de data som skickas när de väljs. Attributet value är alltid valfritt, men det bör vara obligatoriskt för kryssrutor och alternativknappar.
   </td>
  </tr>
    <tr>
   <td>Platshållare</td>
   <td>Text, sökning, URL, telefon, e-post, lösenord och nummer</td>
   <td> Platshållarattributet ger användaren ett kort tips om vilken typ av information som förväntas i fältet.
   </td>
  </tr>
      <tr>
   <td>Beskrivning</td>
   <td>Gäller för alla fält</td>
   <td> Platshållarattributet ger användaren ett kort tips om vilken typ av information som förväntas i fältet.
   </td>
  </tr>
  </tbody>
</table>

<!-- 
## Supported HTML 5 input types in Form Block

The Form Block supports a range of HTML 5 input types, and it also seamlessly renders forms created with AEM core components.

Here is the table which outlines how core components correspond to their HTML-5 input types in Edge Delivery:

<table>
 <tbody>
  <tr>
   <td><b>Core Components</b> </td>
   <td><b>HTML 5 input type</b> </td>
   <td><b>Details</b></td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/form-container.html">Form Container</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#form">form </td>
   <td> Create a form to capture user inputs.
   </td>
  </tr>
  <tr>
   <td><a herf="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/text-input.html">Text Input</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/text">text</a></td>
   <td> Defines a single-line text input field. </td>
  </tr>
  <tr>
   <td><a href = "https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/number-input.html">Number Input</a></td>
   <td><a href = "https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/number">number</a></td>
   <td>Lets user  enter a number input. You can also add built-in validation to reject non-numerical inputs. Lets user  enter a number input. You can also add built-in validation to reject non-numerical inputs. Initially, the input field is displayed as a number input. If a user applies a display pattern, it changes to text to allow the author to apply number formatting, since HTML 5 lacks support for display patterns. However, when the user clicks it, it returns to typing numbers.</td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/date-picker.html">Date Picker</a></td>
   <td><a href = "https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/date">date </a></td>
   <td> Create an input field for entering a date. You have the option to input the date either through a text box, which validates the entry, or through a dedicated date picker interface. Initially, the native date input field is displayed. If a user applies a display pattern, it changes to text to allow the user to apply formatting, since HTML 5 lacks support for display patterns. However, when the user clicks it, it returns to typing a date.</td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/file-attachment.html">File Attachment</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/file">file</a></td>
   <td> Allows user to choose one or more files from the device storage. It supports enhanced file input validations, such as accepted file types, file size restrictions, and minimum/maximum file selection limits. </td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/drop-down.html"> Dropdown List</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select">select</a></td>
   <td> Allows users to select one or more options from a list of predefined options. The options can be of type String, Number, or Boolean.</td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/checkbox-group.html">Checkbox Group</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/checkbox">multiple checkbox</a></td>
   <td> Allow users to select one or more options from a list. Multiple checkboxes are generated with identical names, each corresponding to an item in the enum. </td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/radio-button.html">Radio Button Group</td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/radio">multiple radio</a></td>
   <td> Allows a user to select one option from a group of related options. Multiple radio buttons are generated with identical names, each corresponding to an item in the enum.</td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/button.html">Button</td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/button">button</a></td>
   <td>A UI element that allows users to trigger an action when clicked. </td>
  </tr>
  <tr>
   <td><a href =""https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel-container.html">Panel</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset">fieldset with legend</a></td>
   <td> Group sections within a form, where a nested *legend* element adds a caption for the form.</td>
  </tr>
   <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard.html">Wizard</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset">fieldset</a></td>
   <td>Groups related sections within a form. It also controls the arrangement, supporting display options for positioning them at the top or at the left side. </td>
  </tr>
    <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/text.html">Text</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/p">p</a></td>
   <td>A p tag marks a paragraph. In visual content, paragraphs are chunks of text separated by blank lines or an indented first line</td>
  </tr>
     <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/submit-button.html">Submit button</td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/submit">submit</a></td>
   <td> A UI element that enables users to submit a form to the server upon clicking. If a user adds a submit rule to a button, it functions as the submit button. </td>
  </tr>
     <tr>
   <td><a href = "https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/reset-button.html">Reset button</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/reset">reset</a></td>
   <td>A UI element that resets a form upon clicking. If a user adds a reset rule to a button, it functions as the reset button. </td>
  </tr>
    <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/email-input.html">Email Input</td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/email">email</a></td>
   <td> Allows the user to enter and edit an email address. If the user adds the multiple attributes, a list of email addresses can be added or edited.</td>
  </tr>
   <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/telephone-input.html">Telephone Input</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/tel">tel</a></td>
   <td>Allows user to enter and edit a telephone number.</td>
  </tr>
   <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/header.html">Header</td>
   <td><a href = "https://developer.mozilla.org/en-US/docs/Web/HTML/Element/header"> header</a></td>
   <td>It includes introductory content, typically a group of introductory or navigational aids. It is supported outside Form container. </td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/footer.html">Footer</td>
   <td><a href = "https://developer.mozilla.org/en-US/docs/Web/HTML/Element/footer">footer</a></td>
   <td> Contains information such as copyright data or links to related documents. It is supported outside Form container.</td>
  </tr>
  <tr>
   <td><a href = "https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion.html">Accordion<a></td>
   <td><i>Not yet supported in Form Block</i></td>
   <td> Allows user to create expandable and collapsible sections in a form. </td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/horizontal-tabs.html">Horizontal tabs</a></td>
   <td><i>Not yet supported in Form Block</i></td>
   <td>Organizes multiple sections of a form into separate tabs which are displayed horizontally.</td>
  </tr>
  <tr>
   <td><a href = "https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/image.html">Image</a></td>
   <td><i>Not yet supported in Form Block</i></td>
   <td> Allows user to include images in a form.</td>
  </tr><tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/title.html">Title</a></td>
   <td><i>Not yet supported in Form Block</i></td>
   <td> Refers to the text that appears at the top of the form. </td>
  </tr>
  <tr>
   <td><a href = "https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/submit-button.html">Switch</td>
   <td><i>Not yet supported in Form Block</i></td>
   <td> A two-state toggle that allows user to select between two states such as enabling or disabling a feature, setting, or functionality.</td>
  </tr>
 </tbody>
</table>

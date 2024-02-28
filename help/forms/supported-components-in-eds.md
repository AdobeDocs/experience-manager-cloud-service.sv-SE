---
title: AEM Forms Edge Delivery Service Form Components
description: AEM Forms Edge Delivery Service har tagits fram för bästa prestanda och ger er möjlighet att förutse framtiden för smidig datainsamling och användarengagemang. I artikeln listas alla formulärkomponenter som är tillgängliga i rutan för EDD-formulär.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: 1dc4915f0b149ef67dfa22c8d4c6be7538170d38
workflow-type: tm+mt
source-wordcount: '871'
ht-degree: 0%

---




# HTML-komponenter som stöds i Form Block Edge Delivery

AEM Forms Edge Delivery innehåller ett formulärblock. Med formulärblocket kan du enkelt skapa formulär för att hämta in och lagra inhämtade data.

Formulärblocket har stöd för HTML-5-komponenter som text, e-post, nummer, datum och många fler. Det har också stöd för textområdes-, markerings- och fältuppsättningselement, och innehåller indatavalideringsfunktioner som är inbyggda i HTML-5. Formulärblocket skapar en enhetlig HTML-struktur för alla fälttyper och behållare som säkerställer enhetlighet. Du också [formatera fälttyperna](https://adobe-rnd.github.io/form-block/customization/styling_form) med `form.css` -fil.

## Indatatyper som stöds i HTML 5 i formulärblocket

Formulärblocket har stöd för en rad olika indatatyper för HTML 5, och det återger även smidigt formulär som skapats med AEM kärnkomponenter.

Här följer tabellen som visar hur kärnkomponenterna motsvarar indatatyperna HTML-5 i Edge Delivery:

<table>
 <tbody>
  <tr>
   <td><b>Kärnkomponenter</b> </td>
   <td><b>Indatatypen HTML 5</b> </td>
   <td><b>Information</b></td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/form-container.html">Formulärbehållare</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#form">formulär </td>
   <td> Skapa ett formulär för att hämta användarindata.
   </td>
  </tr>
  <tr>
   <td><a herf="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/text-input.html">Textindata</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/text">text</a></td>
   <td> Definierar ett textinmatningsfält med en rad. </td>
  </tr>
  <tr>
   <td><a href = "https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/number-input.html">Nummerindata</a></td>
   <td><a href = "https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/number">tal</a></td>
   <td>Användaren kan ange ett tal. Du kan också lägga till inbyggd validering för att avvisa icke-numeriska indata. Användaren kan ange ett tal. Du kan också lägga till inbyggd validering för att avvisa icke-numeriska indata. Inledningsvis visas inmatningsfältet som ett tal. Om en användare använder ett visningsmönster ändras det till text så att författaren kan använda nummerformatering, eftersom HTML 5 saknar stöd för visningsmönster. När användaren klickar på den återgår den dock till att skriva siffror.</td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/date-picker.html">Datumväljaren</a></td>
   <td><a href = "https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/date">datum </a></td>
   <td> Skapa ett inmatningsfält för att ange ett datum. Du kan ange datumet antingen via en textruta som validerar inmatningen eller via ett dedikerat datumväljargränssnitt. Inledningsvis visas inmatningsfältet för inmatningsdatum. Om en användare använder ett visningsmönster ändras det till text så att användaren kan använda formatering, eftersom HTML 5 saknar stöd för visningsmönster. När användaren klickar på den återgår den dock till att skriva ett datum.</td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/file-attachment.html">Bifogad fil</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/file">fil</a></td>
   <td> Låter användaren välja en eller flera filer från enhetens lagringsutrymme. Det har stöd för utökade filindatavalideringar, t.ex. godkända filtyper, begränsningar av filstorlek och gränser för minsta/högsta filurval. </td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/drop-down.html"> Listruta</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select">välj</a></td>
   <td> Tillåter användare att välja ett eller flera alternativ i en lista med fördefinierade alternativ. Alternativen kan vara av typen String, Number eller Boolean.</td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/checkbox-group.html">Kryssrutegrupp</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/checkbox">flera kryssrutor</a></td>
   <td> Tillåt användare att välja ett eller flera alternativ i en lista. Flera kryssrutor skapas med identiska namn, som alla motsvarar ett objekt i uppräkningen. </td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/radio-button.html">Grupp med alternativknappar</td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/radio">flera radioapparater</a></td>
   <td> Låter en användare välja ett alternativ i en grupp med relaterade alternativ. Flera alternativknappar genereras med identiska namn, som alla motsvarar ett objekt i uppräkningen.</td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/button.html">Knapp</td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/button">knapp</a></td>
   <td>Ett UI-element som gör att användare kan utlösa en åtgärd när de klickar. </td>
  </tr>
  <tr>
   <td><a href="" https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel-container.html">Panel</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset">fältuppsättning med teckenförklaring</a></td>
   <td> Gruppera avsnitt i ett formulär där ett kapslat *legend*-element lägger till en beskrivning för formuläret.</td>
  </tr>
   <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard.html">guide</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset">fältuppsättning</a></td>
   <td>Grupperar relaterade avsnitt i ett formulär. Det styr också ordningen, med stöd för visningsalternativ för placering överst eller till vänster. </td>
  </tr>
    <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/text.html">Text</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/p">p</a></td>
   <td>Ett p-märkord markerar ett stycke. I visuellt innehåll är stycken textstycken som avgränsas med tomma rader eller en indragen första rad</td>
  </tr>
     <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/submit-button.html">Skicka-knapp</td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/submit">skicka</a></td>
   <td> A UI element that allows users to submit a form to the server when clicking. Om en användare lägger till en skicka-regel till en knapp fungerar den som skicka-knappen. </td>
  </tr>
     <tr>
   <td><a href = "https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/reset-button.html">Knappen Återställ</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/reset">återställ</a></td>
   <td>A UI element that resets a form when clicking. Om en användare lägger till en återställningsregel till en knapp fungerar den som återställningsknapp. </td>
  </tr>
    <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/email-input.html">E-postindata</td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/email">e-post</a></td>
   <td> Låter användaren ange och redigera en e-postadress. Om användaren lägger till flera attribut kan en lista med e-postadresser läggas till eller redigeras.</td>
  </tr>
   <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/telephone-input.html">Telefonindata</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/tel">tel</a></td>
   <td>Användare kan ange och redigera ett telefonnummer.</td>
  </tr>
   <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/header.html">Sidhuvud</td>
   <td><a href = "https://developer.mozilla.org/en-US/docs/Web/HTML/Element/header"> header</a></td>
   <td>Det innehåller introduktionsinnehåll, vanligtvis en grupp med introduktions- eller navigeringshjälpmedel. Det stöds utanför formulärbehållaren. </td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/footer.html">Sidfot</td>
   <td><a href = "https://developer.mozilla.org/en-US/docs/Web/HTML/Element/footer">sidfot</a></td>
   <td> Innehåller information som copyrightdata eller länkar till relaterade dokument. Det stöds utanför formulärbehållaren.</td>
  </tr>
  <tr>
   <td><a href = "https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion.html">Dragspel<a></td>
   <td><i>Stöds ännu inte i formulärblocket</i></td>
   <td> Används för att skapa utökningsbara och komprimerbara avsnitt i ett formulär. </td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/horizontal-tabs.html">Vågräta flikar</a></td>
   <td><i>Stöds ännu inte i formulärblocket</i></td>
   <td>Ordnar flera avsnitt i ett formulär i separata flikar som visas vågrätt.</td>
  </tr>
  <tr>
   <td><a href = "https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/image.html">Bild</a></td>
   <td><i>Stöds ännu inte i formulärblocket</i></td>
   <td> Användare kan inkludera bilder i ett formulär.</td>
  </tr><tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/title.html">Titel</a></td>
   <td><i>Stöds ännu inte i formulärblocket</i></td>
   <td> Avser texten som visas högst upp i formuläret. </td>
  </tr>
  <tr>
   <td><a href = "https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/submit-button.html">Byt</td>
   <td><i>Stöds ännu inte i formulärblocket</i></td>
   <td> En tvålägesväxling som gör att användaren kan välja mellan två lägen, till exempel aktivera eller inaktivera en funktion, inställning eller funktion.</td>
  </tr>
 </tbody>
</table>



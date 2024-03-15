---
title: Komponenter för adaptiva formulärblock och deras egenskaper
description: Det här dokumentet innehåller en översikt över de formulärkomponenter och deras egenskaper som är tillgängliga i AEM Forms Edge Delivery Service.
feature: Edge Delivery Services
exl-id: 7d087d41-9313-482a-a905-8955b0999781
source-git-commit: 703a48903c44678f6fe311de740b7c767c886ba5
workflow-type: tm+mt
source-wordcount: '1006'
ht-degree: 0%

---

# Komponenter för adaptiva formulärblock och deras egenskaper

Med AEM Forms Edge Delivery Services kan du skapa användarvänliga och interaktiva formulär med hjälp av olika komponenter. Dessa komponenter klarar olika typer av datainsamling och kan enkelt anpassas efter dina specifika behov.


![Ett exempelkalkylblad med vissa komponenter och egenskaper](/help/edge/assets/sample-form-in-spreadsheet.png)

The Adaptive Forms Block genererar en [struktur för enhetlig HTML](/help/edge/docs/forms/style-theme-forms.md) för alla fälttyper och behållare (paneler) för att säkerställa konsekvens. Denna enhetliga struktur gör det enklare att [formatera ett formulär](/help/edge/docs/forms/style-theme-forms.md).

## Tillgängliga komponenter

Här är en översikt över de tillgängliga komponenterna:

### Indatafält

* Alla giltiga HTML5 [indatatyper](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#input_types) och [textområde](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea). Till exempel knapp, kryssruta, färg, datum, datum/tid-lokal, e-post, fil, dold, bild, månad, nummer, lösenord, radio, intervall, återställning, skicka, tel, text, tid, url och vecka.

### Markeringskontroller

* [Kryssrutegrupper](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/checkbox): För att välja flera alternativ.
* [Radiogrupper](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/radio): För att välja ett alternativ från en grupp.
* [Listrutor](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select): Om du vill visa en meny med alternativ. Till exempel listruta.

### Behållare

* Paneler/behållare: Om du vill gruppera relaterade formulärelement tillsammans blir det enklare att organisera. Det är en kombination av [fältuppsättning](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset) och [teckenförklaring](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/legend).


## Komponentegenskaper

Varje formulärkomponent har olika egenskaper som gör att du kan styra dess beteende och utseende. Här är de egenskaper som stöds av adaptiva Forms Block-komponenter:


| Egenskap | Tillämpliga komponenter | Information |
|--------------|------------------------------|----------------------------------------------------------------------|
| Typ | Alla | Anger komponentens typ. Den här egenskapen avgör inmatningsfältets beteende och utseende. För textinmatningar kan till exempel typen vara &quot;text&quot;, &quot;email&quot; för e-postinmatningar och &quot;password&quot; för lösenordsinmatningar. Adaptive Forms Block har stöd  <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#input_types">alla giltiga indatatyper för HTML5</a>, <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea">textområde</a>, <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select">välj</a>och <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset">fältuppsättning</a> som typ. |
| Namn | Alla | Identifierar komponenten för att skicka formulär. Attributet name används när formulärdata skickas till servern och associerar användarindata med ett specifikt fält. |
| Etikett | Alla | Ger kontextuell information till användare. Etiketten är den text som visas bredvid komponenten och ger användarna vägledning om vilken information som ska anges. |
| Värde | Text, Lösenord, E-post, Nummer, Intervall, Datum och dess varianter (datetime-local, month, week, time), Kryssruta, Radio, Hidden, Submit, Button | Anger komponentens startvärde. För textinmatningar, textområden och markerade element visas detta som standardtext eller standardalternativ. För alternativknappar och kryssrutekomponenter är detta det värde/de data som skickas när de markeras. Attributet value är valfritt men ska betraktas som obligatoriskt för kryssrutor och alternativinmatningar. |
| Platshållare | Text, Tel, Email, Password, Date (och dess varianter som month, week, time, datetime-local), Number, Range | Visar tips för förväntade indata. Platshållarattributet ger ett kort tips som beskriver det förväntade värdet för indatafältet. Det försvinner när användaren börjar skriva. |
| Beskrivning | Alla | Ger ytterligare information om komponenten och fungerar som hjälptext. Beskrivningsfältet innehåller mer information om syftet eller instruktionerna för att fylla i komponenten. Det underlättar för användarna att förstå inmatningsfältets kontext. |
| Synlig | Alla | Styr inledande synlighet. Attributet visible är en boolesk egenskap som avgör om komponenten från början är synlig eller dold när formuläret läses in. Om värdet är true visas fältet, annars döljs det. |
| Obligatoriskt | Text, Tel, E-post, Lösenord, Datum och dess varianter (datetime-local, month, week, time), Number, Checkbox, Radio, File, Select (dropdown), TextArea | Anger om fältet måste fyllas i innan det skickas. Det obligatoriska attributet är en boolesk egenskap som används för att ange om användaren måste ange indata för fältet innan formuläret skickas. |
| Min | Datum (och dess varianter som månad, vecka, tid, datetime-local), Number, intervall | Anger det minsta tillåtna värdet. Min-attributet anger det lägsta värde som användaren kan ange i fältet. För talinmatningar definieras t.ex. det lägsta godtagbara talet. |
| Max | Datum (och dess varianter som månad, vecka, tid, datetime-local), Number, intervall | Anger högsta tillåtna värde. Attributet max anger det maximala värde som användaren kan ange i fältet. För datumindata definieras till exempel det högsta godtagbara datumet. |
| Acceptera | Fil | Definierar tillåtna filtyper. Attributet accept är en kommaavgränsad lista med unika filtypsspecifikationer som begränsar de filtyper som användare kan välja i ett filindatafält. |
| Flera | Fil | Tillåter flera markeringar. Attributet multiple är en boolesk egenskap som används med filinmatningsfält. Om värdet är true kan användarna välja mer än en fil. |
| Alternativ | Listruta | Anger alternativ för rullgardinsmenyer. Egenskapen options är en kommaavgränsad lista med alternativ för listrutor, som definierar de alternativ som kan markeras och visas för användaren. |
| Markerad | Kryssruta, radio | Anger om fältet är markerat som standard. Attributet checked är en boolesk egenskap som används med kryssrutor och alternativinmatningar. Om värdet är true innebär det att fältet är markerat som standard när formuläret läses in. |
| Fieldset | Alla | Grupperar fält för att skapa visuellt distinkta avsnitt i ett formulär. Fältelementet grupperar relaterade fält i ett formulär och skiljer dem visuellt för att förbättra organisationen och användarupplevelsen. </br> Om du vill ordna en uppsättning fält i en fältuppsättning använder du `fieldset` och ange namnattributet. I exemplet nedan visar vi hur alternativknappar är inkapslade i en enda fältuppsättning för bättre sortering. ![Exempel på fältuppsättning](/help/edge/assets/fieldset-example.png) |
| Upprepningsbar | Alla | En boolesk egenskap för `fieldset` som anger att en viss fältuppsättning kan upprepas för angivna `Min` och `Max` antal gånger. The `Min` egenskapen ska vara 1 eller större, ange inte `Min` till 0. |
| Synligt uttryck | Alla | Ett synligt uttryck refererar till en kalkylbladsformel, som betecknas med taggen &#39;=&#39;, som används för att styra synligheten för ett fält. I den här formeln kan bara egenskapen value i andra fält användas, vilket gör att synlighet i fält kan hanteras enkelt i systemet. |
| Värdeuttryck | Alla | Ett värdeuttryck refererar till en kalkylbladsformel, som betecknas med taggen &#39;=&#39;, som används för att kontrollera värdet i ett fält. I den här formeln kan bara värdeegenskapen i andra fält användas, vilket gör det enkelt att hantera fältvärdet i systemet. |


## Se även

{{see-more-forms-eds}}

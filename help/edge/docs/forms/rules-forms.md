---
title: Använd regler för att lägga till dynamiskt beteende i ett formulär
description: AEM Forms Edge Delivery Services som tagits fram för bästa prestanda och som gör det möjligt att förutse framtiden för smidig datainsamling och användarengagemang. Använd regler för att lägga till dynamiskt beteende i formulären.
feature: Edge Delivery Services
exl-id: 58042016-e655-446f-a2bf-83f1811525e3
source-git-commit: 2affe155b285986128487043fcc4f2938fc15842
workflow-type: tm+mt
source-wordcount: '2216'
ht-degree: 0%

---

# Använd regler för att lägga till dynamiskt beteende i formulär

En av de kraftfulla funktionerna för att skapa formulär med hjälp av ett kalkylblad är möjligheten att använda inbyggda kalkylbladsfunktioner för att skapa regler, vilket gör det möjligt att villkorligt visa eller dölja formulärfält, automatisera beräkningar baserat på användarens indata och skapa en mer dynamisk användarupplevelse.

I den här artikeln beskrivs hur du använder olika egenskaper för adaptiva formulärblock i huvudsak [`Visible`](#visible-property), [`Visibility Expression`](#visible-expression-property) och [`Value Expression`](#value-expression-property) egenskaper tillsammans med [kalkylbladsfunktioner](#spreadsheet-functions-for-rules) för att skapa effektiva regler för formulären. Vi ska också titta på några exempel som visar hur dessa regler kan implementeras i praktiken.

## Om en linjes konstruktion

Regler är som instruktioner som talar om för oss vad vi ska göra i olika situationer. En regel har vanligtvis följande konstruktion:

* Villkor: Dessa anger under vilka omständigheter regeln gäller. Se dem som en fråga som behöver besvaras (ja eller nej).

* Åtgärder: Dessa definierar vad som händer när villkoret är uppfyllt (true) eller inte är uppfyllt (false).


Om du till exempel vill visa en e-postruta när en kryssruta är markerad:

* Villkor: &quot;Tycker du om att prenumerera på tidskrifter och aktiviteter?&quot; är markerad. (Ja eller nej?). Detta villkor ställs in i `Visible` formulärets egenskap.
* Åtgärd (True): E-postrutan visas. (Vad händer om ja). The `Visibility Expression`  använd villkoret som definierats för `visible` för att dynamiskt visa fält.
* Åtgärd (Falskt): E-postrutan är dold. (Vad händer om nej). The `Visibility Expression`  använd villkoret som definierats för `Value` för att dölja fält dynamiskt.

Detaljerade stegvisa instruktioner finns i [visa/dölj e-postfält baserat på ett villkor](#example-1-conditional-email-field)


## Förstå egenskaperna för värde, synlighet, synlighetsuttryck och värdeuttryck

### Synlig egenskap

Tänk dig en ljusbrytare för formulärfältet. The `Visible` -egenskapen är som den växeln och styr om fältet är synligt från början i formuläret när det läses in.

* Sant (som ljusväxeln är på): Fältet visas i formuläret.
* Falskt (som om ljusbrytaren är av): Fältet är dolt i formuläret.

Du kan använda SpreadSheet-formeln (inklusive taggen =) för att skriva en formel med hjälp av kalkylbladsliknande logik för att bestämma fältets synlighet. Du kan använda värden från andra fält i formuläret i den här formeln. Om en användare t.ex. väljer &quot;Individuell&quot; i ett registreringstypfält kan du dölja e-postfältet med en formel som kontrollerar det värdet.

### Synlig uttrycksegenskap (Visa/dölj ett fält)

The `Visible Expression` kan du använda regeln som lagts till i `Visible` för att bestämma om fältet ska visas eller döljas baserat på användarinteraktioner.

Använd `=FORMULATEXT("Address of the corresponding Visible property)` för att använda formeln som anges i `Visible` Egenskap som en sträng till `Visible Expression` egenskapsfält. Detta krävs för att dynamiskt visa/dölja fält i ett publicerat formulär.

![Forumaltext](/help/edge/assets/aem-forms-formulatext.png)

### Värdeegenskap (ange initiala data)

Föreställ dig ett förinställt värde på en nedtoningsbrytare för ett rumsljus. The `Value` -egenskapen liknar den som avgör det inledande tillståndet för de data som en användare ser i fältet.  Den anger eller hämtar aktuella data som visas i formulärfältet.

När formuläret läses in för första gången `Value` anger vad användaren ser i fältet innan han/hon gör några ändringar. Ogilla `Visible` och `Visible Expression` -egenskaper som styr synlighet, påverkar egenskapen Value direkt själva data. Användarna kan ändra det här värdet genom att skriva, välja alternativ (nedrullningsbara menyer) eller interagera med fältet.

Du kan använda Excel-formel (inklusive taggen =) för att skriva en formel med hjälp av kalkylbladsliknande logik för att bestämma vilket värde som visas i fältet. Du kan använda värden från andra fält i formuläret i den här formeln. Du kan till exempel beräkna en rabatt automatiskt baserat på orderbeloppet som anges i ett annat fält.


### Värdeuttrycksegenskap (Beräkna värden som ska visas i ett fält)

Med den här egenskapen kan du styra det värde som visas i ett fält baserat på en formel, som liknar synligt uttryck. Tänk dig en kalkylator inbyggd i fältet.

Använd `=FORMULATEXT("Address of the corresponding Value property)` för att använda formeln som anges i `Value` Egenskap som en sträng till `Value Expression` egenskapsfält. Detta krävs för att dynamiskt beräkna och visa beräknade värden i ett publicerat formulär.

![Forumaltext](/help/edge/assets/aem-forms-formulatext-value.png)

Här är en analogi för att stärka dessa koncept:

* Synlig: Föreställ dig ett formulär som ett hus. Egenskapen&quot;Synlig&quot; fungerar som ljusbrytaren för varje rum (fält). Du bestämmer om rummet är belyst (synligt) eller mörkt (dolt) när någon kommer in i huset (öppnar formuläret).
* Synligt uttryck: Detta är som en omkopplare för rörelsesensorljus. Rummet (fältet) kan till en början vara mörkt (dolt), men en formel (rörelsesensor) kan aktivera det (visa fältet) om någon går förbi (ändrar värdet i ett annat fält).
* Värde: Detta är som en förinställd nedtoningsbrytare för ljuset (ursprungliga data i fältet). Användarna kan sedan justera intensiteten (ändra värdet).
* Värdeuttryck: Det här är som en avancerad räknare inbyggd i priskoden för en produkt i huset (form). Pristaggen (fältet) visar det slutliga priset baserat på en formel (till exempel tillägg av moms till baspriset) som använder annan information som baspriset (värde från ett annat fält).

Genom att kombinera dessa egenskaper med [kalkylbladsfunktioner](#spreadsheet-functions-for-rules)kan du få ett brett urval av dynamiska beteenden i dina formulär.

## Kalkylbladsfunktioner för regler

Adaptiv Forms Block har stöd för en mängd kalkylbladsfunktioner som kan användas för att skapa regler. Här är funktioner som är tillgängliga direkt (OTB):

### Logiska funktioner

* [NOT()](https://docs.oasis-open.org/office/v1.2/os/OpenDocument-v1.2-os-part2.html#__RefHeading__1018452_715980110): Inverterar det logiska läget (TRUE blir FALSE och vice versa).
* [AND()](https://docs.oasis-open.org/office/v1.2/os/OpenDocument-v1.2-os-part2.html#AND): Returnerar endast TRUE om alla angivna villkor är TRUE.
* [OR()](https://docs.oasis-open.org/office/v1.2/os/OpenDocument-v1.2-os-part2.html#OR): Returnerar TRUE om minst ett av de angivna villkoren är TRUE.

### Villkorliga funktioner

* [IF()](https://docs.oasis-open.org/office/v1.2/os/OpenDocument-v1.2-os-part2.html#__RefHeading__1018446_715980110): Utvärderar ett villkor och returnerar ett specifikt värde om värdet är TRUE och ett annat värde om värdet är FALSE.

### Matematiska funktioner

* [SUM()](https://docs.oasis-open.org/office/v1.2/os/OpenDocument-v1.2-os-part2.html#SUM): Lägger till värden från ett angivet cellintervall.
* [ROUND()](https://docs.oasis-open.org/office/v1.2/os/OpenDocument-v1.2-os-part2.html#ROUND): Avrundar ett tal till ett angivet antal decimaler.
* [MIN()](https://docs.oasis-open.org/office/v1.2/os/OpenDocument-v1.2-os-part2.html#MIN): Returnerar det minsta värdet från ett angivet cellintervall.

## Skapa en regel

Låt oss titta närmare på några praktiska exempel som visar hur regler kan användas för att förbättra formulären:

## Exempel 1: Villkorligt e-postfält

I det här exemplet visas hur kryssrutan fungerar som ett villkor. När det är markerat (villkoret är true) visas e-postrutan (åtgärden är true). Om alternativet inte är markerat (villkoret är false) döljs e-postrutan (åtgärden är false).

Skapa ett formulär med en kryssruta och en e-postruta, som visas i bilden nedan:

![Villkorligt e-postformulär](/help/edge/assets/aem-forms-conditional-email-form.png)


Så här använder du en regel för att visa e-postfältet när du markerar en kryssruta:

1. Ange `Value` egenskapen för kryssrutefältet till `TRUE`.
1. Ange `Checked` egenskapen för kryssrutefältet till `FALSE`. Detta garanterar att kryssrutan inte är markerad som standard.
1. Ange `Visible` egenskapen för e-postfältet till `=[address of Checked property of the checkbox field] = true()`. Till exempel `=Q11=TRUE()`. Formeln utvärderas om kryssrutan är markerad eller inte. Om kryssrutan är markerad utvärderas formeln till TRUE. Om kryssrutan inte är markerad utvärderas formeln till FALSE.



   The `TRUE()` returnerar det logiska värdet när du ställer in det på point `Checked` egenskapen, om `checked = false` det returnerar false. If `checked=true`, returneras `true`. Detta garanterar att e-postfältet döljs som standard.


1. Ange `Visible Expression` egenskapen för kryssrutefältet till `=FORMULATEXT ((address of Visible property of the checkbox field))`. Till exempel: `=FORMULATEXT((G12))`. Funktionen FORMULATEXT() tar en formel som indata och returnerar själva formeln som en textsträng. Det hjälper till att använda formeln i formuläret.

   ![Villkorligt e-postfält](/help/edge/assets/aem-forms-visible-expression-formula-text.png)

1. Förhandsgranska och publicera formuläret. När du markerar kryssrutan visas e-postfältet, medan fältet döljs och en dynamisk användarupplevelse skapas.

   ![Villkorlig e-post](/help/edge/assets/aem-forms-coditional-email.gif)


## Exempel 2: Automatisk beräkning

I det här exemplet visas hur ett formulär automatiskt beräknar uppskattad resekostnad när du väljer resedatum i ett formulär.

Skapa ett formulär med ett datumfält, en rumsbudget, en uppskattad resekostnad som visas nedan och en e-postruta som visas i bilden nedan:

![Villkorligt e-postformulär](/help/edge/assets/aem-forms-automatic-calculations-form.png)

Så här använder du en automatisk beräkning för att visa beräknad resekostnad:

1. Ange `Value` egenskapen för `amount` fält till `=F6*DAYS(F3,F2)`. Den här formeln beräknar antal dagar från `Start Date`  och `End Date`, multiplar antal dagar med rumsbudget och visar resultatet `Estimated Trip Cost` fält.

1. Ange `Value Expression` egenskapen för `Estimated Trip Cost` fält till `=FORMULATEXT ((address of value property of the amount field))`. Till exempel: `=FORMULATEXT(F7)`. Funktionen FORMULATEXT() tar en formel som indata och returnerar själva formeln som en textsträng. Det hjälper till att använda formeln i formuläret.

1. Förhandsgranska och publicera formuläret. Nu när du anger en `Start Date`, `End Date`och rumsbudget. The `Estimated Trip Cost` beräknas automatiskt.

## Exempel på funktioner i kalkylblad


Här är några exempel på vanliga tabellfunktioner:

**Logiska funktioner:**

* **NOT():** Inverterar det logiska läget (TRUE blir FALSE och vice versa).

  Exempel: Dölja fältet Bekräfta e-post om e-postfältet lämnas tomt.

   1. Ange `Visible` egenskapen för fältet Bekräfta e-post till `=NOT(if('address of email field'=""))`.

      ![AEM Forms - dölj bekräftelsefält](/help/edge/assets/aem-forms-not-function-hide-email-field.png)


   1. Ange det synliga uttrycket i fältet Bekräfta e-post till `=FORMULATEXT ((address of visible property of the Confirm Email field))`

      ![AEM Forms visible-uttrycksformel](/help/edge/assets/aem-forms-visible-expression-formula-text.png)


* AND(): Returnerar endast TRUE om alla angivna villkor är TRUE.

   * Exempel: Aktivera bara knappen &quot;skicka&quot; om alla obligatoriska fält är ifyllda.

   1. Ange `Visible` egenskapen för skicka-knappen till:



      ```JavaScript
      =AND(NOT(address of `value` property of the `name` field = ""), NOT(address of `value` property of the `email` field = ""), NOT(address of `value` property of the `phone` field))
      ```

      Exempel:

      ```JavaScript
      =AND(NOT(F9=""), NOT(F12=""), NOT(F10=""))
      ```

   1. Ange det synliga uttrycket i fältet Bekräfta e-post till

      ```JavaScript
      =FORMULATEXT ((address of visible property of the Confirm Email field))
      ```

      Exempel:

      ```JavaScript
      =FORMULATEXT(G14)
      ```

      I den här formeln visas bara knappen &quot;skicka&quot; (TRUE) om alla fält (namn, e-post, telefon) är ifyllda (NOT()) returnerar TRUE för varje fält), annars döljs knappen (AND(flera FALSES) = FALSE).

* OR(): Returnerar TRUE om minst ett av de angivna villkoren är TRUE.

   * Exempel: Använder en rabatt om en användare anger någon av de tillämpliga rabattkupongkoderna.

   1. Ange `Visible` egenskapen för fältet&quot;final amount&quot; till:


  ```JavaScript
     =IF(OR(F14="BlackFridaySale", F14="NewYearDiscount"), (F6*DAYS(F3,F2)* 0.7) , (F6*DAYS(F3,F2)))
  ```

   1. Ange att värdeuttrycket för fältet Bekräfta e-post ska vara

      ```JavaScript
      =FORMULATEXT ((address of value property of the final amount field))
      ```

      Exempel:

      ```JavaScript
      =FORMULATEXT(F7)
      ```

      Den här formeln beräknar en rabatt på 30 % om användaren anger en kupongkod (kupongkod = &quot;NewYearDiscount&quot;) ELLER (kupongkod = &quot;BlackFridaySale&quot;), annars anges rabatten till 0.

**Textfunktioner:**

* IF(): Utvärderar ett villkor och returnerar ett specifikt värde om värdet är TRUE och ett annat värde om värdet är FALSE.

   * Exempel: Visa ett anpassat meddelande baserat på en vald produktkategori.

   1. Ange `Value` egenskapen för `message` fält till `Only upto 7 kg check-in lagguage is allowed!`:

   1. Ange `Visible` egenskapen för `message` fält till:


      ```JavaScript
      =if(address of value property of chosen product category ="Economy", TRUE(), FALSE())
      ```

      Exempel:

      ```JavaScript
      =if(F5="Economy", TRUE(), FALSE())
      ```

   1. Ange värdeuttrycket för `message` fält till

      ```JavaScript
      =FORMULATEXT ((address of value property of the final amount field))
      ```

      Exempel:

      ```JavaScript
      =FORMULATEXT(G15)
      ```

      Den här formeln visar meddelandet&quot;Endast upp till 7 kg incheckningsbagage tillåts!&quot; om den valda klassen är&quot;Ekonomi&quot;, annars lämnas meddelandefältet tomt.

**Matematiska funktioner:**

* SUM(): Lägger till värden från ett angivet cellintervall.

  Exempel: Beräkna den totala kostnaden för artiklar i en kundvagn.

  I värdeuttrycket för fältet &quot;total kostnad&quot;: SUM(price * quantity)

  Formeln förutsätter att du har separata fält för&quot;pris&quot; och&quot;kvantitet&quot; för varje artikel. De multipliceras och SUM() används för att addera den totala kostnaden för alla artiklar i kundvagnen.

* ROUND(): Avrundar ett tal till ett angivet antal decimaler.

  Exempel: Avrundar ett beräknat rabattbelopp till två decimaler.

  I värdeuttrycket för fältet &quot;rabattbelopp&quot; (förutsatt att en rabatt beräknas någon annanstans): ROUND(rabatt, 2)

  Den här formeln avrundar rabattvärdet till två decimaler.

* MIN(): Returnerar det minsta värdet från ett angivet cellintervall.

  Exempel: Söker efter den lägsta ålder som krävs för ett registreringsformulär baserat på ett valt land.

  I värdeuttrycket för ett fält av typen &quot;minimal ålder&quot;: MIN(ageLimits[&quot;US&quot;], ageLimits[&quot;UK&quot;], ageLimits[&quot;Frankrike&quot;])

  Formeln förutsätter att du har en tabell med namnet&quot;ageLimits&quot; som lagrar krav på minimiålder för olika länder. MIN() används för att hitta det minsta värdet bland dem.


Med Adaptive Forms Block kan du dessutom ta kontroll över dina formulär genom att skapa [anpassade funktioner](#creating-custom-functions). Med anpassade funktioner kan du definiera egna regler och logik, vilket ger dig fullständig kontroll över hur formulären fungerar.


## Skapa och distribuera anpassade funktioner

Det anpassningsbara Forms-blocket OTB (Out-of-the-box) kan implementeras för många [vanliga funktioner för kalkylblad](#spreadsheet-functions-for-rules). Om du vill ha större kontroll över formulären kan du använda valfri OTB-funktion i Microsoft® Excel eller Google Sheets i dina adaptiva Forms-block. Det adaptiva Forms-blocket innehåller inte implementering för alla OTB-funktioner som finns i Microsoft® Excel eller Google Sheets. Om du behöver någon av dessa funktioner kan du utveckla en anpassad funktion med liknande syntax för att få den funktionalitet som finns i Microsoft® Excel eller Google Sheets. Du kan till exempel implementera [Funktionen Year() i Microsoft® Excel](https://support.microsoft.com/en-us/office/calculate-age-113d599f-5fea-448f-a4c3-268927911b37#) för att beräkna ålder från och med födelsedatumet.


### Skapa en anpassad funktion

Anpassade funktioner finns i `[Adaptive form block]/functions.js` -fil. Att skapa innefattar i allmänhet följande steg:

* Funktionsdeklaration: Definiera funktionsnamnet och dess parametrar (de indata som accepteras).
* Logikimplementering: Skriv koden som anger de specifika beräkningar eller ändringar som utförs av funktionen.
* Funktionsexport: Gör funktionen tillgänglig i reglerna genom att exportera den från den relevanta filen.

### Exempel: Årsfunktion

I det här exemplet visas två anpassade funktioner som efterliknar funktionen YEAR() i Microsoft® Excel för att beräkna åldern:


```JavaScript
/**
 * Get the current date and time
 * @name now
 * @returns {Date} The current date and time as a Date object
 */
function now() {
  const today = new Date();
  return today;
}

/**
 * Get the year from a Date object
 * @name year
 * @param {Date} date The date object
 * @throws {TypeError} If the input is not a Date object
 * @returns {number} The year as a number
 */
function year(date) {
  let inputDate = new Date(date)

  if (!(inputDate instanceof Date)) {
    throw new TypeError("Input must be a Date object");
  }

  const year = inputDate.getFullYear();

  return year;
}

// Make the function accessible for use in rules
export { now, year };
```

### Använd en anpassad funktion i formuläret

Så här använder du den anpassade funktionen i ditt formulär:

1. **Lägg till funktionen**: Inkludera din anpassade funktion i `[Adaptive form block]/functions.js` -fil. Kom ihåg att lägga till den i exportsatsen i filen.
1. **Distribuera filen**: Distribuera den uppdaterade `functions.js` till ditt GitHub-projekt och verifiera att bygget har slutförts.
1. **Funktionsanvändning**: Använd funktionen i formulärets kalkylblad med `Value`, `Value Expression`, `Visible`, eller `Visible Expression` egenskaper, som liknar andra kalkylbladsfunktioner som stöds av OTB.
1. **Förhandsgranska formuläret**: Använd AEM Sidekick för att förhandsgranska formuläret med den nyligen implementerade funktionen.


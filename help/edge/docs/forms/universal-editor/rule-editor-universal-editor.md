---
title: Hur använder man regelredigeraren för att tillämpa regler på formulärfält, vilket möjliggör dynamiskt beteende och komplex logik för formulär som skapats med WYSIWYG?
description: Med regelredigeraren i Universal Editor kan du lägga till dynamiskt beteende och bygga in komplex logik i formulär utan kodning eller skript.
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 846f56e1-3a98-4a69-b4f7-40ec99ceb348
source-git-commit: 0c6f024594e1b1fd98174914d2c0714dffecb241
workflow-type: tm+mt
source-wordcount: '2089'
ht-degree: 0%

---


# Introduktion till regelredigeraren i WYSIWYG Authoring

<span class="preview"> Den här funktionen är tillgänglig via programmet för tidig åtkomst. Om du vill begära åtkomst skickar du ett e-postmeddelande från din officiella adress till <a href="mailto:aem-forms-ea@adobe.com">aem-forms-ea@adobe.com</a> med ditt GitHub-organisationsnamn och databasnamn. Om databas-URL:en till exempel är https://github.com/adobe/abc är organisationsnamnet adobe och databasnamnet abc.</span>


Du kan lägga till dynamiskt formulärbeteende med regelredigeraren, som du kan använda för att skapa regler. Dessa regler möjliggör synlighet för villkorliga fält, automatiserar beräkningar baserat på användarindata och förbättrar den övergripande användarupplevelsen. Regelredigeraren effektiviserar ifyllningsprocessen och ser till att både noggrannheten och effektiviteten är hög.

Regelredigeraren har ett intuitivt visuellt gränssnitt för att skapa och hantera regler. Det användarvänliga sättet gör det tillgängligt för alla användare, även de som saknar omfattande teknisk expertis, så att de enkelt kan implementera logik i sina formulär.

## Förstå en regel

Regler är instruktioner som vägleder användarna när det gäller vilka åtgärder som ska utföras under specifika förhållanden.

* **Villkor**: Ett villkor är en kontroll eller regel som utvärderar om något är sant eller falskt. Svarar på frågan:&quot;Uppfyller detta kraven?&quot;

* **Åtgärd**: En åtgärd är vad som händer när villkoret är sant. Det är den uppgift eller det beteende som utlöses baserat på utvärderingen av villkoret.

En regel följer vanligtvis någon av följande konstruktioner:

* **Condition-Action**: Kontrollera först ett villkor och utför sedan en åtgärd. Regeltypen `When` tvingar `condition-action`-konstruktionen i regelredigeraren.
* **Åtgärdsvillkor**: Utför en åtgärd först och kontrollera sedan ett villkor. Regeltyperna `Set Value Of` och `Validate` i regelredigeraren framtvingar `action-condition`-konstruktionen.
* **Åtgärd-Villkor-Alternativ åtgärd**: Utför en åtgärd, kontrollera ett villkor och utför sedan antingen huvudåtgärden eller en alternativ åtgärd baserat på villkoret. Som standard är den alternativa åtgärden för `Show` `Hide` och för `Enable` är den `Disable`.

Ett villkor kan till exempel kontrollera om en användare har angett ett visst värde i ett fält och åtgärden kan vara att visa eller dölja ett fält.
* **Villkor**: Kontrollera om inkomsten är större än 50 000 USD.
* **Åtgärd**: Om villkoret är sant visar du fältet `Additional Deduction`, annars utför du den alternativa åtgärden: dölj fältet `Additional Deduction`.

Detaljerade stegvisa instruktioner finns i [Lägg till en villkorsregel](#2-add-a-conditional-rule).

## Hur aktiverar jag tillägget Regelredigerare?

Tillägget Regelredigerare är inte aktiverat som standard i Universellt redigeringsprogram. Om du vill aktivera tillägget Regelredigerare skriver du till oss på [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) från ditt officiella e-post-id.

När regelredigeringstillägget har aktiverats för din miljö visas ikonen ![edit-rules](/help/forms/assets/edit-rules-icon.svg) i det övre högra hörnet av redigeraren.

![Regelredigeraren Universal Editor](/help/edge/docs/forms/assets/universal-editor-rule-editor.png)

Markera den formulärkomponent som du vill skriva en regel för och klicka på ikonen ![edit-rules](/help/forms/assets/edit-rules-icon.svg) . Användargränssnittet för Regelredigeraren visas.

![Användargränssnittet i regelredigeraren](/help/edge/docs/forms/assets/rule-editor-for-field.png)

I den här artikeln används `form object` och `form component` omväxlande.

Nu kan du börja skriva regler eller affärslogik för det markerade formulärfältet med [tillgängliga regeltyper i regelredigeraren](#available-rule-types-in-rule-editor).

## Förstå användargränssnittet i regelredigeraren

Regelredigeraren öppnas när du klickar på ikonen ![edit-rules](/help/forms/assets/edit-rules-icon.svg) :

![Användargränssnitt för regelredigeraren](/help/edge/docs/forms/assets/rule-editor-interface.png)

<table border="1">
  <thead>
    <tr>
      <th>Regelredigerarens komponent</th>
      <th>Beskrivning</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>1. Titel</td>
      <td>Visar formulärkomponentens rubrik och den valda regeltypen. Till exempel är 'Ange bruttolön' en textrutekomponent som regeltypen 'När' är markerad för. </td>
    </tr>
    <tr>
      <td>2. Formulärobjekt och funktioner</td>
      <td>På fliken <b>Forms-objekt</b> visas en hierarkisk vy över alla komponenter som finns i formuläret. Fliken <b>Funktioner</b> innehåller en uppsättning inbyggda funktioner i regelredigeraren.</td>
    </tr>
    <tr>
      <td>3. Växla mellan formulärobjekt och funktioner</td>
      <td>Växlingsknappen visar eller döljer alternativt formulärobjekten och funktionsrutan. </td>
    </tr>
    <tr>
      <td>4. Visuell regelredigerare</td>
      <td>Den visuella regelredigeraren är gränssnittet där du kan skapa regler för formulärkomponenterna.</td>
    </tr>
    <tr>
      <td>5. Knapparna Klar och Avbryt</td>
      <td>Knappen <b>Klar</b> används för att spara en regel. Knappen <b>Avbryt</b> ignorerar alla ändringar som du har gjort i en regel och stänger regelredigeraren.</td>
    </tr>
  </tbody>
</table>

Alla befintliga regler för en formulärkomponent visas när du markerar komponenten. Du kan visa titeln och en förhandsgranskning av regelsammanfattningen i regelredigeraren. Dessutom kan du ändra ordningen på regler, redigera regler, aktivera/inaktivera regler eller ta bort regler.

![visa tillgängliga regler för formulärobjekt](/help/edge/docs/forms/assets/rule-editor15.png)

## Tillgängliga regeltyper

Regelredigeraren innehåller en uppsättning fördefinierade regeltyper som du kan använda för att skriva regler, vilket visas i tabellen nedan:

<table border="1">
  <thead>
    <tr>
      <th>Regeltyp</th>
      <th>Beskrivning</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Ange värdet för</td>
      <td>Anger värdet för en formulärkomponent beroende på om det angivna villkoret är uppfyllt eller inte.</td>
    </tr>
    <tr>
      <td>Radera värdet för</td>
      <td>Rensar värdet för den angivna formulärkomponenten.</td>
    </tr>
    <tr>
      <td>Dölj/visa</td>
      <td>Döljer eller visar en formulärkomponent baserat på om ett villkor är uppfyllt eller inte.</td>
    </tr>
    <tr>
      <td>Aktivera/inaktivera</td>
      <td>Aktiverar eller inaktiverar en formulärkomponent baserat på om ett villkor är uppfyllt eller inte.</td>
    </tr>
    <tr>
      <td>Validera</td>
      <td>Kontrollerar formulärkomponenten baserat på ett villkor och visar ett fel om villkoret inte uppfylls. </td>
    </tr>
    <tr>
      <td>När</td>
      <td>Det anger ett villkor för utvärdering följt av en åtgärd som ska utlösas om villkoret är uppfyllt. Det följer på <i>condition-action-alternate</i>-åtgärdsregelkonstruktionen eller <i>condition-action</i>-regelkonstruktionen. </td>
    </tr>
    <tr>
      <td>Format</td>
      <td> Ändrar formulärkomponentens visningsvärde med det angivna uttrycket när dess värde ändras.</td>
    </tr>
    <tr>
      <td>Anropa tjänst</td>
      <td>Anropar en tjänst som konfigurerats med externa API:er, formulärdatamodell eller RESTful-webbtjänster.</td>
    </tr>
    <tr>
      <td>Ange egenskap</td>
      <td>Anger värdet för en egenskap för den angivna formulärkomponenten baserat på ett villkor.</td>
    </tr>
    <tr>
      <td>Ange fokus</td>
      <td>Ställer in fokus på den angivna formulärkomponenten.</td>
    </tr>
    <tr>
      <td>Spara formulär</td>
      <td>Det gör att användaren kan spara formuläret som ett utkast med hjälp av Forms Portal-komponenten Utkast och överföringar. </td>
    </tr>
    <tr>
      <td>Skicka formulär</td>
      <td>Skickar formuläret.</td>
    </tr>
    <tr>
      <td>Återställ formulär</td>
      <td>Återställer formuläret.</td>
    </tr>
    <tr>
      <td>Lägg till/ta bort instans</td>
      <td>Lägger till eller tar bort en instans av den angivna repeterbara panelen eller tabellraden.</td>
    </tr>
    <tr>
      <td>Navigera till</td>
      <td>Navigerar till andra adaptiva Forms, andra resurser som bilder eller dokumentfragment eller en extern URL.</td>
    </tr>
    <tr>
      <td>Utsändningshändelse</td>
      <td>Utlöser specifika åtgärder baserat på fördefinierade villkor eller händelser.</td>
    </tr>
    <tr>
      <td>Navigera bland panelerna</td>
      <td>Gör att du kan flytta fokus mellan olika paneler i ett formulär.</td>
    </tr>
  </tbody>
</table>


Nu ska vi utforska hur du [skriver regler i regelredigeraren](#write-rules).

## Skriv regler

För att förstå hur du skriver regler i Visual Rule Editor ska vi titta på ett enkelt exempel på ett skatteberäkningsformulär:

![Exempel på regelredigerare](/help/edge/docs/forms/assets/rule-editor-1.png)

I den form som beskrivs ovan anger användaren bruttolönen. Baserat på denna inmatning visas villkorsfält och betald moms beräknas.

**Formulärfält:**
* Bruttolön (användarindata)
* Ytterligare avdrag (villkorsfält)
* Skattepliktig inkomst (beräknat fält)
* Skatteskuld (beräknat fält)

**Villkorsregel:**
* Villkor: bruttolön > 50 000
* Åtgärd: Visa fältet Ytterligare avdrag

**Beräkningsregler:**

* Skattepliktig inkomst = bruttolön - avdrag (om tillämpligt)
* Skatteskuld = skattepliktig inkomst * Skatteränta (för enkelhetens skull anta en fast skattesats på 10 %)

Så här skriver du regler:

### 1. Skapa ett formulär

Så här skapar du ett formulär i Universal Editor:

1. Öppna ett formulär i Universal Editor för redigering.
1. Lägg till följande formulärkomponenter:
   * Momsberäkningsformulär (rubrik)
   * Bruttolön (talindata)
   * Ytterligare avdrag (talindata)
   * Skattepliktig inkomst (talindata)
   * Skattepliktig (antal indata)
   * Skicka (Skicka-knapp)
1. Dölj formulärfältet `Additional Deduction` genom att öppna dess `Properties`.

   ![Exempel på regelredigerare](/help/edge/docs/forms/assets/rule-editor2.png)

### 2. Lägg till en villkorsregel för ett formulärfält

När du har skrivit formuläret kan du bara skriva den första regeln för att visa fältet `Additional Deduction` om bruttolönen överstiger 50 000 USD. Så här lägger du till en villkorsregel:

1. Öppna ett formulär i Universal Editor för redigering och markera fältet **[!UICONTROL Gross Salary]** i innehållsträdet och välj ![edit-rules](/help/forms/assets/edit-rules-icon.svg). Du kan också välja fältet **[!UICONTROL Gross Salary]** direkt från rutan **[!UICONTROL Forms Object]**.
   ![Exempel på regelredigerare1](/help/edge/docs/forms/assets/rule-editor3.png)
Gränssnittet för den visuella regelredigeraren visas.
1. Klicka på **[!UICONTROL Create]** om du vill skapa regler.
   ![Exempel på regelredigerare2](/help/edge/docs/forms/assets/rule-editor4.png)
Regeltypen `Set Value Of` är som standard markerad. Du kan inte ändra eller ändra det markerade objektet, men du kan använda listrutan Regel för att välja en annan regeltyp.\
   ![Exempel på regelredigerare3](/help/edge/docs/forms/assets/rule-editor5.png)
1. Öppna listrutan för regeltyp och välj regeltypen **[!UICONTROL When]**.
   ![Exempel på regelredigerare4](/help/edge/docs/forms/assets/rule-editor6.png)
1. Välj listrutan **[!UICONTROL Select State]** och välj **[!UICONTROL is greater than]**. Fältet **[!UICONTROL Enter a Number]** visas.
   ![Exempel på regelredigerare5](/help/edge/docs/forms/assets/rule-editor7.png)
1. Ange `50000` i fältet **[!UICONTROL Enter a Number]** i regeln.
   ![Exempel på regelredigerare6](/help/edge/docs/forms/assets/rule-editor8.png)
Du har definierat villkoret som `When Gross Salary is greater than 50000`. Definiera sedan åtgärden som ska utföras om villkoret är `True`.
1. Välj **[!UICONTROL Show]** i listrutan **[!UICONTROL Select Action]** i programsatsen `Then`.
   ![Exempel på regelredigerare7](/help/edge/docs/forms/assets/rule-editor9.png)
1. Dra och släpp fältet **[!UICONTROL Additional Deduction]** från fliken Formulärobjekt i fältet **[!UICONTROL Drop object or select here]**. Du kan också markera fältet **[!UICONTROL Drop object or select here]** och välja fältet **[!UICONTROL Additional Deduction]** på snabbmenyn, där alla formulärobjekt i formuläret listas.
   ![Exempel på regelredigerare8](/help/edge/docs/forms/assets/rule-editor10.png)
1. Klicka på **[!UICONTROL Add Else Section]** om du vill lägga till ytterligare ett villkor för fältet **[!UICONTROL Gross Salary]** om du anger en lön som är lägre än `50000`.
   ![Exempel på regelredigerare9](/help/edge/docs/forms/assets/rule-editor11.png)
1. Välj **[!UICONTROL Hide]** i listrutan **[!UICONTROL Select Action]** i programsatsen `Else`.
   ![Exempel på regelredigerare10](/help/edge/docs/forms/assets/rule-editor12.png)
1. Dra och släpp fältet **[!UICONTROL Additional Deduction]** från fliken Formulärobjekt i fältet **[!UICONTROL Drop object or select here]**. Du kan också markera fältet **[!UICONTROL Drop object or select here]** och välja fältet **[!UICONTROL Additional Deduction]** på snabbmenyn, där alla formulärobjekt i formuläret listas.
   ![Regelredigeraren, exempel11](/help/edge/docs/forms/assets/rule-editor13.png)
1. Välj **[!UICONTROL Done]** om du vill spara regeln.
Regeln visas så här i Regelredigeraren.
   ![Exempel på regelredigerare12](/help/edge/docs/forms/assets/rule-editor14.png)

>[!NOTE]
>
> Du kan också skriva en Visa-regel i fältet Ytterligare avdrag, i stället för en När-regel i fältet Bruttolön, för att implementera samma beteende.

### 3. Lägg till beräkningsregler för formulärfälten

Skriv sedan en regel för att beräkna `Taxable Income`, vilket är skillnaden mellan `Gross Salary` och `Additional Deduction` (om tillämpligt). Så här lägger du till beräkningsregel i fältet **[!UICONTROL Taxable Income]**:

1. I redigeringsläget markerar du fältet **[!UICONTROL Taxable Income]** och väljer ikonen ![edit-rules](/help/forms/assets/edit-rules-icon.svg) . Du kan också välja fältet **[!UICONTROL Taxable Income]** direkt från rutan **[!UICONTROL Forms Object]**.
1. Välj sedan **[!UICONTROL Create]** för att skapa regeln.
   ![Exempel på regelredigerare13](/help/edge/docs/forms/assets/rule-editor16.png)
1. Välj **[!UICONTROL Select Option]** och välj **[!UICONTROL Mathematical Expression]**. Ett fält som skriver matematiskt uttryck öppnas.
   ![Regelredigeraren, exempel14](/help/edge/docs/forms/assets/rule-editor17.png)

1. I fältet för matematiska uttryck:

   * Markera eller dra och släpp fältet **[!UICONTROL Gross Salary]** i det första **[!UICONTROL Drop object or select here]**-fältet på fliken Forms-objekt.

   * Välj **[!UICONTROL Minus]** i fältet **[!UICONTROL Select Operator]**.

   * Markera eller dra och släpp fältet **[!UICONTROL Additional Deduction]** i det andra **[!UICONTROL Drop object or select here]**-fältet på fliken Forms-objekt.
     ![Regelredigeraren, exempel15](/help/edge/docs/forms/assets/rule-editor18.png)

1. Välj **[!UICONTROL Done]** om du vill spara regeln.

   Lägg nu till en regel för fältet `Tax Payable `, som bestäms genom att multiplicera den beskattningsbara inkomsten med skattesatsen. För enkelhetens skull bör du anta en fast momssats på `10%`.

1. I redigeringsläget markerar du fältet **[!UICONTROL Tax Payable]** och väljer ikonen ![edit-rules](/help/forms/assets/edit-rules-icon.svg) . Välj sedan **[!UICONTROL Create]** för att skapa regler.
   ![Regelredigeraren, exempel16](/help/edge/docs/forms/assets/rule-editor19.png)
1. Välj **[!UICONTROL Select Option]** och välj **[!UICONTROL Mathematical Expression]**. Ett fält som skriver matematiskt uttryck öppnas.
   ![Regelredigeraren, exempel17](/help/edge/docs/forms/assets/rule-editor20.png)
1. I fältet för matematiska uttryck:

   * Markera eller dra och släpp fältet **[!UICONTROL Taxable Income]** i det första **[!UICONTROL Drop object or select here]**-fältet på fliken Forms-objekt.

   * Välj **[!UICONTROL Multiplied by]** i fältet **[!UICONTROL Select Operator]**.

   * Välj **Number** i fältet **[!UICONTROL Select Option]** och ange värdet som `10` i fältet **[!UICONTROL Enter a Number]**.
     ![Regelredigeraren, exempel18](/help/edge/docs/forms/assets/rule-editor21.png)
1. Välj sedan **[!UICONTROL Extend Expression]** i det markerade området runt uttrycksfältet.
   ![Regelredigeraren, exempel19](/help/edge/docs/forms/assets/rule-editor22.png)
1. I fältet för utökat uttryck väljer du **[!UICONTROL divided by]** i fältet **[!UICONTROL Select Operator]** och **[!UICONTROL Number]** i fältet **[!UICONTROL Select Option]**. Ange sedan `100` i nummerfältet.
   ![Exempel på regelredigerare20](/help/edge/docs/forms/assets/rule-editor23.png)
1. Välj **[!UICONTROL Done]** om du vill spara regeln.

### 4. Förhandsgranska ett formulär

När du nu förhandsgranskar formuläret och anger **bruttolön** som `60,000` visas fältet **Ytterligare avdrag** och fältet **Skattepliktig inkomst** och **Skatteskuld** beräknas därefter.

![Förhandsgranska ett formulär](/help/edge/docs/forms/assets/rule-editor-form.png)

Förutom användningsklara funktioner som Summa, Medel som visas under Funktioner Output, kan du [skriva anpassade funktioner](#create-a-custom-function) för att implementera komplexa affärslogik.

## Egen funktion i regelredigeraren

Edge Delivery Services Forms har stöd för anpassade funktioner som gör att man kan definiera JavaScript-funktioner för att implementera komplexa affärsregler. Med de anpassade funktionerna kan man bättre hantera blanketterna genom att underlätta hanteringen och bearbetningen av inmatade data.

### Skapa en anpassad funktion

Om du vill skapa anpassade funktioner redigerar du filen `../[blocks]/form/functions.js`. Att skapa innefattar i allmänhet följande steg:

* **Funktionsdeklaration**: Definiera funktionsnamnet och dess parametrar (de indata som accepteras).
* **Logikimplementering**: Skriv koden som anger de specifika beräkningar eller ändringar som utförs av funktionen.
* **Funktionsexport**: Gör funktionen tillgänglig i reglerna genom att exportera den från den relevanta filen.


I det här exemplet visas två anpassade funktioner som `getFullName` och `days`:

```JavaScript
/**
 * Get Full Name
 * @name getFullName Concats first name and last name
 * @param {string} firstname in Stringformat
 * @param {string} lastname in Stringformat
 * @return {string}
 */
function getFullName(firstname, lastname) {
  return `${firstname} ${lastname}`.trim();
}

/**
 * Calculate the number of days between two dates.
 * @param {*} endDate
 * @param {*} startDate
 * @name days Calculates the numebr of days between two dates
 * @returns {number} returns the number of days between two dates
 */
function days(endDate, startDate) {
  const start = typeof startDate === 'string' ? new Date(startDate) : startDate;
  const end = typeof endDate === 'string' ? new Date(endDate) : endDate;

  // return zero if dates are valid
  if (Number.isNaN(start.getTime()) || Number.isNaN(end.getTime())) {
    return 0;
  }

  const diffInMs = Math.abs(end.getTime() - start.getTime());
  return Math.floor(diffInMs / (1000 * 60 * 60 * 24));
}

// eslint-disable-next-line import/prefer-default-export
export { getFullName, days };
```
![Lägger till anpassad funktion](/help/edge/docs/forms/assets/create-custom-function.png)

### Använda en anpassad funktion i regelredigeraren

Så här använder du den anpassade funktionen i Regelredigeraren:

1. **Lägg till funktionen**: Inkludera din anpassade funktion i filen `../[blocks]/form/functions.js`. Kom ihåg att lägga till den i programsatsen `export` i filen.
1. **Distribuera filen**: Distribuera den uppdaterade `functions.js` filen till ditt GitHub-projekt och verifiera att bygget lyckades.
1. **Funktionsanvändning**: Du kommer åt funktionen i regelredigeraren i ditt formulär genom att välja alternativet `Function Output` i fältet **[!UICONTROL Select Action]**.

   ![Anpassad funktion i regelredigeraren](/help/edge/docs/forms/assets/custom-function-rule-editor.png)

1. **Förhandsgranska formuläret**: Förhandsgranska formuläret med den nyligen implementerade funktionen.

## Ytterligare information

>[!NOTE]
>
> I Universal Editor stöds inte statiska och dynamiska importer i anpassade funktionsskript. Du måste lägga till den fullständiga koden i filen `../[blocks]/form/functions.js`.

I den här artikeln finns begränsad information om regelredigeraren som är tillgänglig i den universella redigeraren. Mer information om regelredigeraren och anpassade funktioner finns i följande artiklar:

{{see-also-rule-editor}}

## Se även

{{universal-editor-see-also}}

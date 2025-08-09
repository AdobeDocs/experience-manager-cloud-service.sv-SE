---
title: Regelredigeraren för Dynamic Forms i Universell redigerare
description: Skapa dynamiska, intelligenta formulär med regelredigeraren i Universell redigerare. Lägg till villkorsstyrd logik, beräkningar och interaktiva beteenden utan kodning.
feature: Edge Delivery Services
role: Admin, Architect, Developer
level: Intermediate
exl-id: 846f56e1-3a98-4a69-b4f7-40ec99ceb348
source-git-commit: 44a8d5d5fdd2919d6d170638c7b5819c898dcefe
workflow-type: tm+mt
source-wordcount: '2598'
ht-degree: 0%

---


# Regelredigeraren för Dynamic Forms i Universell redigerare

Med regelredigeraren kan författare omvandla statiska formulär till responsiva, intelligenta upplevelser - utan att behöva skriva kod. Du kan villkorligt visa fält, utföra beräkningar, validera data, vägleda användare genom flöden och integrera affärslogik som anpassas som persontyp.

## Vad du kommer att lära dig

I slutet av guiden kan du:

- Förstå hur regler fungerar och när olika regeltyper ska användas
- Aktivera och öppna regelredigeraren i Universell redigerare
- Skapa villkorlig logik för att visa eller dölja fält dynamiskt
- Implementera automatiserade beräkningar och datavalidering
- Bygg anpassade funktioner för komplexa affärsregler
- Tillämpa bästa praxis för prestanda, underhåll och användarupplevelse

## Varför ska jag använda regelredigeraren?

- **Villkorlig logik**: Visa endast relevanta fält när det behövs för att minska brus och kognitiv belastning.
- **Dynamiska beräkningar**: Beräkna värden automatiskt (summor, satser, skatt) som användartyp.
- **Dataverifiering**: Förhindra fel tidigt med realtidskontroller och tydliga meddelanden.
- **Guidade upplevelser**: Leda användare genom logiska steg (guider, förgreningar).
- **Ingen kodredigering**: Konfigurera kraftfullt beteende via ett visuellt gränssnitt.

Vanliga scenarier är skattekalkylatorer, låne- och premieskattningar, berättigandeflöden, flerstegsansökningar och enkäter med villkorliga frågor.

## Så här fungerar regler

En regel definierar vad som ska hända när ett villkor är uppfyllt. En regel består av två delar:

- **Villkor**: En sats som utvärderas till sant eller falskt.
   - Exempel: Inkomst > 50 000, Täckning = Ja, fältet är tomt
- **Åtgärd**: Vad händer när villkoret är sant (och eventuellt när det är falskt).
   - Exempel: Visa/dölj ett fält, Ange/Rensa ett värde, Validera indata, Aktivera/Inaktivera en knapp

+++ Regellogiksmönster

- **Villkor → Åtgärd (När/sedan)**

  ```text
  WHEN Gross Salary > 50000
  THEN Show "Additional Deduction"
  ```

  Bäst för villkorlig synlighet och progressiv visning.

- **Åtgärd > Villkor (ange om/Endast om)**

  ```text
  SET Taxable Income = Gross Salary - Deductions
  IF Deductions are applicable
  ```

  Passar bäst för beräkningar och dataomvandlingar.

- **If → then → Else (Alternate action)**

  ```text
  IF Income > 50000
  THEN Show "High Income" fields
  ELSE Show "Standard Income" fields
  ```

  Bäst för förgreningslogik och ömsesidigt uteslutande flöden.

+++

+++ Exempel från verkligheten

- **Villkor**: &quot;Bruttolönen överstiger 50 000 dollar&quot;
- **Primär åtgärd**: Visa &quot;Ytterligare avdrag&quot;
- **Alternativ åtgärd**: Dölj &quot;Ytterligare avdrag&quot;
- **Resultat**: Användarna ser bara de fält som gäller dem

+++

## Förutsättningar


+++ Åtkomstkrav

**Grundläggande behörigheter och konfiguration**:

- **AEM as a Cloud Service**: Redigeringsåtkomst med redigeringsbehörigheter för formulär
- **Universal Editor**: Installerad och konfigurerad i din miljö
- **Regelredigerartillägg**: Aktiverat via [Extension Manager](/help/implementing/developing/extending/extension-manager.md)
- **Behörigheter för formulärredigering**: Möjlighet att skapa och ändra formulärkomponenter i den universella redigeraren

**Verifieringssteg**:

1. Bekräfta att du har åtkomst till Universal Editor från AEM Sites-konsolen
2. Verifiera att du kan skapa och redigera formulärkomponenter
3. Kontrollera att ikonen för regelredigeraren ![redigeringsregler](/help/forms/assets/edit-rules-icon.svg) visas när du väljer formulärkomponenter

+++

+++ Tekniska krav

**Nödvändiga kunskaper och färdigheter**:

- **Kompetens för universell redigerare**: Upplev hur du skapar formulär med textinmatningar, listrutor och grundläggande fältegenskaper
- **Förståelse av affärslogik**: Möjlighet att definiera villkorliga krav och valideringsregler för ditt specifika användningsfall
- **Förtrogenhet för formulärkomponenter**: Kunskap om fälttyper (text, tal, listruta), egenskaper (obligatoriskt, synligt, skrivskyddat) och formulärstruktur

**Valfritt för avancerad användning**:

- **Grundläggande om JavaScript**: Krävs endast för att skapa anpassade funktioner (datatyper, funktioner, grundläggande syntax)
- **JSON-förståelse**: Användbar för komplex datahantering och API-integreringar

**Utvärderingsfrågor**:

- Kan du skapa ett enkelt formulär med textinmatningar och en skicka-knapp i Universell redigerare?
- Förstår du när fält ska behövas eller vara valfria i ditt sammanhang?
- Kan du identifiera vilka formulärelement som behöver villkorlig synlighet i ditt fall?

+++

+++ Aktivera tillägget Regelredigerare

**Viktigt**: Tillägget för regelredigeraren är inte aktiverat som standard i Universal Editor-miljöer.

**Aktiveringssteg**:

1. Navigera till [Extension Manager](/help/implementing/developing/extending/extension-manager.md) i din AEM-miljö
2. Leta reda på tillägget Regelredigerare i listan med tillgängliga tillägg
3. Klicka på **Aktivera** och bekräfta aktiveringen
4. Vänta tills systemet har uppdaterats (kan ta 1-2 minuter)

**Verifiering**:

- När du har aktiverat visas ikonen för regelredigeraren när du väljer en formulärkomponent: ![edit-rules](/help/forms/assets/edit-rules-icon.svg)

![Regelredigeraren Universal Editor](/help/edge/docs/forms/assets/universal-editor-rule-editor.png)
Bild: Ikonen för regelredigeraren visas när du väljer formulärkomponenter

Så här öppnar du Regelredigeraren:

1. Markera en formulärkomponent i Universell redigerare.
2. Klicka på ikonen Regelredigerare.
3. Regelredigeraren öppnas på en sidopanel.

![Användargränssnittet i regelredigeraren](/help/edge/docs/forms/assets/rule-editor-for-field.png)
Bild: Gränssnitt för regelredigerare för redigering av komponentregler

>[!NOTE]
>
> I den här artikeln avser&quot;formulärelement&quot; och&quot;formulärobjekt&quot; samma element (t.ex. indata, knappar, paneler).

## Översikt över regelredigeringsgränssnittet

![Användargränssnitt för regelredigeraren](/help/edge/docs/forms/assets/rule-editor-interface.png)
Bild: Fullständigt gränssnitt för regelredigeraren med numrerade komponenter

- **Komponenttitel och regeltyp**: Bekräftar den valda komponenten och den aktiva regeltypen.
- **Panelen Formulärobjekt och funktioner**:
   - Formulärobjekt: hierarkisk vy med fält och behållare för referens i regler
   - Funktioner: inbyggda hjälpmedel för matematik, sträng, datum och validering
- **Växla panel**: Visa/dölj objekt- och funktionspanelen för att öka arbetsytan
- **Visual rule builder**: Drag-and-drop-driven regeldisposition
- **Kontroller**: Klart (spara), Avbryt (ignorera). Testa alltid reglerna innan du sparar.

+++

+++ Hantera befintliga regler

När en komponent redan har regler kan du:

- **Visa**: Se regelsammanfattningar och logik
- **Redigera**: Ändra villkor och åtgärder
- **Ändra ordning**: Ändra körningsordning (uppifrån och ned)
- **Aktivera/inaktivera**: Växla regler för testning
- **Ta bort**: Ta bort regler säkert

>[!TIP]
>
> Ställ specifika regler före de allmänna. Körningen är uppifrån och ned.

+++

## Tillgängliga regeltyper

Välj den regeltyp som bäst matchar din avsikt.

+++ Villkorlig logik

- **När**: Primär regel för komplext villkorligt beteende (villkor → Åtgärd ± Annars)
- **Dölj/Visa**: Kontrollerar synlighet baserat på ett villkor (progressiv visning)
- **Aktivera/Inaktivera**: Kontrollerar om ett fält är interaktivt (t.ex. inaktivera Skicka tills de obligatoriska fälten är giltiga)

+++

+++ Datahantering

- **Ange värdet för**: Fyll i värden automatiskt (till exempel datum, summor, kopior)
- **Rensa värdet för**: Ta bort data när villkoren ändras
- **Format**: Omforma visningsformatering (valuta, telefon, datum) utan att ändra lagrade värden

+++

+++ Validering

- **Validera**: Anpassad valideringslogik, inklusive fältkontroller och affärsregler

+++

+++ Beräkning

- **Matematiskt uttryck**: Beräkna värden i realtid (summor, skatt, proportioner)

+++

+++ Användargränssnitt

- **Ange fokus**: Flytta fokus till ett visst fält (använd sparsamt)
- **Ange egenskap**: Ändra komponentegenskaper dynamiskt (platshållare, alternativ osv.)

+++

+++ Formulärkontroll

- **Skicka formulär**: Skicka formuläret programmatiskt (endast efter att valideringarna har skickats)
- **Återställ formulär**: Rensa och återställ till ursprungligt läge (bekräfta före användning)
- **Spara formulär**: Spara som utkast för senare (långa formulär, flera sessioner)

+++

+++ Avancerat

- **Anropa tjänsten**: Anropa externa API:er/tjänster (hantera inläsning och fel)
- **Lägg till/ta bort instans**: Hantera repeterbara avsnitt (t.ex. beroenden, adresser)
- **Navigera till**: Dirigera till andra formulär/sidor (bevara data före navigering)
- **Navigera bland paneler**: Stegnavigering och hoppa över i kontrollguiden
- **Skicka händelse**: Utlös anpassade händelser för integreringar eller analyser

+++

## Stegvis självstudiekurs: Bygg en smart skattekalkylator

+++ Självstudiekurs - översikt

I det här exemplet visas villkorlig synlighet och automatiska beräkningar.

![Skärmbild av gränssnittet i regelredigeraren som visar hur en villkorsregel skapas med logiken När-Då för formulärfältets synlighet ](/help/edge/docs/forms/assets/rule-editor-1.png)
Bild: Formulär för momsberäkning med intelligenta villkorsfält

Du skapar ett formulär som:

1. Anpassar till användarindata genom att visa relevanta fält
2. Beräknar värden i realtid
3. Validerar data för att förbättra noggrannheten

+++

+++ Formulärstruktur

| Fältnamn | Typ | Syfte | Beteende |
|-------------------------|---------------|--------------------------------|-----------------------------------------|
| Bruttolön | Nummerindata | Användarens årsinkomst | Villkorlig logik för utlösare |
| Ytterligare avdrag | Nummerindata | Extra avdrag (om de är berättigade) | Visas endast när Lön > $50 000 |
| Skattepliktig inkomst | Nummerindata | Beräknat värde | Skrivskyddad, uppdateringar vid ändring |
| Skatteskuld | Nummerindata | Beräknat värde | Skrivskyddad, beräknad med ett fast pris |

+++

+++ Affärslogik

- **Regel 1: Villkorlig visning**

  ```text
  WHEN Gross Salary > 50,000
  THEN Show "Additional Deduction"
  ELSE Hide "Additional Deduction"
  ```

- **Regel 2: Beräkning av skattepliktig inkomst**

  ```text
  SET Taxable Income = Gross Salary - Additional Deduction
  (Only when Additional Deduction applies)
  ```

- **Regel 3: Skattepliktig beräkning**

  ```text
  SET Tax Payable = Taxable Income × 10%
  (Simplified flat rate)
  ```

+++

+++ Steg 1: Skapa grundformuläret

**Mål**: Bygg basformuläret med alla fält och ursprungliga inställningar.

1. **Öppna Universal Editor**:
   - Navigera till AEM Sites-konsolen, markera sidan och klicka på **Redigera**
   - Kontrollera att [Universal Editor](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/introduction.html?lang=sv-SE) är korrekt konfigurerad

2. **Lägg till formulärkomponenter i den här ordningen**:
   - Titel (H2):&quot;Skatteberäkningsformulär&quot;
   - Antal indata:&quot;Bruttolön&quot; (obligatoriskt: Ja, platshållare:&quot;Ange årslön&quot;)
   - Nummerinmatning:&quot;Ytterligare avdrag&quot; (krävs: Nej, platshållare:&quot;Ange ytterligare avdrag&quot;)
   - Antal indata:&quot;Skattepliktig inkomst&quot; (skrivskyddat: Ja)
   - Antal indata: Skatteskuld (skrivskyddat: Ja)
   - Skicka-knapp: &quot;Beräkna moms&quot;

3. **Konfigurera egenskaper för inledande fält**:
   - Dölj &quot;Ytterligare avdrag&quot; (ange Synlig: Nej på egenskapspanelen)
   - Ange&quot;Skattepliktig inkomst&quot; och&quot;Skattepliktig&quot; till Skrivskyddad: Ja

![Skärmbild av ett momsberäkningsformulär med inmatningsfält för bruttolön, civilstånd och underordnade, som visar formulärstrukturen innan reglerna tillämpas](/help/edge/docs/forms/assets/rule-editor2.png)
Bild: Inledande formulärstruktur med grundläggande komponenter konfigurerade

**Kontrollpunkt**: Du bör ha ett formulär med alla obligatoriska fält där Ytterligare avdrag är dolt och beräknade fält är skrivskyddade.

+++

+++ Steg 2: Lägg till regel för villkorlig synlighet

**Mål**: Visa fältet Ytterligare avdrag bara när bruttolönen överstiger 50 000 USD.

1. **Markera fältet Bruttolön** och klicka på ikonen Regelredigeraren ![edit-rules](/help/forms/assets/edit-rules-icon.svg)
2. **Skapa en ny regel**:
   - Klicka på **Skapa**
   - Ändra regeltyp från Ange värde av till **När**
3. **Konfigurera villkoret**:
   - Välj **större än** i listrutan
   - Ange `50000` i nummerfältet
4. **Ange sedan åtgärd**:
   - Välj **&quot;Visa&quot;** i listrutan Välj åtgärd
   - Dra eller markera fältet **&quot;Ytterligare reduktion&quot;** från formulärobjekt
5. **Lägg till Else-åtgärden**:
   - Klicka på **&quot;Lägg till annat avsnitt&quot;**
   - Välj **&quot;Dölj&quot;** i listrutan Välj åtgärd
   - Välj fältet **&quot;Additional Deduction&quot;**
6. **Spara regeln**: Klicka på **Klar**

>[!NOTE]
>
> Alternativ metod: Du kan uppnå samma resultat genom att skapa en Visa/dölj-regel direkt i fältet&quot;Ytterligare avdrag&quot; i stället för en När-regel för&quot;Bruttolön&quot;.

+++

+++ Steg 3: Lägg till beräkningsregler

**Mål**: Beräkna automatiskt&quot;skattepliktig inkomst&quot; och&quot;skatteskuld&quot; baserat på användarindata.

**Konfigurera beräkning av beskattningsbar inkomst**:

1. **Välj fältet Skattepliktig inkomst** och öppna regelredigeraren
2. **Skapa matematiskt uttryck**:
   - Klicka på **Skapa** → Välj **&quot;Matematiskt uttryck&quot;**
   - Build-uttryck: **Bruttolön - ytterligare avdrag**
   - Dra&quot;Bruttolön&quot; till första fältet
   - Välj operatorn **&quot;Minus&quot;**
   - Dra &quot;Additional Deduction&quot; (Ytterligare minskning) till det andra fältet
3. **Spara**: Klicka på **Klar**

**Konfigurera beräkning av skatteskuld**:

1. **Välj fältet Skatteskuld** och öppna regelredigeraren
2. **Skapa matematiskt uttryck**:
   - Klicka på **Skapa** → Välj **&quot;Matematiskt uttryck&quot;**
   - Build-uttryck: **Skattepliktig inkomst × 10‡ 100**
   - Dra&quot;Skattepliktig inkomst&quot; till det första fältet
   - Välj operatorn **&quot;Multiplicerad av&quot;**
   - Ange `10` som nummer
   - Klicka på **&quot;Utöka uttryck&quot;**
   - Välj operatorn **dividerat med**
   - Ange `100` som nummer
3. **Spara**: Klicka på **Klar**

+++

+++ Steg 4: Testa formuläret

**Verifiera implementeringen genom att testa det fullständiga flödet**:

1. **Förhandsgranska formuläret**: Klicka på förhandsgranskningsläget i Universal Editor
2. **Testa den villkorliga logiken**:
   - Ange bruttolön = `30000` → &quot;Ytterligare avdrag&quot; ska förbli dold
   - Ange bruttolön = `60000` → &quot;Ytterligare avdrag&quot; ska visas
3. **Testa beräkningar**:
   - Med bruttolön = `60000`, ange ytterligare avdrag = `5000`
   - Verifiera skattepliktig inkomst = `55000` (60000 - 5000)
   - Verifiera att skatt betalas = `5500` (55000 × 10 %)

![Förhandsgranska ett formulär](/help/edge/docs/forms/assets/rule-editor-form.png)
Bild: Slutförd momskalkylator med villkorsfält och automatiska beräkningar

**Slutförandevillkor**: Formuläret ska dynamiskt visa/dölja fält och beräkna värden i realtid när användare skriver.


+++

## Avancerat: Anpassade funktioner

För mer komplex affärslogik än inbyggda funktioner kan du skapa anpassade JavaScript-funktioner som integreras smidigt med regelredigeraren.

+++ När anpassade funktioner ska användas

**Idealiska scenarier för anpassade funktioner**:

- **Komplexa beräkningar**: Flerstegsberäkningar kan inte uttryckas så lätt i den matematiska uttrycksregeln
- **Affärsspecifika valideringar**: Anpassad valideringslogik som är specifik för din organisation eller bransch
- **Dataomvandlingar**: Formatkonverteringar, strängändringar eller dataparsning
- **Externa integreringar**: Anrop till interna API:er eller tredjepartstjänster (med begränsningar)

**Fördelar med anpassade funktioner**:

- **Återanvändbarhet**: Skriv en gång, använd i flera formulär och regler
- **Underhållbarhet**: Centraliserad logik som är enklare att uppdatera och felsöka
- **Prestanda**: Optimerad körning av JavaScript jämfört med komplexa regelkedjor
- **Flexibilitet**: Hantera kantfall och komplexa scenarier som inte hanteras av standardregler

+++

+++ Skapa och implementera anpassade funktioner

**Filplats**: Alla anpassade funktioner måste definieras i `/blocks/form/functions.js` i ditt Edge Delivery Services-projekt.

**Utvecklingsarbetsflöde**:

1. **Funktionsdesign**
   - Använd beskrivande, funktionsorienterade funktionsnamn
   - Definiera tydliga parametertyper och returvärden
   - Hantera kantfall och ogiltiga indata på ett smidigt sätt

2. **Implementering**
   - Skriv ren, välkommenterad JavaScript
   - Inkludera indatavalidering och felhantering
   - Testa funktionerna oberoende av varandra före integreringen

3. **Dokumentation**
   - Lägg in omfattande JSDoc-kommentarer
   - Inkludera exempel och parameterbeskrivningar
   - Dokumentera eventuella begränsningar eller beroenden

4. **Distribution**
   - Exportera funktioner med namngiven export
   - Distribuera till din projektdatabas
   - Verifiera byggslutförande före testning

**Exempel på implementering**:

```javascript
/**
 * Concatenates first and last name with proper formatting
 * @name getFullName
 * @description Combines first and last name, handles edge cases like missing values
 * @param {string} firstName - The person's first name
 * @param {string} lastName - The person's last name  
 * @returns {string} Formatted full name or empty string if both inputs are invalid
 */
function getFullName(firstName, lastName) {
  // Handle null, undefined, or empty string inputs
  const first = (firstName || '').toString().trim();
  const last = (lastName || '').toString().trim();
  
  return `${first} ${last}`.trim();
}

/**
 * Calculates the number of days between two dates
 * @name days
 * @description Computes absolute difference in days, handles various date input formats
 * @param {Date|string} endDate - End date (Date object or ISO string)
 * @param {Date|string} startDate - Start date (Date object or ISO string)
 * @returns {number} Number of days between dates, 0 if inputs are invalid
 */
function days(endDate, startDate) {
  // Convert string inputs to Date objects
  const start = typeof startDate === 'string' ? new Date(startDate) : startDate;
  const end = typeof endDate === 'string' ? new Date(endDate) : endDate;

  // Validate date objects
  if (Number.isNaN(start.getTime()) || Number.isNaN(end.getTime())) {
    return 0;
  }

  // Calculate absolute difference in milliseconds, then convert to days
  const diffInMs = Math.abs(end.getTime() - start.getTime());
  return Math.floor(diffInMs / (1000 * 60 * 60 * 24));
}

// Export functions for use in Rule Editor
export { getFullName, days };
```

![Lägger till anpassad funktion](/help/edge/docs/forms/assets/create-custom-function.png)
Bild: Lägga till anpassade funktioner i filen functions.js

+++

+++ Använda anpassade funktioner i Regelredigeraren

**Integreringssteg**:

1. **Lägg till funktion i projekt**
   - Skapa eller redigera `/blocks/form/functions.js` i ditt projekt
   - Inkludera funktionen i exportsatsen

2. **Distribuera och bygg**
   - Genomför ändringar i din databas
   - Kontrollera att byggprocessen har slutförts
   - Tillåt tid för CDN-cacheuppdateringar

3. **Åtkomst i regelredigeraren**
   - Öppna regelredigeraren för alla formulärkomponenter
   - Välj **&quot;Funktionsutdata&quot;** i listrutan **Välj åtgärd**
   - Välj en anpassad funktion i listan med tillgängliga funktioner
   - Konfigurera funktionsparametrar med formulärfält eller statiska värden

4. **Testa noggrant**
   - Förhandsgranska formuläret för att verifiera funktionens beteende
   - Testa med olika indatakombinationer, inklusive kantfall
   - Verifiera prestanda vid inläsning och interaktion av formulär

![Anpassad funktion i regelredigeraren](/help/edge/docs/forms/assets/custom-function-rule-editor.png)
Bild: Välja och konfigurera anpassade funktioner i regelredigeraren

**Bästa tillvägagångssätt för funktionsanvändning**:

- **Felhantering**: Inkludera alltid reservbeteende för funktionsfel
- **Prestanda**: Profilfunktioner med realistiska datavolymer
- **Säkerhet**: Verifiera alla indata för att förhindra säkerhetsproblem
- **Testning**: Skapa testfall som täcker normala fall och kantfall

+++

## Bästa tillvägagångssätt för regelutveckling


+++ Prestandaoptimering

- Minimera regelkomplexiteten; dela upp stora logik i små, fokuserade regler
- Ordna regler efter frekvens (vanligaste först)
- Behåll regeluppsättningar per komponent hanterbara
- Föredra återanvändbara anpassade funktioner framför dupliceringslogik

+++

+++ Användarupplevelse

- Ge tydlig validering och intern feedback
- Undvik att darra visuella ändringar; använd visa/dölj noggrant
- Testa olika enheter och layouter

+++

+++ Utvecklingshygien

- Testa med kantfall och kända värden
- Verifiera i olika webbläsare
- Dokumentåtergivning bakom komplexa regler, inte bara mekaniker
- Underhåll ett regellager för stora formulär
- Använd konsekvent namngivning för komponenter och regler
- Versionsanpassade funktioner och tester i icke-produktionsmiljöer

+++

## Felsöka vanliga problem


+++ Regler som inte aktiveras

- Verifiera komponentnamn och referenser
- Kontrollera körningsordning (uppifrån och ned)
- Validera villkor med kända värden
- Kontrollera webbläsarkonsolen för att se om det finns blockeringsfel

+++

+++ Felaktigt beteende

- Granska operatorer och gruppera (AND/OR)
- Testa uttrycksfragment individuellt
- Bekräfta datatyper (tal kontra strängar)

+++

+++ Prestandaproblem

- Förenkla djupt inkapslade förhållanden
- Egna profilfunktioner
- Minimera externa samtal inuti regler
- Använd specifika väljare och referenser

+++

+++ Anpassade funktionsproblem

- Bekräfta filsökväg: `/blocks/form/functions.js`
- Kontrollera att namngivna exporter är korrekta
- Bekräfta att bygget innehåller dina ändringar
- Rensa webbläsarcache efter distribution
- Validera parametertyper och felhantering

+++

+++ Integrering med Universal Editor

- Bekräfta att tillägget Regelredigeraren är aktiverat
- Välj en komponent som stöds
- Använda en webbläsare som stöds (Chrome, Firefox, Safari)
- Verifiera att du har nödvändig behörighet

## Viktiga begränsningar

>[!IMPORTANT]
>
> Begränsningar för anpassade funktioner:
>
> - Statisk/dynamisk import stöds inte
> - All logik måste finnas i `/blocks/form/functions.js`
> - Funktioner måste vara synkrona (ingen asynkron/await eller Promises)
> - Åtkomsten till webbläsar-API:t är begränsad

>[!WARNING]
>
> Produktionshänsyn:
>
> - Testa noggrant under mellanlagring
> - Övervaka prestanda efter driftsättning
> - Har en återställningsplan för regelproblem
> - Överväg långsamma nätverk och enheter med låg hastighet

## Sammanfattning

Regelredigeraren i den universella redigeraren omvandlar statiska formulär till intelligenta, responsiva upplevelser som anpassar sig efter användarens inmatningar i realtid. Genom att utnyttja villkorslogik, automatiserade beräkningar och anpassade affärsregler kan ni skapa avancerade arbetsflöden för formulär utan att behöva skriva programkod.

**Viktiga funktioner som du har lärt dig**:

- **Villkorlig logik**: Visa och dölj fält baserat på användarindata för att skapa fokuserade, relevanta upplevelser
- **Dynamiska beräkningar**: Beräkna värden automatiskt (skatter, summor, frekvenser) när användarna interagerar med formuläret
- **Dataverifiering**: Implementera realtidsvalidering med tydliga, åtgärdbara feedbackmeddelanden
- **Anpassade funktioner**: Utöka möjligheterna med JavaScript för komplex affärslogik och integrering
- **Prestandaoptimering**: Tillämpa bästa praxis för underhåll och effektiv regelutveckling

**Värde levererat**:

- **Förbättrad användarupplevelse**: Minska kognitiv belastning med progressiv identifiering och intelligenta formulärflöden
- **Minskade fel**: Förhindra ogiltiga inskickade data genom realtidsvalidering och styrda indata
- **Förbättrad effektivitet**: Automatisera beräkningar och datainmatning för att minimera användarnas arbete
- **Underhållbara lösningar**: Skapa återanvändbara, väldokumenterade regler som kan skalas i hela organisationen

**Affärspåverkan**:

Forms blir kraftfulla verktyg för datainsamling, kvalificering av leads och användarengagemang. Regelredigeraren gör det möjligt för icke-tekniska författare att implementera avancerad affärslogik, minska utvecklingskostnaderna och samtidigt förbättra antalet ifyllda formulär och datakvaliteten.

+++

+++ Nästa steg

**Rekommenderad utbildningsväg**:

1. **Börja med grunderna**: Skapa enkla regler för att visa/dölja för att förstå de grundläggande begreppen
2. **Öva med självstudiekurser**: Använd exemplet med beräkningsverktyget för skatt som grund för dina egna formulär
3. **Utöka gradvis**: Lägg till matematiska uttryck och valideringsregler allt eftersom förtroendet ökar
4. **Implementera anpassade funktioner**: Utveckla JavaScript-funktioner för särskilda affärskrav
5. **Optimera och skala**: Använd bästa praxis för prestanda och underhåll regeldokumentation

**Ytterligare resurser**:

- [Dokumentation för Universal Editor](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/introduction.html?lang=sv-SE) för ett bredare sammanhang
- [Extension Manager guide](/help/implementing/developing/extending/extension-manager.md) för att aktivera ytterligare funktioner
- [Edge Delivery Services-formulär](/help/edge/docs/forms/overview.md) för omfattande riktlinjer för formulärutveckling

+++

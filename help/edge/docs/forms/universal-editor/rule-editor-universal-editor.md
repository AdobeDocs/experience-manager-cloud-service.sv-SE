---
title: Regelredigeraren för Dynamic Forms i Universell redigerare
description: Skapa dynamiska, intelligenta formulär med regelredigeraren i Universell redigerare. Lägg till villkorsstyrd logik, beräkningar och interaktiva beteenden utan kodning.
feature: Edge Delivery Services
role: Admin, Architect, Developer
level: Intermediate
exl-id: 846f56e1-3a98-4a69-b4f7-40ec99ceb348
source-git-commit: 2e2a0bdb7604168f0e3eb1672af4c2bc9b12d652
workflow-type: tm+mt
source-wordcount: '3472'
ht-degree: 0%

---


# Regelredigeraren för Dynamic Forms i Universell redigerare

Med regelredigeraren i Universal Editor kan du skapa intelligenta, dynamiska formulär som svarar på användarens inmatningar i realtid. Ni kan omvandla statiska formulär till interaktiva upplevelser med villkorlig fältsynlighet, automatiska beräkningar och komplex affärslogik - allt utan att behöva skriva kod.

## Vad du kommer att lära dig

I slutet av guiden kommer du att:

- Förstå hur regler fungerar och när olika regeltyper ska användas
- Aktivera och öppna regelredigeraren i Universell redigerare
- Skapa villkorslogik för att visa eller dölja formulärfält dynamiskt
- Implementera automatiserade beräkningar och datavalidering
- Bygg anpassade funktioner för komplexa affärsregler
- Tillämpa bästa praxis för optimala formulärprestanda

## Varför ska jag använda regelredigeraren?

**Omvandla statisk Forms till smarta upplevelser:**

- **Villkorlig logik**: Visa relevanta fält baserat på användarval
- **Dynamiska beräkningar**: Beräkna värden automatiskt när användare skriver
- **Dataverifiering**: Ge feedback i realtid och förhindra fel
- **Förbättrat användargränssnitt**: Minska formulärens komplexitet och vägleda användarna genom logiska flöden
- **Ingen kodning krävs**: Visuellt gränssnitt tillgängligt för icke-utvecklare

**Vanliga användningsexempel:**

- Skatteberäkningsformulär med villkorliga avdrag
- Guider i flera steg med förgrenade banor
- Försäkringsformulär med tariffberäkningar
- Enkätformulär med villkorliga frågor
- E-handelsblanketter med dynamisk prissättning

## Hur regler fungerar

Reglerna är automatiserade instruktioner som gör formulären intelligenta och responsiva. De anger vad som ska hända när vissa villkor är uppfyllda.

### **Regelkomponenter**

**Villkor**: Ett logiskt test som utvärderas till sant eller falskt.

- &quot;Är användarens inkomster större än 50 000 dollar?&quot;
- &quot;Har användaren valt &quot;Ja&quot; för försäkringsskydd?&quot;
- &quot;Är formulärfältet tomt?&quot;

**Åtgärd**: Resultatet som inträffar när villkoret uppfylls.

- Visa eller dölja formulärfält
- Beräkna värden automatiskt
- Visa valideringsmeddelanden
- Aktivera eller inaktivera komponenter

### **Regellogikmönster**

**1. Villkorsåtgärd (When-then)**

```
WHEN gross salary > 50000
THEN show "Additional Deduction" field
```

*Bäst för:* Villkorlig fältsynlighet, dynamiskt innehåll

**2. Åtgärdsvillkor (ange om)**

```
SET taxable income = gross salary - deductions
IF deductions are applicable
```

*Bäst för:* Beräkningar, dataomvandlingar

**3. Action-Condition-Alternate (If-then-Else)**

```
IF income > 50000
THEN show "High Income" fields
ELSE show "Standard Income" fields
```

*Passar bäst för:* Förgreningslogik, alternativ som utesluter varandra

### **Real-World Example**

**Scenario**: Formulär för momsberäkning

- **Villkor**: &quot;Bruttolönen överstiger 50 000 dollar&quot;
- **Primär åtgärd**: Visa fältet &quot;Ytterligare minskning&quot;
- **Alternativ åtgärd**: Dölj fältet &quot;Ytterligare minskning&quot;
- **Resultat**: Användarna ser bara relevanta fält utifrån sin inkomstnivå

## Förutsättningar

Innan du börjar arbeta med regelredigeraren bör du kontrollera att du har följande:

### **Åtkomstkrav**

- Redigeringsåtkomst till **AEM as a Cloud Service**
- **Universell redigerare** med regelredigerartillägget aktiverat
- Behörigheter för formulärredigering i din AEM-miljö

### **Tekniska krav**

- **Kunskap om grundläggande formulärdesign**: Förtroende med formulärkomponenter och deras egenskaper
- **Affärslogikens välkända**: Möjlighet att definiera villkorliga krav
- **Grundläggande JavaScript-kunskap** (krävs endast för anpassade funktioner)

### **Aktivera regelredigeringstillägg**

Tillägget Regelredigeraren är inte aktiverat som standard i Universell redigerare. Du kan aktivera den från [Extension Manager](/help/implementing/developing/extending/extension-manager.md).

**Efter aktivering av tillägget:**
Ikonen ![ edit-rules ](/help/forms/assets/edit-rules-icon.svg) visas i det övre högra hörnet när du markerar formulärkomponenter.

![Regelredigeraren Universal Editor](/help/edge/docs/forms/assets/universal-editor-rule-editor.png)
*Figur: Ikonen för regelredigeraren visas när du väljer formulärkomponenter*

**Så här kommer du åt regelredigeraren:**

1. Välj en formulärkomponent i Universell redigerare.
2. Klicka på ikonen ![edit-rules](/help/forms/assets/edit-rules-icon.svg) som visas.
3. Gränssnittet för Regelredigeraren öppnas i en ny panel.

![Användargränssnittet i regelredigeraren](/help/edge/docs/forms/assets/rule-editor-for-field.png)
*Figur: Gränssnitt för regelredigeraren för redigering av komponentregler*

>[!NOTE]
>
> I hela den här artikeln hänvisar&quot;formulärkomponent&quot; och&quot;formulärobjekt&quot; till samma element (t.ex. indatafält, knappar, paneler).

## Översikt över regelredigeringsgränssnittet

Regelredigeraren har ett användarvänligt visuellt gränssnitt för att skapa och hantera regler:

![Användargränssnitt för regelredigeraren](/help/edge/docs/forms/assets/rule-editor-interface.png)
*Figur: Fullständigt gränssnitt för regelredigeraren med numrerade komponenter*

### **Gränssnittskomponenter**

**1. Komponenttitel och regeltyp**

- **Syfte**: Visar namnet på den markerade komponenten och den aktuella regeltypen.
- **Exempel**: &quot;Ange bruttolön&quot; (textinmatning) med regeln &quot;När&quot; vald.
- **Tips**: Bekräfta alltid att du redigerar rätt komponent.

**2. Formulärobjekt och funktionspanel**

- **Fliken Formulärobjekt**: Tillhandahåller en hierarkisk vy över alla formulärkomponenter.
   - Använd för: Referera till andra fält i reglerna.
   - Navigering: Expandera eller komprimera för att hitta specifika komponenter.
- **Fliken Funktioner**: Innehåller inbyggda matematiska och logiska funktioner.
   - Använd för: Utföra komplexa beräkningar och dataändringar.
   - Kategorier: Math, String, Date och Validation.

**3. Växlingsknapp för panel**

- **Syfte**: Visar eller döljer objekt- och funktionspanelen.
- **Tips**: Om du vill öka arbetsytan för regelredigering drar du av panelen.
- **Kortkommando**: Användbart när du arbetar med komplexa regler.

**4. Visual Rule Builder**

- **Syfte**: Huvudområdet för att skapa regellogik.
- **Funktioner**: Dra och släpp-gränssnitt och listrutesäljare.
- **Arbetsflöde**: Välj regeltyp → Definiera villkor → Ange åtgärder.

**5. Kontrollknappar**

- **Klar**: Sparar regeln och stänger redigeraren.
- **Avbryt**: Ignorerar ändringar och stänger redigeraren utan att spara.
- **Tips**: Testa alltid reglerna innan du klickar på Klar.

### **Regelhantering**

När du öppnar regelredigeraren för en komponent som redan har regler:

![visa tillgängliga regler för formulärobjekt](/help/edge/docs/forms/assets/rule-editor15.png)
*Figur: Hantera befintliga regler för en formulärkomponent*

**Tillgängliga åtgärder:**

- **Visa**: Granska regelsammanfattningar och logik.
- **Redigera**: Ändra befintliga regelvillkor eller åtgärder.
- **Ändra ordning**: Ändra körningsordningen för regler (reglerna körs uppifrån och ned).
- **Aktivera/inaktivera**: Aktivera eller inaktivera regler tillfälligt i testningssyfte.
- **Ta bort**: Ta bort regler permanent.

>[!TIP]
>
> **Regelkörningsordning har betydelse**: Regler körs uppifrån och ned. Placera mer specifika villkor före de allmänna.

## Tillgängliga regeltyper

Regelredigeraren innehåller en omfattande uppsättning regeltyper ordnade efter funktion. Välj lämplig typ baserat på ditt specifika användningsfall:

### **Villkorliga logikregler**

**När**

- **Syfte**: Fungerar som primär villkorsregel för implementering av komplex logik.
- **Använd fall**: Om användaren till exempel väljer &quot;Gift&quot;, visar du fält för information om make/maka.&quot;
- **Logiskt mönster**: Villkor → Åtgärd (med en alternativ åtgärd som tillval)

**Visa/Göm**

- **Syfte**: Kontrollerar fältsynlighet baserat på angivna villkor.
- **Använd skiftläge**: Dölj irrelevanta avsnitt eller aktivera progressiv visning.
- **Bästa praxis**: Används för att skapa en ren, fokuserad användarupplevelse.

**Aktivera/inaktivera**

- **Syfte**: Kontrollerar om ett fält kan interagera med, baserat på villkor.
- **Använd skiftläge**: Inaktivera skicka-knappen tills alla obligatoriska fält har slutförts.
- **Bästa praxis**: Ge användarna tydlig visuell feedback.

### **Datahanteringsregler**

**Ange värdet**

- **Syfte**: Fyller i fältvärden automatiskt.
- **Använd skiftläge**: Ange dagens datum, beräkna summor eller kopiera värden mellan fält.
- **Bästa praxis**: Används för att minska användaransträngningen och säkerställa att den är korrekt.

**Rensa värdet för**

- **Syfte**: Tar bort data från fält när villkoren ändras.
- **Använd skiftläge**: Rensa beroende fält när en överordnad markering ändras.
- **Bästa praxis**: Bevara dataintegritet och förhindra överblivna värden.

**Format**

- **Syfte**: Omvandlar hur värden visas.
- **Använd skiftläge**: Formatera valuta, telefonnummer eller datum.
- **Bästa praxis**: Förbättra läsbarheten utan att ändra underliggande data.

### **Verifieringsregler**

**Validera**

- **Syfte**: Implementerar anpassad verifieringslogik.
- **Använd skiftläge**: Använd komplexa affärsregler eller validering mellan fält.
- **Bästa praxis**: Ange tydliga och åtgärdbara felmeddelanden.

### **Beräkningsregler**

**Matematiskt uttryck**

- **Syfte**: Utför automatiserade beräkningar.
- **Använd skiftläge**: Skatteberäkningar, summor eller procentandelar.
- **Bästa praxis**: Uppdatera beräkningar i realtid när användare skriver.

### **Användargränssnittsregler**

**Ange fokus**

- **Syfte**: Riktar användarnas uppmärksamhet till specifika fält.
- **Använd fall**: Fokusera på felfält eller vägleda användarna genom guidestegen.
- **Bästa praxis**: Undvik att störa användarflödet.

**Ange egenskap**

- **Syfte**: Ändrar komponentegenskaper dynamiskt.
- **Använd skiftläge**: Ändra platshållartext eller ändra alternativ i en listruta.
- **Bästa praxis**: Förbättra användarupplevelsen med sammanhangsbaserade ändringar.

### **Formulärkontrollsregler**

**Skicka formulär**

- **Syfte**: Utlösare skickar formulär programmatiskt.
- **Använd skiftläge**: Skicka automatiskt när specifika villkor uppfylls.
- **Bästa praxis**: Verifiera alltid formuläret innan det skickas.

**Återställ formulär**

- **Syfte**: Tar bort alla formulärdata och återställer formuläret till dess ursprungliga tillstånd.
- **Använd skiftläge**: Funktionen Starta om.
- **Bästa praxis**: Bekräfta åtgärden med användaren innan du återställer.

**Spara formulär**

- **Syfte**: Sparar formuläret som ett utkast som kan fyllas i senare.
- **Använd skiftläge**: Användbart för långa formulär eller arbetsflöden med flera sessioner.
- **Bästa praxis**: Ge tydlig feedback om sparstatusen.

### **Avancerade regler**

**Anropa tjänsten**

- **Syfte**: Anropar externa API:er eller tjänster.
- **Använd skiftläge**: Adresssökning, validering i realtid eller dataanrikning.
- **Bästa praxis**: Hantera inläsningstillstånd och felscenarier korrekt.

**Lägg till/ta bort instans**

- **Syfte**: Hanterar repeterbara avsnitt dynamiskt.
- **Använd skiftläge**: Lägg till familjemedlemmar eller flera adresser.
- **Bästa praxis**: Ange tydliga kontroller för att lägga till eller ta bort instanser.

**Navigera till**

- **Syfte**: Dirigerar om användare till andra formulär eller sidor.
- **Använd skiftläge**: Arbetsflöden med flera formulär eller villkorlig routning.
- **Bästa praxis**: Bevara formulärdata före navigering.

**Navigera bland paneler**

- **Syfte**: Kontrollerar navigering i guideliknande formulär.
- **Använd skiftläge**: Flerstegsformulär eller hoppande villkorsstyrda steg.
- **Bästa praxis**: Visa tydliga förloppsindikatorer.

**Utsändningshändelse**

- **Syfte**: Utlöser anpassade händelser för avancerade integreringar.
- **Använd fall**: Analysspårning eller tredjepartsintegreringar.
- **Bästa praxis**: Använd bara för icke-blockerande åtgärder.


## Stegvis självstudiekurs: Skapa en smart skattekalkylator

Det här avsnittet innehåller ett praktiskt exempel som demonstrerar funktionerna i regelredigeraren. Exemplet vägleder dig genom att skapa ett skatteberäkningsformulär som använder villkorsstyrd logik och automatiserade beräkningar.

![Skärmbild av gränssnittet i regelredigeraren som visar hur en villkorsregel skapas med logiken När-Då för formulärfältets synlighet ](/help/edge/docs/forms/assets/rule-editor-1.png)
*Figur: Formulär för momsberäkning med intelligenta villkorsfält*

### **Översikt över självstudiekursen**

I den här självstudien skapar du ett formulär som:

1. **Anpassar till användarindata**: Visar relevanta fält baserat på inkomstnivå.
2. **Beräknar automatiskt**: Beräknar skatteskuld i realtid.
3. **Verifierar data**: Ser till att beräkningarna och datainmatningen är korrekta.

### **Formulärstruktur**

| Fältnamn | Typ | Syfte | Beteende |
|------------|------|---------|----------|
| **Bruttolön** | Nummerindata | Användaren anger årsinkomst | Villkorlig logik för utlösare |
| **Ytterligare avdrag** | Nummerindata | Extra avdrag (om tillämpligt) | Visar när lön > $50 000 |
| **Skattepliktig inkomst** | Nummerindata | Beräknas automatiskt | Uppdateringar om indataändringar |
| **Skatteskuld** | Nummerindata | Slutligt momsbelopp | Beräknar med 10 % ränta |

### **Affärslogik att implementera**

**Regel 1: Visning av villkorliga fält**

```
WHEN Gross Salary > 50,000
THEN Show "Additional Deduction" field
ELSE Hide "Additional Deduction" field
```

**Regel 2: Beräkning av skattepliktig inkomst**

```
SET Taxable Income = Gross Salary - Additional Deduction
(When Additional Deduction is applicable)
```

**Regel 3: Skatteberäkning**

```
SET Tax Payable = Taxable Income × 10%
(Simplified flat rate for demonstration)
```

### **Implementeringssteg**

Följ de här stegen för att skapa ett intelligent skatteformulär:



+++ 1: Skapa grundformuläret

**Mål**: Bygg den grundläggande formulärstrukturen med alla nödvändiga komponenter

Så här skapar du ett skatteberäkningsformulär i Universal Editor:

1. **Öppna Universal Editor**
   - Navigera till din AEM Sites-konsol
   - Markera den sida där du vill lägga till formuläret
   - Klicka på **Redigera** för att öppna den universella redigeraren

2. **Lägg till formulärkomponenter**

   Lägg till de här komponenterna i ordning:

   | Komponent | Typ | Etikett | Inställningar |
   |-----------|------|-------|----------|
   | Titel | Titel | &quot;Skatteberäkningsformulär&quot; | Rubriknivå H2 |
   | Nummerindata | Nummerindata | &quot;Bruttolön&quot; | Obligatoriskt: Ja, platshållare:&quot;Ange årslön&quot; |
   | Nummerindata | Nummerindata | &quot;Ytterligare avdrag&quot; | Obligatoriskt: Nej, platshållare:&quot;Ange ytterligare avdrag&quot; |
   | Nummerindata | Nummerindata | &quot;Skattepliktig inkomst&quot; | Obligatoriskt: Nej, skrivskyddat: Ja |
   | Nummerindata | Nummerindata | &quot;Skatteskuld&quot; | Obligatoriskt: Nej, skrivskyddat: Ja |
   | Skicka-knapp | Skicka | &quot;Beräkna skatt&quot; | Typ: Skicka |

3. **Konfigurera initiala inställningar**

   - **Dölj fältet Ytterligare avdrag**:
      - Välj komponenten &quot;Additional Deduction&quot; (Ytterligare minskning)
      - Ange **Synlig** till **Nej** i panelen Egenskaper
      - Det här fältet visas villkorligt baserat på regler

   - **Gör beräknade fält skrivskyddade**:
      - Välj fälten&quot;Skattepliktig inkomst&quot; och&quot;Skattepliktig&quot;
      - Ange **Skrivskyddad** till **Ja** i Egenskaper

     ![Skärmbild av ett momsberäkningsformulär med inmatningsfält för bruttolön, civilstånd och underordnade, som visar formulärstrukturen innan reglerna tillämpas](/help/edge/docs/forms/assets/rule-editor2.png)
     *Figur: Inledande formulärstruktur med grundläggande komponenter konfigurerade*

**Kontrollpunkt**: Nu bör du ha ett formulär med alla obligatoriska fält, där &quot;Ytterligare avdrag&quot; är dold och beräknade fält är skrivskyddade.

+++

+++ &#x200B;2. Lägg till en villkorsregel för ett formulärfält

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
1. Välj `Then` i listrutan **[!UICONTROL Show]** i programsatsen **[!UICONTROL Select Action]**.
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

+++

+++ &#x200B;3. Lägg till beräkningsregler för formulärfälten

Skriv sedan en regel för att beräkna `Taxable Income`, vilket är skillnaden mellan `Gross Salary` och `Additional Deduction` (om tillämpligt). Så här lägger du till beräkningsregel i fältet **[!UICONTROL Taxable Income]**:

1. I redigeringsläget markerar du fältet **[!UICONTROL Taxable Income]** och väljer ikonen ![edit-rules](/help/forms/assets/edit-rules-icon.svg) . Du kan också välja fältet **[!UICONTROL Taxable Income]** direkt från rutan **[!UICONTROL Forms Object]**.
1. Välj sedan **[!UICONTROL Create]** för att skapa regeln.
   ![Exempel på regelredigerare13](/help/edge/docs/forms/assets/rule-editor16.png)
1. Välj **[!UICONTROL Select Option]** och välj **[!UICONTROL Mathematical Expression]**. Ett fält som skriver matematiskt uttryck öppnas.
   ![Regelredigeraren, exempel14](/help/edge/docs/forms/assets/rule-editor17.png)

1. I fältet för matematiska uttryck:

   - Markera eller dra och släpp fältet **[!UICONTROL Gross Salary]** i det första **[!UICONTROL Drop object or select here]**-fältet på fliken Forms-objekt.

   - Välj **[!UICONTROL Minus]** i fältet **[!UICONTROL Select Operator]**.

   - Markera eller dra och släpp fältet **[!UICONTROL Additional Deduction]** i det andra **[!UICONTROL Drop object or select here]**-fältet på fliken Forms-objekt.
     ![Regelredigeraren, exempel15](/help/edge/docs/forms/assets/rule-editor18.png)

1. Välj **[!UICONTROL Done]** om du vill spara regeln.

   Lägg nu till en regel för fältet `Tax Payable `, som bestäms genom att multiplicera den beskattningsbara inkomsten med skattesatsen. För enkelhetens skull bör du anta en fast momssats på `10%`.

1. I redigeringsläget markerar du fältet **[!UICONTROL Tax Payable]** och väljer ikonen ![edit-rules](/help/forms/assets/edit-rules-icon.svg) . Välj sedan **[!UICONTROL Create]** för att skapa regler.
   ![Regelredigeraren, exempel16](/help/edge/docs/forms/assets/rule-editor19.png)
1. Välj **[!UICONTROL Select Option]** och välj **[!UICONTROL Mathematical Expression]**. Ett fält som skriver matematiskt uttryck öppnas.
   ![Regelredigeraren, exempel17](/help/edge/docs/forms/assets/rule-editor20.png)
1. I fältet för matematiska uttryck:

   - Markera eller dra och släpp fältet **[!UICONTROL Taxable Income]** i det första **[!UICONTROL Drop object or select here]**-fältet på fliken Forms-objekt.

   - Välj **[!UICONTROL Multiplied by]** i fältet **[!UICONTROL Select Operator]**.

   - Välj **Number** i fältet **[!UICONTROL Select Option]** och ange värdet som `10` i fältet **[!UICONTROL Enter a Number]**.
     ![Regelredigeraren, exempel18](/help/edge/docs/forms/assets/rule-editor21.png)
1. Välj sedan **[!UICONTROL Extend Expression]** i det markerade området runt uttrycksfältet.
   ![Regelredigeraren, exempel19](/help/edge/docs/forms/assets/rule-editor22.png)
1. I fältet för utökat uttryck väljer du **[!UICONTROL divided by]** i fältet **[!UICONTROL Select Operator]** och **[!UICONTROL Number]** i fältet **[!UICONTROL Select Option]**. Ange sedan `100` i nummerfältet.
   ![Exempel på regelredigerare20](/help/edge/docs/forms/assets/rule-editor23.png)
1. Välj **[!UICONTROL Done]** om du vill spara regeln.

+++

+++ &#x200B;4. Förhandsgranska ett formulär

När du nu förhandsgranskar formuläret och anger **bruttolön** som `60,000` visas fältet **Ytterligare avdrag** och fältet **Skattepliktig inkomst** och **Skatteskuld** beräknas därefter.

![Förhandsgranska ett formulär](/help/edge/docs/forms/assets/rule-editor-form.png)

+++

Förutom inbyggda funktioner som Sum och Average kan du skapa anpassade funktioner för att implementera komplex affärslogik som är anpassad efter dina specifika behov.

## Avancerat: Anpassade funktioner

**När anpassade funktioner ska användas:**

- För komplexa beräkningar som går utöver de inbyggda funktionerna
- Implementera affärsspecifika valideringsregler
- För dataomformningar och formatering
- Integrera med externa system eller API:er

**Fördelar:**

- **Återanvändbarhet**: Skriv funktionen en gång och använd den i flera formulär och regler
- **Underhållbarhet**: Centraliserad logik som är enkel att uppdatera
- **Prestanda**: Optimerad körning av JavaScript
- **Flexibilitet**: Möjlighet att hantera komplexa scenarier som inte hanteras av standardregler

### **Skapa anpassade funktioner**

**Filplats**: `/blocks/form/functions.js` i ditt AEM-projekt

**Arbetsflöde för utveckling:**

1. **Funktionsdeklaration**
   - Definiera tydliga och beskrivande funktionsnamn och parametrar
   - Använd namn som anger funktionens syfte
   - Dokumentparametrar och returtyper

2. **Logikimplementering**
   - Skriv ren och effektiv JavaScript-kod
   - Hantera kantfall och felscenarier
   - Följ vedertagna metoder för kodning

3. **Funktionsexport**
   - Exportera funktioner för att göra dem tillgängliga i regelredigeraren
   - Använd namngiven export för bättre organisation
   - Testa funktioner före distribution

4. **Dokumentation**
   - Lägga till JSDoc-kommentarer för funktionsdokumentation
   - Inkludera exempel
   - Ange parametertyper och returvärden

I följande exempel visas två anpassade funktioner: `getFullName` och `days`.

```JavaScript
/**
 - Get Full Name
 - @name getFullName Concats first name and last name
 - @param {string} firstname in Stringformat
 - @param {string} lastname in Stringformat
 - @return {string}
 */
function getFullName(firstname, lastname) {
  return `${firstname} ${lastname}`.trim();
}

/**
 - Calculate the number of days between two dates.
 - @param {*} endDate
 - @param {*} startDate
 - @name days Calculates the numebr of days between two dates
 - @returns {number} returns the number of days between two dates
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

Så här använder du en anpassad funktion i Regelredigeraren:

1. **Lägg till funktionen**: Lägg till den anpassade funktionen i filen `../[blocks]/form/functions.js`. Se till att du inkluderar den i programsatsen `export` i filen.
2. **Distribuera filen**: Distribuera den uppdaterade `functions.js` filen till ditt GitHub-projekt och bekräfta att bygget har slutförts.
3. **Funktionsanvändning**: I regelredigeraren i ditt formulär kan du komma åt funktionen genom att välja alternativet `Function Output` i fältet **[!UICONTROL Select Action]**.

   ![Anpassad funktion i regelredigeraren](/help/edge/docs/forms/assets/custom-function-rule-editor.png)

4. **Förhandsgranska formuläret**: Förhandsgranska formuläret för att verifiera att den nyligen implementerade funktionen fungerar som förväntat.

## Metodtips för regelutveckling

### **Prestandaoptimering**

**Minimera regelkomplexitet**

- Behåll enskilda regler enkla och fokuserade.
- Bryt komplex logik i flera mindre regler.
- Undvik djupt kapslade förhållanden när det är möjligt.

**Optimera regelkörning**

- Placera de oftast utlösta reglerna först.
- Använd särskilda villkor för att minska onödiga utvärderingar.
- Tänk på hur reglerna påverkar tiden för inläsning av formulär.

**Resurshantering**

- Begränsa antalet regler per formulärkomponent.
- Använd anpassade funktioner för upprepad logik i stället för att duplicera regler.
- Testa prestanda med realistiska datavolymer.

### **Riktlinjer för användarupplevelser**

**Ge tydlig feedback**

- Använd valideringsmeddelanden som vägleder användarna mot rätt indata.
- Visa inläsningsindikatorer för regler som omfattar externa tjänster.
- Implementera progressiv exponering för att minska kognitiv belastning.

**Behåll formulärsvarstider**

- Undvik regler som orsakar abrupta visuella ändringar.
- Implementera mjuka övergångar för visa/dölj-åtgärder.
- Testa regler på olika enheter och skärmstorlekar.

**Felhantering**

- Ange reservbeteende när reglerna misslyckas.
- Visa användarvänliga felmeddelanden.
- Logga felsökningsfel med en positiv användarupplevelse.

### **Bästa metoder för utveckling**

**Testar strategi**

- Testa regler med kantfall och gränsvärden.
- Kontrollera regelbeteendet i olika webbläsare.
- Testa formulärfunktioner både med och utan JavaScript aktiverat.

**Dokumentation**

- Dokumentera affärslogiken bakom komplexa regler.
- Underhåll regellager för stora formulär.
- Använd konsekventa namnkonventioner för komponenter och regler.

**Versionskontroll**

- Spåra ändringar i anpassade funktioner i versionskontrollen.
- Testregler i en utvecklingsmiljö före produktion.
- Underhåll säkerhetskopior av arbetsregelkonfigurationer.

## Felsökning av vanliga problem

### **Regelkörningsproblem**

**Regler utlöses inte**

- **Kontrollera komponentnamn**: Kontrollera att det finns refererade komponenter och att de har rätt namn.
- **Verifiera regelordning**: Regler körs uppifrån och ned, sortera om vid behov.
- **Verifiera villkor**: Testa villkor med kända värden för att verifiera logik.
- **Webbläsarkonsol**: Sök efter JavaScript-fel som kan blockera körning.

**Felaktigt regelbeteende**

- **Granska logikoperatorer**: Bekräfta OCH/ELLER-villkor är korrekt strukturerade.
- **Testa med exempeldata**: Använd kända värden för att isolera problem.
- **Kontrollera datatyper**: Kontrollera att numeriska jämförelser använder siffror, inte strängar.
- **Validera uttryck**: Testa matematiska uttryck separat.

### **Prestandaproblem**

**Långsam formulärrespons**

- **Minska regelkomplexiteten**: Förenkla komplex villkorslogik.
- **Optimera anpassade funktioner**: Profilera och optimera JavaScript-kod.
- **Begränsa externa anrop**: Minimera serviceanrop i regler.
- **Använd effektiva väljare**: Kontrollera att formulärobjektreferenserna är specifika.

**Minnesanvändning**

- **Rensa händelseavlyssnare**: Ta bort oanvända regelbindningar.
- **Optimera anpassade funktioner**: Undvik minnesläckor i JavaScript-kod.
- **Begränsa regelomfång**: Använd målregler i stället för globala villkor.

### **Egna funktionsproblem**

**Funktioner är inte tillgängliga**

- **Kontrollera filsökvägen**: Verifiera att `functions.js` finns på rätt plats: `/blocks/form/functions.js`.
- **Verifiera export**: Kontrollera att funktioner exporteras korrekt.
- **Skapa process**: Bekräfta att projektbygget innehåller den uppdaterade funktionsfilen.
- **Cacherensning**: Rensa webbläsarcachen efter att nya funktioner har distribuerats.

**Funktionsfel**

- **Parametervalidering**: Kontrollera att funktionsparametrarna matchar förväntade typer.
- **Felhantering**: Lägg till try-catch-block för att hantera undantag på ett bra sätt.
- **Konsolloggning**: Använd console.log för felsökningsfunktionskörning.
- **JSDoc-validering**: Kontrollera att funktionsdokumentationen matchar implementeringen.

### **Integrering med Universal Editor**

**Regelredigeraren visas inte**

- **Tillägg aktiverat**: Kontrollera att regelredigerartillägget är aktiverat.
- **Komponentval**: Kontrollera att du har valt en formulärkomponent som stöds.
- **Webbläsarkompatibilitet**: Testa i webbläsare som stöds (Chrome, Firefox, Safari).
- **Åtkomstbehörigheter**: Bekräfta att användaren har de AEM-behörigheter som krävs.

**Gränssnittsproblem**

- **Panelsynlighet**: Använd växlingsknappen för att visa eller dölja panelen för formulärobjekt.
- **Regelsparande**: Kontrollera att reglerna sparas innan du stänger redigeraren.
- **Zooma i webbläsare**: Återställ webbläsarzoomningen till 100 % för optimal gränssnittsvisning.

## Viktiga begränsningar

>[!IMPORTANT]
>
> **Anpassade funktionsbegränsningar**:
>
> - Statiska och dynamiska importer stöds inte i anpassade funktionsskript.
> - All kod måste inkluderas direkt i filen `/blocks/form/functions.js`.
> - Funktioner måste vara synkrona (inga asynkrona/väntande eller löften).
> - Åtkomsten till webbläsar-API:er är begränsad av säkerhetsskäl.

>[!WARNING]
>
> **Produktionsöverväganden**:
>
> - Testa alla regler noggrant i en staging-miljö.
> - Övervaka formulärprestanda efter att ha implementerat komplexa regler.
> - Ha en återställningsplan för regelrelaterade problem.
> - Tänk på vilken inverkan användare har med långsamma nätverksanslutningar.

## Sammanfattning

Med regelredigeraren i den universella redigeraren kan du skapa intelligenta, dynamiska formulär som ger enastående användarupplevelser. Genom att implementera villkorslogik, automatiserade beräkningar och anpassade affärsregler kan ni:

**Omforma statiskt Forms**:

- Lägg till villkorlig fältsynlighet för renare, mer fokuserade gränssnitt.
- Implementera realtidsberäkningar och datavalidering.
- Skapa sofistikerad affärslogik utan kodning.

**Förbättra användarupplevelsen**:

- Vägled användarna genom logiska formulärflöden.
- Minska antalet fel med intelligent validering.
- Ge omedelbar feedback och hjälp.

**Förbättra effektiviteten**:

- Automatisera repetitiva beräkningar och datainmatning.
- Effektivisera komplexa arbetsflöden med smart routning.
- Minska supportbördan med självbetjäning.

### **Nästa steg**

Nu när du förstår grunderna i regelredigeraren:

1. **Starta enkelt**: Börja med grundläggande regler för att visa/dölja innan du går vidare till komplexa beräkningar.
1. **Öva med exempel**: Använd självstudiekursen för beräkning av skatt som grund.
1. **Utforska avancerade funktioner**: Experimentera med anpassade funktioner för att hitta specifika behov.
1. **Testa noggrant**: Verifiera alltid regler i olika scenarier och enheter.
1. **Övervakningsprestanda**: Kontrollera att reglerna förbättrar snarare än förhindrar användarupplevelsen.

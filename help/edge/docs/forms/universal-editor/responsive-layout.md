---
title: Skapa responsiva Forms med Universal Editor
description: Lär dig hur du utformar, testar och optimerar responsiva formulär för alla enheter med Universal Editor. Lär dig mer om enhetstestning, layoutmönster och mobiloptimeringstekniker för AEM Forms med Edge Delivery Services.
keywords: responsiva formulär, mobilformulär, enhetstestning, universalredigerare, adaptiv layout, formuläroptimering, mobildesign, responsiv design, formulärlayouter, enhetsemulator
feature: Edge Delivery Services
role: User, Developer
level: Beginner
exl-id: 0c7fb491-4bad-4202-a472-87e6e6d9ab40
source-git-commit: ccfb85da187e828b5f7e8b1a8bae3f483209368d
workflow-type: tm+mt
source-wordcount: '1815'
ht-degree: 0%

---


# Skapa responsiva Forms med Universal Editor

Användarna har tillgång till formulär på en mängd olika enheter, inklusive datorer, surfplattor och smarttelefoner. Att skapa responsiva formulär ger en optimal upplevelse för alla användare, oavsett enhet. Den här guiden förklarar hur du utformar, testar och optimerar formulär för alla skärmstorlekar med den universella redigeraren.


Att skapa responsiva formulär innebär två huvudsakliga aktiviteter:

- **Responsiv testning:** Förhandsgranska och testa formulären i olika skärmstorlekar med enhetsemulatorer.
- **Responsiv design:** Välj och implementera layoutmönster som sömlöst kan anpassas till olika enheter.

**I den här guiden får du lära dig att:**

- Testa formulär på datorer, surfplattor och mobila enheter
- Välj lämpliga layoutmönster för ditt innehåll
- Tillämpa bästa praxis för responsiv design
- Felsöka vanliga problem med responsiva formulär
- Optimera formulär för mobila prestanda

## Varför responsiv Forms är viktigt

**Användarupplevelseeffekt:**

- Över 60 % av användarna har tillgång till formulär på mobila enheter
- Dåliga mobilupplevelser ger 67 % högre avhopp
- Responsiva formulär kan öka slutförandegraden med upp till 25 %

**Affärsfördelar:**

- Snabbare ifyllnad av formulär
- Bättre nöjda användare
- Bättre tillgänglighet
- Lägre utvecklings- och underhållskostnader

>[!TIP]
>
> **Mobil-först-metod:** Börja designa för mobila enheter och förbättra sedan för större skärmar. Detta garanterar att kärnfunktionerna fungerar i den mest begränsade miljön.

## Del 1: Testa Forms på olika enheter

Genom att testa formulären på olika enheter kan du identifiera och åtgärda problem som användare inte kan råka ut för. Den universella redigeraren har ett emulatorläge för att simulera olika skärmstorlekar och orienteringar.

### Hur du testar din Forms

**Steg 1: Öppna enhetsemulatorn**

1. Öppna formuläret i Universal Editor.
2. Klicka på ikonen ![Emulator](/help/edge/docs/forms/universal-editor/assets/emulator.png){height=2%,width=2%} **Emulator** i verktygsfältet.
3. Menyn för enhetsväljaren visas.

![Internationellt redigeringsgränssnitt för responsiv testning](/help/edge/docs/forms/universal-editor/assets/universal-editor-emulator.png)

**Steg 2: Välj en enhet för testning**

- **Skrivbord** (1 200 px+ bredd): Standardredigeringsvy
- **Surfplatta** (bredd 768px-1199px): Medium skärmtestning
- **Mobil** (bredd 320px-767px): Testning av liten skärm
- **Anpassad**: Ange exakta dimensioner för specifika enheter

**Steg 3: Testa enhetsorienteringar**

Använd ikonen **Skärmrotator** för att testa båda:

- **Stående läge**: Standardorientering för mobil
- **Liggande läge**: Roterad surfplatta eller telefonvy

### Resultat av enhetstestning

Varje enhetstyp visar unika responsiva beteenden:

| **Enhetstyp** | **Skärmbredd** | **Vad som ska kontrolleras** | **Vanliga problem** |
|-----------------|------------------|-------------------|-------------------|
| **Skrivbord** | 1200px+ | Fullständig layout, alla funktioner synliga | För mycket tomt utrymme, alltför breda layouter |
| **Surfplatta** | 768px-1199px | Komponentstackning, navigeringsanvändbarhet | Slagkraftiga storlekar, problem med beröringsmål |
| **Mobil** | 320px-767px | Layout med en kolumn, navigering med reglage | Liten text, knappar med nära mellanrum |
| **Egen** | Användardefinierad | Enhetsspecifika krav | Brytpunktens kantfall |

### Visuella exempel efter enhet

**Skrivbordsvy (1200px+):**
![Vyn Skrivbordsformulär](/help/edge/docs/forms/universal-editor/assets/universal-editor-desktop.png)
*Layout med full bredd med formulärfält sida vid sida.*

**Tablet-vy (768px-1199px):**
![ Formulärvy för surfplatta ](/help/edge/docs/forms/universal-editor/assets/universal-editor-tab.png)
*Medium-breddslayout med justerat komponentavstånd.*

**Mobilvy (320px-767px):**
![Vyn Mobilformulär](/help/edge/docs/forms/universal-editor/assets/universal-editor-mobile.png)
*Layout med en kolumn och staplade komponenter.*

**Vy för anpassad enhet:**
![Vyn Anpassad enhet](/help/edge/docs/forms/universal-editor/assets/universal-editor-custom.png)
*Användardefinierade dimensioner för riktad testning.*

### Testarbetsflöde

**För nya Forms:**

1. **Bygg i skrivbordsvyn:** Börja med full funktionalitet.
2. **Testa på surfplatta:** Kontrollera anpassningar för medelstora skärmar.
3. **Verifiera på mobilen:** Säkerställ användbarhet på små skärmar.
4. **Åtgärda responsiva problem:** Justera layouter efter behov.
5. **Testa alla enheter igen:** Bekräfta korrigeringar för alla storlekar.

**För befintlig Forms:**

1. **Snabbmobilkontroll:** Fungerar formuläret på telefoner?
2. **Identifiera problemområden:** Anteckningslayout och användbarhetsproblem.
3. **Systematisk testning:** Testa varje enhetsstorlek noggrant.
4. **Dokumentproblem:** Spåra vad som behöver korrigeras.
5. **Implementeringskorrigeringar:** Adressproblem metodiskt.

## Del 2: Välja responsiva layoutmönster

Layoutmönster avgör hur formulärinnehållet anpassas till olika skärmstorlekar. Det rätta mönstret förbättrar både användarupplevelsen och mobilprestandan.

### Översikt över layoutmönster

| **Layouttyp** | **Bäst för** | **Mobila prestanda** | **Komplexitet** |
|---------------------|-------------------------------------------|------------------------|----------------|
| **Panellayout** | Kategoriserat innehåll, formulär i kontrollpanelsformat | Bra | Låg |
| **Guidelayout** | Flerstegsprocesser, komplexa arbetsflöden | Underbar | Medium |
| **Dragspelslayout** | Vanliga frågor och svar, valfria avsnitt | Underbar | Låg |

### Snabbbeslutshandbok

**Använd panellayout när:**

- Ditt innehåll är indelat i olika kategorier
- Användarna måste visa flera avsnitt samtidigt
- Innehållet är relativt enkelt

**Använd guidelayout när:**

- Formuläret har flera logiska steg
- Du vill minska den kognitiva belastningen
- Mobilanvändare är den främsta målgruppen

**Använd dragspelslayout när:**

- Formuläret innehåller valfritt eller sekundärt innehåll
- Det är viktigt att bevara utrymmet
- Innehåll kan grupperas logiskt

### Panellayout

**Syfte:** Organiserar relaterat innehåll i visuellt distinkta avsnitt som kan visas samtidigt.

![Exempel på panellayout](/help/edge/docs/forms/universal-editor/assets/panel-layout.png)

**Responsivt beteende:**

- **Skrivbord (1 200 px+):** Paneler visas sida vid sida eller i ett rutnät
- **Surfplatta (768px-1199px):** Paneler staplas lodrätt med mellanrum
- **Mobil (320px-767px):** Layout med en kolumn och tydliga avsnittsbrytningar

**Implementeringssteg:**

1. Använd [panelkomponenten](https://experienceleague.adobe.com/sv/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel).
2. Gruppera relaterade fält på varje panel.
3. Lägg till tydliga rubriker för varje avsnitt.
4. Se till att det finns tillräckligt med mellanrum mellan panelerna.

**God praxis:**

- Begränsa till 3-4 paneler på datorn för att undvika överväldigande användare.
- Använd beskrivande titlar för varje panel.
- Gruppera relaterade fält logiskt för att minska kognitiv belastning.
- Testa panelnavigering på pekenheter.

**Exempel på användningsexempel:**

- **Jobbprogram:** Personlig information, Utbildning, Upplevelse, Referenser
- **Produktregistrering:** Grundläggande information, Tekniska specifikationer, Garantiinformation
- **Survey Forms:** Demographics, Preferences, Feedback, Contact

### Guidelayout

**Syfte:** Hjälper användarna att stegvis utföra komplexa processer, vilket minskar den kognitiva belastningen och förbättrar slutförandehastigheten.

![Exempel på guidelayout](/help/edge/docs/forms/universal-editor/assets/wizard-layout.png)

**Responsivt beteende:**

- **Alla enheter:** Bevarar fokus i ett enda steg för en optimal mobilupplevelse.
- **Steginnehåll:** anpassas i varje steg (stapling eller sida vid sida).
- **Navigering:** Touchvänliga knappar med tillräckligt avstånd.
- **Förloppsindikator:** Skalas för skärmstorlek.

**Implementeringssteg:**

1. Använd [guidekomponenten](https://experienceleague.adobe.com/sv/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard).
2. Dela upp komplexa formulär i logiska steg (3-7 steg är optimalt).
3. Inkludera förloppsindikatorer för användarorientering.
4. Ange tydliga navigeringskontroller (Nästa, Bakåt, Spara).

**Mobiloptimering:**

- Använd mål med stor beröring (minst 44px) för navigeringsknappar.
- Kontrollera att stegindikatorerna är tydliga och synliga på små skärmar.
- Begränsa antalet fält per steg för att minska rullningen.
- Aktivera autosparande för att förhindra dataförlust.

**God praxis:**

- Se till att det finns en logisk stegförlopp - varje steg bör bygga på det föregående.
- Använd tydliga stegrubriker så att användarna vet vad de ska förvänta sig.
- Validera indata vid varje steg för att fånga upp fel tidigt.
- Tillåt användare att navigera bakåt för att granska eller redigera information.

**Exempel på användningsexempel:**

- **Försäkringsanspråk:** Incident → Bevis → Personlig → Granska
- **Kontoinställning:** Grundläggande information → Inställningar → Säkerhet → Bekräftelse
- **Beställningsprocess:** Produkter → Leverans → Betalning → Sammanfattning

### Dragspelets layout

**Syfte:** Sparar utrymme genom att ordna innehåll i komprimerbara avsnitt, idealiskt för valfri eller sekundär information.

![Exempel på dragspelslayout](/help/edge/docs/forms/universal-editor/assets/accordion-layout.png)

**Responsivt beteende:**

- **Utmärkta mobila prestanda:** Endast relevant innehåll visas.
- **Touchoptimerade rubriker:** Det är enkelt att trycka och expandera avsnitt.
- **Utjämna animeringar:** Ge visuell feedback för interaktioner.
- **Utrymmeseffektivt:** Minimerar rullning på alla enheter.

**Implementeringssteg:**

1. Använd [dragspelskomponenten](https://experienceleague.adobe.com/sv/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion).
2. Gruppera relaterat valfritt innehåll i varje avsnitt.
3. Använd beskrivande avsnittsrubriker.
4. Ange lämpliga öppna/stängda standardlägen.

**Fördelar för mobila enheter:**

- Minskar rullningen genom att komprimera oanvända avsnitt.
- Pekvänlig interaktion med naturliga expanderings-/komprimeringsgester.
- Snabbare inläsning - endast aktivt innehåll syns.
- Bättre fokus - användarna ser bara vad de behöver.

**God praxis:**

- Använd tydliga avsnittsrubriker så att användarna vet vad som finns inuti innan de expanderar.
- Gruppera relaterat innehåll logiskt i varje avsnitt.
- Ange att viktiga avsnitt ska börja utökas vid behov.
- Förgranska korta avsnitt för att hjälpa användarna att bestämma vad de vill expandera.

**Exempel på användningsexempel:**

- **Produktkonfiguration:** Grundläggande → Avancerade → Tillbehör → Support
- **Frågor och svar Forms:** Konto → Fakturering → Teknik → Allmänt
- **Inställningar Forms:** Sekretess → Meddelanden → Utseende → Avancerat

## Del 3: Bästa praxis för responsiv design

### Bästa praxis efter enhetstyp

+++Mobiloptimering (320px-767px)

**Grundläggande praxis:**

- Använd en layout med en kolumn för allt innehåll.
- Tillhandahåll stora, pekvänliga knappar (minst 44px höjd).
- Förenkla navigeringen med alternativ för bakåt/bakåt.
- Minimera rullningen i varje avsnitt.
- Fokusera automatiskt på det första fältet för att visa tangentbordet.

**Fältspecifika riktlinjer:**

- **Textindata:** Full bredd med provutfyllnad.
- **Listrutor:** Använd inbyggda valda element för bättre pekskärmsupplevelse.
- **Datumväljare:** Använd indata för inbyggda datum för mobilkompatibilitet.
- **Filöverföringar:** Ange stora, tydliga överföringsområden.

+++

+++Tablet Optimization (768px-1199px)

**Layoutstrategier:**

- Använd layouter med två kolumner för relaterade fält.
- Testa både stående och liggande orientering.
- Stöd för interaktion med både pekskärmar och mus.
- Skapa större innehållsområden med bibehållen läsbarhet.

+++

+++Desktop Optimization (1 200 px+)

**Avancerade funktioner:**

- Använd flerspaltig layout för effektiv utrymmesanvändning.
- Erbjud kortkommandon för avancerade användare.
- Implementera hovringslägen för interaktiv feedback.
- Avancerad validering med detaljerade felmeddelanden.

+++

## Omfattande felsökning

### Layoutproblem

+++Formulärlayoutbrytningar på mobilen

**Vanliga orsaker:**

- Element med fast bredd som inte skalas
- CSS utformad för skrivbordslayouter
- Bilder eller innehåll som flödar över behållarna

**Lösningar:**

- Se till att bilder och behållare skalas till skärmstorlek.
- Använd design som sätter mobilen först med progressiv förbättring.
- Testa med både enhetsemulatorer och riktiga enheter.
- Använd flexibel storlek i stället för fasta dimensioner.

+++

+++Touch-mål för litet

**Vanliga orsaker:**

- Knappar mindre än 44px × 44px
- Interaktiva element som placerats för nära varandra
- Anpassad CSS åsidosätter pekvänliga standardinställningar

**Lösningar:**

- Se till att alla interaktiva element är minst 44px × 44px.
- Lägg till mellanrum mellan knappar och länkar.
- Testa pekinteraktionen med faktiska fingrar, inte bara med musen.
- Öka målområdena för pekskärmar för enklare knackning.

+++

+++Problem med innehållsspill

**Vanliga orsaker:**

- Lång text eller etiketter som inte radbryts
- Behållare med fast bredd
- Bilder som inte skalas korrekt

**Lösningar:**

- Aktivera figursättning för långt innehåll.
- Använd responsiva bilder som skalas korrekt.
- Implementera flexibla layouter som anpassar sig efter innehållet.
- Testa med olika innehållslängder.

+++

### Prestandaproblem

+++Långsam inläsning på mobil

**Vanliga orsaker:**

- Stora bilder som inte är optimerade för mobiler
- Överdriven exekvering av JavaScript
- För många formulärfält läses in samtidigt

**Lösningar:**

- Optimera bilder för olika skärmstorlekar.
- Läs endast in icke-kritiskt innehåll vid behov.
- Använd tekniker för att snabba upp mobilinläsningen.
- Minimera skript och widgetar från tredje part.

+++

### Testnings- och valideringsproblem

+++Emulator jämfört med verkliga enhetsskillnader

**Vanliga orsaker:**

- Webbläsarspecifika återgivningsskillnader
- Skillnader i interaktion mellan pekskärm och mus
- Variationer i nätverkshastighet

**Lösningar:**

- Testa på faktiska enheter när det är möjligt.
- Använd flera webbläsare för emulatortestning.
- Simulera olika nätverkshastigheter under testningen.
- Validera med verkliga användare i målmiljöer.

+++

## Success Metrics for Responsive Forms

+++Key Performance Indicators

**Mätvärden för användarupplevelse:**

- **Slutförandegrad för formulär:** Mål 85 %+ på mobilt
- **Tid för slutförande:** Mobilens slutförandetid måste vara inom 20 % av datorns
- **Felfrekvens:** Mindre än 5 % valideringsfel
- **Överlämningspunkter:** Identifiera var användare faller bort

**Tekniska prestanda:**

- **Sidinläsningstid:** Under 3 sekunder i 3G-nätverk
- **Core Web Vitals:** Överför alla prestandatester för Google
- **Hjälpmedelspoäng:** WCAG 2.1 AA-kompatibilitet
- **Kompatibilitet mellan olika webbläsare:** 98 %+ funktionalitet i de vanligaste webbläsarna

+++

+++Testchecklista

**Före publicering:**

- Testa formuläret på faktiska mobila enheter.
- Kontrollera att alla beröringsmål är minst 44px × 44px.
- Kontrollera textens läsbarhet i alla skärmstorlekar.
- Bekräfta att formulärvalideringen fungerar på alla enheter.
- Kontrollera att inläsningstiden är mindre än 3 sekunder på mobilen.
- Kontrollera att alla interaktiva element är tillgängliga.
- Testa att skicka formulär på alla enheter som stöds.

+++

## Nästa steg

**Omedelbara åtgärder:**

1. **Granska dina aktuella formulär:** Testa befintliga formulär med enhetsemulatorn.
2. **Identifiera snabba vinster:** Åtgärda uppenbara problem med mobilanvändning först.
3. **Prioritera formulär med mycket trafik:** Fokusera på formulär med störst användarpåverkan.
4. **Implementera en strategi som sätter mobilen först:** Börja med den minsta skärmdesignen.

**Avancerad optimering:**

- **Prestandaövervakning:** Konfigurera analyser för att spåra formulärmått.
- **A/B-testning:** Experimentera med olika layouter och metoder.
- **Samling med användarfeedback:** Samla in insikter från verkliga användare.
- **Kontinuerlig förbättring:** Granska och optimera formulär regelbundet.



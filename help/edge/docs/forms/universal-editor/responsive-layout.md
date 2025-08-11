---
title: Skapa responsiva Forms med Universal Editor
description: Lär dig hur du utformar, testar och optimerar responsiva formulär för alla enheter med Universal Editor. Lär dig mer om enhetstestning, layoutmönster och mobiloptimeringstekniker för AEM Forms med Edge Delivery Services.
keywords: responsiva formulär, mobilformulär, enhetstestning, universalredigerare, adaptiv layout, formuläroptimering, mobildesign, responsiv design, formulärlayouter, enhetsemulator
feature: Edge Delivery Services
role: User, Developer
level: Beginner
exl-id: 0c7fb491-4bad-4202-a472-87e6e6d9ab40
source-git-commit: cfff846e594b39aa38ffbd3ef80cce1a72749245
workflow-type: tm+mt
source-wordcount: '2382'
ht-degree: 0%

---


# Skapa responsiva Forms med Universal Editor

Det moderna webblandskapet kräver formulär som fungerar smidigt på ett ständigt växande spektrum av enheter och skärmstorlekar. Från stora skärmar till kompakta smarttelefoner - användarna förväntar sig enhetliga, intuitiva upplevelser oavsett vilken enhet de väljer. Det är inte längre valfritt att skapa responsiva formulär - det är ett grundläggande krav för att kunna leverera professionella, tillgängliga och konverteringsoptimerade digitala upplevelser.

Universell redigerare innehåller omfattande verktyg och metoder för att utveckla responsiva formulär som på ett intelligent sätt anpassar sig till olika skärmstorlekar, inmatningsmetoder och användarsammanhang. I den här guiden utforskas de tekniska grunderna, implementeringsstrategier och optimeringstekniker som behövs för att skapa formulär som fungerar enastående på alla enheter samtidigt som användbarhet, tillgänglighet och visuell tilltalande bevaras.

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

Panellayouten organiserar relaterat innehåll i visuellt distinkta avsnitt, så att användarna kan visa flera avsnitt samtidigt. Layouten är idealisk för formulär med kategoriserad information som utnyttjar en sida vid sida-presentation på större skärmar.

![Exempel på panellayout](/help/edge/docs/forms/universal-editor/assets/panel-layout.png)

**Responsivt beteende**

- **Skrivbord (1200px och senare):** Paneler visas sida vid sida eller i ett rutnät för maximal synlighet.
- **Surfplatta (768px-1199px):** Paneler staplas lodrätt med lämpligt mellanrum för att behålla klarheten.
- **Mobil (320px-767px):** Paneler visas i en layout med en kolumn, med tydlig separation mellan sektioner för enkel navigering.

**Så här implementerar du**

1. Lägg till [panelkomponenten](https://experienceleague.adobe.com/sv/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel) i formuläret.
2. Gruppera relaterade fält i varje panel för att upprätthålla en logisk ordning.
3. Tilldela tydliga beskrivande rubriker till varje panelavsnitt.
4. Se till att det finns tillräckligt med mellanrum mellan panelerna för att förhindra att det blir rörigt.

**God praxis**

- Begränsa antalet paneler till 3 eller 4 på datorn för att undvika överväldigande användare.
- Använd kortfattade beskrivande titlar för varje panel för att underlätta för användaren.
- Ordna fälten i panelerna logiskt för att minimera kognitiv belastning.
- Testa panelnavigeringen på pekenheter för att säkerställa användbarheten på alla plattformar.

**Vanliga användningsexempel**

- **Jobbprogram:** Avsnitt för personlig information, utbildning, upplevelse och referenser.
- **Produktregistrering:** Paneler för grundläggande information, tekniska specifikationer och garantiinformation.
- **Enkät-Forms:** Grupperingar för demografi, inställningar, feedback och kontaktinformation.

### Guidelayout

Guiden Layout guidar användarna genom en flerstegsprocess och presenterar ett avsnitt i taget. Den här layouten är särskilt effektiv för komplexa formulär eftersom den minskar kognitiv belastning och ökar slutförandehastigheten genom att processen delas upp i hanterbara steg.

![Exempel på guidelayout](/help/edge/docs/forms/universal-editor/assets/wizard-layout.png)

**Responsivt beteende**

- **Alla enheter:** Behåller fokus i ett enda steg, vilket är optimalt för mobilanvändare.
- **Steginnehåll:** Varje steg anpassas responsivt, staplar fält eller ordnar dem sida vid sida beroende på skärmstorleken.
- **Navigering:** Har pekvänliga knappar med lämpligt avstånd för enkel interaktion.
- **Förloppsindikator:** Förloppsindikatorer eller stegindikatorer skalförändras på rätt sätt för olika enheter, vilket ger tydlig feedback om slutförandestatusen.

**Så här implementerar du**

1. Infoga [Wizard Component](https://experienceleague.adobe.com/sv/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard) i formuläret.
2. Dela upp formuläret i logiska steg, helst mellan 3 och 7, så att varje steg är fokuserat och hanterbart.
3. Lägg till förloppsindikatorer som hjälper användarna att förstå sin position i processen.
4. Ange tydliga navigeringskontroller, som knapparna Nästa, Bakåt och Spara.

**Tips för mobiloptimering**

- Använd stora beröringsmål (minst 44 pixlar högt) för navigeringskontroller för att förbättra tillgängligheten.
- Kontrollera att stegindikatorerna är synliga och läsbara på små skärmar.
- Begränsa antalet fält per steg för att minimera rullningen och förbättra fokus.
- Aktivera funktionen för att spara automatiskt för att förhindra dataförlust om användarna lämnar formuläret.

**God praxis**

- Utforma steg för att följa en logisk utveckling, där varje steg bygger på det föregående.
- Använd tydliga beskrivande titlar för varje steg för att ställa in användarnas förväntningar.
- Validera användarindata vid varje steg för att fånga upp fel tidigt och minska frustrationen.
- Tillåt användare att navigera bakåt för att granska eller redigera tidigare information utan att förlora data.

**Vanliga användningsexempel**

- **Försäkringsanspråk:** Steg för incidentinformation, bevisinlämning, personlig information och granskning.
- **Kontoinställning:** Steg för grundläggande information, inställningar, säkerhetsinställningar och bekräftelse.
- **Beställningsprocess:** Steg för produktval, leveransinformation, betalningsinformation och ordersammanfattning.

### Dragspelets layout

Dragspelslayouten sparar utrymme genom att organisera innehållet i komprimerbara avsnitt, vilket gör det idealiskt för valfri eller sekundär information. Den här layouten är särskilt effektiv för formulär med innehåll som kan grupperas logiskt och som inte behöver visas alla samtidigt.

![Exempel på dragspelslayout](/help/edge/docs/forms/universal-editor/assets/accordion-layout.png)

**Responsivt beteende**

- **Mobila prestanda:** Endast det relevanta avsnittet har utökats, vilket minskar behovet av bläddring och förbättrar inläsningstiden.
- **Touchoptimerade rubriker:** Avsnittshuvuden är enkla att trycka och utöka och stöder naturliga gester på mobila enheter.
- **Utjämna animeringar:** Genom att expandera och komprimera avsnitt får du visuell feedback för användarinteraktioner.
- **Space Efficiency:** Komprimerade avsnitt minimerar det lodräta utrymmet, vilket gör det enklare att navigera i formuläret på alla enheter.

**Så här implementerar du**

1. Lägg till [dragspelskomponenten](https://experienceleague.adobe.com/sv/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion) i formuläret.
2. Gruppera relaterat valfritt eller sekundärt innehåll i varje dragspelssektion.
3. Använd tydliga, beskrivande rubriker för varje avsnitt för att hjälpa användarna förstå vilken information som finns i avsnittet.
4. Ange lämpliga standardlägen för öppna och stängda för varje avsnitt baserat på prioritet och användarbehov.

**Fördelar för mobila enheter**

- Minskar rullningen genom att komprimera oanvända avsnitt, vilket gör att användarna kan fokusera på ett avsnitt i taget.
- Pekvänlig interaktion stöder naturliga expanderings-/komprimeringsgester.
- Snabbare inläsning eftersom bara det aktiva innehållet syns.
- Ökat fokus eftersom användarna bara ser den information de behöver vid en viss tidpunkt.

**God praxis**

- Använd tydliga avsnittsrubriker så att användarna vet vad de ska förvänta sig innan de expanderar ett avsnitt.
- Gruppera relaterat innehåll logiskt i varje avsnitt för att underlätta förståelsen.
- Ange att viktiga avsnitt ska börja expanderas om omedelbar åtgärd krävs.
- Förgranska eller sammanfatta avsnitt i korthet för att hjälpa användarna att bestämma vilka avsnitt som ska expanderas.

**Vanliga användningsexempel**

- **Produktkonfiguration:** avsnitt för grundläggande alternativ, avancerade inställningar, tillbehör och support.
- **Vanliga frågor och svar Forms:** Grupperingar av frågor om konto, fakturering, teknik och allmänna frågor.
- **Inställningar för Forms:** Avsnitt för Sekretess, meddelanden, utseende och avancerade alternativ.


## Del 3: Bästa praxis för responsiv design

### Bästa praxis efter enhetstyp

+++Mobiloptimering (320px-767px)

**Layout och interaktion:**

- Använd en layout med en kolumn för allt formulärinnehåll för att maximera läsbarheten och användarvänligheten.
- Kontrollera att alla knappar och interaktiva element är minst 44px höga för tillförlitlig pekinteraktion.
- Ge tydlig och enkel navigering med synliga bakåt- och nästa knappar.
- Minimera behovet av bläddring i varje avsnitt genom att dela upp långa formulär.
- Fokusera automatiskt på det första inmatningsfältet för att fråga det mobila tangentbordet.

**Fältriktlinjer:**

- Textfält bör omfatta hela skärmens bredd med tillräcklig utfyllnad för pekrörelser.
- Använd den inbyggda listrutan/välj element för optimal mobil användning.
- Implementera inbyggda datumväljare för en enhetlig mobilupplevelse.
- Gör filöverföringsområdena stora och tydligt märkta så att de blir lätta att komma åt.

+++

+++Tablet Optimization (768px-1199px)

**Layout och användbarhet:**

- Använd layouter med två kolumner för relaterade fält för att utnyttja utökat skärmutrymme.
- Testa formulärens utseende och användbarhet i både stående och liggande orientering.
- Designa för både pek- och musindata och se till att alla kontroller är lättillgängliga.
- Öka innehållsområdets storlek samtidigt som en tydlig visuell hierarki och läsbarhet bevaras.

+++

+++Desktop Optimization (1 200 px+)

**Avancerade funktioner och layout:**

- Använd flerspaltig layout för att effektivt använda vågrätt utrymme och minska den lodräta rullningen.
- Ange kortkommandon för åtgärder som ofta utförs för att stödja avancerade användare.
- Implementera hovringslägen och visuell feedback för interaktiva element.
- Erbjud avancerad validering med tydliga, detaljerade felmeddelanden för komplexa formulär.

+++

## Felsökning

### Layoutproblem

+++Formulärlayoutbrytningar på mobilen

**Möjliga orsaker:**

- Element med fast bredd som inte anpassar sig till mindre skärmar
- CSS som är först i persondator och som åsidosätter mobilformat
- Bilder eller innehåll som flödar över behållarna

**Så här korrigerar du:**

- Se till att relativa eller procentuella storlekar används för alla bilder och behållare.
- Börja med en CSS-strategi som sätter mobilen först och skapa lager på förbättringar för större skärmar.
- Testa formulär med både enhetsemulatorer och riktiga enheter.
- Undvik fasta dimensioner, använd flexibla layouter.

+++

+++Touch-mål för litet

**Möjliga orsaker:**

- Knappar eller länkar mindre än 44px x x 44px
- Interaktiva element som placerats för nära varandra
- Anpassad CSS som reducerar standardstorlek för pekskärmsmål

**Så här korrigerar du:**

- Kontrollera att alla interaktiva element är minst 44px gånger 44px.
- Lägg till lämpligt avstånd mellan knappar, länkar och andra kontroller.
- Testa med riktiga pekenheter, inte bara en mus.
- Expandera de målområden som behövs för tillgänglighet.

+++

+++Problem med innehållsspill

**Möjliga orsaker:**

- Lång text eller etiketter som inte radbryts
- Behållare med fast bredd
- Bilder som inte skalas responsivt

**Så här korrigerar du:**

- Aktivera figursättning för alla etiketter och innehåll.
- Använd responsiva bilder som skalas med behållaren.
- Designa flexibla layouter som anpassar sig efter olika innehållslängder.
- Testa med både kort och långt innehåll för att säkerställa anpassningsbarhet.

+++

### Prestandaproblem

+++Långsam inläsning på mobil

**Möjliga orsaker:**

- Stora, ooptimerade bilder
- Tung eller överdriven JavaScript
- För många formulärfält läses in samtidigt

**Så här korrigerar du:**

- Optimera bilder för mobiler och använd rätt filformat.
- Skjut upp eller läs in icke-kritiskt innehåll.
- Minimera användningen av skript och widgetar från tredje part.
- Effektivisera formulärfälten så att de bara laddas det som behövs.

+++

### Testnings- och valideringsproblem

+++Emulator jämfört med verkliga enhetsskillnader

**Möjliga orsaker:**

- Skillnader i webbläsaråtergivningsmotorer
- Pekinteraktion simuleras inte korrekt av mus
- Felaktiga nätverkshastigheter

**Så här korrigerar du:**

- Testa alltid på riktiga enheter förutom emulatorer.
- Använd olika webbläsare och enheter för omfattande testning.
- Simulera olika nätverkshastigheter för att identifiera prestandamässiga flaskhalsar.
- Samla in feedback från verkliga användare i er målgrupp.

+++

## Success Metrics for Responsive Forms

+++Key Performance Indicators

**Användarupplevelse:**

- **Färdigställningsgrad för formulär:** Rikta dig för 85 % eller mer på mobila enheter.
- **Dags att fylla i:** Mobilanvändare bör fylla i formulär inom 20 % av tiden för slutförande av skrivbordet.
- **Felfrekvens:** Behåll valideringsfel under 5 %.
- **Överlämningspunkter:** Identifiera och åtgärda de steg där användare faller bort.

**Tekniska prestanda:**

- **Sidinläsningstid:** Mindre än 3 sekunder för en 3G-anslutning.
- **Core Web Vitals:** Uppfyll eller överträffa Google rekommenderade tröskelvärden.
- **Tillgänglighet:** Uppnå WCAG 2.1 AA-överensstämmelse.
- **Webbläsarkompatibilitet:** Kontrollera att det finns mer än 98 % funktionalitet i alla större webbläsare.

+++

+++Testchecklista

**Checklista för förpublicering:**

- Testa formuläret på faktiska mobila enheter (inte bara emulatorer).
- Kontrollera att alla beröringsmål är minst 44px × 44px.
- Kontrollera textens läsbarhet vid alla skärmstorlekar som stöds.
- Bekräfta att formulärvalideringen fungerar likadant på olika enheter och webbläsare.
- Kontrollera att mobilens inläsningstid är mindre än 3 sekunder.
- Kontrollera att alla interaktiva element är tillgängliga via tangentbordet och skärmläsare.
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



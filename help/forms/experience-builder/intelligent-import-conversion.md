---
title: Intelligent import och konvertering
description: Lär dig hur du omvandlar befintliga dokument, PDF-filer och bilder till interaktiva digitala formulär med hjälp av de intelligenta import- och konverteringsfunktionerna i Forms Experience Builder.
hide: true
index: false
hidefromtoc: true
role: Admin, Developer
exl-id: 7268c4be-1e4a-4d31-aa76-9076d7ee83ce
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '821'
ht-degree: 0%

---

# Intelligent import och konvertering

>[!NOTE]
>
> Forms Experience Builder är tillgängligt via ett program för tidig åtkomst. Kontrollera att du har begärt och beviljats åtkomst innan du börjar.

Med den intelligenta import- och konverteringsfunktionen i Forms Experience Builder kan ni omvandla befintliga dokument, PDF:er och bilder till moderna, interaktiva digitala formulär med hjälp av AI-baserad analys och konvertering.

## Källformat som stöds

### PDF dokument

**AcroForm-PDF:er:**

- Interaktiv PDF forms med formulärfält
- Statiska PDF-filer med formulärliknande layouter
- Flersidiga dokument med strukturerat innehåll

**XFA-baserade PDF-filer:**

- Äldre XFA-formulär (XML Forms Architecture)
- Komplexa affärsformulär med avancerad layout
- Blanketter för myndigheter och företag

**Statiska PDF-filer:**

- Inskannade dokument och formulär
- Utskriftsklara formulär utan interaktiva element
- Dokument med blankettliknande strukturer

### Bildfiler

**Format som stöds:**

- PNG, JPG, JPEG, GIF
- Högupplösta skanningar av pappersformulär
- Skärmbilder av digitala formulär
- Handritade skisser och trådramar

**Krav för bildkvalitet:**

- Minst 300 DPI för textigenkänning
- Rensa, läsbar text och formulärelement
- Bra kontrast mellan text och bakgrund
- Korrekt orientering (inte roterad)

### Designfiler

**Figma-designer:**

- Formulärmodeller och prototyper
- UI/UX-designfiler
- Komponentbaserade formulärlayouter

**Andra designformat:**

- Adobe XD-filer
- Sketch-design
- Trådramsdokument

## Importera och konvertera

### Steg 1: Få åtkomst till importfunktionen

1. Öppna Forms Experience Builder
2. Klicka på bilageikonen i gränssnittet
3. Välj alternativet Importera och konvertera
4. Välj källfil

### Steg 2: Ladda upp dokumentet

**För PDF-filer:**

1. Välj ett PDF-dokument
2. Vänta tills AI-filen har analyserat strukturen
3. Granska identifierade formulärelement
4. Bekräfta konverteringsinställningarna

**För bildfiler:**

1. Överför bilden (PNG, JPG osv.)
2. AI analyserar layout och text
3. Granska identifierade formulärfält
4. Justera vid behov

**För designfiler:**

1. Ladda upp designfilen
2. AI extraherar formulärkomponenter
3. Granska de konverterade elementen
4. Anpassa formulärstrukturen

### Steg 3: Granska och anpassa

Efter den första konverteringen:

1. **Granska identifierade fält**: Kontrollera att alla formulärelement identifieras korrekt
2. **Justera fälttyper**: Ändra fälttyper (text, listruta, kryssruta osv.)
3. **Lägg till validering**: Ställ in fältvalideringsregler
4. **Anpassa format**: Använd teman och profilering
5. **Testa funktioner**: Verifiera formulärbeteende och logik

## Exempel på konvertering

### PDF blankettkonvertering

**Ursprungligt PDF-formulär:**

- Statiskt kontaktformulär med namn, e-post, telefonfält
- Avsnittet Företagsinformation
- Kommentarområde

**Konverterat adaptivt formulär:**

- Interaktiva textfält med validering
- Listruta för företagsstorlek
- Flerradigt textområde för kommentarer
- Skicka-knapp med e-postintegrering

### Konvertering av bild till formulär

**Originalbild:**

- Foto på ett pappersregistreringsformulär
- Handskrivet formulär med kryssrutor
- Flera avsnitt för olika information

**Konverterat adaptivt formulär:**

- Digitala textfält som matchar layouten
- Interaktiva kryssrutor och alternativknappar
- Ordnade avsnitt med rätt avstånd
- Mobil design

### Konvertera filer

**OriginalFigma-design:**

- Modern gränssnittsdummy med formulärkomponenter
- Märkesstil och färger
- Komplex layout med flera paneler

**Konverterat adaptivt formulär:**

- Pixelperfekt återskapande av designen
- Interaktiva formulärelement
- Responsivt beteende på olika enheter
- Märkeskonsekvent formatering

## Avancerade konverteringsfunktioner

### Intelligent fältidentifiering

AI identifierar och konverterar automatiskt

- **Textfält**: Textområden med en eller flera rader
- **Markeringsfält**: Listrutor, alternativknappar, kryssrutor
- **Datumfält**: Datumväljare med korrekt formatering
- **Nummerfält**: Numeriska indata med validering
- **Filöverföringar**: Dokument- och bildöverföringsområden

### Bevara layout

Konverteringen bevarar:

- **Ursprunglig struktur**: Bevarar layout och organisation
- **Visuell hierarki**: Underhåller rubriker och avsnittsbrytningar
- **Mellanrum och justering**: Behåller korrekt formuläravstånd
- **Märkeselement**: Bevarar logotyper och formatelement

### Smart validering

Lägger automatiskt till lämplig validering:

- **E-postfält**: Validering av e-postformat
- **Telefonnummer**: Validering av telefonnummerformat
- **Obligatoriska fält**: Markerar obligatoriska fält som är uppenbara
- **Datumintervall**: Anger lämpliga datumbegränsningar

## Bästa tillvägagångssätt för import och konvertering

### Förbereder källdokument

**För PDF-filer:**

- Se till att texten är markeringsbar (inte bara bilder)
- Använd högkvalitativa skanningar för statiska PDF-filer
- Ordna innehåll i logiska avsnitt
- Inkludera rensade fältetiketter

**För bilder:**

- Använd högupplösta bilder (300+ DPI)
- Säkerställ god kontrast och läsbarhet
- Undvik roterade och skeva bilder
- Inkludera alla formulärelement i bilden

**För designfiler:**

- Använd konsekvent namngivning för formulärkomponenter
- Ordna lager logiskt
- Inkludera alla nödvändiga formulärelement
- Exportera med hög kvalitet

### Optimering efter konvertering

**Granska och testa:**

- Testa alla formulärfält och validering
- Verifiera mobilrespons
- Kontrollera tillgänglighetskraven
- Testa inskickningsfunktionen

**Anpassa och förbättra:**

- Lägg in logiska funktioner och villkorliga regler
- Implementera korrekt felhantering
- Konfigurera slutpunkter för överföring
- Använd varumärkesformat och teman

## Felsöka konverteringsproblem

### Vanliga problem

**Dålig fältidentifiering:**

- Förbättra bildkvaliteten eller få klarare PDF-text
- Justera fälttyper manuellt efter konvertering
- Använd mer beskrivande fältetiketter i källan

**Layoutproblem:**

- Justera mellanrum och justering manuellt
- Använd principer för responsiv design
- Testa olika skärmstorlekar

**Saknade element:**

- Lägg till saknade fält manuellt
- Återimportera med bättre källkvalitet
- Använd inkrementell konverteringsmetod

### Få hjälp

För konverteringsproblem:

- Kontrollera [Vanliga frågor om Forms Experience Builder](forms-experience-builder-frequently-asked-questions.md)
- Granska guiden [Komma igång](forms-experience-builder-getting-started.md)
- Kontakta systemadministratören för teknisk hjälp

## Relaterade artiklar

- [Forms Experience Builder - översikt](product-overview.md)
- [Komma igång med Forms Experience Builder](forms-experience-builder-getting-started.md)
- [Installera och konfigurera Forms Experience Builder](deploy-forms-experience-builder.md)
- [Inlämning och integration av blanketter](form-submission-integration.md)
- [Frågor och svar](forms-experience-builder-frequently-asked-questions.md)

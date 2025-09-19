---
title: AI Assistant för AEM Forms (Forms Experience Builder)
description: Skapa kraftfulla formulär snabbare med Form Fragments
feature: Edge Delivery Services
hide: true
index: false
hidefromtoc: true
role: Admin, Architect, Developer
source-git-commit: de524aeddd5f53cbd713ff0523222966752ebbc0
workflow-type: tm+mt
source-wordcount: '1145'
ht-degree: 0%

---


# Komma igång med AI Assistant för AEM Forms (Forms Experience Builder)

>[!NOTE]
>
>
> AI-assistenten för AEM Forms (Forms Experience Builder) är tillgänglig under **programmet** för tidiga användare. Om du är intresserad kan du skicka ett snabbt e-postmeddelande från din arbetsadress till mailto:aem-forms-ea@adobe.com för att begära åtkomst till funktionen.

>[!IMPORTANT]
>
> **Dokumentation som kan ändras**: Dokumentationen testas för närvarande mot produkten och kan uppdateras och revideras. Funktioner, kommandon och exempel kan ändras när AI Assistant för AEM Forms fortsätter att utvecklas under det program som man introducerar tidigt.

AI Assistant för AEM Forms förändrar hur du skapar formulär - beskriv bara vad du behöver på ditt naturliga språk och se hur formulären får liv. I Forms Management UI, Adaptive Forms Editor och Universal Editor förstår man avsikten och bygger upp precis det man söker.

## Komma igång: Tala bara med det

AI-assistenten fungerar som att ha en konversation med en kunnig kollega. I stället för att lära dig komplexa menyer och inställningar beskriver du bara vad du vill skapa.

### Snabbstart

Kom igång snabbt med vår introduktionsvideo:

>[!VIDEO](https://video.tv.adobe.com/v/3463164/)

### Åtkomst till AI-assistenten

Du kan komma åt AI-assistenten från tre olika platser i AEM Forms:

1. **Forms Management UI**
   - Navigera till: Adobe Experience Manager > Forms > Forms &amp; Documents
   - Leta efter ikonen för AI-assistenten till vänster i gränssnittet
   - Klicka på ikonen för att öppna AI-assistentpanelen

   ![Ikon för AI-assistenten*](/help/edge/docs/forms/assets/forms-manager.gif){width="50%"}

2. **Adaptiv Forms Editor**
   - Navigera till: Adobe Experience Manager > Forms > Forms &amp; Documents
   - Markera och öppna ett formulär för redigering
   - Klicka på ikonen AI-assistenten i redigeringsgränssnittet

   ![Ikon för AI-assistenten*](/help/edge/docs/forms/assets/adaptive-forms-editor.gif){width="75%"}

3. **Universell redigerare**

   - Navigera till: Adobe Experience Manager > Forms > Forms &amp; Documents
   - Leta efter ikonen för AI-assistenten till vänster i gränssnittet
   - Klicka på ikonen AI-assistenten i redigeringsgränssnittet

### Så här startar du: enkla konversationer

Det bästa sättet att börja med AI-assistenten är att använda ett naturligt språk. Så här:

**Beskriv bara vad du behöver:**

- &quot;Skapa ett kontaktformulär för min webbplats&quot;
- &quot;Jag behöver ett formulär med kundfeedback med bedömningsskalor&quot;
- &quot;Bygg ett registreringsformulär för mitt kommande event&quot;
- &quot;Gör en enkel enkät om nöjda produkter&quot;

**Lägg till information när du går:**

- &quot;Skapa ett kontaktformulär med namn, e-post, telefon och meddelandefält&quot;
- &quot;Jag behöver ett registreringsformulär i flera steg för en konferens&quot;
- &quot;Bygg ett formulär för kundfeedback med 5 stjärnor och kommentarsektioner&quot;

**Referera till befintliga fält:**

- &quot;Gör e-postfältet obligatoriskt&quot; (för @email)
- &quot;Lägg till validering i telefonnummerfältet&quot; (för @phoneNumber)
- &quot;Visa endast information om make/maka om gift har valts&quot; (för @spouseInfo och @maritalStatus)

### Vad du också kan göra

Förutom det naturliga språket erbjuder AI Assistant ytterligare sätt att interagera:

- **Överför filer**: Bifoga bilder, PDF-filer eller Figma-designer för att visa AI-filen vad du föreställer
- **Använd snabbkommandon**: Skriv `/` om du vill se tillgängliga genvägar för vanliga åtgärder
- **Referensspecifika fält**: Använd `@fieldName` för att ändra befintliga formulärfält (t.ex. `@firstName`, `@emailAddress`)

## Vad du kan skapa: Exempel på arbete

Här är några exempel på vad du kan åstadkomma med ett enkelt, naturligt språk:

### Starta ett nytt formulär

**Enkel metod:**

```
"Create a contact form"
```

**Mer detaljerad metod:**

```
"Create a professional contact form for a law firm with fields for name, email, phone, case type, and message. Make it mobile-friendly."
```

**Med designreferens:**

```
"Create a contact form based on the attached design mockup. Include all the fields shown in the layout."
```

### Lägga till formulärelement

**Grundläggande tillägg:**

```
"Add a section for personal information"
"Include a file upload for resume"
"Add a dropdown for country selection"
```

**Detaljerade specifikationer:**

```
"Add a personal information panel with fields for full name, date of birth, phone number, and email address"
"Include a secure file upload component for documents, limited to PDF files under 5MB"
"Add a country dropdown with options for USA, Canada, UK, and Germany"
```

### Skapa dynamiskt beteende

**Enkel logik:**

```
"Show additional fields when 'Other' is selected"
"Make the email field required"
"Calculate the total automatically"
```

**Komplexa affärsregler:**

```
"Show the spouse information fields only when marital status is set to 'Married'"
"Calculate the total cost by multiplying quantity and price, then add 10% tax"
"Enable the submit button only when all required fields are completed and terms are accepted"
```

### Formulärlayout och design

**Layoutändringar:**

```
"Make this a multi-step form"
"Organize fields in two columns"
"Convert to an accordion layout"
```

**Designförbättringar:**

```
"Create a wizard-style form with 3 steps: personal info, preferences, and review"
"Arrange the address fields in a compact two-column layout"
"Update the layout to match the attached wireframe"
```

### Inlämning och integrering

**Grundläggande överföring:**

```
"Send form data to our email"
"Save responses to a spreadsheet"
"Redirect to a thank you page"
```

**Avancerad integrering:**

```
"Send form submissions to hr@company.com and create a case in our CRM system"
"Submit data to our REST API endpoint and trigger the new customer workflow"
"Email responses to the sales team and add the lead to our marketing automation platform"
```

## Arbeta med bifogade filer

Ladda upp filer så att AI förstår exakt vad du söker:

### Filtyper som stöds

| Filtyp | Bäst för | Exempel |
|-----------|----------|-------------|
| **Bilder** (PNG, JPG, GIF) | Formulärlayouter, gränssnittsdummies, inskannade pappersformulär | &quot;Skapa ett formulär som matchar denna layout&quot; |
| **PDF-filer** | Befintliga formulär att konvertera, specifikationer | &quot;Konvertera detta PDF-formulär till digitalt&quot; |
| **Figma-filer** | Designprototyper, varumärkesriktlinjer | &quot;Bygg detta formulär från min Figma-design&quot; |
| **Designfiler** | Visuella referenser, stilguider | &quot;Matcha formateringen i denna design&quot; |

### Använda bifogade filer

1. **Klicka på bilageikonen** i AI Assistant-gränssnittet
2. **Välj din fil** på din enhet
3. **Beskriv vad du vill att** refererar till den bifogade filen:
   - &quot;Skapa ett formulär baserat på denna bifogade PDF&quot;
   - &quot;Skapa ett kontaktformulär som matchar layouten i den här bilden&quot;
   - &quot;Konvertera det här pappersformuläret till en digital version&quot;

### Bästa praxis med bifogade filer

- **Använd tydliga, högkvalitativa bilder** för bättre AI-analys
- **Fokusera på ett koncept per bilaga** (layout, format osv.)
- **Beskriv vad du vill** tillsammans med den bifogade filen
- **Behåll filer under 10 MB** för optimal bearbetning

## Tips för bästa resultat

### Starta enkelt, skapa

- Börja med grundläggande begäranden:&quot;Skapa ett kontaktformulär&quot;
- Lägg till information gradvis:&quot;Lägg till validering i e-postfältet&quot;
- Testa och förfina:&quot;Gör telefonfältet valfritt&quot;

### Var specifik vid behov

- Istället för: &quot;Make it look good&quot;
- Prova:&quot;Använd professionella färger och ren typografi&quot;

### Använd naturligt språk

- I stället för:&quot;Lägg till textinmatningskomponent&quot;
- Prova:&quot;Lägg till ett fält för förnamn&quot;

### Referera till befintliga element

- Använd `@fieldName` för befintliga fält: &quot;Make @email required&quot;
- Var specifik angående fältnamn: &quot;Uppdatera fältet @phoneNumber&quot;

### Avbryta komplexa begäranden

- Försök med flera mindre i stället för en enda stor begäran
- Bygg formulär steg för steg
- Testa varje ändring innan du går vidare till nästa

## Produkthjälp och -inlärning

AI Assistant kan även lära dig mer om AEM Forms funktioner:

### Ställ frågor som:

- &quot;Hur skapar jag ett flerstegsformulär?&quot;
- &quot;Vad är skillnaden mellan paneler och avsnitt?&quot;
- &quot;Hur konfigurerar jag e-postmeddelanden?&quot;
- &quot;Vilka är de bästa sätten för mobilvänliga formulär?&quot;
- &quot;Hur använder jag teman i mina formulär?&quot;

### Få hjälp om:

- AEM Forms koncept och terminologi
- Stegvisa instruktioner för komplexa funktioner
- God praxis och rekommendationer
- Felsöka vanliga problem

## Referens för avancerade funktioner

För användare som vill utforska avancerade funktioner:

### Snabbkommandon

Skriv `/` om du vill visa tillgängliga kortkommandon:

| Kommando | Syfte | Exempel |
|---------|---------|---------|
| `/create-form` | Starta ett nytt formulär | `/create-form customer survey` |
| `/add-form` | Lägg till formulär i Universal Editor | `/add-form contact form` |
| `/update-layout` | Ändra formulärstruktur | `/update-layout wizard with 3 steps` |
| `/update-field` | Ändra fältegenskaper | `/update-field @email to be required` |
| `/create-rule` | Lägg till dynamiskt beteende | `/create-rule show @spouse if married` |
| `/create-panel` | Lägg till fältbehållare | `/create-panel Personal Information` |
| `/configure-submit` | Ställ in formulärinlämning | `/configure-submit to email support` |
| `/help` | Få hjälp | `/help multi-step forms` |

### Fältreferenssyntax

Använd `@fieldName` för att referera till befintliga fält:

- `@firstName` - fältet för förnamn
- `@email` - E-postfält
- `@phoneNumber` - Telefonnummerfält
- `@dateOfBirth` - Födelsedatum

### Komponenttyper

Använd dessa termer för bästa resultat:

- `text input` - Textfält med en rad
- `text area` - Flerradigt textfält
- `dropdown` - Välj lista
- `checkbox` - En kryssruta
- `checkbox group` - flera kryssrutor
- `radio group` - Grupp med alternativknappar
- `date picker` - datumval
- `file upload` - Bifogad fil
- `panel` - Behållare för grupperingsfält

## Felsökning

### Vanliga problem och lösningar

**AI-assistenten svarar inte:**

- Kontrollera din internetanslutning
- Kontrollera att du är i en miljö som stöds
- Stäng och öppna AI-assistentpanelen igen

**Oväntade resultat:**

- Försök att formulera om din förfrågan mer specifikt
- Dela upp komplexa förfrågningar i mindre steg
- Använd AEM Forms standardterminologi

**Fältreferenser fungerar inte:**

- Kontrollera fältnamn exakt som de visas
- Använd syntaxen `@fieldName` för befintliga fält
- Kontrollera att fältet finns innan du refererar till det

**Problem med designimport:**

- Kontrollera att filerna är tydliga och välstrukturerade
- Använd format som stöds (PDF, PNG, JPG, Figma)
- Kontrollera att filstorleken är mindre än 10 MB

## Feedback och support

Hjälp oss att förbättra AI-assistenten:

- **Ge feedback**: Använd feedbackknappen i AI Assistant-gränssnittet
- **Rapportera problem**: Kontakta Adobe support via officiella kanaler
- **Dela upplevelser**: Dina indata gör assistenten bättre för alla

## Relaterade resurser

[AEM Forms AI Assistant - promptbibliotek](help/forms/experience-builder/forms-experience-builder-prompt-examples-library.md)

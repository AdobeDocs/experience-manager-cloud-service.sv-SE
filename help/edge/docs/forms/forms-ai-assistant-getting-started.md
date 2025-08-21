---
title: Komma igång med Forms Experience Builder
description: Lär dig använda Forms Experience Builder för att skapa och hantera formulär med progressiv publicering för alla användartyper
feature: Edge Delivery Services
hide: true
index: false
hidefromtoc: true
role: Admin, Architect, Developer
exl-id: b8f64082-a23f-4919-ad66-042faad77d30
source-git-commit: 750674bbd29ec1b29388579d77c7c15bd89335ab
workflow-type: tm+mt
source-wordcount: '1720'
ht-degree: 0%

---


# Komma igång med Forms Experience Builder

>[!NOTE]
>
> Funktionen Forms Experience Builder är tillgänglig under **programmet** för tidig användning. Om du är intresserad kan du skicka ett snabbt e-postmeddelande från din arbetsadress till `aem-forms-ea@adobe.com` för att begära åtkomst till funktionen.

>[!IMPORTANT]
>
> **Dokumentation som kan ändras**: Dokumentationen testas för närvarande mot produkten och kan uppdateras och revideras. Funktioner, kommandon och exempel kan ändras allt eftersom Forms Experience Builder fortsätter att utvecklas under det program som antogs tidigt.

Den här omfattande guiden hjälper dig att komma igång med att skapa och hantera formulär med hjälp av konverteringsbaserad AI-teknik. Oavsett om du är nybörjare som vill skapa ditt första formulär eller en avancerad användare som vill utnyttja avancerade funktioner hittar du detaljerad information och praktiska exempel som vägleder dig genom funktionerna i Forms Experience Builder.

## Krav och inställningar

### &#x200B;1. Begär åtkomst

Om du inte har tillgång till Forms Experience Builder:

1. **Begär åtkomst**: Skicka ett e-postmeddelande till [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) från ditt e-postmeddelande
2. **Inkludera information**: Organisationsnamn och projektinformation
3. **Vänta på godkännande**: Adobe granskar och tillhandahåller instruktioner för introduktion

### &#x200B;2. Kontrollera att Forms är aktiverat

Kontrollera att [AEM Forms är aktiverat för din miljö](/help/forms/setup-forms-cloud-service.md) innan du använder Forms Experience Builder.


### &#x200B;3. Konfigurera miljön


* **För Edge Delivery Services (EDS):**

   * [Installationsmiljö för Edge Delivery Services Forms](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md)
   * [Skapa ett nytt formulär med Edge Delivery Forms-mallen](/help/edge/docs/forms/universal-editor/create-forms.md)

* **För kärnkomponentbaserade formulär:**

   * På din Adobe Experience Manager-instans besöker du Forms > Forms &amp; Documents
   * [Skapa en ny sida med hjälp av mallen för kärnkomponenter](/help/forms/creating-adaptive-form-core-components.md)

## Snabbstart

### Få tillgång till Forms Experience Builder

**Universell redigerare**

* Öppna din EDS-sida i Universal Editor
* Leta efter ikonen Forms Experience Builder i den vänstra panelen
* Klicka för att öppna konversationsgränssnittet

**Adaptiv Forms Editor**

* Navigera till: AEM > Forms > Forms &amp; Documents
* Skapa eller öppna en grundkomponentbaserad blankett för redigering
* Klicka på ikonen Forms Experience Builder i redigeringsverktygsfältet

### Ditt första formulär

Prova den här enkla konversationen för att komma igång:

```
👤 You: "Create a simple contact form"
🤖 AI: "I'll create a contact form with name, email, and message fields for you."

👤 You: "Make the email field required"
🤖 AI: "Updated the email field to be required with validation."
```

### Essential Commands

| Symbol | Syfte | Använda |
|--------|---------|------------|
| `/` | Snabbåtgärder och genvägar | Typ `/create` för att skapa formulär, `/help` för hjälp |
| `@` | Referera till befintliga formulärfält | Skriv `@fieldName` om du vill ändra specifika fält (t.ex. `@email`) |
| Oformaterad text | Naturlig konversation | Beskriv vad du vill:&quot;Lägg till ett obligatoriskt telefonnummerfält&quot; |

### Tips för framgång

* **Var specifik**: Det fungerar bättre att lägga till ett obligatoriskt e-postfält med validering än att lägga till e-post
* **Referera till befintliga fält**: Använd `@fieldName` när du ändrar formulär
* **Be om hjälp**: Skriv `/help` följt av din fråga
* **Upprepa**: Gör en ändring i taget för bästa resultat

## Kärnfunktioner

### Två sätt att skapa Forms

#### &#x200B;1. Skapa från grunden

Beskriv dina formulärkrav på ett naturligt språk så genererar Forms Experience Builder den fullständiga formulärstrukturen:

**Exempel:**

* &quot;Skapa ett låneansökningsformulär med personlig information, ekonomisk information och dokumentöverföringar&quot;
* &quot;Bygg ett formulär för kundfeedback med betyg, kommentarer och produktkategorier&quot;
* &quot;Jag behöver ett registreringsformulär i flera steg för en konferens med betalningshantering&quot;

#### &#x200B;2. Importera och konvertera

Omvandla befintliga blanketter och dokument till moderna, interaktiva upplevelser:

**Källor som stöds:**

* **PDF forms**: Överför statiska PDF-filer → Interaktiva digitala formulär med validering
* **Skärmbilder/bilder**: Foto av pappersformulär → Funktionella digitala versioner
* **HTML Forms**: Grundläggande webbformulär → Förbättrad AEM Forms med avancerade funktioner
* **XFA Forms**: Äldre Adobe-formulär → Moderna responsiva formulär
* **URL:er**: Befintliga webbformulär → Inbyggda AEM Forms med förbättrat användargränssnitt

**Så här importerar du:**

1. Klicka på bilageikonen i Forms Experience Builder-gränssnittet
2. Ladda upp filen (PDF, bild, Figma-design osv.)
3. Beskriv era krav:
   * &quot;Konvertera detta PDF-formulär till en digital version&quot;
   * &quot;Skapa ett formulär som matchar skärmbildslayouten&quot;
   * &quot;Bygg detta formulär från min Figma-design&quot;

**Filtyper som stöds:**

* **Bilder** (PNG, JPG, GIF): Formulärlayouter, gränssnittsdummies, skannade formulär
* **PDF-filer**: Befintliga formulär, specifikationer, dokument
* **Figma-filer**: Designprototyper, riktlinjer för varumärken
* **Designfiler**: Visuella referenser, formatguider

### Viktiga interaktioner

#### Lägga till formulärelement

**Grundläggande tillägg:**

```
👤 You: "Add a section for personal information"
🤖 AI: "Added a personal information panel with standard fields"

👤 You: "Include a file upload for resume"
🤖 AI: "Added a secure file upload component for documents"

👤 You: "Add a dropdown for country selection"
🤖 AI: "Added a country dropdown with common options"
```

**Detaljerade specifikationer:**

```
👤 You: "Add a personal information panel with fields for full name, date of birth, phone number, and email address"
🤖 AI: "Created a personal information panel with all requested fields and appropriate validation"

👤 You: "Include a secure file upload component for documents, limited to PDF files under 5MB"
🤖 AI: "Added a file upload field with PDF restriction and 5MB size limit"

👤 You: "Add a country dropdown with options for USA, Canada, UK, and Germany"
🤖 AI: "Added a country dropdown with the specified options"
```

#### Skapa dynamiskt beteende

**Enkel logik:**

```
👤 You: "Show additional fields when 'Other' is selected"
🤖 AI: "Created a conditional rule that shows additional fields when 'Other' is chosen"

👤 You: "Make the email field required"
🤖 AI: "Updated the email field to be required with validation"

👤 You: "Calculate the total automatically"
🤖 AI: "Added calculation logic to automatically compute totals"
```

**Komplexa affärsregler:**

```
👤 You: "Show the spouse information fields only when marital status is set to 'Married'"
🤖 AI: "Created a conditional rule that displays spouse fields based on marital status"

👤 You: "Calculate the total cost by multiplying quantity and price, then add 10% tax"
🤖 AI: "Added calculation logic with quantity, price, and tax computation"

👤 You: "Enable the submit button only when all required fields are completed and terms are accepted"
🤖 AI: "Created validation logic that enables submission only when all conditions are met"
```

#### Formulärlayout och design

**Layoutändringar:**

```
👤 You: "Make this a multi-step form"
🤖 AI: "Converted the form to a progressive layout with navigation"

👤 You: "Organize fields in two columns"
🤖 AI: "Updated the layout to display fields in a two-column arrangement"

👤 You: "Convert to an accordion layout"
🤖 AI: "Transformed the form to use accordion-style sections"
```

**Designförbättringar:**

```
👤 You: "Create a wizard-style form with 3 steps: personal info, preferences, and review"
🤖 AI: "Created a wizard form with three distinct steps and navigation"

👤 You: "Arrange the address fields in a compact two-column layout"
🤖 AI: "Organized address fields in a compact two-column format"

👤 You: "Update the layout to match the attached wireframe"
🤖 AI: "Modified the layout to match the provided design reference"
```

### Integrationsinställningar

Forms Experience Builder kan konfigurera olika slutpunkter för att koppla formulären till externa system och tjänster:

| Integrationstyp | Installationskommando | Användningsfall |
|------------------|---------------|----------|
| **E-post** | &quot;Skicka formulär till e-post&quot; | Anmälningar och bekräftelser för inskickande av formulär |
| **REST API** | &quot;Skicka till REST-slutpunkt&quot; | Anpassade program och tredjepartssystem |
| **Molnlagring** | &quot;Spara till Azure/SharePoint&quot; | Dokumentlagring och filhantering |
| **Arbetsflöde** | &quot;Anslut till Power Automate&quot; | Automatisering och godkännande av affärsprocesser |
| **Marknadsföring** | Integrera med Marketo | Leadhantering och automatiserad marknadsföring |

**Exempel på avancerad integrering:**

```
👤 You: "Send form submissions to hr@company.com and create a case in our CRM system"
🤖 AI: "Configured email submission and CRM integration"

👤 You: "Submit data to our REST API endpoint and trigger the new customer workflow"
🤖 AI: "Set up REST API submission with workflow triggers"

👤 You: "Email responses to the sales team and add the lead to our marketing automation platform"
🤖 AI: "Configured multi-channel submission with email and marketing automation"
```





## Avancerade formuläråtgärder


### Skapa komplexa regler

Skapa sofistikerad validering och affärslogik som svarar på användarinteraktioner och säkerställer dataintegritet:

```
👤 You: "Show the address section only if the user selects 'Ship to different address'"
🤖 AI: "Created a conditional rule that shows/hides the address panel based on checkbox selection"
```

### Skapa formulär i flera steg

```
👤 You: "Create a progressive form with 3 steps: personal info, preferences, confirmation"
🤖 AI: "Created a progressive form with navigation between steps and validation at each stage"
```

### Avancerade fälttyper

* Filöverföring med validering och storleksbegränsningar för dokumenthantering
* Datumväljare med begränsningar och affärsregler för schemaläggning
* Listrutor med dynamiska alternativ som ändras baserat på användarval
* Alternativknappar med villkorlig logik för komplexa beslutsträd


### Konvertering av PDF till formulär

```
👤 You: "Convert this PDF into an interactive form"
🤖 AI: "Analyzed the PDF and created a form with appropriate field types and validation"
```

### URL till formulärkonvertering

```
👤 You: "Create a form from this website"
🤖 AI: "Extracted form elements and created a native AEM Form with enhanced functionality"
```

### Resultatanalys

```
👤 You: "Analyze this form's conversion performance"
🤖 AI: "Provided insights on form effectiveness and suggested optimizations"
```

### Avancerad anpassning

#### Anpassade verifieringsregler

* Fältberoenden som skapar dynamiskt formulärbeteende baserat på användarindata
* Komplex, villkorlig logik som anpassar formulärupplevelsen efter användarens behov
* Anpassade felmeddelanden som ger tydlig vägledning för användarna
* Fältövergripande validering som säkerställer att data är konsekventa över flera indata

#### Optimering av layout

* Snabbhet som gör att formulären fungerar smidigt på alla enheter
* Tillgänglighet som gör att formulär kan användas av personer med funktionshinder
* Förbättrad visuell design som förbättrar användarengagemanget och slutförandefrekvensen
* Förbättrade användarupplevelser som minskar friktionen och ger nöjdare användare

#### Integreringsarbetsflöden

* Godkännandeprocesser i flera steg som dirigerar formulärinlämning via affärsarbetsflöden
* Dataomvandling som konverterar formulärdata till format som krävs av externa system
* Anpassad affärslogik som tillämpar specifika regler och beräkningar på formulärinskickat material
* Avancerad felhantering som ger smidig återställning efter systemproblem

## Kommandoreferens

### Essential Commands

| Symbol | Syfte | Använda |
|--------|---------|------------|
| `/` | Snabbåtgärder och genvägar | Typ `/create` för att skapa formulär, `/help` för hjälp |
| `@` | Referera till befintliga formulärfält | Skriv `@fieldName` om du vill ändra specifika fält (t.ex. `@email`) |
| Oformaterad text | Naturlig konversation | Beskriv vad du vill:&quot;Lägg till ett obligatoriskt telefonnummerfält&quot; |

### Snedstreckskommandon

| Kommando | Kontext | Exempel på användning |
|---------|---------|---------------|
| `/create-form` | Alla miljöer | `/create-form customer survey` |
| `/add-form` | Universal Editor | `/add-form contact form` |
| `/update-layout` | Formulärredigeraren | `/update-layout wizard with 3 steps` |
| `/update-field` | Formulärredigeraren | `/update-field @email to be required` |
| `/create-rule` | Formulärredigeraren | `/create-rule show @spouse if married` |
| `/create-panel` | Formulärredigeraren | `/create-panel Personal Information` |
| `/configure-submit` | Formulärredigeraren | `/configure-submit to email support` |
| `/help` | Alla miljöer | `/help multi-step forms` |

### Fältreferenser

Använd `@fieldName` för att referera till befintliga fält:

* `@firstName`, `@lastName` * Namnfält
* `@email`, `@phoneNumber` * Kontaktfält
* `@address`, `@city`, `@zipCode` * Adressfält
* `@dateOfBirth`, `@startDate` * Datumfält

### Komponenttyper

Använd dessa termer när du beskriver formulärelement:

* `text input` * Textfält med en rad
* `text area` * Flerradigt textfält
* `dropdown` * Välj en lista med alternativ
* `checkbox` * En kryssruta
* `checkbox group` * Flera kryssrutor
* `radio group` * Grupp med alternativknappar
* `date picker` * Datummarkeringsfält
* `file upload` * Fält för bifogad fil
* `panel` * Behållare för grupperingsfält

### Integreringskommandon

| Tjänst | Naturligt språk, kommando | Krav |
|---------|--------------------------|--------------|
| E-post | &quot;Skicka inskickade bidrag till [e-post]&quot; | Giltig e-postadress |
| REST API | &quot;Skicka till REST-slutpunkt [URL]&quot; | API-slutpunkt och autentiseringsuppgifter |
| Azure Storage | &quot;Spara filer till Azure-lagring&quot; | Konfiguration av lagringskonto |
| SharePoint | &quot;Lagra på SharePoint [webbplats]&quot; | Åtkomst till SharePoint webbplats |
| Power Automate | &quot;Utlös strömautomatiseringsflöde&quot; | Flödeskonfiguration |
| Marketo | &quot;Lägg till leads till Marketo&quot; | Marketo API-autentiseringsuppgifter |

### Tips

1. **Använd naturligt språk**: AI hanterar komplexa begäranden och kan tolka detaljerade krav
2. **Var specifik**: Detaljerade beskrivningar ger bättre resultat och exaktare formulärgenerering
3. **Iterera**: Förfina formulär genom konversation för att få en perfekt användarupplevelse
4. **Utnyttja kontext**: Referera befintliga formulärelement för att bygga vidare på det du redan har
5. **Testa noggrant**: Verifiera alla användarscenarier för att säkerställa att formulären fungerar som förväntat

## Produkthjälp och -inlärning

Forms Experience Builder kan även lära dig mer om AEM Forms funktioner:

### Ställ frågor som:

* &quot;Hur skapar jag ett flerstegsformulär?&quot;
* &quot;Vad är skillnaden mellan paneler och avsnitt?&quot;
* &quot;Hur konfigurerar jag e-postmeddelanden?&quot;
* &quot;Vilka är de bästa sätten för mobilvänliga formulär?&quot;
* &quot;Hur använder jag teman i mina formulär?&quot;

### Få hjälp om:

* AEM Forms koncept och terminologi
* Stegvisa instruktioner för komplexa funktioner
* God praxis och rekommendationer
* Felsöka vanliga problem

## Bästa praxis

### Formulärdesign

* **Gör det enkelt**: Börja med viktiga fält och lägg till komplexitet endast när det behövs för att undvika överväldigande användare
* **Använd tydliga etiketter**: Gör fältens syften uppenbara med beskrivande etiketter som vägleder användarna genom formuläret
* **Ange hjälptext**: vägleda användare genom komplexa fält med sammanhangsbaserad hjälp och exempel
* **Testa noggrant**: Verifiera alla användarsökvägar för att säkerställa att formulären fungerar korrekt i alla scenarier

### Användarupplevelse

* **Progressiv visning**: Visa relevanta fält baserat på kontext för att minska kognitiv inläsning och förbättra slutförandefrekvensen
* **Rensa navigering**: Hjälp användarna förstå var de befinner sig i formuläret och vilka steg som återstår
* **Responsiv design**: Säkerställ att formulär fungerar på alla enheter och skärmstorlekar för maximal tillgänglighet
* **Hjälpmedel**: Följ riktlinjerna från WCAG för att göra formulär användbara för personer med funktionshinder

### Prestanda

* **Optimera fältantal**: Be bara om nödvändig information för att minska antalet formuläravbrott och förbättra antalet slutförda formulär
* **Använd lämplig validering**: Förebygg fel före överföring för att ge omedelbar feedback och vägledning
* **Testa slutförandegrad**: Övervaka och förbättra formulärets effektivitet med hjälp av analyser och feedback från användare
* **Regelbundna uppdateringar**: Håll formulären aktuella med affärsbehov och användarförväntningar för optimala prestanda

### Varumärkesöverensstämmelse

* **Skapa varumärkesmallar**: Förbered profilerade formulärmallar med organisationens färger, teckensnitt och format innan du börjar skapa formulär
* **Definiera formatstandarder**: Upprätta konsekventa knappformat, fältlayouter och riktlinjer för mellanrum som kan refereras i uppmaningar
* **Använd varumärkesresurser**: Förbered logotyper, färgkoder och riktlinjer för varumärken så att det blir enkelt att skapa formulär
* **Mallbibliotek**: Skapa en samling profilerade formulärmallar för vanliga användningsområden (kontakt, registrering, feedback)
* **Formatuppmaningar**: Inkludera varumärkesspecifika instruktioner:&quot;Använd företagsblå (#1234AB) för knappar och företagsteckensnittet Helvetica&quot;

### Tips för bästa resultat

**Starta enkelt, skapa**

* Börja med grundläggande begäranden:&quot;Skapa ett kontaktformulär&quot;
* Lägg till information gradvis:&quot;Lägg till validering i e-postfältet&quot;
* Testa och förfina:&quot;Gör telefonfältet valfritt&quot;

**Var specifik vid behov**

* Istället för: &quot;Make it look good&quot;
* Prova:&quot;Använd professionella färger och ren typografi&quot;

**Använd naturligt språk**

* I stället för:&quot;Lägg till textinmatningskomponent&quot;
* Prova:&quot;Lägg till ett fält för förnamn&quot;

**Referera till befintliga element**

* Använd `@fieldName` för befintliga fält: &quot;Make @email required&quot;
* Var specifik angående fältnamn: &quot;Uppdatera fältet @phoneNumber&quot;

**Avbryta komplexa begäranden**

* Försök med flera mindre i stället för en enda stor begäran
* Bygg formulär steg för steg
* Testa varje ändring innan du går vidare till nästa

## Felsökning

| Problem | Snabbkorrigering |
|-------|-----------|
| **Gränssnittet läses inte in** | Uppdatera webbläsare, kontrollera Internetanslutning |
| **Kommandon fungerar inte** | Prova `/help` eller använd ett naturligt språk istället |
| **@fieldName känns inte igen** | Kontrollera stavning, kontrollera att fältet finns först |
| **Filöverföringen misslyckas** | Använd PDF/JPG/PNG under 10 MB |
| **Formuläret ser fel ut** | Var mer specifik:&quot;Gör det mobilvänligt&quot; |
| **Integreringen misslyckas** | Verifiera API-autentiseringsuppgifter och behörigheter |

**Behöver du fortfarande hjälp?** Skriv `/help` följt av din specifika fråga eller kontakta systemadministratören.

Mer support finns i [Forms Experience Builder Prompt Library](ai-assistant-prompt-library.md) eller så kontaktar du systemadministratören för teknisk hjälp.

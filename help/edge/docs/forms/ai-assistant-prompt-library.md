---
title: AEM Forms AI Assistant - promptbibliotek
description: Samling av beprövade promptmönster och exempel för att skapa formulär med hjälp av AI i Forms Management-gränssnittet, Adaptive Forms Editor och Universal Editor.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
role: Admin, Architect, Developer
source-git-commit: d3ade6ee9216b44b55d6808d8acffe83f1e263c9
workflow-type: tm+mt
source-wordcount: '1613'
ht-degree: 0%

---



# AEM Forms AI Assistant - promptbibliotek

Samling av återanvändbara promptmönster och exempel för vanliga formulärgenereringsscenarier. Tänk på dessa som mallar som du kan anpassa efter dina specifika behov. Varje avsnitt behandlar ett visst användningsfall med vägledning om när det ska användas och beprövade exempel.

>[!NOTE]
>
> AI Assistant för AEM Forms kan köpas genom ett program som tagits i bruk för tidigt. Skicka ett e-postmeddelande från din arbetsadress till mailto:aem-forms-ea@adobe.com för att begära åtkomst.

>[!IMPORTANT]
>
> **Dokumentation som kan ändras**: Det här snabbbiblioteket testas för närvarande mot produkten och kan komma att uppdateras och revideras. Frågar, exempel och bästa praxis kan ändras i takt med att AI Assistant för AEM Forms utvecklas under det program där man introducerar programmet.

## Bästa praxis för optimala resultat

För att få ut så mycket som möjligt av AI-assistenten bör du tänka på följande:

### Starta enkelt, bygg stegvis

Börja med mindre, specifika kommandon (t.ex.&quot;Lägg till textinmatning för&quot;Förnamn&quot;&quot;) i stället för alltför komplexa flerstegsbegäranden från början. Det här arbetssättet gör det enklare att felsöka om något inte fungerar som det ska.

**Exempel på enkel start:**

```
Add a text input field for "First Name" with placeholder "Enter your first name"
```

**Bygg sedan stegvis:**

```
Make @firstName mandatory and add validation message "First name is mandatory"
```

### Använd AEM Forms terminologi

Använd termer som &quot;panel&quot;, &quot;textinmatningsfält&quot;, &quot;kryssrutegrupp&quot;, &quot;skicka-åtgärd&quot;, &quot;regel&quot; osv. för att få bättre förståelse av assistenten. Detta garanterar att AI tolkar dina förfrågningar korrekt i AEM Forms-sammanhang.

**Standardtermer:**

- textinmatningsfält i stället för textruta
- &quot;kryssrutegrupp&quot; i stället för &quot;kryssrutor&quot;
- &quot;dropdown&quot; i stället för &quot;select list&quot;
- &quot;panel&quot; i stället för &quot;section&quot; eller &quot;container&quot;
- &quot;skicka åtgärd&quot; i stället för &quot;skicka formulär&quot;
- &quot;rule&quot; i stället för &quot;logic&quot; eller &quot;condition&quot;

### Referensfält tydligt

När du konfigurerar befintliga fält ska du använda @fieldName-notationen (t.ex. &quot;Make @firstName mandatory&quot;). Detta hjälper AI att identifiera exakt vilket fält du refererar till, särskilt i komplexa formulär med många fält.

**Exempel:**

- `Make @email mandatory with real-time validation`
- `Show @spouseInfo panel when @maritalStatus equals "Married"`
- `Set @country default value to "United States"`

### Granska alltid planer

Granska alltid planer noggrant för ändringar som föreslås av assistenten i den universella redigeraren innan du klickar på &quot;Använd&quot;. AI visar vad man tänker göra - ägna en stund åt att kontrollera att det matchar dina förväntningar.

### Validera manuellt

När assistenten har gjort ändringar ska du alltid förhandsgranska och testa formuläret för att kontrollera att det fungerar som det ska. AI är ett kraftfullt verktyg, men slutlig validering är avgörande för att säkerställa kvalitet.

**Checklista för validering:**

- Testa formulärfunktionen i förhandsgranskningsläge
- Verifiera att villkorslogik fungerar korrekt
- Kontrollera mobilrespons
- Testa formulärinlämning
- Validera tillgänglighetsfunktioner

### Iterera och förfina

Om den första prompten inte ger exakt resultat kan du försöka att formulera om eller dela upp förfrågningen i mindre steg. AI lär sig av sitt sammanhang, så mer specifika detaljer ger ofta bättre resultat.

**Exempel på iteration:**

1. Första försöket:&quot;Gör formuläret mobilvänligt&quot;
2. Förfinad:&quot;Optimera formulärlayouten för mobila skärmar under 768px med en kolumn och större touch-mål&quot;

### Ge feedback

Använd den inbyggda feedbackmekanismen för att hjälpa assistenten att lära sig och förbättra. Din feedback gör AI bättre för alla.


## Exempel på inkrementell utveckling

De här exemplen visar hur du skapar formulär steg för steg, startar enkelt och lägger till komplexitet gradvis:

### Exempel 1: Skapa ett kontaktformulär stegvis

**Steg 1 - Starta enkelt:**

```
Create a basic contact form with name, email, and message fields
```

**Steg 2 - Lägg till validering:**

```
Make @name and @email mandatory fields with appropriate validation
```

**Steg 3 - Förbättra användarupplevelsen:**

```
Add placeholder text: @name "Your full name", @email "your.email@company.com", @message "Tell us how we can help"
```

**Steg 4 - Lägg till avancerade funktioner:**

```
Add a dropdown @inquiryType with options: "General Question", "Support Request", "Sales Inquiry", "Partnership"
```

**Steg 5 - Implementera villkorslogik:**

```
Show @urgencyLevel dropdown (Low, Medium, High) only when @inquiryType equals "Support Request"
```

### Exempel 2: Skapa ett registreringsformulär stegvis

**Steg 1 - grundläggande struktur:**

```
Create a user registration form with personal information panel
```

**Steg 2 - Lägg till kärnfält:**

```
Add text input fields: @firstName, @lastName, @email, @phone to the personal information panel
```

**Steg 3 - Lägg till validering:**

```
Make @firstName, @lastName, and @email mandatory with real-time validation
```

**Steg 4 - Lägg till kontoinformation:**

```
Create a new panel "Account Information" with @username and @password fields
```

**Steg 5 - Förbättra säkerheten:**

```
Add password confirmation field @confirmPassword with validation to match @password
```

**Steg 6 - Lägg till inställningar:**

```
Create "Preferences" panel with @newsletter checkbox and @communicationMethod radio group (Email, SMS, Phone)
```

Detta stegvisa tillvägagångssätt hjälper dig att:

- Fånga upp problem tidigt innan de sätts samman
- Testa varje funktion noggrant
- Göra justeringar baserat på användarfeedback
- Få bättre kontroll över utvecklingsprocessen

## Starta ny Forms

**När ska du använda:** I början av ett formulärprojekt. Denna uppmaning hjälper AI att förstå era behov och bygga upp grundstrukturen.

**Så här använder du:** Börja med grundläggande struktur och grundläggande krav. Ange formulärtyp, målgrupp och primärt syfte. Gör efterföljande uppmaningar mer komplicerade.

**Exempelfråga - enkel start:**

```
Create a **customer onboarding form** for new bank account applications with:

**Purpose:** Collect personal information for account setup
**Target Users:** New customers applying for checking/savings accounts
**Basic Structure:** Single panel with essential fields
**Core Fields:** Name, email, phone, account type selection

Start with a simple layout that we can enhance step by step.
```

**Bygg sedan stegvis:**

```
Add an address panel to @customerOnboardingForm with street address, city, state, and zip code fields
```

```
Add employment information panel with @employer, @jobTitle, and @annualIncome fields
```

```
Add file upload field @identityDocuments for identity verification (Accept: .pdf,.jpg,.png)
```

**Alternativa enkla startfrågor:**

```
Create a basic **event registration form** with name, email, and event selection fields
```

```
Build a simple **contact form** with name, email, and message fields
```

```
Design a basic **feedback survey** with rating scale and comments field
```

## Formulärstruktur och layout

**När ska du använda:** När du behöver organisera komplexa formulär eller förbättra användarupplevelsen genom bättre layoutdesign.

**Så här använder du:** Fokusera på användarresan och logisk gruppering av information. Ange layoutinställningar och navigeringsmönster.

**Exempelfråga - Formulärstruktur i flera steg:**

```
Convert this single-page form into a **3-step wizard** with:

**Step 1: Personal Information**
- Name, email, phone, address fields
- Progress indicator showing "Step 1 of 3"
- "Next" button (validate mandatory fields before proceeding)

**Step 2: Preferences & Requirements** 
- Service selection (checkbox group)
- Budget range (dropdown)
- Timeline preferences (radio group)
- Special requirements (text input field)

**Step 3: Review & Submit**
- Summary of all entered information
- Edit links to go back to specific steps
- Terms and conditions checkbox
- Submit button with confirmation

Include "Previous" and "Next" buttons, allow users to jump between completed steps, save progress automatically.
```

**Fråga om layoutoptimering:**

```
Reorganize this form using a **wizard layout** for desktop and single column for mobile. 
```

```
Convert this long form into an **accordion layout** where users can expand/collapse sections.
```

```
Create a **vertical tabbed interface** for this form with tabs for: Basic Info, Contact Details, Preferences, and Review.
```

## Fälthantering och validering

**När du ska använda:** När du behöver lägga till, ändra eller förbättra formulärfält med specifika valideringsregler och beteenden.

**Så här använder du:** Var specifik när det gäller fälttyper, verifieringskrav och förväntningar på användarupplevelse. Referera till befintliga fält med @fieldName-syntax.

**Exempelfråga - fältförbättring:**

```
Enhance the form fields with these specific requirements:

**Email Field (@email):**
- Make mandatory with real-time validation
- Show green checkmark when valid format entered
- Display helpful error message: "Please enter a valid email address"
- Add placeholder: "your.email@company.com"

**Phone Number (@phone):**
- Type: tel for mobile optimization
- Make mandatory for business customers, optional for personal
- Add placeholder: "Enter your phone number"

**Date of Birth (@dateOfBirth):**
- Type: date with date picker
- Validate age is 18+ for account opening
- Show error if under 18: "Must be 18 or older to open account"

**File Upload (@documents):**
- Accept: .pdf,.doc,.docx
- Multiple: true for multiple document upload
- Show upload progress and file names after upload
```

**Fältspecifika frågor:**

```
Add a **file upload field** for resume with these specs: Accept only PDF/DOC/DOCX files, allow multiple files, show upload progress, display file names after upload.
```

```
Create a **dropdown field** for country selection with all countries listed. Set default value based on user's location if available.
```

```
Build a **repeatable panel** for work experience where users can add/remove multiple jobs. Each entry needs: company, title, start date, end date, description.
```

## Villkorlig logik och regler

**När ska du använda:** När du behöver ett dynamiskt formulärbeteende som baseras på användarindata eller affärsregler.

**Så här använder du:** Definiera villkoren och de resulterande åtgärderna tydligt. Använd specifika fältreferenser och logiska operatorer.

**Exempelfråga - komplex villkorlig logik:**

```
Implement these conditional rules for the application form:

**Business vs Personal Account Logic:**
- If @accountType equals "Business", show:
  - Business name field (mandatory)
  - Tax ID field (mandatory)
  - Business address section
  - Number of employees dropdown
- If @accountType equals "Personal", hide all business fields

**Income-Based Requirements:**
- If @annualIncome is less than 25000:
  - Show additional verification section
  - Make co-signer information mandatory
  - Display message: "Additional documentation may be required"
- If @annualIncome is greater than 100000:
  - Show premium services options
  - Enable priority processing checkbox

**Age-Based Validation:**
- If @age is under 18:
  - Show parent/guardian information section
  - Make parent signature upload mandatory
  - Change submit button text to "Submit for Review"
- If @age is 65 or older:
  - Show senior discount options
  - Add accessibility preferences section
```

**Regelspecifika frågor:**

```
Create a **visibility rule** that shows @spouseInformation panel only when @maritalStatus equals "Married" or "Domestic Partnership".
```

```
Add **progressive disclosure** where additional questions appear based on previous answers. Start with basic info, then show relevant follow-ups.
```

```
Implement **smart defaults** where @country selection auto-sets related fields. Allow manual override.
```

## Dataintegrering och överföring

**När ska du använda:** När du behöver ansluta formulär till serverdelssystem, databaser eller externa tjänster.

**Så här använder du:** Börja med grundläggande inskickningsinställningar och lägg sedan till ytterligare integreringar inkrementellt. Ange integreringstyp, dataformatkrav och inställningar för felhantering.

**Exempelfråga - börja med grundläggande överföring:**

```
Configure basic form submission for @applicationForm:

**Primary Submission:**
- Send form data to REST endpoint: `/api/v1/applications`
- Format data as JSON
- Show success message: "Application submitted successfully"
- Show error message if submission fails: "Submission failed, please try again"
```

**Lägg sedan till sekundära åtgärder stegvis:**

```
Add email notification to @applicationForm: Send confirmation email to @email address with application reference number
```

```
Add CRM integration to @applicationForm: Create new lead record with @firstName, @lastName, @email, and set Status to "New Application"
```

**Exempelfråga - avancerad flerkanalsöverföring:**

```
Configure form submission with multiple data destinations:

**Primary Submission:**
- Send form data to REST endpoint: `/api/v1/applications`
- Include authentication header with API key
- Format data as JSON with nested objects for address and employment
- Handle success response (201) by showing thank you message

**Secondary Actions:**
- Send notification email to applicant at @email address
- Copy application data to tracking system
- Trigger workflow for approval process
- Create record in CRM with lead status "New Application"

**Error Handling:**
- If primary submission fails, save data locally and retry
- Show user-friendly error message: "Submission temporarily unavailable"
- Provide option to download form data as backup
- Send alert email to admin team about failed submission

**Success Flow:**
- Redirect to confirmation page with application reference number
- Send confirmation email with next steps
- Display estimated processing timeline
```

**Integrationsspecifika frågor:**

```
Connect this form to **CRM system** to create new leads. Map @firstName to FirstName, @email to Email, set LeadSource to "Web Form", and Status to "New".
```

```
Set up **workflow trigger** when form is submitted. Pass all form data and trigger approval workflow with manager notification.
```

```
Configure **database integration** to save form submissions as records. Create new folder for each submission with uploaded documents.
```

## Design Import och konvertering

**När ska du använda:** När du har befintliga formulärdesigner (PDF, Figma, bilder) som måste konverteras till fungerande AEM-formulär.

**Så här använder du:** Ange en tydlig kontext om källdesignen och ange eventuella ändringar eller förbättringar som behövs.

**Exempelfråga - PDF-formulärkonvertering:**

```
Convert this uploaded **PDF application form** into a functional AEM adaptive form:

**Source Analysis:**
- Analyze the PDF layout and identify all form fields
- Preserve the visual hierarchy and grouping
- Maintain the professional appearance and branding

**Field Mapping:**
- Convert PDF text fields to adaptive form text inputs
- Transform checkboxes to checkbox components
- Convert dropdown lists to AEM dropdown components
- Map signature areas to digital signature fields

**Enhancements:**
- Add real-time validation that wasn't possible in PDF
- Implement conditional logic for dependent fields
- Make the form responsive for mobile devices
- Add progress saving capability
- Include accessibility improvements (ARIA labels, keyboard navigation)

**Styling:**
- Match the original color scheme and fonts
- Maintain professional business appearance
- Ensure consistent spacing and alignment
- Add subtle animations for better user experience

Preserve all original field labels and help text, but improve the user experience with modern form interactions.
```

**Fråga om designimport:**

```
Import this **design mockup** and convert it into an adaptive form. Maintain the exact visual design but add proper validation and mobile responsiveness.
```

```
Analyze this **image of a paper form** and recreate it digitally. Improve the layout for better mobile experience while keeping all mandatory fields.
```

```
Convert this **existing HTML form** to AEM adaptive form format. Preserve all functionality but add AEM-specific features like rules and themes.
```

## Mobiloptimering och respons

**När ska du använda:** När formulär behöver fungera sömlöst på alla enhetstyper och skärmstorlekar.

**Så här använder du:** Börja med grundläggande mobiloptimering och förbättra sedan med avancerade funktioner. Fokusera på mobilfokusering och ange brytpunktsbeteenden stegvis.

**Exempelfråga - Börja med grundläggande mobiloptimering:**

```
Make @contactForm mobile-friendly with:

**Basic Mobile Layout:**
- Single column layout for all form sections
- Larger touch targets for buttons and inputs
- Responsive design that works on phones and tablets
```

**Lägg sedan till avancerade mobilfunktioner:**

```
Enhance @contactForm mobile experience with:
- Sticky submit button at bottom of screen
- Touch-friendly date pickers
- Swipe gestures for multi-step navigation
```

**Exempelfråga - Omfattande optimering för mobiler först:**

```
Optimize this form for **mobile-first responsive design**:

**Mobile Layout (320px - 768px):**
- Single column layout for all form sections
- Larger touch targets (minimum 44px height)
- Simplified navigation with collapsible sections
- Sticky submit button at bottom of screen
- Auto-zoom disabled on input focus

**Tablet Layout (768px - 1024px):**
- Two-column layout for shorter fields (name, email)
- Single column for complex fields (address, comments)
- Side navigation for multi-step forms
- Optimized for both portrait and landscape

**Desktop Layout (1024px+):**
- Multi-column layouts where appropriate
- Horizontal form sections for related fields
- Sidebar navigation for long forms
- Hover states and advanced interactions

**Touch Optimization:**
- Larger checkbox and radio button targets
- Swipe gestures for multi-step navigation
- Pull-to-refresh for saved drafts
- Touch-friendly date/time pickers

**Performance:**
- Lazy load non-critical form sections
- Optimize images and icons for mobile
- Minimize JavaScript for faster loading
- Progressive enhancement approach
```

**Mobilspecifika enkla frågor:**

```
Make @checkoutForm mobile-optimized with large buttons and one-thumb navigation
```

```
Add touch-friendly controls to @surveyForm for tablet users
```

```
Enable offline functionality for @applicationForm with local data saving
```

## Tillgänglighet och efterlevnad

**När ska användas:** När formulär måste uppfylla tillgänglighetsstandarder (WCAG 2.1 AA) eller kompatibilitetskrav.

**Så här använder du:** Ange tillgänglighetskrav och kompatibilitetsstandarder som måste uppfyllas.

**Exempelfråga - hjälpmedelsimplementering:**

```
Make this form **WCAG 2.1 AA compliant** with these accessibility features:

**Keyboard Navigation:**
- Logical tab order through all form elements
- Skip links to main content and form sections
- Keyboard shortcuts for common actions
- Focus indicators clearly visible on all interactive elements

**Screen Reader Support:**
- Proper ARIA labels for all form fields
- Descriptive error messages announced to screen readers
- Form section headings with proper hierarchy (h1, h2, h3)
- Progress announcements for multi-step forms

**Visual Accessibility:**
- Color contrast ratio minimum 4.5:1 for text
- Don't rely solely on color to convey information
- Text size minimum 16px for body text
- Scalable up to 200% without horizontal scrolling

**Motor Accessibility:**
- Large click targets (minimum 44x44px)
- Generous spacing between interactive elements
- No time limits or provide extension options
- Alternative input methods support

**Cognitive Accessibility:**
- Clear, simple language in all instructions
- Consistent navigation and layout patterns
- Error prevention and clear error recovery
- Help text and examples for complex fields

**Testing Requirements:**
- Test with screen readers (NVDA, JAWS, VoiceOver)
- Verify keyboard-only navigation
- Check color contrast with automated tools
- Validate HTML for semantic correctness
```

**Efterlevnadsspecifika frågor:**

```
Ensure this **healthcare form meets HIPAA requirements** with proper data encryption, audit logging, and privacy controls.
```

```
Make this **financial form PCI DSS compliant** with secure payment field handling and data protection measures.
```

```
Create a **government form meeting Section 508 standards** with full accessibility and plain language requirements.
```

## Testning och kvalitet i Assurance

**När ska du använda:** När du behöver validera formulärfunktioner, användarupplevelse och tekniska prestanda.

**Så här använder du:** Ange testscenarier, kantfall och kvalitetskriterier som måste verifieras.

**Exempelfråga - Omfattande formulärtestning:**

```
Create a **comprehensive testing plan** for this application form:

**Functional Testing:**
- Test all field validations with valid and invalid data
- Verify conditional logic shows/hides fields correctly
- Test file upload with various file types and sizes
- Validate calculation fields update correctly
- Test form submission with complete and incomplete data

**User Experience Testing:**
- Test form completion time (target: under 10 minutes)
- Verify error messages are helpful and actionable
- Test progress saving and restoration
- Validate mobile touch interactions
- Check form accessibility with assistive technologies

**Edge Case Testing:**
- Test with extremely long text inputs
- Verify behavior with special characters and emojis
- Test with slow internet connections
- Validate offline functionality if applicable
- Test browser back/forward button behavior

**Performance Testing:**
- Measure form load time (target: under 3 seconds)
- Test with large file uploads
- Verify memory usage with long form sessions
- Test concurrent user submissions
- Validate database performance under load

**Security Testing:**
- Test input sanitization and XSS prevention
- Verify CSRF protection is working
- Test file upload security restrictions
- Validate data encryption in transit and at rest
- Check authentication and authorization controls

**Cross-Browser Testing:**
- Test on Chrome, Firefox, Safari, Edge
- Verify mobile browsers (iOS Safari, Chrome Mobile)
- Test on different operating systems
- Validate older browser fallbacks
- Check print functionality across browsers
```

**Testningsspecifika frågor:**

```
Create **automated test scripts** for this form's critical user paths: successful submission, validation errors, and conditional logic.
```

```
Design a **user acceptance testing plan** with realistic scenarios and success criteria for business stakeholders.
```

```
Set up **performance monitoring** to track form completion rates, abandonment points, and submission success rates.
```

## Avancerade funktioner och integreringar

**När du ska använda:** När du behöver avancerade formulärfunktioner som AI-hjälp, avancerade arbetsflöden eller komplexa integreringar.

**Så här använder du:** Definiera de avancerade funktionerna och integrationskraven tydligt.

**Exempelfråga - AI-förbättrat formulär:**

```
Add **AI-powered features** to enhance this application form:

**Smart Auto-Complete:**
- Use AI to suggest company names as user types
- Auto-populate address fields from partial input
- Suggest job titles based on industry selection
- Provide intelligent form completion suggestions

**Dynamic Question Generation:**
- Generate follow-up questions based on previous answers
- Adapt form complexity to user's experience level
- Show relevant optional fields based on user profile
- Personalize form sections for different user types

**Intelligent Validation:**
- Use AI to detect potentially incorrect information
- Suggest corrections for common data entry errors
- Validate business information against public databases
- Flag suspicious or inconsistent responses

**Content Optimization:**
- A/B test different form layouts automatically
- Optimize field order based on completion patterns
- Adjust form length based on user engagement
- Personalize help text based on user behavior

**Predictive Analytics:**
- Predict likelihood of form completion
- Identify users who might need assistance
- Suggest optimal times for form completion reminders
- Analyze drop-off points and suggest improvements

**Natural Language Processing:**
- Allow voice input for text fields
- Convert speech to text for accessibility
- Analyze open-text responses for sentiment
- Extract structured data from unstructured input
```

**Avancerade integreringsfrågor:**

```
Integrate with **CRM system** to pre-populate known customer data, update records in real-time, and trigger automated follow-up sequences.
```

```
Connect to **payment gateway** for secure transaction processing with PCI compliance, fraud detection, and multiple payment methods.
```

```
Implement **blockchain verification** for document authenticity, immutable audit trails, and decentralized identity verification.
```

## Felsökning och optimering

**När ska användas:** När formulär har prestandaproblem, användarupplevelseproblem eller tekniska problem.

**Så här använder du:** Beskriv det specifika problemet och önskat resultat tydligt.

**Exempelfråga - Prestandaoptimering:**

```
Optimize this form for **better performance and user experience**:

**Current Issues:**
- Form takes 8+ seconds to load on mobile
- Users are abandoning at the address section (60% drop-off)
- File uploads frequently fail or timeout
- Validation errors are confusing users

**Performance Improvements:**
- Implement lazy loading for non-critical form sections
- Optimize images and reduce bundle size
- Add progressive loading indicators
- Cache frequently used data (country lists, etc.)
- Minimize JavaScript execution time

**User Experience Fixes:**
- Simplify the address section with auto-complete
- Add inline validation with helpful error messages
- Implement smart defaults based on user location
- Add progress saving every 30 seconds
- Provide clear instructions for each section

**Technical Optimizations:**
- Implement chunked file uploads with resume capability
- Add client-side validation before server submission
- Optimize database queries for faster responses
- Implement proper error handling and retry logic
- Add comprehensive logging for debugging

**Monitoring & Analytics:**
- Set up form analytics to track user behavior
- Monitor completion rates by section
- Track error rates and types
- Measure performance metrics continuously
- A/B test improvements with real users
```

**Felsökningsfrågor:**

```
**Debug this form submission error:** Users report getting "500 Internal Server Error" when submitting. Check validation logic, server endpoints, and data formatting.
```

```
**Fix mobile layout issues:** Form fields are overlapping on iPhone screens and submit button is not visible. Ensure proper responsive design.
```

```
**Resolve validation conflicts:** Some users can't submit even with valid data. Review validation rules for conflicts and edge cases.
```

## Miljöspecifika bästa metoder

### Forms Management UI

**När ska du använda:** För formulärskaps- och hanteringsaktiviteter på hög nivå.

```
In Forms Management UI, create a new **customer survey template** that can be reused across different departments. Include standard branding, common field types, and configurable sections.
```

### Adaptiv Forms Editor

**När ska du använda:** För detaljerad formulärkonfiguration och komplex regelgenerering.

```
In the Adaptive Forms Editor, configure **advanced business rules** for this loan application: calculate debt-to-income ratio, determine eligibility, and show appropriate next steps.
```

### Universal Editor

**När ska du använda:** För Edge Delivery Services-formulär med visuell redigering.

```
In Universal Editor, create a **responsive contact form** for the company website. Ensure it matches the site design and integrates with the existing content management workflow.
```

## Lathund - snabbguide

| Kommando | Bästa användningsfall | Exempel |
|---------|---------------|---------|
| `/create-form` | Starta nya formulär | `/create-form employee onboarding with personal info and benefits selection` |
| `/add-form` | Lägga till formulär på sidor | `/add-form newsletter signup with email and preferences` |
| `/update-layout` | Ändra formulärstruktur | `/update-layout wizard with 4 steps: info, preferences, review, confirm` |
| `/update-field` | Ändra fältegenskaper | `/update-field @email to be mandatory with real-time validation` |
| `/create-rule` | Lägga till dynamiskt beteende | `/create-rule show @spouseInfo if @maritalStatus equals "Married"` |
| `/create-panel` | Ordna formuläravsnitt | `/create-panel Employment Details with job title, company, salary fields` |
| `/add-panel` | Konvertera designer | `/add-panel from uploaded form image with field recognition` |
| `/configure-submit` | Ställa in datahantering | `/configure-submit to CRM and send confirmation email` |
| `/help` | Få hjälp | `/help how to implement multi-step validation?` |

## Referens för komponentegenskaper som stöds

### Universella egenskaper (alla komponenter)

- **Typ**: Komponenttyp (text, e-post, nummer, tel, datum, kryssruta, radio, listruta, fil osv.)
- **Namn**: Fältidentifierare för formulärsändning
- **Etikett**: Visa text för fältet
- **Beskrivning**: Hjälptext för fältet
- **Synlig**: Boolesk för inledande synlighet
- **Obligatoriskt**: Booleskt för obligatoriska fält

### Egenskaper för inmatningsfält

- **Värde**: Standardvärde/startvärde
- **Platshållare**: Tipstext för inmatningsfält
- **Min**: Minsta värde (för siffror/datum)
- **Max**: Maximalt värde (för siffror/datum)

### Egenskaper för filöverföring

- **Acceptera**: Filtyper (.pdf, .doc, .docx, .jpg, .png osv.)
- **Flera**: Boolean för flera filval

### Egenskaper för markeringskontroll

- **Alternativ**: Alternativ för listrutor (kommaseparerad lista)
- **Markerad**: Standardval för kryssrutor/radio

### Behållaregenskaper

- **Fältuppsättning**: Gruppera relaterade fält
- **Repeterbar**: Boolean för repeterbara avsnitt

### Avancerade egenskaper

- **Synligt uttryck**: Formel för villkorlig synlighet (=formel)
- **Värdeuttryck**: Formel för beräknade värden (=formel)

## Sammanfattning av bästa praxis

### Tekniska riktlinjer

- **Använd bara egenskaper som stöds** från den officiella AEM Forms-komponentspecifikationen
- **Följ rätt syntax** för fältreferenser (@fieldName) och uttryck (=formula)
- **Testa inkrementellt** efter varje ändring för att fånga upp problem tidigt
- **Planera för tillgänglighet** från början, inte som en eftertanke
- **Fundera på mobilanvändare** i varje designbeslut
- **Dokumentkomplexa regler** för framtida underhåll och teamsamarbete

### Strategisk strategi

- **Börja med användarnas behov** - Fokusera på vad användarna behöver göra, inte bara på tekniska funktioner
- **Design för slutförande** - Minimera friktion och kognitiv belastning i formulärdesign
- **Planera dataflöde** tidigt - Fundera på hur data ska behandlas, lagras och användas
- **Bygg för skala** - Designa formulär som kan hantera förväntad användarvolym och datatillväxt
- **Implementera progressiv förbättring** - Kontrollera att grundläggande funktioner fungerar och lägg sedan till avancerade funktioner

### Vanliga fallgropar att undvika

- **Överdrivet komplexa initiala begäranden** - Dela upp stora uppgifter i mindre, hanterbara steg
- **Använder egenskaper som inte stöds** som inte finns i AEM Forms-specifikationen
- **Mobilupplevelsen ignoreras** tills sent i utvecklingsprocessen
- **Hoppar över användartestning** med verkliga scenarier och edge-fall
- **Anta att AI förstår kontext** utan att ge tydliga, specifika instruktioner
- **Glömmer om hjälpmedel** och kompatibilitetskrav
- **Verifierar inte ändringar** innan du går vidare till nästa steg

### Assurance-strategi för kvalitet

1. **Förhandsgranska ofta** - Kontrollera resultatet i förhandsgranskningsläget efter varje ändring
2. **Testa kantfall** - Prova ovanliga indata, lång text, specialtecken
3. **Validera mellan enheter** - Testa på mobiler, surfplattor och datorer
4. **Kontrollera tillgänglighet** - Kontrollera tangentbordsnavigering och skärmläsarkompatibilitet
5. **Prestandatest** - Kontrollera att formulären läses in snabbt och att de fungerar som de ska
6. **Testning av användargodkännande** - Låt verkliga användare testa formuläret innan det distribueras


*Detta promptbibliotek uppdateras kontinuerligt baserat på användarfeedback och nya AI Assistant-funktioner. De senaste funktionerna och exemplen finns i [AEM Forms-dokumentationen](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/home.html?lang=sv-SE).*

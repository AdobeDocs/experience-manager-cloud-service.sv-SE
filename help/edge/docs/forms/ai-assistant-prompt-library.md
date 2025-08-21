---
title: Forms Experience Builder - Prompt Library
description: Samling av beprövade promptmönster och exempel för att skapa formulär med hjälp av AI i Forms Management-gränssnittet, Adaptive Forms Editor och Universal Editor.
feature: Edge Delivery Services
hide: true
index: false
hidefromtoc: true
role: Admin, Architect, Developer
exl-id: 333d42e0-625f-432e-a61b-5d49bf08765a
source-git-commit: 8be2b09200af58c701721b3e8537ea5e6cc3e4a2
workflow-type: tm+mt
source-wordcount: '1338'
ht-degree: 0%

---

# Forms Experience Builder - Prompt Library

Samling av återanvändbara promptmönster och exempel som är optimerade för Forms Experience Builder. Det här smidiga biblioteket fokuserar på de två grundläggande metoderna: Skapa från grunden och Importera och konvertera, med förbättrat stöd för smarta fält som bygger på LLM och enhetlig varumärkeshantering.

>[!NOTE]
>
> Forms Experience Builder är tillgängligt via programmet för tidig användning. Skicka ett e-postmeddelande från din arbetsadress till `aem-forms-ea@adobe.com` för att begära åtkomst.

>[!IMPORTANT]
>
> **Dokumentation som kan ändras**: Det här snabbbiblioteket testas för närvarande mot produkten och kan komma att uppdateras och revideras. Frågar, exempel och bästa metoder kan ändras i takt med att Forms Experience Builder fortsätter att utvecklas under det program som antagits tidigt.

## Använda detta frågebibliotek

Det här biblioteket innehåller återanvändbara promptmönster för vanliga formulärgenereringsscenarier. Mer information finns i [Forms Experience Builder Komma igång-guiden](forms-ai-assistant-getting-started.md#best-practices).

### Snabbtips för det här biblioteket

- **Börja med exempel** - Använd tillhandahållna uppmaningar som mallar och anpassa efter dina behov
- **Två metoder** - Välj Skapa från grunden eller Importera och konvertera.
- **Var specifik** - Lägg till egna detaljer i generiska exempel
- **Testa noggrant** - Verifiera alltid resultat i din specifika miljö

### Märkesmallar och format

**Förbered varumärkesresurser i förväg för att skapa enhetliga formulär:**

- **Varumärkesmallar** - Skapa standardiserade formulärmallar med organisationens färger, teckensnitt och layoutmönster
- **Riktlinjer för format** - Definiera konsekvent fältformat, knappdesign och mellanrumsstandarder
- **Komponentbibliotek** - Skapa återanvändbara formulärkomponenter som matchar din varumärkesidentitet
- **Visual Assets** - Förbered logotyper, ikoner och bakgrundselement för formulärintegrering

**Exempel på fråga om varumärkesmall:**

```
Create a brand template for financial services forms with:
- Corporate blue (#003366) and silver (#C0C0C0) color scheme
- Open Sans font family for all text
- 16px minimum font size for accessibility
- Consistent 24px spacing between sections
- Corporate logo in header with proper sizing
- Professional button styling with hover effects
```

>[!NOTE]
>
>**Anpassade komponenter**: Kontrollera med ditt utvecklingsteam om hur du använder organisationsspecifika komponenter och deras kompatibilitet med Forms Experience Builder innan du implementerar anpassade varumärkeselement.

>[!NOTE]
>
> Detta promptbibliotek har uppdaterats för att återspegla de strömlinjeformade funktionerna i Forms Experience Builder. Vissa avancerade integrerings- och testfunktioner som visas i exemplen kan kräva ytterligare konfiguration.



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

**Steg 2 - Lägg till obligatoriska fält:**

```
Add fields for @firstName, @lastName, @email, @phoneNumber with appropriate validation
```

**Steg 3 - Lägg till affärslogik:**

```
Create a rule: if @age is under 18, show parent/guardian information section
```

**Steg 4 - Förbättra med inställningar:**

```
Add a preferences panel with @newsletterSubscription, @marketingConsent, @termsAccepted
```

**Steg 5 - Lägg till filöverföring:**

```
Include a file upload field for @profilePicture with size limit of 5MB
```

## Skapa och hantera formulär

**När ska du använda:** När du behöver skapa nya formulär eller ändra befintliga.

**Så här använder du:** Välj en av två metoder: Skapa från grunden eller Importera och konvertera (se [Guiden Komma igång](/help/edge/docs/forms/forms-ai-assistant-getting-started.md)).

**Exempelfråga - Skapa enkelt formulär:**

```
Create a customer feedback form with:
- Product rating (1-5 stars)
- Comment field for detailed feedback
- Customer email (optional)
- Submit to email notification
```

**Exempelfråga - skapa komplexa formulär:**

```
Create a comprehensive employee onboarding form with:

**Personal Information Section:**
- Full name (first, middle, last)
- Date of birth with age validation
- Contact information (email, phone, address)
- Emergency contact details

**Employment Details:**
- Position and department selection
- Start date with business day validation
- Salary information with confidentiality notice
- Reporting structure

**Document Upload:**
- Resume/CV upload (PDF, DOC, DOCX)
- ID verification documents
- Tax forms and banking information
- Signed employment agreement

**Preferences:**
- Benefits selection with cost calculator
- Work schedule preferences
- Training requirements
- Equipment needs

**Validation Rules:**
- Email format validation
- Phone number format validation
- Age must be 18 or older
- All required documents must be uploaded
- Terms and conditions must be accepted

**Submit Actions:**
- Send confirmation email to new employee
- Notify HR department
- Create employee record in HR system
- Schedule orientation meeting
```

**Formulärhanteringsfrågor:**

```
Import this PDF application form and convert it to an adaptive form with enhanced validation
```

```
Update the existing contact form to include social media handles and preferred contact method
```

```
Reorganize the registration form into a 3-step wizard: personal info, preferences, confirmation
```

## Fälthantering och konfiguration

**När ska du använda:** När du behöver lägga till, ändra eller konfigurera formulärfält.

**Så här använder du:** Var specifik när det gäller fälttyper, verifieringsregler och krav på användarupplevelse.

**Exempelfråga - grundläggande fälttillägg:**

```
Add a text input field for "Company Name" with placeholder "Enter your company name"
```

**Exempelfråga - avancerad fältkonfiguration:**

```
Add a comprehensive address section with:

**Street Address:**
- Address line 1 (required, max 100 characters)
- Address line 2 (optional, max 100 characters)
- City (required, dropdown with common cities)
- State/Province (required, dropdown)
- Postal code (required, format validation)
- Country (required, default to "United States")

**Validation Rules:**
- Postal code must match state selection
- Address line 1 cannot be empty
- City must be a valid city for selected state

**User Experience:**
- Auto-complete for address fields
- Clear labels and help text
- Mobile-friendly input fields
- Accessibility compliance
```

**Fråga om fältkonfiguration:**

```
Make @email field required with real-time validation and custom error message
```

```
Add a dropdown for @country with options for USA, Canada, UK, Germany, France, and "Other"
```

```
Configure @phoneNumber field with format (XXX) XXX-XXXX and validation
```

```
Add a file upload field for @resume with PDF and DOC restrictions, max 5MB
```

## LLM-Enhanced Smart Fields

**När ska du använda:** När du behöver fält med förifyllda alternativ som utnyttjar AI:s kunskapsbas.

**Så här använder du:** Begär fält som kräver omfattande datauppsättningar - AI kan automatiskt fylla i alternativ med hjälp av den inbyggda kunskapen.

### Geografiska fält och platsfält

**Flygplatser och transport:**

```
Add a dropdown for departure airports with all major international airports
Add arrival airport field with IATA codes and full names
Create a field for nearest airport to user location
Add a selection of train stations for European cities
```

**Administrativa regioner:**

```
Add a complete list of US states with abbreviations
Create a country dropdown with ISO codes and full names
Add a field for major world cities with time zones
Include a dropdown of Canadian provinces and territories
Add a field for UK counties and postal areas
```

### Affärs- och branschdata

**Företagsklassificeringar:**

```
Add a field for industry classification with NAICS codes
Create a dropdown of business entity types (LLC, Corporation, Partnership, etc.)
Add a field for company size categories (startup, SME, enterprise)
Include department selection for large organizations
Add a field for professional service types
```

**Professionella klassificeringar:**

```
Add a field for job titles with common industry roles
Create a dropdown of professional certifications by field
Include education levels with degree types
Add a field for years of experience ranges
Create a selection for programming languages and frameworks
```

### Standarder och bestämmelser

**Finans och juridik:**

```
Add a field for currency codes with symbols and exchange rates
Create a dropdown of tax ID types by country
Include a field for legal document types
Add payment method options with security features
Create a selection for banking institutions by country
```

**Tekniska standarder:**

```
Add a dropdown of file format types with extensions
Include network protocol options
Add a field for database types and versions
Create a selection for API authentication methods
```

### Hälso- och sjukvård

**Medicinska klassificeringar:**

```
Add a field for medical specialties
Create a dropdown of common medications with generic names
Include a field for insurance provider types
Add a selection for medical emergency contact relationships
Create a field for dietary restrictions and allergies
```

### Time and Calendar Intelligence

**Datum- och tidsfält:**

```
Add a field for business hours with time zone handling
Create a dropdown of public holidays by country
Include seasonal options with date ranges
Add a field for conference room booking with availability
Create a selection for recurring meeting patterns
```

### Produkt- och tjänstekategorier

**E-handelsklassificeringar:**

```
Add a field for product categories with subcategories
Create a dropdown of shipping methods with delivery estimates
Include a field for return policy options
Add a selection for customer priority levels
Create a field for subscription billing cycles
```

**Exempel på frågor om smarta fält:**

```
"Add a departure airport field with all major airports worldwide including IATA codes and city names"
```

```
"Create a comprehensive industry field using standard NAICS classification with technology subcategories"
```

```
"Include a professional certification dropdown that adapts based on the selected job field"
```

```
"Add an international phone number field that formats based on the selected country"
```

```
"Create a university selection field with major institutions organized by country and ranking"
```

## Regelskapande och affärslogik

**När du ska använda:** När du måste implementera villkorslogik, verifieringsregler eller affärsprocesser.

**Så här använder du:** Beskriv affärslogiken tydligt och ange villkor och åtgärder.

**Exempelfråga - enkel villkorslogik:**

```
Create a rule that shows @spouseInformation panel only when @maritalStatus equals "Married"
```

**Exempelfråga - komplexa affärsregler:**

```
Implement comprehensive loan application validation:

**Income Validation:**
- If @annualIncome is less than 30000:
  - Show warning message: "Income may be insufficient for requested loan amount"
  - Require additional income documentation
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
Create a **visibility rule** that shows @spouseInformation panel only when @maritalStatus equals "Married" or "Domestic Partnership"
```

```
Add **progressive disclosure** where additional questions appear based on previous answers. Start with basic info, then show relevant follow-ups
```

```
Implement **smart defaults** where @country selection auto-sets related fields. Allow manual override
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

**Exempelfråga - standard för flerkanalsöverföring:**

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
Connect this form to **CRM system** to create new leads. Map @firstName to FirstName, @email to Email, set LeadSource to "Web Form", and Status to "New"
```

```
Set up **workflow trigger** when form is submitted. Pass all form data and trigger approval workflow with manager notification
```

```
Configure **database integration** to save form submissions as records. Create new folder for each submission with uploaded documents
```

## Importera och konvertera befintlig Forms

**När ska du använda:** När du har befintliga formulär, dokument eller designer att omvandla till moderna AEM-formulär.

**Så här använder du:** Överför källfilen och beskriv konverteringskraven (se [Importera guide](/help/edge/docs/forms/forms-ai-assistant-getting-started.md)).

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

Preserve all original field labels and help text, but improve the user experience with modern form interactions
```

**Fråga om designimport:**

```
Import this **design mockup** and convert it into an adaptive form. Maintain the exact visual design but add proper validation and mobile responsiveness
```

```
Analyze this **image of a paper form** and recreate it digitally. Improve the layout for better mobile experience while keeping all mandatory fields
```

```
Convert this **existing HTML form** to AEM adaptive form format. Preserve all functionality but add AEM-specific features like rules and themes
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
```

**Mobilspecifika frågor:**

```
Make this form **touch-friendly** with larger buttons and simplified navigation for mobile users
```

```
Optimize form for **tablet users** with appropriate field sizes and navigation patterns
```

```
Add **swipe gestures** for multi-step form navigation on mobile devices
```

## Tillgänglighet och efterlevnad

**När ska användas:** När formulär måste uppfylla tillgänglighetsstandarder (WCAG) eller kompatibilitetskrav.

**Så här använder du:** Ange den kompatibilitetsnivå som krävs och eventuella tillgänglighetsfunktioner som behövs.

**Exempelfråga - grundläggande tillgänglighet:**

```
Make @contactForm accessible with:

**Basic Accessibility:**
- Proper ARIA labels for all form fields
- Keyboard navigation support
- High contrast color scheme
- Screen reader compatibility
- Focus indicators for all interactive elements
```

**Exempelfråga - avancerad tillgänglighet:**

```
Implement comprehensive accessibility for @applicationForm:

**WCAG 2.1 AA Compliance:**
- Semantic HTML structure with proper headings
- ARIA landmarks and roles for navigation
- Color contrast ratio of at least 4.5:1
- Keyboard-only navigation support
- Screen reader announcements for dynamic content

**Form-Specific Accessibility:**
- Error messages announced to screen readers
- Field validation with clear error descriptions
- Progress indicators for multi-step forms
- Skip navigation links for keyboard users
- Alternative text for all images and icons

**User Experience:**
- Clear focus indicators on all interactive elements
- Logical tab order through form fields
- Descriptive link text and button labels
- Help text available for complex fields
- Timeout warnings for session expiration
```

**Tillgänglighetsspecifika frågor:**

```
Add **screen reader support** to this form with proper ARIA labels and announcements
```

```
Implement **keyboard navigation** for all form interactions and navigation elements
```

```
Ensure **color contrast** meets WCAG AA standards for all text and interactive elements
```

## Prestandaoptimering

**När ska användas:** När formulär måste läsas in snabbt och fungera bra under olika förhållanden.

**Så här använder du:** Ange prestandakrav och optimeringsstrategier.

**Exempelfråga - Grundläggande prestanda:**

```
Optimize @contactForm for performance:

**Loading Optimization:**
- Lazy load non-critical form sections
- Minimize initial bundle size
- Optimize images and assets
- Enable caching for static resources
```

**Exempelfråga - Avancerade prestanda:**

```
Implement comprehensive performance optimization for @applicationForm:

**Loading Performance:**
- Progressive loading of form sections
- Optimize images with WebP format
- Minimize JavaScript bundle size
- Enable gzip compression for all assets

**Runtime Performance:**
- Debounce validation calls to reduce API requests
- Optimize conditional logic execution
- Cache frequently used data
- Implement virtual scrolling for long lists

**User Experience:**
- Show loading indicators for async operations
- Provide offline capability for form data
- Auto-save form progress every 30 seconds
- Optimize form submission with retry logic

**Monitoring:**
- Track form load times and user interactions
- Monitor validation performance
- Measure submission success rates
- Alert on performance degradation
```

**Prestandaspecifika frågor:**

```
Optimize form **loading speed** by implementing progressive loading and asset optimization
```

```
Add **auto-save functionality** to prevent data loss during form completion
```

```
Implement **offline support** so users can complete forms without internet connection
```

## Testning och kvalitet i Assurance

**När ska användas:** När formulär behöver omfattande testning för att säkerställa tillförlitlighet och användarnöjdhet.

**Så här använder du:** Ange testscenarier, valideringskrav och kvalitetsmått.

**Exempelfråga - Grundläggande testning:**

```
Add comprehensive testing for @contactForm:

**Functional Testing:**
- Test all form field validations
- Verify submit functionality works correctly
- Test error handling and user feedback
- Validate conditional logic and rules
```

**Exempelfråga - avancerad testning:**

```
Implement comprehensive testing strategy for @applicationForm:

**Functional Testing:**
- Unit tests for all validation rules
- Integration tests for submit actions
- End-to-end testing for complete user flows
- Cross-browser compatibility testing

**User Experience Testing:**
- Usability testing with target user groups
- Accessibility testing with screen readers
- Mobile device testing on various screen sizes
- Performance testing under load conditions

**Quality Assurance:**
- Automated testing for regression prevention
- Manual testing for edge cases and scenarios
- Security testing for data protection
- Compliance testing for regulatory requirements

**Monitoring:**
- Track form completion rates and abandonment
- Monitor error rates and user feedback
- Measure performance metrics and load times
- Analyze user behavior and interaction patterns
```

**Testningsspecifika frågor:**

```
Add **automated testing** for all form validations and submit functionality
```

```
Implement **user acceptance testing** scenarios for complete form workflows
```

```
Set up **performance monitoring** to track form load times and user interactions
```

## Felsökning

Snabba lösningar på vanliga problem med Forms Experience Builder:

| Problem | Snabbkorrigering |
|-------|-----------|
| Formuläret skickar inte | Kontrollera konfigurationen och valideringsreglerna för Skicka-åtgärd |
| Valideringsfel visas inte | Verifiera fältvalideringsinställningar och placering av felmeddelanden |
| Mobila layoutproblem | Granska responsiva designinställningar och fältstorlek |
| Fält som inte visas | Kontrollera villkorsstyrd logik och synlighetsregler |
| Importfel | Verifiera kompatibilitet och storleksbegränsningar för filformat |
| Integreringsfel | Validera API-slutpunkter och autentiseringsuppgifter |
| Prestandaproblem | Optimera fältantalet och ta bort onödiga valideringar |
| Tillgänglighetsproblem | Granska fältetiketter, ARIA-attribut och tabbordning |

**Fråga om felsökningsläge:**

```
Enable debug mode to identify issues with form submission and field validation
```

**Felanalysfråga:**

```
Analyze form errors: check validation rules, API responses, and user input patterns
```

## Avancerad analys och insikter

**När ska du använda:** När du behöver förstå formulärprestanda och användarbeteende.

**Så här använder du:** Ange de analyskrav och insikter som krävs.

**Exempelfråga - Grundläggande analys:**

```
Add analytics to @contactForm:

**Basic Metrics:**
- Form completion rates
- Field abandonment rates
- Submit success/failure rates
- User session duration
```

**Exempelfråga - avancerad analys:**

```
Implement comprehensive analytics for @applicationForm:

**User Behavior Analytics:**
- Track field completion rates and abandonment
- Monitor user session duration and patterns
- Analyze form navigation and user flow
- Identify bottlenecks and friction points

**Performance Analytics:**
- Measure form load times and performance
- Track API response times and failures
- Monitor validation rule effectiveness
- Analyze submission success rates

**Business Intelligence:**
- Generate reports on form effectiveness
- Track conversion rates and ROI
- Monitor user satisfaction and feedback
- Identify opportunities for optimization

**Predictive Analytics:**
- Predict form completion likelihood
- Identify users likely to abandon
- Recommend form improvements
- Optimize user experience based on data
```

**Analysspecifika frågor:**

```
Add **conversion tracking** to measure form completion rates and user behavior
```

```
Implement **A/B testing** to compare different form designs and optimize performance
```

```
Create **analytics dashboard** to monitor form performance and user insights
```

## Säkerhet och dataskydd

**När ska användas:** När formulär hanterar känsliga data och behöver säkerhetsåtgärder.

**Så här använder du:** Ange säkerhetskrav och dataskyddsåtgärder.

**Exempelfråga - grundläggande säkerhet:**

```
Add security measures to @contactForm:

**Basic Security:**
- HTTPS encryption for all data transmission
- Input validation and sanitization
- CSRF protection for form submissions
- Secure session management
```

**Exempelfråga - avancerad säkerhet:**

```
Implement comprehensive security for @applicationForm:

**Data Protection:**
- End-to-end encryption for sensitive data
- PII data masking and anonymization
- Secure file upload with virus scanning
- Data retention and deletion policies

**Access Control:**
- Role-based access control for form data
- Multi-factor authentication for admin access
- Audit logging for all data access
- Secure API authentication and authorization

**Compliance:**
- GDPR compliance for data handling
- HIPAA compliance for health information
- PCI DSS compliance for payment data
- SOC 2 compliance for data security

**Monitoring:**
- Real-time security monitoring and alerts
- Intrusion detection and prevention
- Data breach notification systems
- Regular security audits and assessments
```

**Säkerhetsspecifika frågor:**

```
Implement **data encryption** for sensitive form submissions and user information
```

```
Add **access control** to restrict form data access based on user roles and permissions
```

```
Set up **security monitoring** to detect and prevent unauthorized access to form data
```

## Kommandoreferens

### Essential Commands

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

### Fältreferenser

Använd syntaxen `@fieldName` för att referera till befintliga fält i dina uppmaningar:

- `@email` - Referensfält för e-post
- `@firstName` - Referensförnamnsfält
- `@maritalStatus` - Referensfält för civilstånd

### Komponenttyper

**Indatakomponenter:**

- `text`, `email`, `number`, `tel`, `date`, `checkbox`, `radio`, `dropdown`, `file`, `textarea`

**Behållarkomponenter:**

- `fieldset`, `panel`, `repeatable`, `wizard`

### Komponentegenskaper

**Universella egenskaper (alla komponenter):**

- **Typ**: Komponenttyp
- **Namn**: Fältidentifierare för formulärsändning
- **Etikett**: Visa text för fältet
- **Beskrivning**: Hjälptext för fältet
- **Synlig**: Boolesk för inledande synlighet
- **Obligatoriskt**: Booleskt för obligatoriska fält

**Egenskaper för indatafält:**

- **Värde**: Standardvärde/startvärde
- **Platshållare**: Tipstext för inmatningsfält
- **Min**: Minsta värde (för siffror/datum)
- **Max**: Maximalt värde (för siffror/datum)

**Egenskaper för filöverföring:**

- **Acceptera**: Filtyper (.pdf, .doc, .docx, .jpg, .png osv.)
- **Flera**: Boolean för flera filval

**Egenskaper för markeringskontroll:**

- **Alternativ**: Alternativ för listrutor (kommaseparerad lista)
- **Markerad**: Standardval för kryssrutor/radio

**Behållaregenskaper:**

- **Fältuppsättning**: Gruppera relaterade fält
- **Repeterbar**: Boolean för repeterbara avsnitt

**Avancerade egenskaper:**

- **Synligt uttryck**: Formel för villkorlig synlighet (=formel)
- **Värdeuttryck**: Formel för beräknade värden (=formel)

### Integreringskommandon

**Skicka åtgärder:**

- E-postaviseringar
- REST API-överföringar
- molnlagring (Azure, SharePoint)
- Automatisering av arbetsflöden (Power Automate, Workfront Fusion)
- Marknadsplattformar (Marketo)
- CRM-integreringar

### Visa riktlinjer för syntax

- **Fältreferenser**: Använd `@fieldName` för befintliga fält
- **Kommandon**: Använd `/command` för specifika åtgärder
- **Naturligt språk**: Beskriv kraven tydligt och specifikt

### Checklista för validering

Mer information om god praxis och riktlinjer för validering finns i [Forms Experience Builder Getting Started Guide](forms-ai-assistant-getting-started.md#best-practices).

*Detta promptbibliotek uppdateras kontinuerligt baserat på användarfeedback och nya funktioner i Forms Experience Builder. De senaste funktionerna och exemplen finns i [AEM Forms-dokumentationen](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/home.html).*

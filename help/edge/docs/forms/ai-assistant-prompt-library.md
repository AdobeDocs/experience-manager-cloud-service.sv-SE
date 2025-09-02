---
title: Forms Experience Builder - Prompt Library
description: Samling av beprövade promptmönster och exempel för att skapa formulär med hjälp av AI i Forms Management-gränssnittet, Adaptive Forms Editor och Universal Editor.
feature: Edge Delivery Services
hide: true
index: false
hidefromtoc: true
role: Admin, Architect, Developer
exl-id: c8f64082-a23f-4919-ad66-042faad77d31
source-git-commit: fe34b44d02c308e7d18a08dd05f21abc67bd0cb2
workflow-type: tm+mt
source-wordcount: '2193'
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

- **Varumärkesmallar** - Förbered standardiserade formulärmallar med organisationens färger, teckensnitt och layoutmönster
- **Riktlinjer för format** - Definiera konsekvent fältformat, knappdesign och mellanrumsstandarder som kan användas i Forms Experience Builder
- **Komponentbibliotek** - Samarbeta med ditt utvecklingsteam för att förbereda återanvändbara formulärkomponenter som matchar din varumärkesidentitet
- **Visual Assets** - Förbered logotyper, ikoner och bakgrundselement för formulärintegrering

<!-- **Example Brand Application Prompt:**

    Apply our financial services brand template with:
    - Corporate blue (#003366) and silver (#C0C0C0) color scheme
    - Open Sans font family for all text
    - 16px minimum font size for accessibility
    - Consistent 24px spacing between sections
    - Corporate logo in header with proper sizing
    - Professional button styling with hover effects

>[!NOTE]
>
>**Custom Components**: Check with your development team about using organization-specific components and their compatibility with Forms Experience Builder before implementing custom brand elements.

>[!NOTE]
>
> This prompt library has been updated to reflect the streamlined Forms Experience Builder capabilities. Some advanced integration and testing features shown in examples may require additional configuration.

-->


## Exempel på inkrementell utveckling

De här exemplen visar hur du skapar formulär steg för steg, startar enkelt och lägger till komplexitet gradvis:

### Exempel 1: Skapa ett kontaktformulär stegvis

**Steg 1 - Starta enkelt:**

    Skapa ett enkelt kontaktformulär med namn, e-post och meddelandefält

**Steg 2 - Lägg till validering:**

    Gör obligatoriska fält för @name och @email med lämplig validering

**Steg 3 - Förbättra användarupplevelsen:**

    Lägg till platshållartext: @name &quot;Ditt fullständiga namn&quot;, @email &quot;your.email@company.com&quot;, @message &quot;Berätta för oss hur vi kan hjälpa&quot;

**Steg 4 - Lägg till avancerade funktioner:**

    Lägg till en nedrullningsbar frågetyp med alternativ: &quot;Allmän fråga&quot;, &quot;Supportförfrågan&quot;, &quot;Försäljningsförfrågan&quot;, &quot;Partnerskap&quot;

**Steg 5 - Implementera villkorslogik:**

    /create-rule show @quickLevel dropdown (Low, Medium, High) enbart när @surveyType är lika med &quot;Support Request&quot;

### Exempel 2: Skapa ett registreringsformulär stegvis

**Steg 1 - grundläggande struktur:**

    Skapa ett användarregistreringsformulär med panelen för personlig information

**Steg 2 - Lägg till obligatoriska fält:**

    Lägg till fält för @firstName, @lastName, @email, @phoneNumber med lämplig validering

**Steg 3 - Lägg till affärslogik:**

    Skapa en regel: Om @age är under 18, visa informationsavsnittet för förälder/vårdnadshavare

**Steg 4 - Förbättra med inställningar:**

    Lägg till en inställningspanel med @newsletterSubscription, @marketingConsent, @termsAccepted

**Steg 5 - Lägg till filöverföring:**

    Inkludera ett filöverföringsfält för @profilePicture med storleksgränsen 5 MB

## Skapa och hantera formulär

**När ska du använda:** När du behöver skapa nya formulär eller ändra befintliga.

**Så här använder du:** Välj en av två metoder: Skapa från grunden eller Importera och konvertera (se [Guiden Komma igång](forms-ai-assistant-getting-started.md#two-ways-to-create-forms)).

**Exempelfråga - Skapa enkelt formulär:**

    Skapa ett formulär för kundfeedback med:
    - Produktklassificering (1-5 stjärnor)
    - Kommentarsfält för detaljerad feedback
    - E-post från kund (valfritt)
     - Skicka till e-postmeddelande

**Exempelfråga - skapa komplexa formulär:**

    Skapa ett omfattande formulär för anställdas introduktion med:
    
    **Personlig informationssektion:*
    - Fullständigt namn (första, mellersta, sista)
    - Födelsedatum med åldersverifiering
    - Kontaktinformation (e-post, telefon, adress)
    - Nödkontaktinformation
    
    **Anställningsinformation:*
    - Val av befattning och avdelning
    - Startdatum med arbetsdagsvalidering&lbrace;9- ary information with privacy notice
    - Reporting structure
    **Document Upload:**
    
    - Resume/CV upload (PDF, DOC, DOCX)
    - ID verification documents
    - Tax forms and Banking information
    - Signed Employment Agreement
    **Preferences:**
    
    - Benefits selection med kostnadsräknare
    - Inställningar för arbetsschema
    - Utbildningskrav
    - Utrustningen behöver 
    **Valideringsregler:*
    
    - Validering av e-postformat
    - Validering av telefonnummerformat
    - Åldern måste vara 18 eller äldre
    - Alla obligatoriska dokument måste överföras
     - Villkor accepteras
    **Skicka åtgärder:**
    
    - Skicka bekräftelsemeddelande via e-post till en ny anställd
    - Meddela HR-avdelningen
    - Skapa medarbetarpost i HR-systemet
     - Schemalägg orienteringsmöte 
    

**Formulärhanteringsfrågor:**

    Importera det här PDF-ansökningsformuläret och konvertera det till ett adaptivt formulär med förbättrad validering
    
    Uppdatera det befintliga kontaktformuläret så att det innehåller handtag för sociala medier och föredragen kontaktmetod
    
    Organisera om registreringsformuläret till en guide i tre steg: personlig information, inställningar, bekräftelse

## Fälthantering och konfiguration

**När ska du använda:** När du behöver lägga till, ändra eller konfigurera formulärfält.

**Så här använder du:** Var specifik när det gäller fälttyper, verifieringsregler och krav på användarupplevelse.

**Exempelfråga - grundläggande fälttillägg:**

    Lägg till ett textinmatningsfält för &quot;Företagsnamn&quot; med platshållaren &quot;Ange ditt företagsnamn&quot;

**Exempelfråga - avancerad fältkonfiguration:**

    Lägg till ett omfattande adressavsnitt med:
    
    **Gatuadress:**
    - Adressrad 1 (krävs, max 100 tecken)
    - Adressrad 2 (valfritt, max 100 tecken)
    - Ort (obligatoriskt, listruta med vanliga städer)
    - Delstat/provins (obligatoriskt, listruta)
    - Postnummer (obligatoriskt, formatvalidering)
    &rbrace;- Land (obligatoriskt, standard är USA)
    
    **Valideringsregler:*
    - Postnummer måste matcha delstatsval
    - Adressrad 1 får inte vara tom
    - Ort måste vara en giltig ort för markerat läge
    
    **Användarupplevelse:*
    - Autofyll för adressfält
     - Tydliga etiketter och hjälptext{11111 5}- Mobilvänliga indatafält 
     - Tillgänglighet 
    

**Fråga om fältkonfiguration:**

    Gör @email-fält obligatoriska med realtidsvalidering och anpassat felmeddelande
    
    Lägg till en listruta för @country med alternativ för USA, Kanada, Storbritannien, Tyskland, Frankrike och &quot;Annat&quot;
    
    Konfigurera @phoneNumber-fältet med formatet (XXX) XXX-XXXX och validering
    
    Lägg till ett filöverföringsfält för @resume med PDF- och DOC-begränsningar, max 5MB

## LLM-Enhanced Smart Fields

**När ska du använda:** När du behöver fält med förifyllda alternativ som utnyttjar AI:s kunskapsbas.

**Så här använder du:** Begär fält som kräver omfattande datauppsättningar - AI kan automatiskt fylla i alternativ med hjälp av den inbyggda kunskapen.

### Geografiska fält och platsfält

**Flygplatser och transport:**

    Lägg till en listruta för avgångsflygplatser med alla större internationella flygplatser
    Lägg till fält för ankomstflygplatser med IATA-koder och fullständiga namn
    Skapa ett fält för närmaste flygplats till användarplats
    Lägg till ett urval av tågstationer för europeiska städer

**Administrativa regioner:**

    Lägg till en fullständig lista med delstater i USA med förkortningar
    Skapa en listruta med ISO-koder och fullständiga namn
    Lägg till ett fält för viktiga världsstäder med tidszoner
    Ta med en listruta med kanadensiska provinser och områden
    Lägg till ett fält för grevskap och postområden i Storbritannien

### Affärs- och branschdata

**Företagsklassificeringar:**

    Lägg till ett fält för branschklassificering med NAICS-koder
    Skapa en listruta med affärsenhetstyper (LLC, Corporation, Partnership, etc.)
    Lägg till ett fält för företagsstorlekskategorier (start, SME, enterprise)
    Inkludera avdelningsval för stora organisationer
    Lägg till ett fält för professionella tjänstetyper

**Professionella klassificeringar:**

    Lägg till ett fält för jobbtitlar med vanliga branschroller
    Skapa en listruta med professionella certifieringar per fält
    Inkludera utbildningsnivåer med gradtyper
    Lägg till ett fält för årens upplevelseintervall
    Skapa ett urval för programmeringsspråk och ramverk

### Standarder och bestämmelser

**Finans och juridik:**

    Lägg till ett fält för valutakoder med symboler och valutakurser
    Skapa en listruta med skatte-ID-typer per land
    Ta med ett fält för giltiga dokumenttyper
    Lägg till betalningsmetodalternativ med säkerhetsfunktioner
    Skapa ett val för bankinstitutioner per land

**Tekniska standarder:**

    Lägg till en listruta med filformattyper med tillägg
    Inkludera nätverksprotokollalternativ
    Lägg till ett fält för databastyper och versioner
    Skapa ett val för API-autentiseringsmetoder

### Hälso- och sjukvård

**Medicinska klassificeringar:**

    Lägg till ett fält för medicinska specialiteter
    Skapa en listruta med vanliga läkemedel med generiska namn
    Inkludera ett fält för försäkringsleverantörstyper
    Lägg till ett val för medicinska kontaktrelationer i nödsituationer
    Skapa ett fält för kostrestriktioner och allergier

### Time and Calendar Intelligence

**Datum- och tidsfält:**

    Lägg till ett fält för kontorstid med tidszonshantering
    Skapa en listruta med allmänna helgdagar per land
    Inkludera säsongsalternativ med datumintervall
    Lägg till ett fält för konferensrumsbokning med tillgänglighet
    Skapa ett urval för återkommande mötesmönster

### Produkt- och tjänstekategorier

**E-handelsklassificeringar:**

    Lägg till ett fält för produktkategorier med underkategorier
    Skapa en listruta med leveransmetoder med leveransuppskattningar
    Ta med ett fält för returpolicyalternativ
    Lägg till ett val för kundprioritetsnivåer
    Skapa ett fält för prenumerationsfaktureringscykler

**Exempel på frågor om smarta fält:**

    &quot;Lägg till ett startfält för en flygplats med alla större flygplatser i världen, inklusive IATA-koder och stadsnamn&quot; 
    
    &quot;Skapa ett omfattande branschfält med hjälp av standard-NAICS-klassificering med tekniska underkategorier&quot;
    
    &quot;Inkludera en listruta för professionell certifiering som anpassas baserat på det valda jobbfältet&quot;
    
    &quot;Lägg till ett internationellt telefonnummerfält som formateras baserat på det valda landet&quot;&lbrace;4&quot;Skapa ett urvalsfält för universitet med större institutioner organiserat per land och rankning&quot;
    
    

## Regelskapande och affärslogik

**När du ska använda:** När du måste implementera villkorslogik, verifieringsregler eller affärsprocesser.

**Så här använder du:** Beskriv affärslogiken tydligt och ange villkor och åtgärder.

**Exempelfråga - enkel villkorslogik:**

    Skapa en regel som bara visar panelen @spouseInformation när @maritalStatus är lika med&quot;Gift&quot;

**Exempelfråga - komplexa affärsregler:**

    Implementera omfattande validering av låneansökningar:
    
    **Inkomstvalidering:**
    - Om @annualIncome är mindre än 30000:
    - Visa varningsmeddelande: &quot;Intäkten kan vara otillräcklig för begärt lånebelopp&quot;
    - Kräv ytterligare inkomstdokumentation
    - Visa meddelande: &quot;Ytterligare dokumentation kan behövas&quot;
    - Om @annualIncome är större än 100000:
    - Visa alternativ för premiumtjänster
    - Markera kryssrutan för prioritetsbearbetning
    
    **Åldersbaserad validering:**
    - Om @age är under 18:
    - Visa informationsavsnitt för överordnade/vårdnadshavare
    - Gör överordnad signaturöverföring obligatorisk
    - Ändra skicka-knapptext till &quot;Skicka för granskning&quot;
    - Om @age är 65 eller äldre: 
    - Visa alternativ för Senior Rabatt 
    - Lägg till hjälpmedelsinställningar 

**Regelspecifika frågor:**

    Skapa en **synlighetsregel** som endast visar panelen @spouseInformation när @maritalStatus är lika med&quot;gift&quot; eller&quot;inhemskt partnerskap&quot;
    
    Lägg till **progressiv disposition** där ytterligare frågor visas baserat på tidigare svar. Börja med grundläggande information och visa sedan relevanta uppföljningar
    
    Implementera **smarta standardvärden** där @country-val autoställer in relaterade fält. Tillåt manuell åsidosättning 

## Dataintegrering och överföring

**När ska du använda:** När du behöver ansluta formulär till serverdelssystem, databaser eller externa tjänster.

**Så här använder du:** Börja med grundläggande inskickningsinställningar och lägg sedan till ytterligare integreringar inkrementellt. Ange integreringstyp, dataformatkrav och inställningar för felhantering.

**Exempelfråga - börja med grundläggande överföring:**

    Konfigurera grundläggande formulärsändning för @applicationForm:
    
    **Primär överföring:**
    - Skicka formulärdata till REST-slutpunkt: `/api/v1/applications`
    - Formatera data som JSON
    - Visa slutförandemeddelande: &quot;Ansökan har skickats&quot;
    - Visa felmeddelande om överföringen misslyckas: &quot;Överföringen misslyckades, försök igen&quot;

**Lägg sedan till sekundära åtgärder stegvis:**

    Lägg till e-postmeddelande i @applicationForm: Skicka bekräftelsemeddelande via e-post till @email-adress med programreferensnummer
    
    Lägg till CRM-integrering i @applicationForm: Skapa ny lead-post med @firstName, @lastName, @email och ställ in statusen till &quot;New Application&quot;

**Exempelfråga - standard för flerkanalsöverföring:**

    Konfigurera formuläröverföring med flera datamål:
    
    **Primär överföring:**
    - Skicka formulärdata till REST-slutpunkt: `/api/v1/applications`
    - Inkludera autentiseringsrubrik med API-nyckel
    - Formatera data som JSON med kapslade objekt för adress och anställning
    - Hantera lyckade svar (201) genom att visa tackmeddelande
    
    **&#x200B; Sekundära åtgärder:**
    - Skicka e-postmeddelanden till sökande på @email address
    - Kopiera programdata till spårningssystemet
    - Utlös arbetsflöde för godkännandeprocess
    - Skapa post i CRM med huvudstatusen&quot;Nytt program&quot;
    
    **Felhantering:**
    - Om den primära överföringen misslyckas sparar du data lokalt och försöker igen
    - Visa användarvänligt felmeddelande: &quot;Inlämningen är inte tillgänglig för tillfället&quot;
    - Ange alternativ för att hämta formulärdata som en säkerhetskopia
    - Skicka ett e-postmeddelande till administratörsteamet om misslyckade inskickningar
    
    **Slutfört:*
    - Omdirigera till bekräftelsesida med programreferensnummer
    - Skicka bekräftelsemeddelande med nästa steg
     - Visa beräknad bearbetningstidslinje

**Integrationsspecifika frågor:**

    Anslut det här formuläret till **CRM-system** för att skapa nya leads. Mappa @firstName till FirstName, @email till Email, ange LeadSource till Web Form och Status till New 
    
    Konfigurera **workflow trigger** när formuläret skickas. Skicka alla formulärdata och utlösa godkännandearbetsflöden med hanteringsmeddelande
    
    Konfigurera **databasintegrering** för att spara formulärinskickade formulär som poster. Skapa en ny mapp för varje sändning med överförda dokument 

<!-- ## Import & Convert Existing Forms

**When to use:** When you have existing forms, documents, or designs to transform into modern AEM forms.

**How to use:** Upload your source file and describe the conversion requirements (see [Import Guide](forms-ai-assistant-getting-started.md#2-import-and-convert)).


**Design Import Prompts:**

    Import this **design mockup** and convert it into an adaptive form. Maintain the exact visual design but add proper validation and mobile responsiveness

    Analyze this **image of a paper form** and recreate it digitally. Improve the layout for better mobile experience while keeping all mandatory fields

    Convert this **existing HTML form** to AEM adaptive form format. Preserve all functionality but add AEM-specific features like rules and themes

## Mobile Optimization & Responsiveness

**When to use:** When forms need to work seamlessly across all device types and screen sizes.

**How to use:** Start with basic mobile optimization, then enhance with advanced features. Emphasize mobile-first approach and specify breakpoint behaviors incrementally.

**Example Prompt - Start with Basic Mobile Optimization:**

    Make @contactForm mobile-friendly with:
    
    **Basic Mobile Layout:**
    - Single column layout for all form sections
    - Larger touch targets for buttons and inputs
    - Responsive design that works on phones and tablets

**Then Add Advanced Mobile Features:**

    Enhance @contactForm mobile experience with:
    - Sticky submit button at bottom of screen
    - Touch-friendly date pickers
    - Swipe gestures for multi-step navigation

**Example Prompt - Comprehensive Mobile-First Optimization:**

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

**Mobile-Specific Prompts:**

    Make this form **touch-friendly** with larger buttons and simplified navigation for mobile users

    Optimize form for **tablet users** with appropriate field sizes and navigation patterns

    Add **swipe gestures** for multi-step form navigation on mobile devices

## Accessibility & Compliance

**When to use:** When forms need to meet accessibility standards (WCAG) or compliance requirements.

**How to use:** Specify the required compliance level and any specific accessibility features needed.

**Example Prompt - Basic Accessibility:**

    Make @contactForm accessible with:
    
    **Basic Accessibility:**
    - Proper ARIA labels for all form fields
    - Keyboard navigation support
    - High contrast color scheme
    - Screen reader compatibility
    - Focus indicators for all interactive elements

**Example Prompt - Advanced Accessibility:**

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

**Accessibility-Specific Prompts:**

    Add **screen reader support** to this form with proper ARIA labels and announcements

    Implement **keyboard navigation** for all form interactions and navigation elements

    Ensure **color contrast** meets WCAG AA standards for all text and interactive elements  

## Performance Optimization

**When to use:** When forms need to load quickly and perform well under various conditions.

**How to use:** Specify performance requirements and optimization strategies.

**Example Prompt - Basic Performance:**

    
Optimize @contactForm for performance:

**Loading Optimization:**

- Lazy load non-critical form sections
- Minimize initial bundle size
- Optimize images and assets
- Enable caching for static resources
    

**Example Prompt - Advanced Performance:**

    
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
    

**Performance-Specific Prompts:**

    
Optimize form **loading speed** by implementing progressive loading and asset optimization
    

    
Add **auto-save functionality** to prevent data loss during form completion
    

    
Implement **offline support** so users can complete forms without internet connection
    

## Testing & Quality Assurance

**When to use:** When forms need comprehensive testing to ensure reliability and user satisfaction.

**How to use:** Specify testing scenarios, validation requirements, and quality metrics.

**Example Prompt - Basic Testing:**

    
Add comprehensive testing for @contactForm:

**Functional Testing:**

- Test all form field validations
- Verify submit functionality works correctly
- Test error handling and user feedback
- Validate conditional logic and rules
    

**Example Prompt - Advanced Testing:**

    
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
    

**Testing-Specific Prompts:**

    
Add **automated testing** for all form validations and submit functionality
    

    
Implement **user acceptance testing** scenarios for complete form workflows
    

    
Set up **performance monitoring** to track form load times and user interactions
    
-->

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

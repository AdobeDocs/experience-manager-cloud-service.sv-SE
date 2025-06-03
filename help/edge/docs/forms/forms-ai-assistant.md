---
title: AI Assistant för AEM Forms (Forms Experience Builder)
description: Skapa kraftfulla formulär snabbare med Form Fragments
feature: Edge Delivery Services
hide: true
hidefromtoc: true
role: Admin, Architect, Developer
source-git-commit: d3ade6ee9216b44b55d6808d8acffe83f1e263c9
workflow-type: tm+mt
source-wordcount: '2061'
ht-degree: 0%

---


# AI Assistant för AEM Forms (Forms Experience Builder)

>[!NOTE]
>
>
> AI-assistenten för AEM Forms (Forms Experience Builder) är tillgänglig under **programmet** för tidiga användare. Om du är intresserad kan du skicka ett snabbt e-postmeddelande från din arbetsadress till mailto:aem-forms-ea@adobe.com och begära åtkomst till funktionen.

>[!IMPORTANT]
>
> **Dokumentation som kan ändras**: Dokumentationen testas för närvarande mot produkten och kan uppdateras och revideras. Funktioner, kommandon och exempel kan ändras när AI Assistant för AEM Forms fortsätter att utvecklas under det program som man introducerar tidigt.

AI Assistant för AEM Forms (Forms Experience Builder) förbättrar redigeringsupplevelsen genom att effektivisera arbetet med att skapa formulär med hjälp av naturliga språkinställningar. I Forms Management UI, Adaptive Forms Editor och Universal Editor kan du skapa smartare och snabbare genom att stödja både skapande- och konfigurationsåtgärder. Den här guiden hjälper dig att komma igång och få ut det mesta av dess funktioner.

## Komma igång

Innan du gör en djupdykning ska vi gå igenom grunderna i hur man får tillgång till och interagerar med AI-assistenten.

### Åtkomst till AI-assistenten

Du kan komma åt AI-assistenten från tre olika platser i AEM Forms:

1. **Forms Management UI**
   - Navigera till: Adobe Experience Manager > Forms > Forms &amp; Documents
   - Leta efter ikonen för AI-assistenten till vänster i gränssnittet
   - Klicka på ikonen för att öppna AI-assistentpanelen

   ![Ikon för AI-assistenten*](/help/edge/docs/forms/assets/forms-manager.gif)

2. **Adaptiv Forms Editor**
   - Navigera till: Adobe Experience Manager > Forms > Forms &amp; Documents
   - Markera och öppna ett formulär för redigering
   - Klicka på ikonen AI-assistenten i redigeringsgränssnittet

   ![Ikon för AI-assistenten*](/help/edge/docs/forms/assets/adaptive-forms-editor.gif)

3. **Universell redigerare**

   - Navigera till: Adobe Experience Manager > Forms > Forms &amp; Documents
   - Leta efter ikonen för AI-assistenten till vänster i gränssnittet
   - Klicka på ikonen AI-assistenten i redigeringsgränssnittet

AI-assistenten anpassar funktionaliteten baserat på din aktuella plats och dina aktuella uppgifter, vilket ger relevant hjälp för varje sammanhang.

### Så här interagerar du:

- Skriv bara in din förfrågan på ditt naturliga språk.
- Använd `/` om du vill visa en lista med tillgängliga kommandon eller snabbåtgärder.
- Referera till specifika formulärfält med `@fieldName` (t.ex. `@firstName`, `@emailAddress`) när du vill att assistenten ska konfigurera eller uppdatera det aktuella fältet.
- Du kan överföra bilder, PDF-filer, Figma-filer eller andra designresurser så att AI Assistant lättare kan förstå dina behov.


### Snabbstart

Kom igång snabbt med vår introduktionsvideo:

>[!VIDEO](https://video.tv.adobe.com/v/3463164/)


I den här videon beskrivs hur du startar assistenten i alla miljöer, grundläggande interaktion och en översikt över dess funktioner.

## Kommandoreferens för AI-assistenten

| Kommando | Beskrivning | Syfte | Användningskontext | Exempel | Viktiga funktioner |
|---------|-------------|---------|---------------|----------|--------------|
| /create-form | Starta ett nytt formulär i Forms Management UI eller Forms Editor | Börjar skapa ett helt nytt formulär från grunden | Forms Management UI, Adaptive Forms Editor | /create-form customer feedback survey based on attached PDF | Innehåller alternativ för formulärstrukturen och skapar formuläret. **Stöder bilagor** för designreferenser |
| /add-form | Lägg till ett nytt formulär i Universal Editor | Lägger till ett nytt formulärblock eller en ny komponent i Universal Editor | Universal Editor för Edge Delivery Services | /add-form contact form with name and email | Infogar formulärblock, som fungerar med blockbaserad redigering. **Stöder bilagor** för layoutvägledning |
| /update-layout | Ändra formulärets layout till dragspels-, tabbbaserad-, guide- eller enkelsidig design | Ändrar den övergripande strukturlayouten och navigeringsmönstret | Alla redigeringsmiljöer | /update-layout guide med 3 steg | Dragspel, flikar, guide, svarsalternativ för en sida |
| /update-field | Ändra egenskaper och konfiguration för befintliga formulärfält | Ändrar fältattribut som etiketter, validering, formatering, beteende | Alla redigeringsmiljöer | /update-field @email to required with validation | Etiketter, valideringsregler, fälttyper, standardvärden, synlighet. **Stöder bilagor** för fältdesignexempel |
| /create-rule | Skapa dynamiskt beteende och villkorlig logik för formulär | Implementerar affärslogik, beräkningar, villkorsstyrd interaktion | Alla redigeringsmiljöer | /create-rule visa @spouseName om @maritalStatus är lika med &quot;Gift&quot; | Villkorlig synlighet, beräkningar, validering, värdeinställning |
| /create-panel | Skapa en ny panel (behållare för gruppering av relaterade fält) | Lägger till strukturella behållare för att ordna formulärfält logiskt | Alla redigeringsmiljöer | /create-panel Personal Information with name, email, phone | Fältgruppering, rubriker, layoutalternativ, fällningar som kan komprimeras. **Stöder bilagor** för panellayoutreferenser |
| /add-panel | Konvertera en bild till en formulärpanel i Universell redigerare | Använder AI för att analysera överförda bilder och konvertera till strukturerade formulärpaneler | Universal Editor | /add-panel from uploaded form image | Bildigenkänning, visuell-till-funktionell konvertering, bibehållen layout. **Kräver bifogade filer** för bildanalys |
| /configure-submit | Ställ in formuläröverföringsåtgärder och datahantering | Definierar vad som händer när användare skickar det ifyllda formuläret | Alla redigeringsmiljöer | /configure-submit to send email to `support@company.com` | E-post, REST API, arbetsflöden, kalkylblad, databaser, Power Automate |
| /help | Hjälp och dokumentation i AI-assistenten | Här finns sammanhangsbaserad hjälp, vägledning och svar om AEM Forms | Alla redigeringsmiljöer | /help how do I create multi-step forms? | Funktionsförklaringar, guider, metodtips, felsökning |

### Kommandokategorier

| Kategori | Kommandon | Exempel på primärt bruk |
|----------|----------|-------------------|
| Skapa formulär | /create-form, /add-form | Starta nya formulär, lägga till formulärblock |
| Struktur och layout | /update-layout, /create-panel, /add-panel | Ordna formulärstruktur, visuell design |
| Fälthantering | /update-field | Konfigurera enskilda formulärelement |
| Logic &amp; Rules | /create-rule | Lägga till dynamiskt beteende och validering |
| Inlämning | /configure-submit | Ställa in datahantering och arbetsflöden |
| Support | /help | Få hjälp och dokumentation |

### Syntaxriktlinjer

| Element | Format | Exempel | Anteckningar |
|---------|--------|---------|-------|
| Kommandon | /command-name | /create-form | Börja alltid med snedstreck |
| Fältreferenser | @fieldName | @email, @firstName | Använd symbolen @ för befintliga fält |
| Naturligt språk | Kommando + beskrivning | /create-rule show field if condition | Kombinera kommandon med beskrivande text |
| Flera åtgärder | Separata kommandon | /create-panel then /update-layout | Använd ett kommando i taget |


### Miljöspecifika funktioner

| Miljö | Tillgängliga kommandon | Specialfunktioner |
|-------------|-------------------|------------------|
| Forms Management UI | /create-form, /help | Framtagning och hantering på formulärnivå |
| Adaptiv Forms Editor och Universal Editor | Alla kommandon | Fullständig funktionsuppsättning, detaljerad konfiguration |



### Fältreferenssyntax (sammanhangsberoende element)

Använd `@fieldName` för att referera till befintliga fält:

- `@firstName` - fältet för förnamn
- `@email` - E-postfält
- `@phoneNumber` - Telefonnummerfält
- `@dateOfBirth` - Födelsedatum

### Komponenttyper

Den här listan innehåller vanliga komponenttyper. AI kan identifiera variationer eller mer specialiserade typer, men med dessa exakta termer får du bäst resultat:

- `text input` - Textfält med en rad
- `text area` - Flerradigt textfält
- `dropdown` - Välj lista
- `checkbox` - En kryssruta
- `checkbox group` - flera kryssrutor
- `radio group` - Grupp med alternativknappar
- `date picker` - datumval
- `file upload` - Bifogad fil
- `panel` - Behållare för grupperingsfält


## Exempel på kärnfunktioner och utökad fråga

AI-assistenten kan hantera en mängd olika kommandon. Här är några exempel som illustrerar dess styrka. Kom ihåg att använda exakta termer för komponenter som &quot;panel&quot;, &quot;textinmatning&quot;, &quot;kryssruta&quot; osv.

| Funktionskategori | Beskrivning | Exempelfrågor |
| ------------------------- | --------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Skapa formulär** | Starta ett nytt formulär från grunden eller baserat på en beskrivning. | `Create a new form titled 'Employee Onboarding'.` <br> `Generate a customer feedback form with fields for name, email, rating (1-5 stars), and comments.` <br> `Start a simple contact form with name, email, and message fields.` <br> `Design a multi-page registration form for an event.` <br> `Create a form based on the attached PDF template.` |
| **Importera design** | Konvertera en befintlig design (bild, Figma, PDF) till ett AEM-formulär. | `Import the form design from this uploaded PDF file.` <br> `Convert the uploaded Figma design into an adaptive form, focusing on the 'User Profile' frame.` <br> `Use this JPEG image of our old paper form to create a new digital version.` <br> `Create a form based on the layout of the attached PNG.` <br> `Recreate the form shown in the attached screenshot with modern styling.` |
| **Lägger till komponenter och paneler** | Lägg till olika formulärfält och strukturella behållare (paneler). | `Add a text input field for 'First Name'.` <br> `Add a 'Personal Details' panel with fields for full name, date of birth, and phone number.` <br> `Insert a checkbox group for 'Interests' with options: Technology, Sports, Music.` <br> `Add a file upload component for 'Resume'.` <br> `Create a repeatable panel named 'WorkExperience' with fields for company, title, and dates.` <br> `Add a panel matching the layout shown in the attached design mockup.` |
| **Layoutjusteringar** | Ändra strukturen och utseendet på formulärlayouten. | `Change the 'Personal Details' panel to a two-column layout.` <br> `Set the overall form layout to a wizard (multi-step) navigation.` <br> `Make the header section span the full width of the form.` <br> `Adjust the spacing between fields in the 'Address' panel to be compact.` <br> `Align all field labels to the left.` <br> `Update the form layout to match the attached wireframe.` |
| **Regelskapande och logik** | Implementera dynamiskt beteende, beräkningar och villkorlig synlighet. | `Make the 'Spouse Name' field visible only if 'Marital Status' is selected as 'Married'.` <br> `Calculate the 'Total Amount' by multiplying @quantity and @price.` <br> `Enable the submit button only when the @termsAndConditions checkbox is checked.` <br> `Set the value of @countryCode to '+1' if @country is 'United States'.` <br> `If @age is less than 18, show a message 'Must be 18 or older'.` |
| **Uppdatering av fältegenskaper** | Ändra attribut för specifika formulärfält som etiketter, platshållare osv. | `Change the label of @email to 'Primary Email Address'.` <br> `Set the @comment field to be a multi-line text area.` <br> `Make the @phoneNumber field mandatory.` <br> `Add placeholder text 'Enter your ZIP code' to the @zipCode field.` <br> `Change the @country field to a dropdown and populate it with: USA, Canada, UK, Germany.` <br> `Update the help description for @password to 'Must include an uppercase letter, a number, and be at least 8 characters long.'` <br> `Set the maximum length of the @username field to 15 characters.` <br> `Configure the @dateOfBirth field to use a date picker.` <br> `Style the @email field to match the design shown in the attached image.` |
| **Skicka åtgärder** | Definiera vad som ska hända när en användare skickar formuläret. | `Configure the form to submit data to the REST endpoint /api/v2/application-submit.` <br> `Set up an email submission to hr@example.com and sales@example.com on successful submission.` <br> `Trigger an AEM workflow named 'NewLeadProcessing' when this form is submitted.` <br> `On submit, redirect the user to a thank you page at /content/thankyou.html.` |
| **Tema** | Använd befintliga AEM Forms-teman för att utforma formuläret. | `Apply the 'Modern Business' theme to this form.` <br> `Switch to the 'Accessible Dark' theme.` <br> `Revert to the default canvas theme.` <br> `Apply styling that matches the brand guidelines shown in the attached style guide.` |
| **Navigering och struktur** | Lägg till navigeringselement eller ordna om delar av formuläret. | `Add a 'Next' button to the current panel and a 'Previous' button to the next panel.` <br> `Create a Table of Contents based on the form's panels.` <br> `Move the 'Address' panel to be before the 'Contact Information' panel.` |
| **Validering** | Ange specifika verifieringsregler för fält. | `Set a regex pattern for the @employeeID field to be 'EMP\d{5}'.` <br> `Ensure the @age field only accepts numeric values between 18 and 99.` <br> `Validate the @email field to ensure it is a valid email format.` |
| **Granska plan** (Universal Editor) | Förhandsgranska assistentens föreslagna ändringar före körning. | `Add a contact form with fields for name, email, subject, and message.` (Assistenten visar en plan med komponenter och egenskaper som den skapar och klickar sedan på Använd). <br> `Create a form based on the attached design file.` (Assistenten analyserar den bifogade filen och visar en detaljerad plan innan implementeringen). |

## Bästa praxis för optimala resultat

För att få ut så mycket som möjligt av AI-assistenten bör du tänka på följande:

- **Starta enkelt, skapa stegvis:** Börja med mindre, specifika kommandon (t.ex. &quot;Lägg till textinmatning för &quot;Förnamn&quot;&quot;) i stället för alltför komplexa flerstegsbegäranden från början.
- **Använd AEM Forms Terminologi:** Använd termer som &quot;panel&quot;, &quot;textinmatningsfält&quot;, &quot;kryssrutegrupp&quot;, &quot;skicka-åtgärd&quot;, &quot;regel&quot; osv. för att få bättre förståelse av assistenten.
- **Referensfält tydligt:** När du konfigurerar befintliga fält ska du använda `@fieldName`-syntaxen (t.ex. `Make @firstName mandatory`).
- **Granska planer** Granska alltid planer noggrant för ändringar som har föreslagits av assistenten i den universella redigeraren innan du klickar på Använd.
- **Validera manuellt:** När assistenten har gjort ändringar ska du alltid förhandsgranska och testa formuläret för att se om det fungerar som det ska. AI är ett kraftfullt verktyg, men slutlig validering är avgörande.
- **Upprepa och förfina:** Om den första prompten inte ger exakt resultat kan du försöka med att omformulera eller dela upp förfrågan i mindre steg.
- **Ge feedback:** Använd den inbyggda feedbackfunktionen för att hjälpa assistenten att lära sig och förbättra materialet (se avsnittet Feedback &amp; Support).

## Produkthjälp med AI Assistant

AI Assistant för AEM Forms är inte bara till för att bygga upp. Den kan även hjälpa dig att lära dig mer, förstå och använda olika funktioner i AEM Forms.

### Hjälpavsnitt som stöds

Du kan ställa frågor till assistenten:

- &quot;Hur skapar jag en ny anpassningsbar form från grunden?&quot;
- &quot;Vad är en panel i Adaptive Forms och hur används den?&quot;
- &quot;Förklara hur du använder ett tema i ett formulär.&quot;
- &quot;Vilka layouttyper stöds för formulär och paneler?&quot;
- &quot;Hur konfigurerar jag olika skicka-åtgärder som att skicka ett e-postmeddelande?&quot;
- &quot;Kan du vägleda mig när jag använder en Figma-design för att skapa ett formulär?&quot;
- &quot;Vilket är det bästa sättet att skapa ett flerstegsformulär?&quot;

### Så här frågar du efter hjälp:

1. Öppna AI-assistenten i Forms Management UI eller Adaptive Forms Editor.
2. Skriv din fråga på ett naturligt språk (t.ex.&quot;Hur lägger jag till en repeterbar panel?&quot;).
3. Assistenten kommer att svara med:
   - Stegvisa instruktioner.
   - Förklaringar av AEM Forms koncept.
   - Länkar till relevant dokumentation för Adobe Experience League, om tillämpligt.

### Tips för att få hjälp:

- **Var specifik:** Ställ en tydlig fråga i taget.
- **Använd nyckelord:** Inkludera nyckelord som är relevanta för AEM Forms-funktioner eller gränssnittselement (t.ex. &quot;adaptiv formulärredigerare&quot;, &quot;regelredigerare&quot;, &quot;tema&quot;).
- **Försök med att upprepa vid behov:** Om assistenten inte förstår eller tillhandahåller den önskade informationen kan du försöka med att förenkla frågan eller använda andra termer.


## Felsökning av vanliga problem

- **Assistenten svarar inte:**
   - Kontrollera att du arbetar aktivt i en miljö som stöds (Forms Management UI, Adaptive Forms Editor eller Universal Editor).
   - Kontrollera din internetanslutning.
   - Stäng AI-assistentpanelen och öppna den igen.

- **Inkorrekta eller oväntade svar:**
   - Gör om din begäran så att den blir mer specifik eller enklare.
   - Dela upp en komplex begäran i mindre, enskilda kommandon.
   - Se till att du använder AEM Forms standardterminologi.

- **Problem med designimport (PDF/Figma/Image):**
   - Kontrollera att designfilen är tydlig, välstrukturerad och läsbar.
   - Kontrollera att filformatet stöds (PDF, Figma link, vanliga bildtyper som PNG, JPG).
   - För Figma måste du se till att ramen du riktar dig mot är tydligt definierad och tillgänglig.

- **Fältet `@fieldName` känns inte igen:**
   - Dubbelkontrollera det exakta namnet på fältet i formuläret. Fältnamn är skiftlägeskänsliga och måste matcha exakt.
   - Kontrollera att fältet redan finns om du försöker ändra det.


## Feedback och support

Din input är ovärderlig för den kontinuerliga förbättringen av AI-assistenten.

- **Ge feedback:** Använd det inbyggda kommandot eller knappen **Ge feedback** i AI Assistant-gränssnittet för att dela med dig av dina upplevelser, rapportera problem eller föreslå förbättringar. (Du kan t.ex. skriva `/feedback` eller leta efter en feedback-ikon).
- **Officiell support:** Om du har allvarliga problem eller behöver mer hjälp kan du kontakta Adobe officiella supportkanaler eller få hjälp av de supportkontakter som har kontaktats av din organisation.


## Relaterat innehåll

[AEM Forms AI Assistant - promptbibliotek](/help/edge/docs/forms/ai-assistant-prompt-library.md)

## Arbeta med bifogade filer

AI Assistant har stöd för bifogade filer för att förbättra formulärframtagningen och konfigurationen. Du kan bifoga olika filtyper för att ge visuell kontext, designreferenser eller befintliga formulär som ska konverteras.

### Bilagetyper som stöds

| Filtyp | Användningsexempel | Kommandon som stöder bifogade filer | Exempel |
|-----------|-----------|-----------------------------------|----------|
| **Bilder** (PNG, JPG, JPEG, GIF) | Formulärlayoutreferenser, UI-dummies, inskannade pappersformulär | /create-form, /add-form, /create-panel, /add-panel, /update-field | Överför en skärmbild av önskad layout |
| **PDF-filer** | Befintliga formulär att konvertera, designa specifikationer | /create-form, /add-form, /create-panel, /add-panel | Konvertera PDF-ansökningsformulär |
| **Figma-filer** | Utforma systemreferenser, gränssnittsprototyper | /create-form, /add-form, /create-panel | Importera designramar från Figma |
| **Designfiler** (Skiss, Adobe XD-export) | Visuella designreferenser | /create-form, /add-form, /create-panel | Referenssystemkomponenter för design |

### Använda bifogade filer

1. **Koppla före eller med ditt kommando:**

   - Klicka på bilageikonen i AI Assistant-gränssnittet
   - Välj dina filer på enheten
   - Skriv det kommando som refererar till den bifogade filen

2. **Referensbilagor i kommandon:**

   ```
   /create-form based on the attached PDF application form
   /add-panel using the layout shown in the uploaded image
   /create-panel following the design in the attached Figma file
   /update-field @email to match the style in the attached screenshot
   ```

3. **Flera bifogade filer:**

   - Du kan bifoga flera filer för jämförelse eller referens
   - Ange vilken bilaga som ska användas: &quot;med den första bifogade bilden&quot; eller &quot;baserad på PDF-filen&quot;

### Bästa praxis för bifogade filer

- **Tydliga bilder med hög kvalitet:** Se till att överförda bilder är tydliga och läsbara för bättre AI-analys
- **Relevanta filnamn:** Använd beskrivande filnamn för att förstå kontexten i AI
- **Enkelt fokus:** Varje bifogad fil ska fokusera på en viss aspekt (layout, fältdesign osv.)
- **Format som stöds:** Håll dig till vanliga format (PNG, JPG, PDF) för bästa kompatibilitet
- **Filstorlek:** Behåll bifogade filer under 10 MB för optimal bearbetningshastighet

### Exempel på arbetsflöden för bifogade filer

**Konverterar ett pappersformulär:**

1. Skanna in eller fotografera pappersformuläret tydligt
2. Överför bildfilen
3. Använd kommando: `/create-form based on the attached form image, converting all fields to digital equivalents`

**Matchande ett designsystem:**

1. Exportera eller ta skärmdumpar relevanta designkomponenter
2. Koppla designreferensen
3. Använd kommando: `/create-panel following the visual style and layout shown in the attached design`

**Fältformateringsreferens:**

1. Bifoga skärmbild av önskat fältutseende
2. Använd kommando: `/update-field @email to match the styling and layout shown in the attached image`

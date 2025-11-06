---
title: Komma igång med Forms Experience Builder
description: Lär dig grunderna i hur du skapar ditt första AI-baserade formulär med Forms Experience Builder. Stegvis självstudiekurs med exempel och bästa praxis.
hide: true
index: false
hidefromtoc: true
role: Admin, Developer
exl-id: c4f838bc-a001-48e7-afaa-c2ff9034f5d4
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1133'
ht-degree: 0%

---

# Komma igång med Forms Experience Builder {#getting-started-forms-experience-builder}

Forms Experience Builder revolutionerar formulärframtagningen genom att utnyttja AI för att omvandla naturliga språkbeskrivningar till fullt fungerande digitala formulär. Den här guiden hjälper dig att skapa ditt första formulär och förstå de centrala koncept som gör Forms Experience Builder kraftfullt.

## Vad är Forms Experience Builder? {#what-is-forms-experience-builder}

Forms Experience Builder är ett AI-drivet formulärverktyg som gör att ni kan skapa avancerade digitala formulär på ett konversationsspråk. I stället för att dra-och-släpp-gränssnitt eller komplex kodning beskriver du bara vad du vill ha och AI skapar formuläret åt dig.

**Nyckelfunktioner:**

* **Skapa formulär för naturligt språk** - Beskriv dina formulärkrav på vanlig engelska

* **Intelligent import och konvertering** - Omvandla befintliga dokument till interaktiva formulär

* **Skapa smarta fält** - AI-baserade fält med förifyllda alternativ

* **Automatisering av affärslogik** - Skapa villkorsregler och validering via konversation

* **Systemintegrering** - Koppla formulär till befintliga arbetsflöden

## Förutsättningar {#prerequisites-getting-started}

Kontrollera att du har:

* **Åtkomst till Forms Experience Builder** - tillgänglig via programmet för tidig åtkomst
* **AEM Forms as a Cloud Service** - Designmiljö för produktion med adaptiva Forms Core-komponenter
* **Grundläggande förståelse** - Förståelse med formulärkoncept och affärskrav

Detaljerade tekniska installationskrav och miljökonfigurationer finns i [Distribuera och konfigurera Forms Experience Builder](deploy-forms-experience-builder.md).

## Olika sätt att skapa formulär {#two-ways-to-create-forms}

När du har använt Forms-guiden för att välja en [mall för kärnkomponenter](/help/forms/creating-adaptive-form-core-components.md) eller [Edge Delivery Services](/help/edge/docs/forms/universal-editor/create-forms.md) , tema och andra alternativ, har Forms Experience Builder två primära metoder för att skapa formulär:

### &#x200B;1. Skapa från grunden {#create-from-scratch}

Skapa formulär med naturliga språkbeskrivningar av era behov.

**När ska du använda:**

* Bygga nya formulär utifrån krav

* Skapa blanketter för nya affärsprocesser

* När du har tydliga specifikationer men inga befintliga dokument

**Exempel:**

    Skapa ett formulär för kundfeedback med:
    - Produktklassificering (1-5 stjärnor)
    - Kommentarsfält för detaljerad feedback
    - E-post från kund (valfritt)
     - Skicka till e-postmeddelande

>[!VIDEO](https://video.tv.adobe.com/v/3473104)



### &#x200B;2. Importera och konvertera {#import-and-convert}

Förvandla befintliga dokument till interaktiva digitala formulär.

Innan du använder det här alternativet ska du överföra din PDF-fil eller en bild av formuläret. PDF kan vara ett AcroForm- eller XFA-baserat PDF-formulär. För [andra typer av PDF forms](https://experienceleague.adobe.com/en/docs/experience-manager-learn/forms/document-services/pdf-forms-and-documents) använder du alternativet [Förbered formulär](https://helpx.adobe.com/in/acrobat/using/creating-distributing-pdf-forms.html) i Adobe Acrobat för att konvertera dem till ett AcroForm

**När ska du använda:**

* Konverterar befintlig PDF forms

* Modernisera pappersbaserade processer

* När du har formulärdesigner att förbättra

**Exempel:**

    /create-form konvertera den bifogade PDF-filen till ett adaptivt formulär 

>[!VIDEO](https://video.tv.adobe.com/v/3474042)


## Ditt första formulär: Stegvis självstudiekurs {#first-form-tutorial}

Låt oss skapa ett enkelt kontaktformulär för att förstå det grundläggande arbetsflödet.

### Steg 1: Börja med en enkel beskrivning {#step-1-simple-description}

Börja med en grundläggande formulärbeskrivning:

    Skapa ett enkelt kontaktformulär med namn, e-post och meddelandefält

Då skapas ett formulär med tre viktiga fält.

![Formulär med tre viktiga fält - skapat med en uppmaning om naturligt språk](/help/forms/assets/forms-experience-builder-contact-us-form.png)

### Steg 2: Lägg till validering och krav {#step-2-add-validation}

Förbättra formuläret med valideringsregler:

    Gör obligatoriska fält för @name och @email med lämplig validering

Symbolen `@` refererar till specifika fält för riktade ändringar.

![Utökad validering i formulärupplevelsebyggaren med hjälp av en fråga om naturligt språk](/help/forms/assets/forms-experience-builder-contact-us-form-add-validation.png)


### Steg 3: Förbättra användarupplevelsen {#step-3-improve-ux}

Lägg till användbar platshållartext och vägledning:

    Lägg till platshållartext: @name &quot;Ditt fullständiga namn&quot;, @email &quot;your.email@company.com&quot;, @message &quot;Berätta för oss hur vi kan hjälpa&quot;

![Valideringen har lagts till med hjälp av naturliga språkuppmaningar i formulärupplevelsebyggaren](/help/forms/assets/forms-experience-builder-contact-us-form-add-placeholder.png)

### Steg 4: Lägg till avancerade funktioner {#step-4-advanced-features}

Inkludera ytterligare funktioner:

    Lägg till två listrutor
    
    - queryType med alternativ: General question, &quot;Support Request&quot;, &quot;Sales Inquiry&quot;, &quot;Partnership&quot;
    
    - EmergencyLevel med alternativ (Low, Medium, High)


![En listrutekomponent har lagts till med hjälp av naturliga språkuppmaningar i formulärupplevelseverktyget](/help/forms/assets/forms-experience-builder-contact-us-form-add-dropdown.png)


### Steg 5: Implementera villkorsstyrd logik {#step-5-conditional-logic}

Skapa smart, sammanhangsberoende beteende genom att lägga till regler som:

    Dölj listrutan @trängningsnivå vid formulärinläsning
    Visa listrutan @trängningsnivå (låg, Medium, hög) bara när @QueryType är lika med &quot;Supportförfrågan&quot;

Det här är två separata regler: den ena döljer listrutan för brådskande ärenden när formuläret läses in och den andra visar den bara när frågetypen är&quot;Supportförfrågan&quot;. Du måste skapa varje regel med en separat fråga. Det går bara att skapa en regel åt gången.

## Förstå AI-konversationen {#ai-conversation-approach}

Forms Experience Builder har ett konversationsgränssnitt där man kan

### Referensfält med @-symboler {#reference-fields}

Använd `@fieldName` för att referera till specifika fält:

    Gör @email till ett obligatoriskt fält
    Lägg till validering i @phoneNumber för amerikanskt format
    Ändra @submitButton-text till &quot;Skicka meddelande&quot;

>[!VIDEO](https://video.tv.adobe.com/v/3474043)


### Använda naturliga språkkommandon {#natural-language-commands}

Beskriv vad du vill ha på engelska:

    - Lägg till ett avsnitt för företagsinformation
    - Skapa en listruta för avdelningsval
     - Inkludera en filöverföring för CV
    - Konfigurera e-postmeddelanden när formuläret skickas

### Bygg stegvis {#build-incrementally}

Börja enkelt och lägg till komplexitet gradvis:

1. **Grundläggande struktur** - Skapa de viktigaste fälten först
2. **Lägg till validering** - Implementera obligatoriska fält och formatvalidering
3. **Förbättra användargränssnittet** - Lägg till platshållare, hjälptext och format
4. **Implementeringslogik** - Lägg till villkorsregler och affärslogik
5. **Konfigurera överföring** - Konfigurera formulärbearbetning och meddelanden


## Vanliga formulärmönster {#common-form-patterns}

### Kontakt- och feedbackformulär {#contact-feedback-forms}

**Grundläggande kontaktformulär:**

    Skapa ett kontaktformulär med:
    - Namn (obligatoriskt)
    - E-postadress (obligatoriskt, validerat)
    - Listrutan Ämne (Allmänt, Support, Försäljning, Partnerskap)
    - Meddelande (obligatoriskt, flera rader)
    - Skicka-knapp

**Formulär för kundfeedback:**

    Skapa ett formulär för kundfeedback med:
    - Produktklassificering (1-5 stjärnor)
    - Kommentarsfält för detaljerad feedback
    - E-post från kund (valfritt)
     - Skicka till e-postmeddelande

### Registrerings- och introduktionsformulär {#registration-onboarding-forms}

**Användarregistrering:**

    Skapa ett användarregistreringsformulär med:
    - Personlig information (namn, e-postadress, telefon)
    - Kontoinställningar (nyhetsbrev, meddelanden)
    - Villkor för godkännande
    - Lösenordsskapande med styrkevalidering

**Anställningskoncern:**

    Skapa ett formulär för anställdas introduktion med:
    - Personlig information och kontaktinformation
    - Anställningsinformation och startdatum
    - Dokumentöverföringar (CV, ID, skatteformulär)
    - Val av förmåner och inställningar

### Undersöknings- och bedömningsformulär {#survey-assessment-forms}

**Kundnöjdhetsundersökning:**

    Skapa en kundnöjdhetsundersökning med:
    - Samlat omdöme (skala 1-10)
    - Kategoribetyg (produkt, tjänst, support)
    - Öppen feedback-sektion
     - Demografisk information (valfritt)

**Kompetensbedömning:**

    Skapa ett formulär för kompetensbedömning med:
    - Kompetenskategorier med kunskapsnivåer 
     - Upplevelsevaraktighet för varje kompetens
    - Certifierings- och utbildningsinformation
    - Självutvärdering och mål

## Testning och validering {#testing-validation}

### Testa alltid formulären {#always-test-forms}

Innan du distribuerar något formulär:

1. **Testa alla fält** - Kontrollera att valideringen fungerar korrekt

2. **Verifiera villkorsstyrd logik** - Kontrollera att reglerna utlöses korrekt

3. **Testa överföringen** - Bekräfta att data har bearbetats korrekt

4. **Verifiera på olika enheter** - Säkerställ mobilkompatibilitet

5. **Granska med intressenter** - Få feedback från slutanvändare

### Vanliga valideringsmönster {#validation-patterns}

**E-postvalidering:**

    Lägg till validering av e-postformat i fältet @email

**Validering av telefonnummer:**

    Lägg till validering av amerikanskt telefonnummerformat i @phoneNumber

**Åldersvalidering:**

    Lägg till åldersvalidering: måste vara 18 eller äldre för @dateOfBirth

**Validering av filöverföring:**

    Lägg till filtypsvalidering: endast PDF, DOC, DOCX tillåts för @resume
    Lägg till filstorleksgräns: maximalt 5 MB för @resume

## Nästa steg {#next-steps}

Nu när du förstår grunderna kan du utforska följande avancerade ämnen:

* **[LLM-förbättrade smarta fält](forms-experience-builder-llm-smart-fields.md)** - Skapa fält med förifyllda alternativ med hjälp av AI-kunskaper
* **[Skapa formulär med AI](forms-experience-builder-prompt-examples-library.md)** - Avancerade promptmönster och exempel
* **[Intelligent import och konvertering](intelligent-import-conversion.md)** - Omvandla befintliga dokument till formulär
* **[Inlämning och integrering av formulär](form-submission-integration.md)** - Koppla formulär till affärssystemen


## Relaterade artiklar

* [Forms Experience Builder - översikt](product-overview.md)
* [LM-förbättrade smarta fält](forms-experience-builder-llm-smart-fields.md)
* [Skapa formulär med AI-funktioner](forms-experience-builder-prompt-examples-library.md)
* [Intelligent import och konvertering](intelligent-import-conversion.md)
* [Inlämning och integration av blanketter](form-submission-integration.md)
* [Frågor och svar](forms-experience-builder-frequently-asked-questions.md)

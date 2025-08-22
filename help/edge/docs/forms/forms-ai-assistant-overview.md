---
title: Forms Experience Builder
description: Skapa kraftfulla formulär snabbare med Form Fragments
feature: Edge Delivery Services
hide: true
index: false
hidefromtoc: true
role: Admin, Architect, Developer
source-git-commit: 9996bc602ae6169dd1aade622d5dbc5b1addeb54
workflow-type: tm+mt
source-wordcount: '1113'
ht-degree: 0%

---


# Introduktion till Forms Experience Builder

>[!IMPORTANT]
>
> **Dokumentation som kan ändras**: Dokumentationen testas för närvarande mot produkten och kan uppdateras och revideras. Funktioner, kommandon och exempel kan ändras allt eftersom Forms Experience Builder fortsätter att utvecklas under det program som antogs tidigt.

Med Forms Experience Builder får Adobe Experience Manager (AEM) Forms kraften från artificiell intelligens. Denna innovativa lösning förändrar hur organisationer skapar, hanterar och optimerar sina digitala formulär genom naturliga språkinteraktioner och intelligent automatisering.

Forms Experience Builder bygger på modern webbteknik och bygger på avancerade AI-tjänster, vilket gör det möjligt för både tekniska och icke-tekniska användare att skapa avancerade, proffsiga formulär genom konversationsgränssnitt. Vare sig du är affärsanalytiker och behöver ett enkelt registreringsformulär eller utvecklare som skapar komplexa flerstegsarbetsflöden effektiviserar Forms Experience Builder hela processen för att skapa formulär.

## Konversationsgränssnitt

Forms Experience Builder har ett intuitivt chattbaserat gränssnitt som gör det lika enkelt att skapa formulär som att föra en konversation:

```
┌─────────────────────────────────────────────────────────┐
│ Forms Experience Builder                               │
├─────────────────────────────────────────────────────────┤
│                                                         │
│  👤 User: Create a customer feedback form              │
│                                                         │
│  🤖 AI: I'll help you create a feedback form. What    │
│       type of feedback do you want to collect?         │
│                                                         │
│  👤 User: Product reviews with ratings and comments    │
│                                                         │
│  🤖 AI: Perfect! I've created a feedback form with:   │
│       * Product rating (1-5 stars)                     │
│       * Comment field                                   │
│       * Customer email (optional)                       │
│       * Submit to email notification                    │
│                                                         │
│  👤 User: Add a field for product category             │
│                                                         │
│  🤖 AI: Added a dropdown field with common categories  │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

## Kärnfunktioner

### Skapa AI-baserade formulär

**Formulärgenerering för naturligt språk**

Skapa kompletta formulär från grunden med enkla engelska beskrivningar. Beskriv helt enkelt era krav, till exempel&quot;Skapa ett formulär för kundfeedback med klassificeringsskalor och kommentarsfält&quot;, så genererar Forms Experience Builder rätt formulärstruktur, fälttyper och valideringsregler.

**Dynamisk fälthantering**

Lägg till, ändra eller ta bort formulärfält med konversationskommandon. AI förstår sitt sammanhang och kan på ett intelligent sätt föreslå fälttyper, valideringsregler och förbättringar av användargränssnittet baserat på dina behov.

**Layoutoptimering**

Uppdatera formulärlayouter och konfigurationer på ett naturligt språk. Begär ändringar som&quot;Gör formuläret mer mobilvänligt&quot; eller&quot;Organisera fält i ett logiskt flöde&quot; så använder Forms Experience Builder lämpliga format- och layoutjusteringar.

### Intelligent import och konvertering

**Konvertering av PDF till formulär**

Förvandla statiska PDF-dokument till interaktiva, dynamiska blanketter. Ladda upp alla PDF-dokument så analyserar Forms Experience Builder strukturen för att skapa ett motsvarande digitalt formulär med lämpliga fälttyper och validering.

**URL till formulärkonvertering**

Konvertera befintliga webbformulär eller webbsidor till AEM Forms. Ange bara en URL så extraherar Forms Experience Builder formulärelementen och återskapar dem som AEM Forms med utökade funktioner.

**Stöd för flera format**

Hantera olika filtyper för att skapa blanketter: PDF, bilder, skärmdumpar och befintliga blankettmallar. Forms Experience Builder kan bearbeta och konvertera dessa till fungerande AEM Forms.

### Avancerad blankettlogik och integration

**Skapa intelligenta regler**

Skapa komplex formulärvalidering och logiska regler för verksamheten med ett naturligt språk. Forms Experience Builder kan generera avancerad villkorsstyrd logik, fältberoenden och valideringsregler som vanligtvis kräver omfattande kodningskunskaper.

**Konfiguration av omfattande överföringsåtgärd**

Konfigurera inskickade formulär så att de kan integreras med era befintliga affärssystem:

- **E-postintegrering**: Konfigurera automatiska e-postmeddelanden och bekräftelser
- **REST API-slutpunkter**: Anslut till anpassade program och tjänster
- **Molnlagring**: Integrera med Azure Blob Storage, SharePoint och OneDrive
- **Automatisering av arbetsflöden**: Anslut till Power Automate och Workfront Fusion
- **Marknadsplattformar**: Direktintegrering med Marketo för lead-hantering
- **AEM-arbetsflöden**: Utnyttja befintliga arbetsflödesfunktioner i AEM

**Prestandaanalys**

Analysera formulärkonverteringens prestanda och användarinteraktionsmönster. Forms Experience Builder ger insikter i formuläreffektiviteten och föreslår optimeringar för att förbättra slutförandefrekvensen och användarupplevelsen.

## Så här fungerar det

Forms Experience Builder har en enkel konverteringsmetod:

```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│  1. Describe    │───▶│  2. AI Creates  │───▶│  3. Refine &    │
│  Your Form      │    │  Initial Form   │    │  Configure      │
│  Requirements   │    │                 │    │                 │
└─────────────────┘    └─────────────────┘    └─────────────────┘
         │                       │                       │
         │                       │                       │
         ▼                       ▼                       ▼
┌─────────────────────────────────────────────────────────────────┐
│  "Create a loan application form"  →  Form with relevant        │
│  "Add conditional logic"           →  fields and basic          │
│  "Connect to CRM system"           →  validation rules          │
└─────────────────────────────────────────────────────────────────┘
```

## Exempel på användningsfall

### Låneansökningsformulär

```
┌─────────────────────────────────────────────────────────┐
│ Loan Application - Multi-Step Form                    │
├─────────────────────────────────────────────────────────┤
│ Step 1: Personal Information                           │
│  🏠 Property Type: [Primary] [Investment] [Commercial] │
│  💰 Loan Amount: [$_______] (triggers different paths) │
│  📊 Income Verification: [W2] [Self-Employed] [Other]  │
│                                                         │
│ Step 2: Financial Details (conditional based on above) │
│  ↳ If Self-Employed: Show tax returns, profit/loss     │
│  ↳ If W2: Show employment history, pay stubs           │
│  ↳ Complex debt-to-income calculations                 │
│                                                         │
│ Step 3: Compliance & Review                            │
│  📋 Regulatory disclosures, digital signatures         │
│  🔍 Automated eligibility pre-screening                │
└─────────────────────────────────────────────────────────┘
```

### Försäkringsanspråksblankett

```
┌─────────────────────────────────────────────────────────┐
│ Insurance Claim - Adaptive Form                        │
├─────────────────────────────────────────────────────────┤
│ 🚗 Claim Type: [Auto] [Property] [Health] [Business]   │
│                                                         │
│ ↳ Auto Selected: Shows accident details, police report │
│ ↳ Property: Shows damage assessment, repair estimates  │
│ ↳ Health: Shows medical provider network, pre-auth     │
│                                                         │
│ 📎 Dynamic Document Requirements:                       │
│   * Photos/videos of damage                            │
│   * Police reports (auto only)                         │
│   * Medical records (health only)                      │
│   * Repair estimates (property only)                   │
│                                                         │
│ 🔄 Real-time claim status updates                      │
└─────────────────────────────────────────────────────────┘
```

### Migrerings- och konverteringsscenarier

Omvandla era befintliga formulär till kraftfulla digitala upplevelser med AI-baserad konvertering.


#### Omvandla PDF forms till Digital Forms

Förvandla PDF forms med olika fält till dynamiska digitala upplevelser med automatiserade beräkningar och mobilresponsiv design.

**Viktiga fördelar:**

- Automatiserade momsberäkningar och fältberoenden
- Integrering av digitala signaturer och e-arkivering
- Mobilresponsiv layoutoptimering
- 95 % minskning av antalet bearbetningsfel


#### Modernisering av äldre XFA-baserade formulär

Du kan konvertera komplexa XFA-program till moderna guider i flera steg med validering i realtid och efterlevnad av hjälpmedelsregler.

**Viktiga fördelar:**

- Effektivt gränssnitt för flerstegsguiden
- Validering i realtid med sammanhangsbaserad hjälp
- Integrering av myndighetsdatabaser
- Komplett WCAG 2.1-kompatibilitet


#### Konvertera skärmbild av formulär till ett digitalt formulär

Ni kan omvandla alla pappersblanketter till en digital upplevelse. AEM Forms optimerar automatiskt layouten och skapar integrerade digitala formulär från en skärmbild.

**Viktiga fördelar:**

- Intelligent fälttypsidentifiering
- Optimerad framtagning av responsiv layout
- Förbättrad validering utöver originalpapper
- Integreringsförberedd arkitektur

#### Importera och förbättra befintliga webbformulär

Du kan importera ditt befintliga webbformulär och lägga till avancerad validering, villkorsstyrd logik och flerkanalsöverföring i formulären utan att befintliga funktioner bryts.

**Viktiga fördelar:**

- Avancerad valideringslogik och regler
- Villkorliga fältbeteenden och arbetsflöden
- Alternativ för flerkanalsöverföring
- Inbyggd analys och prestandaspårning

## Forms Experience Builder jämfört med traditionell utveckling

| Proportioner | Traditionell blankettgenerering | Forms Experience Builder |
|--------|---------------------------|----------------------|
| **Dags att skapa** | 2-3 dagar | 2-3 timmar |
| **Teknisk kunskap** | Obligatoriskt | Krävs inte |
| **Verifieringsregler** | Manuell kodning | Naturligt språk |
| **Mobiloptimering** | Manuell CSS/JS | Automatisk |
| **Tillgänglighet** | Manuell implementering | Inbyggd efterlevnad |
| **Uppdateringar** | Kodändringar krävs | Naturligt språk |


## Fördelar för organisationer

### Demokratiserad blankettgenerering

Ge icke-tekniska användare möjlighet att skapa avancerade blanketter utan programmeringskunskaper. Affärsanalytiker, ämnesexperter och innehållsskapare kan direkt översätta sina krav till funktionella formulär genom naturliga språkkonversationer.

### Reducerad tid till värde (TTV)

Snabba upp formulärutvecklingen dramatiskt från dagar till timmar. Det som tidigare krävde omfattande utvecklingscykler kan nu genomföras i en enda session genom konverteringsbaserad AI, vilket möjliggör snabbare time-to-market för digitala initiativ.

### Gränssnittets tydlighet

Eliminera inlärningskurvan med ett intuitivt konversationsgränssnitt. Man kan skapa komplexa blanketter på ett naturligt språk istället för att lära sig tekniska verktyg för blankettkonstruktion, vilket minskar utbildningstiden och ökar acceptansen.

### Moderniseringsåtgärder för skalförändring

Modernisera befintliga formulärportföljer effektivt. Konvertera befintliga PDF-, XFA- och HTML-formulär till responsiva digitala upplevelser, samtidigt som affärslogiken bevaras och användarupplevelsen förbättras i hela formulärets ekosystem.

## Komma igång

Gå till [Forms Experience Builder-dokumentationen](forms-ai-assistant-getting-started.md) om du vill komma igång med Forms Experience Builder. Du kan öppna Forms Experience Builder via AEM Forms Editor eller Universal Editor, beroende på vilket arbetsflöde du föredrar.

Forms Experience Builder är en kraftfull och intuitiv lösning som kombinerar flexibiliteten i konversationsbaserad AI med tillförlitligheten i blanketthanteringen i enterpriseklass.

## Onboarding och tidig åtkomst

Forms Experience Builder är för närvarande tillgängligt som en del av programmet för tidig åtkomst (EA). Följ de här stegen för att delta och få åtkomst:

1. Kontrollera att du använder den e-postadress till arbetet som är kopplad till din organisation.
2. Skicka ett e-postmeddelande till [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) och begära åtkomst till Forms Experience Builder.
3. Inkludera organisationens namn och relevant projektinformation i din förfrågan för att underlätta introduktionsprocessen.

>[!NOTE]
>
> Tillgång till Forms Experience Builder är begränsad till godkända deltagare i programmet för tidig åtkomst. Adobe kommer att granska din ansökan och ge dig ytterligare anvisningar om hur du går med i programmet om du är berättigad.

Mer information om programmet för tidig åtkomst och dess funktioner finns i [dokumentationen för AEM Forms tidig åtkomst](/help/forms/early-access-ea-features.md).


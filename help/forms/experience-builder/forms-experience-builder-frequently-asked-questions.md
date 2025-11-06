---
title: Forms Experience Builder - Frågor och svar
description: Hitta svar på vanliga frågor om Forms Experience Builder, inklusive konfiguration, användning, felsökning och bästa praxis.
feature: Edge Delivery Services
hide: true
index: false
hidefromtoc: true
role: Admin, Developer
exl-id: f43c2586-9075-47dc-aa45-5ed2d2979b6d
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1060'
ht-degree: 0%

---

# Forms Experience Builder - Frågor och svar

>[!NOTE]
>
> Forms Experience Builder är tillgängligt via ett program för tidig åtkomst. Kontrollera att du har begärt och beviljats åtkomst innan du börjar.

Vanliga frågor och svar om Forms Experience Builder, från grundläggande installation till avancerade funktioner och felsökning.

## Allmänna frågor

### Vad är Forms Experience Builder?

Forms Experience Builder är ett AI-drivet formulärverktyg som gör att ni kan skapa avancerade digitala formulär på ett konversationsspråk. I stället för att dra-och-släpp-gränssnitt eller komplex kodning beskriver du bara vad du vill ha och AI skapar formuläret åt dig.

### Vilka kan använda Forms Experience Builder?

Forms Experience Builder har utformats för att

- **Formulärskapare** som vill skapa formulär snabbt och effektivt
- **Affärsanvändare** som behöver skapa formulär utan teknisk expertis
- **Utvecklare** som vill utnyttja AI för snabb framtagning av formulärprototyper
- **Administratörer** som behöver konfigurera och hantera arbetsflöden för att skapa formulär

### Är Forms Experience Builder tillgängligt för alla AEM Forms-kunder?

Forms Experience Builder är för närvarande tillgängligt via ett Tidig Access-program. Kontakta din Adobe-representant för att få åtkomst och information om din organisations tillgänglighet.

## Installation och konfiguration

### Vilka är förutsättningarna för att använda Forms Experience Builder?

Innan du använder Forms Experience Builder måste du se till att:

- Tillgång till Forms Experience Builder via programmet för tidig åtkomst
- AEM Forms as a Cloud Service med adaptiva Forms Core-komponenter
- Grundläggande förståelse för formulärkoncept och affärskrav

Detaljerade tekniska installationskrav finns i [Distribuera och konfigurera Forms Experience Builder](deploy-forms-experience-builder.md).

### Hur aktiverar jag Forms Experience Builder i min miljö?

Installationen av Forms Experience Builder beror på er AEM Forms-implementering:

**För Edge Delivery Services:**

- Förbered ditt projekt för Edge Delivery Services Forms
- Aktivera Forms Experience Builder i den universella redigeraren

**För kärnkomponentbaserade formulär:**

- Se till att adaptiva Forms Core-komponenter är aktiverade
- Konfigurera Forms Experience Builder i den adaptiva Forms Editor

### Kan jag använda Forms Experience Builder med befintliga formulär?

Ja, Forms Experience Builder kan arbeta med befintliga formulär på flera sätt:

- Importera och konvertera befintliga PDF forms
- Förbättra befintliga adaptiva formulär med AI-baserade funktioner
- Lägga till intelligenta fält i aktuella formulärstrukturer

## Skapa formulär

### Hur skapar jag mitt första formulär?

Börja med en enkel beskrivning av vad du vill:

    Skapa ett kontaktformulär med namn, e-post och meddelandefält

AI genererar den grundläggande formulärstrukturen, som du sedan kan förbättra med ytterligare funktioner, validering och format.

### Vilka typer av formulär kan jag skapa?

Forms Experience Builder har stöd för olika formulärtyper:

- Kontakt- och feedbackformulär
- Registrerings- och introduktionsformulär
- Undersöknings- och bedömningsformulär
- Flerstegsblanketter med villkorsstyrd logik
- Forms med filöverföring och komplex validering

### Kan jag skapa flerstegsformulär?

Ja, du kan skapa flerstegsformulär på ett naturligt språk:

    Skapa ett progressivt formulär med 3 steg: personlig information, inställningar, bekräftelse

AI konfigurerar automatiskt formulärstrukturen med navigering mellan steg.

### Hur lägger jag till validering i formulärfält?

Lägg till validering med naturliga språkkommandon:

    Gör @email till ett obligatoriskt fält med validering av e-postformat
    Lägg till validering av amerikanskt telefonnummerformat i @phoneNumber
    Ange åldersvalidering: måste vara 18 eller äldre för @dateOfBirth

## Avancerade funktioner

### Vad är LLM-förbättrade smarta fält?

Smarta fält som förbättrats med LLM är intelligenta formulärfält som är förifyllda med relevanta alternativ från AI-kunskapsbanker. Till exempel:

- Listrutor med länder i hela världen
- Branschklassificeringar med standardkoder
- Geografiska data med delstater, städer och postnummer

### Hur importerar jag befintliga dokument till formulär?

Du kan importera olika dokumenttyper:

- **PDF forms**: Överför statiska eller interaktiva PDF-filer
- **Bilder**: Överför foton i pappersformulär eller skärmbilder
- **Designfiler**: Importera Figma-design eller andra designformat

Använd bilageikonen i Forms Experience Builder för att ladda upp ditt dokument och beskriva dina konverteringskrav.

### Kan jag integrera formulär med externa system?

Ja, Forms Experience Builder har stöd för olika integreringsalternativ:

- Skicka e-post med anpassade mallar
- REST API-integrering med externa tjänster
- Molnlagringsintegrering (Azure, AWS, Google Cloud)
- Integrering av arbetsflöden (Power Automate, AEM Workflow)

## Felsökning

### AI förstår inte min begäran. Vad ska jag göra?

Prova följande metoder:

- Var mer specifik i beskrivningen
- Dela upp komplexa förfrågningar i mindre steg
- Använd fältreferenser (@fieldName) för riktade ändringar
- Ge tydliga exempel på vad du vill ha

### Min formulärvalidering fungerar inte. Hur lagar jag den?

Kontrollera de här vanliga problemen:

- Kontrollera att fältnamnen matchar exakt (skiftlägeskänsliga)
- Kontrollera att verifieringssyntaxen är korrekt
- Testa valideringsregler individuellt
- Granska felmeddelanden för specifika problem

### Villkorslogik aktiveras inte korrekt. Vad är det för fel?

Felsöka villkorlig logik genom att:

- Kontrollera att fältnamnen refereras korrekt
- Kontrollerar regelsyntax och villkor
- Testa med olika indatakombinationer
- Verifierar fälttyper som matchar regelkrav

### Gränssnittet läses inte in. Vad ska jag göra?

Prova följande lösningar:

- Uppdatera webbläsaren och rensa cache
- Kontrollera din internetanslutning
- Kontrollera att du har rätt åtkomstbehörighet
- Kontakta systemadministratören om problemet kvarstår

## God praxis

### Hur skapar jag bättre formulär med Forms Experience Builder?

Följ dessa standarder:

- **Var specifik**: Tillhandahåll detaljerade beskrivningar av vad du vill ha
- **Börja enkelt**: Börja med grundläggande struktur och lägg till komplexitet gradvis
- **Testa noggrant**: Verifiera alla formulärfunktioner före distributionen
- **Använd inkrementell utveckling**: Skapa formulär steg för steg

### Vad bör jag undvika när jag skapar formulär?

Undvik dessa vanliga misstag:

- Vara för vag i beskrivningarna
- Försöker skapa allt på en gång
- Hoppar över testning och validering
- Mobilrespons övervägs inte

### Hur ser jag till att mina formulär är tillgängliga?

Forms Experience Builder innehåller hjälpmedelsfunktioner:

- Automatisk kontroll av WCAG-kompatibilitet
- Skärmläsarkompatibilitet
- Stöd för tangentbordsnavigering
- Alternativ för högkontrastläge

## Integration och driftsättning

### Hur använder jag formulär som skapats med Forms Experience Builder?

Forms som skapats med Forms Experience Builder följer AEM Forms standarddistributionsprocesser:

- Publicera formulär via AEM författarmiljö
- Konfigurera slutpunkter för formulärsändning
- Ställa in arbetsflöden för formulärbearbetning
- Testa formulär i produktionsmiljön

### Kan jag anpassa AI-svaren och -beteendet?

Ja, du kan konfigurera olika aspekter:

- Svarsstil (kortfattad, detaljerad, balanserad)
- Språkinställningar och terminologi
- Alternativ för gränssnittsanpassning
- Tillgänglighetsinställningar

### Hur får jag hjälp med Forms Experience Builder?

För ytterligare support:

- Kontrollera guiden [Komma igång](forms-experience-builder-getting-started.md)
- Granska [Distribuera och konfigurera guiden](deploy-forms-experience-builder.md)
- Kontakta systemadministratören
- Kontakta Adobe support för tekniska frågor

## Relaterade artiklar

- [Forms Experience Builder - översikt](product-overview.md)
- [Komma igång med Forms Experience Builder](forms-experience-builder-getting-started.md)
- [Installera och konfigurera Forms Experience Builder](deploy-forms-experience-builder.md)
- [LM-förbättrade smarta fält](forms-experience-builder-llm-smart-fields.md)
- [Intelligent import och konvertering](intelligent-import-conversion.md)
- [Inlämning och integration av blanketter](form-submission-integration.md)

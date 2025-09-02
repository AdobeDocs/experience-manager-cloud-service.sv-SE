---
title: Komma igång med Forms Experience Builder
description: Lär dig använda Forms Experience Builder för att skapa och hantera formulär med progressiv publicering för alla användartyper
feature: Edge Delivery Services
hide: true
index: false
hidefromtoc: true
role: Admin, Architect, Developer
source-git-commit: fe34b44d02c308e7d18a08dd05f21abc67bd0cb2
workflow-type: tm+mt
source-wordcount: '2013'
ht-degree: 0%

---


# Komma igång med Forms Experience Builder

>[!NOTE]
>
> Funktionen Forms Experience Builder är tillgänglig i programmet **Tidig åtkomst (EA)**. Om du är intresserad kan du skicka ett snabbt e-postmeddelande från din arbetsadress till `aem-forms-ea@adobe.com` för att begära åtkomst till funktionen.

>[!IMPORTANT]
>
> **Dokumentation som kan ändras**: Dokumentationen testas för närvarande mot produkten och kan uppdateras och revideras. Funktioner, kommandon och exempel kan ändras allt eftersom Forms Experience Builder fortsätter att utvecklas under programmet för tidig åtkomst.

Den här omfattande guiden hjälper dig att komma igång med att skapa och hantera formulär med hjälp av konverteringsbaserad AI-teknik. Oavsett om du är nybörjare som vill skapa ditt första formulär eller en avancerad användare som vill utnyttja avancerade funktioner hittar du detaljerad information och praktiska exempel som vägleder dig genom funktionerna i Forms Experience Builder.

## Krav och inställningar

### &#x200B;1. Begär åtkomst

Forms Experience Builder är för närvarande tillgängligt som en del av programmet för tidig åtkomst (EA). Du behöver följande information för att kunna delta och få åtkomst:

**Nödvändig information**

- **IMS-organisations-ID**: Din Adobe-organisationsidentifierare
- **Program-ID**: Ditt specifika program-ID i Adobe Experience Cloud
- **Projektinformation**: Tidslinje, omfång och användningsfall
- **E-post för officiellt arbete**: Associerad med din organisations Adobe-konto

**Så här skaffar du IMS-organisations-ID och program-ID**

Detaljerade steg för att hitta ditt IMS-organisations-ID och program-ID finns i:

- [Adobe Experience Cloud guide för organisationskonfiguration](/help/onboarding/cloud-manager-introduction.md)
- [Program- och miljöhantering](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)

**Begär åtkomst**

1. Samla ditt IMS-organisations-ID och program-ID med hjälp av guiderna ovan
2. Skicka ett e-postmeddelande till [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) och begära åtkomst
3. Inkludera i din begäran:
   - Organisationsnamn och IMS-organisations-ID
   - Program-ID
   - Projektets tidslinje och omfattning
   - Planerade användningsfall och verksamhetsmål

>[!IMPORTANT]
>
> **Begränsat tillgänglighetsprogram**: Åtkomst till Forms Experience Builder måste godkännas av interna intressenter. Adobe kommer att granska din begäran baserat på programkapacitet och anpassning till kriterierna för tidig åtkomst. Godkännandet är inte garanterat och beror på den aktuella programtillgängligheten.

### &#x200B;2. Kontrollera att Forms är aktiverat

Kontrollera att [AEM Forms är aktiverat för din miljö](/help/forms/setup-forms-cloud-service.md) innan du använder Forms Experience Builder.


### &#x200B;3. Konfigurera miljön


- **För Edge Delivery Services (EDS):**

   - [Installationsmiljö för Edge Delivery Services Forms](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md)
   - [Skapa ett nytt formulär med Edge Delivery Forms-mallen](/help/edge/docs/forms/universal-editor/create-forms.md)

- **För kärnkomponentbaserade formulär:**

   - På din Adobe Experience Manager-instans besöker du Forms > Forms &amp; Documents
   - [Skapa en ny sida med hjälp av mallen för kärnkomponenter](/help/forms/creating-adaptive-form-core-components.md)


## Snabbstart

### Få tillgång till Forms Experience Builder

Forms Experience Builder finns i Forms Managment UI, Universal Editor och Adaptive Forms Editor. Du kan använda någon av dessa metoder för att få åtkomst till formuläret:

**Forms Management UI (för kärnkomponenter)**

1. **Navigera till Forms**: Gå till AEM > Forms > Forms &amp; Documents
1. Klicka på ikonen Forms Experience Builder i verktygsfältet. Det ligger nära det övre vänstra hörnet av användargränssnittet.
   ![Ikon för AI-assistenten*](/help/edge/docs/forms/assets/forms-manager.gif){width="50%"}
1. Börja skapa konversationsformulär


**Adaptiv Forms Editor (för kärnkomponenter)**

1. Gå till AEM > Forms > Forms &amp; Documents
2. [Skapa ett nytt formulär med mallen för kärnkomponenter](/help/forms/creating-adaptive-form-core-components.md)
3. Öppna formuläret för redigering
4. Klicka på ikonen Forms Experience Builder i redigeringsverktygsfältet
   ![Ikon för AI-assistenten*](/help/edge/docs/forms/assets/adaptive-forms-editor.gif){width="75%"}

5. Börja skapa konversationsformulär


**Universell redigerare (för Edge Delivery Services Forms)**

1. Följ [installationsguiden för Edge Delivery Services](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md) för att skapa din EDS-sida
1. Navigera till din EDS-sida i Universal Editor
1. Leta efter ikonen Forms Experience Builder i den högra panelen
1. Klicka för att öppna konversationsgränssnittet



### Ditt första formulär

| Exempel på konversation |   |
|--------------------------------------------------------------------------------------------------------------------------------------------|---|
| **Prova den här konversationen för att skapa ett omfattande kontaktformulär (baserat på Summit-demo):**<br><br>**Du:**&quot;Skapa ett kontaktformulär för att samla in personlig information, inklusive fullständigt namn, e-postadress, telefonnummer, företagsnamn, jobbtitel och ett meddelandefält för frågor&quot;<br><br>**AI:** Välj en mall<br>    En listruta där du kan välja en mall <br><br>**AI:** Välj ett tema <br>    En listruta där du kan välja ett tema <br><br>**AI:** Skapa formulär | ![Ditt första formulär](/help/edge/docs/forms/assets/create-form.png) |
| <br>**AI:** Öppna skapat formulär | </br> Formuläret skapas och öppnas i redigeraren |


### Essential Commands

| Symbol | Syfte | Exempel på användning |
|--------|---------|---------------|
| `/` | Snabbåtgärder och genvägar | `/create-form contact form`, `/help validation rules`, `/update-layout wizard` |
| `@` | Referera till befintliga formulärfält | `@email`, `@firstName`, `Make @phoneNumber required` |
| Oformaterad text | Naturlig konversation | &quot;Lägg till ett obligatoriskt telefonnummerfält&quot;, &quot;Skapa validering för e-post&quot; |

**Exempel på specifika kommandon:**

- `/create-form customer survey` - Skapar ett nytt kundundersökningsformulär
- `/add-field @email validation` - Lägger till validering i befintligt e-postfält
- `/create-rule show @spouse if @maritalStatus equals married` - Skapar villkorlig logik
- `/configure-submit to email support@company.com` - Konfigurera e-postinlämning
- `/help multi-step forms` - Få hjälp med att skapa formulär i flera steg

### Tips för framgång

- **Var specifik**: Det fungerar bättre att lägga till ett obligatoriskt e-postfält med validering än att lägga till e-post
- **Referera till befintliga fält**: Använd `@fieldName` när du ändrar formulär
- **Be om hjälp**: Skriv `/help` följt av din fråga
- **Upprepa**: Gör en ändring i taget för bästa resultat


## Olika sätt att börja skapa ett formulär

### &#x200B;1. Börja med förslag på naturliga språk

Beskriv dina formulärkrav på ett naturligt språk så genererar Forms Experience Builder den fullständiga formulärstrukturen:

**Exempel:**

- &quot;Skapa ett låneansökningsformulär med personlig information, ekonomisk information och dokumentöverföringar&quot;
- &quot;Bygg ett formulär för kundfeedback med betyg, kommentarer och produktkategorier&quot;
- &quot;Jag behöver ett registreringsformulär i flera steg för en konferens med betalningshantering&quot;

### &#x200B;2. Importera och konvertera

Omvandla befintliga blanketter och dokument till moderna, interaktiva upplevelser:

**Källor som stöds:**

- **PDF forms**: Överför statiska PDF-filer för att konvertera dem till interaktiva digitala formulär med valideringar.
- **Skärmbilder eller bilder**: Överför foton av pappersformulär för att generera funktionella digitala versioner
- **XFA Forms**: Konvertera äldre XFA-baserade formulär till moderna responsiva formulär

**Så här importerar du:**

1. Klicka på bilageikonen i Forms Experience Builder-gränssnittet
2. Ladda upp filen (PDF, bild, Figma-design osv.)
3. Beskriv era krav:
   - &quot;Konvertera detta PDF-formulär till en digital version&quot;
   - &quot;Skapa ett formulär som matchar skärmbildslayouten&quot;
   - &quot;Bygg detta formulär från min Figma-design&quot;

**Filtyper som stöds:**

- **Bilder** (PNG, JPG, GIF): Formulärlayouter, gränssnittsmodeller, skannade formulär, handritade skisser
- **PDF-filer**: Befintliga formulär, specifikationer, dokument, Acroforms, XFA-formulär
- **Skärmbilder**: Skärmbilder för dator/mobilapp, foton från pappersformulär, whiteboard-skisser
- **Handritade skisser**: Napkin-skisser, trådramar, konceptritningar (fotograferade)

### Viktiga interaktioner

#### Lägga till formulärelement

**Grundläggande tillägg:**

    👤 Du: &quot;Lägg till ett avsnitt för personlig information&quot;
    👤 Du: &quot;Inkludera en filöverföring för CV&quot;
    👤 Du: &quot;Lägg till en listruta för val av land&quot;

**Detaljerade specifikationer:**

    👤 Du:&quot;Lägg till en personlig informationspanel med fält för fullständigt namn, födelsedatum, telefonnummer och e-postadress&quot;
    👤 Du:&quot;Inkludera en säker filuppladdningskomponent för dokument, begränsad till PDF-filer under 5 MB&quot;
    👤 Du:&quot;Lägg till en landsmeny med alternativ för USA, Kanada, Storbritannien och Tyskland&quot;

#### Skapa dynamiskt beteende

**Enkel logik:**

    👤 Du: &quot;Visa ytterligare fält när &quot;Annat&quot; har valts&quot;
    🤖 AI: &quot;Skapade en villkorsregel som visar ytterligare fält när &quot;Annat&quot; har valts&quot;
    
    👤 Du: &quot;Gör e-postfältet obligatoriskt&quot;
    🤖 AI: &quot;Uppdaterade e-postfältet som ska behövas med validering&quot;
    
    👤 Du: &quot;Beräkna summan automatiskt&quot;
    🤖 AI: &quot;Beräkningslogik har lagts till automatiskt för beräkning av summor&quot; 

**Komplexa affärsregler:**

    👤 Du: &quot;Visa informationsfälten för make/maka endast när äktenskapsstatus är inställd på &quot;Gift&quot; 
    🤖 AI: &quot;Skapade en villkorlig regel som visar makefält baserat på civilstånd&quot;
    
    👤 Du: &quot;Beräkna totalkostnaden genom att multiplicera kvantitet och pris och sedan lägga till 10 % skatt&quot;
    🤖 AI: &quot;Tillagd beräkningslogik med kvantitet, pris och skatteberäkning&quot;
    
    👤 Du:&quot;Aktivera bara skicka-knappen när alla obligatoriska fält har fyllts i och villkoren har accepterats&quot; 
    🤖 AI:&quot;Skapad valideringslogik som endast möjliggör sändning när alla villkor är uppfyllda&quot; 

#### Formulärlayout och design

**Layoutändringar:**

    👤 Du: &quot;Gör det här till ett flerstegsformulär&quot;
    🤖 AI: &quot;Konverterade formuläret till en progressiv layout med navigering&quot;
    
    👤 Du: &quot;Ordna fält i två kolumner&quot;
    🤖 AI: &quot;Uppdaterade layouten så att fält visas i en tvåkolumnslayout&quot;
    
    👤 Du: &quot;Konvertera till en dragspelslayout&quot;
    🤖 AI: &quot;Omformade formuläret så att det används i accordion formatavsnitt&quot;

**Designförbättringar:**

    👤 Du: &quot;Skapa ett guideliknande formulär med 3 steg: personlig information, inställningar och granskning&quot;
    🤖 AI: &quot;Skapade ett guideformulär med tre tydliga steg och navigering&quot;
    
    👤 Du: &quot;Ordna adressfälten i en kompakt layout med två kolumner&quot;
    🤖 AI: &quot;Organiserade adressfält i ett kompakt format med två kolumner&quot;
    
    👤 Du: &quot;Uppdatera layouten så att den matchar den bifogade trådramen&quot; 
    🤖 AI: &quot;Ändrade layouten så att den matchar den angivna designreferensen&quot; 

### Skicka konfiguration

Forms Experience Builder kan konfigurera olika slutpunkter för att koppla formulären till externa system och tjänster:

| Typ av överföringsåtgärd | Installationskommando | Användningsfall |
|------------------|---------------|----------|
| **E-post** | &quot;Skicka formulär till e-post&quot; | Anmälningar och bekräftelser för inskickande av formulär |
| **REST API** | &quot;Skicka till REST-slutpunkt&quot; | Anpassade program och tredjepartssystem |
| **Molnlagring** | &quot;Spara till Azure/SharePoint&quot; | Dokumentlagring och filhantering |
| **Arbetsflöde** | &quot;Anslut till Power Automate&quot; | Automatisering och godkännande av affärsprocesser |
| **Marknadsföring** | Integrera med Marketo | Leadhantering och automatiserad marknadsföring |

**Exempel på konfiguration av avancerad sändning:**

    👤 Du:&quot;Skicka formuläröverföringar till hr@company.com och skapa ett ärende i vårt CRM-system&quot;
    🤖 AI:&quot;Konfigurerad e-postöverföring och CRM-sändningsåtgärd&quot;
    
    👤 Du:&quot;Skicka data till REST API-slutpunkten och aktivera det nya kundarbetsflödet&quot;
    🤖 AI:&quot;Konfigurera REST API-sändning med arbetsflödesutlösare&quot;
    
    👤 Du:&quot;Skicka e-postsvar till säljteamet och lägg till leadet på vår plattform för marknadsföring&quot; 
    🤖 AI:&quot;Konfigurerad flerkanalsöverföring med e-post- och marknadsföringsautomatisering&quot; 





## Avancerade formuläråtgärder


### Skapa komplexa regler

Skapa sofistikerad validering och affärslogik som svarar på användarinteraktioner och säkerställer dataintegritet:

    👤 Du: &quot;Visa endast adressavsnittet om användaren väljer &quot;Leverera till annan adress&quot; 
    🤖 AI: &quot;Skapade en villkorsregel som visar/döljer adresspanelen baserat på kryssruteval&quot;

### Skapa formulär i flera steg

    👤 Du:&quot;Skapa ett progressivt formulär med 3 steg: personlig information, inställningar, bekräftelse&quot;
    🤖 AI:&quot;Skapade ett progressivt formulär med navigering mellan steg och validering vid varje steg&quot;

### Avancerade fälttyper

- Filöverföring med validering och storleksbegränsningar för dokumenthantering
- Datumväljare med begränsningar och affärsregler för schemaläggning
- Listrutor med dynamiska alternativ som ändras baserat på användarval
- Alternativknappar med villkorlig logik för komplexa beslutsträd


### Konvertering av PDF till formulär

    👤 Du:&quot;Konvertera denna PDF till ett interaktivt formulär&quot;
    🤖 AI:&quot;Analyserade PDF och skapade ett formulär med lämpliga fälttyper och validering&quot;





## Produkthjälp och -inlärning

Forms Experience Builder kan även lära dig mer om AEM Forms funktioner:

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

## Bästa praxis

### Formulärdesign

- **Gör det enkelt**: Börja med viktiga fält och lägg till komplexitet endast när det behövs för att undvika överväldigande användare
- **Använd tydliga etiketter**: Gör fältens syften uppenbara med beskrivande etiketter som vägleder användarna genom formuläret
- **Ange hjälptext**: vägleda användare genom komplexa fält med sammanhangsbaserad hjälp och exempel
- **Testa noggrant**: Verifiera alla användarsökvägar för att säkerställa att formulären fungerar korrekt i alla scenarier

### Användarupplevelse

- **Progressiv visning**: Visa relevanta fält baserat på kontext för att minska kognitiv inläsning och förbättra slutförandefrekvensen
- **Rensa navigering**: Hjälp användarna förstå var de befinner sig i formuläret och vilka steg som återstår
- **Responsiv design**: Säkerställ att formulär fungerar på alla enheter och skärmstorlekar för maximal tillgänglighet
- **Hjälpmedel**: Följ riktlinjerna från WCAG för att göra formulär användbara för personer med funktionshinder

### Prestanda

- **Optimera fältantal**: Be bara om nödvändig information för att minska antalet formuläravbrott och förbättra antalet slutförda formulär
- **Använd lämplig validering**: Förebygg fel före överföring för att ge omedelbar feedback och vägledning
- **Testa slutförandegrad**: Övervaka och förbättra formulärets effektivitet med hjälp av analyser och feedback från användare
- **Regelbundna uppdateringar**: Håll formulären aktuella med affärsbehov och användarförväntningar för optimala prestanda

### Varumärkesöverensstämmelse

- **Skapa varumärkesmallar**: Förbered profilerade formulärmallar med organisationens färger, teckensnitt och format innan du börjar skapa formulär
- **Definiera formatstandarder**: Upprätta konsekventa knappformat, fältlayouter och riktlinjer för mellanrum som kan refereras i uppmaningar
- **Använd varumärkesresurser**: Förbered logotyper, färgkoder och riktlinjer för varumärken så att det blir enkelt att skapa formulär
- **Mallbibliotek**: Skapa en samling profilerade formulärmallar för vanliga användningsområden (kontakt, registrering, feedback)
- **Formatuppmaningar**: Inkludera varumärkesspecifika instruktioner:&quot;Använd företagsblå (#1234AB) för knappar och företagsteckensnittet Helvetica&quot;



## Felsökning

| Problem | Snabbkorrigering |
|-------|-----------|
| **Gränssnittet läses inte in** | Uppdatera webbläsare, kontrollera Internetanslutning |
| **Kommandon fungerar inte** | Prova `/help` eller använd ett naturligt språk istället |
| **@fieldName känns inte igen** | Kontrollera stavning, kontrollera att fältet finns först |
| **Filöverföringen misslyckas** | Använd PDF/JPG/PNG under 10 MB |
| **Formuläret ser fel ut** | Var mer specifik:&quot;Gör det mobilvänligt&quot; |
| **Sändningskonfigurationen misslyckas** | Verifiera API-autentiseringsuppgifter och behörigheter |

**Behöver du fortfarande hjälp?** Skriv `/help` följt av din specifika fråga eller kontakta systemadministratören.

Mer support finns i [Forms Experience Builder Prompt Library](ai-assistant-prompt-library.md) eller så kontaktar du systemadministratören för teknisk hjälp.

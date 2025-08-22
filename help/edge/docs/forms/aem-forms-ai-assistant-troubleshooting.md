---
title: Forms Experience Builder - felsökningsguide
description: Omfattande felsökningsguide för Forms Experience Builder, med vanliga problem, lösningar och felsökningstekniker för att skapa och hantera formulär.
feature: Edge Delivery Services
hide: true
index: false
hidefromtoc: true
role: Admin, Architect, Developer
source-git-commit: 9996bc602ae6169dd1aade622d5dbc5b1addeb54
workflow-type: tm+mt
source-wordcount: '2282'
ht-degree: 0%

---


# Forms Experience Builder - felsökningsguide

>[!NOTE]
>
> Forms Experience Builder är tillgängligt via programmet för tidig användning. Skicka ett e-postmeddelande från din arbetsadress till `aem-forms-ea@adobe.com` för att begära åtkomst.

>[!IMPORTANT]
>
> **Dokumentation som kan ändras**: Den här felsökningsguiden testas för närvarande mot produkten och kan komma att uppdateras och revideras. Problem, lösningar och felsökningstekniker kan förändras allt eftersom Forms Experience Builder fortsätter att utvecklas under det tidiga adopterprogrammet.

Denna omfattande felsökningsguide hjälper er att identifiera, diagnostisera och lösa vanliga problem när ni arbetar med Forms Experience Builder. Handboken är ordnad efter problemkategorier med snabba korrigeringar och detaljerade lösningar.

## Snabbreferens - Vanliga problem

| Problem | Snabbkorrigering |
|-------|-----------|
| **Gränssnittet läses inte in** | Uppdatera webbläsare, kontrollera Internetanslutning, verifiera behörigheter för tidig åtkomst |
| **Kommandon fungerar inte** | Prova `/help` eller använd ett naturligt språk i stället för snedstreck |
| **@fieldName känns inte igen** | Kontrollera stavning, kontrollera att fältet finns först, verifiera fältnamnssyntax |
| **Filöverföringen misslyckas** | Använd PDF/JPG/PNG under 10 MB, kontrollera filformatskompatibiliteten |
| **Formuläret ser fel ut** | Var mer specifik:&quot;Gör det mobilvänligt&quot; i stället för&quot;åtgärda layout&quot; |
| **Integreringen misslyckas** | Verifiera API-autentiseringsuppgifter och behörigheter, kontrollera slutpunktens tillgänglighet |
| **Formuläret skickar inte** | Kontrollera konfigurationen och valideringsreglerna för Skicka-åtgärd |
| **Verifieringsfel som inte visas** | Verifiera fältvalideringsinställningar och placering av felmeddelanden |
| **Mobila layoutproblem** | Granska responsiva designinställningar och fältstorlek |
| **Fält visas inte** | Kontrollera villkorsstyrd logik och synlighetsregler |
| **Importfel** | Verifiera kompatibilitet och storleksbegränsningar för filformat |
| **Prestandaproblem** | Optimera fältantalet och ta bort onödiga valideringar |
| **Hjälpmedelsproblem** | Granska fältetiketter, ARIA-attribut och tabbordning |

**Behöver du fortfarande hjälp?** Skriv `/help` följt av din specifika fråga eller kontakta systemadministratören för teknisk hjälp.

## Problem med åtkomst och autentisering

### Kan inte komma åt Forms Experience Builder

**Symtomen:**

- Forms Experience Builder-gränssnittet är inte synligt
- &quot;Åtkomst nekad&quot; eller liknande felmeddelanden
- Ikonen Forms Experience Builder saknas i redigeraren

**Lösningar:**

1. **Verifiera tidig programregistrering för åtkomst**
   - Bekräfta att du har godkänts för det tidiga adopterprogrammet
   - Kontrollera att din förfrågan har skickats från ditt officiella e-postmeddelande
   - Kontakta `aem-forms-ea@adobe.com` om åtkomst fortfarande väntar

2. **Kontrollera miljöinställningar**
   - Verifiera att AEM Forms är aktiverat för din miljö
   - Kontrollera att du använder en webbläsare som stöds (Chrome, Firefox, Safari, Edge)
   - Rensa webbläsarcache och cookies
   - Inaktivera webbläsartillägg som kan störa

3. **Verifiera användarbehörigheter**
   - Bekräfta att du har rätt användarroller och behörigheter
   - Fråga systemadministratören om åtkomsträttigheter
   - Kontrollera att du är inloggad med rätt konto

### Problem med inläsning av gränssnitt

**Symtomen:**

- Tomt eller delvis inläst gränssnitt
- Indikatorer för snurrande inläsning som inte slutförs
- JavaScript-fel i webbläsarkonsolen

**Lösningar:**

1. **Felsökning av webbläsare**
   - Uppdatera sidan (Ctrl+F5 eller Cmd+Skift+R)
   - Prova en annan webbläsare eller ett inkognito/privat läge
   - Kontrollera om det finns webbläsaruppdateringar och installera om de är tillgängliga
   - Inaktivera annonsblockerare och tillägg för sekretess tillfälligt

2. **Nätverksanslutning**
   - Verifiera stabil internetanslutning
   - Kontrollera om företagets brandvägg blockerar nödvändiga domäner
   - Testa med en annan nätverksanslutning om möjligt
   - Kontakta IT-support för problem med nätverkskonfiguration

3. **Cache- och lagringsproblem**
   - Rensa webbläsarcache och lokal lagring
   - Återställ webbläsarinställningarna till standardinställningarna
   - Kontrollera tillgängligt diskutrymme på enheten
   - Försök få åtkomst från en annan enhet

## Problem med kommandon och interaktion

### Snedstreckskommandon fungerar inte

**Symtomen:**

- `/create-form` eller andra snedstreckskommandon känns inte igen
- Inga förslag som fylls i automatiskt visas
- Kommandon ger felmeddelanden

**Lösningar:**

1. **Verifiering av kommandosyntax**
   - Kontrollera korrekt kommandoformat: `/command-name description`
   - Kontrollera om det finns stavfel i kommandonamn
   - Använd naturligt språk som alternativ:&quot;Skapa ett kontaktformulär&quot;
   - Prova `/help` för att verifiera om kommandot är tillgängligt

2. **Kontextspecifika kommandon**
   - Kontrollera att du är i rätt redigeringssammanhang (Universal Editor kontra Adaptive Forms Editor)
   - Vissa kommandon fungerar bara i vissa miljöer
   - Kontrollera kommandoreferens för sammanhangskrav

3. **Alternativa metoder**
   - Använd naturligt språk i stället för snedstreck
   - Dela upp komplexa kommandon i mindre, enklare förfrågningar
   - Prova att skapa formulär steg för steg i stället för att använda ett enda komplext kommando

### Fältreferenser fungerar inte

**Symtomen:**

- `@fieldName` referenser känns inte igen
- Felmeddelanden om okända fält
- Fältändringar tillämpas inte korrekt

**Lösningar:**

1. **Verifiering av fältnamn**
   - Kontrollera den exakta stavningen av fältnamn (skiftlägeskänsligt)
   - Kontrollera att fältet finns innan du refererar till det
   - Använd det exakta fältnamnet som det skapades, inte etiketten
   - Kontrollera namngivningskonventioner för fält (camelCase, snake_case osv.)

2. **Fältreferenssyntax**
   - Använd rätt `@fieldName`-syntax utan blanksteg
   - Undvik specialtecken i fältreferenser
   - Kontrollera om det finns osynliga tecken eller formateringsproblem
   - Försök återskapa fältreferensen manuellt

3. **Felsöka fältreferenser**
   - Visa alla befintliga fält först: &quot;Visa alla aktuella formulärfält&quot;
   - Skapa fält innan de refereras till i regler
   - Använd enkla fältnamn utan komplicerade tecken
   - Testfältet refererar till ett i taget

## Problem med att skapa och utforma formulär

### Formuläret skapas inte som förväntat

**Symtomen:**

- Genererat formulär saknar begärda fält
- Felaktiga fälttyper eller layouter
- Formulärstrukturen matchar inte beskrivningen

**Lösningar:**

1. **Förbättra frågespecifikationen**
   - Mer detaljerad information om formulärbeskrivningar
   - Ange exakta fälttyper och valideringskrav
   - Inkludera layoutinställningar och krav på användarupplevelse
   - Dela upp komplexa formulär i mindre, inkrementella förfrågningar

2. **Interaktiv utvecklingsmetod**
   - Börja med grundläggande formulärstruktur
   - Lägg till fält och funktioner stegvis
   - Testa varje tillägg innan du fortsätter
   - Förfina genom konversationer i stället för en enda komplex begäran

3. **Exempel på bättre frågor**

   I stället för:

       Skapa ett formulär för kunder
   
   Använd:

       Skapa ett kundkontaktformulär med:
       - Fullständigt namn (obligatoriskt textfält) 
       - E-postadress (krävs vid validering) 
       - Telefonnummer (valfritt, formaterat) 
       - Meddelande (obligatoriskt textområde, max 500 tecken) 
       - Skicka till e-postmeddelande 
   

### Problem med layout och format

**Symtomen:**

- Formuläret ser brutet ut på mobila enheter
- Inkonsekvent mellanrum eller justering
- Fält visas inte korrekt
- Dålig visuell hierarki

**Lösningar:**

1. **Mobil svarstid**
   - Begär mobilspecifika optimeringar:&quot;Gör det här formuläret mobilvänligt&quot;
   - Ange krav på responsiv design
   - Testa på faktiska mobila enheter
   - Använda enspaltig layout för mobiler

2. **Layoutförbättringar**
   - Specificera om layoutkraven:&quot;Ordna adressfält i två kolumner&quot;
   - Begär en specifik formatmall:&quot;Använd professionella färger och ren typografi&quot;
   - Ange mellanrums- och justeringsbehov
   - Fråga om tillgänglighetsregler

3. **Varumärkeskonsekvens**
   - Förbered varumärkesriktlinjer innan formulär skapas
   - Inkludera specifika färgkoder och teckensnitt i begäranden
   - Använd enhetlig formatering i alla formulär
   - Skapa varumärkesmallar för återanvändning

### Villkorliga logikproblem

**Symtomen:**

- Regler utlöses inte som förväntat
- Fält som visas/döljs felaktigt
- Valideringslogiken fungerar inte
- Komplexa affärsregler misslyckas

**Lösningar:**

1. **Förenkling av regler**
   - Bryt komplexa regler i mindre, enklare villkor
   - Testa varje regel separat innan du kombinerar
   - Använd tydliga, specifika villkor:&quot;Visa @spouseInfo när @maritalStatus är lika med&quot;Gift&quot;
   - Undvik kapslad eller alltför komplex logik från början

2. **Regeltestning och -felsökning**
   - Testa alla möjliga användarsökvägar och scenarier
   - Verifiera fältnamn och värden i villkor
   - Kontrollera skiftlägeskänslighet i regelvillkor
   - Använd felsökningsläget för att spåra regelkörning

3. **Affärslogikimplementering**
   - Dokumentera verksamhetskraven tydligt före implementering
   - Implementera regler stegvis och testa varje steg
   - Ge tydlig användarfeedback när regler aktiveras
   - Hantera kantfall och undantagsscenarier

## Problem med filimport och konvertering

### Fel vid import av PDF

**Symtomen:**

- PDF-filer som inte överförs eller bearbetas
- Konverterade formulär saknar fält eller innehåll
- Felmeddelanden vid PDF-konvertering
- Dålig fältigenkänning från PDF

**Lösningar:**

1. **Filformat och storlek**
   - Se till att PDF-filerna är under 10 MB
   - Använd högklassiga textbaserade PDF:er (inte skannade bilder)
   - Kontrollera att PDF inte är lösenordsskyddat eller krypterat
   - Prova att konvertera PDF till bildformat om textextraheringen misslyckas

2. **PDF kvalitetsoptimering**
   - Använd PDF-filer med tydliga, väldefinierade formulärfält
   - Säkerställ god kontrast och läsbar text
   - Undvik komplexa layouter och överlappande element
   - Ange ytterligare kontext i konverteringsbegäran

3. **Konverteringsförbättring**
   - Beskriv den förväntade formulärstrukturen i detalj
   - Ange fälttyper och valideringskrav
   - Specifika förbättringar för begäran:&quot;Lägg till svarstider och validering för mobila enheter&quot;
   - Granska och förfina konverterade formulär manuellt

### Problem med konvertering av bilder och skärmbilder

**Symtomen:**

- Dålig fältigenkänning från bilder
- Felaktiga fälttyper eller layouter
- Formulärelement saknas
- Konverteringsfel eller timeout

**Lösningar:**

1. **Krav för bildkvalitet**
   - Använd högupplösta bilder (minst 300 DPI)
   - Säkerställ bra ljus och kontrast
   - Undvik skuggor, bländningar och förvrängningar
   - Beskära bilder för att endast fokusera på formulärinnehållet

2. **Optimala bildformat**
   - Använd PNG- eller JPG-format för bästa resultat
   - Undvik komprimerade bilder i GIF eller låg kvalitet
   - Se till att texten är tydligt läsbar i bilden
   - Prova olika bildorienteringar vid behov

3. **Konverteringsvägledning**
   - Beskriv formulärstrukturen i detalj
   - Ange fälttyper och krav explicit
   - Begär specifika förbättringar under konverteringen
   - Var redo att göra manuella justeringar efter konverteringen

## Integrerings- och inlämningsfrågor

### Fel vid formuläröverföring

**Symtomen:**

- Forms kunde inte skickas
- Felmeddelanden vid överföring
- Data når inte avsedda destinationer
- Timeoutfel vid överföring

**Lösningar:**

1. **Skicka åtgärdskonfiguration**
   - Kontrollera att åtgärden Skicka är korrekt konfigurerad
   - Kontrollera API-slutpunkter och autentiseringsuppgifter
   - Testa med enkel e-postinlämning först
   - Validera krav för dataformat

2. **Nätverk och anslutningar**
   - Kontrollera Internetanslutning och nätverksstabilitet
   - Verifiera att brandväggsinställningarna tillåter att formulär skickas
   - Testa olika nätverksanslutningar
   - Kontrollera om det finns företagsproxy eller säkerhetsbegränsningar

3. **Dataverifieringsproblem**
   - Se till att alla obligatoriska fält är ifyllda
   - Verifiera att dataformaten matchar API-kraven
   - Kontrollera om det finns specialtecken eller kodningsproblem
   - Testa med minimal datauppsättning först

### API-integreringsproblem

**Symtomen:**

- REST API-slutpunkter svarar inte
- Autentiseringsfel
- Felmatchningar i dataformat
- Tidsgränser för integrering eller fel

**Lösningar:**

1. **API-konfigurationsverifiering**
   - Verifiera att API-slutpunkts-URL:er är korrekta och tillgängliga
   - Kontrollera autentiseringsuppgifter och behörigheter
   - Testa API-slutpunkter oberoende av verktyg som Postman
   - Verifiera att API accepterar rätt dataformat (JSON, XML osv.)

2. **Datamappningsproblem**
   - Kontrollera att formulärfältsnamnen matchar API-parameterkraven
   - Kontrollera om det finns obligatoriska fält som kanske saknas
   - Verifiera datatypskompatibilitet (strängar, siffror, datum)
   - Testa med exempeldata för att identifiera mappningsproblem

3. **Felhantering och felsökning**
   - Aktivera detaljerad felloggning för API-anrop
   - Kontrollera API-svarskoder och felmeddelanden
   - Implementera återförsökslogik för tillfälliga fel
   - Ange reservalternativ för användare när API misslyckas

### Problem med e-postintegrering

**Symtomen:**

- Bekräftelsemeddelanden skickas inte
- E-postmeddelanden som går till skräppostmappar
- Felaktig e-postformatering
- Formulärdata saknas i e-postmeddelanden

**Lösningar:**

1. **E-postkonfiguration**
   - Kontrollera att e-postadresserna är korrekt formaterade
   - Kontrollera SMTP-inställningar och autentisering
   - Testa med enkla e-postadresser först
   - Verifiera behörigheter och kvoter för e-postservrar

2. **Optimering av e-postleverans**
   - Använd rätt e-postrubriker och avsändarinformation
   - Undvik skräppostutlösare i ämnesrader
   - Inkludera lämpliga avanmälningsmekanismer
   - Testa e-postleverans till olika leverantörer

3. **Innehåll och formatering**
   - Kontrollera att formulärdata är korrekt formaterade i e-postmeddelanden
   - Kontrollera om det finns specialtecken eller kodningsproblem
   - Testa e-postmallar med olika datakombinationer
   - Se till att e-postinnehållet är tillgängligt och läsbart

## Problem med prestanda och inläsning

### Långsam inläsning av formulär

**Symtomen:**

- Forms tar lång tid att ladda
- Smidiga användarinteraktioner
- Timeout under formuläråtgärder
- Dåliga prestanda på mobila enheter

**Lösningar:**

1. **Formuläroptimering**
   - Minska antalet fält och komplexitet
   - Implementera lazy loading för icke-kritiska avsnitt
   - Optimera bilder och material för webben
   - Ta bort onödiga valideringsregler eller logik

2. **Optimering av webbläsare och enheter**
   - Rensa webbläsarcache och temporära filer
   - Stäng webbläsarflikar och program som inte behövs
   - Kontrollera tillgängligt enhetsminne och lagring
   - Testa olika webbläsare för prestandajämförelse

3. **Nätverksoptimering**
   - Testa med olika nätverksanslutningar
   - Kontrollera om det finns nätverksproblem eller bandbreddsbegränsningar
   - Använd kabelanslutning i stället för WiFi om möjligt
   - Kontakta IT-support för problem med nätverksprestanda

### Prestandaproblem vid validering

**Symtomen:**

- Långsam validering
- Visning av fördröjt felmeddelande
- Frysa formulär under validering
- Timeoutfel vid fältvalidering

**Lösningar:**

1. **Valideringsoptimering**
   - Minska valideringsfrekvensen i realtid
   - Implementera debitering för valideringsanrop
   - Förenkla komplexa valideringsregler
   - Använd validering på klientsidan där det är möjligt

2. **Förenkling av regler**
   - Bryt komplex validering i mindre regler
   - Ta bort onödiga fältöverskridande valideringar
   - Optimera villkorsstyrd logik för prestanda
   - Cachelagra valideringsresultat där så är lämpligt

3. **Förbättringar av användarupplevelsen**
   - Ge omedelbar feedback vid enkel validering
   - Använd progressiv validering i stället för realtid för komplexa regler
   - Visa inläsningsindikatorer under valideringsprocesser
   - Tillåt användare att fortsätta medan valideringsprocesser körs i bakgrunden

## Avancerad felsökning

### Felsökningsläge och diagnostik

**Aktivera felsökningsinformation**

Använd de här anvisningarna för att få mer detaljerad information om formulärproblem:

    Aktivera felsökningsläge för att identifiera problem med formuläröverföring och fältvalidering
    
    Analysera formulärfel: kontrollera valideringsregler, API-svar och användarindatamönster
    
    Visa detaljerad information om formulärstruktur och fältkonfiguration

### Felanalystekniker

**Systematisk felsökningsmetod**

1. **Isolera problemet**
   - Testa med minimal formulärkonfiguration
   - Ta bort komplexa funktioner tillfälligt
   - Testa enskilda komponenter separat
   - Använd elimineringsprocessen för att identifiera rotorsaken

2. **Samla diagnostikinformation**
   - Kontrollera webbläsarkonsolen för JavaScript-fel
   - Granska nätverksförfrågningar och svar
   - Dokumentera exakta steg för att återskapa problemet
   - Samla skärmbilder och felmeddelanden

3. **Testmiljövariabler**
   - Testa olika webbläsare och enheter
   - Testa med olika användarkonton och behörigheter
   - Verifiera i olika nätverksmiljöer
   - Jämför med arbetsformulär eller konfigurationer

### Logganalys och övervakning

**Felsökning i webbläsarkonsolen**

1. Verktyg för webbläsarutvecklare (F12)
2. Kontrollera om det finns JavaScript-fel på fliken Konsol
3. Granska nätverksfliken för misslyckade begäranden
4. Fliken Övervaka prestanda för långsamma åtgärder

**Vanliga felmönster**

- **CORS-fel**: Problem med korsorigo-begäranden med API-integreringar
- **Autentiseringsfel**: Ogiltiga autentiseringsuppgifter eller utgångna token
- **Verifieringsfel**: Konflikter eller syntaxfel i fältverifieringsregeln
- **Nätverkstimeout**: Långsamma eller otillförlitliga nätverksanslutningar

## Hämta ytterligare hjälp

### Självbetjäningsresurser

**Inbyggt hjälpsystem**

- Använd kommandot `/help` följt av specifika frågor
- Få sammanhangsbaserad hjälp i Forms Experience Builder-gränssnittet
- Granska felmeddelanden noggrant för specifik vägledning
- Kontrollera [startguiden för Forms Experience Builder](forms-ai-assistant-getting-started.md)

**Dokumentationsresurser**

- [Forms Experience Builder Prompt Library](ai-assistant-prompt-library.md)
- [Forms Experience Builder Best Practices](aem-forms-ai-assistant-best-practices.md)
- [AEM Forms-dokumentation](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/home.html?lang=sv-SE)

### Eskalering och support

**När ska jag kontakta supporten**

- Problem kvarstår efter försök med dokumenterade lösningar
- Systemomfattande problem som påverkar flera användare
- Säkerhetsfrågor eller dataintegritetsfrågor
- Integrationsproblem som kräver konfiguration på systemnivå

**Information att ange**

- Detaljerad beskrivning av problemet och steg för att återskapa
- Skärmbilder eller skärminspelningar av problemet
- Webbläsare och systeminformation
- Felmeddelanden och konsolloggar
- Formulärkonfiguration och integreringsinformation

**Kontaktmetoder**

- Systemadministratör: För miljö- och åtkomstproblem
- Teknisk support: För komplexa integrerings- och konfigurationsproblem
- Tidig åtkomst-program: `aem-forms-ea@adobe.com` för programspecifika problem

### Community och kunskapsutbyte

**Bästa praxis för problemlösning**

- Dokumentlösningar för framtida referens
- Dela framgångsrika felsökningsstrategier med teammedlemmar
- Bidra till organisationsdatabasen
- Delta i användargrupper och forum

**Kontinuerlig förbättring**

- Regelbunden granskning av vanliga problem och lösningar
- Uppdatera felsökningsprocedurer baserat på nya resultat
- Utbildning och kunskapsutbyte
- Feedback till produktteamet för funktionsförbättringar

Den här felsökningsguiden uppdateras kontinuerligt baserat på användarfeedback och nya funktioner i Forms Experience Builder. Den senaste informationen och ytterligare resurser finns i [AEM Forms-dokumentationen](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/home.html?lang=sv-SE).

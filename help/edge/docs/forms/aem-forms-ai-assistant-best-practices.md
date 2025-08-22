---
title: Forms Experience Builder - Bästa praxis
description: Omfattande metodtips för att skapa effektiva formulär med Forms Experience Builder, som omfattar design, användarupplevelse, prestanda och enhetlig varumärkeshantering.
feature: Edge Delivery Services
hide: true
index: false
hidefromtoc: true
role: Admin, Architect, Developer
source-git-commit: 9996bc602ae6169dd1aade622d5dbc5b1addeb54
workflow-type: tm+mt
source-wordcount: '2072'
ht-degree: 0%

---


# Forms Experience Builder - Bästa praxis

>[!NOTE]
>
> Forms Experience Builder är tillgängligt via programmet för tidig användning. Skicka ett e-postmeddelande från din arbetsadress till `aem-forms-ea@adobe.com` för att begära åtkomst.

>[!IMPORTANT]
>
> **Dokumentation som är föremål för ändring**: Denna metodguide testas för närvarande mot produkten och kan komma att uppdateras och revideras. Bästa praxis, rekommendationer och exempel kan ändras allt eftersom Forms Experience Builder fortsätter att utvecklas under det program som antagits tidigt.

Denna omfattande guide innehåller beprövade metoder för att skapa effektiva, användarvänliga formulär med Forms Experience Builder. Dessa rutiner bygger på framgångsrika implementeringar och användarfeedback från olika branscher och användningsexempel.

## Metodtips för formulärdesign

### Behåll det enkelt

**Börja med viktiga fält**

- Börja med endast den mest nödvändiga informationen för att minska användaröverbelastningen
- Öka komplexiteten gradvis baserat på användarnas behov och verksamhetskrav
- Undvik att fråga efter information som du egentligen inte behöver eller använder
- Tänk på användarens tid och kognitiva belastning när du utformar formulär

**Använd tydliga, beskrivande etiketter**

- Gör fältegenskaperna omedelbart uppenbara med beskrivande etiketter
- Undvik teknisk jargon eller intern terminologi som användarna inte förstår
- Använd enhetliga märkningsregler i alla era formulär
- Ange sammanhang när fältkraven kanske inte är uppenbara

**Ge användbar vägledning**

- Inkludera hjälptext för komplexa fält med exempel och formateringskrav
- Använd platshållartext för att visa förväntade indataformat
- Ge tydliga instruktioner för filöverföring, inklusive godkända format och storleksbegränsningar
- Vägled användarna genom flerstegsprocesser med förloppsindikatorer

**Testa noggrant**

- Validera alla användarsökvägar och scenarier före distributionen
- Testa formulär med verkliga användare från er målgrupp
- Verifiera att all villkorslogik fungerar som förväntat
- Se till att felhanteringen ger tydlig och åtgärdbar feedback

### Progressiv redovisning

**Visa relevanta fält baserat på kontext**

- Visa endast ytterligare fält när de blir relevanta för användarval
- Använd villkorslogik för att minska kognitiv belastning och formulärlängd
- Gruppera relaterade fält tillsammans i logiska avsnitt
- Dölj avancerade alternativ tills användarna anger att de behöver dem

**Exempel på implementering:**

    Skapa en regel som bara visar panelen @spouseInformation när @maritalStatus är lika med&quot;Gift&quot;

**Rensa navigering och förlopp**

- Hjälp användarna förstå var de befinner sig i flerstegsformulär
- Skapa tydlig navigering mellan formuläravsnitt
- Visa förloppsindikatorer för längre formulär
- Tillåt användare att spara förloppet och returnera senare

## Bästa praxis för användarupplevelser

### Mobile-First Design

**Optimering av responsiv layout**

- Utforma formulär med mobilanvändare som det viktigaste att tänka på
- Använda enspaltig layout för mobila enheter
- Se till att beröringsmålen har rätt storlek (minimum 44px)
- Testa formulär på olika enhetsstorlekar och orienteringar

**Pekvänliga interaktioner**

- Använd större knappar och inmatningsfält för pekgränssnitt
- Använd lämpliga indatatyper för att utlösa korrekta mobiltangentbord
- Undvik hovringsberoende interaktioner som inte fungerar på enheter med pekskärm
- Ge tydlig visuell feedback för användarinteraktioner

### Tillgänglighet

**Riktlinjer för WCAG 2.1**

- Följ riktlinjerna för tillgänglighet för webbinnehåll för inkluderande design
- Kontrollera färgkontrastförhållanden (minst 4,5:1 för normal text)
- Ange alternativ text för alla bilder och ikoner
- Implementera korrekt rubrikstruktur och semantisk HTML

**Navigering med tangentbord**

- Se till att alla formulärelement är tillgängliga via tangentbordsnavigering
- Ange tydliga fokusindikatorer för alla interaktiva element
- Implementera logisk tabbordning via formulärfält
- Inkludera länkar för överhoppad navigering för komplexa formulär

**Stöd för Reader-skärm**

- Använd korrekta ARIA-etiketter och beskrivningar för formulärfält
- Ange tydliga felmeddelanden som visas för skärmläsare
- Säkerställ att förändringar av dynamiskt innehåll presenteras korrekt
- Testa formulär med det faktiska skärmläsarprogrammet

### Prestandaoptimering

**Inläsningshastighet**

- Optimera inläsningstiden för formulär genom att minimera den initiala paketstorleken
- Implementera lazy loading för icke-kritiska formuläravsnitt
- Optimera bilder och material för webben
- Aktivera lämpliga cachningsstrategier för statiska resurser

**Körningsprestanda**

- Använd lämplig valideringstidpunkt för att balansera användarupplevelse och prestanda
- Implementera fakturering för validering i realtid för att minska antalet serverförfrågningar
- Cachelagra data som ofta används och valideringsresultat
- Optimera villkorlig logikkörning för komplexa formulär

**Spara automatiskt och dataskydd**

- Implementera automatiskt sparande av formulärförloppet för att förhindra dataförlust
- Möjlighet att fylla i blanketter offline där det är möjligt
- Inkludera återförsökslogik för misslyckade överföringar
- Erbjud dataexportalternativ som säkerhetskopia för användare

## Bästa praxis för enhetlig varumärkeshantering

### Förbered varumärket Assets i förväg

**Skapa varumärkesmallar**

- Utveckla standardiserade blankettmallar med organisationens visuella identitet
- Inkludera enhetliga färgscheman, typografi och layoutmönster
- Förbered återanvändbara komponenter som matchar varumärkesriktlinjerna
- Dokumentformatstandarder för enhetlig implementering i olika team

**Definiera riktlinjer för format**

- Fastställ enhetlig fältformatering, knappdesign och mellanrumsstandard
- Skapa en formatguide som innehåller färgkoder, teckensnittsspecifikationer och layoutregler
- Definiera interaktionsmönster och animeringsriktlinjer
- Förbered varumärkesspecifika felmeddelanden och hjälptext

**Skapa komponentbibliotek**

- Skapa återanvändbara formulärkomponenter som matchar varumärkets identitet
- Utveckla enhetliga navigeringsmönster och element i användargränssnittet
- Förbered varumärkta ikoner, logotyper och visuella resurser för blankettintegration
- Skapa mallar för vanliga formulärtyper (kontakt, registrering, feedback)

### Strategier för varumärkesimplementering

**Formatfråga för konsekvens**

Lägg in varumärkesspecifika instruktioner:

    Skapa ett professionellt kontaktformulär med:
    - Corporate blue (#003366) för primära knappar och rubriker
    - Open Sans-teckensnittsfamilj för alla textelement
    - 16px, minsta teckensnittsstorlek för tillgänglighet
    - Konsekvent 24px-avstånd mellan formuläravsnitt
     - Företagslogotyp i rubrik med rätt varumärkesplacering

**Mallbibliotekshantering**

- Bibehåll en samling varumärkesprofilerade blankettmallar för vanligt bruk
- Versionskontrollera era varumärkesmallar för att säkerställa enhetlighet
- tillhandahålla tydlig dokumentation för användning och anpassning av mallar
- Regelbunden granskning och uppdatering av varumärkesresurser för att upprätthålla aktuella standarder

>[!NOTE]
>
>**Anpassade komponenter**: Koordinera med ditt utvecklingsteam om hur du använder organisationsspecifika komponenter och deras kompatibilitet med Forms Experience Builder innan du implementerar anpassade varumärkeselement.

## Metodtips för innehåll och kommunikation

### Metoder för att skapa formulär

**Två primära metoder**

Välj den metod som passar dig bäst:

1. **Skapa från grunden**: Passar bäst för nya formulär med specifika krav
2. **Importera och konvertera**: Perfekt för att uppdatera befintliga formulär och dokument

**Språkfrågor**

- Var tydlig och detaljerad i formulärbeskrivningarna
- Använd tydligt, affärsinriktat språk i stället för tekniska termer
- Ange sammanhang för formulärets syfte och målgrupp
- Inkludera krav på validering och affärsregler i initiala uppmaningar

### Stegvis utvecklingsstrategi

**Starta enkelt, skapa komplexitet**

- Börja med grundläggande formulärstruktur och viktiga fält
- Lägg till valideringsregler och affärslogik stegvis
- Testa varje tillägg innan du går vidare till nästa förbättring
- Samla in feedback från användarna vid varje utvecklingsfas

**Exempel på inkrementell metod:**

    Steg 1: &quot;Skapa ett enkelt kontaktformulär med namn, e-post och meddelandefält&quot;
    Steg 2: &quot;Gör obligatoriska fält för @name och @email med lämplig validering&quot;
    Steg 3: &quot;Lägg till platshållartext och hjälptext för användarvägledning&quot;
    Steg 4: &quot;Lägg till villkorlig logik baserat på frågetyp&quot;

### Metodtips för fältreferens

**Konsekventa namnkonventioner**

- Använd tydliga, beskrivande fältnamn som matchar deras syfte
- Bibehåll enhetliga namnmönster i alla formulär
- Använd camelCase eller snake_case enhetligt i alla dina formulär
- Namnkonventioner för dokumentfält som ger enhetlighet i team

**Giltiga fältreferenser**

- Använd syntaxen `@fieldName` när du ändrar befintliga fält
- Var tydlig med vilka fält du refererar till i komplexa formulär
- Gruppera relaterade fältändringar i en enda begäran
- Verifiera fältnamn innan de används i villkorslogik

## Bästa praxis för integrering och inlämning

### Flerkanalsstrategi

**Primära och sekundära åtgärder**

- Konfigurera primära slutpunkter för inlämning av affärsprocesser
- Konfigurera sekundära åtgärder för meddelanden, bekräftelser och säkerhetskopiering av data
- Implementera felhantering och återförsökslogik för misslyckade överföringar
- Ge användarfeedback för alla inskickningstillstånd (lyckad, misslyckad, bearbetning)

**Integrationsplanering**

- Börja med grundläggande konfiguration och lägg till integreringar stegvis
- Testa varje integrering separat innan du kombinerar flera slutpunkter
- Krav och autentiseringsmetoder för dokument-API
- Planera för krav på dataomvandling och datamappning

### Felhantering och återställning

**Användarvänliga felmeddelanden**

- Tillhandahålla tydliga, åtgärdbara felmeddelanden som hjälper användarna att lösa problem
- Undvik tekniska felkoder eller systemmeddelanden i användarriktat innehåll
- Erbjud alternativa åtgärder när primär inlämning misslyckas
- Inkludera kontaktinformation för användare som behöver ytterligare hjälp

**Dataskydd och dataåterställning**

- Implementera sparande av lokala data för återställning av formulär efter fel
- Ge användarna möjlighet att hämta sina formulärdata som säkerhetskopia
- Ställ in övervakning och varningar för misslyckade inskickade data
- Förfaranden för återställning av planer för driftavbrott eller underhåll

## Bästa praxis för prestanda och analys

### Övervakning och optimering

**Viktiga prestandamått**

- Spåra antalet ifyllda formulär och antalet punkter där de överges
- Övervaka inläsningstider och användarinteraktionsmönster
- Mät valideringens effektivitet och felgrader
- Analysera feedback och nöjda användare

**Kontinuerlig förbättring**

- Regelbunden granskning av formuläranalyser för att identifiera optimeringsmöjligheter
- A/B-testning av olika formulärdesigner och användarflöden
- Insamling och analys av feedback från användare för iterativa förbättringar
- Prestandatester mot branschstandarder

### Datakvalitet och validering

**Smarta valideringsstrategier**

- Implementera validering i realtid för omedelbar användarfeedback
- Använd progressiv validering för att vägleda användarna genom komplexa krav
- Tillhandahålla tydliga valideringsmeddelanden som förklarar hur du åtgärdar fel
- Balansera verifieringsstrikthet med hänsyn till användarupplevelsen

**Dataintegritet**

- Implementera validering mellan fält för att få datakonsekvens
- Använd lämpliga indatatyper och begränsningar för att förhindra ogiltiga data
- Ge exempel på dataformat och vägledning för komplexa fält
- Regelbunden granskning av inlämnade uppgifter om kvalitet och valideringseffektivitet

## Bästa praxis för säkerhet och efterlevnad

### Dataskydd

**Sekretess efter design**

- Samla endast in de data som behövs för ditt ändamål
- Implementera lämpliga regler för datalagring och borttagning
- tillhandahålla tydliga sekretessmeddelanden och mekanismer för samtycke
- Säkerställa att gällande dataskyddsbestämmelser följs (GDPR, CCPA osv.)

**Säkerhetsimplementering**

- Använd HTTPS-kryptering för alla formuläröverföringar och dataöverföring
- Implementera korrekt indatavalidering och sanering
- Säker filöverföring med lämpliga begränsningar och virusskanning
- Regelbundna säkerhetsrevisioner och säkerhetsluckor

### Överensstämmelseöverväganden

**Regelkrav**

- Förstå och implementera branschspecifika regelkrav
- Dokumentera efterlevnadsåtgärder för revision
- Regelbunden översyn av ändringar i lagstiftningen och deras inverkan på formulär
- Personalutbildning om efterlevnadskrav och genomförande

**Tillgänglighet**

- Följ riktlinjerna för tillgänglighet i WCAG 2.1
- Regelbunden tillgänglighetstestning med hjälpmedelstekniker
- Användartestning för personer med funktionshinder
- Dokumentation om tillgänglighetsfunktioner och efterlevnadsåtgärder

## Collaboration bästa praxis för team

### Dokumentation och kunskapsdelning

**Formulärdokumentation**

- Underhåll tydlig dokumentation av formulärsyften, krav och affärsregler
- Slutpunkter för dokumentintegration, dataflöden och beroenden
- Spara versionshistorik och ändringsloggar för formuläruppdateringar
- Dela med dig av bästa praxis och lärdomar mellan team

**Utbildning och användning**

- Erbjuda utbildning för teammedlemmar om Forms Experience Builder-funktioner
- Ta fram riktlinjer för att skapa enhetliga blanketter i hela organisationen
- Vanliga sessioner för kunskapsdelning med nya funktioner och bästa praxis
- Mentorsprogram för nya användare

### Kvalitet på Assurance

**Granskningsprocesser**

- Implementera peer-granskningsprocesser för formulärdesign och implementering
- Upprätta testprotokoll för formulärfunktioner och användarupplevelse
- Regelbunden granskning av befintliga blanketter för att optimera möjligheterna
- Insamling av feedback från både interna användare och slutanvändare

**Standarder och riktlinjer**

- Utveckla organisationsstandarder för blankettkonstruktion och -implementering
- Skapa mallar och riktlinjer för vanliga formulärtyper
- Fastställa godkännandeprocesser för nya blanketter och större förändringar
- Regelbunden granskning och uppdatering av organisationsstandarder

## Avancerade metodtips

### LLM-Enhanced Smart Fields

**Utnyttjar AI-kunskap**

- Använd AI:s inbyggda kunskap för omfattande fältalternativ
- Begär smarta fält för geografiska data, affärsklassificeringar och branschstandarder
- Implementera intelligent fältifyllning för förbättrad användarupplevelse
- Testa om smarta fält är korrekta och fullständiga för dina specifika användningsfall

**Exempel på smarta fält**

    &quot;Lägg till ett startflygplatsfält med alla större flygplatser i världen, inklusive IATA-koder&quot;
    &quot;Skapa ett omfattande branschfält med hjälp av standard-NAICS-klassificering&quot;
    &quot;Inkludera en listruta för professionell certifiering som anpassas baserat på jobbfält&quot;

### Avancerad formulärlogik

**Komplexa affärsregler**

- Bryta komplex affärslogik i mindre, testbara komponenter
- Dokumentera kraven för affärsregler tydligt före implementering
- Testa kantfall och undantagsscenarier noggrant
- Ge tydlig användarfeedback vid överträdelser av affärsregler

**Beteende för dynamiskt formulär**

- Använd progressiv visning för att visa relevanta fält baserat på användarindata
- Implementera smarta standardvärden som kan åsidosättas av användare
- Skapa anpassningsbara formulär som anpassar sig efter användarbeteenden och önskemål
- Balansera automatisering med användarkontroll och genomskinlighet

## Validering och testning

### Omfattande testningsstrategi

**Testning på flera nivåer**

- Enhetstestning av enskilda formulärkomponenter och valideringsregler
- Integrationstestning för slutpunkter för insändning och dataflöden
- Testning av användarnas godkännande med representativa användargrupper
- Prestandatestning under olika lastförhållanden

**Plattformsövergripande validering**

- Testa formulär i olika webbläsare och versioner
- Validera mobilupplevelsen på olika enheter och skärmstorlekar
- Tillgänglighetstestning med olika hjälpmedelstekniker
- Testning av nätverksvillkor för olika anslutningshastigheter

### Kvalitetsmått

**Resultatindikatorer**

- Färdigställningshastigheten för formulär ligger över branschens riktmärken
- Låg felfrekvens och hög kundnöjdhetspoäng
- Snabba inläsningstider och responsiva användarinteraktioner
- Lyckad integrering med backend-system och -processer

**Kontinuerlig övervakning**

- Regelbunden granskning av formulärprestanda och feedback från användare
- Proaktiv identifiering och lösning av problem
- Trendanalys av formuläranvändning och effektivitet
- Riktmärken mot branschstandarder och bästa praxis

Mer information och detaljerade exempel finns i [Forms Experience Builder Getting Started Guide](forms-ai-assistant-getting-started.md) och [Forms Experience Builder Prompt Library](ai-assistant-prompt-library.md).

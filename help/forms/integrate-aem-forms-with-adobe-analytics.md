---
title: Form Analytics with Adobe Analytics and AEM Forms - Complete Guide
seo-title: "Form Analytics: Track Performance, Boost Conversions with Adobe Analytics & AEM Forms"
description: En komplett guide till blankettanalys med Adobe Analytics och AEM Forms. Spåra formulärprestanda, analysera användarbeteenden, minska antalet användare som slutar svara och optimera konverteringarna.
keywords: formuläranalys, spårning av formulärprestanda, analys av avbrutna formulär, konverteringsoptimering, analys av användarbeteende, Adobe Analytics-formulär, AEM Forms-analys
exl-id: 0730432e-75b8-4b35-a377-ae4a2bee6c9f
feature: Adaptive Forms, Acrobat Sign
role: User, Developer
source-git-commit: ab84a96d0e206395063442457a61f274ad9bed23
workflow-type: tm+mt
source-wordcount: '7697'
ht-degree: 0%

---


# Form Analytics with Adobe Analytics and AEM Forms - Complete Guide {#integrate-aem-forms-with-adobe-analytics}

## Vad är Form Analytics?

Formuläranalys är processen att samla in, mäta och analysera data om hur användarna interagerar med era formulär. Den ger insikter i användarbeteende, identifierar flaskhalsar i blanketternas ifyllnadsprocess och hjälper till att optimera blanketterna för bättre konverteringsgrader.

Formuläranalys handlar inte bara om enkel inskickningsspårning, utan ger omfattande insikter om alla aspekter av användarupplevelsen. Genom att analysera hur användare interagerar med enskilda formulärfält, navigeringsmönster och slutförandebeteenden kan organisationer göra datadrivna förbättringar som avsevärt påverkar affärsresultaten.

### Grundläggande Form Analytics-begrepp

**Spårning av användarinteraktion**
Formuläranalys innehåller detaljerad information om hur användarna interagerar med formulär, inklusive hur mycket tid som läggs på varje fält, musrörelser, rullningsbeteende och interaktionsmönster. Dessa detaljerade data hjälper till att identifiera användarvänlighetsproblem och optimeringsmöjligheter.

**Beteendemönsteranalys**
Genom att analysera användarbeteendemönster i flera olika sessioner kan man identifiera vanliga användarresor, typiska överlämningspunkter och lyckade slutförandesökvägar. Denna analys möjliggör riktade förbättringar som tillgodoser användarnas behov.

**Prestandamätning**
Formuläranalys ger kvantitativa mått som mäter formulärens effektivitet, inklusive konverteringsgrader, slutförandetider, felfrekvens och indikatorer för användarnöjdhet. Dessa mätvärden möjliggör en objektiv bedömning av formulärprestanda och optimeringseffekt.

### Varför Form Analytics är viktigt för företag

Formuläranalys omvandlar rådata från användarinteraktion till användbara företagsinsikter som ger mätbara förbättringar över viktiga affärsvärden:

**Optimering av konverteringsgrad**
Att överge formulär är en kritisk utmaning som direkt påverkar intäkter och generering av leads. Forskningen visar att 68 % av användarna överger formulären innan de fylls i, vilket gör att formuläranalyser är avgörande för att identifiera bortfallspunkter. Formuläranalys möjliggör målinriktade konverteringsoptimeringsstrategier som avsevärt kan öka formulärets prestanda. Effektiv konverteringsoptimering med hjälp av formuläranalys ger mätbara förbättringar när det gäller generering av leads och kundvärvning.

**Förbättring av användarupplevelsen**
Genom att förstå användarproblem och problem kan organisationer skapa smidigare och mer intuitiva formulärupplevelser. Detta leder till nöjdare kunder, lägre supportkostnader och förbättrad varumärkesuppfattning.

**Datadriven beslutsfattande**
I stället för att förlita sig på antaganden eller bästa metoder ger formuläranalysen konkreta data om användarbeteendeanalys. Detta möjliggör evidensbaserad konverteringsoptimering som ger avsevärt bättre resultat än intuitionsbaserade ändringar. Med användarbeteendeanalys via spårning av formulärprestanda kan optimeringsarbetet fokuseras på faktiska användarbehov snarare än antaganden.

**ROI-mätning och -justering**
Formuläranalys kvantifierar effekten av optimeringssatsningar och ger tydliga mätvärden som visar affärsvärdet. Man kan mäta den direkta korrelationen mellan formulärförbättringar och affärsresultat som generering av leads, konvertering och kundvärvningskostnader.

**Konkurrensfördel**
Överlägsna formulärupplevelser blir en konkurrensfördel när det gäller kundvärvning. Organisationer som använder blankettanalys kan skapa användarupplevelser i toppklass som presterar bättre än konkurrenterna och som ökar tillväxten av marknadsandelar.

### Analysmått för nyckelformulär

Effektiv formuläranalys fokuserar på mätvärden som direkt påverkar affärsresultatet och ger användbara insikter för optimering:

**Primära framgångsmått**

- **Konverteringsgrad för formulär**: Procentandel formulärvyer som resulterar i slutförda inskickade formulär - det ultimata måttet på formuläreffektivitet
- **Återgivningsfrekvens för formulär**: Var och varför användare faller bort, vilket ger direkt insikt i användarupplevelseproblem
- **Slutförandetid**: Hur lång tid det tar för användare att fylla i formulär, vilket anger komplexitet och kvalitet på användarupplevelsen

**Detaljerade prestandaindikatorer**

- **Fältnivåanalys**: Vilka specifika fält orsakar problem, vilket möjliggör riktade optimeringsåtgärder
- **Felintervallanalys**: Verifieringsproblem och användarmisstag som förhindrar att formuläret fylls i
- **Mönster för hjälpanvändning**: När och var användare behöver hjälp, vilket anger områden som ska förbättras

**Avancerade beteendemått**

- **Konverteringstrattanalys**: Användarresa via flerstegsformulär som visar förlopps- och bortfallsmönster
- **Prestanda för enhet och webbläsare**: Tekniska faktorer som påverkar slutförandet i olika användarmiljöer
- **Djup för användarengagemang**: Tid som har ägnats åt formulär, interaktionsmönster för fält och indikatorer för användaruppmärksamhet

**Business Impact Metrics**

- **Kvalitetskorrelation för lead**: Hur formulärslutförandebeteendet relaterar till leadkonvertering och kundvärde
- **Traffic Source Performance**: Vilka marknadsföringskanaler genererar formulärinskickat material av högsta kvalitet
- **Säsongs- och kampanjeffekter**: Hur formulärprestanda varierar med marknadsföringsaktiviteter och externa faktorer

## Fördelar med Form Analytics

Implementera blankettanalys ger mätbart affärsvärde i flera dimensioner. Organisationer som använder sig av blankettanalys ser ofta betydande förbättringar av konverteringsgraden, användarnöjdheten och effektiviteten.

### &#x200B;1. Minska antalet blanketter och öka konverteringsgraden

Att överge formulär är en kritisk utmaning som direkt påverkar intäkter och generering av leads:

- **Identifiera brytpunkter**: Spåra exakt var användare överger formulär för att identifiera problematiska fält eller avsnitt
- **Optimera formulärflöde**: Ordna om, förenkla eller ta bort fält som orsakar den högsta avhoppsfrekvensen
- **Förbättringar av A/B-tester**: Testa olika formulärvariationer och mät deras inverkan på slutförandefrekvensen
- **Mobiloptimering**: Identifiera mobilspecifika problem som förhindrar att formuläret fylls i
- **Realtidsövervakning**: Få aviseringar direkt när formulärprestanda försämras

**Affärspåverkan**: Företag ser vanligtvis en avsevärd förbättring av formulärkonverteringsgraden efter att de implementerat analysdrivna optimeringar.

### &#x200B;2. Förbättra användarupplevelsen och tillfredsställelsen

Formuläranalys ger djupgående insikter om användarbeteenden och problempunkter:

- **Minska slutförandetid**: Identifiera fält som tar för lång tid att slutföra och effektivisera processen
- **Minimera användarfrustration**: Spåra felmönster och valideringsproblem för att förbättra formuläranvändbarheten
- **Optimera fältordning**: Ordna fält i den mest logiska och användarvänliga sekvensen
- **Förbättra hjälp och vägledning**: Identifiera var användarna behöver hjälp och ge riktad hjälp
- **Upplevelse mellan olika enheter**: Säkerställ konsekventa prestanda på datorer, surfplattor och mobila enheter

**Affärspåverkan**: Förbättrad användarupplevelse leder till högre kundnöjdhetspoäng och ökad varumärkeslojalitet.

### &#x200B;3. Förbättra datadrivna formulär

Ersätt gissningar med konkreta data när du optimerar formulär:

- **evidensbaserade beslut**: Använd faktiska användarbeteendedata i stället för antaganden för att vägleda förbättringar
- **Mät optimeringseffekt**: Kvantifiera resultatet av formulärändringar med före/efter-analys
- **Prioritera förbättringar**: Fokusera på ändringar som har störst påverkan på affärsstatistik
- **Kontinuerlig optimering**: Upprätta pågående förbättringscykler baserat på prestandadata
- **Intressentrapportering**: Ange konkreta mått för att visa formulärprestanda och avkastning

**Affärspåverkan**: Datadriven optimering ger normalt betydligt bättre resultat än intuitionsbaserade ändringar.

### &#x200B;4. Öka lead-kvalitet och säljeffektivitet

Formuläranalys hjälper till att optimera inte bara kvantitet utan även kvalitet på inskickade formulär:

- **Integrering av leadpoäng**: Korrelera formulärbeteende med leadkvalitet och konverteringspotential
- **Source Attribution**: Förstå vilka trafikkällor som genererar formulärinskickat material av högsta kvalitet
- **Progressiv profilering**: Optimera flerstegsformulär för att samla in mer kvalificerade leads
- **Segmenteringsinsikter**: Identifiera mönster i kundformulärsbeteenden med högt värde
- **Optimering av försäljningsleverans**: Tillhandahåll säljteam med kontext om interaktioner med lead-formulär

**Affärspåverkan**: Högre kvalitet leder till högre konverteringsgrad och minskade kundanskaffningskostnader.

### &#x200B;5. Driftseffektivitet och kostnadsminskning

Formuläranalys driver verksamhetsförbättringar i hela organisationen:

- **Minska supportbiljetterna**: Identifiera och åtgärda vanliga formulärproblem som genererar kundservicesamtal
- **Automatisera optimering**: Ställ in automatiska aviseringar och optimeringsregler baserat på prestandatrösklar
- **Resursallokering**: Fokusera utvecklingsresurser på formulär och fält med störst affärseffekt
- **Regelefterlevnadsövervakning**: Spåra formulärprestanda för regelefterlevnad och tillgänglighetsefterlevnad
- **Integrationseffektivitet**: Optimera integreringar mellan formulär och system baserat på överföringsmönster

**Affärspåverkan**: Operativa förbättringar kan avsevärt minska kostnaderna för formulärrelaterad support.

### &#x200B;6. Konkurrensfördelar genom överlägsen Forms

Med formuläranalys kan organisationer skapa förstklassiga formulärupplevelser:

- **Prestanda för prestandatest**: Jämför formulärprestanda med branschstandarder och konkurrenter
- **Innovationsmöjligheter**: Identifiera unika optimeringsmöjligheter som konkurrenter kan missa
- **Kundlagring**: Överlägsna formulärupplevelser bidrar till kundnöjdhet och kundlojalitet
- **Marknadsdifferentiering**: Använd insikter från formuläranalyser för att skapa konkurrensfördelar i användarupplevelsen
- **Skalbar optimering**: Använd framgångsrika formulärmönster för flera produkter och kampanjer

**Affärspåverkan**: Överlägsna formulärupplevelser kan bli en viktig konkurrensfördel när det gäller kundvärvning.

## Exempel på formuläranalys

Genom att förstå hur formuläranalyser tillämpas på verkliga scenarier kan organisationer identifiera optimeringsmöjligheter och implementera effektiva mätstrategier. Här är några vanliga användningsområden i olika branscher och formulärtyper.

### E-handel och detaljhandel Forms

**Checka ut och betala Forms**

- **Utmaning**: Avstående från stora kundvagnar under utcheckningsprocessen påverkar direkt intäkterna
- **Lösning för formuläranalys**: Spåra antalet ifyllningar fält för fält och formulärprestanda för att identifiera friktionspunkter
- **Vanliga resultat**: Kreditkortsfält, leveransadressvalidering och kontoskapande leder ofta till att formulär överges
- **Resultat av konverteringsoptimering**: Återförsäljare ser vanligtvis en avsevärd förbättring av slutförandet av utcheckning efter analysdriven optimering av formulärprestanda
- **Analys av användarbeteende**: Spåra mönster för övergivna kundvagnar för att förstå när och varför kunder lämnar kassan
- **Affärspåverkan**: Minskad nedläggning av formulär innebär direkt ökade intäkter och förbättrade kostnader för kundförvärv

**Produktregistrering och garanti Forms**

- **Utmaning**: Låga registreringsfrekvenser som påverkar kundsupport och marknadsföring
- **Analyslösning**: Övervaka slutförandefrekvens och identifiera valfri kontra nödvändig fältpåverkan
- **Optimeringsstrategi**: Minska antalet obligatoriska fält och förbättra mobilupplevelsen
- **Affärspåverkan**: Högre registreringsfrekvenser förbättrar kundens livstidsvärde och supporteffektivitet

### Leadgenerering och B2B Forms

**Kontakta och demonstrera Forms**

- **Utmaning**: Balanserar lead-kvalitet med slutförandefrekvens för formulär och minimerar avbrutna formulär
- **Lösning för formuläranalys**: Spåra korrelation mellan formulärprestanda, formulärlängd och lead-konverteringskvalitet
- **Viktiga insikter**: Progressiv profilering fungerar ofta bättre än långa enkelsidiga formulär för konverteringsoptimering
- **Analys av användarbeteende**: Övervaka hur formulärets längd påverkar antalet slutföranden och poängen för leads
- **Resultat av konverteringsoptimering**: B2B-företag ser en betydande förbättring av generering av kvalificerade leads genom optimering av formulärprestanda
- **Affärspåverkan**: Bättre formuläranalyser leder till leads med högre kvalitet och förbättrade konverteringsgrader

**Webbinarium och händelseregistrering**

- **Utmaning**: Maximera händelsens närvaro när nödvändig information samlas in
- **Analyslösning**: Övervaka registreringsslutförande kontra faktisk närvaro
- **Vanliga mönster**: kortare formulär ökar registreringarna men kan minska närvarokvaliteten
- **Bästa praxis**: Använd analyser för att hitta en optimal balans mellan formulärlängd och deltagarkvalitet

### Finansiella tjänster Forms

**Lån- och kreditansökningar**

- **Utmaning**: Komplexa flerstegsprogram med hög avhoppsfrekvens
- **Analyslösning**: Spåra slutförandefrekvensen i varje steg och identifiera bortfallspunkter
- **Kritiska insikter**: Stegen för dokumentöverföring och inkomstverifiering leder ofta till att dokumentet överges
- **Optimeringsstrategi**: Ange tydliga förloppsindikatorer och funktioner för att spara och återuppta
- **Regelbundna överväganden**: Analyserna måste uppfylla sekretesskraven för finansiella data

**Försäkringsoffert och anspråk, Forms**

- **Utmaning**: Samlar in detaljerad information samtidigt som användarengagemanget bibehålls
- **Analyslösning**: Övervaka time-to-complete och engagemang på fältnivå
- **Viktiga resultat**: Automatisk ifyllning och smarta standardvärden förbättrar avsevärt antalet slutförda filer
- **Affärspåverkan**: Förbättrad ifyllnad av formulär har direkt samband med konverteringsgrader för principer

### Hälso- och sjukvård Forms

**Patientregistrering och -användning Forms**

- **Utmaning**: Samla in omfattande medicinsk information effektivt
- **Analyslösning**: Spåra antalet slutförda data för olika patientdemografinivåer
- **Hjälpmedelsfokus**: Övervaka prestanda på olika enheter och hjälpmedelsverktyg
- **Optimeringsprioritet**: Mobiloptimering är avgörande för patientnöjdhet
- **Krav för efterlevnad**: HIPAA-kompatibilitet är nödvändig för alla analysimplementeringar

**Schemaläggning av avtalade tider för Forms**

- **Utmaning**: Minska antalet bildspel samtidigt som bokningsprocessen förenklas
- **Analyslösning**: Korrelera formulärslutförandebeteende med mötesnärvaro
- **Viktiga insikter**: Inställningarna för bekräftelse och påminnelse påverkar närvaron avsevärt
- **Integreringsmöjlighet**: Koppla samman formuläranalyser med system för hantering av möten

### Utbildningsinstitution Forms

**Program och registrering Forms**

- **Utmaning**: Hantera komplexa flerstegsprogram med dokumentkrav
- **Analyslösning**: Spåra slutförandehastigheter i olika programfaser
- **Kritiska värden**: Tid för slutförande och Spara och återuppta användningsmönster
- **Optimeringsfokus**: Mobilupplevelsen blir allt viktigare för studentapplikationer
- **Säsongsrelaterade överväganden**: Prestanda varierar avsevärt under programperioder

**Kursregistrering och feedback för Forms**

- **Utmaning**: Maximera elevernas engagemang med administrativa processer
- **Analyslösning**: Övervaka slutförandefrekvensen och identifiera problem med användarupplevelsen
- **Viktiga insikter**: Integrering med studentportaler förbättrar slutförandefrekvensen
- **Kontinuerlig förbättring**: Regelbunden analys är nödvändig för optimering av termin-över-termin

### Scenarier med gemensam formuläranalys

**Formuläroptimering i flera steg**

Flerstegsblanketter ger normalt 86 % högre konverteringsgrad än enkelsidiga blanketter när de optimeras på rätt sätt:

- **Steg-för-steg-analys**: Spåra slutförandefrekvensen i varje formulärsteg
- **Förloppsindikatorns effekt**: Mät hur förloppsindikatorn påverkar slutförandehastigheten
- **Spara och återuppta användning**: Övervaka hur sparandet av utkast påverkar det slutliga slutförandet
- **Prestanda för mobiler och stationära datorer**: Jämför slutförandehastigheten för olika enheter

**Prestandaanalys på fältnivå**

- **Obligatoriska jämfört med Valfria fält**: Analysera påverkan av fältkrav vid slutförande
- **Optimering av fältordning**: Testa olika fältsekvenser för optimalt flöde
- **Mönster för valideringsfel**: Identifiera vanliga användarmisstag och förbättra valideringen
- **Hjälptexteffektivitet**: Mät fältvägledningens påverkan på slutförandehastigheter

**Säsongs- och kampanjprestanda**

- **Traffic Source Analysis**: Jämför formulärprestanda i alla marknadsföringskanaler
- **Säsongsvariationer**: Spåra hur formulärprestanda ändras under året
- **Kampanjintegrering**: Korrelera formuläranalys med marknadsföringskampanjens resultat
- **A/B-testningsintegrering**: Använd analyser för att mäta testvariationer och optimera kontinuerligt

## Implementeringsscenarier för Real-World Form Analytics

Genom att förstå specifika implementeringsscenarier kan man effektivt använda formuläranalyser i olika affärskontexter. Exemplen visar hur prestandaspårning och konverteringsoptimering ger mätbara affärsresultat.

### Optimering av e-handelskassa

**Scenario**: Onlinebutiken upplever att en stor kundvagn överges vid utcheckning

- **Implementering av formuläranalys**: Spåra kundvagnsavhoppning på formulärnivå med fältanalys
- **Nyckelsökningar**: När betalningsformuläret fylldes i minskade antalet betydligt vid verifiering av kreditkort
- **Strategi för konverteringsoptimering**: Förenklat betalningsformulär, nya förloppsindikatorer, optimerad mobilupplevelse
- **Resultat**: Avbrutna formulär har reducerats avsevärt och intäkterna har ökat
- **Analys av användarbeteende**: Identifierade mobilanvändare hade högre avhoppsfrekvens, vilket ledde till att mobilen först designades om

### Formuläroptimering för leadgenerering

**Scenario**: B2B-programvaruföretag som har problem med leads av låg kvalitet från kontaktformulär

- **Utmaning med formulärprestanda**: Hög andel ifyllda formulär men dålig konvertering från lead till kund
- **Analyslösning**: Korrelera formulärslutförandebeteende med ledkvalitet och försäljningsresultat
- **Optimeringsmetod**: Implementerad progressiv profilering och integrering av lead-poäng
- **Affärspåverkan**: Betydande förbättring av leads och ökning av säljkvalificerade leads
- **Konverteringsoptimering**: Minskad formuläravslut samtidigt som lead-kvalificering förbättras

### Optimering av registrering och introduktion

**Scenario**: SaaS-plattform med hög avanmälan av registreringar under introduktionsprocessen

- **Analys av användarbeteende**: Spåra antalet slutförda registreringar och identifiera flaskhalsar för introduktion
- **Insikter från formuläranalys**: En betydande användarbortgång inträffade under kontoverifieringssteget
- **Optimeringsstrategi**: Effektivare verifieringsprocess, tillagd funktion för Spara och återuppta
- **Resultat**: Ökade antalet slutförda registreringar avsevärt och ökade användaraktiveringshastigheten
- **Långsiktig effekt**: Bättre slutförande av introduktionen korrelerade med högre livstidsvärde för kunder

## Funktioner för formuläranalys i Adobe Analytics

Adobe Analytics har funktioner för blankettspårning i enterpriseklass som gör det möjligt att inhämta detaljerade insikter om användarinteraktioner i blanketterna. Den smidiga integrationen med AEM Forms erbjuder både kraftfulla färdiga analysfunktioner och avancerade anpassningsalternativ som kan anpassas efter företagets behov.

### Varför välja Adobe Analytics för formuläranalys

**Prestanda för företagsskala**
Adobe Analytics hanterar miljontals formulärinteraktioner utan prestandaförluster, vilket gör det idealiskt för webbplatser med hög trafik och komplexa företagsmiljöer. Plattformens robusta infrastruktur säkerställer tillförlitlig datainsamling även under perioder med hög användning.

**Avancerade segmenteringsfunktioner**
Till skillnad från grundläggande verktyg för formuläranalys möjliggör Adobe Analytics avancerad användarsegmentering baserat på beteende, demografiska data, trafikkällor och anpassade affärskriterier. Detta gör att ni kan använda målinriktade optimeringsstrategier för specifika användargrupper och scenarier.

**Insikter och varningar i realtid**
Övervaka formulärprestanda när det händer med realtidskonsoler och automatiska varningar. Identifiera och åtgärda problem direkt och förhindra potentiella intäktsförluster till följd av formulärproblem eller prestandaförsämringar.

### Spårningsfunktioner som är färdiga att användas

AEM Forms integreras smidigt med [Adobe Analytics](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/overview.html?lang=sv-SE) för att automatiskt hämta in och spåra prestandamått för dina publicerade formulär. Du kan övervaka beteendet för både autentiserade och anonyma användare utan ytterligare konfiguration.

Innan du implementerar formuläranalys bör du kontrollera att din [AEM Forms-miljö är korrekt konfigurerad](/help/forms/setup-forms-cloud-service.md) och du har [skapat dina adaptiva formulär](/help/forms/creating-adaptive-form-core-components.md) med hjälp av antingen Core Components eller [Foundation Components](/help/forms/creating-adaptive-form.md).

**Omfattande spårning av formulärhändelser:**

Adobe Analytics tar automatiskt fram en komplett bild av interaktionen med användarformulären:

- **Formuläråtergivning**: Spåra formuläravtryck och vyer för att förstå räckvidd och ursprungligt engagemang
- **Formuläröverföringar**: Övervaka slutförda formulär med detaljerad information om inskickningskontext och användarresa
- **Analys av formuläravhopp**: Fånga exakta avhoppspunkter med granularitet på fältnivå och användarsessionskontext
- **Spårning av verifieringsfel**: Registrera feltyper, frekvens och lösningsmönster för att identifiera användbarhetsproblem
- **Användning av hjälpinnehåll**: Övervaka när användare får åtkomst till hjälpresurser, vilket anger förvirrande eller komplexa områden
- **Interaktioner på fältnivå**: Spåra interaktion, tid och interaktionsmönster för enskilda fält
- **Beteende för att spara utkast**: Förstå användaravsikt och formulärkomplexitet genom att spara och återuppta användningsmönster
- **Spårning mellan sessioner**: Följ användare i flera formulärsessioner för att förstå slutföranderesor

**Avancerade beteendeinsikter:**

- **Tid-för-fält-analys**: Mät hur lång tid användarna lägger på varje formulärfält för att identifiera komplexa problem
- **Mönster för musrörelse**: Spåra användarnas tveksamhet och engagemang genom analys av markörbeteenden
- **Spårning av rullningsdjup**: Förstå hur användare navigerar i långa formulär och identifiera optimal formulärlängd
- **Mönster för felåterställning**: Analysera hur användare svarar på och återställer valideringsfel

### Anpassad händelsespårning

Förutom standardformulärhändelser möjliggör Adobe Analytics avancerad, anpassad spårning:

- **Affärsspecifika mått**: Definiera anpassade händelser med regelredigeraren för att spåra organisationsspecifika formulärinteraktioner
- **Mappning av användarresor**: Skapa anpassade händelser för att spåra komplexa användarsökvägar via flerstegsformulär
- **Konverteringsflödesanalys**: Ställ in anpassade händelser för att mäta specifika konverteringspunkter och släppningsfaser
- **Integrationshändelser**: Spåra formulärinteraktioner med externa system och API:er

### Avancerade rapporteringsfunktioner

Adobe Analytics har funktioner för rapportering i enterpriseklass för att få fram blanketter:

- **Real-Time Dashboards**: Övervaka formulärprestanda och användarinteraktioner när de inträffar
- **Segmenteringsanalys**: Analysera formulärprestanda för olika användargrupper, trafikkällor och demografiska data
- **Tratt Visualization**: Visualisera användarstatus via flerstegsformulär och identifiera optimeringsmöjligheter
- **Kohortanalys**: Spåra prestandaförbättringar för formulär över tid och mät optimeringseffekten
- **Spårning mellan enheter**: Förstå hur användare interagerar med formulär på olika enheter och sessioner

### Integreringsfördelar

Integreringen mellan Adobe Analytics och AEM Forms ger unika fördelar:

- **Enhetlig dataplattform**: Kombinera formuläranalyser med bredare webbplats- och marknadsföringsanalyser
- **Adobe Experience Cloud-integrering**: Utnyttja anslutningar med Adobe Target, Campaign och andra Experience Cloud-lösningar
- **Företagssäkerhet**: Inbyggd kompatibilitet med datasekretesbestämmelser och företagssäkerhetskrav
- **Skalbar arkitektur**: Hantera formulärinteraktioner i stora volymer utan prestandapåverkan
- **Professional Support**: Tillgång till Adobe Enterprise Support och optimeringstjänster

När du har implementerat de integrationssteg som beskrivs i den här artikeln kan du konfigurera och visa omfattande rapporter i [!DNL Adobe Analytics], vilket visas i följande video:

>[!VIDEO](https://video.tv.adobe.com/v/337262)

## Viktiga analysvärden för formulär som ska spåras

Framgångsrik implementering av blankettanalys kräver fokusering på mätvärden som direkt påverkar affärsresultatet. Genom att förstå vilka mätvärden som ska prioriteras kan organisationer fatta datadrivna beslut och optimera formulärprestanda effektivt.

### Primära prestandamått

**Konverteringsgrad för formulär**

- **Definition**: Procentandel av formulärvyer som resulterar i slutförda överföringar
- **Beräkning**: (Formulärinskickningar/Formulärvningar) × 100
- **Affärspåverkan**: Korrelerar direkt till mål för leadgenerering och intäkter
- **Optimeringsmål**: Varierar utifrån bransch- och formulärkomplexitet

**Återgivningsfrekvens för formulär**

- **Definition**: Procentandel användare som startar men inte fyller i formulär
- **Beräkning**: (Formuläret börjar - Formulärkompileringar) / Formulärbörjar × 100
- **Viktiga insikter**: Identifierar problem med användarupplevelsen och optimeringsmöjligheter
- **Benchmark**: Höga avhoppsfrekvenser visar vanligtvis på betydande användbarhetsproblem

**Genomsnittlig slutförandetid**

- **Definition**: Genomsnittlig tid som användare lägger på att fylla i formulär från början till slut
- **Analysfokus**: Identifiera formulär som tar för lång tid och kan frustrera användare
- **Optimeringsmål**: Balansera noggrannhet med användarupplevelseeffektivitet
- **Segmentering**: Jämför slutförandetider mellan enheter, användartyper och trafikkällor

### Fältnivåanalys

**Frekvenser för fältöverlämning**

- **Mätning**: Procentandel användare som överger formulär i specifika fält
- **Optimeringsvärde**: Identifierar problematiska fält som behöver förenklas eller tas bort
- **Vanliga problem**: Komplexa valideringskrav, otydliga instruktioner eller tekniska problem
- **Åtgärdsobjekt**: Prioritera optimeringsåtgärder för fält med högsta avhoppsfrekvens

**Mönster för fältinteraktion**

- **Klickfrekvens**: Procentandel användare som arbetar med specifika formulärfält
- **Tid i fält**: Genomsnittlig tid för användare i enskilda fält
- **Felfrekvens**: Frekvens för valideringsfel för specifika fält
- **Hjälpanvändning**: Hur ofta användare öppnar hjälpinnehåll för vissa fält

**Färdigställningsgrad för fält**

- **Progressiv analys**: Spåra antalet slutförda åtgärder när användarna förflyttar sig mellan formulärfält
- **Identifiering av bortfall**: Hitta exakta platser där användare överger formulär
- **Optimeringsprioritet**: Fokusförbättringar för fält med stegvis minskning av slutförandegrad

### Mätvärden för användarupplevelser

**Analys av felfrekvens**

- **Valideringsfel**: Frekvens och typer av formulärvalideringsfel
- **Tekniska fel**: Problem på systemnivå som påverkar formulärfunktioner
- **Mönster för användarfel**: Vanliga misstag som användare gör när de fyller i formulär
- **Upplösningsspårning**: Övervaka hur felhastighetsförbättringar påverkar den övergripande konverteringen

**Prestanda för mobil och dator**

Mobilformulär har oftast 30 % högre avhoppsfrekvens jämfört med datorversioner, vilket gör enhetsspecifik optimering avgörande:

- **Enhetsspecifika konverteringsgrader**: Jämför formulärprestanda mellan enhetstyper
- **Responsiv designeffekt**: Mät hur mobiloptimering påverkar slutförandehastigheten
- **Synlighet för Touch Interface**: Analysera mobilspecifika interaktionsmönster
- **Enhetsövergripande resa**: Spåra användare som startar formulär på en enhet och fyller i på en annan

**Mätvärden för sidinläsning och prestanda**

Forms som läses in på mindre än 3 sekunder har 70 % högre slutförandegrad än långsammare formulär:

- **Inläsningstid för formulär**: Tid som krävs för att formulär ska kunna återges fullständigt och bli interaktiva
- **Fältsvarstid**: Latens mellan användarindata och systemsvar
- **Bearbetningstid för överföring**: Varaktighet från formulärsändning till bekräftelse
- **Prestandaeffekt**: Korrelation mellan inläsningstider och avhoppsfrekvens

### Avancerade analysvärden

**Analys av användarsegmentering**

- **Trafik Source Performance**: Jämför formulärkonverteringsgrader i alla marknadsföringskanaler
- **Geografiska prestanda**: Analysera antalet slutförda formulär efter plats och språk
- **Analys av användartyp**: Jämför prestanda mellan nya och returnerade användare
- **Demografiska insikter**: Förstå hur olika användargrupper interagerar med formulär

**Konverteringsflödeanalys**

- **Formulärprogression i flera steg**: Spåra användarens framsteg med komplexa formulär
- **Steg-för-steg-konvertering**: Mät slutförandegrad i varje formulärsteg
- **Tratt Optimization**: Identifiera och åtgärda flaskhalsar i formulärutvecklingen
- **Integrering av A/B-tester**: Jämför trattprestanda för olika formulärvarianter

**Business Impact Metrics**

- **Kvalitetsbedömning för leads**: Korrelera formulärslutförandebeteende med konverteringsgrader för leads
- **Intäktsattribuering**: Koppla formuläröverföringar till faktiska affärsresultat
- **Kundens livstidsvärde**: Analysera långsiktigt värde för användare som har förvärvats via olika formulär
- **Kostnad per anskaffning**: Beräkna marknadsföringseffektivitet baserat på data för formulärprestanda

Följande bild visar vilka åtgärder du behöver utföra innan du visar rapporter i [!DNL Adobe Analytics]:

![Analysöversikt](assets/analytics-workflow.png)

## Konfigurera formuläranalys för AEM Forms

Implementering av blankettanalys med Adobe Analytics och AEM Forms kräver systematisk konfiguration för flera komponenter. Det här avsnittet innehåller omfattande riktlinjer för konfiguration, krav och bästa praxis för att implementeringen ska lyckas.

### Krav och krav

Innan du börjar implementera formuläranalysen måste du kontrollera att miljön uppfyller följande krav:

>[!NOTE]
>
>Om du får problem under installationen kan du läsa vår omfattande [felsökningsguide för AEM Forms](/help/forms/troubleshooting-installation-and-configuration.md) för att få information om installations- och konfigurationsproblem.

**Adobe Experience Cloud Access**

- Giltig Adobe Experience Cloud-organisation med Adobe Analytics-licens
- Administrativ åtkomst till Adobe Analytics- och AEM Forms-miljöer
- Adobe Launch-åtkomst (Data Collection) för tagghantering och -konfiguration

**AEM Forms-miljö**

- [AEM Forms as a Cloud Service](/help/forms/setup-forms-cloud-service.md) eller AEM Forms 6.5+ (lokala/AMS-installationer)
- Funktioner för framtagning och publicering av Forms har aktiverats
- Kontrollera att alternativet [Forms är tillgängligt](/help/forms/troubleshooting-installation-and-configuration.md#forms-option-is-unavailable) i din AEM-miljö
- [Adaptiva Forms Core-komponenter](/help/forms/creating-adaptive-form-core-components.md) eller [Foundation-komponenter](/help/forms/creating-adaptive-form.md) tillgängliga

**Tekniska krav**

- Moderna webbläsare med JavaScript aktiverat för spårning av formuläranalys
- HTTPS-protokollimplementering för säker dataöverföring
- Lämpliga brandväggs- och nätverkskonfigurationer för Adobe Analytics datainsamling

**Behörigheter och åtkomst**

- Adobe Analytics administratörsroll för rapportsvitskonfiguration
- AEM Forms Author permissions for form configuration and publishing
- Adobe Launch Developer-åtkomst för taggimplementering och regelgenerering

### Implementeringshandbok steg för steg

#### &#x200B;1. Konfigurera Adobe Analytics {#Configure-adobe-analytics}

Skapa:[!DNL Adobe Analytics]

- En Adobe ID att logga in på [Adobe Experience Cloud](https://experience.adobe.com/#/home).
- En [rapportserie](https://experienceleague.adobe.com/docs/analytics/admin/manage-report-suites/new-report-suite/t-create-a-report-suite.html?lang=sv-SE).


### Installera AEM Forms och [!DNL Adobe Analytics] tillägg {#install-extensions}

Så här konfigurerar du AEM Forms- och [Adobe Analytics](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/analytics/overview.html?lang=sv-SE)-tillägg:

1. Logga in på Adobe Experience Cloud och välj ett namn för företaget.

1. Välj **[!UICONTROL Launch/Data Collection]** och välj **[!UICONTROL Go to Launch/Data Collection]**.

1. Välj **[!UICONTROL New property]** och ange ett namn för konfigurationen.

1. Ange ett domännamn och välj **[!UICONTROL Save]** för att spara egenskapen.

1. Välj det konfigurationsnamn som finns i listan Taggegenskaper.

1. Välj **[!UICONTROL Authoring]** i avsnittet **[!UICONTROL Extensions]**.

1. Välj **[!UICONTROL Catalog]** och välj **[!UICONTROL Install]** som **[!UICONTROL Adobe Experience Manager Forms]**-tillägg. **[!UICONTROL Adobe Experience Manager Forms]** visas i listan över installerade tillägg på fliken **Installed**.

1. Välj **[!UICONTROL Install]** som **[!UICONTROL Adobe Analytics]**-tillägg.
1. Välj rapportsvitens namn i listrutorna **[!UICONTROL Development Report Suites]**, **[!UICONTROL Staging Report Suites]** och **[!UICONTROL Product Report Suites]** och välj **[!UICONTROL Save]** för att spara tillägget.

### Konfigurera dataelement {#configure-data-elements}

Du kan välja vilket som helst av de konfigurerade dataelementen i en regel som skapas för en händelse. När en händelse inträffar i ett anpassat formulär skickar AEM Forms dessa dataelement till [!DNL Adobe Analytics].

När du har installerat tillägget **[!UICONTROL Adobe Experience Manager Forms]** kan du skapa följande dataelement:

<table>
 <tbody>
  <tr>
   <td>FieldName</th>
   <td>FieldTitle</th>
   <td>FormInstance</th>
  </tr>
  <tr>
   <td>FormName<br /> </td>
   <td>FormTitle<br /> </td>
   <td>PageName</td>
  </tr>
  <tr>
   <td>PageURL<br /> </td>
   <td>PanelTitle<br /> </td>
   <td>TimeSpent</td>
  </tr>
 </tbody>
</table>

Utför följande steg för att konfigurera dataelement:

1. Välj **[!UICONTROL Authoring]** i avsnittet **[!UICONTROL Data Elements]**.

1. Välj **[!UICONTROL Create New Data Element]**.

1. Ange ett namn för dataelementet. Exempel: Formulärtitel för dataelementtypen FormTitle.

1. Ange **[!UICONTROL Adobe Experience Manager Forms]** som tilläggsnamn.

1. Välj **[!UICONTROL Data Element Type]**.

1. Välj **[!UICONTROL Save]** om du vill spara dataelementet.

>[!VIDEO](https://video.tv.adobe.com/v/337472)

### Konfigurera regler {#configure-rules}

Utför följande steg för att skapa regler baserade på tillägget **[!UICONTROL Adobe Experience Manager Forms]**:

1. Välj **[!UICONTROL Authoring]** i avsnittet **[!UICONTROL Rules]**.

1. Välj **[!UICONTROL Create New Rule]**.

1. Ange ett namn för regeln. Till exempel Skicka formulär för att registrera formulärinskickade formulär.

1. Välj **[!UICONTROL Events]** i avsnittet **[!UICONTROL Add]**.

1. Ange **[!UICONTROL Adobe Experience Manager Forms]** som tilläggsnamn.

1. Välj händelsetyp. Indata för fältet **[!UICONTROL Name]** fylls i automatiskt baserat på den valda händelsetypen.

1. Välj **[!UICONTROL Keep Changes]** om du vill spara händelsen.

1. Välj **[!UICONTROL Actions]** i avsnittet **[!UICONTROL Add]**.

1. Ange **[!UICONTROL Adobe Analytics]** som tilläggsnamn.

1. Välj **[!UICONTROL Set Variables]** som åtgärdstyp. De alternativ som är tillgängliga i listrutan är bland annat:

   - **[!UICONTROL Set Variables]**: Använd den här åtgärdstypen för att definiera händelsetypen som de markerade dataelementen skickas från AEM Forms till [!DNL Adobe Analytics].

   - **[!UICONTROL Send Beacon]**: Använd den här åtgärdstypen för att skicka data från AEM Forms till [!DNL Adobe Analytics].

   - **[!UICONTROL Clear Variables]**: Använd den här åtgärdstypen för att rensa dataspårningen så att händelsen bara registreras en gång i [!DNL Adobe Analytics].

     Rekommenderat tillvägagångssätt är att använda åtgärdstypen **[!UICONTROL Set Variables]** för att konfigurera händelsen och dataelementen, sedan använda **[!UICONTROL Send Beacon]** för att skicka data och sedan använda **[!UICONTROL Clear Variables]** för att rensa dataspårningen.

1. I avsnittet **[!UICONTROL Props]** mappar du de rapportrutealternativ som är tillgängliga i listrutan med dataelementen som har definierats med [Konfigurera dataelement](#configure-data-elements).

   Om du till exempel vill skicka dataelementet **Formulärtitel** från AEM Forms till [!DNL Adobe Analytics] när du skickar ett formulär:
   1. I avsnittet **[!UICONTROL Props]** väljer du ett utkast för Formulärtitel som är tillgängligt i rapportsviten och sedan ![Databasikon](assets/database-icon.svg) för att mappa det till Formulärtitel som har skapats i [Konfigurera dataelement](#configure-data-elements).

      ![define-props](assets/define-props.png)

   1. Välj **[!UICONTROL Add Another]** om du vill lägga till fler dataelement i listan.

1. I avsnittet **[!UICONTROL Events]** väljer du en händelse bland de tillgängliga alternativen i rapportsviten och väljer **[!UICONTROL Keep Changes]**.

1. I avsnittet **[!UICONTROL Actions]** väljer du + och anger **[!UICONTROL Adobe Analytics]** som tilläggsnamn.

1. Välj **[!UICONTROL Send Beacon]** som åtgärdstyp. I den högra rutan väljer du **[!UICONTROL s.t()]** för att skicka data till [!DNL Adobe Analytics] och behandla dem som en sidvy eller **[!UICONTROL s.tl()]** för att skicka data till [!DNL Adobe Analytics] och inte som en sidvy. Välj **[!UICONTROL Keep Changes]**.

1. I avsnittet **[!UICONTROL Actions]** väljer du + och anger **[!UICONTROL Adobe Analytics]** som tilläggsnamn.

1. Välj **[!UICONTROL Clear Variables]** som åtgärdstyp. Välj **[!UICONTROL Keep Changes]**. När du har utfört de här stegen visas avsnittet **[!UICONTROL Actions]** som:
   ![Åtgärdskonfiguration](assets/actions-config.png)

   Anpassa avsnittet **[!UICONTROL Actions]** enligt dina krav. Du kan till exempel definiera två **Skicka Beacon**-steg i ett åtgärdsflöde för att skicka data till [!DNL Adobe Analytics] och behandla dem som en sidvy i ett enda steg och skicka data till [!DNL Adobe Analytics] och inte behandla dem som en sidvy i det andra steget.

   ![Åtgärdskonfiguration](assets/actions-config-2.png)

1. Välj **[!UICONTROL Save]** om du vill spara regeln.

   Du kan skapa regler för alla händelsetyper, till exempel överge, Fel, fältbesök, Hjälp, Återge, Spara och Skicka.

>[!VIDEO](https://video.tv.adobe.com/v/337425)


### Publiceringsflöden {#publish-flow}

När du har skapat dataelementen och använt dem i regler publicerar du konfigurationen för att samla in formulärdata i [!DNL Adobe Analytics].

Utför följande steg för att publicera konfigurationen:

1. Välj **[!UICONTROL Publishing]** i avsnittet **[!UICONTROL Publishing Flow]**.

1. Välj **[!UICONTROL Add Library]**, ange ett namn och markera miljön för biblioteket.

1. Välj **[!UICONTROL Add All Changed Resources]** och sedan **[!UICONTROL Save & Build to Development]**.

1. I avsnittet **[!UICONTROL Development]** väljer du ![Fler alternativ](assets/more-options-icon.svg) och sedan **[!UICONTROL Approve & Publish to Production]**.

1. Bekräfta att ändringarna och publiceringsflödet snart visas i avsnittet **[!UICONTROL Published]**.

![Publiceringsflöde](assets/publish-flow.png)

## &#x200B;2. Konfigurera AEM Forms {#configure-aem-forms}

Innan du skapar en Adobe Launch-konfiguration skapar du en [Adobe IMS-konfiguration med Adobe Launch som molnlösning](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/connect-aem-launch-adobe-io.html?lang=sv-SE).

### Skapa startkonfiguration för Adobe {#create-adobe-launch-configuration}

Så här skapar du en Adobe Launch-konfiguration:

1. I AEM Forms Author-instansen går du till **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Launch Configurations]**.

1. Välj en mapp för att skapa konfigurationen och välj **[!UICONTROL Create]**.

1. Ange en rubrik för konfigurationen i fältet **[!UICONTROL Title]**.

1. Välj den [associerade Adobe IMS-konfigurationen](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/connect-aem-launch-adobe-io.html?lang=sv-SE).

1. Välj namnet på företaget som användes när [Adobe Analytics](#Configure-adobe-analytics) konfigurerades.

1. Markera namnet på den egenskap som skapades när [Adobe Analytics](#install-extensions) konfigurerades.

1. Välj **[!UICONTROL Save & Close]**.

1. Publicera konfigurationen.

### Aktivera [!DNL Adobe Analytics] för ett anpassat formulär {#enable-analytics-adaptive-form}

Så här använder du konfigurationen [!DNL Adobe Launch] i ett befintligt adaptivt formulär:

1. I AEM Forms Author-instansen går du till **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms & Documents]**.
1. Markera det adaptiva formuläret och välj **[!UICONTROL Properties]**.
1. På fliken **[!UICONTROL Basic]** väljer du den [konfigurationsbehållare](#create-adobe-launch-configuration) som ska användas när Adobe Launch-konfigurationen skapas.
1. Välj **[!UICONTROL Save & Close]**. Det adaptiva formuläret har aktiverats för [!DNL Adobe Analytics].
1. Publicera formuläret.

När du har aktiverat [!DNL Adobe Analytics] för ett anpassat formulär kan du [validate](https://experienceleague.adobe.com/docs/launch-learn/implementing-in-websites-with-launch/implement-solutions/analytics.html?lang=sv-SE#validate-the-page-view-beacon) om det finns ett lämpligt datahändelseflöde mellan AEM Forms och [!DNL Adobe Analytics]. Integreringen av AEM Forms med Adobe Analytics är klar. Nu kan du [konfigurera och visa rapporter i Adobe Analytics](#view-reports-adobe-analytics).

### Skapa regler för att hämta anpassade händelser (valfritt) {#capture-custom-events}

Skapa regler för specifika fält i ett adaptivt formulär med en regelredigerare för att skicka analysdata från ett adaptivt formulär till [!DNL Adobe Analytics].

I en tvåstegsprocess definierar du en regel för ett fält i ett anpassningsbart format. Regeln skickar en händelse. Namnet på händelsen mappas till en anpassad inspelningshändelse i Adobe Launch.

Så här skapar du regler med en regelredigerare i ett anpassat format:

1. Markera fältet och välj ![Regelredigeraren](assets/rule-editor-icon.svg) för att öppna regelredigeringssidan.
1. Definiera ett villkor i regelns [!UICONTROL When]-avsnitt.
1. Välj [!UICONTROL Then] i listrutan **[!UICONTROL Dispatch Event]** i regelns **[!UICONTROL Select Action]**-avsnitt.
1. Ange namnet på händelsen i fältet **[!UICONTROL Type Event Name]**.

Om födelsedatumet till exempel är före ett visst datum skickar AEM Forms **Security** -händelsen.

![Utsändningshändelse](assets/security-event.png)

Så här mappar du händelsen till en anpassad fångsthändelse i [!DNL Adobe Analytics]:

1. [Skapa en regel](#configure-rules).

1. Välj **[!UICONTROL Events]** i avsnittet **[!UICONTROL Add]**.

1. Ange **[!UICONTROL Adobe Experience Manager Forms]** som tilläggsnamn.

1. Välj **[!UICONTROL Capture Custom Event]** i listrutan **[!UICONTROL Event Type]**.

1. Ange namnet på händelsen som du angav i steg 4 när du skapade en regel med regelredigeraren.

1. Välj **Behåll ändringar** och utför resten av åtgärderna som anges i [Konfigurera regler](#configure-rules).

## &#x200B;3. Konfigurera och visa rapporter i [!DNL Adobe Analytics] {#view-reports-adobe-analytics}

När du har konfigurerat ett adaptivt formulär för att skicka händelsedata till [!DNL Adobe Analytics] kan du börja visa rapporter i [!DNL Adobe Analytics]:

1. Välj ![Välj Produkt](assets/select-analytics.png) och välj **[!UICONTROL Analytics]**.

1. Välj **[!UICONTROL Create Project]** och välj **[!UICONTROL Blank project]**.

1. Välj rapportsvitens namn i listrutan högst upp till höger på frihandsformuläret.

1. Ange **Formulärtitel** i texten **[!UICONTROL Search dimension items]** om du vill visa alla formulärtitlar.

1. Släpp den anpassningsbara formulärtiteln i textrutan **[!UICONTROL Drop a segment here (or any other component)]**.

1. I avsnittet **[!UICONTROL Metrics]** släpper du de händelser som ska spåras i textrutan **[!UICONTROL Drop a metric here (or any other component)]**.

1. Välj ![Visualiseringar](assets/visualization-icon.svg) och släpp en diagramtyp i avsnittet Frihand. På samma sätt kan du lägga till flera diagramtyper i avsnittet Frihand.

1. Markera Ctrl + S och ange ett namn för att spara projektet.

<!--

## Add AEM Forms and Adobe Analytics integration specific rules to Dispatcher {#forms-specific-rules-to-dispatcher}

Add AEM Forms and Adobe Analytics integration specific rules to filter the data traffic that is sent to the backend.

Perform the following steps to add AEM Forms and Adobe Analytics integration specific rules to Dispatcher for Experience Manager Forms as a Cloud Service:

1. Open your AEM Project and navigate to `\src\conf.dispatcher.d\filters`.
1. Open `filters.any` file for editing and add the following rule at the end of the file:

     ```json
     /00XX { /type "allow" /path "/content/forms/af/*" /method "POST" /selectors '(analyticsconfigparser)' /extension '(jsp|json)' }
     ```

1. Save and close the file.
1. Compile and deploy the project to your [!DNL AEM Forms] as a Cloud Service environment.



## Limitations {#limitations}

* Adobe Analytics can track form metrics only for authenticated users.

-->

## Konfiguration av avancerad formuläranalys

Förutom grundläggande konfiguration erbjuder Adobe Analytics avancerade konfigurationsalternativ som möjliggör avancerad formulärspårning och analysfunktioner. Dessa avancerade funktioner hjälper organisationer att få djupare insikter och implementera komplexa analysscenarier.

### Anpassade händelser och spårning

**Skapar anpassade formulärhändelser**

Anpassade händelser möjliggör spårning av affärsspecifika interaktioner som går utöver standardformuläranalyser:

- **Affärsprocesshändelser**: Spåra formulärinteraktioner som följer specifika affärsarbetsflöden
- **Händelser för användarengagemang**: Mät avancerade användarbeteenden som förhandsgranskning av formulär, användning av fälthjälp eller komplettering av avsnitt
- **Integrationshändelser**: Övervaka formulärinteraktioner med externa system, API:er eller tredjepartstjänster
- **Prestandahändelser**: Spåra anpassade prestandamått som inläsningstider för formulär eller svarshastighet för fält

**Implementeringsmetod**

1. **Definiera affärskrav**: Identifiera specifika formulärinteraktioner som ger affärsvärde
2. **Skapa anpassade variabler**: Konfigurera anpassade eVars- och props i Adobe Analytics för företagsspecifika data
3. **Konfigurera regelredigerare**: Använd regelredigeraren i AEM Forms för att utlösa anpassade händelser baserat på formulärinteraktioner
4. **Mappa till analyshändelser**: Koppla anpassade formulärhändelser till Adobe Analytics händelsespårning
5. **Verifiera implementering**: Testa anpassade händelser för att säkerställa korrekt datainsamling och rapportering

### Avancerade rapporteringsinställningar

**Konfiguration för flerdimensionell analys**

- **Formuläranalys**: Jämför prestanda för olika formulärtyper och affärsprocesser
- **Mappning av användarresor**: Spåra användarinteraktioner i flera formulär och kontaktytor
- **Attributmodellering**: Förstå hur olika marknadsföringskanaler bidrar till att fylla i formulär
- **Kohortanalys**: Analysera förbättringar av formulärprestanda över tid och användarsegment

**Konfiguration för realtidsrapportering**

- **Live Dashboard-installation**: Konfigurera övervakning av formulärprestanda i realtid
- **Varningskonfiguration**: Ställ in automatiska varningar för problem med formulärprestanda eller avvikelser
- **Prestandatrösklar**: Definiera godtagbara prestandaintervall och övervakningsutlösare
- **Intressentrapporter**: Skapa automatiserade rapporter för olika organisationsroller och ansvarsområden

### Integrering med andra Adobe-verktyg

**Adobe Target-integrering**

- **A/B-testning**: Testa olika formulärvariationer och mät påverkan på prestanda
- **Personalization**: Leverera personaliserade formulärupplevelser baserat på användarbeteende och analysdata
- **Optimering**: Använd analysinsikter för att informera om optimeringsstrategier för mål
- **Konverteringsoptimering**: Kombinera formuläranalyser med bredare konverteringsoptimering

**Adobe Campaign-integrering**

- **Leadstrukturering**: Använd data från formuläranalyser för att informera om e-postmarknadsföring och lead-vårdskampanjer
- **Segmentering**: Skapa användarsegment baserat på beteende och engagemangsmönster för formulärslutförande
- **Kampanjattribuering**: Spåra hur marknadsföringskampanjer påverkar formulärprestanda och slutförandegrad
- **Livscykelmarknadsföring**: Integrera formuläranalyser med bredare marknadsföringsstrategier under kundens livscykel

## Rapporter och insikter från Form Analytics

Att förstå hur man tolkar och agerar på data från formuläranalyser är avgörande för att optimeringen ska lyckas. I det här avsnittet beskrivs viktiga rapporter, instrumentpanelskonfiguration och extrahering av åtgärdbara insikter.

### Förstå er analyspanel

**Instrumentpanel för KPI (Key Performance Indicators)**

- **Formulärkonverteringsfunktion**: Visa användarförlopp genom formulärslutförandeprocessen
- **Avgränsningsanalys**: Identifiera specifika punkter där användare lämnar formulär ofullständiga
- **Prestandatender**: Spåra ändringar av formulärprestanda över tid och identifiera mönster
- **Jämförelseanalys**: Jämför prestanda i olika formulär, tidsperioder och användarsegment

**Kontrollpanel för användningsmått**

- **Aktivitet i realtid av formulär**: Övervaka aktuell formuläranvändning och slutförandefrekvens
- **Övervakning av felfrekvens**: Spåra verifieringsfel och tekniska problem som påverkar formulärprestanda
- **Prestanda för enhet och webbläsare**: Analysera formulärprestanda i olika tekniska miljöer
- **Geografiska prestanda**: Förstå hur formulärprestanda varierar beroende på plats och språk

### Viktiga rapporter att övervaka

**Dagliga prestandarapporter**

- **Sammanfattning av slutförda formulär**: Daglig översikt över formulärinskickade formulär, avhoppsfrekvens och konverteringsmått
- **Felanalys**: Daglig spårning av formulärfel, valideringsproblem och tekniska problem
- **Traffic Source Performance**: Analys av hur olika marknadsföringskanaler skapar formulärslutföranden
- **Prestanda för mobil och dator**: Jämförelseanalys av formulärprestanda för olika enhetstyper

**Trendanalys varje vecka**

- **Prestandatrendidentifiering**: Vecka över vecka-analys av förbättringar eller avböjningar av formulärprestanda
- **Mönster för användarbeteende**: Veckoanalys av mönster för användarinteraktion och trender för engagemang
- **Optimeringspåverkan**: Utvärdering av hur formulärändringar påverkar prestandamått
- **Konkurrensjämförelse**: Jämförelse mellan formulärprestanda och branschstandarder och riktmärken

**Strategiska månadsrapporter**

- **ROI-analys**: Månatlig utvärdering av formuläranalysens påverkan på affärsresultat och intäkter
- **Insikter om användarupplevelser**: Omfattande analys av förbättringar av användarupplevelsen och optimeringsmöjligheter
- **Integreringsprestanda**: Analys av hur integreringen av formuläranalyser påverkar bredare marknadsföring och affärsprocesser
- **Strategiska rekommendationer**: Datadrivna rekommendationer för formuläroptimering och förbättringar av affärsprocesser

### Extrahering av åtgärdbara insikter

**Insikter om prestandaoptimering**

- **Fältnivåoptimering**: Identifiera specifika formulärfält som behöver förbättras eller tas bort
- **Förbättring av användarupplevelsen**: Upptäck problem med användarupplevelsen och implementera riktade förbättringar
- **Optimering av konverteringsgrad**: Använd analysdata för att implementera ändringar som förbättrar antalet slutförda formulär
- **Optimering av tekniska prestanda**: Åtgärda tekniska problem som påverkar inläsning av formulär och prestanda för överföring

**Business Process Insights**

- **Kvalitetsanalys för lead**: Förstå hur beteendet för formulärkomplettering korrelerar med lead-kvalitet och konvertering
- **Marknadsföringsattribuering**: Identifiera vilka marknadsföringskanaler och kampanjer som genererar formulärinskickat material av högsta kvalitet
- **Optimering av kundresor**: Använd formuläranalys för att förbättra fler kundvärvnings- och kundlojalitetsprocesser
- **Resurstilldelning**: Fatta datadrivna beslut om var ni ska investera i formuläroptimeringsresurser

## Felsöka problem med formuläranalys

Även med noggrann implementering kan konfigurationer för formuläranalys stöta på problem som påverkar datainsamling och rapporteringsnoggrannhet. I det här avsnittet finns systematisk felsökningsvägledning för vanliga problem.

### Vanliga installationsproblem

**Datainsamlingsproblem**

- **Formulärdata saknas**: Kontrollera konfigurationen för Adobe Launch och se till att taggarna distribueras korrekt
- **Ofullständig händelsespårning**: Kontrollera regelkonfigurationen och se till att alla formulärhändelser är korrekt mappade
- **Datasvarstid**: Förstå vanliga databehandlingsfördröjningar och identifiera onormala rapporteringsfördröjningar
- **Spårning mellan domäner**: Lös problem med formuläranalys i olika domäner eller underdomäner

>[!TIP]
>
>Ytterligare felsökningsanvisningar finns i våra [felsökningsguider för AEM Forms ](/help/forms/troubleshooting-installation-and-configuration.md) och [felsökning av formulärskapande](/help/forms/form-creation-failing.md).

**Konfigurationsproblem**

- **Rapportsvitsmappning**: Kontrollera att formulär skickar data till rätt Adobe Analytics-rapportsvit
- **Variabelkonfiguration**: Verifiera att anpassade variabler (eVars, props) är korrekt konfigurerade och mappade
- **Regellogikproblem**: Felsök Adobe-startregler som kanske inte aktiveras korrekt
- **Behörighetsproblem**: Lös åtkomstproblem som förhindrar korrekt konfigurering eller datavisning

### Upplösning för dataavvikelser

**Analyser jämfört med formulärsystemsfel**

- **Skillnader i antal inskickade svar**: Åtgärda skillnader mellan antalet inskickade svar från Adobe Analytics och AEM Forms
- **Spårning av användarbeteende**: Åtgärda skillnader i spårning av användarinteraktion mellan system
- **Tidszons- och datumproblem**: Åtgärda rapporteringsavvikelser orsakade av konfigurationsskillnader i tidszon
- **Datainsamling**: Förstå när och hur Adobe Analytics datainsamling påverkar noggrannheten för formuläranalys

**Konsekvens för data på olika plattformar**

- **Spårning av mobiler och stationära datorer**: Säkerställ en konsekvent datainsamling för olika typer av enheter och plattformar
- **Webbläsarkompatibilitet**: Adressspårningsproblem som gäller vissa webbläsare eller webbläsarversioner
- **Tredjepartsintegrering**: Lös problem med datakonsekvens med externa system och integreringar
- **Realtid kontra historiska data**: Förstå och åtgärda skillnader mellan realtidsdata och bearbetade historiska data

### Prestandaoptimering

**Effekt för analysprestanda**

- **Prestanda för sidinläsning**: Minimera analysspårningens påverkan på inläsningstiderna för formulär
- **Effektivitet för datainsamling**: Optimera datainsamlingen för att minska bandbreddsanvändningen och förbättra användarupplevelsen
- **Realtidsbearbetning**: Konfigurera realtidsanalysbearbetning för tidskänsliga formuläranalysbehov
- **Skalbarhetsöverväganden**: Kontrollera att analyskonfigurationen kan hantera formuläranvändning i stora volymer utan prestandaförsämring

**Systemintegreringsprestanda**

- **API-prestanda**: Optimera integreringar mellan AEM Forms och Adobe Analytics för bättre prestanda
- **Effektiv databearbetning**: Förbättra arbetsflödena för databearbetning för att minska fördröjningen och förbättra rapportens tidslängd
- **Resursutnyttjande**: Övervaka och optimera systemresursanvändning för insamling och bearbetning av analysdata
- **Nätverksoptimering**: Konfigurera nätverksinställningar för att optimera dataöverföring mellan system

## Metodtips för formuläranalys

Implementering av blankettanalys kräver att man följer vedertagna standarder för att säkerställa korrekt datainsamling, meningsfulla insikter och hållbara optimeringsprocesser.

>[!TIP]
>
>Innan du implementerar analyser måste du kontrollera att formulären är korrekt konfigurerade med [AEM Forms bästa praxis](/help/forms/introduction-forms-authoring.md) och lämpliga [skicka-åtgärder](/help/forms/configuring-submit-actions.md).

### Genomförande av riktlinjer

**Strategisk planering**

- **Justering av affärsmål**: Se till att implementeringen av formuläranalyser överensstämmer med specifika affärsmål och nyckeltal
- **Intressentengagemang**: Involvera viktiga intressenter i planeringen för att säkerställa att analysen uppfyller organisationens behov
- **Fasad implementering**: Implementera formuläranalys i faser för att hantera komplexitet och säkerställa lyckad distribution
- **Success Metrics Definition**: Definiera tydligt hur framgången ser ut och hur den ska mätas

**Teknisk implementering**

- **Konfigurationsdokumentation**: Behåll omfattande dokumentation om analyskonfigurationen för framtida referens och felsökning
- **Testprotokoll**: Implementera grundliga testprocedurer för att säkerställa korrekt datainsamling före produktionsdistributionen
- **Versionskontroll**: Använd versionskontroll för att analysera konfigurationsändringar och aktivera återställning om problem uppstår
- **Prestandaövervakning**: Kontinuerlig övervakning av analysimplementeringsprestanda och påverkan på formulärfunktioner

### Sekretessöverväganden

**Dataintegritet**

- **GDPR-kompatibilitet**: Kontrollera att implementeringen av formuläranalyser följer EU:s regler för skydd av personuppgifter
- **CCPA-kompatibilitet**: Implementera Kaliforniens sekretesslag för insamling av formulärdata och användarrättigheter
- **Branschspecifika regler**: Adressera hälsovård (HIPAA), ekonomi (PCI DSS) och andra branschspecifika sekretesskrav
- **Hantering av användarsamtycke**: Implementera korrekta mekanismer för insamling och bearbetning av analysdata

**Datasäkerhet**

- **Datakryptering**: Kontrollera att alla formuläranalysdata är krypterade under överföring och i vila
- **Åtkomstkontroller**: Implementera lämpliga åtkomstkontroller för analysdata och rapportering
- **Datalagring**: Upprätta och framtvinga lämpliga datalagringspolicyer för formuläranalysinformation
- **Granskningsspår**: Underhåll granskningsspår för åtkomst av analysdata och konfigurationsändringar

### Optimeringsstrategier

**Kontinuerlig förbättringsprocess**

- **Regelbunden prestandagranskning**: Fastställ regelbundna granskningscykler för att utvärdera formuläranalysens prestanda och identifiera optimeringsmöjligheter
- **Integrering av A/B-tester**: Använd formuläranalysdata för att informera A/B-teststrategier och mäta optimeringseffekten
- **Integrering av användarfeedback**: Kombinera kvantitativa analysdata med kvalitativ användarfeedback för omfattande optimeringsinsikter
- **Korsfunktionell Collaboration**: Främja samarbetet mellan marknadsförings-, UX-, utvecklings- och analysteam för en helhetsoptimering

**Avancerad analysanvändning**

- **Prediktiv analys**: Använd data från tidigare formuläranalyser för att förutsäga användarbeteenden och optimera formulärupplevelser proaktivt
- **Maskinininlärningsintegrering**: Utnyttja maskininlärningsfunktionerna för att identifiera mönster och optimeringsmöjligheter i formuläranalysdata
- **Realtidsoptimering**: Implementera formuläroptimering i realtid baserat på aktuella analysresultat och användarbeteenden
- **Integrering över flera kanaler**: Integrera formuläranalyser med bredare kundreseanalyser för optimering av användarupplevelser

## Vanliga frågor och svar

I det här omfattande avsnittet med vanliga frågor och svar behandlas vanliga frågor om implementering, felsökning och optimering av formuläranalyser för att hjälpa användare på alla erfarenhetsnivåer.

### Komma igång-frågor

**F: Vad är skillnaden mellan formuläranalys och allmän webbplatsanalys?**

S: Formuläranalys fokuserar specifikt på användarinteraktioner i formulär och ger detaljerade insikter om fältbeteende, slutförandemönster och punkter för att överge formulär. Allmän webbplatsanalys spårar sidvisningar och övergripande användarresor, men formuläranalyser ger detaljerade data om formulärspecifika användarupplevelser, valideringsfel, fältslutförandetider och konverteringstrattanalys i själva formulären.

**F: Behöver jag teknisk expertis för att implementera formuläranalyser med Adobe Analytics?**

S: Grundläggande implementering kan utföras med måttlig teknisk kunskap, men avancerade konfigurationer drar nytta av teknisk expertis. Adobe erbjuder automatiserade konfigurationsalternativ genom Experience Cloud Setup Automation för enklare implementeringar. För komplexa företagsdistributioner med anpassade händelser och avancerad rapportering rekommenderas samarbete med utvecklare eller Adobe konsulter.

**F: Hur lång tid tar det att se meningsfulla data från formuläranalyser?**

S: Initiala data visas inom 24-48 timmar efter implementeringen, men meningsfulla insikter kräver vanligtvis 2-4 veckors datainsamling för att identifiera mönster och trender. För att få statistisk betydelse i A/B-tester och optimeringsbeslut kan det ta 4-6 veckors datainsamling, beroende på hur stor mängd data du har i formuläret.

**F: Vilken är den minsta trafikvolym som krävs för effektiv formuläranalys?**

S: Formuläranalys kan ge värden på alla trafiknivåer, men statistisk betydelse för optimeringsbeslut kräver vanligtvis minst 100 formulärinskickade formulär per vecka. För A/B-tester och avancerad analys ger 500+ veckovisa inlämningar mer tillförlitliga insikter. Lägre trafik kan fortfarande dra nytta av kvalitativa insikter om användarbeteendemönster och identifiering av fel.

### Implementerings- och konfigurationsfrågor

**F: Kan jag spåra formulär över flera domäner eller underdomäner?**

S: Ja, Adobe Analytics har stöd för domänövergripande formulärspårning genom korrekt konfigurering av Adobe Analytics spårningskod och Adobe Launch-implementering. Se till att rapportsvitens konfiguration och konfiguration av domänövergripande spårning är konsekvent för att upprätthålla dataintegriteten i olika domäner.

**F: Hur hanterar jag formuläranalyser för flerstegs- eller guideliknande formulär?**

S: Formulär i flera steg kräver specialkonfigurationer för att följa utvecklingen genom varje steg. Implementera anpassade händelser för stegvis komplettering, konfigurera trattanalys för att visualisera bortfallspunkter mellan steg och använd anpassade variabler för att spåra användarsökvägar i formulärguiden. Adobe Analytics tillhandahåller specifik vägledning för formulärspårning på flera sidor.

**F: Vad händer med analysdata om en användare fyller i ett formulär offline eller om JavaScript är inaktiverat?**

S: Adobe Analytics kräver JavaScript för datainsamling, så användare med JavaScript inaktiverat spåras inte. Implementera mekanismer för reservspårning eller analyssamling på serversidan för offlinescenarier. Fundera på effekten på datainsamlingen och implementera alternativa spårningsmetoder för kritiska affärsprocesser.

**F: Hur spårar jag formulärprestanda i olika enheter och webbläsare?**

S: Adobe Analytics samlar automatiskt in enhets- och webbläsarinformation med formuläranalysdata. Konfigurera anpassade rapporter för att analysera formulärprestanda efter enhetstyp, webbläsare, operativsystem och skärmupplösning. Använd dessa data för att identifiera enhetsspecifika optimeringsmöjligheter och säkerställa enhetliga formulärupplevelser på olika plattformar.

### Dataanalys och optimeringsfrågor

**F: Vilken frekvens för formuläravhopp ska jag tänka på som ett problem?**

Svar: Hur många som slutar formulär beror i hög grad på bransch och komplexitet. Enkla kontaktformulär har vanligtvis lägre avhoppsfrekvens, medan komplexa flerstegsblanketter och e-handelscheckningar tenderar att ha högre frekvens. Onormalt höga avhoppsfrekvenser för just din formulärtyp och bransch tyder på optimeringsmöjligheter.

**F: Hur identifierar jag vilka formulärfält som orsakar mest övergivna?**

S: Använd spårning på fältnivå i Adobe Analytics för att analysera antalet slutförda formulär för varje formulärfält. Leta efter betydande bortfall i specifika fält, längre tid än genomsnittet för vissa fält och höga felfrekvenser för vissa fälttyper. Värmemappning och inspelning av användarsessioner kan ge ytterligare kontext för optimering på fältnivå.

**Q: Ska jag optimera för att fylla i formulär snabbt eller noggrant?**

S: Balansen beror på era affärsmål. För leadgenerering kan du optimera för slutförande samtidigt som du behåller ledkvaliteten. För detaljerad datainsamling (enkäter, program) kan du fokusera på förbättringar av användarupplevelsen som minskar friktionen utan att ge avkall på datakvaliteten. Använd A/B-tester för att hitta den optimala balansen för ditt specifika användningsfall.

**F: Hur mäter jag avkastningen på implementeringen av formuläranalys?**

S: Beräkna avkastningen genom att mäta förbättringar i konverteringsgrad, ledkvalitet och driftseffektivitet. Spåra mätvärden som ökad ifyllnad av formulär, minskade supportbiljetter för formulärproblem, förbättrad konverteringsgrad mellan leads och kunder samt minskade kundvärvningskostnader. Kvantifiera dessa förbättringar jämfört med kostnaden för analysimplementering och pågående optimeringsåtgärder.

### Tekniska frågor och felsökningsfrågor

**F: Varför ser jag skillnader mellan antalet inskickade svar från Adobe Analytics och mitt formulärsystem?**

Svar: Vanliga orsaker: JavaScript-fel som förhindrar analysspårning, användare som skickar formulär flera gånger, både trafik som påverkar ett system men inte det andra, skillnader i tidszon vid rapportering och fördröjningar vid databearbetning. Implementera valideringsregler, robotfiltrering och säkerställ enhetliga tidszonsinställningar i alla system.

**F: Hur hanterar jag formuläranalyser för ensidiga program (SPA)?**

S: SPA-program kräver särskild konfiguration för formuläranalys eftersom traditionella sidinläsningshändelser inte inträffar. Implementera anpassad händelsespårning för formulärinteraktioner, använd spårningsfunktionerna i Adobe Analytics SPA, konfigurera virtuella sidvyer för formulärsteg och se till att aktivera dynamiska formulärelement korrekt.

**F: Vad ska jag göra om formuläranalys påverkar sidinläsningsprestanda?**

S: Optimera analysimplementeringen genom att: läsa in analysskript asynkront, implementera lazy loading för icke-kritisk spårning, minska antalet anpassade variabler och händelser, använda effektiva regelkonfigurationer i Adobe Launch och övervaka Core Web Vitals för att säkerställa att analysen inte påverkar användarupplevelsen negativt.

**F: Hur ser jag till att formuläranalyser följer sekretesslagstiftningen?**

S: Implementera integritetsefterlevnad genom att: få användarens samtycke för spårning av analyser, anonyma eller pseudonymisera personuppgifter, genomföra policyer för datalagring, tillhandahålla avanmälningsmekanismer, säkerställa GDPR/CCPA-överensstämmelse vid insamling och behandling av uppgifter samt samarbeta med jurister för att säkerställa regelefterlevnad.

### Frågor om avancerad implementering

**F: Kan jag integrera formuläranalyser med andra Adobe Experience Cloud-lösningar?**

S: Ja, Adobe Analytics kan integreras smidigt med andra Experience Cloud-lösningar. Koppla upp dig med Adobe Target för A/B-testning och -personalisering av formulär, integrera med Adobe Campaign för lead-moderering baserat på formulärbeteende, använd Adobe Audience Manager för avancerad segmentering och utnyttja Adobe Experience Platform för omfattande kundreseanalys.

**F: Hur ställer jag in prediktiv analys för formuläravslut?**

S: Implementera prediktiv analys genom att: samla in omfattande användarbeteendedata, använda Adobe Analytics maskininlärningsfunktioner, implementera poängmodeller i realtid, konfigurera automatiska ingrepp för scenarier med hög risk och kontinuerligt förfina modeller baserat på prestandadata.

**F: Vilket är det bästa sättet att spåra formuläranalyser i en mobilapp?**

S: Analys av mobilappsformulär kräver implementering av Adobe Analytics Mobile SDK. Konfigurera mobilspecifika händelser och variabler, implementera datainsamling och -synkronisering offline, spåra mobilspecifika interaktioner (pekhändelser, enhetsorientering) och säkerställa korrekt attribuering mellan appsessioner och webbinteraktioner.

**F: Hur skapar jag anpassade instrumentpaneler för olika intressenter?**

S: Skapa rollspecifika kontrollpaneler genom att identifiera nyckelvärden för varje intressentgrupp (chefer, marknadsförare, utvecklare), använda Adobe Analytics Workspace för att skapa anpassade visualiseringar, implementera automatiserade rapporteringsscheman, skapa detaljerade analysfunktioner och tillhandahålla utbildning i kontrollpanelens tolkning och användning.

### Felsöka snabbkorrigeringar

**Vanliga problem och lösningar:**

| Problem | Snabbkorrigering | Detaljerad lösning |
|-------|-----------|-------------------|
| Inga data visas | Kontrollera Adobe Launch-distribution | Verifiera taggimplementering och regelkonfiguration |
| Felaktiga antal inskickade data | Validera händelsestart | Granska regellogik och mappning av dataelement |
| Data saknas på fältnivå | Konfigurera fältspårning | Ställ in anpassade variabler för fältinteraktioner |
| Domänöverskridande problem | Konfiguration för uppdateringsspårning | Implementera korrekt konfiguration för domänövergripande spårning |
| Problem med spårning av mobiler | Kontrollera mobilimplementering | Verifiera responsiv design och mobilspecifika händelser |
| Prestandapåverkan | Optimera inläsningsstrategi | Implementera asynkron inläsning och effektiva regler |

>[!MORELIKETHIS]
>
>*[Aktivera Adobe Analytics för ett anpassat formulär](/help/forms/enable-adobe-analytics-adaptive-form-using-experience-cloud-setup-automation.md)

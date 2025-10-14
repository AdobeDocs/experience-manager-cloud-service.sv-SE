---
title: AEM Forms as a Cloud Service - introduktion
description: Upptäck AEM Forms funktioner för att skapa anpassningsbara formulär, automatisera arbetsflöden och hantera digitala dokument. Komplett plattform för blankettstyrda affärsprocesser.
landing-page-description: Lär dig hur du använder AEM Forms as a Cloud Service för att skapa anpassningsbara formulär, bearbeta dokument och automatisera arbetsflöden.
keywords: AEM Forms, adaptiva formulär, formulärbyggare, digitala formulär, automatiserade arbetsflöden, dokumenttjänster, formulärdatamodell
role: Admin, Developer, User
feature: Adaptive Forms, Release Information
hide: true
hidefromtoc: true
index: false
exl-id: 50d7ce19-7d76-4ea1-a54c-8ca0e5379982
source-git-commit: eca09e1bf2ba4466f54e915e01218cc89cf5b116
workflow-type: tm+mt
source-wordcount: '2323'
ht-degree: 0%

---

# AEM Forms as a Cloud Service - introduktion {#introduction}



Adobe Experience Manager Forms as a Cloud Service är en heltäckande plattform för att skapa, hantera och optimera digitala formulärupplevelser. Organisationer använder AEM Forms för att digitalisera pappersbaserade processer, skapa responsiva webbformulär, automatisera dokumentflöden och leverera personaliserad kommunikation i stor skala.

Plattformen kombinerar formulärredigeringsfunktionerna med robusta backend-tjänster, som gör att du kan bygga allt från enkla kontaktformulär till komplexa affärsprogram i flera steg. Med molnbaserad arkitektur får du automatiska uppdateringar, elastisk skalning och säkerhet på enterprise-nivå utan att behöva hantera infrastruktur.

Den här guiden presenterar de viktigaste funktionerna som är organiserade i hela formulärlivscykeln, från den första designen till den pågående optimeringen.

## Nyheter i AEM Forms {#whats-new}

**Högdagrar för den senaste versionen:**

- **Indatakomponent för datum och tid** - Förbättrade användarindata med kalender- och klockgränssnitt för exakt val av datum och tid
- **Förbättrat filöverföringsskydd** - Automatisk validering och kontroll av innehållstyp för att förhindra filformat som inte stöds
- **Förbättrad felhantering** - Bättre felsökning med specifika felkoder för anpassade skicka-åtgärder
- **Postförbättrat dokument** - Alternativ för att exkludera dolda fält för tydligare dokumentgenerering

**Pre-Release-funktioner:**

- **Stöd för AFP-format** - Utskriftsfunktioner i företagsklass med kommunikations-API:er
- **Förbättringar i regelredigeraren** - Stöd för modern JavaScript, dynamiska variabler och sammanhangsberoende panelregler
- **Förbättrade valideringsmetoder** - Panel-, fält- och formulärnivåvalidering med förbättrad flexibilitet

[Visa fullständig versionsinformation →](/help/release-notes/release-notes-cloud/release-notes-current.md#forms)

## Tidig åtkomst {#early-access}

Få exklusiv tillgång till de senaste innovationerna från AEM Forms innan de blir allmänt tillgängliga.

**Aktuella funktioner för tidig åtkomst:**

- **AEM Forms AI Assistant** - Generativ AI för automatisk formulärgenerering, generering av paneler och optimeringsrekommendationer
- **Skriptsignaturkomponent** - Direktsignering i formulär med mus, penna eller pekskärm
- **Direkt API-integrering** - Ansluta till API:er i regelredigeraren utan att behöva konfigurera formulärdatamodellen
- **Forms-optimering** - prestandaanalys med AI-baserad teknik och förslag på förbättringar av konverteringsgrad

**Gå med i programmet:**
Bli en av de första som får tillgång till innovationer och hjälper till att forma framtiden för AEM Forms.

[Begär åtkomst →](mailto:aem-forms-ea@adobe.com) | [Läs mer → &#x200B;](/help/forms/early-access-ea-features.md)


## Kärnfunktioner {#core-capabilities}

AEM Forms klarar hela den digitala formulärresan, från det att de skapas till att de optimeras kontinuerligt. Varje fas bygger vidare på det föregående och skapar en heltäckande plattform för blankettbaserade affärsprocesser.

**AEM Forms Workflow Journey:**

    CREATE → GOVERN → PUBLISH → CAPTURE → PROCESS → INTEGRATE → TRACK → ARCHIVE → IMPROVE
     ↓        ↓        ↓         ↓         ↓         ↓          ↓       ↓        ↓
    Design   Granska   Distribuera   Samla   Handtag   Anslut   Bildskärmsbutik   Optimera 
     ↑                                                                              ↓
     När du bearbetar kommer du att automatiskt kommer automatiskt att lagras, automatiskt kommer att automatiskt automatiskt fortsätta att förbättras genom att alla kommer att lagras, kommer att lagras, kommer att lagras kommer att lagras kommer att lagras kommer att lagras automatiskt kommer kommer att automatiskt kommer kommer kommer att lagras kommer kommer att lagras kommer att lagras, kommer att lagras, kommer att lagras 

### Skapa: Formulärdesign och -utveckling {#create}

Bygg adaptiva blanketter med hjälp av olika metoder som skräddarsytts för olika behov och tekniska krav.

**Visual Form Builder**
Designa responsiva formulär genom dra-och-släpp-gränssnitt med [Core Components](/help/forms/creating-adaptive-form-core-components.md), [Foundation Components](/help/forms/creating-adaptive-form.md) eller [Edge Delivery Services](/help/edge/docs/forms/overview.md) . Den visuella redigeraren ger omedelbar feedback samtidigt som man bevarar ren, semantisk markering som fungerar på olika enheter och hjälpmedelstekniker.

**Dokumentbaserad redigering**
Skapa formulär med välbekanta verktyg som Microsoft Excel via [Edge Delivery Services](/help/edge/docs/forms/overview.md) . Med den här metoden kan skribenter skapa högpresterande formulär utan tekniska kunskaper, samtidigt som man får enastående Google Lighthuse-poäng.

**Mallar och teman**
Snabba upp formulärframtagningen med färdiga [&#x200B; mallar &#x200B;](/help/forms/template-editor-core-components.md) som definierar struktur och ursprungligt innehåll. Använd enhetlig profilering med [teman](/help/forms/using-themes-in-core-components.md) som styr den visuella formateringen i flera formulär, vilket ger enhetlig design och minskar utvecklingstiden.

**Dataintegreringar**
Koppla ihop blanketterna med datasystemen under konstruktionsfasen. [Formulärdatamodellen](/help/forms/create-form-data-models.md) har ett enhetligt gränssnitt för flera datakällor, vilket möjliggör [förifyllning](/help/forms/prepopulate-adaptive-form-fields.md), [valideringsregler](/help/forms/rule-editor-core-components.md) och smidigt dataflöde mellan formulär och affärssystem.

**Valideringar och villkorsstyrd logik**
Implementera [villkorsstyrd logik](/help/forms/rule-editor-core-components.md), progressiv visning och adaptiv validering som vägleder användarna genom komplexa processer. [Funktionen Spara och återuppta](/help/forms/save-core-component-based-form-as-draft.md) gör att användare kan fylla i formulär i flera sessioner.

**HTML5 Forms**
Återge XFA-baserade formulär som [&#x200B; HTML5-formulär &#x200B;](/help/forms/introductionhtml5.md) för mobila enheter och äldre webbläsare. HTML5 Forms ger en inbyggd mobilupplevelse utan plugin-program samtidigt som man bevarar blankettlogiken och valideringen från de ursprungliga XDP-mallarna.

**Interaktiv kommunikation**
Skapa dokumentcentrerad kommunikation som kontoutdrag, fakturor och meddelanden med en visuell redigerare. [Interaktiv kommunikation](/help/forms/interactive-communication/create-interactive-communication.md) kombinerar statiskt innehåll med dynamiska data för att generera personaliserad kommunikation i både tryck och digitala kanaler.

### Styrning: Granskning och efterlevnad {#govern}

Inrätta tillsyns- och godkännandeprocesser för att säkerställa att blanketterna uppfyller organisatoriska standarder och lagstadgade krav.

**Arbetsflödesbaserade godkännanden**
Vidarebefordra formulärdesigner genom granskningsprocesser i flera steg med rollbaserade uppdrag. Intressenter kan [granska](/help/forms/create-reviews-forms.md), [kommentera](/help/forms/add-comments-annotations-versioning-adaptive-form-core-components.md) och godkänna formulär innan de publiceras, vilket ger bibehållen kvalitetskontroll och efterlevnadstillsyn med [AEM-arbetsflöden](/help/forms/aem-forms-workflow.md).

**Versionshantering**
Spåra formulärversionerna och ha spårbarhet för att följa gällande regelverk. Inbyggd [versionshantering](/help/forms/add-comments-annotations-versioning-adaptive-form-core-components.md) gör att du kan återställa ändringar, jämföra upprepningar och upprätthålla historiska poster för efterlevnadsgranskningar.

**Åtkomstkontroll och behörigheter**
Definiera detaljerade behörigheter för att skapa, redigera och publicera formulär. [Rollbaserad åtkomst](/help/forms/forms-groups-privileges-tasks.md) säkerställer att bara behöriga användare kan ändra formulär, samtidigt som åtskilda arbetsuppgifter upprätthålls för känsliga affärsprocesser.

### Publicera: Multi-Channel Distribution {#publish}

Distribuera formulär via flera kanaler och kontaktytor för att nå användarna var de än är.

**Flerkanalspublicering**
Publicera formulär till [&#x200B; AEM Sites &#x200B;](/help/forms/embed-adaptive-form-aem-sites.md) , fristående webbsidor, mobilprogram eller [inbäddning i tredjepartssystem](/help/forms/embed-adaptive-form-core-components-external-web-page.md) . Med single-source-publicering får du en konsekvent upplevelse och kan samtidigt anpassa dig till olika kanalkrav.

**Lokalisering och Personalization**
Leverera formulär på flera språk med [AEM arbetsflöden för översättning](/help/forms/using-aem-translation-workflow-to-localize-adaptive-forms-core-components.md), med stöd för både [vänster-till-höger- och höger-till-vänster-språk](/help/forms/right-left-languages.md). Integrera med Adobe Target för att personalisera formulärupplevelser baserat på användarsegment, beteende eller sammanhangsbaserade data.

**Prestandaoptimering**
Utnyttja Edge Delivery Services för blixtsnabb blankettinläsning och optimala SEO-prestanda. Nätverk för innehållsleverans säkerställer global tillgänglighet med minimal fördröjning.

**Forms Portal**
Skapa centraliserade blankettarkiv där användarna kan hitta, öppna och hantera blanketter. [Forms Portal](/help/forms/configure-forms-portal.md) har sökfunktioner, kategorisering av formulär, hantering av utkast och spårning av överföringar i ett enhetligt gränssnitt för en förbättrad användarupplevelse.

### Hämtning: Användarupplevelse och datainsamling {#capture}

Optimera blankettifyllnaden och maximera datakvaliteten.

**Responsiv design**
Forms anpassar sig automatiskt till olika skärmstorlekar och inmatningsmetoder. Touchoptimerade kontroller, tangentbordsnavigering och skärmläsarkompatibilitet säkerställer [tillgänglighet](/help/forms/creating-accessible-adaptive-forms.md) för alla användartyper.

**Digitala signaturer**
Integrera [&#x200B; Adobe Sign &#x200B;](/help/forms/working-with-adobe-sign.md) för juridiskt bindande e-signaturer i formulärupplevelsen. Användarna kan signera dokument utan att lämna formuläret, vilket effektiviserar godkännandeprocesserna och minskar avhoppsningen.

**Skicka åtgärder**
Konfigurera [skicka-åtgärder](/help/forms/configure-submit-actions-core-components.md) för att definiera vad som händer när användare fyller i och skickar formulär. Skicka data via e-post, databaser, arbetsflöden eller externa system samtidigt som användarna får feedback och bekräftelse direkt.

### Process: Inlämningshantering och routning {#process}

Hantera inskickade formulär med effektiva funktioner för bearbetning, validering och vidarebefordran.

**Dataverifiering och -bearbetning**
Säkerställ dataintegriteten genom validering på serversidan och automatiska bearbetningsregler. Omvandla, validera och skicka inskickade data samtidigt som du genererar kvitton, bekräftelser eller uppföljningsmaterial för användarna.

**Kommunikations-API:er**
Generera, ändra och skydda dokument programmatiskt via [RESTful API:er](/help/forms/aem-forms-cloud-service-communications-introduction.md) . Skapa PDF:er, utskriftsklara format, sammanställ dokument, använd digitala signaturer och bearbeta stora [gruppåtgärder](/help/forms/aem-forms-cloud-service-communications-batch-processing.md) för dokumentarbetsflöden i storföretagsklass.

**Postdokument**
Generera automatiskt PDF-register över inskickade blanketter för att säkerställa att de är korrekta och har bekräftats av användaren. [Dokument för arkivering](/help/forms/generate-document-of-record-core-components.md) skapar formaterade, utskrivbara versioner av ifyllda formulär med inskickade data, med officiell dokumentation för transaktioner och lagstadgade krav.

**Arbetsflödessamordning**
Utöka komplexa affärsprocesser baserat på inskickade formulär. slussa data genom godkännandekedjor, tilldela uppgifter till specifika användare och automatisera rutinmoment med bibehållen åtkomsthistorik.

**Felhantering och återställning**
Inbyggda mekanismer för återförsök och reservbearbetning säkerställer att inga inskickade data går förlorade. Omfattande loggning hjälper till att felsöka problem och upprätthålla serviceavtal.

### Integrera: Serverdelsanslutning {#integrate}

Koppla blanketterna till befintliga affärssystem och datakällor för smidigt informationsflöde.

**Fördefinierade anslutningar**
Inbyggd integrering med lösningarna [&#x200B; Salesforce](/help/forms/configure-salesforce.md), [&#x200B; Microsoft Dynamics](/help/forms/configure-msdynamics.md), [&#x200B; SharePoint](/help/forms/connect-forms-to-sharepoint-document-library.md) och Adobe Experience Cloud. Fördefinierade anslutningar minskar utvecklingstiden samtidigt som ni säkerställer tillförlitlig datasynkronisering.

**RESTful API-integrering**
Anslut till valfri webbtillgänglig tjänst via RESTful API:er via [Skicka-åtgärder](/help/forms/configure-submit-action-restpoint.md) eller [dataintegrering](/help/forms/data-integration.md). Formulärdatamodellen förenklar integreringen och ger ett konsekvent gränssnitt oavsett den underliggande systemarkitekturen.

**Datautbyte i realtid**
Möjliggör dubbelriktat dataflöde mellan formulär och affärssystem. Fyll i formulär i förväg från befintliga poster, validera mot livedata och uppdatera flera system samtidigt när de skickas in via omfattande [dataintegrering](/help/forms/data-integration.md).

### Spåra: Analys och prestandaövervakning {#track}

Förstå formulärprestanda och användarbeteende med omfattande analyser och övervakning.

**Formuläranalys**
Spåra antalet slutförda åtgärder, antalet övergivna mönster och interaktioner på fältnivå genom [Adobe Analytics-integrering](/help/forms/integrate-aem-forms-with-adobe-analytics.md). Identifiera friktionspunkter, mät konverteringsfunktioner och förstå användarbeteenden i olika segment.

**Prestandaövervakning**
Övervaka inläsningstider för formulär, hur snabb överföringen är och systemets prestanda. Realtidskonsoler ger insikter i mätvärden för teknisk hälsa och användarupplevelse.

**Business Intelligence**
Generera rapporter om formuläranvändning, inskickningsvolymer och processeffektivitet. Analyserna bygger på kapacitetsplanering, optimering av användarupplevelser och förbättringar av affärsprocesser.

**Transaktionsrapporter**
Övervaka API-användning, dokumentgenereringsvolymer och [fakturerbara transaktioner](/help/forms/transaction-reports-billable-apis.md) i AEM Forms-distributionen. Spåra konsumtionsmönster, optimera resursallokeringen och följ licenskraven.

### Arkiv: Dokumenthantering och regelefterlevnad {#archive}

Lagra och hantera på ett säkert sätt inskickade blanketter och genererade dokument för långsiktig arkivering och regelefterlevnad.

**Dokumentlagring**
Lagra genererade dokument och inskickade formulär i AEM Digital Asset Management-system eller integrera med externa dokumentarkiv som [SharePoint](/help/forms/configure-submit-action-sharepoint.md), [OneDrive](/help/forms/configure-submit-action-onedrive.md) eller [Azure Blob Storage](/help/forms/configure-submit-action-azure-blob-storage.md).

**Efterlevnad och bevarande**
Implementera datalagringspolicyer som uppfyller lagstadgade krav som GDPR, CCPA och HIPAA. [Automatiska arkiveringsprocesser](/help/forms/aem-forms-cloud-service-communications-batch-processing.md) säkerställer att dokumenten sparas under de perioder som krävs och att de säkert tas bort när det är lämpligt.

**Säkerhets- och åtkomstkontroll**
Använd kryptering, digitala signaturer och [rollbaserade åtkomstkontroller](/help/forms/forms-groups-privileges-tasks.md) för arkiverade dokument. Granskningshistorik spårar dokumentåtkomst och ändringar för efterlevnadsrapportering och säkerhetstillsyn.

### Förbättra: Optimering och förbättring {#improve}

Optimera kontinuerligt formulärprestanda och användarupplevelser med datadrivna insikter och tester.

**Integrering av A/B-testning**
Använd Adobe Target för att testa olika formulärlayouter, fältupplägg och användarflöden. Statistisk analys hjälper till att identifiera de mest effektiva metoderna för olika användarsegment och användningsfall.

**Analysdriven optimering**
Analysera användarbeteendedata för att identifiera förbättringsmöjligheter. [Visa och förstå analysrapporter](/help/forms/view-understand-aem-forms-analytics-reports.md) för värmemappning, fältinteraktionsanalys och mönsterigenkänning av övergivna mönster för att informera om repetitiva designförbättringar.

**Interaktiv förbättring**
Implementera kontinuerliga förbättringsprocesser baserade på användarfeedback, prestandamätningar och affärskrav. [Versionskontroll](/help/forms/add-comments-annotations-versioning-adaptive-form-core-components.md) och återställningsfunktioner möjliggör säkra experiment och snabb upprepning.

## Komma igång {#getting-started}

Vilken strategi ni väljer beror på era omedelbara behov och långsiktiga mål.

### Snabbstart: Enkel Forms {#quick-start}

Välj det redigeringssätt du föredrar baserat på din tekniska bakgrund och dina prestandakrav:

**Skapa visuellt formulär:**

1. **[Skapa adaptiva formulär med kärnkomponenter](/help/forms/creating-adaptive-form-core-components.md)** för moderna, responsiva formulär
2. **[Konfigurera skicka-åtgärder](/help/forms/configure-submit-actions-core-components.md)** för att hantera formulärdata
3. **[Bädda in formulär i AEM Sites](/help/forms/embed-adaptive-form-aem-sites.md)** eller dela via direktlänkar

**Dokumentbaserad redigering:**

1. **[Skapa formulär med Excel](/help/edge/docs/forms/create-forms.md)** med Edge Delivery Services för högpresterande formulär
2. **[Publicera till Edge Delivery](/help/edge/docs/forms/publish-forms.md)** för optimal inläsningshastighet och SEO

**Stöd för äldre formulär:**

- **[HTML5 Forms](/help/forms/introductionhtml5.md)** för mobiloptimerad XFA-formuläråtergivning

### Avancerad implementering: Affärsprocesser {#advanced-implementation}

För komplexa krav som omfattar flera system, dokumentgenerering och arbetsflöden för godkännande:

**Dataintegrering och arbetsflöden:**

1. **[Konfigurera formulärdatamodeller](/help/forms/create-form-data-models.md)** för att ansluta serverdelssystem
2. **[Utforma arbetsflödesprocesser](/help/forms/aem-forms-workflow.md)** för godkännande och routning
3. **[Konfigurera analyser](/help/forms/integrate-aem-forms-with-adobe-analytics.md)** för att mäta prestanda

**Dokumenttjänster och kommunikation:**

1. **[Implementera kommunikations-API:er](/help/forms/aem-forms-cloud-service-communications-introduction.md)** för automatisk dokumentgenerering
2. **[Skapa interaktiv kommunikation](/help/forms/interactive-communication/create-interactive-communication.md)** för anpassade meddelanden och meddelanden
3. **[Konfigurera Forms Portal](/help/forms/configure-forms-portal.md)** för centraliserad formulärhantering

### Företagsdistribution: Skala och styrning {#enterprise-deployment}

För driftsättningar i hela organisationen som kräver styrning, efterlevnad och övervakning:

**Arkitektur och styrning:**

1. **[Granska arkitekturmönster](/help/forms/aem-forms-cloud-service-architecture.md)** för skalbar distribution
2. **[Konfigurera användarhantering](/help/forms/forms-groups-privileges-tasks.md)** och åtkomstkontroller
3. **[Konfigurera utvecklingsarbetsflöden](/help/forms/setup-local-development-environment.md)** för teamsamarbete

**Migrering och övervakning:**

1. **[Planera migreringsstrategier](/help/forms/migrate-to-forms-as-a-cloud-service.md)** från befintliga system
2. **[Implementera transaktionsövervakning](/help/forms/transaction-reports-billable-apis.md)** för användningsspårning och efterlevnad

<details>
<summary><strong> ❓ Vanliga frågor </strong></summary>

**Vad är en formulärbyggare?**
Ett formulärverktyg är ett verktyg som gör att du kan skapa digitala formulär utan att behöva skriva kod. Du kan utforma formulär med dra-och-släpp-gränssnitt, lägga till fält som textrutor och listrutor och publicera dem online för att samla in data från användarna.

**Hur skapar jag ett onlineformulär?**
Med AEM Forms kan du skapa adaptiva formulär med hjälp av Core Components via en visuell dra-och-släpp-redigerare, bygga högpresterande formulär med Edge Delivery Services eller använda Foundation Components för etablerade arbetsflöden. Börja med att välja en mall, lägga till formulärfält, konfigurera dataanslutningar och publicera över flera kanaler.

**Vad är ett bra onlineformulär?**
Bra onlineformulär är mobilresponsiva, läses in snabbt, har tydliga etiketter, använder logisk fältordning, innehåller validering för att förhindra fel och ger omedelbar feedback till användarna när de skickas in.

**Kan jag integrera formulär med andra affärssystem?**
Ja, moderna formulärbyggare har omfattande integreringsfunktioner. Ni kan koppla formulär till CRM-system, e-postmarknadsföringsplattformar, databaser, molnlagring och verktyg för automatisering av arbetsflöden för att effektivisera era affärsprocesser.

**Är onlineformulär säkra?**
Professionella blankettbyggare har säkerhetsfunktioner i företagsklass, som datakryptering, säker dataöverföring, åtkomstkontroll och efterlevnad av regler som GDPR, HIPAA och CCPA för att skydda känslig information.

**Hur lägger jag till e-signaturer i mina formulär?**
Digitala signaturer kan integreras direkt i formulär med Adobe Sign eller andra e-signaturleverantörer. Detta gör att användarna kan signera dokument i formulärupplevelsen, vilket eliminerar behovet av separata signeringsarbetsflöden och minskar behovet av att överge formulär.

**Kan formulär generera PDF-dokument automatiskt?**
Ja, moderna blankettplattformar kan automatiskt generera PDF kvitton, bekräftelser eller urkunder när blanketterna skickas. Detta är nödvändigt för att uppfylla kraven, registrera och ge användarna omedelbar bekräftelse.

**Hur spårar jag formulärprestanda och -analys?**
Med hjälp av formuläranalyser kan ni förstå antalet slutförda formulär, antalet övergivna formulär och användarbeteenden. Integrering med analysplattformar som Adobe Analytics ger insikter om vilka fält som orsakar friktion och hur konverteringsgraden kan optimeras.

**Vad är automatisering av formulärarbetsflöden?**
Automatisering av formulärarbetsflöden skickar in material via godkännandeprocesser, tilldelar uppgifter till teammedlemmar och utlöser åtgärder i andra affärssystem. Detta eliminerar manuell behandling och säkerställer en konsekvent hantering av formulärdata.

**Hur gör jag formulär tillgängliga för användare med funktionshinder?**
[&#x200B; Hjälpmedelsförberedda formulär &#x200B;](/help/forms/creating-accessible-adaptive-forms.md) innehåller korrekt etikettering, tangentbordsnavigering, skärmläsarkompatibilitet och kompatibilitet med WCAG-riktlinjer. Detta garanterar att alla användare kan fylla i formulär oavsett vilken kapacitet eller hjälpmedelsteknik de har.

**Vad kostar formulärbyggare?**
Priserna för AEM Forms as a Cloud Service beror på era specifika behov, användningsvolym och behov av nya funktioner. Om du vill ha detaljerad prisinformation och diskutera en skräddarsydd lösning kontaktar du Adobe eller Adobe.

</details>

## Nästa steg {#next-steps}

Utforska de funktioner som matchar dina aktuella prioriteringar:

- **[Bygg ditt första formulär](/help/forms/creating-adaptive-form-core-components.md)** och upplev redigeringsmiljön
- **[Granska arkitekturalternativ](/help/forms/aem-forms-cloud-service-architecture.md)** för distributionsplanering
- **[Konfigurera utvecklingsmiljön](/help/forms/setup-local-development-environment.md)** för teamsamarbete
- **[Utforska integreringsalternativen](/help/forms/data-integration.md)** för att ansluta befintliga system

Om du vill ha omfattande implementeringsvägledning kan du överväga att använda Adobe Professional Services för att snabba upp driftsättningen och säkerställa bästa praxis från början.

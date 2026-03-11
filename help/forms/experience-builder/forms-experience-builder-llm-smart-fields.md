---
title: Smarta fält som förbättrats med LLM i Forms Experience Builder
description: Lär dig skapa intelligenta formulärfält med förifyllda alternativ med AI-kunskapsbas för geografiska data, affärsklassificeringar och branschstandarder.
hide: true
index: false
hidefromtoc: true
role: Admin, Developer
badgeSaas: label="AEM Forms" type="Positive" tooltip="Gäller AEM Forms)."
exl-id: a03b247c-1e50-4dee-9182-bc81fb83a48b
source-git-commit: 89b0f2a8ca9d2f60365a5c3962b0b4e826f79b3e
workflow-type: tm+mt
source-wordcount: '1480'
ht-degree: 0%

---

# Smarta fält som förbättrats med LLM i Forms Experience Builder {#llm-enhanced-smart-fields}

Forms Experience Builder utnyttjar kraften i de stora språkmodellerna för att skapa intelligenta formulärfält med förifyllda alternativ som bygger på omfattande kunskapsbanker. Detta eliminerar behovet av att manuellt söka efter och mata in stora datamängder, vilket dramatiskt förbättrar effektiviteten och exaktheten vid blankettframtagning.

## Vad är LLM-förbättrade smarta fält? {#what-are-llm-smart-fields}

Smarta fält som förbättrats med LLM är formulärfält som automatiskt fylls i med omfattande och korrekta data med hjälp av AI:s inbyggda kunskapsbas. I stället för att manuellt skapa listrutor eller alternativuppsättningar kan du begära fält som kräver omfattande datauppsättningar och AI genererar automatiskt lämpliga alternativ.

**Viktiga fördelar:**

* **Omfattande datauppsättningar** - tillgång till omfattande, aktuell information i flera domäner
* **Automatisk ifyllning** - Du behöver inte manuellt söka efter och mata in data
* **Standardiserade format** - Använder branschstandardkoder, klassificeringar och namnkonventioner
* **Kontextmedvetna alternativ** - Fält kan anpassas baserat på andra formulärval
* **Tidsbesparande** - Minskar tiden det tar att skapa formulär från timmar till minuter

## När ska vi använda smarta fält som förbättrats med LLM {#when-to-use-smart-fields}

Använd smarta fält som förbättrats med LLM när du behöver:

* **Omfattande datauppsättningar** - Fält som kräver omfattande, standardiserad information
* **Branschstandarder** - klassificeringar, koder eller lagstadgade data
* **Geografisk information** - Platser, regioner eller administrativa avdelningar
* **Professionella data** - Jobbtitlar, certifieringar eller branschklassificeringar
* **Tekniska standarder** - Filformat, protokoll eller systemspecifikationer

## Geografiska fält och platsfält {#geographic-location-fields}

Skapa platsbaserade fält med omfattande geografiska data och administrativ information.

### Flygplatser och transport

**Internationella flygplatser med IATA-koder:**

    Lägg till en listruta för avgångsflygplatser med alla större internationella flygplatser
    Lägg till fält för ankomstflygplatser med IATA-koder och fullständiga namn
    Skapa ett fält för närmaste flygplats till användarplats
    Lägg till ett urval av tågstationer för europeiska städer

**Exempeluppmaningar:**

* &quot;Lägg till ett flygplatsfält för avgång med alla större flygplatser i världen, inklusive IATA-koder och stadsnamn&quot;
* &quot;Skapa en ankomstmeny för flygplatser med internationella flygplatser organiserade på kontinenten&quot;
* &quot;Inkludera ett urval av tågstationer för större europeiska städer med stationskoder&quot;

### Administrativa regioner

**Länder, delstater och provinser:**

    Lägg till en fullständig lista med delstater i USA med förkortningar
    Skapa en listruta med ISO-koder och fullständiga namn
    Lägg till ett fält för viktiga världsstäder med tidszoner
    Ta med en listruta med kanadensiska provinser och områden
    Lägg till ett fält för grevskap och postområden i Storbritannien

**Exempeluppmaningar:**

* &quot;Skapa ett urvalsfält med ISO-landskoder och fullständiga namn&quot;
* &quot;Lägg till en listruta med delstat i USA med förkortningar och fullständiga namn&quot;
* &quot;Inkludera ett kanadensiskt regionfält med territorier och postnummer&quot;
* &quot;Skapa ett storstadsområde med storstadsområden och tidszoner&quot;

## Affärs- och branschdata {#business-industry-data}

Använd omfattande affärsklassificeringar och professionella data för företagsblanketter.

### Företagsklassificeringar

**Bransch- och affärsenhetstyper:**

    Lägg till ett fält för branschklassificering med NAICS-koder
    Skapa en listruta med affärsenhetstyper (LLC, Corporation, Partnership, etc.)
    Lägg till ett fält för företagsstorlekskategorier (start, SME, enterprise)
    Inkludera avdelningsval för stora organisationer
    Lägg till ett fält för professionella tjänstetyper

**Exempeluppmaningar:**

* &quot;Skapa ett omfattande branschområde med hjälp av NAICS-standardklassificering med tekniska underkategorier&quot;
* &quot;Lägg till en listruta av företagstyp med juridiska strukturer och beskrivningar&quot;
* &quot;Inkludera ett företagsstorleksfält med intervall för antal anställda och intäktsintervall&quot;

### Professionella klassificeringar

**Jobbtitlar och certifieringar:**

    Lägg till ett fält för jobbtitlar med vanliga branschroller
    Skapa en listruta med professionella certifieringar per fält
    Inkludera utbildningsnivåer med gradtyper
    Lägg till ett fält för årens upplevelseintervall
    Skapa ett urval för programmeringsspråk och ramverk

**Exempeluppmaningar:**

* &quot;Inkludera en listruta för professionell certifiering som anpassar sig efter det valda jobbfältet&quot;
* &quot;Skapa ett yrkestitelfält med gemensamma roller inom teknik, hälso- och sjukvård och ekonomi&quot;
* &quot;Lägg till ett utbildningsnivåfält med olika typer och specialiseringar&quot;

## Standarder och lagstadgade data {#standards-regulatory-data}

Få tillgång till standardiserade koder, klassificeringar och regelinformation för formulär som fokuserar på regelefterlevnad.

### Finans och juridik

**Valuta, moms och betalningsinformation:**

    Lägg till ett fält för valutakoder med symboler och valutakurser
    Skapa en listruta med skatte-ID-typer per land
    Ta med ett fält för giltiga dokumenttyper
    Lägg till betalningsmetodalternativ med säkerhetsfunktioner
    Skapa ett val för bankinstitutioner per land

**Exempeluppmaningar:**

* &quot;Skapa ett valutamarkeringsfält med ISO-koder, symboler och stora valutakurser&quot;
* &quot;Lägg till ett skatteID-typfält med landsspecifika format för skatteidentifiering&quot;
* &quot;Inkludera en betalningsmetod med säkerhetsfunktioner och bearbetningstider&quot;

### Tekniska standarder

**Filformat och protokoll:**

    Lägg till en listruta med filformattyper med tillägg
    Inkludera nätverksprotokollalternativ
    Lägg till ett fält för databastyper och versioner
    Skapa ett val för API-autentiseringsmetoder

**Exempeluppmaningar:**

* &quot;Skapa en listruta för filformat med vanliga tillägg och MIME-typer&quot;
* &quot;Lägg till ett databasurvalsfält med versioner och funktionsjämförelser&quot;
* &quot;Inkludera ett API-autentiseringsmetodfält med säkerhetsnivåer&quot;

## Hälso- och sjukvård {#healthcare-medical-fields}

Specialiserade data om medicin och hälsovård för branschspecifika formulär.

### Medicinska klassificeringar

**Specifikationer och medicinska data:**

    Lägg till ett fält för medicinska specialiteter
    Skapa en listruta med vanliga läkemedel med generiska namn
    Inkludera ett fält för försäkringsleverantörstyper
    Lägg till ett val för medicinska kontaktrelationer i nödsituationer
    Skapa ett fält för kostrestriktioner och allergier

**Exempeluppmaningar:**

* &quot;Skapa ett specialområde för medicin med subspecialiteter och styrelsemeddelanden&quot;
* &quot;Lägg till ett medicineringsfält med generiska namn, märkesnamn och doseringsformer&quot;
* &quot;Inkludera ett försäkringsleverantörsfält med större transportföretag och plantyper&quot;

## Tidsanalys och kalenderanalys {#time-calendar-intelligence}

Smarta datum- och tidsfält med affärskontext och schemaläggningsinformation.

### Datum- och tidsfält

**Kontorstid och planering:**

    Lägg till ett fält för kontorstid med tidszonshantering
    Skapa en listruta med allmänna helgdagar per land
    Inkludera säsongsalternativ med datumintervall
    Lägg till ett fält för konferensrumsbokning med tillgänglighet
    Skapa ett urval för återkommande mötesmönster

**Exempeluppmaningar:**

* &quot;Skapa ett arbetstidsfält med tidszoner och semesterundantag&quot;
* &quot;Lägg till ett allmänt semesterurval med landsspecifika observationer&quot;
* &quot;Inkludera ett återkommande mötesmönsterfält med frekvensalternativ&quot;

## Produkter och tjänstekategorier {#product-service-categories}

E-handel och tjänsteinriktade områden med omfattande kategorisering.

### E-handelsklassificeringar

**Produkt- och tjänstdata:**

    Lägg till ett fält för produktkategorier med underkategorier
    Skapa en listruta med leveransmetoder med leveransuppskattningar
    Ta med ett fält för returpolicyalternativ
    Lägg till ett val för kundprioritetsnivåer
    Skapa ett fält för prenumerationsfaktureringscykler

**Exempeluppmaningar:**

* &quot;Skapa ett produktkategorifält med underkategorier och SKU-mönster för e-handel&quot;
* &quot;Lägg till en listruta för leveranssätt med leveranstider och kostnadsberäkningar&quot;
* &quot;Inkludera ett faktureringscykelfält för prenumeration med betalningsfrekvenser&quot;

## God praxis för smarta fält som förbättrats med LLM {#best-practices-smart-fields}

### Var specifik i dina förfrågningar

**Bra exempel:**

* &quot;Lägg till en nedrullningsbar meny med ISO-koder, fullständiga namn och valutainformation&quot;
* &quot;Skapa ett specialområde för medicin med brädcertifieringar och underspecialiteter&quot;
* &quot;Inkludera ett fält för programmeringsspråk med ramverk och kunskapsnivåer&quot;

**Undvik otydliga förfrågningar:**

* &quot;Lägg till ett landsfält&quot;
* &quot;Skapa en jobbtitellistruta&quot;
* &quot;Inkludera ett produktkategorifält&quot;

### Kombinera med villkorsstyrd logik

Smarta fält fungerar utmärkt med villkorliga regler:

    Skapa ett professionellt certifieringsfält som visar relevanta alternativ baserade på den valda branschen
    Lägg till ett stadsfält som filtreras baserat på det valda landet
    Ta med ett universitetsfält som anpassar sig baserat på det valda studiefältet

### Validera och anpassa

Fälten som förbättrats med LLM ger omfattande data, men alltid:

* **Granska de genererade alternativen** för att se om de är korrekta och relevanta
* **Lägg till anpassade alternativ** som är specifika för din organisation
* **Ta bort irrelevanta alternativ** för att effektivisera användarupplevelsen
* **Testa med riktiga användare** för att säkerställa användbarhet

## Avancerade tekniker för smarta fält {#advanced-smart-field-techniques}

### Sammanhangsberoende fält

Skapa fält som anpassar sig utifrån andra formulärval:

    Lägg till ett urvalsfält för universitet med större institutioner ordnade per land och rankning
    Skapa en professionell certifieringslistruta som visar relevanta alternativ baserat på befattning
    Ta med ett stadsfält som filtrerar baserat på valt land och region

### Klassificeringar på flera nivåer

Skapa hierarkiska datastrukturer:

    Skapa ett produktkategorifält med huvudkategorier, underkategorier och produkttyper
    Lägg till ett geografiskt fält med land, stat/provins och stadsnivåer
    Ta med ett kunskapsbedömningsfält med kategorier, underkategorier och kunskapsnivåer

### Integrering med externa data

Kombinera kunskap om livslångt lärande med organisationens data:

    Lägg till ett avdelningsfält som innehåller både vanliga företagsavdelningar och organisationens specifika avdelningar
    Skapa ett produktfält som kombinerar branschstandardkategorier med din produktkatalog
    Ta med ett platsfält som sammanfogar geografiska data med dina kontorslokaler

## Felsöka smarta fält {#troubleshooting-smart-fields}

### Vanliga problem och lösningar

**Problem: För många alternativ har genererats**

* **Lösning**: Var mer specifik i din begäran eller lägg till filtervillkor
* **Exempel**: I stället för&quot;alla länder&quot; begär&quot;viktiga partnerländer för handel&quot;

**Problem: Specifika alternativ saknas**

* **Lösning**: Lägg till anpassade alternativ eller förfina din fråga
* **Exempel**: &quot;Inkludera större länder plus [dina specifika länder]&quot;

**Problem: Inaktuell information**

* **Lösning**: Begär aktuella data eller ange datumintervall
* **Exempel**:&quot;Lägg till aktuella allmänna helgdagar för 2024&quot;

### Prestandaoptimering

* **Begränsa alternativ**: Använd filter för att minska antalet genererade alternativ
* **Progressiv visning**: Visa grundläggande alternativ först och tillåt sedan utökning
* **Cachelagring**: Överväg att cachelagra data som används ofta i smarta fält

## Relaterade artiklar

* [Komma igång med Forms Experience Builder](forms-experience-builder-getting-started.md)
* [Skapa formulär med AI-funktioner](forms-experience-builder-prompt-examples-library.md)
* [Skapa regler och logiska funktioner](forms-experience-builder-prompt-examples-library.md#rule-creation--business-logic)
* [Inlämning och integration av blanketter](form-submission-integration.md)

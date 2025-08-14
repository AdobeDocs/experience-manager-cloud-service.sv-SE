---
title: Konfigurera en omdirigeringssida eller ett tackmeddelande
description: Lär dig hur användare kan visa ett tackmeddelande eller omdirigeras till en webbsida som formulärförfattare kan konfigurera när de skapar formuläret.
feature: Adaptive Forms, Edge Delivery Services
role: User
level: Intermediate
source-git-commit: 07160248d5b5817d155a118475878ce04a687a32
workflow-type: tm+mt
source-wordcount: '1133'
ht-degree: 0%

---


# Konfigurera tackmeddelanden och omdirigerings-URL

Upplevelserna efter inlämningen påverkar i hög grad användarnas nöjdhet och antalet ifyllda formulär. Adobe Universal Editor har ett stort antal alternativ för att konfigurera vad användarna ser efter att ha skickat in formulär, antingen genom skräddarsydda tackmeddelanden eller strategiska omdirigeringar till specifika sidor.

I den här artikeln finns detaljerade riktlinjer för hur du implementerar både tackmeddelanden och omdirigerings-URL:er, inklusive tekniska överväganden, bästa praxis och riktlinjer för användarupplevelser för att maximera effekten av dina formulärinskickade formulär.

## Förutsättningar

Innan du konfigurerar upplevelser efter att produkten har skickats in måste du se till att du har:

**Teknisk konfiguration:**

- Tillgång till Universal Editor med rätt behörighet
- Ett befintligt adaptivt formulär som har skapats i den universella redigeraren
- Förstå kraven för din organisations omdirigerings-URL

**Planeringsöverväganden:**

- **Meddelandestrategi**: Definiera ton, längd och specifik information som ska ingå i tackmeddelanden
- **Omdirigeringsstrategi**: Identifiera målsidor och se till att de är optimerade för upplevelser efter att formuläret har fyllts i
- **Analysintegrering**: Planera hur du spårar användarinteraktioner med tackmeddelanden eller omdirigeringsmål

## Konfigurera tackmeddelanden

Tack för att du får ett meddelande med en omedelbar bekräftelse på att formuläret har skickats in och att det kan innehålla anpassat innehåll, nästa steg eller viktig information som är relevant för användarens inlämning.

### Använda tackmeddelanden när

Tack! Meddelanden fungerar bäst när:

- **Enkel bekräftelse**: Användarna måste bekräfta utan ytterligare navigeringskrav
- **Undervisningsinnehåll**: Du måste ange specifika nästa steg eller viktig information
- **Varumärkeskonsekvens**: Meddelandet kan utformas i linje med organisationens kommunikationsstil
- **Enkelsidig upplevelse**: Användare bör vara kvar på den aktuella sidan för att upprätthålla arbetsflödet

### Implementeringssteg

**1. Åtkomst till formuläregenskaper**

Öppna det adaptiva formuläret i den universella redigeraren och klicka på ikonen **Redigera formuläregenskaper** i verktygsfältet. Då öppnas en omfattande dialogruta för formuläregenskaper.

**2. Navigera till din konfiguration**

I dialogrutan Formuläregenskaper väljer du fliken **Tack** för att komma åt konfigurationsalternativen efter överföring.

**3. Konfigurera meddelandevisning**

Välj **Visa meddelande** bland de tillgängliga alternativen. Detta aktiverar meddelandets innehållsredigerare med avancerade textfunktioner.

**4. Skapa ditt meddelandeinnehåll**

I fältet **Meddelandeinnehåll** kan du skapa ett tackmeddelande med RTF-redigeraren. Redigeraren stöder:

- **Textformatering**: Alternativ för fet, kursiv, understrykning och färg
- **Listor**: Punktlistor och numrerade listor för att ordna information
- **Länkar**: Direktlänkar till relevanta resurser eller nästa steg
- **Fullskärmsredigering**: Klicka på ikonen Expandera för en större arbetsyta för redigering

### Tekniska överväganden

**Visningsbeteende för meddelanden:**

- Meddelanden visas i en modal övertäckning omedelbart efter att formuläret har skickats in
- Innehållet stöder HTML-formatering och bevarar responsiv design
- Meddelanden kan stängas av användare eller konfigureras med automatisk stängning av tidtagare

**Riktlinjer för innehåll:**

- Håll meddelandena koncisa samtidigt som du lämnar nödvändig information
- Inkludera rensning av nästa steg vid behov
- Överväg att inkludera referensnummer eller bekräftelseinformation
- Säkra mobilvänlig formatering

### Exempel på implementering

    Tack för ditt bidrag!
    
    Programmet har tagits emot och tilldelats referensnummer #REF-2024-001234.
    
    **Vad händer sedan:**
    - Du får ett bekräftelsemeddelande via e-post inom 15 minuter
    - Vårt team granskar ditt bidrag inom 2 arbetsdagar
    - Vi kontaktar dig direkt om ytterligare information behövs
    
    **Behöver du hjälp?** Kontakta vårt supportteam på support@example.com

## Konfigurera omdirigerings-URL:er

Omdirigerings-URL:er navigerar automatiskt till specifika sidor efter att formuläret har skickats in, vilket möjliggör smidig integrering med befintliga arbetsflöden eller dirigerar användare till relevant innehåll.

### När omdirigerings-URL ska användas

Omdirigerings-URL är optimala för:

- **Arbetsflödesintegration**: Vägleder användare till instrumentpaneler, kontosidor eller nästa steg i en process
- **Innehållsleverans**: Visar relevanta produkter, tjänster eller information baserat på formulärsvar
- **Analysspårning**: Riktning mot sidor med specifika spårningsimplementeringar
- **Flerstegsprocesser**: Flyttar användare till nästa fas i komplexa arbetsflöden

### Implementeringssteg

**1. Åtkomst till formuläregenskaper**

Öppna det adaptiva formuläret i den universella redigeraren och klicka på ikonen **Redigera formuläregenskaper** för att öppna dialogrutan för formulärkonfiguration.

**2. Navigera till din konfiguration**

Välj fliken **Tack** i dialogrutan Formuläregenskaper för att få tillgång till konfigurationsalternativen för omdirigering.

**3. Aktivera omdirigeringsfunktionen**

Välj **Omdirigera till URL** bland de tillgängliga alternativen efter överföring.

**4. Konfigurera mål-URL**

Ange mål-URL:en i fältet. Systemet stöder flera URL-format för flexibel implementering.

### URL-konfigurationsalternativ

**Absoluta URL:er**

Fullständiga webbadresser inklusive protokoll och domän:

    https://www.example.com/thank-you
    https://dashboard.example.com/user/profile

**Relativa sökvägar**

Sökvägar i förhållande till den aktuella domänen:

    /thanks-you
    /dashboard/user-profile
    ../confirmation-page.html

**AEM Sites sidreferenser**

Referenser till andra sidor i din AEM Sites-implementering:

    /content/mysite/en/thanks-you
    /content/mysite/en/next-steps

### Tekniska överväganden

**Omdirigeringsbeteende:**

- Omdirigeringar sker omedelbart efter det att formuläret har skickats in
- Webbläsarhistoriken innehåller omdirigering för korrekt bakåtknappsfunktion
- Omdirigeringstidsplanering kan konfigureras med valfria fördröjningar

**URL-validering:**

- URL-formatet valideras innan konfigurationen tillåts
- Relativa URL:er löses mot den aktuella domänen
- Externa URL-adresser kräver korrekt CORS-konfiguration vid behov

## Bästa praxis och rekommendationer

### Riktlinjer för användarupplevelser

**Meddelandeoptimering:**

- **Klarhet först**: Kontrollera att användarna direkt förstår att överföringen lyckades
- **Värdetillägg**: Ange information som hjälper användare med nästa steg
- **Konsekvent varumärkesprofilering**: Behåll organisationens röst och visuella stil
- **Mobil hänsyn**: Testa meddelanden på olika skärmstorlekar

**Omdirigeringsoptimering:**

- **Sidoptimering**: Kontrollera att omdirigeringsmål är optimerade för postformulärsbesökare
- **Inläsningsprestanda**: Verifiera att omdirigeringssidor läses in snabbt för att upprätthålla användarupplevelsen
- **Innehållsrelevans**: Kontrollera att omdirigeringsinnehåll är relevant för formulärsammanhanget

### Säkerhetsaspekter

**URL-validering:**

- Implementera korrekt validering för omdirigerings-URL:er för att förhindra skadliga omdirigeringar
- Överväg att använda vitlistmetoder för tillåtna omdirigeringsdomäner
- Övervaka omdirigeringsmönster för ovanlig aktivitet

**Innehållssäkerhet:**

- Sanera tackmeddelandeinnehåll för att förhindra skriptinjektion
- Lägg in lämpliga säkerhetsregler för RTF-material
- Regelbunden säkerhetsgranskning av omdirigerade destinationer

### Analyser och spårning

**Implementeringsöverväganden:**

- **Målspårning**: Ställ in analysmål för både tackmeddelandevyer och omdirigeringar
- **Mappning av användarresan**: Spåra hur användare interagerar med upplevelser efter överföringen
- **Konverteringsoptimering**: A/B-testa olika tackmeddelanden och omdirigeringsmål

**Mätningsstrategier:**

- Övervakningstid för tackmeddelanden innan uppsägning
- Spåra klickfrekvenser för länkar i tackmeddelanden
- Analysera användarbeteende på omdirigeringsmålsidor

## Kontrollpunkter för validering

När du har konfigurerat ditt arbete efter överföringen:

**Konfigurationsverifiering:**

- Formuläregenskaperna visar det valda tackalternativet korrekt
- Meddelandeinnehållet visas korrekt i förhandsgranskningsläge
- Omdirigerings-URL:er är korrekt formaterade och tillgängliga
- Alla länkar i meddelanden fungerar korrekt

**Testning av användarupplevelsen:**

- Skicka in testformulär för att verifiera att tackmeddelandet visas korrekt
- Testa omdirigeringsfunktioner i olika webbläsare
- Bekräfta att du svarar mobilt på tackmeddelanden
- Bekräfta omdirigering av destinationer läses in korrekt

**Analysinställningar:**

- Spårningskoder har implementerats korrekt för tackmeddelanden
- Spårning av omdirigeringsmål har konfigurerats
- Målslutförandehändelser har utlösts korrekt

## Nästa steg

När du har konfigurerat ditt arbete efter överföringen:

- **Övervaka prestanda**: Granska analyser för att förstå användarinteraktionen med tackmeddelanden eller omdirigeringssidor
- **Förbättra och förbättra**: Använd användarfeedback och datainsikter för att förfina din strategi efter överföring
- **Skalimplementering**: Använd framgångsrika mönster i andra formulär i organisationen

**Relaterad dokumentation:**

- [Konfigurationsguide för inskickning av formulär](submit-action.md)
- [Bästa praxis för användarupplevelser](responsive-layout.md)


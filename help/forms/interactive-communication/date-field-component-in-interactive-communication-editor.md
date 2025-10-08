---
title: Datumfältsobjekt i interaktiv kommunikationsredigerare
description: Med Datumfältsobjekt i Interactive Communication Editor i AEM Forms kan författare infoga ett kalenderbaserat datummarkeringsfält i ett dokument.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: bd8992792afddb2243736578acd24bc47efad842
workflow-type: tm+mt
source-wordcount: '683'
ht-degree: 0%

---


# Datumfältsobjekt i interaktiv kommunikationsredigerare

>[!NOTE]
>
> Funktionen för interaktiv kommunikation ingår i programmet för tidig anmälan. Skicka ett e-postmeddelande från din arbetsadress till `aem-forms-ea@adobe.com` för att begära åtkomst.

>[!IMPORTANT]
>
> **Dokumentation som kan ändras**: Det här snabbbiblioteket testas för närvarande mot produkten och kan komma att uppdateras och revideras. Frågar, exempel och bästa metoder kan ändras i takt med att Forms Experience Builder fortsätter att utvecklas under det program som antagits tidigt.

## &#x200B;1. Inledning

Med komponenten **Datumfält** i redigeraren för interaktiv kommunikation kan författare infoga ett kalenderbaserat datummarkeringsfält i ett dokument. På så sätt kan användare enkelt välja ett datum från en datumväljare eller ange det manuellt i ett fördefinierat format.

Datumfältet är idealiskt för hämtning av födelsedatum, scheman för avtalade tider, ansökningsdatum eller start-/slutdatum för principer, vilket förbättrar exaktheten och minskar antalet indatafel. Det har stöd för formatering, formatering och databindning för smidig integrering med datamodeller och backend-system.

![Sök efter IC Docu](/help/forms/interactive-communication/assets/date.png)

## &#x200B;2. Egenskaper

Objektet Datumfält innehåller flera konfigurerbara egenskaper:

2.1. Grundläggande fält

- **Namn:** En unik identifierare som används för att referera till fältet i regler, skript och datamodeller.

- **Bildtext:** Den visningsetikett som visas för användaren (t.ex. &quot;Födelsedatum&quot;).

- **Datum:** Det faktiska datumvärdet, som kan vara tomt som standard eller förifyllt med dynamiska data.

- **Reservera:** Ett valfritt reservdatum (visas om inget datum har valts eller om inga data är tillgängliga).

- **Utseende:** En snabbformatsförinställning (t.ex. understruken, platt, kantad) för visuell enhetlighet.

2.2. Typografi

Styr hur datumet visas visuellt i fältet:

- **Teckensnittsvariation:** Välj teckensnittsfamilj, vikt (t.ex. normal, fet) och stil (t.ex. kursiv).

- **Storlek:** är vanligtvis inställd på 10 punkter som standard, men kan anpassas för att vara konsekvent med omgivande innehåll.

2.3. Position

Definierar spatial placering i dokumentlayouten:

- **X- och Y-koordinater:** Anger vågrät och lodrät placering.

- **Bredd och höjd:** Ange i millimeter eller i procent för att justeras mot andra formulärelement.

2.4. Marginal

Anger avstånd runt fältets gränser:

- Överkant (uppåt)

- Nederkant (nedåt)

- Vänster

- Höger

Dessa värden är till hjälp med exakt justering i delformulär eller layoutstödraster.

2.5 Utseende

Definierar fältbehållarens visuella format:

- **Fyllning:** Fältets bakgrundsfärg (t.ex. vitt, ljusgrått).

- **Linje:** Kantfärg eller kontur.

- **Bredd:** Fältkantens tjocklek.

- **Stil:** Alternativ för heldragen, streckad eller prickad linje.

- **Kanter:** Anpassa hörn som rundade eller skarpa för olika designinställningar.

2.6 Närvaro

Anger hur och när fältet visas:

- **Synlig:** Standardinställning där fältet visas vid körning.

- **Dolt (behåller utrymme):** Fältet förblir osynligt, men layoututrymmet bevaras.

Detta är praktiskt när du växlar synlighet dynamiskt baserat på användarindata eller regler.

2.7. Databindning

Kopplar datumfältet till datastrukturer för lagring och förifyllning av värden.

**Databindningstyp:**

- **Använd namn:** Binder fältet till schemat med hjälp av namnattributet.

- **Använd globala data:** Bindningar med en fördefinierad datamodell eller ett schemaelement.

- **Ingen databindning:** Fältet förblir statiskt och är inte anslutet till någon datakälla.

Detta gör att dynamiska datumvärden kan hämtas, visas eller lagras baserat på programlogik.

## &#x200B;3. Användning

Datumfältet är särskilt användbart i följande scenarier:

- Registreringsdatum eller föreningsdatum i introduktionsformulär.

- Välja start- och slutdatum för tjänster, prenumerationer eller händelser.

- Ange ansökningsdeadline, avtalade tider eller verifieringsdatum.

Författare kan placera datumfältet i layoutbehållare eller delformulär och konfigurera valideringen (t.ex. datumformat, intervallgränser) för att förbättra datakvaliteten.

## &#x200B;4. Bästa praxis

- Använd tydliga beskrivningar som &quot;Startdatum&quot; eller &quot;Välj datum för avtalad tid&quot; för bättre användargränssnitt.

- Ange minsta och högsta datumintervall för att förhindra ogiltiga indata (t.ex. framtida DOB).

- Använd konsekventa teckensnittsformat (10 pt rekommenderas) för läsbarhet.

- Bind fält till schemat där integrering av backend-data behövs.

- Dölj ej relevanta datumfält dynamiskt med synlighetsregler.

Objektet **Datumfält** i redigeraren för interaktiv kommunikation är ett kraftfullt verktyg för att hämta tidskänsliga data med precision och enkelhet. När den är utformad med omsorg och kopplad till meningsfulla datasökvägar har den stöd för en sömlös användarupplevelse och effektiv bearbetning av tidsbaserade poster.



---
title: Delformulärsobjekt i interaktiv kommunikationsredigerare
description: Med delformulärsobjekt i Interactive Communication Editor i AEM Forms kan du ordna flera formulärelement på ett flexibelt och strukturerat sätt.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: acad9e05288a606c54e2059c2381725ac982f7d8
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 0%

---


# Delformulärsobjekt i interaktiv kommunikationsredigerare

>[!NOTE]
>
> Funktionen för interaktiv kommunikation ingår i programmet för tidig anmälan. Skicka ett e-postmeddelande från din arbetsadress till `aem-forms-ea@adobe.com` för att begära åtkomst.

>[!IMPORTANT]
>
> **Dokumentation som kan ändras**: Det här snabbbiblioteket testas för närvarande mot produkten och kan komma att uppdateras och revideras. Frågar, exempel och bästa metoder kan ändras i takt med att Forms Experience Builder fortsätter att utvecklas under det program som antagits tidigt.

## &#x200B;1. Inledning

Komponenten **Delformulär** i redigeraren för interaktiv kommunikation fungerar som en dynamisk layoutbehållare som gör att du kan ordna flera formulärelement på ett flexibelt och strukturerat sätt. Det används ofta för att gruppera relaterade fält, skapa upprepade avsnitt eller definiera kapslade datastrukturer för att förbättra användarupplevelsen och databindningen.

Delformulär kan konfigureras så att de flödar i olika layouter, t.ex. uppifrån och ned eller från vänster till höger, vilket gör dem idealiska för komplexa formulärdesigner och återanvändbara avsnitt.

![Sök efter IC Docu](/help/forms/interactive-communication/assets/subform.png)

## &#x200B;2. Egenskaper

2.1 Grundläggande egenskaper

- **Namn:** En unik identifierare för delformuläret som används i referenser, datamodeller och affärsregler.

- **Innehåll:** Definierar hur element i delformuläret ordnas.

   - **Positionerad:** Absolut placering av underordnade element med X- och Y-koordinater.

   - **Flödat (uppifrån och ned):** Ordnar elementen lodrätt.

   - **Flödat (vänster till höger):** Ordnar elementen vågrätt.

2.2 Position

- **Beskrivning:** Anger delformulärets placering i kommunikationslayouten.

- **Inställningar:**

   - X- och Y-koordinater (i mm)

   - Bredd och höjd (i mm)

2.3 Utseende

- **Fyllning:** Anger bakgrundsfärgen för delformulärsområdet.

- **Linje:** Definierar kantfärgen.

- **Bredd:** Anger kanttjockleken.

- **Stil:** Välj bland visuella förinställningar som platt, kantad eller förhöjd.

- **Kanter:** Bestämmer hörnformat - avrundat eller skarpt.

2.4 Närvaro

- **Beskrivning:** Styr delformulärets synlighet under körning.

- **Alternativ:**

   - **Synlig:** Visas alltid.

   - **Dold:** Visas inte, men utrymme behålls i layouten.

2.5 Databindning

- **Databindningstyp:** Länkar delformuläret till en datastruktur (vanligen XML eller JSON).

- **Använd namn:** Bindar data med delformulärets tilldelade namn.

- **Använd globala data:** Ansluter delformuläret till en global schemasökväg för delad dataanvändning.

- **Ingen databindning:** Delformuläret lagrar inte och interagerar inte med någon extern datamodell.

## &#x200B;3. Användning

Delformulär är viktiga i scenarier som kräver gruppering, kapsling eller upprepade fältuppsättningar. Vanliga tillämpningar:

- Ordna adressblock (t.ex. Gata, Ort, Postnummer)

- Upprepade avsnitt för radobjekt eller flera poster

- Strukturera logik för villkorliga formulär med synlighet och regler
Delformulär kan också användas som behållare för dra och släpp-justering i både statiska och dynamiska layouter.

## &#x200B;4. Bästa praxis

- Välj rätt layout (flödesbaserad eller positionerad) baserat på design- och databehov.

- Använd meningsfulla namn för att underlätta dataintegrering och regelreferenser.

- Formatera delformulär för att visuellt särskilja grupperade avsnitt.

- När du använder upprepade delformulär måste du se till att databindningen till arraystrukturer är korrekt.

- Använd regler för villkorlig synlighet för att optimera användarupplevelsen i komplexa formulär.

Objektet **Delformulär** i redigeraren för interaktiv kommunikation är ett kraftfullt sätt att strukturera och styra komplexa formulärlayouter. Delformulär förbättrar både användbarheten och underhållet av dokumentmallar, oavsett om det gäller att organisera inmatningsfält, hantera dynamiskt innehåll eller aktivera modulär design.



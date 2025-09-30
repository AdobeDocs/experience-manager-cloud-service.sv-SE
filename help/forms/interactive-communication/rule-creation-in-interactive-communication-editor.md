---
title: Skapa regel i interaktiv kommunikationsredigerare
description: Med regelgenerering i redigeraren för interaktiv kommunikation kan författare definiera dynamiska beteenden som gör kommunikationen interaktiv och intelligent.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
hide: true
index: false
hidefromtoc: true
source-git-commit: 0c84fa812b74368184d7085fecbb11a1ce4dbfd9
workflow-type: tm+mt
source-wordcount: '481'
ht-degree: 0%

---


# Skapa regel i interaktiv kommunikationsredigerare

>[!NOTE]
>
> Funktionen för interaktiv kommunikation ingår i programmet för tidig anmälan. Skicka ett e-postmeddelande från din arbetsadress till `aem-forms-ea@adobe.com` för att begära åtkomst.

>[!IMPORTANT]
>
> **Dokumentation som kan ändras**: Det här snabbbiblioteket testas för närvarande mot produkten och kan komma att uppdateras och revideras. Frågar, exempel och bästa metoder kan ändras i takt med att Forms Experience Builder fortsätter att utvecklas under det program som antagits tidigt.

## &#x200B;1. Inledning

Med regelgenerering i Interactive Communication Editor kan man definiera dynamiska funktioner som gör kommunikationen interaktiv och intelligent. Reglerna styr hur fält beter sig, visas eller beräknas baserat på användaråtgärder eller underliggande data, och ser till att varje kommunikation är anpassad och sammanhangsberoende.

Reglerna ger skaparna möjlighet att leverera upplevelser som anpassar sig i realtid, från enkla inställningar för synlighet till komplex villkorlig logik, vilket förbättrar användbarheten, tillförlitligheten och engagemanget.

## &#x200B;2. Egenskaper

2.1 Konfigurera fältegenskaper och beteenden

- **Indatatyper:** Definiera den typ av data som ett fält accepterar, till exempel text, siffror, datum eller booleska värden, för att säkerställa korrekt validering och formatering.

- **Synlighetsregler:** Kontrollera om ett fält är synligt, dolt eller dynamiskt visat baserat på villkor (t.ex. &quot;Visa endast rabattfält om kampanjkod används&quot;).

- **Standardvärden:** Fördefiniera värden i fält (t.ex. dagens datum, kundens namn från datamodellen) för att spara tid och förbättra noggrannheten.

2.2 Beräkningar, validering och regelredigerare

- **Fältlogik:** Automatisera beräkningar och fältrelationer, som att summera fakturabelopp eller fylla i beroende fält automatiskt.

- **Anpassade regler:** Skapa avancerad logik med regelredigeraren för komplexa scenarier som behörighetskontroller eller nivåbaserade priser.

- **Villkorliga åtgärder:** Definiera utlösare som svarar på användarindata eller datavärden, till exempel aktivera/inaktivera fält, visa meddelanden eller förgreningar till olika avsnitt.

## &#x200B;3. Användning

Regelskapande används ofta för att säkerställa att formulär och kommunikation är responsiva och sammanhangsberoende:

- **Dynamisk visning:** Dölj eller visa avsnitt baserat på kundtyp eller valda alternativ.

- **Validering:** Förebygg fel genom att kontrollera format, intervall eller obligatoriska indata.

- **Automatiska beräkningar:** Förenkla användaruppgifter med formler (t.ex. moms, summor eller rabatter).

- **Arbetsflödeskontroll:** Aktivera endast specifika knappar, fält eller åtgärder när förutsättningarna är uppfyllda.

- **Personalization:** Anpassa kommunikationen till mottagarens profil, inställningar eller behörighetskriterier.

## &#x200B;4. Bästa praxis

- **Behåll reglerna enkla:** Bryt komplex logik i mindre, modulära regler för enklare underhåll.

- **Prioritera synlighetslogik:** Dölj onödiga fält tidigt för att effektivisera användarupplevelsen.

- **Testa noggrant:** Förhandsgranska regler med flera datauppsättningar för att bekräfta exaktheten och undvika konflikter.

- **Använd standardvärden klokt:** Förifyllda fält som sällan ändras, men som ger flexibilitet vid redigering.

- **Utnyttja villkorliga åtgärder:** Använd dem för att förbättra interaktiviteten men undvika överväldigande användare.

- **Dokumentregler:** Upprätthåll affärslogik för att säkerställa tydlighet för utvecklare och intressenter.

Genom att konfigurera regler noggrant kan man skapa kommunikation som på ett intelligent sätt svarar på data och användaråtgärder - effektivisera processer, minska antalet fel och leverera en smidig, personaliserad upplevelse.

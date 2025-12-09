---
title: Skapa regler i interaktiv kommunikationsredigerare
description: Med Create Rules in Interactive Communication Editor kan man definiera dynamiska beteenden som gör kommunikationen interaktiv och intelligent.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: b2b85d1e802c7f287b875d53a9347ca07ea2b806
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 0%

---


# Regelredigeraren i den interaktiva kommunikationsredigeraren


>[!NOTE]
>
> Funktionen för interaktiv kommunikation ingår i programmet för tidig anmälan. Skicka ett e-postmeddelande från din arbetsadress till `aem-forms-ea@adobe.com` för att begära åtkomst.


>[!IMPORTANT]
>
> **Dokumentation som kan ändras**: Det här snabbbiblioteket testas för närvarande mot produkten och kan komma att uppdateras och revideras. Frågar, exempel och bästa metoder kan ändras i takt med att Forms Experience Builder fortsätter att utvecklas under det program som antagits tidigt.


## &#x200B;1. Inledning


Med regelredigeraren i Interactive Communication Editor kan författare definiera dynamiska beteenden som gör kommunikationen interaktiv och intelligent. Reglerna styr hur fält beter sig, visas eller beräknas baserat på användaråtgärder eller underliggande data, och ser till att varje kommunikation är anpassad och sammanhangsberoende.


Reglerna ger skaparna möjlighet att leverera upplevelser som anpassar sig i realtid, vilket förbättrar användbarheten, tillförlitligheten och engagemanget, från enkla synlighetsinställningar till komplex villkorlig logik.


![Sök efter IC-dokument](/help/forms/interactive-communication/assets/rule-creation.png)


## &#x200B;2. Egenskaper


2.1 Konfigurera fältegenskaper och beteenden


- **Indatatyper:** Definiera den typ av data som ett fält accepterar, till exempel text, siffror, datum eller booleska värden, för att säkerställa korrekt validering och formatering.


- **Synlighetsregler:** Kontrollera om ett fält är synligt, dolt eller dynamiskt visat baserat på villkor (t.ex. &quot;Visa endast rabattfält om kampanjkod används&quot;).


- **Standardvärden:** Fördefiniera värden i fält (t.ex. dagens datum, kundens namn från datamodellen) för att spara tid och förbättra noggrannheten.


2.2 Implementera beräkningar, valideringar och regellogik


- **Fältlogik:** Automatisera beräkningar och fältrelationer, som att beräkna fakturabelopp eller fylla i beroende fält automatiskt.


- **Anpassade regler:** Skapa avancerad logik med regelredigeraren för komplexa scenarier som behörighetskontroller eller nivåbaserade priser.


- **Villkorliga åtgärder:** Definiera utlösare som svarar på användarindata eller datavärden, till exempel aktivera/inaktivera fält, visa meddelanden eller förgreningar till olika avsnitt.


![Sök efter IC-dokument](/help/forms/interactive-communication/assets/rule-creation1.png)


## &#x200B;3. Användning


Regelredigeraren används ofta för att säkerställa att formulär och kommunikation är responsiva och sammanhangsberoende:


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




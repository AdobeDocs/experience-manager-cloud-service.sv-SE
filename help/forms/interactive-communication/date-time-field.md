---
title: Fält för datum/tid i interaktiv kommunikationsredigerare
description: Datum-/tidfältskomponent i interaktiv kommunikationsredigerare i AEM Forms, med vilken författare kan infoga fält där användare kan välja eller ange datum- och/eller tidsvärden.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
exl-id: 7ac93d8c-5454-4789-a7cd-438571a9ff28
source-git-commit: cdaceaabb8eeeec931b1897e1161f408606540b9
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 0%

---

# Datum-/tidfältskomponent i interaktiv kommunikationsredigerare

>[!NOTE]
>
> Funktionen för interaktiv kommunikation ingår i programmet för tidig anmälan. Skicka ett e-postmeddelande från din arbetsadress till `aem-forms-ea@adobe.com` för att begära åtkomst.

## &#x200B;1. Inledning

Med komponenten **Datum/tid-fält** i redigeraren för interaktiv kommunikation (IC) kan författare infoga fält där användare kan välja eller ange datum- och/eller tidsvärden. Den här komponenten används ofta för att samla in information som födelsedatum, scheman för avtalade tider, bokningsfack eller datum för dokumentutleverans/utgångsdatum.

Fältet har stöd för olika formateringsalternativ (t.ex. formaten DD/MM/ÅÅÅÅ, 24-timmarsformat eller 12-timmarsformat), valideringsbegränsningar och anpassning av utseendet så att det matchar kommunikationsdesignen. Det förbättrar användarupplevelsen genom att minska antalet manuella inmatningsfel och främja enhetlighet i datainsamlingen.

![Sök efter IC Docu](/help/forms/interactive-communication/assets/datetime.png)

## &#x200B;2. Egenskaper

Komponenten för datum/tidsfält innehåller flera konfigurerbara egenskaper:

2.1. Grundläggande fält

- **Namn:** En unik identifierare för fältet. Används för referens i regler, uttryck och databindningar.

- **Bildtext:** Etiketten som visas bredvid fältet för att ange dess syfte (t.ex. &quot;Födelsedatum&quot;).

- **Datum:** Tillåter användare att välja eller ange ett kalenderdatum.

- **Tid:** Aktiverar inmatning eller val av specifika tidsvärden om de är konfigurerade.

- **Reservera:** Ett reservvärde som visas när ingen inmatning har angetts, vilket är användbart för skrivskyddade scenarier eller utskriftsscenarier.

- **Utseende:** Välj ett visuellt format som understruket, kantat eller platt för enhetlig gränssnittsåtergivning.

2.2. Typografi

Styr stilen på texten i datum/tid-fältet:

- **Teckensnittsvariant:** Alternativen inkluderar Normal, Fet, Kursiv beroende på temats krav.

- **Teckensnittsstorlek:** Standardvärdet är 10 punkter för att bibehålla en konsekvent layout med formulärlayouten.

2.3. Position

- **Beskrivning:** Definierar placeringen av datum/tid-fältet i formulärlayouten.

- **Inställningar:**

   - **X- och Y-koordinater**

   - **Höjd och bredd** (mäts i mm eller pixlar) för att ändra storlek på fältet exakt.

2.4. Marginal

Definierar avstånd runt fältet för ren justering och flexibel layout:

- Överkant (uppåt)

- Nederkant (nedåt)

- Vänster

- Höger

2.5 Utseende

Definierar behållarens format för att bibehålla visuell konsistens och skärpa:

- **Fyllning:** Fältets bakgrundsfärg.

- **Linje:** Kantfärg runt fältet.

- **Bredd:** Tjocklek på kanten.

- **Stil:** Kantlinjetyper som heldragen, streckad eller ingen.

- **Kanter:** Välj mellan skarpa eller rundade hörn beroende på formulärtemat.

2.6 Närvaro

Bestämmer hur fältet fungerar vid körning:

- **Synlig:** Fältet visas för användare och tar upp layoututrymme.

- **Dold (behåller utrymme):** Fältet är inte synligt, men utrymme är fortfarande reserverat för det i layouten.

2.7. Databindning

Länkar fältet till en datakälla för att lagra eller hämta värden.

- **Databindningstyp:** Anger hur fältet ansluts till data.

- **Använd namn:** Binder fältet med fältnamnet som definierats i schemat.

- **Använd globala data:** Ansluter fältet till data på global nivå som delas i hela kommunikationen.

- **Ingen databindning:** Fältet är inte anslutet till några backend-data (används endast för visuella eller beräknade värden).

## &#x200B;3. Användning

Fältet Datum/tid är idealiskt i scenarier där konsekventa tidsdata krävs. Exempel på vanliga användningsområden:

- Hämtningsdatum för födelse, datum för avtalad tid eller tid för händelse

- Utgåva/utgångsdatum för loggningsdokument

- Välja leverans- eller hämtningsfack

- Tidsstämplar för inspelning av transaktion

Författare kan kombinera fältet med layoutbehållare, valideringar eller villkorliga regler för att styra format, obligatoriska fält och sammanhangsberoende synlighet.

## &#x200B;4. Bästa praxis

- Använd tydliga beskrivningar som&quot;Välj ett datum&quot; eller&quot;Tid för avtalad tid&quot; för att vägleda användarna.

- Aktivera datum-/tidsväljaren för bättre användarupplevelser och färre indatafel.

- Använd formatbegränsningar (t.ex. endast framtida datum) vid behov.

- Ange ett reservvärde för tillgänglighet eller utskrift.

- Se till att typografin och utseendet överensstämmer med den övergripande formulärdesignen.

- Bind fältet till en giltig schemasökväg för att säkerställa korrekt datainhämtning och databearbetning.

Date/Time Field-komponenten i Interactive Communication Editor är en kraftfull och användarvänlig komponent som effektiviserar tidsbaserad inmatning. Med rätt konfiguration av formatering, datahantering och layoutkontroller kan man skapa rena, tillförlitliga och intuitiva formulärupplevelser för både användare och backend-system.

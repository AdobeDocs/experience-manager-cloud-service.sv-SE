---
title: Tabellkomponent i interaktiv kommunikationsredigerare
description: Med Table Component in Interactive Communication Editor i AEM Forms kan man enkelt infoga anpassningsbara tabeller i kommunikationsmallar.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: e651869132a232db577e94946c082c46eea26bb3
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 0%

---


# Tabellkomponent i interaktiv kommunikationsredigerare

>[!NOTE]
>
> Funktionen för interaktiv kommunikation ingår i programmet för tidig anmälan. Skicka ett e-postmeddelande från din arbetsadress till `aem-forms-ea@adobe.com` för att begära åtkomst.

>[!IMPORTANT]
>
> **Dokumentation som kan ändras**: Det här snabbbiblioteket testas för närvarande mot produkten och kan komma att uppdateras och revideras. Frågar, exempel och bästa metoder kan ändras i takt med att Forms Experience Builder fortsätter att utvecklas under det program som antagits tidigt.

## &#x200B;1. Inledning

Med tabellkomponenten i redigeraren för interaktiv kommunikation kan författare enkelt infoga anpassningsbara tabeller i kommunikationsmallar. Den här komponenten stöder tabelldatarepresentation för användningsfall som sammanfattningar, artikellistor, strukturerade indata eller jämförelselayouter.

Författare kan dra och släppa tabellkomponenten på arbetsytan, konfigurera antalet rader och kolumner och välja alternativ som att ta med huvud- och fotrader eller ange layoutriktning. Tabeller kan definieras som standardmallar för enhetlig kommunikation i flera olika sammanhang.

![Sök efter IC Docu](/help/forms/interactive-communication/assets/table.png)

## &#x200B;2. Egenskaper

Tabellkomponenten innehåller flera konfigurerbara egenskaper som hjälper författare att anpassa tabellens beteende och utseende:


2.1 Grundläggande fält

- **Namn:** En unik identifierare för tabellen. Det här namnet används internt för att referera till tabellen i datamodeller och logik.

- **Rader:** Anger antalet innehållsrader (exklusive huvud och fot).

- **Kolumner:** Definierar antalet kolumner i tabellen.

- **Rubrikrad:** Alternativ för att ta med en rubrikrad högst upp i tabellen för kolumnrubriker.

- **Sidfotsrad:** Alternativ för att inkludera en sidfotsrad för summor eller sammanfattningsvärden.

- **Ange som standard:** Tillåter användare att spara den aktuella konfigurationen som en standardtabellmall för framtida bruk.

- **Layoutriktning:** Definierar hur rader fylls i - anges vanligtvis till vänster till höger.

2.2 Position

- **Beskrivning:** Styr tabellens placering i layouten.

- **Inställningar:**

   - **X- och Y-koordinater:** Anger tabellens vågräta (X) och lodräta (Y) positioner på arbetsytan.

   - **Höjd och bredd:** Definierar tabellens totala storlek (i mm), vilket möjliggör flexibel utrymmesallokering.

2.3 Utseende

**Utseende:** Anger tabellens visuella format. Författare kan välja bland fördefinierade förinställningar som kantlinje, platt eller förhöjd.

- **Fyllning:** Bakgrundsfärg för tabellen eller cellerna.

- **Linje:** Kantfärg runt tabellen eller specifika celler.

- **Bredd:** Tjocklek på kantlinjerna.

- **Stil:** Välj kanttyper - rundade hörn eller skarpa hörn.

- **Kanter:** Konfigurera synlighet för cellkanter och hörnradie.

2.4 Närvaro

- **Beskrivning:** Anger tabellens synlighet vid körning.

- **Alternativ:**

   - **Synlig:** Visa tabellen normalt i utdata.

   - **Dold:** Dölj tabellen men behåll utrymme i layouten.

2.5 Databindning

**Databindning:** Koppla tabellen med en datakälla (t.ex. JSON, XML-schema) för att dynamiskt fylla i rader och kolumner med värden under genereringen. Detta är användbart för specificerad fakturering, transaktionsposter eller produktlistor.

## &#x200B;3. Användning

Tabellkomponenten är idealisk för att visa strukturerad eller upprepad information. Exempel på användningsområden är:

- Fakturor och växlar med artikelrader

- Jämförelser av policyer och planer

- Sammanfattningar av profil- eller kontodata

- Produktkataloger eller funktionsmatriser

Författare kan konfigurera antalet rader och kolumner, tillämpa villkorlig synlighet eller binda data för att visa dynamisk information.

## &#x200B;4. Bästa praxis

- Använd rubrikrader för att tydligt märka varje kolumn så att den blir lättare att läsa.

- Använd sidfotsrader för summor eller viktiga anteckningar där det är tillämpligt.

- Använd databindning för att fylla i rader dynamiskt baserat på strukturerade indata.

- Bibehåll enhetlig formatering och konsekvent mellanrum med hjälp av inställningar för utseende och marginaler.

- När du döljer en tabell måste du se till att det finns kontinuitet i layouten genom att välja om du vill behålla utrymme eller inte.

- Använd standardmallar för att standardisera tabellinnehåll i olika dokument.

Table Component in the IC editor är en flexibel, datavänlig komponent som har utformats för att stödja strukturerat innehåll i kommunikationen. Med anpassningsbara layoutalternativ, formateringsfunktioner och kraftfull databindning kan man presentera information på ett tydligt och effektivt sätt.



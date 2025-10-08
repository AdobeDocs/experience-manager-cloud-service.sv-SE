---
title: Komponenten Rectangle i Interactive Communication Editor
description: Med Rectangle Component i Interactive Communication Editor i AEM Forms kan man lägga in grafiska element som fungerar som layoutavgränsare, visuella accenter eller innehållsbehållare.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: bd8992792afddb2243736578acd24bc47efad842
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 0%

---


# Komponenten Rectangle i Interactive Communication Editor

>[!NOTE]
>
> Funktionen för interaktiv kommunikation ingår i programmet för tidig anmälan. Skicka ett e-postmeddelande från din arbetsadress till `aem-forms-ea@adobe.com` för att begära åtkomst.

>[!IMPORTANT]
>
> **Dokumentation som kan ändras**: Det här snabbbiblioteket testas för närvarande mot produkten och kan komma att uppdateras och revideras. Frågar, exempel och bästa metoder kan ändras i takt med att Forms Experience Builder fortsätter att utvecklas under det program som antagits tidigt.

## &#x200B;1. Inledning

Med komponenten Rectangle i redigeraren för interaktiv kommunikation (IC) kan författare lägga till formade grafiska element som fungerar som layoutavgränsare, visuella accenter eller innehållsbehållare. Rektanglar förbättrar den visuella hierarkin och vägleder användaren i strukturerade kommunikationslayouter.
Den här komponenten är inte knuten till data, men den bidrar till att förbättra tydligheten i designen, gruppera relaterade fält och förbättra den övergripande presentationen.

![Sök efter IC Docu](/help/forms/interactive-communication/assets/rectangle.png)

## &#x200B;2. Egenskaper

Komponenten Rectangle innehåller flera anpassningsbara egenskaper:

2.1. Namn

Namn: En unik identifierare för rektangeln. Används främst för att referera i layouthierarkier eller använda format på ett konsekvent sätt.

2.2. Position

- **Beskrivning:** Avgör var rektangeln visas i dokumentlayouten.

- **Inställningar:**

   - **X- och Y-koordinater:** Definiera vågrät och lodrät placering.

   - **Höjd och bredd (i mm):** Kontrollera storleken på rektangeln.

2.3. Marginal

Definierar avstånd runt rektangelkomponenten för att separera den från andra gränssnittselement:

- Överkant (uppåt)

- Nederkant (nedåt)

- Vänster

- Höger

2.4 Utseende

- **Beskrivning:** Styr rektangelns visuella format.

- **Anpassningsalternativ:**

   - **Fyllning:** Rektangelns interna färg.

   - **Linje:** Rektangelns konturfärg.

   - **Linjebredd:** Tjocklek för rektangelns kant.

   - **Stil:** Förinställda stilar som platt, kantad eller upphöjd.

   - **Kanter:** Styr utseendet på hörn (t.ex. rundade eller skarpa kanter).

2.5 Närvaro

- **Beskrivning:** Anger om rektangeln visas när kommunikationen återges.

- **Alternativ:**

   - **Synlig:** Visar rektangeln vid körning.

   - **Dold:** Behåller layoututrymmet utan att visa rektangeln.

## &#x200B;3. Användning

Komponenten Rectangle används vanligtvis för layout- och formateringsändamål i stället för som innehållsindata. Exempel på vanliga användningsområden:

- Skapa visuell separation mellan avsnitt

- Markera grupperade element

- Förbättrad läsbarhet och visuell balans

- Bildrubriker, sidfötter eller utlysningsavsnitt

Rektanglar kan kombineras med andra layoutelement som delformulär eller behållare för komplexa visuella designstrukturer.

## &#x200B;4. Bästa praxis

- Använd enhetlig formatering för rektanglar i hela layouten för att säkerställa visuell harmoni.

- Använd lämpliga marginaler och mellanrum för att förhindra att intilliggande fält trängs ihop.

- Välj fyllnings- och linjefärger som passar ert varumärke eller dokumenttema.

- Använd rundade kanter subtilt för att förbättra estetiken i moderna gränssnittslayouter.

- Dölj rektanglar om de bara behövs för designändamål vid redigering, men inte för slutresultatet.

Rektangelkomponenten är ett icke-interaktivt men kraftfullt verktyg i IC Editor. När de är formaterade och placerade effektivt förbättrar de layoutens precision, visuella flöde och användarupplevelse utan att databindningen eller interaktiviteten blir mer komplex.



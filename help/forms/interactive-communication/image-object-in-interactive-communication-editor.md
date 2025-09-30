---
title: Bildobjekt i interaktiv kommunikationsredigerare
description: Skapa interaktiva kommunikationsfragment i AEM Forms med vilka författare kan förbättra kommunikationslayouten genom att infoga statiska bilder.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: acad9e05288a606c54e2059c2381725ac982f7d8
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 0%

---


# Bildobjekt i interaktiv kommunikationsredigerare

>[!NOTE]
>
> Funktionen för interaktiv kommunikation ingår i programmet för tidig anmälan. Skicka ett e-postmeddelande från din arbetsadress till `aem-forms-ea@adobe.com` för att begära åtkomst.

>[!IMPORTANT]
>
> **Dokumentation som kan ändras**: Det här snabbbiblioteket testas för närvarande mot produkten och kan komma att uppdateras och revideras. Frågar, exempel och bästa metoder kan ändras i takt med att Forms Experience Builder fortsätter att utvecklas under det program som antagits tidigt.

## &#x200B;1. Inledning

Med bildobjektet i den interaktiva kommunikationsredigeraren kan författare förbättra kommunikationslayouten genom att infoga statiska bilder. Den här komponenten är viktig när du vill skapa visuellt tilltalande layouter och införliva varumärkeselement som logotyper och visuella ikoner. Författare kan montera den i både mallsidor och designvyn för att säkerställa ett konsekvent utseende i olika utdataformat, t.ex. PDF.

![Sök efter IC Docu](/help/forms/interactive-communication/assets/image.png)

## 2.Properties

Bildobjektet innehåller flera egenskaper som hjälper dig att konfigurera dess utseende, känsla och beteende.

2.1. Bildbeskrivning

Namn:
Fungerar som en unik identifierare för bildkomponenten, vilket gör det enkelt att referera till i komponenthierarkin eller regelredigeraren.

Välj Bild: Gör att författaren kan överföra eller referera till en bild, till exempel en logotyp, ikon eller någon annan statisk bild från flera källor.


2.2. Position

Beskrivning: Styr bildens rumsliga placering i layouten.

Inställningar:

X- och Y-koordinater

Höjd och bredd (i mm)

2,3 marginal

Definiera avstånd runt textrutan:

- Överkant (uppåt)

- Nederkant (nedåt)

- Vänster

- Höger

2.4 Utseende

Utseende: Definierar bildfältets visuella stil, väljer förinställningar som kantlinje, platt eller upphöjd och anpassar med fyllningsfärg, linjebredd och hörnformat (rundad eller skarp).

2.5 Närvaro

Beskrivning: Anger synligheten för bildobjektet vid körning.

- Alternativ:

   - Synlig

   - Dold (behåller utrymme)

## 3.Usage

Bildobjektet är idealiskt för

- Infoga logotyper i dokumentrubriker

- Visa produktbilder i fakturor eller offerter

- Ökat visuellt engagemang i kommunikation

## 4.Bästa praxis

- Använd bilder från ett delat bibliotek för enkel återanvändning och enhetlighet.

- Behåll bildens form konsekvent för att undvika att sträcka ut eller pixelera.

- Undvik att använda mycket stora bildfiler för att dokumentet ska vara snabbt och responsivt.

- Ange att bilden ska visas eller döljas om den inte alltid behövs.

Bildobjektet i AEM Interactive Communication spelar en viktig roll när det gäller att skapa varumärkesprofilerad, personlig och visuellt effektiv kommunikation. Med konfigurerbara egenskaper förbättras användarupplevelsen samtidigt som designen är konsekvent i olika format.

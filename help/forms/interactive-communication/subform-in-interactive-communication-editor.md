---
title: Delformulär i interaktiv kommunikationsredigerare
description: Delformulär i Interactive Communication Editor hanterar layouter, styr objektpositionering och definierar hur innehåll flödar över sidor.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
hide: true
index: false
hidefromtoc: true
source-git-commit: 0c84fa812b74368184d7085fecbb11a1ce4dbfd9
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 0%

---


# Delformulär i interaktiv kommunikationsredigerare

>[!NOTE]
>
> Funktionen för interaktiv kommunikation ingår i programmet för tidig anmälan. Skicka ett e-postmeddelande från din arbetsadress till `aem-forms-ea@adobe.com` för att begära åtkomst.

>[!IMPORTANT]
>
> **Dokumentation som kan ändras**: Det här snabbbiblioteket testas för närvarande mot produkten och kan komma att uppdateras och revideras. Frågar, exempel och bästa metoder kan ändras i takt med att Forms Experience Builder fortsätter att utvecklas under det program som antagits tidigt.

## &#x200B;1. Inledning

Ett delformulär i Interactive Communication Editor är ett behållarobjekt som används för att gruppera fält, objekt och komponenter i ett logiskt avsnitt. Det hjälper dig att hantera layouter, styra objektplaceringen och definiera hur innehållet flödar över sidor. Delformulär är nödvändiga för att skapa strukturerad, återanvändbar och responsiv kommunikation, särskilt när det gäller dynamiskt eller upprepat innehåll.

Genom att använda delformulär kan författare bibehålla enhetligheten, hantera sidnumrering och binda hela avsnitt till strukturerade datakällor.

## &#x200B;2. Egenskaper

2.1 Formulärdesignlayouter

- **Fast layout:** Objekt behåller exakta positioner på sidan. Bäst för statiska designer där precisionsplacering krävs (t.ex. fakturor eller officiella brev).

- **Flödeslayout:** Objekten justeras dynamiskt baserat på innehållets längd och skärmstorlek. Passar för kommunikation som kräver responsiv design eller olika datalängder.

2.2 Placering av delformulär

- **Sidnumrering:** Styr hur delformulär bryts mellan sidor. Du kan till exempel hålla ihop delformulär eller tillåta sidbrytningar i dem.

- **Position:** Ange om delformuläret ska placeras i förhållande till dess överordnade behållare eller om det ska flöda naturligt i layouten.

- **Utseende:** Definiera bakgrund, kanter och format för delformuläret så att innehållet separeras visuellt.

- **Närvaro:** Konfigurera synlighetsinställningar - Synlig, Dold eller Villkorlig - beroende på affärsregler eller datavärden.

2.3 Databindning

- Delformulär kan bindas direkt till **FDM-noder (Form Data Model)** eller matriser.

- Med bindning kan delformuläret upprepas dynamiskt för varje post i en samling (t.ex. flera principer, transaktioner eller adresser).

- Stöder både statisk och dynamisk ifyllning av innehåll baserat på datastrukturen.

## &#x200B;3. Användning

Delformulär används ofta för

- Strukturera dokument i avsnitt som sidhuvud, brödtext och sidfot.

- Upprepat innehåll som tabeller, specificerade räkningar eller listor med profiler.

- Hantera sidnumrering så att grupperat innehåll hålls ihop.

- Villkorlig visning av avsnitt baserat på regler eller datavärden.

- Använder layoutkontroll (fast eller flödande) beroende på kommunikationstyp.

Författare kan dra ett delformulär från objektbiblioteket till arbetsytan och justera dess layout, placering och bindning från egenskapspanelen.

## &#x200B;4. Bästa praxis

- **Välj layout klokt:** Använd fast layout för formulär som kräver exakt placering och flödeslayout för dynamiska, datadrivna dokument.

- **Bind samlingar noggrant:** Bind delformulär direkt till FDM-samlingar med mallrader för listor eller arrayer.

- **Optimera sidnumrering:** Förhindra klumpiga brytningar genom att gruppera relaterade objekt i ett delformulär.

- **Använd villkorlig närvaro:** Dölj eller visa delformulär dynamiskt baserat på datavärden.

- **Behåll hierarkin:** kapsla delformulär logiskt för att göra komplexa layouter enklare att hantera.

- **Testa med varierade data:** Förhandsgranska med korta, långa och tomma datauppsättningar för att säkerställa att designen anpassas korrekt.

Genom att utnyttja delformulär effektivt kan man få renare layout, bättre kontroll över dynamiskt innehåll och säkerställa att kommunikationen smidigt kan anpassas till både datadrivna och statiska scenarier.

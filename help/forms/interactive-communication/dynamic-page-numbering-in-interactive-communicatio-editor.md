---
title: Dynamisk sidnumrering i Interactive Communication Editor
description: Med Dynamic Page Numbering i Interactive Communication Editor kan man automatiskt visa sidnummer i PDF-utdata.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: 371838c77beafa8c67259a865b25325632bea0b0
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 0%

---


# Dynamisk sidnumrering i Interactive Communication Editor

>[!NOTE]
>
> Funktionen för interaktiv kommunikation ingår i programmet för tidig anmälan. Skicka ett e-postmeddelande från din arbetsadress till `aem-forms-ea@adobe.com` för att begära åtkomst.

>[!IMPORTANT]
>
> **Dokumentation som kan ändras**: Det här snabbbiblioteket testas för närvarande mot produkten och kan komma att uppdateras och revideras. Frågar, exempel och bästa metoder kan ändras i takt med att Forms Experience Builder fortsätter att utvecklas under det program som antagits tidigt.

## Introduktion

Med funktionen Dynamic Page Numbering i Interactive Communication (IC) kan man automatiskt visa sidnummer i PDF-utdata. Sidnumrering kan aktiveras på mallsidenivå, vilket ger en konsekvent numrering över alla associerade designsidor. Detta gör det lättare att hålla ordning på sidorna och ha en professionell layout i flersidig kommunikation.

## Nyckelfunktioner

- **Konfiguration av huvudsida:**
Sidnumrering kan aktiveras på mallsidenivå. Komponenten kan placeras var som helst på arbetsytan efter att ha släppts och anpassats fritt, eftersom den har stöd för alla egenskaper som är tillgängliga i textkomponenten.

- **Automatisk placering:**
En sidnumreringskomponent visas längst ned i mitten på varje sida med formatet:
&quot;**Sidnummer av ##**&quot;

   - Den första **#** representerar det aktuella sidnumret.

   - Den andra **##** representerar det totala antalet sidor i kommunikationen.

- **Dynamisk visning i PDF Preview:**
Sidnumren återges dynamiskt under PDF-förhandsgranskning och ger korrekt sidnumrering i det slutliga resultatet.

### Exempel

När du förhandsgranskar en interaktiv 5-sidig kommunikation visas följande på varje sida:

Sidan 1 av 5

Sidan 2 av 5

... och så vidare, uppdateras dynamiskt under PDF-genereringen.

## Viktiga fördelar

- Förbättrar dokumentläsbarheten och professionalismen.

- Automatiserar sidnumreringen utan manuell åtgärd.

- Bibehåller enhetligheten på alla sidor som är länkade till en mallsida.

---
title: Från kalkylblad till Forms - Mastering Adaptive Form Block - fältverifieringar
description: Skapa kraftfulla formulär snabbare med kalkylblad och anpassade formulärblocksfält! Den här guiden hjälper dig att skapa anpassade valideringar för EDS Forms Block-fält.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
exl-id: 16e1d42a-42d0-4335-ba81-feedea7ed7d7
source-git-commit: 53a66eac5ca49183221a1d61b825401d4645859e
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---

# Lägga till valideringar i formulärfält

Adaptivt formulärblock har inbyggda valideringsfunktioner. Dessa valideringar används automatiskt i moderna webbläsare baserat på den valda fälttypen och de ytterligare egenskaper du anger.

## Fälttyper och validering

Det adaptiva formulärblocket har stöd för en mängd olika [Indatatyper för HTML-5](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#input_types), inklusive text, e-post, nummer, datum med mera. Den rymmer också [textområde](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea), urval och fältuppsättning tillsammans med omfattande indatavalideringsfunktioner som är inbyggda i HTML-5.

använder fälttyper i HTML för att definiera vilken typ av data som en användare kan ange. Olika fälttyper har olika inbyggda valideringsregler:

E-post: Den här fälttypen validerar automatiskt användarindata mot ett vanligt e-postadressformat. Användare som anger en ogiltig e-postadress får ett felmeddelande.
Nummer: Den här fälttypen tillåter endast numeriska indata. Användare som skriver icke-numeriska tecken får ett fel.
Datum: Den här fälttypen validerar användarindata mot ett standarddatumformat. Datum utanför ett rimligt intervall kan också markeras som ogiltiga.
URL: Den här fälttypen validerar användarindata mot ett giltigt URL-format. Användare som anger en ogiltig URL får ett felmeddelande.
Tel: Den här fälttypen är särskilt utformad för telefonnummer och kan utlösa validering baserad på specifika landformat (stöds inte överallt).




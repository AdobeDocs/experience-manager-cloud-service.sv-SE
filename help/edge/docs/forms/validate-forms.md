---
title: Från kalkylblad till Forms - Mastering Adaptive Forms Block Field Validations
description: Skapa kraftfulla formulär snabbare med kalkylblad och anpassade Forms-blockfält! Den här guiden hjälper dig att skapa anpassade valideringar för EDS Forms Block-fält.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
exl-id: 16e1d42a-42d0-4335-ba81-feedea7ed7d7
role: Admin, Architect, Developer
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---

# Lägga till valideringar i formulärfält

Adaptiv Forms Block har inbyggda valideringsfunktioner. Dessa valideringar används automatiskt i moderna webbläsare baserat på den valda fälttypen och de ytterligare egenskaper du anger.

## Fälttyper och validering

Det adaptiva Forms-blocket har stöd för en mängd olika [HTML-5-indatatyper](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#input_types), inklusive text, e-post, tal, datum och mer. Den innehåller även [textarea](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea), select och fieldsSet tillsammans med omfattande indatavalideringsfunktioner som är inbyggda i HTML-5.

använder fälttyper i HTML för att definiera vilken typ av data som en användare kan ange. Olika fälttyper har olika inbyggda valideringsregler:

E-post: Den här fälttypen validerar automatiskt användarindata mot ett vanligt e-postadressformat. Användare som anger en ogiltig e-postadress får ett felmeddelande.
Nummer: Den här fälttypen tillåter endast numeriska indata. Användare som skriver icke-numeriska tecken får ett fel.
Datum: Den här fälttypen validerar användarindata mot ett standarddatumformat. Datum utanför ett rimligt intervall kan också markeras som ogiltiga.
URL: Den här fälttypen validerar användarindata mot ett giltigt URL-format. Användare som anger en ogiltig URL får ett felmeddelande.
Tel: Den här fälttypen är särskilt utformad för telefonnummer och kan utlösa validering baserad på specifika landformat (stöds inte överallt).




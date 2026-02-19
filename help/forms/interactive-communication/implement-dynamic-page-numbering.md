---
title: Dynamisk sidnumrering i Interactive Communication Editor
description: Med Dynamic Page Numbering i Interactive Communication Editor kan man automatiskt visa sidnummer i PDF-utdata.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
exl-id: 9f29da7d-72ad-4737-9ae3-d5cdc4f5ed25
source-git-commit: cdaceaabb8eeeec931b1897e1161f408606540b9
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---

# Dynamisk sidnumrering i Interactive Communication Editor

>[!NOTE]
>
> Funktionen för interaktiv kommunikation ingår i programmet för tidig anmälan. Skicka ett e-postmeddelande från din arbetsadress till `aem-forms-ea@adobe.com` för att begära åtkomst.

## Introduktion

Med funktionen Dynamic Page Numbering i Interactive Communication (IC) kan man automatiskt visa sidnummer i PDF-utdata. Sidnumrering kan aktiveras på mallsidenivå, vilket ger en konsekvent numrering över alla associerade designsidor. Detta gör det lättare att hålla ordning på sidorna och ha en professionell layout i flersidig kommunikation.

![Sök efter IC-dokument](/help/forms/interactive-communication/assets/dynamic-page.png)

## Använda dynamisk sidnumrering i den interaktiva kommunikationsredigeraren

1. Öppna Interactive Communication Editor
Öppna Interactive Communication-projektet i IC Editor.

1. Gå till mallsida
Sidnumrering kan bara aktiveras på mallsidan. Navigera till huvudsidan i kommunikationen.

1. Aktivera sidnumrering
Aktivera alternativet Aktivera sidnummer i panelen Egenskaper. Då läggs sidnummer automatiskt till på alla associerade sidor.

1. Anpassa placering
Komponenten Sidnummer kan placeras var som helst på arbetsytan efter att ha släppts och anpassats fritt med hjälp av standardegenskaper för text.

1. Förhandsgranska i PDF
Sidnummer visas endast vid förhandsvisning av PDF och dynamisk numrering visas på alla sidor.

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

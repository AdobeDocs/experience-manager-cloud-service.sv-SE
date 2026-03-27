---
title: Associera gränssnittet i interaktiv kommunikationsredigerare
description: Upptäck associerat användargränssnitt i Interactive Communication Editor genom att möjliggöra för kundfokuserade agenter att generera skräddarsydd, kompatibel kommunikation.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
badgeSaas: label="AEM Forms" type="Positive" tooltip="Gäller AEM Forms)."
exl-id: 9ba58659-b14c-4ebc-a6d9-e56a4b6aa48b
source-git-commit: f889498f9ee5e71a4d3695dbfbe194d1bbb11488
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 0%

---

# Associera gränssnittet i interaktiv kommunikationsredigerare

>[!NOTE]
>
> Funktionen för interaktiv kommunikation ingår i programmet för tidig anmälan. Skicka ett e-postmeddelande från din arbetsadress till `aem-forms-ea@adobe.com` för att begära åtkomst.

**Associate-gränssnittet** är ett specialiserat, förenklat gränssnitt som är byggt på Interactive Communications-redigeraren (IC). Det är utformat för kundfokuserade proffs, som fältassistenter och serviceagenter, som vill generera skräddarsydd, korrekt och korrekt kommunikation i realtid under live-interaktioner.

![Sök efter IC-dokument](/help/forms/interactive-communication/assets/associate-ui-preview.png)

## Associera gränssnittsgränssnitt

Associate-gränssnittet har en ren arbetsyta med två paneler som möjliggör snabb och säker kommunikationsgenerering:

### Vänster panel: Datainmatning

- Associaterna anger eller bekräftar kundspecifik information.
- Valideringar, hjälptexter och obligatoriska fält ger korrekta indata.

### Högerpanel: Förhandsvisning i realtid

- Visar en direktförhandsvisning av det slutliga dokumentet.
- Uppdateras automatiskt när associationen fyller i data.

### Omedelbar dokumentgenerering

- Generera eller ladda ned den färdiga kommunikationen.

## Användarens personlighet och ansvar

Det tillhörande användargränssnittet styrs av tre huvudroller, var och en med olika ansvarsområden:

### &#x200B;1. Administratör

Ansvarig för systemkonfiguration, styrning, serverdelsintegrering och användaråtkomst.

| Ansvarsområde | Fokus |
|---------------|-------|
| Systemkonfiguration | Ställer in kärninfrastruktur, användargrupper, FDM (Form Data Models), utdata. |
| Styrning och säkerhet | Hanterar användarbehörigheter och ser till att systemet följs. |
| Integrationshantering | Underhåller serverdelsintegreringar och live-kunddataanslutningar. |

### &#x200B;2. Upphovsman

Utformar och hanterar interaktiv kommunikation och konfigurerar den för användargränssnittet (inklusive aktivering av Associate View och valfritt arbetsflöde).

| Ansvarsområde | Fokus |
|---------------|-------|
| Konc.int. redigering och design | Skapar layout, varumärke och en dokumentstruktur som följer standarderna. |
| Fältkonfiguration | Mappar datafält, definierar redigerbara, obligatoriska och skrivskyddade fält. |
| Publicering och aktivering | Publicerar konc.int. och delar länken för associerad åtkomst. |

### &#x200B;3. Associera

Associate-gränssnittet används för att hjälpa kunder, uppdatera information och generera kompatibel kommunikation.


| Ansvarsområde | Fokus |
|---------------|-------|
| Databekräftelse | Fyller i eller validerar kunddata via den vänstra panelen. |
| Förhandsgranska och validera | Säkerställer exaktheten med förhandsgranskningspanelen i realtid. |
| Leverans | Skapar PDF/e-postmeddelandet och skickar det via godkända kanaler. |

>[!NOTE]
>
> Associaterna måste vara en del av gruppen **forms-associates**. För författare som även skickar från det associerade användargränssnittet på författarinstansen lägger du även till dem i **arbetsflödeanvändare**.

## Dynamiska användningsfall

Användargränssnittet i Associate har stöd för direkt, personaliserad dokumentgenerering som är avgörande för branscher med behov av realtidsservice.

| Bransch | Exempel på användningsfall |
|----------|-------------------|
| **Finansiella tjänster** | Generera lånebekräftelsebrev i realtid, sammanfattningar av riskprofiler, kontoframtagning. |
| **Försäkring** | Ta fram utkast till försäkringskort eller sammanställningar av ersättningsanspråk. |
| **Hälsovård** | Skapa sammanfattningar av patientbehandlingsplaner med beräknade löner och scheman. |
| **Offentlig sektor** | Generera polisverifieringsrapporter, kvitton från allmänheten, bekräftelsebrev och sammanfattningar av ärendeuppdateringar på plats. |
| **Offentlig sektor** | Skapa sammanfattningar av ansökningsstatus, servicegodkännandebrev och realtidskommunikation för anmälan av välfärdssystem. |

## Aktivera det associerade användargränssnittet

Författare aktiverar det associerade användargränssnittet och kan även konfigurera ett arbetsflöde för överföringar i **Interaktiva kommunikationsinställningar**:

1. **Aktivera associerad vy** — I **Associera egenskaper** markerar du **Aktivera redigering av associerad vy**, klickar sedan på **Använd ändringar** och sparar dokumentet.
2. **Konfigurera arbetsflöde (valfritt)** - I **Arbetsflöde** aktiverar du **Konfigurera arbetsflöde för uppdatering**, väljer en arbetsflödesmodell och anger en URL för slutförande och omdirigering om du vill.
3. **Konfigurera redigerbara fält** - Aktivera de fält som associerade kan redigera och ange valideringar.
4. **Publicera och dela** - Publicera IC-kortet och dela länken med associerade.

Stegvisa instruktioner med skärmbilder och överföring/arbetsflöde (författare på författare kontra associera vid publicering) finns i [Aktivera och konfigurera associerat gränssnitt för interaktiv kommunikation](/help/forms/interactive-communication/enable-configure-associate-ui.md). Mer information om hur du skapar ett arbetsflöde som genererar PDF från IC-överföringar finns i [Skicka arbetsflöde för Associate UI - IC Generate PDF Output](/help/forms/interactive-communication/submission-workflow-associate-ui-ic-pdf.md).

**Associate-gränssnittet** överbryggar klyftan mellan strukturerat innehåll och kundengagemang i realtid.\
Genom att kombinera intuitiv design, robust serverdelskonfiguration och strikta kompatibilitetskontroller kan organisationer leverera **snabb, korrekt och personaliserad kommunikation** i stor skala.

## Se även

- [Aktivera och konfigurera associerat gränssnitt för interaktiv kommunikation](/help/forms/interactive-communication/enable-configure-associate-ui.md)
- [Integrera associerat gränssnitt i ditt program](/help/forms/interactive-communication/invoke-associate-ui.md)
- [Inlämningsarbetsflöde för Associate UI - IC Generate PDF Output](/help/forms/interactive-communication/submission-workflow-associate-ui-ic-pdf.md)

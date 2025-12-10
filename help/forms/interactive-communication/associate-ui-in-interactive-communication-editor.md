---
title: Associera gränssnittet i interaktiv kommunikationsredigerare
description: Upptäck associerat användargränssnitt i Interactive Communication Editor genom att möjliggöra för kundfokuserade agenter att generera skräddarsydd, kompatibel kommunikation.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: 19270498fa60f860b31400ad40705ecd2f821cf8
workflow-type: tm+mt
source-wordcount: '594'
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

Utformar och hanterar interaktiv kommunikation med Associate UI. ß

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
> Associate måste vara en del av gruppen **forms-associates**.

## Dynamiska användningsfall

Användargränssnittet i Associate har stöd för direkt, personaliserad dokumentgenerering som är avgörande för branscher med behov av realtidsservice.

| Bransch | Exempel på användningsfall |
|----------|-------------------|
| **Finansiella tjänster** | Generera lånebekräftelsebrev i realtid, sammanfattningar av riskprofiler, kontoframtagning. |
| **Försäkring** | Ta fram utkast till försäkringskort eller sammanställningar av ersättningsanspråk. |
| **Hälsovård** | Skapa sammanfattningar av patientbehandlingsplaner med beräknade löner och scheman. |
| **Offentlig sektor** | Generera polisverifieringsrapporter, kvitton från allmänheten, bekräftelsebrev och sammanfattningar av ärendeuppdateringar på plats. |
| **Offentlig sektor** | Skapa sammanfattningar av ansökningsstatus, servicegodkännandebrev och realtidskommunikation för anmälan av välfärdssystem. |

## Aktivera det associerade gränssnittsarbetsflödet

Författaren kan följa stegen nedan för att konfigurera och publicera en interaktiv kommunikation (IC) för åtkomst till gränssnittet för Associate:

>[!NOTE]
>
> Komponenter som stöds för associationer: Datumfält, Numeriskt fält, Textfält.

### Skapa konc:n

Utforma och konfigurera interaktiv kommunikation för att säkerställa att varumärken, databindningar, efterlevnadsregler och integreringar är korrekt inställda.

### Aktivera det associerade användargränssnittet

Aktivera alternativet Associera användargränssnitt i det övre åtgärdsfältet för att göra det tillgängligt för associationsstyrda användare.

### Aktivera komponenten Associate UI

### Konfigurera redigerbara fält

Aktivera de fält som associerade kan redigera i avsnittet med obligatoriska fält.
Ställ in valideringar för att säkerställa korrekt och kontrollerad datainmatning.

### Publicera IC

När du är klar med alla konfigurationer publicerar du den interaktiva kommunikationen för säker åtkomst.

### Dela det publicerade konsolen med associerade

Ange den publicerade IC-länken till Associate så att de kan autentisera, ange kundspecifik information och generera den slutliga kommunikationen med giltiga indata.

**Associate-gränssnittet** överbryggar klyftan mellan strukturerat innehåll och kundengagemang i realtid.\
Genom att kombinera intuitiv design, robust serverdelskonfiguration och strikta kompatibilitetskontroller kan organisationer leverera **snabb, korrekt och personaliserad kommunikation** i stor skala.

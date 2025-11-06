---
title: Inlämning och integration av blanketter
description: Lär dig hur du konfigurerar inskickade formulär och integrerar Forms Experience Builder-formulär med externa system, API:er och arbetsflöden.
feature: Edge Delivery Services
hide: true
index: false
hidefromtoc: true
role: Admin, Developer
exl-id: c772556b-dab6-4fa8-b728-1fe52c6596a4
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '915'
ht-degree: 0%

---

# Inlämning och integration av blanketter

>[!NOTE]
>
> Forms Experience Builder är tillgängligt via ett program för tidig åtkomst. Kontrollera att du har begärt och beviljats åtkomst innan du börjar.

Forms Experience Builder har kraftfulla integreringsfunktioner för att koppla samman formulären med externa system, API:er och arbetsflöden. I den här guiden beskrivs hur du konfigurerar formulärinskickat material och ställer in olika integrationsscenarier.

## Konfigurationsalternativ för överföring

### E-postinskick

Konfigurera formulär att skicka inskickade via e-post:

**Grundläggande e-postkonfiguration:**

- Ange mottagarens e-postadresser
- Konfigurera e-postmallar
- Lägg till CC- och BCC-mottagare
- Konfigurera e-postmeddelanden

**Avancerade e-postfunktioner:**

- Dynamiskt mottagarval
- E-postmallar med formulärdata
- Hantering av bilagor
- Bekräftelse av e-postleverans

### REST API-integrering

Koppla formulär till externa API:er och tjänster:

**API-slutpunktskonfiguration:**

- Ange REST API-URL:er
- Konfigurera autentiseringsmetoder
- Ange begäranderubriker och parametrar
- Hantera svarsdata

**Datamappning:**

- Mappa formulärfält till API-parametrar
- Omforma dataformat
- Hantera kapslade JSON-strukturer
- Hantera felsvar

### Integrering av molnlagring

Lagra formulärinskick i molnlagringstjänster:

**Plattformar som stöds:**

- Microsoft Azure Blob Storage
- Amazon S3
- Google Cloud-lagring
- SharePoint Online

**Konfigurationsalternativ:**

- Ange autentiseringsuppgifter för lagring
- Konfigurera mappstrukturer
- Ange namnkonventioner för filer
- Hantera åtkomstbehörigheter

### Integrering av arbetsflöden

Koppla ihop blanketter med affärsprocesserna:

**Microsoft Power Automate:**

- Starta arbetsflöden när formulär skickas
- Skicka formulärdata till arbetsflödessteg
- Hantera arbetsflödessvar
- Hantera godkännandeprocesser

**Adobe-arbetsflöde:**

- Integrera med AEM Workflow
- Ställ in godkännandekedjor
- Konfigurera meddelandesteg
- Hantera dokumentbearbetning

## Ställa in formulärinskickat material

### Steg 1: Konfiguration av åtkomstöverföring

1. Öppna formuläret i Forms Experience Builder
2. Navigera till sändningsinställningarna
3. Välj Konfigurera formuläröverföring
4. Välj integrationstyp

### Steg 2: Konfigurera e-postinskick

**Grundläggande e-postkonfiguration:**

    Konfigurera e-postöverföring till hr@company.com med:
    - Ämne: &quot;New Employee Application&quot;
    - Include form data in email body
     - Send confirmation to sökande

**Avancerad e-postkonfiguration:**

    Konfigurera dynamisk e-postroutning:
    - Om avdelningen är lika med&quot;IT&quot; skickar du till it-hr@company.com
    - Om avdelningen är lika med&quot;Försäljning&quot; skickar du till sales-hr@company.com
    - Standard är hr@company.com

### Steg 3: Konfigurera API-integrering

**REST API-konfiguration:**

    Skicka formulärdata till REST-slutpunkt:
    - URL: https://api.company.com/forms/submit
    - Metod: POST
    - Autentisering: Bearer-token
    - Innehållstyp: application/json

**Exempel på datamappning:**

    Mappa formulärfält till API:
    - firstName -> user.first_name
    - lastName -> user.last_name
    - email -> user.email_address
    - Department -> user.Department_id

### Steg 4: Konfigurera molnlagring

**Azure Blob Storage-konfiguration:**

    Lagra formulärinskickade formulär i Azure:
    - Behållare: form-sending
    - Mapp: /{year}/{month}/{day}/
    - Filformat: JSON med bilagor
    - Åtkomstnivå: Privat

## Exempel på integrering

### Formulär för kundfeedback

**Sändningskonfiguration:**

- E-postmeddelande till supportteamet
- Lagra data i CRM-system via API
- Skapa supportanmälan automatiskt
- Skicka bekräftelsemeddelande via e-post till kunden

**Implementering:**
Skicka feedback till:
1. E-post <support@company.com> med formulärinformation
2. POST till CRM API för att skapa kundpost
3. Starta arbetsflödet för att skapa supportbiljetter
4. Skicka ett e-postmeddelande till kunden

### Anställningsblankett

**Sändningskonfiguration:**

- Skicka e-post till HR-teamet med information om nyanställd
- Lagra dokument i SharePoint
- Arbetsflöde för att starta introduktioner
- Skapa användarkonton i olika system

**Implementering:**
Bearbeta anställdas introduktion:
1. E-post <hr@company.com> med information om medarbetare
2. Överför dokument till SharePoint personalmapp
3. Starta introduktionsarbetsflödet i Power Automate
4. Skapa konton i HR-system, e-post och andra verktyg

### Formulär för leadgenerering

**Sändningskonfiguration:**

- Lagra ledande data på automatiserad marknadsföring
- Skicka meddelande till säljarna
- Lägg till lead i CRM-system
- Utlös e-postsekvens för uppföljning

**Implementering:**
Framtagning av leads:
1. POST-lead-data till Marketo API
2. Skapa lead-post i Salesforce
3. E-postsäljare med information om lead
4. Starta automatiserad e-postplantningssekvens

## Avancerade integreringsscenarier

### Formulärhantering i flera steg

**Komplex arbetsflödesintegrering:**

- Validera formulärdata mot externa system
- Bearbeta betalningar via betalningslösningar
- Generera dokument och kontrakt
- Skicka meddelanden till olika intressenter

### Dataverifiering i realtid

**API-baserad validering:**

- Validera e-postadresser mot företagskatalogen
- Kontrollera produkttillgänglighet i lagersystem
- Verifiera kundinformation i CRM
- Validera betalningsinformation

### Villkorlig routning av inskickning

**Dynamisk routning baserad på formulärdata:**

- Dirigera till olika avdelningar baserat på frågetyp
- Skicka till olika system baserat på kundnivå
- Bearbeta på ett annat sätt baserat på status för slutförande av formulär
- Hantera olika affärsregler per region

## Säkerhet och efterlevnad

### Dataskydd

**Kryptering och säkerhet:**

- Kryptera känsliga data under överföring
- Säkra API-autentiseringsuppgifter och token
- Implementera korrekta åtkomstkontroller
- Följ principer för datalagring

### Krav för efterlevnad

**GDPR och sekretess:**

- Genomför samtyckeshantering
- Möjlighet att exportera data
- Aktivera begäranden om dataradering
- Underhåll granskningsspår

**Branschstandarder:**

- HIPAA-regelefterlevnad för hälso- och sjukvårdsformulär
- PCI DSS för betalningshantering
- SOX-kompatibilitet för finansiella blanketter
- Branschspecifika regler

## Testning och validering

### Inlämningstestning

**Testscenarier:**

- Verifiera e-postleverans och formatering
- Testa API-anslutning och datamappning
- Verifiera överföringar av molnlagring
- Kontrollera arbetsflödets utlösarfunktion

**Felhantering:**

- Testa scenarier för nätverksfel
- Validera felmeddelandevisning
- Kontrollera återförsöksmekanismer
- Verifiera reservalternativ

### Prestandaoptimering

**Optimeringsstrategier:**

- Implementera asynkron bearbetning
- Använd gruppåtgärder för massdata
- Optimera API-anropsfrekvens
- Cachelagra data som används ofta

## Felsöka integreringsproblem

### Vanliga problem

**Problem med e-postleverans:**

- Kontrollera SMTP-serverkonfiguration
- Verifiera mottagarnas e-postadresser
- Granska inställningar för skräppostfilter
- Testa e-postmallens formatering

**API-integreringsproblem:**

- Verifiera URL:er för API-slutpunkt
- Kontrollera autentiseringsuppgifter
- Validera begärandeformat och rubriker
- Granska API-svarshantering

**Problem med lagringsintegrering:**

- Bekräfta inloggningsuppgifter för lagring
- Kontrollera mappbehörigheter
- Verifiera filöverföringsgränser
- Testa nätverksanslutningen

### Få hjälp

För integreringsfrågor:

- Kontrollera [Vanliga frågor om Forms Experience Builder](forms-experience-builder-frequently-asked-questions.md)
- Granska guiden [Komma igång](forms-experience-builder-getting-started.md)
- Kontakta systemadministratören för teknisk hjälp
- API-dokumentation för externa tjänster

## Relaterade artiklar

- [Forms Experience Builder - översikt](product-overview.md)
- [Komma igång med Forms Experience Builder](forms-experience-builder-getting-started.md)
- [Installera och konfigurera Forms Experience Builder](deploy-forms-experience-builder.md)
- [Intelligent import och konvertering](intelligent-import-conversion.md)
- [Frågor och svar](forms-experience-builder-frequently-asked-questions.md)

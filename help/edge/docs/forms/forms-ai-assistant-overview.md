---
title: Forms Experience Builder
description: Introduktion till Forms Experience Builder
feature: Edge Delivery Services
hide: true
index: false
hidefromtoc: true
role: Admin, Architect, Developer
source-git-commit: ce61bc434614e5d7b92de3f1290e7e15325d27b7
workflow-type: tm+mt
source-wordcount: '937'
ht-degree: 0%

---


# Introduktion till Forms Experience Builder

>[!IMPORTANT]
>
> **Dokumentation som kan ändras**: Dokumentationen testas för närvarande mot produkten och kan uppdateras och revideras. Funktioner, kommandon och exempel kan ändras allt eftersom Forms Experience Builder fortsätter att utvecklas under det program som antogs tidigt.

AEM Forms Experience Builder utnyttjar kraften i generativ AI för att demokratisera och snabba upp skapandet och uppdateringen av digitala formulärupplevelser. Genom att möjliggöra intent-baserade arbetsflöden som bygger på naturliga språkinteraktioner kan användarna smidigt utforma, ändra och optimera formulär snabbt och enkelt.

Forms Experience Builder bygger på modern webbteknik och bygger på avancerade AI-tjänster, vilket gör det möjligt för både tekniska och icke-tekniska användare att skapa avancerade, proffsiga formulär genom konversationsgränssnitt. Denna revolutionerande metod minskar time to value från dagar till timmar, eliminerar tekniska hinder genom gränssnittets enkelhet och anpassar moderniseringen i hela ekosystemet.

## Kärnfunktioner

Forms Experience Builder har två arbetsflöden för att skapa kraftfulla digitala formulär:

### &#x200B;1. Skapa AI-baserade formulär

**Formulärgenerering för naturligt språk**

Skapa kompletta formulär från grunden med enkla engelska beskrivningar. Beskriv helt enkelt dina krav, till exempel&quot;Skapa ett formulär för kundfeedback med klassificeringsskalor och kommentarsfält&quot;, så genererar Forms Experience Builder rätt formulärstruktur. Du använder funktionen som bygger upp visuella redigeringsprogram för att lägga till fler fält, valideringsregler och inskickningslogik.

**Dynamisk fälthantering**

Lägg till, ändra eller ta bort formulärfält med konversationskommandon. AI förstår sitt sammanhang och kan på ett intelligent sätt föreslå fälttyper, valideringsregler och förbättringar av användargränssnittet baserat på dina behov.

**Layoutoptimering**

Uppdatera formulärlayouter och konfigurationer på ett naturligt språk. Begär ändringar som&quot;Ändra formulärlayout till guidelayout&quot; och Forms Experience Builder använder lämpliga format- och layoutjusteringar.

**Konfiguration av omfattande överföringsåtgärd**

Konfigurera inskickade formulär så att de kan integreras med era befintliga affärssystem:

- **E-postintegrering**: Konfigurera automatiska e-postmeddelanden och bekräftelser
- **REST API-slutpunkter**: Anslut till anpassade program och tjänster
- **Molnlagring**: Integrera med Azure Blob Storage, SharePoint och OneDrive
- **Automatisering av arbetsflöden**: Anslut till Power Automate och Workfront Fusion
- **Marknadsplattformar**: Direktintegrering med Marketo för lead-hantering
- **AEM-arbetsflöden**: Utnyttja befintliga arbetsflödesfunktioner i AEM

### &#x200B;2. Intelligent import och konvertering

**Importformat som stöds**

Omvandla befintliga formulär och dokument till interaktiva digitala upplevelser. Forms Experience Builder har stöd för:

- **Acrobat**: Interaktiv PDF forms med befintliga fältstrukturer
- **XFA PDF-filer**: Komplexa XML-baserade formulärarkitekturer
- **Platt PDF-fil**: Statiska dokument konverterade till interaktiva formulär
- **Bilder och skärmbilder**: JPG, PNG-format (kontrollera med team om du har storleksbegränsningar)
- **Handritade Forms**: Skisser och fotografier av pappersformulär

**Intelligent konverteringsprocess**

Det överförda innehållet analyseras till:

- Identifiera fälttyper och relationer
- Bevara layouten i största möjliga utsträckning
- Förbättra med modern responsiv design
- Lägg in avancerad validering och villkorlig logik
- Optimera för tillgänglighet och mobilupplevelse

## Så här fungerar det

Forms Experience Builder har en enkel konverteringsmetod:

    ┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
    │ 1. Beskriv    │───▶│ 2. AI skapar │───▶│ 3. Förfina &amp;    │
    │ Ditt formulär      │    │ Inledande formulär   │    │ Konfigurera      │
    │ Krav   │    │                 │    │                 │
    └─────────────────┘    └─────────────────┘    └─────────────────┘
    │                       │                       │
    │                       │                       │
    ▼                       ▼                       ▼
    ┌───────────────────────────────────────────────────────────────────────────┐
    │&quot;Skapa en låneblankett&quot; → Formulär med relevant                  │
    │ &quot;Lägg till e-postfält&quot;           → fält och grundläggande                          │
    │ &quot;Ange värdet för e-postfältet som har arkiverats till @firstname@gmail.com&quot; → verifieringsregler   │
    └───────────────────────────────────────────────────────────────────────────┘

## Exempelscenarier

<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Transform PDF Forms to Digital Forms">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">Omvandla PDF forms till Digital Forms</p>
                    <p class="is-size-6">Konvertera Acroforms, XFA PDF:er eller platta PDF-dokument till interaktiva digitala formulär med utökad funktionalitet.</p>
                </div>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Modernize Legacy XFA Forms">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">Modernize Legacy XFA Forms</p>
                    <p class="is-size-6">Förvandla komplexa XFA-applikationer till moderna, tillgängliga digitala upplevelser med förbättrade arbetsflöden.</p>
                </div>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Convert Screenshots to Digital Forms">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">Konvertera skärmbilder till Digital Forms</p>
                    <p class="is-size-6">Omvandla bilder, skärmbilder eller handritade formulär till fullt fungerande digitala upplevelser.</p>
                </div>
            </div>
        </div>
    </div>
</div>

<!-- #### Import and Enhance Web Forms

Import existing HTML forms and enhance them with advanced features while preserving existing functionality.

**Key benefits:**

- Advanced validation and business logic
- Conditional field behaviors
- Multi-channel submission options
- Enhanced user experience design -->

## Forms Experience Builder jämfört med traditionell utveckling

| Proportioner | Traditionell blankettgenerering | Forms Experience Builder |
|--------|---------------------------|----------------------|
| **Dags att skapa** | 2-3 dagar | 2-3 timmar |
| **Teknisk kunskap** | Obligatoriskt | Krävs inte |
| **Verifieringsregler** | Manuell kodning | Naturligt språk |
| **Tillgänglighet** | Manuell implementering | Inbyggd efterlevnad |


## Fördelar för organisationer

<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Democratized Form Creation">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">Demokratiserad blankettgenerering</p>
                    <p class="is-size-6">Ge icke-tekniska användare möjlighet att skapa avancerade blanketter utan programmeringskunskaper genom naturliga språkkonversationer.</p>
                </div>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Reduced Time to Value (TTV)">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">Reducerad tid till värde (TTV)</p>
                    <p class="is-size-6">Snabba upp formulärutvecklingen från dagar till timmar och möjliggör snabbare time-to-market för digitala initiativ.</p>
                </div>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Interface Simplicity">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">Gränssnittets tydlighet</p>
                    <p class="is-size-6">Eliminera inlärningskurvan med ett intuitivt konversationsgränssnitt, minska utbildningstiden och öka acceptansen.</p>
                </div>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Scaling Modernization Efforts">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">Moderniseringsåtgärder för skalförändring</p>
                    <p class="is-size-6">Modernisera befintliga formulärportföljer effektivt, bevara logiska funktioner och förbättra användarupplevelsen i hela formulärets ekosystem.</p>
                </div>
            </div>
        </div>
    </div>
</div>

## Onboarding

Forms Experience Builder är för närvarande tillgängligt som en del av programmet för tidig åtkomst (EA). Du behöver följande information för att kunna delta och få åtkomst:

### Nödvändig information

- **IMS-organisations-ID**: Din Adobe-organisationsidentifierare
- **Program-ID**: Ditt specifika program-ID i Adobe Experience Cloud
- **Projektinformation**: Tidslinje, omfång och användningsfall
- **E-post för officiellt arbete**: Associerad med din organisations Adobe-konto

### Så här skaffar du IMS-organisations-ID och program-ID

Detaljerade steg för att hitta ditt IMS-organisations-ID och program-ID finns i:

- [Adobe Experience Cloud guide för organisationskonfiguration](/help/onboarding/cloud-manager-introduction.md)
- [Program- och miljöhantering](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)

### Begär åtkomst

1. Samla ditt IMS-organisations-ID och program-ID med hjälp av guiderna ovan
2. Skicka ett e-postmeddelande till [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) och begära åtkomst
3. Inkludera i din begäran:
   - Organisationsnamn och IMS-organisations-ID
   - Program-ID
   - Projektets tidslinje och omfattning
   - Planerade användningsfall och verksamhetsmål

>[!IMPORTANT]
>
> **Begränsat tillgänglighetsprogram**: Åtkomst till Forms Experience Builder måste godkännas av interna intressenter. Adobe kommer att granska din begäran baserat på programkapacitet och anpassning till kriterier för tidig åtkomst. Godkännandet är inte garanterat och beror på den aktuella programtillgängligheten.

Mer information om programmet för tidig åtkomst och dess funktioner finns i [dokumentationen för AEM Forms tidig åtkomst](/help/forms/early-access-ea-features.md).

## Komma igång

Gå till [Forms Experience Builder-dokumentationen](forms-ai-assistant-getting-started.md) om du vill komma igång med Forms Experience Builder. Du kan öppna Forms Experience Builder via AEM Forms Editor eller Universal Editor, beroende på vilket arbetsflöde du föredrar.

Forms Experience Builder är en kraftfull och intuitiv lösning som kombinerar flexibiliteten i konversationsbaserad AI med tillförlitligheten i blanketthanteringen i enterpriseklass.

---
title: Adaptiva Forms Core-komponenter jämfört med Edge Delivery Services Forms jämfört med Foundation-komponenter
description: Teknisk jämförelse av AEM Forms utvecklingsstrategier - kärnkomponenter, Edge Delivery Services Forms och Foundation Components. Arkitektur, återgivning, funktioner och användningsfall.
keywords: adaptiv formulärjämförelse, kärnkomponenter, grundkomponenter, tjänster för kantleverans, AEM formulärjämförelse, formulärbyggarjämförelse
role: Architect, Developer, Admin
level: Intermediate
feature: Adaptive Forms, Core Components, Edge Delivery Services
exl-id: adaptive-forms-comparison
source-git-commit: 37799555babb15809409ec5cda8a1c46ceff24f2
workflow-type: tm+mt
source-wordcount: '1953'
ht-degree: 0%

---


# Adaptiv Forms: Kärnkomponenter jämfört med Edge Delivery Services Forms jämfört med Foundation-komponenter

Adobe Experience Manager (AEM) Forms erbjuder tre olika sätt att bygga datainhämtningsupplevelser: Adaptiv Forms baserad på kärnkomponenter, Edge Delivery Services Forms och Adaptiv Forms baserad på grundkomponenter. Varje tillvägagångssätt har olika arkitektur, återgivningsmodell och målanvändning. Den här artikeln innehåller en teknisk jämförelse som hjälper systemarkitekter, utvecklare och AEM-kunder att välja rätt metod för sina behov.

## Ökning

Alla tre formulärtyperna har till syfte att samla in användardata och integrera med backend-system. De skiljer sig dock åt när det gäller den underliggande arkitekturen, var formulären återges, hur de levereras och vilka funktioner de stöder.

| Metod | Status | Primär användning |
|----------|--------|------------------|
| **Kärnkomponenter** | Rekommenderas för nya formulär | Moderna, skalbara blanketter som kräver AEM |
| **Edge Delivery Services Forms** | Rekommenderas för prestandakrävande platser | Blanketter med höga prestanda som levereras från grunden med snabb driftsättning |
| **Foundation Components** | Underhållsläge | Befintliga formulär som kräver stöd för äldre funktioner |

## Adaptiv Forms baserad på kärnkomponenter

### Definition

Adaptiva Forms Core-komponenter är en uppsättning med 30 BEM-kompatibla komponenter med öppen källkod som bygger på Adobe Experience Manager WCM Core-komponenter. De representerar Adobe rekommenderade metod för att skapa nya Adaptiva Forms, med modern arkitektur, förbättrade prestanda och automatisk generering av headless-formulär.

### Arkitektur

Core Components använder en standardiserad, modulär komponentarkitektur:

- **Komponentgrund**: Skapad med AEM WCM Core Components
- **Formateringsmetod**: CSS-konventioner för BEM (Blockelementsmodifierare)
- **Innehållslagring**: JCR-databas med strukturerade innehållsnoder
- **Återgivning**: Återgivning på serversidan i AEM med huvudlös återgivning på klientsidan (tillval)
- **Source**: Öppen källkod (tillgänglig på [GitHub](https://github.com/adobe/aem-core-forms-components))

### Återgivningsmodell

Core Components har stöd för flera renderingsmodeller:

1. **SSR (Server-Side Rendering)**: Forms renderar på AEM-servern och levererar fullständiga HTML till webbläsaren
2. **Headless Rendering**: Forms visar JSON-representationer via API:er för klientåtergivning i React, Angular eller andra ramverk
3. **Hybrid Rendering**: En kombination av server- och klientåtergivning för optimala prestanda

### Publiceringsalternativ

- AEM Publish-instanser
- Edge Delivery Services (vid konfigurering)
- Headless-API:er för anpassade klientprogram

### Viktiga funktioner

| Kategori | Funktioner |
|----------|-------------|
| **Komponenter** | 30 standardiserade komponenter inklusive textruta, Numerisk ruta, Datumväljare, Nedrullningsbar meny, Kryssrutegrupp, Alternativknapp, Bifogad fil, Guide, Dragspelspanel, Vågräta/Lodräta flikar |
| **Formulärmodeller** | JSON Schema (v4 och 2020-12), formulärdatamodell (FDM), XDP/XFA-mallar (begränsat) |
| **Regelmotor** | Visuell regelredigerare med villkorslogik, validering, tjänsteanrop, anpassade funktioner |
| **Skicka åtgärder** | REST endpoint, Email, AEM Workflow, SharePoint, OneDrive, Azure Blob Storage, Power Automate, Workfront Fusion, Form Data Model |
| **Förifyll** | Förfyllnadstjänst för formulärdatamodell, anpassade förifyllningstjänster |
| **CAPTCHA** | reCAPTCHA, hCaptcha, Turnstile |
| **Postdokument** | PDF-generering med anpassade mallar eller OTB-mallar |
| **Tillgänglighet** | WCAG-kompatibel, ARIA-etiketter, tangentbordsnavigering, skärmläsarstöd |
| **Lokalisering** | Flerspråksstöd via AEM arbetsflöde för översättning |
| **Versionshantering** | Innehållsversionshantering ärvd från AEM Sites |

### Förutsättningar

- **AEM Forms as a Cloud Service**: Kärnkomponenter är aktiverade som standard
- **AEM 6.5 Forms**: Kräver aktivering via AEM Archetype
- **Användarbehörigheter**: Användaren måste vara i gruppen `forms-users`
- **Mall**: En mall för adaptiv form (kärnkomponent) krävs
- **Tema**: Arbetsytans tema (OTB) eller anpassat tema

### Begränsningar

- **JSON-schemabegränsningar**: Null-typ, unionstyper (alla), OneOf/AnyOf/AllOf/NOT-konstruktioner stöds inte
- **Komponentmellanrum**: Adobe Sign-block, Klottsignatur, Diagram, Bildval är inte tillgängligt (tillgängligt i Foundation-komponenter)
- **Anpassade funktioner**: Generatorfunktioner, asynk/await, klassmetoder som inte stöds
- **Digitala signaturer**: Inte tillgängligt internt (till skillnad från Foundation Components)

### När ska användas

**Rekommenderas för:**

- Nya formulärutvecklingsprojekt
- Organisationer som behöver modern, underhållningsbar arkitektur
- Projekt som kräver flexibel publicering (AEM + Edge Delivery + Headless)
- Anpassade klientapplikationer (React, Angular) via headless API:er
- Projekt som prioriterar prestanda och tillgänglighet
- Krav för flerkanalsleverans (webb, mobil, kioskdator)

**Rekommenderas inte för:**

- Forms som kräver Adobe Sign-integrering (använd Foundation Components)
- Enkla formulär där Edge Delivery Services prestanda är avgörande
- Befintliga grundläggande komponentbaserade formulär (behåll dem i grunden om de inte migreras)

## Edge Delivery Services Forms

### Definition

Edge Delivery Services (EDS) Forms är en sammansättningsbar uppsättning tjänster för att skapa och leverera formulär via Adobe Experience Manager Edge Delivery Services. De möjliggör snabb blankettutveckling med enastående prestanda tack vare edge-baserad leverans, rendering på klientsidan och flera redigeringsmetoder.

### Arkitektur

EDS Forms använder en fristående, edge-first-arkitektur:

- **Innehållskällor**: Microsoft SharePoint, Google Drive (dokumentbaserad) eller Universal Editor (WYSIWYG)
- **Koddatabas**: GitHub
- **Innehållsleverans**: Edge Delivery Services CDN
- **Återgivning**: Återgivning på klientsidan med vanilj-JavaScript
- **Formulärblock**: Adaptivt Forms-block bearbetar formulärdefinitioner och genererar HTML

### Återgivningsmodell

EDS Forms använder endast klientåtergivning:

1. Formulärdefinition lagrad som JSON (konverterad från kalkylblad eller skapad i Universal Editor)
2. JSON har hämtats från kanten: `https://<branch>--<repo>--<owner>.aem.live/<form>.json`
3. Adaptiv Forms Block JavaScript - JSON-processer
4. HTML-struktur som genereras dynamiskt i webbläsaren
5. CSS används för formatering

**HTML-strukturmönster:**

```html
<div class="{Type}-wrapper field-{Name} field-wrapper" data-required="{Required}">
   <label for="{FieldId}" class="field-label">Label</label>
   <input type="{Type}" id="{FieldId}" name="{Name}">
   <div class="field-description" id="{FieldId}-description">Help text</div>
</div>
```

### Redigeringsmetoder

EDS Forms har stöd för två metoder:

#### Universal Editor (WYSIWYG)

- Visual drag-and-drop interface
- Förhandsgranska i realtid med enhetssimulering
- Avancerad regelredigerare för villkorlig logik
- Integrering av formulärdatamodell (FDM)
- Integrering med AEM Workflows
- Stöd för anpassade komponenter
- Skapa mallar

#### Dokumentbaserad redigering

- Skapa Microsoft Excel- och Google-blad
- Kalkylbladsbaserad formulärdefinition
- Direkt publicering (ändringarna återspeglar omedelbart)
- Passar för enkla till måttliga komplexa formulär

### Sändningsalternativ

**Forms Submission Service (FSS):**

- Skicka till Google Sheets
- Skicka till Microsoft Excel (OneDrive/SharePoint)
- E-postaviseringar

**AEM Publicera överföringsåtgärder:**

- REST-slutpunkt
- AEM posttjänster
- Formulärdatamodell
- AEM Workflow
- SharePoint/OneDrive
- Azure Blob Storage
- Microsoft Power Automate
- Adobe Workfront Fusion
- Adobe Marketo Engage

### Viktiga funktioner

| Kategori | Funktioner |
|----------|-------------|
| **Komponenter** | Alla indatatyper för HTML5, kryssrutegrupper, alternativknappar, listrutor, paneler, upprepningsbara avsnitt, bifogad fil, dragspel, guide, modul |
| **Validering** | Validering på fältnivå (obligatoriskt, min/max, mönster), anpassade valideringsmeddelanden |
| **Regler** | Villkorlig synlighet, värdeuttryck, händelsestyrda regler |
| **Integrationer** | Adobe Sign, Salesforce, Microsoft Dynamics, A/B-testning |
| **Säkerhet** | reCAPTCHA Enterprise, hCaptcha, CORS-konfiguration |
| **Analyser** | Adobe Experience Platform Web SDK, formulärvyer och spårning av inskickat material |

### Förutsättningar

**För dokumentbaserad redigering:**

- GitHub-konto
- Google Drive- eller Microsoft SharePoint-konto
- Nod/npm för lokal utveckling
- AEM-projekt med Adaptive Forms Block konfigurerat
- Dela mapp med `forms@adobe.com` (redigera behörigheter)

**För Universal Editor:**

- AEM Forms as a Cloud Service - instans
- Edge Delivery Services-projektet är konfigurerat
- Nödvändiga behörigheter för måldestinationer

**För AEM Publish Submission:**

- Instansens URL för AEM Cloud-tjänsten har konfigurerats
- Konfigurering av filtret för OSGi-refereraren
- CORS-konfiguration för Edge Delivery webbplatsdomäner

### Begränsningar

**Dokumentbaserad redigering:**

- Namngivning av blad begränsat till `helix-default` och `shared-aem`
- Passar bäst för formulär med låg komplexitet
- Begränsade regelfunktioner
- Inga AEM-arbetsflöden (utan AEM Publish)
- Ingen integrering av formulärdatamodell

**Universell redigerare:**

- Statisk/dynamisk import stöds inte i anpassade funktioner
- Formulärfragment kan bara redigeras fristående
- Funktioner för inbäddning av formulär under utveckling

**Allmänt:**

- `shared-aem` ark får inte innehålla PII (offentligt tillgänglig)
- Kräver CORS-konfiguration för korsorigo överföringar
- OSGi Referrer-filter krävs för AEM Publish-överföringar

### När ska användas

**Rekommenderas för:**

- Prestandakrävande webbplatser som kräver hög ljusstyrka
- Webbplatser som redan använder Edge Delivery Services
- Snabb utveckling och driftsättning av blanketter
- Enkel till måttlig datainhämtning för komplexitet
- Team som föredrar att skapa kalkylblad (dokumentbaserad)
- Projekt som kräver snabb time-to-market

**Rekommenderas inte för:**

- Forms kräver omfattande serverbearbetning
- Djupgående integrering med äldre system som saknar REST API:er
- Krav för offlineformulär
- Organisationer som behöver specifika JavaScript-ramverk (React, Angular) med full kontroll

## Adaptiv Forms baserad på grundkomponenter

### Definition

Foundation Components är den klassiska AEM Forms-utvecklingsmetoden. De är de ursprungliga adaptiva Forms-komponenterna som har funnits i AEM Forms i många år. Även om det fortfarande finns stöd för det rekommenderar Adobe Foundation Components i första hand att man underhåller befintliga formulär i stället för att skapa nya.

### Arkitektur

Foundation Components använder traditionell AEM-arkitektur:

- **Innehållsmodell**: WCM `cq:Page`-komponent med JCR-innehållsstruktur
- **Rotstruktur**: `guideContainer` (rot) → `rootPanel` → `items` (formulärfält)
- **Återgivning**: Återgivning på serversidan med JavaScript på klientsidan
- **SOM-uttryck**: Skriptobjektmodell för referens till formulärobjekt

### Återgivningsmodell

Foundation Components använder serversidesrendering:

1. Formulärinnehåll som lagras i JCR-databasen
2. AEM serverprocesser blankettstruktur
3. Fullständigt HTML renderat och skickat till webbläsaren
4. JavaScript hanterar interaktivitet och validering på klientsidan

### Viktiga funktioner

| Kategori | Funktioner |
|----------|-------------|
| **Komponenter** | Över 40 komponenter inklusive alla kärnkomponentekvivalenter plus: Adobe Sign-block, diagram, klottunderskrift, bildval, sammanfattningssteg, bilagelista |
| **Formulärmodeller** | Formulärdatamodell (FDM), XDP/XFA-mallar, XML-schema (XSD), JSON-schema |
| **Regelmotor** | Visual editor + kodredigerare (för grupper med formgivare och avancerade användare) |
| **Digitala signaturer** | Integrering med Adobe Sign, klottersignatur |
| **Skicka åtgärder** | Flera OOTB-åtgärder som liknar kärnkomponenter |

### Komponenter som är exklusiva för grunden

Följande komponenter är **endast tillgängliga** i Foundation Components:

- Adobe Sign-block
- Diagram
- Lista över bifogade filer
- Fotnotsplatshållare
- Bildval
- Klottersignatur
- Sammanfattningssteg
- Turnstile Captcha

### Förutsättningar

- AEM Forms as a Cloud Service eller AEM 6.5 Forms
- Adaptiv formulärmall (Foundation)
- Användare i gruppen `forms-users`

### Begränsningar

- **Publicering**: Endast AEM (inga Edge Delivery Services eller Headless API:er)
- **Prestanda**: Standardprestanda (inte optimerat för Lighthuse-poäng)
- **Arkitektur**: Äldre arkitektur utan BEM-kompatibilitet
- **Öppna Source**: Inte öppen källkod
- **Framtida utveckling**: Underhållsläge; nya funktioner läggs främst till i kärnkomponenter

### När ska användas

**Rekommenderas för:**

- Underhåll befintliga grundformulär
- Forms som kräver integrering av Adobe Sign eller Scribble Signature
- Arbetsflöden som är beroende av etablerade grundfunktioner
- Projekt som endast kräver AEM
- Forms som kräver komponenter exklusivt från grunden (diagram, bildval)

**Rekommenderas inte för:**

- Ny formulärutveckling (använd kärnkomponenter)
- Projekt som kräver Edge Delivery Services
- Headless form APIs
- Prestandakrävande implementeringar
- Projekt som prioriterar framtidssäker arkitektur

## Jämförelsetabell

| Parameter | Kärnkomponenter | Edge Delivery Services Forms | Foundation Components |
|-----------|-----------------|-----------------------------|-----------------------|
| **Status** | Rekommenderas för nya formulär | Rekommenderas för webbplatser med höga prestanda | Underhållsläge |
| **Arkitektur** | Modulär, BEM-kompatibel | Edge först, fristående | Traditionell WCM |
| **Återgivning** | Server-side + Headless | Endast på klientsidan | Serversidan |
| **Publicerar** | AEM + Edge Delivery + Headless API:er | Endast Edge Delivery Services | Endast AEM |
| **Redigering** | AEM Forms Editor | Universell redigerare eller kalkylblad | AEM Forms Editor |
| **Prestanda** | Bra (förbättrat jämfört med Foundation) | Utmärkt (hög ljusstyrka) | Standard |
| **Komponentantal** | 30 | 20+ (alla HTML5-indatatyper) | 40+ |
| **Öppna Source** | Ja (GitHub) | Ja | Nej |
| **Formulärdatamodell** | ✅ | ✅ (endast Universal Editor) | ✅ |
| **JSON-schema** | ✅ | Begränsad | ✅ |
| **Stöd för XDP/XFA** | Begränsad | ❌ | ✅ |
| **XML-schema** | ❌ | ❌ | ✅ |
| **Regelmotor** | Avancerad visuell redigerare | Advanced (Universal Editor) / Limited (dokumentbaserad) | Avancerad visuell + kodredigerare |
| **Digitala signaturer** | ❌ | ❌ | ✅ |
| **Adobe Sign** | ❌ | Integrering via | ✅ (internt block) |
| **Postdokument** | ✅ | ✅ | ✅ |
| **CAPTCHA-alternativ** | reCAPTCHA, hCaptcha | reCAPTCHA Enterprise, Captcha | reCAPTCHA, hCaptcha, Turnstile |
| **AEM Workflow** | ✅ | ✅ (via AEM Publish) | ✅ |
| **Headless API:er** | ✅ (automatiskt) | ❌ | ❌ |
| **Tillgänglighet** | WCAG-kompatibel | WCAG-kompatibel | Grundläggande |
| **Distributionshastighet** | Pipeline-baserad | Direkt (spara live) | Pipeline-baserad |
| **Formatering** | BEM CSS, teman | CSS, teman på projektnivå | CSS, teman |
| **Versionshantering** | ✅ (ärvs från platser) | Git-baserad | ✅ |
| **Lokalisering** | AEM arbetsflöde för översättning | Manuellt/AEM Sites-arbetsflöde | AEM arbetsflöde för översättning |

## Beslutsmatris

| Krav | Rekommenderat tillvägagångssätt |
|-------------|---------------------|
| Utveckling av nya formulär | Kärnkomponenter |
| Underhåll befintliga formulär | Foundation Components (till migrering) |
| Prestandakrävande (hög ljusstyrka) | Edge Delivery Services Forms |
| Headless/single channel delivery | Kärnkomponenter |
| Integrering med Adobe Sign | Foundation Components |
| Skapa kalkylblad | Edge Delivery Services (dokumentbaserad) |
| Skapa visuellt i WYSIWYG med edge delivery | Edge Delivery Services (Universal Editor) |
| Komplexa företagsintegreringar | Kärnkomponenter eller grundkomponenter |
| Snabba prototyper | Edge Delivery Services (dokumentbaserad) |
| Stöd för XFA-/XDP-mallar | Foundation Components |
| Anpassad reaktion/Angular-förskjutning | Kärnkomponenter (Headless API:er) |

## Överväganden vid migrering

### Foundation-komponenter till Core-komponenter

- **Verktyg**: AEM Modernize Tools (Forms Conversion Utility)
- **Insats**: Medelhög till hög beroende på formulärets komplexitet
- **Överväganden**:
   - Reglerna kräver manuell återgivning
   - Foundgängliga komponenter (Adobe Sign-block, Klottsignatur, Diagram) tas bort under migreringen
   - Översättningsinställningar har inte överförts
   - Anpassade funktioner kräver omskrivning

### Traditionell till Edge Delivery Services

- **Metod**: Återskapa formulär med Universal Editor eller dokumentbaserad redigering
- **Insats**: Hög för komplexa formulär, låg för enkla formulär
- **Fördelar**: Betydande prestandaförbättring, modern utvecklingsupplevelse

## Dokumentationsmellanrum och tvetydigheter

Följande områden har ofullständig eller tvetydig dokumentation:

1. **Stöd för kärnkomponenter i XDP/XFA**: Dokumentationen anger &quot;begränsat&quot; stöd men anger inte exakta begränsningar
2. **Inbäddning av Edge Delivery Services-formulär**: Markerat som &quot;Kommer snart&quot; i dokumentationen, aktuell status är oklar
3. **Framtida grundkomponenter**: Ingen explicit tidslinje för borttagning; beskrivs som underhållsläge
4. **API-täckning utan rubrik**: Exakt funktionsparitet mellan serveråtergivna och headless-formulär har inte dokumenterats
5. **Prestandatester**: Specifika jämförelser mellan olika metoder saknas

## Relaterade resurser

- [Skapa en adaptiv form (kärnkomponenter)](/help/forms/creating-adaptive-form-core-components.md)
- [Skapa ett adaptivt formulär (grundkomponenter)](/help/forms/creating-adaptive-form.md)
- [Edge Delivery Services Forms - översikt](/help/edge/docs/forms/overview.md)
- [Universal Editor - komma igång](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md)
- [Dokumentbaserad redigering - självstudiekurs](/help/edge/docs/forms/tutorial.md)
- [Migreringsverktyg](/help/forms/migration-utility-tool-for-af-core-components.md)
- [AEM Forms Core-komponenter i GitHub](https://github.com/adobe/aem-core-forms-components)

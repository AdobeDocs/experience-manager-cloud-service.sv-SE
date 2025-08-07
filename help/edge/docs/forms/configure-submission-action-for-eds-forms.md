---
title: Konfigurera Skicka-åtgärder för AEM Forms med Edge Delivery Services
description: Lär dig hur du konfigurerar skicka-åtgärder i AEM Forms med Edge Delivery Services. Välj mellan Forms Submission Service och AEM Publish Submit Action för att hantera formulärdata på ett säkert och effektivt sätt.
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 8f490054-f7b6-40e6-baa3-3de59d0ad290
source-git-commit: 2e2a0bdb7604168f0e3eb1672af4c2bc9b12d652
workflow-type: tm+mt
source-wordcount: '855'
ht-degree: 0%

---

# Konfigurera Skicka-åtgärder för AEM Forms

Konfigurera hantering av blankettinlämning för att dirigera data till kalkylblad, e-post eller backend-system med AEM Forms med Edge Delivery Services.

## Snabbbeslutshandbok

Välj överföringsmetod:

| Metod | Bäst för | Konfigurera komplexitet | Användningsexempel |
|--------|----------|------------------|-----------|
| **Forms Submission Service** | Enkel datainhämtning | Låg | Kontaktformulär, enkäter, grundläggande datainsamling |
| **AEM Publish Submission** | Komplexa arbetsflöden | Hög | Företagsintegrering, anpassad bearbetning, arbetsflöden |

## Förutsättningar

Innan du konfigurerar skicka-åtgärder måste du se till att:

- AEM Forms as a Cloud Service - instans
- Edge Delivery Services-projektet är konfigurerat
- Formulär som skapats med Document Author eller Universal Editor
- Behörighet krävs för måldestinationer (kalkylblad, e-postsystem eller AEM)

+++ Metod 1: Forms Sändningstjänst

Forms Submission Service är en slutpunkt på Adobe som är perfekt för enkla datainhämtningsscenarier.

### Destinationer som stöds

- **Kalkylblad**: Google-blad, Microsoft Excel (OneDrive/SharePoint)
- **E-post**: Skicka formulärdata till angivna e-postadresser

### Konfigurationssteg

1. **Konfigurera målåtkomst**
   - För kalkylblad: Bevilja redigeringsbehörighet för `forms@adobe.com` i målkalkylblad
   - För e-post: Verifiera att mottagarnas e-postadresser är tillgängliga

2. **Konfigurera formuläröverföring**
   - Öppna formuläret i redigeringsmiljön
   - Ange skicka-åtgärd till&quot;Forms Submission Service&quot;
   - Ange kalkylblads-URL eller e-postadresser
   - Spara och publicera formuläret

3. **Testa överföring**
   - Skicka testdata via formuläret
   - Verifiera att data visas i målmålet
   - Kontrollera felloggar om överföringen misslyckas

### Viktiga anteckningar

- Tjänstkontot `forms@adobe.com` kräver redigeringsåtkomst till målkalkylblad
- E-postmeddelanden skickas omedelbart när formuläret skickas
- Dataverifiering sker på tjänstnivå

![Forms Submission Service Flow](/help/forms/assets/eds-fss.png)

+++

+++ Metod 2: AEM Publish Submit

Skicka formulärdata direkt till AEM as a Cloud Service Publish-instansen för komplex bearbetning.

### Använda AEM Publish

- Anpassade AEM-arbetsflöden krävs efter inskickning
- FDM-integration (Form Data Model) med databaser
- Tjänstintegreringar från tredje part (Marketo, Power Automate, Workfront Fusion)
- Azure Blob Storage eller SharePoint dokumentbibliotek
- Komplex validering eller bearbetningslogik på serversidan

### Tillgängliga överföringsåtgärder

- [Skicka till REST-slutpunkt](/help/forms/configure-submit-action-restpoint.md)
- [Skicka e-post via AEM e-posttjänster](/help/forms/configure-submit-action-send-email.md)
- [Skicka med formulärdatamodell](/help/forms/configure-data-sources.md)
- [Anropa AEM Workflow](/help/forms/aem-forms-workflow-step-reference.md)
- [Skicka till SharePoint](/help/forms/configure-submit-action-sharepoint.md)
- [Skicka till OneDrive](/help/forms/configure-submit-action-onedrive.md)
- [Skicka till Azure Blob Storage](/help/forms/configure-submit-action-azure-blob-storage.md)
- [Skicka till Microsoft Power Automate](/help/forms/forms-microsoft-power-automate-integration.md)
- [Skicka till Adobe Workfront Fusion](/help/forms/submit-adaptive-form-to-workfront-fusion.md)
- [Skicka till Adobe Marketo Engage](/help/forms/submit-adaptive-form-to-marketo-engage.md)

![AEM-publiceringsflöde](/help/forms/assets/eds-aem-publish.png)

### Konfigurationskrav

#### 1. AEM Dispatcher Configuration

Konfigurera Dispatcher på din AEM Publish-instans:

- **Tillåt inskickningssökvägar**: Ändra `filters.any` så att POST-begäranden tillåts till `/adobe/forms/af/submit/...`
- **Inga omdirigeringar**: Kontrollera att Dispatcher-reglerna inte omdirigerar sökvägar för formulärinlämning

#### &#x200B;2. Refererarfilter för OSGi

I AEM OSGi-konsolen (`/system/console/configMgr`):

1. Sök efter &quot;Apache Sling Referrer-filter&quot;
2. Lägg till din Edge Delivery-domän i listan Tillåt värdar
3. Inkludera domäner som `https://your-eds-domain.hlx.page`

#### &#x200B;3. Omdirigeringsregler för CDN

Konfigurera ditt Edge Delivery CDN för att skicka material vidare:

- Vidarebefordra begäranden från `/adobe/forms/af/submit/...` till din AEM Publish-instans
- Implementeringen varierar beroende på CDN-leverantör (Fastly, Akamai, Cloudflare)

#### &#x200B;4. Formulärkonfiguration

1. Skapa formulär i Universal Editor
2. Konfigurera åtgärden skicka för att rikta AEM Forms-åtgärden
3. Ange slutpunktssökväg för överföring
4. Publicera formulär på Edge Delivery webbplats

+++

+++ Formulärinbäddning (valfritt)

Bädda in formulär som skapats på en plats på olika webbsidor eller webbplatser.

### Användningsexempel

- Återanvända standardformulär på flera landningssidor
- Inkludera specialanpassade blanketter i dokumentredigerat innehåll
- Underhåll ett formulär i flera EDS-projekt

### CORS-konfiguration

Konfigurera resursdelning mellan ursprung på formulärkällan:

1. **Lägg till CORS-rubriker** i formulärkällsvar:
   - `Access-Control-Allow-Origin: https://your-host-domain.com`
   - `Access-Control-Allow-Methods: GET, OPTIONS`
   - `Access-Control-Allow-Headers: Content-Type`

2. **Exempelkonfiguration**:

       &#x200B;# Konfiguration för platsen som är värd för formuläret 
       rubriker:
       - sökväg: /forms/**
       anpassad:
       Access-control-Allow-origin: https://host-domain.com
       Access-control-allow-methods: GET, OPTIONS
   

### Inbäddningssteg

1. **Skapa och publicera formulär**
   - Bygg formulär med Document Authoring eller Universal Editor
   - Konfigurera överföringsmetod (FSS eller AEM Publish)
   - Publicera till fristående URL

2. **Konfigurera CORS**
   - Ställ in CORS-huvuden på formulärkällans webbplats
   - Tillåt värdsidans domän att hämta formulär

3. **Bädda in på värdsida**
   - Lägg till block för inbäddning av formulär på värdsidan
   - Punktblock till publicerad formulär-URL
   - Publicera värdsida

![Inbäddad formulärarkitektur](/help/forms/assets/eds-embedded-form.png)

+++

+++ Vanliga problem

| Problem | Lösning |
|-------|----------|
| **Det går inte att skicka formulär** | Kontrollera konsolfel, verifiera slutpunkts-URL, bekräfta behörigheter |
| **Inbäddat formulär visas inte** | Konfigurera CORS-huvuden på formulärkällan, verifiera formulär-URL |
| **403/401 fel med AEM** | Uppdatera Sling Referer-filter, kontrollera autentiseringsinställningar |
| **Data når inte kalkylblad** | Verifiera att `forms@adobe.com` har redigeringsåtkomst, kontrollera kalkylblads-URL |
| **CORS-fel** | Lägg till korrekta `Access-Control-Allow-Origin` rubriker i formulärkällan |

+++

## Konfigurationsexempel

+++ Dokumentbaserat formulär med inskickning av kalkylblad

1. Skapa formulärstruktur i Google Docs/Sheets
2. Konfigurera slutpunkt för Forms-överföringstjänst
3. Bevilja `forms@adobe.com` redigeringsåtkomst till målkalkylblad
4. Publicera dokument på Edge Delivery webbplats
5. Testa inskickning av formulär och dataflöde

+++

+++ Universell redigeringsblankett med AEM Workflow

1. Skapa formulär i Universal Editor
2. Konfigurera åtgärden Skicka till&quot;Anropa AEM Workflow&quot;
3. Konfigurera Dispatcher och referensfilter i AEM Publish
4. Konfigurera CDN-routningsregler
5. Publicera formulär och testa arbetsflödeskörning

+++

## Bästa praxis

- **Använd Forms överföringstjänst** för enkla datainhämtningsscenarier
- **Välj AEM Publish** när komplex bearbetning eller integrering krävs
- **Testa grundligt** i mellanlagringsmiljön före produktionsdistributionen
- **Övervaka överföringar** med AEM loggar och konsolfel
- **Implementera korrekt felhantering** för misslyckade överföringar
- **Verifiera data** på både klient- och servernivå
- **Använd HTTPS** för alla formuläröverföringar och dataöverföringar

## Relaterade ämnen

- [Dokumentbaserad redigering med EDS Forms](/help/edge/docs/forms/tutorial.md)
- [Universell redigerare med EDS Forms](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)
- [AEM Forms Submission Service](/help/forms/forms-submission-service.md)
- [Konfigurera datakällor](/help/forms/configure-data-sources.md)
- [AEM Forms Workflow Reference](/help/forms/aem-forms-workflow-step-reference.md)

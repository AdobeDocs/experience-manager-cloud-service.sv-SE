---
title: Konfigurera Skicka-åtgärder för AEM Forms med Edge Delivery Services
description: Lär dig hur du konfigurerar skicka-åtgärder i AEM Forms med Edge Delivery Services. Välj mellan Forms Submission Service och AEM Publish Submit Action för att hantera formulärdata på ett säkert och effektivt sätt.
feature: Edge Delivery Services
role: Admin, Developer
exl-id: 8f490054-f7b6-40e6-baa3-3de59d0ad290
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '810'
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

#### &#x200B;1. Uppdatera AEM Instance URL i Edge Delivery

Uppdatera AEM Cloud Service-instansens URL i filen `constant.js` i blocket `form` under `submitBaseUrl`. Du kan konfigurera URL-adressen baserat på din miljö:

**För Cloud Service-instans**

```js
export const submitBaseUrl = '<aem-publish-instance-URL>';
```

**För lokal utveckling**

```js
export const submitBaseUrl = 'http://localhost:<port-number>';
```

#### &#x200B;2. Refererarfilter för OSGi

Konfigurera referensfiltret så att dina specifika Edge Delivery-webbplatsdomäner tillåts:

1. Skapa eller uppdatera OSGi-konfigurationsfilen: `org.apache.sling.security.impl.ReferrerFilter.cfg.json`

2. Lägg till följande konfiguration med dina specifika webbplatsdomäner:

   ```json
   {
     "allow.empty": false,
     "allow.hosts": [
       "main--abc--adobe.aem.live",
       "main--abc1--adobe.aem.live"
     ],
     "allow.hosts.regexp": [
       "https://.*\\.aem\\.live:443",
       "https://.*\\.aem\\.page:443",
       "https://.*\\.hlx\\.page:443",
       "https://.*\\.hlx\\.live:443"
     ],
     "filter.methods": [
       "POST",
       "PUT",
       "DELETE",
       "COPY",
       "MOVE"
     ],
     "exclude.agents.regexp": [
       ""
     ]
   }
   ```

3. Distribuera konfigurationen via Cloud Manager

Mer information om konfigurationen för OSGi-referensfilter finns i [Handboken för referensfilter](https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-service/content/headless/deployment/referrer-filter).

#### 3. CORS (Cross-Origin Resource Sharing) Issues

Konfigurera CORS-inställningar i AEM för att tillåta begäranden från dina specifika Edge Delivery-webbplatsdomäner:

**Developer Localhost**

```apache
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(http://localhost(:\d+)?$)#" CORSTrusted=true
```

**Edge Delivery Sites - Lägg till varje webbplatsdomän individuellt**

```apache
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://main--abc--adobe\.aem\.live$)#" CORSTrusted=true
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://main--abc1--adobe\.aem\.live$)#" CORSTrusted=true
```

**Äldre Franklin-domäner (om de fortfarande används)**

```apache
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://.*\.hlx\.page$)#" CORSTrusted=true  
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://.*\.hlx\.live$)#" CORSTrusted=true
```

>[!NOTE]
>
>Ersätt `main--abc--adobe.aem.live` och `main--abc1--adobe.aem.live` med de faktiska webbplatsdomänerna. Varje plats som lagras från samma databas kräver en separat CORS-konfigurationspost.

Detaljerad CORS-konfiguration finns i [CORS-konfigurationsguiden](https://experienceleague.adobe.com/sv/docs/experience-manager-learn/getting-started-with-aem-headless/deployments/configurations/cors).


Om du vill aktivera CORS för din lokala utvecklingsmiljö läser du artikeln [Förstå korsdomänsresursdelning (CORS)](https://experienceleague.adobe.com/sv/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing).

<!--
#### 4. CDN Redirect Rules

Configure your Edge Delivery CDN to route submissions:

- Route requests from `/adobe/forms/af/submit/...` to your AEM Publish instance
- Implementation varies by CDN provider (Fastly, Akamai, Cloudflare)-->

#### &#x200B;4. Formulärkonfiguration

1. Skapa formulär i Universal Editor
2. Konfigurera åtgärden skicka för att rikta AEM Forms-åtgärden
3. Ange slutpunktssökväg för överföring
4. Publicera formulär på Edge Delivery webbplats

+++
<!--
+++ Form Embedding

Embed forms created in one location into different web pages or sites.

### Use Cases

- Reuse standard forms across multiple landing pages
- Include specialized forms in Document-Authored content
- Maintain single form across multiple EDS projects

### CORS Configuration

Configure Cross-Origin Resource Sharing on the form source:

1. **Add CORS Headers** to form source responses:
   - `Access-Control-Allow-Origin: https://your-host-domain.com`
   - `Access-Control-Allow-Methods: GET, OPTIONS`  
   - `Access-Control-Allow-Headers: Content-Type`

2. **Example Configuration**:

        # Configuration for site hosting the form
        headers:
          - path: /forms/**
            custom:
              Access-Control-Allow-Origin: https://host-domain.com
              Access-Control-Allow-Methods: GET, OPTIONS

### Embedding Steps

1. **Create and Publish Form**
   - Build form using Document Authoring or Universal Editor
   - Configure submission method (FSS or AEM Publish)
   - Publish to standalone URL

2. **Configure CORS**
   - Set up CORS headers on form source site
   - Allow host page domain to fetch form

3. **Embed in Host Page**
   - Add form embedding block to host page
   - Point block to published form URL
   - Publish host page

![Embedded Form Architecture](/help/forms/assets/eds-embedded-form.png)

+++-->

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

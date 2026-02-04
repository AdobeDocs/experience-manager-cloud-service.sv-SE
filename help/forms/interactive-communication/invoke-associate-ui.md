---
title: Anropa ett associerat användargränssnitt vid publicering-instans
description: Läs om hur man integrerar och anropar AEM Forms Associate-gränssnittet vid publicering så att kundfokuserade proffs kan generera personaliserad interaktiv kommunikation i realtid.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
hide: true
hidefromtoc: true
source-git-commit: 2f3badafddfdfe1dd21eb74be7189102aa0474bc
workflow-type: tm+mt
source-wordcount: '831'
ht-degree: 0%

---


# Generera anpassad kommunikation med associerat användargränssnitt

<span> Funktionen för interaktiv kommunikation är tillgänglig i programmet för tidig användning. Skicka ett e-postmeddelande från din arbetsadress till `aem-forms-ea@adobe.com` för att begära åtkomst.</span>

Associate-gränssnittet kan anropas direkt i Publish-instanser, vilket gör att kundfokuserade proffs som fältassociatörer och tjänsteagenter kan generera personaliserad kommunikation i realtid under kundinteraktioner.

Tabellen nedan visar de olika verkliga scenarierna där Associate UI kan användas för att skicka personaliserade meddelanden till kunder:

| Bransch | Användningsfall |
|----------|----------|
| **Finansiella tjänster** | Generera lånebekräftelsebrev, kontoutdrag och riskprofilsammanfattningar i realtid under kundmöten |
| **Försäkring** | Ta fram ögonblickliga försäkringskort och sammanställningar av skaderegleringsblanketter hos serviceräknare |
| **Hälsovård** | Skapa sammanfattningar av patientbehandlingsplaner med beräknade lönebelopp och scheman |
| **Offentlig sektor** | Generera polisverifieringsrapporter, kvitton från allmänheten och sammanfattningar av ärendeuppdateringar på plats |

## Förutsättningar

Innan du integrerar det associerade användargränssnittet med ditt program måste du se till att du har:

- Interaktiv kommunikation skapad och publicerad
- Webbläsare med popup-stöd aktiverat
- Associerade [användare måste vara en del av gruppen för formulär-associater](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/administrator-help/setup-organize-users/creating-configuring-roles#assign-a-role-to-users-and-groups)
- Autentisering konfigurerad - [SAML 2.0](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/authentication/saml-2-0)

>[!NOTE]
>
> För Associate UI krävs ytterligare SAML-konfigurationer utöver standardinställningarna som förklaras i artikeln [SAML 2.0-autentisering](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/authentication/saml-2-0). Mer information finns i avsnittet [Ytterligare SAML-konfigurationer för det associerade användargränssnittet](#additional-saml-configurations-for-associate-ui).

### Ytterligare SAML-konfigurationer för associerat användargränssnitt

När du konfigurerar SAML 2.0-autentisering för det associerade användargränssnittet måste du använda följande specifika inställningar i OSGi-konfigurationsfilerna.

#### SAML-autentiseringshanterare

Skapa filen `com.adobe.granite.auth.saml.SamlAuthenticationHandler~saml.cfg.json` i `ui.config/src/main/content/jcr_root/apps/<project-name>/osgiconfig/config.publish`:

```json
  {
    "path": ["/libs/fd/associate"],
    "serviceProviderEntityId": "https://publish-p{program-id}-e{env-id}.adobeaemcloud.com",
    "assertionConsumerServiceURL": "https://publish-p{program-id}-e{env-id}.adobeaemcloud.com/libs/fd/associate/saml_login",
    "idpUrl": "https://login.microsoftonline.com/{azure-tenant-id}/saml2",
    "idpCertAlias": "{your-certificate-alias}",
    "idpIdentifier": "https://sts.windows.net/{azure-tenant-id}/",
    "userIDAttribute": "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name",
    "createUser": true,
    "userIntermediatePath": "saml",
    "synchronizeAttributes": [
      "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname=profile/givenName",
      "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname=profile/familyName",
      "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress=profile/email"
      ],
      "addGroupMemberships": true,
      "defaultGroups": ["forms-associates"],
      "defaultRedirectUrl": "/libs/fd/associate/ui.html",
      "idpHttpRedirect": false,
      "service.ranking": 5002
  }
```

| Egenskap | Beskrivning |
|----------|-------------|
| `path` | Måste anges till `/libs/fd/associate` för associerat användargränssnitt |
| `defaultGroups` | Ange till `forms-associates` för att automatiskt tilldela användare till den obligatoriska gruppen |
| `defaultRedirectUrl` | Dirigerar autentiserade användare till det associerade användargränssnittet |
| `idpHttpRedirect` | Måste vara `false` för SP-initierat flöde |
| `idpCertAlias` | Måste matcha certifikataliaset i Trust Store exakt (skiftlägeskänsligt) |

#### Sling Authenticator

Uppdatera filen `org.apache.sling.engine.impl.auth.SlingAuthenticator~saml.cfg.json` i `ui.config/src/main/content/jcr_root/apps/<project-name>/osgiconfig/config.publish`:

```json
{
  "sling.auth.requirements": ["+/libs/fd/associate/ui.html"],
  "sling.auth.anonymous": false
}
```

#### Dispatcher Filter

Om den inte redan finns lägger du till följande regler i `dispatcher/src/conf.dispatcher.d/filters/filters.any`-filen:

```json
  # Allow Interactive Communications APIs and Associate UI
  /XXXX { /type "allow" /method '(GET|OPTIONS)' /url "/adobe/communications" }
  /XXXX { /type "allow" /method '(GET|POST|OPTIONS)' /url "/adobe/communications/*" }
  /XXXX { /type "allow" /method "GET" /url "/content/dam/fd:fonts/*" }
  /XXXX { /type "allow" /method '(GET|OPTIONS)' /url "/libs/fd/associate/*" }
```

>[!NOTE]
>
> Ersätt `XXXX` med lämplig numerisk sekvens som används i din befintliga `filters.any`-fil.

## Anropa associerat gränssnitt vid publiceringsinstans

Om du vill anropa det associerade användargränssnittet från programmet konfigurerar du Publish instance URL-adressen, förbereder datanyttolasten och använder integrationsfunktionen för att starta det associerade användargränssnittet i ett nytt webbläsarfönster.

### Steg 1: Konfigurera publiceringsinstansens URL

Användargränssnittet för Associate nås via en specifik slutpunkt på din AEM Forms Cloud Service Publish-instans:

```javascript
const AEM_URL = 'https://publish-p{program-id}-e{env-id}.adobeaemcloud.com/libs/fd/associate/ui.html';
```

Ersätt `{program-id}` och `{env-id}` med dina faktiska miljövärden.

### Steg 2: Förbered datanyttolasten

Strukturera din datanyttolast med följande format:

```javascript
const data = {
  id: "your-ic-id",              // Required: Interactive Communication ID
  prefill: {                      // Optional: Data to prefill the IC
    serviceName: "YourService",
    serviceParams: { key: "value" }
  },
  options: {}                     // Optional: Additional configuration options
};
```

**Nyttolastkomponenter:**

| Komponent | Obligatoriskt | Beskrivning |
|-----------|----------|-------------|
| `id` | Ja | Identifieraren för den interaktiva kommunikation som ska läsas in |
| `prefill` | Valfritt | Innehåller tjänstkonfiguration för förifyllning av data. |
| `prefill.serviceName` | Valfritt | Namn på den formulärdatamodelltjänst som ska anropas för förifyllning av data |
| `prefill.serviceParams` | Valfritt | Nyckelvärdepar som skickas till förifyllningstjänsten |
| `options` | Valfritt | Ytterligare egenskaper som stöds för PDF-återgivning - nationella inställningar, includeAttachments, embedFonts, makeAccessible |

### Steg 3: Implementera integreringsfunktionen

Skapa en JavaScript-funktion som startar Associate-gränssnittet och hanterar meddelandekommunikationen:

```javascript
function launchAssociateUI(icId, prefillService, prefillParams, options) {
  if (!icId) {
    console.error('IC ID required');
    return;
  }
   
  const data = {
    id: icId,
    prefill: {
      serviceName: prefillService || '',
      serviceParams: prefillParams || {}
    },
    options: options || {}
  };
   
  const AEM_URL = 'https://your-aem.adobeaemcloud.com/libs/fd/associate/ui.html';
  const win = window.open(AEM_URL, '_blank');
   
  if (!win) {
    alert('Please enable pop-ups for this site');
    return;
  }
   
  const readyHandler = (event) => {
    if (event.data && event.data.type === 'READY' && event.data.source === 'APP') {
      win.postMessage({ type: 'INIT', source: 'PORTAL', data: data }, '*');
      window.removeEventListener('message', readyHandler);
    }
  };
   
  window.addEventListener('message', readyHandler);
   
  // Fallback timeout in case READY message is missed
  setTimeout(() => {
    if (win && !win.closed) {
      win.postMessage({ type: 'INIT', source: 'PORTAL', data: data }, '*');
      window.removeEventListener('message', readyHandler);
    }
  }, 1000);
}
```

### Steg 4: Anropa funktionen

Anropa funktionen med lämpliga parametrar:

```javascript
// Basic invocation with IC ID only
launchAssociateUI('12345', '', {}, {});

// With prefill service
launchAssociateUI('12345', 'FdmTestData', 
  { customerId: '101'}, {});

// With all parameters
launchAssociateUI('12345', 'FdmTestData', 
  { policyNumber: 'POL-123' }, 
  { locale: 'en', acrobatVersion: 'Acrobat_11' });
```

## Testa integrationen med en exempelsida på HTML

Här följer ett enkelt HTML-exempel om du vill se hur användargränssnittet för Associate visas i förgrunden och testa din integrering. På den här exempelsidan kan du ange IC-id:t, konfigurera parametrar för förifyllningstjänsten, ange PDF-alternativ och starta Associate-gränssnittet på din Publish-instans.

```html
<!DOCTYPE html>
<html>
<head>
  <title>Associate UI Integration</title>
  <style>
    body { 
      font-family: sans-serif; 
      max-width: 600px; 
      margin: 50px auto; 
      padding: 20px; 
    }
    .form-group { 
      margin: 20px 0; 
    }
    label { 
      display: block; 
      margin-bottom: 5px; 
      font-weight: bold; 
    }
    input, textarea { 
      width: 100%; 
      padding: 8px; 
      border: 1px solid #ccc; 
      border-radius: 4px; 
      box-sizing: border-box;
    }
    textarea { 
      height: 80px; 
      font-family: monospace; 
    }
    button { 
      padding: 10px 20px; 
      margin: 5px; 
      cursor: pointer; 
      border-radius: 4px;
    }
    .btn-primary { 
      background: #007bff; 
      color: white; 
      border: none; 
    }
    .btn-primary:hover {
      background: #0056b3;
    }
    .error { 
      color: red; 
      font-size: 12px; 
      display: none; 
    }
  </style>
</head>
<body>
  <h1>Launch Associate UI</h1>
  
  <form id="form">
    <div class="form-group">
      <label>IC ID *</label>
      <input type="text" id="icId" placeholder="Enter Interactive Communication ID" required>
    </div>
    
    <div class="form-group">
      <label>Prefill Service</label>
      <input type="text" id="serviceName" placeholder="e.g., CustomerDataService">
    </div>
    
    <div class="form-group">
      <label>Service Parameters (JSON)</label>
      <textarea id="serviceParams" placeholder='{"customerId": "12345"}'>{}</textarea>
      <span id="paramsError" class="error">Invalid JSON format</span>
    </div>
    
    <div class="form-group">
      <label>Options (JSON)</label>
      <textarea id="options" placeholder='{"mode": "edit", "locale": "en_US"}'>{}</textarea>
      <span id="optionsError" class="error">Invalid JSON format</span>
    </div>
    
    <button type="button" onclick="reset()">Reset</button>
    <button type="button" class="btn-primary" onclick="launch()">Launch Associate UI</button>
  </form>

  <script>
    // Replace with your AEM Publish instance URL
    const AEM_URL = 'https://publish-p{program-id}-e{env-id}.adobeaemcloud.com/libs/fd/associate/ui.html';
    
    function validateJSON(str, errorId) {
      const err = document.getElementById(errorId);
      try {
        const obj = JSON.parse(str || '{}');
        err.style.display = 'none';
        return obj;
      } catch (e) {
        err.style.display = 'block';
        return null;
      }
    }
    
    function launch() {
      const icId = document.getElementById('icId').value.trim();
      if (!icId) { 
        alert('IC ID is required'); 
        return; 
      }
      
      const params = validateJSON(document.getElementById('serviceParams').value, 'paramsError');
      const opts = validateJSON(document.getElementById('options').value, 'optionsError');
      
      if (!params || !opts) { 
        alert('Please fix JSON errors before launching'); 
        return; 
      }
      
      const data = {
        id: icId,
        prefill: {
          serviceName: document.getElementById('serviceName').value.trim(),
          serviceParams: params
        },
        options: opts
      };
      
      const win = window.open(AEM_URL, '_blank');
      if (!win) { 
        alert('Pop-up blocked. Please enable pop-ups for this site.'); 
        return; 
      }
      
      const handler = (e) => {
        if (e.data && e.data.type === 'READY' && e.data.source === 'APP') {
          win.postMessage({ type: 'INIT', source: 'PORTAL', data }, '*');
          window.removeEventListener('message', handler);
        }
      };
      
      window.addEventListener('message', handler);
      
      // Fallback timeout in case READY message is missed
      setTimeout(() => {
        if (win && !win.closed) {
          win.postMessage({ type: 'INIT', source: 'PORTAL', data }, '*');
          window.removeEventListener('message', handler);
        }
      }, 1000);
    }
    
    function reset() {
      document.getElementById('form').reset();
      document.getElementById('serviceParams').value = '{}';
      document.getElementById('options').value = '{}';
      document.getElementById('paramsError').style.display = 'none';
      document.getElementById('optionsError').style.display = 'none';
    }
  </script>
</body>
</html>
```

### Hur exemplet fungerar

1. **IC ID-fält**: Ange identifieraren för interaktiv kommunikation (obligatoriskt)
2. **Förifyll tjänst**: Ange formulärdatamodellens tjänstnamn för förifyllnad av data
3. **Tjänsteparametrar**: Ange JSON-objekt med parametrar som ska skickas till förifyllningstjänsten
4. **Alternativ**: Ange konfigurationsalternativ för PDF, till exempel locale, includeAttachments, embedFonts, makeAccessible
5. **Startknapp**: Öppnar det associerade användargränssnittet i ett nytt fönster och skickar initieringsdata

## Exempel på datanyttolast

### Minimal nyttolast (endast IC)

Använd detta när inga förifyllda data krävs:

```json
{
  "id": "12345",
  "prefill": { 
    "serviceName": "", 
    "serviceParams": {} 
  },
  "options": {}
}
```

### Med förifyllda data

Använd detta för att dynamiskt fylla i konstruktorn med kunddata:

```json
{
  "id": "12345",
  "prefill": {
    "serviceName": "IC_FDM",
    "serviceParams": {
      "customerId": "101",
      "accountNumber": "ACC-98765"
    }
  },
  "options": {}
}
```

### Med konfiguration av alternativ

Använd detta för att ange ytterligare återgivningsalternativ:

```json
{
  "id": "12345",
  "prefill": {
    "serviceName": "IC_FDM",
    "serviceParams": {
      "customerId": "101",
      "accountNumber": "ACC-98765"
    }
  },
  "options": { 
      locale: "en_US",
      includeAttachments: "true",
      webOptimized: "false",
      embedFonts: "false",
      makeAccessible: "false"
  }
}
```

## Felsökning

### Popup-fönster blockerad

**Problem**: Associate UI-fönstret öppnas inte.

**Lösning**:
- Aktivera popup-fönster för din domän i webbläsarinställningarna
- Kontrollera att `window.open()` anropas från en användaråtgärd (t.ex. knappklickning)
- Testa med olika webbläsare för att identifiera blockeringsbeteenden

### Data läses inte in

**Problem**: Interaktiv kommunikation öppnas men data fylls inte i.

**Lösning**:
- Verifiera att IC-ID:t är korrekt och att IC:et har publicerats
- Kontrollera webbläsarkonsolen för JavaScript-fel
- Kontrollera att strukturen `postMessage` matchar specifikationen exakt
- Verifiera att tjänsten för formulärdatamodell är korrekt konfigurerad

### Autentiseringsfel

**Problem**: Användaren får ett autentiseringsfel när det associerade användargränssnittet öppnas.

**Lösning**:
- Konfigurera SAML 2.0-autentisering på publiceringsinstansen
- Kontrollera att användaren ingår i gruppen **forms-associates**
- Kontrollera timeoutinställningar för session

### CORS-fel

**Problem**: Resursdelningsfel mellan ursprung i konsolen.

**Lösning**:
- För utveckling: Använd `'*'` som målursprung i `postMessage`
- För produktion: Ange den exakta URL-adressen till ditt program
- Kontrollera att publiceringsinstansens CORS-inställningar tillåter programdomänen

<!--## Best Practices

When implementing the Associate UI integration, follow these best practices:

1. **Validation**: Always validate the IC ID and JSON payload before sending
2. **Error Handling**: Implement proper error handling for `window.open()` failures
3. **User Experience**: Display a loading indicator while the Associate UI initializes
4. **Memory Management**: Remove event listeners after initialization to prevent memory leaks
5. **Testing**: Test the integration with popup blockers enabled to ensure graceful handling
6. **User Permissions**: Verify users have appropriate access to the forms-associates group-->

## Se även

- [Associera gränssnittet i interaktiv kommunikationsredigerare](/help/forms/interactive-communication/associate-ui-in-interactive-communication-editor.md)
- [Interaktiv kommunikation i molnet](/help/forms/early-access-ea-features.md#interactive-communications-on-cloud)
- [Tidiga åtkomstfunktioner](/help/forms/early-access-ea-features.md)
---
title: Integrera associerat gränssnitt för interaktiv kommunikation vid körning
description: Lär dig hur du integrerar AEM Forms Associate-gränssnittet med programmet så att kundansvariga kan generera skräddarsydd interaktiv kommunikation i realtid vid publicering.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
exl-id: f946ccea-86d0-4086-8208-9583b8206244
source-git-commit: 749ad181c7e9e59a0601e0eddd85b0bd0e761f08
workflow-type: tm+mt
source-wordcount: '1074'
ht-degree: 0%

---

# Integrera associerat gränssnitt i ditt program

<span> Funktionen för interaktiv kommunikation är tillgänglig i programmet för tidig användning. Skicka ett e-postmeddelande från din arbetsadress till `aem-forms-ea@adobe.com` för att begära åtkomst.</span>

I den här artikeln beskrivs hur du integrerar det associerade användargränssnittet med ditt program, vilket gör det möjligt för kundanvändare som fältassociatörer och tjänsteagenter att generera personaliserad interaktiv kommunikation i realtid vid publicering.

## Förutsättningar

Innan du integrerar det associerade användargränssnittet med ditt program måste du se till att du har:

- Interaktiv kommunikation skapad och publicerad
- Webbläsare med popup-stöd aktiverat
- Associerade [användare måste vara en del av gruppen för formulär-associater](https://experienceleague.adobe.com/sv/docs/experience-manager-65/content/forms/administrator-help/setup-organize-users/creating-configuring-roles#assign-a-role-to-users-and-groups)
- Autentisering konfigurerad med någon [autentiseringsmekanism som stöds av AEM](https://experienceleague.adobe.com/sv/docs/experience-manager-learn/cloud-service/authentication/authentication) (till exempel SAML 2.0, OAuth eller anpassade autentiseringshanterare)

>[!NOTE]
>
>- I den här artikeln visas autentiseringskonfigurationen med SAML 2.0 med [Microsoft Entra ID (Azure AD) som identitetsleverantör](https://learn.microsoft.com/en-us/power-pages/security/authentication/openid-settings).
>- För Associate UI krävs ytterligare SAML-konfigurationer utöver standardinställningarna som förklaras i artikeln [SAML 2.0-autentisering](https://experienceleague.adobe.com/sv/docs/experience-manager-learn/cloud-service/authentication/saml-2-0). Mer information finns i avsnittet [Ytterligare SAML-konfigurationer för det associerade användargränssnittet](#additional-saml-configurations-for-associate-ui).

### Ytterligare SAML-konfigurationer för associerat användargränssnitt

När du konfigurerar SAML 2.0-autentisering för det associerade användargränssnittet måste du använda följande specifika inställningar i OSGi-konfigurationsfilerna.

#### SAML-autentiseringshanterare

SAML Authentication Handler är en OSGi-fabrikskonfiguration som tillåter flera SAML-konfigurationer för olika resursträd. Detta möjliggör driftsättning av AEM på flera platser och gör att du kan lägga till associerade gränssnittsresurser i din befintliga SAML-konfiguration.

Skapa filen `com.adobe.granite.auth.saml.SamlAuthenticationHandler~saml.cfg.json` i `ui.config/src/main/content/jcr_root/apps/<project-name>/osgiconfig/config.publish`:

```json
  {
    "path": ["/libs/fd/associate"],
    "serviceProviderEntityId": "https://publish-p{program-id}-e{env-id}.adobeaemcloud.com",
    "assertionConsumerServiceURL": "https://publish-p{program-id}-e{env-id}.adobeaemcloud.com/libs/fd/associate/saml_login"
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

Sling-autentiseraren tvingar fram autentisering för åtkomst till associerade gränssnittsresurser vid publicering.

Uppdatera filen `org.apache.sling.engine.impl.auth.SlingAuthenticator~saml.cfg.json` i `ui.config/src/main/content/jcr_root/apps/<project-name>/osgiconfig/config.publish`:

```json
{
  "sling.auth.requirements": ["+/libs/fd/associate/ui.html"],
  "sling.auth.anonymous": false
}
```

#### Dispatcher Filter

Lägg till följande regler för att se till att Interactive Communications API:er och Associate UI fungerar korrekt på Publish-instansen.

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

I det här avsnittet får du hjälp med att starta det associerade användargränssnittet från ditt eget program. Följ de här stegen för att komma igång snabbt. Börja med en färdig HTML-sida och konfigurera den sedan för din miljö.

### Steg 1: Börja med HTML-exempelsidan

Om du snabbt vill testa och förstå hur integreringen av användargränssnittet i Associate fungerar använder du följande exempelsida i HTML. Kopiera koden till en HTML-fil och öppna den i webbläsaren.

>[!NOTE]
>
> Det här exemplet på HTML kräver ett IC ID och en förifyllningstjänst. Du kan testa det med ditt IC-ID och exempeltjänsten Prefill&quot;FdmTestData&quot;.

HTML exempel har ett enkelt formulärgränssnitt där du kan ange din interaktiva kommunikationsinformation och starta gränssnittet för Associate med ett enda klick.

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

### Steg 2: Konfigurera din URL för publiceringsinstans

Innan du kan starta det associerade användargränssnittet måste du peka exemplet mot AEM Forms Cloud Service Publish-instansen.

I HTML-exemplet ovan hittar du följande rad i avsnittet `<script>`:

```javascript
const AEM_URL = 'https://publish-p{program-id}-e{env-id}.adobeaemcloud.com/libs/fd/associate/ui.html';
```

Ersätt platshållarvärdena med den faktiska miljöinformationen:
- `{program-id}`: Ditt program-ID för AEM Cloud-tjänsten
- `{env-id}`: Ditt miljö-ID

Om ditt program-ID till exempel är `12345` och miljö-ID är `67890` blir URL:en:

```javascript
const AEM_URL = 'https://publish-p12345`-e67890.adobeaemcloud.com/libs/fd/associate/ui.html';
```

>[!NOTE]
>
> Av säkerhetsskäl skickas inte parametrar som Interactive Communication ID, prefill service och service-parametrar via URL:en. I stället skickas dessa parametrar säkert med JavaScript `postMessage` API.

### Steg 3: Förstå JavaScript integrationsfunktion

I exemplet på HTML används följande JavaScript-funktion för att starta Associate-gränssnittet. Den här funktionen validerar IC-ID:t, konstruerar datanyttolasten, öppnar det associerade användargränssnittet i ett nytt webbläsarfönster och skickar data med webbläsarens `postMessage`-API.

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

Funktionen accepterar fyra parametrar: IC-ID (obligatoriskt), namn på förifyllningstjänsten, parametrar för förifyllningstjänsten och ytterligare alternativ. Dessa parametrar är strukturerade i datanyttolasten enligt beskrivningen nedan.

### Steg 4: Förstå datanyttolastens struktur

**Nyttolastformat:**

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
| `prefill` | Valfritt | Innehåller tjänstkonfiguration för förifyllning av data |
| `prefill.serviceName` | Valfritt | Namn på den formulärdatamodelltjänst som ska anropas för förifyllning av data |
| `prefill.serviceParams` | Valfritt | Nyckelvärdepar som skickas till förifyllningstjänsten |
| `options` | Valfritt | Ytterligare egenskaper som stöds för PDF-återgivning - locale, includeAttachments, embedFonts, makeAccessible |

#### Exempel på datanyttolast

**Minimal nyttolast (endast IC ID)**

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

**Med förifyllda data**

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

**Med PDF renderingsalternativ**

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
      "locale": "en_US",
      "includeAttachments": "true",
      "webOptimized": "false",
      "embedFonts": "false",
      "makeAccessible": "false"
  }
}
```

### Steg 5: Ange IC-id:t och starta det associerade användargränssnittet

Nu kan du starta Associate-gränssnittet med exempelsidan för HTML:

1. **Ange IC-ID:t**: I fältet **IC-ID** anger du identifieraren för den publicerade interaktiva kommunikationen. Detta är det enda obligatoriska fältet.

1. **Konfigurera förifyllningstjänst**: Om du vill förifylla IC med dynamiska data anger du tjänstnamnet för formulärdatamodellen i fältet **Förifyllningstjänst**. Använd till exempel `FdmTestData` som exempeldata.

   ![Exempel på HTML-gränssnitt](/help/forms/assets/samplehtmlui.png)

1. **Klicka på Starta associerat gränssnitt**: Klicka på knappen **Starta associerat gränssnitt**. Ett nytt webbläsarfönster öppnas med Associate-gränssnittet, som är förinläst med din interaktiva kommunikation.

Ange data så visas det tillhörande användargränssnittet enligt nedan:

![Associera gränssnitt](/help/forms/assets/associateui.png)

>[!NOTE]
>
> Om fönstret inte öppnas kontrollerar du att webbläsaren tillåter popup-fönster för den här platsen.


<!--**Add Service Parameters**: In the **Service Parameters (JSON)** field, enter a JSON object with the parameters your prefill service requires. For example:

   ```json
   {"customerId": "101", "accountNumber": "ACC-98765"}
   ```

  **Set PDF Options** (optional): In the **Options (JSON)** field, configure rendering options such as locale, attachments, or accessibility settings.-->

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

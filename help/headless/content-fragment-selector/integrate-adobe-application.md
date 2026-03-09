---
title: Integrera väljaren för innehållsfragment med ett Adobe-program
description: Integrera väljaren för innehållsfragment med olika Adobe-program.
role: Admin, User, Developer
source-git-commit: a16d9e9fa6483a89283c595372abcc437d1d962e
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---

# Integrera väljaren för innehållsfragment med Adobe {#integrate-content-fragment-selector-with-adobe-application}

Med väljaren för innehållsfragment kan du integrera med olika Adobe-program så att de kan fungera tillsammans sömlöst.

## Förutsättningar {#prerequisites}

Använd följande krav om du integrerar väljaren för innehållsfragment med ett Adobe-program:

* [Förutsättningar](/help/headless/content-fragment-selector/overview.md#prerequisites)
* imsOrg
* imsToken
* apikey

## Integrera väljaren för innehållsfragment med ett Adobe-program {#integrate-content-fragment-selector-with-an-adobe-application}

I följande exempel visas hur du använder väljaren för innehållsfragment när du kör ett Adobe-program under Enhetligt gränssnitt, eller när du redan har en `imsToken` genererad för autentisering.

Inkludera paketet Content Fragment Selector i koden med taggen `script`, vilket visas i exemplet nedan.

* När skriptet har lästs in är den globala variabeln `PureJSContentFragmentSelectors` tillgänglig för användning.
* Definiera väljaren för innehållsfragment [egenskaper](/help/headless/content-fragment-selector/properties.md):

   * egenskaperna `imsOrg` och `imsToken` krävs för autentisering i Adobe-programmet
   * egenskapen `handleSelection` används för att hantera de valda fragmenten.

* Om du vill återge väljaren för innehållsfragment anropar du funktionen `renderFragmentSelector`.
* Innehållsfragmentväljaren visas i behållarelementet `<div>`.

Om du följer dessa steg kan du använda väljaren för innehållsfragment tillsammans med ditt Adobe-program.

```html {line-numbers="true"}
<!DOCTYPE html>
<html>
<head>
    <title>Fragment Selector</title>
    <script src="https://experience.adobe.com/solutions/CQ-fragmentss-selectors/static-fragments/resources/fragments-selectors.js"></script>
    <script>
        // get the container element in which we want to render the FragmentSelector component
        const container = document.getElementById('fragment-selector-container');
        // imsOrg and imsToken are required for authentication in Adobe application
        const fragmentSelectorProps = {
            imsOrg: 'example-ims@AdobeOrg',
            imsToken: "example-imsToken",
            apiKey: "example-apiKey-associated-with-imsOrg",
            handleSelection: (fragmentss: SelectedFragmentType[]) => {},
        };
        // Call the `renderFragmentSelector` available in PureJSContentFragmentSelectors globals to render FragmenttSelector
        PureJSContentFragmentSelectors.renderFragmentSelector(container, fragmentSelectorProps);
    </script>
</head>

<body>
    <div id="fragment-selector-container" style="height: calc(100vh - 80px); width: calc(100vw - 60px); margin: -20px;">
    </div>
</body>

</html>
```

### ImsAuthProps {#imsauthprops}

Egenskaperna `ImsAuthProps` definierar autentiseringsinformationen och det flöde som väljaren för innehållsfragment använder för att hämta en `imsToken`. Genom att ange dessa egenskaper kan du styra hur autentiseringsflödet fungerar och registrera avlyssnare för olika autentiseringshändelser.

Egenskapsinformation finns i [Egenskaper för ImsAuthProps](/help/headless/content-fragment-selector/properties.md#imsauthprops-properties)

### ImsAuthService {#imsauthservice}

Klassen `ImsAuthService` hanterar autentiseringsflödet för fragmentväljaren. Det ansvarar för att erhålla en `imsToken` från Adobe IMS-autentiseringstjänsten. `imsToken` används för att autentisera användaren och auktorisera åtkomst till AEM as a Cloud Service-databasen. `ImsAuthService` använder egenskaperna `ImsAuthProps` för att styra autentiseringsflödet och registrera avlyssnare för olika autentiseringshändelser. Du kan använda funktionen `registerFragmentsSelectorsAuthService` för att registrera instansen `ImsAuthService` med fragmentväljaren. Följande funktioner är tillgängliga för klassen `ImsAuthService`. Om du använder funktionen `registerFragmentsSelectorsAuthService` behöver du dock inte anropa dessa funktioner direkt.

Egenskapsinformation finns i [Egenskaper för ImsAuthService](/help/headless/content-fragment-selector/properties.md#imsauthservice-properties)

### Validering med tillhandahållen IMS-token {#validation-with-provided-ims-token}

```javascript
<script>
    const apiToken="<valid IMS token>";
    function handleSelection(selection) {
    console.log("Selected fragment: ", selection);
    };
    function renderFragmentSelectorInline() {
    console.log("initializing Fragment Selector");
    const props = {
    "repositoryId": "delivery-p64502-e544757.adobeaemcloud.com",
    "apiKey": "ngdm_test_client",
    "imsOrg": "<IMS org>",
    "imsToken": apiToken,
    handleSelection,
    hideTreeNav: true
    }
    const container = document.getElementById('fragment-selector-container');
    PureJSContentFragmentSelectors.renderFragmentSelector(container, props);
    }
    $(document).ready(function() {
    renderFragmentSelectorInline();
    });
</script>
```

### Registrera återanrop till IMS-tjänsten {#register-callbacks-to-ims-service}

```java
// object `imsProps` to be defined as below 
let imsProps = {
    imsClientId: <IMS Client Id>,
        imsScope: "openid",
        redirectUrl: window.location.href,
        modalMode: true,
        adobeImsOptions: {
            modalSettings: {
            allowOrigin: window.location.origin,
},
        useLocalStorage: true,
},
onImsServiceInitialized: (service) => {
            console.log("onImsServiceInitialized", service);
},
onAccessTokenReceived: (token) => {
            console.log("onAccessTokenReceived", token);
},
onAccessTokenExpired: () => {
            console.log("onAccessTokenError");
// re-trigger sign-in flow
},
onErrorReceived: (type, msg) => {
            console.log("onErrorReceived", type, msg);
},
}
```

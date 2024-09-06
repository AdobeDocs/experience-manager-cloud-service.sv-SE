---
title: Resursväljare för  [!DNL Adobe Experience Manager]  som en [!DNL Cloud Service]
description: Integrera resursväljare med olika program från Adobe, andra än Adobe och andra tillverkare.
role: Admin, User
exl-id: 55848de0-aff2-42a0-b959-c771235d9425
source-git-commit: f9f5b2a25933e059cceacf2ba69e23d528858d4b
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 0%

---

# Integrering med ett program som inte är Adobe {#integrate-asset-selector-non-adobe-app}

Med Resursväljaren kan du integrera med olika program från andra tillverkare än Adobe eller från tredje part så att de kan fungera tillsammans sömlöst.

## Förutsättningar {#prereqs-non-adobe-app}

Använd följande förutsättningar om du integrerar resursväljare med ett program som inte är Adobe:

* [Kommunikationsmetoder](/help/assets/overview-asset-selector.md#prereqs)
* imsClientId
* imsScope
* redirectUrl
* imsOrg
* apikey

Resursväljaren stöder autentisering till databasen [!DNL Experience Manager Assets] med hjälp av Identity Management System-egenskaper (IMS) som `imsScope` eller `imsClientID` när du integrerar den med ett program som inte är Adobe.

## Konfigurera resursväljare för ett program som inte är Adobe {#configure-non-adobe-app}

Om du vill konfigurera resursväljaren för ett program som inte är Adobe måste du först logga en supportanmälan för etablering följt av integrationsstegen.

### Logga en supportanmälan {#log-a-support-ticket}

Steg för att logga en supportanmälan via Admin Console:

1. Lägg till **Resursväljaren med AEM Assets** i biljettens titel.

1. Ange följande information i beskrivningen:

   * [!DNL Experience Manager Assets] som en [!DNL Cloud Service]-URL (program-ID och miljö-ID).
   * Domännamn där webbprogrammet som inte kommer från Adobe finns.

## Integreringssteg {#non-adobe-app-integration-steps}

Använd den här exempelfilen `index.html` för autentisering när resursväljaren integreras med ett program som inte är Adobe.

Gå till resursväljarpaketet med taggen `Script`, som visas på *rad 9* till *rad 11* i exempelfilen `index.html`.

*Rad 14* till *rad 38* i exemplet beskriver IMS-flödesegenskaperna, till exempel `imsClientId`, `imsScope` och `redirectURL`. Funktionen kräver att du definierar minst en av egenskaperna `imsClientId` och `imsScope`. Om du inte definierar ett värde för `redirectURL` används den registrerade omdirigerings-URL:en för klient-ID:t.

Eftersom du inte har skapat någon `imsToken` använder du funktionerna `registerAssetsSelectorsAuthService` och `renderAssetSelectorWithAuthFlow`, vilket visas på rad 40 till rad 50 i exempelfilen `index.html`. Använd funktionen `registerAssetsSelectorsAuthService` före `renderAssetSelectorWithAuthFlow` för att registrera `imsToken` med resursväljaren. [!DNL Adobe] rekommenderar att `registerAssetsSelectorsAuthService` anropas när du instansierar komponenten.

Definiera autentiseringen och andra Assets as a Cloud Service åtkomstrelaterade egenskaper i avsnittet `const props`, vilket visas på *rad 54* till *rad 60* i exempelfilen `index.html`.

Den globala variabeln `PureJSSelectors`, som omnämns i *rad 65*, används för att återge resursväljaren i webbläsaren.

Resursväljaren återges på behållarelementet `<div>`, vilket anges på *rad 74* till *rad 81*. I exemplet används en dialogruta för att visa resursväljaren.

```html {line-numbers="true"}
<!DOCTYPE html>
<html>

<head>
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta charset="utf-8">
    <title>Asset Selectors</title>
    <link rel="stylesheet" href="index.css">
    <script id="asset-selector"
        src="https://experience.adobe.com/solutions/CQ-assets-selectors/assets/resources/asset-selectors.js"></script>
    <script>

        const imsProps = {
            imsClientId: "<obtained from IMS team>",
            imsScope: "openid, <other scopes>",
            redirectUrl: window.location.href,
            modalMode: true, // false to open in a full page reload flow
            onImsServiceInitialized: (service) => {
                // invoked when the ims service is initialized and is ready
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

        function load() {
            const registeredTokenService = PureJSSelectors.registerAssetsSelectorsAuthService(imsProps);
            imsInstance = registeredTokenService;
        };

        // initialize the IMS flow before attempting to render the asset selector
        load();
        

        //function that will render the asset selector
            const otherProps = {
            // any other props supported by asset selector
            }
            const assetSelectorProps = {
                "imsOrg": "imsorg",
                ...otherProps
            }
             // container element on which you want to render the AssetSelector/DestinationSelector component
            const container = document.getElementById('asset-selector');

            /// Use the PureJSSelectors in globals to render the AssetSelector/DestinationSelector component
            PureJSSelectors.renderAssetSelectorWithAuthFlow(container, assetSelectorProps, () => {
                const assetSelectorDialog = document.getElementById('asset-selector-dialog');
                assetSelectorDialog.showModal();
            });
        }
    </script>

</head>
<body class="asset-selectors">
    <div>
        <button onclick="renderAssetSelectorWithAuthFlowFlow()">Asset Selector - Select Assets with Ims Flow</button>
    </div>
        <dialog id="asset-selector-dialog">
            <div id="asset-selector" style="height: calc(100vh - 80px); width: calc(100vw - 60px); margin: -20px;">
            </div>
        </dialog>
    </div>
</body>

</html>
```

## Det går inte att komma åt leveransdatabasen {#unable-to-access-delivery-repository}

>[!TIP]
>
>Om du har integrerat resursväljare med hjälp av arbetsflödet Registrera dig för inloggning men fortfarande inte kan komma åt leveransdatabasen, kontrollerar du att cookies i webbläsaren har rensats bort. Annars får du ett `invalid_credentials All session cookies are empty`-fel i konsolen.


---
title: Resursväljare för  [!DNL Adobe Experience Manager]  som en [!DNL Cloud Service]
description: Integrera resursväljare med olika program från Adobe, andra företag än Adobe och tredje part.
role: Admin, User
exl-id: 55848de0-aff2-42a0-b959-c771235d9425
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 0%

---

# Integrering med andra program än Adobe {#integrate-asset-selector-non-adobe-app}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime och Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM Assets-integrering med Edge Delivery Services</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>UI-utökningsbarhet</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Aktivera Dynamic Media Prime och Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>Sök efter bästa praxis</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>Metadata - bästa praxis</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Content Hub</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>Dynamiska media med OpenAPI-funktioner</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>AEM Assets-dokumentation för utvecklare</b></a>
        </td>
    </tr>
</table>

Med Resursväljaren kan du integrera med olika program från andra företag än Adobe eller tredje part så att de kan fungera tillsammans sömlöst.

## Förutsättningar {#prereqs-non-adobe-app}

Använd följande krav om du integrerar resursväljare med ett program som inte är från Adobe:

* [Kommunikationsmetoder](/help/assets/overview-asset-selector.md#prereqs)
* imsClientId
* imsScope
* redirectUrl
* imsOrg
* apikey

Resursväljaren stöder autentisering till databasen [!DNL Experience Manager Assets] med hjälp av Identity Management System-egenskaper (IMS) som `imsScope` eller `imsClientID` när du integrerar den med ett program som inte kommer från Adobe.

## Konfigurera resursväljare för ett icke-Adobe-program {#configure-non-adobe-app}

Om du vill konfigurera resursväljaren för ett program som inte kommer från Adobe måste du först logga en supportanmälan för etablering följt av integrationsstegen.

### Logga en supportanmälan {#log-a-support-ticket}

Steg för att logga en supportanmälan via Admin Console:

1. Lägg till **Resursväljaren med AEM Assets** i biljettens titel.

1. Ange följande information i beskrivningen:

   * [!DNL Experience Manager Assets] som en [!DNL Cloud Service]-URL (program-ID och miljö-ID).
   * Domännamn där webbprogrammet som inte kommer från Adobe finns.

## Integreringssteg {#non-adobe-app-integration-steps}

Använd den här exempelfilen `index.html` för autentisering när resursväljaren integreras med ett program som inte är från Adobe.

Gå till resursväljarpaketet med taggen `Script`, som visas på *rad 9* till *rad 11* i exempelfilen `index.html`.

*Rad 14* till *rad 38* i exemplet beskriver IMS-flödesegenskaperna, till exempel `imsClientId`, `imsScope` och `redirectURL`. Funktionen kräver att du definierar minst en av egenskaperna `imsClientId` och `imsScope`. Om du inte definierar ett värde för `redirectURL` används den registrerade omdirigerings-URL:en för klient-ID:t.

Eftersom du inte har skapat någon `imsToken` använder du funktionerna `registerAssetsSelectorsAuthService` och `renderAssetSelectorWithAuthFlow`, vilket visas på rad 40 till rad 50 i exempelfilen `index.html`. Använd funktionen `registerAssetsSelectorsAuthService` före `renderAssetSelectorWithAuthFlow` för att registrera `imsToken` med resursväljaren. [!DNL Adobe] rekommenderar att `registerAssetsSelectorsAuthService` anropas när du instansierar komponenten.

Definiera autentiseringen och andra åtkomstrelaterade egenskaper för Assets as a Cloud Service i avsnittet `const props`, vilket visas på *rad 54* till *rad 60* i exempelfilen `index.html`.

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
        src="https://experience.adobe.com/solutions/CQ-assets-selectors/static-assets/resources/assets-selectors.js"></script>
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

>[!MORELIKETHIS]
>
>* [Integrera resursväljare med olika program](/help/assets/integrate-asset-selector.md)
>* [Egenskaper för resursväljare](/help/assets/asset-selector-properties.md)
>* [Integrera resursväljare med dynamiska media med OpenAPI-funktioner](/help/assets/integrate-asset-selector-dynamic-media-open-api.md)
>* [Anpassningar av resursväljare](/help/assets/asset-selector-customization.md)

---
title: Resursväljare för [!DNL Adobe Experience Manager] som [!DNL Cloud Service]
description: Använd resursväljaren för att söka efter, hitta och hämta resursers metadata och återgivningar i programmet.
contentOwner: KK
role: Admin,User
exl-id: b968f63d-99df-4ec6-a9c9-ddb77610e258
source-git-commit: b9fe6f4c2f74d5725575f225f8d9eb2e5fbfceb7
workflow-type: tm+mt
source-wordcount: '3896'
ht-degree: 0%

---


# Mikrofrontsväljare för mediefiler {#Overview}

Micro-Frontend Asset Selector har ett användargränssnitt som enkelt kan integreras med [!DNL Experience Manager Assets] -databas så att du kan bläddra bland eller söka efter digitala resurser som är tillgängliga i databasen och använda dem när du redigerar program.

Användargränssnittet Micro-FrontEnd är tillgängligt i ditt program med hjälp av paketet Resursväljare. Alla uppdateringar av paketet importeras automatiskt och den senaste distribuerade resursväljaren läses in automatiskt i programmet.

![Översikt](assets/overview.png)

Resursväljaren har många fördelar, till exempel:

* Enkel integrering med någon av [Adobe](#asset-selector-ims) eller [ej Adobe](#asset-selector-non-ims) program som använder Vanilla JavaScript-bibliotek.
* Enkelt att underhålla när uppdateringar av resursväljarpaketet automatiskt distribueras till resursväljaren som är tillgänglig för ditt program. Det finns inga uppdateringar som behövs i programmet för att läsa in de senaste ändringarna.
* Enkel anpassning eftersom det finns tillgängliga egenskaper som styr visningen av resursväljaren i programmet.
* Fulltextsökning, färdiga och anpassade filter för att snabbt navigera till material som ska användas i redigeringsmiljön.
* Möjlighet att växla databaser inom en IMS-organisation för val av resurser.
* Möjlighet att sortera resurser efter namn, dimensioner och storlek och visa dem i List-, Grid-, Gallery- eller Waterfall-vyn.

<!--Perform the following tasks to integrate and use Asset Selector with your [!DNL Experience Manager Assets] repository:

1. [Install Asset Selector](#installation)
2. [Integrate Asset Selector using Vanilla JS](#integration-using-vanilla-js)
3. [Use Asset Selector](#using-asset-selector)
-->

<!--
## Setting up Asset Selector {#asset-selector-setup}

![Asset Selector set up](assets/asset-selector-prereqs.png)
-->

## Förutsättningar{#prereqs}

Du måste se till att följande kommunikationsmetoder används:

* Programmet körs på HTTPS.
* Programmets URL finns i IMS-klientens tillåtelselista i omdirigerings-URL:er.
* Inloggningsflödet för IMS konfigureras och återges med hjälp av en popup-meny i webbläsaren. Därför bör popup-fönster vara aktiverade eller tillåtna i målwebbläsaren.

Använd ovanstående krav om du behöver arbetsflöde för IMS-autentisering för resursväljaren. Om du redan är autentiserad med IMS-arbetsflödet kan du lägga till IMS-informationen i stället.

>[!IMPORTANT]
>
> Denna databas är avsedd att fungera som kompletterande dokumentation som beskriver tillgängliga API:er och användningsexempel för integrering av resursväljare. Innan du försöker installera eller använda resursväljaren måste du se till att din organisation har fått tillgång till resursväljaren som en del av Experience Manager Assets as a Cloud Service profil. Om du inte har etablerats kan du inte integrera eller använda dessa komponenter. Om du vill begära etablering bör din programadministratör skaffa en supportbiljett som är markerad som P2 från Admin Console och innehålla följande information:
>
>* Domännamn där det integrerande programmet finns.
>* Efter etableringen kommer din organisation att få `imsClientId`, `imsScope`och en `redirectUrl` motsvarar de miljöer som krävs för att konfigurera resursväljaren. Utan dessa giltiga egenskaper kan du inte köra installationsstegen.

## Installation {#installation}

Resursväljaren är tillgänglig via både ESM CDN (till exempel [esm.sh](https://esm.sh/)/[skypning](https://www.skypack.dev/)) och [UMD](https://github.com/umdjs/umd) version.

I webbläsare som använder **UMD-version** (rekommenderas):

```
<script src="https://experience.adobe.com/solutions/CQ-assets-selectors/static-assets/resources/assets-selectors.js"></script>

<script>
  const { renderAssetSelector } = PureJSSelectors;
</script>
```

I webbläsare med `import maps` support med **ESM CDN-version**:

```
<script type="module">
  import { AssetSelector } from 'https://experience.adobe.com/solutions/CQ-assets-selectors/static-assets/resources/@assets/selectors/index.js'
</script>
```

I Deno/Webpack Module Federation med **ESM CDN-version**:

```
import { AssetSelector } from 'https://experience.adobe.com/solutions/CQ-assets-selectors/static-assets/resources/@assets/selectors/index.js'
```

## Integrera resursväljare med Vanilla JS {#integration-using-vanilla-js}

Du kan integrera alla [!DNL Adobe] eller program som inte är Adobe med [!DNL Experience Manager Assets] arkivera och välja resurser inifrån programmet. Se [Integrering av resursväljare med olika program](#asset-selector-integration-with-apps).

Integreringen görs genom att importera resursväljarpaketet och ansluta till Assets-as a Cloud Service med hjälp av Vanilla JavaScript-biblioteket. Redigera en `index.html` eller en lämplig fil i programmet för att

* Definiera autentiseringsinformationen
* Åtkomst till den as a Cloud Service resurskatalogen
* Konfigurera visningsegenskaperna för resursväljaren

Du kan utföra autentisering utan att definiera några IMS-egenskaper om:

* Du integrerar en [!DNL Adobe] program på [Enhetligt gränssnitt](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/aem-cloud-service-on-unified-shell.html?lang=en).
* Du har redan en IMS-token genererad för autentisering.

## Integrera resursväljaren med olika program {#asset-selector-integration-with-apps}

Du kan integrera resursväljaren med olika program som:

* [Integrera resursväljaren med en [!DNL Adobe] program](#adobe-app-integration-vanilla)
* [Integrera resursväljare med andra program än Adobe](#adobe-non-app-integration)

>[!BEGINTABS]

<!--Integration with an Adobe application content starts here-->

>[!TAB Integrering med ett Adobe-program]

### Förutsättningar{#prereqs-adobe-app}

Använd följande krav om du integrerar resursväljare med en [!DNL Adobe] program:

* [Kommunikationsmetoder](#prereqs)
* imsOrg
* imsToken
* apikey

### Integrera resursväljaren med en [!DNL Adobe] program {#adobe-app-integration-vanilla}

I följande exempel visas hur resursväljaren används när en [!DNL Adobe] program under Unified Shell eller när du redan har `imsToken` genereras för autentisering.

Inkludera paketet Resursväljare i koden med `script` -tagg, som i _raderna 6-15_ i exemplet nedan. När skriptet har lästs in visas `PureJSSelectors` global variabel är tillgänglig för användning. Definiera resursväljaren [egenskaper](#asset-selector-properties) som visas i _raderna 16-23_. The `imsOrg` och `imsToken` båda egenskaperna krävs för autentisering i programmet Adobe. The `handleSelection` -egenskapen används för att hantera de valda resurserna. Om du vill återge resursväljaren anropar du `renderAssetSelector` funktionen enligt _rad 17_. Resursväljaren visas i `<div>` behållarelement, som visas i _raderna 21 och 22_.

Följ de här stegen för att använda resursväljaren tillsammans med [!DNL Adobe] program.

```html {line-numbers="true"}
<!DOCTYPE html>
<html>
<head>
    <title>Asset Selector</title>
    <script src="https://experience.adobe.com/solutions/CQ-assets-selectors/assets/resources/assets-selectors.js"></script>
    <script>
        // get the container element in which we want to render the AssetSelector component
        const container = document.getElementById('asset-selector-container');
        // imsOrg and imsToken are required for authentication in Adobe application
        const assetSelectorProps = {
            imsOrg: 'example-ims@AdobeOrg',
            imsToken: "example-imsToken",
            apiKey: "example-apiKey-associated-with-imsOrg",
            handleSelection: (assets: SelectedAssetType[]) => {},
        };
        // Call the `renderAssetSelector` available in PureJSSelectors globals to render AssetSelector
        PureJSSelectors.renderAssetSelector(container, assetSelectorProps);
    </script>
</head>

<body>
    <div id="asset-selector-container" style="height: calc(100vh - 80px); width: calc(100vw - 60px); margin: -20px;">
    </div>
</body>

</html>
```

<!--For detailed example, visit [Asset Selector Code Example](https://github.com/adobe/aem-assets-selectors-mfe-examples).-->

+++**ImsAuthProps**
The `ImsAuthProps` egenskaper definierar autentiseringsinformationen och flödet som resursväljaren använder för att få en `imsToken`. Genom att ange dessa egenskaper kan du styra hur autentiseringsflödet ska fungera och registrera avlyssnare för olika autentiseringshändelser.

| Egenskapsnamn | Beskrivning |
|---|---|
| `imsClientId` | Ett strängvärde som representerar det IMS-klient-ID som används för autentisering. Detta värde tillhandahålls av Adobe och är specifikt för din Adobe AEM CS-organisation. |
| `imsScope` | Beskriver de scope som används vid autentisering. Omfattningarna avgör vilken åtkomstnivå programmet har till organisationens resurser. Flera omfång kan avgränsas med kommatecken. |
| `redirectUrl` | Representerar den URL där användaren omdirigeras efter autentiseringen. Det här värdet ställs vanligtvis in på programmets aktuella URL. Om en `redirectUrl` inte tillhandahålls, `ImsAuthService` använder den redirectUrl som används för att registrera `imsClientId` |
| `modalMode` | Ett booleskt värde som anger om autentiseringsflödet ska visas i ett modalt (popup) eller inte. Om inställt på `true`visas autentiseringsflödet i ett popup-fönster. Om inställt på `false`, visas autentiseringsflödet i en helsidesinläsning. _Obs!_ för bättre användargränssnitt kan du dynamiskt styra det här värdet om användaren har inaktiverat popup-fönster i webbläsaren. |
| `onImsServiceInitialized` | En callback-funktion som anropas när Adobe IMS-autentiseringstjänsten initieras. Den här funktionen har en parameter, `service`, som är ett objekt som representerar Adobe IMS-tjänsten. Se [`ImsAuthService`](#imsauthservice-ims-auth-service) för mer information. |
| `onAccessTokenReceived` | En callback-funktion som anropas när en `imsToken` tas emot från Adobe IMS-autentiseringstjänsten. Den här funktionen har en parameter, `imsToken`, som är en sträng som representerar åtkomsttoken. |
| `onAccessTokenExpired` | En återanropsfunktion som anropas när en åtkomsttoken har upphört att gälla. Den här funktionen används vanligtvis för att utlösa ett nytt autentiseringsflöde för att erhålla en ny åtkomsttoken. |
| `onErrorReceived` | En återanropsfunktion som anropas när ett fel inträffar under autentiseringen. Den här funktionen har två parametrar: feltypen och felmeddelandet. Feltypen är en sträng som representerar feltypen och felmeddelandet är en sträng som representerar felmeddelandet. |

+++

+++**ImsAuthService**
`ImsAuthService` -klassen hanterar autentiseringsflödet för resursväljaren. Den ansvarar för att erhålla en `imsToken` från Adobe IMS-autentiseringstjänsten. The `imsToken` används för att autentisera användaren och ge behörighet till [!DNL Adobe Experience Manager] som [!DNL Cloud Service] Resurskatalog. ImsAuthService använder `ImsAuthProps` egenskaper för att styra autentiseringsflödet och registrera avlyssnare för olika autentiseringshändelser. Du kan använda det praktiska [`registerAssetsSelectorsAuthService`](#purejsselectorsregisterassetsselectorsauthservice) för att registrera _ImsAuthService_ -instans med resursväljaren. Följande funktioner är tillgängliga på `ImsAuthService` klassen. Om du använder _registerAssetsSelectorsAuthService_ behöver du inte anropa dessa funktioner direkt.

| Funktionsnamn | Beskrivning |
|---|---|
| `isSignedInUser` | Avgör om användaren är inloggad på tjänsten och returnerar ett booleskt värde i enlighet med detta. |
| `getImsToken` | Hämtar autentiseringen `imsToken` för den inloggade användaren, som kan användas för att autentisera begäranden till andra tjänster, som att generera resurs_rendering. |
| `signIn` | Initierar inloggningsprocessen för användaren. Den här funktionen använder `ImsAuthProps` för att visa autentisering i antingen ett popup-fönster eller en helsidesinläsning |
| `signOut` | Signerar användaren från tjänsten, gör sin autentiseringstoken ogiltig och kräver att han/hon loggar in igen för att få åtkomst till skyddade resurser. Om du anropar den här funktionen läses den aktuella sidan in igen. |
| `refreshToken` | Uppdaterar autentiseringstoken för den inloggade användaren, vilket förhindrar att den upphör att gälla och säkerställer oavbruten åtkomst till skyddade resurser. Returnerar en ny autentiseringstoken som kan användas för efterföljande begäranden. |

+++

+++**Validering med tillhandahållen IMS-token**

```
<script>
    const apiToken="<valid IMS token>";
    function handleSelection(selection) {
    console.log("Selected asset: ", selection);
    };
    function renderAssetSelectorInline() {
    console.log("initializing Asset Selector");
    const props = {
    "repositoryId": "delivery-p64502-e544757.adobeaemcloud.com",
    "apiKey": "ngdm_test_client",
    "imsOrg": "<IMS org>",
    "imsToken": apiToken,
    handleSelection,
    hideTreeNav: true
    }
    const container = document.getElementById('asset-selector-container');
    PureJSSelectors.renderAssetSelector(container, props);
    }
    $(document).ready(function() {
    renderAssetSelectorInline();
    });
</script>
```

+++

+++**Registrera återanrop till IMS-tjänsten**

```
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

+++

<!--Integration with non-Adobe application content starts here-->

>[!TAB Integrering med ett program som inte är Adobe]

<!--### Integrate Asset Selector with a [!DNL non-Adobe] application {#adobe-non-app-integration}-->

### Förutsättningar {#prereqs-non-adobe-app}

Använd följande förutsättningar om du integrerar resursväljare med ett program som inte är Adobe:

* [Kommunikationsmetoder](#prereqs)
* imsClientId
* imsScope
* redirectUrl
* imsOrg
* apikey

Resursväljaren stöder autentisering till [!DNL Experience Manager Assets] databas med hjälp av Identity Management System-egenskaper (IMS) som `imsScope` eller `imsClientID` när du integrerar det med ett program som inte är Adobe.

+++**Konfigurera resursväljare för ett program som inte är Adobe**
Om du vill konfigurera resursväljaren för ett program som inte är Adobe måste du först logga en supportanmälan för etablering följt av integrationsstegen.

**Logga en supportanmälan**
Steg för att logga en supportanmälan via Admin Console:

1. Lägg till **Resursväljare med AEM Assets** i biljettens titel.

1. Ange följande information i beskrivningen:

   * [!DNL Experience Manager Assets] som [!DNL Cloud Service] URL (program-ID och miljö-ID).
   * Domännamn där webbprogrammet som inte kommer från Adobe finns.
+++

+++**Integreringssteg**
Använd detta exempel `index.html` -fil för autentisering när resursväljaren integreras med ett program som inte är Adobe.

Få åtkomst till resursväljarpaketet med `Script` Tagg, enligt *rad 9* till *rad 11* i exemplet `index.html` -fil.

*Rad 14* till *rad 38* i exemplet beskriver IMS-flödesegenskaperna, som `imsClientId`, `imsScope`och `redirectURL`. Funktionen kräver att du definierar minst en av `imsClientId` och `imsScope` egenskaper. Om du inte definierar ett värde för `redirectURL`används den registrerade omdirigerings-URL:en för klient-ID:t.

Eftersom du inte har en `imsToken` genereras, använder `registerAssetsSelectorsAuthService` och `renderAssetSelectorWithAuthFlow` funktioner, som de visas på rad 40 till rad 50 i exemplet `index.html` -fil. Använd `registerAssetsSelectorsAuthService` function before `renderAssetSelectorWithAuthFlow` för att registrera `imsToken` med resursväljaren. [!DNL Adobe] rekommenderar anrop `registerAssetsSelectorsAuthService` när du instansierar komponenten.

Definiera autentiseringen och andra as a Cloud Service åtkomstrelaterade egenskaper för Assets i dialogrutan `const props` -avsnitt, vilket visas i *rad 54* till *rad 60* i exemplet `index.html` -fil.

The `PureJSSelectors` global variabel, omnämns i *rad 65*, används för att återge resursväljaren i webbläsaren.

Resursväljaren återges på `<div>` behållarelement, enligt *rad 74* till *rad 81*. I exemplet används en dialogruta för att visa resursväljaren.

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

+++

+++**Det går inte att komma åt leveransdatabasen**

>[!TIP]
>
>Om du har integrerat resursväljare med hjälp av arbetsflödet Registrera dig för inloggning men fortfarande inte kan komma åt leveransdatabasen, kontrollerar du att cookies i webbläsaren har rensats bort. Annars slutar det med att `invalid_credentials All session cookies are empty` fel i konsolen.

>[!ENDTABS]

## Egenskaper för resursväljare {#asset-selector-properties}

Du kan använda egenskaperna för resursväljaren för att anpassa hur resursväljaren återges. I följande tabell visas de egenskaper som du kan använda för att anpassa och använda resursväljaren.

| Egenskap | Typ | Obligatoriskt | Standard | Beskrivning |
|---|---|---|---|---|
| *järnväg* | boolesk | Nej | false | Om markerad `true`, återges resursväljaren i en vy med vänster skena. Om den är markerad `false`, återges resursväljaren i modal vy. |
| *imsOrg* | string | Ja | | IMS-ID (Adobe Identity Management System) som tilldelas vid etablering [!DNL Adobe Experience Manager] som [!DNL Cloud Service] för er organisation. The `imsOrg` Nyckeln krävs för att verifiera om den organisation du använder är under Adobe IMS eller inte. |
| *imsToken* | string | Nej | | IMS-innehavartoken används för autentisering. `imsToken` krävs om du använder en [!DNL Adobe] program för integreringen. |
| *apiKey* | string | Nej | | API-nyckel som används för åtkomst till AEM. `apiKey` krävs om du använder en [!DNL Adobe] programintegrering. |
| *rootPath* | string | Nej | /content/dam/ | Mappsökväg där resursväljaren visar dina resurser. `rootPath` kan också användas i form av inkapsling. Med följande sökväg `/content/dam/marketing/subfolder/`kan du inte bläddra igenom någon överordnad mapp, utan bara visa de underordnade mapparna. |
| *bana* | string | Nej | | Sökväg som används för att navigera till en viss katalog med resurser när resursväljaren återges. |
| *filterSchema* | array | Nej | | Modell som används för att konfigurera filteregenskaper. Detta är användbart när du vill begränsa vissa filteralternativ i Resursväljaren. |
| *filterFormProps* | Objekt | Nej | | Ange de filteregenskaper som du behöver använda för att förfina sökningen. Exempel: MIME-typ JPG, PNG, GIF. |
| *selectedAssets* | Array `<Object>` | Nej |                 | Ange valda resurser när resursväljaren återges. Det krävs en array med objekt som innehåller en id-egenskap för resurserna. Till exempel: `[{id: 'urn:234}, {id: 'urn:555'}]` En resurs måste vara tillgänglig i den aktuella katalogen. Om du behöver använda en annan katalog anger du ett värde för `path` också. |
| *acvConfig* | Objekt | Nej | | Resurssamlingens visningsegenskap som innehåller objekt med anpassad konfiguration som åsidosätter standardvärden. Den här egenskapen används också med `rail` för att aktivera spårningsvisning av resursvyn. |
| *i18nSymboler* | `Object<{ id?: string, defaultMessage?: string, description?: string}>` | Nej |                 | Om OTB-översättningarna inte är tillräckliga för ditt programs behov kan du visa ett gränssnitt genom vilket du kan skicka dina egna anpassade, lokaliserade värden via `i18nSymbols` prop. Om du skickar ett värde genom det här gränssnittet åsidosätts standardöversättningarna och i stället används dina egna. Om du vill utföra åsidosättningen måste du skicka en giltig [Meddelandebeskrivning](https://formatjs.io/docs/react-intl/api/#message-descriptor) objekt till nyckeln för `i18nSymbols` som du vill åsidosätta. |
| *intl* | Objekt | Nej | | Resursväljaren innehåller OOTB-standardöversättningar. Du kan välja översättningsspråk genom att ange en giltig språksträng via `intl.locale` prop. Till exempel: `intl={{ locale: "es-es" }}` </br></br> De språksträngar som stöds följer [ISO 639 - Koder](https://www.iso.org/iso-639-language-codes.html) för representation av namn på språkstandarder. </br></br> Lista över språk som stöds: engelska - en-us (standard) spanska - es-es&#39; German - de-de&#39; French - fr-fr&#39; Italian - it-it&#39; Japanese - ja-jp&#39; Korean - ko-kr&#39; Portuguese - pt-br&#39; Chinese (Traditional) - zh-cn&#39; Chinese (Taiwan) - zh-tw |
| *databaseId* | string | Nej | &#39; | Databas från vilken resursväljaren läser in innehållet. |
| *additionalAemSolutions* | `Array<string>` | Nej | [ ] | Här kan du lägga till en lista med ytterligare AEM. Om ingen information anges i den här egenskapen beaktas endast mediebibliotek eller AEM Assets-databaser. |
| *hideTreeNav* | boolesk | Nej |  | Anger om navigeringssidofältet för resursträd ska visas eller döljas. Den används endast i modal vy och därför har den här egenskapen ingen effekt i järnvägsvy. |
| *onDrop* | Funktion | Nej | | Egenskapen gör att en resurs kan släppas. |
| *dropOptions* | `{allowList?: Object}` | Nej | | Konfigurerar släppningsalternativ med tillåtelselista. |
| *colorScheme* | string | Nej | | Konfigurera tema (`light` eller `dark`) för resursväljaren. |
| *handleSelection* | Funktion | Nej | | Anropas med en array med tillgångsobjekt när resurser är markerade och `Select` klickar du på spärrknappen. Den här funktionen anropas bara i modal vy. För järnvägsvy använder du `handleAssetSelection` eller `onDrop` funktioner. Exempel: <pre>handleSelection=(assets: Asset[])=> {..}</pre> Se [Markerad resurstyp](#selected-asset-type) för mer information. |
| *handleAssetSelection* | Funktion | Nej | | Anropas med en array med objekt när resurserna markeras eller avmarkeras. Detta är användbart när du vill lyssna efter resurser när användaren väljer dem. Exempel: <pre>handleSelection=(assets: Asset[])=> {..}</pre> Se [Markerad resurstyp](#selected-asset-type) för mer information. |
| *onClose* | Funktion | Nej | | Anropas när `Close` knappen i modal vy trycks ned. Detta anropas bara `modal` visa och ignorera i `rail` vy. |
| *onFilterSubmit* | Funktion | Nej | | Anropas med filterobjekt när användaren ändrar olika filtervillkor. |
| *selectionType* | string | Nej | enkel | Konfiguration för `single` eller `multiple` urval av resurser i taget. |
| *dragOptions.tillåtelselista* | boolesk | Nej | | Egenskapen används för att tillåta eller neka att resurser som inte kan markeras dras. |
| *aemTierType* | string | Nej | | Du kan välja om du vill visa resurser från leveransnivå, författarnivå eller både och. <br><br> Syntax: `aemTierType:[0: "author" 1: "delivery"` <br><br> Om till exempel båda `["author","delivery"]` används, visar databasväljaren alternativ för både författare och leverans. |
| *handleNavigateToAsset* | Funktion | Nej | | Det är en återanropsfunktion som hanterar markering av en resurs. |
| *noWrap* | boolesk | Nej | | The *noWrap* Egenskapen hjälper till att återge resursväljaren på sidopanelen. Om den här egenskapen inte nämns återges *Dialogrutevy* som standard. |
| *dialogSize* | liten, medelstor, stor, helskärmsbild eller helskärmsövergång | Sträng | Valfritt | Du kan styra layouten genom att ange dess storlek med de angivna alternativen. |
| *colorScheme* | ljus eller mörk | Nej | | Den här egenskapen används för att ange temat för ett resursväljarprogram. Du kan välja mellan ljust eller mörkt tema. |
| *filterRepoList* | Funktion | Nej |  | Du kan använda `filterRepoList` callback-funktion som anropar Experience Manager-databas och returnerar en filtrerad lista med databaser. |

## Exempel på hur du använder egenskaper för resursväljare {#usage-examples}

Du kan definiera resursväljaren [egenskaper](#asset-selector-properties) i `index.html` om du vill anpassa visningen av resursväljaren i programmet.

### Exempel 1: Resursväljaren i vyn Räler

![rail-view-example](assets/rail-view-example-vanilla.png)

Om värdet för AssetSelector `rail` är inställd på `false` eller inte omnämns i egenskaperna visas resursväljaren som standard i den modulala vyn. The `acvConfig` -egenskapen tillåter vissa ingående konfigurationer, som Dra och släpp. Besök [aktivera eller inaktivera dra och släpp](#enable-disable-drag-and-drop) för att förstå hur `acvConfig` -egenskap.

<!--
### Example 2: Use selectedAssets property in addition to the path property

Use the `path` property to define the folder name that displays automatically when the Asset Selector is rendered. In addition, use the `selectedAssets` property to define the IDs for the assets that you need to select within the folder. Moreover, when you want to display assets that are pre-defined within the folder, you can use selectedAssets property.

   ![selected-assets-example](assets/selected-assets-example-vanilla.png)
-->

### Exempel 2: Metadatapuposer

Använd olika egenskaper för att definiera metadata för en resurs som du vill visa med hjälp av en informationsikon. Info pover innehåller information om resursen eller mappen, inklusive namn, dimensioner, ändringsdatum, plats och beskrivning av en resurs. I exemplet nedan används olika egenskaper för att visa metadata för en resurs, till exempel `repo:path` -egenskapen anger platsen för en resurs. <!--`repo` represents the repository from where the asset is showing, whereas, `path` represents the route from where the asset or folder is rendered.-->

![metadata-pover-exempel](assets/metadata-popover.png)

### Exempel 3: Egen filteregenskap i skenvy

Förutom den facetterade sökningen kan du med Resursväljaren anpassa olika attribut för att begränsa sökningen från [!DNL Adobe Experience Manager] som [!DNL Cloud Service] program. Lägg till följande kod för att lägga till anpassade sökfilter i programmet. I exemplet nedan är `Type Filter` sökning som filtrerar resurstypen bland bilder, dokument eller videoklipp eller den filtertyp som du har lagt till för sökningen.

![custom-filter-example-vanilla](assets/custom-filter-example-vanilla.png)

<!--

## Customization after integrating Asset Selector 

### Custom metadata

Assets display panel shows the out of the box metadata that can be displayed in the info of the asset. In addition to this, [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] application allows configuration of the asset selector by adding custom metadata that is shown in info panel of the asset.
-->

## Funktionskodfragment{#code-snippets}

Definiera förutsättningarna i `index.html` -filen eller en liknande fil i programimplementeringen för att definiera autentiseringsinformationen för att komma åt [!DNL Experience Manager Assets] databas. När du är klar kan du lägga till kodfragment efter dina behov.

### Anpassa filterpanelen {#customize-filter-panel}

Du kan lägga till följande kodfragment i `assetSelectorProps` objekt för att anpassa filterpanelen:

```
filterSchema: [
    {
    header: 'File Type',
    groupKey: 'TopGroup',
    fields: [
    {
    element: 'checkbox',
    name: 'type',
    options: [
    {
    label: 'Images',
    value: '<comma separated mimetypes, without space, that denote all images, for e.g., image/>',
    },
    {
    label: 'Videos',
    value: '<comma separated mimetypes, without space, that denote all videos for e.g., video/,model/vnd.mts,application/mxf>'
    }
    ]
    }
    ]
    },
    {
    fields: [
    {
    element: 'checkbox',
    name: 'type',
    options: [
    { label: 'JPG', value: 'image/jpeg' },
    { label: 'PNG', value: 'image/png' },
    { label: 'TIFF', value: 'image/tiff' },
    { label: 'GIF', value: 'image/gif' },
    { label: 'MP4', value: 'video/mp4' }
    ],
    columns: 3,
    },
    ],
    header: 'Mime Types',
    groupKey: 'MimeTypeGroup',
    }},
    {
    fields: [
    {
    element: 'checkbox',
    name: 'property=metadata.application.xcm:keywords.value',
    options: [
    { label: 'Fruits', value: 'fruits' },
    { label: 'Vegetables', value: 'vegetables'}
    ],
    columns: 3,
    },
    ],
    header: 'Food Category',
    groupKey: 'FoodCategoryGroup',
    }
],
```

### Anpassa information i modal vy {#customize-info-in-modal-view}

Du kan anpassa detaljvyn för en resurs när du klickar på ![informationsikon](assets/info-icon.svg) -ikon. Kör koden nedan:

```
// Create an object infoPopoverMap and set the property `infoPopoverMap` with it in assetSelectorProps
const infoPopoverMap = (map) => {
// for example, to skip `path` from the info popover view
let defaultPopoverData = PureJSSelectors.getDefaultInfoPopoverData(map);
return defaultPopoverData.filter((i) => i.label !== 'Path'
};
assetSelectorProps.infoPopoverMap = infoPopoverMap;
```

### Aktivera eller inaktivera dra och släpp-läge {#enable-disable-drag-and-drop}

Lägg till följande egenskaper i `assetSelectorProp` för att aktivera dra och släpp-läge. Om du vill inaktivera dra och släpp ersätter du `true` parameter med `false`.

```
rail: true,
acvConfig: {
dragOptions: {
allowList: {
'*': true,
},
},
selectionType: 'multiple'
}

// the drop handler to be implemented
function drop(e) {
e.preventDefault();
// following helps you get the selected assets – an array of objects.
const data = JSON.parse(e.dataTransfer.getData('collectionviewdata'));
}
```

### Val av tillgångar {#selection-of-assets}

Den valda resurstypen är en array med objekt som innehåller resursinformationen när resursen används `handleSelection`, `handleAssetSelection`och `onDrop` funktioner.

Utför följande steg för att konfigurera valet av en eller flera resurser:

```
acvConfig: {
selectionType: 'multiple' // 'single' for single selection
}
// the `handleSelection` callback, always gets you the array of selected assets
```

**Schemasyntax**

```
interface SelectedAsset {
    'repo:id': string;
    'repo:name': string;
    'repo:path': string;
    'repo:size': number;
    'repo:createdBy': string;
    'repo:createDate': string;
    'repo:modifiedBy': string; 
    'repo:modifyDate': string; 
    'dc:format': string; 
    'tiff:imageWidth': number;
    'tiff:imageLength': number;
    'repo:state': string;
    computedMetadata: Record<string, any>;
    _links: {
        'http://ns.adobe.com/adobecloud/rel/rendition': Array<{
            href: string;
            type: string;
            'repo:size': number;
            width: number;
            height: number;
            [others: string]: any;
        }>;
    };
}
```

I följande tabell beskrivs några av de viktiga egenskaperna för det valda resursobjektet.

| Egenskap | Typ | Beskrivning |
|---|---|---|
| *repo:databaseId* | string | Unik identifierare för databasen där resursen lagras. |
| *repo:id* | string | Unik identifierare för tillgången. |
| *repo:assetClass* | string | Klassificeringen av resursen (till exempel bild eller video, dokument). |
| *repo:name* | string | Namnet på resursen, inklusive filtillägget. |
| *repo:storlek* | tal | Resursens storlek i byte. |
| *repo:sökväg* | string | Platsen för resursen i databasen. |
| *repo:överordnade* | `Array<string>` | En array med överordnade objekt för resursen i databasen. |
| *repo:läge* | string | Aktuellt läge för resursen i databasen (t.ex. aktiv, borttagen och så vidare). |
| *repo:createdBy* | string | Användaren eller systemet som skapade resursen. |
| *repa:createDate* | string | Datum och tid då tillgången skapades. |
| *repo:modifiedBy* | string | Den användare eller det system som senast ändrade resursen. |
| *repo:modifyDate* | string | Datum och tid då tillgången senast ändrades. |
| *dc:format* | string | Resursens format, till exempel filtypen (till exempel JPEG, PNG och så vidare). |
| *tiff:imageWidth* | tal | Bredden på en resurs. |
| *tiff:imageLength* | tal | En tillgångs höjd. |
| *computedMetadata* | `Record<string, any>` | Ett objekt som representerar en bucket för alla resursens metadata av alla slag (databas, program eller inbäddade metadata). |
| *länkar* | `Record<string, any>` | Hypermedialänkar för den associerade resursen. Innehåller länkar för resurser som metadata och återgivningar. |
| *_länkar.<http://ns.adobe.com/adobecloud/rel/rendition>* | `Array<Object>` | En array med objekt som innehåller information om återgivningar av resursen. |
| *_länkar.<http://ns.adobe.com/adobecloud/rel/rendition[].href>* | string | URI:n till återgivningen. |
| *_länkar.<http://ns.adobe.com/adobecloud/rel/rendition[].type>* | string | Återgivningens MIME-typ. |
| *_länkar.<http://ns.adobe.com/adobecloud/rel/rendition[].'repo:size>&#39;* | tal | Återgivningens storlek i byte. |
| *_länkar.<http://ns.adobe.com/adobecloud/rel/rendition[].width>* | tal | Återgivningens bredd. |
| *_länkar.<http://ns.adobe.com/adobecloud/rel/rendition[].height>* | tal | Återgivningens höjd. |

En fullständig lista över egenskaper och detaljerade exempel finns på [Exempel på resursväljarkod](https://github.com/adobe/aem-assets-selectors-mfe-examples).

## Hantera urval av resurser med objektschema {#handling-selection}

The `handleSelection` -egenskapen används för att hantera ett eller flera urval av resurser i Resursväljaren. I exemplet nedan anges syntaxen för användning av `handleSelection`.

![handtag-markering](assets/handling-selection.png)

## Inaktivera urval av resurser {#disable-selection}

Inaktivera markering används för att dölja eller inaktivera att resurser eller mappar kan markeras. Den döljer kryssrutan välj från kortet eller resursen som inte gör att den markeras. Om du vill använda den här funktionen kan du deklarera positionen för en resurs eller mapp som du vill inaktivera i en array. Om du till exempel vill inaktivera valet av en mapp som visas vid den första positionen kan du lägga till följande kod:
`disableSelection: [0]:folder`

Du kan förse arrayen med en lista med MIME-typer (till exempel bild, mapp, fil eller andra MIME-typer, till exempel image/jpeg) som du vill inaktivera. Mime-typerna som du deklarerar mappas till `data-card-type` och `data-card-mimetype` attribut för en resurs.

Dessutom kan resurser med inaktiverad markering dras. Om du vill inaktivera dra och släpp av en viss resurstyp kan du använda `dragOptions.allowList` -egenskap.

Syntaxen för inaktiverad markering är följande:

```
(args)=> {
    return(
        <ASDialogWrapper
            {...args}
            disableSelection={args.disableSelection}
            handleAssetSelection={action('handleAssetSelection')}
            handleSelection={action('handleSelection')}
            selectionType={args.selectionType}
        />
    );
}
```

>[!NOTE]
>
> Om det gäller en resurs är kryssrutan select dold, men om det gäller en mapp går det inte att markera mappen, men navigeringen för den aktuella mappen visas fortfarande.

## Använda resursväljare {#using-asset-selector}

När resursväljaren har konfigurerats och du autentiserats för att använda resursväljaren med [!DNL Adobe Experience Manager] som [!DNL Cloud Service] kan du välja resurser eller utföra olika åtgärder för att söka efter dina resurser i databasen.

![using-asset-selector](assets/using-asset-selector.png)

* **A**: [Visa/dölj panelen](#hide-show-panel)
* **B**: [Databasväxlare](#repository-switcher)
* **C**: [Resurser](#repository)
* **D**: [Filter](#filters)
* **E**: [Sökfältet](#search-bar)
* **F**: [Sortering](#sorting)
* **G**: [Sortera i stigande eller fallande ordning](#sorting)
* **H**: [Visa](#types-of-view)

### Visa/dölj panelen {#hide-show-panel}

Om du vill dölja mappar i den vänstra navigeringen klickar du på **[!UICONTROL Hide folders]** -ikon. Om du vill ångra ändringarna klickar du på **[!UICONTROL Hide folders]** ikonen igen.

### Databasväxlare {#repository-switcher}

Med Resursväljaren kan du också växla databaser för val av resurser. Du kan välja vilken databas du vill använda i listrutan som finns i den vänstra panelen. De databasalternativ som är tillgängliga i listrutan baseras på `repositoryId` egenskap som definieras i `index.html` -fil. Den baseras på miljön från den valda IMS-organisationen som den inloggade användaren har åtkomst till. Konsumenterna kan välja `repositoryID` och i så fall slutar resursväljaren återge repomkopplaren och återger resurser endast från den angivna databasen.
<!--
It is based on the `imsOrg` that is provided in the application. If you want to see the list of repositories, then `repositoryId` is required to view those specific repositories in your application.
-->

### Resurskatalog

Det är en samling resursmappar som du kan använda för att utföra åtgärder.

### Färdiga filter {#filters}

Resursväljaren innehåller även färdiga filteralternativ som kan förfina sökresultaten. Följande filter är tillgängliga:

* `File type`: innehåller mapp, fil, bilder, dokument eller video
* `MIME type`: omfattar JPG, GIF, PPTX, PNG, MP4, DOCX, TIFF, PDF, XLSX
* `Image Size`: innehåller minsta/högsta bredd, minsta/högsta höjd för bilden

  ![rail-view-example](assets/filters-asset-selector.png)

### Anpassad sökning

Förutom textsökningen kan du med Resursväljaren söka efter resurser i filer med hjälp av anpassad sökning. Du kan använda anpassade sökfilter både i den modulala vyn och i vyn Rail.

![anpassad sökning](assets/custom-search1.png)

Du kan också skapa standardsökfilter för att spara de fält som du ofta söker efter och använda dem senare. Om du vill skapa en anpassad sökning efter dina resurser kan du använda `filterSchema` -egenskap.

### Sökfältet {#search-bar}

Med Resursväljaren kan du utföra fullständig textsökning av resurser i den valda databasen. Om du till exempel skriver nyckelordet `wave` i sökfältet, alla resurser som har `wave` nyckelord som nämns i någon av metadataegenskaperna visas.

### Sortering {#sorting}

Du kan sortera resurser i Resursväljaren efter namn, dimensioner eller storlek för en resurs. Du kan också sortera resurserna i stigande eller fallande ordning.

### Typer av vy {#types-of-view}

Med Resursväljaren kan du visa resursen i fyra olika vyer:

* **![listvy](assets/do-not-localize/list-view.png)[!UICONTROL List View]**: I listvyn visas rullningsbara filer och mappar i en enda kolumn.
* **![stödrastervy](assets/do-not-localize/grid-view.png)[!UICONTROL Grid View]**: Stödrastervyn visar rullningsbara filer och mappar i ett rutnät med rader och kolumner.
* **![gallerivy](assets/do-not-localize/gallery-view.png)[!UICONTROL Gallery View]**: I gallerivyn visas filer eller mappar i en centrerad vågrät lista.
* **![vattenfallsvy](assets/do-not-localize/waterfall-view.png)[!UICONTROL Waterfall View]**: I vattenfallsvyn visas filer eller mappar i form av en Bridge.

<!--
### Modes to view Asset Selector

Asset Selector supports two types of out of the box views:

**  Modal view or Inline view:** The modal view or inline view is the default view of Asset Selector that represents Assets folders in the front area. The modal view allows users to view assets in a full screen to ease the selection of multiple assets for import. Use `<AssetSelector rail={false}>` to enable modal view.

    ![modal-view](assets/modal-view.png)

**  Rail view:** The rail view represents Assets folders in a left panel. The drag and drop of assets can be performed in this view. Use `<AssetSelector rail={true}>` to enable rail view.

    ![rail-view](assets/rail-view.png)
-->
<!--

### Application Integration

Asset Selector is flexible and can be integrated within your existing [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] application. It is accessible and localized to add, search, and select assets in your application. With Asset Selector you can:
*   **Configure** You can configure the files/folders that you want to show at the upfront. The assets that are chosen to view can be of any supported formats, for example, JPEG. It lets you control the display of various text or symbols as per your choice.
*   **Perfect fit** Asset selector easily fits in your existing [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] application and choose the way you want to view. The mode of view can be inline, rail, or modal view.
*   **Accessible** With Asset Selector, you can reach the desired asset in an easy manner.
*   **Localize** Assets can be availed for the various locales available as per Adobe's localization standards.
-->
<!--

### Support for multiple instances

The micro front-end design supports the display of multiple instances of Asset Selector on a single screen.

![multiple-instance](assets/multiple-instance.png)
-->

<!--

### Controlled selection with multi-select

You can make default multi-selection of assets by specifying the assets to the component using `selectedAssets` property. You should specify an array of asset IDs. For example, `[{id: 'urn:234}, {id: 'urn:555'}].`
-->
<!--

### Action buttons

When you customize your application with Asset Selector based on ReactJS, you are provided with the following action buttons to perform various actions:
*   **Open in media library** Lets you open the asset in media library.
*   **Upload** Lets you upload an asset directly.
*   **Download** Downloads the asset in [!DNL Adobe Experience Manager] as a [!DNL Cloud Service].
-->
<!--

### Status of an asset

Asset Selector lets you know the status of your uploaded assets. The status can be `Approved`, `Rejected`, or `Expired` of the asset. 
-->
<!--

### Localization

The integration of Asset Selector with [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] allows localized content appear in your application.
-->



<!--Best Practice-->
<!--
+++**Control default selection of the filter**
You can make the selection of filter default by implementing the following code snippet:

```
"defaultValue": [
    "image/*",
    "application/*"
],

{
    "label": "Documents",
    "value": "application/*"
}
```

+++
-->

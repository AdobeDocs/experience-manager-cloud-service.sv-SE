---
title: Integrera väljaren för innehållsfragment med program från andra tillverkare än Adobe eller andra
description: Integrera väljaren för innehållsfragment med olika Adobe-, icke-Adobe- och tredjepartsprogram.
role: Admin, User, Developer
source-git-commit: 3af1a89489af96bf9c9908aea7fb20883956517b
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---

# Integrering med andra program än Adobe {#integration-with-non-adobe-application}

Med väljaren för innehållsfragment kan du integrera med olika program från andra företag eller andra företag så att de kan samarbeta smidigt.

## Förutsättningar {#prerequisites}

Använd följande krav om du integrerar Content Fragment Selector med ett program som inte är Adobe:

* [Förutsättningar](/help/headless/content-fragment-selector/overview.md#prerequisites)
* imsClientId
* imsScope
* redirectUrl
* imsOrg
* apikey

När du integrerar det med ett program som inte är från Adobe stöder väljaren för innehållsfragment autentisering till Adobe Experience Manager (AEM) as a Cloud Service-databasen med hjälp av Identity Management System-egenskaper (IMS) som `imsScope` eller `imsClientID`.

## Konfigurera väljaren för innehållsfragment för ett program som inte är Adobe {#configure-content-fragment-selector-for-a-non-adobe-application}

Om du vill konfigurera väljaren för innehållsfragment för ett icke-Adobe-program måste du först logga en supportanmälan för etablering innan du fortsätter med integrationsstegen.

### Logga en supportanmälan {#logging-a-support-ticket}

Steg för att logga en supportanmälan via Admin Console:

1. Lägg till **väljaren för innehållsfragment med AEM Fragments** i biljettens titel.

1. Ange följande information i beskrivningen:

   * Experience Manager as a Cloud Service URL (program-ID och miljö-ID).
   * Domännamn där webbprogrammet som inte kommer från Adobe finns.

## Integreringssteg {#integration-steps}

Använd följande exempelfil `index.html` för autentisering när du integrerar väljaren för innehållsfragment med ett icke-Adobe-program:

* Gå till paketet Content Fragment Selector med taggen `Script`.

* Definiera IMS-flödesegenskaperna, till exempel `imsClientId`, `imsScope` och `redirectURL`.

   * Funktionen kräver att du definierar minst en av egenskaperna `imsClientId` och `imsScope`.
   * Om du inte definierar ett värde för `redirectURL` används den registrerade omdirigerings-URL:en för klient-ID:t.

* Eftersom exemplet inte har genererat `imsToken` använder du funktionerna `registerFragmentsSelectorsAuthService` och `renderFragmentSelectorWithAuthFlow`.

   * Använd funktionen `registerFragmentsSelectorsAuthService` före `renderFragmentSelectorWithAuthFlow` för att registrera `imsToken` med väljaren för innehållsfragment.
   * Adobe rekommenderar att `registerFragmentsSelectorsAuthService` anropas när du instansierar komponenten.

* Definiera autentiseringen och andra fragment as a Cloud Service-åtkomstrelaterade egenskaper i avsnittet `const props`.
* Den globala variabeln `PureJSContentFragmentSelectors` används för att återge väljaren för innehållsfragment i webbläsaren.
* Innehållsfragmentväljaren återges i behållarelementet `<div>`. I exemplet används en dialogruta för att visa väljaren för innehållsfragment.

**Exempel`ìndex.html`**

```html {line-numbers="true"}
<!doctype html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <link rel="icon" type="image/svg+xml" href="/vite.svg" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <title>testing-cf-mfe-integration-with-3rd-party-app</title>
        <script
            id="content-fragments-selector"
            src="https://experience.adobe.com/solutions/CQ-sites-content-fragment-selector/static-assets/resources/content-fragment-selector.js"
        ></script>
        <script>
            const imsProps = {
                imsClientId: '<IMS_CLIENT_ID>',
                imsScope:
                    'additional_info.projectedProductContext, AdobeID, openid, read_organizations',
                redirectUrl: window.location.href,
                onImsServiceInitialized: (service) => {
                    // invoked when the ims service is initialized and is ready
                    console.log('onImsServiceInitialized', service);
                },
                onAccessTokenReceived: (token) => {
                    console.log('onAccessTokenReceived', token);
                },
                onAccessTokenExpired: () => {
                    console.log('onAccessTokenError');
                    // re-trigger sign-in flow
                },
                onErrorReceived: (type, msg) => {
                    console.log('onErrorReceived', type, msg);
                },
            };

            function load() {
                const registeredTokenService =
                    PureJSContentFragmentSelectors.registerContentFragmentSelectorAuthService(
                        imsProps
                    );
                imsInstance = registeredTokenService;
            }

            // initialize the IMS flow before attempting to render the content fragment selector
            load();

            // function that will render the content fragment selector
            function renderContentFragmentSelectorWithAuthFlow() {
                const contentFragmentSelectorDialog = document.getElementById(
                    'content-fragment-selector-dialog'
                );

                const contentFragmentSelectorProps = {
                    inventoryViewToggleEnabled: true,
                    isOpen: true,
                    noWrap: false,
                    orgId: 'YOUR_ORG_ID@AdobeOrg',
                    // repoId: "author-p12345-e67890.adobeaemcloud.com", // if wanted to restrict to a specific repo
                    runningInUnifiedShell: false,
                    onDismiss: () => contentFragmentSelectorDialog.close(),
                    onSubmit: ({ contentFragments }) => {
                        const selectedContentFragment = contentFragments[0];
                        alert(selectedContentFragment.path);
                    },
                };
                // container element on which you want to render the ContentFragmentSelector component
                const container = document.getElementById('content-fragment-selector');

                /// Use the PureJSContentFragmentSelectors in globals to render the ContentFragmentSelector component
                PureJSContentFragmentSelectors.renderContentFragmentSelectorWithAuthFlow(
                    container,
                    contentFragmentSelectorProps,
                    () => contentFragmentSelectorDialog.showModal()
                );
            }
        </script>
    </head>
    <body>
        <div>
            <button onclick="renderContentFragmentSelectorWithAuthFlow()">
                Content Fragment Selector - Select Content Fragments with Ims Flow
            </button>
        </div>
        <dialog id="content-fragment-selector-dialog">
            <div
                id="content-fragment-selector"
                style="height: calc(100vh - 80px); width: calc(100vw - 60px); margin: -20px"
            ></div>
        </dialog>
    </body>
</html>
```

## Det går inte att komma åt leveransdatabasen {#unable-to-access-delivery-repository}

Om du har integrerat väljaren för innehållsfragment med hjälp av arbetsflödet Logga in men fortfarande inte kan komma åt leveransdatabasen, kontrollerar du att cookies i webbläsaren har rensats.

Annars kanske du kommer att se felet `invalid_credentials All session cookies are empty` i konsolen.
